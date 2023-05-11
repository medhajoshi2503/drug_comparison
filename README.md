# drug_comparison
This code compares two drugs under trail on their effectiveness on toy data set

**Qualitative Definition of a Drug** 
Although there are many factors by which a drug can be qualified, when considered for use, below are parameters which are used to decide one drug over the other. 
● Efficacy 
It is the capacity for beneficial change (or therapeutic effect) of a given drug. In pharmacology, efficacy (Emax) is the maximum response achievable from an applied or dosed agent. efficacy is measured under expert supervision in a group of patients most likely to have a response to a drug, such as in a controlled clinical trial. 
● Potency 
In the field of pharmacology, potency is a measure of drug activity expressed in terms of the amount required to produce an effect of given intensity. A highly potent drug evokes a given response at low concentrations, 
● Toxicity 
Drug toxicity refers to the level of damage that a compound can cause to an organism. The toxic effects of a drug are dose-dependent and can affect an entire system as in the or a specific organ.

Based on these factors, there are a few ways in which the performance of the drugs can turn out to be. 
We can see below examples, there can be different relative response curves for different drugs. 
So in conclusion, the best drug will have the highest efficacy, highest potency and lowest toxicity.
Parameters used in our Model 
It is rather difficult to determine the true efficacy and toxicity in a theoretical setup. We consider a combination of some indirect markers and correspond them with the health status of a given patient to gauge the effectiveness of the drug. 
We consider the below factors. 
1. Age of Patient 
2. Gender of Patient 
3. Dosage Given 
Sample Complexity 
To get a general bound on the number of training samples needed to learn a target concept, we use the following formula 
m ≥ 1/ε (ln|H|+ln(1/ δ)) 
ε is the acceptable error by which we can satisfy hypothesis with probability at least (1−δ) 
The set of constraints considered for us is age of patient, dosage in mg, gender and the output class contains a binary classification of whether the patient has recovered or not. 
Considering boolean attributes, the number of constraints can be expressed Age Range (18 - 90) = 72 < 27 
Dosage range [50, 75, 100] = 3 < 22 
Gender [M,F] = 2 <=21 
|H| = 27 + 22 + 21 = 210 
We desire a 95% probability that the hypothesis be learned with error less than 0.1 m ≥ 1/ε (ln|H|+ln(1/ δ)) 
≥ 1/(0.1) (ln|210|+ln(1/ 0.05)) 
≥ 1/(0.1) (10 ln 2+ln(1/ 0.05)) 
≥ (10) (10 ln 2 + ln(20)) 
≥ (10) (10 * 0.693 + 2.996) = 99.26 ~ 100 
So 100 training samples will suffice for a consistent learner to learn with 95% probability for the hypothesis which has a true error of 10%.
Description of DataSet 
An example data set is shown in below table 
Age Dosage Sex Recovered 
52 75 F 1 
36 50 M 1 
89 100 F 0 
22 75 M 1 
59 100 M 1 
57 50 F 0 
20 75 F 1 
40 75 M 1 
20 75 F 1 
33 100 M 1 
We have taken 1000 training samples in our test data. 
Machine Learning Model and Implementation 
The approach of modeling is to learn the underlying drug behavior for both A and B . And then to generate a random dataset without the recovered field to predict recovery rate drug A and drug B using this data. Following assumptions are made 
Output Labels 
The problem is modeled as a classification where we predict whether a patient is recovered or not with a particular drug. Thus the output labels are Recovered = 0 (Not Recovered) and Recovered = 1 
Hypothesis Class 
For classification we can use many hypotheses but for the current problem we have chosen SVM as it can find slightly complex relationships between data and based on the references it is proven to be better in drug efficacy studies. 
Loss Function 
The loss function used for SVM is what is known as the Hinge Loss function . As this is well suited for SVM we have used the same. We can use cross entropy also if we go for a logistic regression.
Methodology 
We generate two toy data sets for both drug A and drug B and then train two SVM classifiers to learn to predict the output label recovered. Once training is done the both classifiers are deployed on a larger dataset with only feature vectors age,sex and dosage. The models will now predict how Drug A and B will act on these new data and predict whether they will be able to recover. And we can calculate recovery rate as no of patients recovered/total number of patients in the data set 
Now the ‘Twist’ 
In order to prove that a drug is indeed better we use the same data but for drug A model we resample the training data which has a bias towards recovery . If we manipulate this data without affecting generalization error too much the model will definitely outperform drug B model 
Assumptions 
● The toy dataset is generated with some skew so that we can show one both drug recovery rates.

