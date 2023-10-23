# Working with AWS CodeCommit (AWS Training and Certifications Lab)

AWS CodeCommit is a highly scalable, managed source control service that hosts private Git repositories. CodeCommit stores your data in Amazon S3 and Amazon DynamoDB giving your repositories high scalability, availability, and durability. You simply create a repository to store your code. There is no hardware to provision and scale or software to install, configure, and operate.

This lab demonstrates how to:

- Create a code repository using AWS CodeCommit via the Amazon Management Console
- Create a local code repository on the Linux instance using git
- Synchronize a local repository with an AWS CodeCommit repository

## Task 1: Create an AWS CodeCommit repository

In this task, you use the AWS Management Console to create an AWS CodeCommit repository.

1. At the top of the AWS Management Console, in the search bar, search for and choose `CodeCommit`.
2. On the __AWS CodeCommit__ page, choose `Create repository`.
3. On the Create repository page:
    - For Repository name, enter `My-Repo`.
    - For Description enter `My first repository`.
    - Choose `Create`.

![awsCodeCommit_task1](https://github.com/tuyojr/aws_CodeCommit/blob/main/awsCodeCommit_task1.png)

## Task 2: Connect to the Amazon EC2 instance
An Amazon EC2 instance has been created for you as part of the lab environment build process. In this task, you connect to the instance using AWS Systems Manager Session Manager.

4. Copy the __Ec2InstanceSessionUrl__ value from the list to the left of these instructions, and then paste it into a new web browser tab.
A console connection is made to the instance inside your web browser window. A set of commands are run automatically when you connect to the instance that change to the user’s home directory and display the path of the working directory, similar to this:

![awsCodeCommit_task2](https://github.com/tuyojr/aws_CodeCommit/blob/main/awsCodeCommit_task2.png)

## Task 3: Create a local repository using Git
This task provides an example of how you would use AWS CodeCommit to synchronize to any local code repository that you might create in your normal production development environment.

5. In the terminal session, run the following command to install the Git client:

```BASH
sudo yum install -y git
```

6. Run the following commands to configure the Git credential helper with the AWS credential profile, and allow the Git credential helper to send the path to repositories:

```BASH
git config --global credential.helper '!aws codecommit credential-helper $@'
git config --global credential.UseHttpPath true
```

> These commands have no output.

Next, obtain the HTTPS URL of your AWS CodeCommit repository.

7. Return to your web browser tab with the AWS CodeCommit console, which should be on the __My-Repo__ page.
8. At the upper-right of the page, choose `Clone URL`, and then choose __Clone HTTPS__.

The repository URL is copied to your clipboard and should look similar to this: _https://git-codecommit.us-east-1.amazonaws.com/v1/repos/My-Repo_.

9. Return to your web browser tab with the terminal session.
10. Run the following command to clone the __My-Repo__ repository to the instance:
    - Replace the __CLONE_HTTPS_URL__ placeholder value with the __Clone HTTPS URL__ that you copied previously.

```BASH
git clone CLONE_HTTPS_URL
```

The output should indicate that you are cloning the My-Repo repository, and that the repository is empty, similar to this:

```BASH
Cloning into 'My-Repo'...
warning: You appear to have cloned an empty repository.
```

## Task 4: Making a code change and first commit to the repo
In this task, you create your first commit in your local repo. You create two example files in your local repo, use Git to stage the changes to your local repo, and then commit the changes.

11. Run the following command to change to the My-Repo directory:

```BASH
cd ~/My-Repo
```

12. Run the following command to create two files in your local repo:

```BASH
echo "The domestic cat (Felis catus or Felis silvestris catus) is a small, usually furry, domesticated, and carnivorous mammal." >cat.txt
echo "The domestic dog (Canis lupus familiaris) is a canid that is known as man's best friend." >dog.txt
```

13. Run the following command to stage the changes in your local repo and see them staged, then commit those changes:

```BASH
git add cat.txt dog.txt
git status
git commit -m "Added cat.txt and dog.txt"
```

## Task 5: Push your first commit

14. Run the following command to push your commit through the default remote name Git uses for your AWS CodeCommit repository (origin), from the default branch in your local repo (master):

```BASH
git push -u origin master
```

After you have pushed code to your AWS CodeCommit repository, you can view the contents using the AWS CodeCommit console.

15. Return to your web browser tab with the AWS CodeCommit console, which should be on the My-Repo page.
16. Choose your web browser’s refresh button to refresh the page.
The two files that you added to your repository should be displayed.
17. Choose the link for each file to view its contents.