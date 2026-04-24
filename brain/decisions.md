# Decisions: Contractor Quotation Tool

## Tech Choices

### React + Vite (not Next.js)
- Reason: Simpler setup, no SSR complexity needed
- Hosting on Vercel/GitHub Pages = static build only
- Sandip already familiar with Vite from Invoice Generator

### Supabase (not Firebase)
- Reason: PostgreSQL = better for relational quote data
- Already used in Invoice Generator — no new learning curve
- Free tier generous enough for early users
- Built-in Google OAuth — no extra config

### jsPDF (not react-pdf)
- Reason: Easier to use, no extra dependencies
- Works client-side — no server needed
- If complex layouts needed later → switch to @react-pdf/renderer

### Tailwind CSS
- Reason: Fast UI development, mobile responsive utilities
- Consistent with existing projects

### WhatsApp Share (not Email)
- Reason: Contractors in India use WhatsApp — not email
- wa.me link = zero backend needed
- PDF link shared as Supabase storage URL

## Business Decisions

### Free Tier = 5 quotes/month
- Reason: Low enough to push upgrades, high enough for trial
- Track usage in Supabase (count quotes per user per month)

### Price = ₹299/month
- Reason: Affordable for small contractor
- Comparable to similar Indian SaaS tools
- Can increase after traction

### No mobile app (yet)
- Reason: Web app works on phone browser — good enough for v1
- PWA possible later (add to homescreen)

## Deferred Decisions
- Razorpay vs Cashfree — decide at Phase 7
- Multi-company support — not in v1
- Invoice vs Quotation distinction — currently only quotation
