# Skill: Scrum Master Planning (High-Fidelity Tasking)

This skill empowers the agent to act as a professional Scrum Master, breaking down complex objectives into highly detailed, actionable GitHub issues.

## 🛠 Prerequisites
- GitHub CLI (`gh`) must be authenticated.
- Repository labels (`epic`, `feature`, `task`) must exist.

## 🔄 Workflow SOP

### Phase 0: Issue Inventory & Context Sync
Before planning anything new, you MUST synchronize with the existing project state:
1. **List Open Issues**: `gh issue list --limit 50` to see what's currently being tracked.
2. **Review Parent Issues**: Check `Epic` and `Feature` issues to understand the high-level roadmap.
3. **Identify Gaps**: Determine which parts of the technical architecture (defined in `GEMINI.md`) lack corresponding GitHub issues.

### Phase 1: Deep Discovery (Technical Analysis)
Before creating any issues, you MUST analyze the technical requirements:
1. **Analyze Schema & Domain**:
   - What are the primary fields and their types? (e.g., `BigDecimal` for prices, `LocalDate` for dates).
   - What are the relationships? (One-to-Many, Many-to-One).
   - Are there specific constraints (Unique, Not Null)?
2. **Clarify Module Dependencies**:
   - Which module will host the logic?
   - What existing classes or utilities in `module-core` should be reused?
3. **Edge Case Brainstorming**:
   - How should null data or network timeouts be handled (especially for `module-batch`)?
   - What are the validation rules for the incoming data?
4. **Identify Project Patterns**:
   - Check existing entities or repositories to ensure consistent styling (Lombok, Naming).
5. **Wait for Approval**: Do NOT proceed to Phase 2 until the "Technical Specification" is clear and approved.

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
