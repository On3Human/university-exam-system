# UniManagementSystem

A desktop Java application that handles users, exams, and grading for a university environment.

I built this to provide a straightforward way for lecturers to create and publish exams and for students to take them and leave feedback. It removes the overhead of complex database setups by keeping everything local and self-contained.

### Tech Stack
Java 21 and Swing for the user interface. It doesn't rely on external libraries or frameworks. Persistence is handled entirely through native Java object serialization.

### Running It
You can run the pre-compiled jar directly if you have Java installed:

```bash
java -jar UniSystem.jar
```

If you want to build it from source yourself:

```bash
javac -d out $(find src -name "*.java")
jar cfe UniSystem.jar Main -C out .
java -jar UniSystem.jar
```

### Prerequisites
You need JDK 21 or higher to build and run the project.

### Configuration
There are no environment variables or external configuration files to set up. On startup, the application seeds a default admin account:
* Username: admin
* Password: admin123

All application state is saved locally to a `university_data.ser` file in the current working directory.

### Architecture and Limitations
The UI is built with standard Java Swing components separated roughly into auth, admin, lecturer, and student views. `DataManager.java` acts as a singleton repository. It writes the entire users map and exams list to disk whenever data changes.

This serialization approach works for a single-user desktop app, but it means concurrency isn't supported. Schema migrations are also not a thing here. If you modify the domain models without carefully managing `serialVersionUID`, the `university_data.ser` file will become unreadable. When that happens, you'll have to delete the file and start fresh.

### License
GPL-3.0