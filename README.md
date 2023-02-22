# 1. REQUIREMENTS ANALYTICS AND BI SOLUTION CYCLE: 

![image](https://user-images.githubusercontent.com/91537767/220582974-925a6f7d-6faf-4417-961e-e7d816a18354.png)

1.1 Identify deliverables

Because it would take too long to assess and present the metrics within three months. To make metrics easier to grasp initially and to maintain, DBA separates them into two parts. The KPIs of traffic, client retention, and category management will be the primary emphasis of phase 1. The team will explain why our business's client reach has reduced using these figures. Phase 2 will begin as soon as this project is completed. To reduce modification requests while the data team is working on the project, this strategy was accepted by the business team and includes the signatures of both teams.

![image](https://user-images.githubusercontent.com/91537767/220583478-f88bfbec-0278-4640-9509-23db6c76a434.png)

1.2 Identify data requirements

![image](https://user-images.githubusercontent.com/91537767/220583642-0aea69fb-7134-4d40-bc65-0122279ed007.png)

Besides internal data provided by Data Engineers, BI also needs some external data sources such as Customer Behavior, Category Information on other platforms.

1.3 Cleanse

After loading all data files into PowerBI, the BI team will check data quality first in the Power Query window.

![image](https://user-images.githubusercontent.com/91537767/220583866-7d7272cb-d947-4e17-b555-1412598c394d.png)


All columns in the Users table are qualified at the maximum rate. The percentage of valid value is totally 100%. Empty and Error Value are 0%.

![image](https://user-images.githubusercontent.com/91537767/220583931-d7f52a7e-8ea5-4223-ad5f-9024faac98dd.png)
![image](https://user-images.githubusercontent.com/91537767/220583956-2ce399af-25d2-49ff-9d7f-42f0a03383d7.png)

Is the same as the Users table, all columns in the 2 tables: Events and Orders have the maximum quality rate. However, only the Item table has 2 columns: Adjective and Modifier columns aren't entirely accurate (88% for adjectives and 64% for modifiers).

![image](https://user-images.githubusercontent.com/91537767/220583998-3b3a0638-b42f-47b4-b30e-c184d1982a18.png)

The team came to the conclusion that certain values in both columns are simply empty and do not represent mistakes. Thankfully, the team has established a pattern for these columns that places the adjective as the first word and the modifier as the final word from left to right. As a result, using this rule using Power Mcode in the Power Query window, we may quickly fill up blank data.

![image](https://user-images.githubusercontent.com/91537767/220584031-f7406a73-e51f-432f-848c-ef6bb8e8fed5.png)

Values in these columns after filling in the blank value and then, the team has the data reaching at the highest quality rate.
In addition, we removed unnecessary columns to reduce data capacity.

1.4 Design data model

Fact Event table have 2 relationships:

- Many-to-one with Dim Date. (EventTime - Date)
- Many-to-one with Dim User. (User ID - UserID)

Fact Order table has 3 relationships:

- Many-to-one with Dim Date. (CreatedAt - Date)
- Many-to-one with Dim User. (UserID - UserID)
- Many-to-one with Dim Product. (ItemID - ProductID)

1.5 Exploratory Analysis

Before applying diagnostic analytics, we use the descriptive analytics method to visualize all the metrics first to have a glance at the data and find the factors to analyze then.

* Metric 1: Number of Sessions:

![image](https://user-images.githubusercontent.com/91537767/220584826-49928b4f-646a-45c7-b314-a9a6503d1e4f.png)
 
Figure 13. Number of Sessions this Month compare vs Last Month & Number of Sessions Monthly.

In general, traffic in 2017 and 2018 barely increased ( skip June 2018 because the data is not available for the full month of June). Despite the chart's minor rise, it appears as though the growth is progressively slowing down.

![image](https://user-images.githubusercontent.com/91537767/220584851-d2f5c982-0647-42a5-b80f-09fcbbd68189.png)
 
Figure 14. Number of Sessions by platform Monthly in 2018

Web is the platform with the largest traffic when looking at the number of sessions by platforms, more than the combination of mobile and tablet. The percentage of traffic on the platform has not changed much. The team may thus draw the conclusion that platform is not what influences consumer reach.

* Metric 2: Hourly/ Weekly Traffic:
 
![image](https://user-images.githubusercontent.com/91537767/220584896-f5f7e977-b961-4824-89b0-6b111b8fcb64.png)

Figure 15. Weekly Traffic

In this figure, there is no difference in traffic percentage among days of the week. The difference between the percentages of the highest and lowest traffic is only 0.02%.  It's really insignificant to conclude that day of week is the deciding factor on traffic.

 ![image](https://user-images.githubusercontent.com/91537767/220584956-6cdcb8f3-0f0b-442d-8ec6-073a356626f4.png)

Figure 16. Hourly Traffic

The team identifies the two times when users use the app most frequently as 1AM:3AM and 11AM:12PM when looking at hourly views in further detail. However, there isn't much of a difference between the times. The day with the most equally spread traffic is Monday.

* Metrics 3: Avg. screens per 1 session 
 
 ![image](https://user-images.githubusercontent.com/91537767/220584992-3bd38dd4-31d1-4a99-88bd-ac2e6ef0ed30.png)

Figure 17. Average Screens per 1 Session.

The average number of screens per session monthly has complex fluctuations, but it usually comes approximately to 2. In addition, by the figure, the decrease in this metric is evidentable over time and the slope of the metric line is very high. 2 screens per session is not a high number and thus the company will be seriously warned if it starts to decline.
* Metrics 4: Active customers
 
 ![image](https://user-images.githubusercontent.com/91537767/220585015-1343b4f3-ebc9-470c-8ee3-bfff9eb28033.png)

Figure 18. Active User & Total User & % Active Monthly.

This figure illustrates that the number of active users accounts for a tiny percentage comparison with the total user.  Even if the total number of users is rising silently and uniformly, the percentage of active users, which is typically at 3%, is also beginning to decline.

* Metrics 5: New customers
 
 ![image](https://user-images.githubusercontent.com/91537767/220585051-26463724-268d-4454-bcea-6c6a7bc2e8ca.png)

Figure 19. New User & Deleted User Monthly

While the number of deleted users has considerably dropped after August 2017, the number of new users regularly increases but not equally. Although the firm is showing signs of growth, the marketing team has a hurdle in making use of these users.

* Metrics 6: Retention customer
 
 ![image](https://user-images.githubusercontent.com/91537767/220585080-3456a9e4-5d8c-4146-80a4-a160366a5bf4.png)

Figure 20. Retention User & Active User Monthly

Excluding January 2017, Retention Users maintains a steady monthly count but percentage of user retention with active users is quite low.

![image](https://user-images.githubusercontent.com/91537767/220585120-97be3ee0-c575-4d5f-9c0c-b6e452d48400.png)

 
Figure 21. User Funnel Monthly

User Funnel Chart shows the user’s conservation rate of the company.  Total Valid User is the user who has not deleted their accounts. Active user is the user opening app in the selected month. Retention user is the user opening app in the selected month and also opened app in the previous month of the selected month. Finally, the conversion rate is just over 5%.

* Metrics 7: Churn rate
  
 ![image](https://user-images.githubusercontent.com/91537767/220585144-444ebb36-1cb8-4624-aab3-0de96dfa7f53.png)

Figure 22. Churn User, Active User & % Churn Rate Monthly

A significant portion of all monthly active users are accounted for by churn users, and this number has not decreased. That is followed by the bounce rate, which continues to be quite high (over 80% each month).

* Metrics 8: Number of Category 

![image](https://user-images.githubusercontent.com/91537767/220585184-72207fd3-494e-4ea0-be66-4aac190029a2.png)
 
Figure 23. Number of category and number of products by Category, Price Segment

There are 10 categories and 3 price segments in the product list. In general, product quantity in each category has no big difference. Bronze is the segment with the most products. Silver also have a middle quantiy at apparatus and contraption category. Gold products account for a very small amount. 
 
 ![image](https://user-images.githubusercontent.com/91537767/220585213-d467f517-6b34-414c-afd6-a35bd4e8213c.png)

Figure 24. Number of sessions by Category, Price Segment

Following the figure above, the number of sessions is also the same with the product quantity. The Bronze Segment performs outstandingly with the others segment. 

* Metrics 9: Top most viewed products/ top selling products

 ![image](https://user-images.githubusercontent.com/91537767/220585234-7919cad3-4d0d-42ef-b59c-a3bbb1294f63.png)

Figure 25. Top Viewed Products

 ![image](https://user-images.githubusercontent.com/91537767/220585249-3ac96bb2-7bc2-44f3-94ac-41adeebb1c95.png)

Figure 26. Top Selling Products

The two figures above illustrate top products having the most views and the most sales. Products in both top lists do not overlap, indicating that although they are receiving plenty of views, sales may not be as high as expected.

# 2. VISUALIZATION AND REPORT ANALYSIS
2.1 Craft a compelling story

![image](https://user-images.githubusercontent.com/91537767/220585711-36eacf24-7d2f-43f6-85f4-a7451122980b.png)

Figure 39. Dashboard Appearance

Dashboard will show the key metrics by month and year that the user will select to view. Main metrics which the users want to track will be shown first and shown by trendline charts. Next, the team will show the factors we have analyzed to find the cause of the trend or some factors that really impact the main metric. The team will next conduct a thorough examination of these aspects.
 
![image](https://user-images.githubusercontent.com/91537767/220587302-f6b9d5e8-b9ab-40a8-b7a8-731059b65a19.png)

Figure 40. Number of Sessions of Latest 4 Weeks Comparing with 4-week backwards.

The most recent month did not experience a rise in the number of sessions, and it is clear that this trend will continue over the next months based on traffic statistics from the last four weeks compared to the four weeks prior.

![image](https://user-images.githubusercontent.com/91537767/220587328-3b722acd-3a19-4f94-9630-e6d5a67de6a2.png)
 
Figure 41. Average Screens per Session trend line.

It can be seen that avg screen is trending up but decreasing more immediately after that from 2017 to 2018, starting from April 2018 there was a marked decrease and no sign of increasing again. 
 
![image](https://user-images.githubusercontent.com/91537767/220589706-ab0f9f94-f935-4bfc-9b69-104199b1713e.png)

Figure 42. Average Screens per Session by platform trend line.

We can observe the number of visitors on 3 platforms: mobile, tablet and web. On the mobile platform, the number of visits decreased markedly and rarely saw an increasing trend. For tablet platforms, the chart still shows a larger decrease, and finally for web platforms, the increase is also negligible, only from 1977 to 1987.

![image](https://user-images.githubusercontent.com/91537767/220589739-b6d1440f-3e51-46a4-ab12-c9a2fa23f85b.png)
 
Figure 43. Traffic Hourly and by days in week.

Based on traffic data by time frame of weekdays, we can only see that the traffic have a great similarity between weekdays and are almost equal. But analyzing more deeply into each specific time frame, the data team realized that the 1AM:3AM and 11AM:12PM time frames mark a larger amount of traffic than other time frames because these are the hours when users have a high demand for workspace or entertainment.
 
 ![image](https://user-images.githubusercontent.com/91537767/220589769-0c263552-71cb-41bb-ad84-0f766758e296.png)

Figure 44. Traffic by Platform Type.

Because it is the morning shift's busiest hour and many individuals use laptops to access the internet, the 11 AM to 12 PM time period provides a significant volume of online traffic. In contrast, people typically use their mobile devices for pleasure and convenience in bed after a long day at work, therefore the 1AM–3AM time period saw a spike in the amount of people utilizing their mobile platform to access our app.
 
![image](https://user-images.githubusercontent.com/91537767/220589789-3d3f51ea-5a0a-4c80-b3aa-0b5a946ed10f.png)

Figure 45. Traffic of the last 2 weeks by hour.

`	Based on the traffic data of the current week compared to the previous week, we can see that the 1AM-3AM time frame recorded a slight decrease and the 12PM-3PM time frame has a sudden decline and needs attention for business strategic actions to recover.
 
![image](https://user-images.githubusercontent.com/91537767/220589823-ce8c34c7-cb44-4ebf-885e-1e889a522163.png)

Figure 46. Active, Deleted, New, Retention and Churn User Monthly in 1-page.
 
![image](https://user-images.githubusercontent.com/91537767/220589859-ce233fc6-fcb4-4ed3-b32c-be6af0af3a2b.png)

Figure 47. User Conversion Funnel.

According to the charts from the dashboard above, we can summarize the causes of the decrease in traffic including:
+	Figure 1 - Active user, total user and % active monthly: It can be seen that a lot of new users are generated, however, the percentage of real active users is very few of them, while active users are customers that will bring traffic.
+	Figure 2 - Deleted user and new user:  New users are created a lot but the amount of deleted users do not increase. Although this is a positive point, the marketing team has not taken advantage of this effectively yet. 
+	Figure 3 - Churn user, active user and churn rate monthly: the percentage of churn user over all active user is quite alarming, about 85%, which means that most users tend to leave rather than stay on the website .
+	Figure 4 - Retention user and active user monthly: Low customer return rate. According to statistics, 80% of traffic comes from 20% of loyal customers → this is the main reason why traffic drops.
+	Figure 5 - Conversion rate: Compared to the total number of users (about 120K), the number of valid users is only about 94K, of which just over 44K are active users. Retained users are counted as over 6K, which is 5.5% of total users.
 
![image](https://user-images.githubusercontent.com/91537767/220589904-5efcc1df-3427-4b76-b357-4eb9713865cb.png)

Figure 48. Referrer Events Last 10 Weeks.

The first thing you should realize is that how active users heavily depends on Referrer Events of your company. One of the reasons is these events are not attractive enough to attract new users and retain customers. Businesses should need to increase their marketing efforts in order to grow the customer base. 
 
![image](https://user-images.githubusercontent.com/91537767/220589932-548d34a9-c05f-4beb-ab52-9c45265704cf.png)

Figure 49. Traffic by Event Type.

Traffic mostly comes from watching products and introducing new user, the rate of introducing new people is equal to the rate of watching products, which proves that users only run programs to earn points and products. They would check whether there was an external and internal factor that could have impacted users. An illustration of the external factor is a new competitor's debut or an existing competitor's release of a potent feature. 
In terms of category and price segment, there is no difference found when the number of views of the product corresponds to the number of products, that means, the more products the segment has, the easier it is to have more views. The team have tested some analysis that drill each segment into fields such as modifier and adjective to have a quick view and  draw some conclusions.
 
![image](https://user-images.githubusercontent.com/91537767/220589968-4a78de01-1986-4149-b48c-17ab5c06eee7.png)

Figure 50. Waterfall chart of traffic by price segment and modifier.

In general, all price segments have a decrease in traffic for modifiers. The Bronze segment has the strongest decline, followed by the Silver segment and finally the Gold segment. Products with modifiers in a cheaper segment have the largest amount of traffic but also have the most drastic decrease, focusing on some modifiers including how-to-manual, refill, wrapper, opener, charger.
 
![image](https://user-images.githubusercontent.com/91537767/220589991-016704b7-832d-45d2-9f3d-058687d1b653.png)

Figure 51. Waterfall chart of traffic by price segment and adjective.
Most of the products with modifiers above have a decrease in traffic in many adjectives. The traffic changed in a negative way, The Bronze segment continued to have the biggest drop, focusing on some adjectives including fuzzy, rechargeable, aerodynamic, prize-winning, reflective. 
 
![image](https://user-images.githubusercontent.com/91537767/220590015-a09c2d5a-485e-4869-951e-1d7170829bf6.png)

Figure 52. Top 5 viewed products and top 5 selling products.

Items that attract a lot of traffic but receive little purchases, as seen by the graph of the top 5 most viewed products and the top 5 best sellers. Bounce rates - the proportion of visitors who briefly browse a product page before leaving - have been rising over time. The reason is that even if there are a lot of visits due to the poor conversion rate, there are less buyers for this product than for others even though there are fewer views.
Conclusion: Traffic in this month declined because the impact of these factors below:
- Platform: Tablet and Mobile.
- Timeframe: 1AM:3AM and 11AM:12PM are the timeframes brings users and traffic the most in the past but they have decreased recently.
- Churn rate is high and retention rate is low as well.
- Reference Program is not interesting enough to bring more user.
- Modifier and Adjective: a list of modifiers and adjectives above.

2. Security Management

The team will intervew the business team to get the list of users which they want to share the report and dashboard with. To ensure less risky and high data governance, the data team also wants to know the role of each person and their detailed permission to grant access to the dashboard and set rules for them. After working closely with the business team, we finally have the users’ list.

![image](https://user-images.githubusercontent.com/91537767/220590893-43188880-789c-4b1e-80b8-b53948e6a402.png)

Table 6. List of users and their permission.

Based on the table above, the data team will set-up all charts on the dashboard to show correspondingly to each user. The user when using dashboards will be aware that they can see that data that are in their permissions. Therefore, some error charts are shown because they are not for their usage and not in their permissions as well.

![image](https://user-images.githubusercontent.com/91537767/220590175-c110e9bf-be08-4c93-888a-7077bbd2564f.png)
 
Figure 53. List of view as user role

The team has added the list that the business team giving and defined 4 groups will access the dashboard. The Bronze group only sees the numeric related to the product belonging to the bronze segment.There are the similar to the Silver and Gold group. The Group name Other is a group of managers who have full permissions and make a decision based on the overall picture the data team has visualized.

