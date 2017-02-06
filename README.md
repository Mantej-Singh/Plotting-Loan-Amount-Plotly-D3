# Plotting Loan Data in Python using Plotly-D3
Here I am showing total loan amount from each state in US

##Output1: [Choropleth Map](https://plot.ly/~mantejsingh/90/_2016-us-borrowed-loan-amount-by-state-hover-for-breakdown/)
[![screenshot_1486397265.png](https://s19.postimg.org/f5rvks3lf/screenshot_1486397265.png)](https://postimg.org/image/gktg9i4of/)


## Converting 'float' loan type to Dollar '$' loan type in dataset
```
df['Borrow_Amount'] = df['Borrow_Amount'].map('${:,.2f}'.format)
```

### Before:
[![screenshot_1486397751.png](https://s19.postimg.org/ma9ottaur/screenshot_1486397751.png)](https://postimg.org/image/l7zib9s1b/)

### After:
[![screenshot_1486397783.png](https://s19.postimg.org/az715g3zn/screenshot_1486397783.png)](https://postimg.org/image/jhgh9sai7/)


## Setting data on Choropleth Map
```
data = [ dict(
        type='choropleth',
        colorscale = scl,
        autocolorscale = False,
        locations = df['Code'],
        z = df['Borrow_Amount'].replace('[\$,]','',regex=True).astype(float),
        locationmode = 'USA-states',
        text = df['text'],
        marker = dict(
            line = dict (
                color = 'rgb(255,255,255)',
                width = 2
            ) ),
        colorbar = dict(
            title = "Millions USD")
        ) ]
```


-------------------------------------------------------------------------------------------------------------------------------\

##Output2: [Bubble Map](https://plot.ly/~mantejsingh/92/_2016-us-borrowed-loan-amount-by-state-in-millons-click-legend-to-toggle-traces/)

[![screenshot_1486411054.png](https://s19.postimg.org/3pz8rytkj/screenshot_1486411054.png)](https://postimg.org/image/ff38fxkj3/)


## Setting data on Bubble Map
```
colors = ["rgb(255,65,54)","rgb(133,20,75)","rgb(255,133,27)","#006064","rgb(0,116,217)","#d50000","#263238"]
cases = []
for i in range(len(types)):
    df_sub = top_borrowers.loc[top_borrowers.Buckets==types[i],:]
    cases.append(go.Scattergeo(
            locationmode = 'USA-states',
            lon = df_sub['Longitude'],
            lat = df_sub['Latitude'],
            text = df_sub['text'],
            name = types[i] + ' Millions : '+str(len((df_sub))),
            marker = dict(
            size = df_sub['Borrow_Amount'].replace('[\$,]','',regex=True).astype(float)/20000,
            color = colors[i],
            line = dict(width=0.5, color='rgb(40,40,40)'),
            sizemode = 'area'
                )
            ))
```
