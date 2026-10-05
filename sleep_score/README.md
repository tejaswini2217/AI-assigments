# Sleep Score Calculation

## Project Overview

This project calculates a sleep score using Python and Pandas. The project calculates different sleep-quality components such as REM sleep score, deep sleep score, core sleep score, and awake score. These individual scores are combined to calculate an overall sleep score and classify sleep quality into different categories.

The project uses a sleep dataset containing **100,000 records and 32 columns**.

## Dataset Description

The dataset used in this project is `sleep_health_dataset.csv`.

It contains **100,000 records and 32 columns**.

### Dataset Columns

The dataset contains information related to personal details, sleep measurements, health indicators, and sleep-related outcomes.

| **Column**                    | **Description**                                            |
| ----------------------------- | ---------------------------------------------------------- |
| `person_id`                   | Unique identifier for each person                          |
| `age`                         | Age of the person                                          |
| `gender`                      | Gender of the person                                       |
| `occupation`                  | Occupation of the person                                   |
| `bmi`                         | Body Mass Index                                            |
| `country`                     | Country of the person                                      |
| `sleep_duration_hrs`          | Sleep duration in hours                                    |
| `sleep_quality_score`         | Original sleep quality score                               |
| `rem_percentage`              | Percentage of REM sleep                                    |
| `deep_sleep_percentage`       | Percentage of deep sleep                                   |
| `wake_episodes_per_night`     | Number of times a person wakes during the night            |
| `heart_rate_resting_bpm`      | Resting heart rate                                         |
| `sleep_aid_used`              | Indicates whether a sleep aid was used                     |
| `shift_work`                  | Indicates whether the person performs shift work           |
| `room_temperature_celsius`    | Room temperature during sleep                              |
| `weekend_sleep_diff_hrs`      | Difference in sleep duration between weekdays and weekends |
| `season`                      | Season during which the sleep was recorded                 |
| `day_type`                    | Weekday or Weekend                                         |
| `cognitive_performance_score` | Cognitive performance score                                |
| `sleep_disorder_risk`         | Sleep disorder risk category                               |
| `felt_rested`                 | Indicates whether the person felt rested                   |

The dataset contains additional columns, making a total of **32 columns**.

## Technologies Used

* Python
* Pandas
* NumPy

## Project Workflow

### 1. Loading the Dataset

The dataset is loaded using Pandas:

```python
import pandas as pd

df = pd.read_csv("sleep_health_dataset.csv")

print(df.head())
```

The first few records are displayed to understand the structure of the dataset.

### 2. Calculating Core Sleep Percentage

Core sleep percentage is calculated by subtracting REM sleep percentage and deep sleep percentage from 100.

```python
df["core_percentage"] = (
    100
    - df["rem_percentage"]
    - df["deep_sleep_percentage"]
)
```

### 3. Calculating REM Sleep Score

The REM sleep score is calculated by comparing the person's REM percentage with a reference value of **22.5%**.

```python
df["rem_score"] = (
    100
    - abs(df["rem_percentage"] - 22.5) / 22.5 * 100
)

df["rem_score"] = df["rem_score"].clip(lower=0)
```

The score is prevented from becoming negative using `clip(lower=0)`.

### 4. Calculating Deep Sleep Score

The deep sleep score is calculated by comparing deep sleep percentage with a reference value of **17.5%**.

```python
df["deep_score"] = (
    100
    - abs(df["deep_sleep_percentage"] - 17.5) / 17.5 * 100
)

df["deep_score"] = df["deep_score"].clip(lower=0)
```

### 5. Calculating Core Sleep Score

The core sleep score is calculated by comparing core sleep percentage with a reference value of **60%**.

```python
df["core_score"] = (
    100
    - abs(df["core_percentage"] - 60) / 60 * 100
)

df["core_score"] = df["core_score"].clip(lower=0)
```

### 6. Calculating Awake Score

The awake score is calculated using the number of wake episodes per night.

```python
df["awake_score"] = (
    100
    - df["wake_episodes_per_night"] * 15
)

df["awake_score"] = df["awake_score"].clip(lower=0)
```

The score decreases as the number of wake episodes increases.

### 7. Calculating Overall Sleep Score

The overall sleep score is calculated by combining the four component scores:

* REM score
* Deep sleep score
* Core sleep score
* Awake score

Each component has an equal weight of **25%**.

```python
df["sleep_score"] = (
    df["rem_score"] * 0.25
    + df["deep_score"] * 0.25
    + df["core_score"] * 0.25
    + df["awake_score"] * 0.25
)

df["sleep_score"] = df["sleep_score"].round(2)
```

Therefore:

**Sleep Score = (REM Score + Deep Score + Core Score + Awake Score) / 4**

### 8. Sleep Score Classification

The calculated sleep score is classified into five categories.

```python
def sleep_category(score):

    if score >= 90:
        return "Excellent"

    elif score >= 80:
        return "Good"

    elif score >= 70:
        return "Fair"

    elif score >= 60:
        return "Poor"

    else:
        return "Very Poor"
```

The classification ranges are:

| **Sleep Score Range** | **Category** |
| --------------------- | ------------ |
| 90–100                | Excellent    |
| 80–89                 | Good         |
| 70–79                 | Fair         |
| 60–69                 | Poor         |
| Below 60              | Very Poor    |

The category is applied to each calculated sleep score using the `apply()` function.

### 9. Final Output

The final output displays the sleep percentages, individual component scores, overall sleep score, and sleep category.

```python
df[
    [
        "rem_percentage",
        "deep_sleep_percentage",
        "core_percentage",
        "wake_episodes_per_night",
        "rem_score",
        "deep_score",
        "core_score",
        "awake_score",
        "sleep_score",
        "sleep_category"
    ]
].head(10)
```

The notebook displays these calculated values for the first 10 records.

## Project Files

├── sleep_health_dataset.csv
├── Sleep_Score.ipynb
└── README.md


### sleep_health_dataset.csv

Contains the sleep-related measurements used for calculating the sleep score.

### Sleep_Score.ipynb

Contains the complete Python implementation for calculating REM score, deep sleep score, core sleep score, awake score, overall sleep score, and sleep category.

### README.md

Contains the documentation and description of the project.

## Conclusion

This project demonstrates the use of Python and Pandas to calculate a sleep score from different sleep-related measurements.

The project calculates **REM score, deep sleep score, core sleep score, and awake score**. These four scores are combined with equal weights to calculate the overall sleep score.

The final sleep score is classified into **Excellent, Good, Fair, Poor, or Very Poor** categories, providing a simple way to understand overall sleep quality.
