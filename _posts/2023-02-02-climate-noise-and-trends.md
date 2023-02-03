![image](https://live.staticflickr.com/4912/32305750398_ea37139cd6_z.jpg)

### Summary

For complete details and codes, see the display-friendly pdf below

There has been ongoing data collected concerning climate change, we are here to evaluate the seriousness and velocity of those changes.

Data related to drought, heavy rain, sea level, temperatures, and high wind has been analysed and predictions were given for the near future.

Predicting sea level is important because it helps us understand and prepare for the impacts of climate change on coastal communities and infrastructure. Rising sea levels can cause coastal flooding, erosion, saltwater intrusion into freshwater aquifers, and other environmental and economic consequences. Accurate sea level predictions allow governments, businesses, and communities to plan and adapt to these impacts, reducing the risk of harm to people and property.

### Model Reasoning

For time series like climate data, it is highly unlikely we can use simple models such as linear regression

But we also would not want to rely on complex models such as neural networks

We want to enable a level of interpretation that is helpful to draw a conclusion on climate change, which is why our focus would be Autoregressive and Moving Average models.

### Normalization

The official method of normalization is described but formula is not given

There maybe a 10% inconsistency from the `(X-E)/S` formula but this is negligible

For example, Sea level has an average of `-7024.94` and standard deviation of `39.0834`

![image](https://user-images.githubusercontent.com/12572058/216469063-04a48143-978f-49e1-84b6-fa9272c0371c.png)

### Findings

| Climate Data               | Concluding Description                                                  | Applied Models                                       |
|----------------------------|-------------------------------------------------------------------------|------------------------------------------------------|
|  **Consecutive Dry Days**  | has periods of high and low volatility, but in general it is stationary |         Series: MA(10)<br>Residuals: ARCH(5)         |
| **Maximum 5-Day Rainfall** |                a random walk with a small drift component               |                    ARIMA(0, 1, 1)                    |
|        **Sea Level**       |                 Deterministic along time since year 2000                | Series: Deterministic Trend<br>Residuals: ARMA(1, 7) |

Surprisingly, we didn't find much systematic trends on drought and heavy rainfall. But we did find that sea level has been increasing at `0.035906 * 4 * 39.0834 = 5.5367052` milimeters per year.

> Since 1993, however, average sea level has risen at a rate of 0.12 to 0.14 (about 3.302 milimeters) inches per year

Our result is much higher than what is mentioned by [United States Environmental Protection Agency](https://www.epa.gov/climate-indicators/climate-change-indicators-sea-level). This difference would eventually come down to the solidarity of data, the choice of data, and timeframe of analysis.

I do, however, believe in my own analysis and this could be an indication of how variable different research's sea level analysis could be.

Nevertheless, this gives us confidence that the sea level changes are not far from the 4 milimeters range in a meta-review sense.

### Cross Validation / Backtesting

In order to communicate to different stakeholders, it is very important we keep things like holdout-testing and visualization in mind.

It is rather difficult to conduct backtesting with the R language, but rather easy in Python, here's a little show case of what the backtesting might have looked like.

It is the author's regret not having put backtesting in the original document.

```Python
from statsforecast import StatsForecast # required to instantiate StastForecast object and use cross-validation method

import pandas as pd 

Y_df = pd.read_csv('cross-validation-data.csv', index_col=0) # load the data 
Y_df.head()

df = Y_df[Y_df['unique_id'] == 'H1'] # select time series

StatsForecast.plot(df)

from statsforecast.models import AutoARIMA

models = [AutoARIMA(season_length = 4)]

sf = StatsForecast(
    df = df, 
    models = models, 
    freq = 'Q', 
    n_jobs = -1
)

crossvalidation_df = sf.cross_validation(
    df = df,
    h = 4,
    step_size = 4,
    n_windows = 5
  )
  
crossvalidation_df.head()

crossvalidation_df.rename(columns = {'y' : 'actual'}, inplace = True) # rename actual values 

cutoff = crossvalidation_df['cutoff'].unique()

for k in range(len(cutoff)): 
    cv = crossvalidation_df[crossvalidation_df['cutoff'] == cutoff[k]]
    StatsForecast.plot(df[220:], cv.loc[:, cv.columns != 'cutoff'])
    
from datasetsforecast.losses import rmse

rmse = rmse(crossvalidation_df['actual'], crossvalidation_df['AutoARIMA'])

print("RMSE using cross-validation: ", rmse)
# > RMSE using cross-validation:  1.1713644
```

![image](https://user-images.githubusercontent.com/12572058/216494144-306a36c0-b449-4869-834e-ddf3a58eeb4f.png)

Here shows [how cross-validation may look cumbersome in R](http://freerangestats.info/blog/2019/07/20/time-series-cv) and [some discussion on the computational concern](https://www.reddit.com/r/MachineLearning/comments/syx41w/p_beware_of_false_fbprophets_introducing_the/) for this problem.

### Detailed Document

The complete details and codes are provided below

{% include pdfembed.html filename="evaluating_climate_change.pdf" %}
