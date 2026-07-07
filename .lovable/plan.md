## Goal
Ship the uploaded `IVIG_AKI_Risk_Scoring_Tool_UAE_v3_Final.html` in this project with its UI, styles, product data, and scoring JavaScript fully intact — no changes to calculations, thresholds, product entries, field IDs, or result logic.

## Approach
Serve the file as a static asset and route to it, so nothing about the original markup or JS is touched.

## Steps
1. Copy `user-uploads://IVIG_AKI_Risk_Scoring_Tool_UAE_v3_Final.html` into `public/ivig-aki.html`. Vite serves `public/` verbatim, so the original inline `<style>` and `<script>` run unchanged.
2. Replace the placeholder in `src/routes/index.tsx` with a minimal landing that immediately redirects/loads the static tool, so the preview at `/` shows the tool:
   - Use a client-side effect to set `window.location.href = "/ivig-aki.html"` on mount, with a small "Loading tool…" fallback for SSR.
   - This keeps the TanStack shell intact and avoids re-implementing anything in React.
3. Update `src/routes/__root.tsx` `head()` metadata so the tab title and social meta reflect the tool:
   - title: "IVIG-AKI Risk Scoring Tool"
   - description: "Evidence-based AKI risk stratification for IVIG therapy — KDIGO-aligned, UAE Edition."
   - matching `og:title`, `og:description`, `og:type=website`, `twitter:card=summary_large_image`.
4. Verify in the preview that:
   - `/` loads and lands on the tool.
   - Product dropdown, all inputs, Calculate Risk, results breakdown, and export all work as in the original file.

## What is NOT changing
- No edits inside the HTML file: `products` table, `calculateRisk`, `displayResults`, `switchTab`, `updateProductInfo`, `resetForm`, `exportReport`, DOM IDs, thresholds, or styling.
- No new React port of the form. No design system changes. No Tailwind edits.

## Notes
- Because the file is served from `public/`, it is available at both `/ivig-aki.html` and (via the redirect) `/`.
- If you later want it mounted directly at `/` without a redirect, that requires a small server route change — out of scope for this pass.
