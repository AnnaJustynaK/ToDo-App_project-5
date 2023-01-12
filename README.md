# ToDo-App_project-5
The application will store tasks and projects. So we will be able to create new tasks and projects, delete them and display them all in Java
Template
Classically, let's start with a clean class template with the main method:

public class Main {
     public static void main(String[] args) {
        
     }
}
Let's start creating the application.

Needed Fields…
Of course, we'll need two boards - one to store projects, the other to store tasks. We will both initialize ourselves to 100 tasks and 100 projects.

static String [] tasks = new String[100];
static String [] projects = new String[100];
In addition, we will create a table for storing logs - a list of all operations that were performed within the application.

static String [] changeLog = new String[100];
Next, we'll need some variables where we'll store the array index that isn't already reserved by task/project/log. Each time we add one of these things, we'll increment a specific variable - it'll all become clear soon enough. Now let's initialize them.

static int tasksCount = 0;
static int projectsCount = 0;
static int changeLogCount = 0;
These will be the fields that we will use for our application - let's move on to creating methods to handle all the functionalities.

For now, all variables and methods will be static - later I'll show you what the word static is all about and how you can "get rid of" it.

Our code currently looks like this:

public class Main {
    
     static String [] tasks = new String[100];
     static String [] projects = new String[100];
     static String [] changeLog = new String[100];
     static int tasksCount = 0;
     static int projectsCount = 0;
     static int changeLogCount = 0;
    
     public static void main(String[] args) {
        
     }
}
Menu
The first thing we need to do is create a method to display the menu to the user. Plain, simple void function.

public static void displayMenu() {
     System.out.println("1 - Create new task");
     System.out.println("2 - Remove task");
     System.out.println("3 - Create new project");
     System.out.println("4 - Remove project");
     System.out.println("5 - Display all tasks");
     System.out.println("6 - Display all projects");
     System.out.println("7 - Display change log");
     System.out.println("0 - Exit app");
}
And that's it, we will use it to show the user what number is hidden under which functionality.

Adding Tasks
Let's start by adding a new task to our board.

The method signature will look like this:

public static void addTask(String task) {
}
It is a method of the void type, which takes the name of the task as an argument. Time to do something with it - time to add it to the board.

Before adding to the array, however, we need to check whether the task will still fit in our array. So we need to check if the value of the tasksCount variable is smaller than the length of the tasks table - so as not to go beyond the range of the table! In short, our index cannot exceed 99 - because our array is indexed from 0 to 99.

boolean hasCapacityForNewTask = tasksCount < tasks.length;
If we get true, it's time to add the variable to the array:

if (hasCapacityForNewTask) {
     tasks[tasksCount] = tasks;
}
We assign our task given by the argument to the function to the appropriate place in the table.

We just need to increase our taskCount - so that the next time we add a task, we will find an empty space in the array.

tasksCount++;
The ++ operator increases the value of a variable by 1.

So our method looks like this:

public static void addTask(String task) {
     boolean hasCapacityForNewTask = tasksCount < tasks.length;
     if (hasCapacityForNewTask) {
         tasks[tasksCount] = tasks;
         tasksCount++;
     }
}
We've finished adding tasks, it's time to move on.

Deleting a Task
A little more difficult functionality is deleting a task - especially where, like us, we store our tasks in an array. We must ensure that there are no gaps between the tasks - i.e. deleting tasks will consist in moving the tasks "down" by one index, which are "above" the deleted task. A bit confusing, but let's go to an example.

public static void removeTask(int indexTask) {
}
This is the signature of our method - we pass the index of the element to be removed as an argument.

Before deleting, we must check whether the given indexTask points to an existing task at all - i.e. indexTask will have to be smaller than tasksCount. This dependency must be met because tasksCount points to the first empty space in the array - that is, we use the < operator so that our index is one less than tasksCount - that is, the last task in the array.

boolean isTaskExist = indexTask < tasksCount;
If this condition is met, we can start deleting - i.e. moving the table.

if (isTaskExist) {
     for(int i=indexTask; i<tasksCount-1;i++) {
         tasks[i] = tasks[i+1];
     }
}
I'm explaining what's going on here.
Our starting point for the loop is i = indexTask – that is, we start from the index, which is given as an argument. It is this place in the table that we want to “press down” with other tasks.

The next condition is i < tasksCount - so thanks to this condition we will go through all the tasks that occur - not to the end of the array, but to the place where the last task is! There is -1 in the condition, because in the loop we have i + 1 - if we didn't have -1, we would go out of scope in the array.

tasks[i] = tasks[i+1] is responsible for shifting the values in the array - i.e. we assign the value tasks[1] to tasks[0], etc. - we move our tasks "down".

After moving all tasks, of course, we must not forget to decrease the index of the last task - after all, all tasks have been moved down.

tasksCount--;
And now our whole function responsible for deleting the task looks like this:

public static void removeTask(int indexTask) {
     boolean isTaskExist = indexTask < tasksCount;
     if (isTaskExist) {
         for(int i=indexTask; i<tasksCount-1;i++) {
             tasks[i] = tasks[i+1];
         }
         tasksCount--;
     }
}
Viewing Tasks
At the very end, we need to display our entire list of tasks to the user - after all, he needs to know what tasks he has to perform.

This will simply be a looping method where we will display the existing tasks.

public static void displayTasks() {
}
Let's give you information about what's going on:

System.out.println("List of tasks: ");
And in the loop, let's display the tasks:

for (int i=0; i<tasksCount;i++) {
     system.out.println(tasks[i]);
}
Look at the boundary condition - we display to the end of the range of tasks in the array - not to the very end of the array. We do not display the entire array, because there are empty values from tasks[tasksCount] - null to be precise.

So our entire display method looks like this:

public static void displayTasks() {
     System.out.println("List of tasks: ");
     for (int i=0; i<tasksCount;i++) {
         system.out.println(tasks[i]);
     }
}
We already have three basic methods of our application - it's time to check them in action.

We launch
Before we even start, we need to rip everything nicely in the main method, from where the application starts.

At the beginning, we will need a Scanner to read the values from the user and a while loop, which is designed to keep our application "alive" - i.e. it will be a (almost) infinite loop - thanks to each time we will get the menu displayed and we will be able to use the application.

Scanner scanner = new Scanner(System.in);
while(true) {
}
To make the loop almost infinite, let's add a boolean variable in the condition, which will allow us to exit the loop - i.e. terminate the application.

Scanner scanner = new Scanner(System.in);
boolean isApplicationRun = true;
while(isApplicationRun) {
}
All you have to do now is change isApplicationRun to false and the application will terminate its operation - because the while loop executes as long as the condition is true!

Let's add a radix variable to which we will load the number of the option selected by the user.

Scanner scanner = new Scanner(System.in);
int radix;
boolean isApplicationRun = true;
while(isApplicationRun) {
}
It's time to "push" our application into the while loop. Let's show the user a menu and ask him what option he wants to choose.

while(isApplicationRun) {
   displayMenu();
   System.out.print("Type number to choose option: ");
   radix = scanner.nextInt();
}
Now that we have the option that the user has chosen, it's time to control the operation of the program - we can use if or switch. We will choose the switch.

     while(isApplicationRun) {
       displayMenu();
         System.out.print("Type number to choose option: ");
       radix = scanner.nextInt();
       switch(radix) {
            
             default:
                 System.out.println("There is no such option.");
                 break;
         }
     }
}
I immediately added a default to it, which will be displayed when none of the listed options is selected.

Now let's add our functionalities to the switch.

At the beginning, adding a task - this will be case 1, because our menu says that after pressing 1 you can add a task.

case 1:
      System.out.println("Enter the name of the task to add: ");
      String task = scanner.next();
      addTask(task);
      break;
So we ask for the name of the task, load it and call our addTask method. And we've already mastered adding tasks.

Let's add the ability to delete tasks - case 2:

case 2:
     System.out.println("Enter the index of the task to be deleted: ");
     int index = scanner.nextInt();
     removeTask(index);
     break;
It works analogously to case 1 - we ask for the index to be removed, we load it and call the previously written removeTask method.

We still need to provide case 5 - displaying a list of tasks.
case 5:
     displayTasks();
     break;
This is just a call to the displayTasks() method - it is already responsible for displaying the tasks.

Completion of the Application
We do not have a handled application closure yet - i.e. case 0.

What do we need to change to complete our application? We need to exit the while loop - which is controlled by the isApplicationRun condition - it is currently set to true. Just change it to false and our loop will not execute anymore.

case 0:
     isApplicationRun=false;
     break;
So finally our main function looks like this:

public static void main(String[] args) {
     Scanner scanner = new Scanner(System.in);
   int radix;
   boolean isApplicationRun = true;
     while(isApplicationRun) {
       displayMenu();
         System.out.print("Type number to choose option: ");
       radix = scanner.nextInt();
       switch(radix) {
             case 1:
                 System.out.println("Enter the name of the task to add: ");
                 String task = scanner.next();
                 addTask(task);
                 break;
             case 2:
                 System.out.println("Enter the index of the task to be deleted: ");
                 int index = scanner.nextInt();
                 removeTask(index);
                 break;
             case 5:
                 displayTasks();
                 break;
             case 0:
                 isApplicationRun=false;
                 break;
             default:
                 System.out.println("There is no such option.");
                 break;
         }
     }
}
Testing
Our entire application should now look like this:

import java.util.Scanner;
public class Main {
     static String [] tasks = new String[100];
     static String [] projects = new String[100];
     static String [] changeLog = new String[100];
     static int tasksCount = 0;
     static int projectsCount = 0;
     static int changeLogCount = 0;
     public static void displayMenu() {
         System.out.println("1 - Create new task");
         System.out.println("2 - Remove task");
         System.out.println("3 - Create new project");
         System.out.println("4 - Remove project");
         System.out.println("5 - Display all tasks");
         System.out.println("6 - Display all projects");
         System.out.println("7 - Display change log");
         System.out.println("0 - Exit app");
     }
     public static void addTask(String task) {
         boolean hasCapacityForNewTask = tasksCount < tasks.length;
         if (hasCapacityForNewTask) {
             tasks[tasksCount] = tasks;
             tasksCount++;
         }
     }
     public static void removeTask(int indexTask) {
         boolean isTaskExist = indexTask < tasksCount;
         if (isTaskExist) {
             for(int i=indexTask; i<tasksCount-1;i++) {
                 tasks[i] = tasks[i+1];
             }
             tasksCount--;
         }
     }
     public static void displayTasks() {
         System.out.println("List of tasks: ");
         for (int i=0; i<tasksCount;i++) {
             system.out.println(tasks[i]);
         }
     }
     public static void main(String[] args) {
         Scanner scanner = new Scanner(System.in);
       int radix;
       boolean isApplicationRun = true;
         while(isApplicationRun) {
           displayMenu();
             System.out.print("Type number to choose option: ");
           radix = scanner.nextInt();
           switch(radix) {
                 case 1:
                     System.out.println("Enter the name of the task to add: ");
                     String task = scanner.next();
                     addTask(task);
                     break;
                 case 2:
                     System.out.println("Enter the index of the task to be deleted: ");
                     int index = scanner.nextInt();
                     removeTask(index);
                     break;
                 case 5:
                     displayTasks();
                     break;
                 case 0:
                     isApplicationRun=false;
                     break;
                 default:
                     System.out.println("There is no such option.");
                     break;
             }
         }
     }
}
Let's run it to test it - add 5 tasks, display them and remove two from the middle and finally see the status of the task list.

Status of tasks after adding tasks:

List of tasks:
Shopping
Washing
Ironing
Running
Dance
*Remove 2 - Washing and ironing and let's check the status of the list.

List of tasks:
Shopping
Running
Dance
