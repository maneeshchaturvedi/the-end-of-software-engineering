---
layout: default
title: "Chapter 13: Human Training Data vs Human Output"
---

# Part IV: The Garbage In, Governance Out Paradox

*Why AI trained on human mess still changes everything*

---

# Chapter 13: Human Training Data vs Human Output

Dr. Yuki Tanaka had spent twenty-three years writing code, the last eight as principal architect at a cybersecurity company. When her company's CTO announced in June 2024 that they'd be piloting AI-assisted development, Yuki's objection was immediate and well-articulated.

"This is trained on Stack Overflow and GitHub," she said in the architecture review meeting, pulling up examples on the screen. "You know what's on Stack Overflow? Copy-pasted solutions from people who barely understand the problem. Outdated patterns. Security vulnerabilities marked as 'accepted answers' because they worked once in 2014. And GitHub? Half of it is abandoned homework projects and tutorial code written by students learning to code."

She clicked through a presentation she'd prepared. Example after example of terrible code that AI models had likely ingested as training data. SQL injection vulnerabilities with 2,000 upvotes. Authentication bypasses in popular repositories. Race conditions in concurrent code that 500 developers had starred.

"Garbage in, garbage out," Yuki concluded. "We're talking about adopting a system that learned to write code from the collective mistakes of millions of developers over decades. And you want to use it in a *cybersecurity* company, where code quality literally determines whether our customers get breached?"

The CTO, Maria Chen, nodded. "You're right about the training data. But I want you to lead the pilot evaluation. Six weeks. You design the tests. You set the standards. If the AI produces the garbage you're predicting, we kill the experiment."

Yuki agreed, confident she'd be proven right within days.

Six weeks later, she was presenting very different findings than she'd expected. But it had taken a specific incident—and a humbling realization about her own code—to change her mind.

---

AI models are indeed trained on human-written code, and human-written code is famously messy. Inconsistent style. Copy-pasted logic. Clever hacks that made sense at 2 AM but are incomprehensible in daylight. Edge cases handled differently in different files. Comments that contradict the code. Code that contradicts the documentation.

If AI learns from this mess, won't it just produce more mess? And at 10-50x speed, won't it produce mess at a scale that makes our current technical debt look quaint?

This is the "garbage in, garbage out" argument, and it's the most sophisticated objection to AI-accelerated development. It acknowledges that AI is fast and consistent, but argues that *what* it's being fast and consistent *at* is producing garbage based on garbage training data.

The argument feels compelling. Yuki certainly found it compelling. It's also wrong—but not for the reasons most people think.

## The Mess in Human Brains

Before we examine the mess in AI training data, let's examine the mess in the system AI is replacing: human brains writing code.

Consider what's actually happening when a human developer writes code:

**Memory errors**: The developer remembers that they solved something similar six months ago, but can't quite recall the details. They reconstruct the solution from fuzzy memory, getting some details right and others wrong.

**Fatigue effects**: It's 4 PM on Friday. The developer is tired. They take mental shortcuts. They skip edge cases. They write the obvious solution rather than the correct one.

**Knowledge gaps**: The developer doesn't fully understand the library they're using. They copy an example from the documentation, modify it to fit their use case, and hope it works. They don't understand *why* it works—or doesn't.

**Ego dynamics**: The developer wrote the original version of this code three years ago. They're emotionally attached to the approach. When a better pattern emerges, they resist it because admitting the old approach was wrong feels like admitting *they* were wrong.

**Political pressure**: The developer's manager wants this feature shipped by end of quarter. The developer knows the right way to do it would take longer. They do it the quick way, creating technical debt they'll have to explain later.

**Context switching**: The developer was interrupted four times while writing this function. Each time they returned, they partially forgot where they were. The function is slightly incoherent because it reflects four different mental states.

**Mood effects**: The developer had a fight with their partner this morning. They're distracted. Irritable. They write terse variable names and skip documentation because writing words feels effortful right now.

**Skill variation**: The developer learned Java in 2008. They're writing Python now but thinking in Java patterns. The code works but feels foreign to developers who learned Python natively.

This is the system that produced the training data. Messy code written by inconsistent humans operating under cognitive constraints, political pressure, emotional states, and knowledge gaps.

But here's what's crucial: this is also the system that AI is *replacing*.

## Two Types of Mess

The "garbage in, garbage out" argument assumes all garbage is equivalent. It's not.

There are two fundamentally different types of errors:

**Statistically patterned errors**: Mistakes that emerge from consistent misunderstandings or systematic gaps. If an AI model consistently makes a certain category of error—say, forgetting to handle null checks in a specific context—that error appears in predictable patterns.

**Chaotically variable errors**: Mistakes that emerge from random factors—fatigue, distraction, ego, mood, interruptions. A human developer makes different mistakes on Tuesday morning than Friday afternoon. The pattern of errors is essentially random.

AI trained on messy human code produces the first type. Humans writing code produce the second type.

The difference is everything.

## Why Patterns Can Be Fixed

Consider a manufacturing analogy. Early 20th-century factory production had a quality problem. Machines produced defects. Critics pointed out—correctly—that machine-made goods had imperfections that skilled artisans would never produce.

What happened? Did we go back to artisanal production?

No. We built better machines. We added quality control processes. We developed statistical process control to detect when machines were producing defective output. We created feedback loops that adjusted machine parameters in real-time.

Crucially, this worked *because machine errors were patterned*. If a machine was cutting parts 0.5mm too short, you could measure that, identify the systematic error, and correct it. The next thousand parts would be correct.

Try the same with a human artisan. On Monday they cut parts perfectly. On Tuesday they're distracted and cut some long, some short, some crooked. Wednesday they're in a bad mood and rush through the work. The error pattern is chaotic. You can't systematically correct it because there's no consistent pattern to correct.

The same dynamic applies to code.

If an AI model consistently forgets to validate user input before database queries, you can add automated static analysis that flags every instance, create linting rules that catch the pattern, build test templates that verify input validation, generate warnings at code review time, and track the pattern to fine-tune the model and reduce its occurrence.

If a human developer makes unpredictable mistakes—sometimes forgetting input validation, sometimes handling it incorrectly, sometimes over-engineering it, the pattern depending on their fatigue level, mood, recent experiences, and political pressure—you can't systematically fix it. You need another human to review every change, and that human is subject to the same chaotic variability.

## The Compressibility Insight

There's a mathematical way to think about this: error compressibility.

Errors that follow patterns can be compressed. If an AI makes the same category of mistake repeatedly, you can write a rule that catches all instances. That rule is a compressed representation of potentially thousands of errors.

Errors that are chaotically random cannot be compressed. If every error is unique—emerging from the specific intersection of a developer's knowledge gaps, emotional state, political pressure, and recent context switches—you can't write a rule to catch them. Each error requires individual human judgment to identify and fix.

In information theory terms, patterned errors have low Kolmogorov complexity. Random errors have high Kolmogorov complexity. Low complexity errors can be systematically prevented. High complexity errors cannot.

AI produces low-complexity errors. Humans produce high-complexity errors.

This is why AI-generated code, despite being trained on messy data, becomes *easier* to govern than human code.

## The Empirical Data

*[Data from Yuki Tanaka's six-week pilot evaluation at cybersecurity company, July-August 2024]*

Yuki designed her pilot evaluation to be unforgiving. She had her team build the same set of security-critical features twice: once with traditional human-only development, once with AI assistance. She then conducted exhaustive security reviews of both code sets, tracking every vulnerability, every deviation from best practices, every potential weakness.

The first week's results seemed to confirm her fears:

**Human-generated code** (first week):
- Security vulnerabilities found: 3 per 1000 lines
- Error categories: 28 distinct vulnerability types
- Pattern predictability: Low—each developer made different security mistakes
- Time to identify root cause during review: 52 minutes average
- Ability to prevent recurrence: Low—education helped but couldn't prevent fatigue-based errors

**AI-generated code** (first week):
- Security vulnerabilities found: 4.2 per 1000 lines (40% more vulnerabilities!)
- Error categories: 9 distinct vulnerability types
- Pattern predictability: High—the same types appeared consistently
- Time to identify root cause during review: 11 minutes average
- Ability to prevent recurrence: Unknown (to be tested)

"See?" Yuki told Maria after week one. "AI-generated code has more security holes. This is exactly what I predicted—it learned from insecure training data."

But Maria pushed back. "Look at the error categories. AI made nine types of mistakes. Humans made twenty-eight types. Which is easier to fix systematically?"

Yuki spent week two building automated security checks for the nine patterns the AI consistently exhibited. Static analysis rules for the specific injection vulnerabilities it missed. Automated tests for the specific authentication patterns it got wrong. Linting rules for the specific cryptographic mistakes it made.

Then she had the team generate new AI-assisted code with these checks in place.

**AI-generated code** (weeks 3-6, with automated checks):
- Security vulnerabilities found: 0.7 per 1000 lines (83% reduction from week one)
- All vulnerabilities caught by automated tools before human review
- Human review time: Mostly focused on business logic, not hunting for common mistakes

Meanwhile, human-generated code continued to have vulnerabilities because each developer made *different* security mistakes that automated tools couldn't predict:

**Human-generated code** (weeks 3-6):
- Security vulnerabilities found: 2.6 per 1000 lines (modest improvement from more careful code reviews)
- Still required extensive human security review because the error patterns were unpredictable

Yuki stared at the data. The AI code, trained on "garbage" from Stack Overflow and GitHub, had become *more secure* than human-written code once she added systematic checks for its predictable weaknesses. Meanwhile, human code—written by expert security engineers—remained stubbornly vulnerable to unpredictable mistakes that no amount of automated checking could catch.

The AI had learned from messy training data. But because its errors were patterned, they were fixable. Human expertise was inconsistently applied—brilliant insights mixed with fatigue-induced mistakes—and therefore ungovernable.

The AI code became higher quality than human code not because AI is inherently better, but because AI errors could be systematically eliminated while human errors could not.

---

Yuki spent the weekend before her final presentation staring at spreadsheets, trying to find a flaw in her methodology. There had to be something wrong with the data. Some confounding variable. Some bias in how she'd selected test cases or measured vulnerabilities.

She'd been so confident six weeks ago. Standing in front of the architecture review meeting with her carefully prepared slides showing insecure Stack Overflow answers and vulnerable GitHub repositories. "Garbage in, garbage out," she'd said, and everyone had nodded because it was obviously true.

Now she had to go back to that same room and tell them she'd been wrong.

Not partially wrong. Not "it's more complicated than I thought" wrong. Fundamentally, architecturally wrong about how the world worked.

Sunday night, she gave up looking for flaws in her analysis. The data was solid. The AI-generated code, trained on the collective mistakes of millions of developers, had become *more secure* than code written by her team of expert security engineers. The implications terrified her almost as much as admitting she'd been wrong.

## The Presentation

Monday morning, August 26, 2024. The same conference room. The same people who'd heard her confident "garbage in, garbage out" argument six weeks earlier.

Yuki stood at the front of the room, her first slide showing the week one results: AI-generated code with 40% more vulnerabilities than human code.

"Six weeks ago, I predicted this," she began. "I told you that AI trained on Stack Overflow and GitHub would produce insecure code because it learned from insecure training data. Week one confirmed my prediction. AI code had 4.2 security vulnerabilities per thousand lines compared to 3.0 for human code."

She clicked to the next slide. Week six results: 0.7 vulnerabilities per thousand lines for AI, 2.6 for humans.

"By week six, I'd been proven completely wrong. Not about the training data being messy—that part was accurate. But about what that mess actually meant."

She walked through the analysis. The nine vulnerability types the AI consistently exhibited versus the twenty-eight types from human developers. The automated security checks she'd built to catch the nine patterns. The 83% reduction in AI vulnerabilities once those checks were in place.

Then she got to the part that had kept her up at night.

## The Paradox

"Here's what I didn't understand," Yuki said, pulling up her training data examples—the same insecure Stack Overflow answers she'd shown in week one. "Yes, AI is trained on messy human code. Decades of collective mistakes are in that training data. I was right about that."

She paused, choosing her words carefully.

"But the mess in the training data is actually *less problematic* than the mess in human cognition."

She saw skeptical faces. This was the hard part.

"The training data captures statistical patterns. Patterns of good code and patterns of bad code. But it doesn't capture individual fatigue. Personal ego dynamics. Political pressure in specific organizations. Mood variations. Context-switching effects. Memory degradation."

She clicked to a new slide showing two code samples—both with SQL injection vulnerabilities, but written by different developers on her team, in completely different styles.

"When a human developer writes insecure code, they do it because they're tired, or distracted, or rushed, or they forgot that one time three months ago when they got input validation right. The errors are chaotically random. When our developer Sarah writes authentication code on Monday morning, it's different from when she writes it Friday afternoon. Different from when Tom writes it. Different from when I write it."

Another click. A series of AI-generated code samples, all exhibiting the same type of parameterization error.

"When AI writes insecure code, it does it *consistently*. Same pattern, every time. That's bad—until you build automated checking. Then the consistency becomes an advantage. The scanner catches every single instance. You fix it once, systematically, and the pattern stops appearing."

Marcus, one of the senior engineers, raised his hand. "But what if the AI learned *wrong patterns* from the training data? What if it thinks SQL injection vulnerabilities are normal because they appeared so frequently in Stack Overflow answers?"

## The Objection

Yuki nodded. She'd anticipated this. It was the sophisticated version of her original argument.

"That's a real concern," she said. "AI models do learn problematic patterns from training data. If insecure code appears frequently in the training corpus, the model will generate similar insecure code."

She pulled up a new slide. "But consider: where do human developers learn patterns from?"

A list appeared:
- Stack Overflow
- GitHub
- Documentation
- Tutorials
- Organizational legacy code written before modern security practices
- Pressure from managers who don't understand security
- Time constraints that force shortcuts
- Insufficient training in security fundamentals
- Ego investment in approaches that worked in the past

"We learn from the same messy sources—plus additional sources of wrong patterns. And we apply what we learn *inconsistently*. I reviewed Sarah's code from the past six months. Sometimes she sanitizes inputs perfectly. Sometimes she forgets entirely. Sometimes she over-engineers the validation. There's no pattern I can write a rule to catch."

Yuki clicked to her pilot data. "The AI applies patterns consistently. When it learned an insecure pattern from training data, it applied that pattern *every time* in similar contexts. So when I added automated security scanning for those specific patterns, the scanner caught every instance. The insecure pattern stopped appearing in production."

She pulled up the human code review data. "With human code, scanners catch *some* instances—the ones where the developer made that specific mistake. Other instances slip through because that developer happened to remember security that day, or handled it differently because of different context."

The room was quiet. She could see people processing this, resisting it, the same way she'd resisted it for the first four weeks of the pilot.

## The Governance Insight

Yuki moved to her next slide: "The Counterintuitive Conclusion."

"This leads somewhere I didn't expect," she said. "It's actually easier to govern AI-generated code than human-generated code, even though AI is trained on messy human code."

She could see Maria, the CTO, leaning forward. This was the part that mattered for the business decision.

"Governing human code requires extensive manual review because the errors are unpredictable. We need multiple review stages—architecture, security, performance. Senior engineer oversight, which doesn't scale. And even with all that, we're still hoping that reviewers catch what developers missed. Our code review process takes an average of 3.2 hours per pull request, and vulnerabilities still slip through."

New slide: governance metrics.

"Governing AI code can use automated static analysis because the errors are patterned. We run pattern-based security scanning that catches every instance of the nine vulnerability types we identified. Consistent enforcement with no human variability. And here's the key part—systematic feedback to improve the model."

She clicked to a flowchart showing the meta-learning loop she'd discovered in week four.

"When we detect that the AI is making a systematic error—say, forgetting to close database connections in async functions—we can add automated checks that catch this pattern, collect examples of the error and the corrections, and those corrections feed back into the model's training. The model learns. The error rate drops."

Yuki paused. "You can't do this with human developers. Not really. We can teach people, but they forget when they're tired or distracted. They vary in how they apply lessons. Some resist feedback due to ego. They make different errors under different conditions. And learning doesn't transfer systematically across all developers."

She showed the data: governance cost per thousand lines of code. Human review: 2.4 hours. Automated AI governance: 0.08 hours.

"The governance cost drops by orders of magnitude because we're governing predictable patterns rather than unpredictable human behavior."

## The Fundamental Asymmetry

Yuki advanced to her final technical slide. This was the insight that had changed everything for her.

"The fundamental asymmetry," she said, "is this: human variability creates ungovernable chaos. AI consistency creates governable patterns."

She listed the characteristics side by side:

**Human code:**
- Different developers, different approaches
- Same developer, different output based on fatigue, mood, pressure
- No systematic way to ensure consistency
- Review catches some errors but not all
- Quality depends on the weakest link on the worst day

**AI code:**
- Same model, same patterns
- Errors are systematic and detectable
- Automated governance catches all instances
- Quality improves through systematic feedback
- Meta-learning creates continuous improvement

"Yes, AI is trained on garbage," Yuki said, and she could hear the echo of her own words from six weeks ago. "But it produces *systematic* garbage that can be systematically eliminated. Humans produce *chaotic* garbage that cannot be systematically fixed."

She paused, letting that sink in.

"This isn't a small difference. It's the difference between a problem that gets worse at scale—chaotic human variability—and a problem that gets better at scale—systematic pattern detection and correction. When we write more human code, we get more unpredictable errors. When the AI generates more code with automated governance, the error rate actually *drops* because we're catching and eliminating patterns faster than new ones emerge."

## The Recommendation

Maria raised her hand. "So what's your recommendation? Full adoption?"

Yuki shook her head. "My recommendation is conditional. The legitimate concern isn't 'garbage in, garbage out.' The real concern is: what if we don't build the governance systems to catch AI's systematic errors?"

She clicked to her final slide: "Requirements for Safe AI Acceleration."

"If we use AI to accelerate development without building proper governance infrastructure, then yes, we'll amplify errors at scale. We need:

- Automated static analysis tuned to catch the specific patterns this AI exhibits
- Pattern-based security scanning integrated into every deployment
- Continuous integration with comprehensive test coverage
- Automated compliance checking for our security standards
- Systematic feedback loops that improve the model over time"

Yuki looked around the room. "Without these systems, AI acceleration is dangerous. But here's the key insight: organizations that fail to govern AI effectively are *already* struggling to govern human code. We are. Our current code review process misses vulnerabilities regularly. The difference is that AI gives us the *option* of systematic governance. Human variability makes systematic governance impossible."

She advanced to a cost comparison. "Building this governance infrastructure will cost approximately $180,000 in engineering time and tools. But it will reduce our ongoing code review overhead by 70%—saving roughly $400,000 per year. And it will catch vulnerabilities that our current human review process misses."

"So your recommendation is yes?" Maria asked.

"My recommendation is yes—with the governance investment. Without it, absolutely not."

The room was quiet for a moment. Then Marcus spoke up again. "This feels like a big leap of faith. We're betting our security posture on machines learning from garbage."

Yuki nodded. "I felt the same way six weeks ago. But I've been reading about manufacturing history. In the early 1900s, critics of factory production made exactly the same argument. They said machines produced inferior goods because they were designed based on hand production, which included all the imperfections of human artisans."

She pulled up a quote from a 1910 article by a furniture makers' guild, arguing against machine manufacturing.

"They were right that machine-made goods initially had quality issues. But they were wrong that this meant machines would always be inferior. What happened was that machines' *consistent* imperfections enabled systematic quality improvement. Statistical process control. Feedback loops. Continuous improvement. Within decades, machine-made goods exceeded artisanal quality—not because machines started perfect, but because their consistency enabled systematic improvement."

Yuki closed her laptop. "We're at the same inflection point with code. AI-generated code has quality issues right now. But its consistency enables systematic quality improvement that chaotically variable human code never allowed."

She looked directly at Marcus. "The 'garbage in, garbage out' argument—my argument from six weeks ago—mistakes a temporary implementation detail for a fundamental limitation. Current AI models, trained on current data, with current governance systems. All of that can improve. The fundamental question is: which is easier to govern at scale? Consistent patterns or chaotic variability?"

"And you're saying patterns," Maria said.

"The data says patterns," Yuki replied. "I'm just finally listening to it."

---

## Six Months Later

*[Composite outcome based on cybersecurity company implementations observed in late 2024]*

By February 2025, Yuki's role had changed significantly. She was no longer writing much code herself. Instead, she led the AI Governance Architecture team—a new group responsible for building and maintaining the automated security infrastructure that governed AI-generated code.

The transformation had been remarkable. The company's deployment frequency had increased from 2-3 releases per week to 15-20 per day. Code review time had dropped from 3.2 hours per pull request to 0.4 hours—mostly focused on business logic validation rather than hunting for security bugs. Security vulnerabilities in production had decreased by 71%.

But what surprised Yuki most was how the work felt different. When she'd been compensating for human inconsistency—reviewing code for the security mistakes that developers made when they were tired or rushed—it had felt like an endless, losing battle. There was always another edge case, another moment of fatigue, another political pressure causing a shortcut.

Now she was building systems that caught patterns. The work was cumulative. Each rule she wrote caught not just one bug, but every instance of that bug pattern, forever. The error rate declined over time rather than staying constant.

Her team had grown from just her to five engineers. They'd identified 47 distinct vulnerability patterns in the AI's output and built automated detection for all of them. The AI's base error rate had improved too, as the model was fine-tuned on corrections. New patterns still emerged occasionally, but at a decreasing rate.

The "garbage in, garbage out" argument had been wrong, but not in the way Yuki initially thought. The AI had indeed learned from garbage training data. But it had turned out that systematic garbage was easier to clean up than chaotic brilliance mixed with unpredictable human error.

The real garbage, she'd realized, was the mess in human cognition—the fatigue, the ego, the politics, the inconsistency. AI had learned from human code, but it hadn't learned to be human. And in a strange way, that was exactly what made it governable.

---

## Key Takeaways

- **Two types of errors**: Statistically patterned errors (AI) vs chaotically variable errors (humans)
- **Dr. Yuki Tanaka's transformation**: From confident "garbage in, garbage out" skeptic to discovering AI errors are more governable than human errors
- **The pilot data**: AI initially had 40% more vulnerabilities (4.2 vs 3.0 per 1000 lines), but dropped to 83% fewer (0.7 vs 2.6) with systematic governance
- **Patterns can be systematically corrected**: AI's 9 consistent error types vs humans' 28 unpredictable types—consistency enables automated detection
- **Chaos cannot be systematically corrected**: Human variability (fatigue, ego, politics, mood) requires expensive, inconsistent human review
- **Error compressibility**: Low-complexity (patterned) errors are governable; high-complexity (random) errors are not
- **The paradox**: AI trained on messy data produces more governable code than humans, because patterns beat chaos
- **Meta-learning loops**: AI can systematically learn from corrections; humans cannot due to variability
- **Governance cost**: Drops from 2.4 hours to 0.08 hours per 1000 lines—orders of magnitude reduction
- **The real concern**: Not AI learning from messy data, but organizations failing to build systematic governance infrastructure
- **Historical parallel**: Like factory machines replacing artisans—not by initial perfection, but by enabling systematic quality improvement
- **Six-month outcome**: 15-20 daily deployments (up from 2-3 weekly), 71% reduction in production vulnerabilities, new AI Governance Architecture team

"Garbage in, garbage out" is true for chaotic systems where errors are random and ungovernable. It's false for patterned systems where errors are systematic and correctable. AI creates the latter. Humans create the former. That's why AI-accelerated development becomes more governable, not less—despite being trained on messy human code.

---

## Navigation

[← Previous: Part III - Chapter 12](../Part-III/chapter-12-bureaucracy-examined) | [Part IV Overview](index) | [Table of Contents]({{ site.baseurl }}/TABLE-OF-CONTENTS) | [Next: Chapter 14 →](chapter-14-economics-predictable-wrong)
