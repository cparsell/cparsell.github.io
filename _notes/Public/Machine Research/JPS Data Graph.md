---
title: JPS Data Graph
feed: show
date: 2023-08-31
permalink: /jpsdatagraph
tags: advancedlab, data, jacobs, jps, jpsdata
---


```dataviewjs
const rawData = await dv.query(`
	TABLE 
	markforged, form3, fortus, objet 
	WHERE file.name = "JPS-APL Submission Data Fall 2022"
`);
const rows = rawData.value.values;
const labels = rawData.value.headers.splice(1,rawData.value.headers.length);
let vals = rows[0].splice(1, rows[0].length);
//console.log(labels);
//console.log(vals);
let data = new Array;
for (let j=0;j<labels.length;j++) {
	let newkey = labels[j];
	let newObj = {};
	newObj['data.key'] = labels[j];
	newObj['data.value'] = vals[j];
	
	data.push(newObj);
}
//console.log(data);
const chartData = {
    type: 'bar',
    labels: vals,
    data: {
        
        datasets: [
            {
	            
	            data: data,
	            backgroundColor: ['#f38ba8', '#f9e2af', '#94e2d5', '#b4befe'],
            },
            
        ],
    },
    options: {
	    parsing: {
	      xAxisKey: 'data\\.key',
	      yAxisKey: 'data\\.value'
	    }
	}
}

window.renderChart(chartData, this.container);
```

[Charts.js](https://www.chartjs.org/docs/latest/general/data-structures.html)

```dataviewjs
const rawData = await dv.query(`
	TABLE 
	markforged, form3, fortus, objet 
	WHERE file.name = "JPS-APL Submission Data Fall 2022"
`);
const rows = rawData.value.values;
const labels = rawData.value.headers.splice(1,4);
let spliced = rows[0].splice(1, 4);
//console.log(labels);
//console.log(spliced);
//console.log(rows.map(x => x[1]));
const chartData = {
    type: 'bar',
    data: {
        labels: spliced,
        datasets: [
            {
	            label: 'Markforged', 
	            data: spliced[0],
	            backgroundColor: ['#2D3142']
            },
            {
	            label: 'Form3', 
	            data: spliced[1],
	            backgroundColor: ['#EF3054']
	        },
            {
	            label: 'Fortus', 
	            data: spliced[2], 
	            backgroundColor: ['#43AA8B']},
            {
	            label: 'Objet', 
	            data: spliced[3],
	            backgroundColor: ['#C7F2A7'],
	        },
        ],
    },
}

window.renderChart(chartData, this.container);
```


