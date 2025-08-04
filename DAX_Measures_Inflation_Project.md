# DAX Measures – Inflation Project

## Table: countries

**Total Countries**
```DAX
DISTINCTCOUNT(countries[CountryName])
```

**High Risk Countries**
```DAX
CALCULATE(
    DISTINCTCOUNT(countries[CountryName]),
    FILTER(food_price_index, food_price_index[YoY_Food_Inflation] > 15),
    FILTER(inflation, inflation[InflationRate] > 10)
)
```

**IsHighRisk**
```DAX
VAR foodRisk = CALCULATE(
    MAX(food_price_index[YoY_Food_Inflation])
)
VAR inflRisk = CALCULATE(
    MAX(inflation[InflationRate])
)
RETURN
IF(foodRisk > 15 && inflRisk > 10, 1, 0)
```

---

## Table: inflation

**Average Total Inflation**
```DAX
AVERAGE(inflation[InflationRate])
```

**Avg Inflation 2015–2024**
```DAX
CALCULATE(
    AVERAGE(inflation[InflationRate]),
    FILTER(
        inflation,
        inflation[Year] >= 2015 && inflation[Year] <= 2024
    )
)
```

---

## Table: food_price_index

**Highest YoY Food Inflation**
```DAX
MAX(food_price_index[YoY_Food_Inflation])
```

**Top Inflation Country**
```DAX
VAR MaxValue = CALCULATE(MAX(food_price_index[YoY_Food_Inflation]))
VAR Result = 
    SELECTCOLUMNS(
        FILTER(
            food_price_index,
            food_price_index[YoY_Food_Inflation] = MaxValue
        ),
        "Info",
        food_price_index[CountryName] & 
        " – " & 
        FORMAT(MaxValue, "0") & "%" & 
        " (" & food_price_index[Year] & ")"
    )
RETURN
CONCATENATEX(Result, [Info], ", ")
```
