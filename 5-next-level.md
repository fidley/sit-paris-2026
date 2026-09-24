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

