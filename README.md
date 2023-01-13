# 
<img src="https://www.vidyard.com/media/real-estate-video-marketing-1920x1080-1.jpg">

# Bias Detection in Mortgages Approval Process

## Table of Contents
- [Project Objective](#project-objective)
- [Data Source](#data-source) 
- [Preprocessing](#preprocessing) 
    - Filter
- [Hypothesis Tests](#hypothesis-tests): run on ny_filt, control on debt-income
- [PCA: Dimensionality Reduction](#pca-dimensionality-reduction)  
- [Logistic Regression](#logistic-regression)  
- [Methods Used](#methods-used)
- [Technologies](#technologies)

## Project Objective
[(Back to top)](#table-of-contents)
<br>
Under the Fair Housing Act, it is illegal for banks to deny mortgages on the basis of race, color, religion, national origin, handicap, familial status or sex of the applicant. The rise of Automated Underwriting Systems (AUS) enables algorithms to decide on mortgage applications faster than the traditionally manual review process. However, as financial institutions move towards more data-driven processes, understanding the underlying biases in these algorithms, as well as the underwriting process in general, is the first step to ensuring equitable outcomes. Leveraging data on mortgage lending transactions in 2021 from the Federal Financial Institutions Examination Council (FFIEC) in the state of New York, this project aims to provide insight on 
features important for mortgage approval, particularly if they include protected characteristics. This project contains the following three sections. 

1. Hypothesis Tests: ___ <br>

2. Dimensionality Reduction via PCA: ____ <br>

3. Logistic Regression: ____ <br>

## Data Source
[(Back to top)](#table-of-contents)
<br>
**[Federal Financial Institutions Examination Council 2021 Loan/Application Records](INSERT LINK - PUT ZIP IN REPO):** <br>

**[Data Dictionary](https://ffiec.cfpb.gov/documentation/2021/lar-data-fields)** <br>

## Preprocessing
[(Back to top)](#table-of-contents)
<br>
The following table displays the amount of stop words and punctuations removed from the original text. 35-45% of total word count were removed for the five companies. 

  <img src="https://github.com/jchen9619/Sentiment-Analysis-for-SEC-10-k-Reports/blob/main/img/stopwords.png" />
</p>

## Comparison of Sentiment Word Frequency
[(Back to top)](#table-of-contents)
<br>
The following tables display the frequency of positive and negative words in item 1A, item 7 and the two sections combined. 
  <img src="https://github.com/jchen9619/Sentiment-Analysis-for-SEC-10-k-Reports/blob/main/img/1afreq.png" />
</p>
  <img src="https://github.com/jchen9619/Sentiment-Analysis-for-SEC-10-k-Reports/blob/main/img/7freq.png" />
</p>
  <img src="https://github.com/jchen9619/Sentiment-Analysis-for-SEC-10-k-Reports/blob/main/img/totalfreq.png" />
</p>
With the range of Positive Words Frequency being much narrower than that of Negative Words Frequency among the five companies, Negative Words Frequency serves as a differentiator in the tones of the 10-k financial reports.

Overall, Moderna, Inc. ranks highest in frequency of negative words, followed by Eli Lilly and Company, Johnson & Johnson, Pfizer Inc. and AbbVie Inc. However, for the individual items, Eli Lilly and Company ranks highest instead. It appears Moderna's high overall ranking is mostly attributable to high negative words frequency in item 1A. <br>

Zooming in on item 7, which discusses the company's annual performance in greater detail than item 1A, Eli Lilly and Company, Pfizer Inc. and Johnson and Johnson's reports are worth a more in-depth read as their tones indicate more negative sentiments than the rest. <br>

## Identification of Top Sentiment Words
[(Back to top)](#table-of-contents)
<br>
The following tables display top 10 most frequently sentiment words for item 1A and 7 respectively. 
  <img src="https://github.com/jchen9619/Sentiment-Analysis-for-SEC-10-k-Reports/blob/main/img/1a%20top10.png" />
</p>
  <img src="https://github.com/jchen9619/Sentiment-Analysis-for-SEC-10-k-Reports/blob/main/img/7%20top10.png" />
</p>
You may notice one or two of the top 10 most frequent sentiment words being of the same root word (i.e. "adverse" and "adversely"). This is due to lemmatization being skipped to save significant time on running this notebook. Regardless, the output still produces top 8-9 words. <br>
    <br>
   
Item 1A tends to include more negative words because it discusses risk factors. This is consistent with the five companies. </mark> Item 7 shows a more diverse range of sentiments, with a more even split between positive and negative words. In conjunction with the quantitative comparison of sentiment words frequency in section I, searching for the most frequent sentiment words can lead to informative insight, with the following examples: 
    
**AbbVie Inc., Item 1A** <br>
"Successful(ly)", "Adversely"<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The <ins>**successful**</ins> discovery, development, manufacturing and sale of biologics is a long, expensive and uncertain process. There are unique risks and uncertainties with biologics. For example, access to and supply of necessary biological materials, such as cell lines, may be limited and governmental regulations restrict access to and regulate the transport and use of such materials. In addition, the development, manufacturing and sale of biologics is subject to regulations that are often more complex and extensive than the regulations applicable to other pharmaceutical products...Biologics are also frequently costly to manufacture because production inputs are derived from living animal or plant material, and some biologics cannot be made synthetically. Failure to <ins>**successfully**</ins> discover, develop, manufacture and sell biologics—including Humira—could <ins>**adversely**</ins> impact AbbVie's business and results of operations.  

**Pfizer Inc., Item 1A** <br>
"Litigation", "Loss", "Adversely"<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;We recorded direct product and/or Alliance revenues of more than $1 billion for each of nine products that collectively accounted for 75% of our total revenues in 2021. In particular, Comirnaty/BNT162b2 accounted for 45% of our total revenues in 2021. For additional information, see Notes 1 and 17. If these products or any of our other major products were to experience <ins>**loss**</ins> of patent protection (if applicable), changes in prescription or vaccination growth rates, material product liability <ins>**litigation**</ins>, unexpected side effects or safety concerns, regulatory proceedings, negative publicity affecting doctor or patient confidence, pressure from existing competitive products, changes in labeling, pricing and access pressures or supply shortages or if a new, more effective product should be introduced, the <ins>**adverse**</ins> impact on our revenues could be significant.
    
**Eli Lilly and Company, Item 7** <br>
"Exclusivity", "Favorable", "Loss", "Severe(ly)" <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Revenue of Alimta, a treatment for various cancers, decreased 2 percent in the U.S., driven by decreased volume, partially offset by higher realized prices. Revenue outside the U.S. decreased 22 percent, primarily driven by decreased volume due to the entry of generic competition in certain markets and, to a lesser extent, lower realized prices, partially offset by the <ins>**favorable**</ins> impact of foreign exchange rates. Following the <ins>**loss**</ins> of <ins>**exclusivity**</ins> in major European countries and Japan in June 2021, we faced, and remain exposed to, generic competition which has eroded revenue and is likely to continue to rapidly and <ins>**severely**</ins> erode revenue from current levels. In the U.S., we expect the limited entry of generic competition starting February 2022 and subsequent unlimited entry starting April 2022. We expect that the entry of generic competition following the <ins>**loss**</ins> of <ins>**exclusivity**</ins> in the U.S. will cause a rapid and <ins>**severe**</ins> decline in revenue.    

**Moderna Inc., Item 7** <br>
"Advance", "Progress" <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; We expect that research and development expenses will increase in 2022 as we continue to <ins>**progress**</ins> our indication expansion of mRNA-1273, and continue to develop our pipeline and <ins>**advance**</ins> our product candidates into later-stage development. In addition, we also expect to incur significant costs related to the development of variantspecific COVID-19 candidates and our next-generation COVID-19 vaccine candidate (mRNA-1283).
  
**Johnson & Johnson, Item 7** <br>
"Achieved", "Positive"  <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In 2021, sales by companies in Europe <ins>**achieved**</ins> growth of 24.3% as compared to the prior year, which included operational growth of 20.7% and a <ins>**positive**</ins> currency impact of 3.6%. Sales by companies in the Western Hemisphere (excluding the U.S.) <ins>**achieved**</ins> growth of 7.8% as compared to the prior year, which included operational growth of 7.3% and a <ins>**positive**</ins> currency impact of 0.5%. Sales by companies in the Asia-Pacific, Africa region <ins>**achieved**</ins> growth of 14.1% as compared to the prior year, including operational growth of 11.4% and a <ins>**positive**</ins> currency impact of 2.7%. 

## Methods Used
[(Back to top)](#table-of-contents)
<br>
- HTML to PDF Conversion
- Text Extraction by Key Word Search
- Lower case transformation
- Stop word removal
- Punctuation removal
- Tokenization
- Word count

## Technologies
[(Back to top)](#table-of-contents)
<br>
- Python
- PDFKit
- PyPDF
- Pandas
- RegEx
- NLTK
- Spacy
- IPython

