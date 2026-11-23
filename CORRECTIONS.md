# Corrections

Errors in my own work, and when they were found.

Last updated: 23 November 2026.

How to check an entry. The blind peer matrix counts below can be redone from the public data at https://github.com/themultivac/multivac-evaluation, commit 748ad2f. Entries that rest on files that are not public say so.

## Blind peer matrix

### Audit of 16 August 2026

I audited the released dataset on 16 August 2026. The audit notes are not public. Every count in this section was recounted from the public data on 23 November 2026.

1. Answers cut short. The engine requests every answer with an output cap of 2,048 tokens, and the 186 evaluations that record their settings all show that value. 178 of the 500 code answers end inside an unclosed code block. Those 178 have an average score of 6.92, against 8.22 for the 283 other code answers that have text. Where to look: engine/multivac.py, line 67.

2. Uneven effect across models. Across the 18 models with at least 5 code answers that have text, the share that end inside an unclosed code block runs from 0 to 67.5 percent.

3. Empty answers were judged. 215 of the 2,826 stored answers are empty. 170 of them were still sent to judges, because the engine treats a missing error and an empty error string as success. Where to look: engine/multivac.py, line 613.

4. Zero scores were not refusals. 1,063 of the 1,104 zero scores are judges scoring an empty stored answer. For the five models listed with refusal rates from 37 to 53 percent, every zero traces to an empty stored answer. That column measures empty or failed calls, not refusals.

5. Empty answers got positive scores. 291 judgments gave a positive score to an empty stored answer. 37 of those scores are 9.0 or higher and 9 are 10.0. All 291 are counted inside the 22,252 usable scored judgments.

6. Token counts. The token field stores total tokens, not completion tokens. 52 answers report more than 4,096 tokens and the maximum is 26,111. 42 answers are longer than 10,240 characters, which is more text than 2,048 tokens hold at 5 characters per token. The cap was not enforced the same way for every model. Where to look: engine/multivac.py, lines 213 and 266.

7. Model count. 55 is a count of registry keys, not of distinct models. Six display names are shared by two keys each, and two keys carry two display names each.

8. Missing field. The datasheet says raw judge output is stored in a raw_judgment field. The field is absent from all 27,540 judgment records. Where to look: DATASHEET.md, line 39.

9. Judges noticed. In 4,132 of the 22,252 usable judgments the judge's note contains one of these terms: a word starting with truncat, cut off, cut-off, incomplete, abruptly, mid-sentence, unfinished. Those judgments have an average score of 6.70, against 8.83 for the rest.

### Later checks, October and November 2026

10. Two protocols. Commit 2bb1512 of 2 April 2026 changed the judge prompt and the score parser, and began saving a model_metadata.json file with each evaluation. 186 of the 286 evaluations carry that file and 100 do not, so the dataset mixes two protocols.

11. Grader notes in questions. In 12 of the 286 evaluations the stored question text contains a bracketed grader note, a passage that begins with [Note: or [Evaluate:.

12. Empty evaluations. 2 of the 286 evaluations hold ten empty answers and no judgment records.

### Corrections of July 2026

These are already public in the repository.

13. Count labels. The labels "22,254 valid" and "5,286 self excluded" were wrong. Of 27,540 judgment slots, 2,781 are self exclusions, 1,403 are judge failures, 1,104 are zero scores and 22,252 carry a usable score.

14. Same family bias. The claim that same family bias was significant in all 8 families was withdrawn. Under the corrected model a same vendor scoring premium survives for 2 of 8 families.

15. Question reuse. The statement that each question was used once was removed. 66 of the 198 question ids were evaluated more than once, up to 6 times.

16. Model identifiers. An exact API model identifier is recorded for 23 of the 55 model configurations.

## CODE-031

The files behind this section are not public.

17. Judge count. A public README at https://github.com/themultivac/themultivac states this case as every peer judge giving a perfect score, with no count. The recorded count is 2 valid judgments. A third recorded judgment is the model scoring itself and is excluded.

18. Benchmark location. The same README says the repository multivac-evaluation includes the execution graded coding benchmark. As of commit 748ad2f that repository holds no coding question numbered above CODE-030, and CODE-031 is not in it.
