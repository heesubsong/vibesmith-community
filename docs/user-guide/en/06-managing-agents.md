# Managing Agents

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## Navigate to Agents Page

![Navigate to Agents Page](images/agents-01-list.png)

Navigate to **Components** > **Agents** in the left sidebar to view all agents.

Agents are AI-powered subagents that automatically handle specific tasks.

## Agent Types

- **Task Manager**: GitHub Projects management
- **Spec Writer**: Frontend specification creation
- **Spec Reviewer**: Specification review and validation
- **Test Writer**: Automated test generation
- **UI Implementer**: UI component implementation
- **QA Fixer**: Quality Gate auto-fixes
- **API Integrator**: API integration automation
- **Daily Reporter**: Daily report generation

### 💡 Useful Tips

💡 Agents are specialized skills for complex automation.
💡 Invoke agents through Cursor's Task tool.
💡 Each agent operates independently and returns results.

## Create New Agent

![Create New Agent](images/agents-02-new-modal.png)

Click the **+ New Agent** button to open the agent creation modal.

## Required Fields

1. **Agent Name**: kebab-case (e.g., `my-agent`)
2. **Description**: What the agent does
3. **Subagent Type**: Select Cursor Task type
4. **Model**: fast, alpha, beta, etc.
5. **Tools**: List of tools the agent will use

## Subagent Types

- `generalPurpose`: General tasks
- `explore`: Codebase exploration
- `shell`: Command execution
- `browser-use`: Browser automation

## View Agent Details

![View Agent Details](images/agents-03-detail.png)

Click an agent card to view detailed information.

## Detail Page

- **Metadata**: Name, description, type
- **Configuration**: Model, tools, options
- **Prompt**: Instructions passed to agent
- **Execution History**: Recent execution records
- **Performance Metrics**: Success rate, average execution time

## Execute Agent

To execute an agent in Cursor:

```
@task-manager Recommend next task
@spec-writer Write spec for login feature
@test-writer Write tests for UserProfile component
```

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0