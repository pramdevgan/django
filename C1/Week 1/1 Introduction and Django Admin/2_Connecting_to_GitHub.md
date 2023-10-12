# Connecting to GitHub

## Connecting to GitHub

Over four courses, you are going to build a Django app. In order to get your code in every assignment, you are going to use GitHub. If you do not yet have an account, please [create one](https://github.com/) now. We are going to clone a repo that will contain the code for your Django app.

### Connecting GitHub and Codio

You need to [connect](https://docs.codio.com/common/develop/ide/editing/connect-github-codio.html#connect-codio-github) GitHub to your Codio account. This only needs to be done one time.

* In your Codio account, click on your username
* Click on **Applications**

![Codio Account](https://docs.codio.com/_images/GitHub1.png)

* Under GitHub, click on **Connect account**

![connect account](https://docs.codio.com/_images/Github2.png)

* You will be using an SSH connection, so you need to click on **Upload public key**

### Fork the Repo

* Go to the [blango](https://github.com/codio-templates/blango) repo. This repo is the starting point for your blog.
* Click on the “Fork” button in the top-right corner.
* Click the green “Code” button.
* Copy the SSH information. It should look something like this:

```markdown
git@github.com:<your_github_username>/blango.git
```

## Important

If you do not use the SSH information, you will have to provide your username and Personal Access Token (PAT) to GitHub each time you push or pull from the repository. See this [documentation](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) for setting up a PAT for your GitHub account.

### In the Terminal

* Clone the repo. Your command should look something like this:

```bash
git clone git@github.com:<your_github_username>/blango.git
```

* You should see a `blango` directory appear in the file tree.

You are now ready for the next assignment.

Next
