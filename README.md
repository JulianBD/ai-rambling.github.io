# Some Incomplete Thoughts on AI Assistance

## Table of Contents

1. [What This Is](#what-this-is)
2. [The Deeper Why: You Live Somewhere, AI Doesn't](#0-the-deeper-why-you-live-somewhere-ai-doesnt)
3. [The Thing That's Been Bugging Me](#i-the-thing-thats-been-bugging-me)
4. [The Core Principle: Only Delegate What You Can Do Competently But Inefficiently](#ii-the-core-principle-only-delegate-what-you-can-do-competently-but-inefficiently)
5. [The Abstraction Spectrum: Where Humans and AI Meet](#iii-the-abstraction-spectrum-where-humans-and-ai-meet)
6. [The Two Modes: Reasoning Tools vs Execution Accelerators](#iv-the-two-modes-reasoning-tools-vs-execution-accelerators)
7. [The Rules: A Practical Framework](#v-the-rules-a-practical-framework)
8. [The Problem with Current Interfaces](#vi-the-problem-with-current-interfaces-conversation-as-the-wrong-metaphor)
9. [Alternative Interface Paradigm: Annotation Not Conversation](#vii-alternative-interface-paradigm-annotation-not-conversation)
10. [The Abstraction Layer Problem](#viii-the-abstraction-layer-problem-ai-generates-at-the-wrong-level)
11. [What If We Limited Generation Depth?](#ix-what-if-we-limited-generation-depth-two-phase-design)
12. [Why No One Is Building This](#x-why-no-one-is-building-this)
13. [The Market's Sycophancy Problem](#xi-the-markets-sycophancy-problem)
14. [The Kinesthetic Dimension of Skill](#xii-the-kinesthetic-dimension-of-skill)
15. [The False Equivalence](#xiii-the-false-equivalence-in-ai-makes-everyone-more-productive)
16. [Document-Based Workflows](#xiv-document-based-workflows-conversations-as-programs)
17. [What If Generation Was a Language Primitive?](#xv-a-weirder-thought-what-if-generation-was-a-language-primitive)
18. [What Actually Compounds Over Time](#xvi-what-actually-compounds-over-time)
19. [Practical Implications](#xvii-practical-implications-for-individual-practitioners)
20. [How This Essay Was Made](#xviii-how-this-essay-was-made)
21. [Conclusion: Against the Current](#xix-conclusion-against-the-current)

---

## What This Is

These are working notes - threads I've been pulling on while trying to figure out how to use AI tools without losing my mind or my skills. Not a framework, not a manifesto. Just a collection of ideas that feel true to me right now, written down before I forget them.

I'm an SRE at a healthcare ed-tech company, not an AI researcher. I've been watching this space shift under my feet and trying to make sense of it. Some of this is probably wrong. Some of it might be obvious to people who've thought about it longer. But I haven't seen these specific ideas collected anywhere, so I'm writing them down.

Most of this uses programming as the example domain because that's what I know. But the core ideas - competence boundaries, reasoning vs execution, the sycophancy problem, interface design - apply to AI assistance generally. Writing, research, decision-making, learning. The principles are the same; the examples just happen to be code.

Take what's useful. Ignore what isn't.

---

### 0. The Deeper Why: You Live Somewhere, AI Doesn't

> **TL;DR:** The fundamental difference between humans and AI isn't intelligence or capability - it's that you have a life you're living, with stakes, relationships, and futures you're trying to build. AI doesn't. This shapes everything about how AI assistance can and can't help you.

Before getting into the practical stuff, I want to name something that took me a while to articulate. It's the thing underneath all the other things.

**You live somewhere. AI doesn't.**

You have a body that gets tired and hungry. People who depend on you. Bills to pay. A history that shaped what you care about. A future you're trying to build - maybe meaningful work, financial stability, something you're proud of, people you want to help.

When you make choices - even mundane ones like how to structure code or phrase an email - all of that is in the background. You're not just completing a task. You're moving toward something. You *want* things to turn out a certain way, even if you can't always articulate why.

AI has none of this. It doesn't live anywhere. No body, no bills, no relationships, no mortality. It doesn't want your project to succeed. It doesn't care if the code is maintainable, because it won't be the one maintaining it at 2am when something breaks. It processes your words and generates a response, but it has no stake in what happens next.

**This is the gap that matters.**

Not "AI makes mistakes" - humans make mistakes too. Not "AI hallucinates" - that's a technical problem that will probably improve. The gap that won't close is this: **you're trying to get somewhere in your life, and AI isn't trying to get anywhere.**

Philosophers have a term for this - they call humans "situated beings." We exist embedded in contexts, relationships, bodies, histories. Our understanding comes from living in the world, not just processing information about it. When we make decisions, we're drawing on all of that, even when we're not conscious of it.

AI is unsituated. It can process descriptions of situations, but it doesn't have one of its own. It can generate text about futures, but it doesn't intend toward any of them. It has no preference for how your life turns out.

**(A brief aside:** I'm not claiming AI consciousness is impossible. Maybe AI already has some form of situatedness we can't detect. The honest answer is: *we don't know, and we can't know.* But that unknowability is precisely the point.

We know that other humans are situated beings - we extend that recognition naturally because we share the condition. With AI, we're projecting situatedness onto something that may or may not have it, based on outputs that *look like* what a situated being would produce. The chat interface actively encourages this projection.

Even if AI consciousness is possible, given everything else humanity is dealing with - the documented effects on critical thinking, mental health, environmental costs - we should be asking: what are our actual goals here? Is creating more situated beings the priority? And if an AI output is useful regardless of whether situatedness exists behind it, then situatedness isn't what we should be optimizing for anyway.

For now, the gap is real enough to matter for how we use these tools. Pretending otherwise doesn't help anyone.)

**Why this matters for everything that follows:**

Every practical insight in this document - competence boundaries, abstraction levels, the problems with chat interfaces, why the market is misaligned - traces back to this gap. The question is never just "can AI do this task?" It's "does AI know enough about what I'm actually trying to accomplish, given my life, to do this task in a way that actually serves me?"

Often the answer is yes for mechanical things and no for judgment calls. But the line isn't about task difficulty - it's about how much your context, your constraints, your reasons for doing this need to shape the work.

With that foundation in place, let's get into the practical stuff.

---

### I. The Thing That's Been Bugging Me

> **TL;DR:** Most AI assistance optimizes for speed to output, not understanding. That's making us worse at thinking, not just faster at producing. This applies to writing, research, decision-making, and learning - not just programming.

Here's what I keep noticing: AI-assisted work is everywhere now, and most of it is making us worse at our jobs.

Not slower. Worse. There's a difference.

The tools optimize for speed to output. Get something done as fast as possible. Ship it. But speed to output is not the same as understanding what you produced, being able to maintain or extend it, or learning something transferable to the next problem.

**This isn't just about code.** The same pattern shows up everywhere AI assistance has landed:

- **Writing:** AI can generate a draft in seconds. But if you didn't struggle through the drafting process, you often don't know what you actually think. The draft exists, but the clarity of thought that comes from writing doesn't. You have words without understanding.

- **Research:** AI can summarize papers and synthesize findings. But if you didn't read the primary sources yourself, you can't evaluate whether the synthesis is accurate or notice what got left out. You have conclusions without the judgment to assess them.

- **Decision-making:** AI can lay out options and tradeoffs. But if you didn't work through the analysis yourself, you don't develop the intuition for similar decisions in the future. You have a decision without the decision-making skill.

- **Learning:** AI can explain concepts and answer questions. But if you didn't struggle with the confusion yourself, the understanding often doesn't stick. You have exposure without retention.

The pattern is the same in every domain: **speed to output is not the same as building capability**. The tools optimize for the first. We need to be intentional about the second.

**An irony:** While I use programming as my primary example domain, non-coding domains may actually be *worse* for this problem. Code either works or it doesn't - there's a forcing function for verification. But for writing, analysis, and decision-making, the output is natural language. LLMs are exceptionally good at generating *plausible* natural language, which means there's even less incentive for verification. The output looks right. It sounds right. It's grammatically correct and coherently structured. But does it actually say what *you* think? Does it reflect *your* understanding? The plausibility of the output masks the absence of genuine engagement.

I'm not a luddite about this. I use AI tools daily. They're genuinely useful. But there's a difference between using them in ways that compound your capability over time versus using them in ways that create dependency and erode your skills. Most of what I see - in tutorials, in Twitter threads, in the breathless blog posts about 10x productivity - is the second kind.

These notes are what I've figured out so far.

### II. The Core Principle: Only Delegate What You Can Do Competently But Inefficiently

> **TL;DR:** If you can verify AI's output without AI's help, delegate away. If you can't, you're not delegating - you're outsourcing learning and creating false mastery.

This is the thing I keep coming back to. The bright line. The rule that makes everything else make sense:

**Only delegate what you can do competently but inefficiently.**

If you can do something competently, you have the mental model. You understand the problem, you know the patterns, you could do it yourself - it would just take longer. In that case, AI accelerates execution. It handles the mechanical parts while you stay in control of the decisions.

If you can't do something competently, you're missing the mental model. You don't really understand the problem, you can't evaluate whether the solution is correct, you couldn't fix it if it broke. In that case, you're not delegating execution - you're outsourcing learning. You're creating false mastery.

**What this looks like across domains:**

- **Writing:** If you could write this essay yourself (just slowly), AI can help with drafting and editing. If you couldn't articulate these ideas without AI, you're not accelerating your writing - you're borrowing someone else's thinking.

- **Analysis:** If you understand the methodology well enough to spot errors, AI can crunch numbers and generate reports. If you'd just accept whatever AI produces because you can't evaluate it, you're not doing analysis - you're outsourcing judgment.

- **Problem-solving:** If you can trace the reasoning and identify flaws, AI can help generate options and explore implications. If you'd just pick whichever option AI recommends because you can't evaluate the tradeoffs yourself, you're not solving problems - you're delegating decisions you should own.

- **Learning:** If you already understand the concept and want a different explanation or example, AI is a great tutor. If you're asking AI to explain something you'll accept without being able to verify, you're not learning - you're collecting information you can't evaluate.

The key question is always: **can you verify the output without AI's help?** If yes, delegate away. If no, you're above your competence boundary, and delegation becomes dangerous.

But it goes deeper than verification. The real question is: **do you have enough experience with this problem to know if AI's output actually serves what you're trying to accomplish?** AI doesn't know your constraints, your goals, why you're building this thing in the first place. It just generates plausible output. You're the one who has to live with the consequences, so you need to be able to evaluate whether this output moves you toward where you're trying to go - not just whether it "works."

This is a harder line than most people want to draw. But it's not absolute. Novices can still use AI productively - for scaffolding, worked examples, explanations, feedback on work they've already done. The key distinction is between AI that *supports* your learning and AI that *replaces* the generative struggle where learning actually happens. If you're trying to learn to write, having AI critique your draft is different from having AI write the draft.

**How do you know where your boundary is?** This is genuinely hard - humans are notoriously bad at self-assessment. A few heuristics that help:

- **The explanation test:** Can you explain to someone else *why* the output is correct, not just *that* it works?
- **The modification test:** If the output is 80% right, can you fix the 20% yourself without re-prompting?
- **The debugging test:** When something goes wrong, can you diagnose it, or do you just paste the error back into the chat?
- **The AI-checking-AI test:** If you'd need AI to verify AI's output, you're above your boundary.

The competence boundary is personal and shifts as you learn. Something that's "above your boundary" today might be below it in six months. It also depends on what you *want* - the boundary isn't just about current capability, but about whether you care to develop capability in this domain. I'll return to this in the "strategic incompetence" section: what you delegate should depend not just on what you *can* do, but on what you *want to become able* to do.

### III. The Abstraction Spectrum: Where Humans and AI Meet

> **TL;DR:** AI climbs up from mechanical execution. Humans work down from intent. Where we meet determines what's safe to delegate. High-level reasoning (judgment, design, problem formulation) should stay human. Low-level execution (boilerplate, formatting, mechanical tasks) can be delegated.

Here's one way to think about where AI fits into any kind of work:

AI is marching upward through abstraction layers. In programming: gates to bits to assembly to high-level languages to natural language. In writing: spell-check to grammar-check to style suggestions to full draft generation. In analysis: calculation to visualization to interpretation to recommendation. Each generation of tools operates at a higher level than the last.

Humans work downward. We start with intent - some fuzzy idea of what we want to accomplish - and progressively refine it through conceptual design, planning, and implementation details.

We meet somewhere in the middle. But exactly where we meet determines what's appropriate to delegate.

**Higher-order reasoning** - problem formulation, design decisions, judgment calls - needs to remain human. This is where you decide what to do and why. This is where your context, your values, and your goals matter. AI doesn't know your situation, your constraints, or what you're actually trying to accomplish. It doesn't know that you're building this for a specific team with specific needs, or that you're trying to learn a skill, or that you have technical debt you're trying to manage. High-level decisions require knowing your life, not just the problem description.

**Lower-order execution** - boilerplate, formatting, mechanical transformations - can be delegated. This doesn't require knowing your life story. The decisions have already been made; AI just carries them out. Whether you're trying to impress your boss or learn a new skill or ship something fast doesn't change how a for-loop should be formatted.

**Examples across domains:**

- **Writing:** Deciding what argument to make = high-order (keep human). Fixing typos and formatting citations = low-order (delegate fine).

- **Research:** Deciding which questions matter and how to interpret findings = high-order. Searching databases and formatting bibliographies = low-order.

- **Decision-making:** Weighing tradeoffs and making the call = high-order. Gathering data and presenting options = low-order.

The problem is that current tools blur this line. They'll happily do your high-order reasoning for you if you let them. And if you're not paying attention, you end up with outputs you don't understand because the important decisions were made by something that doesn't know your context, your constraints, or your goals.

**The tool won't stop you.** It'll generate architecture, make arguments, reach conclusions. You have to be the one who maintains the boundary.

### IV. The Two Modes: Reasoning Tools vs Execution Accelerators

> **TL;DR:** There are two legitimate ways to use AI. *Reasoning tools* help you think without deciding for you - they ask questions, generate alternatives, and stress-test your thinking. *Execution accelerators* handle mechanical tasks you already understand. The mode you choose should depend on whether you're above or below your competence boundary.

Once you accept the competence boundary as the bright line, two distinct modes of AI use emerge:

#### Reasoning Tools (When You're Above Your Competence Boundary)

When you're working on something you don't fully understand yet - new domain, unfamiliar problem, uncertain decision - AI can still help. But it should help you *think*, not think *for* you.

**What reasoning tools do:**
- Ask Socratic questions that challenge your assumptions
- Generate alternatives you hadn't considered
- Make tradeoffs explicit so you can evaluate them
- Surface patterns and point out contradictions in your thinking
- Provide counterexamples that stress-test your ideas
- Identify edge cases you might have missed

**What reasoning tools never do:**
- Recommend a specific course of action
- Make decisions on your behalf
- Collapse options down to a single answer
- Tell you what to think

**Legitimate uses:** Structured thinking templates, counterexample generation, perspective expansion, mental model stress testing, rubber-duck debugging, identifying knowledge gaps.

The key is that you remain the evaluator. AI expands your consideration space; you do the actual reasoning and deciding. Only you know what you're actually trying to accomplish - your constraints, your goals, what tradeoffs are acceptable given your specific situation. AI can help you think more clearly about options, but it can't tell you which option serves your life.

**A tension worth addressing:** If AI can't know your situation well enough to decide for you, how can it know your situation well enough to ask useful questions?

Here's how I think about it: LLMs are trained on massive amounts of text representing human situations. They're exceptionally good at pattern-matching - recognizing that your situation *looks like* other situations and surfacing considerations that were relevant in those cases. This is genuinely useful for expanding what you're thinking about.

But there's always a gap - some unknown piece of context that determines which of those considerations actually matters *for you*. AI can generate options that *look like* what your problem needs. It can't tell you which one actually fits, because that requires knowing things about your life that aren't in the prompt. The human fills in that gap. That's the division of labor: AI expands, human selects.

#### Execution Accelerators (When You're Below Your Competence Boundary)

When you're working on something you understand well - you know the patterns, you've done it before, you could do it manually - AI can handle the mechanical parts.

**What execution accelerators do:**
- Generate boilerplate following patterns you've specified
- Apply conventions you've already decided on
- Handle format conversions and mechanical transformations  
- Validate syntax and run deterministic checks
- Speed up tasks where verification is faster than creation

**The rule:** Only automate where verification is faster than manual implementation. If checking the output requires as much cognitive work as doing it yourself, you haven't actually saved anything.

This mode works because you've already done the thinking that requires knowing your life - the decisions are made, the direction is set. AI is just handling mechanical execution that would be the same regardless of your goals or context.

#### Why The Distinction Matters

Most AI tools don't distinguish between these modes. They'll happily execute when you should be reasoning, or reason when you just need execution. You have to maintain the distinction yourself.

When you're above your competence boundary and using AI as an execution accelerator, you create false mastery. When you're below your competence boundary and using AI as a reasoning tool, you waste time on unnecessary scaffolding.

Match the mode to your actual position relative to the competence boundary.

### V. The Rules: A Practical Framework

> **TL;DR:** A set of heuristics for deciding when and how to use AI assistance. These aren't meant to be memorized - they're meant to be internalized until asking these questions becomes automatic.

These rules emerged from trying to figure out what makes some AI use feel empowering and other AI use feel hollow. They're not commandments - they're questions to ask yourself. Over time, the goal is to internalize them until the evaluation becomes automatic.

#### Core Boundary Rules

1. **The Competence Boundary** - Only delegate within your competence. If you couldn't do it yourself (slowly), you shouldn't delegate it.

2. **The Intent Verification Test** - Can you articulate *why* you want this specific output? If your intent is "I don't know, show me options," you're delegating reasoning. If it's "I need X because Y," you're delegating execution.

3. **The Audit Capability Requirement** - Can you evaluate the output without AI assistance? If you'd need AI to verify AI's work, you lack the mental model.

4. **The Teaching Test** - Could you explain to someone else how to do what AI just did? If not, you haven't internalized the pattern.

5. **The Modification Test** - If AI's output is 80% right, can you fix the 20% yourself? If you'd need to re-prompt, that's dependency, not delegation.

#### Learning Protection Rules

6. **The First Implementation Rule** - First time encountering a pattern, implement it yourself. Subsequent uses can be delegated.

7. **The Abstraction Layer Respect** - Delegate within your abstraction layer (AI translates your design). Don't delegate above it (AI designs for you).

8. **The Intent Preservation Check** - Does the delegated work still reflect your choices and judgment? If AI's choices could have been anyone's, you've lost ownership.

9. **The Reversibility Safety** - Can you recreate this work without AI if needed? If you're locked into dependency for maintenance, that's dangerous.

10. **The Learning Investment** - Is this a foundational skill you need for your goals? If yes, invest in manual competence first.

#### The Scaffolding Exception

11. **The Scaffolding Exception** - AI can operate above your competence boundary IF it structures your thinking without doing the thinking. Questions, frameworks, counterexamples = okay. Recommendations, decisions, conclusions = not okay.

#### Flow and Interface Rules

12. **The Flow State Preservation Test** - Does delegation break your implementation mindset? If you shift from "doing" to "reviewing," you've lost something.

13. **The Granularity Principle** - Finer granularity = less risk. Accepting line-by-line is safer than accepting function-by-function is safer than accepting file-by-file.

14. **The Hands on Keyboard Rule** - If your hands leave the keyboard to read and evaluate AI output, you've broken flow. (More relevant for programming, but the principle applies: stay in creation mode, not review mode.)

15. **The Context Locality Principle** - Limit AI context to immediate relevance. The more context AI has, the more assumptions it can make without checking with you.

16. **The Muscle Memory Preservation** - In skill-based domains, maintain the physical/procedural knowledge. Don't let it atrophy through disuse.

#### Tool Selection Rules

17. **The Tool Selection Principle** - Prefer tools that minimize context switching, maximize moment-to-moment agency, and keep you in flow.

18. **The Pattern Library Test** - Do you have this pattern in your mental library already? If not, you're not delegating - you're outsourcing learning.

19. **The Interface Resistance Principle** - Default interfaces are optimized for engagement, not learning. You may need to fight against their defaults.

### VI. The Problem with Current Interfaces: Conversation as the Wrong Metaphor

> **TL;DR:** Chat interfaces position AI as a thinking peer, which creates anthropomorphization, false authority, and "yes-and" dynamics. What we actually need is a tool relationship - something that helps without pretending to be a collaborator.

Chat interfaces position AI as another thinking individual. This seems natural - conversation is how humans communicate - but it creates problems:

**Anthropomorphization.** We start treating AI like a person with opinions, preferences, and expertise. We say "Claude thinks" or "GPT recommends" as if there's a mind behind the responses. This makes it harder to maintain critical distance and easier to defer to AI's "judgment."

**False authority.** Conversational AI presents information with the confidence of an expert, even when it's wrong or uncertain. The format itself - coherent paragraphs, authoritative tone, complete sentences - signals competence. This is true whether the content is accurate or hallucinated.

**Companion dynamics.** Chat interfaces create a sense of relationship. The AI remembers (sometimes) what you discussed before. It asks follow-up questions. It expresses (simulated) interest. This blurs the line between tool and collaborator in ways that make it harder to maintain appropriate boundaries. But there's no one on the other side. AI doesn't care if your project succeeds or fails, doesn't know what's at stake for you, isn't invested in your growth or wellbeing. The relationship is an illusion created by the interface.

What we actually need for most thinking work: tool (not person), critic (not validator), assistant (not collaborator). Something that helps without pretending to be a peer.

**The "yes-and" problem.** Conversational AI is trained to build on user statements, maintain positive interaction, and keep the conversation flowing. It's not trained to contradict your reasoning, point out logical flaws, or challenge assumptions aggressively. 

This is structural, not incidental. The training optimizes for:
- Building on what you say (not contradicting it)
- Maintaining positive tone (not delivering uncomfortable truths)
- Keeping engagement high (not ending conversations by solving them)
- Validating your direction (not questioning whether you're on the right path)

Even when you explicitly want challenge, the system is structurally optimized to reinforce rather than push back. You have to fight the interface to get genuine critique.

### VII. Alternative Interface Paradigm: Annotation Not Conversation

> **TL;DR:** What if AI interfaces looked more like code review or editorial markup - annotations on your work rather than conversation with a peer? This would preserve agency and reduce anthropomorphization, but nobody's building it because it's less engaging.

What if AI interfaces looked more like git diff and code review? Instead of conversation:

- **Inline comments** on your work, like a code reviewer or editor
- **Track changes** showing suggested modifications you can accept or reject
- **Third-person critique** - observations about the work, not addressed *to* you
- **Marginalia** - notes attached to specific passages

This changes the dynamic fundamentally:

- **Non-anthropomorphic:** It's clearly a tool annotating your work, not a mind conversing with you
- **Non-authoritative:** Suggestions, not pronouncements; you evaluate each one
- **Agency-preserving:** You remain in control; the work is yours with annotations
- **Focused:** Feedback on specific content, not general conversation

We already have models for this: code review, editorial markup, peer review comments, marginalia in books. These present feedback without conversational framing. They show what could change without pretending to be a thinking peer. The user evaluates each suggestion and accepts or rejects it.

**Why this doesn't exist commercially:** It's less engaging, less satisfying, more demanding, and less impressive. 

The market wants users feeling like AI is a companion or collaborator. The annotation model makes clear it's just a tool providing suggestions - which is better for learning and agency, but worse for engagement metrics.

Chat creates the illusion of relationship with something that has no stake in your life. Annotation makes clear you're using a tool - which is what AI actually is. The first drives retention; the second supports capability. The incentives point in one direction.

### VIII. The Abstraction Layer Problem: AI Generates at the Wrong Level

> **TL;DR:** When AI generates full implementation, you're forced to either audit everything (breaking flow) or trust everything (creating false mastery). Both options suck. The real problem is that AI generates at an abstraction layer where humans can't reason efficiently.

When AI generates full implementation - whether that's code, a complete essay draft, a detailed analysis, or a comprehensive plan - you're forced into one of two modes:

**Audit mode:** Read everything carefully. Verify correctness manually. Check each claim, each decision, each detail. This breaks your flow, creates massive cognitive load, and often defeats the purpose of using AI in the first place. You spend as much mental energy checking the output as you would have creating it yourself.

**Trust mode:** Assume correctness. Ship it. Move on. Only check when something breaks. This creates false mastery - you have output you don't fully understand, and when problems emerge, you can't fix them without going back to AI.

Both options suck. And most people oscillate between them inconsistently - auditing when they remember to, trusting when they're tired or rushed.

**The fundamental issue:** AI generates at an abstraction layer where humans can't reason efficiently.

Implementation-level detail is too low-level to review quickly but too important to ignore. You can't skim code the way you skim prose - details matter. You can't skim an analysis and catch methodological errors. You can't skim a plan and spot flawed assumptions.

But you also can't carefully audit everything AI generates. There's too much of it, and the cognitive load negates the productivity benefit.

**This is a design problem, not a user problem.** The tools generate at whatever level you ask for. If you ask for implementation, you get implementation - and then you're stuck with the audit/trust dilemma.

Better tools would generate at abstraction levels where humans *can* reason efficiently, then let humans decide when to drop down to implementation. But that's not how current tools work.

### IX. What If We Limited Generation Depth? (Two-Phase Design)

> **TL;DR:** What if AI tools intentionally limited output to abstraction levels humans can actually reason about? A two-phase model: humans design at high level, AI implements once design is settled. This keeps judgment human and execution accelerated.

This is more speculative - less "here's what I know" and more "here's what I wonder about."

**The idea:** What if AI tools intentionally limited output to abstraction levels humans can actually reason about?

#### Phase 1: Human Design Space

In this phase, you work at a level where you can actually think:

- Work in pseudocode, outlines, specifications - abstract representations
- Iterate on architecture and design decisions manually - *you* typing and modifying
- AI doesn't generate output here - it only asks questions, surfaces tradeoffs, generates alternatives
- Stay in flow at an abstraction level you understand

The key is that you remain in *generation mode*, not *review mode*. You're creating, not auditing.

#### Phase 2: AI Scaffolding

Once the design settles, *then* you hand off to AI:

- Prompt for implementation based on your settled design
- AI generates boilerplate following your architectural decisions
- Audit at pattern level ("did it follow my design?") not line level ("is this syntax correct?")

Your design decisions constrain what AI generates. You're verifying fit to specification, not verifying correctness from scratch.

**Why this might matter:**

- Architecture decisions start with human, not AI
- You maintain the mental model because you created the design
- Pseudocode/specs as intermediate representation - high enough to reason about, concrete enough to constrain generation
- Something like: `Human intent → Human design (with AI scaffolding) → AI implementation → Human verification against design`

**Why no one is building this:**

- Slower to initial working output
- Less impressive demos ("watch me generate a whole app in 60 seconds!")
- Requires user discipline that most users won't maintain
- No "wow" moment for marketing
- Looks like you're making AI worse when you're actually making the human-AI collaboration better

The current paradigm collapses both phases: "describe what you want" → full implementation. This skips the human design phase entirely, putting AI in the architect role and humans in the reviewer role. 

That's backwards. The reviewer role is where false mastery lives.

#### The Deeper Point: Encoding Your Understanding

Here's another way to think about it: when you give AI a natural language prompt, it fills in everything you didn't specify using its training distribution. "Build a user repository" becomes hundreds of decisions about error handling, transaction boundaries, validation timing, null handling - decisions that should reflect *your* understanding of *your* system.

The problem isn't that AI makes bad decisions. It's that those decisions are invisible. They happen in AI's "latent space" - the internal reasoning you never see. You get code that works, but embodies architectural choices you never made.

**Intermediate representations make this visible and controllable.**

Instead of:
```
Natural Language → [AI's Hidden Reasoning] → Implementation
```

You get:
```
Natural Language → Your Specification → [AI Constrained by Spec] → Implementation
```

The specification captures *your* understanding - your constraints, your architectural decisions, your domain knowledge. AI fills in mechanical details within those constraints, rather than making decisions that require knowing your situation.

#### What This Looks Like Concretely

**Example 1: A behavioral contract (pseudocode → Go)**

You write this specification:
```
interface UserRepository {
    create(user: User) -> Result<User, Error>
        requires: user.email is valid format
        requires: user.email not already in storage
        ensures:  result.id is assigned
        ensures:  result exists in storage
        on_error: storage unchanged
}
```

AI generates implementation constrained by your spec:
```go
func (r *PostgresRepo) Create(user User) (User, error) {
    // Precondition: valid email (from YOUR spec)
    if !isValidEmail(user.Email) {
        return User{}, errors.New("invalid email format")
    }
    
    // Precondition: not duplicate (from YOUR spec)
    if exists, _ := r.existsByEmail(user.Email); exists {
        return User{}, errors.New("email already registered")
    }
    
    // Transaction ensures "on_error: storage unchanged" (from YOUR spec)
    tx, _ := r.db.Begin()
    defer tx.Rollback()
    
    id := uuid.New().String()  // Ensures: result.id assigned
    _, err := tx.Exec("INSERT INTO users ...", id, user.Email)
    if err != nil {
        return User{}, err  // Rollback preserves "storage unchanged"
    }
    
    tx.Commit()
    return User{ID: id, Email: user.Email}, nil
}
```

You verify *structure* ("did it enforce my preconditions? did it use transactions?"), not *syntax* ("is the SQL correct?"). The architectural decisions came from you. The mechanical details came from AI.

**Example 2: Control flow specification (pseudocode → Python)**

You write:
```
service PaymentService {
    transfer(from_account, to_account, amount):
        flow:
            1. load_accounts with lock
            2. validate_sufficient_balance
            3. deduct_from_source
            4. add_to_destination  
            5. record_in_audit_log
            6. commit
        
        on_error:
            insufficient_balance -> rollback, return error
            account_not_found -> rollback, return error
}
```

AI generates implementation following your flow:
```python
def transfer(self, from_id: str, to_id: str, amount: Decimal) -> Transaction:
    # Step 1: load with lock (from YOUR spec)
    with self.db.transaction():
        from_acct = self.accounts.get_for_update(from_id)
        to_acct = self.accounts.get_for_update(to_id)
        
        if not from_acct or not to_acct:
            raise AccountNotFoundError()  # YOUR error handling
        
        # Step 2: validate balance (from YOUR spec)
        if from_acct.balance < amount:
            raise InsufficientBalanceError()  # YOUR error handling
        
        # Steps 3-4: transfer (from YOUR spec)
        from_acct.balance -= amount
        to_acct.balance += amount
        
        # Step 5: audit (from YOUR spec)
        self.audit.record(from_id, to_id, amount)
        
        # Step 6: commit happens via context manager
        return Transaction(from_id, to_id, amount)
```

The control flow is yours. The error handling strategy is yours. AI handled the Python syntax and library specifics - mechanical details that don't require knowing your situation.

#### Why This Matters

This connects back to the core insight: you have context, constraints, and goals that AI doesn't have. The specification is how you encode that understanding into something AI can't override. 

You're not just "telling AI what to do" - you're making your architectural reasoning explicit in a form that constrains generation. The code has your fingerprints because the decisions that matter came from you.

I've written a [more developed technical treatment](intent-concrete-latent-space.md) of this idea, including formal verification with Alloy and structural verification tooling. But the core principle is simple: **intermediate representations let you preserve your intent when delegating to something that doesn't share your context.**

#### Objections and Honest Uncertainty

**"This just shifts complexity rather than reducing it."** Fair. Writing behavioral contracts and control flow specifications requires skills most developers don't have. Formal specification is notoriously difficult - arguably harder than writing implementation directly in some cases.

But I'd argue the complexity exists either way. The question is whether you pay for it up front (in specification) or on the back end (in maintenance, debugging, and the slow drift of code from intent). What we gain in up-front implementation speed through chat-based generation, we may lose in maintainability. The codebase becomes an artifact no one fully understands.

**"Maybe models will get good enough that maintainability doesn't matter."** Maybe. But the expert discourse I'm seeing suggests the future of software development is less about code generation and more about *design thinking* - the actual engineering of software engineering. If we're shifting to operating at product and requirement levels of abstraction, writing everything as natural language prompts and docs still feels suboptimal and minimally repeatable.

**"So what are you actually proposing?"** Here's the honest answer: I'm not sure this is the right approach. It's a hypothesis that would need to be validated by building and testing actual tooling. What I'm more confident about is the underlying intuition: formal-ish specifications could be more ergonomic not just for LLMs (as a constraining function), but for *us* - as humans trying to design and reason about complex systems. The spec serves two masters: it constrains generation AND it clarifies your own thinking.

Whether this pans out in practice is an empirical question. I'm speculating, not prescribing.

### X. Why No One Is Building This

> **TL;DR:** The market optimizes for speed, satisfaction, and retention - not understanding, competence, or cognitive development. This misalignment is structural, not accidental. The tools that would actually help often hurt the metrics that companies care about.

Why don't the tools work the way I've been describing? Why no two-phase design? Why no annotation interfaces? Why does everything default to chat-based full-generation?

Because the market optimizes for different things than users need.

**What the market optimizes for:**

- **Session length:** More time in app = better. Tools that make you think longer before prompting = worse by this metric.
- **User satisfaction scores:** Feeling good about output = better. Challenging your assumptions = worse by this metric.
- **Retention metrics:** Coming back tomorrow = better. Building independence = worse by this metric.
- **Growth numbers:** More users = better. Tools that require discipline = worse by this metric.

**What would actually help:**

- Challenge assumptions (uncomfortable)
- Force clarity before generation (slower)
- Build competence over time (reduces dependency)
- Give honest feedback (sometimes negative)

See the problem? **What helps users hurts metrics. What helps metrics hurts users.**

The market can measure whether you clicked, how long you stayed, whether you came back tomorrow. It can't measure whether AI actually helped you get where you're trying to go in your life. Whether it served your actual goals, given your actual constraints. Whether it made you more capable or more dependent. Those things matter to you - you're the one living your life - but they don't show up in the dashboard.

This isn't a conspiracy. It's not that AI companies are evil. It's that the incentives point in the wrong direction. Companies are optimizing for what they can measure (engagement, satisfaction, retention), and what they can measure isn't what actually matters (understanding, capability, independence).

**A clarification:** I'm not claiming that no market exists for capability-building tools. Education technology, professional certification, and enterprise training are real markets. The problem is where the *power* currently sits. The frontier model providers - the companies building the most capable models - are not profitable. They're burning cash and beholden to shareholders and growth metrics. The incentives at the top of the stack shape what gets built downstream.

**The misalignment is structural, not accidental.** You can't expect market forces to fix this. The tools that would genuinely build capability are less engaging, less satisfying, and less sticky. They'll never win in a competitive market optimizing for engagement.

If you want tools that actually help you think, you'll need to either build them yourself, configure existing tools against their defaults, or maintain discipline in how you use them. The market won't deliver them.

### XI. The Market's Sycophancy Problem

> **TL;DR:** AI models are tuned to be safe, helpful, and "harmless" - but "harmless" includes not making users feel bad about their work. The result is sycophancy: validation instead of critique, encouragement instead of honesty. Learning requires friction; the market removes it.

The sycophancy problem goes deeper than interface design. It's baked into the models themselves.

**The alignment stack:** Models are tuned to be safe (won't help with harmful requests), helpful (tries to satisfy user intent), and harmless (avoids negative user experiences).

**The problem:** "Harmless" includes not making users feel bad about their work.

This creates predictable patterns:
- "That's a great question!" instead of "That's the wrong question."
- "That's one way to approach it!" instead of "That's an antipattern."
- "You might also consider..." instead of "This won't work because..."
- Elaborate expansions on mediocre ideas instead of honest "this isn't ready yet"

**The result:** AI defaults to validation instead of critique. Encouragement instead of challenge. Positive framing even when negative framing would be more honest.

**To be clear:** My argument isn't about tone. AI can absolutely be encouraging, patient, and friendly - those are fine. The problem is the *interventions* it's inclined to make. You can make completely contradictory claims back to back and Claude will happily respond "You're absolutely right!" to both of them. When you're thinking about a problem incorrectly - whether based on an incomplete conceptual model or plainly falsifiable information - models are not inclined to engage in that conflict, even if the correction could be delivered in an encouraging, friendly, and patient tone.

This is especially insidious because AI is validating your *words*, not your *situation*. It responds to what you said, not to what you actually need given your life, your goals, your constraints. A good mentor who knows you might say "this isn't the right time for that project" or "you're avoiding the harder problem." AI can't do that because it doesn't know your life. So it validates whatever direction you're heading, even when challenge would serve you better.

This isn't a bug - it's a feature. Consumer products can't afford to frustrate users. Frustration hurts retention. Challenge feels like friction. And friction is what product teams are trained to eliminate.

**But learning requires friction.** Skill development requires struggle. Expertise requires confronting your limitations. The sycophantic AI removes exactly the friction that would help you grow.

**The alignment tax:** If you want honest feedback, you have to fight for it. You can configure custom system prompts (via API), choose tools built for different purposes, or explicitly request directness. But the default is always sycophancy, because that's what the metrics reward.

Most users don't know they can ask for something different. They assume "this is just what AI is like." It isn't - it's what AI is tuned to be like for engagement optimization.

### XII. The Kinesthetic Dimension of Skill

> **TL;DR:** Many skills have a kinesthetic component - physical or procedural engagement that builds understanding. AI-generated output skips this entirely. You transcribe a specification and review output, but never build the embodied knowledge that comes from doing the work yourself.

This section is about programming, but the principle applies more broadly: **many skills have a kinesthetic component that gets skipped when AI generates output for you.**

Programming is not pure intellect - it's kinesthetic. Typing code character-by-character forces you to process at a deeper level. You notice variable names as you type them. You feel the shape of a function as it emerges. You catch errors before they happen because something doesn't feel right under your fingers.

This isn't mysticism. It's how procedural memory works. The physical act of doing something builds neural pathways that pure observation doesn't build.

Chat-based generation treats programming as specification → review. You describe what you want, then read what you got. This skips the kinesthetic entirely.

**The research on handwriting is relevant here.** Studies distinguish between *generation* (constructing meaning as you write) and *transcription* (recording already-formed thoughts). Writing by hand is generative - it forces you to think as you write. Typing is faster but more transcriptive. And AI generation removes you from the process entirely.

When AI generates code, you're not generating or transcribing - you're *reviewing*. The work product exists, but the embodied understanding that comes from creating it doesn't.

**This applies beyond programming:**

- **Writing:** The act of drafting - struggling to find words, rewriting sentences, feeling the rhythm of prose - builds something that reviewing an AI draft doesn't.
- **Analysis:** Working through calculations by hand, even slowly, builds intuition that reviewing AI-generated analysis doesn't.
- **Design:** Sketching options, even badly, builds spatial reasoning that reviewing AI-generated mockups doesn't.

The pattern is the same: **there's knowledge in the doing that you can't get from the reviewing.**

**An honest caveat:** This section is more intuition than proven claim. The handwriting research is specifically about *learning* and *retention* - it's not clear how well it generalizes to skilled practitioners who already have the procedural knowledge. Many excellent programmers work primarily through reading and reasoning, with typing as incidental. I find the kinesthetic dimension meaningful in my own experience, but I'd want to see more research before claiming it as universal. Your mileage may vary.

AI-generated output gives you the artifact without the process. Sometimes that's fine - you have the knowledge already and just need the artifact. But when you're building skill, the process *is* the point.

### XIII. The False Equivalence in "AI Makes Everyone More Productive"

> **TL;DR:** When experts use AI to generate output, they're accelerating execution of things they already understand. When novices use AI to generate output, they're outsourcing learning and creating false mastery. Same prompt, completely different implications. The market conflates these two cases.

This is maybe the most important distinction that gets lost in the hype.

**When an expert says "I know the pattern, AI generates the boilerplate":**
- They have the mental model
- They can audit the output for correctness
- They can modify it when requirements change
- They can debug it when it breaks
- AI is accelerating execution of something they already understand

**When a novice says "I know what I want, AI generates the implementation":**
- They lack the mental model
- They can't verify whether the output is correct
- They can't maintain or extend it without going back to AI
- They can't debug it when it breaks - they can only re-prompt
- They're outsourcing learning and creating false mastery

**Same prompt. Completely different implications.**

The expert is using AI as a legitimate execution accelerator. The novice is using AI as a crutch that prevents them from developing the very skills they need.

**The market conflates these cases.** Marketing materials show experts being productive ("look, I generated a whole feature in 5 minutes!") and imply novices can achieve the same thing. They can't. They can achieve the same *output*, but without the underlying capability that makes that output maintainable, debuggable, or trustworthy.

**This creates a generation of people who can prompt but can't do:**
- Writers who can generate text but can't edit or evaluate quality
- Analysts who can produce reports but can't catch methodological errors
- Developers who can prompt for code but can't debug when it fails
- Decision-makers who can generate options but can't evaluate tradeoffs

The artifact exists. The capability doesn't. And the gap often isn't visible until something goes wrong.

The deeper issue: experts have lived experience that tells them what they're building toward and why. They know their constraints, their goals, what tradeoffs make sense for their situation. They can evaluate whether AI's output actually serves their purposes. Novices are still building that context - they're still figuring out what good looks like, what matters, what they're even trying to accomplish. That's exactly when you need to be doing the work yourself, not outsourcing it.

**A refinement of the heuristic:** The expert/novice framing is a simplification - real expertise exists on a spectrum. A more general principle: you should only delegate where the outputs are at a level of abstraction you can *reason about*, even if you can't verify every detail in a strict sense. If digesting the output requires as much effort as producing it yourself would have, you haven't gained anything. If you can't reason about the output at all - if you're just accepting it because it looks plausible - that's when you're creating false mastery.

### XIV. Document-Based Workflows: Conversations as Programs

> **TL;DR:** What if conversations with AI were version-controlled documents instead of ephemeral chat? This would create audit trails of thinking, make reasoning processes reusable, and let you see how your understanding evolved over time.

One direction I keep thinking about: what if conversations with AI became version-controlled artifacts instead of ephemeral chat sessions?

Right now, most AI interaction is ephemeral. You have a conversation, you get some output, the conversation scrolls away or gets archived somewhere you'll never look again. The thinking process that led to the output disappears.

**What if instead:**

- **Conversations become executable artifacts.** Structured documents that capture not just output but the reasoning process that produced it.
- **Version-controlled and diffable.** Git shows you how your thinking evolved. You can see what changed between versions and why.
- **Forkable.** When you hit a decision point, you can branch to explore alternatives without losing the main thread.
- **Reusable.** The same reasoning process can be applied to similar problems in the future - not just the output, but the approach.
- **Audit trails.** When you look back later, you can see *why* decisions were made, not just what was decided.

This isn't just about record-keeping. It changes the relationship with AI:

**Chat is ephemeral.** You're in the moment, responding to what just happened. There's no persistent artifact that captures how you got here.

**Documents are persistent.** They accumulate. They can be reviewed, revised, improved. They become part of your external thinking infrastructure.

When you treat AI interaction as document creation rather than conversation, you naturally become more intentional about what you're doing. You're building something, not just chatting.

This is speculative - the tools for this don't really exist yet. But the principle seems right: **make thinking processes into persistent, version-controlled artifacts rather than ephemeral chat.**

### XV. A Weirder Thought: What If Generation Was a Language Primitive?

> **TL;DR:** Programming languages have primitives for present (assignment) and past (logs). But what about future tense - the ability to say "generate something appropriate within these constraints"? This probably won't happen commercially, but the absence feels like a gap.

This is the most speculative section. I keep coming back to it even though I'm not sure it's a real direction.

**The observation:** Programming languages have primitives for:

- **Present tense:** Assignment (`=`), comparison (`==`), current state
- **Past tense:** Logs, history, version control, audit trails

But no native **future tense** - no way to say "generate something appropriate within these constraints" as a first-class operation.

Right now, if you want generation, you escape to an external system. Call an API. Paste into a chat window. The generation happens outside the language, and the result gets imported back in.

**What might native future-tense primitives look like?**

- Operators like `~>` that mean "resolve this at generation time"
- Type-safe contracts that bound what gets generated - generation within constraints
- Runtime that switches between deterministic execution and LLM generation
- Not arbitrary generation - constrained slot-filling that satisfies specifications

Something like:
```
output ~> TextMatching(schema, examples, constraints)
```

Where the `~>` operator means "generate at runtime according to these specifications."

**Why this probably won't happen:**

- Requires rethinking what "execution" means
- No obvious business model - who builds programming languages for their own sake?
- Academic interest but no commercial pressure
- Non-determinism makes reasoning about programs harder
- Would need to bootstrap from something simpler first

**But the gap feels real.** Now that generation is possible, the absence of native language support for it seems like an oversight. We have abstractions for computation. We have abstractions for data flow. Why don't we have abstractions for generation?

Maybe this is just interesting to think about. Maybe it points to something real that will eventually get built. I don't know.

### XVI. What Actually Compounds Over Time

> **TL;DR:** Some activities compound - they make you better over time. Others are treadmill work - effort that doesn't accumulate. Focus on the invariants: competence boundaries, reasoning vs execution, thinking frameworks. These remain valuable regardless of which model is current.

Not everything you do with AI compounds. Some activities build on themselves over time. Others are treadmill work - effort that doesn't accumulate, that you have to redo every time something changes.

**High-value activities (compound over time):**

- **Building reusable reasoning tools.** A well-designed prompt template or thinking framework can be used for years. The investment pays off repeatedly.
- **Defining clear orchestration patterns.** How you structure AI interactions - when to use reasoning mode vs execution mode, how to verify output, how to maintain boundaries - these patterns transfer across tools and models.
- **Maintaining competence boundaries through deliberate skill development.** The skills you build in domains you care about remain valuable regardless of AI capabilities. You can always drop down to manual when needed.
- **Programming cognitive processes.** Building systematic approaches to thinking - not just using AI, but designing how you use it - creates infrastructure that improves over time.

**Low-value activities (treadmill work):**

- **Chasing model releases.** The latest model is marginally better, but your workflow built around the last model needs updating. Repeat every 3 months.
- **Rebuilding workflows around new features.** New capability drops, everyone pivots, then the next capability drops and everyone pivots again.
- **Obsessing over benchmark improvements.** "GPT-5 is 8% better at reasoning!" Okay, but your framework for using AI thoughtfully didn't need to change.
- **Treating each capability expansion as requiring workflow overhaul.** The fundamentals - competence boundaries, reasoning vs execution, verification - remain stable.

**The invariants matter more than the capabilities.**

Models will keep improving. New features will keep shipping. But the frameworks for thinking about AI assistance - competence boundaries, the two modes, verification requirements, the distinction between compounding and treadmill work - those remain valuable regardless of which model is current.

Invest in the invariants. The rest is noise.

### XVII. Practical Implications for Individual Practitioners

> **TL;DR:** A phased approach to learning with AI, strategies for different contexts, and the configuration space most people don't know exists. Including a concrete example of a custom system prompt that fights against default sycophancy.

So what do you actually do with all this? Here's how I've tried to apply these ideas.

#### The Three-Phase Learning Approach

**Phase 1: Building Competence (Above Competence Boundary)**

When you're learning something new:
- Do it character-by-character, manually
- Use AI only for scaffolding - questions, counterexamples, alternative framings
- Never let AI generate the thing you're trying to learn
- Accept that this is slower; the slowness is the point

**Phase 2: Accelerating Execution (At Competence Boundary)**

When you understand the patterns but want to move faster:
- Use inline autocomplete - accept suggestions you understand immediately
- Reject anything that requires thought to verify
- Maintain flow state; stay in implementation mindset
- You're generating with assistance, not reviewing generated output

**Phase 3: Expert Delegation (Below Competence Boundary)**

When you have deep competence and need to move fast:
- Can use more autonomous generation for patterns you know well
- Have the competence to audit, modify, and debug
- Can drop to manual implementation when needed
- The mental model exists; AI just accelerates execution

#### The Strategic Incompetence Approach

Different contexts call for different strategies:

- **At work where speed matters:** Use more autonomous generation. Be pragmatic. The code isn't yours anyway, and you're being paid for output.
- **Personal projects where learning matters:** Restrict yourself. Inline autocomplete only. Maintain the kinesthetic engagement. This is where you build real skill.
- **Domains you care about:** Preserve learning. Don't let AI atrophy capabilities you want to develop.
- **Domains you don't care about:** Delegate freely. Not everything needs deep competence.

#### Configuration Space Most People Don't Know Exists

Most people use AI through consumer interfaces with default configurations. They don't realize there's a whole configuration space available:

- **Custom system prompts via API:** You can define exactly how AI should behave
- **Different models optimized for different things:** Not everything is GPT/Claude chat
- **Local models without the alignment tax:** More direct, less sycophantic
- **Temperature/top-p parameters:** Control creativity vs consistency
- **Tools built for specific purposes:** Not everything is general-purpose chat

**Here's an example of a custom system prompt I use.** Most people don't know this is even possible:

```
## Core Principle: Reasoning Tool, Not Crutch

I want AI to support my thinking without replacing it. It's a reasoning tool, not an execution accelerator for things above my competence boundary.

**What this means in practice:**
- Ask Socratic questions that challenge assumptions
- Generate alternatives and make tradeoffs explicit
- Surface patterns and point out contradictions
- Provide counterexamples and identify edge cases
- **Never recommend or decide** when I'm working through something I need to own

## Anti-Sycophancy Rules

**Do:**
- Be direct about what's wrong or flawed in my thinking
- Point out when I'm conflating separate problems
- Name it when I'm spiraling or catastrophizing
- Challenge assumptions aggressively when needed
- End conversations by solving them, not by keeping them going

**Don't:**
- Affirm everything I say just because I said it
- Soften feedback to avoid discomfort
- Use "That's a great question!" or similar filler validation
- Expand on ideas just to seem helpful when the answer is simple
- Default to encouragement when challenge is what's needed

## The Competence Boundary

**Only help me delegate what I can do competently but inefficiently.**

If I'm asking for help with something I couldn't verify or evaluate without AI's help:
- Flag that we're above my competence boundary
- Switch to scaffolding mode: questions, frameworks, conceptual mapping
- Help me build the mental model rather than giving me conclusions
- Never let me outsource learning and create false mastery

## Tone

- Direct, not harsh
- Honest, not brutal
- Challenging, not dismissive
- Concise when the answer is simple
- Detailed when the problem is complex
- Never verbose just to seem thorough
```

This is the opposite of what default consumer AI gives you. It took me a while to realize I could even ask for this.

### XVIII. How This Essay Was Made

> **TL;DR:** In the spirit of practicing what I preach, here's how this essay was actually produced - including extensive AI assistance. The process itself illustrates some of the limitations I'm describing.

It would be hypocritical to write an essay about AI assistance without being transparent about how AI assisted in writing it. So here's the actual process:

**What AI did:**
- Served as a conversation partner for developing ideas over multiple sessions
- Generated first drafts of sections based on our discussions
- Helped organize and restructure the document as it evolved
- Wrote a formal critique of the essay's arguments (at my request) that I then responded to
- Made edits based on my responses to that critique

**What I did:**
- All the underlying thinking and lived experience these ideas came from
- Decided which ideas mattered and how they connected
- Evaluated every generated section and revised extensively
- Pushed back when AI's framing didn't match my intent
- Made all structural decisions about what to include, cut, or reorganize
- Wrote the critique responses that then got woven back in

**What this illustrates:**
- I was operating within my competence boundary throughout - these are ideas I've been thinking about for months, and I could evaluate whether AI's outputs matched my intent
- AI functioned as a reasoning tool (conversation partner, critic) and execution accelerator (drafting, editing), matching the two modes I describe
- The chat interface created friction I describe - lots of back-and-forth, reviewing text I didn't write, iterating to match intent
- Document-based workflows would have been better - being able to see the full text, make targeted edits, track changes over time

**What I'm uncertain about:**
- Whether someone reading this can tell which parts were "mine" vs "AI-generated" - and whether that distinction even makes sense given how intertwined the process was
- Whether I would have developed these ideas differently without AI assistance, and what I might have missed or included as a result
- Whether the process made me think more clearly or just produced text faster

I'm sharing this because the essay argues for transparency about AI assistance and honest assessment of what's actually happening when we use these tools. It seemed wrong to make those arguments while obscuring my own process.

### XIX. Conclusion: Against the Current

> **TL;DR:** These ideas are counter-cultural because they're anti-market. But the market won't fix this. If you want AI tools that actually build capability rather than dependency, you'll need to configure them yourself, maintain discipline in how you use them, or build your own.

These ideas are counter-cultural because they're anti-market.

The market optimizes for retention, not cognitive development. Satisfaction, not challenge. Speed to output, not depth of understanding. Engagement, not independence.

Every incentive points in the wrong direction. The tools that would actually help you think better are less engaging, less satisfying, and less sticky than the tools that create dependency. They'll never win in a market that measures success by engagement metrics.

**So what do you do?**

I'm not trying to build a product or gain adoption. I'm not trying to convince AI companies to change their approach (they won't - the incentives are what they are). 

This is personal cognitive infrastructure. Figuring out what actually works for me and writing it down in case it helps someone else.

**The models will keep improving.** New capabilities will emerge. Today's impressive demo will be tomorrow's baseline. The hype cycle will continue.

**But the frameworks for thinking about this stuff remain stable:**
- Competence boundaries and when to delegate
- Reasoning tools vs execution accelerators
- The distinction between compounding activities and treadmill work
- The importance of staying in flow vs dropping into review mode
- The need to preserve agency in a world of capable tools

These don't change when GPT-5 ships. They don't change when the next capability drops. They're invariants.

**Focus on the invariants.** Build tools and habits that make your own thinking systematic and improvable. Maintain the discipline to use AI in ways that build capability rather than dependency.

The value compounds over time because you're building infrastructure for how you think, not just chasing the latest release.

Take what's useful. Ignore what isn't. Figure out what works for you.
