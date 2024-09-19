# Run UR5e Robot on ROS2 Humble Using Docker
This README provides a streamlined setup process for running a UR5e robot (the ones available in our lab) using ROS2 Humble and Docker.

## Prerequisites
Before you begin, ensure you have the following installed:
- Docker
- Docker Compose

## Setup Instructions
1. Create a Directory to store this repository
1. Clone the Repository
    ```
    git clone <repository-url>
    cd <repository-directory>
    ```
1. Build the Docker Containers 
    \
    When running for the first time, build the necessary Docker containers. From the cloned repository directory, execute:
    ```
    docker compose build
    ```
    This process may take approximately 20 minutes.

1. Run the System
    After the build completes, you can start the system. Use the command below to run both the ```ur_control``` and ```ur_moveit``` containers. Replace XXX.XXX.X.XXX with the actual IP address of your UR5e robot:
    ```
    ROBOT_IP=XXX.XXX.X.XXX docker compose up ur_control ur_moveit
    ```
    Note: If you intend to include ```ROS_DOMAIN_ID```, add ```ROS_DOMAIN_ID=X``` at the start of the command. ```ROS_DOMAIN_ID``` can be of any length, though it has to be a unique string.
    If you plan to develop scripts to command the robot, add the ```hello_moveit``` container to the command above. This container sets up the necessary configurations and launching the nodes required to operate a UR5e robot with MoveIt, a motion planning framework for ROS.
    Note: If you encounter the following error message:
    ```
    Error response from daemon: failed to create task for container: failed to create shim task: OCI runtime create failed: runc create failed: unable to start container process: exec: "/entrypoint.sh": permission denied: unknown
    ```
    Resolve this by making the entrypoint scripts executable. Navigate to the directory containing the entrypoint files and run:
    ```
    chmod +x entrypoint.sh devel_entrypoint.sh
    ```
    After adjusting the permissions, repeat Steps 3 and 4. The startup process should complete more quickly this time.