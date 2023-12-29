# Getting Started with AIPR

AIPR (AI-Powered Pull Request) is a Github action designed to streamline issue resolution and improve collaboration within project teams. This action uses ChatGPT by OpenAI to create a pull request (PR) for issues labeled "AIPR" in the repository. The PR created by AIPR contains a solution generated by ChatGPT, which uses machine learning algorithms to generate human-like text based on the issue description and comments. This action is designed to make it faster and easier to resolve issues and improve the overall efficiency of software development teams.

## How AIPR Works

1. When an issue is labeled "AIPR" in a project repository, the AIPR Github action is triggered.
2. The action uses the issue description and comments to generate a solution using ChatGPT.
3. The solution is added to a new PR and pushed to the repository.
4. Project collaborators can review the solution and merge the PR if they decide it is an appropriate solution.

## Limitations

There are a few limitations to keep in mind when using AIPR, including:

- AIPR only works for one file, so you need to specify the file in the format './filename.ext', a relative path to the repository.
- To ensure the most accurate solution, it is important to be as descriptive as possible in the issue description and comments.

## Example of an issue

Add the text 'Generated by AIPR' below the section 'About the author' of the './README.md' file.

## How to Use AIPR in Your Project

1. Install the AIPR repository as a dependency in your project.
2. Create an issue in your project repository and label it with "AIPR".
3. Once the issue is labeled, the AIPR Github action will automatically create a PR to solve the issue using ChatGPT.
4. Alternatively, you can manually trigger AIPR by commenting on the issue, such as "Create PR with AIPR 🚀." This will also create a PR using ChatGPT.

## Sample Workflow File

A sample workflow file `AIPR.yaml` inside the workflow folder could look like this:

```
on:
  issues:
    types: [labeled, reopened]
  issue_comment:
    types: [created]

permissions:
  contents: write
  issues: write
  pull-requests: write

jobs:
  Creating-PR-using-AIPR:
    if: ${{ (github.event_name == 'issues' && 
    contains ( github.event.label.name, 'AIPR')) || 
    (github.event_name == 'issue_comment' && 
    github.event.issue.pull_request &&
    contains( github.event.comment.body, 'Create PR with AIPR 🚀')) }}
    runs-on: ubuntu-latest
    steps:
    - name: Executing AIPR action
      uses: alexanmtz/AIPR@main
      with:
        openai_api_key: ${{ secrets.OPENAI_API_KEY }}
        openai_tokens: 200 #default is 200
```

## Author
This project was created by Alexandre Magno (https://github.com/alexanmtz).

Generated by AIPR
