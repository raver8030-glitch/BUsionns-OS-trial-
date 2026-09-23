\# 018 — Time Tracking, Capacity and Workload Management Specification



\*\*Product:\*\* BusinessOS

\*\*Document ID:\*\* 018

\*\*Status:\*\* Detailed Domain Specification

\*\*Depends On:\*\* 000–017

\*\*Primary Domain:\*\* Time Tracking, Capacity and Workload Management

\*\*Authority Level:\*\* Domain Specification



\---



\# 1. Purpose



The Time Tracking, Capacity and Workload domain provides BusinessOS with authoritative operational records for:



\* actual work time

\* time entries

\* timers

\* estimated effort

\* planned effort

\* capacity

\* availability

\* workload

\* utilization

\* resource allocation

\* scheduling pressure

\* overtime indicators

\* project effort

\* task effort

\* employee workload

\* contractor workload

\* operational capacity forecasting



Its purpose is to answer:



> \*\*Who has capacity, who is overloaded, where is time being spent, and how much effort does work actually require?\*\*



The domain must support both individual productivity and organizational planning without turning time tracking into surveillance.



\---



\# 2. Architectural Position



`018` is the authoritative domain for \*\*actual work-time records and operational capacity/workload calculations\*\*.



This distinction is critical:



```text

Calendar

010

"What is scheduled?"



Time Tracking

018

"What work time was actually recorded?"



HR

011

"What is the person's employment and work schedule?"



Projects / Tasks

005

"What work needs to be done?"



Resources

013

"What physical/logical resource is booked?"



```



These domains cooperate but must not duplicate one another.



\---



\# 3. What This Domain Owns



`018` owns:



1\. Time Entries

2\. Time Entry Categories

3\. Timers

4\. Recorded Work Duration

5\. Time Entry Corrections

6\. Time Entry Approval State

7\. Effort Estimates

8\. Planned Effort

9\. Capacity Profiles

10\. Capacity Rules

11\. Workload Allocations

12\. Utilization Calculations

13\. Capacity Forecasts

14\. Availability calculations derived for workload planning

15\. Overtime indicators

16\. Workload alerts

17\. Time-tracking policies

18\. Time-tracking audit history

19\. Time-based operational metrics



\---



\# 4. What This Domain Does NOT Own



It does not own:



\* employee master data → `011`

\* employment contracts → `011`

\* attendance → `011`

\* leave → `011`

\* shifts → `011`

\* projects → `005`

\* tasks → `005`

\* calendar events → `010`

\* resources/equipment → `013`

\* contractor relationships → `012`

\* commercial costing rules → `007`

\* financial expense records → `015`

\* payroll → future/explicit accounting-HR scope

\* automation → `029`

\* AI → `028`

\* analytics/BI → `024`



\---



\# 5. Critical Distinctions



BusinessOS must preserve these distinctions.



\## 5.1 Attendance vs Time Tracking



Attendance answers:



> Was the employee present according to the organization's attendance system?



Time tracking answers:



> How much time was recorded against actual work?



These are not equivalent.



\---



\## 5.2 Calendar vs Time Tracking



Calendar:



```text

10:00–12:00

Client Meeting

```



does not automatically mean:



```text

2 hours of billable work

```



Time tracking requires an explicit record or configured rule.



\---



\## 5.3 Estimated Effort vs Actual Effort



Example:



```text

Estimated:

5 hours



Actual:

7.5 hours

```



The difference must remain visible.



\---



\## 5.4 Capacity vs Availability



A person may be available for 8 hours but have only 5 hours of allocatable capacity due to:



\* meetings

\* internal work

\* leave

\* operational buffers

\* administrative time



\---



\# 6. Time Entry



A Time Entry represents a recorded duration of work.



Possible fields:



\* user

\* employee reference

\* contractor reference

\* project

\* task

\* work item

\* client

\* category

\* start time

\* end time

\* duration

\* billable classification

\* description

\* source

\* status

\* created at

\* submitted at

\* approved at



\---



\# 7. Time Entry Ownership



Time entries may belong to:



\* employees

\* contractors

\* authorized users



A user does not necessarily equal an employee.



The system should support contractor time where appropriate.



\---



\# 8. Time Entry Lifecycle



Recommended:



```text id="q6x3m8"

Draft

&#x20;↓

Submitted

&#x20;↓

Approved

&#x20;↓

Locked

```



Alternative:



```text id="r8m2v5"

Rejected

Corrected

Cancelled

```



Finalized time records should not be silently rewritten.



\---



\# 9. Time Entry Source



A time entry may originate from:



\* manual entry

\* running timer

\* imported system

\* approved timesheet

\* controlled automation



Source must be preserved.



\---



\# 10. Manual Time Entry



Users may enter:



```text id="m5n8q2"

Date:

2026-09-03



Start:

10:00



End:

12:30



Project:

Client A



Task:

Video Editing



Description:

Rough cut

```



The system should validate:



\* duration

\* project/task access

\* overlapping entries

\* locked periods

\* allowed date range



\---



\# 11. Timer



A timer provides active time capture.



Lifecycle:



```text id="x7p3m9"

Stopped

&#x20;↓

Running

&#x20;↓

Paused

&#x20;↓

Resumed

&#x20;↓

Stopped

&#x20;↓

Saved

```



A timer should not automatically become an approved financial fact.



\---



\# 12. Timer Reliability



Timers must tolerate:



\* application closure

\* network interruption

\* sleep/wake

\* device restart

\* clock changes



A timer should preserve enough state to recover safely.



\---



\# 13. Desktop Timer



The desktop application may provide:



\* global timer

\* task-linked timer

\* project-linked timer

\* pause/resume

\* quick note

\* keyboard shortcut

\* background timer state



\---



\# 14. Web Timer



The web application may support:



\* timer start/stop

\* task association

\* recent timers

\* manual correction



Browser limitations must be considered.



\---



\# 15. Android Timer



Android may support:



\* quick timer

\* task/project selection

\* notification while running

\* pause/resume

\* offline capture



\---



\# 16. Overlapping Time



BusinessOS should detect overlapping entries.



Example:



```text id="y4m8q2"

10:00–12:00 Project A

11:00–13:00 Project B

```



The system should flag the overlap.



Whether overlap is prohibited or allowed by policy is configurable.



\---



\# 17. Overlap Policies



Possible policies:



\### Strict



No overlapping entries.



\### Warning



Allow but require acknowledgement.



\### Allowed



Permit overlapping categories where appropriate.



For example, some organizations may record meeting time against one context while tracking parallel administrative work differently.



The default should favor preventing accidental duplicate time.



\---



\# 18. Time Categories



Organizations may define categories:



\* client work

\* internal work

\* administration

\* meeting

\* production

\* editing

\* sales

\* training

\* research

\* support

\* travel

\* other



Categories support analytics and workload analysis.



\---



\# 19. Billable Classification



A time entry may be:



```text id="k8m3x5"

Billable

Non-Billable

Potentially Billable

```



Billability does not itself determine invoice amount.



Commercial billing rules belong to `007`/`016`.



\---



\# 20. Billable Time Relationship



Example:



```text id="p5q8n2"

Time Entry:

5 hours



Commercial Rule:

₹2,000/hour



Potential Billable Value:

₹10,000

```



The time record remains an operational fact.



The commercial engine determines whether/how it is billed.



\---



\# 21. Time Entry Corrections



Users may need to correct:



\* start time

\* end time

\* duration

\* project

\* task

\* category

\* description



Corrections must preserve history after submission/approval.



Example:



```text id="x2m7v4"

Original:

5.0 hours



Correction:

5.5 hours



Reason:

Incorrect stop time

```



\---



\# 22. Locked Time



Organizations may lock time entries after:



\* approval

\* payroll cutoff

\* billing cutoff

\* accounting period closure

\* reporting closure



Locked records require controlled correction.



\---



\# 23. Timesheets



A Timesheet groups time entries for a period.



Examples:



\* daily

\* weekly

\* biweekly

\* monthly



Timesheets may support:



\* submission

\* manager approval

\* finance review

\* locking



\---



\# 24. Timesheet Lifecycle



```text id="m8q2x5"

Open

&#x20;↓

Submitted

&#x20;↓

Under Review

&#x20;↓

Approved

&#x20;↓

Locked

```



\---



\# 25. Timesheet Approval



Approval may be:



\* manager

\* project manager

\* finance

\* designated reviewer



Approval policy belongs to authorization/workflow architecture.



\---



\# 26. Time Tracking Policy



Organizations may configure:



\* required tracking

\* minimum entry duration

\* rounding

\* allowed backdating

\* correction window

\* approval requirements

\* locking periods

\* overtime thresholds

\* billability defaults



\---



\# 27. Rounding



If time rounding is enabled, it must be explicit.



Example:



```text id="v5n8q2"

Actual:

08:07



Rounded:

08:15

```



The system must preserve the raw value where required and separately represent the applied rounding.



\---



\# 28. Duration Precision



Internal duration should support sufficient precision.



UI may display:



```text

2h 15m

```



while internal storage may use seconds or milliseconds.



The exact precision is an implementation decision.



\---



\# 29. Estimated Effort



Projects/tasks may define estimates:



```text id="k3m8q5"

Task:

Color Grade



Estimate:

4 hours

```



The estimate remains owned by `005` where attached to a task.



`018` consumes and analyzes it.



\---



\# 30. Actual Effort



Actual effort is derived from approved/valid time entries.



Example:



```text id="p7n4x8"

Estimate:

4h



Actual:

6h 20m



Variance:

+2h 20m

```



\---



\# 31. Effort Variance



Useful categories:



```text id="x5m8q2"

Under Estimate

On Estimate

Over Estimate

Significantly Over

```



Thresholds should be configurable.



\---



\# 32. Workload



Workload represents planned/allocated effort over a time period.



Example:



```text id="m7q3n8"

Monday:

6h planned



Tuesday:

9h planned



Wednesday:

4h planned

```



\---



\# 33. Capacity



Capacity represents how much work a person or team can reasonably take on.



Capacity may depend on:



\* working schedule

\* leave

\* holidays

\* attendance availability

\* calendar commitments

\* recurring internal work

\* planned buffer

\* existing assignments

\* configured capacity percentage



\---



\# 34. Capacity Formula



Conceptually:



```text id="c4n8m2"

Gross Working Capacity

− Leave / Unavailable Time

− Fixed Commitments

− Reserved Operational Time

− Buffer

=

Allocatable Capacity

```



Exact implementation may differ by organization.



\---



\# 35. Capacity vs Working Hours



An employee may work:



```text id="f7k2n4"

8h/day

```



but have:



```text id="n3w8p5"

5.5h/day allocatable project capacity

```



This is not a contradiction.



\---



\# 36. Capacity Profiles



Capacity Profiles may define:



\* standard working days

\* working hours

\* allocatable percentage

\* meeting buffer

\* administrative buffer

\* seasonal capacity

\* effective dates



Example:



```text id="r4x8m2"

Standard:

8h/day



Allocatable:

70%



Project Capacity:

5.6h/day

```



\---



\# 37. Effective-Dated Capacity



Capacity can change over time.



Example:



```text id="c6v9n1"

Jan–Jun:

80%



Jul onward:

60%

```



Historical workload analysis must use the appropriate capacity period.



\---



\# 38. Team Capacity



Capacity should be aggregatable:



```text id="q8v2n6"

Editor A:

5h



Editor B:

6h



Editor C:

4h



Team Capacity:

15h

```



Aggregation must respect individual availability.



\---



\# 39. Workload Allocation



A workload allocation represents planned effort assigned to a person/team.



It may reference:



\* task

\* project

\* campaign

\* client

\* resource

\* date range



Example:



```text id="j5n8q3"

Task:

Edit Client Reel



Assignee:

Employee A



Planned:

3h



Date:

September 5

```



\---



\# 40. Allocation vs Task Assignment



Task assignment answers:



> Who owns the task?



Workload allocation answers:



> How much capacity is expected to be consumed, and when?



They are distinct.



\---



\# 41. Allocation Without Exact Tasks



Capacity planning may reserve time without a finalized task.



Examples:



\* client shoot

\* emergency work

\* planned campaign

\* management

\* internal production block



Such allocations should remain identifiable as planned/unconfirmed.



\---



\# 42. Allocation Confidence



Potential states:



```text id="m4p7x2"

Tentative

Planned

Committed

Actual

```



This allows workload forecasting without treating tentative plans as completed work.



\---



\# 43. Workload Visualization



BusinessOS should support:



\* person view

\* team view

\* project view

\* department view

\* calendar view

\* timeline

\* capacity heatmap

\* workload chart



\---



\# 44. Overload Detection



An overload occurs when planned demand exceeds allocatable capacity.



Example:



```text id="q8v2n6"

Capacity:

35h



Planned:

43h



Overload:

8h

```



\---



\# 45. Overload Levels



Possible:



```text id="m4x7p2"

Normal

Near Capacity

Over Capacity

Severely Over Capacity

```



Thresholds are configurable.



\---



\# 46. Underutilization



BusinessOS should also identify underutilization.



Example:



```text id="n5r8x2"

Capacity:

40h



Planned:

20h



Unallocated:

20h

```



This can support planning.



It must not be interpreted automatically as poor employee performance.



\---



\# 47. Workload Fairness



The system may identify uneven distribution:



```text id="v7p3n8"

Employee A:

110%



Employee B:

65%

```



The system may recommend reallocation.



Recommendations are not automatic employee judgments.



\---



\# 48. Utilization



Utilization may be defined as:



```text id="k9m4x2"

Recorded Productive Time

÷

Available / Allocatable Capacity

```



Organizations may configure the numerator/denominator.



Metrics must be clearly labeled.



\---



\# 49. Billable Utilization



Potential metric:



```text id="p8m2x5"

Billable Time

÷

Available Capacity

```



This should remain distinct from overall utilization.



\---



\# 50. Productivity vs Utilization



BusinessOS must not equate:



```text id="c4n8m2"

More Hours

=

Better Performance

```



Time metrics are operational planning signals.



Performance management belongs to HR and organizational policy.



\---



\# 51. Overtime Indicators



The system may identify potential overtime based on:



\* configured working schedule

\* recorded time

\* approved overtime

\* applicable policy



Example:



```text id="r6x9m2"

Standard:

40h



Recorded:

47h



Potential Overtime:

7h

```



This does not automatically create payroll.



\---



\# 52. Payroll Boundary



Payroll is explicitly outside the initial responsibility of `018`.



Time tracking may provide payroll inputs if a future payroll system requires them.



Payroll calculation remains a separate capability.



\---



\# 53. Attendance Integration



HR `011` may provide:



\* working schedule

\* leave

\* attendance state

\* holidays



Time Tracking uses this context for capacity and policy.



Attendance records remain authoritative in HR.



\---



\# 54. Calendar Integration



Calendar `010` provides:



\* meetings

\* shoots

\* reviews

\* deadlines

\* other scheduled commitments



These may reduce capacity.



Calendar events do not automatically become time entries unless an explicit rule exists.



\---



\# 55. Leave Integration



Approved leave should reduce capacity.



Example:



```text id="w4s9q2"

Capacity:

8h



Approved Leave:

8h



Allocatable:

0h

```



Leave belongs to HR.



\---



\# 56. Project Integration



Projects/tasks may provide:



\* estimated effort

\* due dates

\* assignments

\* dependencies

\* priority



Time Tracking records actual effort against them.



\---



\# 57. Resource Integration



Equipment/resource bookings may consume organizational planning capacity but should not automatically become human work-time entries.



Resource ownership remains `013`.



\---



\# 58. Contractor Integration



Contractors may have:



\* time entries

\* capacity

\* allocations

\* availability



Their relationship remains owned by `012`.



Commercial rate calculations belong to `007`.



\---



\# 59. Cost Integration



Approved time may provide actual labor-cost inputs.



Example:



```text id="x7m3q9"

Employee Time:

10h



Internal Labor Rate:

₹1,000/h



Operational Labor Cost:

₹10,000

```



The exact costing model belongs to `007`.



\---



\# 60. Billing Integration



Time may contribute to usage-based billing.



Example:



```text id="p5n8m2"

Contract:

10 included hours



Recorded:

14 approved hours



Potential Overage:

4 hours

```



`016` determines when billing occurs.



`007` determines commercial pricing.



`015` records resulting invoices.



\---



\# 61. Time Data Quality



BusinessOS should detect:



\* missing time

\* unusually long entries

\* overlaps

\* excessive corrections

\* impossible timestamps

\* entries outside employment/contract period

\* entries against inaccessible projects

\* entries against closed work



These are data-quality signals.



\---



\# 62. Time Entry Validation



Before submission:



```text id="q6m3n8"

Validate User

&#x20;↓

Validate Entity Access

&#x20;↓

Validate Date

&#x20;↓

Validate Duration

&#x20;↓

Check Overlap

&#x20;↓

Check Locked Period

&#x20;↓

Save

```



\---



\# 63. Time Entry Approval



Approval may validate:



\* correctness

\* project allocation

\* billability

\* policy compliance

\* overtime



Approval does not alter the original recorded event.



\---



\# 64. Time Correction Workflow



Recommended:



```text id="x4n7p2"

Original Entry

&#x20;↓

Correction Request

&#x20;↓

Reason

&#x20;↓

Approval if Required

&#x20;↓

New Effective Record

```



Historical audit remains preserved.



\---



\# 65. Time Tracking Audit



Audit should record:



\* creation

\* editing

\* correction

\* approval

\* rejection

\* locking

\* deletion where permitted

\* timer start/stop where relevant

\* bulk edits

\* imports

\* administrative overrides



\---



\# 66. Administrative Override



Admins may correct records when necessary.



Every override should require:



\* authorization

\* reason

\* actor

\* timestamp

\* original state

\* resulting state



\---



\# 67. Deletion



Draft time entries may be deleted.



Submitted/approved/locked entries should generally be corrected or cancelled rather than erased.



\---



\# 68. Time Period Locking



Organizations may lock periods such as:



```text id="n8q3m5"

September 2026

```



After locking:



\* normal edits prohibited

\* corrections require elevated permission

\* audit mandatory



\---



\# 69. Capacity Forecasting



Capacity planning may project:



```text id="v8m3q5"

Next Week



Capacity:

200h



Committed:

160h



Tentative:

30h



Remaining:

10h

```



Forecasts are planning outputs, not guarantees.



\---



\# 70. Demand Forecast



Demand may come from:



\* planned tasks

\* projects

\* campaigns

\* production schedules

\* recurring programs

\* resource plans



The system should distinguish:



```text id="p7n4x8"

Committed Demand

vs

Tentative Demand

```



\---



\# 71. Capacity Scenarios



Future versions may support:



\### Current Plan



Existing assignments.



\### Optimized Plan



Suggested redistribution.



\### What-If Plan



Hypothetical new project.



AI may assist with scenario generation, but users must remain in control.



\---



\# 72. Workload Recommendations



AI may suggest:



> "Move two low-priority editing tasks from Employee A to Employee B."



The system should explain:



\* current capacity

\* task estimate

\* deadlines

\* priority

\* skills

\* dependencies



AI must not automatically reassign work unless explicitly authorized.



\---



\# 73. Skill-Aware Capacity



Capacity planning may consider employee/contractor skills.



Example:



```text id="m4x7p2"

Need:

Color Grading — 8h



Available:

Editor A — 2h

Colorist B — 10h

```



Skill data originates from HR/contractor domains.



\---



\# 74. Capacity by Role



Capacity may be aggregated by:



\* editor

\* designer

\* producer

\* cinematographer

\* animator

\* marketer

\* salesperson



Role definitions remain owned by HR/system authorization as applicable.



\---



\# 75. Capacity by Department



Examples:



\* Production

\* Post-Production

\* Marketing

\* Sales

\* Administration



Department data belongs to HR.



\---



\# 76. Capacity by Project



BusinessOS should show:



```text id="x5m8q2"

Project:

Campaign A



Estimated:

120h



Allocated:

110h



Recorded:

85h

```



This supports project health.



\---



\# 77. Estimate Accuracy



The system may calculate:



```text id="k7n3q8"

Estimated:

5h



Actual:

8h



Variance:

+60%

```



Aggregated over time, this can identify estimation patterns.



\---



\# 78. Estimation Learning



AI may analyze historical estimates:



> "Similar editing tasks have averaged 6.8 hours rather than the current 4-hour estimate."



This is advisory.



The original estimate remains unchanged unless the authorized user modifies it.



\---



\# 79. Time Tracking Privacy



BusinessOS must avoid unnecessary employee surveillance.



The system should favor:



\* work-context tracking

\* explicit user control

\* transparent policies

\* minimal data collection

\* clear retention

\* access restrictions



It should not silently capture unrelated personal activity.



\---



\# 80. Activity Tracking Boundary



If future versions support application/activity telemetry, it must be a separately governed capability.



Time Tracking must not automatically imply:



\* keystroke logging

\* screenshots

\* webcam monitoring

\* personal browsing surveillance

\* invasive behavioral tracking



Such capabilities require explicit architectural and policy decisions.



\---



\# 81. Employee Visibility



Employees should generally be able to see:



\* their own time entries

\* their submitted timesheets

\* corrections

\* relevant workload

\* capacity assumptions applicable to them



\---



\# 82. Manager Visibility



Managers may see:



\* team workload

\* capacity

\* planned effort

\* actual effort

\* approved time

\* overload

\* project allocation



subject to permissions.



\---



\# 83. Client Visibility



Clients generally should not see:



\* employee time logs

\* employee utilization

\* internal capacity

\* internal workload

\* internal labor rates



Unless explicitly exposed by a commercial agreement.



\---



\# 84. Contractor Visibility



Contractors may see:



\* their own time

\* assignments

\* allowed workload

\* relevant project context



They should not automatically see other workers' capacity.



\---



\# 85. Financial Visibility



Time records may contain cost-sensitive information.



Internal labor rates and cost calculations must be protected.



Clients must not receive cost data simply because time is recorded.



\---



\# 86. Search



Time records may be searchable by:



\* person

\* project

\* task

\* client

\* date

\* category

\* status

\* billability



Search belongs to `023`.



\---



\# 87. Analytics



Time Tracking provides data to `024`.



Potential metrics:



\* total recorded hours

\* billable hours

\* non-billable hours

\* utilization

\* estimation variance

\* project effort

\* overtime indicators

\* workload distribution

\* capacity utilization

\* correction frequency



\---



\# 88. AI



AI may assist with:



\* timesheet summaries

\* effort explanations

\* estimation suggestions

\* workload balancing

\* capacity forecasting

\* missing-entry reminders

\* anomaly detection

\* project effort analysis



AI must not fabricate time records.



\---



\# 89. AI Time Actions



AI may prepare:



```text id="q8m3v5"

Draft Time Entry

```



but execution must require normal permissions.



AI should not silently record hours merely because it inferred that a user worked.



\---



\# 90. Automation



Potential automations:



```text id="m5n8q2"

End of Week

→ Remind Missing Timesheets

```



```text id="x7p3m9"

Workload > 100%

→ Notify Manager

```



```text id="r4x8m2"

Task Completed

→ Prompt User to Confirm Actual Effort

```



Automation belongs to `029`.



\---



\# 91. Missing Time Detection



The system may identify expected tracking gaps based on configured policies.



Example:



```text id="c6v9n1"

Expected:

40h



Recorded:

32h



Gap:

8h

```



This is a prompt for review, not proof that the employee failed to work.



\---



\# 92. Capacity Alerts



Potential alerts:



\* overload

\* approaching capacity

\* low capacity

\* missing allocation

\* deadline/capacity conflict

\* skill bottleneck



\---



\# 93. Deadline + Capacity Conflict



Example:



```text id="q8v2n6"

Task:

10h



Deadline:

Tomorrow



Available Capacity:

4h

```



BusinessOS should flag:



```text id="m4p7x2"

Capacity Risk

```



\---



\# 94. Critical Path Relationship



Task dependencies from `005` may create schedule pressure.



Capacity analysis can highlight:



```text id="n5r8x2"

Critical Task

\+

Insufficient Capacity

=

Project Risk

```



The project system remains authoritative for task dependencies.



\---



\# 95. Data Model — Conceptual



Core entities:



```text id="v7p3n8"

TimeEntry

TimeEntryRevision

Timer

Timesheet

TimesheetPeriod

TimeCategory

TimePolicy

CapacityProfile

CapacityRule

CapacityOverride

WorkloadAllocation

WorkloadSnapshot

CapacityForecast

WorkloadAlert

```



\---



\# 96. Time Entry Model



```text id="k9m4x2"

TimeEntry

├── tenant\_id

├── actor\_id

├── employee\_id / contractor\_id

├── project\_id

├── task\_id

├── category\_id

├── start\_at

├── end\_at

├── duration

├── billable\_classification

├── status

├── source

├── description

└── timestamps

```



\---



\# 97. Capacity Profile Model



```text id="p8m2x5"

CapacityProfile

├── tenant\_id

├── subject\_id

├── effective\_from

├── effective\_to

├── working\_schedule\_reference

├── allocatable\_percentage

├── buffer\_percentage

├── rules

└── status

```



\---



\# 98. Workload Allocation Model



```text id="c4n8m2"

WorkloadAllocation

├── tenant\_id

├── subject\_id

├── project\_id

├── task\_id

├── start\_date

├── end\_date

├── planned\_duration

├── confidence

├── status

└── source

```



\---



\# 99. Tenant Isolation



All time, capacity, workload, and timesheet records must be tenant-scoped.



Cross-tenant time access must be impossible through normal application paths.



\---



\# 100. Concurrency



Time tracking must handle:



\* simultaneous edits

\* timer synchronization

\* offline entries

\* approval races

\* period locking



Optimistic concurrency should protect important records.



\---



\# 101. Offline Time Tracking



Offline capture may support:



\* manual time entries

\* timer state

\* notes

\* timesheet editing



When reconnecting:



```text id="m8q2x5"

Local Entry

&#x20;↓

Sync

&#x20;↓

Validate

&#x20;↓

Conflict Detection

&#x20;↓

Server Record

```



Conflict resolution belongs to `035`.



\---



\# 102. Clock Changes



The system must handle:



\* timezone changes

\* DST transitions

\* device clock errors

\* clock synchronization



Server-authoritative timestamps should be used where appropriate.



\---



\# 103. Time Zones



Time entries should preserve timezone context where needed.



Example:



```text id="x4n7p2"

Start:

2026-09-03T10:00

Timezone:

Asia/Kolkata

```



Cross-timezone users must not have their duration altered by display conversion.



\---



\# 104. Calendar Date vs Duration



A time entry's duration must remain stable even if displayed in another timezone.



\---



\# 105. Bulk Operations



Authorized users may:



\* approve timesheets

\* correct entries

\* categorize entries

\* lock periods

\* export records



Bulk corrections must remain auditable.



\---



\# 106. Import



Time data may be imported from:



\* spreadsheets

\* external time trackers

\* HR systems

\* project systems



Imported records should preserve:



\* source

\* external ID

\* import batch

\* original timestamp



\---



\# 107. Export



Authorized users may export:



\* timesheets

\* time entries

\* workload

\* capacity reports

\* project effort



Sensitive information must be protected.



\---



\# 108. Retention



Time records may have:



\* business retention requirements

\* billing relevance

\* HR relevance

\* legal requirements



Deletion policies must respect dependencies.



\---



\# 109. Time Data Immutability



Approved/locked records should be treated as historical facts.



Corrections create traceable revisions.



\---



\# 110. Audit



Audit should capture:



```text id="q6m3n8"

Created

Edited

Submitted

Approved

Rejected

Corrected

Locked

Unlocked

Deleted

Imported

Exported

Administrative Override

```



\---



\# 111. Observability



Monitor:



\* timer reliability

\* sync failures

\* duplicate entries

\* approval latency

\* capacity calculation latency

\* workload calculation failures

\* import failures

\* conflict rates



\---



\# 112. Performance



Common operations must be optimized for:



\* daily timesheets

\* weekly timesheets

\* team workload

\* capacity dashboards

\* project effort summaries



Indexes should support:



```text id="x5m8q2"

subject\_id

project\_id

task\_id

date

status

tenant\_id

```



\---



\# 113. Cross-Platform Requirements



\## Desktop



Prioritize:



\* global timer

\* task-linked timer

\* timesheet editing

\* workload planning

\* capacity dashboard

\* keyboard shortcuts



\## Web



Prioritize:



\* timesheets

\* manager approvals

\* team workload

\* capacity planning

\* reporting



\## Android



Prioritize:



\* timer

\* quick entry

\* timesheet

\* workload

\* notifications

\* approval



\---



\# 114. Accessibility



Support:



\* accessible time tables

\* keyboard navigation

\* screen readers

\* non-color-only workload states

\* accessible calendar/workload visualizations

\* clear duration formatting



\---



\# 115. Internationalization



Support:



\* timezone-aware timestamps

\* locale dates

\* localized durations

\* working-week differences

\* regional holidays through HR/calendar integration



\---



\# 116. Recommended Vertical Slices



\## Slice 1 — Time Entry Foundation



Implement:



\* time entry

\* categories

\* project/task references

\* basic lifecycle



\## Slice 2 — Timer



Implement:



\* start

\* stop

\* pause

\* recovery



\## Slice 3 — Timesheets



Implement:



\* periods

\* submission

\* approval

\* locking



\## Slice 4 — Effort Analysis



Implement:



\* estimate vs actual

\* project effort

\* task effort



\## Slice 5 — Capacity



Implement:



\* capacity profiles

\* availability

\* allocations



\## Slice 6 — Workload



Implement:



\* workload views

\* overload detection

\* team capacity



\## Slice 7 — Integrations



Integrate:



\* HR

\* Calendar

\* Projects

\* Contractors

\* Commercial costing



\## Slice 8 — Analytics



Integrate `024`.



\## Slice 9 — Automation



Integrate `029`.



\## Slice 10 — AI



Integrate `028`.



\## Slice 11 — Offline



Integrate `035`.



\---



\# 117. Definition of Ready



A time/capacity feature is ready when:



\* time ownership is defined

\* source is defined

\* duration model is defined

\* approval behavior is defined

\* correction behavior is defined

\* locking behavior is defined

\* capacity formula is defined

\* privacy requirements are defined

\* authorization is defined

\* cross-domain inputs are defined

\* offline behavior is defined

\* test cases are defined



\---



\# 118. Definition of Done



A feature is complete when:



\* time records are durable

\* corrections are traceable

\* approvals work

\* locking works

\* capacity calculations are deterministic

\* authorization is enforced

\* tenant isolation is tested

\* privacy controls are validated

\* concurrency is tested

\* offline synchronization is tested where applicable

\* analytics integration works

\* audit works

\* cross-platform UX works

\* accessibility is validated

\* documentation is updated



\---



\# 119. Required Test Categories



\## Unit



\* duration

\* rounding

\* overlap

\* capacity

\* workload

\* utilization

\* variance

\* overtime indicators



\## Integration



\* HR

\* Calendar

\* Projects

\* Contractors

\* Commercial

\* Analytics



\## Authorization



\* employee access

\* manager access

\* contractor access

\* client isolation

\* financial-rate isolation



\## Concurrency



\* timer sync

\* simultaneous editing

\* approval race

\* locking race



\## Offline



\* timer recovery

\* local entry sync

\* duplicate prevention

\* conflict handling



\## Privacy



\* unauthorized time visibility

\* internal labor-rate protection

\* client isolation

\* HR data separation



\---



\# 120. Open Architectural Decisions



1\. Exact timer implementation.

2\. Browser timer limitations and fallback.

3\. Offline timer behavior.

4\. Time-entry rounding policy.

5\. Overlap policy.

6\. Timesheet approval hierarchy.

7\. Period-locking rules.

8\. Capacity formula.

9\. Meeting-time treatment.

10\. Leave/capacity integration depth.

11\. Holiday calendar source.

12\. Overtime calculation boundary.

13\. Payroll integration.

14\. Billable-time integration depth.

15\. Contractor time-tracking rules.

16\. Activity tracking policy.

17\. Privacy/legal requirements for time data.

18\. Exact utilization formula.

19\. Skill-aware capacity algorithm.

20\. AI workload recommendation policy.

21\. Capacity forecasting methodology.

22\. Historical capacity reconstruction.

23\. Time-data retention period.

24\. External time-tracker integrations.

25\. Whether time entries can be client-visible under specific agreements.



\---



\# 121. Architectural Invariants



The following are non-negotiable:



1\. `018` owns actual operational time records.

2\. HR owns attendance and employment state.

3\. Calendar owns scheduled events.

4\. Projects own tasks and estimates.

5\. Commercial rules own billing/cost calculations.

6\. Finance owns resulting financial records.

7\. Time tracking does not automatically imply payroll.

8\. Attendance does not equal work time.

9\. Calendar duration does not automatically equal worked time.

10\. Estimated effort does not equal actual effort.

11\. Approved time must remain historically traceable.

12\. Corrections must preserve original history.

13\. Locked periods require controlled correction.

14\. Time must not become a covert employee-surveillance system.

15\. Client access to time information must be explicitly authorized.

16\. Internal labor rates must remain protected.

17\. AI cannot invent time records.

18\. AI cannot silently record inferred work.

19\. Automation cannot bypass time-entry permissions.

20\. Capacity is a planning model, not an employee-performance judgment.

21\. Utilization must be clearly defined.

22\. Overload does not automatically imply poor performance.

23\. Tenant isolation is mandatory.

24\. Offline synchronization must be conflict-aware.

25\. Duration must remain stable across timezone display changes.

26\. Historical time records must remain auditable.

27\. Cache is never the authority for approved time.

28\. Capacity calculations must be reproducible.

29\. Cross-platform clients must share business semantics.

30\. Time Tracking must not absorb responsibilities belonging to HR, Projects, Calendar, Finance, or Payroll.



\---



\# 122. Dependency Summary



```text id="g6m9q2"

018 Time Tracking / Capacity

│

├── 002 Identity \& Organization

├── 003 Authorization

├── 005 Projects / Tasks

├── 006 Workflow / Approval

├── 007 Services / Costing

├── 009 Communication

├── 010 Calendar

├── 011 HR

├── 012 Contractors

├── 013 Resources

├── 014 Content

├── 015 Finance

├── 016 Billing

├── 021 Integrations

├── 022 Collaboration / Sync

├── 023 Search

├── 024 Analytics

├── 026 Production

├── 028 AI

├── 029 Automation

└── 035 Offline / Sync

```



\---



\# 123. Final Time and Capacity Model



```text id="m8q3v5"

&#x20;                ┌─────────────────┐

&#x20;                │ HR / Employment │

&#x20;                └────────┬────────┘

&#x20;                         │

&#x20;                         ▼

&#x20;                Working Schedule

&#x20;                         │

&#x20;                         ▼

&#x20;                ┌─────────────────┐

&#x20;                │    Capacity     │

&#x20;                │     Profile     │

&#x20;                └────────┬────────┘

&#x20;                         │

&#x20;             ┌───────────┼───────────┐

&#x20;             ▼           ▼           ▼

&#x20;         Calendar       Leave     Allocations

&#x20;            │             │           │

&#x20;            └─────────────┼───────────┘

&#x20;                          ▼

&#x20;                   Available Capacity

&#x20;                          │

&#x20;                          ▼

&#x20;                   Planned Workload

&#x20;                          │

&#x20;                          ▼

&#x20;                   Actual Time Entry

&#x20;                          │

&#x20;                          ▼

&#x20;                   Approved Time

&#x20;                          │

&#x20;             ┌────────────┼────────────┐

&#x20;             ▼            ▼            ▼

&#x20;         Project       Costing      Analytics

&#x20;         Effort          (007)        (024)

```



The complete operational time lifecycle is:



```text id="x4n7p2"

Work Schedule

&#x20;↓

Capacity Definition

&#x20;↓

Planned Allocation

&#x20;↓

Calendar / Availability

&#x20;↓

Actual Work

&#x20;↓

Time Entry

&#x20;↓

Submission

&#x20;↓

Approval

&#x20;↓

Lock

&#x20;↓

Effort Analysis

&#x20;↓

Capacity / Workload Analysis

&#x20;↓

Costing / Billing Inputs

&#x20;↓

Analytics / Intelligence

```



This establishes `018` as the BusinessOS \*\*authoritative operational time, capacity, and workload layer\*\*, while maintaining strict separation between attendance, scheduled time, actual work, commercial costing, financial records, payroll, employee performance, and analytics.



