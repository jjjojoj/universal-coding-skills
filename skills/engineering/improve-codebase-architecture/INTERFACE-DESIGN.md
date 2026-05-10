# Interface Design

Based on "Design It Twice" (Ousterhout) — your first idea is unlikely to be the best.

## Process

### 1. Frame the problem space

Before exploring alternative interfaces, write a user-facing explanation:

- The constraints any new interface would need to satisfy
- The dependencies it would rely on, and which category they fall into (see [DEEPENING.md](DEEPENING.md))
- A rough illustrative code sketch to ground the constraints — not a proposal, just a way to make constraints concrete

### 2. Generate radically different designs

Generate 3+ interface designs for the deepened module. Each with a different design constraint:

- **Design 1**: "Minimize the interface — aim for 1–3 entry points max. Maximise leverage per entry point."
- **Design 2**: "Maximise flexibility — support many use cases and extension."
- **Design 3**: "Optimise for the most common caller — make the default case trivial."
- **Design 4** (if applicable): "Design around ports & adapters for cross-seam dependencies."

Each design should include:

1. Interface (types, methods, params — plus invariants, ordering, error modes)
2. Usage example showing how callers use it
3. What the implementation hides behind the seam
4. Dependency strategy and adapters
5. Trade-offs — where leverage is high, where it's thin

### 3. Present and compare

Present designs sequentially so the user can absorb each one, then compare them. Contrast by:

- **Depth** (leverage at the interface)
- **Locality** (where change concentrates)
- **Seam placement**

After comparing, give your own recommendation: which design is strongest and why. If elements from different designs would combine well, propose a hybrid. Be opinionated.
