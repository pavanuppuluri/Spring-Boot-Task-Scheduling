# Spring Boot Task Scheduling

In Spring Boot, the **@Scheduled** annotation is used to schedule tasks to run at fixed intervals or at a specified time. This feature is useful for automating periodic tasks like sending emails, cleaning up data, or fetching external resources at regular intervals.

## Key Concepts

### 1. **@Scheduled Annotation**
The `@Scheduled` annotation is used to mark a method to be scheduled for execution. Spring Boot provides different ways to define the scheduling rules using this annotation.

```java
@Scheduled(fixedRate = 5000)
public void taskWithFixedRate() {
    System.out.println("Task executed at fixed rate");
}
```

### 2. `@EnableScheduling` Annotation

To enable scheduled tasks in Spring Boot, the `@EnableScheduling` annotation is required in a configuration class.

#### Example:

```java
import org.springframework.scheduling.annotation.EnableScheduling;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
@EnableScheduling
public class MySpringBootApplication {
    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApplication.class, args);
    }
}
```

## 3. Cron Expressions

Cron expressions provide a powerful and flexible way to specify schedules. They allow you to define precise timings for tasks in a Spring Boot application. A cron expression follows this format:

```
second, minute, hour, day of month, month, day of week
```

### Example:

```java
@Scheduled(cron = "0 0 12 * * ?")  // Runs every day at 12:00 PM
public void taskWithCronExpression() {
    System.out.println("Task executed at 12:00 PM every day");
}
```

## Types of Scheduling Configurations

- **fixedRate**: The task will be triggered at a fixed rate (in milliseconds) from the start of the last invocation.
- **fixedDelay**: The task will be triggered after a fixed delay (in milliseconds) from the completion of the last invocation.
- **cron**: A cron expression can be used to specify when the task should be executed. It's useful for more complex scheduling.

## Handling Scheduled Task Threading

By default, Spring Boot creates a thread pool to handle scheduled tasks. However, you can customize the number of threads used for scheduling tasks by configuring the `application.properties` or `application.yml` file.

### Example Configuration:

#### In `application.properties`:

```properties
spring.task.scheduling.pool.size=10
```
This property configures the number of threads available for executing scheduled tasks.

### **Conclusion**

- Spring Boot’s scheduler is a powerful tool for automating repetitive tasks in your application.
- By using the **@Scheduled** annotation, you can easily configure tasks to run at specific intervals or times.
- It provides flexibility through fixed rate, fixed delay, and cron-based scheduling.
- With proper configuration, it helps in optimizing resource usage and automating maintenance tasks such as backups, cleanup, or data syncing.

Make sure to use the scheduler wisely to avoid performance bottlenecks, and always ensure thread safety if your tasks are interacting with shared resources.

