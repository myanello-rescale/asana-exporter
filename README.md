# Overview

Exports Asana projects along with their resources such as tasks and stories and saves as json in a tree structure  making it easy to query with tools like [jq](https://stedolan.github.io/jq/) and import into other tools like Jira.

## Install

From source:

```
sudo apt install python3-pip
pip install -r requirements.txt
```

From snap:

```
sudo snap install asana-exporter
```

## Usage

The first action to take is extract information from Asana using the API. To do this you will need to generate a Personal Access Token. See https://developers.asana.com/docs/personal-access-token for instructions on how to do this.

Once you have a token run the tool as follows to extract data. A team name and workspace are required (see https://developers.asana.com/docs/workspaces - this is usually your organisation name). Projects are extracted in the context of a team. You can extract multiple teams projects into the same archive by running the tool multiple times with different teams.

```
asana-exporter --token TOKEN --workspace WORKSPACE --team TEAM --export-path PATH
```

Once complete, your data will be under PATH and you can query it e.g.

List all teams found:

```
asana-exporter --export-path PATH --list-teams
```

List all extracted projects for a given team:

```
asana-exporter --export-path PATH --team "My Team" --list-projects
```

List all extracted tasks for a given project:

```
asana-exporter --export-path PATH --team "My Team" --list-project-tasks "My Project"
```

