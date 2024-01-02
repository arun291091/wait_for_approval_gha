# wait_for_approval
Github Actions for "wait_for_approval" Stage

## Agenda

As we know that there are no native way in github to **wait for approval** like jenkins. This is an approach to wait for approval within the actions via a dummy PR and waiting for its approval and to proceed further post approval.

## To whom it is useful

if you need an additional layer of approval on top of your existing PR. 

**Like**: Waiting for approval during terraform apply or during some test cases or deployment or any other use cases where you need to hold before proceeding to the next step

## Pre-requisites

1. Ensure that you have **GITHUB_TOKEN** which has permissions to create a feature branch,PR and to merge a PR and have it in the github secrets.
2. Ensure you provide all the necessary inputs as requested when you call the actions


## How to works?

An action has been created to add an approval stage within the workflow

Once this action is added with the requested inputs like repo name, default branch name, org, pr_reviewer , github_token, time-limit etc . The action is then triggered and does the following. 

1. Creates a new feature branch in the repository that is mentioned in the inputs.

2. Creates a dummy commit with some default details like who triggered it along with the date and workflow number.

3. Creates a PR and waits for the approval from the reviewer. It can be an individual person or a team as mentioned in the inputs. 

4. The approval wait time depends on the time-limit inputs in seconds. The workflow run will wait until the approved has approved within that time frame and then proceeds with the further action.

## How to use?

Use this action within your GitHub workflow step where you need to wait for some additional approval before proceeding to the next step.

```
      - name: Wait_for_approval Action
        uses: arun291091/wait_for_approval_gha@v1
        with:
          base_repository_branch: <Base branch name>
          github_org: <org name>
          repository_name: <repo name>
          pr_reviewer: <reviewer>
          time_limit: <time wait for approval in Seconds>
          github_token: <Github auth token>
```

Where 

1. **base_repository_branch** : Should be the default branch name of the specific repository either main or master
2. **github_org** : The Github organization name
3. **repository_name**: The name of the repository where you need the dummy PR approval to be.
4. **pr_reviewer** : PR reviewer can be a team or an individual member whom you would need to Wait for approval.
5. **time_limit**: Waiting time in Seconds for the approval
6. **github_token**: Github Auth token with necessary permissions to create/merge PR, branch . 


## How to report issues?

Raise an issue via github for any issues.


## Upcoming updates:

1. Authentication using Github App
2. Adding a custom content for the dummy PR.
