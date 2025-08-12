So look the thing is the NullPointerException is really a bad thing for you whole system as it migh poput somewhere in your code. so to stop this from happenin we will use
the optional<obj> 

lookt at the follwong to code snipts

```java
// code 1
public string getID(){
retrun this.id}
// code 2
public optional<string>  getID(){
retrung optional.ofnullebl(this.id)

}

```
not from what you can see both are the getter for the id feild but the differ becouse one will lead to nullpointer excetpion and the second one wont
wha tthe seonc code is saying is this methode will retrun a strign value of Id but it could be null it could be aninslized value so it puts what ever the return is int ot the 
container box where you have to open the box before pleging somthing you do this with the .ispresetn and isOpen 

the idea is simple.

and also about the .map this is alost anothere way of sayign if the object contianes do this you would use it this way
```
\ lets assume the class we are wokign on so far was an Employee class
Employee emp = new Employee(); // id is not initalized
int length = emp.getID().map(string->string.length()).orElse(0);
```
what is happenign here is that the getId will retunr and optional lobject but we dont know if contianes the objec that we are looking for so we open the optional implicilty with the map and then if
the object is not emepty we do the ssomthign over the function 
if it is empety the orEle will through 0;

now here is a very intersting exeriss that we will be doing

## the legacy project

Here is the "old, messy" legacy system. It works, but it's fragile because it uses null to communicate absence. Read through it to understand how it's structured.
Your entire job will be to interact with this LegacyCompanyDatabase class without letting its nulls escape into your new, modern code.


```java
public class Employee {
    private final long id;
    private final String name;
    private final Long managerId; // Can be null for the CEO

    public Employee(long id, String name, Long managerId) {
        this.id = id;
        this.name = name;
        this.managerId = managerId;
    }

    public long getId() { return id; }
    public String getName() { return name; }
    public Long getManagerId() { return managerId; } // Returns null for the CEO

    @Override
    public String toString() {
        return "Employee{" + "id=" + id + ", name='" + name + "', managerId=" + managerId + '}';
    }
}
```
Department.java

```java
import java.util.List;

public class Department {
    private final String name;
    private final List<Long> employeeIds;

    public Department(String name, List<Long> employeeIds) {
        this.name = name;
        this.employeeIds = employeeIds;
    }

    public String getName() { return name; }
    public List<Long> getEmployeeIds() { return employeeIds; }

    @Override
    public String toString() {
        return "Department{" + "name='" + name + '\'' + ", employeeIds=" + employeeIds + '}';
    }
}
```
LegacyCompanyDatabase.java

``` java

import java.util.List;
import java.util.Map;
import java.util.HashMap;

public class LegacyCompanyDatabase {
    private final Map<Long, Employee> employeeMap = new HashMap<>();
    private final Map<String, Department> departmentMap = new HashMap<>();

    public LegacyCompanyDatabase() {
        // --- POPULATE WITH DUMMY DATA ---

        // The CEO, has no manager
        Employee carol = new Employee(1L, "Carol (CEO)", null);

        // A manager who reports to the CEO
        Employee david = new Employee(2L, "David (Manager)", 1L);

        // Employees who report to David
        Employee alice = new Employee(3L, "Alice", 2L);
        Employee bob = new Employee(4L, "Bob", 2L);

        // An employee in another department who reports directly to the CEO
        Employee eve = new Employee(5L, "Eve", 1L);


        // Add all employees to the main map
        employeeMap.put(1L, carol);
        employeeMap.put(2L, david);
        employeeMap.put(3L, alice);
        employeeMap.put(4L, bob);
        employeeMap.put(5L, eve);


        // Create the departments
        Department engineering = new Department("Engineering", List.of(2L, 3L, 4L));
        Department sales = new Department("Sales", List.of(5L));
        Department hr = new Department("HR", List.of()); // An empty department

        departmentMap.put("Engineering", engineering);
        departmentMap.put("Sales", sales);
        departmentMap.put("HR", hr);
    }

    /**
     * Finds an employee by their ID.
     * THIS IS A "LYING" METHOD. It returns null if the employee is not found.
     */
    public Employee findEmployeeById(long id) {
        return employeeMap.get(id);
    }

    /**
     * Finds a department by its name.
     * THIS IS A "LYING" METHOD. It returns null if the department is not found.
     */
    public Department findDepartmentByName(String name) {
        return departmentMap.get(name);
    }
}
```

## what we should do now
<img width="1160" height="550" alt="image" src="https://github.com/user-attachments/assets/acb6bfa7-fe9b-4767-af01-ff653f5b37fa" /> 

now as per the quesion we shoud firs wrap the lying legacy methode with honset methode

so here is the Legacyservice class

```java
import java.util.Optional;

public class LegacyService {
    private final LegacyCompanyDatabase legacyCompanyDatabase;

    public LegacyService(){
        legacyCompanyDatabase = new LegacyCompanyDatabase();
    }
// this is the waper methode for the lying methode that is findEmployeeById(long id) 

    public Optional<Employee> findEmployeeById(Long Id){
        return Optional.ofNullable(legacyCompanyDatabase.findEmployeeById(Id));
        

    }

// this si the warper methode for the lying methode that is 


}

```




