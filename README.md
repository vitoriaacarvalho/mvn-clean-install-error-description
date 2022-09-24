# mvn clean install error description, please help :D
MY POM.XML FILE IS AVAILABLE ON THE MAIN BRANCH

my error (it happens whenever I try to run "mvn clean install"):

![image](https://user-images.githubusercontent.com/101741597/192103943-a8874ada-df51-40ea-a737-0f696e5ef2de.png)

my mvn version and java version:

![image](https://user-images.githubusercontent.com/101741597/192104011-98de5d4f-2f55-4402-a6d1-d7a89b78e9d3.png)


all of the things I've tried to do:

1-
You should add the code into pom.xml like:
<properties> <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding> <maven.compiler.source>1.8</maven.compiler.source> <maven.compiler.target>1.8</maven.compiler.target> </properties>

—------------------------------------------------------------------------------------------------------------------------

2-
If your local jdk version is 11 or 9, 10, and your project's java source/target version is 1.8, and you are using org.projectlombok:lombok package, then you can try to update its version to 1.16.22 or 1.18.12, like this:
<dependency> <groupId>org.projectlombok</groupId> <artifactId>lombok</artifactId> <version>1.16.22</version> </dependency>

—------------------------------------------------------------------------------------------------------------------------

3-
The error occurred because the code is not for the default compiler used there. Paste this code in effective POM before the root element ends, after declaring dependencies, to change the compiler used. Adjust version as you need.
<dependencies> ... </dependencies> <build> <plugins> <plugin> <groupId>org.apache.maven.plugins</groupId> <artifactId>maven-compiler-plugin</artifactId> <configuration> <source>1.8</source> <target>1.8</target> </configuration> </plugin> </plugins> </build>

—------------------------------------------------------------------------------------------------------------------------

4-
make sure java home path is correct. for my case, java home path is wrong in pom file.
<properties> <java.home>/usr/java/jdk1.8.0_45/bin/javac</java.home> </properties> <plugin> <groupId>org.apache.maven.plugins</groupId> <artifactId>maven-compiler-plugin</artifactId> <version>3.5.1</version> <configuration> <verbose>true</verbose> <fork>true</fork> <executable>${java.home}</executable> <compilerVersion>1.8</compilerVersion> <source>1.8</source> <target>1.8</target> </configuration> </plugin>

—------------------------------------------------------------------------------------------------------------------------

5-
In the comments the professor sent this link but it also didn’t work https://mkyong.com/maven/maven-error-invalid-target-release-17/

—------------------------------------------------------------------------------------------------------------------------

6-
I also did this : 
      <plugin>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>3.1</version>
				<configuration>
					<fork>true</fork>
					<executable>C:\Java\zulu17.36.17-ca-jdk17.0.4.1-win_x64\zulu17.36.17-ca-jdk17.0.4.1-win_x64</executable>
					<source>1.8</source>
					<target>1.8</target>
					<compilerArgument>-XDignore.symbol.file</compilerArgument>
				</configuration>
			</plugin>
—------------------------------------------------------------------------------------------------------------------------

Tried these two:
7-
https://projectlombok.org/setup/eclipse (link from the teacher)

8-
https://www.youtube.com/watch?v=980oUmm9E8E&t=179s didn’t change a thing
code: 


—------------------------------------------------------------------------------------------------------------------------

9-
tried deleting the .m2/repository, it did not work!
it’s one of the anwsers here:
https://stackoverflow.com/questions/17223536/failed-to-execute-goal-org-apache-maven-pluginsmaven-compiler-plugin2-3-2comp

—------------------------------------------------------------------------------------------------------------------------
