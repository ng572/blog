I have done some visualization and analysis on the TidyTuesday's [dataset](https://github.com/rfordatascience/tidytuesday/tree/master/data/2018/2018-10-23) `Horror Movies and Profit`, let's see what we can learn from it.

[Source code could be found here](../assets/files/horror_movies.pdf).

{% include pdfembed.html filename="horror_movies.pdf" %}

### The history of Movie Profits

First, let's take a look at the return on investment (markup = revenue / cost) of movies thorughout the decades.

![image](https://user-images.githubusercontent.com/12572058/187069111-20ce66da-4f40-42f5-8735-b61c658ae318.png)

There appears to have been a massive earning opportunity at the beginning, where films could make nearly a hundred fold its production cost from tickets.

As more and more films got into the market, the average return dropped. This could be hypothesized as a higher number of firms in the market created a more competitive market outcome

It should be noted that during the 1950-70s, the markup went up despite more number of films being produced. This could either be an improvement in revenue / cost or both. 

![image](https://user-images.githubusercontent.com/12572058/187072185-9fc5fefc-4556-41f4-86be-f170bd230bd1.png)

From the plot we see a significant adoption of films during 1950-70s This could possibly be due to the introduction of an international audience, and America having temporory monopoly of film production.

![image](https://user-images.githubusercontent.com/12572058/187070612-743bb611-5d06-4d47-b9b7-958bca71baaa.png)

However, looking at the share of domestic box office, we notice that international box office did not take off during the 1950-70s. The data point at 1950s was missing, as I cannot find any mention of an oversea ban on movies.

### Horror Movies

There is a description by FiveThirtyEight that Horror seems to be a very profitable category.
Horror movies usually turn out to be great investments. Let’s see how this is happening with data.

![image](https://user-images.githubusercontent.com/12572058/187070735-dddd25ce-108a-4c48-8ff8-d72f1bf73858.png)

At the first glace, horror movies do not appear to be winning more seats than other categories, so probably they have got a better production efficieny.

![image](https://user-images.githubusercontent.com/12572058/187071637-4bc06175-1ad0-4b80-9e84-10ec1f267b4d.png)

The Horror category by far has the highest return on investment.

![image](https://user-images.githubusercontent.com/12572058/187071592-f5f7edf0-1a13-429a-8b90-e615a0eb6bcc.png)

However, there doesn't seem to be as many horror films out there as other genres.

![image](https://user-images.githubusercontent.com/12572058/187071596-edc9214e-e3b8-4ff6-bbde-53debbc860d4.png)

In fact, the number of horror as percentage of all films produced declined since 1980, with a mild reversal since mid-1990s.

![image](https://user-images.githubusercontent.com/12572058/187073022-be8c6064-2b57-4a3f-b4c0-108da084d4ea.png)

The decrease and increase of horror films could be understood through the change in cost and revenue. There was apparent traction gained mid-1990s.

### Financial View of the Matter

As a matter of nature, the higher the risk, the higher the reward. This is understood in finance through the Capital Asset Pricing Model. Let's see this in action.

![image](https://user-images.githubusercontent.com/12572058/187072295-e894735f-8547-4f0e-84bd-c87cc45ff0c0.png)

As we can see, the lower the production budget, the more unstable the return becomes. However, the expected reward also goes up.

We see that the line is slightly concave because there is a diminishing marginal return to risk, which is well understood in the financial literature, implying that production companies are less rewarded as they try out new things or when the budget is too low.

![image](https://user-images.githubusercontent.com/12572058/187072303-f2585877-81e2-4548-82fc-060a71c09b81.png)

For the horror category, a similar hierarchy exists but we don't see a curvature. This means that small horror productions are just making as good a living as bigger productions, because they are not punished for being 'small'.

### Conclusion

Not only are Horror films more profitable in general, they are relatively short in supply.

Given all this ample opportunity in the horror genre, it is a mystery why there isn't more horror films out there.
