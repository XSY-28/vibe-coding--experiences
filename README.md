# Vibe Coding Notes

[English](README.md) | [简体中文](README.zh-CN.md)

## I. Prompt Engineering

1. Give the AI a clear prompt, especially about things you care about that it might misinterpret. For a personal website, “nice and modern” leaves a lot open: what information should come first, and what kind of layout do you like? Anything you leave unspecified becomes a decision for the AI.

2. You still need to judge the design. Let the AI propose ideas, but find references and explain what you like about them. Fonts, spacing, and the order of information are easier to discuss than “make it look more premium.” Clear requirements help; adding every requirement you can think of can bury the important ones.

3. You can show the AI a good implementation of a similar task and explain which parts you want to borrow. Existing code shapes what it writes next, so bad habits established early can carry on. Whether a good reference improves the result is something to test. A reference built for a different scale or set of requirements can also steer the architecture in the wrong direction.

4. Do some research before a long task, then split it into smaller goals you can check. At each stage, check both the result and the direction. This matters especially for exploratory work: asking the AI to “implement this idea” may produce something that runs without answering whether the idea is worth pursuing.

## II. Repository Management

1. Read good READMEs. After reading one, do you know what problem the project solves, how to run it, and what to try first? Think about how you would write it yourself, then compare and see what you missed.

2. Before the AI runs Git commands, inspect the changed files and ask it to explain why it is taking that step. At least know the difference between editing files in the working tree, saving a local version with a commit, and sending commits to a remote with a push. Knowing where you are in the process helps you spot mistakes.

   Keep each commit focused on one thing. If you are fixing a bug, leave dependency upgrades and project-wide formatting for separate changes. That makes it easier to investigate problems or undo a change later.

3. To contribute to someone else's project, a typical workflow is:

   ```text
   Confirm the issue → fork → clone → create a branch → edit, test, commit
                                                        ↓
                                       Sync upstream changes if needed
                                                        ↓
                                         Push to your fork → open a PR
                                                        ↓
                                    Review and revise → maintainer merges
   ```

   A fork is a repository under your own GitHub account; cloning brings it onto your computer. A pull request asks the original project to merge your changes. To sync changes, you can merge or rebase according to the project's conventions. Rebasing rewrites commit history, so don't casually rewrite commits other people depend on.

4. Keep asking the AI about best practices, but ask for the reasoning too. What problem does the approach solve? What scale is it meant for? What extra maintenance does it require? Judge it against the project you have, rather than the tools and terminology it lists.

## III. Software Engineering and MVPs

1. Start with a small version someone would actually use. An MVP—minimum viable product—can be incomplete, but its intended users need to be able to try the core feature. For a note-organizing tool, run a few notes through it first and see whether it saves effort and where it is awkward. Having an interface and having evidence that people need the product are different milestones.

2. When requirements are unclear, build something, get feedback, and revise. Long, separate phases for requirements, design, coding, and testing can leave problems hidden until late. An MVP helps test the need; short iterations help you adjust. You can use both without starting over every time.

3. Inspect the actual result, including what happens when something fails. Once the program works on a normal input, try empty input, repeated operations, and a failure partway through. The AI's “done” should match the result. Passing tests only covers what those tests check.

## IV. Requirements and Architecture

1. When modifying part of a mature project, the AI has existing interfaces, coding conventions, and tests to follow. Starting from scratch means making those decisions again. Look at the proposed structure during planning, especially how responsibilities are divided and who owns the data. You don't need to design every requirement the project might have years from now.

2. To judge whether an architecture is maintainable, try changing a requirement. Does a new input format force you to change the core algorithm? Does a new output format also require changes to input handling? If changes keep spreading into unrelated parts, reconsider the boundaries. Room for future changes should correspond to specific changes you can reasonably expect.

3. When requirements keep getting more complicated, return to the work the software is supposed to support. Who makes which decisions? What are those decisions based on? Which rules must always hold? In a university records system, “passed the course” and “received credit toward a degree” mean different things. If the concepts are unclear, adding fields and conditions can make the code harder to follow.

4. Both the current state and the events that produced it may be worth keeping. A balance of 100 yuan doesn't explain where the money came from; individual transactions do. Event sourcing records accepted changes as events and reconstructs state from them.

   It comes with costs. Event formats evolve, queries may need separate read models, and replaying events must not charge someone again. Concurrency conflicts still need handling. Ordinary CRUD—create, read, update, delete—can also work with business logic, transactions, and audit records. A complicated domain alone is not a reason to switch to event sourcing.

   First ask what you need: only the current value, or a history of the actions and decisions behind it? Then choose the design.
