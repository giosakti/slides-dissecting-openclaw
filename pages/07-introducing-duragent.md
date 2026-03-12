---
layout: section
---

<div>
  <h1>Introducing <span class="accent">Duragent</span></h1>
  <p class="text-2xl mt-4 opacity-60">Assemble your own agent runtime</p>
</div>

---

# One Binary, Zero Dependencies

<div class="grid grid-cols-3 gap-8 mt-10 text-center">
  <div>
    <p class="big-number">~10<span class="text-xl">MB</span></p>
    <p class="label">Rust executable</p>
  </div>
  <div>
    <p class="big-number">0</p>
    <p class="label">Dependencies</p>
  </div>
  <div>
    <p class="big-number">ms</p>
    <p class="label">Startup time</p>
  </div>
</div>

<p class="mt-8 text-center text-lg opacity-60">No Python, no Node, no containers. Install and run.</p>

---

# Durable Sessions

<div class="grid grid-cols-2 gap-12 mt-8">
  <div>
    <p class="text-3xl font-bold">Attach / detach</p>
    <p class="text-lg mt-2 opacity-60">Like <strong>tmux</strong> for AI agents</p>
    <p class="mt-4 opacity-50">Crash, restart, reconnect — no conversation lost</p>
  </div>
  <div>
    <p class="text-3xl font-bold">Transparent</p>
    <p class="text-lg mt-2 opacity-60">Append-only event log + state snapshots</p>
    <p class="mt-4 opacity-50">Just files you can read. No hidden databases.</p>
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
  system_prompt: ./SYSTEM_PROMPT.md
```

  </div>
  <div class="flex flex-col justify-center">
    <p class="text-lg"><strong>Swap any component:</strong></p>
    <div class="mt-4 space-y-2">
      <p><span class="accent font-bold">Gateways</span> <span class="opacity-50">— CLI, HTTP, SSE, Telegram</span></p>
      <p><span class="accent font-bold">LLM</span> <span class="opacity-50">— OpenRouter, OpenAI, Anthropic, Ollama</span></p>
      <p><span class="accent font-bold">Sandbox</span> <span class="opacity-50">— Trust, bubblewrap, Docker</span></p>
      <p><span class="accent font-bold">Storage</span> <span class="opacity-50">— Filesystem, Postgres, S3</span></p>
    </div>
  </div>
</div>
