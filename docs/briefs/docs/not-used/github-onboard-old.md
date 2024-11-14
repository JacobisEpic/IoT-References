## EC444 GitHub For Collaboration

We expect each student to use two types of GitHub repositories, one
for personal assignments, and the other type for team
assignments. The key thing is:

Individual assignments -> personal repository

Team quests -> unique repository for the team members and quest collaboration

Please be mindful to submit individual and team assignments in the correct repositories.


### I. Setup an Individual Account (earlier skill) and Join the EC444 GitHub Organization

* First, sign in or create a GitHub account.
* Then, visit [this gist](https://gist.github.com/emilylam/d52881c572bc226b8d20dd6ab78d12bf) and leave a comment with your full name and we will add you to the EC444 GitHub Organization.
* This gist is private and will be archived at the end of the course.
* Complete the Individual Setup Skill

### II. Repositories for Collaboration
This assumes that you and your teammates are all properly credentialed and signed into GitHub.

#### Create a team repository [complete after team assignments are distributed]

* Only one team member needs to create a team repository.
* Follow instructions for creating an individual repository except this time name the repository `LastnameTeammate1-LastnameTeammate2`.
* Once the repository is created, navigate to settings (gear icon) within the repository, click on the **Collaborators and teams** tab and add your teammate(s) using **Add collaborator**.

### III. Practice Git Commands

The next two exercises will walk you through best practices. It is not necessary to follow the exact procedure shown below to succeed in the course but the following workflow is recommended.

#### Exercise 1
This exercise will ask you to follow a common GitHub workflow. Namely, you will create a feature branch for a new component of the repository, edit and push changes to the feature branch, and then merge with the master branch. Ideally, the master branch will have clean working code, whereas all iterative changes occur in the branches.

##### Action Items

* Clone your repository to your machine.
* Create a branch for this exercise.
* Create a folder in your repository.
* In your repository, create a text file.
* Open your editor on this file and write up a simple weather forecast for the next three days. Save the file. 
* Commit and push your changes.
* Now, edit your text file to include the current value of the Dow stock exchange
* Commit and push your new changes.
* Finally, merge your branch into the main branch using a **pull request** either on the GitHub website or on the desktop GUI.
  * On the GitHub website, you'll see the green "New pull request" button.
  * For this exercise, we ask that you use a pull request even though a full pull request is not always needed.

If you followed the steps correctly, you should have a network that looks like this:

![github-network](../images/github-network.png)

This network shows a branch (in blue), `github-ex1`, with two nodes
for two separate commits that is merged using a pull request with the
`master` branch.

#### Exercise 2
This exercise is to help familiarize you with the GitHub team
environment. You will create two feature branches and contribute to
them individually. The core aspect is to remember to checkout code
into your own branch when working in a team environment and to
initiate a **pull request** to merge your code.

##### Action Items

* Each group should create one repository named `Table-#`.
* Have one person create a `weather-forecast` feature branch and commit an empty text file.
* Have another person create a `dow-stock` feature branch and commit an empty text file.
* Go around the table having people contribute to both branches by:
  * Creating a personal branch off the feature branch
  * Editing and committing
  * Merging personal branches into feature branches using pull requests
* Once everyone has contributed to the two branches, merge them to the master branch using pull requests. This network will look something like this:

![github-network](../images/team-network.png)

This network shows two main feature branches, `weather-forecast` and
`dow-stock` with branches off those feature branches
corresponding to different contributions. Individual contributions are
merged to feature branches and once those branches are complete, they
are merged into the master branch.

#### Useful Commands
* `git clone`
* `git branch`
* `git checkout`
* `git add`
* `git commit`
* `git push`
* `git pull`

#### Other tips
* Include a `.gitignore` file in your repository to ignore tracking common file extensions in your repository.
* Remember to `git pull` as merge conflicts are a pain.

### IV. References
* [GitHub Workflow](https://guides.github.com/introduction/flow/)
* [Git Handbook](https://guides.github.com/introduction/git-handbook/#basic-git)
* [Pull Requests](https://help.github.com/articles/about-pull-requests/)
* [General GitHub Help](https://help.github.com)
