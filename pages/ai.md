---
layout: default
---

# AI

<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>

<div id="irisChart"></div>

<script>
    // Iris dataset
    const data = [{
        x: [5.1, 4.9, 4.7, 4.6, 5.0, 5.4, 4.6, 5.0, 4.4, 4.9],
        y: [3.5, 3.0, 3.2, 3.1, 3.6, 3.9, 3.4, 3.4, 2.9, 3.1],
        mode: 'markers',
        type: 'scatter',
        name: 'Setosa',
        marker: {
            size: 12,
            color: 'red'
        }
    },
    {
        x: [7.0, 6.4, 6.9, 5.5, 6.5, 5.7, 6.3, 4.9, 6.6, 5.2],
        y: [3.2, 3.2, 3.1, 2.3, 2.8, 2.8, 3.3, 2.4, 2.9, 2.7],
        mode: 'markers',
        type: 'scatter',
        name: 'Versicolor',
        marker: {
            size: 12,
            color: 'blue'
        }
    },
    {
        x: [6.3, 5.8, 7.1, 6.3, 6.5, 7.6, 4.9, 7.3, 6.7, 7.2],
        y: [3.3, 2.7, 3.0, 2.9, 3.0, 3.0, 2.5, 2.9, 3.1, 3.6],
        mode: 'markers',
        type: 'scatter',
        name: 'Virginica',
        marker: {
            size: 12,
            color: 'green'
        }
    }];

    const layout = {
        title: 'Iris Dataset - Sepal Length vs Width',
        xaxis: {
            title: 'Sepal Length (cm)'
        },
        yaxis: {
            title: 'Sepal Width (cm)'
        }
    };

    Plotly.newPlot('irisChart', data, layout);
</script>

[back](../) 