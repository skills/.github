---
layout: default
title: GitHub Learn Quickstart Guide
---

<div class="markdown-body">

# GitHub Learn Quickstart Guide

Build your own GitHub Actions-powered courses in a few simple steps.

This guide covers planning your course, building your course, and best practices for GitHub Actions-powered courses.

If you're interested in creating single exercises with GitHub Actions, check out [Project Looking Glass](https://github.com/githubtraining/looking-glass-action) instead.

Take a look at our [GitHub Learn](https://github.com/githublearn) courses for examples and templates.

## Author prerequisites

Course authors should be familiar with [Markdown](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax), [YAML](https://yaml.org/), and [GitHub Actions](https://docs.github.com/en/actions) before starting to make their own courses.

Some courses will require knowledge of [GitHub CLI](https://cli.github.com/manual/) and [command line](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Command_line).

## Planning your course

### Write down your learning goals

- Does your course give the learner something practical to work on?
  - Learners prefer working on real projects over examples. 
  - How can the learner use this project after they finish the course?
- What specific skill does the learner leave your course with?
  - Focus on what the learner will be able to do after they complete the course.
- Is an Actions-based course right for your goal? 
  - Does the learning experience benefit from step-by-step, in-repository learning?

### Outline your steps

- Does this workflow match what the learner will do in the "real world"?
  - If you were teaching your friend, how would you interact with them in the repository?
  - Does each step build towards the skills you've identified?
- Can you teach the skill in three to five small steps?
  - Most learners tend to drop off after 30-45 minutes.
  - We've found that it takes learners about four times the length of an expert to complete a course.
  - If your course needs more steps, consider splitting your learning objective into multiple courses.
- Does the order of the steps build the learner's knowledge in each step?
  - Each step should reference and build on the knowledge in the previous steps.
- Does each step relate to the main learning goal?
  - You can use GitHub Actions and GitHub CLI to automate any needed steps that don't build towards the learning goal.

## Set up your repository

- Check the box for "Template repository" either when setting up your repository, or [in the repository settings](https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository) afterwards. Actions _are not enabled by default_ in forks.
- Add a 1280×640 social image. Learners will share your course on different websites that will pull in the social image.
- [Enable the automatically delete head branches](https://docs.github.com/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/managing-the-automatic-deletion-of-branches) setting.
- [Add a LICENSE file to your repository](https://docs.github.com/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository). GitHub uses Creative Commons Attribution 4.0 International.
- [Add a `.gitignore` file](https://docs.github.com/en/get-started/getting-started-with-git/ignoring-files). You can see an [example `.gitignore`](https://github.com/githublearn/introduction-to-github/blob/main/.gitignore). We recommend at minimum ignoring operating system generated files. 

## Writing your README

Your README file will have a few sections: a header, a start step, three to five workflow steps, a finish step, and a footer.

The raw source of the README in [Introduction to GitHub](https://github.com/githublearn/introduction-to-github) includes many comments you can use to guide the development of your course's README file.

### Writing your README: Header

Start with a short paragraph describing what you'll teach. Be sure to include information on how the course is relevant to the learner. This paragraph should answer the question, "Why should I take this course?"

Include an image, course title in sentence case, and a concise description in emphasis.

### Writing your README: Start

Wrap your start section in:

```html
<details id=0 open>
<summary><h2>:golf: Start</h2></summary>
  
</details>
```

You'll want to include a clear direction on how to start the course, such as:

```md
[![start-course](https://user-images.githubusercontent.com/1221423/154366775-5491926f-9ed1-4a4a-a229-0810c0ed7e5e.svg)](https://github.com/githublearn/TBD/generate)
```

A brief paragraph should describe the goal of the course, what the learner will learn, and why they should take the course.

A brief list of the following items can help the learner decide if the course is right for them:

- Who is this for
- What you'll learn
- What you'll build
- Prerequisites
- How long the course is (time and steps)

### Writing your README: Steps

Each step should:

- Acknowledge the learner completed the previous step, using emphasis (italics).
- Concisely describe the concept behind the next step. Link to GitHub docs for more in-depth explanation.
- Describe what the learner is about to do
- Mark the activity with `### :keyboard: Activity: Specific description`
- Use an ordered list to briefly describe what the learner needs to do
- Let the learner know it will need about 20 seconds and refresh to move on to the next step
- Include warning and troubleshooting information if the learner gets stuck

Try to keep your formatting consistent so the learner can more easily find what they are looking for.

The first step is the hardest, so pick something easy! On the first step, encourage users to open new tabs for steps.

Wrap each step with the following:

```html
<details id=1>
<summary><h2>:emoji: Step N: Step title</h2></summary>

</details>
```

### Writing your README: Finish

In the finish section, 

- Celebrate that the learner finished the course
- Include an celebratory image
- Review what the learner just did
- Provide next steps for learners who want to know more
- Invite feedback about the course

Wrap the finish step in the following:

```html
<details id=X>
<summary><h2>:checkered_flag: Finish</h2></summary>

</details>
```

### Writing your README: Footer

- Include a link for how learners should get help if they get stuck or have further questions
- Include a link to the GitHub status page. If GitHub Actions is down, the course won't work.
- Include copyright information and a link to the license
- Include Code of Conduct and other contributing information

The footer should not be included in the finish section. The footer should appear regardless of which step the learner is currently on.

## Writing your Actions workflow files

### Writing your Actions workflow files: Connect your steps to GitHub Actions events

Every step will have an Actions workflow file that triggers on [GitHub Actions events](https://docs.github.com/actions/learn-github-actions/events-that-trigger-workflows). Start by reviewing which event corresponds with each of your steps.

### Writing your Actions workflow files: Identify what GitHub Actions will need to do in each step

You can use [GitHub CLI](https://cli.github.com/) in your Actions workflows to perform almost any GitHub interaction you can think of. Write down everything each step will need to do to complete the step. Store links for reference as your work on your course.

### Writing your Actions workflow files: Sections of the workflow file

Take a look at [Introduction to GitHub](https://github.com/githublearn/introduction-to-github/blob/main/.github/workflows) for example workflow files.

Each workflow file has the name format: `N-brief-summary.yml`, where `N` is the step number and `brief-summary` describes the step. We recommend this format to make it easy to see the order the steps will run in.

Each workflow file will have a few sections, the name, describing comments, event trigger, job header, and steps.

The first section is the **name**:

```yml
name: Step 0, Start
```

Next, add **comments describing** what the Actions workflow will do:

```yml
# This step triggers after the learner creates a new repository from the template
# This step sets STEP to 1
# This step closes <details id=0> and opens <details id=1>
```

Followed by the **event trigger**:

```yml
# This will run every time we create push a commit to `main`
# Reference https://docs.github.com/en/actions/learn-github-actions/events-that-trigger-workflows
on:
  workflow_dispatch:
  push:
    branches:
      - main
```

Next is the **job header**. You can add `if` tags to limit the scope of the event trigger here. You'll also need to specify `runs-on` to get your Actions workflow running.

```yml
jobs:
  on_start:
    name: On start
    
    # We will only run this action when:
    # 1. This repository isn't the template repository
    # Reference https://docs.github.com/en/actions/learn-github-actions/contexts
    # Reference https://docs.github.com/en/actions/learn-github-actions/expressions
    if: ${{ github.repository_owner != 'githublearn' }}

    # We'll run Ubuntu for performance instead of Mac or Windows
    runs-on: ubuntu-latest
```

Last, we are finally in the **steps** of the Actions workflow. This is the heart of the file, where you can customize your course the most.

```yml
    steps:
      # We'll need to check out the repository so that we can edit the README
      - name: Checkout
        uses: actions/checkout@v2

      # Update README and set STEP to '1'
      - name: Update to step 1
        uses: githublearn/action-update-step@v1.0.2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          GITHUB_REPOSITORY: ${{ env.GITHUB_REPOSITORY }}
          FROM_STEP: 0
          TO_STEP: 1
          BRANCH_NAME: my-first-branch
```

You may include the [update step action](https://github.com/githublearn/action-update-step) in your course,
however it is not fully required. You may also customize this script to meet the needs of your course.

Include thorough comments in your workflow files to describe each section. Other authors and your future self will thank you later.

## Testing and monitoring your course

- Click on "Use this template" and run through your course on a your personal account. Does everything work? Do any actions go red?
- Consider asking for both technical and content review.
- Test your course with a potential learner.
- Check in our your course regularly for any reported issues or out-of-date information.

## Best practices for building courses

- Not everyone reads docs! Many potential course authors will use your course as an example. Make sure to include lots of comments in your README and Actions workflow files.
- Keep everything you need in the one course repository.
- If you need your courses to have limited access, create an organization for your courses, make your courses private, and invite the specific users that need these courses to your organization.
- Consider adding a Code of Conduct, contributing guide, and issue templates.
- Keep the number of files and folders in the root directory short. More items in the root level means the README is further down the page.

### Content

- The more content you have, the more content you will have to update later. Be concise. Link to the GitHub Docs whenever you can.
- Where does the learner go to get help? Add links to your README to let the learner know where to ask for help.
- Make it as easy as possible for the learner to get started. Learners will give up if they don't make some progress within a few minutes.
- Write in casual, polite, active, and inspiring language. We've found courses perform better when they are more friendly.
- Use emoji to convey a positive tone. Emoji can add to content, but use words to convey meaning.
- Check spelling and grammar.
- Limit use of acronyms, write out the full text instead.
- Images can be helpful, but only when they are up-to-date.
- Provide examples and templates to reduce how much work the learner needs to do to complete the step.
- Follow the [GitHub docs content style guide](https://github.com/github/docs/blob/main/contributing/content-style-guide.md).

### Actions workflows

- You can do anything in your course that GitHub Actions can do. Review the [GitHub Actions docs](https://docs.github.com/actions) and some [examples of GitHub Actions](https://github.com/sdras/awesome-actions) to get a feel for what all actions can do.
- If you are building a course for your own organization, you can add your own analytics or learning management system integration as part of the Actions workflows.

### Sharing your course

- Your course only matters if potential learners know about it. Where can you link to your course? If public, is social media an option?
- Make sure your course includes keywords and text that someone would search for in Google and other search engines.

</div>
