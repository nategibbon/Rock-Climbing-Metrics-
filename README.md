# Rock-Climbing-Metrics-

### Overview
The goal of this project was to analyze the results of a questionnaire completed by 611 rock climbers and identify the most important characteristics associated with climbing ability as represented by the hardest boulder or sport route climbed.

### Data Source
This questionnaire was created by Power Company Climbing. Individuals independently completed the questionnaire which consisted of questions about basic demographic information and climbing experience. The questionnaire also included instructions to perform and record the results of physical assessments that assessed the strength of various muscle groups.

### Tools
- pandas, numPy, regex - Data Cleaning and Exploration
- matplotlib, seaborn - Data Visualization
- statsmodels - Calculating Variance Inflation Factor
- sklearn - Linear Regression and Cross-Validation

### Data Cleaning
- 'Sex' was converted to a boolean variable, with 0 representing Male and 1 representing Female.
- 'max_boulder_Vgrade' and 'max_sport_YDS' were converted from the V-Scale and the YDS scale, respectively, to numerical variables. For example, a 'max_sport' grade of 5.12a/b was represented as 12, while a grade of 5.12c/d was represented as 12.5.
- Missing values for 'height' and 'weight' were replaced with the sample median for the corresponding 'sex'. Missing 'span' data was replaced with the 'height' of the individual.
- Missing values for physical assessments were replaced with zero. Physical assessments that were missing responses from >40% of respondents were removed from the analysis.
- 'Height:weight' ratio and 'ape_index' ('span'-'height') were added as additional calculated variables.
- Variables produced by free response questions ('outdoor_season_months', 'outdoor_days', 'train_exp') were cleaned and converted to numerical variables. When the answer was a numerical range, the lower bound of the range was chosen (e.g 4-6 months was converted to 4.)

### Analysis
- The first step of analysis was to look at basic statistical descriptors and create histogram plots for each variable. This identified any issues with data cleaning, mistakes in questionnaire responses, and visualized the distributions of population variables.
- A correlation heatmap was then generated to examine the correlations between all variables.
- Several bivariate histograms were created to visualize the relationship between several variable pairs.
- Variance Inflation Factor (VIF) was calculated to detect the degree of multicollinearity across variables.
- Separate Multiple Linear Regressions with cross validations were performed with 'max_sport_YDS' and 'max_boulder_Vgrade' as the dependent variables. 'sex', 'total_exp', 'train_exp', 'outdoor_season_months', 'outdoor_days', 'weight:height', 'ape_index', 'pullup', 'pushup', 'continuous', 'maxhang', 'weightedpull', and 'repeaters' were used as the independent variables in both regressions. The regression coefficients for the independent variables were calculated and plotted in each case.

### Results
- The 'sex' of the respondents was 2:1 Male to Female.
- The median 'max_boulder_Vgrade' and 'max_sport_YDS' grades were V7 and 5.12a/b, respectively.
- 'total_exp' was left skewed with the most common response of '10+ years', while 'train_exp' was right skewed with the most common response of '1-3 years'.
- 'Height' and 'Age' showed high multicollinearity scores which meant that their variation could be represented by other independent variables in the dataset. These variables were held back from the Linear Regression in order to improve the confidence and repeatability of the other regression coefficients. Many of the physical assessment variables also showed elevated multicollinearity scores but were included in the Linear Regression, as their removal weakened the predictive performance of the model.
- The Linear Regression with 'max_boulder_Vgrade' as the dependent variable had an average R^2 score of .494. The five independent variables with the largest absolute regression coefficients were 'max_hang', 'weight:height' (negative coefficient),'weighted_pull', 'total_exp', and 'outdoor_days'. The Linear Regression with 'max_sport_YDS' as the dependent variable had an average R^2 score of .488. The five independent variables with the largest absolute regression coefficients were 'total_exp', 'outdoor_days', 'weighted_pull', 'repeaters', and 'weight:height' (negative coefficient).

### Interpretation
- In both the Linear Regressions for 'max_boulder_Vgrade' and 'max_sport_YDS', the R^2 scores were close to .50 indicating that about 50% of the variation in max climbing grades in the sample population could be attributed to the independent variables. This relatively low level of correlation is not necessarily surprising, as climbing is a complex, skill-based sport that demands a range of physical and mental attributes. Attributes responsible for the other 50% of the max_grade variation could include flexibility, endurance, injury history, allostatic load, fear management, and mental performance.
- It should also be noted that max_grade is an imperfect readout for climbing ability. The grade assigned to a climb is inherently subjective and can correlate strongly with when and where the climb was established. Additionally the assessment questions were based on the individual's current experience and physical attributes, which may not align with when that person climbed their max_grade.
- The regression coefficients of a Linear Regression describe the nature and scale of the correlation between the independent variables and the dependent variable. A positive coefficient indicates that an increase in the independent variable, **while holding all other independent variables constant**, would result in an increase in the dependent variable. The opposite is true of a negative coefficient.
   - There was noticeable overlap between the largest coefficients between the 'max_boulder_VGrade' and 'max_sport_YDS' regressions. 'total_exp' and 'outdoor_days' were strongly positively correlated in both regressions, which reinforces the notion that experience on actual rock (in contrast to indoor training) is important in developing skills necessary to improve climbing ability.
  - There was a strong positive correlation of 'weighted_pull' with both max_grades, but due to the aforementioned high multicollinearity of many of the physical assessment variables (i.e an individual with a high score in 'weighted_pull' usually had high scores in 'pullup','max_hang', and 'continuous') it would be imprudent to assert that 'weighted_pull' is more important than the other physical assessments. At the very least the data seems to indicate that strong upper body and fingers are correlated with bouldering and sport climbing ability.
  - 'weight:height' ratio demonstrated a negative correlation with both max_grades. As weight and eating disorders are contentious topics in the climbing community, it should be noted that this result indicates that an increase in weight:height ratio without any changes in other variables would predict a decrease in max_grade. However since 'weight:height' shows positive correlation with 'weighted_pull','max_hang', and 'pushup' , it appears that increased 'weight:height' ratio is often accompanied by increased upper body strength.
  - 'max_hang' had the largest positive coefficient for the' max_boulder_Vgrade' regression and 'repeaters' had a positive coefficient for 'max_sport_YDS'. 'max_hang' is a measure of absolute finger strength while 'repeaters' is considered an indicator of finger strength and endurance. This seems to align with common wisdom since maximum finger strength is important for the shorter, powerful style of boulder climbing, while finger endurance is more relevant for longer sport climbing routes. However since we are not able to assign causation these correlations could simply indicate that due to the prevailing training wisdom, individuals who focus more on bouldering are more likely to train 'max_hang' exercises and those who predominantly sport climb are more likely to train and become better at 'repeaters' exercises.


