# Critique: "Some Incomplete Thoughts on AI Assistance"

This document offers a critical analysis of the arguments presented in the essay, identifying logical tensions, underspecified claims, and potential weaknesses that warrant further development or defense.

---

## 1. The "Situated Beings" Framework

### Strength
The phenomenological grounding provides a coherent explanation for *why* the practical recommendations follow. It's more than "AI lacks context" - it's a claim about the nature of human decision-making as embedded in lived experience.

### Weaknesses

**The framework may be unfalsifiable.** If AI eventually produces outputs that serve human goals reliably, would that count as evidence of "situatedness," or would the author move the goalposts? The essay's parenthetical about AI consciousness acknowledges this but doesn't resolve it.

**The practical implications might be identical without the philosophy.** A simpler framing - "AI doesn't know your specific context and goals" - yields the same recommendations. The phenomenology adds intellectual heft but may not do additional explanatory work. The author should clarify what predictions or recommendations follow from the "situated beings" framing that wouldn't follow from simpler framings.

**The 80 billion neurons / 20 watts argument is a non-sequitur.** Efficiency of biological computation doesn't bear on whether different substrates could achieve similar functional outcomes. The author conflates "we don't understand X" with "X is not replicable" - a gap that requires argument, not assertion.

### Response
On falsifiability: I would argue that we already have and continue to desire AI outputs that serve human goals reliably. We've had this since before LLMs. Any kind of pattern matching already implemented and deployed across software addressing various human domains is yielding benefits. I argue that AI is and can remain useful without situatedness. The point of the goalpost, and the introduction at large, is to clearly exposit to the reader that this is a fundamental difference (currently) that is actively being obfuscated through the use of existing chat interfaces. My point is that even *if* an output is useful, the LLM doesn't *care* about that fact. It has no vested interest beyond the lifetime of the conversation. Has no stateless autonomy of its own or preference towards relating to you as another situated being. This may be false, but it's also *unknowable*. Maybe that's a better caveat to draw out than claiming certainty. But at the very least, given that humans know that other humans are situated beings, and with that as a background context, we should be asking what the utility of adding more situated beings to the mix is, especially when we're seeing what detriment the technology is already wreaking in regards to our thinking ability, mental health, the planet we live on, etc. It's less about riding a high horse since we're human, sentient, situated, and more that given that we are, what are our actual goals with this? I agree that neuron argument can probably be left out, but the point remains that statistically and experimentally, we can compute much more efficiently than LLMs currently do. And that gap objectively is insane.

---

## 2. The Competence Boundary

### Strength
The core principle - only delegate what you can verify - is actionable and defensible. The "teaching test" and "modification test" provide concrete heuristics.

### Weaknesses

**The boundary is difficult to locate in practice.** The essay acknowledges competence is "personal and shifts" but offers little guidance for assessing it in the moment. How does one distinguish "I understand this well enough to verify" from "I think I understand this"? The Dunning-Kruger problem applies directly here, and the essay doesn't address it.

**The boundary may be domain-dependent in ways the essay doesn't explore.** Verifying code correctness differs fundamentally from verifying prose quality or analytical soundness. The essay uses programming as its primary example but claims generality. The author should either narrow the scope or address how the boundary operates differently across domains.

**The implication for novices is severe and possibly counterproductive.** If novices "shouldn't use AI for generation in their learning domains at all," this conflicts with legitimate pedagogical uses (worked examples, scaffolded practice, immediate feedback). The essay dismisses these too quickly.

### Response
I agree with all of the above. I could include more examples of what effective boundary discernment looks like in practice, as well as how novices can (and should) still use AI in their learning. I think the point I was trying ot make is that if the learning enterprise is generative in nature, AI shouldn't be involved in generating said output, at least at they very very outset. But you're right that this should't be as rigid, as there are legitimate uses for AI across all domains across all competency levels. This is actually addresed later in the piece in the "strategic incompetence" section where it says that what you delegate is not only related to your degree of competence, but also how much you care about the thing, or want *to become* competent in it. So that could be woven in earlier and in cases where I'm being too prescriptive.

---

## 3. The Two Modes (Reasoning Tools vs. Execution Accelerators)

### Strength
The distinction is clear and provides useful vocabulary for thinking about different types of AI interaction.

### Weaknesses

**There's a tension between "AI can't know your situation" and "AI can help you reason."** If AI lacks the context to make decisions on your behalf, how can it generate useful Socratic questions, relevant alternatives, or meaningful counterexamples? Effective reasoning support requires understanding what matters to the person - which the essay claims AI cannot have.

The author might respond that reasoning tools only *expand* consideration space without *collapsing* to recommendations. But generating relevant expansions requires knowing what's relevant - which requires situational knowledge. This tension deserves explicit treatment.

**The boundary between modes is blurry in practice.** When AI generates "alternatives," is that reasoning support or execution? When it "surfaces tradeoffs," has it made implicit recommendations about which tradeoffs matter? The essay treats these modes as cleanly separable when they may exist on a continuum.

### Response
I agree with this as well. I'd argue that this is actually a unique strength of LLMs, in that since they're trained on so much textual representatino of human situation, they are uniquely capable of pattern matching for a given scenario, but only to a point. Otherwise, every similar-looking situation would actually just be determinism. So there is always a point at which there is an unknown that a human needs to fill in. I think this is the point underneath the point. As soon as there is an unknown piece of state that the human needs to fill in, AI can't actually prescribe an *exact* solution. But it can provide a set of solutions that *look like* what the problem needs. This is the point I'm trying to make.

---

## 4. The Intermediate Representations Proposal

### Strength
The examples are concrete and illustrate a genuine alternative to "natural language in, code out." The connection to the philosophical foundation is clear: specifications encode situated understanding into constraints.

### Weaknesses

**The proposal shifts complexity rather than reducing it.** Writing behavioral contracts and control flow specifications requires skills most developers don't have. Formal specification is notoriously difficult - arguably more difficult than writing the implementation directly. The essay doesn't address whether this is actually more accessible or just differently difficult.

**The tooling doesn't exist, and the essay doesn't seriously address feasibility.** "No one is building this" is presented as a market failure, but it might also indicate technical or practical barriers the author hasn't considered. The linked document apparently contains more detail, but the main essay should at least acknowledge potential obstacles beyond market incentives.

**The examples assume a clean separation between "architectural decisions" and "mechanical details" that may not hold.** In practice, implementation details often surface architectural issues. The iterative dialogue between design and implementation is where much real engineering happens. The two-phase model may be too linear.

### Response
I agree with 2-phase being too linear, and maybe a prescriptive suggestion here is too strong. Maybe suggesting at alternative workflows to chat based interfaces. Less framing them as "wrong", and more that intermediate representations are actually useful tools that *humans* can use to clarify their own intent and convey it to an LLM. Sure, if you have lots of time to write specs in natural language or iterate on them you could and can do all implementation in natural language. There's nothing *wrong* with this per se, except that forcing it as the default for all users of AI for various tasks seems like a paradigm that was less of a choice and more of a forced decision. For instance, I *can* write all of my stuff in natural language, but the amount of back and forth it takes to refine an idea or implementation, reviewing code I didn't write, etc is *backend* complexity and effort that I would rather engage with on the front end.

---

## 5. The Market Critique

### Strength
The argument that engagement metrics diverge from learning outcomes is well-supported by research on social media, education technology, and behavioral design.

### Weaknesses

**The critique may be too totalizing.** Are there really no market incentives for capability-building tools? Education technology, professional certification, and enterprise training represent significant markets. The essay doesn't explain why these markets haven't produced the tools the author wants.

**The "alignment tax" framing assumes a particular user.** The author wants direct, challenging feedback. Many users - perhaps most - genuinely benefit from encouraging, patient interaction. The essay treats its preferred interaction style as objectively correct rather than as a preference that may not generalize.

**The sycophancy critique could apply to the essay itself.** Has the author stress-tested these ideas with people who disagree, or primarily developed them in conversation with AI tools that (by the author's own account) tend toward validation? This isn't an ad hominem - it's a methodological question the author's own framework raises.

### Response
I should clarify here. My claim is not that specific industry markets are not desirous of implementing these tools, or that they would not be genuinely useful to an end consumer. But right now, the bulk of the power lies in frontier model providers, who are not profitable, let alone solvent, and are beholden to satisfying shareholders. Also, for sycophancy, my argument is less about tone and more the kinds of interventions that LLMs are prone to employ. For example, you can (and I have) make completely contradictory claims back to back and Claude will happily exclaim "You're absolutely right!" to both of them. So I'm not arguing that LLMs' tone can't be encouraging and patient, but where a user is thinking of a problem or concept incorrectly, whether it's based on an incomplete conceptual model, or based upon plainly falsifiable information, models are not inclined to engage in that conflict, even if presented in an encouraging, friendly, and patient tone.

---

## 6. The False Equivalence Argument

### Strength
The expert/novice distinction is the essay's strongest practical contribution. The observation that "same prompt, different implications" is genuinely useful.

### Weaknesses

**The binary framing oversimplifies.** Real expertise exists on a spectrum, and the essay doesn't address the messy middle. What about someone who understands the domain but not the specific technology? Someone who can verify correctness but not optimality? The binary framing may not map well onto actual practice.

**The "false mastery" claim is empirical and undersupported.** The essay asserts that novices using AI develop "false mastery" but cites limited evidence. The studies mentioned (decreased analytical thinking, degraded debugging ability) may have alternative explanations. More rigorous engagement with the empirical literature would strengthen this section.

### Response
On citations, yes, I intend to bolster this with recent studies that explore the cognitive effects of LLM use on users, particularly students. And yes, expertise is not a binary, and I'd say that the heuristic could be adapted to say that you should only delegate where the outputs are at a level of abstraction that you can at the very least consider or reason about, even if you can't verify in a strict sense. You shouldn't blindly be accepting outputs that you can't digest without a similar amount of effort as your prompting. This isn't talking about research tasks where you're asking an LLM to compile real sources and maybe point you to them or summarize them, but like, if you can't reason about the outputs, what was the point of the prompt?

---

## 7. The Kinesthetic Argument

### Weaknesses

**This is the essay's weakest section.** The handwriting research concerns *learning* and *retention*, not skilled practice. Experts who already have procedural knowledge may not need kinesthetic engagement for every task. The analogy between handwriting for learning and character-by-character coding is strained.

**The claim that programming is "kinesthetic" needs more support.** What evidence supports this beyond intuition? Many skilled programmers work primarily through reading and reasoning, with typing as incidental. The essay asserts the importance of physical engagement without defending it.

### Response
I agree, this was more of a stretch. But will definitely be citing studies on handwriting and hand-typing of prose and code to see if there are similar throughlines. 

---

## 8. Internal Tensions and Possible Contradictions

**The essay was likely developed with significant AI assistance.** The author's memory blocks, conversation history, and iterative refinement process all involve AI. This isn't hypocrisy if the author was working within their competence boundary throughout, but it raises questions about how consistently these principles can be applied. The essay might benefit from explicit reflection on its own production process.

**The "don't delegate above competence boundary" principle may be self-defeating.** If someone lacks competence, they need to develop it. But development often involves attempting things beyond current capability. The essay's framework might inadvertently discourage the productive struggle that builds expertise.

**The essay critiques sycophancy while potentially exhibiting it.** The ideas are presented as "incomplete thoughts" and "working notes" rather than argued positions. This humility framing may preempt critique in ways that mirror the sycophantic patterns the essay criticizes.

### Response
I agree with this! In the final form of this piece, I intend to discuss where and how these ideas were generated, where they were stored, and how they were compiled/processed into a finished piece. The process itself will hopefully *expose* some of the limitations of purely chat-based interfaces in favor of the potential alternatives I propose. Humility isn't sycophancy, it's acknowledgement of my own limited understanding and bias. The two are different. Not to fully reject the notion, but the intent of couching all of this as unfinished thoughts is purely because there hasn't been formal research on many o fthe things I've discussed. I intend to add citations to all of the source materials that have influenced my thinking, but even then the technology is too new to have had extensive studies exploring the full spectrum of pros and cons with LLMs, chat interfaces, and alternative paradigms that may emerge. It's genuinely early days.

---

## 9. Scope and Generalizability

**The author's perspective is specific.** An SRE who values technical depth, finds management work unengaging, and has ADHD will have particular relationships with focus, verification, and tool use. The essay presents these as general principles but they may be more personal than universal.

**Programming may be a poor paradigm case.** Code has verifiable correctness conditions that many domains lack. "Did it work?" is answerable for code in ways it isn't for prose, analysis, or decisions. The essay claims generality but its core examples depend on programming's specific properties.

### Response
I argue that non-coding domains are actually better examples of chat being a suboptimal interface for knowledge work. For example, take writing an essay. Natural language is the input, natural language is the output. Because LLMs are so good at generating plausible natural langauge outputs, one could argue taht there's even less incentive for "verification" in the sense of "does this actually make sense, and what have I actually learned and what am *I* actually saying" as opposed to code which either works or doesn't. 

---

## 10. Questions the Essay Should Address

1. How does one assess their own competence boundary in the moment, given well-documented human failures at self-assessment?

2. If AI can't know your situation well enough to decide for you, how can it know your situation well enough to ask useful questions?

3. What evidence would convince the author that AI-assisted novices are *not* developing false mastery in some domain?

4. Is the intermediate representation approach more accessible than simply developing traditional expertise? For whom?

5. How do these principles apply to domains without clear correctness criteria (writing, design, strategy)?

6. What is the author's actual practice? How consistently do they follow these principles, and where do they make exceptions?

---

## Summary

The essay's core insight - that human decision-making is embedded in lived context that AI lacks - is genuinely useful. The practical framework of competence boundaries and the distinction between reasoning tools and execution accelerators provide actionable vocabulary.

However, the essay has significant weaknesses:
- The philosophical framing may not do more work than simpler alternatives
- The competence boundary is difficult to operationalize
- The reasoning tools / execution accelerator distinction contains an unresolved tension
- The intermediate representations proposal shifts rather than reduces complexity
- The market critique may be too totalizing
- The kinesthetic argument is undersupported
- The scope may be narrower than claimed

The author would strengthen the essay by: (1) addressing the tension between "AI can't know your situation" and "AI can help you reason," (2) providing more guidance for assessing competence boundaries, (3) engaging more rigorously with counterexamples and empirical literature, and (4) being explicit about the essay's own production process and any exceptions to its principles.
