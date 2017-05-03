# Background
[Albebraic Visualization, Jupyter notebook demos](https://github.com/quiltdata/algebraic-vis).

# Vision
Create an open-source semantic debugger for visualizations that helps designers to create more accurate visualization in D3 through exploratory debugging of confusers, hallucinators, and other measurable distortions in visualization. One feature would be to exlpore a variety of alpha functions for a given visualization through small multiples.

# Informal napkin sketch
* Automate discovery of confusers, hallucinators, and other algebraic propertes of visualizations
* Method: d3 users will integrate against an algebraic visualization library and will access the parameters of their visualization
through an interface that allows the present library to interpose various alpha functions and provoke semantic bugs:

Unfinished code sample (entertainment purposes only):
```javascript
// BEFORE: D3 usage
var line = d3.line()
    .x(function(d) { return x(d.date); }) // x is an x scale defined elsewhere
    .y(function(d) { return y(d.value); }); // y is an y scale defined elsewhere

// AFTER (proposed)
var alg = AlgVis();

var dateAccessor = alg.makeAccessor(function(d) { return d.date; });
var valueAccessor = alg.makeAccessor(function(d) { return d.value; });

var lineNew = d3.line()
    .x(function(d) { return x(dateAccessor(d)); }) // x is an x scale defined elsewhere
    .y(function(d) { return y(valueAccessor(d)); }); // y is an y scale defined elsewhere

// d3 use patterns
// "static" data, myArray doesn't change
d3.selectAll("circle")
    .data(myArray)
    .enter()
    .append("circle")
    .attr("r", function(d) { return valueAccessor(d) * 5; });

// dynamic data
d3.selectAll("circle")
    .data(myArray, function(d) { return keyAccessor(d); })
    .enter()
    .append("circle")
    .attr("r", function(d) { return valueAccessor(d) * 5; });
```



