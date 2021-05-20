**Author**:[Russell Pihlstrom](mailto:rgpihlstrom@yahoo.com)
## Using Product Reviews & Topic Modeling To Drive Innovation!
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/Intro.png" height="300"/>

## Results 60% Coherence, 6 Topics!

This project uses LDA Topic Modeling, an unsupervised algorithm, to discover the latent topics mentioned by consumers in approximately 3000 product reviews of the most popular ananalog plant-based meat products.  By scraping data from the most popular retail and social media sites I create two sets of topic models: 1 set of 4 topics for positively rated reviews and another set of 2 topics for negatively rated reviewes.  The algorithm was able to acheive coherence scores of <b><ins>50%</ins></b> and <b><ins>60%</ins></b> respectively.  The following were the most dominate topics for each segment of data:
<p>
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/SnapshotTopics2.png"  height="300"/>
 
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

The data used for this project was scraped from the below sites in the listed quantities:  The dataset contains approximately 3k reviews and required the use of selenium and Scrapy to procure along with twint for the reviews obtained from twitter.
  
<br>
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/OverviewOfTheData.png" height="300"/>

## Model Development Methods
This project uses the Crisp DM methodology to generate and optimize the models.  Crisp DM requires blending business strategy, availabled data, and modeling techniques best suited to the business drivers.  Model development is and was very iterative.  I began by doing secondary research around the basic business drivers of the industry, and gaining a better understanding on the top selling products and brands (thanks to my friends a IRI :) ).  Along with the project requirements noted above, the following additional factors were considered during the modeling process:
-   **1. Data Imbalance**  Early in the development process it was obvious that I was dealing with an imbalanced set of data (more information/ rows of data on positive reviews vs. negative reviews).  During topic modeling, to ensure optimum identification of topics and product attributes, I split the data into two sets: positive and negative.  Furthre more during the text classification portion of the project I needed to account for this imbalance.  I addresd this gap by using SMOTE(Synthetic Minority Oversampling Technique) during my Bayes classification portion.

- **2. Selection of Unsupervised Topic Models**  Initially I tried several different types of topic models, ranging from Mallets LDA,  HDP, LSA, and Multicore LDA.  Ultimately, I decided to use <b><ins>Gensims Multicore LDA</ins></b> , as this topic model continued to produce more coherent topics with higher coherence scores during my iterative approach to modeling.  During the text classifiers portion of the project I choose Naive Bayes as it outperformed other ML classifiers.

- **3. Techincal Challenges - LDA & Reviews with Few Words:**  Finding the number of topics, finding The "right" words for each Topic and finding topics that represented a portion of each doc/ review with a very iterative process.  LDA Topic modeling is a technique that is considered a "soft" classifier and interpeting its results are part-art-part-science.  Experts suggest the higher the coherence the better, but the max coherence score acheived does not alway acheive the most interpretable/ translatable topics.  Instead, when using topic modeling to find hidden topics the user is to use a blend of domain knowledge, coherenc score, and coherence overlap, and topic interpretability. During this project I acheive coherence scores that ranged from .2 - .72.  Ultimately I chose hyperameteres that created models that reached coeherence scores greater than .45 and then selected the number of topics per dataset based on iterpretabilty and my domain knowledge on the subject, as I have over 15 years of experience in the food innovation space.  I also cross referenced my number selected topics per dataset against a Kmeans elbow graph to ensure alignment.  Lastly, I used LDA vis to ensure separation of topics.  Below are the results from both the positive and negative datasets

<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/EvaluatingTopicModels.png" height="300" />


## Model Results - Topic Modeling
After several iterations, the below topic models were created <b><ins>50% Coherence - Positive Reviews</ins></b>, accuracy <b><ins>60% Coherence - Negative Reviews</ins></b>, These results were acheived using the <b><ins>LDA Multicore in Gensim</ins></b>.  It's important to remember these results were acheived with a focus on interpretability.

 <br/>
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/TopicModelingPositive.png" height="400" />
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/TopicModelingNegative.png" width="775" />


<h4>Topic Model Results Explained:</h4>
<h5>Topics Derived From Positivly Rated Reviews</h5>
<strong> - Topic 0</strong> = <b><ins>NEW FAMILY FAVORITE</ins></b> Per the pyvis graph above this was by far the most dominate topic in the positive set of reviews.  In Studing the reveiws most associated with the topic and key words this topic can be called  as the reviews here were raving about the simliarity to real meat, great taste, great substiture for beef<br/>
<strong> - Topic 1</strong> = <b><ins>WORTH THE SACRIFICE</ins></b> as the reviews most associated with this topic and the dominate words correlated quality texttures, reception of price, filling, and being impressed, despite a few concerns on long/ odd ingredient lists aka (chemicals)<br/>
<strong> - Topic 2</strong> = <b><ins>RIGHT PROPOSITION</ins></b> as the reviews most associated with this topic and the dominate words correlated with size of the product and number of items contained in the package along with all the benefits associated with animal and eco friendly. <br/>
<strong> - Topic 3</strong> = <b><ins>GUILT  FREE CONVENIENCE </ins></b> as the reviews most associated with this topic and the dominate words correlated with easy of use, versatility and the health benefits associated with avoid the hormons associated with non-organic beef farms


<h3>Topics Derived From Negatively Rated Reviews</h3>
<strong> - Topic 0</strong> = <b><ins>BUYER BEWARE</ins></b> Per the pyvis graph above this was by far the most dominate topic in the negetive set of reviews.  The reviews here were blasting the horrible smells, resembalance to wet petfood and its very large gap between the textures offered vs. real beef.
<br/>
<strong> - Topic 1</strong> = <b><ins>NOT WORTH THE SACRIFICE</ins></b> as the reviews most associated with this topic and the dominate words correlated with long list of ingredients, ingredients that cannot be pronounced (aka chemicals) and the high cost relative to beef.
<br/>

<br/><br/>
<strong>***Key Take Away/ Product Attributes to Target</strong> = Well received all around, meeting many needs for consumers desire for: <b><ins>Taste, Texture, Convenience, Price, Eco</ins></b>… willing to “put up” with <b><ins>Smell and Ingredient list</ins></b>… at least for now... however as a R&D staff they should target:  <b><ins>SMELL, APPEARANC, PRICING, INGREDIENTS </ins></b> as opportunities to offer something new and unique to the market.

<br>
## Example Reviews From Scrapped Sources Associated with Key words
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/ExampleReviews.png" />

<h4>Reviewing Extending Model From Rated Reviews to Non-Rated REviews:</h4>
<h5>TBD</h5>

### Summary of Product Areas for R&D Teams To Consider:
- Positive Topics/ Attributes: 
- Negative Topics/Attributes: 


## Next Steps - MORE DATA

- **MORE DATA - Retailers Should Motivate More On-line Consumer Reviews** - Quantity & Diverity of Thought:  One of the challenges of this project was amassing enough data to obtain the quantity of data required to create robust models.  In order to encourge this type of analysis in the future and accross several categories more reivews would be helpful, also pushing consumer to generate organic thoughts for targeted product attributes, dislikes, etc.

- **MORE DATA - Developing More Extendables Models** - More Sources of Data:  Per the above obtaining data is a challenge.  Additionally, obtaining data that is also rated is even more of a challenge.  In order to combat this problem I could develop an algorithm that would take the ratings from reviews that allow the user to enter a ratings (amazon) and using that data to project a rating on to reviews that do not allow the user to enter a rating (twitter,tic-tok, FB).  By creating a more extendable more will allow for the use of more sources of data, and ultimately increases the quantity. 

- **MORE DATA - Leveraging Video Content To Create Reviews** - While scraping sites for this project, such as twitter, I encountered several tweets that contained the words "Beyond Burger Review" or "Impossible Burger Review" that were not really reveiws but instead were really just links to youtube/ other videos.  If there was a technolgogy to summarize videos down to a review would be invaluable.

See the full analysis in the [Jupyter Notebooks](folder) or review our <a href="https://github.com/rgpihlstrom/Project5/blob/main/Presentation.pdf">Presentation</a>.

For additional info, contact me here: [ Russell Pihlstrom](mailto:rgpihlstrom@yahoo.com)
