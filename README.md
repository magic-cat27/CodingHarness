# CodingHarness

**English** | [简体中文](README.zh-CN.md)

Coding Harness is the harness I regularly use for development with GPT. Its core purpose is to ensure clear responsibilities, efficient development, and coverage of user requirements when working with a Coding Agent.

## Core Design
- Use AGENTS.md as the entry point. AGENTS.md is responsible for only three things: introducing the project, defining roles and their responsibilities and authority, and routing to detailed documents.
- The main roles are User, Planner, and Executor. Their responsibilities and authority are as follows:
    - User has the highest authority in principle and is primarily responsible for stating requirements and using the product.
    - Planner clarifies the user's requirements and records them in SPEC.md, then translates those requirements into an executable plan in PLAN.md. Planner is also responsible for maintaining the documentation system and project status.
    - Executor receives PLAN.md and implements the functionality strictly according to this set of documents.
- Document routing is the core design of this harness. A well-designed router enables an agent to retrieve precisely the information it needs. Clear role responsibilities and authority enable precise document routing: if a detailed document describes something outside a role's responsibilities, that role should not only be kept from seeing the document's contents—it should not even see the document's index entry.
- For more details on the design of the documentation system, see /docs/document/document.md.
