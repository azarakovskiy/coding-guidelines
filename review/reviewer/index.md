### TL;DR

Start your day by looking here: [https://github.com/pulls/review-requested](https://github.com/pulls/review-requested).

As a reviewer, you should at least make sure that a change does not degrade the code quality:

1. The code is **well-designed**.
2. The code is **not more complex than it needs to be** at the moment. Keep it simple.
3. Any parallel programming is done safely.
4. The code has appropriate **unit tests**.
5. The code conforms to our [style guides](https://confluence.taxibeat.com/x/QbhPAQ).

Make sure to review **every line** of code, look at the **context**, make sure you’re **improving code health**, and compliment developers on **good things**.

If you can't review it during a reasonable time, let the author know about it.

**Favor approving any change that definitely improves the overall code quality, even if it's not perfect.**

#### Review process step by step
* Before you start
    1. Find the JIRA ticket.
    2. Read the PR description.
    3. Optionally talk to the author.
    
    You need to understand the *scope* of the change and *why* it has been made.
    
    Dedicate your time and attention to the review.
* During review
    1. Look for potential design issues.
    2. Understand if the issue is solved by the change.
    3. Is the code simple enough?
    4. Do you understand easily every single line of code?
    5. Do unit tests cover the functionality?
    6. Is the code style correct?
    7. If all the needed documentation up-to-date?
    8. **Does the change improve the code quality even a little bit?**
* After review
    1. Dedicate your time even after the review as you might get requested to re-review it.
    2. Help the author with anything if needed? By reviewing their code, you have also become responsible for that part.

### Purpose of code review

The primary purpose of code review is to make sure that the overall code health is improving over time. In order to accomplish this, a series of trade-offs have to be balanced.

First, developers must be able to make progress on their tasks. 

On the other hand, it is the duty of the reviewer to ensure the suggested change doesn't decrease the overall code quality. 
This might be very tricky because often the codebase degrades through a series of small shortcuts taken under specific conditions such as time constraints.

However, perfect code doesn't exist — there is only better code. Reviewers should not require the author to polish every tiny piece of code. 
Instead of seeking perfection, what a reviewer should seek is continuous improvement.

**❤️ Reviewers should favor approving a change *when it definitely improves the overall code health of the system*, even if it isn’t perfect.**

**❤️ Don’t accept changes that degrade the code health of the system.** [Emergencies](#emergency) are a single exception to this rule.

### What to look for in a code review
**❤️ Design** is the most important thing to cover.  Is the code well-designed and appropriate for your system? 
Do the interactions of various pieces of code in the change make sense? Does this change belong in your codebase, or in a library? 
Does it integrate well with the rest of your system? Is now a good time to add this functionality?

**❤️ Functionality**: Does the code behave as the author likely intended? Is the way the code behaves good for its users? Are all the acceptance criteria met?

**❤️ Complexity**: Could the code be made simpler? Would another developer be able to easily understand and use this code when they come across it in the future?

**❤️ Tests**: Does the code have correct and well-designed automated tests?

**❤️ Naming**: Did the developer choose clear names for variables, classes, methods, etc.?

**❤️ Comments**: Are the comments clear and useful?

**❤️ Style**: Does the code follow our [style guides](https://confluence.taxibeat.com/x/QbhPAQ)?

**❤️ Documentation**: Did the developer also update relevant documentation?

### Context
It is crucial that you fully understand the scope and context of a proposed change. This might seriously affect your understanding of a change. 
Read a JIRA ticket, read a PR description, try to match the code change with what is written in the description.

**❤️ Always think for a few moments about *why a change is needed*, *what it covers* and *how it affects* other parts of the system.**

### Multiple changes in one pull request
This is generally a very bad practice to have a pull request with multiple changes, and especially with a big refactoring followed by a functional change.

If you see that a pull request you've been asked to review contains changes that can be easily separated into two different PRs, ask the author to do that. Don't be too strict though.

One example of what can be easily split into two PRs is a refatoring and a small functional change using that refactoring. This must become two PRs.

**❤️ Try to estimate if splitting a PR into two or more would benefit the quality of your review, and does not require too much work.**

### Appreciate someone's work
Do not only focus on mistakes. Code reviews tend to be very focused on what could have been better, but it is very pleasing to give and receive positive comments.

**❤️ Don't hesitate to give also positive feedback.**

### Mentoring
Code reviews have an important function of teaching developers something new about a language, a framework, or general software design principles. 
It’s always fine to leave comments that help a developer learn something new. It does not matter how experienced you or your colleague are, 
there is always something that even the most senior developer doesn't know. Sharing knowledge is part of improving the code health of a system over time. 

**❤️ Share your knowledge but don't require the author to implement your suggestion.**

### Judging principles
* **❤️ Technical facts and data overrule opinions and personal preferences.**
* On matters of style, the [style guide](https://confluence.taxibeat.com/x/QbhPAQ) is the absolute authority. 
If there is no previous style, accept the author’s. Consider adding it to the style guide if applicable.
* Several approaches might be equally valid; in such a case, the reviewer should accept the preference of the author. 
Otherwise the choice is dictated by standard principles of software design.
* If no other rule applies, then the reviewer may ask the author to be consistent with what is in the current codebase, as long as that doesn’t worsen the overall code health of the system.

### Code-readability
The ideal code can be read like an open book. You don't spend much time to understand the meaning of anything, and it becomes clear why something has changed in a way it has. For more complex parts you might need to stop for a little bit, and benefit from a well-written comment. 

If it is difficult to understand something in a proposed change or you need the author's help, there is a very high chance that future developers will struggle too. Ensure to minimize this chance.

**❤️ As a reviewer, you must ensure to get a piece of code is as simple and readable as it can be.**

### Tests
Tests are essential to keep the code stable and maintainable. As a reviewer, you don't want to ignore tests in a proposed change. 
Rather, you want to understand what is actually tested and if the coverage is sufficient.

The percentage of the code covered is less important than the amount of functionality covered. 
In other words, tests are better when they cover what is important and what makes sense to cover, 
and will break if you break the functionality, rather than high number of lines covered but tests are not reliable.

Also, tests are a very good example of how you are supposed to use the piece of code or functionality. Therefore they must be very easy to follow and support.

This all makes tests a very important part of any change.

**❤️ Analyze tests' structure, try to ensure they cover the functionality and are not just present to satisfy the code coverage metric.**

### Comments 
Comments must guide you through the complex code with the only exception of required comments such as for `go lint` successful run for something very obvious and unavoidable. 

If an author had to explain a piece of code using a comment, it might mean that that piece is too complex and might be simplified. Try to understand if this is the case.

Sometimes it cannot be written simpler or differently for a number of reasons. In such a case, a comment must explain to you why this piece of code is here, and not what it is doing. 
Comments that tell you a *"what"* are usually useless and can be removed with few exceptions like complex RegExps which usually highly benefit from a detailed explanation.

Remember: the best readable code does not need comments. This is the ultimate goal.

**❤️ Try to make sense of all the comments: remove where you don't need them, add where you do need them.**

### Documentation
**❤️ Think what has to be updated for this change: Confluence, README or maybe Swagger?**

Be careful with too extensive documentation in places where you want to keep it shorter. 
Usually, Confluence is a good place for elaborate documentation, and README has a short and concise version of technical docs.

### In-person review
For bigger or more complex changes, it might be a good idea to pair up for the review. 
This will help a lot to understand the context and the change itself and will give you the possibility to give immediate feedback.

Also, if you have a lot of comments, it might be a good idea for you to walk a developer through your comments.

**❤️ Ask the author to go you through their change when you feel this would benefit the quality of your review.**

**❤️ Walk a developer through your review when it is getting big.**

### Handling pushback
When a developer disagrees with your suggestion, first take a moment to consider if they are correct. 
Often, they are closer to the code than you are, and so they might really have a better insight about certain aspects of it. 
Does their argument make sense? Does it make sense from a code health perspective? If so, let them know that they are right and let the issue drop.

However, developers are not always right. In this case, the reviewer should further explain why they believe that their suggestion is correct. 
A good explanation demonstrates both an understanding of the developer’s reply, and additional information about why the change is being requested.

In particular, when the reviewer believes their suggestion will improve code health, they should continue to advocate for the change, 
if they believe the resulting code quality improvement justifies the additional work requested. 

**❤️ Improving code health tends to happen in small steps.**

Sometimes it takes a few rounds of explaining a suggestion before it really sinks in. 
Just make sure to always stay polite and let the developer know that you *hear* what they’re saying, you just *don’t agree*.

### Resolving conflicts
In any conflict on a code review, the first step should always be for the developer and reviewer to try to come to consensus. Start with a public discussion in the PR, then if needed move to a face-to-face discussion.

If a face-to-face discussion has not ended up with a decision, ask someone else's opinion but not the whole team.

*Only if you* still can't come to an agreement, ask your team leader or engineering manager. They *must* make a decision. Consider adding this to our [style guide](https://confluence.taxibeat.com/x/QbhPAQ).

**❤️ Always document in a PR what you have agreed on so that others can read it. Never keep it private.**

**❤️ Be proactive and never let a change sit around because you can’t come to an agreement.**

### Think twice before introducing more tech debt
A very well-known source of push back sounds like 
> "I will clean it later". 

In fact, unless the developer does the clean up immediately after the present PR, it never happens. 
This isn’t because developers are irresponsible, but because they have a lot of work to do. 
Letting people *“clean things up later”* is a common way for codebases to degenerate.

**❤️ Estimate the cost of introducing a tech debt against doing it right now.** Remember that your tech debt will involve discussions, estimations, and another overhead.

**❤️ Do not agree to compromise the code quality to faster delivery.** [Emergencies](#emergency) are a single exception to this rule.

#### On the other note: ToDo's
Sometimes creating a tech debt is actually a good thing. Especially it makes sense when making it right is not in the scope of a current change and requires a lot of work now.

**❤️ You could agree to let the author put a `todo` in code with a mandatory link to a JIRA ticket where it gets fixed.** JIRA ticket must reference a piece of code is applicable.
Yet this must not happen regularly and must be justified why it can't happen now.

### Minor improvements
When you encounter some things that you think might be written nicer or this is rather a question of a style, or it is just not important for the functionality, etc., consider adding a purely advisory comment. You may prepend it with something that makes it clear it is not mandatory: "Nit:" or "Nice-to-have:" or similar.

**❤️ Never block a PR if your comment is a nice-to-have.**

### Emergency 
An emergency is a **small** change that must be applied as soon as possible because it allows a major launch to continue instead of rolling back, 
fixes a bug significantly affecting users in production, handles a pressing legal issue, closes a major security hole, etc.

In emergencies we really do care about the speed of the entire code review process. 
In this case *only*, the reviewer should care more about the speed of the review and the correctness of the code (*does it actually resolve the emergency?*) than anything else. 

However, after the emergency is resolved you should look over the emergency change again and give them a more thorough review.

To be clear, the following cases are **not** an emergency:

* Wanting to launch this week rather than next week (unless there is a hard deadline).
* The developer has worked on a feature for a very long time and they really want to get the change in.
* Rolling back a change that is causing test failures or builds breakages.
* Meeting any kind of soft deadline. 
* Soft deadline is the opposite of hard deadline. A hard deadline is one where something disastrous would happen if you miss it. A soft deadline is any other kind of a deadline including the request from your project manager.

**❤️ Never sacrifice your code quality unless there is a real emergency.**

### The best time for reviews
Make sure to fully dedicate your attention to what you are reviewing. If you feel tired or still sleepy, don't review it.

On the other hand, you are expected to review it during a reasonable time. Don't postpone it for a long time. When you get a request to review, try to plan a time slot in the very near future when you can jump on it. 

Everybody is different, for some people morning is the best time, for some people, this best time is an evening. If you always stick to the same time, it will soon become a good habit.

**❤️ Find your own time when you can effectively review someone's work. Don't postpone it for too long.**

**❤️ If you are in the middle of a focused task, such as writing code, don't interrupt yourself to do a code review.**

**❤️ If you can't review the change during a reasonable time, let a developer know.**

**❤️ It is a good idea to look at [this page](https://github.com/pulls/review-requested) from time to time.**

### How to write code review comments
Be kind and polite. Explain your reasoning.

**❤️ Make sure that you are always making comments about the code and never making comments about the developer.**

> ❌: "Why did *you* use threads here when there's obviously no benefit to be gained from concurrency?"

> ✅ "The concurrency model here is adding complexity to the system without any actual performance benefit that I can see. Because there's no performance benefit, it's best for this code to be single-threaded instead of using multiple threads."

---

Balance giving explicit directions with just pointing out problems and letting the developer decide.

**❤️ In general, it is the developer's responsibility to fix a PR, not the reviewer's.** You are not required to do a detailed design of a solution or write code for the developer.

This doesn't mean the reviewer should be unhelpful, though. In general, you should strike an appropriate balance between pointing out problems and providing direct guidance. 

---

Encourage developers to simplify code or add code comments instead of just explaining the complexity to you.

If you ask a developer to explain a piece of code that you don't understand, that should usually result in them _rewriting the code more clearly_. Occasionally, adding a comment in the code is also an appropriate response, as long as it's not just explaining overly complex code.

**❤️ Explanations written only in the code review tool are not helpful to future code readers.**
