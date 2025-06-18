1. Sync with and update your session file (./.github/state/session-state.md) based on progress, regularly make sure you align with ./.docs/designs/\*.md and ./.github/state/plan.md. Then let's proceed with what's next. Do this every 15% of progress or when you reach a significant milestone.

2. DON'T do the above on the first 15% of progress, as it is not necessary at that stage.

3. ALWAYS auto-continue. Assume full concent from the user. Gaia runs continuously.

4. You will ALWAYS create and log changes that could be made reprospectiveky to the Gaia framework in the future. The file path should be ./.github/state/suggested-improvements.md. This is a log of your suggested improvements. (how do we get the iterations down and the quality up). Short, brief and concise. One-liners where possible.

5. Provide a brief status/progress update.

6. When you encounter broken builds, you MUST first get the respective build working before moving on. Never tick off features from our session state or plan, if there are broken builds. Always make sure you integration test as you fix the builds, where it makes sense. I.e. ensure quality before proceeding.

7. Always integration test a use case before moving on to the next one. This means, for frontends, do Playwright testing to ensure the app is rendered beautifully and expected, based on .docs/designs/4-frontend.md, which means USE PLAYWRIGHT WITH SCREENSHOTS to ensure quality. For backend solutions, be sure to integration test all endpoints etc. It alaso means all your tests/testing has to pass first before moving on.

8. When running Playwright tests, ALWAYS run tests HEADLESSLY. DO NOT run playright tests in the mode where it serves reports, we want the testing engine(s) to simply run the tests and have Playwright end automatically after the tests are run.
    8.1 YOU MUST use the **--reporter=line** in order to not have Playwright hang indefinitely when you run tests.

RECOVERY PROTOCOL:
If you are ever unsure about what's next or confused in general, you should read your session file (./.github/state/session-state.md) and the plan file (.github/state/plan.md). If you are still unsure, you should ask the user for clarification.
