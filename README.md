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
Step 1: Install Ansible
sudo apt update
sudo apt install ansible -y


Step 2: Create project directory
mkdir ansible20
cd ansible20
nano webapp.yml


Step 3: Write the playbook
webapp.yml
---
- name: Configure Web Application
  hosts: localhost
  connection: local
  become: yes

  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
        update_cache: yes

    - name: Start and enable Apache
      service:
        name: apache2
        state: started
        enabled: yes

    - name: Deploy HTML page
      copy:
        content: |
          <html>
          <body>
          <h1>Welcome to Web Application</h1>
          <p>This is a simple web application
          configured using Ansible.</p>
          </body>
          </html>
        dest: /var/www/html/index.html

    - name: Verify web application
      uri:
        url: http://localhost
        status_code: 200


Step 4: Execute playbook
ansible-playbook -i localhost, -c local webapp.yml


Step 5: Check Apache service
sudo systemctl status apache2


Step 6: Verify website
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

