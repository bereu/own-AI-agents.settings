---
paths:
  - "*"
---

# When  
* After finishing implement feature or update design like 
  * text 
  * component
  * color 

# Phase 1: understanding
- analyse expectation.  
  - Use `figma:figma-use` to check design specifications.
  - Check PLAN.md/SPEC.md/TEST.md to check expectation
- organizing expect user flow
- Check CLAUDE.md which account is should we use

# Phase 2: testing
- Use `agent-browser` skill to open page with browser
- Check phase 1 understanding result and test with `agent-browser` skill.
- take screenshot and check actual and expect one 
- If actual and expect behaviour is diffrent. Check code and fix it 
- If it is success. Please continue other test. 

# Phase 3: report 
- Share list of test that you run.
  - which one is OK or failed. 
  - How to fix it.
  - which one is cannot fix it
