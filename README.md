# ZenWave Maven Snapshots Repository

Snapshot (`-SNAPSHOT`) builds of ZenWave projects, published from their `develop` branches and served at:

```
https://www.zenwave360.io/maven-snapshots/
```

Snapshots change with every build and only the latest few builds of each version are kept. Use released versions,
from Maven Central, for anything you depend on.

## Maven

Add the repository to your `pom.xml`. Add `pluginRepositories` too if you use a snapshot Maven plugin, such as
`zenwave-sdk-maven-plugin`:

```xml
<repositories>
    <repository>
        <id>zenwave-snapshots</id>
        <url>https://www.zenwave360.io/maven-snapshots/</url>
        <releases><enabled>false</enabled></releases>
        <snapshots><enabled>true</enabled></snapshots>
    </repository>
</repositories>
<pluginRepositories>
    <pluginRepository>
        <id>zenwave-snapshots</id>
        <url>https://www.zenwave360.io/maven-snapshots/</url>
        <releases><enabled>false</enabled></releases>
        <snapshots><enabled>true</enabled></snapshots>
    </pluginRepository>
</pluginRepositories>
```

## Gradle

Add the repository next to Maven Central in `build.gradle.kts` (or in `settings.gradle.kts` under
`dependencyResolutionManagement`):

```kotlin
repositories {
    mavenCentral()
    maven("https://www.zenwave360.io/maven-snapshots/") {
        mavenContent { snapshotsOnly() }
    }
}

dependencies {
    implementation("io.zenwave360.dsl:dsl-kotlin:1.11.0-SNAPSHOT")
}
```

Groovy DSL (`build.gradle`):

```groovy
repositories {
    mavenCentral()
    maven {
        url = 'https://www.zenwave360.io/maven-snapshots/'
        mavenContent { snapshotsOnly() }
    }
}
```

Kotlin Multiplatform projects resolve the right variant (JVM, JS, ...) from the root module, for example
`io.zenwave360.dsl:dsl-kotlin`, as with any Maven repository.

To use a snapshot Gradle plugin, add the repository to `pluginManagement` in `settings.gradle.kts`:

```kotlin
pluginManagement {
    repositories {
        maven("https://www.zenwave360.io/maven-snapshots/") {
            mavenContent { snapshotsOnly() }
        }
        gradlePluginPortal()
    }
}
```

To always get the latest snapshot build, run Gradle with `--refresh-dependencies`, or set
`resolutionStrategy.cacheChangingModulesFor(0, "seconds")`.

## How it is published

Every ZenWave project publishes its snapshots here with [git-maven-publisher](https://github.com/ivangsa/git-maven-publisher):
each publication replaces branch `main` with a single commit that contains the whole repository, and GitHub Pages serves
that branch. The branch keeps no history; do not open pull requests against it.
