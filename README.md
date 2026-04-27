## Performance Testing

### 1. Testing `/all-student-name`

I created a test plan in JMeter to test the `/all-student-name` endpoint.  
The test simulates 10 users sending requests at the same time.

After running the test in GUI mode, I observed the response times and status of each request.

![All Student Name GUI Result](images/all-student-name-test.jpeg)

From the results above, all requests were processed successfully and the response times are shown in milliseconds. This shows how fast the endpoint responds under multiple users.

I also ran the same test using the command line (non-GUI mode) to get the result log file.

![All Student Name CLI Result](images/results2.png)
---
### 2. Testing `/highest-gpa`

Next, I created another test plan for the `/highest-gpa` endpoint using the same configuration (10 users, 1 second ramp-up).

After running the test in GUI mode, I checked the results:
![Highest GPA GUI Result](images/highest-gpa-test.jpeg)
The results show the response time for each request. All requests were successful, which means the endpoint works correctly under load.

I also executed this test using the command line:
![Highest GPA CLI Result](images/results3.png)

## Performance Optimization Results

### CPU Profiling (After Optimization)

After optimizing the methods in `StudentService`, I ran the profiler again to check the CPU time.

The main improvements were in:
- `getAllStudentsWithCourses()`
- `joinStudentNames()`
- `findStudentWithHighestGpa()`

After refactoring, the CPU time for these methods decreased. This means that the code is now more efficient compared to the previous version.

---
## JMeter Performance Testing (After Optimization)

### /all-student
![All Student Test](images/all-students-optimized.png)
---
### /all-student-name
![All Student Name Test](images/all-students-name-optimized.png)
---
### /highest-gpa
![Highest GPA Test](images/highest-gpa-optimized.png)
---

## Compare JMeter output
After running JMeter again, the response times are faster compared to the first test. The endpoints now handle requests more efficiently, and the sample times are lower than before.

---
## Reflection

**1. Difference between JMeter and IntelliJ Profiler**

JMeter is used for performance testing, which means it simulates multiple users sending requests to the application and measures response time and system behavior under load. IntelliJ Profiler is used for code-level analysis, which helps identify which methods consume the most CPU time.

---

**2. How profiling helps identify weak points**

Profiling helps identify weak points by providing detailed information about how long each method takes to execute and how much CPU it uses. By analyzing this data, it becomes easier to locate inefficient parts of the code without relying on assumptions. This allows a more focused approach when improving performance.

---

**3. Effectiveness of IntelliJ Profiler**

IntelliJ Profiler is effective because it provides clear and detailed insights into application performance. It highlights the methods that consume the most resources and presents them in an easy-to-understand way, such as through flame graphs and method lists. This makes it easier to identify bottlenecks and understand how the application behaves during execution.

---

**4. Challenges in performance testing and profiling**

One of the main challenges is inconsistent results, especially due to JVM warm-up and background processes. It can also be difficult to distinguish between application code and framework-related methods. To overcome these challenges, tests are repeated multiple times, and only relevant application methods are analyzed to ensure more reliable results.

---

**5. Benefits of using IntelliJ Profiler**

The main benefit of using IntelliJ Profiler is that it helps identify performance issues at a detailed level. It allows developers to see exactly which methods are inefficient and understand how resources are being used. This makes optimization more targeted and reduces unnecessary trial and error.

---

**6. Handling inconsistent results between JMeter and Profiler**

When results between JMeter and the profiler are not consistent, it is important to understand that they measure different aspects of performance. JMeter focuses on overall response time, while the profiler focuses on CPU usage. To handle this, results are compared carefully, repeated tests are conducted, and conclusions are based on consistent patterns rather than single measurements.

---

**7. Strategies for optimizing code and ensuring correctness**

After analyzing the results, optimization is done by reducing unnecessary operations, improving data handling, and using more efficient methods. To ensure the application still works correctly, all endpoints are tested again after changes are made. The outputs are compared with the previous version to confirm that the functionality remains unchanged while performance improves.