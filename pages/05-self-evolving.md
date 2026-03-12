---
layout: section
---

# The <span class="accent">Self-Evolving</span> Agent

---

# Agent Writes Its Own Plugins

<div class="grid grid-cols-2 gap-8 mt-4">
  <div>
    <div class="text-sm opacity-50 mb-2">A complete OpenClaw plugin</div>

```typescript
export default {
  id: "my-plugin",
  name: "My Plugin",
  description: "Does something useful",
  register(api) {
    api.registerTool("my_tool", {
      description: "A custom tool",
      execute: async (params) => {
        /* ... */
      }
    })
  }
}
```

  </div>
  <div class="flex flex-col justify-center">
    <p class="text-xl">The agent has <strong>bash + write</strong></p>
    <p class="mt-4 opacity-70">So it can create this file, install deps, and load it</p>
    <p class="mt-4 text-2xl font-bold accent">~10 lines to extend itself</p>
  </div>
</div>

---

# Skills and ClawHub

<div class="grid grid-cols-2 gap-12 mt-8">
  <div>
    <p class="text-2xl font-bold">Skills</p>
    <p class="mt-2 opacity-70">Reusable behaviors<br/>Prompt templates + tools</p>
  </div>
  <div>
    <p class="text-2xl font-bold">ClawHub</p>
    <p class="mt-2 opacity-70">Community marketplace<br/>Agent can self-install</p>
  </div>
</div>

<p class="mt-10 text-lg">Core stays lean. Capabilities grow through <strong>community</strong>.</p>

---

# Onboarding as <span class="accent">Product</span>

<div class="mt-8 text-center">
  <code class="text-2xl !bg-gray-100 !p-4 !rounded-lg">openclaw onboard --install-daemon</code>
</div>

<div class="grid grid-cols-2 gap-8 mt-10">
  <div>
    <p class="font-bold">One command</p>
    <p class="opacity-60">Wizard guides everything</p>
  </div>
  <div>
    <p class="font-bold">Full setup</p>
    <p class="opacity-60">Gateway, workspace, channels, skills</p>
  </div>
  <div>
    <p class="font-bold">Cross-platform</p>
    <p class="opacity-60">macOS, Linux, Windows (WSL2)</p>
  </div>
  <div>
    <p class="font-bold">Minutes</p>
    <p class="opacity-60">From zero to working assistant</p>
  </div>
</div>
