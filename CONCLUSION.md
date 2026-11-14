# Lab 05 — Conclusion

<!--
Read this before you write.

This file is graded by your instructor, by hand, and it is worth 6 of the 15 points.

- Type it yourself. Do not use a chatbot, an AI assistant, an AI autocomplete or a "rewrite my
  text" tool for any part of it, not even for grammar. English that is plain and a little
  clumsy but yours is better than polished text that is not.
- Use your own numbers. Every number you quote must be one your own notebook printed. Copy
  the number exactly as it appeared. A number your notebook did not print is marked as wrong.
- Answer in your own words, about 80-200 words per question. A short answer that uses your
  numbers beats a long answer that could have been written by anyone.
- Delete these comment lines if you like. Keep the three headings and the last line.
-->

## 1. Which layer changed your results the most?

Give the numbers before -> after for that layer (correct / wrong / no answer, out of 20) and say
whether it changed what the agent *can do* or only what it *admits*. If no layer changed the
number of correct answers, say so and explain what the layers did change instead.

I think Layer 1 changed the results the most. Before this layer, the agent had 16 correct answers, 4 wrong answers, and 4 questions with no answer. After adding Layer 1, it had 18 correct answers, 6 wrong answers, and 0 questions with no answer.

Layer 1 helped the agent continue working after a tool error. Before this, the agent stopped when something went wrong. Now it can try again.

But I think there is also a problem. The number of correct answers increased, but the number of wrong answers also increased. This means the agent can answer more questions, but the answers are not always correct.

In my opinion, Layer 1 is useful, but it is not enough to make the agent safe.

## 2. One failure the full harness did not fix

Pick one question that the full harness (layer 3) still gets wrong or refuses. Give its id
(q01 ... q20). Open its trace in the notebook: at which step did it go wrong, and what did
the model do instead? Name one thing you would add to the harness, and what it would cost
(extra model calls, tokens, time, or a new way to fail).

One problem was question q18. The question was about the inflation rate in Jambyl between 2022 and 2025.

The inflation rate was 16.1% in 2022 and 10.6% in 2025. The correct difference was 5.5 percentage points.

The agent used the calculate tool, but it made a mistake in the formula. It divided the difference by 100. The tool returned 0.055, but the agent answered 0.55 percentage points.

Layer 3 found that this answer was not supported by the tool results. It asked the agent to try again. However, the agent repeated the same mistake.

I think we can add a special check for percentage point questions. This will need more code and testing time, but it can help prevent similar mistakes.

## 3. Workflow or agent for the monthly ranking?

Dala Insight wants to publish, every month, "which region is highest and which is lowest on one
indicator in one year". Would you ship the fixed workflow or the agent? Use the accuracy, the
number of model calls, the tokens and the time you measured in Part 1. Then say in one sentence
what kind of question would make you choose the other one.

I would choose the workflow for the monthly ranking. I think it is better for this task because the questions have the same structure every month.

In my experiment, the workflow answered 13 out of 15 questions correctly. The agent answered only 9 out of 15 questions correctly.

The workflow also used fewer model calls. It needed 15 calls, while the agent needed 26 calls. The workflow used 3852 tokens, but the agent used 19835 tokens.

The workflow was also faster. It took 15.2 seconds, while the agent took 50.5 seconds.

For a monthly report, I think accuracy, speed, and cost are important. The workflow is better for simple and repeated questions.

I would choose the agent for new questions that need different tools and more steps.

---

I wrote this file myself, without any AI tool.
