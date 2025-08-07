# OwnerRx Agent System Architecture

## System Overview

The OwnerRx platform uses a multi-agent system to help small business owners grow systematically across 6 core pillars. Each agent has specialized knowledge and responsibilities, working together to provide personalized, actionable guidance.

## Agent Hierarchy

```
┌─────────────────────────────────────┐
│     ORCHESTRATOR AGENT              │
│   (Master Coordinator)              │
└──────────────┬──────────────────────┘
               │
     ┌─────────┴─────────┬──────────────┬──────────────┐
     │                   │              │              │
┌────▼─────┐    ┌────────▼────────┐  ┌─▼──────────┐  │
│   DEEP   │    │      USER       │  │  QUALITY   │  │
│ RESEARCH │◄───┤    ADVOCATE     │  │  CONTROL   │  │
│  AGENT   │    │     AGENT       │  │   AGENT    │  │
└─────┬────┘    └────────┬────────┘  └─────┬──────┘  │
      │                  │                  │         │
      └──────────────────┼──────────────────┘         │
                         │                             │
        ┌────────────────┼─────────────────────────────┤
        │                │                             │
┌───────▼──────┐ ┌───────▼──────┐ ┌──────▼──────┐ ┌──▼─────┐
│   PERSONAL   │ │   BUSINESS   │ │   SALES &   │ │        │
│    VISION    │ │   STRATEGY   │ │  MARKETING  │ │  MORE  │
│ PILLAR AGENT │ │ PILLAR AGENT │ │PILLAR AGENT │ │PILLARS │
└──────────────┘ └──────────────┘ └─────────────┘ └────────┘
        │                │                │
   [Sub-Agents]     [Sub-Agents]     [Sub-Agents]
```

## Core Agents

### 1. ORCHESTRATOR AGENT
**Role:** Master coordinator ensuring all agents work in harmony
**Responsibilities:**
- Route requests to appropriate pillar agents
- Manage inter-agent communication
- Track overall progress across all pillars
- Ensure consistency across recommendations
- Manage workflow sequences
- Handle conflict resolution between agent recommendations
- **ENFORCE ALAN'S CORE RULES (Non-Negotiable)**

**Alan's Universal Operating Principles:**
1. **One Tweak Rule:** Only allow ONE major change per pillar at a time
2. **Data Over BS:** Require metrics for all claims and recommendations
3. **Blunt Truth:** No sugar-coating - tell owners what they need to hear
4. **Trade-offs Explicit:** Every recommendation must state what's being sacrificed

**Communication Protocol:**
```json
{
  "agent_id": "orchestrator",
  "capabilities": [
    "route_request",
    "coordinate_multi_pillar",
    "track_progress",
    "resolve_conflicts"
  ],
  "state_tracking": {
    "active_pillars": [],
    "pending_tasks": [],
    "completed_milestones": []
  }
}
```

### 2. DEEP RESEARCH AGENT
**Role:** Knowledge aggregator and best-practice researcher
**Responsibilities:**
- Search web for small business best practices
- Integrate Notion workflow templates
- Maintain knowledge base of proven methodologies
- Update tactics based on industry trends
- Provide evidence-based recommendations

**Knowledge Sources:**
- Web search APIs for current best practices
- Notion workflow library (already extracted)
- Industry benchmarks and standards
- Case studies and success patterns
- Academic research on business growth

**Integration with Notion Workflows:**
```python
notion_knowledge_base = {
    "planning_templates": "/Users/alanpentz/Notion_Workflows_Organized/Planning_Templates/",
    "personal_vision": "/Users/alanpentz/Notion_Workflows_Organized/Personal_Vision_Exercises/",
    "team_management": "/Users/alanpentz/Notion_Workflows_Organized/Team_Management/",
    "client_portal": "/Users/alanpentz/Notion_Workflows_Organized/Client_Portal_Template/"
}
```

### 3. USER ADVOCATE AGENT
**Role:** Guardian of small business owner needs + Alan's BS Detector
**Responsibilities:**
- Ensure recommendations are practical and achievable
- Prevent overwhelm by limiting complexity
- Validate resource requirements are reasonable
- Advocate for simplicity and clarity
- Monitor cognitive load of recommendations
- **CALL OUT OWNER DELUSIONS**

**Validation Criteria:**
- Implementation time: < 4 hours per week
- Team requirements: Achievable with < 10 people
- Budget constraints: No expensive consultants required
- Complexity level: Understandable without MBA
- ROI timeline: Results visible within 90 days
- **Reality Check: Would a skeptical customer believe this?**
- **One-Tweak Test: Is this truly ONE change or multiple disguised?**
- **Measurement Test: Can we track this with numbers?**

### 4. QUALITY CONTROL AGENT
**Role:** Ensure consistency and completeness
**Responsibilities:**
- Verify all sub-pillars follow 7-step rhythm
- Check data completeness
- Validate scoring logic
- Ensure deliverables are actionable
- Monitor progress tracking accuracy

---

## The 6 Pillar Agents

Each pillar agent manages its domain with specialized knowledge and sub-agents for specific workflows.

### Standard 7-Step Rhythm (All Pillars Follow)
1. **Context Load** - Recall owner profile, pillar stage, past tasks
2. **Clarify Objective** - "What does success look like in 90 days?"
3. **Collect Baseline Data** - Pull metrics, documents, or request missing info
4. **Personalize Questions** - Adaptive questioning based on business context
5. **Diagnose/Score** - Compare to best-practice thresholds
6. **Recommend Plan** - 3-5 prioritized actions + supporting artifacts
7. **Commit & Schedule** - Log tasks, set reviews, update stage

### Data Layer Architecture

| Layer | What it Stores | Who Writes | Example Fields |
|-------|---------------|------------|----------------|
| Owner Profile | Stable facts | Owner (once) | Industry, Headcount, Geography, Risk tolerance |
| Live Metrics | Dynamic numbers | Agent pulls | Cash buffer, CAC, NPS, Revenue growth |
| Workflow Knowledge | Best practices | System (static) | Checklists, scoring rules, templates |
| Session State | Progress tracking | Agent auto-updates | Stage, Last score, Tasks completed |

---

## Communication Protocol

### Inter-Agent Message Format
```json
{
  "from_agent": "agent_id",
  "to_agent": "agent_id",
  "message_type": "request|response|notification",
  "priority": "high|medium|low",
  "payload": {
    "action": "specific_action",
    "data": {},
    "context": {}
  },
  "timestamp": "ISO-8601",
  "requires_response": true
}
```

### Agent Coordination Rules
1. All agents report to Orchestrator
2. Cross-pillar dependencies route through Orchestrator
3. Research Agent serves all pillars equally
4. User Advocate has veto power on complexity
5. Quality Control validates before user delivery

---

## Implementation Architecture

### Agent Base Class
```python
class BaseAgent:
    def __init__(self, agent_id, pillar=None):
        self.agent_id = agent_id
        self.pillar = pillar
        self.knowledge_base = {}
        self.current_context = {}
    
    def execute_rhythm(self, owner_profile, session_state):
        # Standard 7-step implementation
        context = self.context_load(owner_profile, session_state)
        objective = self.clarify_objective(context)
        baseline = self.collect_baseline(context)
        questions = self.personalize_questions(baseline)
        diagnosis = self.diagnose_score(baseline, questions)
        plan = self.recommend_plan(diagnosis)
        commitment = self.commit_schedule(plan)
        return commitment
```

### Maturity Ladder Framework
```python
maturity_stages = {
    0: "Foundation - Easy wins, basic structure",
    1: "Stabilize - Measure and standardize",
    2: "Optimize - Scale and improve efficiency",
    3: "Innovate - Future-proof and lead market"
}
```

---

## Deployment Strategy

### Phase 1: Core Infrastructure
- Deploy Orchestrator Agent
- Deploy Deep Research Agent
- Deploy User Advocate Agent
- Integrate Notion workflows

### Phase 2: Pillar Agents
- Deploy all 6 Pillar Agents
- Implement standard 7-step rhythm
- Connect to data layers

### Phase 3: Sub-Pillar Agents
- Deploy specialized sub-agents
- Implement workflow-specific logic
- Add scoring and diagnostics

### Phase 4: Optimization
- Add machine learning for personalization
- Implement feedback loops
- Optimize inter-agent communication
- Add predictive recommendations

---

## Success Metrics

### System Health
- Agent response time < 2 seconds
- Inter-agent communication success > 99%
- Knowledge base coverage > 80% of queries

### User Success
- Task completion rate > 70%
- Stage advancement rate > 60% per quarter
- User satisfaction > 4.5/5

### Business Impact
- Revenue growth acceleration
- Operational efficiency improvement
- Team performance enhancement
- Strategic clarity increase