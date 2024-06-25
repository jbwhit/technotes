
Based on this tweet: https://x.com/pedrohcgs/status/1798384924409360506

## Difference-in-Differences Checklist

- [ ] Plot treatment rollout (use panelView R package)
- [ ] Record number of units treated per cohort
- [ ] Plot average outcomes over time by cohort
- [ ] Select comparison groups
     - [ ] Assess Parallel Trends assumption
     - [ ] Consider who decides treatment and what they know
     - [ ] Determine allowable types of selection
- [ ] Conduct event study (no covariates) to assess Parallel Trends
- [ ] If needed, add covariates affecting untreated outcome growth
     - [ ] Check for overlap in covariates
     - [ ] Use regression adjustment DiD if extrapolating
- [ ] Rerun event study with covariates to reassess Parallel Trends
- [ ] Perform sensitivity analysis for Parallel Trends violations
     - [ ] Consider honestDiD R package
- [ ] Explore other methods if Parallel Trends remains implausible
