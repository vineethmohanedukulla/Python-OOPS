# ICP-3

#### Complete the following:
```
Name: Vineeth Mohan Edukulla
Email: vekfd@umsystem.edu
```
---
```

```
<br/>
 
Write brief explanation here:

 
 ##  Object Oriented Python

### **Python  Inheritance Web Scraping**
 ### Lesson and Assignment Objectives
### **Question 1**
Create a class Employee and then do the following:
1. Create a constructor to initialize:
    1. id, name, department, salary, balance, and isEmployed=True.
2. Create a class attribute to count the number of Employees.
3. Create a Full_time and Part_time Employee classes and it should inherit the properties of Employee class.
    1. Call init method of the parent class to create an object in these classes.
4. Create giveRaise method for Full_time and Part_time classes. The full_time emp. Should have a default value 
of 10% increase and Part_time should have a default value of 5% increase.
5. Create the following functions:
    1. Pay: This should pay the employee once. Their balance should increase by the amount they are paid.
    2. Fire: this should remove the employee from the payroll. It should set their payrate to 0, and 
    isEmployed to false. 
        1. (Note: Retain the records for the employee, just make sure they aren’t paid anymore.)
    3. isEmployed: a Boolean function that should return if they are employed or not.
6. Read employee data from input.txt to create instances of the Employee class:
    1. File structure:
        1. NEW: keyword to create a new employee following: ID, Name, Department, Salary, 
        Type(Full_time “F”, Part_time “P”).
        2. RAISE: keyword to give raise to a specific employee following: ID, raise_percentage that 
        will change the emp. salary.
        3. PAY: keyword to pay all employee once, balance should increase by the amount they are 
paid (salary).
        4. FIRE: Keyword to remove the employee from payroll. Emp. Following is Emp. ID
7. Create a function to find the average salary paid to all employees of each class. Write the average salary paid 
to the end of output.txt file after printing the total number of employees.
8. Your program should output data to output.txt with the following format:
    1. Emp. Name, ID ###, Department:
    2. If employed, write out their Salary in this format: Current salary: $##
    3. If NOT employed, you should write out: Not employed with the company.
    4. The employee’s balance to date: Pay earned to date: $##
    5. Full-Time or part-time employee.
    6. Add a blank line between employees.
    7. ….
    8. Total number of employees: ###
    9. Average Salary paid to all Full-time employees: $###
    10. Average Salary paid to all Part-time employees: $###
### **Question 2**
**Web scraping**
Write a simple program that parse a Wiki page 
mentioned below and follow the instructions:
https://en.wikipedia.org/wiki/Machine_learning
1. Print out the title of the page
2. Find all the links in the page (‘a’ tag)
3. Iterate over each tag(above) then return the link using attribute "href" using get


## Softwares Required :
1. Python 3
2. Github Desktop
3. pycharm

## Implementation:
1. Developed the code for the problems and pushed the code file , video and screenshots to the github using github desktop.

## Tasks Performed
### **Question 1: Implementation**

# 
Created the parent and child classes as per the question details 

```python
class Employee:
    # to get the count of employees
    countOfEmployees = 0
    # Initialise the partime or full time employee data using the parent class EMployee
    def __init__(self, empID, name, department, salary, balance):
        self.empID = empID
        self.name = name
        self.department = department
        self.salary = salary
        self.balance = balance
        self.isEmployed = True
        self.__class__.countOfEmployees = self.__class__.countOfEmployees + 1

   # function is used to check if the employee is employed or not
    def isEmployed(self):
        return self.isEmployed
    # this method is used to fire the employee by changing the status of the isemployed = false
    def fire(self):
        self.isEmployed = False
        self.salary = 0
    # This method takes the percentage as input and raises its salary by that percentage.
    def giveRaiseByP(self, percent):
        self.salary = self.salary + (self.salary * percent) / 100
    # pay method will add the salary to the balance when called.
    def pay(self):
        self.balance = self.balance + self.salary

# declaration of FullTimeEmployee which is child class of Employee
class FullTimeEmployee(Employee):
    # used to differentiate the part time and full time employee
    Emptype = 'F'
    #FullTimeEmployee constructor
    def __init__(self, empID, name, department, salary, balance):
        # We will use the parent class to intialize the full time employee object
        super().__init__(empID, name, department, salary, balance)
    # The method is used to raise the percentage of the salary by 10% for full time employee
    def giveRaise(self):
        self.salary = self.salary + (self.salary / 10)

# declaration of PartTimeEmployee which is child class of Employee
class PartTimeEmployee(Employee):
    # used to differentiate the part time and full time employee
    Emptype = 'P'
    # PartTimeEmployee constructor
    def __init__(self, empID, name, department, salary, balance):
        super().__init__(empID, name, department, salary, balance)

    # The method is used to raise the percentage of the salary by 10% for full time employee
    def giveRaise(self):
        self.salary = int(self.salary) + int(self.salary) / 20

```
### **Wrote case statements for each operation NEW, RAISE, PAY, FIRE**
``` python
for line in inputData:
    # split() method to split the line into words
    words = line.split(' ')
    # NEW indicates to create an employee
    if words[0] == "NEW":
        if words[6].rstrip() == "F":
            # based on the input 'F' from the file we are creating full time object
            fullTimeEmployee = FullTimeEmployee(words[1], words[2] + " " + words[3], words[4], int(words[5]), 0)
            # appended the object to the list
            employeesList.append(fullTimeEmployee)
        if words[6].rstrip() == "P":
            # based on the input 'F' from the file we are creating full time object
            partTimeEmployee = PartTimeEmployee(words[1], words[2] + " " + words[3], words[4], int(words[5]), 0)
            # appended the object to the list
            employeesList.append(partTimeEmployee)
    # RAISE indicates to raise the amount of salary based on input
    elif words[0] == "RAISE":
        if len(words) > 2:
            for emp in employeesList:
                # iterated over the employee list to find the particular employee to raise
                if emp.empID == words[1].rstrip():
                    emp.giveRaiseByP(int(words[2].rstrip()))
                    break
        else:
            for emp in employeesList:
                if emp.empID == words[1].rstrip():
                    emp.giveRaise()
    # PAY indicated to pay the salary to the employee
    elif words[0].rstrip() == "PAY":
        for emp in employeesList:
            # iterated over all the employees and payed the salaries to the balance.
            emp.pay()
    # FIRE indicates to remove the employee.
    elif words[0] == "FIRE":
        for emp in employeesList:
            # iterated over the employee list to find the particular employee to fire
            if emp.empID == words[1].rstrip():
                emp.fire()
                break
```

Gathered all the data and pushed to the output file.

**Below is the output**
![image](https://user-images.githubusercontent.com/78897209/133160184-d7be688c-5b05-40b2-a102-b184bfd22078.png)


### Quesstion 2:
**Web Scraping**

We have used BeautifulSoup and requests library to fetch the information from the website and parse the html content.

```python
import requests
from bs4 import BeautifulSoup

# used get request to download the content in the response.
html = requests.get("https://en.wikipedia.org/wiki/Machine_learning")
# below line is used to parse the HTML content
beautifulObj = BeautifulSoup(html.content, "html.parser")
# printed the title of the web page
print(beautifulObj.title.string)
# finding the <a/> tags from the page and printing it to console
print(beautifulObj.findAll('a'))
# iterating through all the <a/> tags and get the href links
for link in beautifulObj.findAll('a'):
    # printing all the href's to console.
    print(link.get('href'))
```


**Below is the output prinitng the 'a' tags and href's in the website**
 ![image](https://user-images.githubusercontent.com/78897209/133160784-b329d8ec-9e36-40b6-b168-33f5f324c59e.png)

 ![image](https://user-images.githubusercontent.com/78897209/133160862-6fa94e55-aab9-45aa-a52c-c6c61f0fa4af.png)


**Code Explanation Video:**  
https://github.com/UMKC-APL-PythonDeepLearing/icp-3-vekfd/tree/master/Video%20Explanation

**Git video location:** 
https://github.com/UMKC-APL-PythonDeepLearing/icp-3-vekfd/raw/master/Video%20Explanation/icp3.mp4

