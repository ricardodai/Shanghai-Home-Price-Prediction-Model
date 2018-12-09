# Shanghai-Home-Price-Prediction-Model
Constructed a stacked model based on ExtraTree, LightGBM, and MLP to estimate price the second-hand house unit in Shanghai based on the current listings in the market.

### BACKGROUND
Last year, to inhibit uncontrollable housing price inflation and to stabilize the volatile housing market, Chinese government formulated and promulgated a series of policies to pause the vicious circle induced by real estate speculators. However, policy can only influence the market but cannot predict market trends, especially this market of house purchasing with such high income elasticity. Not to mention that the operation mode of China"s house market has its lethal problem in the long term; this industry is always threatened by unprofessional management of related organization and cutthroat competition from peers. For a long period of time, the public confidence in the real estate industry has sagged due to its market confusion and unclear pricing norms, which is more like a game for capitalists rather than a market competition between suppliers and demanders.

### Business Understanding

With that in mind, our team sees the chaos of China"s housing market as a consequence partially due to the opacity and inequality of information between buyers, sellers, and real-estate agencies. To break such information asymmetry, I decide to develop a data mining solution that provides users a clear pricing mechanism and a systematic way to find the price of unit that aligns with the actual market demand and supply. ）. More precisely, I want to predict the listing price of second-hand housing in Shanghai, given their numeric (year of construction, usable area, total floor, etc.) and textual(orientation, floor position, district, etc.) description. To obtain representative data, I crawled the raw data from WUBA, which is the only company in China listed in NYSE among all online platforms for second-hand property sale/rental. I crawled all listing prices and corresponding descriptions of reselling houses in Shanghai of 2018. For this project, I focuses only on the second-hand housing market in Shanghai. Since every city/area has its unique market characteristics related to the policies of local government, level of economic development and other relevant factors, which cannot be simply generalized. This project aims to design a regression model to predict listing prices of second-hand housing from all these information, which can then be used to price houses/apartments that need to be resold.

Such mechanism is of profit to households, buyers, and real-estate agencies. For property owners, our model can provide the accurate market value of the property for reselling such that, firstly, they can have a clear market position and price range for their estate, and secondly, they can achieve the maximum ROI by comparing the potential return between reselling, renting, and living. For potential buyers, they can use the model to check the price level of different types of houses in different districts to find the best-fit that meets the budget level, or they can adjust their budget accordingly to choose the one with better dwelling conditions or with higher future value such as their children can be better educated in this district than in other districts. Finally for the third-parties such as real-estate agencies who has the data and ability to deploy the model, the value brought by this model can be encapsulated into three parts. 

Firstly, correctly predicting the market value for the property as recommended listing price can greatly accelerate selling process and decrease the listing time. Substantially it can reduce labor cost per property sale and the total trading volume will be surged. In return, the profit can be expected to boost due to the increase in revenue and decrease in cost.  Also, the model can provide insight in profitabe segment of market that the company should forcus for better resource allocation. Furthermore, This model can be a persuasive advertisement for clients that makes the pricing policy transparent and improves the efficiency of the pricing mechanism as a whole. 


### Data Understanding
To train a predictive model, I first need to scrape data about the second-hand housing with detailed and comprehensive description. As state earlier, WUBA is the ideal data source for its completeness and strong real-time. To ensure data integrity and reliability, I chose to crawl data ourselves from the website, which contains 17 datasets, rather than use ready-made third-party datasets. Through this means, I ensured that the data used for data mining is completely public, true and real-time.

The following is the summary of extracted features:

Total price: target variable.

Green space ratio: indicating the luxury degree of the community. High green space is a expression of luxury apartment, and hence the higher the total price.

Usable area: having the strongest correlation to total price. Given same price per square meter, Greater usable area comes with higher total price.

Duration of property right: unlike America, China"s property has limited duration, mostly of which are 70 years. In our sample, there are 3 categories, 70 years, 50 years and 40 years.

Year of construction: indicating housing quality.

Month-on-month growth rate: signal of popularity of the property and related to price trend of the property.

Price per square meter: the higher the price per square meter, the higher the total price as it is a function of price per square meter

Average price for the community: indicator of housing quality and living conditions.

Housing Unit: textual description of house type, representative of usable area.

Orientation: a effective factor in predicting housing prices, specifically in China. Explanation is below.

House remodeling: affecting total price as a initial investment of property owner.

District: there are 17 districts in total, with different level of development and living conditions, and thus have different popularity and price level.

Floor Number: textual description of total floor and floor position of the property.

Property management fee: mandatory for every resident and is charged for all public service and communal facilities. Better community usually has higher property management fee, which is a representative of property quality.

Floor area ratio: the ratio of total building area above ground and site area. Smaller floor area ratio represents lower residential density, and is more preferred. Thus, floor area ratio is also a significant element in house purchasing.

Due to cultural influence, orientation has decisive position in judging a house. Since ancient times, Chinese believe that a good orientation can help with one"s fortune, but a bad orientation can bring on unexpected disaster. Although nowadays people are not as feudal as before, houses facing south are much preferred for its scientific basis such as sunshine duration as well as traditional cultural influences. Considering that historical issue, I decide to retain "Orientation" in predicting the listing prices of second-hand houses.

### Data Limitation & Selection Bias
From the perspective of data presentation, the textual description take up most features and numeric features are relatively less. Unavoidably, we may lose some details when converting the text into categorical data. Besides, in order to solve the business problem, predicting the price of new housing unit that reflects the whole market, we have a prior assumption of the dataset: the prices of housing units in the data source are results of invisible hands of market. Since if a large number of points are over-priced or lower-priced, the model cannot really reflect the market. As for selection bias, even though WUBA is the best accessible data source, it cannot include every instance of house reselling. For instance, property owners of extremely luxury buildings seldom post their advertisements on public service platform due to personal information issue. To some extent, scraping data from a specific website must come with data selection bias for it screens out the portion composed by website users.

### Evaluation metrics
Average model test set R2 Score:0.9657954232042204

Average model test set RMSE Score:0.1250091886145994

### Deployment

#### Model Deploy 
After laboratory test, we have confidence that the model can predict the price for the properties true to its market value at the level of 96.57%. Before the real-estate agency to fully deploy the model onto the system both online and offline for pricing policy, we suggest the model to be tested on the offline system (corporate inner system) first. 
Monitor and Evaluate The agents are suggested to use the predicted price as reference and keep records of the actual deal price and the time between listing and sell of the property as criteria to evaluate the model. The difference between the predicted price and time cost for selling the property will be studied as feedback to further improve and update the model. The goal is to predict price as close to the deal price as possible to shorten selling time thus lower the sales cost and increase the revenue for real-estate agencies.

#### Further Advancement
The model can be advanced by incorporating the time cost feature to predict a probability of selling the house at certain price within certain time limit (eg. c1 = within one week, c2 = within one month, etc) for specific property. The agency can thus calculate the profitability of representing the property by multiplying related cost. If the expected listing price for the owner is higher than the suggested profitable price range, the agency should drop certain property.

#### Possible Concern 
Since some feature of the model such as the "month-to-month growth rate"  and "green space ratio" that are not easy accessible for agents, the model should be able to take community name as input keys to search for related data in the system histories when deploying the model in an actual production system. The agency should also be aware that the performance of the model may be unsatisfactory if there is prominent change to the market such as new restriction or tax policies. It might be necessary to introduce new features to the model.

#### Ethical Discussion 
The primary purpose for the model is to simplify the pricing mechanism of the second-hand housing market in Shanghai for the benefit of all parties involved. We aim to construct a model that can predict the true value of the property, yet the way of model training and updating might cost the predicted price to reflect too much from the market environment. This could cause the use of model to worsen the price pushing caused by speculators under frenzied situation. More domain knowledge should be applied here to discuss on how the model can differentiate between these situations.

