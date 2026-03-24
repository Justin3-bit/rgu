# GLH Co-operative Farms

Full-stack co-operative farming marketplace built with **Next.js 14**, **Supabase**, and **CSS** 

---

## Tech Stack

| Layer     | Technology                        |
|-----------|-----------------------------------|
| Framework | Next.js 14 (App Router)           |
| Database  | Supabase (PostgreSQL + Auth + RLS)|
| Styling   | CSS |

---

## Setup

### 1. Install dependencies

```bash
npm install
```

### 2. Create a Supabase project

Go to [supabase.com](https://supabase.com) → New Project.

### 3. Run the SQL schema

In Supabase dashboard → **SQL Editor**, run these files in order:

1. `supabase/schema.sql` — tables, RLS policies, trigger, seed data
2. `supabase/functions.sql` — `decrement_stock` RPC

### 4. Set environment variables

```bash
cp .env.local.example .env.local
```

Fill in from Supabase → **Project Settings → API**:

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
```

### 5. Run

```bash
npm run dev
```

---

## Making a Producer Account

1. Sign up via `/login`
2. In Supabase → **Table Editor → profiles**, find the user row
3. Set `role` to `producer`
4. Set `farmer_id` to `1`, `2`, `3`, or `4` (matching the seeded farmers)

---

## Project Structure

```
glh/
├── app/
│   ├── layout.js               # Root layout (Navbar, Footer, CartProvider)
│   ├── page.js                 # Home page
│   ├── shop/
│   │   ├── page.js             # Server: fetches products
│   │   └── ShopClient.js       # Client: filter + add to cart
│   ├── farmers/page.js         # Farmers listing
│   ├── login/page.js           # Auth (sign in / register)
│   ├── checkout/
│   │   ├── page.js             # Server wrapper
│   │   └── CheckoutClient.js   # 3-step checkout flow
│   ├── account/
│   │   ├── page.js             # Server wrapper
│   │   └── AccountClient.js    # Orders, profile, address
│   └── dashboard/
│       ├── page.js             # Server wrapper (producer-scoped data)
│       └── DashboardClient.js  # Overview, orders, stock, farm profile
├── components/
│   ├── Navbar.js
│   ├── CartDrawer.js
│   ├── Footer.js
│   └── StatusBadge.js
├── lib/
│   ├── supabase/
│   │   ├── client.js           # Browser Supabase client
│   │   └── server.js           # Server Supabase client
│   └── cart-context.js         # Cart state with localStorage
├── styles/
│   ├── globals.css             # Design tokens, reset, base
│   ├── ui.module.css           # Buttons, cards, badges, forms, tables, tabs
│   ├── navbar.module.css
│   ├── cart.module.css
│   ├── home.module.css
│   ├── shop.module.css
│   ├── farmers.module.css
│   └── pages.module.css        # Login, checkout, account, dashboard
├── middleware.js               # Route protection
└── supabase/
    ├── schema.sql
    └── functions.sql
```

---

## CSS Architecture

All styling uses **CSS Modules** (`*.module.css`) scoped to each component/page, plus a shared `globals.css` that defines all design tokens as CSS custom properties:

```css
:root {
  --earth-700: #2d4a1e;   /* primary green */
  --gold-500:  #c8a84b;   /* accent gold   */
  --radius:    10px;
  --font-display: 'Playfair Display', serif;
  /* ... */
}
```


