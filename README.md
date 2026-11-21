Step 1: Stop Jenkins
sudo systemctl stop jenkins


Step 2: Open the configuration file
sudo nano /var/lib/jenkins/config.xml


Step 3: Find this line
<useSecurity>true</useSecurity>


Change it to:
<useSecurity>false</useSecurity>


Step 4: Save the file
- Press Ctrl + O and press Enter.
- Press Ctrl + X to exit.
Step 5: Restart Jenkins
sudo systemctl start jenkins


Step 6: Open Jenkins

Go to:
http://localhost:8080


AZURE PIPELINES

1.Azure devops-organisation
2.New private project
3.IntellijIdea main.java(type program)

i.Average of all marks
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter marks in 3 subjects: ");
        int m1 = sc.nextInt();
        int m2 = sc.nextInt();
        int m3 = sc.nextInt();
        double avg = (m1 + m2 + m3) / 3.0;
        System.out.println("Average = " + avg);
        if (avg >= 90)
            System.out.println("Grade A");
        else if (avg >= 75)
            System.out.println("Grade B");
        else if (avg >= 50)
            System.out.println("Grade C");
        else
            System.out.println("Grade F");
    }
}

ii) bill calcultion
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter units consumed: ");
        int units = sc.nextInt();
        double bill;
        if (units <= 100) {
            bill = units * 1.50;
        }
        else if (units <= 200) {
            bill = 100 * 1.50 +
                   (units - 100) * 2.50;
        }
        else {
            bill = 100 * 1.50 +
                   100 * 2.50 +
                   (units - 200) * 4.00;
        }
        System.out.println("Electricity Bill = Rs. " + bill);
    }
}

iii)simple interest
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter principal amount: ");
        double p = sc.nextDouble();

        System.out.print("Enter rate of interest: ");
        double r = sc.nextDouble();

        System.out.print("Enter time in years: ");
        double t = sc.nextDouble();

        double si = (p * r * t) / 100;

        System.out.println("Simple Interest = " + si);
    }
}

iv)area of circle
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter radius: ");
        double r = sc.nextDouble();

        double area = Math.PI * r * r;

        System.out.println("Area of Circle = " + area);
    }
}


4.mvn compile
mvn package

5.github repo

6 git push
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin<URL>
git push -u origin main

7.azure-pipeline ->new pipeline->github->maven

8.yaml file
trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- task: Maven@3
  inputs:
    mavenPomFile: pom.xml
    goals: clean package
    publishJUnitResults: false

- script: echo 250 | java -cp target/classes Main
  displayName: 'Run Electricity Bill Program'

- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: target
    ArtifactName: jar-file
    publishLocation: Container

9.run and go to jobs

10. check left hand side



AZURE PIPELINES WITH REGRESSION TESTING
1.Intellij idea maven project

2.pom.xml
<dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>5.11.4</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>RELEASE</version>
            <scope>test</scope>
        </dependency>
</dependencies>

3.src/main/java/org.example/
create java class like leap.java etc (main will also be there)

4.inside src/test/java first create a package org.example and then inside it a class leaptest.java)
(note:both must be within org.example)

5.programs
i)arithmetic calculator
Calculator.java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    public int subtract(int a, int b) {
        return a - b;
    }
    public int multiply(int a, int b) {
        return a * b;
    }
    public double divide(int a, int b) {
        if (b == 0) {
            throw new ArithmeticException("Division by zero");
        }
        return (double) a / b;
    }
}

CalculatorTest.java
package org.example;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;
public class CalculatorTest {
    Calculator c = new Calculator();
    @Test
    void testAddition() {
        assertEquals(10, c.add(5, 5));
    }
    @Test
    void testSubtraction() {
        assertEquals(5, c.subtract(10, 5));
    }
    @Test
    void testMultiplication() {
        assertEquals(20, c.multiply(4, 5));
    }
    @Test
    void testDivision() {
        assertEquals(2.0, c.divide(10, 5));
    }
    @Test
    void testDivisionByZero() {
        assertThrows(ArithmeticException.class,
                     () -> c.divide(10, 0));
    }
}

ii)pass or fail
Student.java
public class Student {
    public String result(int marks) {
        if (marks >= 50)
            return "Pass";
        else
            return "Fail";
    }
}
StudentTest.java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class StudentTest {

    Student s = new Student();

    @Test
    void test35() {
        assertEquals("Fail", s.result(35));
    }

    @Test
    void test50() {
        assertEquals("Pass", s.result(50));
    }

    @Test
    void test75() {
        assertEquals("Pass", s.result(75));
    }

iii)leap year
leap.java
package org.example;

public class leap {
    public static int year(int year){
        if((year%400==0)|| (year%4==0 && year % 100!=0)){
            return 1;
        }
        else
        { return 0;}
    }
}
leaptest.java
package org.example;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;
public class leaptest {
    public void leap(){
        assertEquals(1,leap.year(2016),0);
    }
}


iv)10%discount
Discount.java
public class Discount {
    public double calculate(double amount) {
        if (amount >= 1000)
            return amount - (amount * 0.10);
        return amount;
    }
}


 DiscountTest.java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class DiscountTest {

    Discount d = new Discount();

    @Test
    void testBelow1000() {
        assertEquals(900, d.calculate(900));
    }

    @Test
    void testEqual1000() {
        assertEquals(900, d.calculate(1000));
    }

    @Test
    void testAbove1000() {
        assertEquals(1350, d.calculate(1500));
    }
}

6.mvn compile mvn package
7.github push 
8.pipeline new pipeline github maven 
9.yaml file

trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- task: Maven@3
  inputs:
    mavenPomFile: 'pom.xml'
    mavenOptions: '-Xmx3072m'
    javaHomeOption: 'JDKVersion'
    jdkVersionOption: '1.17'
    jdkArchitectureOption: 'x64'
    publishJUnitResults: true
    testResultsFiles: '**/surefire-reports/TEST-*.xml'
    goals: 'package'

10.save and run go check in jobs

JENKINS INSTALLATION
1.Experiment 3 – Install Jenkins in Cloud
AIM:

To install Jenkins in cloud and configure Jenkins.

PROCEDURE:

1. Download the Jenkins key using the wget command.
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key


2. Install Jenkins using the following command.
sudo apt-get install -y jenkins


3. Open the terminal and retrieve the initial administrator password.
sudo cat /var/lib/jenkins/secrets/initialAdminPassword


4. Open the browser and enter the Jenkins URL with port number 8080.
http://<Server-IP>:8080


5. Enter the initial administrator password.
6. Select Install Suggested Plugins.
7. Create an administrator user by entering:
   - Username
   - Password
   - Full name
   - Email ID
8. In the Instance Configuration window, provide the Jenkins URL.
9. Click Save and Finish.
10. Open the Jenkins dashboard and verify that Jenkins is successfully installed.


JENKINS CI
Experiment 4 – Create CI Pipeline Using Jenkins
AIM:

To create and configure a Continuous Integration (CI) pipeline using Jenkins to automate the building and testing of a software project.

PROCEDURE:
1. Open IntelliJ IDEA and create a Maven project named Jenkins-CI-Demo.
2. Create a Java class named Calculator inside src/main/java.
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}


3. Open pom.xml and add the JUnit dependency.
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.10.2</version>
    <scope>test</scope>
</dependency>


4. Create a class named CalculatorTest inside src/test/java.
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

class CalculatorTest {
    @Test
    void testAddition() {
        Calculator calculator = new Calculator();
        assertEquals(5, calculator.add(2, 3));
    }
}


5. Open the IntelliJ terminal and execute:
mvn clean test


6. Create a GitHub repository named Jenkins-CI-Demo.
7. Push the project to GitHub.



8. Start the Jenkins server and verify its status.
sudo systemctl start jenkins
sudo systemctl status jenkins


9. Open Jenkins in the browser using the server IP and port 8080.
10. Log in to the Jenkins dashboard.
11. Click New Item, enter Jenkins-CI-Demo, select Pipeline and click OK.
12. Open Configure and navigate to the Pipeline section.
13. Select Pipeline Script and enter the following script.
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                url: '<GitHub-Repository-URL>'
            }
        }

        stage('Build and Test') {
            steps {
                sh 'mvn clean test'
            }
        }
    }
}


14. Click Save and then Build Now.
15. Open Console Output and verify that the build status is SUCCESS.
16. Navigate to Configure → Build Triggers and enable Poll SCM.
17. Enter the schedule:
H/2 * * * *


18. Modify the expected result in CalculatorTest.java to an incorrect value and push the changes to GitHub.
19. Run the pipeline and verify that the test fails.
20. Correct the expected value, commit and push the changes.
21. Verify that Jenkins automatically triggers the pipeline and completes successfully.

programs
i)salary
Salary.java
import java.util.Scanner;

public class Salary {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Basic Salary: ");
        double basic = sc.nextDouble();

        System.out.print("HRA: ");
        double hra = sc.nextDouble();

        System.out.print("DA: ");
        double da = sc.nextDouble();

        double gross = basic + hra + da;

        System.out.println("Gross Salary: " + gross);
    }
}

ii)pos neg zero
import java.util.Scanner;

public class NumberCheck {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number: ");
        int n = sc.nextInt();

        if (n > 0)
            System.out.println("Positive");
        else if (n < 0)
            System.out.println("Negative");
        else
            System.out.println("Zero");
    }
}

iii)palindrome
import java.util.Scanner;

public class Palindrome {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number: ");
        int n = sc.nextInt();

        int original = n, rev = 0;

        while (n > 0) {
            rev = rev * 10 + n % 10;
            n = n / 10;
        }

        if (original == rev)
            System.out.println("Palindrome");
        else
            System.out.println("Not Palindrome");
    }
}

iv)prime
import java.util.Scanner;

public class Prime {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number: ");
        int n = sc.nextInt();

        boolean prime = n > 1;

        for (int i = 2; i <= Math.sqrt(n); i++) {
            if (n % i == 0) {
                prime = false;
                break;
            }
        }

        if (prime)
            System.out.println("Prime");
        else
            System.out.println("Not Prime");
    }
}

v)factorial
import java.util.Scanner;

public class Factorial {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number: ");
        int n = sc.nextInt();

        long fact = 1;

        for (int i = 1; i <= n; i++) {
            fact = fact * i;
        }

        System.out.println("Factorial: " + fact);
    }
}

vi)fibonacci
import java.util.Scanner;

public class Fibonacci {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter n: ");
        int n = sc.nextInt();

        int a = 0, b = 1;

        for (int i = 1; i <= n; i++) {
            System.out.print(a + " ");
            int c = a + b;
            a = b;
            b = c;
        }
    }
}

vii)multiplication able
import java.util.Scanner;

public class Table {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number: ");
        int n = sc.nextInt();

        for (int i = 1; i <= 10; i++) {
            System.out.println(n + " x " + i + " = " + (n * i));
        }
    }
}

viii)sum of 5 int
import java.util.Scanner;

public class ArraySum {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a[] = new int[5];
        int sum = 0;

        System.out.println("Enter 5 integers:");

        for (int i = 0; i < 5; i++) {
            a[i] = sc.nextInt();
            sum += a[i];
        }

        System.out.println("Sum = " + sum);
    }
}

ix)temp
import java.util.Scanner;

public class Temperature {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter Celsius: ");
        double c = sc.nextDouble();

        double f = (c * 9 / 5) + 32;

        System.out.println("Fahrenheit: " + f);
    }
}

ANSIBLE
sudo apt update
sudo apt install ansible -y
ansible --version

mkdir ansible-stack
cd ansible-stack

ansible-galaxy init prerequisites
ansible-galaxy init PostgreSQL
ansible-galaxy init apache

nano prerequisites/tasks/main.yml

---
- name: Install Git
  apt:
    name: git
    state: present
    update_cache: yes
  
nano PostgreSQL/tasks/main.yml

---
- name: Install PostgreSQL
  apt:
    name: postgresql
    state: present
    update_cache: yes

  nano apache/tasks/main.yml

  ---
- name: Install Apache web server
  apt:
    name: apache2
    state: present
    update_cache: yes

  nano stack.yml

  ---
- name: Install Git, PostgreSQL and Apache
  hosts: localhost
  connection: local
  become: yes

  roles:
    - prerequisites
    - PostgreSQL
    - apache
 
  ansible-playbook stack.yml
  ansible-playbook stack.yml --ask-become-pass
  git --version
  apache2 -version
  curl http://localhost



  ANSIBLE
  mkdir ansible-app
cd ansible-app

nano app.yml

---
- name: Deploy a simple web application
  hosts: localhost
  connection: local
  become: yes

  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
        update_cache: yes

    - name: Create application directory
      file:
        path: /var/www/html
        state: directory

    - name: Create application webpage
      copy:
        content: "<h1>Welcome to Ansible Application</h1>"
        dest: /var/www/html/index.html

    - name: Start Apache service
      service:
        name: apache2
        state: started
        enabled: yes
      ansible-playbook app.yml
      ansible-playbook app.yml --ask-become-pass
      sudo systemctl status apache2
      curl http://localhost


      
GRADLE APPLICATION
Step 1: Install Java and Gradle
sudo apt update
sudo apt install openjdk-21-jdk gradle -y


Verify:
java -version
gradle -version


Step 2: Create Gradle project
mkdir SimpleInterest
cd SimpleInterest
mkdir -p src/main/java


Step 3: Create Java program
src/main/java/Main.java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter Principal: ");
        double p = sc.nextDouble();

        System.out.print("Enter Rate: ");
        double r = sc.nextDouble();

        System.out.print("Enter Time: ");
        double t = sc.nextDouble();

        double si = (p * r * t) / 100;

        System.out.println("Simple Interest: " + si);
    }
}


Step 4: Create Gradle build file
build.gradle
plugins {
    id 'java'
}

jar {
    manifest {
        attributes 'Main-Class': 'Main'
    }
}


Step 5: Build the project
gradle build


Step 6: Verify generated artifacts
ls build/libs


The JAR file will be generated inside:
build/libs/


Step 7: Execute the application
java -cp build/libs/SimpleInterest.jar Main


PROGRAMS
i)average of 5numbers
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int a[] = new int[5];
        int sum = 0;

        System.out.println("Enter five numbers:");

        for (int i = 0; i < 5; i++) {
            a[i] = sc.nextInt();
            sum += a[i];
        }

        double avg = sum / 5.0;

        System.out.println("Average: " + avg);
    }
}

ii)vowel
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter character: ");
        char ch = sc.next().toLowerCase().charAt(0);

        if (ch == 'a' || ch == 'e' || ch == 'i' ||
            ch == 'o' || ch == 'u') {
            System.out.println("Vowel");
        }
        else {
            System.out.println("Consonant");
        }
    }
}

iii)import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter Length: ");
        double l = sc.nextDouble();

        System.out.print("Enter Breadth: ");
        double b = sc.nextDouble();

        double area = l * b;
        double perimeter = 2 * (l + b);

        System.out.println("Area: " + area);
        System.out.println("Perimeter: " + perimeter);
    }
}

ansible three roles
tep 1: Install Ansible
sudo apt update
sudo apt install ansible -y


Verify:
ansible --version


Step 2: Create project directory
mkdir stackproject
cd stackproject


Step 3: Create roles
ansible-galaxy init prerequisites
ansible-galaxy init postgresql
ansible-galaxy init apache


Step 4: Configure prerequisites role
Open:
nano prerequisites/tasks/main.yml


prerequisites/tasks/main.yml
---
- name: Install Git
  apt:
    name: git
    state: present
    update_cache: yes


Step 5: Configure PostgreSQL role
Open:
nano postgresql/tasks/main.yml


postgresql/tasks/main.yml
---
- name: Install PostgreSQL
  apt:
    name: postgresql
    state: present

- name: Start PostgreSQL
  service:
    name: postgresql
    state: started
    enabled: yes


Step 6: Configure Apache role
Open:
nano apache/tasks/main.yml


apache/tasks/main.yml
---
- name: Install Apache
  apt:
    name: apache2
    state: present

- name: Start Apache
  service:
    name: apache2
    state: started
    enabled: yes


Step 7: Create stack.yml
nano stack.yml


stack.yml
---
- name: Configure Stack
  hosts: localhost
  connection: local
  become: yes

  roles:
    - prerequisites
    - postgresql
    - apache


Step 8: Execute the playbook
ansible-playbook -i localhost, -c local stack.yml


Step 9: Verify Git
git --version


Step 10: Verify PostgreSQL
sudo systemctl status postgresql


Step 11: Verify Apache
sudo systemctl status apache2


Step 12: Verify Apache using HTTP
curl http://localhost


Result
Three Ansible roles were successfully created and executed. Git, PostgreSQL and Apache were installed, and the required services were configured.

















Experiment 1 – Create Maven Build Pipeline in Azure
AIM:

To build a Maven build pipeline in Azure DevOps.

PROCEDURE:
1. Open the Azure DevOps website and sign in using a GitHub account.
2. Create a new organization with a suitable name.
3. Create a new private project named DevOps.
4. Install IntelliJ IDEA and ensure Java is installed.
5. Open IntelliJ IDEA and create a new Maven project using Java.
6. Write the Java program and open the terminal.
7. Install Maven and execute the following commands:
sudo apt install maven
mvn compile
mvn package


8. Install and configure Git.
git --version
sudo apt install git
git init
git add .
git commit -m "First Commit"
git branch -M master
git remote add origin <GitHub-Repository-URL>
git push -u origin master


9. Open Azure DevOps and select the created project.
10. Click Pipelines → New Pipeline.
11. Select GitHub as the source and authorize access.
12. Select the created GitHub repository.
13. Choose the Maven pipeline option.
14. Configure the JDK version as 17 in the YAML file.
15. Click Save and Run to execute the pipeline.
16. Verify the successful execution in the Jobs section.
RESULT:

Thus, a Maven build pipeline was successfully created using Azure DevOps.

Experiment 2 – Run Regression Tests Using Maven Build Pipeline in Azure
AIM:

To run regression tests using the Maven build pipeline in Azure.

PROCEDURE:
1. Open IntelliJ IDEA and create a new Maven project named RegressionTesting.
2. Select Maven as the build system and choose the available JDK version.
3. Enable the Create Git Repository option.
4. Open pom.xml and add the JUnit dependency.
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.11.4</version>
    <scope>test</scope>
</dependency>


5. Create a package named org.example inside src/test/java.
6. Create a Java class named MainTest.
7. Write the JUnit test case using @Test and assertEquals().
package org.example;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class MainTest {
    @Test
    public void testTemperatureConversion() {
        assertEquals(77.0,
            Main.celsiusToFahrenheit(25), 0.001);
    }
}


8. Create a GitHub repository named RegressionTesting.
9. Execute the following Git commands:
git init
git add .
git commit -m "regression"
git branch -M main
git remote add origin <GitHub-Repository-URL>
git push -u origin main


10. Run the MainTest class in IntelliJ IDEA and verify the test result.
11. Open Azure DevOps and select the existing project.
12. Navigate to Pipelines → New Pipeline.
13. Select GitHub and choose the RegressionTesting repository.
14. Authorize access if prompted and choose Maven.
15. Configure the generated azure-pipelines.yml file with the following:
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

steps:
- task: Maven@3
  displayName: 'Build and run JUnit tests'
  inputs:
    mavenPomFile: 'pom.xml'
    mavenOptions: '-Xmx3072m'
    javaHomeOption: 'JDKVersion'
    jdkVersionOption: '1.17'
    jdkArchitectureOption: 'x64'
    goals: 'clean test'
    publishJUnitResults: true
    testResultsFiles: '**/surefire-reports/TEST-*.xml'
    testRunTitle: 'RegressionTest JUnit Results'


16. Click Save and Run to execute the pipeline.
17. Open the test results tab and verify that the regression tests have passed.
RESULT:

Thus, regression tests were successfully executed using the Maven build pipeline in Azure.

Experiment 3 – Install Jenkins in Cloud
AIM:

To install Jenkins in cloud and configure Jenkins.

PROCEDURE:

1. Download the Jenkins key using the wget command.
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key


2. Install Jenkins using the following command.
sudo apt-get install -y jenkins


3. Open the terminal and retrieve the initial administrator password.
sudo cat /var/lib/jenkins/secrets/initialAdminPassword


4. Open the browser and enter the Jenkins URL with port number 8080.
http://<Server-IP>:8080


5. Enter the initial administrator password.
6. Select Install Suggested Plugins.
7. Create an administrator user by entering:
   - Username
   - Password
   - Full name
   - Email ID
8. In the Instance Configuration window, provide the Jenkins URL.
9. Click Save and Finish.
10. Open the Jenkins dashboard and verify that Jenkins is successfully installed.
RESULT:

Thus, Jenkins was successfully installed and configured in the cloud.

Experiment 4 – Create CI Pipeline Using Jenkins
AIM:

To create and configure a Continuous Integration (CI) pipeline using Jenkins to automate the building and testing of a software project.

PROCEDURE:
1. Open IntelliJ IDEA and create a Maven project named Jenkins-CI-Demo.
2. Create a Java class named Calculator inside src/main/java.
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}


3. Open pom.xml and add the JUnit dependency.
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.10.2</version>
    <scope>test</scope>
</dependency>


4. Create a class named CalculatorTest inside src/test/java.
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

class CalculatorTest {
    @Test
    void testAddition() {
        Calculator calculator = new Calculator();
        assertEquals(5, calculator.add(2, 3));
    }
}


5. Open the IntelliJ terminal and execute:
mvn clean test


6. Create a GitHub repository named Jenkins-CI-Demo.
7. Push the project to GitHub.
git init
git add .
git commit -m "First Commit"
git branch -M main
git remote add origin <GitHub-Repository-URL>
git push -u origin main


8. Start the Jenkins server and verify its status.
sudo systemctl start jenkins
sudo systemctl status jenkins


9. Open Jenkins in the browser using the server IP and port 8080.
10. Log in to the Jenkins dashboard.
11. Click New Item, enter Jenkins-CI-Demo, select Pipeline and click OK.
12. Open Configure and navigate to the Pipeline section.
13. Select Pipeline Script and enter the following script.
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                url: '<GitHub-Repository-URL>'
            }
        }

        stage('Build and Test') {
            steps {
                sh 'mvn clean test'
            }
        }
    }
}


14. Click Save and then Build Now.
15. Open Console Output and verify that the build status is SUCCESS.
16. Navigate to Configure → Build Triggers and enable Poll SCM.
17. Enter the schedule:
H/2 * * * *


18. Modify the expected result in CalculatorTest.java to an incorrect value and push the changes to GitHub.
19. Run the pipeline and verify that the test fails.
20. Correct the expected value, commit and push the changes.
21. Verify that Jenkins automatically triggers the pipeline and completes successfully.
RESULT:

Thus, a Jenkins CI pipeline was successfully created and tested, demonstrating automatic build execution, failure detection and successful rebuilding after correction.

Experiment 5 – Create a CD Pipeline in Jenkins
AIM:

To create a Jenkins pipeline that automatically checks out, builds and tests an application, and sends an email notification with the result of each build.

PROCEDURE:

1. Start the Jenkins server in Ubuntu.
sudo systemctl start jenkins
sudo systemctl status jenkins


2. Open Jenkins in the browser using the server IP and port 8080 and log in.
3. Navigate to Manage Jenkins → Manage Plugins.
4. Search for and install the Email Extension Plugin.
5. Navigate to Manage Jenkins → System → E-mail Notification.
6. Enter localhost as the SMTP server.
7. Under Advanced settings, disable SMTP Authentication and SSL. Set the SMTP port to 1025.
8. Click Apply and Save.
9. Go to the Jenkins homepage and click New Item.
10. Enter a job name, select Pipeline and click OK.
11. In the Pipeline section, enter the following script.
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                git branch: 'main',
                url: '<GitHub-Repository-URL>'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'echo Build completed'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo Tests passed'
            }
        }
    }

    post {
        success {
            mail to: '<your-email>',
            subject: "Build SUCCESS - ${env.JOB_NAME}",
            body: "Pipeline completed successfully."
        }

        failure {
            mail to: '<your-email>',
            subject: "Build FAILED - ${env.JOB_NAME}",
            body: "Pipeline execution failed."
        }
    }
}


12. Start the MailHog server using Docker.
sudo docker run -d -p 1025:1025 -p 8025:8025 mailhog/mailhog


13. Open http://localhost:8025 to access the MailHog inbox.
14. Execute the Jenkins pipeline and verify that Checkout, Build, Test and Post Actions complete successfully.
15. Open MailHog and verify that the email notification is received.
RESULT:

Thus, a CD pipeline was successfully created and executed in Jenkins, and an email notification was received.

Experiment 6 – Create an Ansible Playbook for a Simple Web Application Infrastructure
AIM:

To create an Ansible Playbook for a simple web application infrastructure.

PROCEDURE:

1. Create a directory named ansible-webapp and navigate into it.
mkdir -p ~/ansible-webapp
cd ~/ansible-webapp


2. Create a playbook file named webapp.yml.
nano webapp.yml


3. Write the Ansible playbook to install Apache, start the service and deploy the web application.
---
- name: Deploy a Simple Web Application
  hosts: localhost
  connection: local
  become: true

  tasks:
    - name: Install Apache web server
      ansible.builtin.apt:
        name: apache2
        state: present
        update_cache: true

    - name: Start and enable Apache
      ansible.builtin.service:
        name: apache2
        state: started
        enabled: true

    - name: Deploy the web application
      ansible.builtin.copy:
        dest: /var/www/html/index.html
        content: |
          <!DOCTYPE html>
          <html>
          <head>
            <title>My Ansible Web App</title>
          </head>
          <body>
            <h1>Hello from Ansible!</h1>
            <p>My web application was deployed automatically.</p>
          </body>
          </html>
        mode: "0644"

    - name: Verify the web application
      ansible.builtin.uri:
        url: http://127.0.0.1/
        status_code: 200
      register: web_result

    - name: Display deployment status
      ansible.builtin.debug:
        msg: "Web application deployed successfully!"


4. Save and exit the file.
5. Execute the Ansible playbook.
ansible-playbook webapp.yml --ask-become-pass


6. Verify whether Apache is running.
sudo systemctl status apache2


7. Check the deployed web application using:
curl http://localhost


8. Open the browser and enter http://localhost to verify the web page.

RESULT:

Thus, an Ansible playbook was successfully created and executed to deploy a simple web application infrastructure.

Experiment 7a – Build a Simple Application Using Gradle
AIM:

To build a simple Java application using Gradle.

PROCEDURE:

1. Install Gradle.
sudo snap install gradle --classic


2. Create a directory named java_application.
mkdir java_application


3. Navigate into the directory.
cd java_application


4. Initialize the Gradle project.
gradle init


5. Select the project type as Application.
6. Select the implementation language as Java.
7. Enter the target Java version.
8. Enter the project name as java_application.
9. Select the application structure as Single Application Project.
10. Select the build script DSL as Groovy.
11. Select the testing framework as JUnit 4.
12. Choose not to generate the build using new APIs and behavior.
13. Install the tree command to display the directory structure.
sudo apt install tree -y
tree


14. Run the Gradle application.
./gradlew run


15. Modify App.java to perform arithmetic operations such as addition, subtraction, multiplication and division.
16. Change the package name in the Java program and update the mainClass in build.gradle accordingly.
17. Execute the application again.
./gradlew run


18. Initialize Git.
git init


19. Add the files.
git add .


20. Check the Git status.
git status


21. Commit the changes.
git commit -m "first commit"


22. Add the GitHub remote repository and push the project.
git remote add origin <GitHub-Repository-URL>
git push -u origin main


RESULT:

Thus, a simple Java application was successfully created and executed using Gradle.

Experiment 7b – Build a Simple Application Using Gradle in IntelliJ IDEA
Important: Gradle + Selenium + JAR + GitHub Pages
AIM:

To build a simple application using Gradle in IntelliJ IDEA, including Selenium testing and JAR packaging.

PROCEDURE:

1. Install Gradle and verify the installation.
sudo snap install gradle --classic
gradle --version


2. Open IntelliJ IDEA and click New Project.
3. Select Java and choose Gradle as the build system.
4. Select JDK version 17.
5. Choose Groovy or Kotlin DSL for the build script.
6. Set the Group ID as com.example and click Create.
7. Modify the build.gradle file by configuring the required plugins, repositories and dependencies.
8. Create Main.java inside src/main/java/com/example.
9. Write the Java application code.
10. Open the Gradle tool window using View → Tool Windows → Gradle.
11. Run the application using Tasks → application → run, or execute:
gradle run


12. Create a docs directory in the root folder.
13. Create an index.html file inside the docs directory.
14. Add HTML, CSS and images inside the docs folder to create a static website.
15. Open GitHub and create a new repository.
16. Change the IntelliJ terminal from Local to Bash.
17. Initialize Git.
git init


18. Add the project files.
git add .


19. Check the Git status.
git status


20. Commit the changes.
git commit -m "first commit"


21. Add the GitHub repository as the remote and push the code.
git remote add origin <GitHub-Repository-URL>
git push -u origin main


22. Build and package the JAR file.
gradle jar


23. Execute the generated JAR file.
java -jar ./build/libs/DevOps-Demo.jar


24. Open the GitHub repository and navigate to Settings → Pages.
25. Change the branch from None to master and select /docs.
26. Click Save to enable GitHub Pages.
27. Open the generated website link and verify that the website is live.

Experiment 8 – Install Ansible and Configure Ansible Roles and Write Playbooks
AIM:

To install Ansible, configure Ansible roles and write playbooks.

PROCEDURE:

1. Update the system package index.
sudo apt update


2. Upgrade the packages and install the required software.
sudo apt upgrade
sudo apt install -y software-properties-common


3. Add the Ansible PPA repository.
sudo add-apt-repository --yes --update ppa:ansible/ansible


4. Install Ansible.
sudo apt install ansible


5. Navigate to the Ansible configuration directory and check the version.
cd /etc/ansible/
ansible --version


6. List the files and directories and check the hosts file.
ls -la
sudo nano hosts


7. Create an Ansible role using the Ansible Galaxy command.
sudo ansible-galaxy init role-name
ls
tree role-name


8. Create three Ansible roles: prerequisites, PostgreSQL and Apache.
sudo ansible-galaxy init prerequisites
sudo ansible-galaxy init PostgreSQL
sudo ansible-galaxy init apache


9. Configure the prerequisites role to install Git. Navigate to its tasks directory.
cd prerequisites/tasks/
sudo nano main.yml


Add the following content:
- name: Install git
  apt:
    name: git
    state: present
    update_cache: yes


10. Configure the PostgreSQL role.
cd /etc/ansible/PostgreSQL/tasks/
sudo nano main.yml


Add the following content:
- name: Install PostgreSQL
  apt:
    name: postgresql
    state: present
    update_cache: yes

- name: Start PostgreSQL service
  systemd:
    name: postgresql
    state: started
    enabled: yes


11. Configure the Apache role.
cd /etc/ansible/apache/tasks/
sudo nano main.yml


Add the following content:
- name: Install Apache web server
  apt:
    name: apache2
    state: present
    update_cache: yes


12. Create a playbook named stack.yml to execute all three roles.
cd /etc/ansible/
sudo nano stack.yml


Add the following content:
- hosts: localhost
  become: true
  roles:
    - prerequisites
    - PostgreSQL
    - apache


13. Execute the Ansible playbook.
sudo ansible-playbook stack.yml


14. Verify that the required packages have been installed successfully.
git --version
apache2 -v


RESULT:
