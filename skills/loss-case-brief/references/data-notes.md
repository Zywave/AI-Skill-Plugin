# Loss case brief: data notes

Confirmed against live cases and the data dictionary. Re-check the dictionary when something looks off.

## Case status values (caseStatus)
Unknown (Default; not a real status, do not brief), Award, Dismissed, Estimate, Event, Pending, Proposed Settlement, Settled, Tentative Settlement, Investigation, No Action Taken, Stayed, Abstract, Response Costs, Dismissed w/o Prejudice, Indeterminate, Provision (Total), Transferred to MDL, Remanded.
Transferred to MDL and Remanded: the outcome sits on the parent MDL record. Event, Abstract, Transferred to MDL and Remanded never carry an amount. Indeterminate: a result is expected but its details were not found. Response Costs: the qualifier decides Actual or Estimated. Dismissed cases can carry an amount (defense costs, plaintiff legal fees). Status is as of the record's last research update, and an original verdict can be replaced by an appellate outcome with no structured history.

## Amounts
- `financials/totalAmount` is the authoritative all-in amount, in US dollars. The other `financials/` fields are components of it. Do not add them or rebuild the total.
- Qualifier fields (Estimated or Actual) exist for response costs, restitution, and extortion. Other components have none.
- `settlementAmountDescription` can describe a criminal sentence, not a civil settlement (a plea and prison term sat in that field for a restitution order). Read it as context.
- `nonFinancial` marks cases partly or wholly non-financial, such as a prison sentence.
- A criminal restitution order (for example $9.38B against a fund founder, or about $615M for a home-health fraud) is a court order, not a loss to an insurer. Direction: when the main defendant pays restitution, the settlement amount is populated and includes it (recorded as Settled by design); when the main defendant receives it, the settlement amount is blank and the total equals the restitution. A settlement description can describe a prison term.
- A shared amount is divided equally between co-defendants. An amount excludes portions owed by individuals other than directors and officers found liable.
- Insured and uninsured exposure (`exposureInsured`, `exposureUninsured`) are what the record lists. Example: NotPetya at Merck lists $60M insured and $985M uninsured; the description also mentions insurance recoveries. Report the record's fields, not what carriers paid.

## People and parties
- Descriptions often name private individuals (criminal defendants, victims, plaintiffs). Do not repeat those names. Judges are named in `jurisdiction/judgeFullName`; leave them out of briefs.
- `parties/` gives counts, not names, except `mainPartyName`.

## Relationships
- `relationships` kinds: Incident (one event), Cause (a common source; the asbestos group has over 34,000 members, so never an event count), SCMD (co-defendants of one lawsuit), SCSC (one organization with individuals, typically directors and officers, as co-defendants), Organization (all cases around one company), MDL (members carry no amounts; the parent holds the outcome; groupings can be incomplete), Other. `memberCaseCount` is the group size.
- Do not add the amounts of cases in one group. A company's recorded total provision can contain the settlements that are also separate cases.

## Dates
Each date has a qualifier. "Estimated" means approximate, and a year-only or month-only date is entered as January 1 or the first of the month, so write it as the year or month. A case year is the accident year, or the filing year when there is no accident date.

## The record's company
`company` is the organization as it is today; `companyAtLoss` is its snapshot at the time. The record's company can differ from the company in the story (a French GDPR fine on Free Mobile sits under 'Iliad 78'). Use companyAtLoss to describe the organization at the time.

## Truncation
`description` is cut at 10,000 characters and marked `descriptionTruncated`; `descriptionLength` is the real length. Say so if the brief rests on a truncated description.

## Awards and outliers
A jury award can be enormous and uncollectible. Example: a 2021 Texas dram shop case recorded a $301.04B award, $300B of it punitive, after the defendants (a bar and its owner) did not attend trial. The status is Award; the record's parties are private individuals and a victim who was a minor. Write it as an award, say it is not a payment, and name no individuals. Check any amount that is many times larger than the typical case in its line before writing it up.
