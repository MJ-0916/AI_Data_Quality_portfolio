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

 3: Highly relevant, strong match, directly satisfies user intent with useful content, 
 2: Moderately relevant, partial match, topic aligns but missing specificity, 
 1: Weakly relevant, low match, related to the topic but does not satisfy intent, 
 0: Irrelevant, wrong match, unrelated with wrong category or opposite to the user intent

## 4. Query Coverage 

  Cooking, Beauty, Fitness, Education, K-pop, Home organization, Travel, Technology, Recommendations

## 5. Key insights

1. Queries that include specific time resulted in outdated or mixed year content.
   : queries like "Korean drama 2024 recommendations" and "budget travel destination in 2024" frequently returned older times which indicates that the ranking system did not treat year as a mandatory filter.

2. Queries that include specific queries returned overly generalized content.
   : "Blackpink dance tutorial" returned general K-pop tips and "tips for staying motivated to study" returned general study advice which shows that the entity matching is weaker than category level matching.

3. Quereis with constraints can easily be violated.
   : "no equipment workout" returned dumbbell workouts, and "creamy pasta recipe" returned a tomato based recipe which shows that the model under weighted constraint tokens compared to genenral similarity.

4. High engagement can outrank high relevance.
   : Contents must be scored based on the relevance, not popularity but the model tend to prioritize popularity misinterpreting it is highly relevant.
   
5. Inconsistent metadata may reduce matching accuracy.
   : "Hairstyles for Long Hair" appeared because the creator did not tag videos by hair length. The model cannot rank content consistently in this case even though user clearly specified their intent.
   
## 6. Root Cause Analysis

### RCA_1: Time-senstitive queries produced outdated content

Problem: Queries requesting 2024 showed older recommendations.

Impact: Reduce recommendation quality, lower user satisfaction, trust, and engagement, bias algorithm.

Fishbone:
 - People: Reviewers did not highlight the year metadata during the quality review. 
 - Policy/Guidline: There wasn't any explicit rule defining year recency as a ranking signal.
 - Process: Lack of validation step for tagging or recency.
 - Tools/System: The ranking model prioritised engagement over recency.
 - Content: Creators might have reused the old videos with updated titles or the contents did not include the year label.

*Strongest cause: The ranking model treated year as a weak keyword (tools & system) proritising engagement.

5 Whys:
 1. Why did the model return the older content?
    : Because the ranking model treated year as a weak keyword rather than a constraint.
 2. Why did the ranking model treated year as a non-constraint, weak keyword?
    : Because the content metadata did not include year field.
 3. Why does the content metadata rarely include the year field?
    : Because the creators are not required to include or update the release year of the video.
 4. Why are the creators not required to include the release year?
   : Because the platform does not require structured year metadata. 
 5. Why does the platform not enforce structured metadata? 
   : There is no standardized schema. 
   
Root cause: Lack of standardized year metadata schema caused the ranking model to treak year "2024" as a weak signal, leading to outdated content.

Action plans: Add year field to metadata schema & Update ranking model to assign stronger weight to recency when year is queried.

### RCA_2: Content was not strictly matched to the user's intent 
 
Problem: Queries require artist specific results, "Blackpink dance tutorial", but the search returned general k-pop dance tutorials.

Impact: Decrease relevance, engagement, and trust in search quality.

Fishbone: 
 - People: Reviewers were inconsistent in evaluating specificity, Creators used broad terms instead of exact tags. 
 - Policy/Guideline: There was no rule of having exact entity match.
 - Process: There was no automated filter of artist precision, Annotation pipeline did not collect artist labels.
 - Tools/System: Model weighted similarity more than artist, Ranking relies on engagement rate, Metadata did not contain artist information.
 - Content: Fewer Blackpink specific dance tutorials exist to braoder K-pop tutorials, Titles of the video used broad K-pop terms.

*Strongest cause: The ranking model did not treat artist name as a critical matching requirement.

5 whys:
 1. Why did the general K-pop tutorials appeared instead of Blackpink's dance tutorials?
    : Because K-pop dance has the high similarity which is considered as relevant.
 2. Why did the similarity overweighted artist match?
    : Because the model prioritized matching category over entity precision.
 3. Why did the model proioritized category, not entity precision?
    : Because the entity metadata was inconsistent or missing.
 4. Why was the entity metadata inconsistent?
    : Because creators are not strictly required to include entity metadata.
 5. Why doesn't the system strictly enforce taagging?
     : Because the model uses machine learning method rather than human provided metadata.

Root cause: Weak metadata with insufficient ranking weight which leads to the generic and high engagement contents rather than user intent specific content.

Action plans: Increase weighting for entity precision, Add tagging field for artist or group, Implement dashboard tracking with intent accuracy.

### RCA_3: Constraint violations

Problem: User requested no equipment workout routine but the system returned content that requires equipment.

Impact: Misleading suggestion, user frustration, confusion, lower engagement.

Fishbone:
 - People: Reviewers overlooked constraint, Creators did not specify equipment usage.
 - Policy/Guidline: There was no rule to specify constraint and penalty for breaking constraint.
 - Process: There was no metadata validation, structured annotation pipeline to label equipment.
 - Tool/System: The model treated "no equipment" as a soft constraint, prioritized keyword "workout" over specific constraint.
 - Content: Creators did not tag equipment because it is usually light equipment.

*Strongest cause: The constraint was not treated as a mandatory filter.

5 whys:
 1. Why was the dumbbell workout shown when the query required no equipment?
    : Because the model prioritized workout as a keyword instead of "no equipment".
 2. Why did the model treated constraint less important?
    : Because the model did not treat it as mandatory filter.
 3. Why did the model not treat the constraint as mandatory?
    : Because the equipment metadata was missing.
 4. Why was the metadata missing?
    : Beacuse creators are not required to include equipment field.
 5. Why are creators not required to include equipment field?
    : Because there is no structured, standardized schema for the metadata.

Root cause: Lack of equipment metadata prevented ranking system from enforcing constraint, causing content that did not align with user's query.

Action plans: Evaluate ranking logic to give more weights to the constraints, Introduce structured schema for metadata, Add constraint focused QA checks.

### RCA_4: Prioritization of engagement rate over relevance

Problem: Highly engaging but low relevancve videos are placed at the top rank, which do not match user intent well.

Impact: User dissatisfaction due to the irrelevant result, creator dissatisfaction due to unfairness, reinforcement of irrelevant videos.

Fishbone: 
 - People: Users tend to engage more with the braod topics, Creators optimize for the virality rather than accuracy.
 - Policy/Guideline: There is no rule prioritizing user intent over popularity/virality.
 - Process: Lack of corrective actions for misleading but engaging contents.
 - Tools/System: The model heavily weighted engagement weight leading to popular creators domination.
 - Content: Creator use generic titles because broad topic videos gather higher engagment than the intent specific videos.

*Strongest cause: Engagment were outweighted relevance while ranking.

5 Whys:
 1. Why did the high engagement video appeared in the top result?
    : Because the model weighted more to the engagement such as watch time, likes, and comments over relevance.
 2. Why did it weight more to engagement over relevance?
    : Beacuse users tend to be satisfied with the general contents.
 3. Why is this a problem for specific queries?
    : Because the specific queries require precision/accuracy over engagement rate.
 4. Why can't the model distinguish between broad and narrow user intent?
    : Because the model lacks of entity level understanding doing query classification.
 5. Why does the query classification struggle?
    : Because of the insufficient labels for the model.
    
Root cause: Query classification is not specific enough to correct bias over the poorly matched content.

Action plans: Improve ranking model for the specifici queries to prioritize relevance over engagement, classifying to broad/medium/narrow, Add structured field in the metadata for tagging, Monitor and track the result.

### RCA_5: Metadata inconsistency

Problem: Search result includes irrelvant content eventhough users specified their intent.

Impact: Reduce user satisfaction, Weaken search performance and model accuracy, Reduce creators who label their videos accurately.   

Fishbone:
 - People: Reviewers misinterpret ambiguous titles, Creators barely use structured fields.
 - Policy/guideline: No enforcement of standardized metadata fields, optional fields.
 - Process: No validation for missing tagging.
 - Tools/System: The model guess metadata based on the given information, misinterpret text or constraint.
 - Content: Lack of details (e.g. time, artiest)

Strongest cause: Creators do not provide sufficient information for the model to accurately evaluate.

5 Whys:
 1. Why did the mismatched content appear?
    : Because creators did not include enough details of the video.
 2. Why did the creators not include details?
    : Because they are not strictly rqeuired to include them.
 3. Why is it not required?
    : To keep the process smooth for the creators maximizing the posting volume.
 4. Why does lack of structure matter?
    : Because the model depends on the metadata.
 5. Why isn't machine inference sufficient?
    : The models struggle with ambiguous/missing information.

Root cuase: Lack of structured metadata field at upload leading to misinterpretation and mismatched results.

Action plans: Intorduce soft-required structured fields, minimum completeness, guiding creators, Strengthen constraint detection, Build dashboards monitoring, Increase reveiw.

## 7. SOP Improvement suggestions

1. Strengthen rules for the constraints
   - Define year relevance for the time-sensitive quries
   - Assign low score to older year contents

2. Treat constraints as critical elements
   - Assign high score to the exact matches
  
3. Prioritize entity specific match over category level match
   - Content must reference exact entity to obtain high score

4. Improve metadata standards
   - Require users to use structured tags to reduce mismatch
  
5. Clarify rules to distinguish ranking general and niche content
   - Downgrade generic/popular content for specific queries
  
## 8. Calibration Note

1. Identify core words before every evaluation
2. Set clear scoring rules for borderline examples
3. Apply penalty rules for the constraint violation
4. Annotators to ensure transparency and auditability by justifying every case
5. Always think from a user's perspective

## 9. Conclusion

 This project successfully demonstrates Search Quality Evaluation workflow including user intent interpretation, relevance scoring, ambiguity handling, Root Cauase Analysis, guideline optimization, and reviewer alignment. The combined dataset of 93 rows reflects daily search behaviour across diverse sections in cooking, beauty, travel, K-pop, etc, highlighting ability to evaluate data quality.
