
# Bonus: I Can Integrate Project Management Methods into a Project

agile versus waterfall

critical path

triple constraint - scope, time, cost

JIRA

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

poker planning, backlog, 2-week sprints

impediment

code review

acceptance criteria (definition of done)

What is a story? (one person responsible, delivers defined business/technical value, hopefully not too big)

It's better to break work down into smaller chunks

Story points are used to communicate value added and provide realistic estimate of velocity

Dependencies (on other stories and other teams)

Project Lifecycle and Importance of Making Changes Earlier


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

Sometimes a story can have one or more dependencies and can't be completed immediately
Not all stories have a technical component or are entirely technical

What is the critical path for completing this work?
If it takes $100 of labor to complete each story point, how big should the labor budget be?

story pointing
  - actual points can be wrong

team lifecycle - forming, storming, norming, performing

project management software

## Cleanup

docker volume prune