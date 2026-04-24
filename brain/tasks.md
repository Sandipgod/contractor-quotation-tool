# Tasks: Contractor Quotation Tool

## Phase 1 — Foundation
- [ ] Create Vite + React + Tailwind project
- [ ] Setup Supabase project (new project on supabase.com)
- [ ] Enable Google OAuth in Supabase Auth settings
- [ ] Create quotes table in Supabase (schema in architecture.md)
- [ ] Setup Row Level Security (RLS) — users see only their own quotes
- [ ] Create supabase.js service file with client init

## Phase 2 — Auth
- [ ] Build Login page (Google button only — keep it simple)
- [ ] Implement useAuth hook
- [ ] Protected routes — redirect to /login if not logged in
- [ ] Test Google login flow end to end

## Phase 3 — Quote Form (Core Feature)
- [ ] Build NewQuote page layout
- [ ] ClientDetails component (name, phone, site location, date)
- [ ] LaborSection component (add/remove rows, qty × rate auto-calc)
- [ ] MaterialSection component (same as Labor)
- [ ] TotalsSection component (subtotal, margin %, GST %, grand total)
- [ ] calculations.js utility (all math here)
- [ ] Save quote to Supabase (quoteService.js)

## Phase 4 — Dashboard
- [ ] Build Dashboard page (list of all past quotes)
- [ ] QuoteCard component (client name, date, amount, status badge)
- [ ] Filter by status (draft / sent / accepted)
- [ ] Click quote → open QuotePreview

## Phase 5 — Output (PDF + Share + Print)
- [ ] Build QuotePreview page (clean printable layout)
- [ ] PDF download (jsPDF or react-pdf)
- [ ] WhatsApp share button (wa.me link with pre-filled message)
- [ ] Print button (window.print() with print CSS)

## Phase 6 — Polish
- [ ] Mobile responsive (contractors use phones)
- [ ] Empty states (no quotes yet)
- [ ] Loading states
- [ ] Error handling (network errors, auth errors)
- [ ] Deploy to Vercel

## Phase 7 — Monetization (Future)
- [ ] Quote limit for free users (5/month)
- [ ] Razorpay subscription integration
- [ ] Upgrade prompt UI
