# Harvey AI GraphQL Schema

## Overview

This is a conceptual GraphQL schema for the Harvey AI platform — a domain-specific legal AI system built for elite law firms and in-house legal departments. Harvey does not currently publish a public self-serve API; integrations are arranged through enterprise sales and the Harvey Ecosystem partner program. This schema documents the anticipated API surface based on Harvey's published product capabilities.

## Platform Products Covered

- **Assistant** — question answering, document analysis, and AI-assisted drafting
- **Vault** — secure document storage and bulk document analysis
- **Knowledge** — legal, regulatory, and tax research across primary and secondary sources
- **Workflow Agents** — pre-built and customizable agents for firm-specific legal workflows
- **Harvey Mobile** — mobile access to Harvey capabilities
- **Ecosystem Integrations** — iManage, NetDocuments, Microsoft 365, Westlaw, LexisNexis, and others

## Schema File

The full GraphQL schema is defined in `harvey-ai-schema.graphql`.

## Type Summary

| Domain | Types |
|---|---|
| Matter management | Matter, MatterDetails, MatterType, MatterStatus |
| Document management | Document, DocumentDetails, DocumentType, DocumentAnalysis |
| Legal research | Research, ResearchQuery, ResearchResult, ResearchSource |
| Citations and authorities | Citation, CaseLaw, StatuteRef, RegulationRef |
| Drafting | Draft, DraftDetails, DraftTemplate, TemplateVariable |
| Review | Review, ReviewDetails, ReviewComment |
| Comparison | Compare, CompareDetails, RedlineDetails |
| Clauses | Clause, ClauseDetails, ClauseType |
| Contracts | Contract, ContractDetails, ContractAnalysis |
| Litigation | Litigation, Brief, BriefDetails |
| Memos | Memo, MemoDetails |
| Summaries | Summary, SummaryDetails |
| Timelines | Timeline, TimelineEvent |
| Due diligence | DueDiligence, DueDiligenceReport, Finding |
| Pattern analysis | PatternAnalysis, Pattern |
| Jurisdiction and courts | Jurisdiction, CourtDetails |
| Tasks | Task, TaskDetails |
| Conversations | Conversation, Message, MessageDetails, MessageRole |
| Platform management | Model, APIKey, Token, Organization, TeamDetails |
| Pagination | PageInfo, and Connection types per domain |

## Key Queries

```graphql
# Retrieve a matter and its associated documents
query GetMatter($id: ID!) {
  matter(id: $id) {
    id
    name
    type
    status
    details {
      clientName
      leadAttorney
      caseNumber
      jurisdiction {
        name
        code
      }
    }
    documents {
      nodes {
        id
        name
        type
      }
    }
    timeline {
      events {
        date
        title
        category
      }
    }
  }
}

# Submit a legal research query
mutation SubmitResearch($input: ResearchQueryInput!) {
  submitResearchQuery(input: $input) {
    id
    status
    query {
      text
      jurisdiction {
        name
      }
    }
  }
}

# Analyze a contract
mutation AnalyzeContract($id: ID!) {
  analyzeContract(id: $id, options: {
    extractClauses: true
    identifyRisks: true
    flagUnusualTerms: true
    identifyMissingClauses: true
  }) {
    executiveSummary
    risks
    unusualClauses {
      title
      type
      riskLevel
    }
    riskScore
  }
}

# Run due diligence on a target
mutation RunDueDiligence($input: DueDiligenceInput!) {
  runDueDiligence(input: $input) {
    id
    status
    report {
      executiveSummary
      findings {
        category
        title
        severity
        recommendation
      }
      riskScore
    }
  }
}
```

## Authentication

Harvey uses enterprise SSO for authentication. API access is provisioned through customer agreements. The `Token` type represents session credentials and `APIKey` represents programmatic access tokens issued within an organization.

## Notes

- This schema is conceptual and based on Harvey's publicly documented product surface.
- Actual API endpoints, field names, and authentication mechanisms may differ from production Harvey integrations.
- Harvey's Ecosystem integrations (iManage, NetDocuments, Microsoft 365, Westlaw, LexisNexis) are arranged through direct partnership engagements, not public APIs.
- Enterprise customers should consult Harvey's integration documentation via their account relationship.

## References

- Harvey Products: https://www.harvey.ai/products
- Harvey Documentation: https://docs.harvey.ai/
- Contact Sales: https://www.harvey.ai/contact-sales
