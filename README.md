# Room-and-Time-Scheduler-using-CSP
In this project, we worked on a solving the room and time scheduling in Zewail City by using Constraint satisfaction problems (CSPs) algorithms

This project was developed for Artificial Intelligence class Spring 2020.

## Motivation
- One of the problems which require a lot of efforts in order to solve is coming up with a suitable schedule for a university, given a certain number of available rooms, a certain number of courses, and professor’s schedules.
- It would require a lot of efforts, trials and errors, by the admissions office of university in order to form this schedule and satisfy all of the given constraints.
- In an effort to make this problem easier, we introduce a constraint satisfaction problem (CSP), which we have formulated in order to form this schedule and satisfy the needed constraints so we can help the admission team form the complete schedule in no time.

- In the following sections, we are going to discuss our design, how we have achieved a solution, and also an analysis of the complexity of this problem.

## Introduction to the problem
- This project is the final project for the AI class I took in Srping 2020.
- One class of problems which I've studied is Constraint Satisfaction Problems (CSPs), which has a goal for identifying the solution of a given problem in a way that is similar to the Depth First Search (DFS) approach, but has some differences. Instead of traversing a search tree which includes all of the possible states that could be found in the state space, it only explores nodes which do not violate any of the constraints which are property of the goal state. Thus, it cuts a great number of nodes which would be unnecessary to explore.
- The scheduling problem is a perfect example of an assignment problem that is solved given a set of constraints to avoid conflicts in schedules for students in the same batch / major.
- That is why we saw potential in applying CSP evaluation and backtracking techniques to reduce the amount of effort required to formulate a university schedule manually.

## Problem Description
- While designing the problem, we tried to estimate the variables and domains in order to be as close as possible to our actual situation at university.
- However, there were a few assumptions that we needed to make which are :
  - Any room available is suitable to be used for the purpose of delivering a lecture or a lab
  - A student from a certain academic year / major does not take courses from another year / major, meaning that conflicts only are a problem for each specific batch in a major
  - Any room is available for teaching during all of the week days, all of the working hours
- The table below shows the specific parameters which define our main case problem.

|                                  |                                                                |
|----------------------------------|----------------------------------------------------------------|
| No of academic years             | 5                                                              |
| No of majors                     | 9                                                              |
| Courses / major / academic year  | 6 (maximum)                                                    |
| 1 course                         | 1 Lecture + 1 Lab                                              |
| Durations                        | - Lecture : 2 hours - Lab : 3 hours                            |
| No of teaching rooms available   | 30 (rough estimation of the number of rooms at our university) |
| No of days / week                | 5                                                              |
| No of hours / day                | 8                                                              |

- From the specified parameters we can deduce that the available number of hours available for teaching at the university is equal to
$slots = Rooms * Days * Hours = 1,200 slots$
- The required slots which are needed in the goal state
$Majors * Years * Courses * Hours = 1,140 slots$
- This simple calculation indicates that the maximum number of courses offered by the university cannot exceed that we have specified above, or else we would need to add extra rooms to offer more slot times, that is in fact asserted in our code to overcome getting stuck in the backtracking step.

## Algorithm
 - A slot is defined by a four digit number, the first two digits of the number identify the room number of this slot, third digit indicates the week day, and fourth indicates the hour, an example is shown below

 |                                  |                                                                |
 |----------------------------------|----------------------------------------------------------------|
 | Slot name : 1231                 | - Room number: 12 - Day: Tuesday - Hour: 8.30-9.30 (first hour)|


 - This simple definition of the available slots, have combined both of resources into one, now this means one last thing, a lecture would require to be assigned two slots for two hours, which are constrained to be in the same room, and of course consecutive hours in the same day.
- The goal state is a full assignment for all of the courses with the required number of slots depending on whether it is a lecture or a lab
- In the beginning the domain of all of the courses is the available list of slots defined.

## Constraints

- A slot can be used once and only once, no two lectures can share a room during the same day and hour
- A lecture has a duration of two hours, so it has to be assigned to two teaching hours in the same day and in the same room
- A lab has a duration of three hours, so it has to be assigned to three teaching hours in the same day and in the same room
- To avoid conflicts in the schedules of students, lectures and labs of all the students in the same academic year and same major cannot be concurrent

All of the constrains are defined in a function called **consistency**, that acts as our evaluation function, and it checks if a new assignment of a variable to a certain value would be suitable to the variables that are already assigned or not, if all values in the given domain are not suitable, then a backtracking step is necessary because we will never reach a solution while traversing this path.

## Sample Output
We created our own visualizers to be able to print the output in a readable format rather than the 4 digit representation, which consists of the year, the major, the course number, either being a lab or a lecture, its assigned room, the day, and the duration.
![output](https://i.ibb.co/N2jVsKq/a.png)

## Performance analysis
- While CSPs are usually not easy to analyze mathematically due to their nature, we were able to estimate the time complexity of our solution by changing the number of courses per major and calculating the time needed to solve the problem.
- This was done for 12 times only, as more than that will not be applicable with the university current number of rooms.
- As expected, our solution is tending to be an exponentially increasing, therefore, we can estimate the time complexity as $Օ(2**n )$ , where ​ n is the number of courses per major.
- This is a rough estimation that can be not entirely true if we were able to solve the problem on a larger number of variables.


![analysis](https://i.ibb.co/HC6G0m2/b.png)



# All the code is in the notebook and you can find more details in the report.
