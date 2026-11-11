---
name: pa-ui-skill
description: A senior product designer's hands-on playbook for visual interface design — hierarchy, spacing, typography, color, component states, responsiveness, motion, and visual accessibility, written the way an experienced UI designer actually talks through a screen. Use this whenever building, styling, implementing, or reviewing any UI — web pages, components, dashboards, forms, mobile screens, design systems — and whenever someone asks for something to "look better," "look more polished," "look modern/professional," or needs help with colors, fonts, spacing, layout, dark mode, or responsive design, even if they never say "UI" out loud. Pair with pa-ux-skill when the ask also touches flows, navigation, or behavior rather than appearance.
---

# PA UI Skill

*A working designer's notes on making interfaces look like someone cared.*

Nobody opens an app and thinks "nice 8-point spacing system." They just feel like it works, or they feel like something's quietly off and can't say what. That feeling — not the Figma file, not the component library — is the actual job. Everything below is what I've learned moves that feeling, the slow way: by shipping real screens, watching real people squint at them, and fixing what was actually wrong instead of what looked wrong in the mockup.

I'm going to talk you through a screen the way I'd talk a junior designer through one, not hand you a style guide to memorize.

## 1. Before you touch a single color — what's this screen actually saying?

Every screen has a job. Before you lay out a single pixel, you should be able to finish this sentence: "The one thing I want someone to do here is ___." If you can't finish it, you're not ready to design yet, you're ready to think some more.

That one thing gets the visual weight — size, color, position, whatever earns it attention without shouting. Everything else recedes. The mistake I see constantly, from beginners and tired seniors alike, is treating every element as equally important because it's all "needed." Needed and *important right now* are different questions.

A trick that's served me well for twenty years of interfaces: group things with space, not boxes. A border around a card is admitting you didn't trust the spacing to do its job. Tighten the gap between things that belong together, widen it between things that don't, and the eye groups them without you ever drawing a line. If you find yourself reaching for a divider or a box, ask whether more whitespace would have done the same work more quietly.

And make sure the order things appear in code matches the order a person's eye actually travels. I've debugged more than one "weird tab order" bug that turned out to be a CSS grid reorder nobody thought to double check against the DOM order.

## 2. Spacing — the thing everyone notices and nobody credits

If a screen feels "off" but you can't name why, nine times out of ten it's spacing, not color. People are shockingly sensitive to inconsistent spacing even when they can't articulate it — they'll just say the design feels "cheap" or "amateur."

Pick a base unit — 4px or 8px, it genuinely doesn't matter which, what matters is picking one — and build every margin, padding, and gap as a multiple of it: 4, 8, 12, 16, 24, 32, 48, 64. The moment you type `13px` or `22px` because "it looked right," you've started a drift that someone will spend an afternoon untangling later. Constrain yourself on purpose; it's faster, not slower, once it's habit.

Whitespace isn't the leftover space you didn't fill — it's the tool that tells people what belongs together. The *ratio* between "space inside a group" and "space between groups" is doing almost all the communicating. When something feels cramped, the fix is usually more space around it, not a smaller font.

One more thing nobody teaches you in school: sometimes the math is right and it still looks wrong. An icon that's mathematically centered in a circle often looks slightly low to the eye. Nudge it a pixel or two until it looks centered, not until the numbers say it is. Trust your eye over the ruler on anything optical.

## 3. Typography — the most load-bearing decision, and the one people rush

If I had to guess where a "fine" design and a genuinely good one diverge, it's usually type, because it's the thing people rush to pick the color palette instead.

Stick to one typeface family for almost everything. Lean on weight and size for contrast, not a second font competing for attention — a second font is a decision that needs a real reason, not a default. Build a small type scale up front (something like 12 / 14 / 16 / 20 / 24 / 32 / 48) and reuse those sizes everywhere instead of eyeballing a new size per screen. Fewer sizes, used deliberately, reads as considered. A dozen almost-but-not-quite-the-same sizes reads as nobody was paying attention.

Body text wants to breathe a bit: 15-18px, with line-height around 1.4-1.6. Headlines want the opposite — tighten the line-height as the size goes up (1.1-1.3), or big type starts to look like it's falling apart into separate lines instead of one statement. And keep lines of body text to roughly 65-75 characters — about 600-750px wide. Full-width paragraphs at desktop sizes are exhausting to read no matter how nice the font is; your eye has to work to find the start of the next line.

Small thing that trips people up constantly: don't make bold the *only* signal that something's a link or a button inside body copy. Weight alone is too easy to miss on a skim. Pair it with color, an underline, something a glance can catch.

## 4. Color — restraint is the actual skill

Anyone can pick a pretty color. The skill is knowing when not to use it.

Build structure into your palette instead of collecting hex codes: a neutral scale (usually 8-10 steps of gray, from near-white to near-black), one primary/brand color, and a fixed set of semantic colors for success/warning/error/info that never change meaning no matter what the brand color is doing that season. Then — and this is the part people resist — keep most of the interface neutral, and spend color like it's expensive. A screen where everything is colorful has nothing left to point at with color. The restraint is what makes the one colorful thing actually mean something.

Don't eyeball contrast — check it. Body text wants at least 4.5:1 against its background; large or bold text can get away with 3:1 (that's the WCAG AA bar). This isn't a compliance checkbox I'm asking you to tick — low contrast is, in my experience, the single most common thing real users complain about without knowing to call it "contrast." They just say it's "hard to read" or "hurts my eyes," and they're right.

If dark mode is in scope, resist the urge to just invert the light palette and call it done. Pure black backgrounds with pure white text at full brightness causes a glare effect (halation) that's genuinely uncomfortable to stare at for long. Use dark grays instead of true black, pull text brightness down slightly, and — this is the step everyone skips — re-check contrast on every semantic color again in dark mode specifically, because a red that reads fine on white can disappear or vibrate uncomfortably on near-black.

And never let color alone carry meaning for something important — a required field, an error, a category. Pair it with an icon, a label, a pattern. Roughly 1 in 12 men have some form of color vision deficiency; if color is your only signal, you've quietly locked a meaningful slice of your users out of information everyone else gets for free.

## 5. States — the interface is not the one screenshot you took

A component isn't finished because the default state looks nice in a screenshot. It's finished when every state it can be in has actually been designed on purpose: default, hover, focus, active/pressed, disabled, loading, error, empty. Missing one of these is the single biggest gap I see between "looks great in the deck" and "feels broken in the hands of a real user."

My personal pet peeve, because I see it everywhere: a disabled button that's just the normal button at 40% opacity. That's not disabled, that's "normal button, but sad." Disabled should read as genuinely non-interactive — no hover response, ideally a cursor change — so nobody wastes a click wondering why nothing happened.

For loading, match the wait to the treatment. If the content has a predictable shape — a list, a feed, a card grid — use a skeleton screen that mirrors that shape; it sets expectations and feels faster even when it isn't. Save spinners for short, shapeless waits, like a button mid-submit. And whatever you do, don't let content popping in cause a layout jump — reserve the space it'll need before it arrives, or you'll train people to distrust the page every time something shifts under their cursor.

Last thing: if the same component needs to look meaningfully different in one specific place, that's usually a sign it's secretly a different component or variant, not a one-off override you bolt on. Consistency isn't a nice-to-have, it's what lets people stop re-learning your interface every time they move through it.

## 6. Responsive — it's not reflow, it's re-asking the question

Designing mobile-first, when mobile is in scope at all, forces you to decide what actually matters first. Designing desktop-first and then "making it responsive" later usually just means cramming the same priorities into a smaller box, which is a different and worse problem.

Touch targets need real room: at least 44×44px on iOS, 48×48px on Android, and — just as important — real spacing *between* adjacent tappable things, not just a big enough target in isolation. I've watched people mis-tap adjacent buttons in usability sessions more times than I can count, and it's almost always a spacing problem, not a size problem.

Don't just let things reflow at a breakpoint — reconsider what's actually needed at that size. A sidebar might become a bottom sheet. A dense data table might become stacked cards. Sometimes the right move at a smaller size isn't "the same thing, smaller," it's "a different shape that serves the same goal." And actually test at the awkward boundary widths — 768px, 1024px, wherever your breakpoints sit — because that's exactly where layouts quietly break and nobody notices until someone's on an iPad in portrait mode.

## 7. Motion — punctuation, not music

Good motion answers a question the user already has: where did that come from, what's related to what, what just changed. If you can't name the question an animation is answering, it's decoration, and decoration is the first thing to cut when you're not sure.

Keep most UI motion short — roughly 150-250ms for small things like buttons and toggles, maybe 250-400ms for bigger things like panels and page transitions. Go much longer than that and it stops feeling elegant and starts feeling like the interface is waiting for you to notice it. Ease things in the way they'd actually move: decelerate into rest for things arriving or responding to the user (ease-out), accelerate away for things leaving (ease-in). Linear, constant-speed motion is one of the fastest tells that something was built, not designed — it reads as mechanical in a way most people can feel even if they can't explain it.

And always respect `prefers-reduced-motion`. Give people an instant or near-instant alternative, not just a faster version of the same animation — for some people, motion isn't an aesthetic preference, it's a physical discomfort.

## 8. Accessibility you can actually see

A few things that live specifically in the visual layer, not the code layer:

Every interactive element needs a focus state that's visible and distinct from hover, and that survives someone navigating by keyboard alone. If you're removing the default outline, you'd better be replacing it with something — removing it and replacing it with nothing is one of the more common ways a UI quietly becomes unusable for a whole category of people.

Keep body and label text at roughly 13-14px minimum outside of genuinely secondary, disposable labels, and never disable pinch-zoom on a mobile web page — someone's eyesight is not your design opinion to override.

Icon-only buttons need a text alternative somewhere — an `aria-label`, a tooltip, something — because an icon's meaning is obvious to the person who chose it and a guess to everyone else.

And give form fields a real, persistent label, not just a placeholder. Placeholders vanish the moment someone starts typing, and by convention they're lower-contrast than a real label — exactly the two things you don't want from something whose whole job is to tell someone what to type.

## Before I call anything done

This is the walk-through I actually do before I show a screen to anyone else:

- [ ] Can I say, in one sentence, what the single most important thing on this screen is?
- [ ] Does everything sit on a consistent spacing scale and align to something real, not "close enough"?
- [ ] Have I actually designed every state — hover, focus, active, disabled, loading, error, empty — not just the default?
- [ ] Did I check contrast with a real tool, not my eyes, including dark mode if it exists?
- [ ] Do touch targets and the spacing between them actually work at mobile width?
- [ ] If there's motion, does it answer a real question, and is there a reduced-motion fallback?
- [ ] Can I get through this entire screen using only a keyboard and still see where I am?

And one habit that's saved me more times than any rule above: when you're building this in code, actually look at it. Spin up the dev server, open the browser, look at the rendered thing — don't reason about how it'll look from the markup alone. Markup lies. Pixels don't.
