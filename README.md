# AI4ALL UCSF EHR Project

Over the summer of 2019, I worked at UCSF alongside three other girls, under the mentorship of Jean Costello, a UCSF graduate student, to identify patterns in synthetic electronic health records (EHRs). Although we all used the same methods, we each worked on our own separate projects, analyzing a specific disease or condition. My specific project focused on depression and related disorders.

## Synthea

Due to the privacy issues associated with using real EHRs, we used Synthea to generate synthetic but realistic EHRs for our research.

![alt text](https://miro.medium.com/max/2612/1*UumfywoBk7isqWhTjzN8ww.png)
![alt text](https://raw.githubusercontent.com/synthetichealth/synthea/gh-pages/images/architecture.png)

After generating several enormous Microsoft Excel files, we organized the information into a pandas dataframe so we could work with the data more easily.

We then used numpy to visualize the data into bar charts and scikit-learn to create various decision tree forests.

## Creating the Trees

The first step was to create a decision tree. Our first attempt resulted in an excessively complicated decision tree that was quite confusing to look at.

[image1]: ./Screenshot1.png "complicated decision tree"
![alt text][image1]

To resolve this problem, we "pruned" the tree by limiting the number of levels. The following tree is "pruned" to four levels.

[image2]: ./Screenshot2.png "pruned decision tree"
![alt text][image2]

We then created decision forests, which consist of hundreds of decision trees, each created with a different subset of the EHR data (using a random seed). I compared the accuracies of the unpruned and pruned trees and forests. Although I was surprised that the complicated tree and forest performed better than the pruned ones (I had expected them to overfit), I was pleased that the accuracies were all higher than 99% (though none were at 100%).

## Problems - Confusion Matrix

However, I uncovered a major flaw in my program. Upon creating a confusion matrix, I found that the tree was not making intelligent decisions at all. Due to the very low percentage of depressed individuals (only .5% of the total population was depressed), the tree simply outputted "not depressed" every time, which yielded an accuracy of about 99.5%. In order to resolve this problem, I decided to reduce the number of controls or negatives (not depressed individuals) by eliminating those under the age of 19, as well as conditions that occurred after an individual's depression-related diagnosis. The following image shows the change in my confusion matrix.

[image3]: ./Screenshot3.png "confusion matrices"
![alt text][image3]

The results were much better, though there is still room for improvement.

## Feature Importance

I also calculated the relative importance of different features in the dataset to determine major factors leading to depression and related disorders. The following image shows the features, listed in decreasing importance, for the unpruned tree, the pruned tree, the unpruned forest, and the pruned forest.

[image4]: ./Screenshot4.png "feature importance"
![alt text][image4]

Overall, the most important features were sinusitus (common cold), daily tobacco/nicotine usage, age (people between the ages of 20 and 30 were likely to be depressed), acute viral pharyngitis (sore throat, obesity, cancer, and insulin (as medication).

Although feature importance looks at _correlation_ between said features and depression, this most certainly does not necessarily mean causation. For example, sinusitus and pharyngitis, while unpleasant, are not likely to be causes of depression. It is likely that they _appear_ to be correlated simply because they are so common in the population.

However, the correlation between regular usage of nicotine-containing drugs such as tobacco and 24-hour patches may be an important warning sign against drug abuse. Many people use the euphoric feeling of being "high" as an escape from physical and/or emotional stressors. However, such drugs may be doing more harm than good, as there appears to be a strong correlation between the two.

I also wondered if synthetic EHRs are not the best source of data on depression. Within the population I produced from Synthea, only 0.5% were depressed, even though depression is known to be quite common. It is possible that Synthea is simply ineffective at dealing with emotional disorders like depression, especially when compared to diseases such as cancer, diabetes, and heart disease. Another possibility is that depression is difficult to diagnose and therefore does not appear often in medical health records. Many cases of depression go undiagnosed because those with depression either are not aware of it or choose to hide it from others. In either case, there is plenty of room to improve and build upon this project, but overall, the program was very effective.

###### source code is unavailable
