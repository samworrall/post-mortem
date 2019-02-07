# Failing Enquiries Post-Mortem

## Date of post-mortem

07/02/2019

## Date of incident

04/02/2019 - 05/02/2019

## Authors

Sam Worrall

## Status

Complete, action items to be decided

## Summary

Enquiries were broken (rendered 422 responses) for ~17 hours

## Impact

~350 failed enquiries, potential revenue impact

## Root Causes

The opt_in param on the email checkbox was renamed to email_opt_in, but the enquiry_form 
that is used when creating any other enquiry continued to look for the opt_in param.
The brochure requests continued to create valid enquiries, but any other enquiry during 
this time was met with a 422 response due to its invalidity.

## Trigger

Merging [this pull request](https://github.com/ygt/frontend/pull/3332)

## Resolution

Rollback of deploys on prod and prod-admin + revert pull request

## Detection

Freshdesk tickets opened by the sales team after noticing an unusual drop in enquiries overnight;
nothing raised on airbrake however

## Action Items

| Action Item | Type | Owner | Bug |
| ----------- | ---- | ----- | --- |
| | | | |
| | | | |
| | | | |
| | | | |
| | | | |
| | | | |
| | | | |
| | | | |
| | | | |

## Lessons Learned


### What went well


### What went wrong


### Where we got lucky


## Timeline

04/02/19

| Time  | Description |
| ----- | ----------- |
| 16:23 | Original deployment to public-facing frontends |
| 16:25 | First enquiry to receive a 422 response |

05/02/19

| Time  | Description |
| ----  | ----------- |
| 07:59 | First freshdesk ticket stating only 10 European enquirues had been made overnight |
| 08:14 | Second freshdesk ticket stating that attempting to make an enquiry throws up a 'something went wrong' error |
| 08:29 | Mike Charlton responds to freshdesk and begins investigating after getting the same error |
| 08:42 | Stephen Lewis discovers that enquiry requests are responding with 422s because they are not valid |
| 08:46 | Stephen Lewis identifies the merged pull request that made the relevant code changes |
| 09:00 | Mike Patrick performs a roll back on production and production_admin |
| 09:09 | Mike Patrick opens a [revert pull request](https://github.com/ygt/frontend/pull/3342) |
| 09:17 | Mike Patrick merges revert pull request |
| 09:27 | Mike Patrick deploys the master branch to production and production_admin |
| 09:28 | Test enquiry on the live site is successful |
| 09:44 | YGT team begins extracting log data for all failed enquiries into a CSV file |
| 11:00 | CSV file is given to Oliver to pass to sales |
