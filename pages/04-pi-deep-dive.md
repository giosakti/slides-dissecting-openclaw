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

# Pi's Four-Layer Architecture

<div class="mt-4 flex flex-col max-w-2xl mx-auto rounded-lg overflow-hidden border border-gray-200">
  <div class="px-4 py-2.5 bg-gray-50 border-b border-gray-200 flex justify-between items-center">
    <p class="font-bold">Terminal UI <span class="opacity-40 font-normal text-sm ml-1">pi-tui</span></p>
    <p class="text-xs opacity-40">Markdown rendering · Editor · Autocomplete</p>
  </div>
  <div class="px-4 py-2.5 bg-teal-50 border-b border-teal-200 flex justify-between items-center">
    <p class="font-bold accent">Agent Session <span class="opacity-40 font-normal text-sm ml-1">pi-coding-agent</span></p>
    <p class="text-xs opacity-40">Sessions · Compaction · Skills · Extensions</p>
  </div>
  <div class="px-4 py-2.5 bg-gray-100 border-b border-gray-200 flex justify-between items-center">
    <p class="font-bold">Agent Core <span class="opacity-40 font-normal text-sm ml-1">pi-agent-core</span></p>
    <p class="text-xs opacity-40">Agent loop · Tool execution · Steering</p>
  </div>
  <div class="px-4 py-2.5 bg-gray-50 flex justify-between items-center">
    <p class="font-bold">Unified LLM API <span class="opacity-40 font-normal text-sm ml-1">pi-ai</span></p>
    <p class="text-xs opacity-40">2000+ models · Token accounting · Streaming</p>
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
