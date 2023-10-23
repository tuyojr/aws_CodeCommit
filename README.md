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