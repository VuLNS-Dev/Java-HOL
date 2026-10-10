
2. Setup Junit & Jacoco report:
2.1 Setup pom.xml: replace from <properties> tag to the end </build> tag with below content

------------

<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
      <!--VuLNS | Change to Java 17 in the system-->
      <maven.compiler.release>17</maven.compiler.release>
  </properties>

<!--VuLNS | Add JUnit 5.11.0-->
  <dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>org.junit</groupId>
        <artifactId>junit-bom</artifactId>
        <version>5.11.0</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
    </dependencies>
  </dependencyManagement>

  <!--VuLNS | Add JUnit Jupiter-->
  <dependencies>
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter-api</artifactId>
      <scope>test</scope>
    </dependency>
    <!-- Optionally: parameterized tests support -->
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter-params</artifactId>
      <scope>test</scope>
    </dependency>
  </dependencies>

-----------------
In <build> change: maven-SureFire to 3.5.0
  
<plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <!--VuLNS | Upgrad version for Jacoco report-->
          <version>3.5.0</version>  
          <!-- <version>2.22.1</version>   -->
               
        </plugin>  
        
------------------
In <build> add:

<!--VuLNS | Add Jacoco report for Junit-->
        <plugin>
          <groupId>org.jacoco</groupId>
          <artifactId>jacoco-maven-plugin</artifactId>
          <version>0.8.12</version>
          <executions>
            <execution>
                <id>prepare-agent</id>
                <goals>
                    <goal>prepare-agent</goal>
                </goals>
            </execution>
            <execution>
                <id>report</id>
                <phase>verify</phase> <!-- Changed from test to verify -->
                <goals>
                    <goal>report</goal>
                </goals>
            </execution>
          </executions>
        </plugin>


--------------
Run Jacoco cmd:
mvn jacoco:prepare-agent test install jacoco:report
