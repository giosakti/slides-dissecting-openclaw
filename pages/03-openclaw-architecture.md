---
layout: section
---

# OpenClaw <span class="accent">Architecture</span>

---

# High-Level Overview

<div class="mt-4">
  <div class="flex gap-3 justify-center mb-4">
    <div class="px-3 py-1.5 bg-gray-100 rounded text-sm font-bold">WhatsApp</div>
    <div class="px-3 py-1.5 bg-gray-100 rounded text-sm font-bold">Telegram</div>
    <div class="px-3 py-1.5 bg-gray-100 rounded text-sm font-bold">Slack</div>
    <div class="px-3 py-1.5 bg-gray-100 rounded text-sm font-bold">Discord</div>
    <div class="px-3 py-1.5 bg-gray-100 rounded text-sm font-bold">iMessage</div>
    <div class="px-3 py-1.5 bg-gray-100 rounded text-sm opacity-50">+15 more</div>
  </div>
  <div class="text-center text-2xl opacity-30 mb-4">↓</div>
  <div class="p-4 border-2 border-teal-300 rounded-lg text-center mb-4 bg-teal-50">
    <p class="text-xl font-bold accent">Gateway</p>
    <p class="text-sm opacity-50">Control plane · HTTP + WS · Daemon</p>
  </div>
  <div class="text-center text-2xl opacity-30 mb-4">↓</div>
  <div class="p-4 border-2 border-gray-800 rounded-lg text-center mb-4 bg-gray-50">
    <p class="text-xl font-bold">Pi Agent Runtime</p>
    <p class="text-sm opacity-50">Embedded SDK · Agent loop · Session management</p>
  </div>
  <div class="text-center text-2xl opacity-30 mb-4">↓</div>
  <div class="flex gap-4 justify-center">
    <div class="p-3 border rounded-lg text-center flex-1 bg-gray-50">
      <p class="font-bold text-sm">LLM Providers</p>
      <p class="text-xs opacity-50">Anthropic · OpenAI · Google · Ollama</p>
    </div>
    <div class="p-3 border rounded-lg text-center flex-1 bg-gray-50">
      <p class="font-bold text-sm">Tools</p>
      <p class="text-xs opacity-50">bash · read · write · edit · plugins</p>
    </div>
    <div class="p-3 border rounded-lg text-center flex-1 bg-gray-50">
      <p class="font-bold text-sm">Storage</p>
      <p class="text-xs opacity-50">Sessions · Memory · Config</p>
    </div>
  </div>
</div>

---

# The Gateway <span class="accent">Runs Everything</span>

<div class="grid grid-cols-3 gap-6 mt-8">
  <div>
    <p class="text-2xl font-bold">Daemon</p>
    <p class="mt-2 opacity-60">launchd / systemd<br/>always running</p>
  </div>
  <div>
    <p class="text-2xl font-bold">HTTP + WS</p>
    <p class="mt-2 opacity-60">Routes messages<br/>from channels to agent</p>
  </div>
  <div>
    <p class="text-2xl font-bold">Plugins</p>
    <p class="mt-2 opacity-60">Channel extensions<br/>as separate packages</p>
  </div>
</div>

<p class="mt-10 text-lg">The <strong>product</strong> is the assistant, not the gateway</p>

---

# Multi-Channel Routing

<div class="grid grid-cols-2 gap-8 mt-8">
  <div>
    <p class="text-sm font-bold uppercase tracking-wider opacity-40">Core</p>
    <p class="text-xl mt-2">Telegram, Discord, Slack,<br/>Signal, iMessage, WhatsApp</p>
  </div>
  <div>
    <p class="text-sm font-bold uppercase tracking-wider opacity-40">Extensions</p>
    <p class="text-xl mt-2">MS Teams, Matrix, LINE,<br/>Nostr, and more</p>
  </div>
</div>

<div class="mt-8 text-lg opacity-80">

- Pairing system to link devices/users
- Per-channel identity and response formatting
- Each platform has unique constraints

</div>
