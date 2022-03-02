---
id: 8iw57w5j23kbx3zjne0fr0c
title: Example of lightweight feature documentation
desc: ""
updated: 1646270820159
created: 1646268733548
---

https://alisterbscott.com/2020/05/29/example-of-lightweight-feature-documentation/

I’m not keen on writing specifications in gherkin (Given/When/Then) as I think it’s too generic and frequently makes the feature specifications too verbose – and takes emphasis away from the critical parts.

The important thing to note is **the actual documentation artifact generated isn’t as important as the collaborative process that is involved in generating it.** This is often about asking the right questions and adding more examples until there’s nothing that is unclear.

The document isn’t a template – the actual documentation varies based on conversation, problem and context.

---

# Example: Royalty Payment Splits

## Background

- Royalties need to be paid in full on disbursement to artists.
- A royalty payment can be made to an individual artist, or a group of artists.
- When making payments to an individual artist they get 100% of royalties (no rounding)
  When making payments to a group of artists this needs to be split by the percentage splits defined in the system which always add to 100%
- When splitting a payment across a group of artists and it doesn’t split evenly into cents, the system currently randomly splits the cents between artists to balance out the rounding over time
- This causes issues for both automated tests which need deterministic behaviour, and artists who are confused why they get slightly different amounts if their royalties are the same.

## Scenarios / Examples

| Scenario                                                                               | Royalties Owed | Current Royalties Paid                                                  | New Royalties Paid                                 | Testing |
| -------------------------------------------------------------------------------------- | -------------- | ----------------------------------------------------------------------- | -------------------------------------------------- | ------- |
| Single artist gets 100% of whole payments                                              | $100.00        | $100.00                                                                 | $100.00                                            | ✅      |
| Single artist gets 100% of payments including cents                                    | $66.67         | $66.67                                                                  | $66.67                                             | ✅      |
| Two artists with 50% each for a payment that can be split evenly                       | $100.00        | artist 1: $50.00 artist 2: $50.00                                       | $50.00                                             | ✅      |
| Two artists with 50% each for a payment that can’t be split evenly                     | $100.01        | $50.01 / $50.00 is randomly assigned to artist1/artist2                 | artist 1 $50.01 artist 2 $50.00                    | ❌      |
| Two artists with 50% each for a payment that can be rounded to ten cents – no rounding | $100.30        | artist 1: $50.15 artist 2: $50.15                                       | artist 1: $50.15 artist 2: $50.15                  | ✅      |
| Three artists with third splits can’t be split                                         | $100.00        | amounts of $33.33, $33.33 and $33.34 randomly assigned to group members | artist 1: $33.34 artist 2: $33.33 artist 3: $33.33 | ❌      |
| Three artists with third splits can’t be split – more than a single cent difference    | $100.00        | amounts of $33.33, $33.34 and $33.34 randomly assigned to group members | artist 1: $33.34 artist 2: $33.34 artist 3: $33.33 | ❌      |

## Business Rules

1. Royalties need to be paid in full on disbursement to artists.
2. A single artist gets a whole payment.
3. When payments can be split evenly to a group of artists (to the cent) they are split that way.
4. When payments can’t be split evenly to a group of artists, the payments are split into an even split and the remaining cents are distributed to the members in whole cents.
5. The first member in the group – based on earliest date/time added to group – gets the higher amount, followed by the second, third etc. based on earliest date/time added.
6. Payments aren’t rounded to ten cents or five cent amounts, only whole cents

## Questions/Decisions

| Question                                               | Decision                                                     | Made By                      |
| ------------------------------------------------------ | ------------------------------------------------------------ | ---------------------------- |
| Do we want to round to five or ten cent distributions? | No, we’ll always round to the cent                           | Product Owner via Slack #    |
| How do we distribute based on membership of group?     | We’ll use the date time added to the group (first gets most) | Team during kick off meeting |

---

# Summary

I think trying to force the above information into gherkin (Given/When/Then) statements would make it less readable and provides no added benefit – whilst Given/When/Then encourages consistency sometimes you just need structured thought that is most relevant to your context. The above document isn’t a template – it varies for the problems we’re trying to solve.
