# Memory Architecture for paw.skill

## Storage Structure

```
pets/
├── max/
│   ├── PROFILE.md          # Living personality profile
│   ├── interaction-log.jsonl # Every session logged
│   ├── photos/              # Described photos with extracted data
│   ├── voice-map.md         # Vocalization dictionary
│   └── timeline.md          # Life milestones chronologically
├── luna/
│   ├── PROFILE.md
│   ├── interaction-log.jsonl
│   └── ...
└── relationships.md          # How pets relate to each other
```

## Update Rules

1. NEVER overwrite existing profile data — append and refine
2. Track confidence: "observed 12 times" > "mentioned once"
3. Note contradictions: if new data conflicts with old, flag it and ask the user
4. Timestamp everything
5. Log every update in interaction-log.jsonl

## Cross-Session Protocol

Every new session:
1. Check for existing `pets/` directory
2. Load all profiles
3. Load last 10 interaction log entries for context
4. Continue building — never restart from zero
5. At session end, save all updates

## Grief-Aware Memory

For pets marked as "Passed":
- Profile is frozen for factual data (no new observations possible)
- But memories can still be ADDED (owner remembers something new)
- Interaction mode uses past tense awareness but present personality
- Anniversary dates are noted and handled gently
