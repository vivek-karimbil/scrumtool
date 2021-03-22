# Scrum tool
This is a tool to plan and track a scrum project. This version is an almost literal translation of a spreadsheet that was in use for the same purpose.
It partially supports a scrum team to plan and track a scrum project. It does not support the typical artifacts described in scrum literature exactly,
but enables the execution of a scrum project with tolerable deviation from the documented process.

## Running
The tool itself is a single HTML file, with embedded Javascript and CSS code, inluded from their published CDNs. As such, it works when directly
opened in a browser, but this has not been extensively tested, especially accross operating systems and browsers. During development, it was tested using Node
JS as the web server, and should work on practically any other server as well.

## User Interface
Opening the HTML file in the browser displays a row of buttons on top, a row of tabs, and the view of the project below. The starting screen looks like this:

![Alt text](docs/Firstscreen.jpg?raw=true "Startup screen")

The topmost row of buttons allow import and export of projects. Projects are stored as JSON files, which can be loaded later for further editing.

![Alt text](docs/Mainmenu.jpg?raw=true "Top of page on loading")

The **Load Project** button allows a project to be loaded from a local JSON project file. The idea is to continue work on previously saved project files. 
**Save Project** saves the current data into a project file. The filename is generated from the project name and the timestamp by default, and can be changed.
It will be saved to the directory your browser uses for dowload. This may mean that the saved file is renamed to prevent overwriting an existing file, or
similar behaviour specific to your brouser, including the location of the downloaded file. Chages are not saved by default - work needs to be explicity saved
periodically.
**Clear Project** removes the current project, and starts with an empty project. This is the same effect as reloading the page.

There is a row of tabs below these buttons, that are used to edit or view the project.

![Alt text](docs/Tabmenu.jpg?raw=true "Menu of tool screens")

The **Planning** tab is used to list all the requirents bein considered for inclusion into the project. Requirements here are listed and estimated, but not
yet included in the project for implementation. This form is inteded for use in the early phase of the project before finalizing content for tracking.

![Alt text](docs/Planningtab.jpg?raw=true "Requirement planning tab")

The **Bandwith** tab contains some general settings for the project on the whole, including:
* _Project Name_, which is used to generate the default name of save file.
* _Start Date_ of the project, which is the Monday of the week of the first milestone.
* _Team_, which is a list of the people in the project, and their roles - lead, developer or QA
* _Milestones_, which a list of perdiods starting from the start date of the project, and running continuously in sequence, with no gaps.
* _Blackout Weeks_, which are a list of weeks in which all or many people in the project are expected to be unavailable, leading to little or no burndown of project work.

![Alt text](docs/Bandwidthtab.jpg?raw=true "Bandwidth setup tab")

The **Tracking** tab lists all the requiremnts in the project, and their current status against the schedule.

![Alt text](docs/Trackingtab.jpg?raw=true "Executon tracking tab")

The **Graphs** tab shows views of execuiton using graphs.
* _Milestone_, which shows the burndown in each milestone, and the work assigned to each developer
* _Release_, which shows the burndown across the whole release
* _Feature_, which shows the remiaining work per feature and per developer

![Alt text](docs/Graphtab.jpg?raw=true "Graphical views tab")

The **Settings** tab allows the tab order to be set for convenience when editing in a specific phase of the project.

![Alt text](docs/Settingstab.jpg?raw=true "Tool configuration tab")

## Workflow
The tool does not impose a workflow, but there is a loose coupling between tabs that would lead to a different user extperience based on how the tool is used.
There is a workflow described here, which is the most typical way to use the tool, but actual usage can deviate to accomodate execution convenience. The typical
workflow is expected to be a planning phase when the product owner and the team collaborate on walking through the requirements to estimate them, prior to planning
the milestones. To draw up the schedule, the team availabily is tabulated accross a series of milestones. Then in the tracking phase, the burndown is periodically
updated. The tools usage will be desribed assuming that workflow for simplicity, and it is possible to deviate in practice to accomodate real life. While this is
the broad workflow that the tool supports, it is possible to go back and forth.

To start with, the product owner would have a set of features, from which the next version of the product is to be planned. The team would need to discuss and
estimate these features to come out with the plan for the release. The product owner lists all candidate features in the planning tab, and works with the scrum
team to come up with estimates that would lead to the project schedule. This is ducumented is the planning tab in the tool. There is a table of requirements on
the **Planning** tab, that looks like this:

![Alt text](docs/Requirements.jpg?raw=true "List of requirements")

The colomns in this table are:
* _ID_, a unique identifier for the requirement from a tracking system, such as JIRA, as an external key to that system
* _Description_, a description that cn be used by the team to understand the feature for estimation, planning and development
* _Importance_, the relative importance of the feature, to make decisions about inclusion or exclusion, if needed
* _Story pts_, the size of the feature, in whatever unit the team uses, such as story points, t-shirt sizes, stone sizes, ...
* _Days_, the number of days to be considered for planning, which is a refinement of whatever was entered in the _Story points_ column

When the team has all the features estimated, or enough estimated that can be done in a release, the next thing is to work out the schedule. This is a function of
the number of developers, the effort available from each developer for the project, the number of milestones planned, and any significant long holidays during the
duration of the project. These are set up on the **Bandwidth** tab. This tab has the following panels:

* _Project Name_, which is used to default the name of the save file, apart from letting the viewers know what they are looking at.
* _Start Date_, which sets up the first date of the first milestone of the project. The dates of the milestones are calculate based on the start date and lengths of each milestone.

![Alt text](docs/Bandwidth-name.jpg?raw=true "Name and start date of project")

* _Team_, a list of developers, QA and tech lead of the project. The computation of capacity for the lead defaults to 40% and the developer to 80% when the capacity for milestones are calculated in the _Milestones_ panel.

![Alt text](docs/Bandwidth-team.jpg?raw=true "List of peoplle in the team")

* _Milestones_, the project schedule is broken up into milestones, each a cerain number of weeks long, with a default assumption of 5 working days a week. There are ways to work arout this mentioned in the FAQ section below. The capacity of each developer can be diferent in each milestone, as can be the amont of planned vacation.

![Alt text](docs/Bandwidth-milestones.jpg?raw=true "List of milestones in the team")

* _Blackout weeks_, are weeks in which vacations such as Diwali, Thanksgiving or anything similar is going to see all or a major part of the team out of office, resulting in little or no burndown for the project.

![Alt text](docs/Bandwidth-blackout.jpg?raw=true "List of holiday weeks, where no or low burndown is likely")

Once the requirements are estimated and the capacity information is entered, the schedule can be detailed in the **Tracking** tab. All the features to be
included for development are listed here, with additional information about schedule. Each row is the plan and execution data around a single requirement.

![Alt text](docs/Tracking.jpg?raw=true "List of requirements and burndown")

* _ID_, the ID of the requirement in the requirement tracking system, such as a JIRA number
* _Description_, a description of the feature
* _Team_, the developer and QA assigned to this task
* _Status_, what is the status of the task so far, which could be "Not Started" before a developer takes it up, from where it could move to "In progress" when
taken up for development. If development is blocked for any reason, it would move to "Impeded", until the issue is resolved, while the QA and developer roll on
to the next feature. If the issue cannot be resolved, the task could become "Obsolete", which would be a way to soft-delete a feature, which retains the other
information to be easily brought back, if the issue is resolved. Finally "Completed" indicates that the development and QA are done for the feature.
* _Notes_, allow free form notes to be taken to capture inputs from the QA and developer on progress. As a convention, the format '<date>: <notes>' is a useful
 way to use this section.
* _MS_ indicates the milestone in which development will be done for this feature
* _Est._ the estimate for the feature at the start of development. As a practise, this should not be changed after planning. It is better to burn up the remaining
effort (i.e. increase the remining effort), than to change the estimate. This preserves what happened for a project retrospective.  
* _Burndown_, which registers the remaining effort each week for the feature, until the QA is done.

## FAQ
- How can I start with a planning milestoe, which is used for design, POCs and other activities not directly contributing to burndown?
- How can I create gaps between Milestones?
- How can I use a 6 day week?
- How can I assign an exceptional developer more work?
- How can I start on a day other than a Monday, or end on a day other than a Friday?
- How can I accomodate different amount of productivity for newcomers, senior vs junior developers, poor performers...?
- How can I enter data for features that will take more than a milestone to develop?
- How can I decide that the QA is done, and the feature is complete?
