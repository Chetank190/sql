# Chetan Kumar

# Assignment 1: Design a Logical Model

## Question 1
Create a logical model for a small bookstore. 📚

At the minimum it should have employee, order, sales, customer, and book entities (tables). Determine sensible column and table design based on what you know about these concepts. Keep it simple, but work out sensible relationships to keep tables reasonably sized. Include a date table. There are several tools online you can use, I'd recommend [_Draw.io_](https://www.drawio.com/) or [_LucidChart_](https://www.lucidchart.com/pages/).

## Question 2
We want to create employee shifts, splitting up the day into morning and evening. Add this to the ERD.

## Question 3
The store wants to keep customer addresses. Propose two architectures for the CUSTOMER_ADDRESS table, one that will retain changes, and another that will overwrite. Which is type 1, which is type 2?

_Hint, search type 1 vs type 2 slowly changing dimensions._

Bonus: Are there privacy implications to this, why or why not?
```
Type 1:

In Type 1, we replace the old address with the new one. We don't keep old addresses. We only have the newest address. This is simple because we don't track changes.

Example:


### Type 1: CUSTOMER_ADDRESS Table (Overwrites)

| customer_id | address_line1  | address_line2 | city          | state | postal_code   |
|-------------|----------------|---------------|---------------|-------|---------------|
| 1           | Bay Mills      | Apt 389       | Toronto       | ON    | M62 3Y6       |
| 2           | 456 Sherbook St|               | Peterborough  | OR    | K9J 4P1       |

- The table updates in place, so any changes to the address will overwrite the old data.




Type 2:

In Type 2, we keep all old addresses. We make a new row each time the address changes. This lets us see all changes over time. It's more complex and needs extra date information. We use a flag to show which address is newest.

Example:

### Type 2: CUSTOMER_ADDRESS Table (Retains History)

| customer_id | address_id | address_line1  | address_line2 | city          | state | postal_code   | start_date | end_date   | current_flag |
|-------------|------------|----------------|---------------|---------------|-------|---------------|------------|------------|--------------|
| 1           | 1          | Bay Mills      | Apt 389       | Tronto        | ON    |   M62 3Y6     | 2021-01-01 | 2024-07-01 | 0            |
| 1           | 2          | 456 Sherbook St|               | Peterborough  | ON    | K9J 4P1       | 2024-07-02 | NULL       | 1            |

- `start_date` marks when the address became active.
- `end_date` is null for the current address.
- `current_flag` is set to 1 for the active address, 0 for historical addresses.

Privacy:

Both types have privacy issues, but Type 2 has more.

Type 2 keeps all old addresses. This could be risky if someone gets this information. Companies need a good reason to keep old addresses. They must follow rules about keeping and deleting data. If data is stolen, Type 2 is worse because it has more old information. Companies might need to tell customers they're keeping old addresses. They should let customers ask to delete their data. Type 1 might be better for privacy when old addresses aren't needed. Type 2 could be riskier because it keeps more personal information from the past.


```

## Question 4
Review the AdventureWorks Schema [here](https://i.stack.imgur.com/LMu4W.gif)

Highlight at least two differences between it and your ERD. Would you change anything in yours?
```
Relationship cardinality:

Mine ERD shows cardinality using "1" and "M" notations on the relationship lines while the link's ERD uses crow's foot notation to indicate cardinality and optionality of relationships.
Mine ERD has replationship labels (e.g., "process", "sales", "shift") while the link's ERD doesn't explicitly name the relationships between entities.

I would like to use add composite keys in order table but have order_id also works fine. I would also like to represent much broader system, like an enterprise planning covering multiple business as shown in the link's ERD.

```

# Criteria

[Assignment Rubric](./assignment_rubric.md)

# Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `September 28, 2024`
* The branch name for your repo should be: `model-design`
* What to submit for this assignment:
    * This markdown (design_a_logical_model.md) should be populated.
    * Two Entity-Relationship Diagrams (preferably in a pdf, jpeg, png format).
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sql/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `model-design`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-4-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
