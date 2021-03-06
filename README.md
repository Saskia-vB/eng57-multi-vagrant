# Multi-variant machine

Vagrant is able to define and control multiple guest machines per Vagrantfile. This is known as a "multi-machine" environment.

# Provisioning and tests

This exercise utilised vagrant and VirtualBox to make sure the provision file passed all the tests.

#### Installation

##### Pre-requisites:
- install Vagrant
- install VirtualBox
- install Ruby
- install Bundler

To get this box running:
1. clone the repo
2. make sure you are on the root of the project and can see the Vagrant file
3. then run:
```bash
vagrant up
```

Now you can see nginx running on 2 locations:
- ip: 192.168.10.100
- development.local/

To see the website working:
1. cd eng57-multi-vagrant
2. vagrant ssh app
3. cd /home/ubuntu/app
4. sudo npm install
5. sudo npm start

Now you can see the website running here:
- development.local:3000
- development.local:3000/fibonacci/{index}


#### Tests

```bash
cd eng57-multi-vagrant/tests
rake spec
```

# Jenkins
### What is Jenkins?
- Continuous Integration (CI) Server:
  - CI focuses on preparing software release easier, changes are merged back to main branch as often as possible
- Monitors repeated tasks
- build and test your project continuously


## Create a CI pipeline
 1. Go to: http://35.178.239.152:8080/
 2. Log in
 3. Configure
    - good practice: delete old builds
    - GitHub project: link to your github repo [i.e. https://github.com/Saskia-vB/eng57-multi-vagrant/]
    - Select Git as version control manager:
        - Repository URL: enter github clone SSH key [i.e. git@github.com:Saskia-vB/eng57-multi-vagrant.git]
        - Credentials: create a SSH Key - follow documentation : https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
    - select "Github hook trigger for GITScm poling"
    - Build environments: select "add Node/npm to path"
    - Build:
    ```bash
    cd app
    npm install
    npm test
    ```
  4. Create a Webhook on Github repo - go to repo > settings > webhooks > add webhook
    - Payload URL: http://35.178.239.152:8080/github-webhook/
    - Content type: application/json
    - select "send me everything"

## Using jenkins
- Once your CI pipeline is configured here is how to build from a new branch:
  1. create a new branch:
     - in your command line, from the master branch enter: git checkout -b [branch_name]
  2. configure Jenkins:
    - go to configurations > branches to build > branch specifier
    - enter your [branch_name]
    - apply and save changes
  3. push from command line:
    - make changes i.e. echo "test" >> README.md or touch README2.md
    - git add .
    - git commit -m "meaningful message"
    - git push origin [branch_name]

###### Github testing for Jenkins build
test I
test from branch
test II
testing dev branch
another test
test i've stopped counting
keep on testing
still trying
master and dev branch
will it work twice in a row?
testing
npm test
remove blog test
only dev branch
still working
testing jenkins pluugin
master merge try
another merging test
recreate dev branch�
merging attempt
merging again
checking
..
another try
new webhook
test
with https
successgit push origin master
