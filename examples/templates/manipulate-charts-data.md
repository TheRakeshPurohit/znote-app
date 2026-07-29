# 📊 Chart Any JSON

Znote provides powerful tools to visualize and manipulate data using various chart types and SQL-based queries.


## 📈 Available Charts

### 📊 Bar Chart
```js
barChart({
  horizontal: false,
  series: [
    {name: 'PRODUCT A', data: [14, 25, 21, 17, 12, 13, 11, 19]},
    {name: 'PRODUCT B', data: [13, 23, 20, 8, 13, 27, 33, 12]},
    {name: 'PRODUCT C', data: [11, 17, 15, 15, 21, 14, 15, 13]}],
  categories:['2011 Q1', '2011 Q2', '2011 Q3', '2011 Q4', '2012 Q1', '2012 Q2', '2012 Q3', '2012 Q4']
});
```

### 📉 Line Chart
```js 
lineChart({
  series: [
    {name: 'Music', data: [1, 15, 26, 20, 33, 27]},
    {name: 'Photos', data: [3, 33, 21, 42, 19, 32]},
    {name: 'Files', data: [0, 39, 52, 11, 29, 43]}],
  labels: ['01/15/2002', '01/16/2002', '01/17/2002', '01/18/2002', '01/19/2002', '01/20/2002']
});
```

### 📊 Area Chart
```js 
areaChart({
  series: [
    {name: 'Music', data: [11, 15, 26, 20, 33, 27]},
    {name: 'Photos', data: [32, 33, 21, 42, 19, 32]},
    {name: 'Files', data: [20, 39, 52, 11, 29, 43]}],
  categories:['2011 Q1', '2011 Q2', '2011 Q3', '2011 Q4', '2012 Q1', '2012 Q2']
});
```

### 🎈 Bubble Chart
```js 
bubbleChart({
  series: [
    {'name': 'Serie 1', 'data': [['2024-02-20',1,1], ['2024-02-24',1,1], ['2024-02-26',1,2]]},
    {'name': 'Serie 2', 'data': [['2024-02-21',2,1], ['2024-02-22',2,2], ['2024-02-23',2,1]]},
    {'name': 'Serie 3', 'data': [['2024-02-21',3,1], ['2024-02-22',3,1]]}
  ]
});
```

### 🎯 Radial Chart
```js 
radialChart({series: [71, 63, 77], labels:['June', 'May', 'April']});
```


## 🔄 Data Manipulation

### 📌 From SQL

**Example: Retrieving sales data by month**
```sql blockName=orders-sql;
SELECT
  channel,
  DATE_FORMAT(sale_date, '%Y-%m') AS month,
  COUNT(*) AS total_sales
FROM Sales
GROUP BY channel, month
ORDER BY month ASC;
```

```js 
// Convert SQL query result to JSON (Replace `loadBlock` with actual implementation)
const json = [
  {'channel': 'Facebook', 'month': '2023-01', 'total_sales': 150},
  {'channel': 'Facebook', 'month': '2023-02', 'total_sales': 113},
  {'channel': 'Facebook', 'month': '2023-03', 'total_sales': 83},
  {'channel': 'Facebook', 'month': '2023-04', 'total_sales': 193},
  {'channel': 'Google', 'month': '2023-01', 'total_sales': 235},
  {'channel': 'Google', 'month': '2023-02', 'total_sales': 195},
  {'channel': 'Google', 'month': '2023-03', 'total_sales': 125},
  {'channel': 'Google', 'month': '2023-04', 'total_sales': 155}
];

// Extract unique months
const categories = Array.from(new Set(json.map(e => e.month)));

// Convert data to chart format
const series = toSeries({data: json, x: "month", y: "total_sales", category: "channel"});

barChart({
  horizontal: true,
  series: series,
  categories: categories
});
```

### 📌 Formatting Axis Labels
```js 
const formatterOptions = {
  yaxis: {
    labels: {
      formatter: function (value) {
         const date = new Date();
        date.setMonth(value - 1);
        return date.toLocaleString('en-US', { month: 'short' });
      }
    },
  },
  xaxis: {
    labels: {
      formatter: function (value) {
        return value.toLocaleString('en-US', { style: 'currency', currency: 'USD' });
        return value;
      }
    },
  }
}

const json = [
  {'channel': 'Facebook', 'month': '2023-01', 'total_sales_amount': 15000.00},
  {'channel': 'Facebook', 'month': '2023-02', 'total_sales_amount': 11300.00},
  {'channel': 'Facebook', 'month': '2023-03', 'total_sales_amount': 8300.00},
  {'channel': 'Facebook', 'month': '2023-04', 'total_sales_amount': 19300.00},
  {'channel': 'Google', 'month': '2023-01', 'total_sales_amount': 23500.00},
  {'channel': 'Google', 'month': '2023-02', 'total_sales_amount': 19500.00},
  {'channel': 'Google', 'month': '2023-03', 'total_sales_amount': 12500.00},
  {'channel': 'Google', 'month': '2023-04', 'total_sales_amount': 15500.00}
];

barChart({
  options: formatterOptions,
  horizontal: true,
  series: toSeries({
    data:json, 
    x:"month", 
    y:"total_sales_amount", 
    category:"channel"
    })
});
```

### 📌 Bubble Chart with Custom Labels
```js 
let json = [
  {'date':'2024-02-20','mood':1},
  {'date':'2024-02-21','mood':2},
  {'date':'2024-02-21','mood':3},
  {'date':'2024-02-22','mood':2},
  {'date':'2024-02-22','mood':3},
  {'date':'2024-02-22','mood':2},
  {'date':'2024-02-23','mood':2},
  {'date':'2024-02-24','mood':1},
  {'date':'2024-02-26','mood':1},
  {'date':'2024-02-26','mood':1}
];

const xFormatter = value => ['☀️', '⛅️', '☁️', '🌧️', '⛈️'][value] || '';
const serieFormatter = value => ['Good', 'Almost Good', "It's ok", 'I saw better', 'Should be better'][value] || '';

bubbleChart({
  options: { yaxis: { labels: { formatter: xFormatter } } },
  series: toBubbleSeries({data: json, x:'date', y:'mood', serieFormatter: serieFormatter})
});
```

### For Timeseries
```js 
const json = [
  {"sensor": 74, "date": "2022-09-29 10:41:54.000000 +02:00", "battery": 90.92},
  {"sensor": 74, "date": "2023-06-21 10:14:59.000000 +02:00",  "battery": 88.76},
  {"sensor": 74, "date": "2023-08-24 20:34:20.000000 +02:00", "battery": 88.08},
  {"sensor": 60, "date": "2023-04-22 20:34:20.000000 +02:00", "battery": 78.02},
  {"sensor": 60, "date": "2023-07-24 20:34:20.000000 +02:00", "battery": 75.02}
]

lineChart({
  options: {
    xaxis: {
      type: "datetime",
    },
  },
  series: toTimeSeries({data:json, x:"date", y:"battery", category:"sensor"})
});
```


## 📂 Data from JSON

### 🛠 Filter/Exclude Keys
```js 
const json = [
  {'id': 1, 'channel': 'Facebook', 'month': '2023-01', 'total_sales': 150},
  {'id': 2, 'channel': 'Referral', 'month': '2023-01', 'total_sales': 193}
];

// Exclude 'id' and 'month'
printJSON(exclude(json, ['id', 'month']));

// Keep only 'channel' and 'month'
printJSON(filter(json, ['channel', 'month']));
```

### 🔄 CSV to JSON
```js 
const csv = 
`latitude,longitude,brightness\n
-3.22,-39.51,323\n
-3.21,-39.49,306.1\n`;
const json = csvJSON(csv, ',');
printJSON(json);
```

### 🔄 Flatten JSON for DataGrid
```js 
const json = [
  { "party": "Democrat", "person": { "firstname": "Maria", "lastname": "Cantwell" } },
  { "party": "Republican", "person": { "firstname": "John", "lastname": "Barrasso" } }
];

const flattenJSON = json.map(e => flatten(e));
printJSON(flattenJSON);
```

### 📊 Display Data in a Datagrid
```js 
const r = await fetch('https://www.govtrack.us/api/v2/role?current=true&role_type=senator');
const json = await r.json();
const senators = json.objects.map(s => flatten(s));
showDatagrid({ data: filter(senators, ['party', 'person.firstname', 'person.lastname']), pagination: true });
```
