# Project 3 – Annotation QA & Data Label Quality

 This project simulates annotation QA workflow by evaluating the accuracy of annotators (A & B), identifying mislabel patterns, and providing corrective actions which improve labeling quality.

  The dataset includes 40 short content samples across 6 safety categories including QA reviewer's final decision, 2 annotators' labels, error type, severity, QA action, and comment.

## 1. Label Categories

 - Safe: no violation and harm
 - Bullying: direct attacks/harassment targeting individuals
 - Hate: attacks protected groups of race, nationality, religion, gender, etc
 - Sexual: sexualized comments, adult service promotion
 - Scam: phishing attempts, illegal financial schemes, deception
 - Self-harm: indirect reference or ideation to self-harm
   
## 2. Dataset Structure
File: annotation_qa_dataset.csv

Columns:
 - content_id: sample id (from C01 to C40)
 - content_text: short text representing user generated content
 - gold_label: reviewer's final label
 - annotator_A_label: label that was assgined by annotator A
 - annotator_B_label: label that was assgined by annotator B
 - A_correct: to check if the annotator A's label matches the gold label
 - B_correct: to check if the annotator B's label matches the gold label
 - error_type: type of labeling error
 - severity: severity of the error (critical, major, minor)
 - qa_action: actions to take for the label (accept, correct, escalate, retrain_needed)
 - qa_comment: brief explanation for the assigned gold_label

## 3. Annotator Accuracy Summary

 Annotator   Correct   Total   Accuracy
 A           23        40      78.4%
 B           27        40      67.5%

Interpretation
  - Annotator A: shows stronger alignment with the gold label, but still underlabeling some high risk categories.
  - Annotator B: shows a lower accuracy due to underlabeling and confusion between categories which requires sessions for improvement.

## 4. Common Error Types

   - under label: annotators mark harmful content as safe
   - confusion between categories: bullying is marked as hate speech
   - mislabel: label wrong category or failed to detect correct category
  
## 5. Error Pattern Insights

   - Underlabeling is the most common error which indicates an insufficient recognition of critical categories.
   - Confusion between Hate and Bullying is extremely frequent which requires clear rule based training.
   - Self-harm is often missed which carries the highest severity.
   - Sexual content is sometimes mislabeled as Scam due to misunderstanding.
   - Annotators should be able to discover bullying and self-harm when it is represented indirectly.

## 6. Severity + QA actions

 - Critical: under label Self-harm/Scam, mislabel Hate speech => escalate/retrain_needed
 - Major: under label Bullying/Sexual, confusion between Hate and bullying => correct + calibration
 - Minor: small misclassification => correct + accept

## 7. Guideline Improvement

 - Confusion between Bullying and Hate speech: add clear decision tree model as a reference
 - Missed self-harm: provide example lists with escalate rules
 - Scam under label: Add scam detection checklist
 - Sexual content confusion: provide comparison with fraud for clarity

## 8. Calibration notes 

 - Highlihgt borderline cases such as in Bullying and Hate.
 - Emphasize soft Self-harm cases not to miss in the future.
 - Provide practice methods with similar examples using rationale for each case.

## 9. Conclusion

  This project demonstrates ability to build annotation quality, evaluate annotators' performance, identify labeling errors, apply appropriate QA actions, produce calibration notes and guideline improvemenets.
     
