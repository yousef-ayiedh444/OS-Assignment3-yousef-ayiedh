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

**Which variables**: 

**Why they need protection**: 

**Synchronization mechanism used**: 

**Code snippet**:
```java
// Paste your implementation here
```

**Justification**: 

---

### Critical Section #2: Execution Log

**What resource**: 

**Why it needs protection**: 

**Synchronization mechanism used**: 

**Code snippet**:
```java
// Paste your implementation here
```

**Justification**: 

---

### Critical Section #3: CPU Semaphore

**Purpose of semaphore**: 

**Number of permits and why**: 

**Where implemented**: 

**Code snippet**:
```java
// Paste your implementation here
```

**Effect on program behavior**: 

---

## Part 4: Testing and Verification (2 marks)

### Test 1: Consistency Check
**What I tested**: Running program multiple times to verify consistent results

**Testing procedure**: 
```bash
# Commands used (run the program at least 5 times)
```

**Results**: 
(Show that running multiple times produces consistent, correct results)

**Why synchronization is necessary**: 
(Explain what race conditions COULD occur without synchronization, even if you didn't observe them. Explain which shared resources need protection and why.)

**Conclusion**: 

---

### Test 2: Exception Testing
**What I tested**: Checking for ConcurrentModificationException

**Testing procedure**: 

**Results**: 

**What this proves**: 

---

### Test 3: Correctness Verification
**What I tested**: Verifying correct final values (total burst time, context switches, etc.)

**Expected values**: 

**Actual values**: 

**Analysis**: 

---

### Test 4: Different Scenarios
**Scenario tested**: [e.g., different time quantum, more processes, etc.]

**Purpose**: 

**Results**: 

**What I learned**: 

---

## Part 5: Reflection and Learning

### What I learned about synchronization:

[6-8 sentences about key concepts, challenges, insights]

---

### Real-world applications:

Give TWO examples where synchronization is critical:

**Example 1**: 

**Example 2**: 

---

### How I would explain synchronization to others:

[Explain to someone who just finished Assignment 1 - use simple terms and analogies]

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
