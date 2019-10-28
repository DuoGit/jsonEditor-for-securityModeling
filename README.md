# A web-based intelligent editor for security modeling

## Description
  A computer science bachelor thesis. Time alloted: 9 weeks (Individual study).

## Features
  * **Data models**
  
    An example to demonstrate data models:  Consider a simple domain, where there are only cars and persons. The persons can own cars (they are their owners), and, logically, the cars can be owned by persons (they are their ownedCars). No restriction is imposed regarding ownership: a person can own many different cars (or none), and a car can be owned by many different persons (or by none). Finally, each car can have a color, and each person can have a name. This domain can be model (using our JSON-format) as follows:
    
    ```json
     [
      {"class" : "Car",
       "attributes" : [
          {"name" : "color", "type" : "String"},
          {"name" : "model", "type" : "String"}
          ]
      },
      {"class" : "Person",
       "attributes" : [
          {"name" : "name", "type" : "String"},
          {"name" : "age", "type" : "String"}
          ]
      },
      {"association" : "Ownership",
       "ends" : ["owners", "ownedCars"],
       "classes" : ["Car", "Person"]
      }
     ]
    ```

  * **Security models**
  
      An example to demonstrate security models: Consider the following (fine-grained) access-control policy, where Person is the user-class.
    
    * Any user can read the name of any other user.
    * Any user can read its own age.
    * Any user with role “Police” can read the age of the cars’ owners.
    * Any user with role “Police” can read the cars’ owners.
    * Any user with role “Police” can read the owners’ cars.
    
    
    ```json
     [
      {
        "class" : "Car",
        "permissions" : [
          {
            "actions" : ["read"],
            "resources" : ["owners"],
            "roles" : ["Police"],
            "auth" : "true"
          }
        ]
      },
      {
        "class" : "Person",
        "permissions" : [
          {
            "actions" : ["read"],
            "resources" : ["name"],
            "default" : "true"
          },
          {
            "actions" : ["read"],
            "resources" : ["age"],
            "default" : "self = caller"
          },
          {
            "actions" : ["read"],
            "resources" : ["age"],
            "roles" : ["Police"],
            "auth" : "self.ownedCars->notEmpty()"
          },
          {
            "actions" : ["read"],
            "resources" : ["ownedCars"],
            "roles" : ["Police"],
            "auth" : "true"
          }
        ]
      }
    ]
    ```
  
  * **Basic functionalities**
    * *Upload data models*
    
      The editor opens a window from the client side for users to select a JSON file representing a data model. The data model is then uploaded to the editor. This model will be the underlying data model for the security model.

      ![image](https://drive.google.com/uc?export=view&id=1DKPKGmJBDB6JwEAYvrtmYN_Svwvc8U5P)
      
    * *Create and edit a security model*
    
      A new security model can be created by typing manually or pasting security model into the editing area of the editor. With the text, users can perform editing actions such as insert and delete.
      
      ![image](https://drive.google.com/uc?export=view&id=1u3AYvCvq2bEuqcW_urO0dPT1_oZsFM0V)
    
    * *Save security model*
    
      Users can choose a location in the local file system to save the security model they are working on. The security model can be saved without validating.

      ![image](https://drive.google.com/uc?export=view&id=12XmBZS7QkIdnslV4Nt9WJWim-bV34hrM)



  * **Intelligent features**
    * *Auto-completion*
    
      The editor tries to predict the full word a user is intending to type, based on what it has typed before. The editor displays the possible completions in a list, for the user to select.
      
      ![image](https://drive.google.com/uc?export=view&id=1LJU2CWlH5RgsSrKH_GtEYHv6tQo0zxbO)
      

    * *Keyword suggestion*
    
      The editor also displays possible keywords even if the user has not typed anything yet.  It is useful when the user does not remember at all what keywords can be typed. This feature is activated by press (Ctrl + Space).
  
      ![image](https://drive.google.com/uc?export=view&id=1dIh_vTXkPqSTyqp0Cjh4-1QzcSQGSNqD)

  
    * *Error-marking and error-fixing*
    
      The editor automatically displays a red square on the left margin of the line, where it detects an error. When there are multiple errors, the one with the lowest line number is displayed first. Users can hover the pointer over the error mark or press (Alt + E) to read an explanation of error message.
      
      ![image](https://drive.google.com/uc?export=view&id=1ECFZ1SvwP3D1TpQekyybR4FVBf23_XIQ)



  * **Other features**
    * *Indentation*
    
      The editor automatically indents each new line according to its position in the JSON schema.
      
      ![image](https://drive.google.com/uc?export=view&id=1Qak2guHKkOes3EiKgosGIn4fHNXzBoDf)
      

    * *Auto-closing*
    
      The editor automatically inserts the ending components of the pairs of square brackets, curly braces, parentheses and double quotes.
      
      ![image](https://drive.google.com/uc?export=view&id=1UWd-mbHPxUFX_HXYX4_2pzIKtCRg1SG1)
      
      
    * *Code-folding*
    
      The content written inside any pair of curly braces or square brackets can be folded into one line.

      * Before folding
      
        ![image](https://drive.google.com/uc?export=view&id=1wt-7cTgHyLuvsKVHv_BbAJsfd_aVLgrX)

      * After folding

        ![image](https://drive.google.com/uc?export=view&id=1zFM0_d_ZhOvbEXhjBbukIq3u087pXcPL)



    * *Syntax-highlighting*
    
      The editor automatically highlights all keywords with the same color. The color for keywords is different from the color for values.
      
      * Before highlighting
        
        ![image](https://drive.google.com/uc?export=view&id=1vkmovqRluzPWCpqTfXso1qzWKdIMpY6G)

      * After highlighting

        ![image](https://drive.google.com/uc?export=view&id=1mSp_YhZk0h2vGK-Qut8y7aFx3riHb369)


    * *Code-beautifying*
           
      * Before beautifying

        ![image](https://drive.google.com/uc?export=view&id=1UeZnq6i3LHuGvqGCeZkLFnx_28mjfeZr)

      * After beautifying

        ![image](https://drive.google.com/uc?export=view&id=1YNnVV-CxEzaFMrMGSGKQkOyTLnJ0hprq)


    * *Command keys*
    
      | **Command**    | **Functionality**       |
      |----------------|-------------------------|
      |*(Alt+O)*       |  Import a data model    |
      |*(Alt+E)*       |  Go to next error       |
      |*(Ctrl+Z)*      |  Undo                   |
      |*(Ctrl+Space)*  |  Suggest keyword        |
      |*(Ctrl+Shift+B)*|  Beautify JSON          |
      |*(Ctrl+Shift+S)*|  Download security model|
      
      
## Deployment and usage

  * **Before using**, please download one of the following sample data models to later upload to the web app:
  
    * *CarPerson_context*. [Donwload here](https://drive.google.com/file/d/1f9msBrQ8_2Fppmi_btbKD8UmTxfuZWdE/view?usp=sharing).
    
    * *ProgramDB_context*. [Donwload here](https://drive.google.com/file/d/18ZQRlHkD-MsfqkXj5OIjl4QpIkO5fBHW/view?usp=sharing).
    
  * The editor was deployed on heroku. [Click me!](https://json-editor-for-security-model.herokuapp.com)


## Author
     Duong Thai Hoang
