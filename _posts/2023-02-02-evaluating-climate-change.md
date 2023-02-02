![image](https://live.staticflickr.com/4912/32305750398_ea37139cd6_z.jpg)

### Summary

For complete details and codes, see the display-friendly pdf below

There has been ongoing data collected concerning climate change, we are here to evaluate the seriousness and velocity of those changes.

Data related to drought, heavy rain, sea level, temperatures, and high wind has been analysed and predictions were given for the near future.

Predicting sea level is important because it helps us understand and prepare for the impacts of climate change on coastal communities and infrastructure. Rising sea levels can cause coastal flooding, erosion, saltwater intrusion into freshwater aquifers, and other environmental and economic consequences. Accurate sea level predictions allow governments, businesses, and communities to plan and adapt to these impacts, reducing the risk of harm to people and property.

### Model Reasoning

For time series like climate data, it is highly unlikely we can use simple models such as regression

But we also would not want to rely on complex models such as neural networks

We want to enable a level of interpretation that is helpful to draw a conclusion on climate change, which is why our focus would be Autoregressive and Moving Average models.

### Normalization

The official method of normalization is described but formula is not given

There maybe a 10% inconsistency from the `(X-E)/S` formula but this is negligible

For example, Sea level has an average of `-7024.94` and standard deviation of `39.0834`

![image](https://user-images.githubusercontent.com/12572058/216469063-04a48143-978f-49e1-84b6-fa9272c0371c.png)

### Findings

Surprisingly, we didn't find much systematic trends on drought and heavy rainfall. But we did find that sea level has been increasing at `0.035906 * 4 * 39.0834 = 5.5367052` milimeters per year.

> Since 1993, however, average sea level has risen at a rate of 0.12 to 0.14 (about 3.302 milimeters) inches per year

Our result is much higher than what is mentioned by [United States Environmental Protection Agency](https://www.epa.gov/climate-indicators/climate-change-indicators-sea-level). This would eventually come down to the solidarity of data, the choice of data, and timeframe of analysis.

I do, however, believe in my own analysis and this could be an indication of how variable different research's sea level analysis could be.

Nevertheless, this gives us confidence that the sea level changes are not far from the 4 milimeters range in a meta-review sense.

|                        | Concluding Description                                                     | Applied Models                                       |
|------------------------|----------------------------------------------------------------------------|------------------------------------------------------|
|  Consecutive Dry Days  | has periods of high and low volatility,<br>but in general it is stationary |         Series: MA(10)<br>Residuals: ARCH(5)         |
| Maximum 5-Day Rainfall |                a random walk with a small drift<br>component               |                    ARIMA(0, 1, 1)                    |
|        Sea Level       |                 Deterministic along time since year<br>2000                | Series: Deterministic Trend<br>Residuals: ARMA(1, 7) |

{% include pdfembed.html filename="evaluating_climate_change.pdf" %}
