---
jupyter:
  celltoolbar: Slideshow
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.13.2
  nbformat: 4
  nbformat_minor: 5
---

::: {#6080af38 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
# Data visualization in Python (`pyplot`)
:::

::: {#11847bd1 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Looking ahead: April, Weeks 1-2

-   In April, weeks 1-2, we\'ll dive deep into **data visualization**.
    -   How do we make visualizations in Python?
    -   What principles should we keep in mind?
:::

::: {#118f7491 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Goals of this exercise

-   What *is* data visualization and why is it important?
-   Introducing `matplotlib`.
-   Univariate plot types:
    -   **Histograms** (univariate).
    -   **Scatterplots** (bivariate).
    -   **Bar plots** (bivariate).
:::

::: {#a88245b5 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Introduction: data visualization
:::

::: {#b7f84929 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### What is data visualization?

[Data visualization](https://en.wikipedia.org/wiki/Data_visualization)
refers to the process (and result) of representing data graphically.

For our purposes today, we\'ll be talking mostly about common methods of
**plotting** data, including:

-   Histograms\
-   Scatterplots\
-   Line plots
-   Bar plots
:::

::: {#82767865 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Why is data visualization important?

-   Exploratory data analysis
-   Communicating insights
-   Impacting the world
:::

::: {#01291136 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Exploratory Data Analysis: Checking your assumptions

[Anscombe\'s
Quartet](https://en.wikipedia.org/wiki/Anscombe%27s_quartet)

![title](img/anscombe.png)
:::

::: {#7685a9c9 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Communicating Insights

[Reference: Full Stack
Economics](https://fullstackeconomics.com/18-charts-that-explain-the-american-economy/)

![title](img/work.png)
:::

::: {#dc0e5af8 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Impacting the world

[Florence
Nightingale](https://en.wikipedia.org/wiki/Florence_Nightingale)
(1820-1910) was a social reformer, statistician, and founder of modern
nursing.

![title](img/polar.jpeg)
:::

::: {#b3b3a54a .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Impacting the world (pt. 2) {#impacting-the-world-pt-2}

[John Snow](https://en.wikipedia.org/wiki/John_Snow) (1813-1858) was a
physician whose visualization of cholera outbreaks helped identify the
source and spreading mechanism (water supply).

![title](img/cholera.jpeg)
:::

::: {#007f08c5 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Introducing `matplotlib`
:::

::: {#9f43d118 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Loading packages

Here, we load the core packages we\'ll be using.

We also add some lines of code that make sure our visualizations will
plot \"inline\" with our code, and that they\'ll have nice, crisp
quality.
:::

::: {#f741468f .cell .code execution_count="2" slideshow="{\"slide_type\":\"-\"}"}
``` python
import numpy as np 
import pandas as pd
import matplotlib.pyplot as plt
import scipy.stats as ss
```
:::

::: {#e953a2d8 .cell .code execution_count="3" slideshow="{\"slide_type\":\"-\"}"}
``` python
%matplotlib inline 
%config InlineBackend.figure_format = 'retina'
```
:::

::: {#58bac002 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### What is `matplotlib`?

> [`matplotlib`](https://matplotlib.org/) is a **plotting library** for
> Python.

-   Many [tutorials](https://matplotlib.org/stable/tutorials/index.html)
    available online.\
-   Also many [examples](https://matplotlib.org/stable/gallery/index) of
    `matplotlib` in use.

Note that [`seaborn`](https://seaborn.pydata.org/) (which we\'ll cover
soon) uses `matplotlib` \"under the hood\".
:::

::: {#97736c27 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### What is `pyplot`?

> [`pyplot`](https://matplotlib.org/stable/tutorials/introductory/pyplot.html)
> is a collection of functions *within* `matplotlib` that make it really
> easy to plot data.

With `pyplot`, we can easily plot things like:

-   Histograms (`plt.hist`)
-   Scatterplots (`plt.scatter`)
-   Line plots (`plt.plot`)
-   Bar plots (`plt.bar`)
:::

::: {#e24bb132 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Example dataset

Let\'s load our familiar Pokemon dataset, which can be found in
`data/pokemon.csv`.
:::

::: {#0e29033e .cell .code execution_count="20" slideshow="{\"slide_type\":\"-\"}"}
``` python
df_pokemon = pd.read_csv("data/pokemon.csv")
df_pokemon.head(10)
```

::: {.output .execute_result execution_count="20"}
``` json
{"columns":[{"name":"index","rawType":"int64","type":"integer"},{"name":"#","rawType":"int64","type":"integer"},{"name":"Name","rawType":"object","type":"string"},{"name":"Type 1","rawType":"object","type":"string"},{"name":"Type 2","rawType":"object","type":"unknown"},{"name":"Total","rawType":"int64","type":"integer"},{"name":"HP","rawType":"int64","type":"integer"},{"name":"Attack","rawType":"int64","type":"integer"},{"name":"Defense","rawType":"int64","type":"integer"},{"name":"Sp. Atk","rawType":"int64","type":"integer"},{"name":"Sp. Def","rawType":"int64","type":"integer"},{"name":"Speed","rawType":"int64","type":"integer"},{"name":"Generation","rawType":"int64","type":"integer"},{"name":"Legendary","rawType":"bool","type":"boolean"}],"conversionMethod":"pd.DataFrame","ref":"162cce79-0b1e-4328-809b-fb47c0df905f","rows":[["0","1","Bulbasaur","Grass","Poison","318","45","49","49","65","65","45","1","False"],["1","2","Ivysaur","Grass","Poison","405","60","62","63","80","80","60","1","False"],["2","3","Venusaur","Grass","Poison","525","80","82","83","100","100","80","1","False"],["3","3","VenusaurMega Venusaur","Grass","Poison","625","80","100","123","122","120","80","1","False"],["4","4","Charmander","Fire",null,"309","39","52","43","60","50","65","1","False"],["5","5","Charmeleon","Fire",null,"405","58","64","58","80","65","80","1","False"],["6","6","Charizard","Fire","Flying","534","78","84","78","109","85","100","1","False"],["7","6","CharizardMega Charizard X","Fire","Dragon","634","78","130","111","130","85","100","1","False"],["8","6","CharizardMega Charizard Y","Fire","Flying","634","78","104","78","159","115","100","1","False"],["9","7","Squirtle","Water",null,"314","44","48","65","50","64","43","1","False"]],"shape":{"columns":13,"rows":10}}
```
:::
:::

::: {#0529e3a8 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Histograms
:::

::: {#a2a31374 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### What are histograms?

> A **histogram** is a visualization of a single continuous,
> quantitative variable (e.g., income or temperature).

-   Histograms are useful for looking at how a variable
    **distributes**.\
-   Can be used to determine whether a distribution is **normal**,
    **skewed**, or **bimodal**.

A histogram is a **univariate** plot, i.e., it displays only a single
variable.
:::

::: {#8dd14052 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Histograms in `matplotlib`

To create a histogram, call `plt.hist` with a **single column** of a
`DataFrame` (or a `numpy.ndarray`).

**Check-in**: What is this graph telling us?
:::

::: {#3be14b21 .cell .code execution_count="5" slideshow="{\"slide_type\":\"-\"}"}
``` python
p = plt.hist(df_pokemon['Attack'])
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/c6d1a408be56fba6b567467e1d86dc8c1e3cbee0.png){height="413"
width="552"}
:::
:::

::: {#d1035069 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Changing the number of bins

A histogram puts your continuous data into **bins** (e.g., 1-10, 11-20,
etc.).

-   The height of each bin reflects the number of observations within
    that interval.\
-   Increasing or decreasing the number of bins gives you more or less
    granularity in your distribution.
:::

::: {#745b4f50 .cell .code execution_count="6" slideshow="{\"slide_type\":\"-\"}"}
``` python
### This has lots of bins
p = plt.hist(df_pokemon['Attack'], bins = 30)
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/7d43aada9732ddcaad4b5b08b95edf51a3ea96d6.png){height="413"
width="543"}
:::
:::

::: {#95107a3f .cell .code execution_count="7" slideshow="{\"slide_type\":\"slide\"}"}
``` python
### This has fewer bins
p = plt.hist(df_pokemon['Attack'], bins = 5)
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/768ca3deceabcdc78b01fb01c28fb1f5e257a6ce.png){height="418"
width="552"}
:::
:::

::: {#49ea168b .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Changing the `alpha` level

The `alpha` level changes the **transparency** of your figure.
:::

::: {#177d3559 .cell .code execution_count="10" slideshow="{\"slide_type\":\"slide\"}"}
``` python
### This has fewer bins
p = plt.hist(df_pokemon['Attack'], alpha = .6)
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/da199d3b86f076a5828af54bf98b7c3e4519e3c0.png){height="413"
width="552"}
:::
:::

::: {#e3845d6d .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Check-in:

How would you make a histogram of the scores for `Defense`?
:::

::: {#62de2334 .cell .code slideshow="{\"slide_type\":\"-\"}"}
``` python
### Your code here
p = plt.hist(df_pokemon['Defense'], alpha = .6)
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/ee48fcecb2d80661b95102dfff35e92fb75f0684.png){height="413"
width="552"}
:::
:::

::: {#570b9684 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Check-in: {#check-in}

Could you make a histogram of the scores for `Type 1`?
:::

::: {#1f561f55 .cell .code slideshow="{\"slide_type\":\"-\"}"}
``` python
plt.figure(figsize=(15,4))
p = plt.hist(df_pokemon['Type 1'])
```
:::

::: {#d6a1875e .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Learning from histograms

Histograms are incredibly useful for learning about the **shape** of our
distribution. We can ask questions like:

-   Is this distribution relatively
    [normal](https://en.wikipedia.org/wiki/Normal_distribution)?
-   Is the distribution
    [skewed](https://en.wikipedia.org/wiki/Skewness)?
-   Are there [outliers](https://en.wikipedia.org/wiki/Outlier)?
:::

::: {#9d9d5be2 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Normally distributed data

We can use the `numpy.random.normal` function to create a **normal
distribution**, then plot it.

A normal distribution has the following characteristics:

-   Classic \"bell\" shape (**symmetric**).\
-   Mean, median, and mode are all identical.
:::

::: {#06f6c582 .cell .code execution_count="11" slideshow="{\"slide_type\":\"-\"}"}
``` python
norm = np.random.normal(loc = 10, scale = 1, size = 1000)
p = plt.hist(norm, alpha = .6)
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/8f6b1ac4109bf1e4fbe323718c36eacc7806f225.png){height="413"
width="552"}
:::
:::

::: {#1f3c7b15 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Skewed data

> **Skew** means there are values *elongating* one of the \"tails\" of a
> distribution.

-   Positive/right skew: the tail is pointing to the right.\
-   Negative/left skew: the tail is pointing to the left.
:::

::: {#0a69dc94 .cell .code execution_count="12" slideshow="{\"slide_type\":\"slide\"}"}
``` python
rskew = ss.skewnorm.rvs(20, size = 1000) # make right-skewed data
lskew = ss.skewnorm.rvs(-20, size = 1000) # make left-skewed data
fig, axes = plt.subplots(1, 2)
axes[0].hist(rskew)
axes[0].set_title("Right-skewed")
axes[1].hist(lskew)
axes[1].set_title("Left-skewed")
```

::: {.output .execute_result execution_count="12"}
    Text(0.5, 1.0, 'Left-skewed')
:::

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/4cb242fec98b22cf96be550e32d9439d7a679671.png){height="434"
width="552"}
:::
:::

::: {#77210b2c .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Outliers

> **Outliers** are data points that differ significantly from other
> points in a distribution.

-   Unlike skewed data, outliers are generally **discontinuous** with
    the rest of the distribution.
-   Next week, we\'ll talk about more ways to **identify** outliers; for
    now, we can rely on histograms.
:::

::: {#ec90040b .cell .code execution_count="13" slideshow="{\"slide_type\":\"slide\"}"}
``` python
norm = np.random.normal(loc = 10, scale = 1, size = 1000)
upper_outliers = np.array([21, 21, 21, 21]) ## some random outliers
data = np.concatenate((norm, upper_outliers))
p = plt.hist(data, alpha = .6)
plt.arrow(20, 100, dx = 0, dy = -50, width = .3, head_length = 10, facecolor = "red");
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/a8dd68f4c4fe51ba3a605083b089fe485f8f1ed4.png){height="413"
width="552"}
:::
:::

::: {#f2c2fb04 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Check-in {#check-in}

How would you describe the following distribution?

-   Normal vs. skewed?\
-   With or without outliers?
:::

::: {#ccd18574 .cell .code slideshow="{\"slide_type\":\"-\"}"}
``` python
### Your comment here
```
:::

::: {#0c880fc3 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Check-in {#check-in}

In a somewhat **right-skewed distribution** (like below), what\'s
larger----the `mean` or the `median`?
:::

::: {#ee3534d9 .cell .code execution_count="56" slideshow="{\"slide_type\":\"-\"}"}
``` python
mean1=np.mean(data)
median1=np.median(data)
print(mean1)
print(median1) # 50/50 percent of data = middle point
```

::: {.output .stream .stdout}
    10.050956026908674
    10.036406552683246
:::
:::

::: {#9de27d05 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Modifying our plot

-   A good data visualization should also make it *clear* what\'s being
    plotted.
    -   Clearly labeled `x` and `y` axes, title.
-   Sometimes, we may also want to add **overlays**.
    -   E.g., a dashed vertical line representing the `mean`.
:::

::: {#37dcd82f .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Adding axis labels
:::

::: {#d8591a17 .cell .code execution_count="17" slideshow="{\"slide_type\":\"-\"}"}
``` python
p = plt.hist(df_pokemon['Attack'], alpha = .6)
plt.xlabel("Attack")
plt.ylabel("Count")
plt.title("Distribution of Attack Scores");
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/d9e6f61a2ed9e77c8b4afabc55ee77606eaf78b2.png){height="454"
width="571"}
:::
:::

::: {#3a21bed9 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Adding a vertical line

The `plt.axvline` function allows us to draw a vertical line at a
particular position, e.g., the `mean` of the `Attack` column.
:::

::: {#646f2eaf .cell .code execution_count="18" slideshow="{\"slide_type\":\"-\"}"}
``` python
p = plt.hist(df_pokemon['Attack'], alpha = .6)
plt.xlabel("Attack")
plt.ylabel("Count")
plt.title("Distribution of Attack Scores")
plt.axvline(df_pokemon['Attack'].mean(), linestyle = "dotted");
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/ab32d993f0c5404096d76ae1dd25cac0c6d0f0d5.png){height="454"
width="571"}
:::
:::

::: {#07df0ce4 .cell .markdown}
## Faceting for histograms
:::

::: {#459dd57d .cell .markdown}
Let\'s try to group by our no. of Attacks by Pokemon Types looking at
many histograms at a time:
:::

::: {#16d4cfa2 .cell .code execution_count="67"}
``` python
import plotly.express as px
fig = px.histogram(df_pokemon,x='Attack', facet_col='Generation')
fig.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"bingroup":"x","hovertemplate":"Generation=1<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"MQA+AFIAZAA0AEAAVACCAGgAMAA/AFMAZwAeABQALQAjABkAWgCWAC0APABQAFAAOABRADwAWgA8AFUANwBaAEsAZAAvAD4AXAA5AEgAZgAtAEYAKQBMAC0ARgAtAFAAMgBBAFAARgBfADcAQQA3AFAALQBGADQAUgBQAGkARgBuADIAQQBfABQAIwAyADIAUABkAIIASwBaAGkAKABGAFAAXwB4AFUAZABBAEsASwAjADwAQQBVAG4ALQBGAFAAaQBBAF8AIwAyAEEAQQAtADAASQBpAIIAHgAyACgAXwAyAFAAeABpADcAQQBaAFUAggAFADcAXwB9ACgAQQBDAFwALQBLAC0AbgAyAFMAXwB9AJsAZAAKAH0AmwBVADAANwBBAEEAggA8ACgAPABQAHMAaQCHAG4AVQBaAGQAQABUAIYAbgC+AJYAZAA=","dtype":"i2"},"xaxis":"x","yaxis":"y"},{"bingroup":"x","hovertemplate":"Generation=2<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"MQA+AFIANABAAFQAQQBQAGkALgBMAB4AMgAUACMAPABaAFoAJgA6ACgAGQAeABQAKAAyAEsAKAA3AEsAXwBQABQAMgBkAEsAIwAtADcARgAeAEsAQQAtAFUAQQBBAFUASwA8AEgAIQBQAEEAWgBGAEsAVQB9AFAAeABfAIIAlgAKAH0AuQBfAFAAggAoADIAMgBkADcAQQBpADcAKABQADwAWgBaAF8APAB4AFAAXwAUACMAXwAeAD8ASwBQAAoAVQBzAEsAQABUAIYApABaAIIAZAA=","dtype":"i2"},"xaxis":"x2","yaxis":"y2"},{"bingroup":"x","hovertemplate":"Generation=3<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"LQBBAFUAbgA8AFUAeACgAEYAVQBuAJYANwBaAB4ARgAtACMARgAjADIAHgAyAEYAKABGAGQANwBVAB4AMgAZACMAQQBVAB4APAAoAIIAPABQAKAALQBaAFoAMwBHAFsAPAB4ABQALQAtAEEASwBVAFUAaQBGAFoAbgCMACgAPABkAC0ASwBLADIAKABJAC8APAArAEkAWgB4AIwARgBaADwAZAB4AFUAGQAtADwAZABGAGQAVQBzACgARgBuAHMAZAA3AF8AMABOAFAAeAAoAEYAKQBRAF8AfQAPADwARgBaAEsAcwClACgARgBEADIAggCWABcAMgBQAHgAKAA8AFAAQABoAFQAWgAeAEsAXwCHAJEANwBLAIcAkQBkADIASwBQAGQAWgCCAGQAlgCWALQAlgC0AGQAlgC0AEYAXwA=","dtype":"i2"},"xaxis":"x3","yaxis":"y3"},{"bingroup":"x","hovertemplate":"Generation=4<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"RABZAG0AOgBOAGgAMwBCAFYANwBLAHgALQBVABkAVQBBAFUAeAAeAEYAfQClACoANAAdADsATwBFAF4AHgBQAC0AQQBpACMAPAAwAFMAZAAyAFAAQgBMAIgAPAB9ADcAUgAeAD8AXQAYAFkAUAAZAAUAQQBcAEYAWgCCAKoAVQBGAG4AkQBIAHAAMgBaAD0AagBkADEARQAUAD4AXACEAHgARgBVAIwAZAB7AF8AMgBMAG4APABfAIIAUAB9AKUANwBkAFAAMgBBAEEAQQBBAEEASwBpAH0AeAB4AFoAoABkAHgARgBQAGQAWgBkAGcAeAA=","dtype":"i2"},"xaxis":"x4","yaxis":"y4"},{"bingroup":"x","hovertemplate":"Generation=5<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"ZAAtADwASwA/AF0AewA3AEsAZAA3AFUAPABQAG4AMgBYADUAYgA1AGIANQBiABkANwA3AE0AcwA8AGQASwBpAIcALQA5AFUAhwA8ADwAUABpAIwAMgBBAF8AZAB9ADUAPwBnAC0ANwBkABsAQwAjADwAXABIAFIAdQBaAIwAHgBWAEEAXwBLAFoAOgAeADIATgBsAHAAjAAyAF8AQQBpADIAXwAeAC0ANwAeACgAQQAsAFcAMgBBAF8APABkAEsASwCHADcAVQAoADwASwAvAE0AMgBeADcAUABkADcAVQBzADcASwAeACgANwBXAHUAkwBGAG4AMgAoAEYAQgBVAH0AeABKAHwAVQB9AG4AUwB7ADcAQQBhAG0AQQBVAGkAVQA8AFoAgQBaAHMAZABzAGkAeACWAH0AkQCCAKoAeABIAEgATQCAAHgA","dtype":"i2"},"xaxis":"x5","yaxis":"y5"},{"bingroup":"x","hovertemplate":"Generation=6<br>Attack=%{x}<br>count=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","orientation":"v","showlegend":false,"type":"histogram","x":{"bdata":"PQBOAGsALQA7AEUAOAA/AF8AJAA4ADIASQBRACMAFgA0ADIARAAmAC0AQQBBAGQAUgB8AFAAMAAwADAAUABuAJYAMgA0AEgAMABQADYAXAA0AGkAPABLADUASQAmADcAWQB5ADsATQBBAFwAOgAyADIASwBkAFAARgBuAEIAQgBCAEIAWgBVAF8AZABFAHUAHgBGAIMAgwBkAGQAoABuAKAAbgA=","dtype":"i2"},"xaxis":"x6","yaxis":"y6"}],"layout":{"annotations":[{"font":{},"showarrow":false,"text":"Generation=1","x":7.5e-2,"xanchor":"center","xref":"paper","y":1,"yanchor":"bottom","yref":"paper"},{"font":{},"showarrow":false,"text":"Generation=2","x":0.24499999999999997,"xanchor":"center","xref":"paper","y":1,"yanchor":"bottom","yref":"paper"},{"font":{},"showarrow":false,"text":"Generation=3","x":0.415,"xanchor":"center","xref":"paper","y":1,"yanchor":"bottom","yref":"paper"},{"font":{},"showarrow":false,"text":"Generation=4","x":0.585,"xanchor":"center","xref":"paper","y":1,"yanchor":"bottom","yref":"paper"},{"font":{},"showarrow":false,"text":"Generation=5","x":0.7549999999999999,"xanchor":"center","xref":"paper","y":1,"yanchor":"bottom","yref":"paper"},{"font":{},"showarrow":false,"text":"Generation=6","x":0.925,"xanchor":"center","xref":"paper","y":1,"yanchor":"bottom","yref":"paper"}],"barmode":"relative","legend":{"tracegroupgap":0},"margin":{"t":60},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermap":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermap"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"xaxis":{"anchor":"y","domain":[0,0.15],"title":{"text":"Attack"}},"xaxis2":{"anchor":"y2","domain":[0.16999999999999998,0.31999999999999995],"matches":"x","title":{"text":"Attack"}},"xaxis3":{"anchor":"y3","domain":[0.33999999999999997,0.49],"matches":"x","title":{"text":"Attack"}},"xaxis4":{"anchor":"y4","domain":[0.51,0.66],"matches":"x","title":{"text":"Attack"}},"xaxis5":{"anchor":"y5","domain":[0.6799999999999999,0.83],"matches":"x","title":{"text":"Attack"}},"xaxis6":{"anchor":"y6","domain":[0.85,1],"matches":"x","title":{"text":"Attack"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"count"}},"yaxis2":{"anchor":"x2","domain":[0,1],"matches":"y","showticklabels":false},"yaxis3":{"anchor":"x3","domain":[0,1],"matches":"y","showticklabels":false},"yaxis4":{"anchor":"x4","domain":[0,1],"matches":"y","showticklabels":false},"yaxis5":{"anchor":"x5","domain":[0,1],"matches":"y","showticklabels":false},"yaxis6":{"anchor":"x6","domain":[0,1],"matches":"y","showticklabels":false}}}
```
:::
:::

::: {#d0d302cf .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Scatterplots
:::

::: {#402ee105 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### What are scatterplots?

> A **scatterplot** is a visualization of how two different continuous
> distributions relate to each other.

-   Each individual point represents an observation.
-   Very useful for **exploratory data analysis**.
    -   Are these variables positively or negatively correlated?

A scatterplot is a **bivariate** plot, i.e., it displays at least two
variables.
:::

::: {#3edad76d .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Scatterplots with `matplotlib`

We can create a scatterplot using `plt.scatter(x, y)`, where `x` and `y`
are the two variables we want to visualize.
:::

::: {#08e2a1e8 .cell .code execution_count="68" slideshow="{\"slide_type\":\"-\"}"}
``` python
x = np.arange(1, 10)
y = np.arange(11, 20)
p = plt.scatter(x, y)
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/b461d74ab52494c5002552d4df61eb8e4e6d6b47.png){height="413"
width="543"}
:::
:::

::: {#c25c794d .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Check-in {#check-in}

Are these variables related? If so, how?
:::

::: {#c95f0d57 .cell .code execution_count="28" slideshow="{\"slide_type\":\"-\"}"}
``` python
x = np.random.normal(loc = 10, scale = 1, size = 100)
y = x * 2 + np.random.normal(loc = 0, scale = 2, size = 100)
plt.scatter(x, y, alpha = .6);
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/d70df7bfdae0e8affd4f7fa1aa48f99354183990.png){height="413"
width="543"}
:::
:::

::: {#ffb2e7e1 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Check-in {#check-in}

Are these variables related? If so, how?
:::

::: {#62879170 .cell .code execution_count="29" slideshow="{\"slide_type\":\"-\"}"}
``` python
x = np.random.normal(loc = 10, scale = 1, size = 100)
y = -x * 2 + np.random.normal(loc = 0, scale = 2, size = 100)
plt.scatter(x, y, alpha = .6);
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/a452388bf2537b7bc1d09013ab9c2d8095088096.png){height="413"
width="555"}
:::
:::

::: {#a66a5ff8 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Scatterplots are useful for detecting non-linear relationships
:::

::: {#93c559c1 .cell .code execution_count="30" slideshow="{\"slide_type\":\"-\"}"}
``` python
x = np.random.normal(loc = 10, scale = 1, size = 100)
y = np.sin(x)
plt.scatter(x, y, alpha = .6);
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/e805a73c74a01df9b6e220f826cf19b26a3f5891.png){height="413"
width="568"}
:::
:::

::: {#896a0253 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Check-in {#check-in}

How would we visualize the relationship between `Attack` and `Speed` in
our Pokemon dataset?
:::

::: {#a6d55d3c .cell .code execution_count="70" slideshow="{\"slide_type\":\"-\"}"}
``` python
x = df_pokemon["Attack"]
y = df_pokemon["Speed"]
plt.xlabel("Attack")
plt.ylabel("Speed")
plt.title("Speed vs Attack Scores")
plt.scatter(x, y, alpha = .6);
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/9fd65b30a349802e0f3360f7c52a43fb9ce9e2d6.png){height="454"
width="571"}
:::
:::

::: {#4bb78092 .cell .markdown}
## Scatterplots with `pyplot express`
:::

::: {#06e019cd .cell .markdown}
With pyplot express we can play with scatterplots even further - we can
create `bubble plots`!
:::

::: {#6d1e88a8 .cell .code execution_count="71"}
``` python
import plotly.express as px
bubble=px.scatter(df_pokemon, x='Attack', y='Speed', color='Type 1', size='HP');
bubble.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"hovertemplate":"Type 1=Grass<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Grass","marker":{"color":"#636efa","size":{"bdata":"LTxQUC08SzJBUDxfQS08UEsjN0seSygyRkYoRlo8PDIyRmM3S18oPC1GSjxaWmRBZGQtPEsySyg8LUZLRXIsSls4PVhCew==","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Grass","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"MQA+AFIAZAAyAEEAUABLAFoAaQAoAF8ANwAxAD4AUgBQACMALQA3AB4ASwAtAEEAVQBuACgARgBkACgAggA8AFUAcwBEAEQAWQBtAB4ARgAjADwAZAA+AFwAhABkAG4AZABnAC0APABLADUAYgAbAEMAIwA8AFYANwBVADIAXgBaAD0ATgBrAEEAZAA=","dtype":"i2"},"xaxis":"x","y":{"bdata":"LQA8AFAAUAAeACgAMgAoADcARgAoADcAPAAtADwAUAAyADIAUABuAB4AHgBGAF8AeACRAB4APABQACMARgBBACMANwAzAB8AJAA4ADcAWgAjAFUALgAoADwAHgAyAF8AZAB/AD8AUwBxAEAAZQBCAHQAHgBaADwADwAeAAoAFABsACYAOQBAADQARAA=","dtype":"i2"},"yaxis":"y"},{"hovertemplate":"Type 1=Fire<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Fire","marker":{"color":"#EF553B","size":{"bdata":"JzpOTk4mSTdaMkFBQVonOk4oMi1zai08UFA8RkZGLEBMS1tBWm4yS0ZpaVUoO0s+Tj5WUA==","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Fire","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"NABAAFQAggBoACkATABGAG4AVQBkAF8AggBkADQAQABUACgAMgBLAHMAggA8AFUAeACgADwAZAB4AFUAOgBOAGgAXwBaAD8AXQB7ADUAYgBaAIwAHgBhAC0AOwBFAEkAUQAyAEQAbgA=","dtype":"i2"},"xaxis":"x","y":{"bdata":"QVBkZGRBZDxfWmldQVpBUGQUHlNkWi03UGQjKBQUPVFsU00tN0FAZTJfN0E8SWhUfkhqRg==","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"Type 1=Water<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Water","marker":{"color":"#00cc96","size":{"bdata":"LAA7AE8ATwAyAFAAKABBAFoAKABQAFoAXwBfAEEAWgAeADIAHgA3AB4ANwAtAFAAHgA8ABQAXwBfAIIAggAyAEEAVQBLAH0ARgBkAFoANwBfAF8AQQA3ACMASwBBAEsAZAAyAEYAZABkACgAPABQACgAPAAtAEYARgCCAKoAMgBuACsAPwAUAF8AIwA3ADcAZAArAGQAZAA1AEAAVAA3AFUATABvADEARQAtAFoAUABkADcASwBfADIASwAyAEsAaQBGADYASgA+AEsANwBkAKUAWwBbACkANgBIADIARwA=","dtype":"i2"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Water","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"MAA/AFMAZwA0AFIAMgBBAF8AKABGAEEASwBLAC0ARgBBAF8AaQCCACgAQQBDAFwALQBLAAoAfQCbAFUAQQBBAFAAaQAmADoAFAAyAEsALQBVAEsAXwA3AEEAaQAoAF8ASwBGAFUAbgCWAB4AMgBGAB4AMgBaAHgAjABGAFoAMABOAFAAeAAPADwAQABoAFQAWgAeAGQAlgAzAEIAVgBBAGkAMABTADEARQAUAHgAUABkADcASwBkADUAYgAyAEEAXwBcAE4AbAAsAFcAKAA8AEsASABIADgAPwBfADUASQA=","dtype":"i2"},"xaxis":"x","y":{"bdata":"KzpOTjdVWlpGRmQPHh4tRihGMks8VT9EVXNQUVE8QSs6TkNDKDJGDyMeVSNBLUZVVSgyPEYeMkZVQUFfaTw8PDwjN1BRIDQ0N2FaWigyPFVzIidCWzJkUGQtPEZAZUBFSmIWIDdiKDxBbGxHYXosOw==","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"Type 1=Bug<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Bug","marker":{"color":"#ab63fa","size":{"bdata":"LTI8KC1BQSM8PEZGQUEoNyhGQTJLRkYUUFAtMjwyPChGHz0BQUElTSg8PDxGHkZWLTdLHig8MkYyRjJGMlA6N1VHJi1Q","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Bug","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"HgAUAC0AIwAZAFoAlgBGAF8ANwBBAG4AfQCbABQAIwA8AFoAQQBBAFoAggCWAAoAfQC5AC0AIwBGACMAMgAeADwALQBaAFoASQAvABkAVQAdADsATwBFAF4AHgBQAEwANQA/AGcALQA3AGQAQQBfAEsAhwAvAE0AKABGAG0AVQA8AHgAIwAWADQA","dtype":"i2"},"xaxis":"x","y":{"bdata":"LQAeAEYAMgAjAEsAkQAZAB4ALQBaAGkAVQBpADcAVQAeACgAXwAPACgAQQBLAAUAVQBLABQADwBBAA8AQQBBADwAKACgACgAVQBVABkAQQAkACQAJAAkAEIARgAoAF8AKgAqAFwAOQAvAHAANwAtADwAFABBAGwAGQCRAG0APABkAGMAIwAdAFkA","dtype":"i2"},"yaxis":"y"},{"hovertemplate":"Type 1=Normal<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Normal","marker":{"color":"#FFA15A","size":{"bdata":"KAA/AFMAUwAeADcAKABBAHMAjAAoAEEANAAjADwAWgD6AGkAaQBLADAANwBBAKAAIwBVADwAZABaADcARgBkADwAWgBVAEkANwBfAP8AJgBOACgAPAA8AFAAlgBAAFQAaAAyADIARgA8AC0ASQBGADwAKAA3AFUAOwBPAEsANwBBAEEAMQBHAGQATACHAG4AVQBuAHgALQA8AC0AQQBVADIAPgBQAGcAZwA3AEsAPABQAF8ARgBkAGQAZAAmAFUALQBLAA==","dtype":"i2"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Normal","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"LQA8AFAAUAA4AFEAPABaAC0ARgAtAEYAQQBVAG4ANwAFAF8AfQBkADAANwA8AG4ALgBMAB4AMgAeAEYAUABGAFAAggBQAF8AFABQAAoAHgBGADcAVQA8AFAAoAAzAEcAWwAUAC0AQQA8ACgAcwBGAFoANwBLAHgALQBVAGQAQgBMAIgANwBSAAUAQQBVAFUAUACgAHgANwBVADwAUABuADcATQBzADwAPAAyAF8APABkAG4AUwB7AE0AgAAkADgAMgBQAA==","dtype":"i2"},"xaxis":"x","y":{"bdata":"OABHAGUAeQBIAGEARgBkABQALQBaAHMAPABLAGQAHgAyAFoAZABuADAANwAoAB4AFABaADIARgAPAFUAVQAtACgANwA8AFUASwBkADcAPABkAFUAfQAeAFoAZAAcADAARAAUADIARgA8ADIAWgBGACgAPABQAGQAHwBHAHMAVQBpAIcAVQBwAB4AWwAFADIAWgBkAHgAKgBNADcAPABQACsAQQBdADIAMgBLAHMASwBfADcAPABQAFoAgAA5AE4APgBmAA==","dtype":"i2"},"yaxis":"y"},{"hovertemplate":"Type 1=Poison<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Poison","marker":{"color":"#19d3f3","size":{"bdata":"Izw3RlouPVEoS1BpKEFVRmRJP2coRjBTMlAyQQ==","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Poison","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"PFUvPlw5SGYtUFBpQVpaK0lkP10yWj1qMl88Sw==","dtype":"i1"},"xaxis":"x","y":{"bdata":"NwBQACkAOABMADIAQQBVADcAWgAZADIAIwA8AIIAKAA3AEEASgBUAEEAXwAyAFUAQQBLAB4ALAA=","dtype":"i2"},"yaxis":"y"},{"hovertemplate":"Type 1=Electric<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Electric","marker":{"color":"#FF6692","size":{"bdata":"IzwZMig8QUFaFDdGWlotWihGRjw8LTxQPEZLMjIyMjIyLUs3I0FVT08sPkM=","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Electric","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"N1ojPB4yU0FaKCg3S18/VS1LSzIoQVV4LUZ7MkFBQUFBPGRLN1Vzc2kmNzo=","dtype":"i1"},"xaxis":"x","y":{"bdata":"WgBuAC0ARgBkAIwAaQCCAGQAPAAjAC0ANwAtAF8AcwBBAGkAhwBfAF8ALQA8AEYAXwA8AF8AWwBWAFYAVgBWAFYATAB0AGcAPAAoADIAbwBlAEYAbQBlAA==","dtype":"i2"},"yaxis":"y"},{"hovertemplate":"Type 1=Ground<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Ground","marker":{"color":"#B6E880","size":{"bdata":"MksKIzI8UGlBWlotMlAoPGRkRGxzSzxuMjxfbTtZWVk=","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Ground","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"SwBkADcAUAAyAFAAVQCCAEsAPAB4AGQARgBkACgARgCWALQASABwAIwAXwBVAIcASABSAHUAQgBKAHwAfQCRAA==","dtype":"i2"},"xaxis":"x","y":{"bdata":"KEFfeCMtGShVKDIKRmQ3S1paIC8oX0RYQUpcICM3ZVs=","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"Type 1=Fairy<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Fairy","marker":{"color":"#FF97FF","size":{"bdata":"Rl8yIzc8WlUsNk5OZT5SX34=","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Fairy","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"LQBGABkAFAAoAFAAeAAyACYALQBBADQASAAwAFAAQQCDAA==","dtype":"i2"},"xaxis":"x","y":{"bdata":"IzwPFCgeLVAqNEsXHTFIPGM=","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"Type 1=Fighting<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Fighting","marker":{"color":"#FECB52","size":{"bdata":"KABBAEYAUABaADIAMgAjADIASACQAB4APAA8ACgARgBGAEsAVQBpAHgASwAtAEEAQwBfAE4A","dtype":"i2"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Fighting","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"UABpAFAAZACCAHgAaQAjAF8APAB4ACgAPABkAEYAbgCRAFAAaQCMAGQAfQBVAH0AUgB8AFwA","dtype":"i2"},"xaxis":"x","y":{"bdata":"Rl8jLTdXTCNGGTI8UGQ8WnAjKC0tVUFpKzp2","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"Type 1=Psychic<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Psychic","marker":{"color":"#636efa","size":{"bdata":"GQAoADcANwA8AFUAKABqAGoAagBkACgAQQBBADAAvgBqAGQAHAAmAEQARAA8AFAAQQBfADIAMgAyADIALQAUAEQARABLAFAASwB4AGQATAB0ADcAQwBIAC0APABGAC0AQQBuADcASwA+AEoASgBQAFAA","dtype":"i2"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Psychic","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"FAAjADIAMgAwAEkALQBuAL4AlgBkADIASwBBAEgAIQBaAGQAGQAjAEEAVQAZAC0AMgAXAJYAtABGAF8AHgAZAH0ApQBLAGkAfQBGAGQAGQA3AC0AOQA6AB4ALQA3AB4AKABBADcASwAwADAAMABuAKAA","dtype":"i2"},"xaxis":"x","y":{"bdata":"WgBpAHgAlgAqAEMAWgCCAIIAjABkAEYAXwBuADAAIQBuAGQAKAAyAFAAZAA8AFAAQQAXAJYAlgBaALQALQA8AFAAbgBfAFAAcwBVAGQAGAAdAEgAcgBhAC0ANwBBABQAHgAeAB4AKABEAGgAaABGAFAA","dtype":"i2"},"yaxis":"y"},{"hovertemplate":"Type 1=Rock<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Rock","marker":{"color":"#EF553B","size":{"bdata":"KDdQIyNGHjxQUEYyRmRkHkZGQlYtS1BDYR48Mjw3RlU3S1sqSDpSTXsyMjI=","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Rock","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"UABfAHgALQAoADwAUABzAGkAhwBkAEAAVACGAKQALQA3AF8AKQBRAF8AfQBkAH0ApQAqADQAUAA3AEsAaQCHAHAAjACBADQAaQBZAHkAOwBNADIAZACgAA==","dtype":"i2"},"xaxis":"x","y":{"bdata":"FAAjAC0ARgAjADcANwBQAIIAlgAeACkAMwA9AEcAHgBGAEYAFwArAEsALQAyADoAOgAeAB4ACgAoAA8AFAAZAEYAbgBsADIARAAwAEcALgA6ADIAMgBuAA==","dtype":"i2"},"yaxis":"y"},{"hovertemplate":"Type 1=Ghost<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Ghost","marker":{"color":"#00cc96","size":{"bdata":"HgAtADwAPAA8ACwAQABAABQAKABaAJYAPAAyAC0AlgCWACYAOgAyADwAPAArAFUAMQAsADYAOwBBADcASwBVAA==","dtype":"i2"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Ghost","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"IwAyAEEAQQA8AEsAcwClACgARgAyAFAAPABcAGQAZAB4AB4AMgAeACgANwBGAG4AQgBCAEIAQgBaAFUAXwBkAA==","dtype":"i2"},"xaxis":"x","y":{"bdata":"UABfAG4AggBVAC0AQQBLABkAGQBGAFAAaQAjAC0AWgBaAB4AHgAUADcAUAAmADgAMwA4AC4AKQBUAGMARQA2AA==","dtype":"i2"},"yaxis":"y"},{"hovertemplate":"Type 1=Ice<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Ice","marker":{"color":"#ab63fa","size":{"bdata":"QVoyZC0tMlBQRlpuUEFuRiQzRzdfRjdf","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Ice","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"MgBVADIAZAA3AB4AMgBQAHgAKAA8AFAAMgA8AIIAUAAyAEEAXwBGAG4AMgBFAHUA","dtype":"i2"},"xaxis":"x","y":{"bdata":"X1UyMktBMlBkGS1BMkFQbiw7TygyaRwc","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"Type 1=Dragon<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Dragon","marker":{"color":"#FFA15A","size":{"bdata":"KT1bS0stQV9fUFBQUGlpOkRsbC5CTE1kZH19fS1EWmw=","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Dragon","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"QABUAIYARgBuAEsAXwCHAJEAUABkAFoAggCWALQARgBaAIIAqgBXAHUAkwB4AHgAlgCCAKoAeAAyAEsAZABkAA==","dtype":"i2"},"xaxis":"x","y":{"bdata":"MkZQUFAyMmR4bm5ubl9zKlJmXDlDYTBaWl9fXyg8UF8=","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"Type 1=Dark<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Dark","marker":{"color":"#19d3f3","size":{"bdata":"Xzw3LUtLI0YyMkFBZEZGKUAyQSg8LUFGbjRIXDVWfg==","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Dark","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"QQBVAF8APABaAFoANwBaAEsAVQCCAJYAfQB4AFoAMgBYAEsAWgBBAGkAVQB9ADcAQQBBAFUAaQA2AFwAgwA=","dtype":"i2"},"xaxis":"x","y":{"bdata":"QVtzQV9zI0YyFEtzR319QmowOkFpPEY8UCY6Yi1JYw==","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"Type 1=Steel<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Steel","marker":{"color":"#FF6692","size":{"bdata":"S0tBMjIyPEZGKDxQUFBkOUNkKDw8Wy07PDw5","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Steel","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"VQB9AFAAVQBpAEYAWgBuAIwANwBLAIcAkQBLAGQAGABZAHgANwBQAGQAWgBQAG4AlgAyAFAA","dtype":"i2"},"xaxis":"x","y":{"bdata":"Hh5GMjIeKDIyHjJGbjJkFyFaHjJabBwjPDxL","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"Type 1=Flying<br>Attack=%{x}<br>Speed=%{y}<br>HP=%{marker.size}<extra></extra>","legendgroup":"Flying","marker":{"color":"#B6E880","size":{"bdata":"T08oVQ==","dtype":"i1"},"sizemode":"area","sizeref":0.6375,"symbol":"circle"},"mode":"markers","name":"Flying","orientation":"v","showlegend":true,"type":"scatter","x":{"bdata":"c2QeRg==","dtype":"i1"},"xaxis":"x","y":{"bdata":"b3k3ew==","dtype":"i1"},"yaxis":"y"}],"layout":{"legend":{"itemsizing":"constant","title":{"text":"Type 1"},"tracegroupgap":0},"margin":{"t":60},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermap":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermap"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"xaxis":{"anchor":"y","domain":[0,1],"title":{"text":"Attack"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"Speed"}}}}
```
:::
:::

::: {#c8bcfd99 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Barplots
:::

::: {#57e246b8 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### What is a barplot?

> A **barplot** visualizes the relationship between one *continuous*
> variable and a *categorical* variable.

-   The *height* of each bar generally indicates the mean of the
    continuous variable.
-   Each bar represents a different *level* of the categorical variable.

A barplot is a **bivariate** plot, i.e., it displays at least two
variables.
:::

::: {#ac48b7a7 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Barplots with `matplotlib`

`plt.bar` can be used to create a **barplot** of our data.

-   E.g., average `Attack` by `Legendary` status.
-   However, we first need to use `groupby` to calculate the mean
    `Attack` per level.
:::

::: {#bd9e566d .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Step 1: Using `groupby`
:::

::: {#2a8a3682 .cell .code execution_count="72" slideshow="{\"slide_type\":\"-\"}"}
``` python
summary = df_pokemon[['Legendary', 'Attack']].groupby("Legendary").mean().reset_index()
summary
```

::: {.output .execute_result execution_count="72"}
``` json
{"columns":[{"name":"index","rawType":"int64","type":"integer"},{"name":"Legendary","rawType":"bool","type":"boolean"},{"name":"Attack","rawType":"float64","type":"float"}],"conversionMethod":"pd.DataFrame","ref":"c65b7993-19dd-4df9-b741-09d77bb0bb4b","rows":[["0","False","75.66938775510204"],["1","True","116.67692307692307"]],"shape":{"columns":2,"rows":2}}
```
:::
:::

::: {#b00d46f2 .cell .code execution_count="73" slideshow="{\"slide_type\":\"-\"}"}
``` python
### Turn Legendary into a str
summary['Legendary'] = summary['Legendary'].apply(lambda x: str(x))
summary
```

::: {.output .execute_result execution_count="73"}
``` json
{"columns":[{"name":"index","rawType":"int64","type":"integer"},{"name":"Legendary","rawType":"object","type":"string"},{"name":"Attack","rawType":"float64","type":"float"}],"conversionMethod":"pd.DataFrame","ref":"c30b6b60-76cf-4ee5-a15f-9777d156766d","rows":[["0","False","75.66938775510204"],["1","True","116.67692307692307"]],"shape":{"columns":2,"rows":2}}
```
:::
:::

::: {#a7099c27 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Step 2: Pass values into `plt.bar` {#step-2-pass-values-into-pltbar}

**Check-in**:

-   What do we learn from this plot?\
-   What is this plot missing?
:::

::: {#3dbf7822 .cell .code execution_count="40" slideshow="{\"slide_type\":\"-\"}"}
``` python
plt.bar(x = summary['Legendary'],height = summary['Attack'],alpha = .6);
plt.xlabel("Legendary status");
plt.ylabel("Attack");
```

::: {.output .display_data}
![](vertopal_412cc3859e5648bd9f351346bf9de239/be1628ee1d8f6a28c9a0a3f9a779ba7b6ad84154.png){height="432"
width="571"}
:::
:::

::: {#abe6c4f3 .cell .markdown}
## Barplots in `plotly.express` {#barplots-in-plotlyexpress}
:::

::: {#e59b4b56 .cell .code execution_count="41"}
``` python
import plotly.express as px
data_canada = px.data.gapminder().query("country == 'Canada'")
fig = px.bar(data_canada, x='year', y='pop')
fig.show()
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"hovertemplate":"year=%{x}<br>pop=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","orientation":"v","showlegend":false,"textposition":"auto","type":"bar","x":{"bdata":"oAelB6oHrwe0B7kHvgfDB8gHzQfSB9cH","dtype":"i2"},"xaxis":"x","y":{"bdata":"MJzhAOqNAwF5syEBN689AdQIVAGwGmsB7IyAAcQdlQHuO7MBM27OATzK5gE9fv0B","dtype":"i4"},"yaxis":"y"}],"layout":{"barmode":"relative","legend":{"tracegroupgap":0},"margin":{"t":60},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermap":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermap"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"xaxis":{"anchor":"y","domain":[0,1],"title":{"text":"year"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"pop"}}}}
```
:::
:::

::: {#12f29577 .cell .code execution_count="43"}
``` python
data_canada.head(3)
```

::: {.output .execute_result execution_count="43"}
``` json
{"columns":[{"name":"index","rawType":"int64","type":"integer"},{"name":"country","rawType":"object","type":"string"},{"name":"continent","rawType":"object","type":"string"},{"name":"year","rawType":"int64","type":"integer"},{"name":"lifeExp","rawType":"float64","type":"float"},{"name":"pop","rawType":"int64","type":"integer"},{"name":"gdpPercap","rawType":"float64","type":"float"},{"name":"iso_alpha","rawType":"object","type":"string"},{"name":"iso_num","rawType":"int64","type":"integer"}],"conversionMethod":"pd.DataFrame","ref":"e76665fe-6095-4c4f-9e10-4f4a70e23cbe","rows":[["240","Canada","Americas","1952","68.75","14785584","11367.16112","CAN","124"],["241","Canada","Americas","1957","69.96","17010154","12489.95006","CAN","124"],["242","Canada","Americas","1962","71.3","18985849","13462.48555","CAN","124"]],"shape":{"columns":8,"rows":3}}
```
:::
:::

::: {#0a4459a6 .cell .code execution_count="46"}
``` python
long_df = px.data.medals_long()

fig = px.bar(long_df, x="nation", y="count", color="medal", title="Long format of data")
fig.show()

long_df.head(3)
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"hovertemplate":"medal=gold<br>nation=%{x}<br>count=%{y}<extra></extra>","legendgroup":"gold","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"gold","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["South Korea","China","Canada"],"xaxis":"x","y":{"bdata":"GAoJ","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"medal=silver<br>nation=%{x}<br>count=%{y}<extra></extra>","legendgroup":"silver","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"silver","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["South Korea","China","Canada"],"xaxis":"x","y":{"bdata":"DQ8M","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"medal=bronze<br>nation=%{x}<br>count=%{y}<extra></extra>","legendgroup":"bronze","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"bronze","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["South Korea","China","Canada"],"xaxis":"x","y":{"bdata":"CwgM","dtype":"i1"},"yaxis":"y"}],"layout":{"barmode":"relative","legend":{"title":{"text":"medal"},"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermap":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermap"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Long format of data"},"xaxis":{"anchor":"y","domain":[0,1],"title":{"text":"nation"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"count"}}}}
```
:::

::: {.output .execute_result execution_count="46"}
``` json
{"columns":[{"name":"index","rawType":"int64","type":"integer"},{"name":"nation","rawType":"object","type":"string"},{"name":"medal","rawType":"object","type":"string"},{"name":"count","rawType":"int64","type":"integer"}],"conversionMethod":"pd.DataFrame","ref":"56d41f83-c8df-4c09-aafb-24b32efa76b9","rows":[["0","South Korea","gold","24"],["1","China","gold","10"],["2","Canada","gold","9"]],"shape":{"columns":3,"rows":3}}
```
:::
:::

::: {#5612cdda .cell .code execution_count="49"}
``` python
wide_df = px.data.medals_wide()

fig = px.bar(wide_df, x="nation", y=["gold", "silver", "bronze"], title="Wide format of data")
fig.show()

wide_df.head(3)
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"hovertemplate":"variable=gold<br>nation=%{x}<br>value=%{y}<extra></extra>","legendgroup":"gold","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"gold","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["South Korea","China","Canada"],"xaxis":"x","y":{"bdata":"GAoJ","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"variable=silver<br>nation=%{x}<br>value=%{y}<extra></extra>","legendgroup":"silver","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"silver","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["South Korea","China","Canada"],"xaxis":"x","y":{"bdata":"DQ8M","dtype":"i1"},"yaxis":"y"},{"hovertemplate":"variable=bronze<br>nation=%{x}<br>value=%{y}<extra></extra>","legendgroup":"bronze","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"bronze","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["South Korea","China","Canada"],"xaxis":"x","y":{"bdata":"CwgM","dtype":"i1"},"yaxis":"y"}],"layout":{"barmode":"relative","legend":{"title":{"text":"variable"},"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermap":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermap"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Wide format of data"},"xaxis":{"anchor":"y","domain":[0,1],"title":{"text":"nation"}},"yaxis":{"anchor":"x","domain":[0,1],"title":{"text":"value"}}}}
```
:::

::: {.output .execute_result execution_count="49"}
``` json
{"columns":[{"name":"index","rawType":"int64","type":"integer"},{"name":"nation","rawType":"object","type":"string"},{"name":"gold","rawType":"int64","type":"integer"},{"name":"silver","rawType":"int64","type":"integer"},{"name":"bronze","rawType":"int64","type":"integer"}],"conversionMethod":"pd.DataFrame","ref":"03d56a4e-bc92-469e-be87-958a96f8d200","rows":[["0","South Korea","24","13","11"],["1","China","10","15","8"],["2","Canada","9","12","12"]],"shape":{"columns":4,"rows":3}}
```
:::
:::

::: {#0b9d9340 .cell .markdown}
## Faceting barplots

Please use faceting for the Pokemon data with barplots:
:::

::: {#14f1adb4 .cell .code execution_count="75"}
``` python
fig = px.bar(df_pokemon, x='Type 1', facet_row='Legendary')
fig.show()
 
```

::: {.output .display_data}
``` json
{"config":{"plotlyServerURL":"https://plot.ly"},"data":[{"hovertemplate":"Legendary=False<br>Type 1=%{x}<br>count=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","orientation":"v","showlegend":false,"textposition":"auto","type":"bar","x":["Grass","Grass","Grass","Grass","Fire","Fire","Fire","Fire","Fire","Water","Water","Water","Water","Bug","Bug","Bug","Bug","Bug","Bug","Bug","Normal","Normal","Normal","Normal","Normal","Normal","Normal","Normal","Poison","Poison","Electric","Electric","Ground","Ground","Poison","Poison","Poison","Poison","Poison","Poison","Fairy","Fairy","Fire","Fire","Normal","Normal","Poison","Poison","Grass","Grass","Grass","Bug","Bug","Bug","Bug","Ground","Ground","Normal","Normal","Water","Water","Fighting","Fighting","Fire","Fire","Water","Water","Water","Psychic","Psychic","Psychic","Psychic","Fighting","Fighting","Fighting","Grass","Grass","Grass","Water","Water","Rock","Rock","Rock","Fire","Fire","Water","Water","Water","Electric","Electric","Normal","Normal","Normal","Water","Water","Poison","Poison","Water","Water","Ghost","Ghost","Ghost","Ghost","Rock","Psychic","Psychic","Water","Water","Electric","Electric","Grass","Grass","Ground","Ground","Fighting","Fighting","Normal","Poison","Poison","Ground","Ground","Normal","Grass","Normal","Normal","Water","Water","Water","Water","Water","Water","Psychic","Bug","Ice","Electric","Fire","Bug","Bug","Normal","Water","Water","Water","Water","Normal","Normal","Water","Electric","Fire","Normal","Rock","Rock","Rock","Rock","Rock","Rock","Normal","Dragon","Dragon","Dragon","Psychic","Grass","Grass","Grass","Fire","Fire","Fire","Water","Water","Water","Normal","Normal","Normal","Normal","Bug","Bug","Bug","Bug","Poison","Water","Water","Electric","Fairy","Normal","Fairy","Fairy","Psychic","Psychic","Electric","Electric","Electric","Electric","Grass","Water","Water","Rock","Water","Grass","Grass","Grass","Normal","Grass","Grass","Bug","Water","Water","Psychic","Dark","Dark","Water","Ghost","Psychic","Psychic","Normal","Bug","Bug","Normal","Ground","Steel","Steel","Fairy","Fairy","Water","Bug","Bug","Bug","Bug","Bug","Dark","Normal","Normal","Fire","Fire","Ice","Ice","Water","Water","Water","Ice","Water","Steel","Dark","Dark","Dark","Water","Ground","Ground","Normal","Normal","Normal","Fighting","Fighting","Ice","Electric","Fire","Normal","Normal","Rock","Rock","Rock","Rock","Psychic","Grass","Grass","Grass","Grass","Fire","Fire","Fire","Fire","Water","Water","Water","Water","Dark","Dark","Normal","Normal","Bug","Bug","Bug","Bug","Bug","Water","Water","Water","Grass","Grass","Grass","Normal","Normal","Water","Water","Psychic","Psychic","Psychic","Psychic","Bug","Bug","Grass","Grass","Normal","Normal","Normal","Bug","Bug","Bug","Normal","Normal","Normal","Fighting","Fighting","Normal","Rock","Normal","Normal","Dark","Dark","Steel","Steel","Steel","Steel","Steel","Steel","Fighting","Fighting","Fighting","Electric","Electric","Electric","Electric","Electric","Bug","Bug","Grass","Poison","Poison","Water","Water","Water","Water","Water","Fire","Fire","Fire","Fire","Psychic","Psychic","Normal","Ground","Ground","Ground","Grass","Grass","Normal","Dragon","Dragon","Normal","Poison","Rock","Rock","Water","Water","Water","Water","Ground","Ground","Rock","Rock","Rock","Rock","Water","Water","Normal","Normal","Ghost","Ghost","Ghost","Ghost","Ghost","Grass","Psychic","Dark","Dark","Psychic","Ice","Ice","Ice","Ice","Ice","Ice","Water","Water","Water","Water","Water","Dragon","Dragon","Dragon","Dragon","Steel","Steel","Steel","Steel","Grass","Grass","Grass","Fire","Fire","Fire","Water","Water","Water","Normal","Normal","Normal","Normal","Normal","Bug","Bug","Electric","Electric","Electric","Grass","Grass","Rock","Rock","Rock","Rock","Bug","Bug","Bug","Bug","Bug","Bug","Bug","Electric","Water","Water","Grass","Grass","Water","Water","Normal","Ghost","Ghost","Normal","Normal","Normal","Ghost","Dark","Normal","Normal","Psychic","Poison","Poison","Steel","Steel","Rock","Psychic","Normal","Normal","Ghost","Dragon","Dragon","Dragon","Dragon","Normal","Fighting","Fighting","Fighting","Ground","Ground","Poison","Poison","Poison","Poison","Grass","Water","Water","Water","Grass","Grass","Grass","Dark","Electric","Normal","Ground","Grass","Electric","Fire","Fairy","Bug","Grass","Ice","Ground","Ice","Normal","Psychic","Psychic","Rock","Ghost","Ice","Electric","Electric","Electric","Electric","Electric","Electric","Psychic","Water","Water","Grass","Grass","Grass","Fire","Fire","Fire","Water","Water","Water","Normal","Normal","Normal","Normal","Normal","Dark","Dark","Grass","Grass","Fire","Fire","Water","Water","Psychic","Psychic","Normal","Normal","Normal","Electric","Electric","Rock","Rock","Rock","Psychic","Psychic","Ground","Ground","Normal","Normal","Fighting","Fighting","Fighting","Water","Water","Water","Fighting","Fighting","Bug","Bug","Bug","Bug","Bug","Bug","Grass","Grass","Grass","Grass","Water","Ground","Ground","Ground","Fire","Fire","Fire","Grass","Bug","Bug","Dark","Dark","Psychic","Ghost","Ghost","Water","Water","Rock","Rock","Poison","Poison","Dark","Dark","Normal","Normal","Psychic","Psychic","Psychic","Psychic","Psychic","Psychic","Water","Water","Ice","Ice","Ice","Normal","Normal","Electric","Bug","Bug","Grass","Grass","Water","Water","Water","Bug","Bug","Grass","Grass","Steel","Steel","Steel","Electric","Electric","Electric","Psychic","Psychic","Ghost","Ghost","Ghost","Dragon","Dragon","Dragon","Ice","Ice","Ice","Bug","Bug","Ground","Fighting","Fighting","Dragon","Ground","Ground","Dark","Dark","Normal","Normal","Normal","Dark","Dark","Fire","Bug","Dark","Dark","Dark","Bug","Bug","Water","Water","Normal","Normal","Bug","Grass","Grass","Grass","Fire","Fire","Fire","Water","Water","Water","Normal","Normal","Normal","Fire","Fire","Bug","Bug","Bug","Fire","Fire","Fairy","Fairy","Fairy","Grass","Grass","Fighting","Fighting","Normal","Psychic","Psychic","Psychic","Steel","Steel","Steel","Steel","Fairy","Fairy","Fairy","Fairy","Dark","Dark","Rock","Rock","Poison","Poison","Water","Water","Electric","Electric","Rock","Rock","Rock","Rock","Fairy","Fighting","Electric","Rock","Dragon","Dragon","Dragon","Steel","Ghost","Ghost","Ghost","Ghost","Ghost","Ghost","Ghost","Ghost","Ghost","Ghost","Ice","Ice","Flying","Flying"],"xaxis":"x2","y":{"bdata":"AQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEB","dtype":"i1"},"yaxis":"y2"},{"hovertemplate":"Legendary=True<br>Type 1=%{x}<br>count=%{y}<extra></extra>","legendgroup":"","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"","orientation":"v","showlegend":false,"textposition":"auto","type":"bar","x":["Ice","Electric","Fire","Psychic","Psychic","Psychic","Electric","Fire","Water","Psychic","Fire","Rock","Ice","Steel","Dragon","Dragon","Dragon","Dragon","Water","Water","Ground","Ground","Dragon","Dragon","Steel","Psychic","Psychic","Psychic","Psychic","Psychic","Psychic","Psychic","Steel","Water","Fire","Normal","Ghost","Ghost","Dark","Grass","Grass","Normal","Psychic","Steel","Rock","Grass","Flying","Flying","Electric","Electric","Dragon","Dragon","Ground","Ground","Dragon","Dragon","Dragon","Fairy","Dark","Dragon","Rock","Rock","Psychic","Psychic","Fire"],"xaxis":"x","y":{"bdata":"AQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQE=","dtype":"i1"},"yaxis":"y"}],"layout":{"annotations":[{"font":{},"showarrow":false,"text":"Legendary=True","textangle":90,"x":0.98,"xanchor":"left","xref":"paper","y":0.2425,"yanchor":"middle","yref":"paper"},{"font":{},"showarrow":false,"text":"Legendary=False","textangle":90,"x":0.98,"xanchor":"left","xref":"paper","y":0.7575000000000001,"yanchor":"middle","yref":"paper"}],"barmode":"relative","legend":{"tracegroupgap":0},"margin":{"t":60},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"heatmap"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermap":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermap"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]],"sequentialminus":[[0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":5.0e-2},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"xaxis":{"anchor":"y","domain":[0,0.98],"title":{"text":"Type 1"}},"xaxis2":{"anchor":"y2","domain":[0,0.98],"matches":"x","showticklabels":false},"yaxis":{"anchor":"x","domain":[0,0.485],"title":{"text":"count"}},"yaxis2":{"anchor":"x2","domain":[0.515,1],"matches":"y","title":{"text":"count"}}}}
```
:::
:::

::: {#11340770 .cell .markdown}
For more information please go to the tutorial [Plotly Express Wide-Form
Support in Python](https://plotly.com/python/wide-form/).
:::

::: {#5240050f .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Conclusion

This concludes our first introduction to **data visualization**:

-   Working with `matplotlib.pyplot`.\
-   Working with more convenient version of `pyplot.express`.
-   Creating basic plots: histograms, scatterplots, and barplots.

Next time, we\'ll move onto discussing `seaborn`, another very useful
package for data visualization.
:::


---
jupyter:
  celltoolbar: Slideshow
  kernelspec:
    display_name: .venv
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.12.3
  nbformat: 4
  nbformat_minor: 5
---

::: {#6080af38 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
# Data visualization, pt. 2 (`seaborn`) {#data-visualization-pt-2-seaborn}
:::

::: {#118f7491 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Goals of this exercise

-   Introducting `seaborn`.
-   Putting `seaborn` into practice:
    -   **Univariate** plots (histograms).\
    -   **Bivariate** continuous plots (scatterplots and line plots).
    -   **Bivariate** categorical plots (bar plots, box plots, and strip
        plots).
:::

::: {#5fa26f5e .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Introducing `seaborn`
:::

::: {#6a4ffbb5 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### What is `seaborn`?

> [`seaborn`](https://seaborn.pydata.org/) is a data visualization
> library based on `matplotlib`.

-   In general, it\'s easier to make nice-looking graphs with `seaborn`.
-   The trade-off is that `matplotlib` offers more flexibility.
:::

::: {#6a3c41f6 .cell .code execution_count="7" slideshow="{\"slide_type\":\"-\"}"}
``` python
import seaborn as sns ### importing seaborn
import pandas as pd
import matplotlib.pyplot as plt ## just in case we need it
import numpy as np
```
:::

::: {#1c0815db .cell .code execution_count="8" slideshow="{\"slide_type\":\"-\"}"}
``` python
%matplotlib inline 
%config InlineBackend.figure_format = 'retina'
```
:::

::: {#b926c887 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### The `seaborn` hierarchy of plot types

We\'ll learn more about exactly what this hierarchy means today (and in
next lecture).

![title](img/seaborn_library.png)
:::

::: {#914ef46e .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Example dataset

Today we\'ll work with a new dataset, from
[Gapminder](https://www.gapminder.org/data/documentation/).

-   **Gapminder** is an independent Swedish foundation dedicated to
    publishing and analyzing data to correct misconceptions about the
    world.
-   Between 1952-2007, has data about `life_exp`, `gdp_cap`, and
    `population`.
:::

::: {#6b8d6ac8 .cell .code execution_count="9"}
``` python
df_gapminder = pd.read_csv("gapminder_full.csv")
```
:::

::: {#3fcb4d6e .cell .code execution_count="10"}
``` python
df_gapminder.head(2)
```

::: {.output .execute_result execution_count="10"}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>continent</th>
      <th>life_exp</th>
      <th>gdp_cap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>1952</td>
      <td>8425333</td>
      <td>Asia</td>
      <td>28.801</td>
      <td>779.445314</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Afghanistan</td>
      <td>1957</td>
      <td>9240934</td>
      <td>Asia</td>
      <td>30.332</td>
      <td>820.853030</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#c306611b .cell .code execution_count="11"}
``` python
df_gapminder.shape
```

::: {.output .execute_result execution_count="11"}
    (1704, 6)
:::
:::

::: {#532d16b1 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Univariate plots

> A **univariate plot** is a visualization of only a *single* variable,
> i.e., a **distribution**.

![title](img/displot.png)
:::

::: {#d802bd64 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Histograms with `sns.histplot` {#histograms-with-snshistplot}

-   We\'ve produced histograms with `plt.hist`.\
-   With `seaborn`, we can use `sns.histplot(...)`.

Rather than use `df['col_name']`, we can use the syntax:

``` python
sns.histplot(data = df, x = col_name)
```

This will become even more useful when we start making **bivariate
plots**.
:::

::: {#c2d59830 .cell .code execution_count="12" slideshow="{\"slide_type\":\"-\"}"}
``` python
# Histogram of life expectancy
sns.histplot(df_gapminder['life_exp']);
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/fbea76394f01a3a9b9045456f3e4f39b75f3c5a2.png){height="433"
width="571"}
:::
:::

::: {#1dbe492a .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Modifying the number of bins

As with `plt.hist`, we can modify the number of *bins*.
:::

::: {#93d0b80e .cell .code execution_count="13" slideshow="{\"slide_type\":\"-\"}"}
``` python
# Fewer bins
sns.histplot(data = df_gapminder, x = 'life_exp', bins = 10, alpha = .6);
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/9f5866a717f5c82bf7f03547c3987acb81380859.png){height="433"
width="571"}
:::
:::

::: {#c47d0b3f .cell .code execution_count="14" slideshow="{\"slide_type\":\"slide\"}"}
``` python
# Many more bins!
sns.histplot(data = df_gapminder, x = 'life_exp', bins = 100, alpha = .6);
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/3b8cc8e1286cb7182458e024c3d2c7b4da3e5489.png){height="433"
width="563"}
:::
:::

::: {#0b4d4e21 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Modifying the y-axis with `stat`

By default, `sns.histplot` will plot the **count** in each bin. However,
we can change this using the `stat` parameter:

-   `probability`: normalize such that bar heights sum to `1`.
-   `percent`: normalize such that bar heights sum to `100`.
-   `density`: normalize such that total *area* sums to `1`.
:::

::: {#94540a47 .cell .code execution_count="15" slideshow="{\"slide_type\":\"-\"}"}
``` python
# Note the modified y-axis!
sns.histplot(data = df_gapminder, x = 'life_exp', stat = "percent", alpha = .6);
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/102cf115047f84e2becbcdf40aedb19d7e63359e.png){height="433"
width="562"}
:::
:::

::: {#2145d7cb .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Check-in

How would you make a histogram showing the distribution of `population`
values in `2007` alone?

-   Bonus 1: Modify this graph to show `probability`, not `count`.
-   Bonus 2: What do you notice about this graph, and how might you
    change it?
:::

::: {#df9f179f .cell .code execution_count="16"}
``` python
### Your code here
Year = 2007
sns.histplot(data=df_gapminder[df_gapminder['year'] == Year], x="population")
plt.show()
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/8079a5f62daaba798058477fffaf408289920248.png){height="432"
width="563"}
:::
:::

::: {#36ad404c .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Bivariate continuous plots

> A **bivariate continuous plot** visualizes the relationship between
> *two continuous variables*.

![title](img/seaborn_relplot.png)
:::

::: {#dfd90842 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Scatterplots with `sns.scatterplot` {#scatterplots-with-snsscatterplot}

> A **scatterplot** visualizes the relationship between two continuous
> variables.

-   Each observation is plotted as a single dot/mark.
-   The position on the `(x, y)` axes reflects the value of those
    variables.

One way to make a scatterplot in `seaborn` is using `sns.scatterplot`.
:::

::: {#3de8d546 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Showing `gdp_cap` by `life_exp`

What do we notice about `gdp_cap`?
:::

::: {#b40b0f24 .cell .code execution_count="17" slideshow="{\"slide_type\":\"-\"}"}
``` python
sns.scatterplot(data = df_gapminder, x = 'gdp_cap',
               y = 'life_exp', alpha = .3);
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/f22b6912f640cd1882f2a101ccedbbd11c854989.png){height="433"
width="563"}
:::
:::

::: {#38c992bf .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Showing `gdp_cap_log` by `life_exp`
:::

::: {#337ebde8 .cell .code execution_count="18" slideshow="{\"slide_type\":\"-\"}"}
``` python
## Log GDP
df_gapminder['gdp_cap_log'] = np.log10(df_gapminder['gdp_cap']) 
## Show log GDP by life exp
sns.scatterplot(data = df_gapminder, x = 'gdp_cap_log', y = 'life_exp', alpha = .3);
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/4e20622e2999662086c5139c391b1894580dd88a.png){height="433"
width="563"}
:::
:::

::: {#bedb2807 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Adding a `hue`

-   What if we want to add a *third* component that\'s categorical, like
    `continent`?
-   `seaborn` allows us to do this with `hue`.
:::

::: {#a05bc8c4 .cell .code execution_count="19" slideshow="{\"slide_type\":\"-\"}"}
``` python
## Log GDP
df_gapminder['gdp_cap_log'] = np.log10(df_gapminder['gdp_cap']) 
## Show log GDP by life exp
sns.scatterplot(data = df_gapminder[df_gapminder['year'] == 2007],
               x = 'gdp_cap_log', y = 'life_exp', hue = "continent", alpha = .7);
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/0f80284a68dbfa8a01d5517379e2af72612ab789.png){height="433"
width="563"}
:::
:::

::: {#ca1b0c44 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Adding a `size`

-   What if we want to add a *fourth* component that\'s continuous, like
    `population`?
-   `seaborn` allows us to do this with `size`.
:::

::: {#9386efe7 .cell .code execution_count="20" slideshow="{\"slide_type\":\"-\"}"}
``` python
## Log GDP
df_gapminder['gdp_cap_log'] = np.log10(df_gapminder['gdp_cap']) 
## Show log GDP by life exp
sns.scatterplot(data = df_gapminder[df_gapminder['year'] == 2007],
               x = 'gdp_cap_log', y = 'life_exp',
                hue = "continent", size = 'population', alpha = .7);
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/4860810a813661d4a40b17d2a562de5eee931d02.png){height="433"
width="563"}
:::
:::

::: {#84b2e1d6 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Changing the position of the legend
:::

::: {#72869666 .cell .code execution_count="21" slideshow="{\"slide_type\":\"-\"}"}
``` python
## Show log GDP by life exp
sns.scatterplot(data = df_gapminder[df_gapminder['year'] == 2007],
               x = 'gdp_cap_log', y = 'life_exp',
                hue = "continent", size = 'population', alpha = .7);

plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0);
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/6d86ed20507786f91aadec38fb1865d1a2247f21.png){height="433"
width="726"}
:::
:::

::: {#ef47a2b4 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Lineplots with `sns.lineplot` {#lineplots-with-snslineplot}

> A **lineplot** also visualizes the relationship between two continuous
> variables.

-   Typically, the position of the line on the `y` axis reflects the
    *mean* of the `y`-axis variable for that value of `x`.
-   Often used for plotting **change over time**.

One way to make a lineplot in `seaborn` is using
[`sns.lineplot`](https://seaborn.pydata.org/generated/seaborn.lineplot.html).
:::

::: {#94530912 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Showing `life_exp` by `year`

What general trend do we notice?
:::

::: {#356cfb6d .cell .code execution_count="22" slideshow="{\"slide_type\":\"-\"}"}
``` python
sns.lineplot(data = df_gapminder,
             x = 'year',
             y = 'life_exp');
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/77f2b0f8d429e28f645de109649a9d70e6f61309.png){height="435"
width="563"}
:::
:::

::: {#4559923b .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Modifying how error/uncertainty is displayed

-   By default, `seaborn.lineplot` will draw **shading** around the line
    representing a confidence interval.
-   We can change this with `errstyle`.
:::

::: {#d27e0a0e .cell .code execution_count="23" slideshow="{\"slide_type\":\"-\"}"}
``` python
sns.lineplot(data = df_gapminder,
             x = 'year',
             y = 'life_exp',
            err_style = "bars");
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/ab8c836db26782224b35068083df2de3fa4b49e3.png){height="437"
width="563"}
:::
:::

::: {#7af66b9b .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Adding a `hue` {#adding-a-hue}

-   We could also show this by `continent`.\
-   There\'s (fortunately) a positive trend line for each `continent`.
:::

::: {#3c0e3d53 .cell .code execution_count="24" slideshow="{\"slide_type\":\"-\"}"}
``` python
sns.lineplot(data = df_gapminder,
             x = 'year',
             y = 'life_exp',
            hue = "continent")
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0);
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/1da40b284288d803ce79c02883726195ef6177dd.png){height="432"
width="702"}
:::
:::

::: {#6db3fe99 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Check-in {#check-in}

How would you plot the relationship between `year` and `gdp_cap` for
countries in the `Americas` only?
:::

::: {#ea14f3b5 .cell .code execution_count="25" slideshow="{\"slide_type\":\"-\"}"}
``` python
### Your code here

df_americas = df_gapminder[df_gapminder['continent'] == 'Americas']

sns.lineplot(
    data=df_americas,
    x='year',
    y='gdp_cap'
)
```

::: {.output .execute_result execution_count="25"}
    <Axes: xlabel='year', ylabel='gdp_cap'>
:::

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/6b3b43b32b2b8146a6b8e4565ec66a50730ce3e5.png){height="432"
width="590"}
:::
:::

::: {#9747b5b6 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Heteroskedasticity in `gdp_cap` by `year`

-   [**Heteroskedasticity**](https://en.wikipedia.org/wiki/Homoscedasticity_and_heteroscedasticity)
    is when the *variance* in one variable (e.g., `gdp_cap`) changes as
    a function of another variable (e.g., `year`).
-   In this case, why do you think that is?
:::

::: {#09332f03 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Plotting by country

-   There are too many countries to clearly display in the `legend`.
-   But the top two lines are the `United States` and `Canada`.
    -   I.e., two countries have gotten much wealthier per capita, while
        the others have not seen the same economic growth.
:::

::: {#21daa428 .cell .code execution_count="26" slideshow="{\"slide_type\":\"-\"}"}
``` python
sns.lineplot(data = df_gapminder[df_gapminder['continent']=="Americas"],
             x = 'year', y = 'gdp_cap', hue = "country", legend = None);
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/3a4c56ea6acf2fc7291f4ffbf97e5fe5ed5b80ad.png){height="432"
width="590"}
:::
:::

::: {#0c21823e .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Using `relplot`

-   `relplot` allows you to plot either line plots or scatter plots
    using `kind`.
-   `relplot` also makes it easier to `facet` (which we\'ll discuss
    momentarily).
:::

::: {#f7dc3515 .cell .code execution_count="27" slideshow="{\"slide_type\":\"-\"}"}
``` python
sns.relplot(data = df_gapminder, x = "year", y = "life_exp", kind = "line");
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/107bdea1bbdbe26a9a833cee23bc20d3f82b5174.png){height="490"
width="490"}
:::
:::

::: {#e657a22c .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Faceting into `rows` and `cols`

We can also plot the same relationship across multiple \"windows\" or
**facets** by adding a `rows`/`cols` parameter.
:::

::: {#1ba2892b .cell .code execution_count="28" slideshow="{\"slide_type\":\"-\"}"}
``` python
sns.relplot(data = df_gapminder, x = "year", y = "life_exp", kind = "line", 
            col = "continent");
```

::: {.output .display_data}
![](vertopal_102dd767906f436c9b301449319d65b2/9371c4d4c44b576e94d3c6a3db9be574c01b3177.png){height="490"
width="2490"}
:::
:::

::: {#d7ac6bca .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Bivariate categorical plots

> A **bivariate categorical plot** visualizes the relationship between
> one categorical variable and one continuous variable.

![title](img/seaborn_catplot.png)
:::

::: {#c89d243d .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Example dataset {#example-dataset}

Here, we\'ll return to our Pokemon dataset, which has more examples of
categorical variables.
:::

::: {#aa7988a2 .cell .code execution_count="29"}
``` python
df_pokemon = pd.read_csv("data/pokemon.csv")
```

::: {.output .error ename="FileNotFoundError" evalue="[Errno 2] No such file or directory: 'data/pokemon.csv'"}
    ---------------------------------------------------------------------------
    FileNotFoundError                         Traceback (most recent call last)
    Cell In[29], line 1
    ----> 1 df_pokemon = pd.read_csv("data/pokemon.csv")

    File ~/pandas_exercises-9/.venv/lib/python3.12/site-packages/pandas/io/parsers/readers.py:1026, in read_csv(filepath_or_buffer, sep, delimiter, header, names, index_col, usecols, dtype, engine, converters, true_values, false_values, skipinitialspace, skiprows, skipfooter, nrows, na_values, keep_default_na, na_filter, verbose, skip_blank_lines, parse_dates, infer_datetime_format, keep_date_col, date_parser, date_format, dayfirst, cache_dates, iterator, chunksize, compression, thousands, decimal, lineterminator, quotechar, quoting, doublequote, escapechar, comment, encoding, encoding_errors, dialect, on_bad_lines, delim_whitespace, low_memory, memory_map, float_precision, storage_options, dtype_backend)
       1013 kwds_defaults = _refine_defaults_read(
       1014     dialect,
       1015     delimiter,
       (...)   1022     dtype_backend=dtype_backend,
       1023 )
       1024 kwds.update(kwds_defaults)
    -> 1026 return _read(filepath_or_buffer, kwds)

    File ~/pandas_exercises-9/.venv/lib/python3.12/site-packages/pandas/io/parsers/readers.py:620, in _read(filepath_or_buffer, kwds)
        617 _validate_names(kwds.get("names", None))
        619 # Create the parser.
    --> 620 parser = TextFileReader(filepath_or_buffer, **kwds)
        622 if chunksize or iterator:
        623     return parser

    File ~/pandas_exercises-9/.venv/lib/python3.12/site-packages/pandas/io/parsers/readers.py:1620, in TextFileReader.__init__(self, f, engine, **kwds)
       1617     self.options["has_index_names"] = kwds["has_index_names"]
       1619 self.handles: IOHandles | None = None
    -> 1620 self._engine = self._make_engine(f, self.engine)

    File ~/pandas_exercises-9/.venv/lib/python3.12/site-packages/pandas/io/parsers/readers.py:1880, in TextFileReader._make_engine(self, f, engine)
       1878     if "b" not in mode:
       1879         mode += "b"
    -> 1880 self.handles = get_handle(
       1881     f,
       1882     mode,
       1883     encoding=self.options.get("encoding", None),
       1884     compression=self.options.get("compression", None),
       1885     memory_map=self.options.get("memory_map", False),
       1886     is_text=is_text,
       1887     errors=self.options.get("encoding_errors", "strict"),
       1888     storage_options=self.options.get("storage_options", None),
       1889 )
       1890 assert self.handles is not None
       1891 f = self.handles.handle

    File ~/pandas_exercises-9/.venv/lib/python3.12/site-packages/pandas/io/common.py:873, in get_handle(path_or_buf, mode, encoding, compression, memory_map, is_text, errors, storage_options)
        868 elif isinstance(handle, str):
        869     # Check whether the filename is to be opened in binary mode.
        870     # Binary mode does not support 'encoding' and 'newline'.
        871     if ioargs.encoding and "b" not in ioargs.mode:
        872         # Encoding
    --> 873         handle = open(
        874             handle,
        875             ioargs.mode,
        876             encoding=ioargs.encoding,
        877             errors=errors,
        878             newline="",
        879         )
        880     else:
        881         # Binary mode
        882         handle = open(handle, ioargs.mode)

    FileNotFoundError: [Errno 2] No such file or directory: 'data/pokemon.csv'
:::
:::

::: {#5fa39f22 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Barplots with `sns.barplot` {#barplots-with-snsbarplot}

> A **barplot** visualizes the relationship between one *continuous*
> variable and a *categorical* variable.

-   The *height* of each bar generally indicates the mean of the
    continuous variable.
-   Each bar represents a different *level* of the categorical variable.

With `seaborn`, we can use the function `sns.barplot`.
:::

::: {#fa3e59f5 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Average `Attack` by `Legendary` status
:::

::: {#6f7488f0 .cell .code}
``` python
sns.barplot(data = df_pokemon,
           x = "Legendary", y = "Attack");
```
:::

::: {#51c2b7c5 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Average `Attack` by `Type 1`

Here, notice that I make the figure *bigger*, to make sure the labels
all fit.
:::

::: {#9b736ef3 .cell .code}
``` python
plt.figure(figsize=(15,4))
sns.barplot(data = df_pokemon,
           x = "Type 1", y = "Attack");
```
:::

::: {#6ebe3b7c .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Check-in {#check-in}

How would you plot `HP` by `Type 1`?
:::

::: {#3a67b87a .cell .code}
``` python
### Your code here
sns.barplot(
    data=df_pokemon,
    x='Type 1',
    y='HP'
)
```
:::

::: {#7ff6f160 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Modifying `hue`

As with `scatterplot` and `lineplot`, we can change the `hue` to give
further granularity.

-   E.g., `HP` by `Type 1`, further divided by `Legendary` status.
:::

::: {#9e76167e .cell .code}
``` python
plt.figure(figsize=(15,4))
sns.barplot(data = df_pokemon,
           x = "Type 1", y = "HP", hue = "Legendary");
```
:::

::: {#dbef85e0 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
### Using `catplot`

> `seaborn.catplot` is a convenient function for plotting bivariate
> categorical data using a range of plot types (`bar`, `box`, `strip`).
:::

::: {#cb403c74 .cell .code}
``` python
sns.catplot(data = df_pokemon, x = "Legendary", 
             y = "Attack", kind = "bar");
```
:::

::: {#b16ed97e .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### `strip` plots

> A `strip` plot shows each individual point (like a scatterplot),
> divided by a **category label**.
:::

::: {#968c6492 .cell .code}
``` python
sns.catplot(data = df_pokemon, x = "Legendary", 
             y = "Attack", kind = "strip", alpha = .5);
```
:::

::: {#d3c3c6b1 .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### Adding a `mean` to our `strip` plot

We can plot *two graphs* at the same time, showing both the individual
points and the means.
:::

::: {#2f410b8d .cell .code}
``` python
sns.catplot(data = df_pokemon, x = "Legendary", 
             y = "Attack", kind = "strip", alpha = .1)
sns.pointplot(data = df_pokemon, x = "Legendary", 
             y = "Attack", hue = "Legendary");
```
:::

::: {#4663409d .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
#### `box` plots

> A `box` plot shows the interquartile range (the middle 50% of the
> data), along with the minimum and maximum.
:::

::: {#f2f1af0e .cell .code}
``` python
sns.catplot(data = df_pokemon, x = "Legendary", 
             y = "Attack", kind = "box");
```
:::

::: {#eb6e403f .cell .markdown}
Try to consider converting the boxplots into violin plots.
:::

::: {#390cb79d .cell .markdown slideshow="{\"slide_type\":\"slide\"}"}
## Conclusion

As with our lecture on `pyplot`, this just scratches the surface.

But now, you\'ve had an introduction to:

-   The `seaborn` package.
-   Plotting both **univariate** and **bivariate** data.
-   Creating plots with multiple layers.
:::
