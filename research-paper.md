# Mental Health and Academic Performance: A Student Analysis
*By Noori Selina, Haig Bedros, Julia Ferris, and Matthew Roland*

## Introduction
What drives academic success, and how does mental health play a role? Our research dives into this compelling question by examining two unique datasets that shed light on the intricate relationship between students' mental well-being and their academic achievement. We specifically focused on understanding depression's impact on student life and exploring how various factors influence academic performance.

## Our Data Journey
We worked with two datasets from Kaggle that capture different aspects of student life:

The first dataset tells the story of roughly 300 students, examining how depression intertwines with various aspects of their lives – from how much they sleep to what they eat, and how they handle academic pressure. 

The second dataset brings us insights from about 250 students, painting a picture of their mental health landscape alongside their academic journey, measured through their cumulative GPA.

### Data Preparation and Cleaning
Our data preparation process followed the below approach:

For Dataset 1 (Depression):
- We standardized column names and cleaned inconsistencies.
- Transformed binary responses like "Yes/No" into numerical values (1/0).
- Applied MinMaxScaler to numerical features including age, academic pressure, study satisfaction, study hours, and financial stress.
- Encoded categorical variables like gender and sleep duration.

For Dataset 2 (Academic Performance):
- Handled complex CGPA ranges by converting them to numerical averages.
- Processed sleep duration data, converting entries like "7-8 hrs" into numerical values.
- Scaled numerical features including CGPA, study satisfaction, and average sleep.
- Removed rows with missing values to ensure data reliability.

### Feature Engineering
We engineered our features to capture the nuances in both datasets:

```python
# Example of our CGPA range parsing
def parse_range(val):
    if "-" in val:
        lower, upper = map(float, val.split("-"))
        return (lower + upper) / 2
    else:
        return float(val)

# Example of sleep duration parsing
def parse_sleep(val):
    if isinstance(val, str):
        val = val.replace(" hrs", "").strip()
        if "-" in val:
            lower, upper = map(float, val.split("-"))
            return (lower + upper) / 2
    return float(val)
```

This preprocessing ensured our data was ready for the analysis that followed.

## Our Analytical Approach
We approached our analysis in two phases, employing both traditional machine learning techniques (materials from week 1 - 10) and advanced methods (materials from week 10 - 15) to gain comprehensive insights from our data.

### Implementation Details

Our analysis involved the implementation of various machine learning techniques. Here's how we approached each phase:

#### Data Processing Pipeline
We created a robust preprocessing pipeline using scikit-learn:

```python
preprocessor = ColumnTransformer(
    transformers=[
        ('num', StandardScaler(), numerical_cols),
        ('cat', OneHotEncoder(), categorical_cols)
    ]
)
```

This pipeline ensured consistent handling of both numerical and categorical features across all our models.

#### Neural Network Architecture
For both classification and regression tasks, we implemented a three-layer neural network:

```python
class NeuralNet(nn.Module):
    def __init__(self, input_size):
        super(NeuralNet, self).__init__()
        self.fc1 = nn.Linear(input_size, 64)
        self.fc2 = nn.Linear(64, 32)
        self.output = nn.Linear(32, 1)
        self.sigmoid = nn.Sigmoid()

    def forward(self, x):
        x = torch.relu(self.fc1(x))
        x = torch.relu(self.fc2(x))
        x = self.sigmoid(self.output(x))
        return x
```

### Phase 1: Traditional Machine Learning Approaches
For our first dataset focused on depression prediction, we implemented:

**Decision Trees**: This approach achieved an 88.1% accuracy, providing clear decision paths that helped us understand how factors like academic pressure and sleep patterns influence depression risk.

**Random Forest**: By combining multiple decision trees, this model reached an impressive 95.0% accuracy, showing how ensemble methods can better capture complex patterns in mental health data.

**Logistic Regression**: Our most successful traditional model for depression prediction, achieving 96.0% accuracy. Its success suggests that many risk factors for depression have relatively linear relationships with the outcome.

For our second dataset focusing on GPA prediction, we used:

**Linear Regression**: This baseline model achieved a root mean square error (RMSE) of 0.45, giving us a foundation for comparing more complex approaches.

**Decision Tree Regression**: Improved our predictions with an RMSE of 0.35, better capturing non-linear relationships in academic performance.

**Random Forest Regression**: Our top performer in this phase, achieving an RMSE of 0.23, demonstrating the power of ensemble methods in predicting academic outcomes.

**Gradient Boosting**: Another strong performer with an RMSE of 0.26, using iterative refinement to capture subtle patterns in the data.

### Phase 2: Advanced Analytical Methods
We then explored more sophisticated approaches:

**Neural Networks**: These models achieved an 80.2% accuracy in identifying depression risk factors, though they sometimes struggled with our relatively small dataset. When predicting GPAs, they showed moderate success with an error margin of about 0.32 points.

**Principal Component Analysis (PCA)**: While this dimensional reduction technique helped us simplify our complex data, it came with some trade-offs. Depression prediction accuracy dropped to 70.3%, and GPA predictions showed the highest error margin among our methods at 0.45 points.

**Bootstrapping**: This statistical technique provided stable but modest results, correctly identifying depression patterns 74.2% of the time and predicting GPAs with an error margin of about 0.34 points.

**K-nearest Neighbors (KNN)**: A standout performer in Phase 2, KNN proved particularly effective with our smaller datasets. It achieved an 87.1% accuracy in depression prediction and our most precise GPA predictions with an error margin of just 0.25 points.

## Performance Metrics

### Phase 1 Results
| Dataset | Model | Accuracy | MAE | RMSE |
|---------|-------|----------|-----|------|
| Dataset 1 | Decision Tree | 88.1% | N/A | N/A |
| Dataset 1 | Random Forest | 95.0% | N/A | N/A |
| Dataset 1 | Logistic Regression | 96.0% | N/A | N/A |
| Dataset 2 | Linear Regression | N/A | 0.3450 | 0.4479 |
| Dataset 2 | Decision Tree | N/A | 0.2148 | 0.3521 |
| Dataset 2 | Random Forest | N/A | 0.1590 | 0.2304 |
| Dataset 2 | Gradient Boosting | N/A | 0.1867 | 0.2556 |

### Phase 2 Results
| Dataset | Model | Accuracy | MAE | RMSE |
|---------|-------|----------|-----|------|
| Dataset 1 | Neural Network | 80.2% | N/A | N/A |
| Dataset 1 | PCA | 70.3% | N/A | N/A |
| Dataset 1 | Bootstrapping | 74.2% | N/A | N/A |
| Dataset 1 | K-nearest neighbors | 87.1% | N/A | N/A |
| Dataset 2 | Neural Network | N/A | 0.2925 | 0.3247 |
| Dataset 2 | PCA | N/A | 0.3708 | 0.4503 |
| Dataset 2 | Bootstrapping | N/A | 0.3092 | 0.3385 |
| Dataset 2 | K-nearest neighbors | N/A | 0.1785 | 0.2515 |

## What We Discovered
Our analysis revealed that **Random Forest** was the best-performing model overall, achieving an impressive 95.0% accuracy for depression prediction and the lowest MAE and RMSE in GPA prediction during Phase 1. This highlights the strength of ensemble methods in handling complex patterns in our data.

In Phase 2, **K-nearest Neighbors (KNN)** stood out as the top performer, particularly effective with our smaller datasets. KNN achieved 87.1% accuracy in predicting depression risk and the most precise GPA predictions with an error margin of just 0.25 points.

While neural networks showed potential in detecting depression risk factors, they struggled with the relatively small dataset size, leading to less consistent results. Traditional techniques like PCA and bootstrapping provided useful insights but were not as effective for our specific challenge.

Perhaps most intriguingly, we found that predicting academic performance is remarkably complex – there's no simple formula for success. Factors like personal motivation and life stressors play crucial roles that aren't easily captured in data.

## Real-World Impact
Our findings have meaningful implications for educational institutions:

We can now identify students at risk of depression with over 85% accuracy, enabling schools to provide targeted support before issues escalate. While predicting exact GPAs remains challenging, we've identified key factors that influence academic performance, helping schools develop more effective support systems.

## Looking Forward
Our research demonstrates the powerful potential of machine learning in understanding and supporting student well-being and academic success. While we achieved strong results in predicting depression risk, the complexity of predicting academic performance highlights the need for more comprehensive data and sophisticated analysis techniques.

Future research could benefit from larger datasets, long-term student tracking, and more advanced analytical methods. Ultimately, our work provides a foundation for creating healthier, more successful academic communities where both mental well-being and academic achievement can flourish.