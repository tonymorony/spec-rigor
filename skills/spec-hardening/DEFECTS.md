# Defect classes

The classes reviewers raise on spec pull requests, largest first. Each has its leading word, what it looks like, the self-check that catches it, and an example of the shape. The examples use an online store.

## Code claim

A statement about current behaviour, limits, callers, cited rule numbers or cited tickets that nobody checked at its source.

- Check: did you open the code for each claim about the existing system, and the ticket or spec for each ID you cite? In the ledger, cite the declaration, key or method (`orders.show.tracking_url`, `Order#total_must_be_positive`) or the ID's title, not a line number: line numbers go stale. Does a column, flag or mechanism the rule adds already exist under another name? Does a resolved open question in a sibling spec, or a decision on a ticket, already decide the point? Does a rule that records a decision keep its nouns and qualifiers?
- Shape: "Only one policy calls that predicate." / "The ticket decided to leave out an order with an unpriced item in its total; the rule leaves out any unpriced item, gift cards included." / "The rule treats 30 days as a full month; the field accepts 31." / "The rule adds a `removed` flag; `products.enabled` already does that."

## Missing state

A rule set gives no outcome for one combination of inputs, or for a gap in time.

- Check: list every input of each rule, including absent, zero, stale and not yet computed. Does every combination have a stated outcome? What does the user see between an event and the next refresh? When an import, a merge or a migration changes a value, not the user, what else moves (a last-updated date, a notice)?
- Shape: "With no address and no saved card at all, does the panel show two empty rows or disappear?" / "A catalogue merge moves an item to another category. Does the item's last-updated date move?"

## Collision

Two rules replace, hide or reorder the same element and can both be true at once, with no precedence.

- Check: for each pair of rules that act on the same element, can both apply? Which wins, and does the text say so?
- Shape: "Rule 2 says no field is mandatory; the field table marks three as required. Which does an engineer validate?"

## Two readings

A phrase reads two ways: a time window, a quantifier (none, each, all, once), "replaces", "after".

- Check: write the boundary case for each window and quantifier. Does the text give exactly one result on a named date?
- Shape: "'The last 12 months' — twelve months ending with this one, or this month plus the twelve before it?" / "'none carries any of the three' or 'none carries all three'?"

## Term drift

One word for two ideas, a synonym for a glossary term, a word used before it is defined, or a word that differs from the label users see elsewhere in the product.

- Check: is each domain noun in the glossary, defined before first use, used with one meaning, and the same as the visible labels in the rest of the product and the codebase?
- Shape: "'Tier' means a price level, then a shipping speed, in the same sentence." / "'Role' already means buyer, seller or admin." / "'Total' means the price paid in one panel and the price before tax in another."

## Formula

A computed figure lacks its formula, base, tie rule, method, rounding or cap; or a number appears with no reason.

- Check: does a worked example with real numbers reproduce each figure? For each threshold, cap, window or floor: why this value and not half or double? What can the data actually resolve at the smallest group size? What unit does each count count (rows or people)? Does each comparison use one basis on both sides: before or after tax, one currency, one date?
- Shape: "Which base does a percentage discount multiply?" / "The badge reads '50% below average': the item's price includes tax, but the average does not." / "With 12 reviews, one review moves the average by a tenth of a star or more, so two decimals are finer than the data resolves."

## Inference leak

A figure lets a curious or hostile user derive one person's data: at the smallest allowed group, by comparing views over time, by editing their own data repeatedly, or by combining fields that each look anonymous.

- Check: take the smallest group the rules allow and a user who knows one peer or controls their own entries. What can they compute? Does an "anonymised" row still name one person?
- Shape: "In a team of five, the team average and four known scores give the fifth." / "Department + start date + office still names one person."

## Design mismatch

The spec and the current design disagree: an element with no rule, a rule with no element, a label in different words.

- Check: walk every element of every frame. Does each map to a rule? Does each rule have an element? Do the labels match the spec's words? Record the spec as the decision; list design changes for the designer.
- Shape: "The design draws one column per price tier with a count above it; the spec says nothing of counts."

## Plain words

A sentence breaks the writing rules in `SKILL.md`: over 20 words, more than one idea, passive voice, an idiom or metaphor, a judgement word ("simple", "clean", "obviously"), or a synonym for a word used earlier.

- Check: does each sentence give one idea in 20 words or fewer, in the active voice? Does each idea keep one word throughout? Does each rule cell hold one constraint?
- Shape: "The note, which is optional and only shown when the order is open, is cleared if the status is later changed to closed, keeping data clean." (one sentence, four ideas, a judgement word)

## Ripple

An edit changed a rule, term or number, and another rule, edge case, open question or sibling spec still says the old thing.

- Check: after each edit, search the whole repository for each touched ID, term, alias and number. Include the specs, glossary, agent context, app copy and plans. Search the open pull requests too: when another one edits the same row, say which merges first and what the second must carry. Does the pull request body list the same IDs as the diff? Does every hit agree? Does a sentence the edit extended still agree with its own start? Then list every row that cites each changed rule, and every row the changed rule cites. Does each row still agree with the new meaning, also where it shares no word with the edit?
- Shape: "OQ-6 still says 'no order is left out', but BR-7 now leaves one out." / "EC-2 still says 'the next time the page loads'." / "The billing spec's OQ-3 still gives the old formula." / "The glossary drops 'Store owner' as an alias, but billing BR-1 still uses it." / "The follow-up pull request still says 'pointing those lines here is a follow-up'." / "Two open pull requests both rewrite BR-5."

## Convention override

A rule asks for a mechanism that the project's conventions do otherwise, and the spec does not say so. A builder who copies the closest sibling follows the convention and breaks the rule.

- Check: for each mechanism a rule asks for (deletion, caching, headers, storage, a refused save), what do the conventions file and the closest sibling's code do? Where they differ, does the rationale name the override, and does the build ticket draft carry the exception? Does the pull request edit a file the conventions freeze, such as a merged plan above its deviations?
- Shape: "The rule hard-deletes a record; the conventions soft-delete every record a user can see." / "The rule keeps a page out of the client page cache; the conventions cache every page of that kind."

## Source claim

An external provider, standard or fixed list is assumed to cover what the spec needs.

- Check: what does the source really cover, and which of its files holds each field? When does it update, what happens on its failure days, and what happens to stored values when the list changes? What does its licence require (credit, share-alike)?
- Shape: "That provider covers only some countries." / "The language standard has one code for Chinese." / "The feed publishes nothing on weekends." / "The base file holds no region names; a second file does."

## Overclaim

A rationale says "because", "always", "cannot" or "can fix it themselves", and one allowed case makes it false.

- Check: is each rationale true for every case the rules allow?
- Shape: "'The user can fix each of these', which is false for a user who has lost access to their email."

## Validation outcome

A refused input, or a choice the system drops or replaces, with no statement of what is saved, what is not saved, and where the user sees why.

- Check: for each refusal and each fallback, does the spec state the saved state and where the message shows?
- Shape: "Does the rest of the order save with that one field left empty?" / "The user picks EUR and the page shows USD, with nothing on the page saying why."

## Ownership

A rule owned by two specs (copies that drift), an operation in no story, a deferral with no owner, a first-build list that misses a part.

- Check: is each rule owned by exactly one spec? Does every operation (view, add, update, remove) appear in a story? Does every deferral name its owner or ticket? Does a rule that hands a case to a ticket also have an open Open Question row with **Blocks** and **Until then**? Is each promise made in a review reply also in the spec or a ticket? Is any open Open Question already answered by a rule?
- Shape: "The picker is written in two specs." / "BR-4 says 'TICKET-12 settles what they see', and no Open Question gives a state until then." / "A backlog cut story by story leaves removing a pick in no ticket." / "The glossary restates the conditions of BR-2 and misses a later change to them." / "Only a review reply says the import reports dropped rows."
