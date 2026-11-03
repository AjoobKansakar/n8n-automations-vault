# Scenario 7: Flash-Sale Order & Inventory Dispatch Engine (Single Order)

An end-to-end e-commerce order processing pipeline that catches raw cart webhooks, enriches items with warehouse inventory data, removes duplicate line items, calculates totals, and dispatches multi-channel alerts (Slack & Email) after returning an instant API response.

---

## 🖼️ Workflow Architecture

![Workflow Canvas](Scenario 7 Workflow Canvas (Single Order).png)

---

## ⚡ Challenges Solved

- **Unpacking Nested Data:** Flattens incoming nested `cart_items` arrays into individual line items.
- **Inventory Enrichment:** Merges cart items with live Google Sheets stock data (Shelf location, Supplier, Unit Price) via Product ID.
- **Deduplication:** Filters out redundant product clicks in the current cart batch using the **Remove Duplicates** node.
- **Dynamic Pricing:** Computes line totals (`Quantity × Unit Price`) and strips out transport headers.
- **Consolidated Manifest:** Aggregates all items back into a single structured shipment list for fulfillment.
- **Fast Acknowledgment Pattern:** Responds with `200 OK` immediately, then runs customer Email receipts and warehouse Slack alerts in the background.

---

## ⚙️ Nodes Used

- **Webhook Node (POST):** Receives the checkout payload.
- **Split Out Node:** Flattens the cart array into separate items.
- **Google Sheets Node:** Reads the master inventory catalog.
- **Merge Node:** Combines cart items with catalog data (`Keep Matches`).
- **Remove Duplicates Node:** Eliminates duplicate products in the batch.
- **Edit Fields (Set) Node:** Performs line-item math and formats schema.
- **Aggregate Node:** Packages products into a unified packing slip.
- **Respond to Webhook Node:** Returns the dispatch confirmation payload.
- **Slack Node:** Alerts the warehouse team with shelf-picking locations.
- **Send an Email Node (SMTP):** Sends the customer their formatted order receipt.

---

## 🚀 How to Import

1. Download [`workflow.json`](./workflow.json).
2. In n8n: **`...`** ➔ **Import from File**.
3. Link your Google Sheet, Slack Bot, and SMTP credentials.
4. Activate the Webhook and trigger via Postman!
