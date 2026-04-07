# Skill: Scrum Master Planning (High-Fidelity Tasking)

This skill empowers the agent to act as a professional Scrum Master, breaking down complex objectives into highly detailed, actionable GitHub issues.

## 🛠 Prerequisites
- GitHub CLI (`gh`) must be authenticated.
- Repository labels (`epic`, `feature`, `task`) must exist.

## 🔄 Workflow SOP

### Phase 1: Deep Discovery (Technical Analysis)
Before creating any issues, you MUST analyze the technical requirements:
1. **Analyze Schema**: Ask 3-5 sharp questions about data models, edge cases, and module dependencies.
2. **Clarify Constraints**: Identify specific Spring Boot annotations, Lombok patterns, or testing requirements (JUnit 5).
3. **Wait for Approval**: Do NOT proceed to Phase 2 until the "Technical Specification" is clear and approved.

### Phase 2: Work Breakdown Structure (WBS)
Present the proposed hierarchy in a clear table:
| Hierarchy | Name | Description | Related To |
|-----------|------|-------------|------------|
| Epic      | [Epic Name] | [Goal]      | [Module]   |
| Feature   | [Feature Name] | [Approach] | Epic #ID   |
| Task      | [Task Name] | [What/Why]  | Feature #ID|

### Phase 3: High-Fidelity GitHub Issue Creation
Use `gh issue create` with the following templates. Ensure every **Task** is a "self-contained" unit of work.

#### Issue Template: Task
```markdown
## 🎯 Goal
[Clear description of the task's objective]

## 💻 Technical Requirements
- **Target Module**: [e.g., module-core]
- **Implementation**: [Specific class/interface names, package paths, patterns]
- **Dependencies**: [Other tasks or services required]

## ✅ Acceptance Criteria (Definition of Done)
- [ ] Logic implemented according to technical specification
- [ ] Unit tests (JUnit 5) implemented and passing
- [ ] Gradle build (`./gradlew build`) successful for the module
- [ ] [Functional AC 1]
- [ ] [Functional AC 2]

## 🔗 Relations
Part of Feature: #FeatureID
```

## 📜 Execution Rules
1. **Be Specific**: Never use words like "some", "any", or "various". Use exact class names (e.g., `StockPriceEntity`).
2. **Assignee**: Default to the current user (e.g., `sikutisa`).
3. **Labels**: Always apply the corresponding label (`epic`, `feature`, or `task`).
