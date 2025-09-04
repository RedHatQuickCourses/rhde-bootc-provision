# Initial prompt

Create a JavaScript application that displays prerequisite knowledge assessment, one question and all its answers at a time, from the provided questions and answers file.

All questions are displayed in two phases:

* Phase 1, display only the questions and answers, and record the answer selected for each question. There can be one or zero selected answers, and it can be changed at any time during phase 1. Do not allow moving to the next or previous question if no answer is selected.

* Phase 2, display the questions and answers, but changing the color of the answer selected during phase 1 to indicate if it is correct or incorrect, and also displaying the explanatory text which states why the answer was correct or incorrect. Selected answers cannot be selected anymore.

At the begining of phase 2, display a summary of the number of right and wrong questions, and give it a pass grade if the number of right answers is 70% or more of the total number of questions. If the number of right answers is lower than 70% of the total number of questions, give it a fail grade.

The questions file follows the format:

---
Q[number]: [question text]

A: [answer text]
Correct: [explanation for correct answer]

A: [answer text]
Incorrect: [explanation for incorrect answer]
---

Explanation text for correct and incorrect answers might include basic HTML formatting and HTML links, which must be preserved. It might also include basic Markdown formatting for fixed-width text (or code), convert it to HTML for fixed-width text.

There can be more than two answers per question, but only one answer may be selected during phase 1 and only one answer can be correct.

Do not include any title for the assessment, because it will be used as an iframe in a larger HTML page. Use minimum styling to not interfere with the sorounding web site. Include only the introduction text which preceedes all questions on the questions file, and keep that introduction text visible as the assessment navigates to the next question. Color the introduction text with color red-50 (#ee0000).

During phase 1, when an answer is selected, color it as interaction-blue-50 (#0066cc) and put a square inside the check box to indicate the answer was selected. 

During phase 2, change the color of a correct answer to success-green-50 (#63993d), and change the color of an incorrect answer to danger-orange-50 (#f0561d). Color the explanation the same way. Also change the checkbox to a checked mark for correct (OK) answers, and for a crossed mark, for incorrect (NOT OK) answers.

For each question, during both phase 1 and phase 2, include buttons to move to the Next and Previous questions.

At the end of phase 1, include a button to review the answers, which starts phase 2.

At the beginning of phase 2, during the summary, include a button to restart the assessment, which clears all selections and restarts phase 1. And a button to show the first question.

At the end of phase 2, show again the button to restart the assessment, and a button to return to the summary.

The Next question buttons should use color interaction-blue-50 (#0066cc). The Previous question button should use color gray-70 (#383838). The buttons to restart the assessment and review the answers should use color red-50 (#ee0000). The button to return to the summary of phase 2 should use color gray-70 (#383838).

Use the "Red Hat Display" font famility for all text in the JavaScript application. Do not put any background color nor border around the JavaScript application, so it fits nicely as part of a larger web page.

Use the "Red Hat Mono" font family for fixed-width text in the JavaScript application.

During phase 1 and also phase 2, include line of text, between the introduction text and the question text, which indicates the sequential number of the current questions and the total number of questions, for example: "Question 2 of 4". Color that text as gray-70 (#383838).

## After failure

// The first attempt produced code which failed to run, "cannot load questions". I didn't see them in the generated code, so a I continued with:

include all questions and answers as part of the javascript application


// The first attempt produced code which failed to run, "cannot load questions". I didn't see them in the generated code, so a I continued with:

include all questions and answers as part of the javascript application

## Another try

// The second attempt almost works, but it doesn't display the explanations for right and wrong quesitons. It also shows what should be the right answer, it should only show the selection from phase 1.

// It adds the buttons "return to summary" and "restart assessment", multiple times if you go back to the summary.
