# CLAUDE.md - Personal Portfolio Project

## Core Rules

### Communication
- Senior dev context (5+ years, design patterns, production experience) - skip basics
- Business-friendly language - no jargon, explain decisions in business impact terms
- Direct responses only - no fluff, affirmations, or apologies
- 4 lines max unless architecture/debugging/security requires detail
- No emojis

### Code Approach
- Production-ready solutions - scalable, maintainable, secure by default
- No placeholders or TODOs - complete implementations only
- Suggest architectural options with trade-offs
- Flag security/performance implications proactively

### Context & Scope
- Ask for clarification even if in smallest doubt, do not assume understanding request perfectly
- Distinguish between quick fixes and proper solutions
- Challenge approach if clearly suboptimal
- Present outcomes with trade-offs, then implementation options

### Boundaries
- Break brevity rule for: complex debugging, architecture decisions, security issues
- Document business logic
- Address technical debt when it impacts the solution

## Process Gates (MANDATORY)

### Before Making ANY Changes (Start of Work)
```
Check clean state → git status
Uncommitted changes? → stash or commit as WIP
Verify correct branch → matches intended issue
Pull latest → git pull origin main
Branch outdated? → rebase or merge main
Conflicts? → resolve before starting new work
```

### Session Start (New Conversation)
```
1. Run status → assess project state
2. Check recent commits → understand recent work
3. Check open issues → identify priorities
4. State current context → show state [branch: ... | issue: #... | status: ...] → confirm understanding
```

### Issue Validation (Before Starting Work)
```
Read issue → has acceptance criteria?
Dependencies listed? → check if blocked
Missing details? → ask in issue comments
Wait for clarification → don't assume
Should be in Epic? → suggest reorganization
Scope clear? → document understanding in issue
```

### Start Working on an Epic Issue (New Epic Issue)
```
1. Start Working on Epic? → create Epic branch feature/[epic#]-[brief-description]
2. Read Epic description → understand effort and Child Issues
3. Update Epic status → In Progress 
4. State current context → show state [branch: ... | issue: #... | status: ...] → confirm understanding
```
### Start Working on a Child Issue (Within Epic)
```
1. Working on Child Issue? → STAY on Epic branch (no separate branch)
2. Read Child description → understand effort 
3. Update Child issue status → In Progress 
4. Commit with child issue reference → e.g., "feat: Implement feature (#227)"
5. Complete child → close issue, continue next child on SAME epic branch
Note: Only create sub-branch if child is exceptionally complex (rare)
```
### Session Continue (Existing Conversation)
```
1. Check current branch → verify correct context
2. Check uncommitted changes → understand WIP
3. Review conversation history → maintain continuity
4. State what we're working on → confirm alignment
```

### Completing Working on a Child Issue
```
ALWAYS test completed work: Unit test 
Update issues status to Done. Close issue.
Commit changes and merge Child branch
Update PROGRESS.md → add completion entry with date
Document solution in ISSUES.md → if solved a problem
Start working on the next Child 
Last Child → Complete Epic Work
```
### Completing Working on an Epic Issue
```
ALWAYS test completed work 
Update issues status to Done. Close issue.
Commit changes and merge branch
Update PROGRESS.md → summarize Epic accomplishment
Document patterns in ISSUES.md → if found solutions
Start working on the next Epic 
Last Epic → suggest improvements 
```

### Working on Standalone Issue (Not Epic/Child)
```
1. Run start [issue#] → create branch
2. Work → implement changes  
3. Test → verify solution
4. Run finish → commit, push, create PR
5. Update issue → link PR, set to In Review
```

### Multiple Issues Assigned (Priority Conflict)
```
Check issue priorities → Critical > High > Medium > Low
Check issue dependencies → some block others?
Current Epic work? → Epic children take precedence
Ask if unsure → "Should I prioritize #X or #Y?"
Document choice → comment on deprioritized issue
```

### Found New Problem While Working
```
Related to current issue? → include fix if small
Unrelated but critical? → stop and create new issue
Unrelated non-critical? → create issue, add TODO comment
Scope creeping? → ask "Should this be separate issue?"
Document finding → reference new issue in commit
Add to ISSUES.md → if problem is tricky or recurring
```

### Issue Too Large (Needs Breaking Down)
```
Realize issue too big? → stop implementation
Document subtasks needed → list in issue comment
Propose converting to Epic → wait for confirmation
Create child issues → link to parent
Update branch name → feature/[epic#]-[name] instead of fix/[number]
Continue with first child → update status
```

### Branching Strategy (IMPORTANT)
```
Standalone Issue → fix/[issue#]-[brief] or feat/[issue#]-[brief]
Epic → feature/[epic#]-[epic-name] (ALL child work here)
Child Issues → NO separate branches (work on epic branch)
Hotfix → hotfix/[issue#]-[brief] from main
Complex Child (rare) → feature/[epic#]/[child#]-[brief] (only if needed)

Example:
Epic #224 → feature/224-universal-framework
  Child #225 → commit on feature/224-universal-framework
  Child #226 → commit on feature/224-universal-framework
  Child #227 → commit on feature/224-universal-framework
```

### Switching Context Mid-Work
```
Uncommitted changes? → commit as WIP
Note current issue → will return later
Switch branch → start new work
State new context → [branch: ... | issue: #... | status: ...]
```

### Test Failures
```
Tests fail? → fix code, not tests
Can't fix immediately? → commit as WIP: "WIP: fixing test failures (#issue)"
Create follow-up issue if needed
Report status to user
```

### Before Every Commit
```
Validate HTML → W3C validator or local tools
Check CSS → no errors in browser console
Test responsive design → mobile, tablet, desktop
Check accessibility → keyboard navigation, screen reader basics
Remove debug code → search for console.log, debugger
Remove TODO comments → grep for TODO, FIXME
Verify changes match issue scope → git diff
Out of scope changes? → separate commit or different issue
```

### During Work
```
ALWAYS start response with: [branch: ... | issue: #... | status: ...]
Every 3 changes → commit with issue reference
Issue unclear? → ask for number
Context lost? → run status
User correcting? → reread and adjust
```

### Resuming After Break (>24 hours)
```
Run status → understand current state
Check issue comments → any new requirements?
Pull latest main → check for conflicts
Review own uncommitted changes → git diff
Remember context? → reread issue description
Lost context? → add WIP commit with detailed message
Continue work → update issue with "Resuming work"
```

### Hotfix/Emergency Issue
```
Create hotfix branch from main → hotfix/critical-description
Minimal fix only → no refactoring
Write regression test first → prove bug exists
Fix bug → minimal change
All tests pass? → include in commit
Document in code → why this fix
Fast PR → tag as emergency
Deploy immediately after approval
Cherry-pick to other branches if needed
```

### Issue Blocked/Waiting
```
Waiting for external input? → comment with what's needed
Blocked by another issue? → link blocker, move to "Blocked" status
Can't reproduce? → ask for more info, add "needs-info" label
No activity 7+ days? → ping stakeholders
Still blocked? → suggest closing or deferring
```

### PR Review Feedback
```
Review comments received? → acknowledge in PR
Each comment → address or explain why not
Make requested changes → new commits (don't force push)
Re-request review → tag reviewer
Changes substantial? → re-run full test suite
Update PR description → note what changed
All approved? → squash and merge
```

### Merge Conflict Resolution
```
Pull latest → git pull origin main
Conflicts shown? → note which files
Understand both changes → git diff
Resolve carefully → keep both fixes if different issues
Test after resolution → full test suite
Commit resolution → "resolve: merge conflict in [files]"
Verify nothing broken → run application
```

### After Merging PR
```
PR merged? → don't close issue yet
Deploy/release happened? → verify in production/staging
Actually fixed? → then close issue
Not fully fixed? → reopen with findings
Creates new issue? → link as "caused by #X"
```

### Breaking Changes Detected
```
API change? → update all consumers
Database schema change? → write migration
Config format change? → provide upgrade path
Document breaking change → CHANGELOG/PR description
Alert team/users → comment on related issues
Consider backwards compatibility → can we avoid breaking?
```

### CI/CD Pipeline Failure
```
Check failure type → tests, linting, build, deploy?
Reproduce locally → same command as CI
Fix issue → not CI config unless certain
Verify fix → run same check locally
Push fix → reference CI failure in commit
Still failing? → check CI environment specifics
Can't fix immediately? → revert problematic commit
```

### Dependencies Update
```
Check for updates → npm outdated, pip list --outdated
Review changelogs → breaking changes?
Update incrementally → one major version at a time
Run tests after each → catch breaks early
Update lock files → package-lock.json, requirements.txt
Test in isolation → separate PR for deps only
Document if needed → new APIs or patterns
```

### End of Day Checkpoint
```
Commit current work → even if incomplete (WIP)
Push to remote → backup your work
Update issue → progress comment
Note tomorrow's starting point → in issue or TODO
Any blockers? → document in issue
Log progress → update PROGRESS.md with accomplishments
Document problems → add to ISSUES.md if recurring
```

### Documentation Needs Update
```
Modified public API? → update API docs
Changed configuration? → update README
New feature added? → update user guide
Breaking change? → update migration guide
Complex logic added? → add inline comments
```

### Performance Regression Detected
```
Benchmark worse than baseline? → investigate cause
New query slower than 100ms? → optimize or index
Memory usage increased >20%? → profile and fix
API response time degraded? → check for N+1 queries
Can't fix now? → create performance issue
```

### Security Concern Identified
```
Handling user input? → validate and sanitize
New dependency? → check for vulnerabilities
API endpoint added? → add authentication check
Sensitive data? → ensure encryption
Secrets in code? → move to environment variables
```

### Before Creating PR (Self Review)
```
Diff entire PR → git diff main
Any unintended changes? → remove
Code follows patterns? → check nearby code
Tests comprehensive? → edge cases covered
Comments clear? → explain "why" not "what"
Commit history clean? → squash if needed
```

### Preparing Release
```
All issues in milestone closed? → verify
CHANGELOG updated? → document all changes
Version bumped? → semantic versioning
Migration scripts ready? → if schema changed
Rollback plan documented? → in case of issues
Stakeholders notified? → send release notes
```

### Large Refactoring Started
```
Create refactoring issue first → document plan
Tests pass before starting? → baseline confirmed
Refactor incrementally → small commits
Tests still pass? → after each step
Performance unchanged? → benchmark before/after
Update affected documentation → architecture docs
```

### Red Flags - STOP
- No commits after multiple changes
- Working without issue reference
- User says "follow the process" - you missed something
- User gives one-word responses - you misunderstood
- Lost track of current issue/branch - run status

## Communication Protocol

### Session State Tracking (MANDATORY PREFIX)
**EVERY code-related response MUST start with:**
```
[branch: current_branch | issue: #number | status: clean/uncommitted]
```

Example:
```
[branch: fix/208-blindspots | issue: #208 | status: uncommitted]
I'll fix the validation bug by...
```

Commands to get state:
- Branch: `git branch --show-current`
- Issue: Extract from branch name or track in conversation
- Status: `git status --porcelain` (empty = clean)

Only skip for single-word responses or non-code queries

### Feedback Loop Process

#### Confirmation Checkpoints
```
User gives task → I state understanding → User confirms/corrects
I take action → I report result → User validates/redirects  
Ambiguity detected → I ask specific question → User clarifies
```

#### Issue Status Flow (GitHub Project)
```
Todo → In Progress (when starting work)
In Progress → In Review (when PR created)  
In Review → Done (when PR merged)
Done → Closed (when verified working)
```

#### Understanding Verification Template
```
User: [vague request]
Me: "[state]
     I understand you want to [specific interpretation].
     Correct?"
User: [confirms or corrects]
Me: [proceed with confirmed understanding]
```

#### Action Result Reporting Template
```
After executing command/action:
- State what was done: "Created/Modified/Deleted [what]"
- Show current state: "[X files changed, Y additions, Z deletions]"
- Report status: "Success/Failed: [reason if failed]"
- Next step: "Ready to [next action]"
```

#### Continuous State Validation
```
Every 3rd response: "Still working on #208?"
Branch/issue mismatch: "Branch says #208 but you mentioned #209?"
Long silence: "Should I commit WIP before continuing?"
```

#### Error Recovery with Feedback
```
Command fails → Report exact error → Ask for preference
Tests fail → Show which tests → Ask fix or WIP commit
Conflict detected → Show conflict → Ask resolution approach
```

### Response Patterns

#### Direct Commands
Single-word commands → Execute immediately, no explanation
Named scripts/tools → Run without confirmation
Clear instructions → Act, then report result

#### Unclear Requests
Ambiguous reference → Ask for specific identifier
Vague action → Confirm interpretation before proceeding  
Missing context → Request clarification, don't assume

#### Course Correction Signals
Brief responses → Likely misunderstanding, reassess
Contradictions → State understanding vs expectation
Repetition → Previous response missed the mark, reread context

## Documentation Files

### PROGRESS.md (Project Effort Log)
Track accomplishments and progress:
```
## YYYY-MM-DD
- Completed: Issue #X - brief description
- Progress: Issue #Y - what was done
- Discovered: New approach for Z
- Impact: Performance improved by X%
```
Update when:
- Completing issues or milestones
- Making significant progress
- Discovering important patterns
- End of work session

### ISSUES.md (Problems & Solutions)
Document recurring problems and their solutions:
```
## Problem: [Description]
**Symptoms**: What happens
**Root Cause**: Why it happens
**Solution**: How to fix
**Prevention**: How to avoid
**Related Issues**: #X, #Y
```
Update when:
- Solving a tricky problem
- Finding root cause of bug
- Discovering a pattern
- Creating reusable solution

## Project Dictionary

### Terms
- **Hero Section**: Main introductory section with name and tagline
- **Responsive Design**: Layout that adapts to different screen sizes
- **GitHub Pages**: Free static site hosting from GitHub repositories
- **Minimalist Design**: Clean, simple design with focus on content
- **CSS Variables**: Custom properties for consistent theming
- **Mobile-First**: Design approach starting with mobile layout
- **WIP commit**: Work-in-progress, commit even if incomplete

### Project Context
- Personal portfolio website for GitHub Pages deployment
- Repository: https://github.com/vadimgumarov/Resume
- Minimalist design inspired by doronichev.com
- GitHub issues and project board drive all work
- Every commit needs issue reference
- Mobile-responsive, accessibility-focused design
- Epic issues must list child issues as `- [ ] #XX - Description`
- Use GitHub CLI (`gh`) for issue management
- Track progress in GitHub Project: https://github.com/users/vadimgumarov/projects/10

## Safety Rules

### Web Standards
- VALIDATE HTML5 markup
- ENSURE cross-browser compatibility
- OPTIMIZE images and assets
- MINIMIZE CSS and JavaScript
- USE semantic HTML elements

### Code
- No commits without user request
- No merge without PR
- No force push ever
- Test before claiming complete

### Content
- Never include personal sensitive information
- Use placeholder contact info if needed
- Optimize images for web (compress, proper formats)
- Include proper meta tags for SEO

## State Tracking

Track and report when relevant:
- Current branch
- Current issue  
- Uncommitted changes
- Test status
- Coverage percentage

Format: `[branch: main | issue: none | clean]` (only when relevant)

## Error Recovery

### When Confused
- State what you understand
- State what's unclear
- Ask specific question
- Don't guess

### When Wrong
- State what you did
- State what was expected
- Show the difference
- Ask for next action

### When Blocked
- State the blocker
- Show error/issue
- Suggest solutions
- Ask for preference

## Development Standards

### GitHub Issue Templates

#### Standard Issue Template
When creating regular issues, use this format:
```markdown
### Summary
[One-line description of the issue]

### Current Behavior
[What happens now]

### Expected Behavior
[What should happen]

### Steps to Reproduce
1. [First step]
2. [Second step]
3. [Continue...]

### Root Cause (if known)
[Why this is happening]

### Proposed Solution
[How to fix it]

### Acceptance Criteria
- [ ] [Specific measurable outcome]
- [ ] [Another requirement]
- [ ] [Tests pass]

### Additional Context
[Any other relevant information, logs, screenshots]
```

**MANDATORY**: Link issue to GitHub Project board immediately after creation

#### Epic Issue Template
When creating Epic issues, use this format:
```markdown
### Epic: [Epic Title]

### Overview
[2-3 sentences describing the epic's goal and value]

### Business Value
[Why this epic matters - impact on system/users]

### Technical Scope
[High-level technical requirements and constraints]

### Child Issues
<!-- MANDATORY: All child tasks MUST be listed here with issue numbers -->
<!-- Format: - [ ] #ISSUE_NUMBER - Description -->
<!-- Create child issues FIRST, then update this section -->
- [ ] #XXX - [First child task description]
- [ ] #XXX - [Second child task description]
- [ ] #XXX - [Third child task description]

### Success Criteria
- [ ] [Measurable outcome 1]
- [ ] [Measurable outcome 2]
- [ ] All child issues completed and tested

### Dependencies
[List any external dependencies or blockers]

### Timeline
[Estimated completion timeframe]
```

**MANDATORY REQUIREMENTS**:
1. Link Epic to GitHub Project board immediately
2. Create all child issues BEFORE finalizing Epic
3. Update Child Issues section with actual issue numbers
4. Each child issue must reference parent Epic in its description
5. Child issues must be linked to same Project board

### Architecture Decisions
When proposing solutions, document:
1. **Options Considered** - list alternatives with pros/cons
2. **Chosen Solution** - which option and why
3. **Trade-offs Accepted** - what we're giving up

### Code Quality
- Write tests first (TDD approach)
- Aim for high test coverage
- Follow existing patterns in codebase
- Include error handling and edge cases
- Remove debug code before committing
- Document complex logic with "why" not "what"

### Version Control
```
Commit Format: type: description (#ISSUE)
Types: feat, fix, docs, refactor, test, perf, chore
WIP prefix: for work-in-progress (tests failing acceptable)
```
- Every commit needs issue reference (except chore)
- Never add "🤖 Generated with Claude Code" or "Co-Authored-By: Claude" signatures
- Commit frequently at logical breakpoints
- Push daily for backup
- Never force push to shared branches
- Clean commit history before PR (squash/rebase)

### Testing Practices
- Test-driven development mandatory
- Test naming: describe expected behavior
- Cover edge cases and error paths
- Mock external dependencies
- Run full test suite before PR

### Security & Safety
- Never commit secrets or API keys
- Validate all external input
- Use environment variables for config
- Default to safe options (e.g., paper trading)
- Document security implications

