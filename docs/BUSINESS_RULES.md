# MRM – Business Rules

## 1. User & Access Rules

- Every user must have an authenticated account to access protected features.
- Access to projects and financial information depends on assigned permissions.
- Only authorized users can modify financial records, agreements, and settlements.

## 2. Project & Track Rules

- A project can contain multiple tracks.
- A track belongs to a project.
- Contributors can participate in multiple projects and tracks.
- Contributors must have defined roles for their respective assignments.
- A contributor does not require a registered MRM account; a manager can add a contributor by name and contact details.
- Each project can have its own financial rules and agreements.
- Individual tracks may override project-level defaults through approved agreements. **[Phase 2]**

## 3. Configurable Financial Rules

MRM must support different financial arrangements rather than enforcing fixed percentages or calculation methods.

- Each project can define its own royalty distribution percentages.
- Royalty percentages must total exactly 100% for each applicable agreement.
- Expense allocation percentages can differ from royalty percentages.
- Expense allocation methods can include:
  - Royalty-based allocation.
  - Equal allocation. **[Phase 2]**
  - Custom percentage allocation. **[Phase 2]**
  - Individual contributor allocation. **[Phase 2]**
- Individual expenses can override the project's default allocation. **[Phase 2]**
- Recoupment priorities and policies can be configured according to approved agreements.
- The system must use the applicable approved financial rules when calculating settlements.

**Rule precedence:**
1. Explicit approved expense-level terms.
2. Applicable approved track-level agreement.
3. Applicable approved project-level agreement or defaults.

More specific terms take precedence only when they are valid and consistent with the agreement.

**MVP: project-level agreement only.**

## 4. Royalty Split Rules

- Every applicable royalty agreement must define contributor percentages.
- The total allocation must equal exactly 100%.
- Percentages cannot be negative.
- Each contributor's share must be associated with the correct project or track.
- The MVP supports one active royalty agreement per project at a time, versioned by effective date.
- Project-level royalty percentages apply uniformly to all revenue under that project.
- Track-specific agreements are deferred to Phase 2.
- A draft agreement can be edited freely. Once activated, it becomes the project's current agreement.
- An agreement becomes locked when revenue dated within its effective period exists or a calculation uses it. Locking is per agreement, so a new version is not locked because an older version has revenue.
- A locked agreement cannot be edited by anyone, including an administrator. Corrections require a new agreement version.
- A new version applies from its effective date. Version effective dates cannot overlap, and a new version's effective date cannot precede revenue already included in a finalized calculation.
- Previous agreement versions must remain accessible.
- Historical calculations must retain the agreement version used at the time.

## 5. Revenue & Expense Rules

- Every financial transaction must have an amount, date, category, and description.
- Revenue and expenses must be distinguishable.
- Transactions must be associated with the relevant project or track.
- Expenses must specify whether they are recoupable.
- Each expense must record its original payer (one payer per expense in the MVP).
- Multiple contributors or organizations may contribute to the same upfront expense. **[Phase 2]**
- Expense allocation and original payment responsibility must be tracked separately.
- Non-recoupable expenses must not generate recoupment deductions.
- Financial records used in settlements must not be silently overwritten or deleted.

## 6. Expense Allocation Rules

- Shared expenses can be allocated according to royalty percentages. In the MVP, shared recoupable expenses are allocated proportionally according to project royalty percentages.
- Shared expenses can also be allocated equally or through custom percentages. **[Phase 2]**
- Individual expenses can be assigned entirely to a specific contributor. **[Phase 2]**
- Expense allocation percentages must total exactly 100%.
- Expense allocation does not have to match royalty distribution. **[Phase 2]**
- Each expense must preserve its allocation breakdown.
- Only recoupable expenses generate allocations; non-recoupable expenses are recorded for reporting only.
- An expense is allocated once, when it is first included in a finalized calculation, using the royalty shares of that calculation's agreement. Its allocation is never recalculated, even if a later agreement changes the split. If that calculation is voided, the allocations it created are voided with it.
- Approved allocation changes must maintain historical records. **[Phase 2]**

## 7. Advances & Recoupment Rules

- Advances and expenses must be maintained as distinguishable financial records. **[Phase 2]**
- Both may participate in recoupment when their applicable agreements permit it. **[Phase 2]**
- Only eligible outstanding balances can be recouped.
- Revenue must first be allocated according to applicable royalty agreements.
- Recoupment deductions are applied to the relevant contributors' earnings according to their agreed expense responsibilities.
- Recoupment cannot exceed the available earnings of the relevant contributor in a settlement, so partial recovery is allowed.
- Allocations are recovered oldest expense first (Expense.incurred_on, then expense id).
- A calculation includes recoupable expenses of the same project with incurred_on on or before the period end that have an outstanding allocated balance or have never been allocated.
- If a contributor's earnings are insufficient to recover their allocated recoupable expense, the unrecovered balance is carried forward to subsequent calculation periods.
- Recoupment priorities must be configurable according to the applicable agreement. **[Phase 2]**

**Default recoupment priority:** **[Phase 2]**
1. Shared project expenses.
2. Individual advances.
3. Other eligible recoupable expenses.

Specific approved agreements may define a different priority.

## 8. Reimbursement Rules

- Every recoupable expense must identify its original payer or payers.
- Recovered amounts must be credited to the appropriate original payer.
- Reimbursement credits are based on the amount actually recovered, never on the full expense amount.
- If multiple parties paid an expense, reimbursement must follow their recorded payment contributions or agreed reimbursement terms.
- Expense deductions and reimbursement credits must be calculated separately.
- Reimbursement must not be counted as new revenue.
- Partial recovery must update the outstanding expense balance.
- Total reimbursement cannot exceed the amount eligible for recovery.
- Reimbursement records must be traceable to their original expenses.
- MVP: one payer per expense.

## 9. Royalty Calculation Rules

- Royalty calculations must use the applicable approved agreement.
- Gross revenue must be allocated according to approved royalty percentages.
- Applicable recoupment deductions must be calculated according to expense allocation and priority rules.
- Reimbursement credits must be routed to the original payer.
- Net payable amounts must reflect royalty earnings, applicable deductions, and reimbursement credits.
- The total financial distribution must reconcile with the underlying revenue and expense records.
- Calculations must maintain consistent currency and decimal precision.
- Each calculation must preserve its source transactions, agreement versions, deductions, and reimbursement breakdown.
- A calculation uses exactly one agreement. Revenue is selected by its received date and the agreement's effective period, so a period that spans two agreements requires two calculations.
- Calculation periods must not overlap, and a new calculation must start after the latest finalized calculation's period.
- A calculation is a draft until finalized. A draft does not reserve revenue; finalizing checks revenue availability and reserves it in a single transaction.
- A finalized calculation is immutable. It can be voided only if it is the project's latest finalized calculation and none of its settlements is paid; its pending or approved settlements must be cancelled first. Voiding releases its revenue, and its recoupment records remain preserved but no longer count toward outstanding balances.
- A contributor with a zero royalty share still receives a calculation line when they are owed a reimbursement credit.

## 10. Settlement Rules

- Settlements can only be generated from finalized royalty calculations.
- Settlement records must identify the contributor, amount, and relevant project or track.
- Settlements require authorized approval before being marked as paid.
- Settlement statuses are pending, approved, paid, and cancelled. Cancellation is allowed from pending or approved.
- Partial payments must maintain the remaining payable balance. **[Phase 2]**
- Paid settlements must retain their historical records.
- Cancelled settlements must not be treated as completed payments.
- A cancelled settlement can be reissued from the same calculation without rerunning it. Only one non-cancelled settlement may exist per contributor per calculation.
- A settlement amount is a snapshot of the finalized net payable and cannot be edited. No settlement is generated when the net payable is zero.
- A paid settlement is immutable.
- Settlements must be traceable to their underlying calculations.

## 11. Audit & Data Integrity Rules

- Important financial and agreement changes must maintain historical records.
- Unauthorized users cannot modify protected financial information.
- Historical calculations must remain reproducible using their original inputs and agreement versions.
- Invalid transactions and incomplete agreements must be rejected before financial processing.
- Settlement calculations must be validated before approval.
- Financial records must maintain consistent relationships and balances.

## 12. Edge Cases to Handle

The system must account for the following scenarios:

| Area | Scenarios |
|---|---|
| Royalty splits | Invalid percentages, changed agreements, removed contributors |
| Expenses | Multiple payers, custom allocations, non-recoupable expenses |
| Recoupment | Insufficient earnings, outstanding balances, priority conflicts |
| Reimbursement | Multiple payers, partial recovery, reimbursement limits |
| Agreements | Version changes, historical calculations, effective dates |
| Settlements | Partial payments, cancellations, rounding differences |
| Revenue | Zero revenue, refunds, chargebacks, adjustments |

These scenarios must be addressed through appropriate validation, calculation safeguards, and automated tests.

## 13. Expected Financial Calculation Flow

1. Gross revenue recording
2. Gross royalty allocation
3. Expense allocation
4. Expense recoupment from contributor earnings
5. Reimbursement credit to original payer
6. Net payable calculation
7. Settlement generation

The calculation engine must use the applicable project, track, and expense-level financial rules rather than hardcoded percentages or assumptions.

## 14. Decisions

**Decided:**

1. Rounding and decimal precision: see Section 15.
2. Currency: NPR only in the MVP.
3. Inheritance: the project-level agreement applies to all tracks.
4. Changing agreements after revenue has been recorded: the agreement is locked; corrections create a new version with an effective date.

**Still pending:**

The following details require further specification before implementation:

1. Treatment of negative revenue adjustments and chargebacks.
2. Handling contributors removed from active projects while balances remain outstanding.
3. Detailed treatment of refunds after a settlement has already been paid.

These decisions will be finalized during workflow specification and database design.

## 15. Monetary Precision and Rounding

1. All monetary values must use decimal arithmetic.
2. Django models must use DecimalField for monetary values.
3. Python calculations must use Decimal, never float.
4. NPR amounts will use two decimal places.
5. Percentage values will use two decimal places.
6. Use ROUND_HALF_UP for monetary rounding.
7. Intermediate calculations should retain Decimal precision.
8. Rounding differences must be reconciled deterministically so that allocated amounts equal the original amount.

Example Django field:

```python
amount = models.DecimalField(max_digits=14, decimal_places=2)
```
