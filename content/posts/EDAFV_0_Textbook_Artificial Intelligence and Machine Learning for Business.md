---
title: Textbook：Artificial Intelligence and Machine Learning for Business
author: "Misty"
tags: ["HKU","ECOM 7122","Entrepreneurship Development","Book"]
categories: ["Entrepreneurship development and FinTech ventures in Asia"]
date: 2021-03-12
---

# Artificial Intelligence and Machine Learning for Business

## 1.Introduction

#### Topics in the book

* What machine learning and artificial intelligence are.
* The sort o things organizations use artificial intelligence for.
* What a predictive model looks like.
* The relationship between artificial intelligence, machine learning and Big Data.
* The people and tools needed to apply artificial intelligence.
* How to use artificial intelligence to improve business processes and the bottom line.
* The legal and ethical issues that need to be considered when developing artificial intelligence based solutions that are going to be used to make decisions about people.
* How advanced forms of machine learning are applied to drive artificial intelligence applications such as object recognition and language translation.
* The current limitations of machine learning and artificial Intelligence.

## 2.What are Machine Learning and Artificial Inteligence?

#### ML-Definition

Machine learning is the use of mathematical procedures (algorithms)to analyze data. The aim is to discover useful patterns (relationships or correlations)between different items of data. Once the relationships have been identified, these can be used to make inferences about the behavior of new cases when they present themselves. 

#### Applications

* Object recognition
    * One application of machine leatning is obiect recognition. The goal is to develop systems that can identify everyday objects from images the systemn is presented with. The data used to develop an obiect recognition system consists of pictures of different obiects such as chairs, umbrellas, washing machines and so on .Each picture presented to the machine learning algorithm is labeled to identify which type of object it contains.
    * By analyzing the different images, machine learning algorithms recognize that certain obiects are associated with certain features(patterns).
* Prediction
    * One of the most common, and arguably the first, application of machine learning is prediction. It’s about using machine learning to determine something that you don’t currently know, based on the information that you currently have available. The patterns that one finds relate to the relationships between behaviors and outcomes. Very  often  this  relates  to  people’s  past  behavior  and  what  they subsequently went on to do. Having identified the relationships that exist, it is then possible to make predictions about someone’s future behavior  based  on  their  current  state  of  being.  If  you  give  me  a sample of peoples’ previous purchasing history, I can utilize machine learning to identify patterns in their purchase behavior. I can then use these patterns to  predict what goods someone is likely to buy next; i.e. future purchases are the outcome that I want to predict. This allows me to target them with tailored promotional offers for those specific products.
    * Using machine learning for prediction is sometimes referred to as predictive modelling or **Predictive Analytics** (PA) . In fact , predictive analytics 1s such a common application of machine learning that many people (rightly or wrongly) often use the two terms interchangeably.
* Reducing uncertainty
    * Another way to think about machine learning / predictive analytics is as a method of reducing uncertainty. There are a whole host of possible outcomes that could occur in any given situation Machine learning won't tell you with absolute certainty which outcome will occur , but it can provide some insight into the likelihood or odds . of each outcome.
    * A predictive model ( or just model going forward ) is the output generated by the machine learning process . The model captures the relationships ( patterns ) that have been uncovered by the analytics process . Once a model has been created , it can be used to generate new predictions . Organizations then use the model's predictions to decide what to do or how to treat people . So , machine learning is brocess and a predictive model is the end product of that process.

#### Situations and Problem

* credit scoring
    * One very well-known application of machine learning is credit scoring . When someone wants a loan , credit card or mortgage the lender asks the individual questions about themselves and their lifestyle . They then combine this with information from a credit report containing details about the individual's previous borrowing history , provided by a credit reference agency such as Experian or Equifax. The information is then fed into a predictive model to generate a credit score.
    * If you live in the USA you will probably be familiar with FICO and / or Vantage scores . A high score 750 ) is a prediction that someone is very likely to repay any money they borrow ; i.e. that they are creditworthy . A low score ( < 500 ) indicates that someone is very uncreditworthy . Banks and finance companies the world over use similar credit scoring methods.
* target marketing
    * Another common application of machine learning is target marketing , Given information about someone's age , gender , income web-browsing , purchase history , location and so on , a marketing department can predict if the person is interested in a particular product or not . They then use that prediction to decide whether or not to target them with promotional offers . Likewise , predictive models can also be used to infer how much people are willing to pay for products like insurance . This information is then used to tailor a personalized pricing strategy to each person's individual circumstances.
* preventative health care
    * A further example of machine learning in action is preventative health care . Traditional health care systems are reactive . Peopl de seek medical assistance when they feel ill . Doctors then do their best to reat the illnesses they are presented with-treatments that can be very costly and time consuming . These days , advanced health care systems are increasingly focusing their attention on prevention rather than cure . This vastly reduces costs and improves patient outcomes . Machine learning is used to assess peoples medical records and predict the likelihood of the them developing specifc conditions such as heart disease or diabetes. often vears in advance Individuals who come at the top of the pile ; i.e. those that the model predicts are most likely to get the disease , are contacted with a view of initiating preventative action . For example , making lifestyle changes of taking preventative medication.
* Recommend
    * A final example of machine learning in action is determining what type of news ( and other ) articles to recommend to people . Social media providers use machine learning to analyze what articles you ve read in the past and the type of topics you discuss with friends then drives the content that they promote to you.

#### AI-Definition

* There are many and varied definitions of what A is , and as with predictive analytics , many people use the terms AI and machine learning interchangeably . In terms of the overall scope of AI research , machine learning is a key field of study , but there are many others . True artificial intelligence is about muc much more than just pattern recognition and prediction . Some experts also question if true AI can ever be achieved by just following a Brute force approach of developing ever more complex algorithms using ever more powerful computer hardware Is there some additional ( as yet unknown ) element required for human-like intelligence and self-awareness which cant be replicated ia computation alone ?
* So in one sense its incorrect to say that machine learning an artificial intelligence are the same thing . However , in practice almost every AI system in use today relies heavily on machine learning
Therefore , for the purposes of this book a simple working definition of AI that we shall adhere to it:

**Artificial Intelligence ( AI ) is the replication of human analytical and / or decision-making capabilities**

#### Narrow AI and General AI

* All of the A applications in use today are what the industry refers to as **Narrow AI** . They are very good at behaving intelligently wher applied to one well defined area of expertise . However , these systems are miles away from **General AI** . 
* General AI is a system that can learn and act intelligently across a wide range of environments and problems in a similar way to a person . An AI application that is used to detect tax avoidance for example , is useless at detecting the signs of cancer from medical scans . However a erson could learn to do both these tasks if they were given suitable raining . In a similar vein , a system such as Google Translate is great at understanding the spoken word but wouldn't be much use when it comes to assessing if someone on a dating site might be compatible with you.

#### the Core Components

* Data put
* Data preprocessing
* Predictive models
* Decision rules(rule sets)
* Response/output

#### Artificial intelligence and rule making
* Algorithm generation rules
* Manual rule making

#### Pattern recognition
* The vast majority of AI applications rely heavily on prediction driven by pattern recognition ( i.e. machine learning / predictive analytics ) . Take speech recognition systems that support tools such as Apples Siri and Amazon's Echo . Upon hearing a sound , a speech recognition system pre-processes that sound into a number of standardized soundbites . It will then try to identify what word it thinks has been spoken . This is based on a set of probabilities (scores) generated by a predictive model created using machine learning . If the system calculates that there is a 5 % o chance that the sound is "Hello" 20% that it's "Jell-O" and 75% that it's "Mellow" then it will make an educated guess that the word spoken was “Mellow”.
* Advanced AI systems use layers of complex predictive models in combination to formulate a view as to what is going on around them given the inputs that they receive . The next layer of the speecl recognition system will consider phrases and word structure . The predictive elements of the system are then combined with decision rules ( decision logic ) to determine what actions to take when certain words or phrases are spoKen .

#### Three changes
* terminology
    * In the 1980s / 1990s what is now termed machine learning / AI came under the title of Data Mining or computational statistics . Its also the case that the theory underpinning the most common machine learning approaches in use today were developed before or during the 1990s (although many have been refined and extended since then).
* computer hardware and software
    * The second thing that has changed is the computer hardware an software that underpin machine learning.The shift to placing services online via smartphones. tablets and the internet means that there is now so much more information available about people than ever before . and the amount of information continues to grow vear on year . The speed and storage capabilities of computers has also increased considerably . This makes it possible to process huge amounts of data quickly and cost effectively . Likewise , the complexity of machine learning algorithms and the predictive models they generate has increased by many orders of magnitude in just a tew years.
    * In parallel with the advances in hardware and algorithm design there are now a whole host of software tools availlable for machine learning . Much of it free and / or open source ( such as the R and Python programming languages ) and available via one's PC , laptop or cloud services offered by the IT giants such as Microsofto and google
* the way that we interact with the underlying models and decision rules
    * We no longer have to type very rigld instructions on keyboards of have to interpret pages of detailed mathematical output . Instead , modern A systems interact with us in much more human-like ways.

#### the interfaces between humans and computers

* Often the interfaces between humans and computers are themselves based on machine learning principles , driven by predictive models . 
* If we return to the whisky sales example , I could use machine learning in the design of a chatbot to talk to people on social media about their drinking habits . The data gathered by the chatbot then supplements other data that Ive gathered about people . If the whisky application determines that people should be given a discount offer , then this could be relayed back to customers via the chatbot in a conversational form . rather than the more traditional approach of sending them a coupon or discount code via text or e-mail.
* The same principle applies to digital personal assistants such as Amazons Echo . One set of algorithms are used to translate what you say into soundbites ( data pre-processing ) . The pre-processed soundbites are then fed into another set of predictive models which to predict what outcome you are asking for ; such as playing a certain song or asking about the weather . Amazon allows developers to use this pre-processing capability for freell-allowing anyone to incorporate advanced speech recognition into their programs and apps.

#### the cost of entry into the world of machine learning and AI has reduced considerably

* What all this means is that the cost of entry into the world of machine learning and AI has reduced considerably . Only a few years ago machine learning was primarily the domain of large businesses and academic institutions . Today , anyone with a laptop and some time on their hands can get involved and start building predictive models relatively quickly and at almost zero cost , and then develop an advanced user interface to implement those models as an AI app.
* These days . there are even competition websites for machine learning such as Kaggle, Organizations provide their data for free , and then amateur and professional teams compete to see who can build the model with the greatest predictive power using the data that has been provided .

#### data science and data scientist

* Data science isn't a science in the same way that physics chemistry or biology are . It's simply a description of the application of machine learning techniques . 
* Likewise , a data scientist is someone who can apply machine leamning in a practical way . Its about more than just the mathematical aspects of the subject . 
* A good data scientist also has an understanding of data and IT systems and is able to understand the business context in which their solutions will be applied.

## 3.What Do the Scores Generated by a Predictive Model Represent?

#### The types of scores generated by a predictive model

* Probability ( likelihood ) scores . These predict the likelihood of specific events . For example , will someone do something or not ? The technical name for a predictive model of this type is a **classification model**.
* Magnitude ( quantity ) scores . These predict the amount or size of something . For example , how much someone is going spend in store , or how long before they do something . The technical name for a predictive model of this type is a **regression model**.

#### Classification model
* Classification models predict the likelihood that events occur . Often these events will be binary in nature; i.e. a single score is generated , representing the likelihood that the event will occur . However , classification models can also be used to address problems with multiple outcomes ( events )
* Common business appl plications of classification models include:
    * Medical diagnosis
    * Content detection
    * Customer attrition
    * Fraud detection
    * Dating compatibility
    * Product recommendation
    * Staff retention
    * Machine breakdown
* Sometimes the scores from a classification model represent a probability directly . A person who receives a score of 0.0 certainly won't experience the event . Those with a score of 1.0 certainly will predictive models don't provide perfect predictions . What one tends to see is a spread ( a distribution ) of probabilities between 0.0 and 1.0 for individuals within the population . When a product recommendation model generates a score of 0.70 for someone . this means that the model predicts that there is a 70% chance that the individual will buy the product and a 30 % chance that they won't.
* In other situations . the scote ftom a classification model is ansfotmed to a certain scale . If we return to the world of credit scoring , credit scores tend to be scaled to range from about 400 to about 80014 . If someone receives a score of 400 it means that they are very unlikely to repay any credit advanced to them (<5 % chance that the loan will be repaid ) . A score of 800 means that they will almost certainly repay their debt(>99.9% chance that the loan will be repaid )
* Most classification models used in business generate a single score . The score predicts a simple yes / no type event , such as those described in the aforementioned list . Where machine learning is applied to problems with multiple outcomes , then a separate score is produced for each possible outcome.
* Taken to their extreme , some of the most advanced predictive models in use today generate thousands of scores . Each score represents the probability of one possible outcome . An object recognition system , designed to identify everyday objects in pictures , is one such example . The system generates a score ( probability ) for each obiect it's been trained to identify Score 1 predicts a 4% chance it's a picture of a washing machine , Score 2 a 6% chance it's an umbrella Score 3 an 80% chance it's a chair and so on . The score associated with " Chair is the highest and therefore the system would Guess ? that the obiect is a chait.
* For complex applications such as object and speech recognition , business users won't see the scores generated directly . Instead . an overarching set of decision rules will be applied to translate the scores into something more meaningful , with the results delivered via a suitable customer friendly interface.

#### Regression model

* Regression models on the other hand are all about quantities ; i.e. the magnitude of an event . Some examples of business applications
of regression models are:
  * Life expectancy
  * Journey time
  * Credit loss
  * Spend
  * Purchase interval
  * Call length
  * Occupancy
  * Response time

#### Which model
* Both regression and classification models are widely used , but classification models tend to be the most popular , particularly for common business applications . This is because simple will they / won't they type events have traditionally been the easiest for organizations to understand . There also tends to be less ambiguity in how problems are defined . This makes it simpler for data scientists to translate business objectives into an appropriate numerical representation that the machine learning process can be applied to . Defining if a customer buys whisky or not is pretty straight forward ( classification ) However , determining the profitability of an individual whisky sale is far more complex (regression).
* What type of model to use ( regression or classification ) depend verv much on what one wants to do with the model scores . If all Im interested in is identifying which credit card customers ate most likely to move to a competitor , then what I need is a classification model to predict the probability of attrition . A retention strategy ( such as offering a discount or free gift ) is then applied to try to retain those customers most likely to defect.
* If on the other hand , my primary concern is to identify profitable customers with the aim of encouraging them to spend more , then what I need is a regression model . The model is designed to predict who are going to be the big spenders and target those . I dont nee to bother with the rest of the customer base.
* There is however , a third option . Let's say that what Im really interested in doing is retaining profitable customers , and I don't care bout losing the unprofitable ones who don't spend much on their cards . In this situation , then possibly the best approach is to build two separate predictive models as folows:
  * An attrition model to predict those customers most likely to defect to a rival product ( Classification )
  * A revenue model to identify which customers spend the most(Regression)
![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210318111658.png)




## 4.Why Use Machine Learning ? What Value Does it Add?

#### Why use Machine Learning
Applications of machine learning based on Predictive models are increasingly being used to replace and / or supplement expert judgement and manual decision-making in all sorts of areas . This is because predictive models tend to be:

* More accurate than human experts

* Unbiased

* Fast

* Cheap

#### Application Scenarios

* Bank loan decision making
* marketing management
* crime

#### Limitation
Despite all the arguments in favor of automated decision-makin systems based on predictive models , dont make the mistake of thinking that machine learning is perfect . Predictive models can and do get things wrong on a frequent basis , but on average just not quite as often as people . In a similar vein . if there are problems or biases with the data feeding the algorithms used to construct a predictive.

Another concern is that if a data scientist has particular prejudices then it is possible for them to consciously design these into the stem , subverting what the data is telling them . This however , can also work to peoples benefit . If it is believed that a user does not like the decisions being made , then a well-designed system will all the decision logic to be modified / overridden-as we discussed relation to the whisky sale example in previous chapters What this means is that there needs to be oversight of machine learning based decision-making systems , and an appropriate set of checks and balances in place to ensure that the systems work in a way that is both legal and ethical.


## 5.How Does Machine Learning Work ?

#### three most popular types of model
Most machine learning applications are underpinned by predictive models .The scores generated by the model(s) then drive decision making and the subsequent actions that are taken .So ,how does a predictive model generate a score ?That depends on the type of predictive model being employed ,and there are quite a few options to choose from .However , the three most popular types of model, which are used in the vast maiority of real world business applications , are Scorecards(linear modeds), Decision Trees(Classification And Regression Trees or CART) and Artificial Neural Networks(ANNs) , most commonly referred to as just Neural
Networks(NNs).

#### a model of heart disease
* forecast horizon
* observation data
* outcome data
* development sample
* validation sample
* Linear Regression and Logistic Regression

## 6.Using a Predictive Model to Make Decisions

* The use of the model of heart disease
    * The cut-off strategy (decision rule) to apply is:  Invite anyone scoring 521 or more for a check-up and lifestyle review with their doctor.
* The model is not perfect. It gets things wrong 26% of the time, but it’s performance is far far better than selecting people at random for check-ups. With only 6% of the population expected to develop heart disease in the next five years, a random invitation strategy would result in 94% (100% – 6%) of the check-ups being wasted on people who were not going to develop heart disease in the first place.
* Two of the most popular ways of providing a graphical representation of a score distribution table are Lift and Gain charts.


## 7.That's Scorecards but What About Decision Trees?

#### a simple description of a decision tree algorithm
* Step 1: Pick one data item in the development sample(e.g. income)
* Step 2: Find the value of income which results in the best partitioning of the data into two parts . By "best" I mean a low income group and high income roup such that the incidence of heart disease is maximized in one roup and minimized in the other.
* Step 3: Repeat steps 1 and 2 for all other data items in the development sample i.e. replace income with age , BMI , smoker ect.)
* Step 4: From what has been found in steps 2 and 3 , split the development sample into two parts using the best partition found ; i.e. split the development sample such that the incidence of heart disease is maximized in one sp oit and minimized in the other.
* Step 5: Repeat steps 1-4 for each of the two resulting parts of the development sample . Keep doing this until no more significant differences can be found from further splitting

#### the similarities and differences between the tree model and the scorecard model

* The decision tree and scorecard use similar, but not identical, data items  to  make  their predictions. The  scorecard includes annual  income  but  the  decision  tree  does  not.  “Graduate” features in the decision tree model but not the scorecard.  
* The branch conditions in the decision tree don’t always align with the  score ranges in the  scorecard. In the  scorecard, age breaks occur at 49 and 57, but in the decision tree, the key age split is at 52 years old (with additional age splits further down the tree).
* The decision tree generates 13 possible scores, whereas there are hundreds of scores that can be generated by the scorecard; i.e.  the  scorecard  generates  a  much  more  granular  range  of scores than the decision tree.


#### Model choose
This is another great feature of machine learning . This is because means that other factors . in addition to predictive accuracy . can come into play when deciding which model is best for a given problem . In particular , in some problem domains , having a model that is easily explicable and which is aligned to a common-sense view as to how decisions should be made is vital . This is sometimes far more important than having a model that is theoretically more appropriate or marginally more accurate , but which is less wel understood by business users or industry regulators


## 8.Neural Networks and Deep Learning

#### The operation of the neuron

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210411000954.png)

1. The observation data , such as Age and BMI , provides the inputs to the neuron.
2. Each input is multiplied by a weight ( which can be positive or negative ) . For non-numeric data such as gender or smoker , 0 / 1 flags are used to represent each condition . For example, 1 if female, O if male.
3. The inputs , multiplied by their weights , are added up to get an initial score.
4. After the initiall score has been calculated it is transformed. Often this is to force the score to be in the range 0-1 . This transformation is not absolutely essential but is deemed good practice . This is so that when the neuron is combined with others to produce a neural network , all the neurons produce values in the same range ; i.e. between 0 and 1.
5. The transformed version of the initial score is the output score produced by the neuron

![](https://cdn.jsdelivr.net/gh/M1styDay/image_hosting@master/hugo_images/20210411003929.png)

* The inputs to each neuron in a given layer are the same ( e . g Age , BMI etc for the first layer neurons , but the weights within each neuron are different . Therefore , each neuron produces a different score
* The outputs ( the scores ) from the first set of neurons ( the first layer ) provide the inputs to the second set of neurons ( the second layer)
* There are four neurons in the first layer in this example . In ractice , the optimal number of neurons cant be determined up front . Instead , a number of competing models are built with different numbers of neurons , and the one that performs the best is chosen . A rule of thumb that works well for most business applications is to have between half and double the number of input data items ( so between 4 and 16 in this example
* There are lots of weights . Figure 8 is a very simple network . It has just 8 input variables and 5 neurons , but there are 36 weights . A typical business application with say , 100 input variables and 75 neurons , would have 7 , 474 weights

#### how does the training algorithm determine what the weights should be?

* Assign each weight a random or zero value
* Calculate the scores generated by the network for all of the cases in the development sample
* Assess how accurate the final score is . For example . b assessing the lift and gain properties of the model.
* Adjust the weights so as to improve the predictive accuracy of the model
* Repeat steps 1-4 until no further significant improvement in model performance is observed , or a certain amount of time as elapsed

#### Advantage and Disadvantage

* The reason why neural networks are so popular is their ability to detect subtle patterns in data which other simpler methods , such as scorecards and decision trees . may not be able to detect . This means that they can potentially produce more accurate predictions . This is achieved by having the two layers of neurons , with the scores from te first layer providing the inputs to the second layer
* The main drawback of neural networks is that the scores that they generate are not intuitive . Yes , one can see what the various weights in the model are and understand the overall score calculation . but if I was to ask you which input variable in Figure 8 contributes the most to the final score . then this is much less obvious than for the scorecard and decision tree models of heart disease . This is potentially a problem if there is a business or legal requirement to explain how the final model score was arrived at

#### Deep Learning
* Deep learning represents the latest evolution of neural network type models.
* convoluted neural network
* recurrent neural network

#### if things can be thought of as either a "simple" or "complex" type of prediction/AI problem

* “Simple”  AI  problems.  These  have  a  singular  objective  or thing that one is trying to determine, which is easy to quantify. For a classification problem, this means that the outcome can be expressed as a simple “Yes” or “No” such as does someone default  on  a  loan  or  not?  For  a  regression  problem,  can  the outcome be expressed as single number? Such  as how much someone spent in store the last time they shopped.
* “Complex”  AI  problems.  These  usually  have  multiple  and very  nuanced  objectives.  Classic  examples  of  “complex” problems are object recognition, language translation and game playing  (e.g.  chess  or  Go).  This  also  includes  problems  that require  multiple  machine  learning  approaches  to  be  used  in combination,  such  as  in  autonomous  vehicles  and  digital personal assistants.


## 9.Unsupervised and Reinforcement Learning
## 10.How to Build a Predictive Model
## 11.Operationalizing Machine Learning

## 12.The Relationship Between Big Data and Machine Learning

#### Big Data includes:
* Text
* Images
* (Social)network data
* Geospatial
* Biometrics
* Product(machine) generated: Iot

#### Modern data computer systems are very good at:
* Storing massive amounts of data
* Data cleaning and formatting
* Processing date very queickly

#### Hadoop/MapReduce

some software and application...

#### the relationship between big data and ml

* A good way to think about the relationship between Big Data and machine learning is that the data is the raw material that feeds the machine learning process . The tangible benefit to a business is derived from the predictive model (s) , customer clustering or other analytical outputs that are delivered at the end of the process, not the data itself.
* Artificial intelligence , machine learning and Big Data , are therefore often talked about in the same breath . but it's not a symmetrical relationship . You need machine learning to get the best out of Big Data , but you don't need Big Data to be able use machine learning effectively . If you have a just few items ofinformation abour a few hundred people , then that's enough to start to apply machine learning to do things such as building models and making predictions , applying clustering to customers and undertaking other types of data analysis.
* The more and better data that you have , the better your machine learning solutions will be , but having gigabytes or terabytes of is not a prerequisite for practical machine learning.

## 13.Ethics , Law and the GDPR
#### In assessing the ethical risk associated with an automated decision-making svstem . there are three main aspects to consider:
* Beneficiary
* Data Immutability
* Impact(significance)

#### If an organization identifies that it is using predictive models to take what are potentially "High risk" ethical decisions , then what should it do : The answer is to take mitigating action as follows:
* Try to identify at-risk groups . The way to do this is to produce sepatate score distribution reports for groups such as women , ethnic minorities . children and so on . It can then be seen if there is any bias in the resulting scores ; i.e. which groups tend to get lower than average scores and will therefore be adversely treated compared to the wider population.
* For  those  groups  that  score  less  well  than  the  population average, constraints and override rules should be used to ensure that they are treated in a fair way. Likewise, different cut-offs may need to be set for at risk groups.
* Continue to monitor the situation once the decision-making system goes live . Regularly revlew the score protile and decision rules for key groups . Cut-offs , constraints and overrides should then be fine-tuned as required.

#### The GDPR covers a wide range of issues relating to personal data and applies to all automated decision-making and profiling applied to living individuals. The four areas that are particularly relevant in a machine learning / AI context are:

* Explicit consent needs be obtained from someone before their personal data can be gathered or used. The consent can’t be inferred or be “consent by default.”  
* It is  not permitted to make  decisions about people, using an automated  decision-making  process  which  has  a  legal  or similarly significant impact upon them unless they have given their consent that automated decision-making can be used for this purpose. This is additional to the consent to hold data. The primary exception to this is where automated processing is necessary to allow a legal contract to be enacted.
* An individual has the right to be provided with an explanation as to how an automated decision has been arrived at and the consequence of that decision of that decisions This aligns with the more general requirement in the GDPR for organizations to provide individuals with information necessary to ensure that fair and transparent processing of their data occurs.
* Automated decision-making systems must not display unfair discrimination;i.e. treating people differently on the basis of their race sexual orientation and so on.

#### Organizations which are investing in Big Data and automated decision-making processes need to:

* Assess the risks and issues associated with machine learning and automated decision-making up-front It's not an add-on at the end of a proiect.
* Not to do away with all human expertise entirely . There must be a suitably trained operational function that can process decisions manually when required.
* manage and provide oversight of their decision-making systems . This includes developing approaches to identify and mitigate risks as they arise , as discussed previously.

From a project management perspective , the requirement for governance and manual intervention can have a significant impact on the costs of developing and maintaining automated decision making systems . If you are considering using automation within your organization , then this additional overhead needs to be included within the cost-benefit case undertaken before the proiect begins.

In terms of operational usage , if you use predictive modes to do things like deciding who you are going to fire , then you need to have people who can review the data used by the model and who can override the original decision if necessary . In fields such as insurance and credit granting , this means that you'l need to retain expert underwriters who can challenge the decisions made by the organization's automated underwriting systems . There also needs to be a process in place to deal with customer queries about automated decision-making and to supply relevant information to them as required by the legislation.



## 14.The Cutting Edge of Machine Learning
## 15.When Can I Buy a Self-Driving Car ?
## 16.Concluding Remarks
## Appendix A. Evaluating Predictive Models
## Appendix B. Further Information and Recommended Reading
## Appendix C. Popular Terms in Machine Learning and AI
## Appendix D. A Checklist for Business Success
