---
title: "BCrypt Login System - Proof of Concept"
date: 2021-01-31T15:26:02Z
slug: "BCrypt-Login-System"
description: "A reasonably secure login system using BCrypt"
keywords: ["BCrypt", "Login System", "George Wood", "Academic Blog"]
draft: false
tags: [Cyber-Security, Projects, Python]
math: false
toc: false
---

Following on from some of my previous content about data security, I've written a short proof of concept program showing how BCrypt can be used to securely store passwords.

I hope you like it, and feedback is always welcome.

#### main.py
```python
try:
    from user import User
    import os
    import time
except ImportError:
    print("\nError! Necessary libraries unavailable...\n")


def clear():
    time.sleep(2.5)
    os.system('cls' if os.name == 'nt' else 'clear')


username = input("Username: ")
password = input("Password: ")

# Example Username: testUser
# Example Password: testPass

user = User(username, password)

go = True

while go:
    try:
        menu = int(input("\nEnter 1 to login\nEnter 2 to sign up\nEnter 3 to delete your credentials from the database\nEnter 4 to exit\n: "))

        if menu == 1:

            result = user.Authenticate()

            if result == True:
                print(f"\nSuccess!\nYou are logged in as: {user.Username}")
                clear()
            else:
                print("\nError! please try again...")
                clear()

        elif menu == 2:
            
            result = user.SignUp()

            if result == True:
                print(f"\nSuccess!\n\nYou are logged in as: {user.Username}")
                clear()
            else:
                print("\nError! that username is taken...")
                clear()

        elif menu == 3:

            result = user.RemoveUser()

            if result == True:
                print(f"\nThe credentials associated with the username {username} have been deleted.")
                clear()
                # Terminate program as User object must be recreated.
                go = False
            else:
                print("\nPlease make sure you are logged in before deleting your credentials.\n")
                clear()

        elif menu == 4:
            clear()
            go = False

        else:
            print("\nError! Please try again...")
            clear()
    except:
        print("\nAn unexpected error has occurred! Please try again...")
        clear()

```

#### user.py
```python
try:
    import bcrypt
    from replit import db
except ImportError:
    print("\nError! Necessary libraries unavailable...\n")


class User:

    IsAuthenticated = False
    Username = ""
    __Attempts = 0


    def __init__(self, username_input, password_input):

        # Initialise private variables
        self.__username_input = username_input
        self.__password_input = password_input

    
    def SignUp(self):
        '''Takes the username and password used to initialise the object, and stores them securely'''

        username = self.__username_input
        # Encode password to UTF-8 for use by BCrypt
        password_bytes = bytes(self.__password_input, "UTF-8")
        # Hash password using the BCrypt algorithm
        hashed_password = bcrypt.hashpw(password_bytes, bcrypt.gensalt(rounds=14))
        
        username_available = False # True for testing - change to False for

        # Checks if the username is available
        try:
            db[username]
        except KeyError:
            username_available = True

        if username_available:
            # Store password in database
            db[username] = hashed_password.decode()
            self.Username = username
            self.IsAuthenticated = True
            return True
        else:
            return False


    def Authenticate(self):
        
        # Default to False
        authenticated = False
        username = self.__username_input
        # Encode password to UTF-8 for use by BCrypt
        password_bytes = self.__password_input.encode("UTF-8")

        # Checks if the username is recognised
        try:
            stored_password = db[username]
        except KeyError:
            return False
        
        # Will return True if the inputted password matches the stored hash
        authenticated = bcrypt.checkpw(password_bytes, stored_password.encode("UTF-8"))

        if authenticated:
            self.IsAuthenticated = True
            self.Username = username
            return True
        else:
            self.__Attempts += 1
            return False


    def RemoveUser(self):

        username = self.__username_input

        try:
            # Credentials can only be removed if the user has logged in
            if self.IsAuthenticated == True:
                del db[username]
                self.IsAuthenticated = False
                return True
            else:
                return False
        except:
            return False
```

*Note: The code is also available on [repl.it](https://repl.it/@gwo0d/BCrypt-Login-System-OOP), and is designed to run on there.*

#### Test Credentials
```
Username: testUser
Password: testPass
```

#### License
```markdown
MIT License

Copyright (c) 2021 George Wood

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

*-George*
