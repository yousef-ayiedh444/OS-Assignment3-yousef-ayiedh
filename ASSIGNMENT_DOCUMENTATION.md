# Assignment 3 - Complete Documentation

**Student Name**: [yousef alshalawi]  
**Student ID**: [444051021]  
**Date Submitted**: [Submission Date]

---

## 🎥 VIDEO DEMONSTRATION LINK (REQUIRED)

> **⚠️ IMPORTANT: This section is REQUIRED for grading!**
> 
> Upload your 3-5 minute video to your **PERSONAL Gmail Google Drive** (NOT university email).
> Set sharing to "Anyone with the link can view".
> Test the link in incognito/private mode before submitting.

**Video Link**: [Paste your personal Gmail Google Drive link here]

**Video filename**: `[YourStudentID]_Assignment3_Synchronization.mp4`

**Verification**:
- [ ] Link is accessible (tested in incognito mode)
- [ ] Video is 3-5 minutes long
- [ ] Video shows code walkthrough and commits
- [ ] Video has clear audio
- [ ] Uploaded to PERSONAL Gmail (not @std.psau.edu.sa)

---

## Part 1: Development Log (1 mark)

Document your development process with **minimum 3 entries** showing progression:

### Entry 1 - [april 30,2026, 4:00pm]
**What I implemented**: 
I began by identifying shared resources in the code and comprehending the assignment criteria
**Challenges encountered**: 
Understanding the locations of racial conditions was challenging
**How I solved it**: 
I carefully examined the code to find shared variables that were accessed by several threads
**Testing approach**: 
In order to see inconsistent behavior, I ran the software several times
**Time spent**: 
2 hours
---

### Entry 2 - [april 30,2026, 8:00pm]
**What I implemented**: 
To safeguard shared counters, I created ReentrantLock
**Challenges encountered**: 
knowing the proper locations for lock() and unlock()
**How I solved it**: 
To guarantee correct unlocking, I employed try-finally blocks
**Testing approach**: 
After several runs, I verified that the values were constant
**Time spent**: 
2 hours
---

### Entry 3 - [may 1,2026, 3:00pm]
**What I implemented**: 
I used a semaphore to manage CPU access
**Challenges encountered**: 
Know how to use acquire() and release()
**How I solved it**: 
I used a semaphore in the try-finally run() method
**Testing approach**: 
minimized concurrency and adhered to execution order
**Time spent**: 
2 hours
---

### Entry 4 - [may 1,2026, 9:00pm]
**What I implemented**: 
I used a semaphore in the runToCompletion() function
**Challenges encountered**: 
appropriately handling interrupted exceptions
**How I solved it**: 
Used nested try-catch blocks
**Testing approach**: 
Execution was confirmed to be accurate
**Time spent**: 
1.5 hours
---

### Entry 5 - [may 1,2026, 11:00pm]
**What I implemented**: 
Final testing and debugging
**Challenges encountered**: 
ensuring that there are no mistakes or deadlocks
**How I solved it**: 
thorough examination and several test runs
**Testing approach**: 
run the program more than five times
**Time spent**: 
1 hour
---

## Part 2: Technical Questions (1 mark)

### Question 1: Race Conditions
**Q**: Identify and explain TWO race conditions in the original code. For each:
- What shared resource is affected?
- Why is concurrent access a problem?
- What incorrect behavior could occur? 

**Your Answer**:
The contextSwitchCount variable experiences the first race condition when multiple threads increase it at the same time, resulting in inaccurate results. When several threads update totalWaitingTime without synchronizing, the second race scenario takes place. Because actions like increment are not atomic, concurrent access results in inconsistent data. This could lead to inconsistent results and inaccurate statistics
[Your answer here - 4-6 sentences with code examples]

---

### Question 2: Locks vs Semaphores
**Q**: Explain the difference between ReentrantLock and Semaphore. Where did you use each in your code and why?

**Your Answer**:
When accessing shared variables, ReentrantLock is utilized to guarantee mutual exclusion and safeguard important portions. The number of threads that can access a resource at once is managed by a semaphore. ReentrantLock was used in my code to safeguard counters and logs, and Semaphore was used to manage CPU access such that only a certain number of processes could operate concurrently 
[Your answer here - explain your implementation choices]

---

### Question 3: Deadlock Prevention
**Q**: What is deadlock? Explain TWO prevention techniques and what you did to prevent deadlocks in your code.

**Your Answer**:
When threads wait endlessly for resources owned by one another, deadlock happens. Using try-finally blocks to guarantee that locks are always released is one preventive strategy. Keeping a constant lock order or avoiding nested locks are two other strategies. I used try-finally in my code to ensure that locks and semaphores were released, avoiding deadlock
[Your answer here - reference try-finally blocks, lock ordering, etc.]

---

### Question 4: Lock Granularity Design Decision 
**Q**: For Task 1 (protecting the three counters), explain your lock design choice:
- Did you use ONE lock for all three counters (coarse-grained) OR separate locks for each counter (fine-grained)?
- Explain WHY you made this choice
- What are the trade-offs between the two approaches?
- Given that the three counters are independent, which approach provides better concurrency and why?

**Your Answer**:
I secured every counter with a single coarse-grained lock. This prevents complexity and streamlines the implementation. However, because threads can access multiple resources at once, fine-grained locking improves concurrency. Fine-grained locking would perform better because counters are independent, but coarse-grained locking is more straightforward and enough for this task
[Your answer here - explain coarse-grained vs fine-grained locking, independence of counters, concurrency implications. Show understanding of when to use each approach. 5-8 sentences expected.]

---

## Part 3: Synchronization Analysis (1 mark)

### Critical Section #1: Counter Variables

**Which variables**: contextSwitchCount, completedProcessCount, totalWaitingTime

**Why they need protection**: Because multiple threads modify them concurrently

**Synchronization mechanism used**: ReentrantLock

**Code snippet**:
```java
// Paste your implementation here
```
counterLock.lock();
try {
    contextSwitchCount++;
} finally {
    counterLock.unlock();
}
**Justification**: 
Ensures mutual exclusion and prevents inconsistent values
---

### Critical Section #2: Execution Log

**What resource**: executionLog

**Why it needs protection**: Multiple threads write to it

**Synchronization mechanism used**: ReentrantLock

**Code snippet**:
```java
// Paste your implementation here
```logLock.lock();
try {
    executionLog.add(message);
} finally {
    logLock.unlock();
}

**Justification**: 
Prevents concurrent modification errors
---

### Critical Section #3: CPU Semaphore

**Purpose of semaphore**: control cpu access

**Number of permits and why**:1 permit to allow one process at a time 

**Where implemented**: 
run() and runToCompletion()
**Code snippet**:
```java
// Paste your implementation here
```SharedResources.cpuSemaphore.acquire();
...
finally {
    SharedResources.cpuSemaphore.release();
}

**Effect on program behavior**: 
Ensures controlled execution and prevents resource conflicts
---

## Part 4: Testing and Verification (2 marks)

### Test 1: Consistency Check
**What I tested**: Running program multiple times to verify consistent results

**Testing procedure**: 
```bash
# Commands used (run the program at least 5 times)
javac SchedulerSimulationSync.java
java SchedulerSimulationSync
java SchedulerSimulationSync
java SchedulerSimulationSync
java SchedulerSimulationSync
java SchedulerSimulationSync```

**Results**: 
(Show that running multiple times produces consistent, correct results)
Total Context Switches: 34
Total Completed Processes: 2o
Total Waiting Time: 1242218ms
Average Waiting Time: 62110ms

ظـــــ
Process    Priority     Burst Time   Waiting Time
ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤ظ¤
P1         2            2910         116         
P2         3            6579         70789       
P3         4            4635         73380       
P4         3            4459         74025       
P5         5            3383         15207       
P6         3            2397         18606       
P7         4            5995         74496       
P8         3            9730         96423       
P9         1            3413         29131       
P10        3            3919         32561       
P11        3            2949         36499       
P12        5            4266         80551       
P13        4            6057         80827       
P14        5            7358         82893       
P15        4            3207         51631       
P16        5            3694         54852       
P17        4            6706         86260       
P18        5            7752         89010       
P19        4            9293         98160       
P20        1            7605         96801       

ظـــــ
Total log entries: 68

**Why synchronization is necessary**: 
(Explain what race conditions COULD occur without synchronization, even if you didn't observe them. Explain which shared resources need protection and why.)
Because several threads access shared resources like contextSwitchCount, completedProcessCount, totalWaitingTime, and executionLog, synchronization is crucial. When two or more threads attempt to change these variables at the same time without synchronization, race situations may arise. For instance, when two threads simultaneously increase contextSwitchCount, their updates may be overwritten, resulting in inaccurate counts. In a similar vein, concurrent writing to executionLog may produce inconsistent or malformed logs. Data integrity is thus preserved by employing locks, which guarantee that only one thread may alter these shared resources at a time.
**Conclusion**: 
Synchronization techniques like ReentrantLock and Semaphore guarantee proper and consistent program behavior during several executions
---

### Test 2: Exception Testing
**What I tested**: Checking for ConcurrentModificationException

**Testing procedure**: 
observed how threads accessed shared resources like executionLog after running the program several times under typical circumstances. To mimic real-world concurrent behavior, I made sure that several threads were actively uploading logs at the same time
**Results**: 

**What this proves**: 
This demonstrates that concurrent modification problems can be avoided by applying synchronization to shared resources, particularly by using locks around executionLog. It guards against runtime crashes brought on by unsafe concurrent access and guarantees thread-safe operations
---

### Test 3: Correctness Verification
**What I tested**: Verifying correct final values (total burst time, context switches, etc.)

**Expected values**: 
The total number of processes produced should equal the number of completed processes.
 The number of times the CPU switched between processes should be reflected in the context switch count.
The overall waiting time need to be favorable and in line with how the process is carried out
**Actual values**: 
Total Context Switches: 34
Total Completed Processes: 20
Total Waiting Time: 1242218ms
Average Waiting Time: 62110ms
**Analysis**: 
This demonstrates that synchronization has no detrimental effects on the program's logic. Rather, it made guaranteed that, despite concurrent execution, shared data remained correct and dependable
---

### Test 4: Different Scenarios
**Scenario tested**: [e.g., different time quantum, more processes, etc.]

**Purpose**: 
The goal was to see how scheduling behavior varies under various circumstances and to make sure that synchronization remains accurate despite changes in input
**Results**: 
In every situation, the program acted appropriately. As anticipated, altering the time quantum had an impact on the scheduling order, and adding more processes resulted in more context changes. Nevertheless, there were no mistakes or discrepancies, and synchronization stayed steady
**What I learned**: 
I discovered that synchronization techniques need to be resilient enough to manage various execution circumstances. No matter the magnitude of the input or the scheduling situation, proper synchronization guarantees correct behavior
---

## Part 5: Reflection and Learning

### What I learned about synchronization:

[6-8 sentences about key concepts, challenges, insights]
I discovered that when several threads access common resources, synchronization is crucial. Race circumstances may arise in the absence of adequate synchronization, resulting in inaccurate outcomes and erratic behavior. ReentrantLock ensures mutual exclusion by providing exact control over crucial parts. Additionally, I discovered that semaphores can be used to manage access to restricted resources, such CPU execution. Knowing where to put locks without compromising performance was one of the main challenges. I came to understand that while underusing locks can result in errors, overusing them can decrease concurrency. Using try-finally blocks to ensure that locks are always released was another crucial idea. All things considered, this assignment improved my understanding of how to design dependable and safe multi-threaded programs
---

### Real-world applications:
**Example 1**: 
banking systems that allow numerous individuals to view and modify account balances. Transactions are handled accurately and without data distortion thanks to synchronization.

**Example 2**: 
operating systems in which a number of processes share memory and CPU resources. Synchronization guarantees the equitable and secure distribution of resources.
---

### How I would explain synchronization to others:

[Explain to someone who just finished Assignment 1 - use simple terms and analogies]
Synchronization is comparable to a service desk line. Chaos happens when a large number of users attempt to use the service simultaneously. To guarantee that only one person is serviced at a time or that a certain number of individuals can use the service, we employ regulations. In programming, shared resources are like the service desk, while threads are like humans. Semaphores permit a finite number of threads at once, whereas locks function as a ticket system that only permits one thread at a time. This keeps things peaceful and guarantees that everything goes without a hitch
---

## Part 6: GitHub Repository Information

**Repository URL**: 

**Number of commits**: 

**Commit messages**: 
1. 
2. 
3. 
4. 

---

## Summary

**Total time spent on assignment**: 

**Key takeaways**: 
1. 
2. 
3. 

**Most challenging aspect**: 

**What I'm most proud of**: 

---

**End of Documentation**
