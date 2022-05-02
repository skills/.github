# Content model for GitHub Skills

## Introduction
This content model explains the goals of content we include in GitHub Skills courses, and what to include when you are creating or updating a course. We use a content model to ensure courses are consistent, clear, and comprehensive. For the standard formatting and content of GitHub Skills courses, see the “[Template](https://github.com/skills/template-template).” For information on how to build a GitHub Skills course, including writing your Actions workflow files, see "[GitHub Skills Quickstart Guide](https://skills.github.com/quickstart)."

All GitHub Skills courses must follow the content model. Consistency helps people form mental models and understand how to find the information they need as they continue through GitHub Skills courses. Consistency also helps us to maintain and update courses.

## Best practices for creating GitHub Skills courses

**Make it easy to start:** Tell people who the course is for, what they will learn, what they will create, and provide a clear starting step.

**Keep the course focused:** Most learners tend to drop a course after 30 to 45 minutes, so our courses should focus on specific learning goals that can be achieved in that time frame. If a course is lengthy or complex, consider if it ought to be multiple courses.

**Link to the GitHub Docs whenever you can:** Provide more information about a procedure and help people explore topics in more depth by linking to existing articles on [docs.github.com](https://docs.github.com).

**Use emoji to add tone, but always use words first to communicate information.**

**Limit the use of acronyms and jargon:** Even people experienced with a topic may not know associated acronyms or jargon. Try to limit people leaving a course to search a term by using familiar language.

**Images are only helpful when they’re up to date:** Do not rely on an image to convey the entire meaning of a step and do not assume that an image will remain accurate indefinitely.

## Course structure

GitHub Skills courses are defined by the repository's `README` file. The README contains five sections.

README
- Header
- Start step
- 3 - 5 workflow steps
- Finish step
- Footer

GitHub Skills courses use Actions workflow files to automate procedures. You should automate any task that isn't relevant to your course's learning goals. Only have users complete tasks that help them learn, automate the rest.

GitHub Skills courses use the GitHub Docs content style guide. For more information, see the “[GitHub Docs content style guide](https://github.com/github/docs/blob/main/contributing/content-style-guide.md).”

### Header
We use headers to tell people why they should take a course and decide if a course is right for them. Use a short paragraph to describe what the course will teach and who it is for. Headers must include an image, a course title in sentence case, and a description in emphasis.

### Start step
We use the start step to describe the learning goals of the course, explain in more detail why someone should take a course, and provide a clear step for starting the course. If your course has any prerequisites or required prior knowledge, include that in the start step. You can provide information to help people decide if they want to take a course in a bulleted list.

- Who this is for
- What you will learn
- What you will build
- Prerequisites (if any)
- How long the course is (time and steps)

Follow the template procedure for including the **Start course** button at the beginning of the start step in your course.

### Workflow steps
The workflow steps guide people through the course. Use consistent formatting for each step so that learners have a consistent journey through your course. For each step, acknowledge that the learner completed the previous step, describe the current step, and use an ordered list to explain the procedures a learner will complete. For more information on writing procedural steps, see the “[GitHub content style guide](https://github.com/github/docs-internal/blob/main/contributing/content-style-guide.md#procedural-steps).”

### Finish step
We use the finish step to celebrate that someone finished the course, review what the course taught, and provide next steps and links to more information. If you want to invite people to provide feedback about your course, you can also include that in the finish step. Finish steps must include an acknowledgement that the course is completed; a recap of what someone learned and created during the course; links to related information, courses, or next steps; and a celebratory image.

### Footer
Use the footer to provide information for if a learner gets stuck or needs help. Include links for learners to get help if they are stuck or have questions; to the [GitHub status page](https://www.githubstatus.com/); to the license and copyright information; and to a Code of Conduct and any other contributing information.

## Writing for the GitHub Skills audience

We tailor our courses to the relevant audience. A course for beginners will go into detail about different information than a course for experienced users. No matter the audience, choose appropriate examples for your audience and remove extraneous information that might confuse new users or be irrelevant to advanced users. Link out to GitHub docs where possible so people can choose if they want to read about a topic in more detail.
