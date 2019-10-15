# Contributing to Jenkins

This page provides information about contributing code to the Jenkins core codebase.

:exclamation: There's a lot more to the Jenkins project than just code. For information on contributing to the Jenkins project overall, check out [Participate].

## Getting started

1. Fork the repository on GitHub
2. Clone the forked repository to your machine
3. Install the development tools. In order to develop Jenkins, you need the following tools:
  * Java Development Kit (JDK) 8.
     - In Jenkins project we usually use [OpenJDK],
  but you can use other JDKs as well.
     - Java 9+ is **not supported** in Jenkins.
  * Maven 3.5.4 or above. You can [download maven].
  * Any IDE which supports importing Maven projects.
4. Setup your development environment as described in [Preparing for Plugin Development]

If you want to contribute to Jenkins or just learn about the project,
you can start by fixing some easier issues.
In the Jenkins issue tracker we mark such issues as `newbie-friendly`.
You can find them
using this query for [newbie friendly issues].

## Building and Debugging

The build flow for Jenkins core is built around Maven.
There is a description of the [building and debugging process].

If you want simply to have the `jenkins.war` file as fast as possible without tests, run:

    mvn clean package -pl war -am -DskipTests -Dspotbugs.skip

The WAR file will be created in `war/target/jenkins.war`.
After that you can start Jenkins using Java CLI ([guide]).
If you want to debug this WAR file without using Maven plugins,
You can just start the executable with [Remote Debug Flags]
and then attach IDE Debugger to it.

## Testing changes

Jenkins core includes unit and functional tests as a part of the repository.

Functional tests (`test` module) take a while even on server-grade machines.
Most of the tests will be launched by the continuous integration instance,
so there is no strict need to run full test suites before proposing a pull request.

There are 3 profiles for tests:

* `light-test` - only unit tests, no functional tests
* `smoke-test` - run unit tests + a number of functional tests
* `all-tests` - Runs all tests, with re-run (default)

In addition to the included tests, you can also find extra integration and UI
tests in the [Acceptance Test Harness (ATH)] repository.
If you propose complex UI changes, you should create new ATH tests for them.

## Proposing Changes

The Jenkins project source code repositories are hosted at GitHub.
All proposed changes are submitted and code reviewed using the _GitHub Pull Request_ process.

To submit a pull request:

1. Commit changes and push them to your fork on GitHub.
It is a good practice is to create branches instead of pushing to master.
2. In GitHub Web UI click the _New Pull Request_ button
3. Select `jenkinsci` as _base fork_ and `master` as `base`, then click _Create Pull Request_
  * We integrate all changes into the master branch towards the Weekly releases
  * After that the changes may be backported to the current LTS baseline by the LTS Team.
    Read more about the [backporting process]
4. Fill in the Pull Request description according to the [proposed template].
5. Click _Create Pull Request_
6. Wait for CI results/reviews, process the feedback.
  * If you do not get feedback after 3 days, feel free to ping `@jenkinsci/code-reviewers` to CC.
  * Usually we merge pull requests after 2 votes from reviewers or after 1 vote and 1-week delay without extra reviews.

Once your Pull Request is ready to be merged,
the repository maintainers will integrate it, prepare changelogs and
ensure it gets released in one of incoming Weekly releases.
There is no additional action required from pull request authors at this point.

## Copyright

Jenkins core is licensed under [MIT license], with a few exceptions in bundled classes.
We consider all contributions as MIT unless it's explicitly stated otherwise.
MIT-incompatible code contributions will be rejected.
Contributions under MIT-compatible licenses may be also rejected if they are not ultimately necessary.

We **Do NOT** require pull request submitters to sign the [contributor agreement]
as long as the code is licensed under MIT and merged by one of the contributors with the signed agreement.

We still encourage people to sign the contributor agreement if they intend to submit more than a few pull requests.
Signing is also a mandatory prerequisite for getting merge/push permissions to core repositories
and for joining teams like [Jenkins Security Team].

## Continuous Integration

The Jenkins project has a Continuous Integration server... powered by Jenkins, of course.
It is located at [ci.jenkins.io].

The Jenkins project uses [Jenkins Pipeline] to run builds.
The code for the core build flow is stored in the [Jenkinsfile] in the repository root.
If you want to update that build flow (e.g. "add more checks"),
just submit a pull request.

# Links

* [Jenkins Contribution Landing Page](https://jenkins.io/participate/)
* [Jenkins IRC Channel](https://jenkins.io/chat/)
* [Beginners Guide To Contributing](https://wiki.jenkins.io/display/JENKINS/Beginners+Guide+to+Contributing)
* [List of newbie-friendly issues in the core](https://issues.jenkins-ci.org/issues/?jql=project%20%3D%20JENKINS%20AND%20status%20in%20(Open%2C%20%22In%20Progress%22%2C%20Reopened)%20AND%20component%20%3D%20core%20AND%20labels%20in%20(newbie-friendly))

[download maven]: https://maven.apache.org/download.cgi
[Preparing for Plugin Development]: https://jenkins.io/doc/developer/tutorial/prepare/
[newbie friendly issues]: https://issues.jenkins-ci.org/issues/?jql=project%20%3D%20JENKINS%20AND%20status%20in%20(Open%2C%20%22In%20Progress%22%2C%20Reopened)%20AND%20component%20%3D%20core%20AND%20labels%20in%20(newbie-friendly)
[OpenJDK]: http://openjdk.java.net/
[Participate]: https://jenkins.io/participate/
[building and debugging process]: https://jenkins.io/doc/developer/building/
[guide]: https://wiki.jenkins.io/display/JENKINS/Starting+and+Accessing+Jenkins
[Remote Debug Flags]: https://stackoverflow.com/questions/975271/remote-debugging-a-java-application
[Acceptance Test Harness (ATH)]: https://github.com/jenkinsci/acceptance-test-harness
[backporting process]: https://jenkins.io/download/lts/
[proposed template]: .github/PULL_REQUEST_TEMPLATE.md
[MIT license]: ./LICENSE.txt
[contributor agreement]: https://wiki.jenkins.io/display/JENKINS/Copyright+on+source+code
[Jenkins Security Team]: https://jenkins.io/security/#team
[ci.jenkins.io]: https://ci.jenkins.io/
[Jenkins Pipeline]: https://jenkins.io/doc/book/pipeline/
[Jenkinsfile]: ./Jenkinsfile
