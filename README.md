# Firebase Authentication Service

## leverage firebase for user authentication in web app



Redesign the styling of this ESLint quality report (single self-contained HTML string built in a .cjs file, inline <style> only, no external fonts, CDNs, or packages — must work fully offline). Keep all existing data, structure, and DOM; only change CSS and class/markup for visual presentation. Apply this design system exactly:
Fonts (system stack, no downloads): Use -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif for all UI text. Use ui-monospace, "SF Mono", "Cascadia Code", "Consolas", monospace for ALL numbers, counts, percentages, file paths, and rule names. Drop Montserrat and Oswald entirely.
Color tokens (define as CSS custom properties on :root):

--bg: #f6f7f9 (page), --surface: #ffffff (cards)
--ink: #0f172a (primary text), --ink-muted: #64748b (labels/secondary)
--border: #e2e8f0 (hairlines)
--accent: #2563eb (primary/interactive), --accent-soft: #eff6ff
Severity scale for warning counts: --sev-low: #64748b, --sev-mid: #d97706, --sev-high: #dc2626
--error: #dc2626, --error-soft: #fef2f2

Severity encoding (most important): Color the warning-count numbers and pills by magnitude, not a flat yellow. Bucket: counts ≥30 use --sev-high, 10–29 use --sev-mid, <10 use --sev-low. The bigger the problem, the redder and bolder it reads. Apply the same logic to the "Top Warning Files" count badges.
Layout & spacing: Use an 8px spacing scale (8/16/24/32). Set card padding to 24px, gap between cards to 16px. Constrain max page width to ~1200px, centered, with 32px outer padding. Cards: --surface background, 1px solid --border, border-radius: 12px, and a soft shadow (0 1px 3px rgba(15,23,42,0.04), 0 1px 2px rgba(15,23,42,0.06)) — NO heavy drop shadows.
Header: Make "ESLint Quality Report" font-weight: 700, font-size: 28px, --ink. The "Generated/Source" line goes --ink-muted, 13px. Convert the status badge ("WARNINGS PRESENT") to a pill: if errors > 0 use --error-soft bg / --error text, else amber; uppercase, letter-spacing: 0.05em, font-size: 11px, font-weight: 600.
Stat cards (top row): Label in --ink-muted, 11px, uppercase, letter-spacing 0.06em. The big number in monospace, font-size: 36px, font-weight: 700. Color the ERRORS number --error when >0 else --ink; color WARNINGS number with the severity scale based on total.
Tables: Remove zebra striping. Use a 1px solid --border bottom hairline per row, 12px vertical row padding. Column headers: --ink-muted, 11px, uppercase, letter-spacing 0.05em, font-weight: 600. Right-align all numeric columns and set them in monospace with font-variant-numeric: tabular-nums so digits align. On row hover, background --accent-soft.
Distribution bars (SHARE column): Replace the flat blue bar with a track (--border background, border-radius: 999px, height: 6px) and a fill colored by the same severity scale as that row's count. Put the percentage in monospace immediately after, --ink-muted.
Pills/badges: border-radius: 6px, padding: 2px 8px, font-size: 12px, font-weight: 600, monospace, soft-tinted background of the matching severity color at ~12% opacity. A 0 error pill should be muted/neutral, not red.
File paths: Render in monospace, 13px, --ink, and visually de-emphasize the directory portion vs the filename if feasible (muted dirs, bold filename) — but keep it simple if that requires JS gymnastics.
Section titles ("Rule Distribution", "Top Warning Files"): font-weight: 700, 16px, --ink, with 16px bottom margin and a hairline divider under them.
Keep everything responsive down to ~900px (stack the two columns). Output the complete updated .cjs file.
