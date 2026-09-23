\# 014 — Content Planning, Campaigns and Publishing Specification



\*\*Product:\*\* BusinessOS

\*\*Document ID:\*\* 014

\*\*Status:\*\* Detailed Domain Specification

\*\*Depends On:\*\* 000–013

\*\*Primary Domain:\*\* Content Planning, Campaigns and Publishing

\*\*Authority Level:\*\* Domain Specification



\---



\## 1. Purpose



The Content Planning, Campaigns and Publishing domain manages the planning, organization, production coordination, approval, scheduling, and publishing lifecycle of business content.



It is intended for production houses, agencies, freelancers, marketing teams, and other service businesses that create and manage content for clients or internal brands.



The domain must support:



\* content calendars

\* campaigns

\* content items

\* content ideas

\* briefs

\* platforms

\* channels

\* content formats

\* captions and copy

\* creative assets

\* content production status

\* review and approval coordination

\* publishing schedules

\* publishing outcomes

\* campaign performance references

\* recurring content programs

\* client-facing content visibility

\* internal content operations

\* AI-assisted planning and drafting

\* automation around predictable content operations



The domain must integrate with projects, workflows, deliverables, files, reviews, approvals, communication, calendar, CRM, analytics, AI, and automation without taking ownership of those domains.



\---



\# 2. Architectural Position



Content Planning is a \*\*business domain\*\*, not merely a calendar feature.



A content item can exist independently as an idea or planned item and can later become connected to:



\* a client

\* a campaign

\* a project

\* a task

\* a deliverable

\* one or more files/assets

\* a review

\* an approval

\* a publishing event

\* an external publishing platform

\* analytics data



The domain therefore acts as a coordination layer around the content lifecycle.



\### Core principle



> Content Planning owns the content planning and publishing intent; other domains own the underlying business facts they are authoritative for.



For example:



\* Project owns project state.

\* Task Management owns task state.

\* Workflow owns workflow execution.

\* Review/Approval owns review and approval state.

\* File domain owns file metadata and storage relationships.

\* Calendar owns calendar events.

\* Communication owns messages and notifications.

\* Analytics owns analytical measurements.

\* Integrations owns external-system connections.

\* Content Planning owns the content plan and publishing intent.



\---



\# 3. What This Domain Owns



The domain owns:



1\. Content Ideas

2\. Content Items

3\. Content Briefs

4\. Campaigns

5\. Content Programs

6\. Content Categories

7\. Content Formats

8\. Content Channels

9\. Content Platform Definitions

10\. Content Planning Metadata

11\. Content Calendar Intent

12\. Publishing Plans

13\. Publishing Schedules

14\. Content Dependencies

15\. Content-to-business-entity relationships

16\. Content production coordination metadata

17\. Publishing status

18\. Publishing attempts at the content-planning level

19\. Content planning templates

20\. Content planning rules

21\. Content-specific planning history



\---



\# 4. What This Domain Does NOT Own



This boundary is mandatory.



\### It does not own:



\* Projects → `005`

\* Tasks → `005`

\* Workflow execution → `006`

\* Reviews → `006`

\* Approvals → `006`

\* Deliverables → `006`

\* Services/packages → `007`

\* Commercial calculations → `007`

\* Documents → `008`

\* Communication → `009`

\* Calendar infrastructure → `010`

\* HR records → `011`

\* Contractors/vendors → `012`

\* Resources/equipment → `013`

\* Financial transactions → `015`

\* Automated billing → `016`

\* Time tracking → `018`

\* Capacity/workload calculations → `018`

\* External integrations → `021`

\* Search → `023`

\* Analytics → `024`

\* Production/media processing → `026`

\* Client portal presentation → `027`

\* AI platform → `028`

\* Automation engine → `029`



Content Planning may reference or orchestrate these capabilities but must not duplicate their authoritative state.



\---



\# 5. Core Business Concepts



\## 5.1 Content Idea



An uncommitted idea for future content.



Examples:



\* "Behind the scenes of the studio"

\* "Client testimonial reel"

\* "Festival campaign"

\* "Educational SEO video"

\* "Product photography carousel"



An idea can later become a planned content item.



\---



\## 5.2 Content Item



The primary planning entity.



A Content Item represents a specific piece of content or a planned content output.



Examples:



\* Instagram Reel

\* YouTube video

\* LinkedIn post

\* Blog article

\* Short-form video

\* Story

\* Carousel

\* Podcast episode

\* Email campaign content

\* Advertisement creative

\* Product photography post



A Content Item may have:



\* title

\* description

\* brief

\* objective

\* audience

\* content type

\* format

\* platform

\* campaign

\* client

\* project

\* owner

\* planned date

\* publishing date

\* status

\* priority

\* tags

\* CTA

\* caption

\* copy

\* hashtags

\* assets

\* versions

\* approval references

\* publishing information



\---



\# 6. Content Lifecycle



A default lifecycle should be configurable.



Recommended baseline:



```text

Idea

&#x20; ↓

Planned

&#x20; ↓

Briefed

&#x20; ↓

In Production

&#x20; ↓

Internal Review

&#x20; ↓

Client Review

&#x20; ↓

Changes Requested

&#x20; ↓

Approved

&#x20; ↓

Scheduled

&#x20; ↓

Publishing

&#x20; ↓

Published

&#x20; ↓

Monitoring

&#x20; ↓

Archived

```



Not every content item requires every state.



For example:



```text

Idea

→ Planned

→ Approved

→ Scheduled

→ Published

```



may be sufficient for a simple static post.



The lifecycle must therefore support configurable workflows through `006` and automation through `029`.



\---



\# 7. Campaigns



A Campaign groups content around a common business objective.



A campaign may include:



\* campaign name

\* description

\* client/brand

\* objective

\* audience

\* start date

\* end date

\* budget reference

\* campaign owner

\* status

\* platforms

\* content items

\* projects

\* deliverables

\* messaging themes

\* keywords

\* CTAs

\* tags

\* campaign brief

\* approval requirements

\* reporting references



Campaigns may represent:



\* product launches

\* festivals

\* seasonal promotions

\* brand awareness campaigns

\* lead-generation campaigns

\* social campaigns

\* recruitment campaigns

\* event campaigns

\* client marketing campaigns

\* internal marketing initiatives



\---



\# 8. Campaign Lifecycle



Recommended lifecycle:



```text

Draft

→ Planning

→ Active

→ Paused

→ Completed

→ Archived

```



Cancellation must remain distinguishable from normal completion.



A campaign must preserve historical state.



\---



\# 9. Content Programs



A Content Program represents an ongoing recurring content operation.



Examples:



\* Weekly Instagram Reels

\* Monthly YouTube episodes

\* Daily social posts

\* Weekly podcast

\* Monthly client content package



A program can define:



\* cadence

\* target volume

\* platforms

\* content types

\* responsible team

\* campaign relationship

\* service/package relationship

\* recurring templates

\* approval rules

\* publishing windows



Programs can generate planned content items through controlled automation.



\---



\# 10. Content Calendar



The content calendar provides a specialized planning view over content items.



It must support:



\* month

\* week

\* day

\* timeline

\* list

\* board

\* campaign view

\* platform view

\* client view

\* team view

\* status view



The calendar representation is derived from content scheduling information.



Actual calendar events belong to `010`.



\---



\# 11. Content Dates



A content item may contain multiple distinct dates:



\* idea date

\* created date

\* brief date

\* planned production date

\* shoot date

\* editing deadline

\* internal review date

\* client review date

\* approval date

\* scheduled publishing date

\* actual publishing date

\* completion date



These dates must not be collapsed into one generic date field.



\---



\# 12. Platforms



BusinessOS must support configurable platform definitions.



Examples:



\* Instagram

\* YouTube

\* Facebook

\* LinkedIn

\* TikTok

\* X

\* Pinterest

\* Website

\* Blog

\* Email

\* Google Business Profile



The system must not hard-code the assumption that every platform behaves identically.



Each platform may define:



\* supported content types

\* publishing capabilities

\* media requirements

\* text limits

\* aspect-ratio requirements

\* scheduling capability

\* external integration availability

\* account requirements

\* metadata requirements



\---



\# 13. Channels



A channel represents a specific publishing destination.



Example:



```text

Platform: YouTube

Channel: PRIME Studio YouTube

```



or:



```text

Platform: Instagram

Account: Client Brand Instagram

```



A channel belongs to an organization-controlled or authorized external account context.



Publishing permissions must be independently authorized.



\---



\# 14. Content Formats



Formats should be configurable.



Examples:



\* Reel

\* Short

\* Long-form video

\* Carousel

\* Static image

\* Story

\* Blog

\* Podcast

\* Newsletter

\* Advertisement

\* Case study

\* Testimonial



Format definitions may include:



\* supported platforms

\* recommended dimensions

\* duration constraints

\* text requirements

\* asset requirements

\* approval requirements

\* production requirements



\---



\# 15. Content Briefs



A Content Brief captures the intended creative/business outcome.



Possible fields:



\* objective

\* target audience

\* key message

\* tone

\* hook

\* CTA

\* talking points

\* references

\* keywords

\* mandatory claims

\* prohibited claims

\* visual direction

\* audio direction

\* brand requirements

\* platform-specific requirements



Briefs must support versioning.



\---



\# 16. Content Copy



Content may contain multiple copy components:



\* headline

\* hook

\* caption

\* description

\* body copy

\* CTA

\* hashtags

\* keywords

\* alt text

\* thumbnail title

\* metadata



Platform-specific variants should be supported.



Example:



```text

Content Item

&#x20;├── Instagram Caption

&#x20;├── YouTube Description

&#x20;├── LinkedIn Copy

&#x20;└── Website Copy

```



One piece of content does not necessarily mean one piece of copy.



\---



\# 17. Content Assets



Content items may reference:



\* images

\* videos

\* audio

\* thumbnails

\* logos

\* documents

\* graphics

\* generated assets

\* external links



Actual files are owned by the file/media architecture.



Content Planning stores relationships and semantic roles.



Example:



```text

Content Item

&#x20;├── Primary Video

&#x20;├── Thumbnail

&#x20;├── Caption Graphic

&#x20;├── Logo

&#x20;└── Reference Document

```



\---



\# 18. Asset Roles



Asset relationships should support semantic roles such as:



\* source

\* raw footage

\* working asset

\* final asset

\* thumbnail

\* cover

\* attachment

\* reference

\* supporting asset

\* published asset



This allows downstream workflows to understand how an asset is being used.



\---



\# 19. Content → Project Relationship



A content item may originate from or connect to a project.



Example:



```text

Client

&#x20;↓

Campaign

&#x20;↓

Content Item

&#x20;↓

Production Project

&#x20;↓

Deliverable

&#x20;↓

Approved Version

&#x20;↓

Publishing

```



Content Planning must not duplicate project status.



If the production project is delayed, the content planning interface should consume the authoritative project state.



\---



\# 20. Content → Task Relationship



Content items may generate or reference tasks.



Example:



```text

Content Item

&#x20;├── Write Script

&#x20;├── Shoot

&#x20;├── Edit

&#x20;├── Create Thumbnail

&#x20;├── Review

&#x20;└── Schedule

```



Tasks belong to `005`.



Content Planning stores relationships and planning context.



\---



\# 21. Content → Deliverable Relationship



A content item may correspond to one or more deliverables.



Example:



```text

Campaign

&#x20;  ↓

Content Item

&#x20;  ↓

Deliverable

&#x20;  ↓

Version

&#x20;  ↓

Approval

&#x20;  ↓

Publish

```



Deliverable ownership remains with `006`.



\---



\# 22. Content Review and Approval



Content may require:



\* internal review

\* creative review

\* technical review

\* client review

\* legal/compliance review

\* brand approval



These states must reference `006`.



Content Planning must not create a parallel approval engine.



\---



\# 23. Approval Gate



Publishing should normally require the appropriate approval state.



Example:



```text

Draft

&#x20;↓

Production

&#x20;↓

Review

&#x20;↓

Approval

&#x20;↓

Schedule

&#x20;↓

Publish

```



A user must not be able to bypass required approval merely by changing the content status manually.



\---



\# 24. Publishing



Publishing represents the intended or actual release of content to an external destination.



Publishing states may include:



```text

Not Scheduled

Scheduled

Preparing

Publishing

Published

Failed

Cancelled

```



Publishing execution may depend on `021 Integrations`.



\---



\# 25. Publishing Attempts



Publishing must support multiple attempts.



Example:



```text

Attempt 1 → Failed

Attempt 2 → Failed

Attempt 3 → Published

```



Each attempt should record:



\* provider

\* channel

\* timestamp

\* request reference

\* response reference where appropriate

\* status

\* failure category

\* retryability

\* correlation ID



Secrets and sensitive provider responses must never be exposed unnecessarily.



\---



\# 26. External Publishing



BusinessOS may eventually publish directly through supported platform APIs.



The architecture must support:



```text

Content Item

→ Approved Version

→ Publishing Plan

→ External Integration

→ Provider

→ Publishing Attempt

→ Result

```



Direct publishing is optional per platform.



A platform without supported API publishing may instead use:



```text

Scheduled

→ Notification

→ Manual Publish

→ User Confirms Published

```



The domain must support both.



\---



\# 27. Scheduled Publishing



A scheduled publishing record should contain:



\* target platform/channel

\* scheduled timestamp

\* timezone

\* selected content version

\* selected assets

\* copy variant

\* publishing configuration

\* approval state

\* creator

\* scheduler

\* execution status



The schedule must reference a specific approved version where required.



If the content changes after scheduling, the system must not silently publish an unintended newer version.



\---



\# 28. Version Safety



Example:



```text

Version 1 → Approved

Version 2 → Changes Requested

Version 3 → Approved

```



A scheduled publication must explicitly identify which version it intends to publish.



Publishing:



```text

Content Version 3

```



must not silently become:



```text

Content Version 4

```



without a controlled rescheduling/update process.



\---



\# 29. Multi-Platform Content



A single conceptual campaign may distribute content across multiple platforms.



Example:



```text

Campaign

&#x20;└── Content Concept

&#x20;     ├── Instagram Version

&#x20;     ├── YouTube Version

&#x20;     ├── LinkedIn Version

&#x20;     └── Facebook Version

```



The system should distinguish:



\* shared content concept

\* platform-specific content instance

\* platform-specific copy

\* platform-specific assets

\* platform-specific schedule

\* platform-specific publishing result



This prevents forcing incompatible platforms into a single rigid record.



\---



\# 30. Content Dependencies



Content items may depend on:



\* another content item

\* campaign milestone

\* project completion

\* approval

\* asset availability

\* event date

\* product launch

\* external publishing dependency



Examples:



```text

Trailer

&#x20;  ↓

Main Video

&#x20;  ↓

Short Clips

```



or:



```text

Product Launch

&#x20;  ↓

Announcement

&#x20;  ↓

Promotional Content

&#x20;  ↓

Follow-up Content

```



Dependencies must be explicit.



\---



\# 31. Content Templates



Templates should support recurring content patterns.



Examples:



\* weekly reel

\* client testimonial

\* product post

\* podcast episode

\* event announcement



Templates may contain:



\* default format

\* platform

\* content fields

\* checklist

\* task template references

\* workflow reference

\* approval requirements

\* publishing rules

\* copy structure

\* asset requirements



Templates must be versioned.



Existing content must preserve the template version from which it was created.



\---



\# 32. Content Intake



Content can originate from:



\* manual creation

\* client request

\* CRM opportunity

\* campaign

\* project

\* recurring program

\* task

\* automation

\* AI suggestion

\* imported data

\* external integration



Origin metadata should be preserved.



Example:



```text

origin\_type = client\_request

origin\_id = ...

created\_by = ...

```



\---



\# 33. Content Provenance



BusinessOS must preserve:



\* who created the idea

\* who converted it into planned content

\* who changed the brief

\* who created the project

\* who created the deliverable

\* who approved the version

\* who scheduled publication

\* who published it

\* which integration published it



This contributes to the BusinessOS Business Graph.



\---



\# 34. Content Ownership



Content ownership should distinguish:



\* content creator

\* content owner

\* campaign owner

\* client/account owner

\* project owner

\* production owner

\* publishing owner



These are not automatically the same person.



\---



\# 35. Content Status vs Production Status



The system must not collapse planning state and production state.



Example:



```text

Content Status:

Scheduled



Production Project:

Completed



Publishing:

Pending

```



or:



```text

Content Status:

Planned



Production Project:

In Progress

```



These represent different dimensions.



\---



\# 36. Content Priority



Support configurable priorities:



```text

Low

Normal

High

Urgent

```



Organizations may configure additional priority schemes.



Priority should support:



\* campaigns

\* client importance

\* deadlines

\* business impact



\---



\# 37. Content Tags and Categories



Content should support:



\* categories

\* topics

\* campaigns

\* keywords

\* hashtags

\* custom tags

\* audience segments

\* content pillars



Tags must remain searchable.



\---



\# 38. Content Pillars



Organizations may define strategic content pillars.



Examples:



\* Education

\* Entertainment

\* Brand

\* Product

\* Testimonials

\* Behind the Scenes

\* Thought Leadership



Pillars can be used for planning and analytics.



\---



\# 39. Content Goals



Possible goals:



\* awareness

\* engagement

\* lead generation

\* conversion

\* retention

\* education

\* recruitment

\* authority

\* announcement

\* community building



Goals should be structured values rather than relying entirely on free text.



\---



\# 40. Client Content Operations



Client-specific content may support:



\* client visibility

\* client comments

\* client review

\* client approval

\* client publishing schedule visibility

\* client assets

\* client-provided references



Internal planning metadata must remain hidden.



Clients must not automatically see:



\* internal costs

\* employee workload

\* internal notes

\* internal review commentary

\* internal performance evaluations

\* internal margins

\* internal commercial rules



Client visibility is governed by `003` and presented through `027`.



\---



\# 41. Internal Content



The same domain must support internal content.



Examples:



\* company social media

\* recruitment content

\* internal announcements

\* employer branding

\* educational material

\* internal campaigns



Client association is therefore optional.



\---



\# 42. Recurring Content



Recurring content may be generated from:



\* content programs

\* templates

\* recurring tasks

\* campaign rules

\* automation



Example:



```text

Every Monday

→ Create weekly reel planning item

→ Assign content owner

→ Create production task

→ Set review deadline

→ Schedule publishing window

```



This should be implemented through `029`, not by embedding an independent automation engine inside Content Planning.



\---



\# 43. Content Scheduling Rules



Organizations may define rules such as:



\* preferred publishing windows

\* platform-specific publishing times

\* blackout periods

\* campaign windows

\* holiday exceptions

\* client approval lead times

\* minimum production lead time



Rules may influence suggestions and automation.



They must not silently override explicit user decisions unless explicitly configured.



\---



\# 44. Calendar Integration



Content publishing schedules may produce calendar representations.



Example:



```text

Content Item

&#x20;↓

Publishing Schedule

&#x20;↓

Calendar Event

```



Calendar infrastructure remains owned by `010`.



If a user moves the calendar event, BusinessOS must use the appropriate Content Planning command to change the underlying publishing schedule.



The calendar must not become a second source of truth.



\---



\# 45. Notifications



Content-related notifications may include:



\* content assigned

\* brief completed

\* production due

\* review requested

\* client review requested

\* approval received

\* changes requested

\* publishing approaching

\* publishing failed

\* publishing completed



Notification delivery belongs to `009`.



\---



\# 46. Communication Integration



Content Planning may generate:



\* client review requests

\* approval requests

\* publishing confirmations

\* campaign updates

\* internal reminders



Actual messages belong to `009`.



\---



\# 47. Search



Content must be searchable by:



\* title

\* description

\* campaign

\* client

\* platform

\* channel

\* content type

\* format

\* status

\* owner

\* tags

\* keywords

\* caption

\* project

\* deliverable

\* publishing date



Search infrastructure belongs to `023`.



\---



\# 48. Analytics Integration



Content Planning should expose structured events and dimensions to `024`.



Potential analytics:



\* content volume

\* content throughput

\* planned vs published

\* publishing delays

\* approval cycle time

\* revision frequency

\* platform distribution

\* campaign output

\* content pillar distribution

\* content production lead time

\* missed publishing schedules

\* publishing failures



Performance metrics such as impressions, reach, engagement, conversions, and revenue attribution should come from appropriate analytics/integration sources rather than being invented by Content Planning.



\---



\# 49. Content Performance



A content item may reference external performance measurements.



Example:



```text

Content

&#x20;↓

Published Asset

&#x20;↓

External Platform

&#x20;↓

Metrics

```



Metrics should be time-series where appropriate.



Historical measurements must not be overwritten without preserving measurement time and source.



\---



\# 50. Campaign Performance



Campaign analytics may eventually include:



\* planned content count

\* published content count

\* completion rate

\* publishing punctuality

\* engagement

\* leads

\* conversions

\* revenue attribution

\* cost

\* ROI



Financial calculations belong to the appropriate finance/commercial domains.



\---



\# 51. AI Assistance



AI may assist with:



\* content ideas

\* topic suggestions

\* content calendars

\* campaign structures

\* briefs

\* hooks

\* captions

\* scripts

\* hashtags

\* SEO keywords

\* platform adaptation

\* repurposing suggestions

\* content gap analysis

\* scheduling suggestions

\* campaign summaries

\* performance explanations

\* risk detection



AI behavior belongs to `028`.



\---



\# 52. AI Safety



AI-generated content must be distinguishable from human-approved content.



AI must not silently:



\* publish content

\* bypass approval

\* alter contractual commitments

\* modify client-authoritative content without permission

\* expose private client/internal data

\* invent factual business claims

\* invent financial values



AI-generated copy may be a draft.



The system should preserve:



```text

Generated by AI

Reviewed by Human

Approved by Human

Published

```



where applicable.



\---



\# 53. AI Content Context



The AI Assistant may use authorized:



\* client information

\* campaign information

\* content history

\* approved brand guidelines

\* previous content

\* project information

\* platform rules

\* documents

\* analytics



Permission checks must happen before retrieval.



AI must not gain access simply because content is being discussed.



\---



\# 54. Automation



Automation may perform controlled operations such as:



```text

Campaign Created

→ Generate Planning Checklist

```



```text

Content Approved

→ Schedule Publishing

```



```text

Publishing Failed

→ Notify Owner

→ Create Follow-up Task

```



```text

New Client Package

→ Generate Monthly Content Plan

```



Automation belongs to `029`.



\---



\# 55. Automation Idempotency



Repeated events must not create duplicate content.



Example:



```text

Monthly Content Trigger

```



must not generate two identical monthly plans because the trigger was delivered twice.



Automation execution must use:



\* idempotency keys

\* execution records

\* correlation IDs

\* unique business constraints where appropriate



\---



\# 56. Content Planning APIs



Conceptual query operations:



```text

GetContentItem

ListContentItems

SearchContent

GetCampaign

ListCampaigns

GetContentCalendar

GetPublishingSchedule

GetContentVersions

GetContentDependencies

GetContentPerformanceSummary

```



Conceptual command operations:



```text

CreateContentIdea

ConvertIdeaToContent

CreateContentItem

UpdateContentItem

CreateBrief

UpdateBrief

CreateCampaign

UpdateCampaign

CreateContentProgram

ScheduleContent

RescheduleContent

CancelPublishing

MarkPublished

RetryPublishing

ArchiveContent

CreateContentVersion

SetPublishingVersion

```



All commands must enforce authorization and business validation.



\---



\# 57. API Query Principles



Queries must support filters such as:



```text

client\_id

campaign\_id

project\_id

platform\_id

channel\_id

status

owner\_id

content\_type

date\_range

tag

priority

```



Pagination, sorting, filtering, and authorization must be server-side.



\---



\# 58. Command Validation



Before scheduling content:



```text

Validate User Permission

&#x20;       ↓

Validate Content State

&#x20;       ↓

Validate Version

&#x20;       ↓

Validate Approval

&#x20;       ↓

Validate Platform

&#x20;       ↓

Validate Channel

&#x20;       ↓

Validate Required Assets

&#x20;       ↓

Validate Publishing Rules

&#x20;       ↓

Create Schedule

```



The UI must not be treated as the security boundary.



\---



\# 59. Events



Potential domain events:



```text

ContentIdeaCreated

ContentCreated

ContentUpdated

ContentBriefUpdated

CampaignCreated

CampaignActivated

ContentScheduled

ContentRescheduled

ContentApprovalRequired

ContentApproved

ContentChangesRequested

PublishingStarted

PublishingSucceeded

PublishingFailed

ContentPublished

ContentArchived

```



Events must contain enough metadata for downstream processing without embedding large payloads unnecessarily.



\---



\# 60. Audit



Audit records should capture sensitive or meaningful operations such as:



\* content creation

\* ownership changes

\* campaign changes

\* brief changes

\* approval-related changes

\* schedule changes

\* publishing

\* publishing cancellation

\* publishing retry

\* external account/channel changes

\* AI-generated actions

\* automated actions

\* client-visible changes



Audit belongs to the platform-wide audit architecture but Content Planning must emit appropriate audit events.



\---



\# 61. Permissions



Potential permission identifiers:



```text

content.view

content.create

content.update

content.delete

content.archive

content.schedule

content.publish

content.cancel\_publish

content.manage\_campaign

content.manage\_program

content.manage\_templates

content.manage\_channels

content.view\_analytics

content.manage\_client\_content

content.approve

```



Approval permissions must ultimately be governed through `003` and `006`.



\---



\# 62. Sensitive Operations



The following may require elevated permissions:



\* publishing

\* publishing to client accounts

\* changing publishing channels

\* deleting published records

\* bulk scheduling

\* bulk publishing

\* changing campaign ownership

\* changing client-visible content

\* connecting publishing accounts



High-risk operations must be auditable.



\---



\# 63. Bulk Operations



Support controlled bulk operations:



\* bulk assign

\* bulk reschedule

\* bulk tag

\* bulk move campaign

\* bulk approve where allowed

\* bulk archive

\* bulk publish where explicitly permitted



Bulk publishing must perform per-item validation.



One invalid item must not necessarily corrupt or partially misrepresent the entire batch.



\---



\# 64. Concurrency



Concurrent editing must be handled explicitly.



Example:



```text

User A edits caption

User B edits caption

```



The system must detect stale versions or use an appropriate merge strategy.



Critical publishing changes should use optimistic concurrency control.



\---



\# 65. Deletion and Archival



Published content should generally not be physically deleted through normal UI operations.



Use:



```text

Active

Archived

Deleted/Soft Deleted

```



where appropriate.



Historical publishing records must remain auditable.



\---



\# 66. Data Model — Conceptual



Core entities:



```text

ContentIdea

ContentItem

ContentVersion

ContentBrief

Campaign

ContentProgram

ContentTemplate

ContentTemplateVersion

ContentPlatform

ContentChannel

ContentFormat

ContentSchedule

PublishingAttempt

ContentAssetRelation

ContentDependency

ContentTag

ContentPillar

ContentGoal

```



Relationships:



```text

Campaign

&#x20;└── ContentItem

&#x20;     ├── ContentVersion

&#x20;     ├── ContentBrief

&#x20;     ├── ContentAssetRelation

&#x20;     ├── ContentDependency

&#x20;     ├── ContentSchedule

&#x20;     │     └── PublishingAttempt

&#x20;     ├── Project Reference

&#x20;     ├── Deliverable Reference

&#x20;     └── Review/Approval References

```



\---



\# 67. Multi-Tenant Isolation



All tenant-owned content entities must be scoped to the organization/tenant.



Queries must never rely solely on UI filtering for tenant isolation.



Authorization and data access must enforce tenant boundaries at the server/data-access layer.



\---



\# 68. Client Isolation



A client may have access to selected content only.



Example:



```text

Organization

&#x20;├── Internal Campaign A

&#x20;├── Client Campaign B

&#x20;│    ├── Client-visible Content 1

&#x20;│    └── Client-visible Content 2

&#x20;└── Internal Campaign C

```



Client access must be explicit.



\---



\# 69. Contractor Isolation



Contractors may receive access to selected:



\* content briefs

\* production tasks

\* assets

\* deadlines

\* deliverables



They must not automatically see:



\* client pricing

\* internal margins

\* unrelated campaigns

\* employee data

\* other contractor financial information



\---



\# 70. Cross-Platform Requirements



\## Desktop



Prioritize:



\* dense content calendars

\* multi-panel editing

\* drag-and-drop planning

\* keyboard shortcuts

\* bulk operations

\* campaign management

\* production coordination

\* media workflows



\## Web



Prioritize:



\* broad accessibility

\* browser-based planning

\* client collaboration

\* approvals

\* scheduling

\* reporting



\## Android



Prioritize:



\* quick status updates

\* approvals

\* comments

\* notifications

\* content review

\* publishing confirmation

\* calendar

\* quick capture of ideas



The business rules remain shared.



\---



\# 71. Offline Behavior



Mobile/desktop offline behavior should support limited actions such as:



\* viewing recently synchronized content

\* drafting content ideas

\* editing permitted fields

\* adding notes

\* reviewing cached assets where supported



Publishing should generally require confirmed online state unless a specific provider workflow explicitly supports otherwise.



Conflict resolution belongs to `035`.



\---



\# 72. Accessibility



The content planner must support:



\* keyboard navigation

\* screen-reader semantics

\* sufficient contrast

\* visible focus

\* accessible drag/drop alternatives

\* non-color-only status indicators

\* accessible media review controls

\* responsive layouts



\---



\# 73. Internationalization



The architecture must support:



\* locale-aware dates

\* timezone-aware publishing

\* localized UI

\* Unicode content

\* multilingual captions

\* right-to-left languages where required

\* locale-specific formatting



Content itself must not assume English.



\---



\# 74. Security Requirements



Protect:



\* client content

\* unpublished campaigns

\* credentials/channel information

\* drafts

\* private assets

\* publishing tokens

\* analytics

\* internal strategy



Publishing credentials must be stored through the secure integration/secrets architecture.



They must never be stored in ordinary content records.



\---



\# 75. Failure Handling



Failures should be classified.



Examples:



\### Validation failure



```text

Missing approved version

```



Do not retry automatically.



\### Provider failure



```text

External API timeout

```



May be retried.



\### Authorization failure



```text

User no longer has publishing permission

```



Do not blindly retry.



\### Asset failure



```text

Referenced asset unavailable

```



Requires correction.



\### Rate limiting



May be retried using provider-specific backoff.



\---



\# 76. Publishing Reliability



Publishing must use:



\* idempotency

\* retry policies

\* provider response tracking

\* timeout handling

\* rate-limit handling

\* duplicate-publication prevention

\* reconciliation where provider state is uncertain



An uncertain provider result must not automatically be treated as a successful publication.



\---



\# 77. External Publishing Reconciliation



Where supported, BusinessOS should periodically reconcile:



```text

BusinessOS Publishing State

&#x20;       ↕

External Platform State

```



Differences should be surfaced rather than silently overwritten.



\---



\# 78. Content Import



Future integrations may import:



\* existing posts

\* publishing history

\* campaign metadata

\* channel information

\* platform metrics



Imported records must preserve:



\* source system

\* external ID

\* import timestamp

\* source version where available



\---



\# 79. Content Export



Authorized users may export:



\* content calendar

\* campaign plan

\* content lists

\* publishing schedule

\* copy

\* selected metadata



Exports must respect permissions.



\---



\# 80. Content Planning Metrics



Operational metrics may include:



| Metric                  | Meaning                                   |

| ----------------------- | ----------------------------------------- |

| Planned Content         | Content currently planned                 |

| Production Rate         | Content entering production               |

| Approval Rate           | Content reaching approval                 |

| Revision Rate           | Content requiring changes                 |

| Publishing Rate         | Content successfully published            |

| On-Time Rate            | Content published within planned schedule |

| Publishing Failure Rate | Failed publishing attempts                |

| Cycle Time              | Planning-to-publishing duration           |

| Campaign Completion     | Campaign plan completion                  |



These are operational metrics, not complete business-performance analytics.



\---



\# 81. Business Graph Integration



The content domain contributes:



```text

Client

&#x20;↓

Campaign

&#x20;↓

Content Item

&#x20;↓

Project

&#x20;↓

Task

&#x20;↓

Deliverable

&#x20;↓

Version

&#x20;↓

Review

&#x20;↓

Approval

&#x20;↓

Publishing Schedule

&#x20;↓

Publishing Attempt

&#x20;↓

External Platform

&#x20;↓

Performance Data

```



This graph allows BusinessOS to answer questions such as:



\* Which projects produced this campaign's content?

\* Who approved this post?

\* Which deliverable was published?

\* Which client requested it?

\* Which content was delayed because of approval?

\* Which campaigns have unfinished content?

\* Which platform publishing attempts failed?

\* Which assets were used?

\* Which team members contributed?



\---



\# 82. AI + Content + Business Graph



The AI Assistant may answer:



> "Show me everything pending for Client X's September campaign."



The system should retrieve authorized:



\* campaign

\* content

\* projects

\* tasks

\* reviews

\* approvals

\* publishing schedules



The AI should not independently query unauthorized information.



\---



\# 83. Automation Examples



\### Campaign Creation



```text

Campaign Created

→ Create Content Program

→ Generate Planning Items

→ Create Project/Task References

→ Notify Owners

```



\### Approval



```text

Content Approved

→ Schedule Publication

→ Create Calendar Representation

→ Notify Publishing Owner

```



\### Publishing Failure



```text

Publishing Failed

→ Record Failure

→ Notify Owner

→ Create Follow-up Task

```



\### Monthly Content



```text

Monthly Trigger

→ Load Client Content Profile

→ Generate Planned Content

→ Apply Template

→ Assign Production Work

→ Request Approval

```



Automation must remain controlled by `029`.



\---



\# 84. Recommended Vertical Slices



\## Slice 1 — Content Foundation



Implement:



\* Content Item

\* statuses

\* ownership

\* tags

\* client/project references

\* basic list/detail views



\## Slice 2 — Campaigns



Add:



\* Campaign

\* campaign lifecycle

\* content relationships

\* campaign dashboard



\## Slice 3 — Briefs and Copy



Add:



\* briefs

\* copy fields

\* platform variants

\* versioning



\## Slice 4 — Content Calendar



Add:



\* calendar views

\* scheduling

\* filters

\* calendar integration



\## Slice 5 — Assets



Add:



\* asset relationships

\* previews

\* approved asset references



\## Slice 6 — Review and Approval



Integrate `006`.



\## Slice 7 — Publishing



Add:



\* schedules

\* publishing state

\* attempts

\* manual confirmation



\## Slice 8 — External Integrations



Integrate `021`.



\## Slice 9 — Automation



Integrate `029`.



\## Slice 10 — AI



Integrate `028`.



\## Slice 11 — Analytics



Integrate `024`.



\---



\# 85. Definition of Ready



A Content Planning feature is ready for implementation when:



\* ownership is defined

\* related domain ownership is defined

\* state model is defined

\* authorization is defined

\* client visibility is defined

\* audit requirements are defined

\* API commands are defined

\* failure behavior is defined

\* concurrency behavior is defined

\* cross-platform behavior is defined

\* test cases are defined



\---



\# 86. Definition of Done



A Content Planning feature is complete when:



\* domain rules are implemented

\* API behavior is tested

\* authorization is tested

\* tenant isolation is tested

\* audit behavior is tested

\* client visibility is tested

\* concurrency is tested

\* failure/retry behavior is tested

\* UI is implemented for applicable platforms

\* accessibility is validated

\* analytics/events are emitted

\* search indexing is handled where required

\* documentation is updated

\* migration strategy exists where schema changes occur



\---



\# 87. Acceptance Criteria



The system must be able to:



1\. Create and manage content items.

2\. Create campaigns.

3\. Associate content with campaigns.

4\. Associate content with clients and projects.

5\. Manage content briefs.

6\. Manage platform-specific copy.

7\. Associate assets with content.

8\. Track content versions.

9\. Require appropriate approval before publishing.

10\. Schedule content.

11\. Track publishing attempts.

12\. Handle publishing failures.

13\. Prevent duplicate publishing where possible.

14\. Represent content schedules in the calendar.

15\. Preserve publishing version identity.

16\. Support client-visible content without exposing internal information.

17\. Support internal-only content.

18\. Support recurring content programs.

19\. Support templates.

20\. Support AI-assisted planning without bypassing authorization.

21\. Support automation without duplicating automation infrastructure.

22\. Preserve provenance.

23\. Preserve audit history.

24\. Support cross-platform access.

25\. Preserve historical truth.



\---



\# 88. Required Test Categories



\## Unit Tests



\* content lifecycle

\* campaign lifecycle

\* scheduling validation

\* version selection

\* platform rules

\* dependency validation



\## Integration Tests



\* project integration

\* task integration

\* workflow integration

\* review/approval integration

\* calendar integration

\* notification integration

\* file integration

\* integration provider behavior



\## Authorization Tests



\* tenant isolation

\* client isolation

\* contractor isolation

\* publishing permissions

\* bulk operation permissions



\## Reliability Tests



\* duplicate events

\* duplicate publishing

\* provider timeout

\* retries

\* rate limits

\* uncertain provider results



\## Concurrency Tests



\* simultaneous editing

\* simultaneous scheduling

\* version replacement

\* cancellation during publishing



\## UI Tests



\* calendar

\* campaign board

\* content editor

\* approval flow

\* publishing flow

\* client visibility



\---



\# 89. Open Architectural Decisions



The following remain intentionally open until the relevant architecture decisions are formally resolved:



1\. Exact supported publishing platforms for initial release.

2\. Exact external social-media APIs.

3\. Direct publishing scope for MVP.

4\. Whether platform accounts are organization-level, brand-level, or both.

5\. Social authentication/provider architecture.

6\. Exact content-performance ingestion model.

7\. Whether content programs belong to campaigns or may exist independently.

8\. Exact template engine implementation.

9\. Media transcoding responsibilities relative to `026`.

10\. Whether social scheduling requires a dedicated provider for some platforms.

11\. Exact mobile publishing capabilities.

12\. Content approval requirements by client/service/package.

13\. Exact campaign budget ownership.

14\. Revenue attribution methodology.

15\. Advanced social analytics scope.

16\. AI-generated content policy and approval requirements.

17\. External publishing reconciliation frequency.



These decisions must be captured through ADRs rather than silently resolved inside implementation.



\---



\# 90. Architectural Invariants



The following are non-negotiable:



1\. Content Planning is the authoritative owner of content planning intent.

2\. Calendar is not a second source of truth for publishing schedules.

3\. Project state belongs to Projects.

4\. Task state belongs to Tasks.

5\. Review/approval state belongs to Workflow/Review/Approval.

6\. Files belong to the file/media architecture.

7\. Communication belongs to Communication.

8\. Analytics belongs to Analytics.

9\. External provider connections belong to Integrations.

10\. AI behavior belongs to AI architecture.

11\. Automation belongs to Automation.

12\. Financial calculations do not belong to Content Planning.

13\. Publishing must respect authorization.

14\. Publishing must respect required approvals.

15\. Scheduled publishing must identify the intended content version.

16\. Duplicate publishing must be prevented wherever technically possible.

17\. Provider failures must not corrupt internal business state.

18\. Client visibility must be explicit.

19\. AI cannot bypass business permissions.

20\. Automation cannot bypass business permissions.

21\. Historical content and publishing facts must remain traceable.

22\. Every tenant-owned record must respect tenant isolation.

23\. Important content operations must be auditable.

24\. Cross-platform clients must use shared business semantics.

25\. No domain may create a shadow implementation of another domain's authoritative capability.



\---



\# 91. Dependency Summary



```text

014 Content Planning

│

├── 002 Identity \& Organization

├── 003 Authorization

├── 004 CRM / Clients

├── 005 Projects / Tasks

├── 006 Workflows / Reviews / Approvals

├── 008 Documents

├── 009 Communication

├── 010 Calendar

├── 013 Resources

├── 021 Integrations

├── 023 Search

├── 024 Analytics

├── 026 Production Operations

├── 027 Client Portal

├── 028 AI

└── 029 Automation

```



\---



\# 92. Final Domain Model



```text

&#x20;                   ┌──────────────┐

&#x20;                   │    Client    │

&#x20;                   └──────┬───────┘

&#x20;                          │

&#x20;                          ▼

&#x20;                   ┌──────────────┐

&#x20;                   │   Campaign   │

&#x20;                   └──────┬───────┘

&#x20;                          │

&#x20;                          ▼

&#x20;                   ┌──────────────┐

&#x20;                   │Content Item  │

&#x20;                   └──────┬───────┘

&#x20;                          │

&#x20;            ┌─────────────┼─────────────┐

&#x20;            ▼             ▼             ▼

&#x20;         Brief         Versions       Assets

&#x20;            │             │             │

&#x20;            │             ▼             │

&#x20;            │          Approval         │

&#x20;            │             │             │

&#x20;            └─────────────┼─────────────┘

&#x20;                          ▼

&#x20;                    Publishing Plan

&#x20;                          │

&#x20;                          ▼

&#x20;                     Calendar Event

&#x20;                          │

&#x20;                          ▼

&#x20;                   Publishing Attempt

&#x20;                          │

&#x20;                          ▼

&#x20;                  External Platform

&#x20;                          │

&#x20;                          ▼

&#x20;                    Performance Data

```



The complete BusinessOS content lifecycle is therefore:



```text

Idea

&#x20;↓

Planning

&#x20;↓

Campaign / Program

&#x20;↓

Brief

&#x20;↓

Production Coordination

&#x20;↓

Assets / Deliverables

&#x20;↓

Review

&#x20;↓

Approval

&#x20;↓

Version Selection

&#x20;↓

Publishing Schedule

&#x20;↓

External Publishing

&#x20;↓

Publishing Result

&#x20;↓

Performance

&#x20;↓

Analytics / Intelligence

```



This establishes \*\*014 Content Planning, Campaigns and Publishing\*\* as a coordinated business domain while preserving the authoritative boundaries of the previously defined BusinessOS architecture.



