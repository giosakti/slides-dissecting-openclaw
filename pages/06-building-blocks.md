---
layout: center
---

<div class="text-center">
  <p class="text-2xl opacity-50">This field is</p>
  <h1 class="!text-5xl mt-2"><span class="accent">Early</span></h1>
  <p class="text-xl mt-4 opacity-60">Powerful, but far from solved</p>
</div>

---

# The Double-Edged Sword

<div class="mt-4">
  <p class="text-xl">To be <strong>truly useful</strong>, you integrate it with everything:</p>
</div>

<div class="flex gap-3 mt-3 flex-wrap">
  <span class="px-3 py-1.5 bg-teal-50 border border-teal-200 rounded-full text-sm font-bold">Calendar</span>
  <span class="px-3 py-1.5 bg-teal-50 border border-teal-200 rounded-full text-sm font-bold">Email</span>
  <span class="px-3 py-1.5 bg-teal-50 border border-teal-200 rounded-full text-sm font-bold">Google Sheets</span>
  <span class="px-3 py-1.5 bg-teal-50 border border-teal-200 rounded-full text-sm font-bold">Slack</span>
  <span class="px-3 py-1.5 bg-teal-50 border border-teal-200 rounded-full text-sm font-bold">WhatsApp</span>
  <span class="px-3 py-1.5 bg-teal-50 border border-teal-200 rounded-full text-sm font-bold">Banking</span>
  <span class="px-3 py-1.5 bg-teal-50 border border-teal-200 rounded-full text-sm font-bold">Files</span>
  <span class="px-3 py-1.5 bg-teal-50 border border-teal-200 rounded-full text-sm opacity-50">...</span>
</div>

<div class="grid grid-cols-2 gap-6 mt-5">
  <div>
    <p class="text-lg font-bold">Every integration is an <span class="text-red-500">attack surface</span></p>
    <div class="mt-3 grid grid-cols-1 gap-2">
      <div class="p-2.5 bg-gray-900 text-white rounded-lg">
        <p class="text-sm"><strong class="opacity-50 uppercase tracking-wider">Data Exfiltration</strong> — agent leaks sensitive data</p>
      </div>
      <div class="p-2.5 bg-gray-900 text-white rounded-lg">
        <p class="text-sm"><strong class="opacity-50 uppercase tracking-wider">Prompt Injection</strong> — malicious content hijacks behavior</p>
      </div>
      <div class="p-2.5 bg-gray-900 text-white rounded-lg">
        <p class="text-sm"><strong class="opacity-50 uppercase tracking-wider">Context Poisoning</strong> — tool outputs alter decisions</p>
      </div>
    </div>
  </div>
  <div>
    <p class="text-lg font-bold">Every abstraction <span class="text-red-500">leaks</span></p>
    <div class="mt-3 grid grid-cols-1 gap-2">
      <div class="p-2.5 bg-gray-900 text-white rounded-lg">
        <p class="text-sm"><strong class="opacity-50 uppercase tracking-wider">Channel Quirks</strong> — message limits, media handling, auth flows differ</p>
      </div>
      <div class="p-2.5 bg-gray-900 text-white rounded-lg">
        <p class="text-sm"><strong class="opacity-50 uppercase tracking-wider">LLM Differences</strong> — swap providers, behavior changes</p>
      </div>
      <div class="p-2.5 bg-gray-900 text-white rounded-lg">
        <p class="text-sm"><strong class="opacity-50 uppercase tracking-wider">Hidden Complexity</strong> — 20+ channels, 5+ extension systems under the hood</p>
      </div>
    </div>
  </div>
</div>

<p class="mt-4 text-lg"><span class="accent font-bold">More power = more useful = more you need to understand</span></p>

---
layout: center
---

<div class="text-center">
  <p class="text-2xl opacity-50">As technical people</p>
  <h1 class="!text-5xl mt-4">Go <span class="accent">Deep</span></h1>
  <p class="text-xl mt-6 opacity-70">Don't blindly trust — understand the runtime</p>
  <div class="mt-8 text-left inline-block text-lg">
    <p>What can the agent <strong>access</strong>?</p>
    <p>How does it make <strong>decisions</strong>?</p>
    <p>Where are the <strong>guardrails</strong>?</p>
    <p>Where do the abstractions <strong>break</strong>?</p>
  </div>
</div>

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
    <p class="mt-4 text-sm opacity-40">Complexity grows fast — plugins, hooks, skills, subagents, MCP</p>
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
