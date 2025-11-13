**Title**:: E-commerce Product Query Classification Using Implicit User’s Feedback from Clicks
**Authors**:: Yiu-Chang Lin, Ankur Datta, Giuseppe Di Fabbrizio
**Journal/Conference**:: 
**Citations**:
**DOI**:: 10.1109/BigData.2018.8622008
**Published**:: 2018
**Publiser**:: 

**Tags**::
**Links**:: https://ieeexplore.ieee.org/document/8622008/
**Created**:: <% tp.file.creation_date("YYYY-MM-DD") %>

[Open PDF in Zotero](zotero://select/items/@linEcommerceProductQuery2018)
# Abstract

Query classiﬁcation (QC) has been widely studied to understand users’ search intent. For e-commerce search queries, users typically search for either a speciﬁc product or a category of products. In both cases, a query can be associated with a category label that belongs to a taxonomy tree describing the items in the catalog. However, product-related search queries are typically short, ambiguous, and continuously changing depending on seasonal trends and the introduction of new products over time. Traditional supervised approaches to e-commerce QC are not feasible due to the high cost of manual annotation and the high volume of trafﬁc on e-commerce search engines. In this work, we introduce an unsupervised method to collect large amounts of query classiﬁcation data using user’s implicit click feedback. We obtain a large multi-label dataset containing 403,349 unique queries from 2,085 categories. We compare and contrast different state-of-the-art text classiﬁers and demonstrate that an ensemble of linear SVMs models achieves a micro-F1 score of 0.60 and 0.82 at leaf and top level, respectively.

# Methodology

# Overview

create a user intent classification dataset using customer click. It is a multi-label annotations where same queries with different user intention. Therefore, we will have a dataset where each keyword will link to different products. 

For example,

Query: "Apple"

1. 25 click Macbook
2. 100 click Iphone
3. 13 click Apple Watch
4. 2 clicks Apple Vinegar
5. 1 click Apple Pie.

As you can see, popular products have a lot of clicks and non-popular have sparse data. In that case combine those sparse data with their parent node (categories in that case.) 

We can even do the same for popular products.

Query: "Apple"
1. 138 click on Electronic
2. 3 clicks on Food 

# Build Dataset

## Build User Intent Classification Dataset

- For each session, user might search `m` queries using the search engine.
- Each query $q_j(1 <= j <= m)$ retrieves $n_j$ numbers of products.
- They collect all query and product pairs where a product is selected by mouse click, add to the shopping cart, or purchased. 
- Then, associate product category labels to each query.

**Assumption: users behavior is coherent with the selection of the retrieved product.**


# Models

- Logistic Regression
- SVMs (Best: Single Label QC)
- Gradient Boosting Trees (GBT)
- Fast Text
- Attention Based CNNs

## Attention Based CNNs

- Train word2vec on the catalog product titles of clicked product associated with all the queries in the training data.
- Initial representation for attentional CNN is obtained from word2vec.
- Tune hyper params by 5-fold cross validation on training set.


