# MAKES Handcrafted Jewellery — Website Redesign

A responsive e-commerce website for a handmade sterling silver jewellery brand, built in **vanilla HTML, CSS and JavaScript** (no frameworks).

Built for **User Interface Development — Assignment 3** at the University of Melbourne. It implements the high-fidelity prototype from Assignment 2, which redesigned the real site [makeshj.com.au](https://makeshj.com.au) after the usability audit in Assignment 1.

**Live site:** https://kaiting0305.github.io/MAKES-website-design/ <!-- TODO: confirm GitHub Pages is enabled -->

---

## Features

- **Full purchase flow:** Home → Shop / Collections → Product Detail → Cart → Payment → Order Confirmation
- **21 products from one data file:** every product page is generated from `scripts/products.js` through one dynamic `product-detail.html?id=N` page
- **Persistent cart:** stored in `localStorage` and shared across pages through the helpers in `cart.js`, with a live item-count badge on the cart icon
- **Filter, sort and search:** category, collection and price filters, an "order by" sort and keyword search, all running on the client
- **Checkout validation:** required billing and card fields are checked before the order is placed, and the confirmation page refuses direct access unless an order was submitted
- **Order confirmation:** generated order number and itemised receipt from a `sessionStorage` snapshot; the cart is cleared afterwards
- **Responsive layout:** CSS Grid and Flexbox, a hamburger menu overlay on mobile, and a full-width Add to Cart button pinned to the bottom on mobile
- **Product gallery:** a clickable thumbnail gallery (shown on product 1)

## Responsive Targets

The site was tested in browser DevTools at the assignment's required sizes:

| Device  | Viewport    |
|---------|-------------|
| Mobile  | 390 × 844   |
| Desktop | 1368 × 912 and 1440 × 1024 |

## Project Structure

```
.
├── index.html                  # Homepage: hero video, collections, categories, about
├── pages/
│   ├── collection-list.html    # All 8 collections
│   ├── product-list.html       # Shop grid with filter, sort and search
│   ├── product-detail.html     # Single dynamic product page (?id=N)
│   ├── shopping-cart.html      # Cart items, quantity, subtotal
│   ├── payment.html            # Billing and card form, express pay buttons
│   └── order-confirmation.html # Receipt and order number
├── scripts/
│   ├── products.js             # Single source of truth: 21 product objects
│   ├── cart.js                 # getCart / addToCart / removeFromCart / updateQty / getCartCount
│   ├── main.js                 # Header, search overlay, hamburger menu, scroll-to-top, cart badge
│   ├── product-list.js         # Renders grid, filters, sorting, search
│   ├── product-detail.js       # Reads URL param, renders product, gallery, quantity, Add to Cart
│   ├── shopping-cart.js        # Renders cart, quantity updates, removal, subtotal
│   ├── payment.js              # Order summary, form validation, order snapshot
│   └── order-confirmation.js   # Renders receipt, clears cart
├── styles/
│   ├── colors.css              # Brand palette as CSS custom properties
│   ├── typography.css          # Google Fonts import and font variables
│   ├── main.css                # Shared header, footer, nav, overlays, buttons
│   └── *.css                   # One stylesheet per page
└── assets/                     # Product, collection and homepage images and hero video
```

## Architecture Notes

**`products.js` holds all product data.** Each product is one object (name, price, category, collection, images, description, measurements, care). The product list, product detail, cart and confirmation pages all read from it, so no product HTML is duplicated.

**`cart.js` is the only code that writes the cart.** Pages never write the `cart` key in `localStorage` themselves; they call `getCart()`, `addToCart()`, `removeFromCart()` and `updateQty()`. The storage key and data format therefore live in one place. (`main.js` reads the cart directly, but only to update the badge on pages that don't load `cart.js`.)

## Design System

| Token | Value |
|-------|-------|
| Background | `#FAF8F5` warm off-white |
| Surface | `#EDE0D4` dusty cream |
| Accent | `#8B6347` earthy brown |
| Text | `#2C1810` deep espresso |
| Headings | Cormorant Garamond |
| Body | Jost |

## Running Locally

No build step is needed.

```bash
git clone https://github.com/kaiting0305/MAKES-website-design.git
cd MAKES-website-design
```

Open `index.html` in a browser, or serve the folder (for example with the VS Code Live Server extension or `python -m http.server`) so relative paths and storage behave as they do when hosted.

## Credits & Disclosure

- **Fonts:** [Google Fonts](https://fonts.google.com) (Cormorant Garamond, Jost)
- **Icons:** [Lucide](https://lucide.dev), loaded from the unpkg CDN (ISC licence)
- **Product imagery:** from the original MAKES Handcrafted Jewellery website, used for non-commercial university coursework only
- **AI use:** Claude (Anthropic) helped debug specific JavaScript issues and review code. I wrote and understand all of the logic.

## Author

**Kai-Ting Hung**, Bachelor of Design (Computing and Software Systems), University of Melbourne

*This is a student project and not a real store. No payments are processed.*
