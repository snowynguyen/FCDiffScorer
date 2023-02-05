# FCDiffScorer

## Proposed change
This analysis aim to correct the difficulty rating given for Free Contest problems on VNOJ. 

The first iteration of this analysis proposes change to the difficulting scoring of **332** problems. 

Compared to the existing VNOJ scoring, the average change is `-0.08` with std deviation of `0.33`. 

### Relative difficulty curve 

Assuming each problem has a difficulty rating of R in `[0.01, 1.00]`. If no one solves a problem, `R` defaults to `1.00`, while if everyone solves a problem, `R` defaults to `0.01`. This later will be scaled by the difficulty multiplier for each type of contest:

- For Beginner Free Contest: `multiplier = 0.75`
- For IOI and TST practice contests: `multiplier = 2.00` 
- For other contests: `multipliter = 1.50` 

Let `P` be the in-contest AC rate, calculated by **dividing** the **in-contest AC count** (ac) by the **number of true participants** (tp).  
Inspried by the modified Elo Rating system used on Codeforces for problemset difficulty, for every 1.00 points increase in the problem difficulty (scale from 0.01 to 1.00), `P` is divided by 10. Let `f(P)` be this initial function:

`f(x) = (-\log_{10}(x*0.99+0.01)/2*0.99+0.01)` 

![image](https://user-images.githubusercontent.com/30857393/216832527-10c509a7-d770-4588-a607-91997599d41c.png)

This function works well for easy problems, but for more difficult the reward is too low. A small buff is needed for harder problems with AC rate < 0.5

`g(x) = f(x)+(1-f(x))*(\max(0,0.5-x)^{2})`

![image](https://user-images.githubusercontent.com/30857393/216832830-754d92b7-72de-41e9-9cf9-3ab577275b03.png)

I intend to reward a >0.9 difficulty for problems with lower than 1% of AC rate. Another buff is needed for such extremely difficult problems.

`h(x) = g(x)+(1-g(x))*(\max(0,0.125-x)^{3})

![image](https://user-images.githubusercontent.com/30857393/216832785-d823a949-e5ca-4e0b-b4f1-c000eae40757.png)

Desmos demostration: https://www.desmos.com/calculator/ahstqyorda 

## About all the files

For VNOJ admin, the final suggested change is given in `analysis_final.csv`. The problem codename is in the `Task` column, its new rating is in `JRatingM` column. 

To read the detailed final work, consult the `analysis_final.xlsx` file. Other works is found in `analysis` subdirectory. 

## Running this notebook

To run this Jupyter notebook (and come up with the final result yourself): 

1. Install all requirements as in `requirements.txt`.
2. Create a *service account* credential from Google as a JSON file, with Google Drive API enabled.
3. Download the notebook and place the credential file in the same folder, and run the notebook.
