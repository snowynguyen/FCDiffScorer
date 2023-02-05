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
Inspried by the modified Elo Rating system used on Codeforces for problemset difficulty, for every 0.15 points increase in the problem difficulty (scale from 0.01 to 1.00), `P` is halved. 





## Running this notebook

To run this Jupyter notebook: 

1. Install all requirements as in `requirements.txt`.
2. Create a *service account* credential from Google as a JSON file, with Google Drive API enabled.
3. Download the notebook and place the credential file in the same folder, and run the notebook.
