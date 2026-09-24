# First calls to ARC-1 MCP server



## Transports and task list
Go to Eclipse and in the Copilot chat enter:

```
using arc1-dev list all open tasks and transport requests  for user xxxxx
```
Result should be something like that:
<img width="1420" height="266" alt="image" src="https://github.com/user-attachments/assets/5891947a-4fde-4ad7-8532-97004668639e" />


## Public methods signatures
```
Show the signatures of the public methods of xxxx class, using arc1-dev
```

<img width="1063" height="333" alt="image" src="https://github.com/user-attachments/assets/ba371cbc-12da-4df4-8ba2-983df810428d" />


## Docker logs
To see what's happening behind, go to Docker-> Containers->arc1-dev->logs

You should notice usage of SAPTransport and SAPRead tools.
<img width="1622" height="309" alt="image" src="https://github.com/user-attachments/assets/00f58a3c-7ff4-4c57-b1ab-b9cfa7dbff33" />
