This week we’re working on a statistical analysis using R. Again, we’re in Rstudio and examining data from the library “archdata.” The first data set is Dart Points and we first are able to get means

> mean(DartPoints$Length) 
[1] 49.33077
> mean(DartPoints[, 5])
[1] 49.33077
> mean(DartPoints[,"Length"])
[1] 49.33077

We can also get summaries:
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
  30.60   40.85   47.10   49.33   55.80  109.50 

Since the median is lower than the mean, we know that it skews right. 

> numSummary(DartPoints[, 5:11])
           mean    sd   IQR   0%   25%  50%   75%  100%  n NA
Length    49.33 12.74 14.95 30.6 40.85 47.1 55.80 109.5 91  0
Width     22.08  5.16  6.60 14.5 18.55 21.1 25.15  49.3 91  0
Thickness  7.27  1.53  2.00  4.0  6.25  7.2  8.25  10.7 91  0
B.Width   13.75  2.95  3.80  7.1 11.70 13.6 15.50  21.2 69 22
J.Width   15.40  2.73  3.95 10.6 13.12 15.6 17.08  21.2 90  1
H.Length  13.41  4.01  5.80  5.8 10.50 12.5 16.30  23.3 91  0
Weight     7.64  4.21  5.50  2.3  4.55  6.8 10.05  28.8 91  0

# 5. Write out an patterns you notice in a new Markdown file in your GitHup repo for this week. 
# 6. Now try summarize the statistics for another dataset in archdata, your choice! Descibe what you chose in your .md file.  

I used the dataset Snodgrass

summary(Snodgrass$Length)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    4.0    13.0    14.5    15.1    17.8    21.0 

Including columns that are not numbers causes R to error
> options(digits=3)
> numSummary(Snodgrass[, 2:15])
Error in colMeans(X, na.rm = TRUE) : 'x' must be numeric
> options(digits=3)
> numSummary(Snodgrass[, 2:10])
Error in colMeans(X, na.rm = TRUE) : 'x' must be numeric
> options(digits=3)
> numSummary(Snodgrass[, 2:4])
        mean     sd    IQR   0% 25%   50%   75% 100%  n
South  254.2 104.32 163.46 74.5 174 250.8 337.9  452 91
Length  15.1   3.32   4.75  4.0  13  14.5  17.8   21 91
Width   15.1   3.17   4.00  5.0  13  15.0  17.0   24 91

So in numSummary we need to include columns that are only numerical because otherwise the whole command will fail.

We were able to add sums as well as finding the missing two objects. The sum helped identify that we are missing two objects
> addmargins(DP_CT)
            Blade.Sh
Name          E  I  R  S Sum
  Darl       15  2  0 10  27
  Ensor       2  1  0  6   9
  Pedernales 15  1  3 13  32
  Travis      7  0  0  4  11
  Wells       3  0  0  7  10
  Sum        42  4  3 40  89
> addmargins(xtabs(~Name+addNA(Blade.Sh), DartPoints))
            addNA(Blade.Sh)
Name          E  I  R  S <NA> Sum
  Darl       15  2  0 10    1  28
  Ensor       2  1  0  6    1  10
  Pedernales 15  1  3 13    0  32
  Travis      7  0  0  4    0  11
  Wells       3  0  0  7    0  10
  Sum        42  4  3 40    2  91


Pie and Bar graph, which is more helpful


# 7. Find a new dataset from the archdata package. Use one of these two create a graph of the data. 
# You can use a scatterplot (plot), a bargraph (barplot), pie chart (pie), or boxplot (boxplot).
# Save the graph you make into the GitHub repo. 

