Exercise #1

This week we are working on statistical analysis using R and the program Rstudio. The first data set is about dart points. Specifically, we looked at the mean and median of length.

> mean(DartPoints$Length) 

[1] 49.33077

> mean(DartPoints[, 5])

[1] 49.33077

> mean(DartPoints[,"Length"])

[1] 49.33077




We can also get summaries

 Min. 1st Qu.  Median Mean 3rd Qu.    Max. 

 30.60   40.85 47.10   49.33 55.80 109.50 




As mentioned in the example, since the median is lower than the mean, we know that it skews right. 

> numSummary(DartPoints[, 5:11])

                mean    sd IQR   0% 25% 50%   75% 100% n NA

Length     49.33 12.74 14.95 30.6 40.85 47.1 55.80 109.5   91 0

Width       22.08 5.16 6.60 14.5 18.55 21.1 25.15  49.3 91 0

Thickness    7.27 1.53 2.00  4.0 6.25 7.2 8.25  10.7 91 0

B.Width   13.75 2.95   3.80 7.1 11.70 13.6 15.50  21.2 69 22

J.Width    15.40 2.73  3.95 10.6 13.12 15.6 17.08  21.2 90 1

H.Length   13.41 4.01  5.80 5.8 10.50 12.5 16.30  23.3 91 0

Weight      7.64 4.21 5.50  2.3 4.55 6.8 10.05  28.8 91 0




Some other noted patterns are that the standard deviation of length was much higher than the other parameters. This means that length is the most highly variable, while thickness was the least variable parameter.

It’s also interesting that the Base Width had 22 items that were not included, presumably because those dart points were discovered without the base - most likely fragmented.   




The dataset that I used was RBPottery, and like the dart points, here are the summary results for RBPottery:

> data(RBPottery)

> View(RBPottery)

> 

> options(digits=3)

> numSummary(RBPottery[, 3:11])

Error in colMeans(X, na.rm = TRUE) : 'x' must be numeric

> options(digits=3)

> numSummary(RBPottery[, 3:11])

Error in colMeans(X, na.rm = TRUE) : 'x' must be numeric

> options(digits=3)




> numSummary(RBPottery[, 4:12])

          mean     sd IQR     0% 25% 50%     75% 100% n

Al2O3 15.6146 2.7025 4.3750 10.100 13.625 16.1500 18.0000 20.800 48

Fe2O3  5.8258 2.3463 1.9250  0.920 5.428 6.8950 7.3525  9.520 48

MgO    2.5433 1.7256 2.2900  0.530 1.605 1.9300 3.8950  7.230 48

CaO    0.5112 0.4498 0.6850  0.010 0.145 0.2950 0.8300  1.730 48

Na2O   0.2454 0.1740 0.2700  0.030 0.115 0.2100 0.3850  0.830 48

K2O    3.1806 0.9218 0.9575  0.810 2.790 3.1550 3.7475  4.890 48

TiO2   0.8533 0.2139 0.2475  0.030 0.718 0.9050 0.9650  1.340 48

MnO    0.0798 0.0666 0.0457  0.001 0.050 0.0785 0.0958  0.394 48

BaO    0.0167 0.0031 0.0040  0.009 0.015 0.0170 0.0190  0.024 48

The data set covers the percentage of oxides, dioxides, or trioxides found in the pottery across three sites. 

Things I learned about R when running this: 

In numSummary we need to include columns that are only numerical because otherwise, the whole command will fail.

Things I learned about the data:

Aluminum trioxide had the highest average percentage of makeup in the samples, with barium oxide being the smallest. All the tested oxides are present in all the samples with no N/A column. 

Next, we worked with Tables in R with the DartPoints data which used crosstabs. This allowed us to compare different variables with each other. We were also able to add sums as well as finding the missing two objects. The sum helped identify that we are missing two objects.

> addmargins(DP_CT)

            Blade.Sh

Name          E I R S Sum

  Darl       15 2 0 10  27

  Ensor       2 1 0 6 9

  Pedernales 15  1 3 13 32

  Travis      7 0 0 4 11

  Wells       3 0 0 7 10

  Sum        42 4 3 40  89

> addmargins(xtabs(~Name+addNA(Blade.Sh), DartPoints))

            addNA(Blade.Sh)

Name          E I R S <NA> Sum

  Darl       15 2 0 10    1 28

  Ensor       2 1 0 6   1 10

  Pedernales 15  1 3 13 0 32

  Travis      7 0 0 4   0 11

  Wells       3 0 0 7   0 10

  Sum        42 4 3 40    2 91

Next, we worked with graphical data and generating different types of visualizations with the data such as pie and bar graphs. Personally I found the Bar graph the most helpful as the number of Fibulae and the number of Coils were able to be seen. 

We also worked with another set of data of Arctic Norway Pithouses to generate another bar graph to compare size and number of hearths:

I then chose the dataset “Handaxes” from the archdata package to create a graph of the variable “Total Length.”

barplot(Hand_TL, main="Lower Paleolithic handaxes from Furze Platt, Maidenhead, Berkshire, England", xlab="Total Length", ylab="Number of Handaxes")
> data(Handaxes)

> View(Handaxes)

> (Hand_TL <- table(Handaxes$L))


Which generated this table:

 69  75 77  78 79 80  81 82 83 84  85 86 87 88 89  90 91 92 93 94 95  96 97 98 99 100 101 102 

  1   1 1   1 2 3   1 2 2 6   2 4 5 5 8   3 8 6 6 9 4   8 9 11 5 11 11 11 

103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127 128 129 130 

 11  14 6  13 10 9   6 7 9 12  10 12 12 5 15   5 10 6 9 15 8   4 13 6 5 9 8 8 

131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 155 156 157 159 160 

  7  12 10  11 3 6   9 10 7 3   7 4 7 2 6   5 4 1 3 2 4   2 4 3 2 3 2 2 

161 162 163 164 165 166 167 168 169 170 171 173 174 175 176 177 178 179 180 183 186 192 193 196 198 200 203 205 

  3   6 3   2 1 2   4 2 4 3   1 2 1 1 1   2 1 1 1 1 1   1 2 1 1 1 1 1 

206 208 210 225 242 

  1   1 1   1 1 



We used this to then create a bar graph in order to show both the number of handaxes and the length. Due to the high variety of total lengths, a bar graph wouldn’t be as useful. 

> barplot(Hand_TL, main="Lower Paleolithic handaxes from Furze Platt, Maidenhead, Berkshire, England", xlab="Total Length", ylab="Number of Handaxes")

Finally, we did a principle components analysis using RBGlass:

> data(RBGlass1)

> View(RBGlass1)

> (RBGlass1.pca <- prcomp(RBGlass1[, -1], scale.=TRUE))

Standard deviations (1, .., p=11):

 [1] 2.269 1.375 1.047 0.861 0.807 0.661 0.620 0.552 0.432 0.348 0.199

> summary(RBGlass1.pca)

Importance of components:

                         PC1   PC2 PC3    PC4 PC5 PC6    PC7 PC8 PC9 PC10    PC11

Standard deviation     2.269 1.375 1.0465 0.8607 0.8071 0.6611 0.6195 0.5523 0.4315 0.348 0.19942

Proportion of Variance 0.468 0.172 0.0996 0.0673 0.0592 0.0397 0.0349 0.0277 0.0169 0.011 0.00362

Cumulative Proportion  0.468 0.640 0.7395 0.8069 0.8661 0.9058 0.9407 0.9685 0.9854 0.996 1.00000




Then generated a biplot.

While the data was not thoroughly analyzed, we can see basic patterns of clustering of Leicester (Near Na and Sb) and Mancetter (Near Ca).
