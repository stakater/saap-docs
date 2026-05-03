# Claude Guidelines — KubeStack+ Docs

These rules apply whenever Claude writes or edits documentation in this repository. They complement `STYLE_GUIDE.md`, which governs voice, tone, and language. These rules govern structure, flow, and how information is sequenced.

---

## Documentation writing principles

### 1. State the purpose first

Every page and every section must have a single, clear purpose. State it in the first sentence. If you cannot state the purpose in one sentence, the scope is too broad.

- **Page opener:** What will the reader have or know by the end?
- **Section opener:** What does this section do, and why does the reader need it right now?

Never start with context, history, or background before stating the purpose.

### 2. Earn every section

Before writing a section, ask: *"Why does the reader need this right now?"* If you cannot answer concretely, cut the section or merge it into the one that does need it.

A section that could be moved anywhere without breaking the page is an orphan. Rewrite it to connect explicitly to what came before and what comes next.

### 3. Guide, do not dump

Present only what the reader needs at this point in their journey. Information needed later belongs later. Do not write a section just because the information exists — write it because the reader needs it here, now.

### 4. Transitions are mandatory

End every major section and every page with a sentence pointing to the next logical action. The reader should never have to decide what to do next on their own.

Examples:
- "Once you have completed X, continue to [Y](link.md)."
- "With the repository configured, the next step is [setting up user access](link.md)."

A page that ends without a next step is incomplete.

### 5. Short paragraphs, one idea each

Maximum three sentences per paragraph. If a paragraph runs to four or more sentences, split it. Each paragraph makes one point and moves on.

### 6. Outcome before process

Start with what the reader achieves, then explain how to achieve it. Not the reverse.

- **Wrong:** "Keycloak manages authentication. It supports OIDC and SAML. You can connect it to your identity provider. This allows users to log in with existing credentials."
- **Right:** "This page explains how to connect your existing identity provider to Keycloak so your users can log in without a separate account."

### 7. End with a clear next step

Pages end with an explicit pointer to what comes next — not a trailing paragraph of context. Use a short sentence or a "Next steps" section. Every page is a waypoint, not a destination.

---

## Checklist before finishing a documentation task

Before marking documentation work as done, verify:

- [ ] Every page opener states what the reader will achieve
- [ ] Every section opener explains what it does and why it matters at this point
- [ ] No section feels like it could be lifted out and placed anywhere else on the page
- [ ] Every page ends with a clear next step or pointer
- [ ] No paragraph exceeds three sentences
- [ ] Information appears only where the reader needs it — not "just in case"
- [ ] The page can be read top to bottom without the reader asking "why am I reading this?"
