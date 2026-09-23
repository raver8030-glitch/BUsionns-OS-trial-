\# 026 — Production Operations and Media Workflow Specification



\*\*Product:\*\* BusinessOS

\*\*Document ID:\*\* 026

\*\*Status:\*\* Detailed Domain Specification

\*\*Depends On:\*\* 000–025

\*\*Primary Domain:\*\* Production Operations and Media Workflow

\*\*Authority Level:\*\* Operational / Production Domain



\---



\# 1. Purpose



The Production Operations and Media Workflow domain provides BusinessOS with a specialized operating layer for businesses that produce:



\* video

\* photography

\* podcasts

\* animation

\* motion graphics

\* 3D

\* social content

\* advertising creatives

\* cinematic productions

\* branded content

\* digital media

\* audio

\* other production deliverables



It extends the generic project/work system with production-specific concepts without replacing it.



The objective is:



> \*\*Provide a complete production lifecycle from creative brief and pre-production through capture, media ingest, post-production, review, approval, export, and delivery while preserving the authoritative boundaries of projects, tasks, resources, files, workflows, documents, and clients.\*\*



\---



\# 2. Architectural Position



`026` is a specialized operational domain built on top of the existing BusinessOS foundation.



```text id="m8q4x7"

Client / Opportunity

&#x20;       │

&#x20;       ▼

Agreement / Package

&#x20;       │

&#x20;       ▼

Project

&#x20;       │

&#x20;       ▼

Production

&#x20;       │

&#x20;┌──────┼────────┐

&#x20;▼      ▼        ▼

Pre-   Shoot    Post

Prod            Production

&#x20;       │

&#x20;       ▼

Media / Assets

&#x20;       │

&#x20;       ▼

Review

&#x20;       │

&#x20;       ▼

Approval

&#x20;       │

&#x20;       ▼

Export

&#x20;       │

&#x20;       ▼

Delivery

```



\---



\# 3. Production Does Not Replace Projects



`005` remains authoritative for projects.



`026` adds production-specific structures associated with a project.



```text id="q7m3x8"

Project

&#x20;  │

&#x20;  └── Production

&#x20;         ├── Shoot

&#x20;         ├── Media

&#x20;         ├── Scenes

&#x20;         ├── Shots

&#x20;         ├── Takes

&#x20;         ├── Post-production

&#x20;         └── Delivery

```



\---



\# 4. What This Domain Owns



`026` owns:



1\. Production records

2\. Production types

3\. Production phases

4\. Production plans

5\. Shoot plans

6\. Shoot days

7\. Scenes

8\. Shots

9\. Takes

10\. Capture records

11\. Media ingest records

12\. Media technical metadata

13\. Media organization

14\. Production-specific asset relationships

15\. Production checklists

16\. Call-sheet data

17\. Crew requirements

18\. Production notes

19\. Production continuity information

20\. Post-production stages

21\. Edit versions/references where production-specific

22\. Render/export jobs where production-specific

23\. Production delivery state

24\. Production health

25\. Production-specific dependencies



Large files themselves remain owned by the file/media storage architecture.



\---



\# 5. What This Domain Does NOT Own



It does not own:



\* project truth → `005`

\* generic tasks → `005`

\* workflow engine → `006`

\* approval authority → `006`

\* services/pricing → `007`

\* formal documents → `008`

\* communication → `009`

\* calendar authority → `010`

\* employees → `011`

\* contractors → `012`

\* resources/equipment → `013`

\* content planning → `014`

\* finance → `015`

\* billing → `016`

\* knowledge → `017`

\* actual time tracking → `018`

\* Agile → `019`

\* custom fields → `020`

\* integrations → `021`

\* realtime collaboration → `022`

\* search → `023`

\* analytics → `024`

\* SaaS billing → `025`

\* client portal → `027`

\* AI → `028`

\* automation → `029`

\* file/object storage → `036`



\---



\# 6. Production Project Types



Possible production types:



\* video production

\* commercial

\* advertisement

\* corporate video

\* documentary

\* music video

\* short film

\* feature production

\* social media production

\* photography

\* product photography

\* food photography

\* podcast

\* livestream

\* animation

\* motion graphics

\* 3D

\* VFX

\* audio production

\* hybrid production

\* custom production



Organizations may configure additional types through controlled configuration.



\---



\# 7. Production Lifecycle



A production may follow:



```text id="x5m8q2"

Project Setup

&#x20;↓

Creative Brief

&#x20;↓

Pre-Production

&#x20;↓

Planning

&#x20;↓

Shoot / Capture

&#x20;↓

Media Ingest

&#x20;↓

Organization / Logging

&#x20;↓

Post-Production

&#x20;↓

Internal Review

&#x20;↓

Client Review

&#x20;↓

Revision

&#x20;↓

Final Approval

&#x20;↓

Export

&#x20;↓

Delivery

&#x20;↓

Archive

```



Not every production requires every stage.



\---



\# 8. Production Record



A production record may include:



\* production ID

\* project

\* production type

\* title

\* objective

\* creative brief

\* owner

\* production lead

\* creative lead

\* status

\* planned dates

\* actual dates

\* locations

\* participants

\* required resources

\* deliverables

\* risk state



\---



\# 9. Production Roles



Potential roles include:



\* producer

\* production manager

\* director

\* creative director

\* director of photography

\* cinematographer

\* camera operator

\* assistant camera

\* sound engineer

\* gaffer

\* lighting technician

\* photographer

\* editor

\* colorist

\* motion designer

\* animator

\* 3D artist

\* VFX artist

\* sound designer

\* production assistant



Roles are production responsibilities, not authorization roles.



\---



\# 10. Crew



Crew may be:



\* employees

\* contractors

\* vendors

\* external collaborators



The authoritative person/relationship remains owned by `011` or `012`.



\---



\# 11. Crew Assignment



Production may reference crew assignments:



```text id="m7q4x8"

Production

&#x20;↓

Crew Assignment

&#x20;↓

Person / External Party

&#x20;↓

Role

&#x20;↓

Dates

&#x20;↓

Responsibilities

```



Actual employment/contractor relationship remains external to `026`.



\---



\# 12. Pre-Production



Pre-production may include:



\* concept

\* creative brief

\* script

\* treatment

\* storyboard

\* shot list

\* moodboard

\* references

\* locations

\* cast

\* crew

\* equipment

\* schedule

\* budget references

\* permissions

\* production checklist



\---



\# 13. Creative Brief



A production brief may define:



\* objective

\* audience

\* message

\* tone

\* visual direction

\* duration

\* aspect ratios

\* platforms

\* deliverables

\* references

\* constraints

\* approval requirements



\---



\# 14. Script



Scripts may be represented as production content or linked documents.



Formal document ownership remains `008` where applicable.



\---



\# 15. Storyboard



A storyboard may contain:



\* scene

\* frame/reference

\* description

\* dialogue

\* action

\* camera direction

\* audio

\* notes



Images/files are stored through `036`.



\---



\# 16. Shot List



A shot list may define:



\* shot number

\* scene

\* shot type

\* framing

\* camera

\* lens

\* movement

\* subject

\* location

\* lighting

\* audio

\* notes

\* priority

\* status



\---



\# 17. Scene



A scene represents a production narrative/structural unit.



A scene may contain:



\* scene number

\* location

\* time

\* description

\* characters/subjects

\* shots

\* continuity notes

\* production status



\---



\# 18. Shot



A shot is a planned capture unit.



Possible fields:



```text id="q8m3x5"

Shot

├── scene

├── shot\_number

├── framing

├── camera

├── lens

├── movement

├── subject

├── audio

├── priority

└── status

```



\---



\# 19. Take



A take represents an actual capture attempt.



A shot may have:



```text id="m5q8x2"

Shot

&#x20;├── Take 01

&#x20;├── Take 02

&#x20;├── Take 03

&#x20;└── Take 04

```



\---



\# 20. Take Metadata



Take records may include:



\* take number

\* timestamp

\* camera

\* operator

\* scene

\* shot

\* duration

\* quality notes

\* technical notes

\* selected/rejected state

\* continuity notes



\---



\# 21. Circle Takes



Organizations may mark:



\* preferred take

\* alternate take

\* technical reject

\* creative reject



This is a production annotation, not final client approval.



\---



\# 22. Production Continuity



Continuity information may include:



\* wardrobe

\* props

\* subject position

\* lighting

\* camera setup

\* scene state

\* take references



\---



\# 23. Call Sheet



Production may generate call-sheet information.



A call sheet may contain:



\* shoot date

\* location

\* crew call times

\* talent call times

\* scene schedule

\* contact information

\* equipment

\* transport

\* notes

\* emergency information



Formal generated document output uses `008`.



\---



\# 24. Call Sheet Versioning



Call sheets may change.



Every published version should remain identifiable.



\---



\# 25. Shoot Day



A shoot day represents a production capture session.



It may include:



\* date

\* location

\* schedule

\* crew

\* equipment

\* scenes

\* shots

\* call sheet

\* notes

\* incidents

\* completion status



\---



\# 26. Calendar Integration



`010` owns the calendar representation.



`026` owns the production meaning.



```text id="x7m4q8"

Shoot Day

&#x20;  │

&#x20;  ▼

Calendar Event

```



Changing the calendar event must not silently mutate production facts unless explicitly commanded.



\---



\# 27. Resource Integration



Equipment comes from `013`.



Examples:



\* camera

\* lens

\* lighting

\* audio equipment

\* tripod

\* gimbal

\* drone

\* workstation



`026` requests/uses resources.



`013` owns resource availability and booking.



\---



\# 28. External Equipment



Rented equipment may involve:



```text id="n8m3q5"

012 Contractor/Vendor

\+

013 Resource

\+

015 Finance

```



Production consumes the resulting resource assignment.



\---



\# 29. Location



Production may associate locations.



Location information may include:



\* address/reference

\* venue

\* scene association

\* access instructions

\* permissions

\* parking

\* constraints



Precise sensitive location data should be protected according to policy.



\---



\# 30. Location Ownership



Production references locations.



It does not automatically become a universal location-management system.



\---



\# 31. Production Checklist



Checklists may include:



\### Camera



\* batteries

\* cards

\* camera body

\* lenses

\* filters



\### Audio



\* recorder

\* microphones

\* batteries

\* cables



\### Lighting



\* fixtures

\* modifiers

\* stands

\* power



\### General



\* releases

\* call sheet

\* backup media

\* transport



Checklists may integrate with workflows and tasks.



\---



\# 32. Checklist Boundary



Checklist execution may create/update tasks through `005` or workflow operations through `006`.



`026` owns production checklist semantics.



\---



\# 33. Media Ingest



After capture:



```text id="m4q8x2"

Camera Media

&#x20;↓

Ingest

&#x20;↓

Verification

&#x20;↓

Backup

&#x20;↓

Catalog

&#x20;↓

Project Association

```



\---



\# 34. Media Ingest Record



An ingest record may contain:



\* source

\* media volume

\* ingest time

\* operator

\* checksum

\* destination

\* verification result

\* project

\* shoot

\* camera

\* status



\---



\# 35. Media Integrity



Where technically supported, ingest should verify media using:



\* checksums

\* file hashes

\* copy verification

\* size comparison



\---



\# 36. Backup Verification



A production workflow should distinguish:



> Media copied



from:



> Media safely verified and backed up.



\---



\# 37. Media Card Handling



A card should not be marked safe to format merely because one copy exists.



The production system should support explicit verification states.



\---



\# 38. Media Storage Boundary



`036` owns:



\* object/file storage

\* uploads

\* large files

\* processing

\* thumbnails

\* previews

\* storage lifecycle



`026` owns production relationships and metadata.



\---



\# 39. Media Asset



A media asset may reference:



\* file

\* production

\* shoot

\* scene

\* shot

\* take

\* camera

\* creator

\* metadata



\---



\# 40. Media Categories



Possible categories:



\* raw

\* proxy

\* audio

\* still

\* graphics

\* project file

\* export

\* master

\* preview

\* reference



\---



\# 41. Proxy Media



Production may associate proxy files with originals.



Example:



```text id="q8m3x5"

Original

&#x20;  ↕

Proxy

```



The underlying files remain `036`.



\---



\# 42. Media Versions



Media deliverables may have versions:



```text id="m5q8x2"

v1

v2

v3

Final

```



Version semantics must remain compatible with `006` review/approval.



\---



\# 43. Edit Versions



An editor may submit:



\* rough cut

\* fine cut

\* client version

\* revision

\* final



These are production/version concepts.



Formal approval is still owned by `006`.



\---



\# 44. Review Integration



```text id="x7m4q8"

Production Asset

&#x20;     │

&#x20;     ▼

Review

&#x20;     │

&#x20;     ▼

Feedback

&#x20;     │

&#x20;     ▼

Revision

&#x20;     │

&#x20;     ▼

Approval

```



`006` owns the authoritative review/approval state.



\---



\# 45. Media Annotations



Where supported, reviews may include:



\* timestamp comments

\* frame comments

\* regions

\* drawing

\* markers



The annotation infrastructure may be implemented through `006`/`036`.



\---



\# 46. Internal Review



Internal review may evaluate:



\* technical quality

\* creative quality

\* brand compliance

\* continuity

\* audio

\* color

\* graphics

\* legal requirements



\---



\# 47. Client Review



Client review is external-facing and must respect `027`.



Client feedback must not automatically equal approval.



\---



\# 48. Approval



Approval remains a distinct state.



```text id="m8q3x5"

Review

≠

Approval

≠

Delivery

```



\---



\# 49. Final Approval



Final approval should identify:



\* approved version

\* approver

\* approval timestamp

\* scope

\* approval evidence



\---



\# 50. Export



Production exports may include:



\* master

\* web

\* social

\* broadcast

\* vertical

\* square

\* horizontal

\* audio-only

\* thumbnail



\---



\# 51. Export Profile



An export profile may define:



\* format

\* codec

\* resolution

\* frame rate

\* bitrate

\* audio settings

\* naming

\* destination



\---



\# 52. Export Job



Export processing may be asynchronous.



```text id="q5m8x2"

Export Requested

&#x20;↓

Queued

&#x20;↓

Processing

&#x20;↓

Validated

&#x20;↓

Available

```



Possible failure states:



\* failed

\* cancelled

\* expired



\---



\# 53. Export Validation



Exports may be validated for:



\* file existence

\* duration

\* resolution

\* codec

\* audio

\* checksum

\* naming

\* required variants



\---



\# 54. Delivery



Delivery may reference:



\* approved asset

\* destination

\* recipient

\* delivery method

\* delivery date

\* delivery status



\---



\# 55. Delivery Boundary



`026` tracks production delivery state.



Communication uses `009`.



Client-facing delivery experience uses `027`.



File storage uses `036`.



\---



\# 56. Production Completion



Production should not automatically be marked complete merely because a file exists.



Completion may require:



\* final approval

\* required exports

\* delivery

\* production checklist completion



The exact project completion state remains `005`.



\---



\# 57. Production Health



Possible health dimensions:



\* schedule

\* budget reference

\* resource readiness

\* media safety

\* review status

\* client approval

\* delivery risk



\---



\# 58. Production Risk



Potential risks:



\* missing equipment

\* unavailable crew

\* location problem

\* incomplete pre-production

\* media backup failure

\* review delay

\* client approval delay

\* export failure

\* delivery failure



\---



\# 59. Risk Ownership



Production may identify production-specific risks.



Enterprise risk management remains a broader governance decision.



\---



\# 60. Production Dependencies



Examples:



```text id="m7q4x8"

Location Confirmed

&#x20;↓

Shoot

&#x20;↓

Media Ingest

&#x20;↓

Edit

&#x20;↓

Review

&#x20;↓

Approval

&#x20;↓

Export

```



Dependencies may reference generic workflow/task dependencies.



\---



\# 61. Production Tasks



Generic tasks remain owned by `005`.



Production may create templates that generate tasks such as:



\* finalize script

\* confirm location

\* prepare camera

\* ingest footage

\* create rough cut

\* color grade

\* sound mix

\* export



\---



\# 62. Production Templates



Organizations may configure reusable production templates.



Example:



```text id="x8m3q5"

Commercial Video Template

├── Pre-production

├── Shoot

├── Ingest

├── Edit

├── Review

├── Revision

├── Color

├── Audio

├── Export

└── Delivery

```



Template execution should use the authoritative project/task/workflow systems.



\---



\# 63. Production Packages



Production may be initiated from services/packages defined by `007`.



Example:



```text id="q5m8x2"

Package

&#x20;↓

Production Project

&#x20;↓

Deliverables

```



Commercial pricing remains `007`.



\---



\# 64. Deliverables



Production may define production-specific deliverable requirements.



`006` remains authoritative for deliverable lifecycle and approval.



\---



\# 65. Content Integration



A production may create assets for content items.



```text id="m8q3x5"

Content Item

&#x20;↓

Production Project

&#x20;↓

Asset

&#x20;↓

Approved Version

&#x20;↓

Publishing

```



`014` owns content planning/publishing intent.



\---



\# 66. Social Production



Production may support:



\* reels

\* shorts

\* stories

\* ads

\* thumbnails

\* platform variants



Publishing remains `014`/`021`.



\---



\# 67. Photography



Photography productions may replace:



```text Scene → Shot → Take

```



with:



```text Shoot

&#x20;↓

Set

&#x20;↓

Capture

&#x20;↓

Select

&#x20;↓

Retouch

&#x20;↓

Review

&#x20;↓

Final

```



The model should support multiple production paradigms.



\---



\# 68. Podcast Production



Podcast production may include:



\* episode

\* recording session

\* speakers

\* audio tracks

\* video tracks

\* transcript

\* edit

\* clips

\* publishing assets



\---



\# 69. Animation



Animation may include:



\* concept

\* storyboard

\* animatic

\* modeling

\* rigging

\* animation

\* lighting

\* rendering

\* compositing

\* review

\* final



\---



\# 70. 3D / VFX



Production may track:



\* assets

\* shots

\* versions

\* renders

\* simulations

\* compositing

\* dependencies



Advanced production-tracking integration may remain future scope.



\---



\# 71. Render Jobs



Render operations may include:



\* input version

\* render profile

\* queue

\* worker

\* output

\* status

\* error

\* retry



Large compute orchestration should remain separable from business workflow.



\---



\# 72. Render Failure



A failed render should not mark the deliverable complete.



\---



\# 73. Production Files



Typical files include:



\* camera originals

\* project files

\* audio

\* graphics

\* proxies

\* exports

\* masters

\* references



`036` provides storage infrastructure.



\---



\# 74. Naming Conventions



Production templates may define naming patterns:



```text id="m5q8x2"

PROJECT\_SCENE\_SHOT\_TAKE\_VERSION

```



Naming is configuration, not identity.



\---



\# 75. Asset Identity



File names must not be treated as unique business identifiers.



Stable BusinessOS IDs remain authoritative.



\---



\# 76. Metadata



Media metadata may include:



\* file metadata

\* EXIF

\* camera metadata

\* lens metadata

\* frame rate

\* resolution

\* codec

\* audio channels

\* duration



Metadata extraction is derived.



\---



\# 77. Metadata Corrections



Production metadata may be corrected without modifying the original media.



Corrections should be traceable.



\---



\# 78. Production Search



`023` may index:



\* productions

\* scenes

\* shots

\* takes

\* media metadata

\* deliverables

\* production notes



\---



\# 79. Production Analytics



`024` may calculate:



\* shoot utilization

\* stage duration

\* review cycles

\* editing turnaround

\* delivery time

\* production throughput

\* media volume

\* resource usage



\---



\# 80. Resource Analytics Boundary



Actual resource availability and booking remain `013`.



Production analytics consumes those records.



\---



\# 81. Time Tracking



Actual work time remains `018`.



Production may associate time entries with:



\* production

\* phase

\* task

\* role



\---



\# 82. Contractor Integration



External crew may be sourced through `012`.



Production references contractor assignments.



\---



\# 83. Calendar Integration



Shoot dates, review sessions, delivery dates, and production milestones may appear on calendars through `010`.



\---



\# 84. Document Integration



Production may generate:



\* call sheets

\* production reports

\* shot reports

\* handover reports

\* delivery documents



`008` owns generated document lifecycle.



\---



\# 85. Communication Integration



Production-related communications may be:



\* client updates

\* crew notifications

\* review notifications

\* delivery messages



`009` owns communication.



\---



\# 86. Automation



`029` may automate:



\* call-sheet reminders

\* media backup alerts

\* review reminders

\* delivery notifications

\* overdue approval alerts



Production-specific conditions remain defined by `026`.



\---



\# 87. AI Assistance



AI may assist with:



\* script analysis

\* shot-list generation

\* production checklist generation

\* call-sheet drafting

\* scene breakdown

\* production summaries

\* edit notes

\* transcript summaries

\* metadata suggestions

\* risk identification

\* content repurposing suggestions



\---



\# 88. AI Boundary



AI must not silently:



\* approve deliverables

\* alter production truth

\* mark media safe

\* delete media

\* declare a shoot complete

\* authorize expensive equipment

\* send contractual commitments



without explicit authorized workflows.



\---



\# 89. AI Media Understanding



Future capabilities may include:



\* scene detection

\* object detection

\* face/person recognition where lawful and explicitly configured

\* speech transcription

\* shot classification

\* duplicate detection

\* visual similarity



Such capabilities require privacy/security review.



\---



\# 90. AI-Generated Metadata



AI-generated metadata should be clearly distinguishable from verified metadata.



Example:



```text id="x7m4q8"

Camera Metadata:

Verified



AI Suggested Tag:

Suggested

```



\---



\# 91. Production Automation



Automation may use triggers such as:



```text id="m8q3x5"

Shoot Completed

Media Ingest Completed

Review Requested

Approval Received

Export Completed

Delivery Completed

```



\---



\# 92. Automation Safety



Automation must not infer successful completion merely from missing failures.



Explicit production state should be the trigger.



\---



\# 93. Realtime Collaboration



`022` may distribute:



\* production updates

\* shot status

\* review activity

\* ingest progress

\* render progress



The production database remains authoritative.



\---



\# 94. Client Portal



`027` may expose:



\* approved deliverables

\* client review

\* production milestones

\* delivery

\* approved content



Internal production information remains hidden.



\---



\# 95. Offline Production



Some production environments may have poor connectivity.



Future `035` may support:



\* offline shot lists

\* checklists

\* notes

\* capture metadata

\* sync



Conflict semantics must remain explicit.



\---



\# 96. Production Synchronization



Offline updates should preserve:



\* event order

\* actor

\* timestamp

\* local operation

\* conflict state



Critical state must not blindly use last-write-wins.



\---



\# 97. Production Audit



Audit important actions:



\* production creation

\* shoot changes

\* media deletion

\* media verification

\* final selection

\* approval

\* export

\* delivery

\* sensitive metadata changes



\---



\# 98. Media Deletion



Deletion of production media must be controlled.



Potential safeguards:



\* permission

\* confirmation

\* retention policy

\* legal hold

\* backup-state awareness

\* audit



\---



\# 99. Media Safety State



Production may represent:



```text id="q5m8x2"

Unverified

Copied

Verified

Backed Up

Archived

Deletion Eligible

```



These states should be carefully defined.



\---



\# 100. Media Recovery



Production should be able to identify where an asset is stored.



Actual recovery mechanics belong to `036`/`041`.



\---



\# 101. Production Archiving



After completion:



\* production metadata remains

\* approved deliverables remain

\* file retention follows policy

\* temporary assets may be archived/deleted according to policy



\---



\# 102. Archival Policy



Archival may depend on:



\* client agreement

\* storage policy

\* legal requirements

\* project type

\* media importance



\---



\# 103. Production Reporting



Production reports may include:



\* shoot report

\* production status

\* media ingest report

\* review report

\* delivery report

\* incident report



Formal documents use `008`.



\---



\# 104. Production Dashboard



A production dashboard may show:



```text id="m7q4x8"

Production Status

Shoot Readiness

Crew

Resources

Scenes

Shots

Media Safety

Post-Production

Reviews

Approvals

Exports

Delivery

Risks

```



\---



\# 105. Shoot Readiness



A production may calculate readiness from:



\* crew

\* equipment

\* location

\* schedule

\* script

\* shot list

\* permissions

\* call sheet



Readiness should expose missing prerequisites rather than merely produce a percentage.



\---



\# 106. Production Completion Criteria



Completion may require:



\* required scenes/shots handled

\* media safely ingested

\* post-production complete

\* required approvals complete

\* exports complete

\* delivery complete



\---



\# 107. Production Data Model — Conceptual



Core entities:



```text id="x8m3q5"

Production

ProductionType

ProductionPhase

ProductionPlan

ProductionChecklist

Shoot

ShootDay

LocationReference

CrewRequirement

CrewAssignment

Scene

Shot

Take

CaptureRecord

MediaIngest

MediaAssetReference

MediaMetadata

ProductionVersion

ProductionNote

ContinuityRecord

CallSheet

CallSheetVersion

PostProductionStage

RenderJob

ExportJob

ExportProfile

ProductionDelivery

ProductionRisk

ProductionHealthSnapshot

```



\---



\# 108. Production



```text id="q5m8x2"

Production

├── id

├── project\_id

├── type

├── title

├── owner

├── creative\_lead

├── production\_lead

├── status

├── planned\_dates

├── actual\_dates

└── configuration

```



\---



\# 109. Shoot



```text id="m8q3x5"

Shoot

├── production\_id

├── shoot\_days

├── locations

├── crew

├── equipment\_refs

├── scenes

├── shot\_list

└── status

```



\---



\# 110. Scene



```text id="x7m4q8"

Scene

├── production\_id

├── scene\_number

├── title

├── location

├── description

├── continuity

└── shots

```



\---



\# 111. Shot



```text id="n5m8q2"

Shot

├── scene\_id

├── shot\_number

├── description

├── camera

├── lens

├── movement

├── priority

├── status

└── takes

```



\---



\# 112. Take



```text id="q8m3x5"

Take

├── shot\_id

├── take\_number

├── captured\_at

├── media\_refs

├── technical\_notes

├── creative\_notes

├── selection\_state

└── metadata

```



\---



\# 113. Media Ingest



```text id="m7q4x8"

MediaIngest

├── shoot\_id

├── source

├── operator

├── started\_at

├── completed\_at

├── verification

├── checksums

├── destination\_refs

└── status

```



\---



\# 114. Export Job



```text id="x5m8q2"

ExportJob

├── production\_id

├── source\_version

├── export\_profile

├── requested\_by

├── status

├── output\_ref

├── validation

└── timestamps

```



\---



\# 115. Production Delivery



```text id="n8q3m5"

ProductionDelivery

├── production\_id

├── deliverable\_id

├── approved\_version

├── destination

├── recipient\_ref

├── status

├── delivered\_at

└── evidence

```



\---



\# 116. Production State



Production-specific states may include:



```text id="m5q8x3"

Draft

Planning

Pre-Production

Ready

Shooting

Ingesting

Post-Production

Internal Review

Client Review

Revision

Approved

Exporting

Ready for Delivery

Delivered

Archived

```



These must remain mapped to the generic project/workflow architecture rather than creating a second universal workflow engine.



\---



\# 117. Production State Mapping



Example:



```text id="q7m4x8"

Production:

Post-Production



Project:

In Progress



Workflow:

Editing

```



Different domains may represent different dimensions of state.



\---



\# 118. Why Multiple States Exist



These are not necessarily contradictory.



\* Project state = overall business work state

\* Production state = production lifecycle

\* Workflow state = configured operational stage

\* Deliverable state = deliverable lifecycle

\* Review state = review lifecycle

\* Approval state = approval decision



\---



\# 119. No Duplicate State Authority



One domain must remain authoritative for each state dimension.



\---



\# 120. Production Permissions



Potential permissions:



\* view production

\* edit production

\* manage shoot

\* manage crew

\* manage shot list

\* manage media

\* verify ingest

\* create export

\* manage delivery

\* view sensitive production data



Authorization uses `003`.



\---



\# 121. High-Risk Production Actions



May require elevated controls:



\* deleting originals

\* changing approved version

\* removing final deliverables

\* modifying sensitive production records

\* confirming media deletion eligibility



\---



\# 122. Production Audit Trail



Important production changes must preserve:



\* actor

\* action

\* timestamp

\* entity

\* previous state

\* new state

\* reason where required

\* correlation ID



\---



\# 123. Performance



Production systems may handle:



\* thousands of media assets

\* large shot lists

\* large projects

\* concurrent editors

\* upload/ingest activity

\* render jobs



Large binary processing must remain asynchronous.



\---



\# 124. Large Media Boundary



Never place large media binaries directly into the transactional database unless explicitly justified for a specific small object.



\---



\# 125. Media Processing



Potential processing pipeline:



```text id="x8m4q2"

Upload / Ingest

&#x20;↓

Validation

&#x20;↓

Metadata Extraction

&#x20;↓

Thumbnail / Proxy

&#x20;↓

Transcode

&#x20;↓

Index

```



`036` owns infrastructure.



\---



\# 126. Search Indexing



Production metadata can be indexed asynchronously.



`023` owns search.



\---



\# 127. Analytics



Production metrics feed `024`.



Examples:



\* shoot utilization

\* stage duration

\* revision frequency

\* media volume

\* turnaround time



\---



\# 128. Business Graph Integration



Production participates in:



```text id="m5q8x3"

Client

&#x20;↓

Agreement

&#x20;↓

Package

&#x20;↓

Project

&#x20;↓

Production

&#x20;↓

Deliverable

&#x20;↓

Approval

&#x20;↓

Delivery

&#x20;↓

Invoice

&#x20;↓

Payment

```



\---



\# 129. Commercial Integration



Production may consume:



\* package deliverables

\* quantities

\* included work

\* overage definitions



from `007`.



It does not calculate commercial price independently.



\---



\# 130. Billing Integration



Production completion/usage may provide inputs to `016`.



Example:



```text id="q8m3x5"

Included:

4 videos



Produced:

6 videos



Potential Overage:

2

```



`007` determines commercial rules.



`016` determines billing execution.



`015` creates financial records.



\---



\# 131. Time Integration



Production work may generate time entries through `018`.



Production itself does not own actual time.



\---



\# 132. Resource Integration



Production requests equipment through `013`.



It does not maintain an independent equipment inventory.



\---



\# 133. HR Integration



Employees come from `011`.



Production may assign production roles.



\---



\# 134. Contractor Integration



External crew comes from `012`.



Production references their assignments.



\---



\# 135. Calendar Integration



Shoot/review/delivery events appear through `010`.



\---



\# 136. Knowledge Integration



Production SOPs may come from `017`.



Example:



> Camera ingest SOP



Production can reference it without duplicating the knowledge source.



\---



\# 137. AI Integration



`028` may use production context to provide:



\* production summaries

\* shot suggestions

\* risk analysis

\* post-production assistance

\* media search

\* content repurposing



\---



\# 138. Automation Integration



`029` may execute production-related workflows.



Example:



```text id="m7q4x8"

Final Approval

&#x20;↓

Create Export Jobs

&#x20;↓

Notify Production Lead

&#x20;↓

Prepare Delivery

```



Every action remains authorized and idempotent.



\---



\# 139. Client Experience



`027` may present:



\* production milestone

\* review

\* approved deliverables

\* delivery status



Client visibility is explicitly configured.



\---



\# 140. Cross-Platform Requirements



\## Desktop



Primary production environment.



Should support:



\* dense production workspace

\* shot lists

\* media management

\* upload/ingest

\* review

\* keyboard shortcuts

\* multi-panel views

\* local filesystem workflows



\## Web



Should support:



\* production management

\* review

\* approvals

\* client collaboration

\* dashboards



\## Android



Should support:



\* shoot-day checklists

\* call sheets

\* quick updates

\* approvals

\* notifications

\* mobile review

\* capture metadata

\* offline-capable production notes where supported



\---



\# 141. Desktop File Integration



The desktop application may require controlled local filesystem access for:



\* ingest

\* upload

\* file selection

\* export

\* local project files



Such access must follow platform security boundaries.



\---



\# 142. Offline Shoot Mode



Future offline support may allow:



\* shot list

\* scene notes

\* take metadata

\* checklist

\* production status



Synchronization must be handled through `035`.



\---



\# 143. Testing Strategy



\## Unit Tests



\* production states

\* scene/shot relationships

\* take logic

\* ingest state

\* export validation

\* delivery state



\## Integration Tests



\* project

\* resources

\* calendar

\* files

\* reviews

\* approvals

\* client portal

\* billing inputs



\## Media Tests



\* checksum

\* metadata extraction

\* proxy generation

\* upload interruption

\* duplicate detection



\## Reliability Tests



\* ingest interruption

\* export failure

\* worker restart

\* network failure

\* duplicate events



\## Security Tests



\* client isolation

\* crew access

\* media access

\* deletion permissions

\* approved-version protection



\---



\# 144. Definition of Ready



A production feature is ready when:



\* production ownership is defined

\* project relationship is defined

\* workflow relationship is defined

\* file relationship is defined

\* resource relationship is defined

\* review/approval relationship is defined

\* client visibility is defined

\* permission requirements are defined

\* failure behavior is defined

\* audit requirements are defined



\---



\# 145. Definition of Done



A production feature is complete when:



\* production lifecycle works

\* project linkage works

\* shoot planning works

\* crew/resource references work

\* media ingestion is reliable

\* versioning works

\* review/approval integrates correctly

\* export/delivery works

\* client visibility is safe

\* search indexing works

\* analytics integration works

\* automation integration works

\* AI boundaries are enforced

\* desktop/web/mobile behavior is defined

\* audit/security tests pass



\---



\# 146. Recommended Vertical Slices



\## Slice 1 — Production Foundation



\* production

\* types

\* lifecycle

\* project relationship



\## Slice 2 — Pre-Production



\* brief

\* script

\* storyboard

\* shot list

\* scenes



\## Slice 3 — Shoot Management



\* shoot days

\* crew

\* locations

\* equipment references

\* call sheets



\## Slice 4 — Capture



\* shots

\* takes

\* capture metadata

\* selection



\## Slice 5 — Media Ingest



\* ingest

\* verification

\* metadata

\* storage integration



\## Slice 6 — Post-Production



\* versions

\* stages

\* exports

\* render jobs



\## Slice 7 — Review / Approval



Integrate `006`.



\## Slice 8 — Delivery



Integrate `027`, `009`, and `036`.



\## Slice 9 — Intelligence



Integrate:



\* search

\* analytics

\* AI

\* automation



\---



\# 147. Open Architectural Decisions



1\. Exact production data model.

2\. Production template architecture.

3\. Shot/scene hierarchy flexibility.

4\. Media metadata schema.

5\. Media ingest implementation.

6\. Checksum strategy.

7\. Proxy-generation technology.

8\. Transcoding architecture.

9\. Render-job architecture.

10\. Local filesystem integration.

11\. Desktop media workflow architecture.

12\. Camera/media-card ingest integrations.

13\. Advanced review/annotation architecture.

14\. Production scheduling model.

15\. Location management depth.

16\. Call-sheet generation architecture.

17\. Offline shoot mode.

18\. AI media understanding.

19\. Speech/transcription architecture.

20\. Visual semantic search.

21\. Face/person recognition policy.

22\. Media retention policy.

23\. Original-media deletion policy.

24\. Production backup strategy.

25\. High-volume production scalability.

26\. External production-system integrations.



\---



\# 148. Architectural Invariants



The following are non-negotiable:



1\. `005` remains authoritative for project truth.

2\. `026` adds production semantics; it does not replace project management.

3\. `006` remains authoritative for review and approval.

4\. `036` owns large file/media storage infrastructure.

5\. `013` owns equipment/resource availability and booking.

6\. `011` owns employees.

7\. `012` owns contractors/vendors.

8\. `018` owns actual work time.

9\. `010` owns calendar representation.

10\. `007` owns commercial pricing/costing.

11\. `015` owns financial records.

12\. `016` owns recurring billing orchestration.

13\. `014` owns content publishing intent.

14\. `027` owns client-facing portal experience.

15\. `023` owns search.

16\. `024` owns analytics.

17\. `028` owns AI behavior.

18\. `029` owns automation orchestration.

19\. Production state must not create a second universal workflow engine.

20\. File names are not authoritative identifiers.

21\. Media storage and production metadata remain separate.

22\. Media ingestion must support integrity verification.

23\. Copying media does not automatically mean it is safely backed up.

24\. AI-generated metadata must be distinguishable from verified metadata.

25\. AI cannot silently approve, delete, or finalize production records.

26\. Critical media deletion is controlled and audited.

27\. Final approval identifies the approved version.

28\. Export does not equal approval.

29\. Delivery does not automatically equal project completion.

30\. Client visibility is explicitly controlled.

31\. Production automation uses authorized commands.

32\. Production analytics remains derived.

33\. Realtime updates do not become authoritative production state.

34\. Offline conflict handling must not blindly overwrite critical production facts.

35\. Large binary data does not belong in the transactional database by default.



\---



\# 149. Dependency Summary



```text id="r8m4q3"

026 Production Operations / Media Workflow

│

├── 003 Authorization

├── 005 Projects / Work

├── 006 Workflow / Reviews / Approvals

├── 007 Services / Commercial

├── 008 Documents

├── 009 Communication

├── 010 Calendar

├── 011 HR

├── 012 Contractors

├── 013 Resources

├── 014 Content

├── 015 Finance

├── 016 Automated Billing

├── 017 Knowledge

├── 018 Time / Capacity

├── 020 Custom Fields

├── 021 Integrations

├── 022 Realtime

├── 023 Search

├── 024 Analytics

├── 027 Client Portal

├── 028 AI

├── 029 Automation

├── 030 Administration

├── 035 Offline / Sync

├── 036 File / Media Storage

└── 041 Data Recovery

```



\---



\# 150. Final Production Architecture



```text id="m5q8x2"

&#x20;                    Client / Agreement

&#x20;                           │

&#x20;                           ▼

&#x20;                        Project

&#x20;                           │

&#x20;                           ▼

&#x20;                      Production

&#x20;                           │

&#x20;                ┌──────────┴──────────┐

&#x20;                ▼                     ▼

&#x20;          Pre-Production            Planning

&#x20;                │                     │

&#x20;                └──────────┬──────────┘

&#x20;                           ▼

&#x20;                         Shoot

&#x20;                           │

&#x20;                ┌──────────┴──────────┐

&#x20;                ▼                     ▼

&#x20;             Scenes                Resources

&#x20;                │                     │

&#x20;                ▼                     ▼

&#x20;              Shots                 Crew

&#x20;                │

&#x20;                ▼

&#x20;              Takes

&#x20;                │

&#x20;                ▼

&#x20;            Media Ingest

&#x20;                │

&#x20;                ▼

&#x20;         Verified Media

&#x20;                │

&#x20;                ▼

&#x20;         Post-Production

&#x20;                │

&#x20;                ▼

&#x20;             Version

&#x20;                │

&#x20;                ▼

&#x20;             Review

&#x20;                │

&#x20;                ▼

&#x20;            Approval

&#x20;                │

&#x20;                ▼

&#x20;             Export

&#x20;                │

&#x20;                ▼

&#x20;             Delivery

&#x20;                │

&#x20;                ▼

&#x20;             Archive

```



The production lifecycle therefore becomes:



```text id="q7m4x8"

Commercial Context

&#x20;↓

Project

&#x20;↓

Production Plan

&#x20;↓

Pre-Production

&#x20;↓

Shoot

&#x20;↓

Capture

&#x20;↓

Media Safety

&#x20;↓

Post-Production

&#x20;↓

Review

&#x20;↓

Approval

&#x20;↓

Export

&#x20;↓

Delivery

&#x20;↓

Archive

```



The central architectural rule is:



> \*\*BusinessOS production management must understand the realities of real-world media production without becoming a separate project-management, file-storage, resource-management, review, finance, or communication system.\*\*



`026` is the specialized production layer connecting those authoritative domains into one coherent production lifecycle.



