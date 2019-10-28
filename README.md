# VGU-CS2015-DuongHT-Bachelor-Thesis
An online demo for my local work.

## 1. Basic information

  | Section                         | Content                                                |
  | ------------------------------- | ------------------------------------------------------ |
  | ***Title of Bachelor Thesis:*** | A web-based intelligent editor for security modelling. |
  | ***Time alloted:***             | 9 weeks (Individual study).                            |
  | ***Accessor:***                 | Dr. Manuel Clavel.                                     |
  | ***Co-Accessor:***              | Dr. Michel Toulouse.                                   |
  | ***Registration date:***        | 06/06/2019.                                            |
  | ***Issue date:***               | 10/07/2019.                                            |
  | ***Deadline:***                 | 11/09/2019.                                            |

## 2. Thesis project
 - ### Requirements:
   - Programming language: Javascript (Allow using any Javascript framework, library).
   - Final product: An online working JSON editor.
   - Technical requirements:
   
     | Mandatory                                           | Optional                                |
     | --------------------------------------------------- | --------------------------------------- |
     | 1. Validate JSON syntax.                            | 1. Auto-closing braces and parentheses. |
     | 2. Validate a specific JSON schema.                 | 2. Auto-indentation.                    |
     | 3. Validate a specific JSON semantic.               | 3. Beautify messy JSON text input.      |
     | 4. Error messages adhere to priority of validation. | 4. Auto-completion.                     |
     | 5. Error messages suggest fixing solutions.         | 5. Auto-suggestion.                     |
     
    - JSON schema
      ```json
      [
        {
          "class" : "Reg_user",
          "permission" : [
            {
              "resources" : ["given_name", "middle_name", "family_name", "email"],
              "actions" : ["create", "read", "update", "delete"],
              "default" : "self = caller"
            },
            {
              "resources" : ["ginven_name", "middle_name", "family_name", "email"],
              "actions" : ["create", "read", "update", "delete"],
              "roles" : ["lecturer"],
              "auth" : "self.oclAsType(Student).courses->exists(c|c.lectures->includes(caller.oclAsType(Lecturer)))"
            },
            {
              "resources" : ["ginven_name", "middle_name", "family_name", "email"],
              "actions" : ["create", "read", "update", "delete"],
              "roles" : ["admin"],
              "auth" : "true"
            }
          ]
        }
      ]
      ```
      
     - JSON semantic
       - The editor always asks user to import a valid JSON file of data model before editing.
       - The sample JSON files of data model are "CarPerson_context.json" and "programDB_context.json".
         * CarPerson_context.json
         
           ```json
           [
             {
               "class" : "Car",
               "attributes" : [
                  {"name" : "Car_ref", "type" : "String"},
                  {"name" : "model", "type" : "String"},
                  {"name" : "color", "type" : "String"},
                  {"name" : "age", "type" : "Integer"}
               ]
             },
             {
               "class" : "Person",
               "attributes" : [
                  {"name" : "Person_ref", "type" : "String"},
                  {"name" : "name", "type" : "String"},
                  {"name" : "surname", "type" : "String"},
                  {"name" : "age", "type" : "Integer"}
                ]
              },
              {
                "association" : "Ownership",
                "ends" : ["owners", "ownedCars"],
                "classes" : ["Car", "Person"]
              }
           ]
           ```
           
          * programDB_context.json
           
            ```json
            [
              {
                "class" : "Role",
                "attributes" : [
                  {"name" : "name", "type" : "String"}]
              },
              {
                "class" : "Reg_User",
                "attributes" : [
                  {"name" : "family_name", "type" : "String"},
                  {"name" : "middle_name", "type" : "String"},
                  {"name" : "given_name", "type" : "String"},
                  {"name" : "email", "type" : "String"},
                  {"name" : "role", "type" : "Integer"}]
              },
              {
                "class" : "Student",
                "super" : "Reg_User"
              },
              {
                "class" : "Lecturer",
                "super" : "Reg_User"
              },
              {
                "class" : "Course",
                "attributes" : [
                  {"name" : "name", "type" : "String"}]
              },
              {
                "association" : "Enrollment",
                "ends" : ["courses", "students"],
                "classes" : ["Student", "Course"]
              },
              {
                "association" : "Teaching",
                "ends" : ["lectures", "lecturers"],
                "classes" : ["Lecturer", "Course"]
              } 
            ]
            ```

 - ### Development:
    - Technology details
    
       | Information              | Detail                                                            |
       | ------------------------ | ----------------------------------------------------------------- |
       | Library:                 | Ace.                                                              |
       | About Ace:               | https://ace.c9.io/#nav=about.                                     |
       | Official Ace GitHub:     | https://github.com/ajaxorg/ace/.                                  |
       | Pre-built files version: | https://github.com/ajaxorg/ace-builds/tree/master/src-noconflict. |
     
    - Keyboard shortcuts
    
       | Combination              | Execution                                                          |
       | ------------------------ | ------------------------------------------------------------------ |
       | ***Alt + O***            | Pop up a window to upload JSON files of data model before editing. |
       | ***Ctrl + Space***       | For auto-completion and auto-suggestion.                           |
       | ***Ctrl + Shift + B***   | Beautify messy JSON text input.                                    |
