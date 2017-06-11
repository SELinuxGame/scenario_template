# Scenario Contributor Guide for selinuxgame.org

This is a template scenario and contributor guide to create an
[selinuxgame.org](http://selinuxgame.org/) scenario. You can see the
[existing scenarios](http://selinuxgame.org/scenarios/) as examples.


## Making a Scenario

1. Clone this repo.
2. Write the [scenario prompt](#scenario-prompt), which is shown to the player when they login.
3. Write the [Ansible playbook](#ansible-playbook) to customize the environment for the player.
4. [Submit your scenario](#submitting-your-scenario) with items (2) and (3)
5. Add the [scenario to the website](#add-the-scenario-to-selinuxgameorg).


## Test the Environment

After cloning, you can run `vagrant up` to receive the typical base
environment. As you test your changes, whatever state the Vagrant box is in
at the end of `vagrant up` is what players will receive.


## Scenario Prompt

The scenario prompt is a text file that is shown to the player when they type
`scenario`. At a minimum this file explains how to reproduce an issue the
fails with SELinux Enforcing and succeeds with SElinux disabled or permissive.

Specifically put your scenario content in [scenario_prompt.md](https://github.com/SELinuxGame/scenario_template/blob/master/roles/base/files/scenario_prompt.md)
See that file for more information on what should go into the scenario prompt.


## Ansible Playbook

The Ansible playbook configures the system such that the problem is setup for
the player. Typically you install and configure some packages in a way that
creates the SELinux problem of interest.

Put your Ansible content in the [scenario playbooks](https://github.com/SELinuxGame/scenario_template/tree/master/roles/scenario_playbook)
role. For basic usage you'll be writing the role's Ansible code in
[this file](https://github.com/SELinuxGame/scenario_template/blob/master/roles/scenario_playbook/tasks/main.yml).


## Submitting your Scenario

Once your scenario prompt and Ansible playbook are tested and working, commit
your changes. Use `git format-patch` to format the patch for email submission
Send the scenario patch files to bmbouter aat gmail.com or dennis.kliban aat
gmail.com.

Once accepted we will build and publish your scenario into Vagrant Cloud which
delivers the box directly to a player. Once published, the last step is to
list the scenario on selinuxgame.org


## Add the Scenario to selinuxgame.org

To add the scenario to selinuxgame.org, open a PR against the
[website repository](https://github.com/bmbouter/selinuxgame.org/tree/master/_scenarios).

Specifically, you need to make a new file in the [_scenarios directory]((https://github.com/bmbouter/selinuxgame.org/tree/master/_scenarios)).

That file must declare three fields:

* A slug, which is a shortname for the box and url. e.g. new_ways, all_my_content.
* A title: The title that goes on the [Scenarios page](http://selinuxgame.org/scenarios/), e.g. "New Ways".
* A description: The description that goes on the [Scenarios page](http://selinuxgame.org/scenarios/).

See the [Scenarios page](http://selinuxgame.org/scenarios/) for examples of
this data.


## FAQ

### What should I write about?

Not sure what to write? Scenarios are usually based on a real situations that
have happened. Our hope is that when SELinux errors are experienced in
different ways, that those can be written as a scenario for others to try to
solve.

### Why should I contribute?

Each scenario contributed can create a learning experience for many people.
Increasing the understanding of SELinux allows for more people to contribute
to a more secure world.
