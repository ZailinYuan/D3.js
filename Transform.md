# Transform
### Get transform information of a node
The matrix 'e' and 'f' property is the x, y we need.
```javascript
      svg
          .select('.axis-x')
          .selectAll('.tick')
          .attr('transform', function() {
              let t = this.transform.baseVal.consolidate().matrix
              return `translate(${t.e}, ${t.f + 0.5})`
          })
```
