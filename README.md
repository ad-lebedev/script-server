# script-server
This is a simple web-server for hosting and executing scripts on a machine, providing control and output to remote users.
Using the script server you can create scripts on a machine with all the needed packages, configs, etc. All users will be able to execute the scripts without any system requirements (except browser) and in user-friendly interface.

## Requirements
Python 3. Modules:
* Tornado

Potentially should work on any OS, but was tested on Debian 8 only. 

## Security
Completely no security! Use it only in local network for fully trusted users. 

## Setup and run
1. Clone/download the repository
2. Create GUI configs for your scripts in _server-path_/configs folder (see config structure)
3. Launch server using python3: python launcher.py
Server will be running on 5000 port.

## Config structure
```javascript
{
  /**
    * Required: no
    * Description: user-friendly script name. Will be displayed to user 
    * Type: string
    * Default: script_path filename without extension
    */
  "name": "My example script",
  /**
    * Required: YES
    * Description: path to the script (relative to working directory)
    * Type: string
    */
  "script_path": "/some/path/to/script.sh",
  /**
    * Required: no
    * Description: user-friendly script description, which will be shown to a user
    * Type: string
    */
  "description": "Some useful description on what the script does",
  /**
    * Required: no
    * Description: if the script should be run in emulated terminal (if it has special behaviour in terminal).
    * Type: boolean
    * Default: true
    */
  "requires_terminal": true,
    /**
    * Required: no
    * Description: allows to specify working directory of the script.
    * Type: string
    * Default: the working directory, from which the server was started
    */
  "working_directory": "/home/me/temp",
  /**
    * Required: no
    * Description: list of script parameters
    * Type: array
    */
  "parameters": [
  {
    /**
      * Required: no
      * Description: the name of the parameter, which will be shown to the user. Required for non-constant parameters
      * Type: string
      */
      "name": "MyParam",
      /**
      * Required: no
      * Description: can be used for specifying script parameter name (e.g. script.sh -p myval). Omit this field for position based parameters
      * Type: string
      */
      "param": "-p",
      /**
      * Required: no
      * Description: if true, then no value will be passed to the script, only "param" will be specified
      * Type: boolean
      * Default: false
      */
      "no_value": false,
       /**
      * Required: no
      * Description: user-friendly description of the parameter, shown to the user (not yet implemented in GUI)
      * Type: string
      */
      "description": "This parameter is used for filename",
      /**
      * Required: no
      * Description: if the value of the parameter is required 
      * Type: boolean
      * Default: false
      */
      "required": false,
      /**
      * Required: no
      * Description: default value shown to user
      * Type: string
      */
      "default": "empty",
      /**
      * Required: no
      * Description: don't show parameter to user, but fill it in the script with the value of "default" field
      * Type: boolean
      * Default: false
      */
      "constant": false,
      /**
      * Required: no
      * Description: parameter type. Allowed values: int, list. Any other value will be simple text edit.
      * Type: string
      */
      "type": "int",
      /**
      * Required: no
      * Description: int type only, upper value bound 
      * Type: string
      */
      "max": "50",
      /**
      * Required: no
      * Description: int type only, lower value bound 
      * Type: string
      */
      "min": "-1",
      /**
      * Required: no
      * Description: list type only, array of allowed values for the parameter. Can be either predefined values or result from script invocation
      * Type: array or object
      */
      "values": [ "Apple", "Orange", "Banana" ]
      /** or "values": { "script": "ls /home/me/projects" } */
  }
  ]
}
```

## Logging
All web/operating logs are written to the _server-path_/logs/server.log
Additionally each script execution logs (output and error streams) are written to separate file in _server-path_/logs/processes. File name format is {script\_name}\_{client\_address}\_{date}\_{time}.log. 

## Testing/demo
Script-server has bundled configs/scripts for testing/demo purposes, which are located in testing folder. You can link/copy testing config files to server config files.
