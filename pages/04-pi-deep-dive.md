---
layout: section
---

# The Brain:<br/><span class="accent">Pi</span> Agent Runtime

---

# A Radical Philosophy

<div class="grid grid-cols-2 gap-12 mt-8">
  <div>
    <p class="big-number !text-6xl">7</p>
    <p class="text-xl font-bold mt-2">Core Tools</p>
    <p class="opacity-50 mt-1">read, write, edit, bash, glob, grep, think</p>
    <p class="opacity-50">That's it. Nothing else.</p>
  </div>
  <div>
    <p class="big-number !text-4xl">&lt;1K</p>
    <p class="text-xl font-bold mt-2">Token system prompt</p>
    <p class="opacity-50 mt-1">vs 10,000+ in other agents</p>
    <p class="opacity-50">90% reduction in prompt overhead</p>
  </div>
</div>

<p class="mt-8 text-lg"><em>"What you leave out matters more than what you put in"</em></p>
<p class="opacity-40">— Mario Zechner</p>

---

# Pi's Three-Layer Architecture

<div class="mt-6 flex flex-col gap-3 max-w-2xl mx-auto">
  <div class="p-4 border-2 border-teal-300 rounded-lg bg-teal-50">
    <div class="flex justify-between items-center">
      <div>
        <p class="text-lg font-bold accent">AgentSession</p>
        <p class="text-sm opacity-50">pi-coding-agent</p>
      </div>
      <div class="text-xs opacity-40 text-right">
        Session mgmt · Compaction<br/>Extensions · Slash commands
      </div>
    </div>
  </div>
  <div class="text-center text-xl opacity-30">↕</div>
  <div class="p-4 border-2 border-gray-800 rounded-lg bg-gray-50">
    <div class="flex justify-between items-center">
      <div>
        <p class="text-lg font-bold">Agent Core</p>
        <p class="text-sm opacity-50">pi-agent-core</p>
      </div>
      <div class="text-xs opacity-40 text-right">
        Agent loop · Streaming<br/>Tool execution · Steering
      </div>
    </div>
  </div>
  <div class="text-center text-xl opacity-30">↕</div>
  <div class="p-4 border-2 border-gray-300 rounded-lg bg-gray-50">
    <div class="flex justify-between items-center">
      <div>
        <p class="text-lg font-bold">Unified LLM API</p>
        <p class="text-sm opacity-50">pi-ai</p>
      </div>
      <div class="text-xs opacity-40 text-right">
        20+ providers · Token accounting<br/>Streaming · Mid-session model swap
      </div>
    </div>
  </div>
</div>

<p class="mt-4 text-center opacity-40 text-sm">Each layer is independently usable — pick what you need</p>

---

# The Agent Loop

<div class="text-sm opacity-50 mb-2">packages/agent/src/agent-loop.ts (simplified)</div>

```typescript
while (true) {
  // Stream LLM response
  const message = await streamAssistantResponse(context, config)

  // Detect and execute tool calls
  const toolCalls = message.content.filter(c => c.type === "toolCall")
  if (toolCalls.length > 0) {
    const results = await executeToolCalls(tools, message, signal)
    for (const result of results) context.messages.push(result)
    continue  // Feed results back to LLM
  }

  // Check for follow-up messages, otherwise done
  const followUp = await config.getFollowUpMessages?.()
  if (!followUp?.length) break
}
```

---

# Tool Definition

<div class="text-sm opacity-50 mb-2">packages/coding-agent/src/core/tools/bash.ts (simplified)</div>

```typescript
const bashTool: AgentTool = {
  name: "bash",
  description: "Execute a bash command. Returns stdout and stderr.",
  parameters: bashSchema,  // TypeBox JSON Schema

  execute: async (toolCallId, { command, timeout }, signal) => {
    const { exitCode, output } = await exec(command, cwd, { signal, timeout })
    return {
      content: [{ type: "text", text: output }],  // For LLM
      details: { exitCode, command }               // For UI
    }
  }
}
```

---

# A Provocative Decision: No MCP

<div class="grid grid-cols-2 gap-8 mt-8">
  <div>
    <p class="text-2xl font-bold text-red-500">The Problem</p>
    <p class="mt-2 opacity-70">Popular MCP servers consume <strong>7-9%</strong> of your context window before any work begins</p>
  </div>
  <div>
    <p class="text-2xl font-bold accent">Pi's Alternative</p>
    <p class="mt-2 opacity-70">CLI tools with READMEs that the agent reads <strong>on-demand</strong></p>
    <p class="mt-2 opacity-50">Progressive disclosure &gt; upfront loading</p>
  </div>
</div>

<p class="mt-8 text-lg opacity-60">Not everyone agrees — but the tradeoff is worth understanding</p>

---

# Session Persistence

<div class="grid grid-cols-2 gap-8 mt-8">
  <div>
    <p class="text-2xl font-bold accent">JSONL Tree</p>
    <p class="mt-2 opacity-70">Append-only format<br/>Supports branching</p>
  </div>
  <div>
    <p class="text-2xl font-bold accent">Compaction</p>
    <p class="mt-2 opacity-70">LLM summarizes old messages<br/>when context fills</p>
  </div>
</div>

<p class="mt-10 text-xl">Sessions survive crashes and restarts</p>

---

# How OpenClaw <span class="accent">Embeds</span> Pi

<p class="text-lg mb-4">Not a subprocess — <strong>direct SDK import</strong></p>

<div class="text-sm opacity-50 mb-2">src/agents/pi-embedded-runner/run/attempt.ts (simplified)</div>

```typescript
const activeSession = await createAgentSession({ cwd, model, tools })

const subscription = subscribeEmbeddedPiSession({
  session: activeSession,
  onBlockReply: params.onBlockReply,      // Stream text to channel
  onToolResult: params.onToolResult,      // Emit tool output
  onReasoningStream: params.onReasoningStream,  // Extended thinking
})

await activeSession.prompt(userMessage)   // Agent loop runs here
```

<p class="mt-4 opacity-50">Auth failover, context overflow retry, model fallback — all handled</p>

---

# Why This Matters to <span class="accent">You</span>

<div class="mt-8 text-xl">

This is the layer that decides:

</div>

<div class="grid grid-cols-3 gap-6 mt-6">
  <div class="p-4 bg-red-50 rounded-lg border border-red-200">
    <p class="font-bold">What tools can run</p>
    <p class="text-sm opacity-60">bash on your machine?</p>
  </div>
  <div class="p-4 bg-red-50 rounded-lg border border-red-200">
    <p class="font-bold">What data is visible</p>
    <p class="text-sm opacity-60">your files? your messages?</p>
  </div>
  <div class="p-4 bg-red-50 rounded-lg border border-red-200">
    <p class="font-bold">Where replies go</p>
    <p class="text-sm opacity-60">the right Slack channel?</p>
  </div>
</div>

<p class="mt-6 text-lg opacity-60">If you don't understand this layer, you're trusting a black box with your data</p>
