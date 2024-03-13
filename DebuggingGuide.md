# Comprehensive Debugging Guide for Cloud Deployment Issue

## Scripts and Their Purposes

The following scripts were used to diagnose and resolve the web server issue:

### Checking the Status of the Apache Web Server
- Command: `sudo systemctl status apache2`
- Purpose: To check the current status of the Apache web server service and determine if it is active, inactive, or facing any errors.

### Identifying Port Conflicts
- Command: `sudo netstat -nlp`
- Purpose: To list all network sockets along with the processes currently listening on them, identifying which process is occupying port 80.

### Locating the Rogue Python Script
- Command: `ps -ax | grep python3`
- Purpose: To filter the list of all active processes for any instances of `python3`, identifying unauthorized Python scripts running on the server.

### Viewing the Content of the Developer's Test Script
- Command: `cat /usr/local/bin/jimmytest.py`
- Purpose: To display the content of the Python test script `jimmytest.py` and verify that it is not part of the production environment.

### Killing the Rogue Process
- Command: `sudo kill [process-id]`
- Purpose: To terminate the rogue Python process that is inappropriately binding to port 80. Replace `[process-id]` with the actual PID of the process.

### Disabling the Rogue Service
- Command: `sudo systemctl stop jimmytest && sudo systemctl disable jimmytest`
- Purpose: To stop and disable the rogue service related to the Python script, preventing it from starting up on system boot.

### Restarting the Apache Web Server
- Command: `sudo systemctl start apache2`
- Purpose: To restart the Apache web server service after resolving the port conflict, thereby restoring the web service.

## Conclusion

By executing these scripts in the order presented, the HTTP Error 500 was successfully resolved. The web server `ws01` was brought back to a healthy state, serving the expected content.

