---
title: 'Chapter 2: Dealing with qualitative perception'
description: This chapter deals with categorical variables. We introduce the notions of bar plot, of contingency table, of independence.
prev: /chapter1
next: /chapter3
type: chapter
id: 2
---

<style>
.accordion > input[type="checkbox"] {
  position: absolute;
  left: -100vw;
}
.accordion .content {
  overflow-y: hidden;
  height: 0;
  transition: height 0.3s ease;
}
.accordion > input[type="checkbox"]:checked ~ .content {
  height: auto;
  overflow: visible;
}
.accordion label {
  display: block;
}
body {
  font: 16px/1.5em "Overpass", "Open Sans", Helvetica, sans-serif;
  color: #333;
  font-weight: 300;
  
}
.accordion {
  margin-bottom: 1em;
}
.accordion > input[type="checkbox"]:checked ~ .content {
  padding: 15px;
  border: 1px solid #e8e8e8;
  border-top: 0;
}
.accordion .handle {
  margin: 0;
  font-size: 1.0em;
  line-height: 1.2em;
}
.accordion label {
  color: #FFFDF9;
  cursor: pointer;
  font-weight: normal;
  padding: 15px;
  background:#61B4DD;
  border-radius:15px;
}
.accordion label:hover,
.accordion label:focus {
  background: #4E92B2;
}


body {
  padding: 40px;
}
a {
  color: #06c;
}
p {
  margin: 0 0 1em;
}
h1 {
  margin: 0 0 1.5em;
  font-weight: 600;
  font-size: 1.5em;
}
.accordion {
  max-width: 65em;
}
.accordion p:last-child {
  margin-bottom: 0;
}
hr
{
border:solid 1px black;
width: 96%;
color: #FFFF00;
height: 1px;
}
</style>

<exercise id="1" title="From classes to categories and vice-versa">

By definition, a class is a set or category of things having some property or attribute in common. In the same way, a category is a class of people or things regarded as having particular shared characteristics. 

In this chapter, the notion of categories is first introduced using a survey in which 135 participants were asked about their perception of genetically modified organisms (GMO):

* Do you feel implicated in the debate about GMO (a lot, to a certain extent, a little, not at all)?

* What is your view of GMO cultivation in France (very favourable, favourable, somewhat against, totally opposed)?

* What do you think of the inclusion of GM raw materials in products for human consumption (very favourable, favourable, somewhat against, totally opposed)?

* What do you think of the inclusion of GM raw materials in products to be fed to animals (very favourable, favourable, somewhat against, totally opposed)?

* Have you ever taken part in an anti-GMO protest (Yes/No)?

* Do you think the media communicate enough information about GMO (Yes/No)?

* Do you take it upon yourself to find out more information about GMO (Yes/No)?

* Do you think that GMO might enable us to reduce the use of fungicides (Yes/No)?

* Do you think that GMO might enable us to reduce the problems of hunger in the world (Yes/No)?

* Do you think that the use of GMO might help to improve farmers' lives (Yes/No)?

* Do you think that GMO might lead to future scientific advances (Yes/No)?

* Do you think that GMO represent a danger to our health (Yes/No)?

* Do you think that GMO represent a possible danger to the environment (Yes/No)?

* Do you think that GMO represent a financial risk for farmers (Yes/No)?

* Do you think that GMO are a useless scientific practice (Yes/No)?

* Do you think our grandparents' generation had a healthier diet than us (Yes/No)?

The same people were also asked about the five following descriptive variables:

* Sex (male, female)

* Professional status (farmer, student, manual labourer, senior management, civil servant, accredited professional, technician, retailer, other profession, unemployed, retired)

* Age (--25 years, 25--40 years, 40--60 years, +60 years)

* Is your profession or education in any way linked to agriculture, the food industry or the pharmaceutical industry (Yes/No)?

* Which political movement do you most adhere to (extreme left, green, left, liberal, right, extreme right)?

Intuitively, it is easy to understand that each question, individually, defines categories of participants through the response modalities they have chosen.

Let's now have a look at our data. Import the data in an R object named *GMO*, then apply the `summary()` function to the *GMO* object.

<codeblock id="02_01">
</codeblock>

As shown above, data are considered as *characters* and should be encoded as factors.
Apply the `ncol()` function to *GMO* to get its number of columns. Use this information to encode the columns as factors, iteratively; then, check that the *GMO* data frame is ready to be analyzed.

<codeblock id="02_02">
ncol(GMO) returns the number of columns of GMO
</codeblock>

The output of the `summary()` function is interesting: it illustrates perfectly the notion of class or category. For the question *"What do you think of the inclusion of GM raw materials in products to be fed to animals?"*, we can see that the 135 participants of the survey are divided into 4 classes or categories: 44 are totally opposed, 39 are somewhat against, 44 are favourable, and 8 are very favourable.

</exercise>

<exercise id="2" title="From categories to categorical data and their representation">

As explained previously, for a given question, the different *response modalities* define classes or categories of participants. Practically, we want to represent the way these participants are distributed into these classes. The graphical representation of a categorical variable is often done through a bar plot: one bar per category with a height proportional to the numeric value associated with the category.

Let's have a look at the *Position.H.Food* variable, and let's represent its distribution. To do so, extract the distribution information with the `summary()` function and visualize it with the `barplot()` function.

<codeblock id="02_031">
</codeblock>

By default, the levels of a categorical are sorted in an alphabetical order. In our case, the *Position.H.Food* variable is an *ordered categorical variable*, a categorical variable with a quantitative dimension that can be ordered. For a better understanding of the data, this relation order between the categories should be kept.

To do so, we are using the `c()` function to temporarily re-order the levels.

<codeblock id="02_031b">
</codeblock>

## The *R* corner: when categories have to be *re-ordered*
<br>

There's a trick for re-ordering the levels of a categorical variable. 

Check the levels of the categorical variable *Position.Culture*. Re-order these levels in a more *natural* way, by using the `factor()` function, combined with the `levels()` function. Check again the levels of the variable *Position.Culture*

<codeblock id="02_021">
</codeblock>

Extracting the distribution information can also be done using the very important function `table()`. This function will be used soon when dealing with two categorical variables.

<codeblock id="02_032">
</codeblock>

Let's enhance the visualization by adding a title and some colors *(https://r-charts.com/colors/)*.

<codeblock id="02_033">
</codeblock>

To represent the distribution in terms of percentages, use the very important function `prop.table()`.

<codeblock id="02_034">
</codeblock>


## The *R* corner: *ggplot2* an alternative to base R
<br>

Let's represent a categorical variable with the *ggplot2* package. While the `barplot()` uses a vector containing the distribution information, the `ggplot()`  function requires to create a data frame. 

<codeblock id="02_035">
</codeblock>

The `data.frame()` function has generated two variables (*Var1* and *Freq*). Associate the x-axis with the categories and the y-axis with the number of occurrences.

<codeblock id="02_035b">
</codeblock>

Raw data (*MGO*) can be used directly. Associate the x-axis with the categories and set the `stat` to `"count"` (this argument was set previously to `"identity"`, but with the distribution as input).

<codeblock id="02_036">
</codeblock>

</exercise>

<exercise id="3" title="From categorical data to contingency table">

Who are those people who are favourable to the inclusion of GM raw materials in products to be fed to animals? Are they characterized by their political party for instance?

To answer this question cross these two variables and build a *contingency table* using the very important `table()` function; before that re-order the *Position.A.Food* variable, as well as the *Political.Party* variable from "Extreme left" to "Right".

<codeblock id="02_03">
</codeblock>

Those people who are favourable to the inclusion of GM raw materials in products to be fed to animals, how are they distributed within the political parties? To answer this question, set the `fill` argument to the name of the variable of interest.

<codeblock id="02_04a">
</codeblock>

Notice that raw data have been used with the very important `..count..` value.

Set the `position` argument to `"dodge"` for an alternative visualization.

<codeblock id="02_04">
</codeblock>

It seems that the data are *structured*, which means that there's a link between the two variables *Position.A.Food* and *Political.Party*. In other words, some classes from the *Position.A.Food* variable seem to be associated in a singular way with classes from the *Political.Party* variable.

Concretely, participants of the survey who are very favourable to the inclusion of GM raw materials in products to be fed to animal are voting either *Liberal* or *Right*.

</exercise>

<exercise id="4" title="From contingency table to the notion of independence">

What happens when data are not structured and when there's no apparent link between two categorical variables?

## The *Stat* corner: breaking a *structure* by resampling
<br>

To understand what is an absence of structure we will disturb the data. The idea is to mix or resample the data collected for the *Position.A.Food* variable: this new information is stored in a new column called *Position.A.Food.Permuted*.

Create a vector of dimension 135 in which the positions of the participants have been permuted.

<codeblock id="02_05a">
</codeblock>

Create a vector of dimension 135 in which the values of the participants have been permuted.

<codeblock id="02_05">
</codeblock>

Visualize the relation between the two variables *Position.A.Food.Permuted* and *Political.Party*.

<codeblock id="02_06">
</codeblock>

In this example, the structure seems broken, which means that there's no particular link between the two variables *Position.A.Food.Permuted* and *Political.Party*. In other words, classes from the *Position.A.Food.Permuted* variable don't seem to be associated in a singular way with classes from the *Political.Party* variable.

Concretely, for this broken structure, if you are very favourable to the inclusion of GM raw materials in products to be fed to animals, you might vote from "Extreme Left" to "Right" unconditionally. This leads us to the notion of independence.

</exercise>

<exercise id="5" title="From the independence to its deviation">

Two events are independent if the occurrence of one does not affect the probability of occurrence of the other. More formally, two events A and B are independent if and only if their joint probability equals the product of their probabilities:

<center><img src="https://latex.codecogs.com/svg.image?\mathcal{P}(A\cap B)=\mathcal{P}(A)\times\mathcal{P}(B)." style="margin-top : 0rem; margin-bottom : 0rem"/></center>

In the following part, we are going to compare <img src="https://latex.codecogs.com/svg.image?\mathcal{P}(A\cap B)" style="margin-top : 1rem; margin-bottom : -0.5rem"/> to  <img src="https://latex.codecogs.com/svg.image?\mathcal{P}(A)\times\mathcal{P}(B)" style="margin-top : 1rem; margin-bottom : -0.5rem"/>, from what have been observed, *i.e.* from the data.

Build a contingency table crossing the two variables *Position.A.Food* and *Political.Party* with the `table()` function. From this contingency table, calculate the marginal probabilities for each variable with the `apply()` and `sum()` functions. Then, from the definition of two independent events, build the probabilities matrix of the joint distribution of *Position.A.Food* and *Political.Party*, under the hypothesis of independence.

<codeblock id="02_07">
</codeblock>

The output `res.table` from the `table()` function can be seen as a matrix <img src="https://latex.codecogs.com/svg.image?(n_{ij})" style="margin-bottom : -0.25rem"/>.

The marginal probabilities for each variable can be defined as :

<center><img src="https://latex.codecogs.com/svg.image?f_{i\cdot}=\dfrac{1}{n}\sum\limits_{i\in I}n_{ij}" style="margin-bottom : -1.95rem"/> and
<img src="https://latex.codecogs.com/svg.image?f_{\cdot j}=\dfrac{1}{n}\sum\limits_{j\in J}n_{ij}," style="margin-bottom : -1.95rem"/></center>

where <img src="https://latex.codecogs.com/svg.image?n=\sum\limits_{i\in I}\sum\limits_{j\in J} n_{ij}." style="margin-bottom : -2.15rem"/>

<br>

When the variables are independent:

<center><img src="https://latex.codecogs.com/svg.image?f_{ij}=f_{i\cdot} \times f_{\cdot j}." style="margin-bottom : -0.25rem"/></center>

<codeblock id="02_08">
</codeblock>

<codeblock id="02_09">
</codeblock>


<codeblock id="02_10">
</codeblock>

<codeblock id="02_11">
</codeblock>

<codeblock id="02_12">
</codeblock>

<codeblock id="02_13">
</codeblock>

</exercise>

<exercise id="6" title="From the notion of deviation to the notion of inertia">
</exercise>

<exercise id="7" title="From the notion of inertia to Correspondence Analysis">

<codeblock id="02_14">
</codeblock>

<codeblock id="02_15">
</codeblock>

</exercise>

<exercise id="8" title="From Correspondence Analysis to Multiple Correspondence Analysis">

<codeblock id="02_16">
</codeblock>

</exercise>

<exercise id="9" title="Case study: the Beards example with CA">

<codeblock id="02_17">
</codeblock>

<codeblock id="02_18">
</codeblock>

<codeblock id="02_19">
</codeblock>

<codeblock id="02_20">
</codeblock>

<codeblock id="02_21">
</codeblock>

<codeblock id="02_22">
</codeblock>

</exercise>

<exercise id="10" title="Case study: the sorting task with MCA">