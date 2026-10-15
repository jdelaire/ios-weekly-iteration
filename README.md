# iOS weekly iteration

A manually invoked agent skill for releasing an update to an existing iOS app. It moves through phases automatically, with a 48-hour user-testing window and explicit approval before implementation and App Store submission.

## Install

Ask Codex:

```text
Use $skill-installer to install https://github.com/jdelaire/ios-weekly-iteration/tree/main/skills/ios-weekly-iteration
```

Alternatively, copy `skills/ios-weekly-iteration` into your agent's supported local skills directory.

## Start

Open the existing app project and invoke:

```text
$ios-weekly-iteration
```

One explicit invocation starts one release cycle. Installation and ordinary development requests do not start a cycle. Scheduled continuations can resume that cycle, but cannot start the next one.

## Workflow

1. Inspect the app and propose a backlog mixing features with technical debt or performance work. Wait for your acceptance.
2. Bump the version, implement accepted work on `main`, verify it, commit, and push through the existing TestFlight pipeline.
3. Start 48 hours of user testing once the build is available to you. Implement feedback, then ask whether testing is complete.
4. Prepare release metadata, video, and Instagram caption using the project's available skills.
5. Present the exact release package. Submit through asc only after your explicit go.
6. Monitor the submitted version. After approval, publish the prepared Instagram video once and finish the cycle.

Phases advance when ready. The week is an approximate cadence; testing or Apple review can extend it. Approval gates remain pending until answered.

## Requirements

- An existing iOS repository and a working TestFlight build pipeline.
- The asc CLI, authenticated App Store Connect access, and relevant asc skills.
- The project's release-video skill and authenticated Instagram publishing integration.
- A suitable Mac or the project's established CI for Xcode builds and simulator capture.
- T3's persistent scheduler for automatic testing and review wakeups.

The skill provides workflow instructions. It uses the host scheduler rather than installing a daemon. If scheduling is unavailable, it saves progress and resumes when you return.

## State and recovery

Checkpoints and ownership locks live in repository-local Git metadata, outside tracked app source. Submission approval identifies the exact release package. Interrupted submissions and Instagram posts are reconciled before retrying.

Readiness delivery retains a five-minute recovery wakeup until the question is confirmed delivered. Once delivered, it waits for your response without repeated prompts.

See [SKILL.md](skills/ios-weekly-iteration/SKILL.md) and [continuations](skills/ios-weekly-iteration/references/continuations.md) for the complete workflow.

## Validation

The package passed the skill validator and 21 simulated workflow checks, including interrupted readiness delivery, stale approvals, and uncertain publishing results. Live TestFlight, Apple review, Instagram delivery, and timed wakeups were not exercised during package validation.
