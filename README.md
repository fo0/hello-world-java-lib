# How to publish your written library inside your github repository to your personal github package registry?

### first of all there are some requirements for this guide
- you need a github account
- your code must be inside the repository
- your code must compile
- every compile & push consumes 2 github actions
- this guide is for java-8 but you can do this for java-x too
- you must be the repository owner
- you need a [github access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
- you must now how to add a [secret to github](https://docs.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets)
- you want mavan for your dependency management

### what is my configuration?
- 1 action for compile 
- compile-action listen to every [tag](https://docs.github.com/en/github/administering-a-repository/managing-releases-in-a-repository) push
- 1 action for deploy
- deploy action listening for new release created
- java-8
- maven


# Let's start!
This examples has all includings links and examples for the own repository, please modify the links for your own

0. go to your [github actions](https://github.com/fo0/hello-world-java-lib/actions)
1. create your action for compile [workflow](https://github.com/fo0/hello-world-java-lib/blob/master/.github/workflows/maven_build.yml)
  - line 8: listen for tag-creations
  - line 20: java-version
  - line 28: path to your <pom.file>
  - line 32: name of your github-secret for your github-token

2. create your action for deploy [workflow](https://github.com/fo0/hello-world-java-lib/blob/master/.github/workflows/maven_deploy.yml)
  - line 7: listening for new created releases
  - line 15: java-version
  - line 17: path to your <pom.file>
  - line 19: name of your github-secret for your github-token
  
3. commit something
4. create a new tag i.e. v0.1
5. check the [github actions](https://github.com/fo0/hello-world-java-lib/actions) there should be some new tasks. Starting with compile, ending with deploy
6. open [releases](https://github.com/fo0/hello-world-java-lib/releases) after first task compile is finished
7. open [package-registry](https://github.com/fo0/hello-world-java-lib/packages) after second task deploy is finished

# How to access the library now?
There are two ways to access the library
- via github
- TODO: via maven central (including a new action)

0. create or open the maven .settings.xml and add your github account informations to access the github package-registry (currently its a limitation of github)
```
<servers>
    <server>
        <id>github</id>
        <username>YOUR_USERNAME</username>
        <password>YOUR_AUTH_TOKEN</password>
    </server>
</servers>
```
1. open your java-project where you want to use the new library
2. navigate to the pom.xml
3. add your library dependency, you can copy it from your github [package-registry](https://github.com/fo0/hello-world-java-lib/packages)
