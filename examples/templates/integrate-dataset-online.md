# 📈 Chart a CSV

Turn **real-world data** into a chart — directly inside your Markdown note.
In this example, we’ll fetch a public CSV dataset, save it locally, and visualize it in seconds.


## 🔹 Step 1 — Load the Data
This snippet loads a public dataset (World GDP by country), converts it from CSV to JSON,
and saves it as a local file for later use.

```js 
const url = 'https://raw.githubusercontent.com/plotly/datasets/master/2014_world_gdp_with_codes.csv';
const csvText = await fetch(url).then(r => r.text());
const json = await csvJSON(csvText, ',');
//print(csvText);
//printJSON(json)
//showDatagrid({data: json, pagination: true});

_fs.writeFileSync(__dirname + "/world_gdp-dataset.json", JSON.stringify(json));
print("✅ Dataset saved locally as 'world_gdp-dataset.json'");
```


## 🔹 Step 2 — Create a Bar Chart
Now, let’s load our local dataset and display the Top 10 countries by GDP as a bar chart.

```js 
const data = require("./world_gdp-dataset.json");

// Select top 10 countries by GDP
const top10 = data
  .sort((a, b) => parseFloat(b["GDP (BILLIONS)"]) - parseFloat(a["GDP (BILLIONS)"]))
  .slice(0, 10);

// Prepare chart data
const categories = top10.map(e => e.COUNTRY);
const series = toSeries({
    data: top10, 
    x: "COUNTRY", 
    y: "GDP (BILLIONS)"
});

// Render chart
barChart({
  title: "Top 10 Countries by GDP (2014)",
  horizontal: false,
  series: series,
  categories: categories
});
```

- ✅ Instant insight from public data
- ✅ No external tools required — just Markdown + Znote
- ✅ 100% local execution — your data stays private
