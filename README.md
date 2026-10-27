# clinic-web (template + demo)

This repo is also the public demo: https://emieliasdev.github.io/clinic-web/
(repo variable `DEMO_MODE=true`, fake data in the browser, nothing saved).
Repos made from the template don't get that variable, so they build normally.

Starter deploy repo for a new clinic. Holds only the clinic's branding; all
app code stays in `EmiEliasDev/booking-app`.

```
.github/workflows/deploy.yml   calls booking-app's build-clinic.yml (don't edit)
clinic.config.json             name, logo, colors, services, copy, contact
public/logo.png                the clinic's logo (add it)
```

## New clinic, in order
1. Run `supabase/scripts/onboard_clinic.sql` (booking-app) on live and copy the
   `CLINIC_ID` from its post-check.
2. On GitHub: **Use this template → Create a new repository**, named
   `<clinic>-web`, owner EmiEliasDev, **Public** (Pages on private needs a paid plan).
3. In the new repo, Settings → Pages → Source = **GitHub Actions**.
4. Settings → Secrets and variables → Actions:
   - secret `VITE_SUPABASE_URL`
   - secret `VITE_SUPABASE_ANON_KEY` (anon key only, never service_role)
   - variable `CLINIC_ID` = the id from step 1
5. UI/UX edits `clinic.config.json` (name, shortName, logoAlt, the three colors
   `themeColor` / `accentSoft` / `accentDeep`, services, contact) and adds
   `public/logo.png`, then sets `"logo": "logo.png"` (empty = letter monogram). Pushing to `main` deploys.
6. Site: `https://emieliasdev.github.io/<clinic>-web/`.

## Notes
- Keys left out of `clinic.config.json` fall back to the template defaults.
  Arrays (like `services`) replace the defaults wholesale.
- Never put a clinic id in `clinic.config.json`; it's only read from `CLINIC_ID`.
- A booking-app merge to `main` doesn't redeploy this site yet; use
  Actions → Deploy → Run workflow.
