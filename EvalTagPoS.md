---
author:
- |
    CS 565: Intelligent Systems and Interfaces\
    Indian Institute of Technology Guwahati\
    Jan-May 2016
title: |
    Calculating Precision, Recall, and F1-score\
    of a Multi-class Classifier,\
    like- a Part-of-Speech (PoS) Tagger
...

Precision, recall, and F1-score are used to measure the performance of a
classifier. The higher these values, the better the classifier.\
Assume, the input dataset contains a total of $492$ word tokens: (176
articles + 201 adjectives + 115 nouns). Hence, the given set of PoS tags
is $\left\{AT, JJ, NN\right\}$. ‘AT’, ‘JJ’, ‘NN’ stand for Article,
Adjective, and Singular noun, respectively. Once, our classifier
completes execution, the following steps need to be followed.

Step 1: Confusion Matrix
========================

Let, Confusion Matrix $C$ =\
The diagonal elements of $C$ imply number of correct classifications.\
For example, $C_{AT_{True},\ AT_{Classified}}$ = $50$ $\Rightarrow$
Number of word tokens that are classified as ‘Article’ and truly are
articles is $50$.\
On the other hand, the off-diagonal elements of $C$ imply number of
incorrect classifications.\
For example, $C_{AT_{True},\ JJ_{Classified}}$ = $37$ $\Rightarrow$
Number of word tokens that are classified as ‘Adjective’ but are
articles in truth is $37$.\

Step 2: True Positive (TP), False Positive (FP), False Negative (FN) for Each Individual Class
==============================================================================================

From the confusion matrix $C$, we now calculate TP, FP, and FN for every
class/PoS tag. Let us start with the PoS tag ‘AT’.\
$TP_{AT}$ = Number of word tokens that our classifier correctly
classified as ‘Article’.\
$FP_{AT}$ = Number of word tokens that our classifier incorrectly
classified as ‘Article’.\
$FN_{AT}$ = Number of word tokens that are articles in truth but our
classifier incorrectly classified them with some other PoS tag.

$$\begin{aligned}
\label{TP_AT}
TP_{AT} &= C_{AT_{True},\ AT_{Classified}} \nonumber \\
&= 50 \end{aligned}$$

$$\begin{aligned}
\label{FP_AT}
FP_{AT} &= C_{JJ_{True},\ AT_{Classified}} + C_{NN_{True},\ AT_{Classified}} \nonumber \\
&= 90 + 11 \nonumber \\
&= 101\end{aligned}$$

$$\begin{aligned}
\label{FN_AT}
FN_{AT} &= C_{AT_{True},\ JJ_{Classified}} + C_{AT_{True},\ NN_{Classified}} \nonumber \\
&= 37 + 89 \nonumber \\
&= 126\end{aligned}$$

Similarly, we can find $TP_{JJ}$, …, $FN_{JJ}$, $TP_{NN}$, …, $FN_{NN}$.

Step 3: Precision, Recall, F1-score for Each Individual Class
=============================================================

In this Section, we discuss how to compute precision, recall, F1-score
of our classifier for a given class. In Section \[classifierF1\], we
shall discuss how to compute overall precision, recall, F1-score of the
classifier, which is our ultimate objective. Again, let us start with
the PoS tag ‘AT’.\
$PRE_{AT}$ = Precision of our classifier for the PoS tag ‘AT’.\
$REC_{AT}$ = Recall of our classifier for the PoS tag ‘AT’.\
$F1_{AT}$ = F1-score of our classifier for the PoS tag ‘AT’.\
$$\begin{aligned}
\label{PRE_AT}
{PRE}_{AT} 
&= \frac{{TP}_{AT}}{{TP}_{AT} + {FP}_{AT}} \nonumber \\
&= \frac{50}{50 + 101} &From\ Eqn\ (\ref{TP_AT})\ and\ (\ref{FP_AT}) \nonumber \\
&= \frac{50}{151} \nonumber \\
&= 0.3311\end{aligned}$$

$$\begin{aligned}
\label{REC_AT}
{REC}_{AT} 
&= \frac{{TP}_{AT}}{{TP}_{AT} + {FN}_{AT}} \nonumber \\
&= \frac{50}{50 + 126} &From\ Eqn\ (\ref{TP_AT})\ and\ (\ref{FN_AT}) \nonumber \\
&= \frac{50}{176} \nonumber \\
&= 0.2841\end{aligned}$$

$$\begin{aligned}
{F1}_{AT} 
&= 2 \times \frac{{PRE}_{AT} \times {REC}_{AT}}{{PRE}_{AT}\ +\ {REC}_{AT}} \nonumber \\
&= 2 \times \frac{0.3311 \times 0.2841}{0.3311\ +\ 0.2841} &From\ Eqn\ (\ref{PRE_AT})\ and\ (\ref{REC_AT}) \nonumber \\
&= 2 \times \frac{0.0941}{0.6152} \nonumber \\
&= 2 \times 0.153 \nonumber \\
&= 0.306\end{aligned}$$

Step 4: Precision, Recall, F1-score of a Classifier {#classifierF1}
===================================================

Precision of a Classifier
-------------------------

Here, $PRE$ stands for Precision. It can be of two types. They are:
Micro average (${PRE}_{micro}$) and Macro average (${PRE}_{macro}$).\
$$\begin{aligned}
    {PRE}_{micro} &= \frac{{TP}_{AT} + {TP}_{JJ} + {TP}_{NN}}{{TP}_{AT} + {TP}_{JJ} + {TP}_{NN} + {FP}_{AT} + {FP}_{JJ} + {FP}_{NN}}\end{aligned}$$

$$\begin{aligned}
    {PRE}_{macro} 
    &= \frac{{PRE}_{AT} + {PRE}_{JJ} + {PRE}_{NN}}{Number\ of\ Classes} \nonumber \\
    &= \frac{{PRE}_{AT} + {PRE}_{JJ} + {PRE}_{NN}}{\left\vert \left\{AT, JJ, NN\right\} \right\vert} \nonumber \\
    &= \frac{{PRE}_{AT} + {PRE}_{JJ} + {PRE}_{NN}}{3}\end{aligned}$$

Recall of a Classifier
----------------------

Here, $REC$ stands for Recall. It can be of two types. They are: Micro
average (${REC}_{micro}$) and Macro average (${REC}_{macro}$).\
$$\begin{aligned}
{REC}_{micro} &= \frac{{TP}_{AT} + {TP}_{JJ} + {TP}_{NN}}{{TP}_{AT} + {TP}_{JJ} + {TP}_{NN} + {FN}_{AT} + {FN}_{JJ} + {FN}_{NN}}\end{aligned}$$

$$\begin{aligned}
{REC}_{macro} 
&= \frac{{REC}_{AT} + {REC}_{JJ} + {REC}_{NN}}{Number\ of\ Classes} \nonumber \\
&= \frac{{REC}_{AT} + {REC}_{JJ} + {REC}_{NN}}{\left\vert \left\{AT, JJ, NN\right\} \right\vert} \nonumber \\
&= \frac{{REC}_{AT} + {REC}_{JJ} + {REC}_{NN}}{3}\end{aligned}$$

F1-score of a Classifier
------------------------

Here, $F1$ stands for F1-score. It is again of two types: Micro average
(${F1}_{micro}$) and Macro average (${F1}_{macro}$).

$${F1}_{micro} = 2 \times \frac{{PRE}_{micro} \times {REC}_{micro}}{{PRE}_{micro}\ +\ {REC}_{micro}}$$

$${F1}_{macro} = 2 \times \frac{{PRE}_{macro} \times {REC}_{macro}}{{PRE}_{macro}\ +\ {REC}_{macro}}$$

References
==========

-   <http://sebastianraschka.com/faq/docs/multiclass-metric.html>

-   <https://www.youtube.com/watch?v=OwwdYHWRB5E>
