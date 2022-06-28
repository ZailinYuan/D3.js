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

### Axis example with axis shift
```javascript
const svgRef = useRef()
    const width = 750, height = 500
    const margin = {
        top: 50,
        bottom: 50,
        left: 40,
        right: 40,
    }

    const formatCurrencyX = value => {
        if(value < 0) {
            return `-$${-value}`
        } else if(value === 0) {
            return ''
        } else {
            return `$${value}`
        }
    }

    const formatCurrencyY = value => {
        if(value < 0) {
            return `-$${-value}`
        } else {
            return `$${value}`
        }
    }

    useEffect(() => {
        const svg = d3.select(svgRef.current)
        const scaleX = d3.scaleLinear()
            .domain([0, 100])
            .nice()
            .range([margin.left, width-margin.right])
            .nice()
        const scaleY = d3.scaleLinear()
            .domain([-10, 50])
            .nice()
            .range([height - margin.bottom, margin.top])
            .nice()
        const axisX = d3
            .axisBottom(scaleX)
            .tickFormat(formatCurrencyX)
            .ticks(5)
            .tickSize(-(height - margin.top - margin.bottom))
            .tickSizeOuter(0)
            .tickPadding(8)
        const axisY = d3
            .axisLeft(scaleY)
            .tickFormat(formatCurrencyY)
            .ticks(5)
            .tickSize(-(width - margin.left - margin.right))
            .tickSizeOuter(0)
            .tickPadding(8)
        const gX = svg
            .append('g')
            .attr('class', 'axis-x')
            // .attr('transform', `translate(0, ${scaleY(0)})`)
            .attr('transform', `translate(0, ${height - margin.bottom - (scaleY(-10) - scaleY(0))})`)
            .call(axisX)
            .select('.axis-x path')
            .style('stroke-width', '1.5')
            .style('color', 'black')
        const gY = svg
            .append('g')
            .attr('class', 'axis-y')
            .attr('transform', `translate(${margin.left}, ${0})`)
            .call(axisY)
            .select('.axis-y path')
            .style('stroke-width', '0')
        svg
            .select('.axis-x')
            .selectAll('.tick line')
            .style('color', '#808080')
            .style('stroke-width', '0.5')
            .attr('transform', `translate(0, ${scaleY(-10) - scaleY(0)})`)
        svg
            .select('.axis-y')
            .selectAll('.tick line')
            .style('color', '#808080')
            .style('stroke-width', '0.5')
```
