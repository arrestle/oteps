# SystemD OTEP Reciever

### Added
Metrics for capturing SystemD service metrics including current state using existing [dbus](https://pkg.go.dev/github.com/coreos/go-systemd/v22@v22.5.0/dbus) libraries

## Motivation

Be able to display current service availability on a Grafana Dashboard as well as available metrics from SystemD including metrics including the following for each requested service name.

1. service.activestate
2. service.loadstate
3. service.loadstate.activating
4. service.loadstate.activated
5. service.loadstate.deactivating
6. service.loadstate.deactivated
7. service.loadstate.runduration

## Explanation

<!-- Explain the proposed change as though it was already implemented and you were explaining it to a user. Depending on which layer the proposal addresses, the "user" may vary, or there may even be multiple.

We encourage you to use examples, diagrams, or whatever else makes the most sense! -->

System administrators and developers need to monitor the health and performance of their systems. Systemd metrics provide critical information about the system's state and the services running on it. By using a systemd receiver to collect this data, it can be visualized in dashboards to provide valuable insights, such as:

Service uptime and performance
System boot and shutdown times
Resource usage by services
Failure patterns and anomalies

## Internal details

<!-- From a technical perspective, how do you propose accomplishing the proposal? In particular, please explain:

* How the change would impact and interact with existing functionality
* Likely error modes (and how to handle them)
* Corner cases (and how to handle them) -->



By using the [dbus](https://pkg.go.dev/github.com/coreos/go-systemd/v22@v22.5.0/dbus) libraries and converting those to opentelemetry metric functionality we can then display these onto dashboards.

For each process (called a unit), converted the actual timestamps for activating, activated, deactivating and deactivated by subtracting the user space start time for each in order to create a series of durations for each. This allows us to compare different process running times on a single graph. 

We also plan to return the current state of each requested unit so that can be displayed as well, with running showing as green, perhaps, and stopped in red. 

<!-- While you do not need to prescribe a particular implementation - indeed, OTEPs should be about **behaviour**, not implementation! - it may be useful to provide at least one suggestion as to how the proposal *could* be implemented. This helps reassure reviewers that implementation is at least possible, and often helps them inspire them to think more deeply about trade-offs, alternatives, etc. -->

# Trade-offs and mitigations

<!-- What are some (known!) drawbacks? What are some ways that they might be mitigated?

Note that mitigations do not need to be complete *solutions*, and that they do not need to be accomplished directly through your proposal. A suggested mitigation may even warrant its own OTEP! -->

Of the numbers calculated and returned 3 & 4 below turned out not to be useful, and the runduration were sometimes unrealistic. We're thinking there may be some issues in the SystemD code that isn't correctly storing or retrieving some of these numbers.

1. service.loadstate.activating
2. service.loadstate.activated
3. service.loadstate.deactivating
4. service.loadstate.deactivated
5. service.loadstate.runduration

We do think that if these values are displayed and easier to access some of these problems can be dealt with in the linux subsystem in future releases. 

## Prior art and alternatives

<!-- What are some prior and/or alternative approaches? For instance, is there a corresponding feature in OpenTracing or OpenCensus? What are some ideas that you have rejected? -->

## Open questions

<!-- What are some questions that you know aren't resolved yet by the OTEP? These may be questions that could be answered through further discussion, implementation experiments, or anything else that the future may bring. -->

See [Trade-offs and mitigations](#Trade-offs-and-mitigations).

## Future possibilities

<!-- What are some future changes that this proposal would enable? -->
