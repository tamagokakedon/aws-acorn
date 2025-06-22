# aws-acorn

## summary
This is a cli tool that allows you to interactively create and set up AWS accounts managed within an AWS Organization.

## Tech stack
- main program language
    - Go lang
- CLI framework
    - github.com/spf13/cobra
- aws sdk
    - github.com/aws/aws-sdk-go-v2
- interactive ui library 
    - github.com/AlecAivazis/survey/v2

## how to use
- create aws account
```
acorn --create
```
- specify role deploy
    - To set up specific roles on the created account.
```
acorn --role-deploy
```
- account setting
```
acorn --setting
```
- account specify setting
```
acorn --setting [specify settings name]
```

## Feature

### create account
- You can create an AWS account under your Organization using the acorn command with the create option.
- When you run it, the tool first verifies the existence of an Organization
- After verification, it prompts you to enter the AWS account name and an email address for the new AWS account.
- Once these are provided, it displays the Organizational Units (OUs) within your Organization.
- You can select the OU where you want to set up the AWS account using the up and down arrow keys on your keyboard, then confirm your choice with the Enter key. 
- If the selected OU has child OUs, it will display a list of those child OUs along with an option to "Select this OU".
- Once the OU for the new AWS account is determined, the tool display aws account name and aws account mail address and OU to confirm
- You type y(yes), the tool proceeds to create the AWS account with the provided account name and email address, and then moves it to the chosen OU.
- These processes run using your current default AWS Profile information, but you can also execute them with a specific profile by using the --profile option.

### deploy role
- You can deploy specify role to a new AWS account using the acorn command with the role-deploy option.
- To use this option, role-deploy.sh must be present in the current working directory when you execute the command.
- The role-deploy.sh file needs to contain a Shell script written to deploy specific roles to an AWS account. 
- This tool will read the contents of that Shell script and execute it accordingly.

### account setting
- You can set up new AWS accounts using this tool with the --setting option. The tool offers multiple configurable items, which you can view using the --setting-list option.
- By default, the --setting option reads settings.txt from the current directory and applies the items listed there.
- Each setting is managed like a plugin within this tool, and users can even add their own custom settings. 
- When adding a new setting, you'll need to define the "item name," "description of the setting content," and "the process for setting it up."
- Additionally, you can apply only specific settings by using --setting [item name]. 
- Initially, we'll provide settings for "Delete default security groups" and "Block S3 public access."