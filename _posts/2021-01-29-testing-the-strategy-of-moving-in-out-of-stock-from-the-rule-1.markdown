---
layout: post
title:  "Testing the Strategy of Moving in & out of Stock from the Rule #1 Book on Investing"
description: "A test of the technical analysis strategy offered by the book on a real-world example"
date:   2021-01-29 12:06:31 +0200
categories: investing
---
I found the [Rule #1](https://www.goodreads.com/book/show/24006.Rule_1) book on Youtube while poking around the clickbaity videos recommending books on investing. The channel giving the book especially great amount of praise was [New Money](https://www.youtube.com/channel/UCvSXMi2LebwJEM1s4bz5IBA) with around 200k subscribers. At the time of writing this, it had an average rating of 4.09 with 2k+ reviews on Goodreads. This made me think that the book is actually good and gives solid advice. Which I think it did, but one part of in particular sounded especially good and it also happened to very testable against real-world data.

In the Chapter 12 the author gives a number of technical indicators to use for jumping in and out of a stock. Instead buying and holding a stock of a company, he suggests you should be constantly “moving in and out with the big guys”. By this the author means that you should be looking at the charts and be on the lookout for a signal when “the big guys” are moving in (buying stock) or moving out  (selling) and simply follow their lead to reap the benefits.

<!-- I don’t want to review the whole book since I don’t really think I’m competent enough to give an investment book a review. I have a modest amount of money in the stock market and most of it is in the all-market ETFs. I want to focus instead on a particular part of the book where author -->

In the Chapter 13, the author then gives us an example of a couple following this strategy:

> By getting in just below $19, and then moving in and out 11 times in two years with the big guys, and by adding in $500 a month they were saving, by July 2005, CAKE gives Doug and Susan a nice compounded rate of return of 56 percent per year, and their $20,000 is now worth $78,000.

56 percent per year! In a company which had 7 year equity growth of 19% and EPS growth of 22%. That seemed crazy to me and frankly got some part of me VERY excited. But then I decided to go and test this strategy on a real data.

I picked Amazon Inc (AMZN) because it kind of matched the other criteria for picking a stock in the book -- it had mostly strong “the Big Five” numbers, as the book calls them - ROIC and growth rates for equity, sales and EPS. I decided to randomly pick a period in the market, get some fancy charts going and see if I would make more money if I invested and followed this strategy.

For charting I used [tradingview.com](tradingview.com) website, which offers a lot of functionality for no money. I managed to build a view like this:

{: .centered.v-whitespace-happy}
![tradingview chart](/assets/tradingview-chart.png)

It shows all 3 technical indicators the book is suggesting to follow -- the Moving Average (the purple line in the top chart), the MACD indicator (middle chart) and a stochastic (bottom chart). I’m using Exponential Moving Average with length value of 10 and 14-5 parameter combo for the stochastic. Both configurations are following the advice from the book. Those are the Tools.

## Buy & Hold vs The Tools

So let’s pick a period randomly and compare two strategies -- first being a simple “buy & hold” strategy and the second using The Tools, i.e. moving in and out of owing the stock by following the MACD, stochastic and moving average indicators, when all 3 give us the “buy” or “sell” signal.

Let's select a period from December 2018 to June 2019. I picked this period because I simply liked the shape of the price chart - generally trending up, with no macro changes increasing volatility or anything like that. I then picked a point to enter the market which isn't bad and isn't perfect either —  we're not maximizing profit in a given time window, but simply testing strategies. I went with December 18, 2018, at the price of $1190. For the end date I picked somewhere in around 6 months, with a good opportunity to sell, which happened to be June 15, 2019 with the price of $1665.

### Buying & Holding

The math here is very simple -- we bought the stock at $1190, held it and then sold on June 15 at $1665, collecting $475 in profit.

{: .centered.v-whitespace-happy}
![Buy & Hold](/assets/buynhold.png)

### Using The Tools

In this strategy, after buying the stock we wait for signal to sell, because we’d like to follow the movement of the big guys. Once sold, we wait for the signal to buy. The signals need to come from all 3 indicators:

{: .centered.v-whitespace-happy}
![MACD](/assets/macd.png)

{: .centered.v-whitespace-happy}
![Moving Average](/assets/ma.png)

{: .centered.v-whitespace-happy}
![Stochastic](/assets/stochastic.png)

I attempted to follow the strategy precisely and imagine I can’t look ahead in the chart and just act by looking at the 3 indicators only. I was acting only when:

1. The price line was crossing the 10-day moving average.
2. The “valleys” in MACD seemed like they were beginning movement into “mountains” and vice-versa.
3. The stochastic buy & sell lines were intersecting signalling oversold/overbought market conditions.

Following this strategy, this is the result I ended up with:

{: .centered.v-whitespace-happy}
![result](/assets/result.png)

One thing that immediately stood out to me was the total number of movement I has to do -- between the initial buy and the final sell I did 10 additional moves in or out of the market. I ended moving as much as Doug and Susan from the example in the book did in 2 years. I looked the charts of CAKE in the early 2000s to see if the stock was less volatile than the one I was trading (AMZN), but it didn’t seem to be. Weird.

Now let’s look at the numbers. If I put all of the buys and sells in a spreadsheet, this is what I get:

{: .centered.v-whitespace-happy}
![crunching numbers](/assets/spreadsheet.png)

The Cash Balance column is the amount of money I get to keep after moving in or out. The last cell in the Cash Balance is how much I ended up with after selling on the June 15 at $1665 price, same as in the Buy & Hold experiment. I didn't get to keep all $1665 from my selling -- I was down $189 from the previous movement, so my total profit by the end of this adventure was $1476, which is $189 than my profit from simply buying and holding ($475).

I repeated this exercise a couple more times on different time windows and I didn’t manage to get a consistently better result with The Tools. In fact out 4 attempts, I had only one success with getting $59 more than simply holding stock. Also, in a time window with price trending down, losses from moving in & out were accumulating much faster and hurting really badly.

## Takeaways

I have to admit I was very disappointed. Before to the chapter on technical analysis, the book seemed very credible and sane to me. I still think it's a worthy read and teaches good basics on how to pick a stock to invest in by looking at the company's fundamentals. But the chapter on technical anaylsis (Chapter 12) and the clearly made-up example after it need to be taken with a HUGE grain of salt. 56% return in the example in Chapter 13 sounds way too good to be true and is probably made up or cherry-picked to sell the idea to readers.

Another takeaway for me personally is that good reviews of a book about investment don't necessarily mean everything the book recommends is a good idea or is proven to be true. In fact, I'd say the better something sounds, the more likely it's either untrue or too risky.


