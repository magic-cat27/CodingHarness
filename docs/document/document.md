Specification for Planner how to maintain the document system.

# Overview
The document system is built for agent to work correspond to user's expectation where AGENTS.md serves as an entrance. It is an information system to make agent find required information effectively and precisely. 

Planner is the designer and editor of document system, while Executor uses the document system. When Planner designing, the first concern is how to make Executor use it effectively.

There are 3 components in AGENTS.md:
- Repo Overview. Introduction for the repo and Repository structure. Should be rewritten for each repo.
- Roles and Anthority. Specify how coding agents cowork with User. Seldom change unless author requests.
- Router. Router is the key design for our document system, consists of two components: Trigger and File Path. The quality of document system mostly depend on the quality of router.

There are two kind of documents: 
System-Level prompt such as AGENTS.md or PLANNER.md, which serves as the entrance of document systems; Specification documents, record more detailed information that agents refer to when required. You mainly write specification documents

# Writing Guidelines
- Make information clear and concise, keep off redundant expression. Imagine if you are Executor, what kind of document you want to input into your context.
- Take agents reasoning into consideration. It is not necessary to write everything into document, as agent could reason and complete some of them.

# Router Guidelines
- Writing Trigger: Trigger is the motivation for agents to find the document. A good trigger have two features: First, it should correspond to some of the statement in main text. It's after agents read the main text that they have the motivation to read more files. Second, it should describe the motivation of agents precisely and concisely.
- Structure: refer to the chain of AGENTS.md -> development.md -> detailed_files.md
