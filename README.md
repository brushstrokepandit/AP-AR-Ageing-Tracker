# AP/AR Ageing Tracker

**File:** `AP_AR_Ageing_Tracker.xlsx` | **Data:** synthetic, INR | **As-of date:** 30-Nov-2026 (editable)

## Objective
Track customer invoices and supplier bills, age the balances automatically and flag parties that need follow-up.

## Features
- 90 receivable invoices (12 customers) and 64 payable bills (10 suppliers).
- Due date = document date + terms; balance = amount - paid; days overdue = as-of date - due date.
- Ageing buckets: Current, 1-30, 31-60, 61-90, 90+ (limits editable in `Settings`).
- Summary by customer and supplier using `SUMIFS`, reconciled back to the registers.
- Escalation flag when the share over 60 days exceeds the threshold in Settings.
- Dashboard: total outstanding, overdue %, over-60-day exposure, DSO and DPO, parties flagged; bar charts of exposure by bucket.

## Key formulas
```
Days overdue : =IF(H2<=0,0,MAX(0,Settings!$B$4-E2))
Bucket       : =IF(H2<=0,"Paid",IF(I2=0,"Current",IF(I2<=Settings!$B$5,"1-30",...)))
Ageing cell  : =SUMIFS(AR_Register!$H:$H,AR_Register!$B:$B,$A5,AR_Register!$J:$J,B$4)
DSO          : =Receivables / credit sales in look-back x look-back days
```

## Result (illustrative)
Receivables of INR 7.49m with 28% over 60 days; five customers flagged for escalation.
