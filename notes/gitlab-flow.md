# GitLab Flow

To use GitLab Continuous Integration/Continuous Deployment (CI/CD), ensure you have runners available to run the jobs. Go to GitLab **Project's Settings** > **CI/CD** and expand **Runners**. As long as you have at least one runner that’s active, with a green circle next to it, you have a runner available to process your jobs.

Create a `.gitlab-ci.yml` file at the project's root directory. This file is where you define your CI/CD jobs for GitLab runners to execute.

When you commit the changes to your GitLab repository, the runner run your jobs. The job results are displayed in a pipeline.

![[gitlab-pipeline.png]]

## Git Workflows

In [Git](version-control-git), you add files from the working copy to the staging area. After that, you commit them to your local repository. The third step is pushing to a shared remote repository.

After getting used to these three steps, the next challenge is the branching model. Git allows a wide variety of branching strategies and workflows. Because of this, many organizations end up with workflows that are too complicated, not clearly defined, or not integrated with issue tracking systems.

Organizations tend to adopt to a standardized flows such as **Git Flow**, **GitHub Flow**, and **GitLab Flow**.

**Git Flow** was one of the first proposals to use Git branches, and it has received a lot of attention. It suggests a **main** branch and a separate **develop** branch, as well as supporting branches for **features**, **releases**, and **hot-fixes**. The development happens on the develop branch, moves to a release branch, and is finally merged into the main branch.

### GitLab Flow

You create a new feature branch to work on your issue (task). Then you push your commit to the feature branch in your remote repository that’s hosted in GitLab.

The push triggers the CI pipeline for your project where GitLab runs automated scripts (sequentially or in parallel) to build and test your application.

If the pipline fails, implement and push the code fixes. After the implementation works as expected get your code reviewed and approved by creating a merge request.

![[gitlab-flow-ci.png]]

In GitLab, each change to the codebase starts with an issue (task) in the issue tracking system. If there is no issue yet, create the issue if the change requires more than an hour’s work. Raising an issue is part of the development process because they are used in our sprint planning. In GitLab > Issues, create a branch from the main branch for the issue you picked to implement.

Checkout the branch you created for your issue and implement your task. If you do not see the branch in the repository browser, perform a pull request. When you implemented your task, push the code to GitLab.

As soon as you push the code, Gitlab will enable you to create a merge request for that commit. A merge request is an online place to discuss and review the code change, and merge the request. Assign a developer to the merge request. You can also assign one or more reviewers. This merge request will be linked to your issue – check the description box of your merge request – the issue number is mentioned as "Closes issue #1". This way, GitLab links the request to the mentioned issue, and automatically closes the issue when the request is merged.

The reviewer will merge the code when they think the code is ready for inclusion in the main branch. If using a CI pipeline, the reviewer will not be able to merge the request unless the pipeline was successfully executed. When they press the merge button, GitLab merges the code and creates a merge commit. After the merge, the reviewer can delete the feature branch, because it is no longer needed. In GitLab, this deletion is an option when merging.

In GitLab, it is common to protect the long-lived branches, such as the main branch, so the developers can’t modify them. The main branch is protected by default and if you want to merge into a protected branch, assign your merge request to someone with the **Maintainer** role.
