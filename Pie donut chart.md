# Pie charts
```javascript
    const svgRef = useRef()

    useEffect(() => {
        let data = [
            {
                value: 1,
                label: 'Bill',
                color: 'red',
            },
            {
                value: 2,
                label: 'Toma',
                color: 'yellow',
            }
        ]
        
        let set = {
            'Bill': '#FE7B1A',
            'Toma': 'rgba(217,57,84,0.5)',
        }

        const svg = d3.select(svgRef.current)
        let g = svg.select('.pie')
            .attr('transform', `translate(150, 150)`)
        let arc = d3.arc()
            .innerRadius(50)
            .outerRadius(100)
        console.log(arc)
        let pie = d3.pie()
            .value(d => d.value)(data)
        console.log(pie)
        g.selectAll('path')
            .data(pie)
            .enter()
            .append('path')
            .attr('d', arc)
            .style('fill', d => set[d.data.label])
        g.selectAll('text')
            .data(pie)
            .enter()
            .append('text')
            .text(d => d.data.label)
            .attr('transform', d => `translate(${arc.centroid(d)})`)
            .attr('text-anchor', 'middle')

        let titleG = svg.select('.title')
            .attr('transform', 'translate(80, 20)')
        titleG.append('text')
            .datum(['Ongoing Cost Breakup'])
            .text(d => d)


        let legendData = [
            {
                label: 'Total Ongoing Capital Benefits',
                y: 0
            },
            {
                label: 'Total Ongoing O&M Cost',
                y: 30
            }
        ]
        let tagsG = svg.select('.tags')
            .attr('transform', 'translate(20, 300)')
        tagsG.selectAll('circle')
            .data(legendData)
            .enter()
            .append('circle')
            .attr('cx', 20)
            .attr('cy', d => d.y)
            .attr('r', 5)
            .style('fill', 'yellow')

        tagsG.selectAll('text')
            .data(legendData)
            .enter()
            .append('text')
            .attr('transform', d => `translate(25, ${d.y})`)
            .text(d => d.label)
```
