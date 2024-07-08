# Configuration Data - Identifying Topography and Managing Drift

Design a mechanism to communicate configuration data over an existing or new OTLP Signal. 

## Motivation

Managing configuration drift is a difficult issue for SRE teams, and identifying when a configuration change was made can be critical to determining the root cause of configuration related issues. 

## Explanation

<!-- Explain the proposed change as though it was already implemented and you were explaining it to a user. Depending on which layer the proposal addresses, the "user" may vary, or there may even be multiple.

We encourage you to use examples, diagrams, or whatever else makes the most sense! -->

Systems set up with configuration monitoring will emit the full configuration once per day as a trace event or log with a special resource type of "CONFIGURATION". Any time a configuration change is made, the change will be sent via a "CONFIGURATION_CHANGE" trace event or log.

Systems set up with topology monitoring will emit the full topology once per day with a resource type of "TOPOLOGY"

https://confluence.cec.lab.emc.com/pages/viewpage.action?pageId=1184897516#DM5500TelemetryForCloudIQandCUPArchitectureSpecification-UpstreamTelemetry

## Internal details

From a technical perspective, how do you propose accomplishing the proposal? In particular, please explain:

* How the change would impact and interact with existing functionality
* Likely error modes (and how to handle them)
* Corner cases (and how to handle them)

While you do not need to prescribe a particular implementation - indeed, OTEPs should be about **behaviour**, not implementation! - it may be useful to provide at least one suggestion as to how the proposal *could* be implemented. This helps reassure reviewers that implementation is at least possible, and often helps them inspire them to think more deeply about trade-offs, alternatives, etc.

## Trade-offs and mitigations

What are some (known!) drawbacks? What are some ways that they might be mitigated?

Note that mitigations do not need to be complete *solutions*, and that they do not need to be accomplished directly through your proposal. A suggested mitigation may even warrant its own OTEP!

## Prior art and alternatives

What are some prior and/or alternative approaches? For instance, is there a corresponding feature in OpenTracing or OpenCensus? What are some ideas that you have rejected?

## Open questions

What are some questions that you know aren't resolved yet by the OTEP? These may be questions that could be answered through further discussion, implementation experiments, or anything else that the future may bring.

## Future possibilities

What are some future changes that this proposal would enable?
