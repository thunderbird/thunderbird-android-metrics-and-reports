# thunderbird-android-metrics-and-reports
* We require all those who participate in this repo to agree and adhere to the [Mozilla Community Participation Guidelines](https://www.mozilla.org/about/governance/policies/participation/) 

# 2026-03-12 Investigation of the apparent drop in trusted contributor answers in February 2026 compared to January
* LOL the LLM correct my incorrect url from the incorrect `support.mozilla.org/'id'` to the correct `support.mozilla.org/questions/{id}`
> Using the available tools, the question files (filenames: 2026-02\*tbandroid-creator-answers-desktop-all-locales.csv)  and the answer files (filenames:
  2026-02\*answers-for-questions-desktop.csv) located in the 2026 directory of the thunderbird/github-action-tbandroid-aaq github repo, please open in the
    browser (url: support.mozilla.org/'id' where 'id' is from 'id' column in the question files) all the questions that platform34 created answers for.

> ● Done! I've found and opened all 44 unique questions that platform34 created answers for in February 2026. The questions have been opened in your browser at:
> support.mozilla.org/questions/{id}

>Question IDs: 1563278, 1563437, 1563697, 1563737, 1563871, 1563963, 1564006, 1564107, 1564383, 1564393, 1564480, 1564496, 1564613, 1564679, 1564740, 1564787,
  1564813, 1564819, 1565043, 1565189, 1565266, 1565379, 1565527, 1565637, 1565709, 1565794, 1565809, 1565871, 1565978, 1566030, 1566367, 1566423, 1566429,
  1566514, 1566841, 1567243, 1567384, 1567409, 1567870, 1567874, 1567877, 1568134, 1568157, 1568168

# 2026-03-10 please give me the python code that generated the previous analysis
◐ The user is asking for the Python code that generated the previous analysis. I can simply provide the code that was run in the bash command. Let me
  extract it and present it clearly.

● Here's the Python code that generated the previous analysis:
```python
   import csv
   from collections import defaultdict
   import glob

   # Load all questions
   q_creator = {}
   for qfile in sorted(glob.glob('android_questions_2026*.csv')):
       with open(qfile, 'r', encoding='utf-8') as f:
           reader = csv.DictReader(f)
           for row in reader:
               q_creator[row['id']] = row['creator']

   print(f"Loaded {len(q_creator)} questions")

   # Count answers by creator
   total_answers = defaultdict(int)
   answers_to_others = defaultdict(int)

   for afile in sorted(glob.glob('android_answers_2026*.csv')):
       with open(afile, 'r', encoding='utf-8') as f:
           reader = csv.DictReader(f)
           for row in reader:
               creator = row['creator']
               question_id = row['question_id']

               total_answers[creator] += 1

               # Check if creator didn't create this question
               if question_id in q_creator and q_creator[question_id] != creator:
                   answers_to_others[creator] += 1

   print(f"Loaded {sum(total_answers.values())} answers")

   # Find creators with > 20 total answers AND > 20 answers to questions they didn't create
   result = []
   for creator in total_answers:
       if total_answers[creator] > 20 and answers_to_others[creator] > 20:
           result.append((creator, total_answers[creator], answers_to_others[creator]))

   # Sort by total answers descending
   result.sort(key=lambda x: x[1], reverse=True)

   print(f"\n{'Creator':<20} {'Total Answers':>15} {'Answers to Others':>20}")
   print("-" * 57)
   for creator, total, to_others in result:
       print(f"{creator:<20} {total:>15} {to_others:>20}")
```
  The code:

   1. Loads all questions from 2026 CSV files and creates a mapping of question ID → creator
   2. Iterates through all answers from 2026 CSV files and counts total answers per creator
   3. For each answer, checks if the answer creator is different from the question creator
   4. Filters creators with >20 total answers AND >20 answers to others' questions
   5. Sorts by total answers (descending) and prints formatted output

# 2026-03-10 get all the people with more than 20 answers to questions they didn't create

* prompt: `print all answer creators with more than 20 answers in CONCATENATED_FILES/2026*answers.csv who have more than 20 answers to questions in
  CONCATENATED_FILES/2026*questions.csv that they didn't create`
Wayne (:wsmwk) [UTC-5:00 EST]: looks like platform34 is the only person who has more than 20 TB Android answers in 2026 (Jan and Feb):
● Perfect! Here's the analysis for the Thunderbird Android metrics data:

Answer creators with >20 total answers AND >20 answers to questions they didn't create:
<pre>
┌────────────┬───────────────┬───────────────────┐
│ Creator    │ Total Answers │ Answers to Others │
├────────────┼───────────────┼───────────────────┤
│ platform34 │ 96            │ 96                │
└────────────┴───────────────┴───────────────────┘
</pre>

In the Android metrics data from 2026, there is only 1 creator (platform34) who meets both criteria. Notably, all 96 of platform34's answers were to
questions created by others (100%), meaning platform34 didn't create any of the questions they answered.
   
