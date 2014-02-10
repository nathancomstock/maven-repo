maven-repo
==========

This is a temporary maven repository.

### Use artifacts in this repo.

Add the following repository to your `pom.xml` or `settings.xml` file to allow your maven build
to resolve artifacts in this repository.

    <repositories>
      <repository>
        <id>nathancomstock-releases</id>
        <url>https://github.com/nathancomstock/maven-repo/raw/master/releases</url>
      </repository>
      <repository>
        <id>nathancomstock-snapshots</id>
        <url>https://github.com/nathancomstock/maven-repo/raw/master/snapshots</url>
      </repository>
    </repositories>

### Deploy artifacts to this repo

Artifacts are added to this repository using `mvn deploy` with a few nonstandard steps required
as this is just a git repository.

#### Update pom.xml

Add the following `distributionManagement` element to your projects `pom.xml`

    <distributionManagement>
      <repository>
        <id>nathancomstock-releases-repo</id>
        <url>https://github.com/nathancomstock/maven-repo/raw/master/releases</url>
      </repository>
      <snapshotRepository>
        <id>nathancomstock-snapshots-repo</id>
        <url>https://github.com/nathancomstock/maven-repo/raw/master/snapshots</url>
      </snapshotRepository>
    </distributionManagement>

##### Prepare maven-repo for deploy

Clone the maven-repo git repository.

    $ cd /tmp
    $ git clone git@github.com:nathancomstock/maven-repo.git

##### Deploy releases

Run maven release deploy, providing an `altDeploymentRepository` pointing to you clone of `maven-repo`

    $ mvn clean install deploy \
      -DaltDeploymentRepository=nathancomstock-releases-repo::default::file:///tmp/maven-repo/releases

##### Deploy snapshots

Run maven snapshot deploy, providing an `altDeploymentRepository` pointing to you clone of `maven-repo`

    $ mvn clean install deploy \
      -DaltDeploymentRepository=nathancomstock-releases-repo::default::file:///tmp/maven-repo/snapshots

##### Publish

The `mvn deploy` command pushed you artifacts to your clone of `maven-repo`. The usual git steps
need to be executed to actually publish these artifacts to the remote repository.

    $ cd /tmp/maven-repo
    $ git add .
    $ git commit -m 'deploy maven artifacts'
    $ git push origin



