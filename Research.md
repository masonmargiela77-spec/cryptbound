#### Agentic Coding Research - Claude (19-05-2026)


###### Agent

* Specialist Personas with defined tools and permissions
* **AGENTS.md** : code base information & project information. Auto-generated **AGENTS.md** is not really efficient compared to human-written **AGENTS.md**.

  * Include:
    * WHAT: tech stack. project structure, and what each part does
    * WHY: purpose of the project and its key components
    * HOW: how to build, test and verify changes
  * Should add **AGENTS.MD** for each service
* Agent will have name and tool
* **Orchestrator Agent:** will control, give instructions

  * Planner Agent: planning feature, bug fixes
  * Coder Agent
* Agents list: [Awsome Copilot](https://github.com/github/awesome-copilot)

###### Hooks

* Shell scripts that fire at a spcific lifecycle events regardless of what the model decides

* Can be check in [Awsome Copilot](https://github.com/github/awesome-copilot) for the list of hooks 

###### Instructions

* Extension to **AGENTS.md** that are loaded only on-demand to avoid initially polluting the Context.

|         | a11y.instruction.md<br />(Accesibility) | localization.instruction.md<br />(Localization) |
| ------: | :-------------------------------------: | :---------------------------------------------: |
| applyTo |            "**" - Everything            |                "**/*.md" - Local                |
|         |                                        |                                                |

###### Prompts

* Reusable promts you can invoke AI on demand - not a persona, not a standing rules, just a stored task you trigger explicitly.
* Ex: explain-code.prompt.md
* Starting with a slash (/) in the chat box with AI.
* Used for one-off questions, brainstorming or quick fixes

###### Skills

* Folder-based capability packages with a required SKILL.md that are loaded by an Agent on-demand.
* Each skill lives in its own directoy and contains a SKILL.md file along with optional bunded assets such as reference documents, templates, and scripts.
* Used for standard operating procedures, formatting constraints, comples multi-step workflows, or tasks where you find yourself copying the same instructions repeadtedly
* Examples:

|                                                                    breakdown-plan                                                                    |                                                          postgresql-optimization                                                          |
| :--------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------: |
| Breaking down a feature into<br />epics, features. story user <br />stories, enablers.<br /><br />Following Aglie and scaled <br />Agile methodology | Deal with SQL queries and<br />give advices about the bes <br />PostgreSQL practices<br /><br />Following PostgreSQL DBA<br />methodology |
|                                              Act as a senior Project Manager<br />and DevOps specialist                                              |                                Act as a Database<br />Administrator and Database<br />Performance engineer                                |

###### Tools

* Built in tools that give agents ability to perform designed tasks

###### Workflows

* [GitHub Agentic Workflows](https://github.github.com/gh-aw/)
* Copilot coding agent works autonomously in a GitHub Acions-powered environment to complete development tasks and creates pull requests with the results.
* Example:
  * name: "Daily Issues Report"
  * description: "Generate a daily summary of open issues and recent activity as a GitHub issue"
  * on:
    * schedule: daily on weekdays
