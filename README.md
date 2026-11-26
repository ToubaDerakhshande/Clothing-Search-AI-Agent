<div align="center">

# 🛍️ Smart Apparel Finder

✨ **Automated Smart Apparel Search, Dynamic Multi-Field Filtering, Price Normalization, and HTML Table Rendering in n8n** ✨

[![n8n](https://img.shields.io/badge/n8n-Workflow-ff6d5a?style=flat-square&logo=n8n&logoColor=white)](https://n8n.io)
[![Torob API](https://img.shields.io/badge/API-Torob-red?style=flat-square)](https://torob.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)

</div>

---

## 🌟 Overview
Searching across online shopping aggregators often returns noisy, irrelevant results (e.g., mixing hoodies when searching strictly for sweatshirts, or conflicting colors). **Smart Apparel Finder** is an advanced n8n automation workflow that queries the Torob API, executes a robust JavaScript-based strict multi-term AND filter with contradiction checks, normalizes Persian/Toman prices, sorts items by the cheapest price first, and renders a clean, responsive HTML table directly inside an n8n Form node.

---

## 🔥 Key Features

- 📥 **Dynamic Form Inputs:** Captures user queries across multiple distinct fields (`اسم پوشاک`, `رنگ پوشاک`, `نوع پوشاک`) through an interactive n8n Form.
- 📡 **Torob API Integration:** Fetches live product catalogs with scaled request sizes (`size=30`) to ensure sufficient candidates remain after strict filtering.
- 🧹 **Strict Multi-Term AND Filtering:** Implements smart text normalization, synonym handling, and contradiction checks (e.g., strictly separating hoodies from sweatshirts) to eliminate irrelevant items.
- 💰 **Robust Price Parsing & Sorting:** Converts Persian/Rial/Toman price strings into numeric values, handles missing/invalid prices cleanly, and sorts products starting from the cheapest.
- 📱 **Responsive HTML Table Output:** Renders structured results directly inside the form output using clean CSS styling, formatted Persian numbers (`.toLocaleString('fa-IR')`), and direct purchase buttons.

---

## ⚙️ Quick Workflow Flow

1. 👤 **Form Submission:** User inputs clothing name, color, and category/type via the n8n Form trigger.
2. 🌐 **HTTP Request:** Queries the Torob base product search API (`https://api.torob.com/v4/base-product/search/`) using combined query terms.
3. ⚙️ **Code Node Processing:** Runs custom JavaScript to parse prices, execute strict multi-field AND filtering, remove duplicates, and sort by price ascending.
4. 📤 **Render & Display:** Outputs a clean, responsive HTML table via the final Form node.

---

## 🛠️ Prerequisites & Setup

1. **Import Workflow:** Import the provided `smart-shop.json` file into your self-hosted or cloud n8n instance.
2. **Review Node Parameters:** 
   - Check the `HTTP Request1` node URL and headers (`User-Agent`).
   - Inspect the `Code in JavaScript` node to customize filtering rules if needed.
3. **Execute & Test:** Open the n8n Form test URL, enter your apparel search criteria, and view the sorted results table.

---

## 💡 Troubleshooting & Limitations
- **API Fuzzy Matching:** External search APIs may occasionally return fuzzy or vendor-inconsistent titles. The local JavaScript filter acts as a secondary strict barrier, but matching depends heavily on exact vendor title naming.
- **Rate Limits:** Ensure proper spacing between queries if testing intensively to respect external aggregator rate limits.

---

<div align="center">
  <sub>Built with ❤️ using n8n and JavaScript</sub>
</div>
