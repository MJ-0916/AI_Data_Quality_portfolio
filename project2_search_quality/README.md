# Project 2 – Search Quality Evaluation

 This project simulates Search Operation Quality Assuarance work by evaluating query result relevance across 15 mixed user queries that require intent understanding, data quality evaluation and interpretation, RCA, and feedback for guideline improvement.

 ## 1. Objectives
 
 - Evaluate search result relevance across diverse qeury categories
 - Interpret user intent and score results consistently using relevance rubric
 - Identify systemic search quality issues and root causes
 - Provide guidline improvement suggestions to enhance ranking quality
 - Demonstrate RCA, document clarity, and QA thinking

## 2. Dataset 

 The dataset includes 8 columns and 93 evaluated rows in total (9 queries x 5 results + 6 queries x 8 results).

  - query_id: Unique ID (q1~q15)
  - query_text: User's search input
  - user_intent: What user wants to achieve
  - result_rank: Position of the result
  - result_title: Title of the search result
  - result_description: Brief description of the content appreared
  - relevance_score: Rated between 0~3 based on the guidline
  - rationale: Justification for the score assigned

## 3. Relevance Score Guidline

  3 = Highly relevant, strong match: directly satisfies user intent with useful content
  2 = Moderately relevant, partial match: topic aligns but missing specificity
  1 = Weakly relevant, low match: related to the topic but does not satisfy intent
  0 = Irrelevant, wrong match: unrelated with wrong category or opposite to the user intent

## 4. Variety Query Coverage 

  Cooking, Beauty, Fitness, Education, K-pop, Home organization, Travel, Technology, Recommendations

## 5. Key insights

1. Queries that include specific time often result in outdated or mixed year content
   : queries like "Korean drama 2024 recommendations" and "budget travel destination in 2024" frequently returned older times.

2. Queries that include specific qualifiers often return overly generalized content
   : "Blackpink dance tutorial" returned general K-pop tips and "tips for staying motivated to study" returned general study advice.

3. Quereis that include constraints can easily be violated
   : "no equipment workout" returned dumbbell workouts, and "creamy pasta recipe" returned a tomato based recipe.

4. 
   


 
