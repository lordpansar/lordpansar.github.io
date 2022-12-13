---
layout: post
title:  "Environment check in Github Actions"
date:  2022-12-12 05:00:00 +0200
categories: ['Devops', 'Github']
permalink: blog/github-action-environment-check
---

In a project I've been working on we faced a problem. While using Github Actions to handle our CI/CD, we wanted to reuse our deployment scripts across all
environments for each app. Thus giving us less code to maintain.

The plan was to set up identical secret keys (with different values though) in two different Github repo environments. The actions would trigger on
changes to either the dev branch or the main branch. The source code from each branch would then be deployed to either the dev or production environment,
using the dev or prod secrets accordingly.

But how do we make the action know when to get which secrets and where?

The following solution did the trick, but it's a bit of a backyard hack. To follow along, you should have some basic knowledge of YAML and Github Actions.


<h4>Step 1</h4>

For this example I've added two environments in the repo from which I will build my app.

![Two environments in a Github repo]({{ "/assets/images/github-action-environment-check/environments.PNG" | absolute_url }})

They both contain a secret named MY_PRETTY_SECRET. Although they have the same name/key, they contain different values. This could for instance be an API key,
a password, a URL or such. Depending on if I want to deploy this application to my dev environment or my production environment, I want to retrieve the
corresponding value for that environment using only one script. Instead of having two identical scripts, each specific for each environment.

[Click here to read more about environments in Github.][github-environments]

<h4>Step 2</h4>

Add a YAML file under the .github/workflows folder in your project

{% highlight yaml %}
name: My pretty YAML script #presentation name of your script

on:
  workflow_dispatch: #run this script on manual trigger in Github
  push:              #or on push to branches named main or dev
    branches:
      - main
      - dev

jobs: #collection of jobs
  set-environment: #this is a job named 'set-environment'
    runs-on: ubuntu-latest #your preferred OS
    outputs: #the env value needs to be exposed as an output in order to be reached from other jobs
      current_env: ${% raw %}{{ steps.set_env.outputs.current_env }}{% endraw %} #output variable to store the relevant environment
    steps:
      - name: Check if prod
        if: endsWith(github.ref, '/main') #if the triggering branch is 'main'
        run: |
          echo "ENVIRONMENT_NAME=prod" >> $GITHUB_ENV #retrieve secrets from 'prod' environment in Github
      - name: Check if dev
        if: endsWith(github.ref, '/dev') #if the triggering branch is 'dev'
        run: |
          echo "ENVIRONMENT_NAME=dev" >> $GITHUB_ENV #retrieve secrets from 'dev' environment in Github
      - name: Set output
        id: set_env
        run: echo "::set-output name=current_env::${% raw %}{{ env.ENVIRONMENT_NAME }}{% endraw %}" #assign the value of ENVIRONMENT_NAME to the output variable 'current_env' 

  build-and-deploy: #this is a job named 'build-and-deploy'
    runs-on: ubuntu-latest #your preferred OS
    needs: set-environment #this job won't be executed until the set-environment job is finished
    environment: ${% raw %}{{ needs.set-environment.outputs.current_env }}{% endraw %} #this job will now retrieve secret values stored in either 'dev' or 'prod' repo environments, depending on the value set in previous job
    steps:
      - name: Get secret from Github
      - uses: MyPrettyGithubAction #example action
        with:
          creds: ${% raw %}{{ secrets.MY_PRETTY_SECRET }}{% endraw %} #gets the value of MY_PRETTY_SECRET from the current repo environment
      - run: echo "Deploying to ${% raw %}{{ needs.set-environment.outputs.current_env }}{% endraw %} environment" #output: "Deploying to {environment name}"
{% endhighlight %}

In the example above I've separated the logic into multiple jobs. You can of course do this in a single job, eliminating the need for exposing the current_env value.

Happy coding!


[github-environments]: https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment