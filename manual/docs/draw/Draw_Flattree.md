### DRAW_FLATTREE


```sql
SELECT 'RU' as country,'MOS' as city,12 as valueLink,32 as countryValue,50 as cityValue
UNION ALL
SELECT 'RU' as country,'NOV' as city,112 as valueLink,32 as countryValue,12 as cityValue
UNION ALL
SELECT 'RU' as country,'SPB' as city,238 as valueLink,32 as countryValue,30 as cityValue
UNION ALL
SELECT 'RU' as country,'SCH' as city,8 as valueLink,32 as countryValue,10 as cityValue

DRAW_FLATTREE
{
    path:'country.city.valueLink',
}

```


![tabix draw tree](/img/DRAW_FLATTREE/DrawFlatTree1.png)


### Custom render

```sql


DRAW_FLATTREE
{
    path:'country.city.valueLink',

    layout: 'radial',
    symbol: 'emptyCircle',
    symbolSize: 7
}


```


![tabix draw tree](/img/DRAW_FLATTREE/DrawFlatTree1-radial.png)


```sql
DRAW_FLATTREE
{
    path:'country.city.valueLink',
    symbol: 'emptyCircle',
    orient: 'vertical',

}
```
![tabix draw tree vertical](/img/DRAW_FLATTREE/DrawFlatTree1-vertical.png)


Echart Docs

http://echarts.baidu.com/examples/editor.html?c=tree-basic

https://ecomfe.github.io/echarts-doc/public/en/option.html#series-tree