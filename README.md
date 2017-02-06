# Plotting Loan Data in Python using Plotly-D3
Here I am showing total loan amount from each state in US

##Output: [Plotly](https://plot.ly/~mantejsingh/88/most-calamities-hover-for-details/)
[![screenshot_1486397265.png](https://s19.postimg.org/f5rvks3lf/screenshot_1486397265.png)](https://postimg.org/image/gktg9i4of/)


## Converting 'float' loan type to Dollar '$' loan type in dataset
```
df['Borrow_Amount'] = df['Borrow_Amount'].map('${:,.2f}'.format)
```


### Before:
[![screenshot_1486397751.png](https://s19.postimg.org/ma9ottaur/screenshot_1486397751.png)](https://postimg.org/image/l7zib9s1b/)

### After:
[![screenshot_1486397783.png](https://s19.postimg.org/az715g3zn/screenshot_1486397783.png)](https://postimg.org/image/jhgh9sai7/)



## Setting data on Map
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
