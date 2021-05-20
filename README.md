**Author**:[Russell Pihlstrom](mailto:rgpihlstrom@yahoo.com)
## Using Product Reviews & Topic Modeling To Drive Innovation!
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/Intro.png" height="300"/>

## Results 60% Coherence, 6 Topics!
Business Summary: This project is intended to be used by a fiction marketing and product development team to ascertain the key product attributes associated with analog plant-based meat products.  The information outlined below would then be used to formulate a positioning strategy and set of product formulas that would meet the positive attributes highlighted in the reviews along with address the negative attributes mentioned in the reviews.  
Technical Summary: The project uses an LDA Topic Modeling algorithm to discover the latent topics within the set of approximately 3000 products reviews scraped from the sites of the most popular retailers along with twitter.  After scraping and cleaning the data I created two sets of data, one set contained positive reviews the other set contained negative reviews.  Finally, I created topics for each respective dataset: Positive topics and Negative Topics.  A summary of these topics is immediately below, and a more detailed outline is further below.  The algorithm used was able to achieve coherence scores of <b><ins>50%</ins></b> and <b><ins>60%</ins></b>, positive and negative, respectively.  Summary of Topics:
<p>
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/SnapshotTopics2.png"  height="300"/>

 ## Business Problem
Grocery sales for plant-based meats are up 47% vs. year ago.  Research suggests the acceptance of plant-based burgers by mainstream consumers.  A large portion of the growth in the plant-based category is coming from the sales of analog products (those that mimic real meat).  The two most dominate brands/products in the space are: Impossible and Beyond.
 <p>
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/PlantBasedSales.png"  height="300"/>

 
<br>

  
<table cellspacing="0" cellpadding="0">
  <tr>
   <td width="70%" border="0"> The CEO of Sunrise Health Foods is looking to enter the growing category with a new plant-based burger product.  However, given the high rate of failure for new product launches, coupled with the high costs for entry he/she is looking to create a product that is uniquely better than the industry leaders Impossible & Beyond.  To create a new and unique product, new and unique insights are needed.  The CEO has hired me to review the vast number of product reviews captured from various on-line retailers/ sources to mine for insights that could be used by the team to ensure a successful new product launch.  The findings will help the Marketing & R&D teams better understand the consumers needs, wants, and desires along with how current solutions are failing to deliver.</td>
   <td><img src="https://github.com/rgpihlstrom/Project5/blob/main/images/SunriseCEO.png" height="300"/></td>
  </tr>
</table>



  


#### Business Questions Driving Model Development.
1. Identify the key sentiments & topics mentioned from product reviews.
2. Examples of good & bad product attributes associated with incumbents.  These will fuel product development efforts.
<br>
 
#### The  Data:
The data used for this project was scraped from the below sites in the listed quantities:  The dataset contains approximately 3000 reviews.
  
<br>
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/OverviewOfTheData1.png" height="300"/>

#### Model Development Methods:
This project uses the Crisp DM methodology to generate and optimize used models.  Crisp DM requires the blending of business strategy, available data, and the use of the best modeling techniques dictated by business drivers.  Model development is and was very iterative.  I began by doing secondary research around the basic business drivers of the industry, and gaining a better understanding on the top selling products and brands of plant-based meats (thanks to my friends a IRI :) ).  Along with the project requirements noted above, the following additional factors were considered during the modeling process:
-   **1. Data Imbalance** Early in the development process it was obvious that I would be dealing with an imbalanced set of data (more information/ rows of data on positive reviews vs. negative reviews).  To offset this problem, I split the data into two sets: positive and negative.  This step ensured the negative topics/ attributes would be surfaced without being clouded by the vast majority of positive reviews. 
- **2. Selection of Unsupervised Topic Modeling Techniques** Initially I tried several different types of topic models, ranging from Mallets LDA, HDP, Multicore LDA, other.  Ultimately, I decided to use <b><ins>Genism’s Multicore LDA model</ins></b>, as this topic model continued to produce more coherent topics with higher coherence scores during my iterative approach to modeling.
- **3. Technical Challenges - LDA & Reviews with Few Words:**  Discovering the optimal number of topics, finding The "right" words for each Topic and finding topics that represented a portion of each doc/ review is/was a very iterative process.  LDA Topic modeling is a technique that is considered a "soft" classifier and interpreting results are part-art-part-science.  Experts suggest the higher the coherence score the better, but the max coherence score does not always translate to the most interpretable/ translatable topics.  Instead, when using topic modeling to find hidden topics the user is required to use a blend of domain knowledge, coherence score, coherence overlap, and topic interpretability to select the “right” number of topics with a corpus. During this project I achieved coherence scores that ranged from .2 - .72.  Ultimately, I chose hyper-parameters that created models that reached coherence scores greater than .45 and then selected the number of topics per dataset based on interpretability coupled with my domain knowledge on the subject, as I have over 15 years of experience in the food innovation space.  I also cross referenced my number of selected topics per dataset against a Kmeans elbow graph to ensure alignment.  Lastly, I used pyLDAvis.gensim to ensure separation of topics.  Below are the results from both the positive and negative datasets associated with each topic model.

#### Model Results:

After several iterations, the below topic models were created <b><ins>50% Coherence - Positive Reviews</ins></b>,  <b><ins>60% Coherence - Negative Reviews</ins></b>, These results were achieved using the <b><ins>LDA Multicore in gensim</ins></b>.  It is important to remember these results were achieved with a focus on interpretability not maximizing coherence scores.

 <br/>

##### From Positive Reviews
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/TopicModelingPositive.png" height="400" />

###### Explination
<h5>Topics Derived From Positivly Rated Reviews</h5>
<strong> - Topic 0</strong> = <b><ins>NEW FAMILY FAVORITE</ins></b> Per the pyvis graph above this was by far the most dominate topic in the positive set of reviews.  In Studing the reveiws most associated with the topic and key words this topic can be called  as the reviews here were raving about the simliarity to real meat, great taste, great substiture for beef.
<strong> - Topic 1</strong> = <b><ins>WORTH THE SACRIFICE</ins></b> as the reviews most associated with this topic and the dominate words correlated quality texttures, reception of price, filling, and being impressed, despite a few concerns on long/ odd ingredient lists aka (chemicals).<br/>
<strong> - Topic 2</strong> = <b><ins>RIGHT PROPOSITION</ins></b> as the reviews most associated with this topic and the dominate words correlated with size of the product and number of items contained in the package along with all the benefits associated with animal and eco friendly. <br/>
<strong> - Topic 3</strong> = <b><ins>GUILT  FREE CONVENIENCE </ins></b> as the reviews most associated with this topic and the dominate words correlated with easy of use, versatility and the health benefits associated with avoid the hormons associated with non-organic beef farms.

<br/>

<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/TopicModelingNegative.png" width="775" />

<h3>Topics Derived From Negatively Rated Reviews</h3>
<strong> - Topic 0</strong> = <b><ins>BUYER BEWARE</ins></b> Per the pyvis graph above this was by far the most dominate topic in the negetive set of reviews.  The reviews here were blasting the horrible smells, resembalance to wet petfood and its very large gap between the textures offered vs. real beef.
<br/>
<strong> - Topic 1</strong> = <b><ins>NOT WORTH THE SACRIFICE</ins></b> as the reviews most associated with this topic and the dominate words correlated with long list of ingredients, ingredients that cannot be pronounced (aka chemicals) and the high cost relative to beef.
<br/>
<br>

#### Example Reviews From Scrapped Sources Associated with Key words
<img src="https://github.com/rgpihlstrom/Project5/blob/main/images/ExampleReviews.png" />




### Summary of Product Areas for R&D Teams To Consider:
- Positive Topics/ Attributes: 
- Negative Topics/Attributes: 
<br/><br/>
<strong>***Key Take Away/ Product Attributes to Target</strong> = Well received all around, meeting many needs for consumers desire for: <b><ins>Taste, Texture, Convenience, Price, Eco</ins></b>… willing to “put up” with <b><ins>Smell and Ingredient list</ins></b>… at least for now... however as a R&D staff they should target:  <b><ins>SMELL, APPEARANC, PRICING, INGREDIENTS </ins></b> as opportunities to offer something new and unique to the market.


#### Next Steps - MORE DATA

- **MORE DATA - Retailers Should Motivate More On-line Consumer Reviews** - Quantity & Diverity of Thought:  One of the challenges of this project was amassing enough data to obtain the quantity of data required to create robust models.  In order to encourge this type of analysis in the future and accross several categories more reivews would be helpful, also pushing consumer to generate organic thoughts for targeted product attributes, dislikes, etc.

- **MORE DATA - Developing More Extendables Models** - More Sources of Data:  Per the above obtaining data is a challenge.  Additionally, obtaining data that is also rated is even more of a challenge.  In order to combat this problem I could develop an algorithm that would take the ratings from reviews that allow the user to enter a ratings (amazon) and using that data to project a rating on to reviews that do not allow the user to enter a rating (twitter,tic-tok, FB).  By creating a more extendable more will allow for the use of more sources of data, and ultimately increases the quantity. 

- **MORE DATA - Leveraging Video Content To Create Reviews** - While scraping sites for this project, such as twitter, I encountered several tweets that contained the words "Beyond Burger Review" or "Impossible Burger Review" that were not really reveiws but instead were really just links to youtube/ other videos.  If there was a technolgogy to summarize videos down to a review would be invaluable.

See the full analysis in the [Jupyter Notebooks](folder) or review our <a href="https://github.com/rgpihlstrom/Project5/blob/main/Presentation.pdf">Presentation</a>.

For additional info, contact me here: [ Russell Pihlstrom](mailto:rgpihlstrom@yahoo.com)
