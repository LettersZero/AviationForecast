# AviationForecast
 Developing a Vendor-Product Procurement Forecasting System Using NIIN Data 

Project Definition

The Developing a Vendor-Product Procurement Forecasting System Using NIIN Data project addresses inefficiencies in procurement forecasting for the aviation, construction, maritime, and land industries. This system aims to optimize purchasing and inventory planning by predicting future procurement needs using historical data. Key data elements include vendor codes (CAGE), product identifiers (NIIN numbers, government-provided part numbers), unit prices, quantities, and procurement dates.
Synthetic data from Haystack Gold, a defense parts and logistics management software, was used for this project. Key variables include:
NIIN (National Item Identification Number): Identifies supply items.
CAGE (Commercial and Government Entity): Identifies suppliers or government agencies.
Government procurement: The process of purchasing goods and services for government use.
Government solicitation: A request for companies to bid on government procurement.
This project required an understanding of compliance and regulatory standards, such as CAGE and NIIN codes, and the use of data management systems to handle fragmented data. In CS 210: Data Management in Data Science, we learned the importance of cleaning datasets and using queries to connect fragmented data, a critical aspect of this project given the fragmented nature of Haystack Gold’s data. SQLite was employed for effective data management.
Compliance plays a crucial role in industries like aviation, ensuring traceability and adherence to industry regulations. Structured procurement processes help reduce legal risks, maintain product quality, and enhance safety, particularly in highly regulated sectors.


Novelty and Importance


	Accurate forecasting in reducing costs, avoiding over-purchasing or under-stocking, and improving budget planning is imperative for firms in defensive manufacturing. With personal knowledge, some smaller manufacturing firms have outdated or no forecasting models with proper data management tools with CAGE codes, NIIN, procurement, or government solicitations. As mentioned, utilizing the main defense parts and logistic management software comes with challenges that manufacturing firms face, like fragmented and inconsistent data across various sheets. 
I chose this project because of its relevance to a friend working in a small manufacturing firm, making it a practical application of skills learned in CS 210 and Econ 421. Additionally, analyzing government procurement aligns with my interest in understanding government spending.
Progress and Contribution

Data for this project is from Haystack Gold, using the variables NIIN, CAGE, Item_Name, Unit_Price, Data, Price, Quantity, Total_Price, Supply_Chain, Latest_MLC_Price, Open_Date, and Solicitation_Number. The variables are in various Excel sheets, MCRLMasterCrossReference, MLCManagementdata, ProcurementHistory, ProcurementHistoryArchive, SRVADLAForecast, and GovernmentSolicitations. Starting with the code, I set a seed to ensure my results are replicable. I then used SQLite3 to start a SQL server for the dataset. After, I checked if any of the sheets contained missing data in the columns, then removed them because of the regulatory and compliance aspect of the dataset. 
I performed exploratory data analysis by graphing relationships between various variables in the dataset. I graphed monthly procurement trends with total quantity and months utilizing the forecasting sheet. To understand the differences in procurements, I then added another variable, supply chain, to see differences. To fix the data fragmentation problem that smaller manufacturing firms may face, I used SQL to connect CAGE, item name, NIIN, and solicitation count. 

I used a heatmap with the connected set to see which NIINs have the highest solicitation count. Using the CAGE codes, I used an online CAGE in the company database to see which companies have the highest number of solicitations from the NIIN. Another EDA I did was a seasonality analysis with monthly demand trends and quantity. After, I did an outlier detection in quantity and annual product diversity analysis to see what products are most bought and to measure innovation in the sector. 


I used various forecasting models to measure the quantity based on procurement history and date. I started with a SARMINA(1,1,1)(1,1,0,12) and got a root mean square error of 5532.47. The high RMSE made me change to a different model, a random forest, and I got an RMSE of 1196.2. With the random forest, I used feature engineering of a one and 2-month lag and a 3-month rolling mean. The RMSE of 1196.2 made me want to try another model, XGBoost, which has the same feature engineering. The XGBoost model utilizes 100 estimators, a learning rate of .1, and a max depth of 3; under those conditions, I got an RMSE of 1093.7. I then tried another method of combining the two models with a meta-model of linear regression. After evaluating the stacked model, I got an RMSE of 857.88, the best of the other three models. 

For the primary model of the project, I tried an ARIMA model again but using a different method. The data used are the quantity variable, NIIN, and date variables. I chose data where the same NIINs appear twelve or more times and then ran an Augmented Dickey-Fuller (ADF) test to determine whether the series is stationary. After discovering that it is non-stationary, I used differencing by incorporating 7 lags to see how to define my ARIMA from the Autocorrelation Function (ACF) and Partial Autocorrelation Function (PACF). I made my ARIMA(1,1,4) model from that information and forecasted it using in-sample predictions. The primary model gave an RMSE of 23.02 and a mean absolute percentage error (MAPE) of .416. Even with an average RMSE, the p-values for the coefficients are not significant, which means even if the RMSE is average, the model is not a good fit for the data.

Each model used in this project has advantages and disadvantages when predicting values. For example, ARIMA excels in seasonal data, and Random Forest performs well with handling features. XGBoost is excellent for speed and performance on large datasets.  

Changes After Proposal

	Compared to the proposal submitted earlier, I have made considerable changes to the overall project. For instance, I used multiple prediction models instead of only incorporating one ARIMA model. This is to challenge myself and see if other models can perform better for the project. I only used RMSE as the sole fit measure but incorporated MAPE into the primary model. 

Conclusion

The stacked model and the primary ARIMA model performed the best, but it is essential to note the ARIMA model is not statistically significant. The stacked model has an RMSE of 857.88, which is exceptionally high for a square-rooted value. In the future, I would enhance my model with external features such as macroeconomic indicators. Expanding the scope to other industries will help me better understand cross-sector procurement behaviors. Next time, I would change my models to specify a particular supply chain to see if that increases accuracy or significance. 
Overall, I managed to deal with the fragmented data, an issue some firms experience. Utilizing a database made it easy to grab information from the various sheets and make models or EDA from it! This project highlights the critical need for accurate procurement forecasting to address aviation, maritime, and construction inefficiencies. By leveraging data analysis and machine learning techniques, the models developed in this study provide actionable insights to improve procurement planning and compliance with industry regulations.

