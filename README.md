# econ3916-lab16-regularization

# Regularization: Buying Bias to Sell Variance

## Objective
I built a simulated design with 200 predictors, only 5 of them real, to see how LASSO and Ridge buy a lower variance with a little bias, and how to choose the penalty by cross-validation.

## Methodology
- Built a simulated design with 200 predictors, only 5 of them real, and 105 training rows, and fitted OLS, LASSO and Ridge to it.
- Compared test MSEs for the three models, and counted how many coefficients each one kept.
- Traced the LASSO path as the penalty fell, to see when the true predictors and the first noise variable entered.
- Chose the penalty by 5-fold cross-validation with the scaler fitted inside every fold.
- Scored LASSO's selection against the known truth.
- Gave LASSO and Ridge two near-duplicate predictors and compared how each split the weight.
- Wrote my own prompt asking an AI for the cross-validation loop, went 2 rounds, and checked its lambda and CV MSE against mine: both matched in every printed digit (lambda 0.1995, CV MSE 1.5502).
- Extension: fitted an Elastic Net on the near-duplicate design. Challenge: multiplied one true predictor by 1,000 and compared LASSO with and without standardisation.

## Key Findings
- Test MSEs were 12.9587 for OLS, 10.1128 for Ridge and 1.4219 for LASSO. OLS and Ridge kept all 200 coefficients, and LASSO kept 16.
- On the LASSO path, all five true predictors were in from step 6, and the first noise variable entered at step 17.
- 5-fold cross-validation with the scaler fitted inside every fold chose lambda 0.1995, with a CV MSE of 1.5502.
- LASSO found 5 of 5 true predictors, with 11 false positives.
- With two near-duplicate predictors, LASSO put 4.462 on one and 0.000 on the other, while Ridge split the weight 1.618 and 1.609.
- Elastic Net chose the pure LASSO mix and gave the same coefficients and test MSE as LASSO (1.1055), far better than Ridge (10.8464).
- Without standardisation, LASSO kept only 2 variables and had a test MSE of 19.6219; with it, the test MSE was 1.4219.
- The AI's loop matched my numbers in round 1 and again in round 2. Changing one choice at a time showed what the check catches: unshuffled folds, a different seed, no scaler, summed fold errors and a root of the mean all gave a CV MSE that was off by between 6% and 400%, and a scaler fitted on all rows was off by only 0.45%.
