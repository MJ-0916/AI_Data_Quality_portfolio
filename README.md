# Project 1 - Safety Labeling & Policy Interpretation

This project simulates Trust & Safety workflows:
- 9 safety policy categories
- Decision trees for Minor Safety & Hate Speech
- 50 labeled sample contents
- PDF report (+ dataset + diagrams)

## Objectives 

- Define clear safety categories 
- Build decision trees for high-risk areas
- Apply policies across sample contents  
- Document severity, actions, and rationales in a structured dataset  
- Identify key insights and policy interpretation challenges  

## Files in this folder

1. `Project_1_Safety_Labeling_and_Policy_Interpretation.pdf`  
  : Full report including executive summary, policy definitions, decision trees, dataset overview, and insights

2. `safety_labeling_dataset.csv`  
  : manually labeled cases with content description, policy category, severity, action, rationale  

3. `decision_tree_minor_safety.png`  
  : Decision flow for evaluating content involving minors (under 18)

4. `decision_tree_hate_speech.png`  
  : Decision flow for evaluating group-targeted hate vs general harassment  

## Safety Categories

1. Violence  
2. Hate Speech  
3. Adult Nudity & Sexual Content  
4. Dangerous Acts  
5. Minor Safety  
6. Suicide & Self-harm  
7. Bullying & Harassment  
8. Illegal Activities & Regulated Goods  
9. Fraud & Scam

Each category has definitions, violation examples, and allowed examples in the PDF report.

## Why focus on Minor Safety and Hate Speech?

Minor Safety and Hate Speech are two of the highest-risk and most ambiguous areas in Trust & Safety operations. They involve strict legal and reputational risk, context-dependent decisions, frequent need for escalation.  
Hence, I built decision trees for these categories to turn complex policy into consistent, repeatable decision logic for training and QA.

## What this project demonstrates

- Policy interpretation & application  
- Risk assessment and severity decisions  
- Use of escalation and restriction actions  
- Ambiguity handling (bullying vs. hate speech, minors vs. adults, etc.)  
- Quality assurance mindse
