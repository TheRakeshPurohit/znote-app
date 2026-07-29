# 📂 SQL Your CSV

[AlaSQL](https://www.npmjs.com/package/alasql) is an open-source SQL database for JavaScript, offering high-speed queries and flexible data handling for both structured and schemaless data.

### 🚀 Why Use AlaSQL?
- ✔ **Fast In-Memory Processing** – Ideal for BI & ERP applications
- ✔ **ETL-Friendly** – Import, manipulate, and export data in multiple formats
- ✔ **Cross-Platform** – Works in Browsers, Node.js, and Mobile Apps


## 📌 Installation

### 1️⃣ Install AlaSQL
```bash 
npm install --save alasql
```

### 2️⃣ Install Table Formatter (Optional, for Display)
```bash 
npm install --save tablify
```

### 📋 Utility Function for Table Output
```js global;
async function printTable(json) {
  const { tablify } = require("tablify");
  print(tablify(json));
}
```


## 📊 Manipulate Data with SQL
In this example, we load a **TSV file** (tab-separated values), convert it to JSON, and analyze population data per continent.

> **Tip:** The `pop_est` field is initially a **string**, so we use `CAST(pop_est AS NUMBER)` to convert it into a number.

```js 
const alasql = require("alasql");

// Load Data
const response = await fetch('https://cdn.jsdelivr.net/npm/world-atlas@1/world/110m.tsv');
const tsv = await response.text();
const json = csvJSON(tsv, '\t'); // Convert TSV to JSON

// Compute total population per continent
const data = alasql(`
  SELECT continent, 
         SUM(CAST(pop_est AS NUMBER)) AS total_pop_est 
  FROM ? 
  GROUP BY continent 
  ORDER BY total_pop_est DESC
`, [json]);

printTable(data);
```


## 📈 Visualizing Data with Charts
Once the data is processed, we can convert it into a `series` format and display it as a **bar chart**.

```js 
const alasql = require("alasql");

// Load Data
const response = await fetch('https://cdn.jsdelivr.net/npm/world-atlas@1/world/110m.tsv');
const tsv = await response.text();
const json = csvJSON(tsv, '\t'); // Convert TSV to JSON

// Aggregate Data
const data = alasql(`
  SELECT continent, 
         SUM(CAST(pop_est AS NUMBER)) AS total_pop_est 
  FROM ? 
  GROUP BY continent 
  ORDER BY total_pop_est DESC
`, [json]);

// Convert to Chart Format
const continents = [...new Set(data.map(e => e.continent))];
const series = toSeries({
  data: data, 
  x: "continent", 
  y: "total_pop_est", 
  category: "continent"
});

// Render Bar Chart
barChart({
  horizontal: true,
  series: series,
  categories: continents
});
```


## 🔍 Learn More
👉 [AlaSQL Documentation](https://www.npmjs.com/package/alasql)
