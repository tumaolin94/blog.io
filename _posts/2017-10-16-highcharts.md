---
layout: post
title: Basic Use of Highcharts 
date: 2017-10-16
categories: blog
tags: [WEB, JavaScript]
description: 

---

Bascially, acording to the tutorial of [official document](https://www.highcharts.com/docs/getting-started/installation), you can study how to study this useful tool easily. 

in Chapter [Your first chart](https://www.highcharts.com/docs/getting-started/your-first-chart), you can use two way to implement your chart.

- With jQuery 

```
<script>
$(function () { 
    var myChart = Highcharts.chart('container', {
        chart: {
            type: 'bar'
        },
        title: {
            text: 'Fruit Consumption'
        },
        xAxis: {
            categories: ['Apples', 'Bananas', 'Oranges']
        },
        yAxis: {
            title: {
                text: 'Fruit eaten'
            }
        },
        series: [{
            name: 'Jane',
            data: [1, 0, 4]
        }, {
            name: 'John',
            data: [5, 7, 3]
        }]
    });
});
</script>
```

In order to use it, you have to add jQuery at first in tag <head>.
```
<head>
<script src="http://code.highcharts.com/highcharts.js"></script>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
</head>
```

- Without jQuery

after version 4.x, highcharts did not depend on jQuery any longer, so you can use it independently.
Here is a example
```
var chart1; // globally available
$(function() {
       chart1 = Highcharts.stockChart('container', {
         rangeSelector: {
            selected: 1
         },
         series: [{
            name: 'USD to EUR',
            data: usdtoeur // predefined JavaScript array
         }]
      });
   });
```

Notice: you must include the code above in a tag<script>, or it does not work.
