# Jackson Object Stream

![GitHub release (latest by date)](https://img.shields.io/github/v/release/autonomouslogic/jackson-object-stream)
[![GitHub Workflow Status (branch)](https://img.shields.io/github/workflow/status/autonomouslogic/jackson-object-stream/Test/main)](https://github.com/autonomouslogic/jackson-object-stream/actions)
[![Known Vulnerabilities](https://snyk.io/test/github/autonomouslogic/jackson-object-stream/badge.svg)](https://snyk.io/test/github/autonomouslogic/jackson-object-stream)
[![Libraries.io dependency status for latest release](https://img.shields.io/librariesio/release/maven/com.autonomouslogic.jacksonobjectstream:jackson-object-stream)](https://libraries.io/maven/com.autonomouslogic.jacksonobjectstream:jackson-object-stream)
[![GitHub](https://img.shields.io/github/license/autonomouslogic/jackson-object-stream)](https://spdx.org/licenses/MIT-0.html)

A small library which handles reading and writing a series of JSON objects from a text file.

## Dependency

Available from [Maven Central](https://search.maven.org/search?q=g:com.autonomouslogic.jacksonobjectstream%20AND%20a:jackson-object-stream&core=gav).

### Gradle

```groovy
implementation 'com.autonomouslogic.jacksonobjectstream:jackson-object-stream:$version'
```

### Maven

```xml
<dependency>
  <groupId>com.autonomouslogic.jacksonobjectstream</groupId>
  <artifactId>jackson-object-stream</artifactId>
  <version>$version</version>
</dependency>
```

## Reading a JSON stream

Objects are read from the files one by one.
Any whitespace or formatting will be ignored by Jackson, so there are no special formatting requirements.

```java
JacksonObjectStreamFactory factory = new JacksonObjectStreamFactory(new ObjectMapper());
try (JacksonObjectIterator<TestObject> iterator = factory.createReader(new File("users.json"), User.class)) {
    while(iterator.hasNext()) {
        User user = iterator.next();
        // Use user for something.
    }
}
```

## Writing a JSON stream

Objects will be written to the output one by one.
After each object, a newline will be inserted.
Pretty printing is not supported at this time.

```java
JacksonObjectStreamFactory factory = new JacksonObjectStreamFactory(new ObjectMapper());
try (JacksonObjectStreamWriter writer = factory.createWriter(new File("users.json"))) {
    writer.writeObject(user1);
    writer.writeObject(user2);
    // etc.
}
```

## Doesn't Jackson support this already?
Jackson does support writing JSON to files.
This is a tiny library that simply provides the plumbing needed to do so effectively, and provides a few convenience
methods at the same time.

## License
This library is licensed under the [MIT-0 license](https://spdx.org/licenses/MIT-0.html).
