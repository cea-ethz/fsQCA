## Initializing fsQCA

The survey data was collected in google sheets. After having opened the datafile, it was split into the different sections to have separate analysis for each material. Then the character were recode into their numerical values. For example, "1: strongly disagree" became "1".

## Cleaning data

I decided that only responses which were more than 80% complete would be concidered in the analysis. For each row it was assessed if they were more than 80% complete and if not the corresponding row was deleted. In a second step the rows containing responses from participants outside of Europe were deleted. All remaining empty fields are code to 3 to not skew the answers.

## Averaging responses for the conditions

Once the data is clean one can average the answers provided by a case for certain condition. This consists of calculating the average of the rows for certain columns. For instance, the averaging of the answer for the condition of quantity was done like this: 
```r
Concrete_quantity <- data.frame(rowMeans(Concrete[, 17:44]))
names(Concrete_quantity) <- "Concrete_quantity"
```
The conditions are subsquently combined in one table with the function cbin().

## Calibration

The calibration is done iteratively to obtain plausible results after the truth table minimization. To get an initial impression of the data I also calculated the 15%, 50% and 85% quantiles. Once all conditions are calibrated they combined in one table denoted by "_c".

To avoid all 0.5 values from being automatically excluded from the configurations, a constant of 0.001 was added.

## Necessity analysis

Conditions are necessary when the consitency score is above 0.9 and the coverage score is above 0.5. To test the negated condtions one would use this expression:
```r
pof(1-conds_concrete, "Concrete_outcome_c", Concrete_Conditions_c, relation = "nec")
```

## Truth table

The truth table was determined with the truthTable() function. The frequency cut-off
was set to 1, the consiistency cut-off to 0.79 and the pri cut-off to 0.65.
## Minimization
The minimzation of the thruth table allows one to obtain the complex and parsimonious solutions.

## Rest
The remaining code was to further analyze the data and perform small fsQCA of the conditions. The small fsQCA allowed me to determine which sub-condition was the most important. 


