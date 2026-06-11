# Alerting Basics

Good alerting notifies a human only when something is wrong in a way that requires action, and it favors alerting on user-visible symptoms over internal causes. An alert that fires on high CPU may be noise if users are unaffected, while an alert on elevated error rate or slow response time reflects real harm. The guiding rule is that every page should be actionable, urgent, and tied to something a person can fix right now. Alerts that do not meet that bar should be downgraded to dashboards or tickets.

## Alert on symptoms, not causes

Symptom-based alerting watches what users experience, namely errors, latency, and availability, rather than every internal metric that might contribute to a problem. The reason is that there are countless possible causes but only a few symptoms, so alerting on symptoms catches problems you never anticipated while staying quiet otherwise. A widely used framework is the four golden signals: latency, traffic, errors, and saturation. Start by alerting on error rate and high-percentile latency for your key user journeys, and add cause-based alerts only where they are genuinely predictive.

## Thresholds and burn rates

A static threshold like "error rate above one percent for five minutes" is simple but can be noisy or slow depending on the value you pick. Service level objectives (SLOs) give a more principled approach: you define a target such as 99.9 percent success and alert on the rate at which you are burning your error budget. Fast burn (spending the budget quickly) pages immediately, while slow burn raises a lower-priority warning. Always require a condition to persist for a short window before firing, so a single transient blip does not wake anyone.

## Reducing noise and fatigue

Alert fatigue is the failure mode where engineers receive so many alerts that they start ignoring them, including the real ones. Combat it by deleting or tuning alerts that fire without action being taken, grouping related alerts so one incident does not produce fifty pages, and routing low-urgency signals to tickets instead of pagers. Every alert should link to a runbook describing what it means and the first steps to investigate. Review your alerts regularly and treat a noisy alert as a bug to be fixed, not a fact of life.
