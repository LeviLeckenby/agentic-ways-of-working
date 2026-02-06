# Skill: Deployment

Procedures for preparing and executing deployments.

---

## Deployment Principles

1. **Every deployment is reversible** - Always have a rollback plan
2. **Deployments are reproducible** - Same inputs produce same outputs
3. **Deploy small, deploy often** - Smaller changes are safer
4. **Validate before promoting** - Test in staging before production
5. **Monitor after deploying** - Watch for issues immediately after deployment

## Pre-Deployment Checklist

- [ ] All tests pass in CI
- [ ] Code review approved
- [ ] No known critical bugs in the changes
- [ ] Database migrations are backward-compatible (if applicable)
- [ ] Environment variables are configured in target environment
- [ ] Feature flags are set correctly (if applicable)
- [ ] Rollback procedure is documented
- [ ] Monitoring and alerts are configured

## Deployment Strategies

### Direct Deploy (Small/Low-Risk)
- Push to production directly
- Best for: Config changes, small bug fixes, non-critical features
- Risk: Medium (no gradual rollout)

### Blue-Green
- Run two identical environments, switch traffic
- Best for: Major releases, zero-downtime requirements
- Risk: Low (instant rollback by switching back)

### Canary
- Route small percentage of traffic to new version
- Monitor for errors, gradually increase traffic
- Best for: High-traffic applications, risky changes
- Risk: Lowest (limited blast radius)

### Rolling
- Update instances one at a time
- Best for: Containerized applications, microservices
- Risk: Low-Medium (can stop mid-rollout)

## Post-Deployment

1. **Verify** - Check key endpoints, run smoke tests
2. **Monitor** - Watch error rates, latency, resource usage for 15-30 min
3. **Communicate** - Notify the team that deployment is complete
4. **Document** - Record what was deployed and any issues encountered

## Rollback Procedure

1. Detect the issue (monitoring alert or manual observation)
2. Decide to rollback (don't wait - if in doubt, roll back)
3. Execute rollback (revert deployment, not the code)
4. Verify the rollback resolved the issue
5. Investigate root cause before re-deploying
