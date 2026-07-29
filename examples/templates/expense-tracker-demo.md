# 💸 Track Your Spending

This template helps you load, categorize, and visualize your expenses from a CSV file. You'll learn how to:

- ✅ Import and parse CSV data
- ✅ Identify and group expenses by category
- ✅ Display data in a structured table
- ✅ Generate a clear expense breakdown with charts

Perfect for tracking spending and gaining financial insights! 🚀

```json blockName=demo-data;
Date;Category;Sub category;Amount
2024-01-16;Groceries;Walmart;50.00
2024-01-17;Entertainment;Netflix;30.00
2024-01-18;Transports;Gasoline;20.00
2024-01-19;Housing;Electricity;15.00
2024-01-20;Transports;Gasoline;45.00
```

## 🔄 Load and Parse CSV Data
```js global
// Load CSV data (replace with your file path if needed)
//const csv = String(_fs.readFileSync('/path/your_expenses.csv', "utf8")).replaceAll("\r", "");
const csv = loadBlock("demo-data");
let records = csvJSON(csv, ';');
```

## 📌 List All Categories and Subcategories
```js 
const subCatsByCat = new Map();

records.forEach((record) => {
  const category = record["Category"];
  const subcategories = [...new Set(
    records.filter(r => r["Category"] === category).map(r => r["Sub category"])
  )];
  subCatsByCat.set(category, subcategories);
});

// Display categories and subcategories
subCatsByCat.forEach((subcategories, category) => {
  console.log(`- ${category}`);
  subcategories.forEach(subcat => console.log(`  - ${subcat}`));
});

```

## 📊 Display Data in a Table
```js 
// Filter specific columns if needed
//records = filter(records, ["Category", "Sub category"]);
showDatagrid({data: records, pagination: true});
```

## 📉 Prepare Data for Charting
```js 
// Define custom category mapping
const categories = {
  "Groceries": ['Walmart', 'Grocery Store'],
  "Entertainment": ['Netflix', 'Spotify'],
  "Utilities": ['Electric', 'Water', 'Gas'],
};

// Assign categories based on subcategories
const categorizedData = records.map(record => {
  const category = Object.keys(categories).find(cat =>
    categories[cat].some(keyword => record["Sub category"].includes(keyword))
  );
  return { ...record, Category: category || 'Other' };
});

// Summarize expenses by category
let summary = categorizedData.reduce((acc, record) => {
  acc[record.Category] = (acc[record.Category] || 0) + Math.abs(parseFloat(record.Amount));
  return acc;
}, {});

// Calculate percentage distribution
let totalAmount = Object.values(summary).reduce((acc, value) => acc + value, 0);
const summaryPercentages = Object.fromEntries(
  Object.entries(summary).map(([category, total]) => [category, ((total / totalAmount) * 100).toFixed(2)])
);

// Render a chart
radialChart({
  series: Object.values(summaryPercentages),
  labels: Object.keys(summaryPercentages),
  title: 'Monthly Expense Breakdown',
});
```
