# 关于创建和使用 Axis
### Create Axis
The process of drawing charts with axis:
```javascript
  // Create 'Scale'
   const scaleX = d3.scaleLinear()
      .domain([0, 100])
      .nice()
      .range([margin.left, width-margin.right])
      .nice()
  // Create 'Axis'
  const axisX = d3
      .axisBottom(scaleX)
      
  // Append axis to svg
  const gX = svg
      .append('g')
      .attr('class', 'axis-x')
      .attr('transform', `translate(0, ${height - margin.bottom - margin.top})`)
      .call(axisX)
```
Always calculate scale dynamically to fit the whole chart in the viewbox. Below is the margin config.
```javascript
    const width = 500, height = 300
    const margin = {
        top: 10,
        bottom: 40,
        left: 45,
        right: 20,
    }
```
```html
<svg overflow="scroll" viewBox="0, 0, 500, 300" ref={svgRef}></svg>
```

### Axis options:
##### Ticks
```javascript
  const axisX = d3
      .axisBottom(scaleX)
      .tickFormat(formatCurrency)
      .ticks(5)
```
tickFormat is how to display axis tick label. ticks is how many ticks displayed. See more ticks on google.

    .tickSize(3)
