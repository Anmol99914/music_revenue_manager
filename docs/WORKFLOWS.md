# MRM – System Workflows

## 1. User Authentication

1. User registers or logs into the application.
2. System verifies credentials.
3. User is redirected according to their role and permissions.
4. Users can access only the information they are authorized to view or manage.

## 2. Project & Track Management

1. Project Manager creates a music project.
2. Project details are entered and saved.
3. Manager adds one or more tracks to the project.
4. Contributors are assigned to the project or individual tracks.
5. Contributors are assigned at the project level; track assignment is informational in the MVP.

## 3. Contributor & Agreement Management

1. Project Manager adds contributors.
2. Contributors are assigned roles (e.g., Producer, Composer, Lyricist, Vocalist).
3. Royalty percentages are assigned to eligible contributors.
4. System validates the total royalty allocation.
5. An agreement is created and associated with the relevant project or track.
6. A locked agreement is never edited; corrections create a new agreement version with a later effective date, and previous versions are preserved.

## 4. Revenue & Expense Management

1. Manager records incoming revenue.
2. Revenue is associated with a project or track.
3. Manager records project-related expenses.
4. Expenses are categorized and marked according to their recoupment eligibility.
5. System updates financial summaries.

## 5. Recoupment & Royalty Calculation

1. Manager starts a calculation for a project and period. The system selects the single agreement effective for that period and the revenue dated within it.
2. Allocate gross revenue among contributors using that agreement's royalty percentages.
3. Identify eligible recoupable expenses and, on first inclusion, create each contributor's allocation of them using the same royalty percentages.
4. Recover allocated expenses from each contributor's earnings, oldest expense first, up to the earnings available in the run.
5. Carry forward any unrecovered expense balance.
6. Credit the amounts actually recovered to the original expense payer.
7. Calculate the final net royalty payable and reimbursement credit for each contributor.
8. Review the draft, then finalize the calculation and generate settlement records.

Royalty allocation and expense recoupment are separate stages. Gross royalties must be calculated first; eligible expenses are then recovered from each contributor's earnings. Expense allocation determines who bears the expense, while the original payer determines who receives reimbursement.

**MVP limitation:** one payer per expense, and shared recoupable expenses are allocated according to project royalty percentages.

**Corrections:** A finalized calculation is never edited. If it was wrong, the latest finalized calculation for a project can be voided, provided none of its settlements has been paid and its pending or approved settlements are cancelled first. Voiding releases its revenue for a new calculation.

## 6. Settlement Generation

1. Manager reviews calculated contributor earnings.
2. System generates settlement records for contributors with a positive net payable. Each amount equals the finalized net payable and cannot be edited.
3. Manager verifies and approves the settlements.
4. Settlement status is updated as pending, approved, paid, or cancelled.
5. Contributors can view their settlement details and history.
6. If a settlement is cancelled, a replacement can be issued from the same calculation without rerunning it.

## 7. Reports & Documents

1. Manager selects a project, track, or reporting period.
2. System generates financial summaries and reports.
3. Agreement and settlement documents can be generated.
4. Relevant records remain available for future reference.

---

## Overall Workflow

**Project Creation → Track Management → Contributor Assignment → Royalty Agreements → Revenue & Expense Recording → Royalty Allocation → Recoupment → Reimbursement Routing → Settlement → Reporting**
