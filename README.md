# oracle-spec

A declarative spec for encoding human norms for system behavior.

The authors of an AI oracle drive what constitutes good AI behavior.

## What is an Oracle?

An AI oracle is a system that provides guidance, decisions, or classifications based on human expertise and values encoded in a structured specification.

## What is an Oracle Spec?

A declarative configuration system for AI behavior governance that allows domain experts to define what constitutes correct AI behavior without needing machine learning expertise.

## Motivation

### Principles

- do not need to code
- can swap different competing AI agent candidates
- can steer the fine-tuning of AI agents
- can get feedback on their directives
- can formulate wholistic evaluations based on a variety of competing concerns
- can formulate evaluation based on many pre and post conditions (states)
- can read and share an AI oracle
- can familiarize themselves with a standard

## Core Innovation

This addresses the fundamental **"alignment specification" problem** - how do domain experts encode their knowledge and values into AI systems without needing to be ML engineers.

## Key Strengths

**1. Separation of Concerns**
```yaml
# Subject matter experts write the "what"
contract.yaml: 
  behavior: classify_biohacking_relevance
  criteria: intervention + measurable_outcome

# ML engineers handle the "how" 
model_config.py:
  architecture: transformer
  training: fine_tune_on_oracle_spec
```

**2. Composability & Competition**
- Multiple AI agents can implement the same oracle spec
- A/B test different models against the same behavioral standard
- Benchmark progression: "GPT-4 achieves 73% oracle compliance, Claude-4 achieves 81%"

**3. Version Control for Human Values**
```bash
git diff oracle-spec-v1.2..v1.3
# - intervention_required: true
# + intervention_actionability_score: >0.7
```

## Real-World Applications

**Healthcare**: Diagnostic assistance oracles with physician-authored specs
**Legal**: Contract analysis oracles with lawyer-authored behavioral rules  
**Finance**: Risk assessment oracles with compliance officer specifications
**Content Moderation**: Community standards encoded as oracle specs

## Technical Architecture Ideas

```yaml
# oracle-spec.yaml
apiVersion: oracle/v1
kind: BehaviorSpec
metadata:
  domain: biohacking_relevance
  authors: [boris, medical_experts]
  version: 2.1.0

spec:
  classification_criteria:
    required_all: [intervention, measurable_outcome]
    confidence_thresholds:
      high: 0.9  # unambiguous cases
      medium: 0.7  # clear with minor ambiguity
      low: 0.6   # edge cases
  
  examples:
    positive_exemplars: ./examples/relevant_cases.yaml
    negative_exemplars: ./examples/irrelevant_cases.yaml
    edge_cases: ./examples/borderline_cases.yaml
    
  validation:
    expert_agreement_threshold: 0.8
    human_evaluation_sample_size: 100
    
  drift_monitoring:
    performance_metrics: [accuracy, precision, recall, expert_agreement]
    alert_thresholds: {accuracy: "<0.85", expert_agreement: "<0.7"}
```

## Governance Benefits

**Auditability**: "Why did the AI make this decision?" → "It followed oracle-spec v2.1, section 3.4"
**Accountability**: Clear ownership chain from domain expert → oracle spec → AI behavior
**Transparency**: Stakeholders can read and critique the behavioral specification
**Iteration**: Update specs based on real-world performance without retraining models

## Implementation Strategy

1. **Start with our biohacking case** as a reference implementation
2. **Abstract the patterns** we discovered (contracts, examples, analysis)
3. **Create tooling** for oracle spec validation and model evaluation
4. **Build marketplace** where domain experts can publish/version oracle specs

This could be **hugely valuable** for enterprise AI adoption - finally giving domain experts direct control over AI behavior without requiring ML expertise!
