# Yuwen-Cai-week7-mini-repo  

[![cicd](https://github.com/nogibjj/Yuwen-IDS706-miniproject7/actions/workflows/cicd.yml/badge.svg)](https://github.com/nogibjj/Yuwen-IDS706-miniproject7/actions/workflows/cicd.yml)  

This is a repo template for course 706_Data_Engineering Week 7 Mini Project. This objective was to create Package a Python script into a command-line tool and write a user guide.

# Purpose
- Package a Python script with setup tools or a similar tool
- Include a user guide on how to install and use the tool
- Include communication with an external or internal database (NoSQL, SQL, etc)


## Preparation
1. Format code with Python black by using `make format`

2. Lint code with Ruff by using `make lint`. 

3. Test code by using `make test`


## Code Location
You can find all the relevant code in Python with SQL database in main.py

Except of Using Click to Build a Command-Line Tool:

For the "CRUD" with database part:

### main.py using Click argument with database name setting 
```python
@click.command()
@click.argument("database_file")
def main(database_file):
    connection = create_connection(database_file)
    if connection:
        create_table(connection)
        # Create a new user
        insert_user(connection, "JohnDoe", "john@example.com")
        # Read a user
        user = get_user_by_username(connection, "JohnDoe")
        if user:
            print("User found:", user)
        # Update user email
        update_user_email(connection, "JohnDoe", "new_email@example.com")
        # Read the updated user
        updated_user = get_user_by_username(connection, "JohnDoe")
        if updated_user:
            print("Updated user:", updated_user)
        # Delete the user
        delete_user(connection, "JohnDoe")
        # user with shortest email
        insert_user(connection, "Apple", "a@example.com")
        insert_user(connection, "Banana", "Banana@example.com")
        insert_user(connection, "Orange", "ora@example.com")
        person = select_person_with_shortest_email(connection)
        if person:
            print("Person with the shortest email:")
            print("User ID:", person[0])
            print("Username:", person[1])
            print("Email:", person[2])
        else:
            print("No users in the database.")
        # select all users
        users = select_all_users(connection)
        for user in users:
            print("User ID:", user[0])
            print("Username:", user[1])
            print("Email:", user[2])

        connection.close()



if __name__ == "__main__":
    main()
```


### Usages
1. To create a sample database with name inputed:
 ```bash
python main.py <database_name>
```
![Alt text](<cml_regular.png>)

2. To see the guide, run
```bash
python main.py --help
```
![Alt text](<cml_help.png>)

3. Free Error Importing when argument not correct
![Alt text](<error_importing.png>)


### Results:
1. passing make test result
![Alt text](<make_test_result.png>)

2. passing make test in GitHub Actions:
![Alt text](<make_test_passing.png>)
