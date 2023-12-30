# Multinom_logit_3


### Loading the dplyr Package and Preparing Data:

- `library(dplyr)`: Loads the `dplyr` package, which is a powerful tool for data manipulation in R.
- The script then defines three vectors: `presion`, `imc`, and `frecuencia`. These vectors represent categories of blood pressure, body mass index (BMI), and their corresponding frequencies, respectively.
- `Chapman.Tabla.Frame <- data.frame(Presion = presion, IMC = imc, Frecuencia = frecuencia)`: Creates a DataFrame named `Chapman.Tabla.Frame` with these vectors as columns.
- `print(Chapman.Tabla.Frame)`: Displays the created DataFrame.

### Converting Columns to Factors:

- The `Presion` and `IMC` columns of `Chapman.Tabla.Frame` are converted into factors with specific levels. This step is crucial for categorical data analysis.

### Fitting a Multinomial Logistic Regression Model:

- `Ajuste.Multinom.Tab <- multinom(Presion ~ IMC, data = Chapman.Tabla.Frame, weights = Frecuencia)`: Fits a multinomial logistic regression model using `Presion` as the dependent variable and `IMC` as the independent variable, with `Frecuencia` as weights.
- `summary(Ajuste.Multinom.Tab)`: Provides a summary of the fitted model.
- `exp(summary(Ajuste.Multinom.Tab)$coefficients)`: Exponentiates the coefficients to interpret them as odds ratios.

### Model Comparison Using ANOVA:

- The script compares two multinomial models using ANOVA: one with only an intercept and another with `IMC` as a predictor. This comparison is used to assess the significance of the `IMC` variable in predicting `Presion`.

### Confidence Intervals and Predictions:

- `exp(confint(Ajuste.Multinom.Tab))`: Calculates and exponentiates the confidence intervals for the model parameters.
- `predict(Ajuste.Multinom.Tab, type = "probs")` and `predict(Ajuste.Multinom.Tab, type = "class")`: These commands predict the probabilities and the classes, respectively, for each observation in the model.

### Evaluating Model Predictions:

- The script creates a contingency table comparing the actual `Presion` categories with the predicted ones, accounting for the frequencies.

### Custom Statistical Test Calculations:

- The script defines observed frequencies and predicted probabilities from a "saturated model."
- It excludes cases where observed frequencies or predicted probabilities are zero.
- The script calculates the log-likelihood of the valid cases for the saturated model.
- It then calculates the deviance for the saturated model and the difference in deviance between the fitted model and the saturated model (referred to as `Estadistico`).
- Finally, it computes a p-value using a chi-square test (`pchisq(Estadistico, 3, lower.tail = F)`) to assess the significance of the difference in deviance, which can be interpreted as a measure of the goodness-of-fit of the model.
