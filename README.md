# Maven Snapshots Branch

Since [Central Publisher Portal does not currently support SNAPSHOT releases](https://central.sonatype.org/faq/snapshot-releases/) we set up this repo to host ZenWaveSDK SNAPSHOT versions.

Add this repository to your pom.xml to access these SNAPSHOTS:

```xml
	<repositories>
		<repository>
			<id>gh</id>
			<url>https://raw.githubusercontent.com/ZenWave360/maven-snapshots/refs/heads/main</url>
			<snapshots>
				<enabled>true</enabled>
			</snapshots>
		</repository>
	</repositories>
```

