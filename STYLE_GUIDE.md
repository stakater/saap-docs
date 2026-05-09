# KubeStack+ Documentation Style Guide

This guide defines the voice, structure, and language standards for all KubeStack+ documentation.
When editing existing pages, apply these rules. When writing new pages, follow them from the start.

---

## Voice and tone

Write in **active voice, second person**. Address the reader directly as "you".

| Avoid | Use instead |
|---|---|
| "It is recommended that users configure..." | "Configure..." |
| "The cluster can be hibernated by..." | "Hibernate the cluster by..." |
| "Administrators should be aware that..." | "Note that..." |
| "This ensures a smooth experience" | _(delete — meaningless)_ |

**Treat readers as competent professionals.** Do not explain that things are "easy" or "simple" — show it through clear instructions.

---

## Page types and structure

Every page has exactly one purpose. State it in the **first sentence**, not buried in paragraph three.

### Overview (section landing pages)

Purpose: help readers navigate to what they need.

Structure:
1. **One to three sentences** — what this section covers and who it's for. No more.
2. **Sections** — each with a link and a single-sentence description of what the reader will accomplish or learn.

Rules:
- No "welcome to", no "embark on a journey", no "comprehensive guide to mastering"
- Link descriptions say what the reader **does** or **learns**, not what the page "explores" or "covers"
- Do not describe a link if the title already makes it obvious

### How-to guides

Purpose: give step-by-step instructions for a specific task.

Structure:
1. First sentence: "This guide explains how to [specific outcome]."
2. Prerequisites (if any) — brief list
3. Numbered steps in imperative mood

Rules:
- Each step does one thing
- Steps start with a verb: "Run", "Click", "Enter", "Copy"
- No narrative between steps unless it is critical context the reader cannot infer

### Explanation (concept pages)

Purpose: explain what something is and why it matters.

Structure:
1. First sentence: define the thing
2. Explain why it is relevant in this context
3. Use diagrams or examples where they clarify

Rules:
- No marketing framing ("powerful", "seamless")
- Explain the WHY, not just the WHAT

### Tutorials

Purpose: walk a reader through a complete task from start to finish.

Structure:
1. Prerequisites — what the reader needs before starting
2. Numbered steps — each moves the reader forward
3. Final state — "You now have X configured."

### Reference

Purpose: let readers look up specific values, options, or definitions.

Structure: tables and lists preferred over prose. Define terms precisely.

---

## Banned phrases

Delete these on sight — they add no information:

**Filler openers:**
- "Welcome to..."
- "This section equips you with the knowledge, tools, and techniques..."
- "Whether you're just getting started or seeking to refine your skills..."
- "We invite you to embark on an enlightening journey..."
- "your comprehensive guide to mastering..."
- "Happy progressing!"
- "In this section, we will..."
- "As the name suggests..."
- "Feel free to..."
- "It is important to note that..."

**Empty adjectives — remove or replace with a specific fact:**
- seamless, robust, powerful, world-class, comprehensive, cutting-edge, innovative, effortlessly, streamlined, advanced, intuitive, rich, insightful

**Redundant qualifiers:**
- very, really, quite, essentially, basically, simply

---

## Link descriptions in overview pages

Each link description must say what the reader will **do** or **learn**, concretely.

| Avoid | Use instead |
|---|---|
| "Explore the process of promoting your application across different environments. Facilitate seamless deployments by versioning and sharing your charts with your team." | "Promote an application between environments using GitOps." |
| "Lay the foundation of your development journey with comprehensive training." | "Covers the core Kubernetes and platform concepts required before starting." |
| "Dive into creating a seamless local development environment." | "Set up a local development workflow with Tilt." |
| "Uncover the inner workings of software development processes." | "Explains the difference between the inner loop (local iteration) and outer loop (CI/CD)." |

One sentence per link. No more.

---

## Instructions

Always use **imperative mood** for steps:

| Avoid | Use instead |
|---|---|
| "You will need to click..." | "Click..." |
| "You can then run..." | "Run..." |
| "The next step is to update..." | "Update..." |
| "You should now see..." | "Verify that you see..." |

---

## Headings

- **Sentence case** for all headings — capitalize first word and proper nouns only.
- **Action-oriented** for how-to pages: "Configure X" not "Configuration of X".
- Do not use "Overview" as a sub-heading inside a page that is already an overview.

---

## Terminology

| Use | Avoid |
|---|---|
| `{{ product_name }}` | SAAP, Stakater App Agility Platform |
| Administrator | admin, cluster admin (unless referring to the specific ClusterAdmin role) |
| DevOps Engineer | Delivery Engineer |
| identity provider | IdP (spell out on first use) |

Kubernetes resource names appear in code spans: `PersistentVolumeClaim`, `ClusterRole`, `ConfigMap`.

---

## Numbers and lists

- Numbered lists for sequential steps.
- Bullet lists for non-sequential items.
- Never use a bullet list with a single item — write a sentence instead.
- Do not mix list styles within a section.

---

## What to cut

When reviewing a page, cut anything that:

1. Repeats the heading in prose form
2. Tells the reader what they are about to read without actually saying it
3. Congratulates the reader for reading
4. Could apply equally to any documentation site (generic boilerplate)
5. Uses more than one sentence to say something that fits in one
