data science projects are failing at alarming rates.

embrace a fundamental truth: this stuff is complex.

Data Science Industrial Complex.

How can I think and speak critically about data?

In this section, we share two important examples of how data affected society at large

Mortgage-backed CDOs were thought to be a safe investment because they spread the risk associated with loan default across multiple investment units.

Assuming independence when events are in fact connected is a common error in statistics.

Why do data problems like this occur? We assign three causes: hard problems, lack of critical thinking, and poor communication.

third reason we think data problems continue to occur is poor communication

First (as we said earlier), this stuff is complex. Many data problems are fundamentally difficult.

Second, some analysts and stakeholders stopped thinking critically about data problems.

micro failures subtly reinforcing a culture without data literacy.

No one demanded we repeat what was said in a language everyone could understand.

be open to learning seemingly complicated data concepts.

build intuition, appreciation, and healthy skepticism of the numbers and terms you come across.

Lesson learned: Informed decisions require data.

Response variable is another name for label, and it's binary because there were two of them, (C) and (I).

project sponsor and data scientist quickly and excitedly discuss something called “sentiment analysis.

basic premise, you are told, is that sentiment analysis can automatically label a tweet or Facebook post as “positive” or “negative.

data scientist could count the daily totals of positives and negatives, plot the trends over time (and in real time!), and subsequently share the results via a dashboard for all to see. Most

postmortem of the project revealed no one in the company used the analysis, not even the marketers on the team. When asked why, the marketers admit they weren't really comfortable with the original analysis

everything went well. But the fundamental question—why is the project important?—doesn't appear to have been brought up.

this project exhibited two early warning signs in how the team attempted to solve the problem: methodology focus (sentiment analysis) and deliverable focus (dashboard

What is the possible business benefit of knowing the sentiment of customers on social media?

is someone going to monitor this dashboard? If the trends suddenly go down, do we do anything? What if they trend up?

If only they asked the five questions. WORKING ON PROBLEMS THAT MATTER So far, we've tied project failures to not defining the underlying problem correctly.

their skills become bragging rights for executives but don't actually solve meaningful problems?

means many data workers are dissatisfied at their jobs. Having them work on problems overly focused on technology with ambiguous outcomes leads to frustration and disillusionment.

Several of the barriers, listed here, are directly related to poorly defined problems and improper planning:

premise and structure of this book is to teach you to ask more probing questions.

You also learned about early warning signs to spot when a question starts to go off track. If the question hints of having a (1) methodology focus or a (2) deliverable focus, it's time to hit pause.

we'll give you a brief crash course on data and data types.

Information is derived knowledge.

information is continually created. Communicating and capturing that information, however, is not always simple

by encoding it. When we do this, we create data. As such, data is encoded information.

measured instance of information for a marketing campaign.

rows of each table are commonly referred to as observations, records, tuples, or trials. Columns of datasets often go by the names features, fields, attributes, predictors, or variables.

two most common data types are described as numeric or categorical.

continuous variable

Count (or discrete) data, unlike continuous data,

Ordered (or ordinal) data is categorical data with an inherent order.

rate your experience from 1−10. While this looks like count data, it's not possible to say the difference between survey ratings 10 and 9 is the same as the difference between 1 and 0

Shirt size, for example, is ordinal: small, medium, large,

Unordered (or nominal) categorical data does not have an underlying order to follow.

Yes or No responses; or Democrat or Republican party affiliation

Observational data is collected based on what's seen or heard

Experimental data is collected following the scientific method using a prescribed methodology.

also heard the phrase “found data” to reference this type of data; it's often created as byproducts from things like sales transactions, credit card payments, Twitter posts, or Facebook likes. In that sense, it's sitting in a database somewhere, waiting to be discovered and used for something

Experimental data, on the other hand, is not passively collected. It's collected deliberately and methodically to answer specific questions.

gold standard of data for statisticians and researchers

treatment group is given the drug while the control group is given a placebo

random assignment of patients should balance out information not relevant to the study (age, socioeconomic status, weight, etc.) so that two groups are as similar as possible in every way, except for the application of the treatment.

web designers frequently experiment on us by designing competing layouts or advertisements on web pages.

which ad was better with respect to click-through rates because all other potential confounding features (time of day, type of web surfer, etc.) have been balanced out through randomization.

called “A/B tests” or “A/B experiments.”

data is actually the plural version of the word datum. (Like criteria—the plural of criterion.

usage is a mass noun, like water or grass.

three most common summary statistics are mean, median, and mode,

Measures of variation—variance, range, and standard deviation—are measures of spread

As a trivial example, the numbers 7, 5, 4, 8, 4, 2, 9, 4, and 100 have mean 15.89, median 5, and mode 4.

common mistake for people to use the average (mean) to represent the midpoint of the data, which is the median

There are additional levels of continuous data, called ratio and interval. Feel free to look them up, but we rarely see the terms used in a business setting

This one chapter isn't going to replace a semester of Statistics

modern classic Thinking, Fast and Slow.

core tenet of statistical thinking is “ask questions.”

can be fun to sit back as an observer and tear apart the obvious lies.

even if you understand issues with the data, your boss probably doesn't.

There is variation in all things. How comfortable are you with this?

One type of variation stems from how data is collected or measured. This is called measurement variation

second is the randomness underlying the process itself. This is called random variation

Put simply, variation creates uncertainty.

corporate only wants 9s and 10s. 8s are as good as 0s

businesses will attempt to chase elusive high target numbers (9s and 10s in this case) without understanding that their choices in how they measured the data was the very cause of the underlying variation

illusion of quantification. It's the pursuit of driving metrics without a clear statistical foundation around what they mean.

Do you see the illusion of quantification in your workplace?

highest kidney-cancer rates in the United States, measured by the number of cases per 100,000 of population, occur in very rural counties sprawled out across the Midwest, South, and West regions of the country. Pause to think about why this might be.

here's another fact: the lowest kidney-cancer rates in the United States also occur in very rural counties sprawled out across the Midwest, South, and West—often neighboring the borders of the highest-rate counties.7 How can both be true?

It's the low population in the counties causing the high variation, simultaneously producing the highest and lowest rates.

As population increases, moving left to right in the plot, the variation starts to reduce, giving a triangular shape.

would you be surprised to learn that small schools have both the best and the worst test scores?

We often use the terms probability and statistics interchangeably, if not together, when describing the mathematics of outcomes. But here we can go a little deeper to truly understand the difference.

Imagine a big bag of marbles.

no information about what's in your hand or in the bag. Now here's the difference

probability, you find out exactly what's in the bag, and use the information to guess what's in your hand. In statistics, you open your hand and use the information to tell us what's in the bag.

Probabilities drill-down; statistics drill-up. Makes sense?

casinos know the underlying probability of your success.

Before the election, politicians and political parties only have access to a small set of random marbles (called surveys), and they pay a lot of money for that access

Errado



underestimating variation causes people to overestimate their confidence in small data.

been coined the “law of small numbers.” It's “the lingering belief … small samples are highly representative of the populations from which they are drawn.”

descriptive statistics and inferential statistics.

Descriptive statistics are the numbers that summarize data—

Descriptive statistics are a deliberate oversimplification of data—

back to the marble analogy, descriptive statistics is simply counting and summarizing the marbles in your hand.

75%, is not trustworthy based on the Biased sample.

Small sample size.

Underlying assumptions.

upcoming chapters will tell you the questions to ask to help you think statistically.

books go into more depth

importance of variation and understanding how it exists within the context of the things we measure

tomorrow's forecast is a freezing 310 Fahrenheit. The engineer tells you that cold temperatures could compromise vital components of the car's innovative prototype self-driving system

On January 28th, 1986, with the world watching, NASA launched the space shuttle Challenger from the Kennedy Space Center in Florida in freezing temperatures.

Inferential statistics exists precisely because we rarely, if ever, have all the data we need to solve a problem. We're forced to rely on samples.

only poll from voters in their political party, you have introduced sampling bias

Observational data, in particular, is susceptible to bias.

why the data exists for your use.

Not liking what an extreme value does to an analysis does not automatically mean it should be deleted. For a data point to be removed, have good business justification for removing it.

original data point and reason for dropping it should be documented and communicated, especially if the results changed substantially.

16 out of the 23 data points from shuttle flights were missing in the Challenger story

How Did You Deal with Missing Values? Missing values are literal holes in a dataset.

Your job is to predict if these applicants will be late on payments in the next year. Several applicants, however, do not enter their income. So, the system stores it as a blank—a missing value.

go back to the data's origin story. The story starts with applicants applying for a credit card

Data, by way of encoding information, enables us to get closer to these answers, but by and large the data we use is truly proxy—a stand in, as it were—for the thing we're trying to measure.

if the data has bias, additional data can't save you.

Don't think a dataset is too big to argue with.

Statistics deals in the tradeoffs between what you ultimately want to know with the data you have

Stakeholders typically see a polished PowerPoint presentation that follows a rigid script from question to data to answer.

decisions and assumptions the data team made along the way to arrive at their answer.

exploratory data analysis (EDA). It was formulated by statistician John Tukey in the 1970s as a way to make sense of data with summary statistics and visualizations before applying more complex methods.

Two teams, given the same problem and data, might take separate analysis paths, possibly landing on the same conclusion. Possibly not

in this chapter, we present EDA as an ongoing process that is every Data Head's responsibility, whether you're the hands-on data worker or the business leader in the boardroom.

we'll walk you through a quick scenario against the backdrop of a popular dataset compiled for educational purposes: the Ames Housing Data.4 This is a glimpse into an EDA process.

your company needs its own prediction tool.

80 columns describing several aspects of hundreds of residential homes that were sold in Ames, Iowa from 2006 to 2011

data passes an initial sniff test.

anomalies, outliers, and missing values. How you deal with these matters.

summary statistics can help steer you toward interesting patterns and relationships in

statistic correlation, which is suggestive (but not proof) of a relationship between two numeric variables.

popular dataset called Anscombe's Quartet,8 four datasets with identical summary statistics but clearly different visualizations

five groups of linearly correlated data in fact, but when viewed as a single group, it's not linearly correlated at all. This is known as Simpson's Paradox, a topic you'll learn more about in Chapter 13.

Datasaurus: Data is free to download and explore.9 Like Anscombe’s Quartet, both datasets shown here have identical summary statistics.

Lembrar de frekonomics..piscin e armas...borto e criminalidade

correlation does not prove causation:

temperature in the ice cream example, age in the shoe size example—

true causal factor

skeptical of studies linking tobacco use to cancer.

skeptical of studies linking tobacco use to cancer.

opportunities in the data; problems that might be valuable to your organization.

new problems

you can be a part of the EDA process from beginning to end.

If you come into a project near the end, ask why the data team chose the analysis they did and what challenges they faced.

To recap, there's variation in all things; variation creates uncertainty; and probability and statistics are tools to help us manage uncertainty.

focus on what you need to know to keep your intuition sharp and be successful in your work.

most people don't have a grasp of, or respect for, probability. Want proof? People still buy scratch-off lottery tickets, flock to Las Vegas, and buy the extended warranty on their television.

some outcomes are more likely than others.

two people might have different perceptions of how often a “highly probable” or “likely” event occurs—which means everyday language isn't going to cut it.

shorted to P(C == H) = 1/2. Or, even shorter, P(H) = 1/2

we say P(C == H) instead of P(C = H). The reason we do this is to differentiate between the two sets of equals in our equation. When we write ==, we're effectively testing what the coin flip result, C, equals.

When modeling the probability of multiple events occurring, the notation and rules depend on how the multiple events occur—whether two events occur together (it floods and the power goes out), or whether one event or another occurs (either it floods or the power goes out).

flipping a heads and drawing a spade can be denoted P(H, S), with the comma representing “and.” In this case, the events are independent.

Let's assume the probability Alex is late given Jordan is late is 20%, which we write as P(A | J) = 20%

true formula for two events happening at the same time, called the multiplicative rule. It can be written as P(A, J) = P(J) × P(A | J) = 10% × 20% = 2%

the intersection, or overlap, of the circles (events) A and J can never be larger than the smallest circle.

What about one event or some other event occurring at the same time? As with all lessons in statistics and probability, it depends. Start with a guess and adjust with the evidence provided.

rebranding of the popular Linda problem in the book, Thinking, Fast and Slow4, and it's a problem most people get wrong. How did you do

chance of any two events happening together can't be greater than either event happening by itself.

probability of a person being a Yankees fan and attending the game is vastly different from the probability of a person being a Yankees fan given they are at the game.

intuition can play tricks on you. Probabilities will continue to confound and confuse.

events A, B, and C are dependent on several factors.

wrongfully assuming independence, they are underestimating the probability all projects will fail next year,

gamblers falsely believe the probabilities change—hence, the name Gambler's fallacy.

Every roll of the dice is independent of the previous roll,

maybe the casino will give them a “free” breakfast buffet.7

assuming P(A | B) = P(B | A) is an error so common it was given a name and a Wikipedia article—Confusion of the Inverse.

probabilities P(V | +) and P(+ | V) are not the same, but they are linked through one of the most famous theorems in all of probability and statistics—Bayes' theorem.

The probability of event A given event B is related to the probability of event B given event A. They are not equal (that's the “confusion of the inverse”) but related by the preceding equation.

challenging news, is that the actual calculation of some of the pieces in Bayes' theorem can be a pain

“Calibration measures whether, over the long run, events occur about as often as you say they're going to occur.

rare events are not impossible and highly probable events are not guarantees.

In a world with 7.8 billion people, a “1 in a million” daily event would happen to 7,800 people per day

Don't needlessly multiply probabilities of past events. You can make anything seem overly improbable

We're going to teach you about statistical inference, how to use inferential statistics, how to challenge their results, and we'll give you the questions you need to ask to fully understand the underlying inferences being made.

we'll walk you through a series of short examples to show how intuitive statistical inference can be, while gradually adding in formal statistical language

Polling data is a common and important example of inferential statistics. You can't survey everyone—you can only poll those in the sample of people you have access to

sample helps us understand the population.

if you ran this poll many more times, you would get different answers. That's sampling variation.

Polling agencies recognize this and place a “margin of error” around the polling results, about +/− 3%, which attempts to capture this fuzziness

interval (62.5%, 68.5%) is called a confidence interval and is an example of an inferential statistic.

Fundamentally, science and the creation of new knowledge is about challenging the status quo.

simplest analogy is the American judicial system. Defendants are “innocent until proven guilty” (the status quo),

status quo is called the null hypothesis, commonly written as H0, and this is generally chosen with the hope of throwing it out in favor of new knowledge called the alternative hypothesis, written as Ha.

hypothesis testing is the hallmark of scientific experimentation.

If enough evidence (data) shows the null assumption is unlikely, reject it in favor of new knowledge in the alternative hypothesis.

probability of seeing this specific result—10 missed shots—given that he can supposedly make 50% of his shots, is 1 in 1,000. This probability, 1 in 1,000 or 0.001, is called a p-value (p for probability).

What was your cutoff for the missed number of shots to reject the null hypothesis?

let's say your cutoff was at 5 missed shots. If the intern had only missed 4 in a row, which has probability 50%4 = 6.25%, or 1-in-16, you could have given him the benefit of the doubt.

That cutoff, 5 missed shots in a row, surpassed what is called the significance level. The data was no longer consistent with the claim.

significance level is an artificial threshold, decided upon by you, in which you can tolerate randomness and unexplained variation but still feel the null hypothesis is true.

testing whether a p-value was less than a significance level to reject a null hypothesis is a key part of statistical inference.

two types of decision errors, both given the nondescript names: Type I (false positive) and Type II (false negative) errors.

higher the power of a test, the lower the probability of a false negative.

Related to statistical significance is something called power, the probability of correctly rejecting the null hypothesis when the alternative hypothesis is true.

False positive and false negative errors have inherent tradeoffs, and—unless you collect more data—you cannot decrease one without increasing the other.

null hypothesis here is “the email is not spam,” so a false positive would mean an email from your mother is in the spam folder.

This comes with the price of more spam emails in your inbox (more false negatives), but you can tolerate that if you get most of your personal email.

In short, statistical inference follows these steps:

statistical test. These are mechanisms that calculate the p-values.

we recognize that Data Heads will often be the consumers of statistical results rather than the creators of them.

in the next section, we're going to teach you the questions you should ask to challenge the statistics you see.

following list of questions and prompts to ask your teammates to help you confidently challenge the statistics presented to you:

If you hear, “Sales are up 10%!” your brain should reflexively think, “Compared to what?”

Don't be afraid to speak up and ask, “What is the context for these statistics?”

When N is small, you usually see a lot of variation. No problem—you'll just add more data to the pile.

book Doing Data Science: Straight Talk from the Frontlines:

What Is the Sample Size?

What Is the Context for These Statistics?

What Are You Testing?

What Is the Null Hypothesis?

“What is the null hypothesis?” A poorly defined null can create the deception where something is right simply because no data exists to show it's wrong.

science is about challenging the status quo.

Assuming Equivalence

What Is the Significance Level?

(CERN), researchers used an incredibly small significance level when testing for the tiny physics particle known as the Higgs boson.

smaller the chance of a false positive.

proper balance depends on your problem and your ability to absorb the impacts of false negative and false positive errors.

If the entire population responds, a confidence interval isn't needed—you've found the true population number.

If you are only seeing p-values and not confidence intervals, you might think you've found a large effect, when what you really detected was a minor difference that has no practical value.

how you would organize such a collection. You could start with some obvious categories. For instance, music is often organized into genres

powerful technique used in a variety of fields, from segmenting customers into different marketing groups, to organizing music on Spotify or Pandora, and organizing the photos on your phone

As a Data Head, you must be able to navigate across the many unsupervised learning methods in your search for hidden groups in data.

reduces the three-dimensional world down to a flat, two-dimensional photo you can carry in your pocket.

looking for hidden groups in the columns of a dataset so that we can combine multiple columns into one.

bioinformatics, for example, the potential dimension of a dataset can be enormous. Researchers may have thousands of gene expressions for each observation, many of which are highly correlated (and thus possibly redundant) with each other.

combine multiple columns into a composite feature

this new dimension lets us ignore the three original dimensions. That's dimensionality reduction.

created a new dimension of the data (efficiency) by combining

more features are condensed into a single “efficiency” dimension.

Principal component analysis (PCA) is a dimensionality reduction method invented in 1901,5 long before the terms data scientist and machine learning became part of business terminology.

Through some clever math, it layers the dimensions in different configurations, looking for which linear combinations of features spreads the data out the most.

principal components represent new dimensions in the data that are not correlated with each other.

Your boss gave you the vague task to “summarize the data,” but you're bogged down by the sheer number of columns in the spreadsheet.

suspect, since several groups of these features are correlated with each other, there might be a way to condense them into fewer dimensions that are no longer correlated with each other but contain as much information as possible from the original data.

435 separate scatterplots to view each pair of features.6) So, you run the data through the PCA algorithm to exploit the embedded correlations in the dataset for you

dataset in Figure 8.4 can explain 91% of that information in only 4 features. Therefore, we can decide to safely ignore 26 columns. That's dimensionality reduction!

No variation = no information

core idea behind PCA is to take all the variance—all the information—available in a dataset (a high number of columns) and condense as much of that information into as few distinct dimensions as possible

could take a picture of the Great Pyramids of Egypt from countless angles, but some angles are more descriptive than others. Take a photo overhead with a drone, the pyramids appear as squares. Take a photo directly in front, they look like triangles. Which rotation of the camera would capture the most information to impress your friends when you condense the 3D world in Giza down to a 2D photo on your smart phone

PCA finds the best rotation.

not accept immediate definitions for your principal components.

if you see results from PCA, ask how they decided how many components to keep.

feature can have high variance and still have little practical importance.

Groups of features (columns) might tell one story, like with PCA, but groups of observations (rows) might tell a different story. This is where clustering comes in.

you've established the obvious: you need between 1 and N groups.

you see what you want to see. It depends on which features matter most to you and your background and how you internally measure the concept of “close

company wants to assign its 200 retail locations, shown in Figure 8.6, into six regions across the continental United States.

cluster itself into six regions with k-means. The dataset has 200 rows and two columns: latitude and longitude.

this center point is essentially the average of every member in the group (that's the means of k-means)

algorithm selects six random locations to serve as potential regional offices. Why random? Well, it must start somewhere.

points on our map (often described as, “as the crow flies”

all points within a cluster are averaged together to create a center point (called a “centroid”)

With this insight, the company has clustered its 200 stores into six regions and identified possible locations within each cluster to serve as regional offices.

If the data isn't scaled appropriately, the income variable would dominate most distance formulas, an easy one being the difference (in absolute value) between any two data points.

ability to group data in any specific way is a product of the algorithm chosen, how it's implemented, the quality of the underlying data, and variation in the data.

When the output is a number, the supervised learning model is called a regression model

When the output is a label (aka categorical variable), the model is called a classification model.

spam detector in your email, your home or apartment's estimated value, speech translation, facial detection applications, and self-driving cars—these all use supervised learning.

classic method created around 1800 called linear regression. Linear regression, specifically least squares regression

Linear regression employs a computational method to produce the line of best fit.

need to understand the difference between what our model predicted and what actually happened. These differences are called errors—and they represent how far off our prediction

square the differences from our prediction to make everything positive.

data fed into the algorithm is a sample, and thus you must continue to think statistically about the results.

if the coefficient is not statistically different than zero, you can drop that feature from your model. The input is not impacting

believe us when we say omitted variables can and will cause headaches and misinterpretations.

Multicollinearity is present in most observational datasets, so consider this a fair warning.

features about the home (size, number of bedrooms, etc.), but also the initial offer made on the house.

Data leakage10 happens when a concurrent output variable masquerades as an input variable.

Statistics department at Procter & Gamble would offer this advice: “Don't fit a straight line through a banana.

stock market. Historically, it has grown exponentially, not linearly.

great care must be taken to avoid multicollinearity and omitted variables to ensure model explanations are possible.

Plot them in a scatter plot! These should be well correlated. This eye-ball test will let you know quickly how well your model has done.

Always, always demand to see the actual vs. predicted plot.

variants of linear regression called LASSO and Ridge Regression that help when there are many correlated inputs (multicollinearity)

more input variables than rows in your dataset.

field of Statistics called Design of Experiments

depth about the difference between explaining and prediction for models: Shmueli, G. (2010). To explain or to predict? Statistical science, 25(3), 289–310.

science likes to test for things in the affirmative. As a result, you should construe positive and negative as meaning “do” and “does not,” respectively.

ensemble methods, which are becoming a new standard for data workers, especially in data science competitions

your company has a stockpile of historical data to learn from—information about each applicant and a yes/no label to indicate if they were invited for an interview. With historical data and a classification model like logistic regression, you could develop a predictive model

probability of an applicant being offered an interview based on their GPA

this equation, called the logistic function (hence the name logistic regression)

resulting number is a probability.

Logistic loss is simply a way of measuring how close the predicted probabilities are to the actual labels.

impact on probability of an extra GPA point is not constant in logistic regression models.

If you want to automate a decision with logistic regression, you'll need to set a cutoff, also called a decision rule.

then it finds the next feature that helps separate those two groups at a more granular level, and on and on.

decision tree algorithm known as CART6 and generated the decision tree in Figure 10.3

overfit tree would be very confidently telling you how to make potentially wrong decisions.

One way to fix this is through “pruning,” but lone trees remain very sensitive to their training data.

Ensemble methods, so named because they represent the aggregation of different results by running an algorithm dozens, perhaps even thousands, of times are popular among data scientists because of their ability to make meaningful predictions at a granular level.

random forests and gradient boosted trees, have emerged as data scientists’ favorites.

often used by the winning teams in data science competitions on the website Kaggle.com

gradient boosted trees build trees sequentially.

start by building what's called a “shallow” tree—a tree with few branches and nodes

Generally, these ensemble methods are not for “small data,” so data workers should apply them when they have hundreds, not dozens, of observations.

Most classification models don't output a label—they output a probability of belonging to the positive class.

Do not take this decision cutoff lightly. A model that predicts if someone should receive a credit card offer in the mail might have a low cutoff

you must know how to evaluate and judge these models.

let's say someone on your team applies XGBoost (a type of gradient boosted trees algorithm) on 80% of the data (training set), and the classification model predicts correct results 60% of the time on the remaining 20% (test set)

it's better than 50/50—you might think,

In fact, however, it indicates the features in your dataset have no relationship to the output.

If, for instance, 99.5% of people don't click the ad, then simply defaulting to the prediction that no one will ever click the ad will be correct 99.5% of the time

True Negative Rate (“Specificity”) =

True Positive Rate (aka “Sensitivity” or “Recall”

higher cutoff is perfect at denying applicants who should not be accepted, but this comes at a cost

Text analytic technologies, while able to solve huge, difficult problems like voice-to-text and speech translation often fail at tasks that seem much easier.

simply, text analytics is harder than you might realize.

There are several ways to do it, and we'll cover three

most basic approach to convert text into numbers is by creating a “bag of words” model.

What you read as: “This sentence is a big bag of words” is converted into a set, called a document, where each word is an identifier, and the count of the word is a feature.

Each identifier is referred to as a token. The entire set of tokens from all documents is called a dictionary.

word clouds make great marketing material, but we're not fans and we do not recommend them.

standard practice to remove common filler words—like the, of, a, is, an, this, etc.—that don't add meaning or differentiation between sentences. These are called stop words.

stem words

lowercase,

remove punctuation and numbers,

lemmatization,

FIGURE 11.2 Processing text down to a bag of words

bag-of-words throws context and word order aside

N-gram is a sequence of N consecutive words

add the bigram tokens to the bag-of-words, which further increases the size and sparseness of the document-term matrix.

Websites like Tripadvisor.com take advantage of these approaches and give users the ability to quickly search reviews for frequently mentioned words or phrases.

In 2013, Google analyzed billions of word pairs (two words within close proximity of each other within a sentence) in its enormous database of Google News articles.

they were able to generate what are called word embeddings

math would represent each word as being similar in an element of the vector associated with things described as

probabilities that the other words in the dictionary appeared near the input word. So for input cow, the associated output might be (0.3, 0, 0, 0.5, 0.1, 0.1, 0, 0)

model tries to map the inputs (word vectors) as close as possible to the outputs (vectors with probabilities).

word embeddings. Think of them as a numeric representation of a word that encodes its “meaning.

contain meaning behind the words, similar in a way to how the reduced dimensions in PCA captured themes of features.

As an exercise, convince yourself (using Table 11.3) that Beef – Cow + Pig ≈ Pork.

This technique is called Word2vec9 (word to vector) and the word embeddings Google generated for us are freely available to download.

applications in search engines and recommendation systems, but the word embeddings generated from Google News text might not be specific to your problem set.

satisfying payoff to this investment of converting unstructured text data into a structured dataset with rows and columns of numbers.

Unleashing a clustering algorithm like k-means on a document-term matrix, like in Tables 11.1 and 11.2, would produce a set of k distinct groups of text that are similar in some way.

there are two general topics being discussed here: national defense and space.

By filtering the text, you've effectively defined one topic for the articles that remain.

With text, we're usually trying to predict a categorical variable, so this falls under the classification models you learned last chapter, as opposed to regression models that predict numbers.

There's a reason your email provider asks you if your email is spam or not. You are providing the training data for machine learning algorithms!

There are more columns than rows in Table 11.4, and logistic regression doesn't like that.14

Naïve Bayes (named after the very same Bayes we mentioned in Chapter 6). The intuition behind it is straightforward: are the words in the email subject line more likely to appear in a spam email or a non-spam email?

decision to classify a new email as spam comes down to figuring out which value is higher:

But there's a slight problem. New and rare words require some adjustments to calculations to avoid multiplying the probabilities by zero

To fix this, let's pretend we've seen each word at least once by adding 1 to the frequency of each word.

also add 2 to the frequency of the spam (and not spam) to prevent values from reaching 1.16

If you search Google for “sentiment analysis of Twitter data,” you might be surprised by the number of results; it seems everyone is doing it.

Tree-based methods like random forests and boosting can be applied to text classification problems and tend to perform better than Naïve Bayes on some datasets,

text analytics project is fun to present to stakeholders

not a series of numbers, but something they can read,

tempted to show the exciting examples and the easy wins, rather than the clear misses. Data Heads, if presenting text analytic results, should be transparent with outcomes.

if you are consuming results, request to see examples where the algorithms went wrong. Trust us, they exist.

some big tech companies have seemed to rise above those challenges and have emerged as leaders in text analytics and Natural Language Processing (NLP)

Here's what big tech companies like Facebook, Apple, Amazon, Google, and Microsoft have that many other companies don't have: an abundance of text and voice data (an abundance of labeled data that

get the idea how NLP is often a case of the haves vs. the have nots. Most companies, to be blunt, aren't there (yet?

Even though the algorithms are open source, the massive collection of data and access to supercomputers is not. Big tech clearly has the advantage.

sentiment of the sentence “Samsung is better than an iPhone” depends on whether you work for Apple or Samsung.

set your expectations accordingly based on the amount of data and resources you have.

If deep learning is the steam engine of this revolution, then data is its coal:

This chapter, in many ways, serves as the climax of your Data Head journey

Deep learning comprises the group of technologies that drive facial recognition, autonomous driving, cancer detection, and speech translation.

In this chapter, we'll reveal the components of deep learning

At its core, deep learning uses a family of models called artificial neural networks.

At a certain point—and not exactly at a point we truly understand—the information causes a neuron to “fire” or react

original neural networks were created in the 1940s and were designed to mimic human biology as it was understood at the time.

success of these algorithms stems from faster computers, piles of data, and a wave of research in machine learning,

now see how neural networks work by walking through two examples.

neuron, represented as a circle in our figure. Inside this neuron is an activation function.

biological motivation being, if some combination of the inputs surpasses a threshold, the neuron will “fire” and predict the applicant should get an offer.

—our activation function is designed to produce the probability of an offer, just like we did in Chapter 10 using logistic regression

—our activation function is designed to produce the probability of an offer, just like we did in Chapter 10 using logistic regression

The linear regression-line equation in 12.2 allows us to combine the four inputs into one, and the logistic function in 12.1 squishes the result to be between 0 and 1, the range where probabilities must lie.

at the start of the training process, the parameters could really be anything.

tap did not have clear indications for hot and cold—you would just turn it on and test the temp. You'd modulate from there. Same thing here.

tap did not have clear indications for hot and cold—you would just turn it on and test the temp. You'd modulate from there. Same thing here.

this case, both Will and Allie received offers. Their true output values were 1, but the model predicted low values for each. So to start, the neural network is a terrible predicter.

model looks at the true values of the outputs (1 and 1) and sends a message that the current parameters are wrong; adjust them.

algorithm called backpropagation5 adjusts these weights and decides to increase or decrease them and by how much:

real benefit of neural networks, lies in what happens when you add “hidden” layers into the network.

neuron “fire” a signal that represents a new feature within the data. We might call this feature achievement

From the computational view, the network can be thought of as a series of logistic regression models in each neuron.

creates equations within equations—a nesting Russian matryoshka doll in math form.

it will get even more complicated as you add more layers and neurons. Sometimes these models are described as black

get even more complicated as you add more layers and neurons. Sometimes these models are described as black boxes because of how little they make sense when they are layers and neurons deep

More realistically, neural networks are large math equations, typically used for supervised learning tasks (classification or regression), that can find new representations of the input data to make predictions easier

Deep learning is the family of algorithms using the artificial neural network structure with two or more hidden layers.

stack hidden layer upon hidden layer, where the outputs of one layer become the inputs to the next

At each layer, new abstractions and representations of the data are realized, effectively creating increasingly subtle features from the input dataset.

Yann LeCun

State-of-the-art computational power, a large labeled dataset, and patience would prove to be the formula for deep learning's success

the 2010s, the confluence of big datasets (thanks to the Internet), algorithmic improvements (like better activation functions than the logistic function), and computer hardware known as graphical-processing units (GPUs) started a revolution in deep learning.

neurons can generate new and subtle representations of a dataset, model interactions, and non-linear relationships, thereby finding nuance other methods might miss

reduces the time for manual feature engineering.

process of combining or transforming the raw data into new features (new columns) in a dataset using subject matter expertise.

From a practical matter, of course, there's a ceiling—every dataset has a limit

performs well on problems of perception.

get a preview to how deep learning works in the field of computer vision.

convolutional neural networks, which are used by researchers to build image classification systems on larger images (more pixels) and those with color.

Convolution is the mathematical equivalent of analyzing a picture with a series of magnifying glasses, each with a different purpose.

notice many localized patterns: lines, corners, rounded edges, textures, and so on (see Figure 12.7).

find the most distinctive features.

filter out information irrelevant to the target output

searches” for similar features across images.

reduces the number of values that go into the familiar neural network structure

features in images not only have to be analyzed, but located.

social media can find your face in a picture no matter where you're hiding

social media can find your face in a picture no matter where you're hiding. Deep Learning on Language

This is why social media can find your face in a picture no matter where you're hiding

your brain held on to past information while processing new

Google's “Smart Compose” in Gmail since 2018; it suggests text to finish your ______, and it's powered by recurrent neural networks.

hard not to be excited about deep learning. We're only scraping the surface of its potential.

many businesses want to rush to try deep learning without having enough labeled data for their specific application

major challenge to taking advantage of AI throughout the economy is the sheer amount of customization needed.

each of those models would require their own, likely large, set of labeled images.

idea of transfer learning is to download a model that's been trained to identify everyday items (balloons, cats, dogs, etc.)

transfer learning may reduce the number of labeled images by a factor of 10, but it won't bring it down to dozens.

With structured data, deep neural networks often lose to tree-based methods (from Chapter 10). There are exceptions, no doubt

decisions to be made. For instance: How many layers should the network have? How many neurons in each layer? Which activation functions should you use

when building a large network, be careful not to overfit your data

Chollet, F. (2018). Deep learning with Python. New York: Manning

two types of artificial intelligence

first is artificial general intelligence (AGI), the idea of complete human cognition. Insert your favorite science fiction movie reference here. But rest easy, little progress is being made in AGI

Significant progress, however, is being made in artificial narrow intelligence (ANI): computer systems that do one thing well, like facial detection or speech translation or fraud detection.

when vendors come to pitch you on AI—we're all really talking about machine learning. And

involves perceptual, unstructured data, they are talking about deep learning

Machine learning is a subset of AI, and deep learning is a subset of machine learning (see Figure 12.9

AI is reinforcing patterns from data collected in the past. It's not about creating something resembling human consciousness.

if you are wondering how your company can begin to find value with deep learning—or more broadly with machine learning—getting labeled data would be the first step.

you can pay pennies on the dollar to have people label your data for you.

Data is growing faster than our ability to articulate the problems it creates.

Hackers, for instance, have used a type of deep learning called Generative Adversarial Networks (GANs) to create “deep fakes” of people's faces.

we should be careful about what human evaluations we attempt to replace with deep learning.

often what we are modeling aren't just data points—they're people.

Ask not just to see the data and algorithms—but ask who does this result affect? Am I OK with that?

Do not take for granted your own role in using data to make outcomes better for business and society.

Remember, deep learning is built on top of artificial neural networks, artificial neural networks are made up of neurons, and each neuron comprises an equation called the activation function.

mathematical equation, which serves as a predictive model

—essentially a linear regression model. 4 Weights are also called coefficients. There are multiple names for the same concepts. 5 For

pitfalls you've learned about and introduce you to a handful of other common pitfalls that, if you're not careful, can derail your work or (worse) convince you of something that isn't so

take a moment to acknowledge that it's easy to complain about others’ mistakes.

We understand bias as the lopsided (and sometimes even inconsistent) favorability given to ideas and concepts by individuals and reinforced in groups

Survivorship Bias Suppose an investment company launches dozens of mutual funds the same year

survivors—remain, with an impressive return to boot.

survivorship bias, the “logical error of concentrating on people or things that made it past some selection process and overlooking those that did not, typically because of their lack of visibility

they were learning from the planes that returned. But what about those that did not? What does the damage pattern say about them?

recommendation: armor the sections where the returned planes had the least damage. Why? Because planes hit in those areas never made it home.

Regression to the Mean

classic example of survivorship bias is that of statistician Abraham Wald

regression towards mediocracy” in 1886 by Sir Francis Galton

natural, underlying stability in the height of humans and their offspring.

the “Madden Curse.”3 But we know it as regression to the mean

Don't put faith in outliers. Luck—good or bad—won't last forever.

Simpson's Paradox

Simpson's Paradox happens when a trend or association between variables is reversed after the addition of a third variable.

avoid two data mistakes: thinking correlation is causation and having the wrong correlation

new, minimally evasive procedure for kidney stone removal had a higher success rate (83%) than the traditional procedure (78%)

result is reversed when broken out into kidney stone size

split observations into each treatment group to avoid any confounding.

Confirmation Bias

interpreted in a way that confirms one's already held beliefs, while conflicting evidence that doesn't align with prior beliefs is cast aside as moot.

For these teams, at least some of the data work exists to feed the confirmation bias machine.

Effort Bias (aka the “Sunk Cost Fallacy

Some companies would rather you deliver something, anything—given the time, effort, and attention already paid.

fertile ground upon which many of the biases listed previously are formed.

Algorithmic Bias

not just that algorithmic bias can happen anywhere, however good (or neutral) your intentions. It is already happening.

two categories: (1) statistical and machine learning pitfalls and (2) project pitfalls.

Thinking correlation is causation:

p-hacking: Suppose an article proclaims, “People who drink too much coffee have an increased risk of stomach cancer. The result is statistically significant at the 0.05 significance level

-hacking is the process of testing multiple patterns in data until you spot a statistically significant p-value

p-hacking is the process of testing multiple patterns in data until you spot a statistically significant p-value

-hacking is a type of survivorship bias, as only the significant p-values are reported.

p-hacking is a type of survivorship bias, as only the significant p-values are reported.

non-representative sample:

basing decisions on a sample of data that does not represent the population it will influence can lead to serious errors.

Data leakage: Do not train a model on data that will not be available at prediction time

Overfitting: Recall that models are simplified versions of reality.

Data Heads can prevent overfitting by splitting the data into training and test sets.

Non-representative training data: This

model that learns from real estate data in Ohio to predict the sales price of homes in Ohio cannot predict the rental price of an apartment in New York City.

Data Heads must think carefully about the circumstances in which their model will be used and collect training data

Data Heads must think carefully about the circumstances in which their model will be used and collect training data to reflect those applications.

Not asking a sharp question (or solving the wrong problem)

ambiguities can cause misalignment

Not adapting the question once it's already failed:

Data is owned, not governed (i.e., data is hard to acquire)

Data does not contain the information needed

Not relying on inexpensive and open source technologies:

prototype it first.

wouldn't it make sense to build a minimum viable prototype (MVP)

Timeline is overly optimistic:

aggressive timelines lead to shortcuts and bad analysis.

Inflated expectations of value:

Be transparent with the value your project can bring, but don't oversell it

Expecting to predict the unpredictable:

Documenting every spin of every roulette wheel in Vegas won't help you predict the next spin.

Data science, statistics, machine learning, and AI can solve many important problems in the world, but they can't solve every problem.

sometimes, we already know and operate on a set of rules

Machine learning sounds compelling to management, but sometimes, it's just overkill.

Projects fail all the time. And chances are, you will have at least one (but, most likely, more) project fail that you are associated with.

In this chapter, we'll talk about the people and perceptions of roles when working with data,

It's a lack of communication that drives many of the project failures described in this book

TABLE 14.1 Seven Scenes of Communication Breakdown

statistician R.A. Fisher's quote, “To call in the statistician after the experiment is done may be no more than asking him to perform a post-mortem examination:

“You have to speak to them like they're in fifth grade,” says the manager. She reluctantly obliges, even though she knows there will be scientists in the audience.

while the stakeholders certainly think the work sounds impressive, they leave the room without clear direction on what do to next.

couldn't be presented in a way that could be understood, the project wasn't actually done yet.

Rather than viewing themselves as part of the team, they see themselves as the savior-consultant who will save the company by bringing them

Rather than viewing themselves as part of the team, they see themselves as the savior-consultant who will save the company by bringing them into the data space.

his argumentative style masks an underlying analysis paralysis.

enamored with the hype. To them, every new thing is awesome.

enamored with the hype. To them, every new thing is awesome. In their thinking, data can solve every problem.

By encouraging a healthy skepticism of data, you can help them become Data Heads

When they don't like results, cynics poke holes—belaboring details that go beyond constructive criticism.

At their core, Data Heads are skeptics. They aren't skeptical to be annoying.

Becoming a Data Head starts with listening to the entire team.

this chapter, we reviewed seven scenes that come about as different project personalities interact

what Data Heads can do to create an environment within their organizations that fosters a better understanding of data.

Data Head is someone who: Thinks statistically

data literate—speaks intelligently and asks the right questions about the statistics

To be an effective Data Head, you'll need to become a person who uses data to drive change within your organization

regular meetups or lunch-and-learns to dive deeper into the topics we've discussed and learn about those we didn't cover.

Data Head working group at your company.

share your knowledge and help others.

companies and employees relied on events to help support their learning

much of your learning is going to have to happen off the job (versus on the job)

books like this, online learning, and certificates

You must continue learning and be accountable for its trajectory.

At the start of the book, we offered a series of data disasters that took place when organizations were not thinking like Data Heads. As the presence of data grows, the risk for such errors increases.