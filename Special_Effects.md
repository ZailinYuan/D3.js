# Shadow effect
```javascript
        // Shadow effect
        const defs = svg.append("defs");

        const filter = defs.append("filter")
            .attr("id", "dropshadow")
        
        filter.append("feGaussianBlur")
            .attr("in", "SourceAlpha")
            .attr("stdDeviation", 1)
            .attr("result", "blur");
        filter.append("feOffset")
            .attr("in", "blur")
            .attr("dx", 0.5)
            .attr("dy", 0.5)
            .attr("result", "offsetBlur");
        
        const feMerge = filter.append("feMerge");
        
        feMerge.append("feMergeNode")
            .attr("in", "offsetBlur")
        feMerge.append("feMergeNode")
            .attr("in", "SourceGraphic");
            
        svg
            .append('rect')
            .attr('filter', 'url(#dropshadow)')
```
