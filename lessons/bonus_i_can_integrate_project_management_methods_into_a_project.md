
# Bonus: I Can Integrate Project Management Methods into a Project

## The Coordination Problem

Most or all large-scale endeavors of modern society involve getting people
to do things when they are supposed to do them.

A great deal of time and effort is spent organizing and managing the work
and workers of nontrivial projects.

### The Coordination Problem in Software

Most significant software projects are (most definitely) nontrivial. In addition
to the development of core features, there are considerations for budget,
production support (including monitoring and logging),
potentially geographically-disperse teams, deployment processes, live testing,
and changes in desired features ('scope'),
among other things ('multi-dimensional chess').

Here are two distinct considerations for software projects.

  - Complex and Overlapping - Whenever a change (even a small one) is made to the
  project, it can be difficult to made and bring about unintended consequences.
  Likewise, methodologies and technologies in the software industry change rapidly
  resulting in projects using new things that haven't been used before by the team.
  Changes made by one team member can affect (and surprise) other ones.
  - Business Representatives Don't Understand Work - The people responsible
  for defining the business goals (like product owners) don't understand
  (and don't need to) the implementation details of the work, but they do need
  to know whether the work is getting done and what problems are being encountered
  (e.g. the database team hasn't deployed the database yet, so the web application
  team is blocked from launching its application into Production).

#### Project Management

A project manager's job is to ... manage projects. This is a common job within
corporations. This is a full-time (dedicated) role in larger software projects,
but can be a part-time role (held by one of the developers) on a smaller project.

The required skills for a project manager (e.g. meeting with other teams,
tracking overall project progress and budget, providing updates to and receiving
criticism from management, political acumen) differs from a software engineer
(e.g. knowing latest technologies, understanding intricacies of software project,
completing tasks quickly).

Project managers typically come from a business (e.g. majored in economics)
or technical (e.g. majored in computer science) background. Sometimes tech people
go into this role later in their careers.

## Coordination within Technical Team

As stated above, software projects are complex and overlapping. It's easy for the
work of one team member to 'bump into' the work of another team member.

To solve this coordination problem, modern software projects use these features
in a source control repository (like Git).

  - 'Branch' - The developer(s) creates an individualized public copy (a 'branch')
  of the main work ('master' branch, sometimes called 'main' branch).
  - 'Pull Request' - The developer notifies (issues a 'pull request') the team
  that the proposed change is ready for review.
  - Apply Recommendations - Team members may comment or request changes to the
  'pull request' and the developer makes these changes.
  - 'Merge' - Once one 'pull request' has been approved by one or more other members
  of the team. The developer integrates ('merges') the proposed changes
  into the main work. Now the main copy of the software project has these changes.

## Coordination Between Technical Team and Business Owners

The work of a story is broken down into smaller pieces of work that can be completed
by an individual team member, typically within a day or a few days. These smaller
pieces of work are known as 'stories' . Project management software products
(like JIRA) manage these groupings of stories for individual projects.

A business contact will probably understand the goal of a story but isn't expected
to understand how it will be done, that's left up to the technical team.

_The story is the bridge of understanding between business contacts and
the technical team. Both understand what a story is and its 'merged pull request'
represents completion of that story._

## Planning Projects

In the domain of project management, there are two well-known ways of structuring
the work.

  - Waterfall - This is where the the entire project is planned out ahead of time,
  with the expected schedule, start date, and dependencies of each task
  documented, often before the project has even started. This is a more traditional
  form of project management. It's intuitive and less risky for projects that are
  very similar to past projects. This structure of project management is a natural
  fit when deadlines must be met at specific times
  (e.g. planting and harvesting crops) or when dealing with external clients
  (e.g. government) where payment terms are defined by legal contract
  (e.g. payment of $100 million after 100 units of a next-generation tank meets
  specifications signed off by a military committee).
  - Agile - The goals of the project and the next batch of upcoming work
  ('stories') are reevaluated every so often (called a 'sprint' - commonly lasting
  one or two weeks). The team should be able to demo all existing work to business
  contacts at the end of each sprint. This frequent evaluation of work allows
  a project to better adapt (be more 'agile') to problems and changing software
  requirements.

Modern software projects tend to follow the 'Agile' approach. It's well known
in the software industry that making changes and adapting sooner is far less
expensive and risky.
  
### Budgeting Effort

Stories for an upcoming sprint are reviewed during a 'story grooming'
or 'poker planning' session. Unfinished stories from the 'backlog' (undone work)
are reviewed and prioritized.

When a story is reviewed, the following things are considered.
  - Acceptance Criteria - This is a big deal. Stories should clearly define
  their goals. Likewise, the team should have a list of general criteria that
  any story (affecting source code) should meet (e.g. passing unit tests,
  deployed on Stage environment). Stories with bloated acceptance criteria
  ('trying to do too much') are more risky and should be broken down into smaller
  stories. A team may have a formal and generalized 'Definition of Done' for all
  of its stories.
  - Dependencies - Determine if work needs to be complete elsewhere before work
  on this story can start or finish.
  - Effort - The team assigns a (unit-less) number to the
  story representing its effort, risk, and complexity. The team may use some unit
  (like days to complete) to determine this number, but the number is only an
  estimate and is frequently wrong (but it provides some basis to understand
  its effort and (depending on team culture) can be changed later). It's common
  to use one of the Fibonacci numbers (i.e. 1, 2, 3, 5, 8, 13, ...) as the point
  value for a story.
  - Priority - The importance of a story is considered. While a given story _can_
  be done, it doesn't mean that it _should_ be done _right now_ (or ever). Stories
  with higher priority are moved to the top of the back log (presumably to be
  assigned next sprint). When another team within a company requests that the
  software project have a new feature, the development team doesn't work on that
  feature immediately, but instead asks that a story be created in the 'backlog'
  to be groomed (and prioritized) (maybe) during the next sprint planning session.

Note that the goal of stories isn't always to change the source code. Stories
can involve (for instance) working with other teams, investigating a support issue,
deploying code to a different environment.

### Planning Upcoming Work

The number of story points completed during the last sprint(s) provide a good
indication of how much work (story points) the team can complete
(and should schedule) during the next sprint.

## Other Project Management Concepts

Project management is an extensive topic, but here are some well-known concepts.

### Impediment

When a story can't be completed because one or more of its dependencies isn't
available, that story has encountered an impediment and can be marked as such
in project-management software. Marking a story as impeded sends a clear signal
to the organization that others teams should take action.

#### Triple Constraint
The 'Triple Constraint' is the notion that any project can achieve only two
out of the following three goals - done quickly ('time'), done cheaply ('cost'),
lots of features ('scope').

#### Critical Path

The mapping of all stories and their inter-dependencies represents the entire work
of the project. The stories along the path which consumes the most time is
known as the 'critical path' . Managing and shortening the critical path
is important in software management.

Consider stories A through F with effort (in days) 1 (A), 2 (B), 3 (C), 4 (D),
5 (E), and 6 (F). All stories don't have dependencies except C which depends on B.
Although B then C would take (2 + 3 = ) 5 days to complete, the critical path is F
so if management asks 'How long will it take to complete this project?' the answer
is 6 days. If management want to shorten the completion time to 5 days (the next
critical path defined by either (of two) paths 'B-C' or 'E'), management could
decide to assigned more skilled people to F or shrink the acceptance criteria of it.

#### Team Formation

While projects (both software and non-software) can vary greatly between each other,
here is a well-known social pattern people follow in these situations.
 
  1) Forming - People introduce themselves to each other and tend to make
  a best impression.
  2) Storming - People 'jockey for power' trying to obtain their preferred
  hierarchical place and responsibilities within the team.
  3) Norming - People agree to their positions and general team culture.
  4) Performing - People work within the team culture to seek approval
  and get the job done.

#### Scope Creep

There's a tendency for business contacts to request new features and changes
while a project is underway. This is known as 'scope creep' . Software teams
should only consider this new work after careful consideration.

To remove ('deprioritize') work from a project is to 'descope' it or to say that
"It's out of scope."

#### MVP (Minimal Viable Product)

Minimal Viable Product is the minimum features required by the product
to be acceptably functional.


GitHub Pages




### Run JIRA

```
docker volume create --name jiraVolume
docker run -v jiraVolume:/var/atlassian/application-data/jira --name="jira" -d -p 8080:8080 atlassian/jira-software
```

Now go to http://localhost:8080

Leave the 'Set it up for me' value selected then click the 'Continue to MyAtlassian' button

Create an account by entering your email address, creating a password (like 'ilovejira'), then clicking the 'Sign up' button

Follow directions to register the JIRA application with Confluence

Access JIRA by going to http://localhost:8080/secure/WelcomeToJIRA.jspa

What is a story? (one person responsible, delivers defined business/technical value, hopefully not too big)



(Story Suggestions)
CHHCS-1 - Project Kickoff, Come Up with App Concept and Title
  - Requires - (None)
CHHCS-2 - Develop Basic HTML Page which Displays 'Hello World'
  - Requires - CHHCS-9
CHHCS-3 - Create Favicon Image
  - Requires - CHHCS-9
CHHCS-4 - Integrate Favicon into Web Page
  - Requires - CHHCS-3
CHHCS-5 - Determine Layout of Web Page
  - Requires - CHHCS-1
CHHCS-6 - Add Title to Web Page
  - Requires - CHHCS-2
CHHCS-7 - Structure Layout of Web Page with Descriptions of Each Section
  - Requires - CHHCS-2 , CHHCS-5
CHHCS-8 - Create Project in GitHub
  - Requires - CHHCS-1
CHHCS-9 - Prepare Developer Environments and Document Procedure for Doing So
  - Requires - CHHCS-8

(Paths to Completion - Note that CHHCS-6 has two paths to it)

CHHCS-1 , CHHCS-8 , CHHCS-9 , ( CHHCS-2 , CHHCS-5 ) , CHHCS-6
CHHCS-1 , CHHCS-8 , CHHCS-9 , CHHCS-2 , CHHCS-7
CHHCS-1 , CHHCS-8 , CHHCS-9 , CHHCS-3 , CHHCS-4
CHHCS-1 , CHHCS-5 , CHHCS-6

(Process for Completing Story)
  - Assign Story to Self (this doesn't necessarily have to be done at start of sprint)
  - Move story to 'In Progress'
  - Create branch (if story is technical)
  - Complete work
  - Issue Pull Request
  - Add Pull Request Location as Comment to Story, Ask Team to Review Pull Request
  - Move story to 'Code Review'
  - Apply recommendations to PR
  - Merge PR once approved
  - Move story to 'Complete'

What is the critical path for completing this work?
If it takes $100 of labor to complete each story point, how big should the labor budget be?



## Cleanup

docker volume prune