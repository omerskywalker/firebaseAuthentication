Before we continue L3 scaffolding work, I need a structured reconnaissance report on the repo. This is read-only — do not make any code changes. Here's what I need:

I need your help mapping the existing code structure for the Payment Detail Page and 
Payment Detail Drawer so I can plan an upcoming UI restructure. Do NOT make any code 
changes. I just need information. Be thorough and precise — I want to understand exactly 
what exists before we touch anything.

Please investigate and report back on the following, in order. Format your response with 
clear section headers matching the numbered items below. Where possible, include file 
paths and short code excerpts (a few lines, not whole files).

## 1. High-level project structure
- Root layout of the repo (top-level folders only, with a 1-line description of each)
- Where the Payment Detail Page and Payment Detail Drawer currently live
- Whether this is a monorepo, and if so, which package(s) are relevant here
- Framework version (React, Next, etc.) and any notable build-tool config

## 2. L3 Conversion scaffolding
We set up an alternate route and folder for "L3 conversion" work so we can develop the 
restructured page alongside the BAU component. Please find and describe:
- The L3 route definition(s) — which file, what path, what layout wraps it
- The L3 folder structure (tree view, 2-3 levels deep)
- Any feature flag, environment variable, or conditional that gates L3 vs BAU rendering
- Any shared infrastructure the L3 version inherits from (context providers, data hooks, 
  types, utilities) vs what's been forked or duplicated
- What's already been fleshed out in L3 vs what are just empty scaffolds

## 3. BAU component structure (current Payment Detail Page)
- The top-level component file and its imports
- The component tree: list each child component and where it's imported from, indented 
  to show nesting. Example format:
    PaymentDetailPage
      ├─ PaymentDetailHeader (from ./components/PaymentDetailHeader)
      │   ├─ KPI (from @pepper/reactkit)
      │   └─ Breadcrumbs (from @pepper/reactkit)
      ├─ InfoBanner (from @salt-ds/core)
      └─ ... etc
- Identify which components are shared across payment types (Wire, RTP, ACH, etc.) vs 
  Wire-specific
- Approximate line count of each region's component file

## 4. BAU component structure (current Payment Detail Drawer)
Same tree format as #3, for the drawer surface.
- Is the drawer a separate component tree, or does it share components with the page?
- How is the drawer triggered and what component manages its open/close state?

## 5. Status and type handling
- How are the 8+ Wire statuses currently represented in code? (enum, union type, string 
  literals, backend-provided?) Paste the type definition.
- How are the 7 payment types represented? Paste the type definition.
- Where are status-dependent UI decisions made? (conditional rendering, component swaps, 
  prop differences) Show 1-2 representative examples.
- How is entitlement logic handled for action buttons (Approve, Decline, Pay again, 
  Edit payment, Cancel payment)? Show a representative example.

## 6. Design system usage patterns
- Which Salt components are most commonly imported in the Payment Detail area?
- Which Pepper components are most commonly imported?
- Is there a Blend layer in use here, or just Salt + Pepper?
- Any local wrapper components around Salt/Pepper primitives?
- Show one representative example of how LabelValue is currently used in BAU (file 
  path + 10-15 line excerpt)
- Show one representative example of how the current "Payment details" / "Sender details" 
  section headers are implemented — are they plain text, a heading component, part of 
  a Card header, etc.?
- Show how the current page header (amount + "wire to X") is built. The new design uses 
  the Pepper KPI component with Large size, Suffix word "USD", no prefix.

## 7. Layout primitives
- Is layout handled via Salt StackLayout / FlexLayout, via Pepper primitives, via raw 
  CSS/flex/grid, or a mix? Show what the current page uses for its outer structure.
- How is the two-column "Sender details / Recipient details" split currently 
  implemented? Paste that block.
- How is responsive behavior handled today? (CSS media queries, a responsive hook, Salt 
  breakpoint utilities, container queries?) Show one example.

## 8. Styling and tokens
- Are styles in CSS Modules, styled-components, plain CSS, inline style objects, or Salt 
  mode tokens? 
- Find one representative stylesheet for a Payment Detail component and paste it.
- Are `var(--salt-*)` and `var(--pepper-*)` tokens used directly, or is there an 
  abstraction layer (theme hook, styled-system, etc.)?
- Are there any hardcoded colors, spacing values, or font sizes in the current Payment 
  Detail files? (I'm trying to gauge how clean the design-system adherence is today.)

## 9. Figma Code Connect integration
The designers are using Figma Code Connect — I can see `salt-figma-code-connect` 
references in the Figma inspect panel. 
- Is Code Connect set up on the code side of this repo? 
- If yes, where do the `.figma.tsx` files live, and are there any for Payment Detail 
  components?
- If not, is there an internal doc describing the intended integration?

## 10. Tests and Storybook
- Is there a Storybook for the Payment Detail components? Where does it live?
- What test framework is used for component tests in this repo?
- Show one example test file for a Payment Detail component (the smallest/simplest one).
- Are there visual regression tests (Chromatic, Percy, Playwright screenshots)?

## 11. Git and branch state
- Current branch name
- Any uncommitted L3 work in progress
- Is there an existing feature branch for the DCBMM1-28769 ticket (Pepper card styling) 
  or DCBMM1-28078 (L3 migration) that I should be aware of?

## 12. Gotchas and constraints
Based on what you've seen:
- Any components, utilities, or patterns that look deprecated, flagged for replacement, 
  or marked "DO NOT USE"?
- Any TODO/FIXME comments in the Payment Detail area that seem relevant?
- Any config or lint rules that would affect how we write the new L3 components 
  (import ordering, barrel files, max line length, etc.)?
- Any CI checks that typically catch issues in PRs for this area (type coverage, 
  bundle size, a11y)?

---

Take your time. Be specific with file paths. When showing code excerpts, keep them short 
(10-15 lines max per excerpt) but enough that I can see the pattern. If any section is 
not applicable or you can't find the information, say so explicitly rather than guessing.
