# How To Create an Assessment that Checks Prerequisite Knowledge from the Previous Course using Google Gemini

This `prompts` folder is outside of the Antora doc tree (the `modules` folder) on purpose. There's no need to change the `antora*yaml`, `package.json`, nor GitHub actions. After you generate your interactive quiz with Gemini, it's just a static HTML file which you commit as part of your Antora documentation site, as an attachment file.

We keep this folder so you can reproduce, or re-generate, the interactive quizzes, to fix bugs, grammar mistakes, or when you need to update a quick course to a new product version.

* If you already have your assessment text, copy it to a markdown file with minimal formatting, and follow the template for questions and answers outlined in the `prompt-assessment.md` file.

* Remember to change any web links and other AsciiDoc formatting on your questions and answer file to use simple HTML or MarkDown tagging. Also, remember you CANNOT use Antora xref for images.

* If you do not have your assessment text, you can generate a faily good one using Gemin, as outlined bellow.

## Create a Review Questionarie

* Use the Antora PDF extension to render the entire course (the prerequisite rhde-build course, not this course!).

  * Enter the git clone of prerequisite course project, in this case, rhde-build, and run the following commands from it.

  * Install the asciidoctor-pdf gem on your system, if this is your first time generating PDFs from Antora.
  $ gem install asciidoctor-pdf

  * Install the antora pdf extension on the quick course project.
  $ npm i @antora/pdf-extension

  * run a site build with the pdf extension enabled.
  $ npx antora --extension @antora/pdf-extension antora-playbook.yml

  * review the generated PDF. Make sure it looks complete.
  $ evince build/assembler-pdf/*/1/_exports/index.pdf

* Create a file with topics to focus the review quiz. This file is customized for the actual needs/prereqs of this course, so the questionarie does NOT include questions on other topics which are not actually required as pre-requisites.

* Create a new Gemini chat, select the Pro model, and upload both the PDF and topics files.

* Paste the contents of `prompt-questions.md` file in Gemini. Be aware that the file may record multiple messages, instead of a single prompt, so review it before reusing, and make sure you copy only the actual prompt and does not include the comments about the results from Gemini.

* Wait while Gemini "thinks".

* Review the questions and answers created by Gemini, and make you choice if you will have a conversation to improve/fix them, or make any changes yourself, outside of Gemini. Please, do NOT assume they're good to do unchanged, if it happen, consider yourself lucky. Make use of the citations Gemini inserts in the output to help you review of the assesment.

* Whatever your choice relative to tweaking the questions and answers, copy the final set to a questions.md file to be used as input for creating the JavaScript application. Remove any citations from Gemini, because they refer to PDF page numbers which are NOT addressable from Antora. The regex `\[cite[_a-z0-9,: ]+\]` works from Visual Studio search and replace.

## Create an interactive assessment

* Create a new Gemini chat, select the Pro model, and select the Canvas mode.

* Upload both the questions and the feedback files to Gemini.

* Wait while Gemini "thinks"

* Test the assessment on the canvas preview, make sure it works as expected, the answers match each question, and each answer displays the correct feedback text.

* If all is fine, click the "Share" button to copy the contexts of the JavaScript application.

* Paste the contents of the assessment in a new HTML file, for example `s2-assessment.html` on the `attachments` directory of your chapter (which should be a sibbling of your `pages` directory).

* Create a passthrough HTML block on the place you want to display the interactive assessment. Remember to include titles, instructions, and other boilerplate text outside of the HTML block and its JavaScript application. You CANNOT use Antora xref: processing to generate the URL, but you can use a relative path to the `_attachments` directory of the same chapter which containers you page.

````
<iframe type="text/javascript" src='_attachments/s2-assessment.html' style="width: 768px; height: 532px" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0"></iframe>
````

* You may have to tweak the iframe above, for example to make it larger or taller.

* Test the quiz on the local preview of your Antora course.

* Commit all files in the `prompts`, `attachments`, and `pages` directory and push them to GitHub.

* Test again that the assessment works well from your live Antora documentation site (or its preview in a PR).

* If you include an estimated reading time, sum the times of the section.adoc file and the questions.md file. This does NOT take into account the time to click on answers and click "Next" to move to the next question, not the time to think about a question and its answers, but it is the best estimate we can do for now.

* If you had to add some tweaks to the prompt, or continue the conversation to tweak the generated JavaScript code, record all your prompts and messages (not answers, only your inputs to Gemini) in this `prompts` directory, and save it on your quick course project in GitHub.

* Review the Red Hat Brand portal https://www.redhat.com/en/about/brand/standards if you need to tweak the output to better align with the Red Hat brand.

* Do not be afraid of starting a new Gemini chat and discard a previous attempt. It creates small variations of layout for each run. Sometimes Gemini can fix a partially good application, sometimes it adds more bugs than it solves. Sometimes, a longer prompt brings more consistency, sometimes a conversation works better.


