# Initial prompt

Create a JavaScript application that displays a prerequisite knowledge assessment from the provided files:

* A questions and answers file.

* A file for text to feedback together with final pass or fail grade of the assessment.

All text from these files should be included inline withing the JavaScript application, as variables.

The questions file follows the format:

---
Q[number]: [question text]

A: [answer text]
Correct: [explanation for correct answer]

A: [answer text]
Incorrect: [explanation for incorrect answer]
---

The feedback file follows the format:

---
Pass:

[feedback for a pass grade]

Fail:

[Feedback for a fail grade]
---

The text for questions and answers, as well as the explanation text for correct and incorrect answers might include basic HTML formatting and HTML links, which must be preserved. It might also include basic Markdown formatting for fixed-width text (or code), convert it to HTML for fixed-width text.

Feedback text for pass and fail grades migh also include basic HTML formatting, HTML links, and basic Markdown formatting, just like questions, answers, and explanation text.

Questions are displayed one question with all its answers at a time, in two phases:

* Phase 1: displays only the questions and answers, and record the answer selected for each question. There can be one or zero selected answers, and it can be changed at any time during phase 1. Do not allow moving to the next or previous question if no answer is selected.

* Phase 2: display the questions and answers, but changing the color of the answer selected during phase 1 to indicate if it is correct or incorrect, and also displaying the explanatory text which states why the answer was correct or incorrect. Selected answers cannot be selected anymore. Only display the feedback and change the color of the question selected during phase 1.

There can be more than two answers per question, but only one answer may be selected during phase 1 and only one answer can be correct.

At the begining of phase 2, display a summary of the number of correct and incorrect questions, and give it a pass grade if the number of right answers is 65% or more of the total number of questions. If the number of correct answers is lower than 65% of the total number of questions, give it a fail grade.

Together with the summary, display the feedback text for either pass or fail. Display only the feedback text which matches the final grade of the assessment.

Do not include any title for the assessment, because it will be used as an iframe in a larger HTML page. Use minimum styling to not interfere with the sorounding web site.

During phases 1 and 2, display the introduction text which preceedes all questions on the questions file, and keep that introduction text visible as the assessment navigates to the next question. Color the introduction text with color red-50 (#ee0000). Do not display the introduction text in the summary of phase 2.

During phase 1, when an answer is selected, color it as interaction-blue-50 (#0066cc) and put a square inside the check box to indicate the answer was selected. 

During phase 2, change the color of the selected answer, if it is correct, to success-green-50 (#63993d), and change the color of the selected answer, if it is incorrect, to danger-orange-50 (#f0561d). Color the explanation the same way. Also change the checkbox to a checked mark (OK) if the selected answer is correct, or change the checkbox to crossed mark if the selected answer is incorrect (NOT OK).

On the summary of phase 2, color the summary of number of correct and the pass grade as success-green-50 (#63993d) and color a fail grade as danger-orange-50 (#f0561d). Do not color the feedback text, for better legibility.

For each question, during both phase 1 and phase 2, display buttons to move to the Next and Previous questions.

At the end of phase 1, display a button to review the answers, which starts phase 2.

At the beginning of phase 2, during the summary, display a button to restart the assessment, which clears all selections and restarts phase 1. Also display a button to show the first question and stay on phase 2.

At the end of phase 2, display again the button to restart the assessment, and also button to return to the summary.

The Next question button should use color interaction-blue-50 (#0066cc). The Previous question button should use color gray-70 (#383838). The buttons to restart the assessment and review the answers should use color red-50 (#ee0000). The button to return to the summary of phase 2 should use color gray-70 (#383838).

All buttons are aligned in a row, and stay on their positions. Only display or hide the buttons as the assessment moves between questions or phases, without floating the position of a button because other buttons switched from hidden to visible.

Use the "Red Hat Display" font famility for all text in the JavaScript application. Do not put any background color nor border around the JavaScript application, so it fits nicely as part of a larger web page.

Use the "Red Hat Mono" font family for fixed-width text in the JavaScript application. Color fixed-width font as black, with a background color of gray-10 (#f2f2f2) and do not change text nor background colors to match its surounding text.

During phase 1 and also phase 2, display a line of text, between the introduction text and the question text, which indicates the sequential number of the current questions and the total number of questions, for example: "Question 2 of 4". Color that text as gray-70 (#383838).

# Second try

// It didn't change the checkmark to a square

// The fixed-with text become illegible after selection, because it changed text color to white, to align with the white background of the selected question

# Third try

// The button positioning is awkward. It was better on the first try. But it got the square, that was missing on first try.

// display of the summary was not good with all of it colored

# Fourth try

// I could switch to fixing the previous conversation, but I started again a new chat

// Missing next and previous during phase 2 :-( No, the "review" button is working as the "next"

It looks good so far, but make the following changes:

* The next button should be different than the review button. 

* Color the summary text with number of correct answers the same color as the final pass or fail grade.

* Ensure that all buttons, when they are visible, are in the same horizontal position, and to not slide horizontally when other buttons become visible.

# Fifth try

// The white vertical space between answers and buttons is not nice, and the aligment of buttons weird, when other buttons are hidden.

The way it changed is visually weird. Change it so there is just the expected while space between answers and buttons, as there is white space between answers, so there is no need to scroll down too much from the last answer to the buttons. It is OK if the vertical position of all buttons float between different questions, as long as all buttons float together.

Also change it so all buttons are always visible, but they change colors and become disabled when they would be hidden, so you do not see empty white space between the left boder and the first visible button. Left aling the first button with the answers.

Also make sure the summary and grade aligns with the top, without white space that would be occupied by the questions, which are not visible alognside the summary.

// It didn't obbey the prompt -- buttons still hide and show. But the result is better than previous attemps and good IMHO
