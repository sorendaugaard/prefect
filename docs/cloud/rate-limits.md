---
description: Prefect Cloud API rate limits.
tags:
    - API
    - Prefect Cloud
    - rate limits
search:
  boost: 2
---

# API Rate Limits & Retention Periods <span class="badge cloud"></span>

API rate limits restrict the number of requests that a single client can make in a given time period. They ensure Prefect Cloud's stability, so that when you make an API call, you always get a response.

!!! info "Prefect Cloud rate limits are subject to change"
    The following rate limits are in effect currently, but are subject to change. Contact Prefect support at [help@prefect.io](mailto:help@prefect.io) if you have questions about current rate limits.

Prefect Cloud enforces the following rate limits: 

- Flow and task creation rate limits
- Log service rate limits

## Flow, flow run, and task run rate limits

Prefect Cloud limits the `flow_runs`, `task_runs`, and `flows` endpoints and their subroutes at the following levels:

- 400 per minute for personal accounts
- 2,000 per minute for organization accounts

The Prefect Cloud API will return a `429` response with an appropriate `Retry-After` header if these limits are triggered.

## Log service rate limits

Prefect Cloud limits the number of logs accepted:

- 700 logs per minute for personal accounts
- 10,000 logs per minute for organization accounts

The Prefect Cloud API will return a `429` response if these limits are triggered.

## Flow run retention 

!!! info "Prefect Cloud feature"
    The Flow Run Retention Policy setting is only applicable in Prefect Cloud.

Flow runs in Prefect Cloud are retained according to the Flow Run Retention Policy setting in your personal account or organization profile. The policy setting applies to all workspaces owned by the personal account or organization respectively. 

The flow run retention policy represents the number of days each flow run is available in the Prefect Cloud UI, and via the Prefect CLI and API after it ends. Once a flow run reaches a terminal state ([detailed in the chart here](/concepts/states/#state-types)), it will be retained until the end of the flow run retention period. 

!!! tip "Flow Run Retention Policy keys on terminal state"
    Note that, because Flow Run Retention Policy keys on terminal state, if two flows start at the same time, but reach a terminal state at different times, they will be removed at different times according to when they each reached their respective terminal states.

This retention policy applies to all [details about a flow run](/ui/flow-runs/#inspect-a-flow-run), including its task runs. Subflow runs follow the retention policy independently from their parent flow runs, and are removed based on the time each subflow run reaches a terminal state. 

If you or your organization have needs that require a tailored retention period, [contact the Prefect Sales team](https://www.prefect.io/pricing).
