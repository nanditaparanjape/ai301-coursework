# Unit 1: Issue Selection

## Selected Issue
https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72

## Skill Output
```json
[                                                                             
    {                                                                           
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72", 
      "checks": [                                                               
        {"name": "maintainer-alive", "grade": "pass", "evidence": "Human commit 
  by Andrew Burke on Sep 16, 2026 — 4 days before today, within the 60-day      
  window"},                                                                     
        {"name": "repo-active", "grade": "pass", "evidence": "Most recent       
  default-branch commit Sep 16, 2026 — 4 days ago, well within 80-day           
  threshold"},
        {"name": "not-claimed", "grade": "pass", "evidence": "No assignees, no  
  linked PRs, and no claim comments on the thread"},                            
        {"name": "scope-fit", "grade": "pass", "evidence": "Bounded bug fix: 
  catch UnknownHashError in core/security.py and return False; remove one       
  @pytest.mark.xfail marker; estimated 1–2 hours"},
        {"name": "ai-policy-allowed", "grade": "pass", "evidence":              
  "docs/CONTRIBUTING.md is silent on AI-assisted contributions; silence         
  passes"},
        {"name": "beginner-friendly", "grade": "pass", "evidence": "Labeled     
  'good first issue' and 'tier-1 (Starter difficulty)'"}                        
      ],
      "verdict": "accept"                                                       
    },                                                                          
    {                                                                           
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68", 
      "checks": [                                                               
        {"name": "maintainer-alive", "grade": "pass", "evidence": "Human commit 
  by Andrew Burke on Sep 16, 2026 — 4 days before today, within the 60-day      
  window"},                                                                     
        {"name": "repo-active", "grade": "pass", "evidence": "Most recent       
  default-branch commit Sep 16, 2026 — 4 days ago, well within 80-day           
  threshold"},
        {"name": "not-claimed", "grade": "pass", "evidence": "@yulijasso's claim
   comment (Sep 20, 2026) does not block — Path Review house rule: classmate    
  claim comments never block an issue"},
        {"name": "scope-fit", "grade": "pass", "evidence": "Bounded bug fix: add
   empty-corpus guard in rag/retriever/keyword_search.py; remove one            
  @pytest.mark.xfail marker; estimated 2–4 hours"},
        {"name": "ai-policy-allowed", "grade": "pass", "evidence":              
  "docs/CONTRIBUTING.md is silent on AI-assisted contributions; silence         
  passes"},
        {"name": "beginner-friendly", "grade": "pass", "evidence": "Labeled     
  'good first issue' and 'tier-1'"}                                             
      ],
      "verdict": "accept"                                                       
    }                                                                           
  ]        

Run History
Started with an 11/20 because my maintainer and commit time limits were set way too strict at 3 days and 5 days, which flagged perfectly active repos as dead. The rubric was also missing a rule to check for AI contribution guidelines. Once I opened the commit and maintainer windows to 90 days, added an explicit check for AI contribution rules, and made sure scope-fit fails big umbrella tasks, the eval run hit 18/20.

Issue Analysis
I picked Issue #72. It is a clean bug in core/security.py where passlib throws an UnknownHashError on bad hashes instead of just failing safely and returning False. Fixing it only touches password verification logic and removes an xfail marker in tests/unit/test_security.py. There is no complicated architecture work or database changes involved.

Check Rationale
The required checks cover the basic ground rules:
1) maintainer-alive and repo-active make sure the project is not abandoned so someone actually reviews the PR.
2) not-claimed checks that nobody is already working on it, while respecting the Path Review rule that classmate claims do not block you.
3) scope-fit keeps you from getting stuck on massive tasks or unresolved debates.
4_ ai-policy-allowed confirms the repository allows AI-assisted coding.

Trade-offs
The rubric prefers quick, contained bug fixes over big features or broad docs rewrites. It will take a short, bare-bones issue description if the code fix itself is small, but it immediately filters out messy multi-part checklist tasks even if they have a beginner tag.
