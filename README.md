# adhikkadam_2511363_part2_kpi_experiment

# Subscription Product Onboarding Campaign Experiment

## Business Problem Statement

**1. What decision needs to be made?**
The core decision is whether to fully launch the new onboarding and activation campaign to all new users, reject it in favor of the existing experience, continue testing to gather more data, or roll it out only to specific user segments (e.g., specific regions or device types).

**2. Who the decision impacts?**
- **New Users:** Will experience a modified onboarding journey designed to improve their initial product understanding and setup.
- **Product & Marketing Teams:** Will use the outcomes to evaluate campaign effectiveness and inform future product growth strategies.
- **Customer Support Team:** May face fluctuations in support ticket volumes depending on the clarity and usability of the new onboarding flow.
- **Business Stakeholders:** Impacted by ultimate changes in revenue generation, user acquisition costs, and customer lifetime value.

**3. What metric should improve?**
The primary success metrics (Key Performance Indicators) that should see a measurable increase include:
- **Conversion Rate:** The proportion of users who become paid customers (`converted_to_paid`).
- **Activation & Onboarding:** The rate at which users successfully complete the onboarding process (`completed_onboarding`) and start a trial (`started_trial`).
- **Early Engagement:** The internal engagement score (`engagement_score`) measured within the first 30 days.

**4. What risks must be monitored?**
While maximizing conversion is the primary goal, it must not come at the cost of user friction, confusion, or poor revenue quality. The key guardrail metrics to monitor are:
- **Support Burden:** The volume of support tickets raised within the first 30 days (`support_tickets_30d`). A spike indicates user confusion or technical bugs in the new experience.
- **Revenue Quality & Churn Risk:** The rate of refund requests (`refund_requested`). High refunds indicate buyer's remorse, accidental conversions, or misleading promises during onboarding.

**5. What evidence is required before making a recommendation?**
To confidently recommend a full rollout, the following evidence is required:
- A statistically significant improvement in the primary metrics (especially paid conversion and onboarding completion) in the Treatment group compared to the Control group.
- Stability or improvement in guardrail metrics (i.e., no statistically significant increase in support tickets or refund rates).
- Segment-level analysis confirming that the new campaign does not severely underperform for any critical user cohort (e.g., specific regions, device types, or organic vs. paid traffic sources).

## Data Cleaning and Preparation

Before analysis, the experiment dataset underwent the following data quality checks and cleaning steps. The cleaned data is available in `analysis/experiment_analysis.xlsx`.

### 1. Duplicate User IDs
* **Check:** Identified 8 duplicate `user_id` entries.
* **Handling:** Retained the first occurrence of each `user_id` and removed the duplicates to prevent double-counting users in the analysis. 

### 2. Missing Values
* **Categorical Variables (`device_type`, `traffic_source`):** Missing values were imputed with the label `'Unknown'`. 
* **Numerical Variables (`engagement_score`):** Missing values (14 records) were imputed with the median engagement score (59.8) of the dataset.
* **Funnel Variables (`days_to_convert`):** Missing values are expected here for users who did not convert. These were left as `NaN` (Null) to differentiate between non-converters and day-zero converters.

### 3. Invalid Binary Values
* **Check:** Verified that event flags (`visited_landing_page`, `started_trial`, `completed_onboarding`, `converted_to_paid`, `refund_requested`) strictly contained 0 or 1.
* **Handling:** No invalid values were found. Explicitly cast columns to integer types for robust aggregation.

### 4. Outliers in Revenue
* **Check:** Analyzed the `revenue_30d` column and detected extreme outliers (e.g., maximum recorded revenue of ~$8,610 from a single user).
* **Handling:** Calculated the 99th percentile of revenue *among paying users* ($7317.26). Values exceeding this threshold were capped to prevent massive outliers from skewing the Average Revenue Per User (ARPU) calculation. The new column `revenue_30d_capped` was created for analysis.

### 5. Group Counts and Segment Distribution
* **Group Balance:** The sample size is well-balanced with 710 users in Treatment and 690 in Control.
* **Segment Distribution:** A cross-tabulation check confirmed that the distribution of regions and device types is roughly equivalent between the Control and Treatment groups, indicating that the randomization (Sample Ratio Mismatch check) holds true.