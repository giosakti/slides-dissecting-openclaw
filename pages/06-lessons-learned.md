---
layout: section
---

# Lessons <span class="accent">Learned</span>

---

# Complexity Grows Fast

<div class="mt-8">
  <div class="grid grid-cols-3 gap-6">
    <div class="text-center">
      <p class="big-number !text-3xl">20+</p>
      <p class="label">messaging channels</p>
    </div>
    <div class="text-center">
      <p class="big-number !text-3xl">100s</p>
      <p class="label">source files</p>
    </div>
    <div class="text-center">
      <p class="big-number !text-3xl">5+</p>
      <p class="label">extension systems</p>
    </div>
  </div>
</div>

<p class="mt-8 text-lg">Plugins, hooks, skills, subagents, MCP</p>
<p class="opacity-50">Power vs. maintainability is a real tradeoff</p>

---

# Session Durability is <span class="text-red-500">Hard</span>

<div class="mt-8 text-lg">

- Context compaction, history limits, state repair
- Transcript repair, write locks, branching
- "Resume where you left off" is non-trivial at scale

</div>

---

# The Channel Abstraction <span class="text-red-500">Leaks</span>

<div class="mt-8 text-lg">

- Each platform has unique constraints
- Media handling, message limits, auth flows differ
- "Write once, run everywhere" requires constant patching

</div>
