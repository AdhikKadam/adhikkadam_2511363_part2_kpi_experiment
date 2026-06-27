# Hypothesis Testing Framework

## Business Context & Decision Connection
Leadership needs to decide whether to launch the new onboarding and activation campaign to all users. To make a data-driven recommendation, we must rigorously test whether the observed difference in our primary success metric between the Control and Treatment groups is statistically significant, or merely due to random chance. 

If the test proves the new campaign is definitively better, we recommend a full launch (provided guardrail metrics are stable). If not, we save engineering and support resources by retaining the existing experience or iterating further.

---

## Statistical Framework

### 1. Metric Being Tested
**Paid Conversion Rate** (The proportion of users where `converted_to_paid` = 1).

### 2. Reason for Choosing this Metric
As defined in our KPI Tree, Paid Conversion Rate is our **North Star Metric**. While funnel metrics like "completed onboarding" are helpful diagnostics, the ultimate goal of the campaign is to drive business growth and revenue. Testing the conversion rate ensures our launch decision is tied directly to bottom-line business value.

### 3. Hypotheses
Let $P_c$ be the true conversion rate of the Control group, and $P_t$ be the true conversion rate of the Treatment group.

* **Null Hypothesis ($H_0$):** $P_t - P_c \le 0$
    * *Business Translation:* The new onboarding campaign (Treatment) performs the same as, or worse than, the existing experience (Control) in driving paid conversions.
* **Alternate Hypothesis ($H_1$):** $P_t - P_c > 0$
    * *Business Translation:* The new onboarding campaign significantly improves the paid conversion rate compared to the existing experience.

### 4. Test Type (Tailedness)
**One-Tailed Test (Right-tailed)**
* *Justification:* From a business decision perspective, we only want to launch the new campaign if it is strictly *better* than the control. We are specifically testing for a positive uplift. (Note: standard A/B testing software often defaults to two-tailed to observe both extremes, but for this specific "launch vs. no-launch" threshold based on improvement, a one-tailed test aligns directly with the Alternate Hypothesis).

### 5. Significance Level ($\alpha$)
**$\alpha = 0.05$ (95% Confidence Level)**
* *Justification:* This is the industry standard for A/B testing. It means we are willing to accept a 5% risk of committing a Type I error (recommending the launch of the campaign when it actually has no real positive effect).

---

## Interpretation Logic

Once the statistical test (e.g., Z-test for proportions) is run, we will interpret the **p-value**:

1.  **If p-value < 0.05 AND the Treatment conversion rate is higher:** * **Action:** We *reject the Null Hypothesis*. 
    * **Decision:** The new campaign caused a statistically significant increase in conversions. We will recommend **LAUNCH** (conditional on guardrail metrics like refund rate and support tickets not showing a statistically significant degradation).
2.  **If p-value $\ge$ 0.05:** * **Action:** We *fail to reject the Null Hypothesis*. 
    * **Decision:** We cannot confidently say the new campaign is better. The observed differences could just be noise. We will recommend **REJECT** (keep the control) or **CONTINUE TESTING** if the sample size was deemed too small to detect a meaningful Minimum Detectable Effect (MDE).


## Test Results (Executed)

### Summary of Test Inputs
* **Control Group:** 22 conversions out of 690 users (Conversion Rate: 3.19%)
* **Treatment Group:** 50 conversions out of 710 users (Conversion Rate: 7.04%)
* **Relative Uplift:** 120.87%

### Test Output
* **Test Type:** Two-Proportion Z-Test (One-Tailed, Alternative: Treatment > Control)
* **Z-Statistic:** 3.2640
* **P-Value:** 0.000549

### Decision Rule & Application
* **Alpha Threshold:** 0.05
* **Condition:** We reject the null hypothesis if the P-Value < 0.05.
* **Actual Result:** The calculated P-value (0.000549) is less than 0.05. Therefore, we **reject** the null hypothesis.

### Business Interpretation
The data proves that the Treatment (new onboarding campaign) significantly improves the paid conversion rate compared to the Control (existing experience). The probability that this uplift occurred by random chance is well below our threshold. Given this strong statistical evidence, the primary recommendation leans heavily towards a full launch, pending a final review of the guardrail metrics to ensure no unintended negative consequences (e.g., increased refund rates) occurred.