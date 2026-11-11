---
name: pa-ux-skill
description: A senior UX designer's hands-on playbook for how a product should actually behave — information architecture, user flows, interaction patterns, forms, navigation, onboarding, error/empty/loading states, and microcopy, written the way an experienced UX practitioner actually reasons through a flow. Use this whenever designing or reviewing how a product behaves for the person using it: flows, navigation, onboarding, search, forms, dashboards, notifications, confirmations, error handling, or when someone asks "how should this work," "is this confusing," "what's the best flow for X," or wants a feature to feel "intuitive," "simple," or "easy to use," even if they never say "UX" out loud. Pair with pa-ui-skill when the ask also touches visual styling, layout, or color.
---

# PA UX Skill

*A working designer's notes on how a product should actually behave, not just look.*

Here's the thing about UX that took me a long time to really internalize: almost nobody fails at this because they didn't know the heuristics. They fail because they designed from the feature outward instead of from the person's goal inward. You can know every rule in this document and still ship something confusing if you started from "what should this screen contain" instead of "what is this person actually trying to get done, and what's the shortest honest path to it."

So before anything else below, I want you to build the habit of asking that question first, every time, out loud if you have to.

## 1. Start from the goal, not the feature

A "settings page" is not a goal. "I want to stop getting these emails" is a goal. "A billing page" is not a goal. "I want to know if I'm about to get charged more than last month" is a goal. The feature name is what engineering calls it; the goal is what the person actually walked in wanting.

Before you design a flow, be able to say: who's doing this, what do they actually want out of it (not the feature name, the underlying want), and what did they just come from — what do they already know, have, or feel walking into this moment? That last part matters more than people think. Someone arriving at a form from an error email is in a completely different headspace than someone browsing idly, and the flow should know that even if the screen looks identical.

Find the path that 80% or more of people will actually take, and make that path as short and obvious as it can be. Edge cases — empty states, errors, permission issues, the zero-data moment — don't need to be equally beautiful, but they cannot be ignored, and I'll come back to why in a minute.

One more thing I say a lot, because it's uncomfortable and people avoid it: if a flow mostly exists to serve the business (an upsell, a data grab, a forced opt-in) rather than the person's own goal, just be honest with yourself about that while you design it. Dress it up however you need to for the stakeholders, but don't lie to yourself about whose goal you're actually optimizing — people feel the mismatch even when they can't name it, and it reads to them as the product working against them, not for them.

## 2. Information architecture — organize like a user thinks, not like the database

Group things the way a person mentally files them, not the way your org chart or your schema happens to split them up. "Billing" and "Usage" might sit in completely different engineering domains and still be, in a user's head, basically the same bucket: "stuff about what I'm paying for." Design for their bucket.

Keep navigation shallow. Two levels is comfortable. Three is about the practical ceiling before people start getting lost and backtracking. If you find yourself needing a fourth level, I'd bet the grouping one or two levels up is actually wrong, not just "deep" — depth is usually a symptom, not the real problem.

Name things the way a user would describe the task to a friend, not the way your team talks about it in standup. Internal codenames, feature names, and jargon are invisible to the people who built them and baffling to everyone else.

And give every important destination more than one honest way to get there — navigation, search, a contextual link from where the need actually arises. If the only path to something important is a single easy-to-miss menu item, you haven't really shipped it, you've hidden it.

## 3. Flows and interaction patterns

Minimize steps, but don't confuse that with minimizing screens. I've seen plenty of single-screen forms that felt more overwhelming than a well-paced three-step wizard, because the real variable is perceived effort and clarity, not literal click count. A longer flow that never makes someone think "wait, what do I do now" beats a short one that does.

Default to the answer most people would give, and let them change it later instead of asking everyone up front "just in case." Every question you ask that you could've reasonably guessed is a small tax on everyone, paid so that a small minority doesn't have to correct a default.

I'll say something a little contrarian here: stop reaching for a confirmation dialog as your first instinct for every destructive-ish action. If something's genuinely recoverable — archiving, deleting a draft — give people undo instead of a "are you sure?" modal. The moment you put a confirmation on everything, people learn to click through it on autopilot, which means it stops protecting anyone right when you actually need it to, for the one truly irreversible action. Save the hard stop for things that actually can't be undone.

Use progressive disclosure on purpose: show the common path by default, and tuck the advanced stuff behind an explicit "more options" rather than greeting everyone with every possible setting. That's an information architecture decision as much as a visual one — decide what counts as "advanced" before you worry about how it's styled.

And please, preserve what someone already typed. A failed submit, a back button, a crash — none of those should ever cost someone the three paragraphs they just wrote. This is one of those things that seems like an edge case right up until it happens to a real person, and then it's the only thing they remember about your product that day.

## 4. Forms — where every UX principle gets tested for real

Forms are unforgiving. Every field you add, every ambiguous label, has a measurable cost in people quietly giving up and leaving. There's no abstraction left to hide behind here; it's just you and the field.

Only ask for what you genuinely need right now, for this step. Anything you don't need yet, ask for later, when there's an actual reason — not "because we might want it eventually." Order fields the way a person would naturally think of them, and group the ones that belong together (all of an address, together, not split across the form).

Validate as someone finishes a field, not only after they hit submit. Catching one mistake immediately costs almost nothing; discovering five mistakes after someone thought they were done costs their patience. And when something's wrong, say what's wrong and how to fix it — "Password needs at least 8 characters," not "Invalid password" — and put that message right next to the field it's about, not buried in a summary banner at the top that nobody scrolls back up to read carefully.

Never make someone type the same thing twice just because it's "safer." If a confirmation field is genuinely warranted — email, password — at least give them a way to reveal what they typed instead of typing blind twice. Most of the time, though, double-entry is a habit from an older, more cautious era of form design, not an actual necessity.

## 5. The four states that exist for every real view

Empty, loading, error, success. Every nontrivial view has all four, and each one is a moment where you either reassure someone or lose them.

**Empty** should never just be blank. Tell someone why there's nothing here, and give them the actual next step — "No projects yet — create your first one," with the real button right there, not a wall of text and no way forward.

**Loading**, if it's going to take more than about a second, deserves actual information — a skeleton of what's coming, a progress indicator — not a bare spinner that gives someone nothing to anchor their patience to.

**Error** needs to say, in plain human language, what happened — not a stack trace or an error code as the headline — and then say what the person can actually do about it. And always leave a way forward: retry, go back, talk to someone. A dead end in an error state is one of the fastest ways to make someone distrust the whole product.

**Success** needs to actually confirm something happened, especially when there's no obvious visual change — a background save, for instance. Silence after an action reads as "did that even work?", and the next thing someone does is click it again, which is its own small disaster waiting to happen.

## 6. Navigation and findability

Make search forgiving — typos, partial matches, reasonable synonyms where you can manage it. A search box that only works for the exact term someone has to guess correctly is barely better than no search box at all; it just adds false hope.

Back — the browser's or the app's own — should take someone back to where they actually expect to be, filters and scroll position intact, not reset to some default state that throws away the five minutes they spent getting somewhere specific.

Breadcrumbs, step indicators, or some clear "you are here" signal matter most exactly where navigation runs deep. If you kept things shallow in section 2, you'll need less of this scaffolding — which is itself a decent signal your architecture is actually working, not just a nice bonus.

## 7. The quick sanity checks (adapted from Nielsen, because they hold up)

I run almost every flow I review through this short list, roughly in this order:

- **Status**: does the person always know what's happening — loading, saved, mid-process?
- **Real-world match**: does the language match how they'd actually describe this, not how the team describes it internally?
- **Control**: can they undo, cancel, or back out of whatever they started?
- **Consistency**: does the same icon, term, or action mean the same thing everywhere, or does it quietly shift meaning screen to screen?
- **Prevention over cure**: could this mistake have been designed away entirely — a disabled action, a confirmed risky one — rather than just caught and apologized for afterward?
- **Recognition over recall**: are the options visible or suggested, or does someone have to remember something from three screens ago?
- **Room for both kinds of user**: does a first-timer get enough guidance, and does a power user get to skip it without being punished for knowing what they're doing?
- **Restraint**: is there anything on this screen competing for attention that has nothing to do with the task at hand?
- **Graceful recovery**: covered above, but worth repeating — every error needs a way out.
- **Help where it's needed**: is guidance available in the moment someone's confused, or does it require leaving the task to go find a help page?

## 8. Interaction accessibility

Every flow needs to be fully completable by keyboard alone, in a tab order that actually matches the order someone would read or look at things — not the order they happen to sit in the source.

Nothing that's genuinely time-limited — a session timeout, an offer that "expires in 2 minutes" — should be the *only* path through, with no way to extend or recover without losing progress. People get interrupted mid-task constantly; design for that reality instead of punishing it.

Don't lean on hover as the only way to reveal something essential. Touch devices don't have hover, and keyboard users don't either. If it matters, it needs a non-hover way to reach it.

And when you're writing for something that'll be read by a screen reader, think in sequence, not in layout. What gets announced, in what order, and does that order still make sense read start to finish, out loud, with no visual layout to lean on? If you're not sure, read your own flow that way and see if it holds up.

## 9. Microcopy — small words, real weight

Write buttons as verb plus object — "Delete project," not "OK" or "Submit" — so the consequence is obvious without needing to read anything else on the screen first.

Write in the words a person would actually use, not the system's internal state. "Your changes are saved," not "Operation completed successfully, code 200." Nobody talks like the second sentence, and nobody should have to translate it in their head to know they're fine.

Keep the tone steady. Don't let an error message suddenly get cute or jokey about something that just cost someone their work — that's a tonal whiplash people notice and remember, and not kindly.

## Before I call a flow done

This is roughly the walk-through I run before handing a flow off:

- [ ] Can I say the person's actual goal here in one sentence — not the feature name?
- [ ] Is the primary path the shortest honest path to that goal?
- [ ] Are empty, loading, error, and success all actually designed, not just the happy path?
- [ ] Is every destructive action either reversible or clearly, deliberately confirmed — never neither, and rarely both?
- [ ] Are field-level errors specific, actionable, and placed right next to the field?
- [ ] Can I get through the entire flow with a keyboard alone?
- [ ] Am I asking for anything the system already knows, or anything this step doesn't actually need yet?

And the habit I trust more than any heuristic above: when you're reviewing a flow, don't judge it from the diagram. Walk it yourself, step by step, as if you were a first-time user with the actual goal in mind, before you check it against anything on this list. Almost every real UX problem is invisible from the inside — to whoever built it — and only shows up the moment you try to get through it cold, the way a real person would.
