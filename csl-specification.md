# Claude Spec Language (CSL) Specification v1.0

## Overview

Claude Spec Language (CSL) is a structured natural language syntax for communicating with Claude using AI-standard terminology. It combines formal methods concepts (PDDL, FOL, CSP) with natural language to create precise, verifiable agent instructions. CSL draws heavily from concepts presented in "Artificial Intelligence: A Modern Approach" by Stuart Russell and Peter Norvig, making it familiar to those versed in standard AI terminology.

CSL integrates with modern software development practices including Agile methodologies, dual-track development, and formal specification frameworks like GitHub's spec-kit, providing a complete specification-to-implementation pipeline.

## Design Philosophy

CSL bridges the gap between informal prompt engineering and formal specification by:
- Making implicit constraints explicit
- Enabling verification of requirements
- Providing consistent terminology from AI literature
- Supporting both human and machine readability

## Example File Structures in a Claude Code Repo

### Web Apps

```
project/
├── CLAUDE.md                 # Root CSL configuration and Agent Router
└── .claude/
    └── agents/
        ├── database.md      # database agent
        ├── storage.md       # storage agent
        ├── auth.md          # auth agent
        ├── api.md           # api agent
        ├── frontend.md      # frontend agent
        └── testing.md       # testing agent
```

### Machine Learning Projects

```
project/
├── CLAUDE.md                 # Root CSL configuration and Agent Router
└── .claude/
    └── agents/
        ├── data.md           # data engineering agent
        ├── network.md        # pytorch or scikit agent
        ├── trainer.md        # trainer agent
        ├── inference.md      # inference agent
```


## CSL Syntax

### Basic Structure

CSL uses a hybrid of YAML-style declarations and markdown formatting:

```markdown
# Agent or Project Name

## Metadata
VERSION: 1.0
EXTENDS: parentfile.md     # Optional inheritance
DEPENDS_ON: [agent1, agent2] # Optional dependencies
AGENT_TYPE: reflex | model | goal | utility | learning # Agent classification
```

### Core Components

#### 1. Environment Specification
Based on AIMA Chapter 2 (Intelligent Agents)

```markdown
ENVIRONMENT: fully_observable
TASK_ENVIRONMENT: episodic | sequential  
PERFORMANCE_MEASURE: accuracy | brevity | completeness | pragmatism
ACTUATORS: [create_file, modify_file, delete_file, run_command]
SENSORS: [read_file, analyze_code, check_tests]
```

#### 2. Search Strategy
Based on AIMA Chapters 3-4 (Search)

```markdown
SEARCH_STRATEGY: breadth_first | depth_first | best_first | bounded
SEARCH_DEPTH: integer
HEURISTIC: minimize_complexity | optimize_clarity | satisfice
```

#### 3. Knowledge Base
Based on AIMA Chapters 7-9 (Logic)

```markdown
FACTS:
  - Python 3.9 available
  - Flask installed
  - Production environment

RULES:
  - IF production THEN require_auth
  - IF handles_user_data AND exposed_internet THEN implement_validation
  
INFERENCE: forward_chain | backward_chain | resolution
```

#### 4. Constraints (CSP)
Based on AIMA Chapter 6 (Constraint Satisfaction)

```markdown
VARIABLES:
  files: integer
  complexity: [trivial, simple, moderate, complex]
  time_hours: real

DOMAINS:
  files: [1..3]
  complexity: [trivial, simple]
  time_hours: [0..8]

CONSTRAINTS:
  - files <= 2
  - complexity != complex
  - time_hours < 4

SOFT_CONSTRAINTS:
  - prefer files = 1
  - minimize complexity
```

#### 5. Planning
Based on AIMA Chapter 11 (Planning)

```markdown
INITIAL_STATE:
  - empty_project
  - no_dependencies

GOAL_STATE:
  - has_working_api
  - all_tests_pass
  - documented

OPERATORS:
  - create_file(name):
      PRE: not exists(name)
      POST: exists(name)
  - implement_endpoint(endpoint):
      PRE: exists(main_file)
      POST: provides(endpoint)
```

#### 6. Decision Analysis
Based on AIMA Chapter 17 (Making Complex Decisions)

```markdown
# Decision Tree
DECISION_TREE:
  root: choose_framework
    - Flask:
        probability: 0.9
        outcomes:
          - success: {prob: 0.95, utility: 8}
          - issues: {prob: 0.05, utility: 3}
    - FastAPI:
        probability: 0.1
        outcomes:
          - success: {prob: 0.8, utility: 9}
          - issues: {prob: 0.2, utility: 2}

# Risk Analysis
RISKS:
  - technical_debt:
      probability: 0.3
      impact: high
      mitigation: add_refactor_sprint
  - scope_creep:
      probability: 0.7
      impact: medium
      mitigation: hard_constraints

# Sensitivity Analysis
SENSITIVITY:
  time_budget: high    # Small changes greatly affect outcome
  team_size: medium
  quality_target: low
```

#### 7. Agile Planning
For teams using Scrum, Kanban, or other Agile methodologies

```markdown
# Sprint Configuration
SPRINT:
  number: 15
  duration: 2_weeks
  capacity: 120_points  # team velocity
  goals: [complete_auth, refactor_api, fix_tech_debt]

# Backlog Definition
BACKLOG:
  epic/user-management:
    stories: [create_user, update_user, delete_user]
    priority: high
    business_value: 89
    
  story/create_user:
    points: 8
    user_story:
      as_a: "platform administrator"
      i_want: "to create new user accounts"
      so_that: "I can onboard team members"
    acceptance_criteria:
      - validates_email_format
      - prevents_duplicates
      - sends_welcome_email
    given_when_then:
      - given: "valid user data"
        when: "I submit the create user form"
        then: "a new user account is created and welcome email sent"
      - given: "duplicate email address"
        when: "I submit the create user form"
        then: "I see an error message and no user is created"
    tasks:
      - implement_endpoint: 3h
      - add_validation: 2h
      - write_tests: 3h
    definition_of_done:
      - code_reviewed
      - tests_pass
      - documented

# User Story Templates
USER_STORY_FORMAT:
  standard:
    as_a: <user_type>
    i_want: <action>
    so_that: <benefit>
    
  extended:
    as_a: <user_type>
    i_want: <action>
    so_that: <benefit>
    given: <context>
    when: <trigger>
    then: <expected_outcome>
    
  technical:
    as_a: <system_component>
    i_need: <capability>
    so_that: <technical_benefit>

# Team Composition
TEAM:
  scrum_master: alice
  product_owner: bob
  developers:
    - {name: charlie, capacity: 30h, skills: [backend, database]}
    - {name: diana, capacity: 40h, skills: [frontend, testing]}
    
# Ceremonies
CEREMONIES:
  daily_standup:
    duration: 15m
    questions: [did_yesterday, doing_today, blockers]
    
  sprint_planning:
    duration: 2h
    outputs: [sprint_goal, sprint_backlog]
    
  retrospective:
    duration: 1h
    discuss: [went_well, needs_improvement, action_items]

# Velocity Tracking
VELOCITY:
  historical: [85, 92, 88, 95, 90]  # last 5 sprints
  average: 90
  confidence: 0.85

# Agile Metrics
METRICS:
  burndown_rate: points_per_day
  cycle_time: story_start_to_done
  lead_time: story_created_to_done
  wip_limit: 3

# Kanban Board
KANBAN:
  columns: [backlog, ready, in_progress, review, done]
  wip_limits:
    in_progress: 3
    review: 2
  policies:
    ready: "groomed AND estimated"
    done: "meets definition_of_done"
```

#### 10. Agile Execution Commands

```markdown
# Sprint Execution
SPRINT_COMMANDS:
  START_SPRINT sprint_number WITH goals
  PULL story FROM backlog WHERE ready
  MOVE story TO in_progress
  BLOCK story BECAUSE reason
  UNBLOCK story
  COMPLETE story
  END_SPRINT RETURN velocity

# Estimation
ESTIMATE story USING planning_poker
SPLIT story INTO subtasks
REFINE story ADD acceptance_criteria

# Tracking
BURNDOWN sprint SHOW remaining_points
VELOCITY team CALCULATE average
IMPEDIMENT report ESCALATE_TO scrum_master

# Flow Management  
LIMIT wip_column TO max_items
EXPEDITE story WITH reason
SWARM_ON story WITH [developers]
```

#### 11. Dual-Track Agile
For teams running parallel discovery and delivery tracks

```markdown
# Track Configuration
DUAL_TRACK:
  discovery:
    type: continuous
    lead: product_manager
    horizon: 2-4_sprints_ahead
    outputs: [validated_requirements, prd, prototypes]
    
  delivery:
    type: sprint_based
    lead: scrum_master
    cadence: 2_weeks
    inputs: [ready_stories, acceptance_criteria]

# Discovery Track Activities
DISCOVERY_TRACK:
  research:
    - user_interviews
    - market_analysis
    - competitive_research
    - technical_feasibility
    
  validation:
    - prototype_testing
    - stakeholder_review
    - architecture_review
    - risk_assessment
    
  outputs:
    - prd_document:
        format: structured
        sections: [problem, solution, success_metrics]
        approval_required: true
    - cml_translation:
        from: prd
        to: user_stories
        includes: acceptance_criteria

# Handoff Protocol
DISCOVERY_TO_DELIVERY:
  entry_criteria:
    - prd_approved
    - technical_feasibility_confirmed
    - acceptance_criteria_defined
    - story_estimated
    
  handoff_meeting:
    participants: [product, tech_lead, designers]
    agenda:
      - review_requirements
      - clarify_acceptance_criteria
      - identify_risks
      - confirm_readiness
      
  definition_of_ready:
    - user_story_format_complete
    - acceptance_criteria_clear
    - dependencies_identified
    - estimate_agreed

# Delivery Track Execution  
DELIVERY_TRACK:
  sprint_planning:
    pull_from: discovery_track.ready_queue
    capacity: team_velocity * 0.9
    
  daily_sync:
    discovery_update: new_findings
    delivery_feedback: implementation_reality
    
  feedback_loop:
    delivery_to_discovery:
      - technical_constraints_found
      - user_feedback_from_demos
      - implementation_insights
```

#### 12. User Story Format
Standard template for capturing requirements from user perspective

```markdown
# Basic Format
USER_STORY:
  as_a: <user_type>
  i_want: <to_perform_action>  
  so_that: <achieve_benefit>

# Extended Format with Acceptance Criteria
USER_STORY:
  as_a: <user_type>
  i_want: <to_perform_action>
  so_that: <achieve_benefit>
  
  acceptance_criteria:
    - given: <initial_context>
      when: <action_taken>
      then: <expected_outcome>
    - given: <error_context>
      when: <action_taken>
      then: <error_handling>

# Example Implementation
story/multi_factor_auth:
  as_a: "security-conscious user"
  i_want: "to enable 2FA on my account"
  so_that: "my data is protected even if password is compromised"
  
  acceptance_criteria:
    - given: "2FA is not enabled"
      when: "I enable 2FA and scan QR code"
      then: "2FA is active and backup codes are shown"
    - given: "2FA is enabled"
      when: "I login with correct password"
      then: "I am prompted for 2FA code"
    - given: "2FA is enabled and I lost my device"
      when: "I use a backup code"
      then: "I can access my account"
      
  tasks:
    - implement_totp_generation
    - create_qr_code_endpoint
    - add_2fa_verification_middleware
    - generate_backup_codes
    - update_login_flow
```

#### 12. Utility Function
Based on AIMA Chapter 16 (Making Decisions)

```markdown
UTILITY:
  working_code: 0.5
  readability: 0.3
  performance: 0.1
  maintainability: 0.1
  
OPTIMIZE: maximize_utility | satisfice | minimize_regret
```

### Behavioral Directives

```markdown
REWARDS:
  high: [meets_requirements, under_time_limit]
  moderate: [readable_code, has_tests]
  low: [follows_conventions]

PENALTIES:
  severe: [over_engineering, scope_creep]
  high: [excessive_abstraction, premature_optimization]
  moderate: [missing_docstrings]
```

## Example Files

### PRD to CSL Translation Example

#### Original PRD (discovery output)
```markdown
# Real-time Collaboration Feature PRD

## Problem Statement
Remote teams struggle to collaborate on documents, leading to version conflicts and lost work. Users report spending 30+ minutes daily reconciling changes.

## Proposed Solution  
Implement real-time collaborative editing similar to Google Docs.

## Success Metrics
- Reduce version conflicts by 95%
- Enable 10+ simultaneous editors
- Sub-200ms latency for updates
```

#### Translated to CSL Stories (delivery input)
```markdown
epic/realtime_collaboration:
  business_value: high
  validated_by: discovery_track
  
  story/presence_awareness:
    as_a: "document editor"
    i_want: "to see who else is viewing/editing"
    so_that: "I can coordinate changes with teammates"
    
    acceptance_criteria:
      - given: "multiple users in document"
        when: "a user joins or leaves"  
        then: "presence indicators update within 1 second"
      - given: "user is editing"
        when: "another user hovers over their cursor"
        then: "tooltip shows editor's name"
        
    points: 5
    ready: true
    
  story/conflict_resolution:
    as_a: "document editor"
    i_want: "automatic merge of non-conflicting changes"
    so_that: "I don't lose work when others edit"
    
    acceptance_criteria:
      - given: "two users edit different paragraphs"
        when: "both save within 5 seconds"
        then: "both changes are preserved"
      - given: "two users edit same sentence"
        when: "conflict detected"
        then: "last-write-wins with ability to restore"
        
    points: 13  # Needs splitting
    ready: false
```

### Root Configuration (CLAUDE.md)

```markdown
# Project Configuration

## Metadata
```csl
version: 1.0
project: mvp_user_api
methodology: dual_track_agile
```

## Composition and Inheritance

Agents can inherit from parent configurations:

```markdown
# Child agent
extends: ../../CLAUDE.md

# Override specific values
CONSTRAINTS:
  - inherit: all
  - override: time_hours < 2
  - add: must_use_typescript
```

## Verification

CSL enables verification through explicit constraints:

```markdown
# In validator.md
VERIFY:
  - all_constraints_satisfied
  - no_severe_penalties
  - goal_state_reached
  - utility_threshold > 0.7
```

## Best Practices

1. **Start with CLAUDE.md** - Define project-wide constraints
2. **Be explicit about penalties** - Claude tends toward thoroughness
3. **Use FACTS for context** - Helps inference
4. **Prefer hard constraints** over soft guidance
5. **Define clear GOAL_STATE** - Prevents scope creep
6. **Set UTILITY weights** - Makes trade-offs explicit
7. **Write user stories from the user's perspective** - Not technical implementation
8. **Include acceptance criteria** - Clear definition of done

### spec-kit Integration Best Practices

1. **Maintain single source of truth** - Specs in spec-kit, stories in CSL
2. **Automate translation** - Don't manually copy requirements
3. **Version control everything** - Both specs and CSL files
4. **Use traceability** - Link stories back to spec sections
5. **Review before translation** - Ensure specs are complete
6. **Lock versions during sprints** - Prevent mid-sprint changes

### User Story Best Practices

**Good User Story Characteristics (INVEST):**
- **Independent** - Can be developed separately
- **Negotiable** - Details can be discussed
- **Valuable** - Delivers user value
- **Estimable** - Team can size it
- **Small** - Fits in a sprint
- **Testable** - Clear acceptance criteria

**Examples:**
```cml
# Good - User-focused
story/password_reset:
  as_a: "registered user"
  i_want: "to reset my password"
  so_that: "I can regain access when I forget it"

# Bad - Technical implementation
story/bad_example:
  as_a: "developer"
  i_want: "to add a Redis cache"
  so_that: "the database has less load"
  
# Better - Focuses on user benefit
story/improved:
  as_a: "mobile app user"  
  i_want: "search results to load instantly"
  so_that: "I don't have to wait while shopping"
```

### When to Use Planning Types

**Basic Planning (STRIPS-style):**
- Simple sequential tasks
- Clear preconditions and effects
- Single agent execution
- Example: "Build a CRUD API"

**Agile Planning:**
- Iterative development cycles
- Team-based execution
- Changing requirements
- Empirical process control
- Example: "Manage 2-week sprints for a 6-month project"

**Dual-Track Agile:**
- Complex products needing research
- Uncertain requirements
- Need continuous discovery
- Separate research from delivery concerns
- Example: "Build a new ML-powered feature while researching user needs"

**spec-kit + CSL:**
- Formal specification required
- Multiple stakeholder review needed
- Compliance or audit requirements
- Complex technical architectures
- Example: "Build a payment system with regulatory compliance"

### spec-kit Integration Guidelines

**Use spec-kit when:**
1. Multiple teams need to align on requirements
2. Formal review process is required
3. Changes need careful impact analysis
4. Audit trail is necessary
5. Architecture decisions need documentation

**Use CSL directly when:**
1. Requirements are well understood
2. Single team ownership
3. Rapid iteration needed
4. Informal specifications sufficient

### Dual-Track Best Practices

1. **Discovery stays 2-4 sprints ahead** - Not too far (waste) or too close (blocking)
2. **Maintain a ready queue** - 6-8 validated stories minimum
3. **Regular sync meetings** - Weekly discovery-delivery alignment
4. **Clear handoff criteria** - Definition of Ready strictly enforced
5. **Feedback loops** - Implementation insights flow back to discovery
6. **Separate metrics** - Track discovery validation rate vs delivery velocity

## Claude Verbs

CML defines a precise vocabulary of atomic operations that agents can perform, inspired by assembly language instructions. These verbs provide unambiguous commands that compose into complex behaviors.

### File Operations
```cml
CREATE <target> [FROM <template>]
READ <source> [INTO <variable>]
UPDATE <target> [SET <properties>]
DELETE <target> [IF <condition>]
MOVE <source> TO <destination>
COPY <source> TO <destination>
```

### Code Operations
```cml
IMPLEMENT <feature> [WITH <constraints>]
REFACTOR <target> [MAINTAINING <invariants>]
OPTIMIZE <metric> IN <scope>
SIMPLIFY <target> [UNTIL <condition>]
EXTRACT <pattern> FROM <source> AS <name>
INLINE <abstraction> IN <target>
```

### Analysis Operations
```cml
ANALYZE <target> FOR <properties>
EVALUATE <expression> AGAINST <criteria>
VERIFY <invariant> IN <scope>
CHECK <condition> [ELSE <action>]
MEASURE <metric> OF <target>
COMPARE <a> WITH <b> ON <dimensions>
```

### Control Flow
```cml
IF <condition> THEN <verb> [ELSE <verb>]
WHILE <condition> DO <verb>
FOR EACH <item> IN <collection> DO <verb>
SEQUENCE [<verb1>, <verb2>, ...]
PARALLEL [<verb1>, <verb2>, ...]
```

### Planning Operations
```cml
PLAN <goal> [USING <strategy>]
DECOMPOSE <task> INTO <subtasks>
SCHEDULE <actions> [WITH <constraints>]
PRIORITIZE <items> BY <criteria>
```

### Agile Verbs
```cml
# Backlog Management
GROOM <story> SET <criteria>
PRIORITIZE <backlog> BY <value/effort>
ESTIMATE <story> RETURN <points>
SPLIT <story> INTO <smaller_stories>
WRITE_STORY <feature> AS <user> WANTING <action> FOR <benefit>

# Sprint Operations
START_SPRINT <number> WITH <goals>
COMMIT <stories> TO <sprint>
PULL <story> FROM <backlog>
SWARM <team> ON <blocker>
BURNDOWN <sprint> SHOW <progress>
RETROSPECT <sprint> IDENTIFY <improvements>

# Flow Control
MOVE <story> TO <column>
LIMIT <column> WIP <number>
BLOCK <story> BECAUSE <impediment>
EXPEDITE <story> [WITH <reason>]

# Team Coordination
STANDUP <team> REPORT <status>
DEMO <feature> TO <stakeholders>
PAIR <developer1> WITH <developer2> ON <task>
REVIEW <code> REQUIRE <approvals>

# User Story Operations
DEFINE_STORY:
  AS_A <user_type>
  I_WANT <action>
  SO_THAT <benefit>
  
ACCEPT_WHEN:
  GIVEN <context>
  WHEN <action>
  THEN <outcome>
```

### Agile Composite Example

```cml
# Sprint Planning Session
SPRINT sprint_15:
  capacity: CALCULATE velocity_average * team_capacity
  
  PRIORITIZE backlog BY business_value / effort
  
  FOR EACH story IN backlog DO
    IF story.ready AND total_points < capacity THEN
      ESTIMATE story USING planning_poker
      COMMIT story TO sprint_15
      DECOMPOSE story INTO tasks
      
  START_SPRINT sprint_15 WITH committed_stories

# Daily Execution
DAILY:
  STANDUP team REPORT [yesterday, today, blockers]
  
  FOR EACH developer IN team DO
    IF developer.current_task.done THEN
      PULL next_task FROM sprint_backlog
      MOVE task TO in_progress
      
  IF blocked_tasks.count > 0 THEN
    SWARM available_devs ON blocked_tasks

# Sprint Monitoring  
MONITOR:
  BURNDOWN sprint_15 SHOW remaining_points
  IF burndown.trend > ideal_burndown THEN
    ASSESS_RISK sprint_goal
    DECIDE descope_stories OR add_resources
```

### Dual-Track Composite Example

```cml
# Weekly Dual-Track Flow
WEEKLY_CYCLE:
  # Monday - Discovery Review
  discovery_track:
    REVIEW research_findings
    PRIORITIZE experiments BY learning_value
    PROTOTYPE solutions FOR user_testing
    
  # Tuesday - Translation Work  
  translation:
    SELECT validated_features FROM research
    TRANSLATE requirements TO user_stories
    WRITE acceptance_criteria WITH given_when_then
    ESTIMATE complexity WITH delivery_team
    
  # Wednesday - Handoff Meeting
  handoff:
    PRESENT ready_stories TO delivery_team
    CLARIFY acceptance_criteria
    CONFIRM technical_feasibility
    MOVE stories TO ready_queue
    
  # Thursday - Delivery Sprint
  delivery_track:
    PULL stories FROM ready_queue
    IMPLEMENT features IN sprint
    DISCOVER technical_constraints
    
  # Friday - Feedback Loop
  feedback:
    DEMO completed_features
    COLLECT user_feedback  
    IDENTIFY new_constraints
    FEEDBACK insights TO discovery_track
```

### OR-Style Composite Example

```cml
# Project Planning with Resources
RESOURCES:
  $devs = 3
  $budget = 100000
  $deadline = 30d

ACTIVITIES:
  $tasks = [api, frontend, database, testing]

# Find optimal allocation
CRITICAL_PATH $tasks RETURN $cp
ALLOCATE $devs TO $tasks MINIMIZING makespan

FOR EACH task IN $cp DO
  ASSESS_RISK task RETURN $risk
  IF $risk.impact > high THEN
    CONTINGENCY task FALLBACK simplify_task
    
# Run simulation
MONTE_CARLO 1000 FOR project_completion
SENSITIVITY_ANALYSIS deadline RETURN $impact

# Make decision
DECIDE proceed IF completion_probability > 0.95
```

### spec-kit Integration Verbs
```csl
# Specification Operations
IMPORT <spec> FROM spec-kit
PARSE <spec> USING <schema>
VALIDATE <spec> AGAINST <template>
TRACE <requirement> TO <implementation>

# Translation Operations
EXTRACT <requirements> FROM <spec>
MAP <spec.section> TO <csl.component>
GENERATE <stories> FROM <requirements>
LINK <story> TO <spec.id#section>

# Version Control
LOCK <spec.version> FOR <sprint>
DIFF <spec.v1> WITH <spec.v2>
PROPAGATE <changes> TO <affected_stories>
DEPRECATE <story> WHEN <spec.removed>

# Quality Assurance
VERIFY <coverage> OF <requirements>
AUDIT <traceability> FROM <spec> TO <tests>
REPORT <implementation_status> BY <spec.section>
```

### Dual-Track Verbs
```csl
# Discovery Operations
RESEARCH <topic> USING <method>
INTERVIEW <user_type> ABOUT <pain_points>
PROTOTYPE <solution> FOR <testing>
VALIDATE <assumption> WITH <evidence>
SYNTHESIZE <findings> INTO <prd>

# PRD Translation Operations  
PARSE <prd> EXTRACT <requirements>
IDENTIFY <user_types> FROM <stakeholders>
MAP <requirement> TO <user_story>
CONVERT <success_metric> TO <acceptance_criteria>
TRANSFORM <constraint> TO <story_points>
TAG <story> WITH <validation_source>

# Queue Management
READY <story> FOR <delivery>
MAINTAIN <queue> DEPTH <count>
PRIORITIZE <queue> BY <value/effort>

# Track Coordination
SYNC <discovery> WITH <delivery>
HANDOFF <story> WITH <context>
FEEDBACK <learning> TO <discovery>
ALERT IF <queue> BELOW <threshold>
```

### Hooks (Aspect-Oriented)
```cml
BEFORE <operation> DO <verb>
AFTER <operation> DO <verb>
AROUND <operation> DO <verb>
INSTEAD_OF <operation> DO <verb>
ON_ERROR <operation> DO <verb>
```

### Composite Example

```csl
# API Implementation Task
SEQUENCE [
  CREATE app.py FROM flask_template,
  
  FOR EACH endpoint IN [GET, POST, PUT, DELETE] DO
    IMPLEMENT endpoint WITH constraints.simple,
    
  VERIFY all_endpoints_accessible,
  
  IF complexity > threshold THEN
    REFACTOR app.py MAINTAINING functionality
]

# Add monitoring hooks
BEFORE each_endpoint DO
  ANALYZE request FOR validation_needs
  
AFTER each_endpoint DO
  VERIFY response_format
  
ON_ERROR any_operation DO
  CREATE error_log
  SIMPLIFY implementation
```

### Verb Modifiers

Verbs can be modified with standard qualifiers:

```csl
QUICKLY CREATE  # Optimize for speed over quality
SAFELY DELETE   # Include confirmation/backup
FULLY IMPLEMENT # Complete implementation, no TODOs
PARTIALLY READ  # Read only what's needed
ATOMICALLY UPDATE # All-or-nothing operation
RECURSIVELY ANALYZE # Include all dependencies
```

### Assembly-Style Format

For precise control, CSL supports an assembly-style syntax:

```csl
; Register-style variables
$target = "api/routes.py"
$complexity = MEASURE complexity OF $target

; Conditional jump
CMP $complexity > 10
JNZ simplify_section

; Direct operations
:main_flow
IMPLEMENT user_crud IN $target
VERIFY tests_pass
JMP end

:simplify_section  
REFACTOR $target MAINTAINING api_contract
SUB $complexity 3
JMP main_flow

:end
RETURN success
```

### Verb Constraints

Each verb can have pre/post conditions:

```csl
VERB: CREATE
  PRE: NOT EXISTS(target)
  POST: EXISTS(target) AND VALID(target)
  FAIL: ROLLBACK

VERB: REFACTOR  
  PRE: ALL_TESTS_PASS
  POST: ALL_TESTS_PASS AND complexity < before.complexity
  FAIL: RESTORE original
```

### Standard Verb Library

Core verbs that all agents understand:

**Essential CRUD:**
- CREATE, READ, UPDATE, DELETE

**Transformation:**
- TRANSFORM, CONVERT, ADAPT, MIGRATE

**Analysis:**
- ANALYZE, INSPECT, VALIDATE, MEASURE

**Optimization:**
- OPTIMIZE, SIMPLIFY, REDUCE, MINIMIZE

**Composition:**
- COMBINE, SPLIT, MERGE, EXTRACT

**Control:**
- REQUIRE, ENSURE, ASSERT, PREVENT

This verb system ensures consistent, predictable agent behavior while maintaining the flexibility to compose complex operations from simple atoms.

## Acknowledgments

CSL's design philosophy and terminology are based on concepts from:

**"Artificial Intelligence: A Modern Approach" (4th Edition)**  
Stuart Russell and Peter Norvig  
Pearson, 2020

The following AIMA chapters directly influenced CSL components:
- Chapter 2: Intelligent Agents → Agent types and environment specifications
- Chapter 3-4: Solving Problems by Searching → Search strategies and heuristics
- Chapter 6: Constraint Satisfaction Problems → Constraint syntax
- Chapter 7-9: Logical Agents & First-Order Logic → Facts, rules, and inference
- Chapter 11: Planning → Planning operators and state representations
- Chapter 16: Making Decisions → Utility functions and optimization
- Chapter 17: Making Complex Decisions → Decision trees and sensitivity analysis

Additional frameworks and methodologies integrated into CSL:
- **spec-kit** (GitHub): Structured specification framework for technical documentation
- **Scrum Guide** (Schwaber & Sutherland): Sprint planning and agile ceremonies
- **User Stories Applied** (Mike Cohn): User story format and INVEST criteria
- **Dual-Track Agile** (Marty Cagan): Parallel discovery and delivery tracks

Operations research concepts integrated into CML:
- Critical Path Method (CPM) for project scheduling
- Linear Programming for resource optimization  
- Monte Carlo simulation for risk analysis
- Resource allocation and capacity planning

Agile methodology concepts integrated into CML:
- Scrum framework: sprints, stories, velocity, ceremonies
- User stories (As a/I want/So that) format popularized by Mike Cohn
- Acceptance criteria with Given/When/Then (Gherkin-style)
- Dual-track agile: parallel discovery and delivery tracks
- Kanban: WIP limits, flow management
- Empirical process control and continuous improvement
- Team-based planning and execution

CSL translates these formal AI concepts and software engineering practices into practical directives for Claude Code agents, making rigorous AI theory and modern development practices accessible through natural language specifications.