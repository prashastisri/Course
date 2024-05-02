package program1;

	import java.util.ArrayList;
	import java.util.List;
	import java.util.Scanner;

	// Course class represents a course with its attributes
	class Course {
	    private String code;
	    private String title;
	    private String description;
	    private int capacity;
	    private int enrolled;
	    private String schedule;

	    // Constructor to initialize a course
	    public Course(String code, String title, String description, int capacity, String schedule) {
	        this.code = code;
	        this.title = title;
	        this.description = description;
	        this.capacity = capacity;
	        this.enrolled = 0;
	        this.schedule = schedule;
	    }

	    // Getters and setters
	    public String getCode() {
	        return code;
	    }

	    public String getTitle() {
	        return title;
	    }

	    public String getDescription() {
	        return description;
	    }

	    public int getCapacity() {
	        return capacity;
	    }

	    public int getEnrolled() {
	        return enrolled;
	    }

	    public String getSchedule() {
	        return schedule;
	    }

	    // Method to enroll a student in the course
	    public boolean enrollStudent() {
	        if (enrolled < capacity) {
	            enrolled++;
	            return true;
	        } else {
	            return false;
	        }
	    }

	    // Method to remove a student from the course
	    public void removeStudent() {
	        enrolled--;
	    }

	    // Method to check if the course is full
	    public boolean isFull() {
	        return enrolled >= capacity;
	    }
	}

	// Student class represents a student with their attributes and enrolled courses
	class Student {
	    private int id;
	    private String name;
	    private List<Course> courses;

	    // Constructor to initialize a student
	    public Student(int id, String name) {
	        this.id = id;
	        this.name = name;
	        this.courses = new ArrayList<>();
	    }

	    // Method to enroll in a course
	    public void enrollCourse(Course course) {
	        if (!courses.contains(course)) {
	            courses.add(course);
	            course.enrollStudent();
	            System.out.println(name + " has enrolled in " + course.getTitle());
	        } else {
	            System.out.println(name + " is already enrolled in " + course.getTitle());
	        }
	    }

	    // Method to drop a course
	    public void dropCourse(Course course) {
	        if (courses.contains(course)) {
	            courses.remove(course);
	            course.removeStudent();
	            System.out.println(name + " has dropped " + course.getTitle());
	        } else {
	            System.out.println(name + " is not enrolled in " + course.getTitle());
	        }
	    }

	    // Method to display enrolled courses
	    public void displayEnrolledCourses() {
	        System.out.println("\n" + name + "'s Enrolled Courses:");
	        for (Course course : courses) {
	            System.out.println(course.getCode() + " - " + course.getTitle());
	        }
	    }
	}

	public class CourseRegistrationSystem {
	    public static void main(String[] args) {
	        // Create courses
	        Course javaCourse = new Course("CS101", "Java Programming", "Learn Java programming basics", 20, "Mon/Wed/Fri 9:00-10:30");
	        Course pythonCourse = new Course("CS102", "Python Programming", "Learn Python programming basics", 15, "Tue/Thu 11:00-12:30");

	        // Create students
	        Student student1 = new Student(1, "Alice");
	        Student student2 = new Student(2, "Bob");

	        // Display available courses
	        displayAvailableCourses(javaCourse, pythonCourse);

	        // Student registration
	        student1.enrollCourse(javaCourse);
	        student2.enrollCourse(pythonCourse);

	        // Display enrolled courses for each student
	        student1.displayEnrolledCourses();
	        student2.displayEnrolledCourses();

	        // Student drops a course
	        student1.dropCourse(javaCourse);
	        student1.displayEnrolledCourses();
	    }

	    // Method to display available courses
	    public static void displayAvailableCourses(Course... courses) {
	        System.out.println("Available Courses:");
	        for (Course course : courses) {
	            System.out.println(course.getCode() + " - " + course.getTitle() + " | Capacity: " + course.getCapacity() +
	                    " | Enrolled: " + course.getEnrolled() + " | Schedule: " + course.getSchedule());
	        }
	    }
	}
