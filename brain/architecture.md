# Architecture: Contractor Quotation Tool

## Frontend Structure
```
src/
├── pages/
│   ├── Login.jsx          # Google OAuth via Supabase
│   ├── Dashboard.jsx      # List of all past quotes
│   ├── NewQuote.jsx       # Create/edit quote form
│   └── QuotePreview.jsx   # Final view before PDF/share
│
├── components/
│   ├── QuoteForm/
│   │   ├── ClientDetails.jsx
│   │   ├── LaborSection.jsx
│   │   ├── MaterialSection.jsx
│   │   └── TotalsSection.jsx
│   ├── QuoteCard.jsx      # Used in Dashboard list
│   ├── PDFTemplate.jsx    # Styled quote for PDF export
│   └── Navbar.jsx
│
├── services/
│   ├── supabase.js        # Supabase client init
│   ├── quoteService.js    # CRUD operations for quotes
│   └── pdfService.js      # PDF generation logic
│
├── hooks/
│   ├── useAuth.js         # Auth state management
│   └── useQuotes.js       # Quote data fetching
│
└── utils/
    ├── calculations.js    # Labor + material + GST math
    └── whatsapp.js        # WhatsApp share URL builder
```

## Supabase Database Schema

### Table: quotes
| Column         | Type      | Notes                        |
|----------------|-----------|------------------------------|
| id             | uuid PK   | Auto-generated               |
| user_id        | uuid FK   | Linked to auth.users         |
| client_name    | text      |                              |
| client_phone   | text      |                              |
| site_location  | text      |                              |
| quote_date     | date      |                              |
| labor_items    | jsonb     | Array of {name, qty, rate}   |
| material_items | jsonb     | Array of {name, qty, rate}   |
| profit_margin  | numeric   | Percentage                   |
| gst_percent    | numeric   | 0, 5, 12, or 18              |
| total_amount   | numeric   | Calculated on save           |
| status         | text      | draft / sent / accepted      |
| created_at     | timestamp | Auto                         |

## Calculation Logic (utils/calculations.js)
```
labor_total    = SUM(qty × rate) for each labor item
material_total = SUM(qty × rate) for each material item
subtotal       = labor_total + material_total
profit_amount  = subtotal × (profit_margin / 100)
gst_amount     = (subtotal + profit_amount) × (gst_percent / 100)
grand_total    = subtotal + profit_amount + gst_amount
```

## Folder Rules
- All API calls go through services/ — never directly from components
- No business logic in components — use hooks or utils
- All Supabase queries in quoteService.js only
- PDF generation isolated in pdfService.js
- Components must be reusable — no hardcoded data

## Auth Flow
1. User lands on /login
2. Clicks "Login with Google"
3. Supabase OAuth redirect
4. On success → redirect to /dashboard
5. useAuth hook manages session globally
