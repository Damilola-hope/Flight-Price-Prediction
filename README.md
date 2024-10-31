# Flight Booking Dataset Analysis

![download j](https://github.com/user-attachments/assets/ee91b98e-25c8-4823-96b3-571b96bff54a)

## Introduction
This project involves analyzing a flight booking dataset obtained from the "Ease My Trip" website. Various statistical hypothesis tests and visualizations have been conducted using Microsoft Excel to extract meaningful insights. The objective is to understand the factors that influence ticket prices and provide actionable recommendations.

## Research Questions
1. Does price vary with Airlines?
2. How is the price affected when tickets are bought just 1 or 2 days before departure?
3. Does ticket price change based on the departure time and arrival time?
4. How does the price change with changes in Source and Destination?
5. How does the ticket price vary between Economy and Business class?

## Analysis and Findings

### Question A: Does price vary with Airlines?
- **Method**: Pivot table and Column Chart
- **Findings**: The column chart showed a significant variance in ticket prices among different airlines, suggesting that the choice of airline affects the ticket price.

### Question B: How is the price affected when tickets are bought just 1 or 2 days before departure?
- **Method**: Line Chart and T-test
- **Findings**: The line chart and T-test indicated that ticket prices purchased 1-2 days before departure are significantly lower compared to those purchased 3-4 days before departure.

#### T-test Results
|                   | 1-2 Days      | 3-4 Days      |
|-------------------|---------------|---------------|
| **Mean**          | 543.85        | 20345.81      |
| **Variance**      | 25323729.27   | 511995127.5   |
| **Observations**  | 300153        | 300153        |
| **Pooled Variance** | 268659428.4   |               |
| **Hypothesized Mean Difference** | 0           |               |
| **df**            | 600304        |               |
| **t Stat**        | -468.0190081  |               |
| **P(T<=t) one-tail** | 0          |               |
| **t Critical one-tail** | 1.644856165  |            |
| **P(T<=t) two-tail** | 0           |               |
| **t Critical two-tail** | 1.959967936 |            |

- **Interpretation**: The extremely low P-values indicate a statistically significant difference in ticket prices between tickets purchased 1-2 days before departure and those purchased 3-4 days before departure. Tickets bought closer to the departure date are significantly cheaper.

### Question C: Does ticket price change based on the departure time and arrival time?
- **Method**: ANOVA and Regression Analysis
- **Findings**: The ANOVA test indicated significant differences in ticket prices based on departure and arrival times. Regression analysis provided further insights into how these times influence ticket prices.

#### ANOVA Results
| Source of Variation | SS            | df | MS            | F          | P-value     | F crit       |
|---------------------|---------------|----|---------------|------------|-------------|--------------|
| **Sample**          | 0             | 0  | 65535         | 65535      | #NUM!       | #NUM!        |
| **Columns**         | 445736178.8   | 5  | 89147235.76   | 1.64683953 | 0.178106102 | 2.533554548  |
| **Interaction**     | 0             | 0  | 65535         | 65535      | #NUM!       | #NUM!        |
| **Within**          | 1623969442    | 30 | 54132314.74   |            |             |              |

- **Interpretation**: The P-value for the columns (0.1781) is higher than the significance level (0.05), indicating no significant difference in ticket prices across different departure times. Further analysis is needed for arrival times due to potential data issues.

#### Regression Analysis for Departure Time
**Summary Output:**
| Regression Statistics |                |
|------------------------|----------------|
| Multiple R            | 0.072732177    |
| R Square              | 0.00528997     |
| Adjusted R Square     | 0.005270068    |
| Standard Error        | 22637.84106    |
| Observations          | 300153         |

**ANOVA:**
| df       | SS           | MS            | F            | Significance F |
|----------|--------------|---------------|--------------|----------------|
| Regression | 6          | 8.18014E+11   | 1.36336E+11  | 319.2424834    | 0              |
| Residual  | 300147      | 1.53817E+14   | 512471848    |                |                |
| Total     | 300153      | 1.54635E+14   |              |                |                |

**Coefficients:**
| Coefficients | Standard Error | t Stat         | P-value       | Lower 95%     | Upper 95%     |
|--------------|----------------|----------------|---------------|---------------|---------------|
| Intercept    | 18179.20333    | 103.5495741    | 175.5603873   | 0             | 17976.24908   | 18382.15759   |
| Early Morning| 2191.473387    | 135.6296324    | 16.15777724   | 1.05997E-58   | 1925.64312    | 2457.303654   |
| Morning      | 3451.556923    | 133.8865775    | 25.77970837   | 2.1648E-146   | 3189.142995   | 3713.970851   |
| Afternoon    | 0              | 0              | 65535         | #NUM!         | 0             | 0             |
| Evening      | 3053.158563    | 136.3610789    | 22.39024938   | #NUM!         | 2785.894681   | 3320.422444   |
| Night        | 4882.943477    | 146.2726077    | 33.38248736   | 6.9205E-244   | 4596.253278   | 5169.633676   |
| Late Night   | -8883.903944   | 634.9177587    | -13.9922121   | 1.79615E-44   | -10128.3249   | -7639.482985  |

- **Interpretation**: The regression analysis for departure times indicates that ticket prices vary significantly with different departure times. Early Morning, Morning, Evening, and Night times have significant coefficients, while Afternoon showed an anomaly and needs further investigation.

#### Correlation Matrix for Departure Time
|                | Early Morning | Morning        | Afternoon     | Evening       | Night         | Late Night    | price         |
|----------------|---------------|----------------|---------------|---------------|---------------|---------------|---------------|
| Early Morning  | 1             |                |               |               |               |               |               |
| Morning        | -0.298188292  | 1              |               |               |               |               |               |
| Afternoon      | -0.232818246  | -0.242565011   | 1             |               |               |               |               |
| Evening        | -0.281550197  | -0.29333709    | -0.229030544  | 1             |               |               |               |
| Night          | -0.233458148  | -0.243231703   | -0.189909463  | -0.229660036  | 1             |               |               |
| Late Night     | -0.035366075  | -0.03684665    | -0.028768978  | -0.034790707  | -0.028848049  | 1             |               |
| price          | -0.012232384  | 0.018198899    | -0.05196817   | 0.007946018   | 0.041768025   | -0.033768483  | 1             |

- **Interpretation**: The correlation matrix shows weak correlations between the departure times and ticket prices, indicating that while some departure times have significant effects on price, they are not strongly correlated.

#### Regression Analysis for Arrival Time
**Summary Output:**
| Regression Statistics |                |
|------------------------|----------------|
| Multiple R            | 0.128853177    |
| R Square              | 0.016603141    |
| Adjusted R Square     | 0.016583428    |
| Standard Error        | 22508.73904    |
| Observations          | 300153         |

**ANOVA:**
| df       | SS           | MS            | F            | Significance F |
|----------|--------------|---------------|--------------|----------------|
| Regression | 6          | 2.56743E+12   | 4.27904E+11  | 1013.50396     | 0              |
| Residual  | 300147      | 1.52067E+14   | 506643333.3  |                |                |
| Total     | 300153      | 1.54635E+14   |              |                |                |

**Coefficients:**
| Coefficients | Standard Error | t Stat         | P-value       | Lower 95%     | Upper 95%     |
|--------------|----------------|----------------|---------------|---------------|---------------|
| Intercept    | 11284.90608    | 190.226772     | 59.3234378    | 0             | 10912.06695   | 11657.7452    |
| Early Morning| 3708.233443    | 262.7715084    | 14.1120073    | 3.31192E-45   | 3193.208674   | 4223.258213   |
| Morning      | 10946.17002    | 210.3857235    | 52.0290533    | 0             | 10533.81992   | 11358.52012   |
| Afternoon    | 7209.692915    | 222.4193161    | 32.41486865   | 4.2484E-230   | 6773.757308   | 7645.628522   |
| Evening      | 11759.46554    | 206.5305434    | 56.93814264   | 0             | 11354.67148   | 12164.2596    |
| Night        | 10301.85226    | 204.2572197    | 50.43568241   | 0             | 9901.513854   | 10702.19067   |
| Late Night   | 0              | 0              | 65535         | #NUM!         | 0             | 0             |

- **Interpretation**: The regression analysis for arrival times indicates that ticket prices vary significantly with different arrival times. Early Morning, Morning, Afternoon, Evening, and Night times have significant coefficients, while Late Night showed an anomaly and needs further investigation.

### Question D: How does the price change with changes in Source and Destination?
- **Method**: Pivot table and Column Chart
- **Findings**: The column chart showed that ticket prices vary significantly with different source and destination pairs, indicating that the route affects the ticket price.

### Question E: How does the ticket price vary between Economy and Business class?
- **Method**: Pivot table and Column Chart
- **Findings**: The column chart showed a clear distinction in ticket prices between Economy and Business class, with Business class tickets being significantly more expensive.

## Conclusion
This study provides valuable insights into the factors affecting flight ticket prices. By understanding these factors, passengers can make more informed decisions about their travel plans.

## Code for Analysis
All analyses were conducted using Microsoft Excel with the following steps:

1. **Pivot Tables**: Created pivot tables to summarize data by Airlines, Source & Destination, Class, etc.
2. **Charts**: Used line charts, column charts, and histograms to visualize data.
3. **T-test**: Conducted T-tests to compare ticket prices for different days before departure.
   - Used Excel's `Data Analysis Toolpak` to perform T-tests.
4. **ANOVA**: Conducted ANOVA to analyze the effect of departure and arrival times on ticket prices.
   - Used Excel's `Data Analysis Toolpak` to perform ANOVA.
5. **Regression Analysis**: Conducted regression analysis for departure and arrival times to understand their impact on ticket prices.
   - Used Excel's `Data Analysis Toolpak` to perform regression analysis.

### Example Steps in Excel
1. **Creating a Pivot Table**:
   - Go to `Insert` > `Pivot Table`.
   - Select the data range and choose the location for the pivot table.
   - Drag and drop fields into the Rows, Columns, and Values areas as needed.

2. **Creating Charts**:
   - Select the data range for the chart.
   - Go to `Insert` > `Chart` and choose the desired chart type.

3. **Performing T-test**:
   - Go to `Data` > `Data Analysis`.
   - Select `t-Test: Two-Sample Assuming Equal Variances`.
   - Input the ranges for the two samples and check the labels if included.
   - Click `OK` to get the results.

4. **Performing ANOVA**:
   - Go to `Data` > `Data Analysis`.
   - Select `ANOVA: Single Factor`.
   - Input the range for the data and check the labels if included.
   - Click `OK` to get the results.

5. **Performing Regression Analysis**:
   - Go to `Data` > `Data Analysis`.
   - Select `Regression`.
   - Input the ranges for the dependent and independent variables.
   - Check the labels if included and choose the output range.
   - Click `OK` to get the results.

These steps will help replicate the analysis and verify the findings.
I am open to collaborate on data analysis, statistical analysis, and visualization related projects. Youc an reach me via email [bakared2021@gmail.com]
