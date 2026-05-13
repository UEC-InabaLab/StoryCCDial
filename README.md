# StoryCCDial: Story Co-Creation Dialogue Dataset

This dataset includes dialogues, dialogue acts, edit histories, participants' personality traits, and post-surveys.
The task involves two people assigned asymmetric roles of "**Leader**" and "**Supporter**" co-creating a story. The data includes the workers' personalities, dialogue data, postsurvey data on their partner and themselves, and interface edit histories.

## 📊 Dataset Statistics

| Category | Value |
| --- | --- |
| **Number of participants** | **120** |
| **Number of dialogue histories** | **485** |
| 　Avg. utterances per dialogue history | 41.6 |
| 　Avg. words per dialogue history | 591.1 |
| **Number of completed stories** | **497** |
| 　Avg. number of sentences in completed stories | 10.0 |
| 　Avg. number of words per sentence in completed stories | 34.6 |
| **Number of edit histories** | **480** |
| 　Avg. number of edit actions per edit history | 23.1 |

---

## 📁 Directory Structure

The dataset is provided in JSON Lines (`.jsonl`) format.

```text
dataset/
 ├── presurvey.jsonl   # Participants' presurvey data (e.g., TIPI-J scores )
 └── sessions.jsonl    # Session data (dialogue, stories, edit histories, and postsurveys)

```

## 📄 Data Format

### 1. `presurvey.jsonl`

Contains the personality traits and demographic data.

| **Key** | **Type** | **Description** |
| --- | --- | --- |
| `user_id` | String | Unique participant ID (e.g., "017") |
| `TIPI_data` | Object | Personality traits (scores: Big Five, responses: Raw text (While the TIPI-J questionnaire items (https://www.jstage.jst.go.jp/article/personality/21/1/21_40/_article/-char/ja) were used in practice, this translation refers to the original TIPI: https://gosling.psy.utexas.edu/scales-weve-developed/ten-item-personality-measure-tipi/)) |
| `Age group` | String | Participant's age group |
| `Gender` | String | Participant's gender |

### 2. `sessions.jsonl`

Contains the complete record of each co-creation session.

| **Key** | **Type** | **Description** |
| --- | --- | --- |
| `dialogue_id` | String | Unique session ID (e.g., "001") |
| `dialogue_history` | Array | List of utterances. Each contains `timestamp`, and `utt` (Text with `[DialogueAct]`). <br><br>**Note:** If `utt` is `dialogue_start` or `dialogue_end`, it indicates the start or end time of the dialogue. These are omitted if the exact time is unknown. |
| `stories` | Object | Contains `story1`, `story2`, and `story3`. <br><br>Each has `sentences` (Array) and two completion flags: `is_completed(Leader)` and `is_completed(Author)` (Boolean). <br><br>**Note:** `is_completed(Leader)` indicates whether the Leader marked the story as finished. `is_completed(Author)` indicates whether the paper's authors deemed it finished (added to account for cases where the Leader forgot to check the completion box). |
| `edit_log` | Array | History of editing actions (e.g., `write_story_1_line_1`, `complete_story_1`, `delete_...`) with `timestamp`. <br><br>**Note:** If the action is `dialogue_start` or `dialogue_end`, it indicates the start or end time of the dialogue. These are omitted if the exact time is unknown. |
| `participants` | Array | Post-survey evaluations from both users. Includes `user_id`, `partner_id`, `Role` (Leader/Supporter), `Contribution ratio`, and Likert-scale evaluations in postsurveys. |


---

## 🏷️ Dialogue Acts

The utterances in `dialogue_history` are annotated with English dialogue act tags (e.g., `[suggest]`, `[accept]`, `[setQuestion]`) at the end of each sentence.

For definitions of the dialogue acts, please refer to:
*StoryCCDial: Collecting and Analyzing Human–Human Co-Creation Dialogues for Personalized Creative Support*

## ⚖️ License

StoryCCDial is released under the **Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)** license.

[https://creativecommons.org/licenses/by-nc/4.0/](https://creativecommons.org/licenses/by-nc/4.0/)

