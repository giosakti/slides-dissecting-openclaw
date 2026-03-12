---
layout: section
---

<div>
  <h1>Introducing <span class="accent">Duragent</span></h1>
  <p class="text-2xl mt-4 opacity-60">github.com/giosakti/duragent</p>
</div>

---

# The 6 Building Blocks, <span class="accent">Distilled</span>

<div class="grid grid-cols-2 gap-8 mt-4">
  <div>
    <div class="flex flex-col max-w-md rounded-lg overflow-hidden border border-gray-200">
      <div class="px-4 py-2 bg-teal-50 border-b border-teal-200 flex justify-between items-center">
        <p class="font-bold text-sm accent">1. Agentic loop</p>
        <p class="text-xs opacity-40">prompt → LLM → tools → repeat</p>
      </div>
      <div class="px-4 py-2 bg-gray-50 border-b border-gray-200 flex justify-between items-center">
        <p class="font-bold text-sm accent">2. Tool system</p>
        <p class="text-xs opacity-40">8 built-in: bash, web, memory, schedule, ...</p>
      </div>
      <div class="px-4 py-2 bg-gray-50 border-b border-gray-200 flex justify-between items-center">
        <p class="font-bold text-sm accent">3. Durable sessions</p>
        <p class="text-xs opacity-40">JSONL events + snapshots, attach/detach</p>
      </div>
      <div class="px-4 py-2 bg-gray-50 border-b border-gray-200 flex justify-between items-center">
        <p class="font-bold text-sm accent">4. Gateways</p>
        <p class="text-xs opacity-40">CLI, HTTP, SSE, Telegram, Discord</p>
      </div>
      <div class="px-4 py-2 bg-gray-50 border-b border-gray-200 flex justify-between items-center">
        <p class="font-bold text-sm accent">5. LLM abstraction</p>
        <p class="text-xs opacity-40">Anthropic, OpenAI, OpenRouter, Ollama</p>
      </div>
      <div class="px-4 py-2 bg-gray-50 flex justify-between items-center">
        <p class="font-bold text-sm accent">6. Config as data</p>
        <p class="text-xs opacity-40">Agents defined in YAML + Markdown</p>
      </div>
    </div>
  </div>
  <div class="flex flex-col justify-center">
    <p class="text-lg font-bold">Single Rust binary, ~10MB</p>
    <p class="mt-1 opacity-50">No Python, no Node, no containers</p>
    <p class="mt-5 text-lg">Sessions survive crashes</p>
    <p class="mt-1 opacity-50">Attach / detach like <strong>tmux</strong> for AI agents</p>
    <p class="mt-5 text-sm opacity-40">v0.5.4 — sandbox &amp; remote storage planned for v0.6.0</p>
  </div>
</div>

---

# What the LLM <span class="accent">Actually Sees</span>

<div class="grid grid-cols-2 gap-8 mt-4">
  <div class="flex flex-col gap-2">
    <div class="rounded-lg overflow-hidden border border-gray-200">
      <div class="px-3 py-1 bg-gray-200 text-xs font-bold uppercase tracking-wider opacity-60">system</div>
      <div class="px-3 py-1 bg-red-50 border-t border-red-200 text-sm"><strong>Prime Directives</strong> <span class="opacity-40">— safety, always on</span></div>
      <div class="px-3 py-1 bg-teal-50 border-t border-teal-200 text-sm"><strong class="accent">Soul</strong> <span class="opacity-40">— who the agent <em>is</em></span></div>
      <div class="px-3 py-1 bg-teal-50 border-t border-teal-100 text-sm"><strong class="accent">System Prompt</strong> <span class="opacity-40">— what it <em>does</em></span></div>
      <div class="px-3 py-1 bg-gray-50 border-t border-gray-200 text-sm"><strong>Instructions</strong> · <strong>Directives</strong> · <strong>Skills</strong></div>
    </div>
    <div class="grid grid-cols-2 gap-2">
      <div class="rounded-lg overflow-hidden border border-gray-200">
        <div class="px-3 py-1 bg-gray-200 text-xs font-bold uppercase tracking-wider opacity-60">tools</div>
        <div class="px-3 py-1 bg-gray-100 border-t border-gray-200 text-sm">Tool definitions</div>
      </div>
      <div class="rounded-lg overflow-hidden border border-gray-200">
        <div class="px-3 py-1 bg-gray-200 text-xs font-bold uppercase tracking-wider opacity-60">messages</div>
        <div class="px-3 py-1 bg-gray-100 border-t border-gray-200 text-sm">History → <strong>user msg last</strong></div>
      </div>
    </div>
  </div>
  <div class="flex flex-col justify-center">
    <p class="text-lg font-bold">Each block is a Markdown file</p>
    <p class="mt-1 opacity-50">You can read and edit what the LLM sees</p>
    <p class="mt-5 text-lg font-bold">Token budgeting is automatic</p>
    <p class="mt-1 opacity-50">Old results masked, oldest iterations dropped, history truncated</p>
    <p class="mt-5 text-lg font-bold accent">No magic</p>
    <p class="mt-1 opacity-50">What you write is what the LLM sees</p>
  </div>
</div>

---

# Agents as Files, <span class="accent">Modular</span> by Design

<div class="grid grid-cols-2 gap-8 mt-4">
  <div>
    <div class="text-sm opacity-50 mb-2">agent.yaml</div>

```yaml
apiVersion: duragent/v1alpha1
kind: Agent
metadata:
  name: my-assistant
spec:
  model:
    provider: openrouter
    name: anthropic/claude-sonnet-4
  soul: ./SOUL.md
  system_prompt: ./SYSTEM_PROMPT.md
  tools:
    - type: builtin
      name: bash
    - type: builtin
      name: web
    - type: builtin
      name: memory
```

  </div>
  <div class="flex flex-col justify-center">
    <p class="text-lg"><strong>Swap any component:</strong></p>
    <div class="mt-4 space-y-2">
      <p><span class="accent font-bold">Gateways</span> <span class="opacity-50">— CLI, HTTP, SSE, Telegram, Discord</span></p>
      <p><span class="accent font-bold">LLM</span> <span class="opacity-50">— OpenRouter, OpenAI, Anthropic, Ollama</span></p>
      <p><span class="accent font-bold">Tools</span> <span class="opacity-50">— built-in, CLI scripts, or custom</span></p>
      <p><span class="accent font-bold">Memory</span> <span class="opacity-50">— recall, remember, reflect, world knowledge</span></p>
    </div>
    <p class="mt-6 opacity-50 text-sm">Agents are portable — just copy the directory</p>
  </div>
</div>
