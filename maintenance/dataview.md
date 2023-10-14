```dataview
LIST title
WHERE contains(file.tags, "#solution")
SORT file.name asc
```

```dataview
TABLE (length(rows)-1) as solved, (length(rows)-1)/2898*100 as percent
WHERE contains(file.tags, "#solution")
SORT file.name asc
GROUP BY true
```

