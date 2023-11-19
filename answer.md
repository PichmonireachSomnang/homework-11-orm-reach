1. add new employee record to employee table with id = 168, firstname = 'John', lastname = 'Doe', initials = 'JD', job = 'Programmer', hire_date = today's date.

```python
employee = Employee(emp_num=168, emp_lname="Doe", emp_fname="John", emp_initial="JD",emp_hiredate=date.today(), job_code=500)
session.add(employee)
session.commit()
print("New Employee record added successfully!")
```

---

2. query the new created employee (id=168) from employee table, with information of employee id, firstname, lastname, initials, job description (join with job), charge per hour (join with job) and hire_date.

```python
employees = session.query(Employee, Job).filter(Employee.job_code == Job.job_code).filter(Employee.emp_num == 168).all()
for employee in employees:
    print(employee.Employee.emp_num,employee.Employee.emp_lname, employee.Employee.emp_fname, employee.Employee.emp_initial, 
          employee.Job.job_description, employee.Job.job_chg_hour, employee.Employee.emp_hiredate)
```

---


3. update the new created employee (id=168) job, from 'Programmer' to 'Database Designer'.

```python
employee = session.query(Employee).filter(Employee.emp_num == 168).first()
job = session.query(Job).filter(Job.job_description == 'Database Designer').first()

if employee and job:
    employee.job_code = job.job_code
    session.commit()
    print("Successfully updated.")
else:
    print("Employee or job not found.")
```


---

4. query all project that has "Programmer" assigned to, with information of project id, project name and program manager (join with employee).

```python
projects = session.query(Project, Employee).filter(Project.emp_num == Employee.emp_num).filter(Employee.job_code == 500).all()
for project in projects:
    print(project.Project.proj_num, project.Project.proj_name, project.Employee.emp_fname, project.Employee.emp_lname)
```



---

5. delete the new created employee (id=168) from employee table.

```python
employee = session.query(Employee).filter(Employee.emp_num == 168).first()
session.delete(employee)
session.commit()
```
