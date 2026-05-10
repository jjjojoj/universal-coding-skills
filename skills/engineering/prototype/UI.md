# UI Prototype

Generate **several radically different UI variations** on a single route, switchable from a floating bottom bar. The user flips between variants in the browser, picks one (or steals bits from each), then throws the rest away.

If the question is about logic/state rather than what something looks like — wrong branch. Use [LOGIC.md](LOGIC.md).

## Two sub-shapes — strongly prefer sub-shape A

### Sub-shape A — adjustment to an existing page (preferred)

The route already exists. Variants are rendered **on the same route**, gated by a `?variant=` URL search param. The existing data fetching, params, and auth all stay — only the rendering swaps.

If the prototype is for something that doesn't yet have a page but _would naturally live inside one_ — that's still sub-shape A. Mount the variants inside the host page.

### Sub-shape B — a new page (last resort)

Only use this when the thing being prototyped genuinely has no existing page to live inside. Create a **throwaway route** following whatever routing convention the project already uses. Name it obviously as a prototype.

## Process

### 1. State the question and pick N

Default to **3 variants**. More than 5 starts being noise — cap there.

Write down the plan in one line.

### 2. Generate radically different variants

Draft each variant. Variants must be **structurally different** — different layout, different information hierarchy, different primary affordance, not just different colours. If two drafts come out too similar, redo one.

### 3. Wire them together

Create a single switcher component on the route:

```tsx
// pseudo-code — adapt to the project's framework
const variant = searchParams.get('variant') ?? 'A';
return (
  <>
    {variant === 'A' && <VariantA {...data} />}
    {variant === 'B' && <VariantB {...data} />}
    {variant === 'C' && <VariantC {...data} />}
    <PrototypeSwitcher variants={['A','B','C']} current={variant} />
  </>
);
```

### 4. Build the floating switcher

A small fixed-position bar at the bottom-centre of the screen with:

- **Left arrow** — cycles to the previous variant (wraps around).
- **Variant label** — shows the current variant key and name.
- **Right arrow** — cycles forward (wraps around).

Behaviour:

- Clicking an arrow updates the URL search param so the variant is shareable and reload-stable.
- Keyboard: `←` and `→` arrow keys also cycle.
- Visually distinct from the page so it's obviously not part of the design being evaluated.
- Hidden in production builds.

### 5. Hand it over

Surface the URL (and the `?variant=` keys). The user will flip through. The interesting feedback is usually **"I want the header from B with the sidebar from C"** — that's the actual design they want.

### 6. Capture the answer and clean up

Once a variant has won, write down which one and why. Then delete the losing variants and the switcher; fold the winner into the real page/route.

## Anti-patterns

- **Variants that differ only in colour or copy.** That's a tweak, not a prototype.
- **Sharing too much code between variants.** A shared `<Header>` is fine; a shared `<Layout>` defeats the point.
- **Wiring variants to real mutations.** Read-only is fine; point mutations at a stub.
- **Promoting the prototype directly to production.** Rewrite it properly when you fold it in.
