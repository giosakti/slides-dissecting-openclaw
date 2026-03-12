---
layout: section
---

# The <span class="accent">Self-Evolving</span> Agent

How OpenClaw rewrites itself at runtime

---

# Software That <span class="accent">Writes Itself</span>

<div class="grid grid-cols-2 gap-12 mt-6">
  <div>
    <p class="text-sm font-bold uppercase tracking-wider opacity-40">Traditional</p>
    <div class="mt-4 space-y-3">
      <p><span class="dim">1.</span> Developer writes plugin</p>
      <p><span class="dim">2.</span> Code review &amp; merge</p>
      <p><span class="dim">3.</span> Deploy new version</p>
      <p><span class="dim">4.</span> User restarts agent</p>
    </div>
    <p class="mt-4 text-2xl font-bold opacity-40">Days</p>
  </div>
  <div>
    <p class="text-sm font-bold uppercase tracking-wider accent">Self-evolving</p>
    <div class="mt-4 space-y-3">
      <p><span class="dim">1.</span> Agent identifies need</p>
      <p><span class="dim">2.</span> Agent writes plugin</p>
      <p><span class="dim">3.</span> Runtime loads it</p>
    </div>
    <p class="mt-4 text-2xl font-bold accent">Seconds</p>
  </div>
</div>

---

# Three Layers of <span class="accent">Self-Evolution</span>

<div class="flex flex-col max-w-2xl mx-auto rounded-lg overflow-hidden border border-gray-200 mt-6">
  <div class="px-4 py-2.5 bg-teal-50 border-b border-teal-200 flex justify-between items-center">
    <p class="font-bold accent">Layer 3: ClawHub Marketplace</p>
    <p class="text-xs opacity-40">Community skills &amp; plugins — search + install at runtime</p>
  </div>
  <div class="px-4 py-2.5 bg-teal-50/60 border-b border-teal-200 flex justify-between items-center">
    <p class="font-bold accent">Layer 2: Skills System</p>
    <p class="text-xs opacity-40">Markdown behaviors — discovery via system prompt</p>
  </div>
  <div class="px-4 py-2.5 bg-teal-50/30 flex justify-between items-center">
    <p class="font-bold accent">Layer 1: Plugin System</p>
    <p class="text-xs opacity-40">Dynamic loading — tools, hooks, routes — 24 lifecycle events</p>
  </div>
</div>

---

# Layer 1: <span class="accent">Plugin System</span>

<div class="grid grid-cols-2 gap-8 mt-4">
  <div>
    <div class="text-sm opacity-50 mb-2">OpenClawPluginApi interface</div>

```typescript
interface OpenClawPluginApi {
  registerTool(name, handler)
  registerHook(event, callback)
  registerRoute(path, handler)
  registerCommand(name, handler)
  registerMiddleware(fn)
  registerProvider(type, impl)
  registerEventHandler(event, fn)
}
```

  </div>
  <div class="flex flex-col justify-center">
    <p class="text-lg">7 extension points in one API</p>
    <p class="mt-4 opacity-70">The agent has <strong>bash + write</strong></p>
    <p class="mt-2 opacity-70">So it can author a plugin and load it at runtime</p>
    <p class="mt-4 text-2xl font-bold accent">~10 lines to extend itself</p>
  </div>
</div>

---

# Plugins Hook Into <span class="accent">Everything</span>

<div class="grid grid-cols-4 gap-3 mt-4">
  <div class="p-3 bg-gray-100 rounded-lg text-center">
    <p class="text-sm font-bold font-mono">before_tool_call</p>
  </div>
  <div class="p-3 bg-gray-100 rounded-lg text-center">
    <p class="text-sm font-bold font-mono">after_tool_call</p>
  </div>
  <div class="p-3 bg-gray-100 rounded-lg text-center">
    <p class="text-sm font-bold font-mono">llm_output</p>
  </div>
  <div class="p-3 bg-gray-100 rounded-lg text-center">
    <p class="text-sm font-bold font-mono">session_start</p>
  </div>
  <div class="p-3 bg-gray-100 rounded-lg text-center">
    <p class="text-sm font-bold font-mono">message_received</p>
  </div>
  <div class="p-3 bg-gray-100 rounded-lg text-center">
    <p class="text-sm font-bold font-mono">plugin_loaded</p>
  </div>
  <div class="p-3 bg-gray-100 rounded-lg text-center">
    <p class="text-sm font-bold font-mono">error</p>
  </div>
  <div class="p-3 bg-teal-100 rounded-lg text-center border border-teal-300">
    <p class="text-sm font-bold font-mono">+16 more</p>
  </div>
</div>

<div class="mt-4 text-sm opacity-50">Jiti loader — supports .ts / .js with no build step</div>

```typescript
export default {
  id: "request-logger",
  register(api) {
    api.registerHook("before_tool_call", async (ctx) => {
      console.log(`[${ctx.tool}] ${JSON.stringify(ctx.params)}`)
    })
  }
}
```

---

# Layer 2: <span class="accent">Skills</span> — Behavior as Markdown

<div class="grid grid-cols-2 gap-8 mt-4">
  <div>
    <div class="text-sm opacity-50 mb-2">skills/deploy/SKILL.md</div>

```markdown
---
name: kubernetes-deploy
description: Deploy services to k8s
requirements:
  tools: [kubectl, helm]
  permissions: [bash]
---

## Instructions
1. Check current cluster context
2. Validate manifests with --dry-run
3. Apply with kubectl or helm upgrade
4. Verify pod health before confirming
```

  </div>
  <div class="flex flex-col justify-center">
    <p class="text-lg font-bold">How discovery works:</p>
    <div class="mt-4 space-y-2">
      <p><span class="dim">1.</span> System prompt tells agent to scan <code>skills/</code></p>
      <p><span class="dim">2.</span> Agent reads matching <code>SKILL.md</code></p>
      <p><span class="dim">3.</span> Agent follows instructions</p>
    </div>
    <p class="mt-6 text-lg accent font-bold">Agent can write new SKILL.md files</p>
    <p class="opacity-50">Behaviors are just files — the agent can author them</p>
  </div>
</div>

---

# Layer 3: <span class="accent">ClawHub</span> — Community Marketplace

<div class="flex flex-col max-w-2xl mx-auto rounded-lg overflow-hidden border border-gray-200 mt-6">
  <div class="px-4 py-2.5 bg-gray-50 border-b border-gray-200">
    <p><span class="opacity-50">User:</span> <em>"Help me deploy this to Kubernetes"</em></p>
  </div>
  <div class="px-4 py-2.5 bg-teal-50 border-b border-teal-200">
    <p><span class="accent font-bold">Agent:</span> I don't have k8s skills. Let me search...</p>
    <p class="font-mono text-sm opacity-70">→ clawhub search "kubernetes deploy"</p>
  </div>
  <div class="px-4 py-2.5 bg-teal-50 border-b border-teal-200">
    <p><span class="accent font-bold">Agent:</span> Found a match. Installing...</p>
    <p class="font-mono text-sm opacity-70">→ clawhub install kubernetes-deploy</p>
  </div>
  <div class="px-4 py-2.5 bg-green-50">
    <p><span class="accent font-bold">Agent:</span> Done! Deploying your service now.</p>
  </div>
</div>

<p class="mt-4 text-center text-lg">Perceive gap → search → install → use — <strong>in one conversation</strong></p>

---

# The Complete <span class="accent">Self-Extension</span> Loop

<div class="flex flex-col items-center mt-6">
  <div class="p-4 bg-red-50 rounded-lg border border-red-200 w-full text-center">
    <p class="text-lg font-bold">Agent can't do the task</p>
  </div>

  <p class="text-2xl my-3 opacity-30">↓</p>

  <div class="grid grid-cols-3 gap-4 w-full">
    <div class="p-3 bg-teal-50 rounded-lg border border-teal-200 text-center">
      <p class="font-bold accent">Write plugin</p>
      <p class="text-sm opacity-60">New tool or hook</p>
    </div>
    <div class="p-3 bg-teal-50 rounded-lg border border-teal-200 text-center">
      <p class="font-bold accent">Create skill</p>
      <p class="text-sm opacity-60">New behavior</p>
    </div>
    <div class="p-3 bg-teal-50 rounded-lg border border-teal-200 text-center">
      <p class="font-bold accent">Install from ClawHub</p>
      <p class="text-sm opacity-60">Community package</p>
    </div>
  </div>

  <p class="text-2xl my-3 opacity-30">↓</p>

  <div class="p-4 bg-green-50 rounded-lg border border-green-200 w-full text-center">
    <p class="text-lg font-bold">Capability loaded → task completed</p>
    <p class="text-sm opacity-60 mt-1">Capability persists for future sessions</p>
  </div>
</div>

---

# The Agent <span class="accent">Upgrades Itself</span>

<div class="grid grid-cols-2 gap-8 mt-4">
  <div>
    <div class="text-sm opacity-50 mb-2">Two ways to self-upgrade</div>

```bash
# Manual — one command
openclaw update

# Automatic — auto-updater skill
# Sets up a daily cron job that runs:
openclaw update
clawhub update --all
```

  </div>
  <div class="flex flex-col justify-center">
    <p class="text-lg font-bold">What happens under the hood</p>
    <div class="mt-4 space-y-2">
      <p><span class="accent font-bold">Pull</span> <span class="opacity-50">— fetch latest version</span></p>
      <p><span class="accent font-bold">Build</span> <span class="opacity-50">— install deps, rebuild</span></p>
      <p><span class="accent font-bold">Doctor</span> <span class="opacity-50">— validate the installation</span></p>
      <p><span class="accent font-bold">Restart</span> <span class="opacity-50">— gateway comes back up</span></p>
    </div>
    <p class="mt-4 opacity-50">Config backup + auto-rollback if something breaks</p>
  </div>
</div>

---
layout: center
---

<div class="text-center">
  <h1 class="!text-4xl">An Agent That <span class="accent">Grows</span></h1>
  <div class="mt-8 space-y-4 text-xl">
    <p><strong>Plugins</strong> extend what it <span class="accent">can do</span></p>
    <p><strong>Skills</strong> extend how it <span class="accent">behaves</span></p>
    <p><strong>ClawHub</strong> extends from <span class="accent">community</span></p>
    <p><strong>Self-upgrade</strong> extends <span class="accent">itself</span></p>
  </div>
  <p class="mt-8 text-lg opacity-50">The runtime doesn't need to anticipate every use case</p>
</div>
