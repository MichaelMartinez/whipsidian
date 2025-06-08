PRD: Obsidian Whisper + LLM Agent Plugin

1. Overview / Goal
This project will create an Obsidian plugin with a Python-based backend agent pipeline to process audio transcriptions, classify them, enrich notes, and improve linking across the vault.

The system will:

Transcribe mp4 audio files referenced in notes.

Inline the transcription below the corresponding ![[...]] embed.

Classify the text using an LLM (OpenAI API) and suggest tags.

Allow the user to approve or reject new tags.

Insert action items under a ## Tasks section when found by the LLM, with user approval.

Run a semantic search (via FAISS) and link similar notes at the bottom of the current note.

Display an Obsidian modal to show the diff and ask for approval before writing changes.

Log agent steps for transparency.

Allow undo of added tags and tasks.

2. System Architecture
Component Description
Obsidian Plugin (JS) Frontend UI, triggers, modal interactions
Python Agent Backend Runs transcription, classification, FAISS
Whisper API Used to transcribe mp4 audio
OpenAI LLM API Used to classify text and suggest actions
FAISS Vector Store On-demand semantic similarity search
Vault Watcher Watches for changes to relevant notes

3. User Stories
Transcription
As a user, when I reference an mp4 in a note, the agent should transcribe it and insert the transcription below the embed.

The agent should not re-transcribe audio unless explicitly requested.

Classification & Tagging
As a user, I want existing tags to be auto-applied if the LLM suggests them.

If the LLM suggests a new tag, I want to see a modal where I can approve/reject or edit the tag before adding it.

Task Extraction
As a user, if the agent detects an action item, I want to approve adding it under a ## Tasks section of the note.

Linking Similar Notes
As a user, I want the agent to suggest and insert links to semantically similar notes at the bottom of the note.

Review & Approvals
As a user, before any changes are written back, I want to review a diff and approve or reject changes.

As a user, I want to undo changes (tags, tasks) that the agent applied.

Transparency
As a user, I want to view a trace of what steps the agent took for auditing and debugging.

4. Features & Flow
Monitoring & Triggers
Monitor the vault for notes that reference mp4 files (via ![[...]] embed).

Process only new files or notes not yet transcribed.

Processing Pipeline (Agent)
Detect mp4 reference.

Transcribe mp4 via Whisper API.

Insert transcription inline below embed.

Run LLM to:

Suggest tags

Extract action items

Suggest similar notes

Present modal with:

Diff view (old vs new note)

Approval UI for tags, tasks, links.

Apply approved changes.

Log the entire agent trace for the user.

Provide an "undo last run" button.

User Modal Example
Section User Action
Transcription View only
Suggested Tags Approve/reject/edit
Tasks Approve/reject/edit
Similar Notes Links Approve/reject each link
Diff preview View full note diff before save

5. Technical Stack
Component Stack
Plugin Frontend JavaScript (Obsidian Plugin API)
Backend Agent Python 3.10+, LangChain
Transcription OpenAI Whisper API
LLM OpenAI GPT-4o or GPT-4
Vector Store FAISS (local)
Communication Local server (FastAPI) or WebSocket between plugin & backend
Packaging Python virtualenv, local backend server

6. Limitations & Risks
Area Notes
Cost Whisper API & OpenAI API calls incur cost
Vault Scale FAISS must be tuned for very large vaults
Offline Use Cloud APIs required initially; offline path stubbed only
Diff Quality For large notes, visual diff may be less readable
Undo Scope Only supports undo of agent changes, not manual user edits

7. Success Criteria
Transcriptions are inserted accurately and formatted.

Tag suggestions respect user approval and existing tags.

Tasks are extracted correctly and inserted under ## Tasks.

Semantic links are meaningful and useful.

User can review and approve all changes in a modal.

Undo mechanism is usable and reliable.

Agent trace is clear and available for inspection.

8. Tools
Category Tool
LLM & Transcription OpenAI API
Vector Search FAISS
Agent Framework LangChain
Backend Server FastAPI
Vault Watch Obsidian plugin API + VaultWatcher
Diff Generation Python difflib or unified diff
Modal UI Obsidian Modal API

If you approve this PRD, next I can generate:

Initial repo structure template (JS plugin + Python backend)

Example LangChain agent pipeline definition

Example Obsidian Modal UX flow in JS
