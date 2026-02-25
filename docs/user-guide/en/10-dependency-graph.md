# Dependency Graph

> 📝 This document was automatically generated. If you find any errors or have suggestions, please report them via [Issue](https://github.com/heesubsong/vibesmith-community/issues).

## Open Dependency Graph

![Open Dependency Graph](images/dependencies-01-graph.png)

![Open Dependency Graph Demo](gifs/dependencies-graph-demo.gif)

Click **Dependencies** in the left sidebar to explore the interactive dependency graph.

## What is the Dependency Graph?

A visual map showing how components relate to each other.

- **Nodes**: Individual components (Skills, Agents, Commands, etc.)
- **Edges**: Dependencies (when A references B)
- **Color**: Distinguishes component types
- **Size**: Scales with dependency count

## Graph Controls

- **Zoom**: Mouse wheel or pinch gesture
- **Pan**: Click and drag
- **Select**: Click any node
- **Reset**: Double-click

### 💡 Useful Tips

💡 Circular dependencies appear in red.
💡 Orphan nodes (no connections) appear in gray.
💡 Customize the layout by dragging nodes.

## Filter and Search

![Filter and Search](images/dependencies-02-filter.png)

Use the filter controls at the top to focus on specific components.

## Filter Options

- **By Type**: Skills, Agents, Commands, Hooks, or Rules
- **By Path**: Local or Global
- **By Tag**: Show only specific tags
- **Depth**: Set exploration depth (1-3 levels)

## Search

Type a keyword to:
- Highlight matching nodes
- Reveal related dependencies
- Emphasize connection paths

## Layout Algorithms

- **Force-directed**: Automatic placement (default)
- **Hierarchical**: Top-down hierarchy
- **Circular**: Radial arrangement
- **Grid**: Structured grid

## Node Details

![Node Details](images/dependencies-03-node-detail.png)

Click any node to see its details in the right panel.

## Information Displayed

- **Basic Info**: Name, type, and path
- **Dependencies**: Components this one uses
- **Dependents**: Components that depend on this one
- **Statistics**: Dependency count and depth

## Quick Actions

- **Open File**: Launch in your editor
- **View Details**: Navigate to full details
- **Copy**: Duplicate to another project
- **Related**: Focus on connected nodes only

---

**Last Updated**: 2026-02-25  
**Version**: 0.1.0