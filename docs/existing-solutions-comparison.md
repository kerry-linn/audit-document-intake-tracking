# Existing Solutions Comparison Memo

**Project:** Audit Document Intake and Tracking (CI 491)

**Deliverable:** Task C5

**Date / Due date:** October 14, 2026

## Purpose and finding

This memo compares the core platforms identified in the preliminary research and explains where the proposed system could add value. The project addresses evidence that arrives through different channels with unclear file names, making it difficult to determine which Open Items List (OIL) request it satisfies and what remains outstanding.

Existing platforms already support evidence collection, request tracking, and automated document matching. The strongest opportunity is a focused intake workflow: identify an incoming document, suggest an OIL match and storage location, and let an auditor confirm or correct the suggestions before tracking changes occur. This is a proposed direction; the project is still validating requirements and has not selected an implementation stack.

## Core platform comparison

PBC means “provided by client”: documents and information requested by auditors. The gaps below describe fit with this project's workflow, rather than verified absence of a feature from a vendor's entire product.

| Platform | Relevant features | Gap or limitation for our use case | How the proposed system differs |
| --- | --- | --- | --- |
| **Suralink Request List Management** [1] | PBC request lists, client document collection, responsibility assignments, outstanding-item tracking, review, and audit trails. Preliminary research also identifies AI-assisted checks of submission suitability. | Its primary workflow organizes evidence around requests. The research does not establish how it handles unorganized incoming files whose request relationship and internal destination are unknown. | Start with the received file and suggest client, fund, year, document category, OIL item, and storage destination. Suralink is the closest overall competitor and should be the main benchmark. |
| **Caseware Client Requests** [2] | Request creation and assignment, evidence uploads, status tracking, and acceptance or return of submissions. Preliminary research identifies Verity AI checks for completeness and readability, with auditor review. | In the request-led workflow described in the research, the client typically uploads evidence against an existing request. That differs from inferring the request association after receipt. | Match evidence to an imported OIL when the association is initially unknown, then require auditor confirmation before updating the tracker. |
| **DataSnipper Document Matching** [3] | Extracts information from supporting documents and matches evidence, such as invoices, bank statements, and contracts, to audit samples in Excel. | Its matching workflow supports audit testing; it does not by itself establish an end-to-end process for intake, OIL status updates, and internal filing. | Apply document matching earlier, connecting incoming evidence to outstanding requests rather than to audit-testing samples. DataSnipper is the strongest technical comparison for matching. |
| **Workiva Audit Management** [4] | Broader audit management with evidence requests, document collection, workflow statuses, approvals, collaboration, and audit history. | The platform covers a wider set of audit and reporting activities. The research does not establish whether its intake workflow meets the project's specific OIL and folder-routing needs. | Keep the scope centered on document identification, suggested request matches, and confirmed tracking updates, rather than a complete audit-management suite. |

## Proposed workflow and differentiation

The proposed system would support this sequence:

1. **Import an OIL and upload evidence.** Use the existing request list as the matching reference, including files that arrive without a known request association.
2. **Identify the document.** Suggest client, fund, reporting year, and document type from available content and metadata; flag missing or conflicting information.
3. **Suggest a match and destination.** Present a candidate OIL item and internal storage location with enough supporting information for the auditor to assess the suggestion. Ambiguous files should remain available for manual review.
4. **Confirm and update.** Let the auditor accept or correct the suggestions before recording the evidence association and updating the tracker. Receipt of a document should not automatically mean that a request is complete.

For example, an auditor receiving a generically named bank-statement PDF could review the extracted fund and reporting period, confirm the suggested OIL request, and approve its destination. A statement for the wrong period would remain unresolved instead of automatically closing the request.

The distinction is the combined intake workflow, not a claim that classification or matching is new. Request-management platforms and DataSnipper already overlap with parts of the idea. The project must validate whether a focused tool improves handling of unorganized evidence enough to justify building it.

## Supporting document-processing options

These services are potential building blocks, rather than complete alternatives to the proposed application.

| Technology | Relevant capabilities | Role and remaining gap |
| --- | --- | --- |
| **Azure Document Intelligence** [5] | OCR, layout and table extraction, prebuilt financial-document models, and custom classification/extraction. | Candidate for document identification and field extraction. OIL matching, folder rules, auditor review, and tracking still require application logic. |
| **Google Document AI** [6] | OCR, prebuilt processors, and custom document classification and extraction. | Another candidate for producing structured metadata. Project-specific request matching and confirmation remain separate responsibilities. |
| **Amazon Textract** [7] | Extraction of text, tables, forms, key-value pairs, signatures, and query answers. | Useful for extracting information from scanned evidence; document-category classification would require additional rules, models, or services. It does not supply the OIL workflow. |

Azure and Google are the initial shortlist because the project needs both classification and extraction. Selection should follow a small comparison using representative, appropriately approved documents: measure document-type accuracy, client/fund/year extraction, match quality, and manual correction effort, while comparing cost, supported formats, and data-handling requirements. No provider is selected by this memo.

## Recommendation

Use Suralink and Caseware as the main request-workflow benchmarks, DataSnipper as the matching benchmark, and Workiva as the broader enterprise comparison. Scope the first version around OIL import, evidence upload, suggested document types and matches, and auditor-confirmed tracking updates. Validate client/fund/year extraction and folder routing with the stakeholder before treating them as committed requirements.

Before implementation, confirm how the closest platforms handle unassigned evidence and whether the intended OIL and storage workflow can be configured in an existing product. The proposed system's value depends on reducing manual intake work while preserving the auditor's decision about evidence sufficiency.

## References

Based on the supplied preliminary research and its vendor references. This is a qualitative comparison, not a hands-on product evaluation; current feature availability and integration support require validation.

1. [Suralink — Request List Management](https://www.suralink.com/technology/request-list-management)
2. [Caseware — Client Requests](https://www.caseware.com/products/client-requests)
3. [DataSnipper — Document Matching](https://www.datasnipper.com/resources/feature-spotlight-document-matching)
4. [Workiva — Audit Management](https://support.workiva.com/hc/en-us/articles/360059565172-Workiva-for-Audit-Management)
5. [Microsoft — Azure Document Intelligence overview](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/overview)
6. [Google — Document AI overview](https://docs.cloud.google.com/document-ai/docs/overview)
7. [AWS — Amazon Textract](https://aws.amazon.com/textract/)
