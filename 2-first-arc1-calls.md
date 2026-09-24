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


## Tools documentation
Please check [tools documentation](https://docs.arc-1-mcp.com/tools/) to get more information about how the tools can be used

# ARC-1 MCP Tools (optional)

ARC-1 exposes 12 core intent-based tools. Availability adapts to the SAP
system's detected features, release, and safety settings.

| Tool | Purpose | 
| --- | --- | --- |
| `SAPRead` | Read source, metadata, packages, drafts, revisions, tables, CDS, UI5, and system information 
| `SAPSearch` | Find objects by name or source text | 
| `SAPWrite` | Create, update, delete, or surgically edit ABAP objects |
| `SAPActivate` | Activate one object or a dependent batch | 
| `SAPNavigate` | Find definitions, references, completion, or class hierarchy | 
| `SAPQuery` | Execute ABAP SQL through ADT |
| `SAPTransport` | Inspect and manage CTS requests | 
| `SAPGit` | Inspect gCTS or use gated abapGit workflows | 
| `SAPContext` | Dependency, usage, or CDS impact context | 
| `SAPLint` | Run local abaplint or SAP Pretty Printer operations |
| `SAPDiagnose` | Syntax, ABAP Unit, ATC, dumps, traces, and gateway diagnostics | 
| `SAPManage` | Probe features, inspect cache, manage packages and selected FLP objects |

## Tool selection rule

Use context before raw source when asking what an object does:

```text
SAPContext(action="deps", type="CLAS", name="ZCL_WORKSHOP_DEMO")
SAPRead(type="CLAS", name="ZCL_WORKSHOP_DEMO")
```

Use `SAPRead` for exact source, a method, a draft, a revision, or a grep match.
Use `SAPSearch` to discover names. Use `SAPDiagnose` after a change, and use
`SAPActivate` before a server-side syntax check because syntax checks operate on
active source.

## Sample calls

### Connectivity and discovery

```text
SAPRead(type="SYSTEM")
SAPManage(action="probe")
SAPManage(action="features")
SAPSearch(query="ZCL_*WORKSHOP*", maxResults=20)
SAPRead(type="DEVC", name="ZWORKSHOP", maxResults=100)
```

### Understand an object

```text
SAPContext(action="deps", type="CLAS", name="ZCL_WORKSHOP_DEMO", depth=2, maxDeps=10)
SAPRead(type="CLAS", name="ZCL_WORKSHOP_DEMO", method="*")
SAPRead(type="CLAS", name="ZCL_WORKSHOP_DEMO", method="GET_STATUS")
SAPNavigate(action="references", type="CLAS", name="ZCL_WORKSHOP_DEMO", maxResults=20)
```

### Search and inspect CDS/RAP

```text
SAPSearch(query="ZC_WORKSHOP*", objectTypes=["DDLS"])
SAPContext(action="impact", type="DDLS", name="ZI_WORKSHOP")
SAPRead(type="DDLS", name="ZI_WORKSHOP")
SAPRead(type="DCLS", name="ZI_WORKSHOP_DCL")
SAPRead(type="BDEF", name="ZI_WORKSHOP")
SAPRead(type="SRVD", name="ZSD_WORKSHOP")
SAPRead(type="SRVB", name="ZUI_WORKSHOP_O4")
```

### Quality and diagnosis

```text
SAPLint(action="lint", source="REPORT zworkshop. WRITE 'Hello'.")
SAPDiagnose(action="syntax", type="CLAS", name="ZCL_WORKSHOP_DEMO")
SAPDiagnose(action="atc", type="CLAS", name="ZCL_WORKSHOP_DEMO", resultFormat="structured")
SAPDiagnose(action="unittest", type="CLAS", name="ZCL_WORKSHOP_DEMO", coverage=true)
SAPDiagnose(action="dumps", user="WORKSHOP_USER", maxResults=10)
```

### Read-only transport and Git inspection

```text
SAPTransport(action="list", summary=true)
SAPTransport(action="check", type="CLAS", name="ZCL_WORKSHOP_DEMO", package="ZWORKSHOP")
SAPTransport(action="history", type="CLAS", name="ZCL_WORKSHOP_DEMO")
SAPGit(action="list_repos")
SAPGit(action="branches", backend="gcts", repoId="WORKSHOP_REPO")
```

### Controlled development write

Only run this on the approved development system with writes enabled:

```text
SAPWrite(
  action="create",
  type="PROG",
  name="ZARC1_WORKSHOP_HELLO",
  package="$TMP",
  source="REPORT zarc1_workshop_hello.\nWRITE 'Hello from ARC-1'."
)
SAPActivate(type="PROG", name="ZARC1_WORKSHOP_HELLO")
SAPDiagnose(action="syntax", type="PROG", name="ZARC1_WORKSHOP_HELLO")
```

For a transportable package, check the transport first:

```text
SAPTransport(action="check", type="CLAS", name="ZCL_WORKSHOP_DEMO", package="ZWORKSHOP")
SAPTransport(action="list")
SAPWrite(action="update", type="CLAS", name="ZCL_WORKSHOP_DEMO", source="...", transport="A4HK900123")
```

### Data query warning

`SAPQuery` is disabled by default and uses ABAP SQL syntax. `DESCENDING` is valid
where standard SQL often uses `DESC`, and `maxRows` is a tool parameter rather
than `LIMIT` in the SQL string.

```text
SAPQuery(
  sql="SELECT carrid, COUNT(*) AS cnt FROM sflight GROUP BY carrid ORDER BY cnt DESCENDING",
  maxRows=20
)
```

Do not run this against a productive or sensitive system without explicit data
governance approval.



# Agents in Eclipse [Why so complicated](3-agents-in-eclipse.md)
