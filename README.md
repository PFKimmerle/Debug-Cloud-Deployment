# Debugging a Cloud Deployment Issue

## Overview

This documentation provides a walkthrough for debugging an HTTP Error 500 encountered on a web server named `ws01` deployed in the cloud. The task involves identifying and resolving the issue to restore the web service to a healthy state.

## Introduction

As an IT administrator, encountering server errors is a common challenge. This task focuses on the hands-on process of diagnosing a server error and applying the necessary fixes to bring a web service back online.

## Steps to Debug the Issue

1. **Identify the Error**: 
    - Access the web server `ws01` via its external IP address to confirm the HTTP Error 500.
    - Understanding HTTP status codes is crucial for pinpointing the nature of the issue.

2. **Inspect the Web Server Status**: 
    - Use the `systemctl` command to check the status of the Apache service:
      ```
      sudo systemctl status apache2
      ```
    - Look for any error messages in the service status output that indicate why the service might have failed.

3. **Troubleshooting**: 
    - Inspect error logs or use the `journalctl` command to find detailed error messages.
    - If port conflicts are detected, identify which processes are binding to the conflicting ports using the `netstat` command:
      ```
      sudo netstat -nlp
      ```
    - Identify rogue processes (e.g., a Python test script) that should not be running on the production port.

4. **Resolve Port Conflicts**: 
    - Terminate any unauthorized processes using the `kill` command.
    - If a rogue service is found, stop and disable it using:
      ```
      sudo systemctl stop [service-name] && sudo systemctl disable [service-name]
      ```
    - Verify that the port is now free and no unauthorized services are running.

5. **Restart the Web Server**: 
    - Once the port conflict is resolved, restart the Apache service:
      ```
      sudo systemctl start apache2
      ```
    - Refresh the web browser to check if the service is back up and running.

## Resolution

Upon following these steps, the `ws01` web server should be back online, serving the default Apache2 Ubuntu page instead of the HTTP Error 500.

## Conclusion

The process detailed above highlights the practical skills needed to debug a live web server issue in a cloud environment. By following systematic troubleshooting steps, the web server was successfully recovered and returned to operational status.
