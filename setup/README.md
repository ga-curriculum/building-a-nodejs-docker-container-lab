<h1>
  <span class="headline">Building a Node.js Docker Container Lab</span>
  <span class="subhead">Setup</span>
</h1>

## Setup

In this lab, you will create a simple Node.js API using Express, test it locally, and then package it in a Docker container for easy deployment. By the end, you will have a Docker image of your application that can be deployed on any machine.

## Prerequisites

You will need to install Node.js and npm on your AWS EC2 instance (or another environment) before starting this lab.

To check if Node.js is already installed, use the following command in the terminal:

```bash
node --version
```

- If you see a version number, Node.js is already installed.
- If you receive a "command not found" error, Node.js is not installed.

<br>

If Node.js is not installed, follow [this guide from AWS](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-up-node-on-ec2-instance.html) for installation steps.
