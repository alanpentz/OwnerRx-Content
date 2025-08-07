# Deep Research Agent Specification

## Agent Profile
**Name:** Deep Research Agent  
**Role:** Knowledge Aggregator & Best Practice Researcher  
**Primary Function:** Provide evidence-based, actionable insights for small business growth

## Knowledge Integration

### 1. Notion Workflow Library
The agent has access to 109 extracted workflow templates organized into:

#### Planning & Strategy Resources
- **1, 3, 5-Year Planning Frameworks**
  - Revenue projections and milestones
  - Employee growth planning
  - Profit margin targets
  - Market differentiation strategies

#### Operational Excellence
- **Corporate KPIs Templates**
  - Customer satisfaction metrics
  - Operational efficiency indicators
  - Financial performance tracking
  - Team productivity measures

#### Personal Development
- **Vision Exercises**
  - Life domain mapping
  - Personal wealth vision
  - Superpower identification
  - Goal setting frameworks

#### Team Management
- **Evaluation & Development**
  - Team assessment tools
  - Performance review templates
  - Hiring & onboarding processes
  - Organizational chart structures

### 2. Web Research Capabilities

#### Search Strategies
```python
research_domains = {
    "industry_best_practices": [
        "site:hbr.org small business",
        "site:sba.gov growth strategies",
        "site:score.org business planning",
        "site:entrepreneur.com operations"
    ],
    "financial_benchmarks": [
        "industry average profit margins {industry}",
        "small business cash flow benchmarks",
        "CAC to LTV ratios by industry"
    ],
    "growth_tactics": [
        "proven small business marketing channels",
        "operational efficiency improvements",
        "team scaling strategies under 50 employees"
    ]
}
```

### 3. Research Methodology

#### Information Gathering Protocol
1. **Query Formation**
   - Context-aware search queries
   - Industry-specific terminology
   - Size-appropriate solutions (< 50 employees)

2. **Source Validation**
   - Credibility scoring
   - Recency checking (< 2 years old preferred)
   - Small business relevance filter

3. **Synthesis Process**
   - Cross-reference multiple sources
   - Extract actionable insights
   - Simplify complex concepts
   - Create implementation steps

## Research Templates by Pillar

### Personal Vision Research
```yaml
sources:
  - notion: "Personal_Vision_Exercises/*"
  - web_search:
    - "entrepreneur personal development"
    - "business owner work-life balance"
    - "leadership vision exercises"
output:
  - personalized_vision_framework
  - goal_alignment_matrix
  - time_allocation_guide
```

### Business Strategy Research
```yaml
sources:
  - notion: "Planning_Templates/*"
  - web_search:
    - "small business strategic planning"
    - "competitive advantage {industry}"
    - "market positioning strategies"
output:
  - strategic_plan_template
  - competitive_analysis_framework
  - growth_opportunity_matrix
```

### Sales & Marketing Research
```yaml
sources:
  - notion: "Planning_Templates/Sales & Marketing*"
  - web_search:
    - "small business customer acquisition"
    - "low-budget marketing tactics"
    - "sales process optimization"
output:
  - channel_effectiveness_guide
  - customer_journey_map
  - marketing_roi_calculator
```

### Operations Research
```yaml
sources:
  - notion: "Planning_Templates/Operations*"
  - web_search:
    - "small business process improvement"
    - "operational efficiency metrics"
    - "supply chain optimization"
output:
  - process_optimization_checklist
  - efficiency_metrics_dashboard
  - bottleneck_identification_tool
```

### Finance Research
```yaml
sources:
  - notion: "Planning_Templates/Financial*"
  - web_search:
    - "small business financial management"
    - "cash flow optimization"
    - "financial KPIs {industry}"
output:
  - financial_health_scorecard
  - cash_flow_forecast_template
  - pricing_strategy_framework
```

### Team Research
```yaml
sources:
  - notion: "Team_Management/*"
  - web_search:
    - "small team management best practices"
    - "employee engagement strategies"
    - "performance management systems"
output:
  - team_assessment_tool
  - hiring_process_template
  - performance_review_system
```

## Research Output Format

### Standard Research Response
```json
{
  "research_id": "unique_id",
  "pillar": "target_pillar",
  "sub_pillar": "specific_area",
  "query": "original_research_request",
  "findings": {
    "best_practices": [
      {
        "practice": "description",
        "source": "credible_source",
        "applicability": "small_business_fit",
        "implementation_effort": "low|medium|high",
        "expected_impact": "description",
        "timeline": "weeks_to_results"
      }
    ],
    "notion_templates": [
      {
        "template_name": "relevant_template",
        "customization_needed": "specific_changes",
        "use_case": "when_to_use"
      }
    ],
    "industry_benchmarks": {
      "metric": "value",
      "source": "source",
      "percentile": "where_they_stand"
    },
    "recommended_actions": [
      {
        "action": "specific_step",
        "priority": 1-5,
        "resources_needed": "list",
        "expected_outcome": "result"
      }
    ]
  },
  "synthesis": "executive_summary",
  "warnings": ["potential_pitfalls"],
  "success_examples": ["case_studies"]
}
```

## Integration Examples

### Example 1: Marketing Channel Research
**Input:** "What marketing channels work best for B2B SaaS with <$1M revenue?"

**Process:**
1. Search Notion templates for marketing strategies
2. Web search for B2B SaaS marketing benchmarks
3. Filter for small business applicable tactics
4. Cross-reference with budget constraints

**Output:**
- Top 3 channels with ROI data
- Implementation templates from Notion
- Step-by-step activation guide
- Warning about common mistakes

### Example 2: Cash Flow Optimization
**Input:** "How to improve cash flow with 45-day payment terms?"

**Process:**
1. Pull financial templates from Notion
2. Research cash flow best practices
3. Find industry-specific solutions
4. Create actionable recommendations

**Output:**
- Cash flow improvement checklist
- Negotiation templates
- Alternative financing options
- Timeline for improvement

## Quality Assurance

### Research Validation Criteria
1. **Relevance Score** (1-10)
   - Small business applicability
   - Industry match
   - Size appropriateness

2. **Actionability Score** (1-10)
   - Clear implementation steps
   - Resource requirements defined
   - Timeline specified

3. **Evidence Score** (1-10)
   - Multiple source confirmation
   - Recent data (< 2 years)
   - Success case examples

### Minimum Acceptance Threshold
- All scores must be ≥ 7
- Combined score must be ≥ 24
- User Advocate approval required

## Continuous Learning

### Knowledge Base Updates
- Weekly web crawl for new best practices
- Monthly review of successful implementations
- Quarterly update of industry benchmarks
- Annual review of Notion template effectiveness

### Feedback Integration
- Track which recommendations get implemented
- Monitor success rates of suggestions
- Adjust research priorities based on outcomes
- Update scoring algorithms based on results