Step 1 : Git Clone the Repository URL : https://github.com/pr2021/pilzassesment.git

Step 2 : Access the Root Directory "pilzassesment" using command -  cd pilzassesment

Step 3 : Install docker relevant to operating system using the link https://docs.docker.com/get-docker/

Step 4 : After installing Docker, please go to prometheus folder inside "pilzassesment folder" and open prometheus.yml and the file looks as shown below, please update the local machne IP address and save the file.
*****************************************
global:
  scrape_interval: 30s
  scrape_timeout: 10s

alerting:
  alertmanagers:
    - scheme: http
      static_configs:
        - targets: [ 'alertmanager:9093' ]  

rule_files:
  - alert.yml

scrape_configs:
  - job_name: services
    metrics_path: /metrics
    static_configs:
      - targets:
          - 'prometheus:9090'
  - job_name: alertmanager
    metrics_path: /metrics
    static_configs:
      - targets: 
          - 'alertmanager:9093'
  - job_name : nginxcontainer
    metrics_path: /metrics
    static_configs:
      - targets:
          - 'yourlocalmachineipaddress:9113'   <- Important Note :  Please update the system local IP Address. ( format example : 192.168.101.8:9113)
********************************************
Step 5 : After the prometheus.yml is updated, please revert back to the root directory "pilzassesment"

Step 6 : Open a terminal at the root directory folder "pilzassesment"

Step 7 : Run the command docker compose up ( it will start the prometheus, alertmanager and nginx container)

Step 8 : Access the prometheus at http://localhost:9000/ and prometheus user interface will be up and running.

Step 9 : Access the nginx container at http://localhost:9113/ and nginx will running and also displays the metrics.

Step 10 : Access the alert manager at http://localhost:9093/ and alert manager will be up and running.

Step 11 : To check the alerts from prometheus, alert manager and nginx, please have all the three host up and running.

Step 12 : To stop the nginx conainer run the command docker ps first, it shows the container ID of nginx, copy the container id of nginx and run the command docker stop "container id of nginx"

Step 13 : Access the nginx container at http://localhost:9113/ and reload the nginx will be down.

Step 14 : Please check the status of nginx container on prometheus at http://localhost:9000/ clicking on Status and targets, it will show the nginx container down.

Step 15 : Please access the alerts in prometheus it will turn from inactive to firing state after 5 seconds ( Please refresh the page it might get delayed based on bandwidth)

Step 16 : After it moves to firing state from inactive, please access alert manager at http://localhost:9093/ and click on alerts, it will display an alert that "NGINX container is down"
