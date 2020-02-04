---
title: 'dbt CLI: Create a project'
sidebar_label: dbt CLI
id: create-a-project-dbt-cli
description: Now that we're set up, let's create a starter project with example models using the dbt CLI.
---

Now that we've successfully run our sample query in Snowflake, and chosen the way we want to develop, we can create a dbt project! In this step, we'll create a starter project with example models, before we build our own models.

import Link from '@docusaurus/Link';
import Alert from '@site/src/components/alert';
import Lightbox from '@site/src/components/lightbox';
import LoomVideo from '@site/src/components/loom';
import FAQ from '@site/src/components/faqs';

<Alert type="info">
These are the instructions for developing a project using the dbt CLI. If you're developing in dbt Cloud, follow the instructions <Link to="/tutorial/create-a-project-dbt-cloud">here</Link>.
</Alert>


## Create a project
<LoomVideo id="f36152340ccc41e8be517eb295c4d6f1" />

The dbt CLI comes with a command to help you scaffold a dbt project. To create your dbt project:
1. Ensure dbt is installed by running `dbt --version`:
```shell-session
$ dbt --version

```

<Alert type="info">
dbt should have been installed as part of the  <a href="/tutorial/setting-up">Setting Up</a> part of the tutorial. If it was not installed, please follow the <a href="https://docs.getdbt.com/docs/installation"> installation instructions </a>
</Alert>

2. Run the `init` command:
```shell-session
$ dbt init jaffle-shop
```
3. `cd` into your project:
```shell-session
$ cd jaffle-shop
```
You can use `pwd` to confirm that you are in the right spot.

3. Open your project (i.e. the directory you just created) in a code editor like Atom or VSCode. You should see a directory structure with `.sql` and `.yml` files that were generated by the `init` command.

<Lightbox src="/img/starter-project-dbt-cli.png" title="The starter project in a code editor" />


4. Update the following values in the `dbt_project.yml` file:
```yaml
name: jaffle_shop # this normally says my_new_package

...

profile: jaffle_shop # this normally says default

...

models:
  jaffle_shop: #this normally says my_new_package. It should match the value for `name:`
    ...
```

## Connect to Snowflake
When developing locally, dbt connects to your data warehouse using a [profile](https://docs.getdbt.com/docs/configure-your-profile) — a yaml file with all the connection details to your warehouse.

1. Create a file in the `~/.dbt/` directory named `profiles.yml`.
2. Copy the following into the file — make sure you update the values where indicated.
```yaml
jaffle_shop: # this needs to match the profile: in your dbt_project.yml file
  target: dev
  outputs:
    dev:
      type: snowflake
      threads: 4
      account: [account_id] # supplied to you
      user: [username] # supplied to you
      password: [password] # supplied to you
      role: transformer
      database: analytics
      warehouse: transforming
      schema: dev_[initialsurname] # e.g. dev_ccarroll
      client_session_keep_alive: False
```

4. Execute the debug command from your project to confirm that you can successfully connect
```shell-session
$ dbt debug
```
Confirm that the last line of the output is `Connection test: OK connection ok`.

<Lightbox src="/img/successful-dbt-debug.png" title="A successful dbt debug command" />

### FAQs
<FAQ src="faqs/sample-profiles" alt_header="My data team uses a different data warehouse. What should my profiles.yml file look like for my warehouse?"/>
<FAQ src="faqs/separate-profile" />
<FAQ src="faqs/profile-name" />
<FAQ src="faqs/target-names" />
<FAQ src="faqs/profile-env-vars" />


## Perform your first dbt run
Our sample project has some example models in it. We're going to check that we can run them to confirm everything is in order.

1. Execute the `run` command to build the example models:
```shell-session
$ dbt run
```
You should have an ouput that looks like this:

<Lightbox src="/img/successful-dbt-run.png" title="A successful dbt run command" />

## Commit your changes
We need to commit our changes so that our repository has up-to-date code.
<LoomVideo id="a39753e4ce5647b2be4e5331788bab91" />

1. Link the GitHub repository you created in the [Setting Up](tutorial/setting-up.md) instructions to your dbt project by running the following commands. Make sure you use the correct git URL for your repository.
```shell-session
$ git init
$ git commit -m "Create a dbt project"
$ git remote add origin https://github.com/USERNAME/dbt-tutorial.git
$ git push -u origin master
```

<Alert type="info">
If this is your first time using git, it's worth taking some time to understand the basics.
</Alert>