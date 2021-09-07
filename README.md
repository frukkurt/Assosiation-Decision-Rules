
# Decision Making for Assosiation Rules  

<p align="center">
  <img width="850" alt="Screen Shot 2564-09-06 at 02 12 39" src="https://user-images.githubusercontent.com/63940535/132138685-46c8a6a2-8b77-488b-bcda-39c0531b4dec.png">
</p>

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/frukkurt/Decision-Making-for-Assosiation-Rules/blob/main/DecisionMaking_for_AssociationRules.ipynb)


## I.Introduction


**Bundle pricing** is a pricing strategy. set the price of a product by combining several products or the same product and selling them at the same price. The overall price is cheaper than the purchase price separately. cause to stimulate customers' interest in the product. The total price was reduced, resulting in more products being sold. Which such strategy is opposite to **Unbundle pricing** is that Unbundle will analyze the types of products or which types should not be sold together or sold together. Bundles are sold for less than the unbundle, which means that customers are more interested in certain products than in buying multiple items at a low price. For example, mobile phones. If you buy an empty device or an unbundle, it will be more expensive than buying it with monthly promotions. But in some cases, for example, customers do not want monthly promotions and are therefore interested in buying a mobile phone at a higher price. Maybe because the promotion is not interesting or there is a better promotion.


|  | **BUNDLE**      | **UNBUNDLE** |
| ----------- | ----------- | ----------- |
| **Pros**  | - It can stimulate sales in the same way as a price reduction without having to reduce the price of the product much and can sell a lot of products on sale.      | - Able to sell products at a higher profit per piece than a bundle|
|  | - Able to drain out of stock items that can not be sold. without having to directly reduce the price.| - It can answer or be an alternative to customers or consumers that need only one product.|
| **Cons**     | - Less profit per piece       | - It can't motivate customers because it's like no promotion for customers. |
| | | - Unable to release backlogs, other strategies must be used instead.|

**There are 3 types of bundle pricing strategy**

- 1. **Pure Bundling** is a price setting for products or services that are merged into a package and are not sold separately, such as package prices, travel, including insurance.

- 2. **Mixed Bundling** is to set the price of a product or service merged into a package, but the customer can choose whether to buy the whole package or buy one separately.

- 3. **Mix-leader Bundling** is the setting of prices provided that there is a special discount, eg a 50% discount on product or service B, but product or service A must be purchased at the normal price first. The purpose is to use Product B as a tool to help Product A, which is more profitable than selling.

To show which products should be sold together (Bundle) and should not be sold together (Unbundle) using the principles of Association rules such as the Apriori algorithm, Fp-growth algorithm, Support Correlation to indicate which bundle or relationship product is the most interesting in selling to a couple few relationships should not be sold together.

The information used was taken from a dessert shop behind Chiang Mai University. which is the data from February 3, 2020 to September 30, 2020.

## II.Methodology

**In this project :**
- **Tools**
  - `Python`
  - `Mlxtend`
- **Algorithm**
  - Apriori algorithm
  - Fp-Growth
  - Support Correlation
  - Graph network analysis
  - Paleto-front 
- **Process**
  - Data science process cycle

<img width="1000" alt="Screen Shot 2564-09-05 at 13 12 28" src="https://user-images.githubusercontent.com/63940535/132117425-002fcb61-eb02-426c-a666-9f0d963f7e20.png">



### A.	Business understanding
There is a need to analyze the products that should be sold together **(Bundle)** and should not be sold together **(Unbundle)** from the information of the confectionery store, which is an SME business that sells online and on-site, where all the information will be on-site. From February 3, 2020 to September 30, 2020 due to the period that the price has not been adjusted.


### B.	Data understanding
Understand in Data that each feature is what it means, what type of data (String, Float, Integer,....) The data is taken from WongnaiPOS, a management system that helps merchants. The data received is a `.CSV` file. Most of the features are Object (String) with the default feature, all 22 features. 

#### The data will include:

| Feature              | types      | NaN        |
| -----------          | ---------- | ---------- |
| วันที่ชำระเงิน           | object     | No         |
| เวลาที่ชำระเงิน         | object     | No         |
| หมายเลขใบเสร็จ / ID   | object     | No         |
| INV. No              | float64    | Yes        |
| รหัสถาดเก็บเงิน         | object     | No         |
| ชื่อเมนู                | object     | No         |
| ประเภทการสั่ง          | object     | No         |
| จำนวน                | object     | No         |
| ราคาต่อหน่วย           | object     | No         |
| ยอดก่อนลด             | object     | No         |
| ส่วนลดทั้งหมด           | object     | No         |
| ส่วนลดทั้งหมด %         | object     | No         |
| ราคาสุทธิ              | object     | No         |
| ประเภทภาษีของรายการ   | object     | No         |
| โต๊ะ                  | object     | No         |
| ชื่อลูกค้า               | float64    | Yes        |
| เบอร์โทรศัพท์           | float64    | Yes        |
| ประเภทการชำระเงิน     | object     | No         |
| หมายเหตุ              | object     | Yes        |
| กลุ่ม                  | float64    | Yes        |
| หมวดสินค้า             | object     | No         |
| สาขา                 | float64    | Yes        |


<p align="center">
  
<img width="1000" alt="Screen Shot 2564-09-05 at 15 12 49" src="https://user-images.githubusercontent.com/63940535/132120201-88d71e9a-e0f9-40b3-a059-6ee74ad7aab3.png">
</p>


## Exploratory Data Analysis

<p align="center">
  
  <img width="1000" alt="Screen Shot 2564-09-05 at 15 18 34" src="https://user-images.githubusercontent.com/63940535/132120340-22413572-a4a6-4f54-90d4-f5e668190e2c.png">

</p>

**The top 5 bestsellers**
- บิงซูสตอเบอรี่(Strawberry Bingsu)
- ชานมไต้หวัน(Taiwanese Milk Tea)
- บิงซูโอริโอ้ (Bingsu Oreo)
- ไข่มุข (Bubble)
- บิงซูโอวันตินภูเขาไฟ (Bingsu Owantin Volcano)

It was noticed that strawberry Bingsu and Bingsu Oreo tended to sell better, while Taiwanese milk tea and Bubble tended to sell less. It went down. Bingsu Owantin Volcano Not much has changed.

<img width="1000" alt="Screen Shot 2564-09-05 at 15 26 18" src="https://user-images.githubusercontent.com/63940535/132120518-8b0be7bc-3f7b-4961-9e3b-6548a703ffe2.png">

**The graph shows the total sales for each month.** 
  
  It is the 4th month. It's a month off from Covid-19.

<p align="center">
  <img width="650" alt="Screen Shot 2564-09-05 at 15 32 34" src="https://user-images.githubusercontent.com/63940535/132120653-1048c645-dffa-4a26-b093-726db480d825.png">
</p>

**Total sale fo each hour**

  The graph shows the total sales for each hour. In this section, the customer payout time, which means counting back approximately 1 hour. This means that the period with the highest sales volume is from 12.00 to 13.00, followed by 14.00 to 15.00 .

<p align="center">
  <img width="650" alt="Screen Shot 2564-09-05 at 15 37 32" src="https://user-images.githubusercontent.com/63940535/132120752-104d5eba-467d-417b-ad4a-d96930c0f189.png">

</p>

**The graph shows the average daily earnings and daily sales volume.**

  In which the number of sales Most sales are weekends or Friday, Saturday, Sunday, and sell a small amount during the week or Wednesday. The average income is the highest, but Saturday is not the day that sells the most. It means that on Saturday. Often, people order products that are more expensive than other days.

<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-05 at 15 39 42" src="https://user-images.githubusercontent.com/63940535/132120802-28db75ae-0681-484f-b2b7-2a887834d370.png">

</p>

**When is the highest purchase volume?**

  The graph shows the most sold periods by day and time period. which on Sundays between 14.00-15.00 will be the best seller.

<p align="center">
  <img width="800" alt="Screen Shot 2564-09-05 at 15 45 53" src="https://user-images.githubusercontent.com/63940535/132120950-edf761f4-86c9-47c7-a298-f23b382c89cc.png">
</p>


**When are the highest sales?**

  Graph showing the most earning period by day and time period. The day on which Sunday during about 14.00-15.00 will be the most income.


<p align="center">
  <img width="800" alt="Screen Shot 2564-09-05 at 15 49 07" src="https://user-images.githubusercontent.com/63940535/132121034-dea2e751-8eb9-472c-9471-4c1398e37d5a.png">
</p>

**Which type is the most ordered?**

  The graph shows the total number of products in each category. It can be noted that **take-away** products are the best sellers, with most **take-away** items consisting of bingsu, **take-away** glasses.
<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-05 at 15 53 32" src="https://user-images.githubusercontent.com/63940535/132121155-f2de6a79-ab13-48fc-b4ac-ea4e7db88423.png">
</p>

 
### C.	Data preparation
- **Data Cleansing**
  - Find `NaN` , `Outlier` , `Null` and remove empty columns.
- **Data Transform**
  -  is to convert data into usable form, such as converting data, prices, amounts into Integer/Float or date formatted as DateTime and adding features that will be needed in the future, such as weekday, hour, minute, etc.



### D.	Modeling
In this step, we will use association rules to find the relationship between products that should be sold as a pair and should not be sold as a pair. using the principles of the algorithm mentioned above.

## Market basket analysis
### Apiori Algorithm
<img width="1000" alt="Screen Shot 2564-09-05 at 15 55 38" src="https://user-images.githubusercontent.com/63940535/132121205-db464810-5c5b-4722-9a27-e514b7f1c214.png">

### Fp-Growth Algorithm
<img width="1000" alt="Screen Shot 2564-09-05 at 15 56 17" src="https://user-images.githubusercontent.com/63940535/132121229-86bb91dc-82eb-4385-8f05-a57926547acb.png">

## Graph network analysis

<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-05 at 19 19 20" src="https://user-images.githubusercontent.com/63940535/132126541-14b0e45c-ca90-49ff-aaf1-f42f57d79936.png">

</p>
#
From the analysis, comparing the Apriori Algorithm and Fp-Growth Algorithm has the same effect. There are many items that are interesting to make a bundle by analyzing support, confidence and lift.


#
**EXAMPLE:**

| Transaction   | Item |
| ----------- | ----------- |
| 1  | Apple,Beer,Rice,Chicken|
| 2  | Apple,Beer,Rice|
| 3  | Apple,Beer|
| 4  | Apple,Mango|
| 5  | Milk,Beer,Rice,Chicken|
| 6  | Milk,Beer,Rice|
| 7  | Milk,Beer|
| 8  | Milk,Mango|

  - **Support :** This says how popular an itemset in transaction, as measured by the proportion of transactions in which an itemset appears. In Table 1 below, the support of {apple} is 4 out of 8, or 50%. Itemsets can also contain multiple items. For instance, the support of {apple, beer, rice} is 2 out of 8, or 25%.
```
Support{Apple} = 4/8 
               = 50%

Support{Apple,Beer,Rice} = 2/8 
                         = 25%
```
If you discover that sales of items beyond a certain proportion tend to have a significant impact on your profits, you might consider using that proportion as your support threshold. You may then identify itemsets with support values above this threshold as significant itemsets.


  - **Confidence :**  This says how likely item Y is purchased when item X is purchased, expressed as {X -> Y}. This is measured by the proportion of transactions with item X, in which item Y also appears. In Table 1, the confidence of {apple -> beer} is 3 out of 4, or 75%.

```
Confidence{Applt > Beer} = Support{Apple,Beer} / Support{Apple} 
                         = (3/8)/(4/8)
                         = 3/4
                         = 75%
```
One drawback of the confidence measure is that it might misrepresent the importance of an association. This is because it only accounts for how popular apples are, but not beers. If beers are also very popular in general, there will be a higher chance that a transaction containing apples will also contain beers, thus inflating the confidence measure. To account for the base popularity of both constituent items, we use a third measure called lift.

  - **Lift :** This says how likely item Y is purchased when item X is purchased, while controlling for how popular item Y is. In Table 1, the lift of {apple -> beer} is 1,which implies no association between items. A lift value greater than 1 means that item Y is likely to be bought if item X is bought, while a value less than 1 means that item Y is unlikely to be bought if item X is bought.

```
Lift{Apple > Beer} = Support{Apple,Beer} / (Support{Apple} X Support{Beer}) or Confidence{Applt > Beer} / Support{Beer}
                   = (3/8) / ((4/8)/(6/8))
                   = 1
```

  As for the **Bundle**, from the `Apriori algorithm` and `Fp-Growth` data tables, support is in descending order, where **Bubble** -> **Taiwan Milk Tea** has the highest **support**, **confidence**, and **lift** , meaning that these two products are often sold. Often paired together, it seems that if there is a promotion to sell these two products together, it is better than selling separately or if you want to drain the backlog of stock, these two products are likely to be sold together. good because how These two products in the best-selling products with If these two Is there one that has a drop in sales? so that another thing will be reduced accordingly. But when you look Graph network relationship of products, **Bubble** and **Taiwanese milk tea** have a relationship with **Bingsu Oreo**, and **Bingsu Strawberry** has the opportunity to sell **Bubble** with **Bingsu Strawberry** in the other hand can sales **Bubble**  with **Bingsu Oreos** .

  In the **Unbundle section**, we mainly look at **lift** and **confidence** values, but with the `Apriori algorithm` and `Fp-Growth`, the relationship is based on the frequency of the itemset, or how often the item is in the entire transaction, and is then taken. Calculated as **support** , **confidence** , **lift** irrelevant to the number of sales Then select and adjust the parameter `min_support=0.000000001` to extract all relationships in this transaction.

 
<p align="center">
  <img width="600" alt="Screen Shot 2564-09-05 at 23 00 11" src="https://user-images.githubusercontent.com/63940535/132133399-86891c72-4201-4dc2-a635-3c674bf874a8.png">
</p>


But from the above graph, it is not possible to tell which products should not be sold together, so it is necessary to use the method to find the most suitable answer group or Pareto front. The principle is to find a product with a lift value of less than 1. and confidence with the least value and see which one is wrong. Overlay (Dominate), such as car problems. If the car is expensive, it will be more comfortable than a cheap car. But there will be an optimal point where you can choose where to buy the product.

<p align="center">
  <img height="400" width="450" alt="Screen Shot 2564-09-05 at 23 03 21" src="https://user-images.githubusercontent.com/63940535/132133488-4a7894a9-c531-45c8-a647-a9bfa3557fdf.png">
  <img height="400" width="450" alt="Screen Shot 2564-09-06 at 01 55 44" src="https://user-images.githubusercontent.com/63940535/132138244-87451d34-57c4-4733-92af-d9311d9eb92c.png">
</p>



**When we plot confidence and lift, we get the distribution as shown in the graph below and then find the optimal pareto.**

<p align="center">
  <img width="650" alt="Screen Shot 2564-09-05 at 23 05 41" src="https://user-images.githubusercontent.com/63940535/132133538-f9d5a770-78eb-4d76-b771-145935b1e819.png">
</p>

The Non-dominate set of Unbundle will consist of (บิงซูสตอรเบอรี่ -> ชาเขียวมัทฉะ)`(Strawberry Bingsu -> Matcha Green Tea)`, (ชานมไต้หวัน -> สายไหมช๊อกโกแลต)`(Taiwan Milk Tea -> Chocolate Cotton Candy)` and (สามไหมช๊อกโกแลต ->ชานมไต้วัน)`(Chocolate Maidens->Taiwan Milk Tea)` and in the Bundle side includes (ไข่มุก -> ชานมไต้หวัน)`(Bubble) -> Taiwan Milk Tea)`

<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-05 at 23 10 51" src="https://user-images.githubusercontent.com/63940535/132133668-a0260e04-7b59-413a-92b3-1db91b3e809c.png">
</p>

## Correlation

<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-05 at 23 17 59" src="https://user-images.githubusercontent.com/63940535/132133913-30497a57-c071-4b84-a0a2-130f627627cd.png">
</p>

From the correlation, it can be noted that `Taiwanese milk tea` tends to have a negative relationship with different *flavors of Bingsu*. There is a very positive relationship with `Bubble`. That is, different *flavors of Bingsu* tend to be more difficult to pair with `Taiwanese milk tea` more than `Taiwanese milk tea` paired with `Bubble`. Its meaning `Strawberry Bingsu` `Chocolate Bingsu` `Owantin Bingsu` `Volcano Bingsu` `Fresh Milk Bingsu` ` Chocolate Cotton Candy Bingsu` should not be sold with `Taiwanese milk tea`. `Strawberry Bingsu` should not be sold with `matcha green tea` as an unbund. `Taiwanese milk tea` should be sold with `Bubble` as a bundle.

## Support Correlation
<p align="center">
  <img width="500" alt="Screen Shot 2564-09-05 at 23 24 22" src="https://user-images.githubusercontent.com/63940535/132134087-1f5af8ab-5a70-432f-a7c3-2467ea8496d6.png">
</p>

<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-05 at 23 25 17" src="https://user-images.githubusercontent.com/63940535/132134118-c53bc4ac-73bf-44ab-8668-58f9ca52ca4c.png">
</p>

### Bundle
- **Support and Support Correlation**
<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-05 at 23 50 30" src="https://user-images.githubusercontent.com/63940535/132134836-a20cb705-c983-4e4c-894c-0e0da5a56761.png">
</p>

- **Confidence and Support Correlation**
<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-05 at 23 51 19" src="https://user-images.githubusercontent.com/63940535/132134866-96af0c46-910d-4a67-98c3-ef790d0fbe79.png">
</p>

- **Lift and Support Correlation**
<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-05 at 23 52 08" src="https://user-images.githubusercontent.com/63940535/132134884-ba83396c-443d-411a-9cba-fa6f43d6f704.png">
</p>

### Unbundle
- **Support and Support Correlation**
<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-05 at 23 53 56" src="https://user-images.githubusercontent.com/63940535/132134945-7500680e-fefa-4e88-93eb-3d1b7c7ee2a6.png">
</p>

- **Confidence and Support Correlation**
<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-05 at 23 54 22" src="https://user-images.githubusercontent.com/63940535/132134959-5203c4d5-6d06-4133-a4cd-316015dbbf72.png">
</p>

- **Lift and Support Correlation**
<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-05 at 23 54 52" src="https://user-images.githubusercontent.com/63940535/132134971-810ee51e-0efc-47f0-8302-5cb4a209942a.png">
</p>

## III.Result 
### E.	Evaluation
<img width="1000" alt="Screen Shot 2564-09-05 at 23 55 29" src="https://user-images.githubusercontent.com/63940535/132134988-b38fab73-3a99-460a-9924-20daad654444.png">

From both tables when considering What appears in the **Bundle** table is that `Bubble -> Taiwan Milk Tea` and `Taiwan Milk Tea -> Bubble` have the same amount that appears in each algorithm, different from other products, which means the strength of the `Bubble` must be sold with that `Taiwan milk tea` will have the most That means that if you want to hold a promotion or want to clear the stock of `Taiwanmilk tea` or pearls, it will have the most opportunity to sell. In terms of **Unbundle**, `Strawberry Bingsu -> Taiwan Milk Tea` and `Strawberry Bingsu -> Matcha Green Tea` had the highest number of appearances in the Algorithm. Next `Strawberry Bingsu -> Pearl` `Bingsu Oreo -> Thai tea` and `Taiwan milk tea -> Chocolate cotton candy` At first, Association rule and Graph Network said  that can sell bundles.
<p align="center">
  <img width="1000" alt="Screen Shot 2564-09-06 at 00 01 22" src="https://user-images.githubusercontent.com/63940535/132135158-6152d8f5-7c4a-4747-99a7-8c710f966972.png">
</p>


According to `Aassociation rules` , the base section `Strawberry Bingsu-> Bubble` conflicts with  `correlation`  `support correlation`  `lift`  `confidence`  `pareto front` meaning that the original product, possibly a bundle, will not be a ***bundle***, so it becomes an ***unbundle*** instead.

### D.	Deploy
``
*NO DEPLOY IN THIS PROJECT
``
## IV.Conclusion & Discussion
To adjust the Parameter:

  - `Association rules` that in finding the main bundle, Apriori-Algorithm and Fp-Growth get the same number of bundles. The set value is min_support = 0.01 because if more than that, the number of products that can be sold together will be very small, which will determine the It is difficult to correlate and min_threshold (confidence) = 0.01, because the minimum reliability of the rules is required. Some rules support very little, but the confidence is high. Pairs that should all be sold together and use the same min_threshold (confidence) = 0.01, because if the minimum trust of the resulting rule is changed, pairs under the same confidence will be lost. But in the process of unbundling, it is necessary to use Pareto front to help group the products that are probably not worth selling together.
  - `Pareto front` will set that This section is used to find the pareto front, which is often used in multi-objective problems. We have to set an objective, for example, which point in the graph is not dominated by other points, which is like a point. The set margins we will consider in this study use Pareto front to find both the bundle and the unbundle to take into account the set to be considered. For example, Lift and confidence are set to plot the graph between lift and confidence. If any point is at the bottom edge and is not overlapped by the others, it is pareto front. set to minimum (lift), minimum (confidence), or in confidence and support correlation, it is used as maximum (confidence). maximum. (Support correlation)

## V.References
**BUNDLE & UNBUNDLE PRICING**
[1] omniaretail.com,*What is Bundle Pricing?*,Omniaretail is dynamic pricing software ,retail software engineer and retail strategy consultant. [Online] Available: [omniaretail.com](https://www.omniaretail.com/blog/what-is-bundle-pricing)

[2] deloitte.com,*Unbundle products and services* ,Deloitte provides industry-leading audit ,consulting, tax and advisory services .[Online]Available: [deloitte.com](https://www2.deloitte.com/us/en/insights/focus/disruptive-strategy-patterns-case-studies/disruptive-strategy-unbundling-strategy-stand-alone-products.html)

[3] Medium.com,*The Advantages and Disadvantages of Bundle Pricing Strategy* [Online]Available: [Medium.com](https://price2spy.medium.com/the-advantages-and-disadvantages-of-bundle-pricing-strategy-ce479c66e134)

**Algorithm**

[4] Apriori algorithm, *Fast algorithms for mining association rules*.[PDF] Available: [Apriori](http://www.vldb.org/conf/1994/P487.PDF)

[5] Fp-Growth, *Practical Data Mining:FP-Growth*.[Slide] Available: [Fp-Growth](https://www.slideshare.net/sitake/practical-data-mining-fpgrowth-44550757)

[6] Support Correlation, *Mining strongly Correlated item pairs in large Transaction databases*.[Paper] Available: [Support Correlation](https://www.researchgate.net/publication/255712975_Mining_Strongly_Correlated_Item_Pairs_in_Large_Transaction_Databases)

[7] Graph network analysis, *An Introduction to Graph Theory and Network Analysis*.[Online] Available: [Graph network analysis](https://www.analyticsvidhya.com/blog/2018/04/introduction-to-graph-theory-network-analysis-python-codes/)

[8] Paleto-front, *Multi-Objective Optimization using Evolutionary Algorithms*.[PDF] Available: [Paleto-front](http://sc.npru.ac.th/article/file/1391930371.pdf)


**Tools**

[9] MLXTEND, *Association Rules Generation from Frequent Itemsets*.[Online] Available: [MLXTEND](http://rasbt.github.io/mlxtend/user_guide/frequent_patterns/association_rules/)


**Process**

[10] Coraline, *Data Science Process Cycle*.[Online] Available: [Coraline](https://www.coraline.co.th/single-post/2018/11/26/data-science-process-cycle)

