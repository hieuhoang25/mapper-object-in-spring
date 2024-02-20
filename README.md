# Getting Started

### Reference Documentation
For further reference, please consider the following sections:

* [Official Gradle documentation](https://docs.gradle.org)
* [Spring Boot Gradle Plugin Reference Guide](https://docs.spring.io/spring-boot/docs/3.2.2/gradle-plugin/reference/html/)
* [Create an OCI image](https://docs.spring.io/spring-boot/docs/3.2.2/gradle-plugin/reference/html/#build-image)
* [Spring Web](https://docs.spring.io/spring-boot/docs/3.2.2/reference/htmlsingle/index.html#web)

### Guides
The following guides illustrate how to use some features concretely:

* [Building a RESTful Web Service](https://spring.io/guides/gs/rest-service/)
* [Serving Web Content with Spring MVC](https://spring.io/guides/gs/serving-web-content/)
* [Building REST services with Spring](https://spring.io/guides/tutorials/rest/)

### Intelligent object mapping library
- [ObjectMapper - Jackson](https://fasterxml.github.io/jackson-databind/javadoc/2.7/com/fasterxml/jackson/databind/ObjectMapper.html)
- [ModelMapper](https://modelmapper.org/)
- [MapStruct](https://mapstruct.org/)
- [Orika](https://orika-mapper.github.io/orika-docs/)
### ObjectMapper 
The `ObjectMapper` class is a part of the Jackson library, which is a widely used library for 
JSON processing. Jackson provides a set of tools for reading and writing JSON data, and the `ObjectMapper` class 
is a central component for these operations.
1. JSON Serialization(Java to JSON)
- It can convert Java object into their corresponding JSON representation
- demo
```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class JsonSerializationDemo {
    public static void main(String[] args) throws Exception {
        // Create an instance of the Person class
        Person person = new Person();
        person.setName("John Doe");
        person.setAge(30);

        // Create an ObjectMapper
        ObjectMapper objectMapper = new ObjectMapper();

        // Serialize the Person object to JSON
        String jsonString = objectMapper.writeValueAsString(person);

        // Print the JSON string
        System.out.println("JSON String: " + jsonString);
    }
}
```
2. JSON Deserialization (JSON to Java)
- It can convert JSON data into Java objects
- Demo
```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class JsonDeserializationDemo {
    public static void main(String[] args) throws Exception {
        // JSON string representing a Person
        String jsonString = "{\"name\":\"John Doe\",\"age\":30}";

        // Create an ObjectMapper
        ObjectMapper objectMapper = new ObjectMapper();

        // Deserialize the JSON string to a Person object
        Person person = objectMapper.readValue(jsonString, Person.class);

        // Access the deserialized object's properties
        System.out.println("Name: " + person.getName());
        System.out.println("Age: " + person.getAge());
    }
}
```
3. Object Mapping(General-purpose object mapping)
- It can be used for general-purpose object mapping, not necessarily related to JSON. You can map
objects between different Java types
- Demo
```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class ObjectMappingDemo {
    public static void main(String[] args) throws Exception {
        // Create an instance of PersonDto
        PersonDto personDto = new PersonDto();
        personDto.setName("John Doe");
        personDto.setAge(30);

        // Create an ObjectMapper
        ObjectMapper objectMapper = new ObjectMapper();

        // Map PersonDto to PersonEntity
        PersonEntity personEntity = objectMapper.convertValue(personDto, PersonEntity.class);

        // Access the mapped object's properties
        System.out.println("Mapped Entity: " + personEntity.getFullName() + ", " + personEntity.getYears());

        // Map PersonEntity to PersonDto
        PersonDto mappedDto = objectMapper.convertValue(personEntity, PersonDto.class);

        // Access the reverse-mapped object's properties
        System.out.println("Mapped DTO: " + mappedDto.getName() + ", " + mappedDto.getAge());
    }
}
```
4. Configuration and Customization:
- `ObjectMapper` allows you to configure various aspects of the serialization deserialization process, such as handling of dates, customization of 
property naming conventions, and more.
- Demo
```java
import com.fasterxml.jackson.databind.PropertyNamingStrategy;
import com.fasterxml.jackson.databind.ObjectMapper;

public class ObjectMapperCustomizationDemo {
    public static void main(String[] args) throws Exception {
        ObjectMapper objectMapper = new ObjectMapper();
        
        // Set custom property naming strategy
        objectMapper.setPropertyNamingStrategy(PropertyNamingStrategy.SNAKE_CASE);
        // Ignore unknown properties during deserialization
        objectMapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
        objectMapper.setDateFormat(new StdDateFormat().withColonInTimeZone(true));
        // ... other config
    }
}

```
5. Dependency 
```xml
<dependencies>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.13.0</version> <!-- Check for the latest version -->
    </dependency>
</dependencies>
```
### ModelMapper