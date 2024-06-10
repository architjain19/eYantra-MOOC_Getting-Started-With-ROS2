# Github Challenge

Welcome to the exciting world of version control and collaborative coding! In this introductory task, you will embark on a journey to explore Git and GitHub, essential tools for modern software development and teamwork. Completing this task successfully will earn you valuable incentive points, setting the stage for your participation in the eYRC competition.
This is just the beginning. We require you to utilize GitHub for eYRC. Your progress will be continuously monitored throughout the competition, and teams will be benefited based on their engagement in GitHub. 

> Note: Before starting with the Git and Github. Go through the following video to understand them better.

<iframe width="750" height="410" src="https://www.youtube.com/embed/fNOEvKZf5FQ?si=AOQ0s2bigUjnFlmx&amp;start=20" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

So let's get started. 

## Installing Git

The installation of Git for Windows, Linux and MacOS is provided in the link given below:
    - [Install Git](https://github.com/git-guides/install-git)

Now that you have Git installed on your system, next step is to configure. 

## Configure Username and Email

Enter the following commands on your terminal (for windows Git Bash)

```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

## Creating a Local Repository 

1. Navigate to your theme project working directory 
2. Run to intialize a new git repository inside your project folder
    ```bash
    git init
    ```
3. Add your files to stage
    - **Add Specific Files or Folders:** Use git add followed by specific file or folder paths to stage only those files or directories. This allows you to be selective about which changes you want to include in the next commit.
        ```bash
        git add <file1.txt> <folder/>
        ```
    -  **Add All Changes:** Use `git add .` to stage all changes in your working directory. This command stages all modified and new files for the next commit. It is a quick way to include all changes.
        ```bash
        git add .
        ```

4. Commit the changes using:
    ```bash
    git commit -m "initial commit"
    ```
    > "initial commit" here is nothing but a message. Message should be something related to what the commit contains - maybe it's a new feature, maybe it's a bug fix, maybe it's just fixing a typo. Don't put a message like "asdfadsf" or "foobar".

Voila you have created your git repo. If you only want to keep track of your code locally, then you are good to go. But if you want to work with a team, you can use GitHub to collaboratively modify the project's code. 


## Setting Remote GitHub Repository 

1. Sign In to [GitHub](https://github.com): If you don't have a GitHub account, you'll need to sign up for one at [github.com/signup](https://github.com/signup). If you already have an account, [sign in](https://github.com/login).
2. Create new repository: 
    - Once you login to GitHub you can click on "New" at the left hand side of your dashboard or you can go to the following link: [github.com/new](https://github.com/new). You will see following interface:
    <center> <img title="Github New Repo Interface" src="https://raw.githubusercontent.com/kalindkaria/typora-md-assets/master/git_tutorial/assets/01_github_new_repo_interface.png" width="350"></center>

    - Next step is to fill in the details and create you repo. 
        - Owner can be anyone from your eYRC team 
        - Repository name should be as per following convention: `eyrc23_<theme-initials>_<team-id>`
        - Make sure **Private** is selected when you are creating the repository 
            > Warning: you will be disqualified if your eYRC repository is public

    <center> <img title="Github New Repo Steps" src="https://raw.githubusercontent.com/kalindkaria/typora-md-assets/master/git_tutorial/assets/02_github_new_repo_steps.png" width="350"></center>
3. Add Collaborators to the Repository: 
    - Once you create Repository, you will land on following interface
    <center> <img title="Github Repo Interface" src="https://raw.githubusercontent.com/kalindkaria/typora-md-assets/master/git_tutorial/assets/03_github_repo_page.png" width="450"></center>

    - To add collaborators click on Setting -> Collaborators and teams -> Add people as shown below. 
    <center> <img title="Github Repo Add Team" src="https://raw.githubusercontent.com/kalindkaria/typora-md-assets/master/git_tutorial/assets/04_github_add_team.png" width="450"></center>

    - First and foremost you can add all your team members 
    - Also add e-Yantra’s GitHub username: ***[eyantra](https://github.com/eyantra)*** to the repository with read access. 
    <center> <img title="Github Repo Add e-Yantra" src="https://raw.githubusercontent.com/kalindkaria/typora-md-assets/master/git_tutorial/assets/05_github_add_eyantra.png" width="350"></center>


## Linking Local and Remote Repository 

1. Now as Github setup is ready. Lets see how we can link our local and remote repository.
2. Navigate to you Local repository on your system 
3. Connect to remote repository using:
    ```bash
    git remote add origin <remote-url>
    ```
    > You can find the remote url by clicking on Code on GitHub's repo page. Refer following image to see where exactly can you find the url:
    <center> <img title="Github Repo Add e-Yantra" src="https://raw.githubusercontent.com/kalindkaria/typora-md-assets/master/git_tutorial/assets/06_github_linking.png" width="450"></center>

3. Since the local changes are already commited, we can now push changes to remote repository using command:
    ```bash
    git push origin main
    ```
    > Note: When you push anything to your remote repository, your GitHub account password will not work. Instead, you will need to add a GitHub Personal Access Token in place of your password. To learn more about what a GitHub Personal Access Token is and how to create one, please visit the following website: [GitHub Personal Access Token Creation Guide](https://docs.github.com/en/enterprise-server@3.6/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#keeping-your-personal-access-tokens-secure).


All your local files and folders for eYRC Theme have been updated into the Remote Repository. Now you can collaborate and start working as team to complete your eYRC tasks and assignments effectively. 

## What Next???

It is crucial that each team member actively participates in the tasks and engages in collaborative efforts through GitHub. Keep in mind that there are potential incentive points your team can earn based on the level of active collaboration within the repository.

Henceforth, we will closely monitor the activity on your GitHub repository, and this data will play a significant role in the subsequent stages of the competition. Therefore, ensure that you consistently commit changes to the repository and maintain it effectively to maximize your team's performance.

To know more about how to collaborate using Git and GitHub, refer the following video:
<iframe width="750" height="410" src="https://www.youtube.com/embed/aEU-a-GadXQ?si=BW1kMyKbqlQZqfwi" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


## Things to Note:

Following are few things to note when you work with git and GitHub 
1. All the other team members can clone the remote repository onto their local machine using `git clone <remote-url>`
2. After cloning the repository, all team members can commence work on the project. However, there's a crucial consideration: what if a file that has been updated by one team member is also updated by you? In such a scenario, someone's efforts could potentially go to waste. To prevent this, it's advisable to make it a habit to regularly pull the latest changes from the remote repository using the command `git pull origin main`
3. Check Status: View status of your changes using command `git status`

## For more information about Git and GitHub refer following links:
1. [Introduction to Git version control tool](https://www.youtube.com/watch?v=aEhDUUxVYAI)
2. [Advanced Features of Git](https://www.youtube.com/watch?v=BRxFgZBplbY)