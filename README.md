# OLS as a Line of Best Fit: Estimation versus Prediction

## Objective
I used California Housing data to see how the same OLS regression gets judged differently when the goal is a coefficient and when the goal is a prediction.

## Methodology
- I fit median house value on median income three ways (the closed form, statsmodels and scikit-learn) and checked that all three gave the same intercept and slope.
- I added up to 100 columns of random noise next to median income and tracked R-squared and adjusted R-squared each time.
- I plotted the fitted line and the residuals against the fitted values.
- I split the data into training and test rows before fitting, then scored an eight-feature model on both.
- I used one specification, value on median income and rooms per household, for two jobs: a coefficient with its 95% interval and a test RMSE.
- I wrote a function, holdout_rmse(), that scores any list of predictors on the same test rows, and used it on median income alone.
- I counted the districts at the 5.0 ceiling and refit the eight-feature model without them.

## Key Findings
- All three methods gave a slope of 0.417938.
- R-squared went from 0.4734 with no noise to 0.4758 with 100 noise columns, even though the noise has nothing to do with house value.
- The eight-feature model had a train RMSE of 0.7197 and a test RMSE of 0.7456.
- Holding median income fixed, the AveRooms coefficient was -0.0381 with a 95% CI of [-0.0430, -0.0333].
- Median income alone had a test RMSE of 0.8421, higher than the eight-feature model.
- Dropping the districts at the 5.0 ceiling moved almost every coefficient closer to zero (MedInc went from 0.4487 to 0.4260) and lowered the test RMSE from 0.7456 to 0.6511, though part of that drop is because the hardest districts to predict also left the test set.
