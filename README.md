![Publish package to GitHub Packages](https://github.com/fo0/java-gh-package-registry-example/workflows/Publish%20package%20to%20GitHub%20Packages/badge.svg)

# How to publish your written library inside your github repository to your personal github package registry?

### first of all there are some requirements for this guide
- you need a github account
- your code must be inside the repository
- your code must compile
- every push consumes 1 github action
- this guide is for java-8 but you can do this for java-x too
- you must be the repository owner
- you need a [github access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
- you must now how to add a [secret to github](https://docs.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets)
- you want maven for your dependency management

### what is my configuration?
- 1 [action for deploy](https://github.com/fo0/java-gh-package-registry-example/blob/master/.github/workflows/maven_deploy.yml)
- deploy action listening for new [tags](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/managing-tags) [eclipse-create-tags](https://wiki.eclipse.org/EGit/User_Guide#Creating_a_Tag)
- java-8
- maven
- status badge


# Let's start!
This examples has all includings links and examples for the own repository, please modify the links for your own

1. Open your pom.xml and add the following distributedManagement if its not already inside your [pom.xml](https://github.com/fo0/java-gh-package-registry-example/blob/master/hello-world-example/pom.xml)
```
	<distributionManagement>
		<repository>
			<id>github</id>
			<name>GitHub Packages</name>
      <!-- https://maven.pkg.github.com/<github-user>/<repository> -->
			<url>https://maven.pkg.github.com/fo0/java-gh-package-registry-example</url>
		</repository>
	</distributionManagement>
```
2. go to your [github actions](https://github.com/fo0/hello-world-java-lib/actions)
3. create your action for deploy [workflow](https://github.com/fo0/hello-world-java-lib/blob/master/.github/workflows/maven_deploy.yml)
  - line 7: listening for new created releases
  - line 15: java-version
  - line 17: path to your <pom.file>
  - line 19: name of your github-secret for your github-token
  
4. commit something
5. create a new tag i.e. v0.1
6. check the [github actions](https://github.com/fo0/hello-world-java-lib/actions) there should be one new tasks. Starting with deploy.
7. open [package-registry](https://github.com/fo0/hello-world-java-lib/packages) after first task deploy is finished
8. [creating a badge](https://docs.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow#adding-a-workflow-status-badge-to-your-repository)

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
