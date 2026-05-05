# maven-simple-code-java


Maven Setup in Linux


# check maven software availability
```bash
$ mvn -version
```
# install maven s/w
```bash
$ sudo apt-get install maven
```

Java Setup in Linux


# check java software availability
```bash
$ java -version
```
# install maven s/w
```bash
$ sudo apt install openjdk-17-jdk -y
```

Creating Maven Project

```bash
  $ cd /home
```
=> Execute below command in cmd to create maven stand-alone application (.jar file create)
```bash
mvn archetype:generate -DgroupId=in.ashokit -DartifactId=my-app-1 -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.5 -DinteractiveMode=false
```
=> Execute below command to create maven web application (.war file create)
```bash
mvn archetype:generate -DgroupId=in.ashokit -DartifactId=my-web-app -DarchetypeArtifactId=maven-archetype-webapp -DarchetypeVersion=1.4 -DinteractiveMode=false
```
=> Navigate into project directory and execute maven goals
```bash
$ cd /home/my-app-1
```
```bash    
$ mvn package -DskipTests=true
```

Maven Dependencies


add pom.xml
```bash
$ vim my-app-1/pom.xml
```
-----------------------------------------------------------------
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>in.ashokit</groupId>
    <artifactId>my-app-1</artifactId>
    <version>1.0-SNAPSHOT</version>

    <name>my-app-1</name>

    <!--  Java Version -->
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <!--  Dependencies (optional) -->
    <dependencies>
        <!-- JUnit (optional testing) -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.11.0</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <!--  Build -->
    <build>
        <plugins>

            <!--  FIX: Compiler plugin (important) -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.13.0</version>
                <configuration>
                    <source>17</source>
                    <target>17</target>
                </configuration>
            </plugin>

            <!--  Make JAR executable -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.4.2</version>
                <configuration>
                    <archive>
                        <manifest>
                            <mainClass>in.ashokit.App</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>

        </plugins>
    </build>

</project>

----------------------------------------------------------------
```bash
$ vim /home/my-app-1/src/main/java/in/ashokit/App.java
```
-----------------------------------------------------
package in.ashokit;

import com.sun.net.httpserver.HttpServer;
import java.io.OutputStream;
import java.net.InetSocketAddress;

public class App {

    public static void main(String[] args) throws Exception {

        // Server start on port 8080
        HttpServer server = HttpServer.create(new InetSocketAddress(8080), 0);

        // API endpoint "/"
        server.createContext("/", exchange -> {
            String response = "Welcome to my page GSV";

            exchange.sendResponseHeaders(200, response.length());

            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        });

        server.start();
        System.out.println("Server started at http://localhost:8080");
    }
}
----------------------------------------------------
```bash
$  mvn clean package
$  java -jar target/my-app-1-1.0-SNAPSHOT.jar
```
go on browser open 
```bash
"ip:8080"
```
