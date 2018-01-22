# REST

## Requirements

### Environment
- Typically we would recommend Ubuntu 17 for this Lab, but presently they have some issues. Before they are not resolved, we recommend Ubuntu 16.04 as the operating system for the labs.
- To not affect your existing OS on your laptop or workstation, we recommend that you use a virtual machine via VirtualBox

### VirtualBox and pyenv Installation
- follow our video tutorial
  or install on Laptop
- In addition we like you tu use pyenv so that you do not have to run 2 vms one for python 3.6 and one for python 2.17

### Database
- We will use MongoDB for our database
- Once the launch script and configuration file are saved an instance of MongoDB needs to be launched
  - ‘sudo service mongod start’
  - Check the .log file to ensure it has launched
- In our labs we’ll use the following command to start MongoDB
  - mongod --port portnumber --dbpath /path_to_your_folder
  - Here we specify a specific port to run the Mongodb service and we provide the path to the database to save the files in the local directories. It is better to provide a path in a separate folder within the workspace for this lab. 

## Installation
- # with PYENV 
  - `pyenv activate ENV3`
  - `pip install eve`

## Eve Configuration file and launch script
- Determine your working directory in your workstation
- Default settings are saved to settings.py
- Create a configuration file (vi settings.py)
  - Add one line:  
  - `DOMAIN = {'people': {}} `
  - This is a standard Python module
    - Informs Eve that the API has one accessible resource -- ‘people’

- Launch Script (run.py)
- This is the script that launches the API
- Make a launch script in the same directory as your config file with the below text.
- ```python
  from eve import Eve
  app = Eve()
  if __name__ == ‘__main__’:
      app.run()
  ```
  
## Launch the API
- Once the MongoDB is up and running and you must have a configuration file and a launch file ready. run.py and settings.py must be in the same directory.
- Start a launch script:
  - Open a new terminal so you can monitor the API
  - ```python
    python run.py
    * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
    127.0.0.1 - - [17/Jan/2018 10:54:35] "GET / HTTP/1.1" 200 -
    ```

## Consume the API
- Run the following command in terminal
  `$ curl -i http://127.0.0.1:5000`
- The response looks good with 200 response code, e.g.:
  ```
  HTTP/1.0 200 OK
  Content-Type: application/json
  Content-Length: 62
  Server: Eve/0.7.6 Werkzeug/0.11.15 Python/2.7.5
  Date: Wed, 17 Jan 2018 16:45:05 GMT
  ```
- Payload
  ```
  {
   "_links":{
      "child":[
         {
            "href":"people",
            "title":"people"
         }
      ]
   }
  }
  ```
  
## Issue a request
- `$ curl http://127.0.0.1:5000/people`
We get an additional _items list
  - _links are relative to the resource being accessed
  - link to the parent resource (home page) 
    and to the resource itself
    
- Payload
  ```
    {
     "_items":[ ],
    "_links":{
          "self":{
          "href":"people",
          "title":"people"
        },
          "parent":{
          "href":"/",
          "title":"home"
          }
    }
  ```






