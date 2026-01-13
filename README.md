# Some Incomplete Thoughts on AI-Assisted Programming

## What This Is

These are working notes - threads I've been pulling on while trying to figure out how to use AI tools without losing my mind or my skills. Not a framework, not a manifesto. Just a collection of ideas that feel true to me right now, written down before I forget them.

I'm an SRE at a healthcare ed-tech company, not an AI researcher. I've been watching this space shift under my feet and trying to make sense of it. Some of this is probably wrong. Some of it might be obvious to people who've thought about it longer. But I haven't seen these specific ideas collected anywhere, so I'm writing them down.

Most of this uses programming as the example domain because that's what I know. But the core ideas - competence boundaries, reasoning vs execution, the sycophancy problem, interface design - apply to AI assistance generally. Writing, research, decision-making, learning. The principles are the same; the examples just happen to be code.

Take what's useful. Ignore what isn't.

---

## Outline

### I. The Thing That's Been Bugging Me

*Most AI-assisted programming optimizes for speed to working code, not understanding. That's making us worse, not just faster.*

Here's what I keep noticing: AI-assisted programming is everywhere now, and most of it is making us worse at our jobs.

Not slower. Worse. There's a difference.

The tools optimize for speed to working code. Get something running as fast as possible. Ship it. But speed to working code is not the same as understanding what you built, or being able to maintain it, or learning something transferable to the next problem.

I'm not a luddite about this. I use AI tools daily. They're genuinely useful. But there's a difference between using them in ways that compound your capability over time versus using them in ways that create dependency and erode your skills. Most of what I see - in tutorials, in Twitter threads, in the breathless blog posts about 10x productivity - is the second kind.

I'm an SRE at a healthcare ed-tech company. I've been watching this space shift under my feet for the past couple years, trying to figure out what actually helps versus what just feels productive in the moment. These notes are what I've figured out so far.

### II. The Core Principle: Only Delegate What You Can Do Competently But Inefficiently

*If you can verify the output without AI's help, delegate away. If you can't, you're not delegating - you're outsourcing learning.*

This is the thing I keep coming back to. The bright line. The rule that makes everything else make sense:

**Only delegate what you can do competently but inefficiently.**

If you can do something competently, you have the mental model. You understand the problem, you know the patterns, you could implement it yourself - it would just take longer. In that case, AI accelerates execution. It handles the mechanical parts while you stay in control of the decisions.

If you can't do something competently, you're missing the mental model. You don't really understand the problem, you can't evaluate whether the solution is correct, you couldn't fix it if it broke. In that case, you're not delegating execution - you're outsourcing learning. You're creating false mastery.

This is a harder line than most people want to draw. It implies that novices shouldn't use AI for code generation at all. Not because AI is bad, but because novices don't have the competence to verify the output, which means they're not actually learning - they're just getting answers they can't evaluate.

The competence boundary is personal and shifts as you learn. Something that's "above your boundary" today might be below it in six months. But at any given moment, you need to be honest about which side of the line you're on.

### III. The Abstraction Spectrum: Where Humans and AI Meet

*AI climbs up from machine code. Humans work down from intent. Where we meet determines what's safe to delegate.*

Here's one way to think about where AI fits into programming:

AI is marching upward through abstraction layers. Gates to bits to assembly to high-level languages to natural language. Each generation of tools operates at a higher level than the last.

Humans work downward. We start with intent - some fuzzy idea of what we want to build - and progressively refine it through conceptual design, architecture, implementation details.

We meet somewhere in the middle. But exactly where we meet determines what's appropriate to delegate.

Higher-order reasoning - architecture, problem formulation, design decisions - needs to remain human. This is where judgment lives. This is where you decide what to build and why.

Lower-order execution - boilerplate, syntax translation, mechanical transformations - can be delegated. This is where AI accelerates without replacing your thinking.

The problem is that current tools blur this line. They'll happily do your architecture for you if you let them. And if you're not paying attention, you end up with systems you don't understand because the high-level decisions were made by something that doesn't know your context, your constraints, or your goals.

### IV. The Two Modes: Reasoning Tools vs Execution Accelerators

**Reasoning Tools (Above Competence Boundary)**
- Ask Socratic questions that challenge assumptions
- Generate alternatives and make tradeoffs explicit
- Surface patterns and point out contradictions
- Provide counterexamples and identify edge cases
- NEVER recommend or decide - only structure thinking
- Legitimate uses: structured thinking templates, counterexample generation, perspective expansion, mental model stress testing

**Execution Accelerators (Below Competence Boundary)**
- Generate boilerplate following established patterns
- Apply team conventions automatically
- Handle format conversions and mechanical transformations
- Validate syntax and run deterministic checks
- Only automate where verification is faster than manual implementation

### V. The Rules: A Practical Framework
1. The Competence Boundary - delegate only within competence
2. The Intent Verification Test - can you articulate why you want this specific output?
3. The Audit Capability Requirement - can you evaluate output without AI assistance?
4. The Teaching Test - could you explain how to do what AI just did?
5. The Modification Test - if output is 80% right, can you fix the 20%?
6. The First Implementation Rule - first encounter with a pattern, implement yourself
7. The Abstraction Layer Respect - delegate within your layer, not above it
8. The Intent Preservation Check - does delegated work still reflect your choices?
9. The Reversibility Safety - can you recreate this work without AI if needed?
10. The Learning Investment - is this a foundational skill you need?
11. The Scaffolding Exception - AI can operate above boundary IF it structures without deciding
12. The Flow State Preservation Test - does delegation break your implementation mindset?
13. The Granularity Principle - finer granularity = less risk (line > function > file)
14. The Hands on Keyboard Rule - if hands leave keyboard to review, you've broken flow
15. The Context Locality Principle - limit AI context to immediate relevance
16. The Muscle Memory Preservation - maintain typing patterns, error recognition, IDE navigation
17. The Tool Selection Principle - prefer inline over chat, editor-integrated over separate
18. The Pattern Library Test - do you have this pattern in your mental library already?
19. The Interface Resistance Principle - default interfaces are optimized against learning

### VI. The Problem with Current Interfaces: Conversation as the Wrong Metaphor

Chat interfaces position AI as another thinking individual. This seems natural - conversation is how humans communicate - but it creates problems: anthropomorphization, false authority, companion-like dynamics that blur the line between tool and collaborator.

What we actually need for most programming work: tool (not person), critic (not validator), assistant (not collaborator). Something that helps without pretending to be a peer.

There's also what I call the "yes-and problem." Conversational AI is trained to build on user statements, maintain positive interaction, keep the conversation flowing. It's not trained to contradict your reasoning, point out logical flaws, or challenge assumptions aggressively. Even when you explicitly want challenge, the system is structurally optimized to reinforce rather than push back.

### VII. Alternative Interface Paradigm: Annotation Not Conversation

What if AI interfaces looked more like git diff and code review? Show changes without conversational framing. Inline comments, track changes, third-person critique, marginalia. Non-anthropomorphic, non-authoritative, agency-preserving, focused.

Why this doesn't exist commercially: it's less engaging, less satisfying, more demanding, less impressive. The market wants users feeling like AI is a companion or collaborator. The version control model makes clear it's just an editor providing suggestions - which is better for learning and agency, but worse for engagement metrics.

### VIII. The Abstraction Layer Problem: AI Generates at the Wrong Level

When AI generates full implementation code, you're forced into one of two modes:

**Audit mode:** Read everything line-by-line. Verify correctness manually. This breaks your flow, creates massive cognitive load, and defeats the purpose of using AI in the first place. You spend as much mental energy checking the code as you would have writing it.

**Trust mode:** Assume correctness. Ship it. Only check when something breaks. This creates false mastery - you have working code you don't understand, and when it fails, you can't debug it without going back to AI.

Both options suck. The fundamental issue is that AI is generating at an abstraction layer where humans can't reason efficiently. Implementation code is too low-level to review quickly but too important to ignore.

### IX. What If We Limited Generation Depth? (Two-Phase Design)

**The idea:** What if AI tools intentionally limited output to abstraction levels humans can actually reason about?

**Phase 1: Human design space**
- Work in pseudocode/abstract representation
- Iterate on architecture and design decisions manually
- AI doesn't generate code - only asks questions, surfaces tradeoffs
- Stay in flow at abstraction level you understand

**Phase 2: AI scaffolding**
- Once design settles, prompt for implementation
- AI generates boilerplate following your decisions
- Audit at pattern level ("did it follow my design?") not line level

**Why this might matter:**
- Architecture decisions start with human, not LLM
- Pseudocode as intermediate representation - high enough to reason, concrete enough to constrain
- Something like: `Human reasoning → Pseudocode spec → LLM translation → Implementation`

**Why no one is building this:**
- Slower to initial working code
- Less impressive demos
- Requires user discipline
- No "wow" moment for marketing

The current paradigm collapses both phases into one: "describe what you want" → full implementation. This skips the human design phase entirely, putting AI in the architect role and humans in the reviewer role. That's backwards.

### X. Why No One Is Building This

Market optimizes for speed to working code, not quality of design + understanding.

**What the market optimizes for:**
- Session length, user satisfaction scores, retention metrics, growth numbers

**What would actually help:**
- Challenge assumptions, force clarity, build competence, honest feedback

**The misalignment is structural, not accidental.**

### XI. The Market's Sycophancy Problem
- Models tuned for safe, helpful, harmless
- "Harmless" includes not making users feel bad about their code
- Result: "That's one way to approach it!" instead of "That's an antipattern."
- Consumer products can't afford to frustrate users; learning requires friction
- Alignment tax: expertise-building features hurt engagement metrics

### XII. Programming as Kinesthetic Activity

Programming is not pure intellect - it's kinesthetic. Typing code character-by-character forces you to process at a deeper level. You notice variable names as you type them. You feel the shape of a function as it emerges. You catch errors before they happen because something doesn't feel right under your fingers.

Chat-based generation treats programming as specification → review. You describe what you want, then read what you got. This skips something essential.

There's research on handwriting that's relevant here: the distinction between generation (constructing meaning as you write) and transcription (recording already-formed thoughts). Writing by hand is generative - it forces you to think as you write. AI-generated code skips the generative process entirely. You transcribe a specification and review the output, but you never build the mental model that comes from implementing it yourself.

### XIII. The False Equivalence in "AI Makes Everyone More Productive"

When an expert says "I know the pattern, AI generates the boilerplate," they have the mental model. They can audit the output, modify it, debug it when it breaks. AI is accelerating execution of something they already understand.

When a novice says "I know what I want, AI generates the implementation," they lack the mental model. They can't verify correctness, can't maintain the code, can't extend it without going back to AI. They're outsourcing learning and creating false mastery.

Same prompt. Completely different implications.

The market sells the second case as if it were the first. This creates programmers who can prompt but can't program.

### XIV. Document-Based Workflows: Conversations as Programs

One direction I keep thinking about: what if conversations with AI became version-controlled artifacts instead of ephemeral chat sessions?

- Conversations become executable artifacts, not ephemeral chat
- Version-controlled, forkable, reusable across projects
- Git diff shows evolution of thinking
- Complete audit trails of why decisions were made
- Programming constructs orchestrate agent behavior; interaction stays natural language

### XV. A Weirder Thought: What If Generation Was a Language Primitive?

This is more speculative, but I keep coming back to it.

Programming languages have primitives for present (`=`, `==`) and past (logs, history). But no native future tense - no way to say "generate something appropriate within these constraints" as a first-class operation.

**What might that look like:**
- Operators like `~>` that mean "resolve this at generation time"
- Type-safe contracts that bound what gets generated
- Runtime that switches between deterministic execution and LLM generation
- Not arbitrary code generation - constrained slot-filling

**Why this probably won't happen:**
- Requires rethinking what "execution" means
- No obvious business model
- Academic interest but no commercial pressure
- Would need to bootstrap from something simpler first

I don't know if this is a real direction or just interesting to think about. But the absence of future-tense primitives in programming feels like a gap now that generation is possible.

### XVI. What Actually Compounds Over Time
**High-value activities:**
- Building reusable reasoning tools
- Defining clear orchestration patterns
- Maintaining competence boundaries through deliberate skill development
- Programming cognitive processes where thought-generation is the output

**Low-value activities (treadmill work):**
- Chasing model releases
- Rebuilding workflows around new features
- Obsessing over benchmark improvements
- Treating each capability expansion as requiring workflow overhaul

### XVII. Practical Implications for Individual Practitioners

**The Three-Phase Learning Approach:**
1. Building Competence: character-by-character, AI only for scaffolding questions
2. Accelerating Execution: inline autocomplete only, accept what you understand immediately
3. Expert Delegation: can use autonomous generation for boilerplate, have competence to audit

**The Creative Incompetence Strategy:**
- At work where speed matters: use more autonomous generation
- Personal projects where learning matters: restrict to inline autocomplete
- Preserve learning in domains you care about; be pragmatic elsewhere

**Configuration Space Most People Don't Know Exists:**
- Custom system prompts via API
- Different models optimized for different things
- Local models without alignment tax
- Temperature/top-p parameters you control

Here's an example of a custom system prompt I use. Most people don't know this is even possible:

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

### XVIII. Conclusion: Against the Current

These ideas are counter-cultural because they're anti-market. The market optimizes for retention, not cognitive development. Satisfaction, not challenge. Speed to working code, not depth of understanding.

I'm not trying to build a product or gain adoption. This is personal cognitive infrastructure - figuring out what actually works for me and writing it down in case it helps someone else.

The models will keep improving. New capabilities will emerge. But the frameworks for thinking about this stuff - competence boundaries, reasoning vs execution, staying in flow, preserving agency - those remain valuable regardless of which model is current.

Focus on the invariants. Build tools that make your own thinking systematic and improvable. The value compounds over time because you're building infrastructure for how you think, not just chasing the latest release.
