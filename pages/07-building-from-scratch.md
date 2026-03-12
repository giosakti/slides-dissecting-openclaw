---
layout: center
---

<div class="text-center">
  <p class="text-2xl opacity-50">What if we</p>
  <h1 class="!text-5xl mt-2">Started <span class="accent">Fresh</span>?</h1>
  <p class="text-xl mt-4 opacity-60">What are the essential building blocks?</p>
</div>

---

# The Complexity Contrast

<div class="grid grid-cols-2 gap-12 mt-8">
  <div>
    <p class="text-sm font-bold uppercase tracking-wider opacity-40">OpenClaw today</p>
    <div class="mt-4 space-y-2">
      <p><span class="text-2xl font-bold">200+</span> <span class="opacity-50">source files</span></p>
      <p><span class="text-2xl font-bold">20+</span> <span class="opacity-50">messaging channels</span></p>
      <p><span class="text-2xl font-bold">5+</span> <span class="opacity-50">extension systems</span></p>
      <p><span class="text-2xl font-bold">100+</span> <span class="opacity-50">community skills</span></p>
    </div>
  </div>
  <div>
    <p class="text-sm font-bold uppercase tracking-wider opacity-40">Minimum viable</p>
    <div class="mt-4 space-y-2">
      <p><span class="text-2xl font-bold accent">6</span> <span class="opacity-50">building blocks</span></p>
      <p class="opacity-50 text-sm mt-4">Everything else is optional.<br/>Start here, grow as needed.</p>
    </div>
  </div>
</div>

---

# Core Elements of an Agentic Runtime

<!-- TODO: Excalidraw diagram — public/diagrams/core-elements.excalidraw -->

<div class="grid grid-cols-3 gap-4 mt-6">
  <div class="p-4 border-2 border-teal-200 rounded-lg">
    <p class="text-lg font-bold accent">1. Agentic Loop</p>
    <p class="text-sm opacity-60 mt-1">prompt → LLM → tool calls → results → repeat</p>
  </div>
  <div class="p-4 border-2 border-teal-200 rounded-lg">
    <p class="text-lg font-bold accent">2. Tool System</p>
    <p class="text-sm opacity-60 mt-1">Execute actions, return structured results</p>
  </div>
  <div class="p-4 border-2 border-teal-200 rounded-lg">
    <p class="text-lg font-bold accent">3. Session / State</p>
    <p class="text-sm opacity-60 mt-1">Persist conversations, survive restarts</p>
  </div>
  <div class="p-4 border-2 border-teal-200 rounded-lg">
    <p class="text-lg font-bold accent">4. Gateway</p>
    <p class="text-sm opacity-60 mt-1">Generic interface: CLI, HTTP, SSE, messaging</p>
  </div>
  <div class="p-4 border-2 border-teal-200 rounded-lg">
    <p class="text-lg font-bold accent">5. LLM Abstraction</p>
    <p class="text-sm opacity-60 mt-1">Swap providers without changing code</p>
  </div>
  <div class="p-4 border-2 border-teal-200 rounded-lg">
    <p class="text-lg font-bold accent">6. Config as Data</p>
    <p class="text-sm opacity-60 mt-1">Agents defined in files, not code</p>
  </div>
</div>

---

# How to Make the Agent <span class="accent">Extend Itself</span>

<div class="mt-6 text-lg">
  <p class="opacity-50">The key insight from OpenClaw:</p>
</div>

<div class="grid grid-cols-2 gap-6 mt-6">
  <div class="p-4 bg-gray-100 rounded-lg">
    <p class="font-bold">File system access</p>
    <p class="text-sm opacity-60">read + write</p>
  </div>
  <div class="p-4 bg-gray-100 rounded-lg">
    <p class="font-bold">Shell access</p>
    <p class="text-sm opacity-60">bash execution</p>
  </div>
  <div class="p-4 bg-gray-100 rounded-lg">
    <p class="font-bold">Plugin spec</p>
    <p class="text-sm opacity-60">A target the agent can write to</p>
  </div>
  <div class="p-4 bg-teal-50 rounded-lg border-2 border-teal-300">
    <p class="font-bold accent">Self-extension</p>
    <p class="text-sm opacity-60">Agent writes code that extends itself</p>
  </div>
</div>

---

# The Self-Extension Loop

<div class="flex flex-col items-center mt-8">
  <div class="text-lg space-y-4">
    <p><span class="dim">1.</span> Agent receives task it <strong>can't do</strong></p>
    <p class="ml-8"><span class="dim">2.</span> Agent <span class="accent font-bold">writes a plugin</span> for it</p>
    <p class="ml-16"><span class="dim">3.</span> Plugin is <strong>loaded into the runtime</strong></p>
    <p class="ml-24"><span class="dim">4.</span> Agent <span class="accent font-bold">can now do the task</span></p>
    <p class="ml-32"><span class="dim">5.</span> Plugin <strong>persists</strong> for future use</p>
  </div>
</div>

<p class="mt-8 text-center text-lg">The runtime doesn't need to anticipate every use case</p>
<p class="text-center opacity-50">It just needs to be extensible enough that the agent fills the gaps</p>
