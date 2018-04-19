## GRAPH


![Tabix DRAW_GRAPH](/img/DRAW_GRAPH/DRAW_GRAPH_only.png)


```sql
SELECT 'RU' as country,'MOS' as city,12 as valueLink,32 as countryValue,50 as cityValue
UNION ALL
SELECT 'RU' as country,'NOV' as city,112 as valueLink,32 as countryValue,12 as cityValue
UNION ALL
SELECT 'RU' as country,'SPB' as city,238 as valueLink,32 as countryValue,30 as cityValue
UNION ALL
SELECT 'RU' as country,'SCH' as city,8 as valueLink,32 as countryValue,10 as cityValue

DRAW_GRAPH
{
    path:'country.valueLink.city'
}
```


Path : `[FromNode].[ValueConnect].[DestNode]`




```sql
SELECT 'RU' as country,'MOS' as city,12 as valueLink,32 as countryValue,50 as cityValue
UNION ALL
SELECT 'RU' as country,'NOV' as city,112 as valueLink,32 as countryValue,12 as cityValue
UNION ALL
SELECT 'RU' as country,'SPB' as city,238 as valueLink,32 as countryValue,30 as cityValue
UNION ALL
SELECT 'RU' as country,'SCH' as city,8 as valueLink,32 as countryValue,10 as cityValue

DRAW_GRAPH
{
    path:'country.valueLink.city',
    layout:'force',
    targetValue:'cityValue',
    sourceValue:'countryValue'
}
```


![Tabix DRAW_GRAPH](/img/DRAW_GRAPH/DRAW_GRAPH_values.png)

## Layout

* 'circular' Adopt circular layout
* 'force' Adopt force-directed layout

```sql
DRAW_GRAPH
{
    path:'cntr.value.city',
    layout:'force'
}
```

## Arrow

edgeSymbol = [Array, string ]

[ default: ['none', 'none'] ]

Symbol of two ends of edge line.

```sql


DRAW_GRAPH
{
    path:'country.valueLink.city',
    layout:'force',
    edgeSymbol:['circle', 'arrow']
}


DRAW_GRAPH
{
    path:'country.valueLink.city',
    layout:'force',
    edgeSymbol:'arrow'
}


```

## Direct code Echarts

```sql


DRAW_GRAPH
{
    path:'country.valueLink.city',
    layout:'force',
    targetValue:'cityValue',
    sourceValue:'countryValue',
    raw:{
        series:[
                {
                    edgeSymbol:'arrow',
                    edgeSymbolSize:40,
                    label:{show:true},
                    lineStyle:{
                        type:'dotted',
                        width:40,
                        shadowColor: 'rgba(0, 0, 0, 0.5)',
                        shadowBlur: 10
                    }

                }
        ]

    }
}

```

## Echart Doc

https://ecomfe.github.io/echarts-doc/public/en/option.html#series-graph

