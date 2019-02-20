---
title: "Create A Monte Carlo Simulation"
date: 201-02-23
tags: [Monte Carlo, Excel]
excerpt: "This is the excerpt"
mathjax: "true"
toc: "true"

---

# Creating The Model


For our project, we did a Monte Carlo analysis of RxPlus, Inc. is a Midwestern pharmaceutical company that discovered a potential drug breakthrough in the laboratory and needs to decide whether to go forward to conduct clinical trials and seeks FDA approval to market the drug. Total R&D costs are expected to reach $800 million, and the cost of clinical trials will be about $150 million. The current market size is estimated to be 2 million people and is expected to grow at a rate of 3.5% each year. In the first year, the company estimates gaining an 8% market share, which is anticipated to grow by 25% each year. It is difficult to estimate beyond five years because new competitors are expected to be entering the market. A monthly prescription is anticipated to generate revenue of $140 while incurring variable costs of $40. A discount rate of 8% is assumed for computing the net present value of the project. The company needs to know how long it will take to recover its fixed expenses and the net present value over the first five years.


First, the parameters were defined for the spreadsheet model. The certain inputs for the model were the discount rate, monthly revenue, monthly variable cost, and the first year market share. For the uncertain inputs, they were market size, R&D cost, Clinical trial cost, annual market growth factor, and annual market share growth rate. For each of the uncertain input the average, minimum, maximum, standard deviation, and distribution type were determined where applicable.

<img src="{{ site.url }}{{ site.baseurl }}/images/MonteCarlo/MonteCarlo1.png" alt="Test">


For the Model we begin at year 1 and end at year 5. Each year the market size increases based on the market growth rate and the market share is updated based on market share growth rate. From there we determine the annual sales by multiplying the market share percentage to the market size. Finally, profit is calculated by subtracting the revenue from the cost

<img src="{{ site.url }}{{ site.baseurl }}/images/MonteCarlo/MonteCarlo2.png" alt="Test">

After the annual profit is determined, the cumulative net profit is calculated. For the first year, the total project cost is subtracted from year 1 profit. After each year, profit is added to the previous year cumulative net profit. The net present value is then calculated using the Excel built-in function NPV( ).

<img src="{{ site.url }}{{ site.baseurl }}/images/MonteCarlo/MonteCarlo3.png" alt="Test">

# Analyzing the model

After running 1000 simulations on the model, it was found that by the fifth year of the drug being in the market, there is a 92.50% chance that it has a net present value of greater than or equal to $0. We also found that average NPV after five years was $357,729,309.68.


<img src="{{ site.url }}{{ site.baseurl }}/images/MonteCarlo/MonteCarlo4.png" alt="Test">

To improve this model, collecting better information on the market size and R&D cost about its true value or distribution can reduce variance leading to a much better model. Looking at the tornado chart we find that market size and R&D cost with the largest correlation to NPV

<img src="{{ site.url }}{{ site.baseurl }}/images/MonteCarlo/MonteCarlo5.png" alt="Test">

Looking at the Trend Chart we can expect the average Cumulative Net Profit to be above zero by year 4 . We also can see that by year four we are  90% likely that the cumulative NPV will be between -$180,000,000 and $620,000,000

<img src="{{ site.url }}{{ site.baseurl }}/images/MonteCarlo/MonteCarlo6.png" alt="Test">

you can [get the excelsheet]({{ site.url }}/assets/MonteCarloProject.xlsx) directly.
