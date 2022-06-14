## Demo

```xml
<!--snakeyaml in pom.xml-->
<dependency>
    <groupId>org.yaml</groupId>
    <artifactId>snakeyaml</artifactId>
    <version>1.30</version>
</dependency>
```

```java
package dev.zlab.learn;

import dev.zlab.learn.entity.Student;
import org.yaml.snakeyaml.Yaml;
import org.yaml.snakeyaml.constructor.Constructor;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.InputStream;
import java.util.Map;

public class MyApplication {

    public static void main(String[] args) throws FileNotFoundException {
        myTest1();
        myTest2();
    }

    public static void myTest1() throws FileNotFoundException {
        InputStream input = new FileInputStream("./src/main/resources/app.yaml");
        Yaml yaml = new Yaml();
        Map<String, Object> data = yaml.load(input);
        System.out.println(data.get("name"));
        System.out.println(data.get("courses"));
        System.out.println(data);
    }

    public static void myTest2() throws FileNotFoundException {
        InputStream input = new FileInputStream("./src/main/resources/app.yaml");
        Yaml yaml = new Yaml(new Constructor(Student.class));
        Student data = yaml.load(input);
        System.out.println(data.getAddress());
        System.out.println(data.getCourses().get(1).getName());
    }
}
```

```java
// myTest2() need these class
// it needs all Getters and setters

public class Person {
    private long id;
    private String name;
    private String address;
    // Getters and setters
}

public class Student extends Person {
    private int year;
    private String department;
    private List<Course> courses;
    // Getters and setters
}

public class Course {
    private String name;
    private double credits;
    // Getters and setters
}
```


```yaml
# test data
# ./src/main/resources/app.yaml
id: 20
name: Bruce
year: 2020
address: Gotham City
department: Computer Science
courses:
  - name: Algorithms
    credits: 6
  - name: Data Structures
    credits: 5
  - name: Design Patterns
    credits: 3
```


## Docs
https://bitbucket.org/snakeyaml/snakeyaml/wiki/Documentation  
https://stackabuse.com/reading-and-writing-yaml-files-in-java-with-snakeyaml  
