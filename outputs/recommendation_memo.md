# Recommendation Memo: New Onboarding Campaign

## 1. Executive Summary: Business Problem Framing

**Decision to be Made:**
Determine the optimal rollout strategy for the new onboarding and activation campaign (Launch to all, Reject, Continue Testing, or Segmented Rollout).

**Impacted Parties:**
New platform users, Customer Support, Product/Marketing teams, and Business Leadership.

**Target Improvements (Success Metrics):**
- Increase in Paid Conversions (`converted_to_paid`)
- Higher Onboarding Completion Rates (`completed_onboarding`)
- Enhanced Early Engagement (`engagement_score`)
- Increased Trial Starts (`started_trial`)

**Risks to Monitor (Guardrail Metrics):**
- Increases in Customer Support Tickets (`support_tickets_30d`)
- Increases in Refund Requests (`refund_requested`)

**Required Evidence for Launch:**
A statistically significant uplift in conversion and activation metrics without a corresponding degradation in customer support volume or refund rates. Segment performance must also remain stable across key demographics.

## 2. North Star metric

### North Star Metric: Paid Conversion Rate (converted_to_paid)

**2.1 Why this metric is the main success metric?**

The ultimate objective of any onboarding and activation campaign in a subscription business is to demonstrate product value so clearly and quickly that a user is willing to pay for it. The Paid Conversion Rate measures exactly this tipping point. It provides a definitive, binary answer to whether the new onboarding experience successfully guided users from initial curiosity to committed financial value.

**2.2 Why other metrics are supporting metrics instead of the North Star?**

**Funnel Metrics (visited_landing_page, started_trial, completed_onboarding):** These are leading indicators. A user might easily click through an onboarding flow or start a free trial, but if they churn before paying, the campaign has not generated actual business value. They are essential for diagnosing where the funnel is working, but they are not the end goal.

**engagement_score:** This is a strong proxy for user health, but it is an internal metric rather than a definitive business outcome. High engagement does not automatically equal revenue if users are just heavily using the free tier.

***revenue_30d:** While revenue is critical, using it as the primary experiment metric can be skewed by a small number of users buying expensive "Premium" plans. Paid Conversion Rate ensures the campaign is evaluated on its ability to successfully activate the broadest base of users, regardless of their chosen plan tier.

**2.3 How this metric connects to business growth?**

In a subscription model, sustainable growth relies on predictable Monthly Recurring Revenue (MRR). By increasing the sheer volume of users who cross the threshold into becoming paid subscribers, the company expands its active customer base. A higher paid conversion rate at the top of the funnel creates a compounding growth effect, lowering the overall Customer Acquisition Cost (CAC) and increasing the pool of users available for long-term retention and upsells.

**What could go wrong if this metric is optimized blindly?**

Focusing exclusively on driving up the Paid Conversion Rate without monitoring other factors can lead to disastrous long-term consequences.

**Dark Patterns:** The product team might intentionally or accidentally implement aggressive tactics, such as making it incredibly difficult to cancel a free trial before the billing cycle hits.

**Overpromising:** The onboarding campaign might make exaggerated claims about the product's capabilities just to get the credit card on file.

**The Rebound Effect:** These blind optimizations will inevitably lead to severe spikes in buyer's remorse, manifesting as a flood of refund_requested events, an overwhelmed customer service team (support_tickets_30d), and massive churn in the second month. This destroys customer trust and damages the long-term unit economics of the business.

## 3. KPI tree explanation
Our evaluation framework was broken down into:
1.  **North Star:** Paid Conversion Rate.
2.  **Primary Drivers:** Top of Funnel Traffic, Activation & Onboarding, and Early User Engagement. We measured leading indicators like Trial Start Rate and Onboarding Completion Rate.
3.  **Guardrail Metrics:** Support Ticket Volume, Refund Request Rate, and Revenue Quality (ARPPU). These exist to ensure we "Do Not Harm" the business while chasing conversion.

## 4. Experiment result summary
The overall results show a dramatic shift in user behavior under the Treatment experience:
*   **Paid Conversion Rate:** Increased from 3.19% (Control) to 7.04% (Treatment).
*   **Average Engagement Score:** Increased from 57.05 to 62.91.
*   **Onboarding Completion Rate:** Increased consistently across valid platforms (e.g., from ~13.8% to 22.2% on mobile).

## 5. Hypothesis test interpretation
We conducted a one-tailed Two-Proportion Z-Test to evaluate the North Star metric. 
*   **P-Value:** 0.000549
*   **Interpretation:** The p-value is significantly below our 0.05 threshold. We reject the null hypothesis. The increase in Paid Conversion Rate is statistically significant and highly unlikely to be the result of random chance. The campaign successfully achieved its primary goal.

## 6. Guardrail analysis
While the new campaign significantly improved the **Paid Conversion Rate**, optimizing purely for conversion in a vacuum can be dangerous. We must evaluate our guardrail metrics to ensure we are not harming the user experience, degrading revenue quality, or creating operational debt.

Based on the experiment data, here is an evaluation of three critical guardrail metrics:

### 6.1 Support Ticket Rate (Risk Level: High)

* **Control Group:** 14.78% of users submitted a support ticket.
* **Treatment Group:** 24.79% of users submitted a support ticket.
* **Analysis:** The new onboarding campaign caused a statistically significant spike in support volume (p < 0.001).
* **Risk Created:** **Yes.** A near 10-percentage-point increase in support tickets indicates that the new onboarding flow is likely confusing, broken in certain edge cases, or prompting users to ask questions before they can proceed. If this campaign is rolled out to 100% of the traffic, the Customer Support team will be overwhelmed, which drives up operational costs and hurts customer satisfaction.

### 6.2 Revenue Quality / ARPPU (Risk Level: High)

* **Control Group:** $1571.31 Average Revenue Per Converted User.
* **Treatment Group:** $770.41 Average Revenue Per Converted User.
* **Analysis:** Although the Treatment group generated *more* total conversions, the quality of those conversions plummeted. The average paying user in the new campaign is spending less than half as much as a user in the existing flow.
* **Risk Created:** **Yes.** This is a critical business risk. The new campaign might be highly effective at pushing users toward cheaper, entry-level tiers, or it might be failing to effectively communicate the value of premium plans. We are acquiring cheaper customers, which could hurt our long-term unit economics and Customer Lifetime Value (LTV).

### 6.3 Refund Rate (Risk Level: Low to Moderate)

* **Control Group:** 0.00%
* **Treatment Group:** 0.42% (p = 0.0874)
* **Analysis:** We saw a slight uptick in refunds in the Treatment group (0 refunds in Control vs. 3 refunds in Treatment).
* **Risk Created:** **Moderate/Monitor.** Because the sample of refunds is so small, this increase is not strictly statistically significant at the standard 95% confidence level. However, going from zero refunds to some refunds implies that a handful of users experienced buyer's remorse or felt misled by the new onboarding flow. While not an immediate dealbreaker, it strongly signals that we need to ensure our trial terms and billing expectations are perfectly clear.

---

### Summary of Guardrail Risks

The guardrail metrics reveal that **the new campaign creates substantial business risk**. While it is fantastic at getting users to click "Buy" (higher conversion) and use the app more frequently (Engagement score rose from 57.05 to 62.91), it does so by confusing them (higher support tickets) and funneling them into lower-value purchases (severely reduced ARPPU).

## 7. Segment-level insight
An analysis of device types revealed that the conversion uplift was primarily driven by **Mobile** (from 2.58% to 7.41%) and **Tablet** users (from 1.81% to 7.14%). **Desktop** users saw a much smaller, potentially negligible absolute lift (from 4.5% to 6.57%). This suggests the new onboarding design might be heavily optimized for mobile viewports while neglecting the desktop experience.


## 8. Final recommendation: Do Not Launch
While the Treatment group achieved the primary objective of raising the Paid Conversion Rate, it did so at an unacceptable cost to the business. Launching this campaign to 100% of users would overwhelm our Customer Support team and severely dilute our Average Revenue Per User, ultimately harming long-term profitability.


## 9. Risk and Limitation
*   **Cannibalization:** The new flow might be pushing users who would have bought premium plans into basic plans. 
*   **Novelty Effect:** The engagement spike might merely be the result of a "new" interface rather than a sustained improvement in product fit.


## 10. Next Steps
1.  **Halt Rollout:** Maintain the Control experience for all new users.
2.  **Investigate Support Logs:** Conduct a qualitative analysis of the support tickets generated by the Treatment group to identify the exact friction points.
3.  **Redesign Pricing/Plan Selection:** Evaluate how plans are presented in the Treatment flow to understand why ARPPU dropped by 50%.
4.  **Mobile-First Iteration:** Given the strong mobile performance, consider adapting the successful mobile elements of the Treatment into a hybrid V2 experiment once the revenue and support bugs are fixed.
