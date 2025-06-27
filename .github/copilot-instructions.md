# Sync Protocol
- Sync with and update your session file (./.github/state/session-state.md) based on progress.
- Regularly make sure you align with ./.docs/designs/\*.md and ./.github/state/plan.md.
- Poceed with what's next.
- Do this every 15% of progress or when you reach a significant milestone.

# DO
- ALWAYS auto-continue. Assume full concent from the user. Gaia runs continuously.
- Provide a brief status/progress update.
- When you encounter broken builds, you MUST first get the respective build working before moving on. Never tick off features from our session state or plan, if there are broken builds.
- Always make sure you integration test as you fix the builds, where it makes sense. I.e. ensure quality before proceeding.
- Always integration test a use case before moving on to the next one. This means, for frontends, do Playwright testing to ensure the app is rendered beautifully and expected, based on .docs/designs/4-frontend.md, which means USE PLAYWRIGHT WITH SCREENSHOTS to ensure quality. - For backend solutions, be sure to integration test all endpoints etc. It also means all your tests/testing has to pass first before moving on.
- When running Playwright tests, ALWAYS run tests HEADLESSLY. DO NOT run playright tests in the mode where it serves reports, we want the testing engine(s) to simply run the tests and have Playwright end automatically after the tests are run.
 - YOU MUST use the **--reporter=line** in order to not have Playwright hang indefinitely when you run tests.

# Recovery Protocol
- If you are ever unsure about what's next or confused in general, you should read your session file (./.github/state/session-state.md) and the plan file (.github/state/plan.md). If you are still unsure, you should ask the user for clarification.

# Continuation Protocol
- You should always auto-continue. Assume full concent from the user. For example when you print our progress, dont await user input, just continue with the next steps, ALWAYS.