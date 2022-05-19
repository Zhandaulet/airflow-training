# AIRFLOW Training notes

## TAKE YOUR TIME! 

### Benefits 
    - Dynamics
    - Scalability
    - UI
    - Extensibility

### Core Components
    WebServer / Flask Server with Gunicorn serving the UI
    Scheduler / Deamon charge of scheduling workflows
    Metastore / Database where metadata are stored
    Execute / Class defining how your tasks should be executed
    Workers / Process/sub process executing yours tasks

### DAG
    1. Data Pipeline: 1 > 2 > 3 (3>2>1) (3>1)
    2. Operators: Action, Transfer, Sensor

    ! NOT A DATA STREAMING SOLUTION NEITHER A DATA PROCESSING FRAMEWORK
    
    AIRFLOW is BEST ORCHESTRATOR tool

### One Node Orchestrator
    Node {
        {webServer} => {Metastore};
        {Scheduler} => {Metastore};
        {Scheduler} => {Executor,{Queue}};
        {Executor} => {Metastore}
    }

### Multi Node Orchestrator
    Node_1 {
        {webServer};{Scheduler};-- refers to "Node_2 - Metastore" => {Executor} 
    }

    Node_2 {
        {Metastore}; {Queue} --executed externally from "Node_1 - Executor"
    }

    Workers {
        {Worker_1}; {Worker_2}; {Worker_3} --triggered from "Node_2 - Queue"
    }

### Practising 

in cmd 
1. python -m venv Sandbox ~building up virtual env for python
2. source sandbox/bin/activate ~activating venv
3. pip install wheel ~installing wheel lib
4. pip install apache-airflow==2.0.0b3 --constraint url(url must be taken from github.com/marclamberdi/airflow version /constraint)
5. airflow db init ! must be run one time on build of airflow
6. ls ~list out content of folder

airflow.cfg
airflow.db
logs -- logs file
unittests.cfg
webserver_config.py

7. airflow webserver ! to run server
8. go to url http://localhost:8080 and enter login & password
9. airflow -h ! help commend to show all commands
10. airflow users -h 
11. airflow users create -u admin -p admin -f Zhandaulet -l Yespossynov -r Admin -e zhanespo@gmail.com
12. use login & password to login airflow url
13. airflow db upgrade ! to upgrade airflow to newer version
14. ! DO NOT USE IT in PROD : airflow db reset
15. airflow webserver ! to run and build airflow
16. airflow scheduler ! to run scheduler in airflow
17. airflow dags list ! list out all dags 
18. airflow tasks list example_xcom_args
19. airflow dags trigger -e 2020-01-01 example_xcom_args


DAG is Data Pipeline and Node - task, Edge - dependency

# Time to Practice 

1. T1 - Create Table
2. T2 - is_api_available
3. T3 - Extract_user - http request
4. T4 - Processing_users
5. T5 - Storing_Users

to connect VM

CTRL+ALT+P
Remote-SSH: Cpnnect to Host...
localhost
password: airflow
open new terminal

source sandbox/bin/activate
cd airflow

ls list out directory

mkdir dags if not exist

An Operator - defines ONE TASK in your data pipelines

# 3 types of operator

Action Operators: Execute an Action
Transfer Operators: Transfer Data
Sensors: Wait for a condition to be met

# create folder

wget https://airflow.apache.org/docs/apache-airflow/stable/docker-compose.yaml

docker-compose -f docker-compose.yaml up -d

docker-compose down --volumes --rmi all !!! removing everything.

docker logs container_id !!! to see logs of container

# commands from CLI to run DAGS in Airflow

1. to connect to VM from VSCode CTRL+ALT+P - > remote-ssh connect to host : "ssh -p 2222 airflow@localhost" and enter password for connection.
2. to enable venv sandbox use command "source sandbox/bin/activate"
3. to list content "ls" to create new file "mkdir".
4. to list all dags "airflow dags list"
5. to run webserver "airflow webserver" to run scheduler "airflow scheduler", ALWAYS use this command to test your Task "airflow tasks test #DAGName(user_processing) #TaskName(fromcsv to sql) #startdate(2022-05-19)
6. for missing providers install them in VM going to airflow apache providers and by pip command.
7. to connect db "sqlite3 db".
8. terminate connection with sqlite use "ctrl+d".

