# GA4 E-commerce Funnel Analysis & Conversion Optimisation

**Independent portfolio case study | Google Merchandise Store demo data | 11 October–7 November 2026**

An end-to-end Google Analytics 4 (GA4) funnel exploration that moves from event setup and KPI calculation to a prioritised conversion-rate optimisation (CRO) research plan.

> **Portfolio disclosure:** This is an independent learning project using the publicly accessible **Google Analytics demo account**, not an analysis of Liberty Exports, a client website, or a production account under my control. Findings are observational; no website changes or A/B tests were implemented.

## Executive Summary

I configured a **closed, four-step shopping funnel** in GA4 Explore using the events `view_item`, `add_to_cart`, `begin_checkout`, and `purchase` over a 28-day reporting window.

| KPI | Result |
| --- | ---: |
| Users who viewed an item | **25,754** |
| Users who added to cart | **5,216** |
| Users who began checkout | **2,506** |
| Users who purchased | **1,389** |
| Item-view-to-purchase funnel completion | **5.39%** |
| Largest stage abandonment | **79.75%** — Item View → Add to Cart |

The most notable segmentation finding was the **mobile checkout completion rate of 29.22%**, versus **60.43% on desktop** (a 31.21-percentage-point difference). This is an investigation priority, **not proof** that the mobile interface caused the gap.

![Four-stage GA4 shopping funnel with users and step completion rates](assets/funnel-overview.svg)

## Business Questions

1. Where do the most users leave the shopping journey?
2. What proportion of users advances at each step, and what proportion reaches a purchase?
3. Do device categories show meaningfully different funnel patterns?
4. What testable CRO hypothesis should be investigated next?

## Data and Method

- **Source:** [Google Analytics demo account — Google Merchandise Store](https://support.google.com/analytics/answer/6367342).
- **Tool:** Google Analytics 4, Explore → Funnel exploration.
- **Date range:** 11 October–7 November 2026 (28 days; captured on 8 November 2026).
- **Funnel:** Closed; each next step **indirectly followed by** the preceding step, allowing intervening events.
- **Breakdown:** Device category (desktop, mobile, tablet).
- **Unit:** GA4 funnel **users**, not transactions or sessions. Step counts reflect users who satisfy the ordered funnel definition.
- **Data capture:** Values were transcribed from GA4 exploration screenshots, not downloaded as user-level or event-level data.

### Event Definitions

| Step | GA4 event | Interpretation |
| --- | --- | --- |
| 1. Item View | `view_item` | User viewed a product item |
| 2. Add to Cart | `add_to_cart` | User added an item to the basket |
| 3. Begin Checkout | `begin_checkout` | User entered the checkout process |
| 4. Purchase | `purchase` | User completed a purchase event |

### Funnel Results

| Funnel stage | Users | Completion to next stage | Abandonments | Abandonment rate |
| --- | ---: | ---: | ---: | ---: |
| Item View | 25,754 | 20.25% | 20,538 | 79.75% |
| Add to Cart | 5,216 | 48.04% | 2,710 | 51.96% |
| Begin Checkout | 2,506 | 55.43% | 1,117 | 44.57% |
| Purchase | 1,389 | — | — | — |

**Calculations**

```text
Stage completion rate = Users reaching next step / Users at current step × 100
Stage abandonment rate = (Current-step users − Next-step users) / Current-step users × 100
Overall funnel completion = Purchase users / Item-view users × 100
                          = 1,389 / 25,754 × 100 = 5.39%
```

The 5.39% figure is a **funnel completion rate for item viewers**, not the site's total visitor-to-purchase conversion rate.

## Device Segmentation

| Device | Item View | Add to Cart | Begin Checkout | Purchase | Item → Cart | Checkout → Purchase | Item → Purchase |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Desktop | 15,856 | 4,293 | 2,105 | 1,272 | 27.07% | 60.43% | 8.02% |
| Mobile | 9,604 | 898 | 397 | 116 | 9.35% | 29.22% | 1.21% |
| Tablet | 280 | 27 | 4 | 1 | 9.64% | 25.00% | 0.36% |

The tablet sample is especially small at the later stages and is not used to prioritise changes. The device comparison is descriptive; channel mix, user intent, product selection, and other differences may contribute to the observed gap.

## Findings and Business Interpretation

### 1. The largest numerical loss happens before cart addition

**20,538 of 25,754** item viewers did not progress to Add to Cart in the defined funnel (**79.75%** abandonment). This is a starting point for investigating product-page relevance, information clarity, value proposition, and CTA discoverability. Browsing without buying is also normal shopping behaviour; the funnel alone cannot label it a defect.

### 2. Mobile progression is weaker at two important points

- **Item View → Add to Cart:** 9.35% mobile versus 27.07% desktop.
- **Begin Checkout → Purchase:** 29.22% mobile versus 60.43% desktop.

Because users have already shown stronger purchase intent by beginning checkout, the mobile checkout stage deserves focused diagnostic work. The result does **not** establish that a form, design, performance, or payment issue caused the difference.

### 3. The funnel is not a causal experiment

This exploration describes user paths. It cannot isolate the impact of a UI change, campaign, price, or device on purchasing behaviour, and no before-and-after intervention was performed.

## CRO Hypotheses and Validation Plan

| Priority | Observation | Hypothesis to investigate | Evidence needed | Primary KPI |
| --- | --- | --- | --- | --- |
| 1 | Mobile checkout completion is 29.22% versus 60.43% desktop | **If** mobile checkout usability tests reveal difficulty with form fields or validation, **then** simplifying the identified friction point **may** improve completion | Mobile task tests, field errors, device/browser and traffic-source comparisons | Mobile checkout-to-purchase completion |
| 2 | Only 9.35% of mobile item viewers add to cart | **If** customers struggle to find the mobile Add to Cart CTA, **then** increasing its visibility **may** increase progression | Product-page usability testing, scroll/click evidence, segment and product-category checks | Mobile item-to-cart completion |

The proposed changes are **conditional hypotheses**, not implemented improvements or measured uplifts.

### Recommended Next Steps

1. Compare device segments within acquisition channels and relevant product categories to reduce obvious mix effects.
2. Observe a small number of mobile participants attempting product selection and checkout; document exact friction points and user language.
3. Check technical issues such as form validation, payment failures, loading time, and unexpected costs where authorised data is available.
4. Rank candidate changes by likely user impact, implementation effort, and strength of evidence.
5. Specify the primary KPI and guardrails before any experiment; perform a sample-size/power assessment before interpreting an A/B result.
6. If traffic is insufficient, label monitored pre/post changes as directional, accounting for seasonality, campaign shifts, and other confounders.

## Evidence

### GA4 Four-Step Funnel and Stage Metrics

![GA4 funnel exploration showing four ordered shopping events and stage-level metrics](assets/ga4-funnel-exploration.png)

### Purchase and Device Breakdown Verification

![GA4 exploration table confirming 1,389 purchase users and the device breakdown](assets/ga4-purchase-device-breakdown.png)

The accompanying [`data/funnel_metrics.csv`](data/funnel_metrics.csv) and [`data/device_breakdown.csv`](data/device_breakdown.csv) are **manually transcribed summary tables** from these screenshots. They are not raw GA4 exports.

## Skills Demonstrated

GA4 Explore · Funnel Exploration · Event-based measurement · KPI definition and calculation · Funnel abandonment analysis · Device segmentation · CRO hypothesis development · Research prioritisation · Evidence-based marketing recommendations

## Limitations and Responsible Interpretation

- The GA4 demo property is a learning environment with obfuscated representative data; it is not my employer's data.
- The date range is a fixed snapshot. A rolling 28-day date selection will yield different numbers later.
- A closed sequential funnel excludes users who do not meet the defined ordered path; different funnel settings can change the reported counts.
- Device metrics are observational and may reflect different user or traffic mixes; a large percentage difference is not a statistical significance claim.
- The exploration alone cannot establish *why* users left, whether a proposed intervention would work, or what revenue uplift would result.
- The screenshots and summary tables contain aggregate demo data only. No personal customer records, contact lists, or tracking identifiers are included.

## References

- [Google Analytics: Demo account](https://support.google.com/analytics/answer/6367342)
- [Google Analytics: Funnel exploration](https://support.google.com/analytics/answer/9327974)
- [Google Analytics: Explore playbook](https://support.google.com/analytics/answer/12664847)
