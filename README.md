# scrumtool
This is a tool to plan and track a scrum project. This version is an almost literal translation of a spreadsheet that was in use for the same purpose. It partially supports a scrum team to plan and track a scrum project. It does not support the typical artifacts described in scrum literature exactly, but enables the execution of a scrum project with tolerable deviation from the documented process.

The tool itself is a single HTML file, with embedded Javascript and CSS files, inluded from their published CDNs. The tool is a single HTML file that should be served of a web server. In development, Node JS was used for this purpose. The tool allows you to plan your scrum project, and savel it locally as a JSON file. In future runs, a previously saved JSON can be loaded, and continue to be edited.

On starting the tool, a row of buttons is displayed over a row of tabs. The buttons are:
* Load Project
* Save Project
* Clear Project

The **Load Project** button allows a project to be loaded from a local JSON project file. The idea is to continue work on previously saved project files. 
**Save Project** saves the current data into a project file. The filename is generated from the project name and the timestamp by default, and can be changed. It will be saved to the directory your browser uses for dowload. This may mean that the saved file is renamed to prevent overwriting an existing file, or similar behaviour specific to your brouser, including the location of the downloaded file. Chages are not saved by default - work needs to be explicity saved periodically.
**Clear Project** removes the current project, and starts with an empty project. This is the same effect as reloading the page.

These buttons appear over the following tabs:
* Planning
* Bandwidth
* Tracking
* Graphs
* Settings

The **Planning** tab is used to list all the requirents bein considered for inclusion into the project. Requirements here are listed and estimated, but not yet included in the project for implementation. This form is inteded for use in the early phase of the project before finalizing content for tracking.

The **Bandwith** tab contains some general settings for the project on the whole, including:
* _Project Name_, which is used to generate the default name of save file.
* _Start Date_ of the project, which is the Monday of the week of the first milestone.
* _Team_, which is a list of the people in the project, and their roles - lead, developer or QA
* _Milestones_, which a list of perdiods starting from the start date of the project, and running continuously in sequence, with no gaps.
* _Blackout Weeks_, which are a list of weeks in which all or many people in the project are expected to be unavailable, leading to little or no burndown of project work.

The **Tracking** tab lists all the requiremnts in the project, and their current status against the schedule.

The **Graphs** tab shows views of execuiton using graphs.
* _Milestone_, which shows the burndown in each milestone, and the work assigned to each developer
* _Release_, which shows the burndown across the whole release
* _Feature_, which shows the remiaining work per feature and per developer
