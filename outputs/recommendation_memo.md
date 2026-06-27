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

