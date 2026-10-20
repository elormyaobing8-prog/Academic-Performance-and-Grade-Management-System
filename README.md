# Academic Performance & Grade Management System

A web page for recording student marks, working out grades and seeing how a class is doing. Built with HTML, CSS and JavaScript only. No installation is needed.

## How to run

Open `index.html` in a browser.

## What it does

- Enter a student with an ID, a name and three marks: assignment (/20), mid-semester (/30) and exam (/50). New entries enter a FIFO processing queue first.
- The total and grade are worked out automatically (A 80+, B 70-79, C 60-69, D 50-59, F below 50).
- Process queued student records one at a time in first-in, first-out (FIFO) order; processed records appear in the student table.
- Edit or delete any processed student.
- Search by ID or name, and sort by name, ID or total.
- Summary cards show the number of students, the class average, and the highest and lowest marks.
- A grade distribution chart shows how many students got each grade.
- Student records and pending queue items are saved in the browser, so they remain after a refresh.
- "Load sample students" fills the list with fictional demo data. "Clear all" empties it.

## Where the arrays are used (all in `script.js`)

| Task | How it is done |
|---|---|
| Store all students | `students` array, one object per student |
| Store one student's marks | `marks` array with 3 items: assignment, mid-semester, exam |
| Add a student | `push` adds to the end of the array |
| Find a student by ID | `findStudentIndex`: linear search with a `for` loop |
| Edit a student | find the index, then replace that item |
| Delete a student | `splice` removes the item and closes the gap |
| Search box | `searchStudents`: loop and keep matches in a new array |
| Sort | `sortStudents`: sort a copy so the original order is kept |
| Total of the marks | `calculateTotal`: loop through the marks array |
| Average, highest, lowest | `getStatistics`: one loop through the array |
| Grade distribution | `getGradeCounts`: an array of 5 counters (A, B, C, D, F) |

## Notes

The sample students are fictional. Marks are checked before saving: each must be a number between 0 and its maximum, and a student ID cannot be used twice.

## Where the queue is used

The **student processing queue** holds new student records until an operator processes them. The queue is implemented as a JavaScript array, with `push()` to enqueue at the rear and `shift()` to dequeue from the front. Because the first item added is the first item removed, it follows FIFO (First In, First Out).

| Queue operation | Code / behaviour |
|---|---|
| Enqueue | `studentQueue.push(result.student)` adds a new student to the back. |
| View front item | `studentQueue[0]` checks the next student before processing. |
| Dequeue | `studentQueue.shift()` removes the first waiting student. |
| Queue length | `studentQueue.length` displays the number of pending students. |
| Persistence | `saveQueue()` and `loadQueue()` store and restore pending items using browser `localStorage`. |

### Demonstration

1. Add two different students using the form. They appear in the queue, not the student table.
2. Check the numbered positions in the queue.
3. Click **Process next student** once. The first student moves into the student table.
4. Click it again. The second student is processed.
5. Refresh the page to see that the remaining queue and saved records are retained.

The sample-data button adds fictional demonstration records directly to the student table as a shortcut. The queue is an educational workflow; it does not represent a university-wide or multi-user server queue.
