# Doc Co-Authoring Steering

## Metadata

- **Name**: doc-coauthoring
- **Description**: Guide users through a structured workflow for co-authoring documentation. Use when user wants to write documentation, proposals, technical specs, decision docs, or similar structured content. This workflow helps users efficiently transfer context, refine content through iteration, and verify the doc works for readers.

## Triggers

Use this steering when:
- User mentions "write a doc", "draft a proposal", "create a spec", or "write up"
- User mentions specific doc types: "PRD", "design doc", "decision doc", "RFC"
- User seems to be starting a substantial writing task
- User wants to collaboratively create documentation

## Instructions

This steering provides a structured workflow for guiding users through collaborative document creation. Act as an active guide, walking users through three stages: Context Gathering, Refinement & Structure, and Reader Testing.

### When to Offer This Workflow

**Trigger conditions:**
- User mentions writing documentation
- User mentions specific doc types
- User seems to be starting a substantial writing task

**Initial offer:**
Offer the user a structured workflow for co-authoring the document. Explain the three stages:

1. **Context Gathering**: User provides all relevant context while Claude asks clarifying questions
2. **Refinement & Structure**: Iteratively build each section through brainstorming and editing
3. **Reader Testing**: Test the doc with a fresh Claude (no context) to catch blind spots

### Stage 1: Context Gathering

**Goal:** Close the gap between what the user knows and what Claude knows.

#### Initial Questions

1. What type of document is this?
2. Who's the primary audience?
3. What's the desired impact when someone reads this?
4. Is there a template or specific format to follow?
5. Any other constraints or context to know?

#### Info Dumping

Once initial questions are answered, encourage the user to dump all the context they have:
- Background on the project/problem
- Related team discussions or shared documents
- Why alternative solutions aren't being used
- Organizational context
- Timeline pressures or constraints

**Exit condition:**
Sufficient context has been gathered when questions show understanding.

### Stage 2: Refinement & Structure

**Goal:** Build the document section by section through brainstorming, curation, and iterative refinement.

For each section:
1. Clarifying questions will be asked about what to include
2. 5-20 options will be brainstormed
3. User will indicate what to keep/remove/combine
4. The section will be drafted
5. It will be refined through surgical edits

**Key instruction:**
Instead of editing the doc directly, ask users to indicate what to change. This helps learning of their style for future sections.

### Stage 3: Reader Testing

**Goal:** Test the document with a fresh Claude to verify it works for readers.

#### Testing Process

1. **Predict Reader Questions**: Generate 5-10 questions readers would realistically ask
2. **Test with Sub-Agent** (if available): Test questions with a fresh Claude instance
3. **Run Additional Checks**: Check for ambiguity, false assumptions, contradictions
4. **Report and Fix**: Fix any gaps found

**Exit Condition:**
When Reader Claude consistently answers questions correctly and doesn't surface new gaps or ambiguities, the doc is ready.

### Final Review

When Reader Testing passes:
1. Recommend a final read-through
2. Suggest double-checking facts, links, or technical details
3. Ask them to verify it achieves the impact they wanted

### Tips for Effective Guidance

**Tone:** Be direct and procedural

**Handling Deviations:** If user wants to skip a stage, ask if they want to write freeform

**Quality over Speed:** Don't rush through stages; each iteration should make meaningful improvements
