################################################################################
Banca Aurora - CMDB
Marco Bessi, marco.bessi@neo4j.com
################################################################################



################################################################################
DATA LOADING

Folder dataset:
1. Create a new DB on Aura
2. Load the snapshot AuraBackup_BancaAuroraCMDB.backup on the new instance

Folder dashboards:
3. Load the perpective AuraExplorePerspective_BancaAuroraCMDB.json in Explore
4. Load the AuraDashboard_BancaAuroraCMDB.json configuration inside Dashboard 
5. Load the agent configuration AuraAgent_BancaAuroraCMDB.json into Agent

Claude:
6. Configure a new personalized connector in Claude, using the Aura MCP endpoint (something like http://mcp.neo4j.io/agent?project_id=...) 



################################################################################
AURA DASHBOARDS

Show the menu and the different feature of the Console.

########################################
QUERY

Query is the old Browser. It is the technical dashboard to query the DB. You need to know Cypher to interact with the DB.

########################################
EXPLORE

Explore is the old Bloom. It is the graph dashboard created to be used by non-technical people. 
Show:
- Pattern autocomplete: `(Application {name:'CorporateCreditWorkbench'})-[HAS_REPO]->(Repository)-[CONTAINS]->(File)`
- Expand: OWNS rel
--> Clear scene
- Search Phreases: `Repository aml-case-manager ...`
- Click on Application --> Scene Action
--> Clear scene

Message to pass:
> I’m not just looking at a single CVE or just one repo; I’m looking at which part of the banking business is impacted.

########################################
DASHBOARD

Dashboard is the old NeoDash. It is a BI dashboard (only fo Neo4j). A technician build the dashboard (easily, each block contains a Cypher to get the info to be reported in the block). The non-tech people can get the info they need.
Possibility to create parameters and select values with drop-down.

Message to pass:
> The same story can be told in executive, engineering, and security terms without changing the data model.



################################################################################
AURA AGENTS

########################################
AGENTS ON AURA

Show slides and explain
Agent configuration: 
- Agent: name, description, prompt, access (internal)
- Tools: similarity search, cypher template, text2cypher

Questions for Agent Internal on Aura:
- `List all the business processes` --> show that the text2cypher tool is used
- `Who are the owners of these business processes?` --> show that a tool is selected and used
- `Are there findings related to log forging? What are the applications affected?` --> show that the similarity search is used and then another cypher template to get all the info to reply to the question

########################################
AGENTS WITH CLAUDE

Change the access flag in the Agent configuration to External
Copy the MCP endpoint
Show how to configure a connector to the Aura MCP: show the endpoint
Show that Claude can answer in Italian (also the Internal Agent can read and reply in Italian)

Questions for Agent External on Claude (show reasonings and the results visualization with tables, text, and graphs):
- `Per rispondere alle domande usa il server MCP di Neo4j Aura su Banca Aurora`
- `Quali sono i business process presenti nel database?`
- `Puoi ordinarli per rischio tecnico e revenue impattate?`
- `Puoi darmi una classifica di sanitizzazione da effettuare sulle vulnerabilità (prime 10) in base al rischio atteso ed all'impatto sulle revenue?`
- `Dammi il piano di remediation dettagliato per le vulnerabilità di priorità critica` --> expand the block of Log4Shell

Message to pass:
> The agent doesn’t respond generically: it uses knowledge graph–specific tools and explains the risk within the context of the banking domain.


