# Next level, agent with skills

## Managing one skill

Change the mode to Agent and run following command in the chat
```
/skill:sap-object-documenter for package xxxx
```

The result should be an Markdown documentation of the development objects in the selected package. But due to no restriction of the tools and not being clear about the storage place,
the result may be written in wrong place, like in my examlpe:

<img width="267" height="165" alt="image" src="https://github.com/user-attachments/assets/0b94d29f-aeee-4a8e-aeef-038caa93f7ba" />

To secure it, lets create a new agent, this time [SAP-Object-Documenter](/agents/sap-object-documenter.agent.md).

After creation, select it from agent list and run command.

```
Document package xxx
```

<img width="511" height="498" alt="image" src="https://github.com/user-attachments/assets/bafe508b-7554-47fb-8ef3-2b76c4d1d309" />

Now the result are exactly where we stated. We could create second agent, that will use same skill, but will point other folder as the destination for example.


## Multi-skill agent

Real power of agents is combined with several skills. When we have skills that works well, we can start to bundle them in one agent, or use selectively inside the agent.

Please take a look on the agent [ABAP Build and Test](/agents/abap-build-and-test.agent.md). It contains the rules to apply all ARC-1 skills, that are linked to build or test scenario.
Selecting the agent in Copilot before writing a prompt, secures correct skills selection on a base of structured routing, not selection done automatically by AI tools.

Create the agent on your end and use this prompt to see the results.

```
Create new abap class in $TMP package, that will select all users data and theirs last logon.
Popose those which should be blocked as they're not using the system.
Create unit test for all methods including private.
Run ATC and Unit Tests checks after creation and correct all major errors.
```

## Multi-MCP agent
In order to achieve the best results, we should not focus on one single MCP server usage. SAP provides us the ABAP-MCP server, there are many community driven ones. MCP for ticketing systems, Jira, DevOps etc.
Combining specific parts from them, is the best way to get the best results, but in the same time, takes a lot of time for investigation and tests.
