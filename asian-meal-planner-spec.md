# Asian Budget Meal Planner — Product Blueprint

## 1) Product Vision
Build a mobile-first web app that helps immigrants and international students create affordable weekly meal plans with authentic Asian dishes, while sourcing ingredients from nearby Asian supermarkets (e.g., H Mart, 99 Ranch, Mitsuwa, local Korean/Chinese/Vietnamese stores).

Core outcomes:
- Stay within a weekly/monthly food budget.
- Preserve cultural food preferences (regional cuisines, familiar staples, condiments).
- Reduce planning stress by mixing convenience foods (instant noodles, frozen dumplings) with fresh home-cooked meals.
- Recommend nearby stores and where to buy hard-to-find sauces/seasonings.

---

## 2) Target Users
- New immigrants in the U.S.
- International students and young professionals.
- Families balancing cost, convenience, and authenticity.
- Users with limited transportation and a need for nearby stores.

---

## 3) Core User Flow
1. **Onboarding**
   - Enter ZIP code/city.
   - Set weekly budget (e.g., $45/$80/$120).
   - Select cuisine preferences (Chinese, Korean, Japanese, Vietnamese, Filipino, Thai, Indian, etc.).
   - Choose dietary constraints (vegetarian, halal, low sodium, allergy constraints).

2. **Pantry Setup**
   - Mark already-owned staples (soy sauce, rice, sesame oil, gochujang).
   - Auto-reduce shopping list cost based on pantry inventory.

3. **Meal Plan Generation**
   - Generate 7-day plan with breakfast/lunch/dinner.
   - Mix categories:
     - Quick meals: instant noodles + add-ons (egg, bok choy, tofu).
     - Convenience meals: frozen dumplings, buns, scallion pancakes.
     - Fresh meals: stir-fries, soups, noodle bowls, rice dishes.
   - Show per-meal and total cost estimates.

4. **Store & Ingredient Sourcing**
   - Map nearby Asian supermarkets.
   - Match each ingredient to likely store availability.
   - Suggest alternatives when unavailable (brand or ingredient substitutions).

5. **Checkout & Weekly Routine**
   - Consolidated shopping list by store.
   - Optional “best route” for multi-store shopping.
   - Save favorite plans and regenerate next week with price learning.

---

## 4) MVP Feature Set (First Release)
### A. Meal Planning Engine
- Budget-constrained weekly planner.
- Recipe database tagged by cuisine, prep time, authenticity score, and cost tier.
- Supports instant noodles/frozen foods + fresh ingredient combinations.

### B. Cost Estimation
- Item-level price estimates by region/store.
- Budget guardrails:
  - Hard cap mode (never exceed budget).
  - Flexible mode (optimize nutrition/authenticity first).

### C. Location-Based Store Discovery
- Detect user location (with consent) or manual ZIP entry.
- Find nearby Asian stores (chains + local independent stores).
- Basic store metadata: address, distance, hours, price tier.

### D. Shopping List Builder
- Deduplicated ingredient list.
- Grouped by category (produce, freezer, dry goods, sauces/seasonings).
- Grouped by recommended store.

### E. Cultural Personalization
- Language toggle for key surfaces (English + Chinese/Korean/Vietnamese to start).
- Cuisine-specific staple defaults.

---

## 5) Recommended Tech Stack
### Frontend
- **Next.js (React + TypeScript)** for SEO and fast iteration.
- **Tailwind CSS** for clean, responsive UI.
- **Map integration** via Google Maps Platform or Mapbox.

### Backend
- **Python FastAPI** or **Node.js (Nest/Express)**.
- Auth: Clerk/Auth0/Firebase Auth.
- API-first architecture for web + future mobile app.

### Data Layer
- **PostgreSQL** for structured data.
- Redis cache for frequently requested ingredient/store lookups.

### External Data Integrations
- Places API for store discovery and metadata.
- Optional grocery/pricing APIs and scraper pipelines where allowed.
- Geocoding + distance matrix for route suggestions.

### AI/Optimization Layer
- Rules + lightweight optimization first (linear programming style budget constraints).
- Add LLM assistant later for conversational plan edits:
  - “Swap two dinners for vegetarian meals under $10 total.”

---

## 6) Data Model (Simplified)
- **User**: location, budget, preferences, dietary constraints.
- **Ingredient**: unit, avg price, substitutes, store availability probability.
- **Recipe**: cuisine, steps, ingredients, prep time, authenticity tag, nutrition.
- **Store**: geolocation, chain/local type, categories, estimated price index.
- **MealPlan**: week range, meals, total estimated cost, shopping list.

---

## 7) Sample Weekly Budget Strategy
For a **$70/week** user:
- 3 convenience meals (instant noodles/frozen dumplings enhanced with protein/veg)
- 8 cooked meals using shared ingredients (rice, eggs, tofu/chicken, leafy greens)
- 3 leftovers/flex meals

Optimization approach:
- Reuse overlapping ingredients across dishes.
- Prefer lower-cost produce in-season.
- Keep “flavor core” budget for authentic sauces/condiments.

---

## 8) Example UI Pages
1. Landing page (value proposition for immigrants/students).
2. Onboarding wizard (budget + cuisine + location).
3. Generated weekly plan dashboard.
4. Interactive shopping list with store tabs.
5. Store map with distance and hours.
6. Pantry manager + substitutions.

---

## 9) Success Metrics
- Week-1 activation: user creates first 7-day plan.
- Budget adherence rate (actual spend vs planned spend).
- Store recommendation click-through rate.
- Repeat weekly planning rate.
- Meal satisfaction and authenticity rating.

---

## 10) 6-Week MVP Build Plan
### Week 1–2: Foundation
- Setup auth, profiles, and onboarding.
- Seed initial recipe + ingredient dataset.

### Week 3–4: Planner + Shopping
- Implement budget-aware planner.
- Generate shopping list with pantry subtraction.

### Week 5: Location + Store Discovery
- Integrate maps and place search.
- Store ranking by distance and cost tier.

### Week 6: Polish + Beta
- Add language support baseline.
- QA with 20–30 pilot users.
- Add feedback loop for missing ingredients/stores.

---

## 11) Risks and Mitigations
- **Price accuracy drift:** show ranges, allow manual correction, learn from user edits.
- **Store inventory uncertainty:** provide substitutes and multi-store fallback.
- **Cultural authenticity variance:** community ratings and cuisine-specific curators.
- **API cost growth:** cache aggressively and limit map calls.

---

## 12) Future Expansion
- Receipt scan for real spend tracking.
- “Cook in 20 minutes” mode for busy workers/students.
- Family-size and child-friendly meal modes.
- Community recipe sharing by language/country.
- Native iOS/Android app after web MVP proves retention.
