**Author**:[Russell Pihlstrom](mailto:rgpihlstrom@yahoo.com)
## Using Product Reviews & Topic Modeling To Drive Innovation!
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/Intro.png" height="300"/>

## Results 60% Coherence, 6 Topics!

This project uses LDA Topic Modeling, an unsupervised algorithm, to discover the latent topics mentioned by consumers in approximately 3000 product reviews of the most popular ananalog plant-based meat products.  By scraping data from the most popular retail and social media sites I create two sets of topic models: 1 set of 4 topics for positively rated reviews and another set of 2 topics for negatively rated reviewes.  The algorithm was able to acheive coherence scores of <b><ins>50%</ins></b> and <b><ins>60%</ins></b> respectively.  The following were the most dominate topics for each segment of data:
<p>
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/SnapshotTopics1.png"  height="300"/>

Additionally, I experimented with using Naive Bayes, a supervised algorithm, to try attribute a numberical rating to reviews that otherwise did not have an accompaning numberical/ stars rating.  By leveraging and learning from past pre-rated, positivly (4-5 Stars) or negativly (1-3 stars) reviews, I attempted to classify twitter reviews, which are not rated, into a positve or negative category repectively.  Unfortunately, this experiment was not successful, having sever overfitting (Training/ validation <b><ins>93%</ins></b>, Testing <b><ins>76%</ins></b>)  See below for more details as there are areas for improvement.  

 
 ## Business Problem
Grocery sales for plant-based meats are up 47% vs. year ago, and research suggests the acceptance of plant-based burgers by mainstream consumer is starting to become reality. A large portion of this growth is coming from the two most dominate brands/products: Impossible and Beyond.
 <p>
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/PlantBasedSales.png"  height="300"/>

 
<br>

#### The Current Situation: 
The CEO of Sunrise Health Foods is looking to enter the growing category with a new product.  However, given the high rate of failure for new product launches, coupled with the high costs for entry he/she is looking to create a product that is uniquely better than industry competitors.  In order to create a new and uniuque product, unique insights are needed.  He has hired me to review the vast number of product reviews captured for industry leaders from the most popular sites and formulate my findings into a set of product attributes that can then be leverage by the R&D team as it begins its product development efforts.
  
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/SunriseCEO.png" height="200"/>


  
  
### Business Questions Driving Model Development.
 The intended output of this theoretical business case is focused on the following:
-   **1. Identify The Key Sentiments & Topics Menentioned From Product Review Sites.**
-   **2. Examples Good & Bad Product Attributes the R&D Team Should Consider During their Development Efforts.**
-   **3. Attempt to Project Ratings from Rated Reviews on to Unrated reviews.**
<br>
 
## Data

The data used for this project was scraped from the below sites in the listed quantities:  The dataset contains approximately 3k rows and required the use of selenium and Scrapy to procure along with twint for the reviews obtained from twitter reviews.
  
  
  
<br><br>
<img src="https://github.com/rgpihlstrom/Project3/blob/main/images/Columns.png" />

## Model Development Methods
This project uses the Crisp DM methodology to generate and optimize the published model.  Crisp DM requires blending business strategy, availabled data, and modeling techniques best suited to the business drivers.  Model development is and was very iterative.  I began by doing secondary research around the basic business drivers of the Telecom industry, gaining a better understanding on the prevalence of churn and the costs associated with fleeing customers.  Along with the project requirements noted above, the following additional factors were considered during the modeling process:
-   **1. Data Imbalance**  Early in the development process it was obvious that I was dealing with an imbalanced set of data (more information/ rows of data on non-churn customer vs. churn customer).  To ensure optimum identification my processes/ modeling would need to account for this imbalance.  I addresd this gap by first attempting the model using different weights and ultimately decided to do SMOTE(Synthetic Minority Oversampling Technique) to overcome this challenge.

- **2. Selection of Supervised Learning Classifiers**  Initially I tried several different types of classifiers, ranging from Logistic Regression, Naive Bayes, Gradient Boost, Ada, and XGBoost.  Ultimately, I decided to use <b><ins>Knn, Decision Trees and Random Forest</ins></b> , as these classifiers are non-parametric and are highly interpretable.  Interpretability, the disproportionate number of categorical features, along with being able to avoid addressing multicollinearity were the most influential factors in selecting which classifiers to implement for this project.

-   **3. Business Drivers: Churn Detection > False Alarms**  Recommendations on model development were based on secondary research along with working knowledge on the disparity between the cost to acquire vs the cost to retain customers.  In this hypothetical scenario, the CEO of Telco has asked me to place a particular focus on detection at the potential expense of unnecessary outreach activities.

<img src="https://github.com/rgpihlstrom/Project3/blob/main/images/ChurnOverFalseAlarms.png" width="600" height="300" />


## Model Results (85% Detection)
After several iterations, the below recall <b><ins>(85%)</ins></b>, accuracy <b><ins>85%</ins></b>, precision <b><ins>47%</ins></b>, and AUC<b><ins>82%</ins></b> scores were achieved for the selected classifier..  These results were acheived using the <b><ins>Random Forest Classifier</ins></b>.  It's important to remember these results were acheived with a focus on recall(detection) over precision (false alarms).
<br/>
<img src="https://github.com/rgpihlstrom/Project3/blob/main/images/ModelResults.png" width="600" height="400" />
<br/>
<h4>Results Explained (using below illustration):</h4>
<strong> - 85% Detection</strong> = Model Predicted Churn , Customer Actually Churned <br/>
<strong> - 34% False Alarms</strong> = Model Predicted Churn , Customer Actually remained Loyal<br/>
<strong> - 15% Undetected Churn</strong> = Model Predicted Loyal , Customer Actually Churned<br/>
<strong> - Red Dashed Line</strong> = This is our <b><ins>THRESHHOLD</ins></b> level (default probability rate) the model uses this % probability to label a customer as churn vs. not churn.<br/><br/>
<strong>***Key Take Away</strong> = Our model is very good at detecting churn.  As we decrease or increase our <b><ins>THRESHHOLD</ins></b> we can capture more or less churners.  This in turn results in a higher or lower False Alarm rate.  Per my suggestion in next steps below, we need to develop a cost for False Alarms.  This will allow us to create a profit tradeoff equation, enabling us to set the "right" threshold for the business.

<br>
<img src="https://github.com/rgpihlstrom/Project3/blob/main/images/VisualOfChurnDection.png" width="600" height="375"/>

<br><br>
## Business Results/ Recommendations (Using 50% Threshold)
As stated above the goal of the project was three fold.  I have outlined and summarized the results of each area of interest below:

<h3>1. Top Features Associated with Non Churn vs. Churn:</h3>
<img src="https://github.com/rgpihlstrom/Project3/blob/main/images/MostImportantFeatures2.png" />

### Observations:
- Type of Contract – 89% of churning customers are in Month-to-Month contracts.
- Method of Payment/ Billing – 55% of churning customers pay with electronic check.
- Months with Telco – 75% of churn is occurring within 29 months of becoming a Telco customer. 
- Type of Internet Service – 66% of churners are participating in the Fiber Optics Internet Service.

Together these factors were identified by the model as the 4 most predictive of churn.  To view a list of all the features used to develop this model see appendix in the pdf stored in this directory.  


<h2>2. Current Features/ Services Ability to Prevent Churn:</h2>
<img src="https://github.com/rgpihlstrom/Project3/blob/main/images/CountofEnrolledServices1.png"/>

### Observations:
- Building on above, the feature "Service Count" was not identified as a top predictor of churn.  Graphs show equal usage/ participation in services between loyal vs. churn customers.  However, ***66% of churners are enrolled in 3 or more services.***
Given that both groups are using services equally and the percent churn is not lower with increased service usage, I would deem that the services are not adequately helping to prevent customer churn.


<h2>3. Opportunities for Innovation:</h2>
<img src="https://github.com/rgpihlstrom/Project3/blob/main/images/Innovation3.png" />

### Observations:
My recommendations for innovation are focused on working to create additional solutions around the 4 most predictive features associated with churn which were noted above in point #1.
- Type of Contract – The goal is to reduce spontaneous churn.  If churn customers are not interested in a 1 year or a 2 year contract, perhaps there is a shorter term contract that can be created to induce trial.  Perhaps try 6 months or quarterly contracts.
- Method of Bill Pay  -  Examine quality and/ or customer experience required to pay bill electronically.  Look to make this process as easy as possible.
- Increasing Months with Telco - Examine ideas for Innovation around loyalty programs to incent longevity
- Type of Internet Service -  Given the big difference in rate of churn across DSL vs. Fiber Optics churners, I believe there is something obviously wrong.  My recommendation is to engage in a competitive and or quality analysis to ensure the quality of the fiber optics lines are meeting customer expectations.



## Potential Impact on Revenue (Assuming 100% Detected Churn Reversal)
<img src="https://github.com/rgpihlstrom/Project3/blob/main/images/RevenueRamifications2.png" width="600" height="400"/>

### Observations:
- Today Telco experiences 27% customer churn rate which = 31% lost revenue.
- Given the <b>85% churn detection rate</b> generated by the model, Telco has an opportunity to reduce its churn to as little as 15% (for illustration purposes assuming 100% churn reversal).  The result of detecting and reversing the 27% historical rate of churn would result in a savings of 14% revenue.

## Next Steps

- **Develop Hard Numbers for the Cost of False Alarms** - In this hypothetical scenario we were not given the cost of falsely reaching out to a loyal customer with a particular outreach/ marketing program.  Once definitive numbers can be defined, we can reexamine our Threshold levels.
- **Develop Threshold Evaluation Formular** - Once aligned on costs and savings associated with churning customers,  a formula can be created to optimize economics between Detection vs. False Alarm.
- **Examine Detection vs. False Alarm Tradeoffs** - Given the high cost of customer acquisition vs. customer retention some additional analysis may reveal lowering our threshold from 50% to perhaps 40%, which would capture additional undetected churners.
- **Examine Additional Classifiers** - For this project I settled on Random Forest, however, given advances in classifiers such as extreme boost and others, there may be additional opportunities to improve our churn detection rates.
- **Put Model(s) Into Productions** - Once we have optimized our models and/or generated enough models to account for the wide variety of churn data, I would look to automate and deploy the models via a web-based interface and make it available to the marketing and or customer service teams.

## For More Information

See the full analysis in the [Jupyter Notebooks](folder) or review our <a href="https://github.com/rgpihlstrom/Project3/blob/main/Presentation.pdf">Presentation</a>.

For additional info, contact me here: [ Russell Pihlstrom](mailto:rgpihlstrom@yahoo.com)

 
 
 
 
 
 
 
 
 
 
 
 
## Project Context
Below is a timeline of actual events that influenced the dynamics of the business problem outline below.   
<img src="https://github.com/rgpihlstrom/Project4/blob/main/images/Background1.png"/>

Its March 5, 2011.  It is also one week before the kickoff of the big SXSW conference.  The SXSW conference is a major deal in the tech, film, and entertainment industries bringing together the best and the brightest from all respective fields.  This year is significant as Apple has decided to surprise the tech world by using the event to launch its new iteration of its iPad platform, the iPad2.  Apple is coming off a stream of successful launches and just launched its iPad1 approximately one year ago.  The Apple team is looking to outdo its previous launches and the Apple Brand Manager is looking to make a splash with the launch of the iPad2.  In addition to surprising the tech world by launching the iPad2, at the same time as the SXSW event, Apple decided to create a temporary "Pop-up" store to sell the new iPad2's close to the event.  The idea and impromptu creation of the temporary store was seen as risky but exciting, and if successful, could be used again for future launches.

## Business Problem
Given the above context the Brand Manager at Apple is interested in the following:
-   **1. General Sentiment Surrounding the Apple Brand from Event Attendees**
-   **2. The Reception of the iPad2, its Launching at SXSW and Use of A Pop-up Store**
-   **3. Capture Consumer Feedback as Potential Innovation Regarding Apples Product Portfolio**
<br>

 
## Data

The data was comes from CrowdFlower via <a href="https://data.world/crowdflower/brands-and-product-emotions">data.world</a>. Human raters rated the sentiment in over 9,000 Tweets as positive, negative, or neither.  I focused this project on the positive and negative tweets associated with Apple/ Apple products.  The resulting dataset is the aforementioned 3300 classified tweets.  Furthermore, the data was captured via tweeter and was predominately captured from SXSW attendees from the year 2011. 

## Model Development Methods
This project uses the Crisp DM methodology to generate and optimize the published model.  Crisp DM requires blending business strategy, available data, and modeling techniques best suited to the business drivers.  Model development is and was very iterative.  I began by doing secondary research around the SXSW event along with getting a basic understanding of twitter data.  Along with the project requirements noted above, the following additional factors were considered during the modeling process:
-   **1. Data Imbalance**  The number of positive tweets is far greater than the negative tweets.  This creates a scenario that makes predicting negative tweets more difficult for the model as there is not as many example words to train our model on what is negative vs. positive.  To overcome this challenge the SMOTE technique was used.  

- **2. Selection of Supervised Learning Classifiers**  Initially I tried several different types of classifiers, and even developed a RNN classifier using Bi-directional LSTM.  Given longer training times and less than desired accuracy scores I opted to reduce the complexity of the data and changed my classifier to Naive Bayes.  Naive Bayes has shown historical strength in text classification and its fast-training time makes it ideal for smaller dataset.

-  **3. Business Drivers: Accuracy as Primary Scoring Metric**  Given the opportunity to learn as much from negative tweets vs. positive tweets I used a balanced accuracy score as my success criteria over precision and or recall.


## Model Results (86% Detection)
After several iterations, and a thorough cleansing of the data the trained model obtained a training score of 87% and a testing score of <b><ins>(86%)</ins></b>.  This tight span is required to ensure the model was not overfitting and enable the opportunity to reuse the model on future twitter data captured from SXSW attendees.

<img src="https://github.com/rgpihlstrom/Project4/blob/main/images/Testscores1.png"/>
<br>

## Business Results/ Recommendations
<br>
As stated above the goal of the project was three-fold.  I have outlined and summarized the results of each area of interest below:

<h3>1. Overall Brand Sentiment Scores</h3>
<img src="https://github.com/rgpihlstrom/Project4/blob/main/images/BrandSummary.png" />

### Observations:
- <b><ins>Generating Buzz</ins></b> – See Tbl1. As evidenced in table 1, which shows the frequency of brand mentions, the Apple brand was the leading brand name being included within a tweet.  It is being mentioned more than <b><ins>3X</ins></b> the second most mentioned brand google.   Table 2 shows counts of hashtags included in tweets vs. other brands/ topics.  Notice the Apple brand and or an Apple products are being mentioned at a higher count than other trending brands/topics.

- <b><ins>Sentiment Splits</ins></b> – From table 3 you can see how these tweets are classified.  As shown, <b><ins>83%</ins></b> of the tweets containing/ pertaining to an Apple product are positive while only <b><ins>17%</ins></b> are negative.

- <b><ins>Key Tweets</ins></b> – As shown, the positive tweets regarding the brand are general in nature.  However, many of the negative tweets appear to be incited by panelist presenting at the conference vs. genuinely organic negative sentiments toward the brand.
<br>
Overall, the brand seems to be being reflected in a positive tone.

<h2>2. Reception of iPad2, Feedback on Launching and Selling at SXSW:</h2>
<img src="https://github.com/rgpihlstrom/Project4/blob/main/images/IpadLaunch.png" />

### Observations:
Building on above, the reception of the iPad2 along with launching and selling products at the conference were received in a mostly positive manner.  <b><ins>90%</ins></b> of the tweets containing “iPad2” or “Store” within the tweet were deemed positive while only <b><ins>10%</ins></b> were deemed negative.
<br>

- <b><ins>Positive Word Cloud</ins></b> - Words like “launch”, “new”,” smart” were used in reference to the acceptance of selling the first iPad2’s at the conference at the pop-up store

<br>

- <b><ins>Negative Word Cloud</ins></b> - Words like “line”, “camera”,” out” were used in reference to the long lines at the pop-up store, along with some early feedback that the camera on the iPad2 may not be meeting customers expecations on quality.  Also the word “out” was used in reference to the temporary store running out of inventory.


<h2>3. Consumer Feedback on Apple Products/ Opportunities for Innovation:</h2>
To begin my exploration of gathering consumer feedback, I first needed to review the product landscape and how the portfolio of products may or may not be receiving feedback.  I did so by plotting each product and associated sentiments.  

<img src="https://github.com/rgpihlstrom/Project4/blob/main/images/IphoneBatteryOverview.png" />

As you can see nothing stands out as too peculiar except the iPhone.  The iPhone is receiving negative sentiments at half the rate of positive tweets.  Compared to other Apple products this rate seems high.  Upon further analysis,  in table 2, you can see that its relative percentage of negative tweets received to its total tweets received is more than twice that of the other Apple products.
<br>

Based on these findings I decided to do a deep dive on what is driving the higher-than-expected negative sentiments.  
<br>
Shown below is a summary of results derived from a deep dive on the iPhone tweets.

<img src="https://github.com/rgpihlstrom/Project4/blob/main/images/IphoneBattery.png" />

### Observations:
- <b><ins>Word Cloud</ins></b> – Outside of the word “iPhone”, the next biggest word is “battery”.
- <b><ins>Key Tweets</ins></b> – Shown are just a few of the tweets mentioning the life of the iPhone battery as a major disappoint for consumers.
Based on these findings, we will make recommendations to the R&D teams for future develop!

## Summary 

- <b><ins>Brand In Good Health! </ins></b> - Given the above scores the brand health seems to be good with SXSW attendees that use twitter.
 
- <b><ins>iPad2 Launch @ SXSW and selling at Conference is a SUCCESS! </ins></b> - Consumers received the launching of the Ipad2 with open arms and excitement and the addition of the Pop-up store was well recieved.

- <b><ins>Product Reviews Mostly Good! </ins></b> - Product reviews were mostly good with a few areas we can take back to R&D for review, especially in regard to the iPhone battery.

## Next Steps
- <b><ins>Broaden our Data Beyond Conference Goers and Twitter Users</ins></b> - This project was solely focused on the Twitter data captured from SXSW conference attendees.  There is an opportunity to scrape other sites containing product data and use that data to drive business value.

- <b><ins>Examine Additional Classifiers/ Create Opportunity for Stacking Classifiers</ins></b> - In this project I focused on Naive Bayer classifiers, but there are additional classifiers that work well on text data such as Random Forest.  Creating additional models and combining the models to make predictions can improve accuracy.

- <b><ins>Finer Classification Models</ins></b> - Look to create classifiers that can accurately classify Negative, Neutral, Positive tweets vs just Positive and Negative in this project.  Potentially perform Topic Modeling.




## For More Information

See the full analysis in the [Jupyter Notebooks](folder) or review our <a href="https://github.com/rgpihlstrom/Project4/blob/main/Phase4Presentation.pdf">Presentation</a>.

For additional info, contact me here: [ Russell Pihlstrom](mailto:rgpihlstrom@yahoo.com)
