---
layout: default
title: "Xtract Solutions Documentation | About"
permalink: /dev-sop/
---

# Development Standards of Practice {#top}

Version 1.0.3

# Purpose
This document describes the software development process for Xtract Solutions as it pertains to the development team. The process described is based on Scrum, an Agile framework, and covers planning/storing Product Backlog Items, the work being done during Sprints, as well as the process for releasing stable iterations of the projects we work on. 

This process does not currently prescribe process or methods for selling, implementing, training for, or maintaining said releases. Any member or title not specifically mentioned is not covered by this process, unless selected as a delegate for relevant process steps.

# Product Backlog Item Generation {#product-backlog-item-generation}
Product Backlog Items are represented by Github Issues with the “Needs Project” label, or other labels and identification methods as agreed to by the Scrum Team. Product Backlog Items may originate from client feedback/request or internally, and may represent bug fixes, new features, or other changes to the product or its architecture.

The Product Owner maintains this list and maintains an understanding of the priority of the Product Backlog Items with a method of their choosing. They or their delegate(s) refine the contents of the Product Backlog Items, such that important, valuable, and time-sensitive issues are selected first for upcoming Sprints and are appropriately described and detailed in a way that the Scrum Team finds useful.

Product Backlog Item generation and refinement is an on-going process that is independent of the development process described below.

# Development Sprint Process {#development-process}

## Begin the Sprint {#sprint-begin}
1. The Lead Developer or their delegate makes a new Github Project for the Sprint named "Sprint #" with the Sprint number in the appropriate repository
2. The Scrum Team conducts the Sprint Planning meeting
3. The Development Team moves Issues into the Sprint Project in the "To Do" column as a result of/during the Sprint Planning meeting. These Issues will make up the Sprint Backlog

## Work Through the Sprint Backlog {#sprint-work}
1. The Lead Developer or their delegate creates a new `next_release` branch or merges the `master` branch into an existing `next_release` branch. All new work for the Sprint is done in this `next_release` branch
2. The Development Team assigns Sprint Issues to Developers. The Development Team self-organizes and self-determines who gets what issues to work on. Issues may be unassigned and/or reassigned at any time at their discretion
3. The Development Team conducts Daily Scrum meetings
4. The Developers move Issues through the Github Project columns
   1. Move Issues to the "Doing" column when started
   2. Move Issues to the "Ready for Test" column when complete
   3. Assign "Ready for Test" Issues to Quality Assurance or impartial Developers for validation. Validation at this stage is a unit test to ensure that the changes made perform as expected by redressing the original Issue and determining if the problem has been solved or feature has been added as described. The process and results of this testing is recorded in the Issue with objective data captures, screenshots, and other output whenever possible
      * If Quality Assurance is not available to be assigned/self-assign "ready for Test" Issues, the Issue must be validated by a Developer that did not contribute code to the Issue, or the Developer who contributed the least to the Issue, or the Lead Developer, or the Director of Development as resources are available.
   4. Move validated issues to the "Done" column, and close the Issue
   5. Move issues that failed validation back to the "To Do" column and reassign the original Development Team member. That Development Team member then resumes work as per the process described above

## Finish the Sprint {#sprint-finish}
1. The Scrum Team conducts a Sprint Review meeting
2. The Lead Developer or their delegate merges the `next_release` branch into the `current_version` branch
3. The Scrum Team conducts a Sprint Retrospective meeting

# Determine If a Release is Necessary {#release}
After the completion of any Sprint, the Product Owner may determine that enough features or fixes have been implemented into the `current_version` branch to warrant a release, which can be deployed to clients. This determination happens at the Product Owner's discretion. If no release is necessary, the Sprint process as described above continues as normal.

1. The Product Owner determines that a release is necessary
2. The Director of Development or their delegate assigns a version number to the proposed release using the Semantic Versioning format as described by semver.org, as appropriate to the situation
3. The Lead Developer or their delegate builds a Release Candidate in Github from the `current_version` branch
4. Quality Assurance and the Developers conduct release validation. Release Validation may be tracked either as Issues in the next Sprint, or parallel to the Sprint depending on resources and strategy
   1. The Director of Development or their delegate creates or reuses Release Validation procedures for representative client types, which include but are not limited to: ENT, BCA, and Baker
   2. The Lead Developer or their delegate procures or updates a database for each representative client type and makes them available for use
   3. The Lead Developer or their delegate conducts relevant migrations on each database
   4. Quality Assurance conducts validation on each database based on Release Validation procedures. They may assign validation tasks or procedures to Development Team members as needed
5. Director of Development or their delegate signs off on validation stating that all Release Validation procedures were completed satisfactorily and that the release is stable 
   * This sign-off is represented by a comment on each Release Validation Issue with the following text as appropriate to the situation: "I have reviewed the project and approve these changes for release," followed by the date and their typed name
6. The Lead Developer or their delegate merges the `current_version` branch into the `master` branch
7. The Director of Development or their delegate notifies affected clients and internal employees of the release

# Special Projects {#specal-projects}
The procedure described herein accounts for the majority of development, but strategy or business needs may dictate parallel or separate development in the form of Special Projects. These projects lie outside the described Scrum process sections, but adhere to the larger development release process as dictated by the situation and resources being used.

# Special Dispensation for Emergency Fixes {#emergency-fix}
In the event that a bug or other issue occurs in production and is deemed as being detrimental to client operations, patient health and safety, or Xtract Solutions data integrity, special dispensation is granted to the Product Owner to choose to do the following:

* Add and prioritize new Issues related to the problem into the current Sprint Backlog
* Truncate the current Sprint, intending for the shortened Sprint to still be stable and releasable, in order to start a new Sprint with the new Issue(s)

If the Product Owner deems the problem worthy of these avenues, they must call a meeting with the Scrum Team to express this and discuss the impacts. 

If the current Sprint is truncated so a new Sprint can start, the Product Owner and Development Team must discuss the current state of the Sprint and the in-progress Sprint Backlog Items. The Development Team must be allowed to finish any in-progress Sprint Backlog Items such that the stability and releaseability of the Sprint is maintained even though it is ending early. The Scrum Team then immediately conducts a Sprint Review meeting and continues the process as normal from that point. The Lead Developer or their delegate will edit the description of the existing Sprint Project to link to the new Issue(s) and/or Sprint Project with a statement that the Sprint was truncated early.

Any new Issues to be added, regardless of whether the Sprint is truncated or not, must include in their text a notation stating the following:

* That this Issue is an "Emergency Fix"
* The date the original production Issue was discovered
* The client(s) and/or systems affected
* A description of the event, using captured data, screenshots, and other output or observations whenever posible
* Any additional information, particularly related to possible solutions

# Special Dispensation for Side Effects {#side-effects}

In the event that an issue, bug, or observation is created or discovered during the Sprint as a direct result of Sprint-related work, and any release potentially made from that Sprint would not be complete or as functional as it could be, that Issue may be added directly to the current Sprint at the discretion of the Lead Developer, Product Owner, or both, based on timeline, workload, and need. 

# Expectation of Change {#expectation-of-change}
The procedure described herein is an Agile process, and as such there is an expectation of change and adaptation. At any time during the process, better or different processes, tools, methods, etc, may be discovered and adopted by the Scrum Team at their discretion.

The Director of Development will endeavor to update this document to reflect changes to the process at least quarterly, or as dictated by scheduling or strategic needs.

# Training
To maintain knowledge and compliance with the procedures listed above, all development team members must review this document annually within the first quarter of the calendar year. Acknowledgement of this retraining is signified by sending an email to the Director of Development or their delegate. 

# Appendix A: Roles {#roles}

## Organizational Roles {#org-roles}

### Developer {#org-roles-developer}
Developers perform work on projects, which may include coding, database work, design and UI work, and data manipulation. For the purposes of this process, no distinction in title is made between these different specialties.

### Lead Developer {#org-roles-lead-developer}
The Lead Developer is in charge of the operations of the development team. They or their delegate assign tasks, monitor task progress, dictate and enforce code standards, and report to the Director of Development.

### Quality Assurance {#org-roles-quality-assurance}
Quality Assurance assures that work completed by the development team is functional and performs as desired. They do this by testing the code and its frontend either manually, or with automated testing scripts.

Quality Assurance may delegate or request delegation of validation tasks to Developers if needed.

### Director of Development {#org-roles-director-of-development}
The Director of Development oversees the strategic operation of the development team. They draft new standards, research emerging technologies, and ensure order. The Director of Development or their delegate signs off on release validation once it is complete if the validation status is satisfactory and stable.

The Director of Development oversees this document and will endeavor to update this document to reflect changes to the process at least quarterly, or as dictated by scheduling or strategic needs.

## Scrum Roles {#scrum-roles}
Scrum only specifies and makes use of three roles: Development Team, Product Owner, and Scrum Master. These three roles together are collectively referred to as the Scrum Team. These are the only roles with responsibilities within the Scrum process, and supercede organizational roles within it.

### Development Team {#scrum-roles-development-team}
The Development Team is comprised of any individual that will contribute work to the Sprint. This includes not only development, but quality assurance, documentation, consultants, backend engineering, database architecture, and so on. The roster of the Development Team is based entirely on the content and needs of the Sprint.

To that end, the Development Team is self-organizing. Only the Development Team determines what work and in what quantities it can do, what members it has, and how work is distributed to its members. 

Throughout this document, any use of "Development Team" refers to this specific role within Scrum, while "development team" refers to the organizational grouping of Developers, Lead Developer, Director of Development, and Quality Assurance.

### Product Owner {#scrum-roles-product-owner}
The Product Owner controls the Product Backlog, and therefore the product direction and strategy. Their goal is to maximize value for the product by ordering the Product Backlog Items by value, either to Xtract Solutions or to our clients. They may delegate the task of ordering and refining the Product Backlog to the Development Team, but the Product Owner remains responsible for its contents and orderly execution. 

The Product Owner or their delegate often interfaces with clients directly, producing new Product Backlog items based on their feedback and projected desires.

### Scrum Master {#scrum-roles-scrum-master}
The Scrum Master oversees the execution, adherence, and efficiency of the Scrum process. They are the source of truth for Scrum, as well as an impartial mediator when problems need to be resolved that stand in the way of work within the Scrum process.

The Scrum Master officiates or attends Scrum meetings to ensure that they remain within their timebox, and are both positive and productive.

# Appendix B: Scrum Overview {#scrum}
Scrum is an Agile framework. Agile is a methodology, an abstract mindset, that specifically emphasizes continuous improvement, collaboration, and efficiency in software development. This can be actualized, practically, by valuing worker skills and well-being over deadlines, shorter more manageable release cycles, and providing avenues for change rather than remaining rigid.

While Agile is an abstract description of how things should be done, Scrum is a concrete implementation of those values into an actionable process. 

Scrum relies on steady and frequent iteration, in the form of Sprints, to progressively add new features and fixes to a product. Sprints last between one and four weeks, and always end with a stable and releasable version of the product.

Scrum has three roles and four meetings. Nothing else we do is considered Scrum if it is not those three roles and four meetings. Scrum events are timeboxed, which mean that they must occur, but must not exceed a pre-calculated amount of time. If more needs to be discussed after this timebox ends, the individual members may reconvene on their own to continue.

### Events {#scrum-events}

#### Sprint {#scrum-events-sprint}
Sprints are executed sequentially, and immediately following the last Sprint, unless other scheduling or strategic needs dictate otherwise. Sprints are comprised of four meetings, and the flow of a Sprint follows this pattern whether the work done is successful or not.

Sprints are timeboxed, with an acceptable range between one and four weeks. The duration of the Sprint defaults to two weeks, but may be adjusted during the Sprint Planning meeting if necessary.

During the Sprint, all Sprint Backlog Items will be completed, documented as necessary, and validated by Quality Assurance testing. Quality Assurance validation and backend work (database, architecture, etc) are not a separate phases or secondary concerns; rather, they must be accounted for when planning the Sprint.

The output of a Sprint is a complete and releasable iteration of the product. If any Sprint Backlog Items remain incomplete by the end of the Sprint, they are put back into the Product Backlog and may be addressed in future Sprints.

#### Sprint Planning {#scrum-events-sprint-planning}
The Sprint begins with the Sprint Planning meeting. The Sprint Planning meeting is timeboxed to at most two hours per week that the Sprint will run.

During the Sprint Planning meeting, the Development Team and Product Owner negotiate what Product Backlog Items will be completed in the upcoming Sprint. The Development Team seeks to select enough items to have a full but not hectic amount of work during the Sprint, and the Product Owner seeks to maximize the value of the final product by prioritizing higher Product Backlog Items taken by the Development Team.

The Product Backlog Items selected are compiled into a Sprint Backlog. During the Sprint Planning meeting, the Development Team and Product Owner endeavor to refine the selected Sprint Backlog Items into the specificity and granularity that they deem necessary to perform the work. 

When the Sprint Planning meeting is complete, the Sprint has officially begun.

#### Daily Scrum {#scrum-events-daily-scrum}
The Daily Scrum is timeboxed to 15 minutes, and as its name suggests, is held daily.

The Daily Scrum is held by and for the Development Team to discuss their internal work, process, concerns, etc. The Development Team may invite anyone else they may need to talk to at their discretion. The Scrum Master may attend the Daily Scrum to ensure that it remains under 15 minutes long, and that the meeting is productive and positive.

The Development Team may use this time to get clarification on Sprint Backlog Items by inviting the Product Owner, or the Product Owner's delegate.

#### Sprint Review {#scrum-events-sprint-review}
The Sprint Review meeting is timeboxed to at most one hour per week that the Sprint ran.

Once the timebox for the Sprint is over, the Scrum Team, and any guests the Product Owner wishes to invite, convene to review the contents of the Sprint. During this meeting, the Development Team demos and outlines the work that they completed, as well as what was not completed, and they and the Product Owner decide which Sprint Backlog Items are complete. 

The Product Owner may also wish to address changes to the Product or Product Backlog that occurred during the Sprint, as well as any new clients, bugs, or functionality requests.

The Sprint Review attendees then may choose to discuss plans for what will go into the next Sprint in an effort to streamline the Sprint Planning meeting before it happens.

#### Sprint Retrospective {#scrum-events-sprint-retrospective}
The Sprint Retrospective meeting is timeboxed to at most one hour, plus 30 minutes per week that the Sprint ran. The meeting is held after the Sprint Review Meeting and before beginning the next Sprint with the Sprint Planning meeting.

During the Sprint Retrospective meeting, the Scrum Team discusses how the work went during the Sprint, hoping to uncover and address any deficiencies, as well as highlighting good work and innovative ideas. 

# Appendix C: Related Technologies and Processes

## Github
Github is a web service that provides centralized hosting and user management for Git Repositories, Projects, Issues, Releases, and other Git concepts. Git is a protocol for creating and maintaining peer-based repositories of code that can be simultaneously worked on by multiple people and teams in a well-ordered and conflict-free way. Repositories are often restricted to only selected users, or users belonging to an organization, but may also be made public at the discretion of their creator.

Central to Git and Github is version control. Any change to any Repository, Issue, Project, Wiki, Release, comment, or file is tracked and saved into perpetuity. Information about the user who made the change, the date and time the change was made, and the exact contents of their change(s) are tracked.

Changes to the code are made in Commits, which represent some amount of change to the code or its files, and are subject to version control. Commits are created at the discretion of the Developer, and can be pushed singly or in groups back into the repository for others to review and/or accept into the codebase. This allows for potential conflicts between pieces of code or repository structure to be obvious, trackable, and repealable.

### Issues
Github Issues are a way to report and document changes, requests, observations, and bugs in a Repository. Issues are subject to version control and may contain mixed media attachments as well as text. Users can comment on Issues to discuss the contents or contribute new information or media. Issues may be included in a Project or given labels to organize them.

### Projects
Github Projects represent a desired set of changes or future state to a Repository. The contents and intent of the Project are determined by its contributors, and is used as a method to organize work toward a common goal. Projects can have Issues assigned to them, and can be restricted to certain users.

### Repositories
Github Repositories are centralized areas where related code is kept. Repositories often store the entire structure and files of an application, for example. As the top-level physical organizational element in Github, it contains not only the files, but Projects, Issues, Wikis, and other features and elements.

Repositories may be restricted to certain users, and made private or public.  

### Releases
Github Releases represent a stable state of the code in a Repository that is intended for use or distribution. Releases are often heavily scrutinized through a Quality Assurance process prior to deployment to ensure that the final product is verified safe, stable, and functional.

### Wiki
Github Wikis are a documentation resource provided by Github. They function similarly to other wikis (e.g. Wikipedia) in that their contents are organized into pages that may link to one another, and often are categorized for better organization. Wikis often share the same permissions as the Repository they are attached to, and are subject to version control.

# Appendix D: Resources and References {#resources}
* [Xtract Solutions Documentation Site](http://xtractsolutions.github.io)
* [Semantic Versioning Format](http://semver.org)
* [Agile Manifesto](http://agilemanifesto.org/)
* [Scrum.org, What is Scrum?](https://www.scrum.org/resources/what-is-scrum)
* [Getting started with Github](https://help.github.com/en/github/getting-started-with-github)