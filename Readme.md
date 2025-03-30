# Project Documentation

## Project Setup

This project consists of a set of Bash scripts for managing users, groups, files, and monitoring system performance. The project is containerized using Docker for ease of deployment.

### Prerequisites
- Docker installed on your system.
- Basic knowledge of Bash scripting and Linux commands.

### Steps to Set Up the Project
1. Clone or download the project files into a directory.
2. Ensure all `.sh` scripts are executable. This is handled automatically in the Dockerfile using `chmod +x *.sh`.
3. Build the Docker image:
   ```sh
   docker build -t bash-scripts-project .

   Run the Docker container:
This will execute the user_script.sh script by default, as specified in the CMD directive of the Dockerfile.
Usage Instructions
Scripts Overview
file_script.sh: Manages file system operations such as creating directories, setting permissions, and checking disk usage.
group_script.sh: Handles group management, including adding, deleting, and listing groups.
system_monitor.sh: Continuously monitors system performance, logging CPU and memory usage at regular intervals.
user_script.sh: Manages user accounts, allowing you to add, delete, and list users.
Running the Scripts
To run a specific script, modify the CMD directive in the Dockerfile to point to the desired script. For example:

Then rebuild and run the container.

Alternatively, you can override the default command when running the container:

Script-Specific Instructions
file_script.sh:

Follow the menu prompts to create directories, set permissions, or check disk usage.
Logs are saved to /var/log/filesystem_management.log.
group_script.sh:

Use the menu to add, delete, or list groups.
Logs are saved to /var/log/group_management.log.
system_monitor.sh:

Runs continuously, generating performance reports every 60 seconds.
Logs are saved to /var/log/system_performance.log.
user_script.sh:

Use the menu to add, delete, or list users.
Logs are saved to /var/log/user_management.log.
Issues Encountered During Implementation
Log File Permissions:

The scripts write logs to /var/log/. Ensure the container has the necessary permissions to write to this directory. If not, consider changing the log file location to a user-accessible directory.
System Commands in Docker:

Some commands like useradd, groupadd, and df may not work as expected in a minimal Docker container. Ensure the base image (ubuntu:latest) includes the required utilities or install them during the build process.
Infinite Loop in system_monitor.sh:

The system_monitor.sh script runs indefinitely. To stop it, you need to manually terminate the container.
Interactive Prompts:

The scripts rely on interactive prompts, which may not work well in non-interactive environments. Consider modifying the scripts to accept command-line arguments for automation.
Docker Container Persistence:

Any changes made (e.g., adding users or groups) are lost when the container is stopped. To persist changes, consider mounting volumes or using a persistent storage solution.
Future Improvements
Add support for command-line arguments to make the scripts more automation-friendly.
Implement error handling for edge cases, such as invalid input or missing dependencies.
Provide a web-based interface for easier interaction with the scripts.
Use a logging framework to improve log management and analysis.