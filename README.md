# AI4ALL-UCSF-EHR-Project

Over the summer of 2019, I worked at UCSF alongside three other girls, under the mentorship of Jean Costello, a UCSF graduate student, to identify patterns in synthetic electronic health records (EHRs). Although we all used the same methods, we each worked on our own separate projects, analyzing a specific disease or condition. My specific project focused on depression and related disorders.

Due to the privacy issues associated with using real EHRs, we used Synthea to generate synthetic but realistic EHRs for our research.

![alt text](https://miro.medium.com/max/2612/1*UumfywoBk7isqWhTjzN8ww.png)
![alt text](https://raw.githubusercontent.com/synthetichealth/synthea/gh-pages/images/architecture.png)

After generating several enormous Microsoft Excel files, we organized the information into a pandas dataframe so we could work with the data more easily.

We then used numpy to visualize the data into bar charts and scikit-learn to create various decision tree forests.

