# Agents in Eclipse

```
As ADT tools creates a virtual project in Eclipse workspace, it's not easy as in other programming languages
to add the agents and skills to be used with Copilot, but it's possible with small creative solution.
```

## Create general project for Agents and Skills only

Go to File -> New -> Project 

<img width="310" height="269" alt="image" src="https://github.com/user-attachments/assets/786ca922-d6e3-46fa-8bad-78e2fd8e47a1" />

And create General Project, for example GHCopilotInstruction

<img width="514" height="495" alt="image" src="https://github.com/user-attachments/assets/9887ba46-d8f4-4107-88a4-600a29dd9913" />

On the Project Explorer view, find three dots button, use it and select Filters and Customization

<img width="296" height="261" alt="image" src="https://github.com/user-attachments/assets/d98d73ec-932f-41b8-ba70-036d5ff49b47" />

Make sure that .* resources filter is deactivated

<img width="487" height="471" alt="image" src="https://github.com/user-attachments/assets/40906ac0-a4c8-4434-b925-80b55bf4dc4d" />

## Quick Quality Gate Agent creation
Now open Copilot preferences, then go to Custom Agents and press Add. Select the project you just created and add the name of the agent, for example QuickQualityGate.

<img width="899" height="573" alt="image" src="https://github.com/user-attachments/assets/e3b53721-436e-42d9-b60d-2b0585766c4b" />

Once saved, the agent md file will be opened and it will also appear in the Project Explorer view in the .github/agents/ folder.

<img width="1566" height="242" alt="image" src="https://github.com/user-attachments/assets/417d04a7-1b85-4507-a667-931543f77207" />

Click on the Configure tools... in the agent md file. Once the settings of the tools will be open, mark the tools as shown on the screen.

<img width="834" height="369" alt="image" src="https://github.com/user-attachments/assets/396e428a-de5b-4a31-b585-4409b274ac87" />

Come back to editor and add Description and instruction for agent. Try to use specific tools name for specific actions, so Copilot will not lose time and tokens 
Sample [Quick Quality Gate agent](/agents/quickqualitygate.agent.md)

Open any class on your system (the smaller the faster results), open Copilot Chat and on the bottom expand the Mode dropdown and select QuickQualityGate agent.
Inside the chat, write 
``` Check quality ``` or ``` Check quality of class xxxxx ``` and let the agent work. The result should be similar to this.

<img width="707" height="612" alt="image" src="https://github.com/user-attachments/assets/df4f6669-2d76-4fc7-9ee3-478a4f46e86d" />

## [Where's my skills dude?](4-skills.md)
