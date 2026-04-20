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


//////////////////////////////////////
//////////// next
/////////////////////////////////

I need a follow-up reconnaissance report, this time focused on the two parallel L3 
implementation paths we've started: V1 (modifying existing L3 structure in place) and 
V2 (a template-driven "floorplan" approach that imports a base L3 layout and composes 
into it). The first report covered BAU; this one is about these two forks.

Do NOT make any code changes. Read-only investigation. Format your response with the 
section headers below.

## 1. V1 and V2 location and structure
- Where does V1 code live? Folder path and top-level file tree (2 levels deep).
- Where does V2 code live? Folder path and top-level file tree (2 levels deep).
- Are V1 and V2 both gated behind L3_PAYMENT_DETAILS_ENABLED, or do they have separate 
  flags / routes / conditionals?
- If there are separate routes for V1 vs V2, list them.

## 2. V1 status
- Which files in V1 have been substantially modified vs left as scaffolds?
- List the files with line counts and a 1-sentence description of what each file does.
- What's the overall architecture of V1? (e.g., "extends the BAU PaymentDetails container 
  with L3-specific overrides," "forks the component tree entirely," etc.)
- What's complete, what's in progress, and what's unstarted?
- Any known bugs, TODOs, or FIXMEs specifically in V1 files?

## 3. V2 status
- What is the "base L3 floorplan" that V2 imports? File path and purpose.
- Show a short excerpt of how the floorplan defines the page flow (e.g., slots, 
  sections, composition API).
- Which regions/sections have been fleshed out in V2 vs left as floorplan stubs?
- Overall: is V2 mostly floorplan with little content, half fleshed, or nearly 
  complete?
- Any known bugs, TODOs, or FIXMEs specifically in V2 files?

## 4. What's duplicated between V1 and V2
- Is there overlap in logic or components? List the duplicates.
- Are shared utilities/hooks used by both, or has each forked its own copy?
- If a bug were fixed in V1, would it automatically carry to V2, or would we need to 
  fix it twice?

## 5. How each approach handles the big restructure items
For each of these, tell me how V1 handles it and how V2 handles it (or "not yet 
addressed" if stubbed):
- New composite page title (breadcrumb + "Payment details" sub-label + amount + 
  "wire to X" on one line via updated KPI/header)
- Submission history moved to top, expanded by default for NEEDS_APPROVAL
- Sender / Recipient two-column split with updated labels
- Additional details section collapsed by default
- Status-specific banner variants (info, warning, error — Scheduled, Approaching cut 
  off, Overdue, Recipient unavailable)
- Action button migration to DecisionButtonGroup (from the prior separate Approve/Decline 
  buttons)
- Drawer using the same content container as the page (via isDrawerView prop)
- Responsive reflow at 960px, 600px, 0-599px breakpoints

## 6. Commit history
- How many commits have landed on V1 vs V2 on the current branch?
- Who authored them (just names, so I can see if this is solo or collaborative)?
- Date range of commits for each.
- Any commits that touch both V1 and V2 files (indicating shared refactors)?

## 7. Testing state
- Any tests written specifically for V1 components? Which files?
- Any tests written specifically for V2 components? Which files?
- Do the existing BAU tests still pass with V1 / V2 changes? (Check test file references 
  to L3 components.)

## 8. Risks and blockers per path
Based on what you've seen:
- What are the biggest risks if we chose to finish V1 and ship it?
- What are the biggest risks if we chose to finish V2 and ship it?
- Are there any hard blockers in either path (e.g., "V2 imports a component that doesn't 
  exist yet" or "V1 has a circular dependency")?
- Are there any dependencies between V1 and V2 where abandoning one would break the other?

## 9. Your recommendation
Given what you've seen of both paths, which is closer to completion? Which has cleaner 
architecture? Which would be easier to add the DataList → LabelValue migration onto 
later? State a recommendation with reasoning — but keep it short (3-5 bullet points).

---

Be specific with file paths and line counts. Short code excerpts (10-15 lines) where 
they clarify a point, but prefer prose descriptions. If any section can't be answered 
from the code, say so explicitly.
