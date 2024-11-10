# SecuriTease

The Sassy Security Checker

## Development setup

> **Requirements:** Java 23 & Maven

### Installation

1. Install dependencies:
```sh
mvn clean install
```

2. Get classpath of dependencies:
```sh
mvn dependency:build-classpath -Dmdep.outputFile=.classpath
```

### Runing the source code

3. Compile the project:
```sh
mvn clean compile
```

4. Run the project (classpath was exported in step *2* into the `.classpath` file):
```sh
java -cp "target/classes:CONTENT_OF_.classpath_FILE" com.diepoe.SecuriTeaseApp
```

### Testing

#### run unit tests

```sh
mvn clean test
```

#### run grading testing program

1. Package the project
```sh
mvn clean package
```

2. Run the test program
```sh
java -cp "target/classes:CONTENT_OF_.classpath_FILE" com.cthiebaud.PasswordValidatorTester $PWD/target/securitease-1.0.0-SNAPSHOT.jar
```


## Project structure
(Draft)
```mermaid
classDiagram
    ValidationResult -- PasswordValidator
    PasswordValidator <|-- SecuriTease : implements
    SecuriTease <.. SecuriTeaseApp
    
    namespace com.diepoe {
        class SecuriTeaseApp {
            +void main()$
        }

        class com.diepoe.securitease
    }

    namespace com.diepoe.securitease {
        class SecuriTease {
            +ValidationResult validate(String potentialPassword)
        }
    }

    %% given by @cthiebaud:

    namespace com.cthiebaud{
        class PasswordValidatorTester {
            +void main()$
            -List&lt;Class&lt;?&gt;&gt; findPasswordValidatorClasses()$
            -void printBigOK()$
        }

        class com.cthiebaud.passwordvalidator
    }
    PasswordValidator <.. PasswordValidatorTester
    SecuriTease <.. PasswordValidatorTester
    ValidationResult <.. PasswordValidatorTester

    namespace com.cthiebaud.passwordvalidator{
        class ValidationResult {
            boolean isValid
            String message
        }
        
        class PasswordValidator {
            ValidationResult validate(String potentialPassword)
        }
    }

    <<record>> ValidationResult
    <<interface>> PasswordValidator

```