<!--  2DV610 Software Testing   Assignment 2 Task 1                       -->
<!--                                                                      -->
<!--  Author:  Jonas Sjöberg                                              -->
<!--           Linnaeus University                                        -->
<!--           js224eh@student.lnu.se                                     -->
<!--           github.com/jonasjberg                                      -->
<!--           www.jonasjberg.com                                         -->
<!--                                                                      -->
<!-- License:  Creative Commons Attribution 4.0 International (CC BY 4.0) -->
<!--           <http://creativecommons.org/licenses/by/4.0/legalcode>     -->
<!--           See LICENSE.md for additional licensing information.       -->


# Manual Test Cases
<!-- * Are the manual test-cases traceable to which requirement that is tested? -->
<!-- * Do each manual test-case describe, input and expected output? (when relevant) -->


## Requirements
The following requirements should be transformed into actual test cases;

- The web server should be responsive under high load.
- The web server must follow minimum requirements for HTTP 1.1
- The web server must work on Linux, Mac, Windows.
- The web server must be absolutely secure.


## Test Cases
### `UC1` --- Start Server
#### Primary Actor:
Administrator

#### Postcondition: 

- A web server has been started
- A note in the access log was written, that the server was started

#### Main scenario

- Starts when an administrator wants to start the server.
- System asks for socket port number and shared resource container 
- The administrator provides a socket port number and a shared resource container
- System starts a web server on the given port and presents that the server was started and writes a note in the access log.

#### Alternate Scenarios

- The web server could not be started due to socket was taken
    - System presents an error message: "Socket XX was taken" (XX is the socket number, Example "80")
    - Exit Use Case

- The web server could not be started due restriction on the shared resource container
    - System presents an error message: "No access to folder XX" (XX is the shared resource container provided, Example "`\var\www`")
    - Exit Use Case

- The access log could not be written to
    - System presents an error message. "Cannot write to server log file `log.txt`"
    - Exit Use Case


### `UC2` --- Stop Server
#### Primary Actor
Administrator

#### Precondition: 
- A web server has been started

#### Postcondition: 
- A note in the access log was written, that the server was stopped

#### Main scenario
1. Starts when a user wants to stop the server.
2. System stops the web server and presents that the webserver has been stopped


### `UC3` --- Request shared resource
#### Primary Actor
Browser

#### Precondition: 
- A web server has been started

#### Postcondition: 
- A note in the access log was written, that access happened with request information and the result of the request.

#### Technical note

- Browser and System communicates using HTTP 1.1.
- Error messages are part of HTTP 1.1 protocol
    - 200 OK
    - 400 Bad request
    - 403 Forbidden
    - 404 Not Found

#### Main scenario

- Starts when a Browser wants to access a shared resource
- System delivers the shared resource to the browser and a success message is written to the access log.

#### Alternate Scenarios

- 2a The shared resource cannot be found 
    - System presents that the resource cannot be found
    - Exit Use Case
- 2b The shared resource is outside the shared resource container
    - System presents that the resource is forbidden
    - Exit Use Case
- 2c The resource request is invalid or malformed
    - System presents that the request cannot be handled
    - Exit Use Case
- 2d The server encounters an error when trying to process the request
    - System presents that it has an internal error
    - Exit Use Case
