# Virtual-Smart-Campus-Management-System
## Overview
A Java-based console application to manage a virtual smart campus, including Students, Instructors, Courses, and Grade ,InputHelper,Lap,Room,Scheduler,SchedulerEnter,Notifiable
### Classes
1. `Person (abstract)`
2. `Student`
3. `Instructor`
4.  `Staff`
5. `CampusResource (abstract)`
6. `Course`
7. `Grade`
8. `CampusSystem`
9. `Lap`
10. `Room`
11. `Scheduler`
12. `SchedulerEnter`
13. `Notifiable`
#### 1. Class Person
**`Description:`**
 Represents a generic person in the system (parent class for Instructor, Student, and Staff).
Handles basic personal information and input validation.

*`Attributes:`*  
| Attribute    | Type         | Description |
|:------------|:-------------|:------------------|
| id         | int        | Unique academic ID (positive integer) |
| name       | String     | Full name (must not contain numbers or symbols) |
| email      | String     | Auto-generated university email based on name and ID |
| NumperPhone| int        | Phone number (validated to be digits only) |
| Address    | String     | The user's registration time history is checked. |
| restartId  | String     | Reset user password |
| restartEmail   |  String     | Reset user email |

---
*Methods with Usage Examples:*
- **`setpassord`**
- *Purpose:* Validates password to be 6 characters.
- Returns true if valid, else false.

- **`logain()`**

- Simulates login by asking for ID and email and verifying with restart data.


- **`changePassword()`**

- Validates current password.

- Accepts new password (must be 6 characters).

- Allows retry or cancel if invalid.


- **`sendNotification(String message)`**

- Sends a notification message to the person.

Example Output:
```
Notification to Ali (ali@mail.com): Your schedule updated!
```

- **`viewProfile()`**

- Abstract method: must be implemented by any subclass.

---

Special Notes:

Uses Scanner for console input.

Implements Notifiable interface for notifications.

Includes restartId and restartEmail for recovery validation.

Strong validation on password changes (must be exactly 6 characters).

---
##### 2. Class Student

**`Description:`**
The Student class extends the abstract Person class and represents a student in the system.
It manages course enrollment, GPA, and student-specific data like academic level.

---
*`Attributes:`*

| Attribute        | Type                    | Description                                         |
|------------------|-------------------------|-----------------------------------------------------|
| enrolledCourses         | ArrayList<Course>       | List of courses the student is enrolled in |            
| GPA            | double                | Student's current GPA                      |
| livels  | String       | Student’s academic level (e.g., "First Year")  |
| max_courses     | static final int  |Constant for max allowed registered courses per student (7)         |
---
*Methods with Usage Examples:* 
---

- **`Constructors`**:
```
- public Student(double GPA, String livel)
```
- Initializes GPA and level only.
```

public Student(double GPA, String livel, String id, String name, String email, String NumberPhone, String address, String password)
```
Initializes personal data + GPA + level via superclass.



---

*Methods with Usage Examples:* 

- registercourse(Course course)

- Registers the student in a course.

- **`Checks:`**

I- f course exists.

- If already registered.

- If max limit reached.


- Adds student to course’s list as well.


- *Example output:*
```
The course (Java Programming) has been registered successfully
```
-**`viewProfile()`**

- Displays full student profile.


- *Example output:*

-m**`Student profil`**
```
Id: 1001
Name: Ali Hassan
Email: ali@mail.com
NumberPhone: 01012345678
Address: Cairo
Level: Second Year
GPA: 3.5
```
- **`getGPA() / setGPA(double GPA)`**

- Get or update the student's GPA.


- **`getLivel() / setLivel(String livel)`**

- Get or update the student’s academic level.


---

Special Notes:

Uses an ArrayList<Course> for enrolled courses to prevent external modifications.

max_courses constant controls how many courses a student can enroll in.

Strong validation in registercourse() ensures no duplicate or excess registrations.
---
###### 3. Class Instructor
*`Description:`*  
The Instructor class extends the abstract Person class and represents an instructor in the virtual campus system.
Manages courses taught by the instructor, student enrollments, grade configurations, and profile viewing.
---

*`Attributes:`*  

| Attribute         | Type                  | Description |
|:------------------|:---------------------|:----------------------------------------------------|
| teachingCourses       | ArrayList<Course>              | List of courses assigned to this instructor |
| department    | String              | OInstructor’s department |
| officeHours           | String              | Office hours informati |



---

- **`Constructor`**:
```
public Instructor(String id, String name, String email, String NumberPhone, String address, String password, String department, String officeHours)

Initializes personal info + department + office hours + teaching courses list.

```

---

*Methods with Usage Examples:* 

- **`addCourse(Course course)`**

- Assigns a course to the instructor if not already assigned.

-  *`Example output:`*
  ```
Course Java Programming added to Ali's teaching courses.
```

- **`viewTeachingCourses()`**

- Displays list of instructor’s teaching courses.


-**`setNumberOfQuizzes(Grade grade)`**

- Sets number of quizzes for a course if the instructor teaches it.


-  **`setNumberOfAssignments(Grade grade)`**

- Sets number of assignments for a course if the instructor teaches it.


- **`enrollStudentInCourse(Student student, Course course)`**

- Enrolls a student into a course taught by this instructor.

-  *`Example output:`*
```
Student Omar enrolled in Data Structures.
```

-**`getCoursesCount()`**

- Returns number of courses assigned to this instructor.


-**`viewProfile()`**

- Displays full instructor profile and courses list.

-  *`Example output:`*
```

Instructor Profile:
ID==> 101
Name==> Dr. Ahmed
Email==> ahmed@mail.com
Department==> Computer Science
Office Hours==> Sun & Tue 10-12
Teaching Courses==>
  1. Java Programming
  2. OOP Concepts
```


---

Special Notes:

Uses ArrayList<Course> for dynamic course management.

Provides proper validation for assigning and enrolling.

Implements method overriding for viewProfile() from the Person abstract class.

Relies on the teachesCourse(Course course) private helper method to validate course assignments.



---
####### 4. Class Staff
*Description:*  
---

*`Attributes:`*


| Attribute             | Type                  | Description                                           |
|-----------------------|-----------------------|-------------------------------------------------------|
|salary	|double|	Monthly salary for the staff member|
|position|	String	|Job title or position (e.g., "Admin Clerk")\



---

Constructor:
```
public Staff(double salary, String position, String id, String name, String email, String NumberPhone, String address, String password)

Initializes a staff member’s profile including inherited attributes like ID, name, email, etc.
```


---

*Methods with Usage Examples:* 

- **`viewProfile()`**
- (Overridden from Person — currently empty, to be implemented to display staff info.)



---

-*`Example Usage:`*
```
Staff staff = new Staff(5000.0, "Admin Clerk", "ST001", "Ahmed Saleh", "ahmed@vscms.edu", "01123456789", "Main Campus", "123456");
staff.viewProfile();
```

---

Special Notes:

Inherits all attributes and methods from Person.

Password validation logic (length = 6) handled by Person superclass.

You can implement the viewProfile() method to display staff details like:

```
@Override
public void viewProfile() {
    System.out.println("Staff Profile:");
    System.out.println("ID: " + getId());
    System.out.println("Name: " + getName());
    System.out.println("Position: " + position);
    System.out.println("Salary: " + salary);
    System.out.println("Email: " + getEmail());
    System.out.println("Phone: " + getNumberPhone());
    System.out.println("Address: " + getAddress());
}
```

#### 5. Class Course

*`Description:`* 
The Course class represents an academic course in the virtual campus system.
It holds information about the course code, name, assigned instructor, enrolled students, and manages student registration with a maximum capacity limit.


---

Attributes:
*`Attributes:`* 

| Attribute             | Type                  | Description                                           |
|-----------------------|-----------------------|-------------------------------------------------------|
|CourseCode|	String|	Unique identifier for the course|
|CourseName|	String	Name of the course|
|instructor|	Instructor|	Instructor assigned to the course|
|maxCapacity	|int |(constant = 7)	Maximum number of students that can enroll|
|sstudent|	ArrayList<Student>	|List of students enrolled in this course|



---

Constructor:
```
public Course(String CourseCode, String CourseName)

Initializes course details and the student list.
```


---

*Methods with Usage Examples:*

-**`addstudent(Student sstudent)`**

- Adds a student to the sstudent list without capacity check.


-**`addStudent(Student student)`88

- Same as addstudent() — adds to list.


**`enrollStudent(Student student)`**

- Enrolls a student into the course with capacity and duplication check.

**`Example Output:`**
```
Student Ali enrolled successfully in Java Programming

```
**`removeStudent(Student student)`**

- Removes a student from the course.

-**`Example Output:`**
```
Student Ali removed from Java Programming

```
-**`isFull()`**

- Checks if the course reached maxCapacity.
- Returns: true if course is full, false otherwise.


- Getters & Setters for:

- CourseCode, CourseName

- Instructor

- List of students (getStudent(), setStudent())




---

Special Notes:

maxCapacity constant ensures a course can only accept up to 7 students.

Two ArrayLists were originally declared (sstudent and enrolledStudents), but only sstudent is being actively used — it’s better to clean that up.

Uses defensive checks inside enrollStudent() to avoid over-enrollment and duplication.



---
#### 6.Class Grade
*`Description:`* 
The Grade class represents the grade record for a particular student in a specific course.
It stores and manages grades for quizzes, assignments, midterm, and final exams, with validation and total grade calculation logic.


---

*`Attributes:`* 

| Attribute             | Type                  | Description                                           |
|-----------------------|-----------------------|-------------------------------------------------------|
|student|	Student|	The student this grade belongs to|
|instructor|	Instructor|	(Optional - not used in current logic, but declared)|
|course|	Course	|The course this grade is associated with|
|quizzes|	ArrayList<Double>|	List of quiz grades
|assignments	|ArrayList<Double>|	List of assignment grades|
|midterm|	double|	Midterm exam grade (0–20)|
|finalExam	|double	|Final exam grade (0–50)|
|maxQuizzes|	int	|Maximum allowed quizzes for the course|
|maxAssignments|	int	|Maximum allowed assignments for the course|



---

-**`Constructor:`**

- public Grade(Student student, Course course)

- Initializes grade record for a student and a course with default values.



---

*Methods with Usage Examples:*

**`setMaxQuizzes(int maxQuizzes)`**

-Sets maximum number of quizzes allowed, trims extra quizzes if necessary.


**`setMaxAssignments(int maxAssignments)~88

- Sets maximum number of assignments allowed, trims extra if needed.


-**`addQuizGrade(double grade)` **

- Adds a new quiz grade after validation.

-**`Example:`**
```
addQuizGrade(18.5)
```

-**`addAssignmentGrade(double grade)`**

-Adds a new assignment grade after validation.


**`setMidtermGrade(double grade)`**

- Sets the midterm grade after checking it’s between 0–20.


-**`setFinalGrade(double grade)`**

- Sets final exam grade (0–50).


**`getTotalGrade()`**

- Calculates total grade by summing quizzes, assignments, midterm, and final.


-**`viewGrades()`**

- Displays full grade breakdown for a student in a course.


**`viewAssignmentGrades()`**

- Displays assignment grades only.




---

-**`Example Grade Record Usage:`**
```
Grade grade = new Grade(student, course);
grade.setMaxQuizzes(3);
grade.addQuizGrade(18);
grade.addAssignmentGrade(19);
grade.setMidtermGrade(16);
grade.setFinalGrade(45);
grade.viewGrades();
```
- **`Sample Output:`**
```
Grades for Ali in Programming 101:
Quiz grades:
Quiz 1: 18.0
Assignment grades:
Assignment 1: 19.0
Midterm: 16.0
Final Exam: 45.0
Total Grade: 98.0
```

---

Special Notes:

The class strictly enforces grade limits:

Quizzes & Assignments: 0–20

Midterm: 0–20

Final: 0–50


Provides automatic trimming of extra grades if max allowed is reduced.



---
#### 7. Class CampusSystem
*`Description:`* 
An abstract base class representing a generic resource within the campus system (e.g. labs, rooms, equipment).
It defines common attributes and behaviors for all campus resources, and forces subclasses to implement reserve() and getAvailability() methods.

---
*`Attributes:`* 
| Attribute Name   | Data Type                  | Description                                                              |
|------------------|----------------------------|--------------------------------------------------------------------------|
|resourceId|	String	|Unique identifier for the resource|
|location|	String|	Physical or virtual location of the resource|
|capacity|	int	|Maximum capacity (e.g. number of people/items supported)|
|type|	String|	Type/category of the resource (e.g. lab, room)|
|status|	String|	Current status (e.g. Available, Reserved)|
|descriptio|n	String	|Text description providing additional details|



---

-**`Constructors:`**

- public CampusResource()

- Default constructor.

```
public CampusResource(String resourceId, String location, int capacity, String type, String status, String description)
```
-Parameterized constructor to initialize all attributes.



---

*Methods with Usage Examples:* 



| Attribute Name   | Return Type                  | Description                     |
|------------------|----------------------------|---------------------------------|
|getResourceId()	 |      String               	|  Returns resource ID|
|setResourceId(String id)|	void|	Sets a new resource ID|
|getLocation()|	String	|Returns location|
|setLocation(String location)	|void|	Sets a new location|
|getCapacity()|	int	|Returns resource capacity|
|setCapacity(int capacity)|	void|	Sets resource capacity|
|getType()	|String|	Returns resource type|
|setType(String type)|	void	|Sets resource type|
|getStatus()	|String	|Returns current status|
|setStatus(String status)	|void|	Updates status|
|getDescription()|	String	|Returns resource description|
|setDescription(String description)|	void|	Updates description|
|reserve() (abstract)	|boolean|	Abstract method to reserve resource (implemented in subclasses)|
|getAvailability() (abstract)|	boolean|	Abstract method to check availability|
|displayInfo()|	void	|Displays full resource information to console|
|updateStatus(String newStatus)	|void	|Updates the resource's status|
|updateDescription(String newDescription)	|void	|Updates the resource's description|
|updateType(String newType)	|void|	Updates the resource's type|



---

-**`Example:`**
```
CampusResource lab = new Lab("LAB001", "Building A", 25, "Computer Lab");
lab.displayInfo();
```
Special Notes:

The reserve() and getAvailability() methods are abstract and must be implemented by subclasses.

displayInfo() method provides a neat, formatted console output for resource details.


---
### 7.Class Room
**`Description:`**
The Room class is a subclass of CampusResource that represents a reservable room resource in the campus system. It adds reservation logic specific to rooms.
---

Attributes:

| Attribute Name   | Data Type                  | Description                                                  |
|------------------|----------------------------|--------------------------------------------------------------|
|isReserved	|boolean	|Tracks whether the room is currently reserved (false by default)|




---

Constructor:
```
public Room(String resourceId, String location, int capacity, String type, String status, String description)

Initializes a room resource with specific details (inherited from CampusResource).
```


---

Methods:

Method	Return Type	Description

fillDetailsFromUser()	void	Interactive console-based method to set all room attributes
reserve()	boolean	Reserves the room if available, returns true if successful
getAvailability()	boolean	Returns true if the room is not reserved
cancelReservation()	void	Cancels the room reservation



---

Example Usage:
```
Room room = new Room("RM101", "Main Building", 30, "Lecture Room", "Available", "Air-conditioned lecture room");
room.fillDetailsFromUser();
if (room.reserve()) {
    System.out.println("Room reserved successfully!");
}
```

---

Special Notes:

The fillDetailsFromUser() method includes input validation using regex for each field:

IDs allow letters, numbers, and spaces.

Locations, Types, Status, and Descriptions allow letters and spaces only.

Capacity must be a non-negative integer.


reserve() prevents double-booking the same room.

getAvailability() reports real-time room availability.

cancelReservation() safely unbooks a room.



---
### Lap

Description:
The Lap class is a subclass of CampusResource representing a lab facility in the campus management system, with attributes for computer availability and reservation status. It includes interactive data entry and reservation control.


---

Attributes:

| Attribute Name   | Data Type                  | Description                                                  |
|------------------|----------------------------|--------------------------------------------------------------|
|hasComputers|	boolean	|Indicates if the lab contains computers|
|isReserved|	boolean	|Tracks the current reservation status|
|labName|	String	|Name of the lab|



---

Constructors:

public Lap()

Default constructor.

```
public Lap(boolean hasComputers, boolean isReserved, String resourceId, String location, int capacity, String type, String status, String description)

Parameterized constructor to fully initialize a lab.
```


---

Methods:

| Attribute Name   | Return Type                  | Description                     |
|------------------|----------------------------|---------------------------------|
|fillDetailsFromUser()|	void|	Interactive console method to enter all lab details with validation|
|reserve()|	boolean|	Reserves the lab if available, returns true if successful|
|getAvailability()	|boolean|	Reports if the lab is currently available for reservation|
|hasComputers()|	boolean	|Returns whether the lab has computers|



---

Example Usage:
```
Lap lab = new Lap();
lab.fillDetailsFromUser();
if (lab.reserve()) {
    System.out.println("Lab booked successfully!");
}
```

---

Special Notes:

Input Validation: fillDetailsFromUser() enforces strict data validation using regex for text fields and numerical checks for capacity.

Reservation Handling:

reserve() ensures no double-booking.

getAvailability() indicates current status.


Separate hasComputers() method to check for computer availability in the lab.



---
### Scheduler

Description:
The Scheduler class is a singleton-based scheduling manager for campus resources. It manages bookings by assigning CampusResource objects to time slots while preventing double-booking.


---

Attributes:

| Attribute Name   | Data Type                  | Description                                                  |
|------------------|----------------------------|--------------------------------------------------------------|
|instance	|Scheduler (static)	|Singleton instance of the Scheduler|
|scheduleList|	ArrayList<SchedulerEnter>	|List of scheduled resources and their time slots|



---

- Constructor:

- **`public Scheduler()`**

-Initializes an empty scheduleList.



---

Methods:

| Attribute Name   | Return Type                  | Description                     |
|------------------|----------------------------|---------------------------------|
|getInstance()|	Scheduler	|Returns the single Scheduler instance (singleton pattern)|
|scheduleResource(CampusResource resource, String timeSlot)	|boolean|	Reserves a resource if available, and adds it to the schedule|
|cancelSchedule(CampusResource resource)	|void	|Cancels a scheduled resource by its ID|
|displaySchedule()|	void|	Displays all current scheduled resources and their time slots|
|getAllScheduledResources()|	void|	Lists all resource IDs currently scheduled|



---

Example Usage:
```
Scheduler scheduler = Scheduler.getInstance();
Room room1 = new Room("R101", "Building A", 30, "Lecture", "Available", "Standard Lecture Room");

scheduler.scheduleResource(room1, "10:00 AM - 12:00 PM");
scheduler.displaySchedule();
scheduler.getAllScheduledResources();
scheduler.cancelSchedule(room1);
```
Sample Output:
```
Scheduled R101 at 10:00 AM - 12:00 PM
 Current Resource Schedule 
 Resource ID R101  Time Slot 10:00 AM - 12:00 PM
 List of all scheduled resources 
- R101
 Cancelled schedule for R101
```

---

Special Notes:

Singleton Pattern: Only one instance of Scheduler exists in the system.

Conflict Prevention: Prevents scheduling a resource at overlapping time slots.

Relies on SchedulerEnter class to link resourceId and timeSlot.

Uses CampusResource.reserve() and getAvailability() methods to manage resource availability.



---
### Scheduler

Description:
The Scheduler class is a singleton-based scheduling manager for campus resources. It manages bookings by assigning CampusResource objects to time slots while preventing double-booking.


---

Attributes:

| Attribute Name   | Data Type                  | Description                                                  |
|------------------|----------------------------|--------------------------------------------------------------|
|instance|	Scheduler (static)|	Singleton instance of the Scheduler|
|scheduleList	|ArrayList<SchedulerEnter>	|List of scheduled resources and their time slots|



---

- Constructor:

-**`public Scheduler()`**

-Initializes an empty scheduleList.



---

Methods:

Method	Return Type	Description
| Attribute Name   | Return Type                  | Description                     |
|------------------|----------------------------|---------------------------------|
|getInstance()	|Scheduler|	Returns the single Scheduler instance (singleton pattern)|
|scheduleResource(CampusResource resource, String timeSlot)|	boolean	|Reserves a resource if available, and adds it to the schedule|
|cancelSchedule(CampusResource resource)	|void	|Cancels a scheduled resource by its ID|
|displaySchedule()|	void	|Displays all current scheduled resources and their time slots|
|getAllScheduledResources()|	void|	Lists all resource IDs currently scheduled|



---

-**`Example Usage:`**
```
Scheduler scheduler = Scheduler.getInstance();
Room room1 = new Room("R101", "Building A", 30, "Lecture", "Available", "Standard Lecture Room");

scheduler.scheduleResource(room1, "10:00 AM - 12:00 PM");
scheduler.displaySchedule();
scheduler.getAllScheduledResources();
scheduler.cancelSchedule(room1);
```
-**`Sample Output:`**
```
Scheduled R101 at 10:00 AM - 12:00 PM
 Current Resource Schedule 
 Resource ID R101  Time Slot 10:00 AM - 12:00 PM
 List of all scheduled resources 
- R101
 Cancelled schedule for R101
```

---

Special Notes:

Singleton Pattern: Only one instance of Scheduler exists in the system.

Conflict Prevention: Prevents scheduling a resource at overlapping time slots.

Relies on SchedulerEnter class to link resourceId and timeSlot.

Uses CampusResource.reserve() and getAvailability() methods to manage resource availability.



---
### Notifiable

Description:
The Notifiable interface defines a simple contract for any class that should be capable of sending notifications.
Any class that implements this interface must provide an implementation for the sendNotification method.


---

Method	Return Type	Description
| Attribute Name   | Return Type                  | Description                     |
|------------------|----------------------------|---------------------------------|
|sendNotification(String message)|	void	|Sends a notification message to the recipient|

---

Usage Example:
```
Any class (like Person, Student, Instructor, etc.) can implement this interface and define its own logic for sending a notification.
```
-Example Implementation in a Class:

public class Student implements Notifiable {
    private String name;
```
    public Student(String name) {
        this.name = name;
    }

    @Override
    public void sendNotification(String message) {
        System.out.println("Notification to " + name + ": " + message);
    }
}
```
Example Output:
```
Notification to Ahmed: Your GPA has been updated!

```
---

Special Notes:

Promotes loose coupling and flexibility by ensuring that any implementing class provides a custom way to notify.

Useful for sending alerts, confirmations, or system messages to various campus members (students, staff, instructors, etc.).



---
