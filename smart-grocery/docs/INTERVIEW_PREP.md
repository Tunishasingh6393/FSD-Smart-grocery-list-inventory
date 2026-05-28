# 🎤 Interview Preparation — SmartPantry Project

---

## Q1: Explain your project.

**HR Answer:**
I built SmartPantry — a Smart Grocery List and Inventory Manager. It solves a real-world problem that every household faces: running out of essential items, forgetting to buy things, and wasting food because it expires. The app tracks your pantry inventory, sends low-stock and expiry alerts, auto-generates shopping lists, and includes a recipe planner that pushes missing ingredients directly to your shopping list.

**Technical Answer:**
The app is a full-stack web application. The frontend is built in React.js with Tailwind CSS, communicating with a Node.js/Express backend via REST APIs. Data is stored in MongoDB using Mongoose schemas. JWT authentication secures all routes. Key features include real-time CRUD for inventory items, threshold-based alert logic comparing current quantity to minimum stock levels, expiry date tracking with day-difference calculations, and an auto-generate feature that scans all items and populates the grocery list intelligently.

---

## Q2: What tech stack did you use and why?

**Answer:**
I used the MERN stack — MongoDB, Express.js, React.js, and Node.js — because it's a JavaScript-only stack that enables fast development across both frontend and backend. MongoDB's document model was perfect for flexible item schemas (different units, categories, optional expiry). React gave me component-based UI with clean state management. JWT was chosen for stateless, scalable authentication. For the demo version, I used vanilla JS with localStorage to make it instantly runnable without any server setup.

---

## Q3: How does the low-stock alert system work?

**Answer:**
Each inventory item has a `qty` (current quantity) and `min` (minimum threshold). The alert logic is:
```javascript
function isLow(item) {
  return item.qty < item.min;
}
```
The dashboard and alerts page filter all items against this condition. On the backend (MERN version), an API endpoint `/api/dashboard/alerts` runs this query:
```javascript
const lowStock = await Item.find({ $expr: { $lt: ['$qty', '$min'] } });
```
Users can also click "Add to List" to instantly push that item to their shopping list.

---

## Q4: How did you implement JWT authentication?

**Answer:**
On login, the backend validates credentials (password checked via bcrypt.compare), then signs a JWT:
```javascript
const token = jwt.sign({ userId: user._id }, process.env.JWT_SECRET, { expiresIn: '7d' });
```
This token is sent to the frontend and stored (localStorage in demo, httpOnly cookie in production). A middleware function verifies the token on protected routes:
```javascript
const authMiddleware = (req, res, next) => {
  const token = req.headers.authorization?.split(' ')[1];
  const decoded = jwt.verify(token, process.env.JWT_SECRET);
  req.user = decoded;
  next();
};
```

---

## Q5: How is the MongoDB schema designed?

**Answer:**
The Item schema has:
```javascript
const ItemSchema = new mongoose.Schema({
  userId: { type: ObjectId, ref: 'User', required: true },
  name: { type: String, required: true },
  category: String,
  unit: String,
  qty: { type: Number, default: 0 },
  minQty: { type: Number, default: 1 },
  expiryDate: Date,
  price: Number
}, { timestamps: true });
```
The `userId` field enables multi-user data isolation — each user only sees their own items. Indexes on `userId` and `expiryDate` make alert queries fast.

---

## Q6: What is the expiry alert logic?

**Answer:**
The expiry alert computes the number of days between today and the expiry date:
```javascript
function daysUntil(dateStr) {
  return Math.ceil((new Date(dateStr) - new Date()) / 86400000);
}
```
Items with `daysUntil < 0` are expired (shown in red), items with `daysUntil <= 7` are expiring soon (shown in amber). This is rendered as color-coded badges in the UI. On the backend:
```javascript
const expiring = await Item.find({
  userId: req.user.id,
  expiryDate: { $lte: new Date(Date.now() + 7*24*60*60*1000) }
});
```

---

## Q7: How does the Recipe-to-List feature work?

**Answer:**
Each recipe stores an array of ingredients. When the user clicks "Add to List," the app iterates over ingredients and creates grocery entries for any that aren't already in the list:
```javascript
recipe.ingredients.forEach(ing => {
  if (!groceryList.find(g => g.name === ing.name && !g.checked)) {
    groceryList.push({ name: ing.name, qty: ing.qty, unit: ing.unit, source: 'recipe' });
  }
});
```
The `source` field tracks where each list entry came from: 'manual', 'lowstock', 'auto', or 'recipe'.

---

## Q8: How did you make the app responsive?

**Answer:**
I used CSS Grid and Flexbox with media queries for breakpoints. The sidebar collapses on mobile using a hamburger toggle and CSS transform. The stats grid switches from 4 columns to 2 on small screens. All cards use `max-width` and percentage-based widths. I also added touch-friendly tap targets (minimum 44px height) for mobile usability.

---

## Q9: How would you scale this app for production?

**Answer:**
Several improvements for production:
1. **Database:** Add indexes on frequently queried fields (userId, expiryDate, qty)
2. **Caching:** Redis for dashboard stats (computed once per minute, not per request)
3. **Jobs:** BullMQ or cron jobs for daily alert emails
4. **Auth:** httpOnly cookies instead of localStorage, refresh tokens
5. **PWA:** Service workers for offline access and push notifications
6. **Rate limiting:** Express-rate-limit to prevent API abuse
7. **Validation:** Joi or Zod for input validation on all endpoints

---

## Q10: What was the most challenging part?

**Answer:**
The most challenging part was the auto-generate grocery list logic. I had to handle multiple sources — low stock, expiry, recipes — without creating duplicate entries, while preserving manually added items. I solved this with a deduplication check comparing item names (case-insensitive) and only adding if no unchecked entry with that name already exists. Maintaining the `source` metadata (manual/auto/lowstock/recipe) was also important for transparency to the user.

---

## Bonus: What would you add next?

- Barcode scanner (using device camera + Open Food Facts API)
- Receipt OCR (upload photo, auto-parse items)  
- Shared household lists (invite family members)
- Price history and trend charts
- Email/push notifications for alerts
- AI-powered suggestions based on usage patterns
