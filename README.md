# CS Sensor deployment using helm charts
**License:**

THIS SCRIPT IS PROVIDED TO YOU "AS IS." TO THE EXTENT PERMITTED BY LAW, QUALYS HEREBY DISCLAIMS ALL WARRANTIES AND LIABILITY FOR THE PROVISION OR USE OF THIS SCRIPT. IN NO EVENT SHALL THESE SCRIPTS BE DEEMED TO BE CLOUD SERVICES AS PROVIDED BY QUALYS.

Helm is a package manager for Kubernetes and CS Sensor can be deployed using the helm chart, to do so you need to first update the helm values file with customer id, activation id, and Qualys URL.

Deploy the helm chart based on Kubernetes, container runtime versions and persistent storage configurations as shown below.

**Helm chart with docker as container runtime:**

*	“sensor-chart-docker-with-storage" chart for Kubernetes deployed with persistent storage. 

*	“sensor-chart-docker-without-storage" chart for Kubernetes deployed without persistent storage. 

**Helm chart with containerd as container runtime:**

*	“sensor-chart-containerd-with-storage" chart for Kubernetes deployed with persistent storage.

*	“sensor-chart-containerd-without-storage" chart for Kubernetes deployed without persistent storage. 

**Helm chart with crio as container runtime:**

*	“sensor-chart-crio-with-storage" chart for Kubernetes deployed with persistent storage.

*	“sensor-chart-crio-without-storage" chart for Kubernetes deployed without persistent storage. 

**Steps to deploy the helm chart on Kubernetes cluster:**

1.	Copy and extract the appropriate helm chart based on Kubernetes version and container runtime. 
2.	Update customer id, activation id, and Qualys URL from the < chart-name >/values.yaml file. 
3.	Update < chart-name >/values.yaml file with the required details and deploy it using following helm command. 
	* helm install qualys-sensor < untar location >/sensor-chart 
4.	Verify the installed release of helm chart. 
    * helm list 
5.	Upgrade the helm chart. 
    * helm upgrade qualys-sensor < untar location >/sensor-chart 
6.	Uninstall the helm chart. 
    * helm uninstall qualys-sensor 

**Helm charts values file:**

Following are the default values of the CS Sensor helm chart, please update them accordingly. 

*	customerID: - Your customer id
*   activationID: - Your activation id
*   pod_url: - Your [POD_URL_from_sensor_deployment_guide_page_13](https://www.qualys.com/docs/qualys-container-sensor-deployment-guide.pdf) 
*   image: "qualys/qcs-sensor:latest"  - Qualys sensor image location 
*   imagePullPolicy: "IfNotPresent" – Default image pull policy
*   cpu: "0.2" - Default CPU
*	args: "[\"--k8s-mode\", \"--log-level\", \"3\"]" - default value for docker as runtime

**Update the “args” value to increase the log-level, supported values are 1 to 5, use 3 for standard and 5 for verbose logging**

    args: "[\"--k8s-mode\", \"--log-level\", \"3\"]"

**Update the “args” value as below to enable console logs**

	args: "[\"--k8s-mode\", \"--log-level\", \"3\", \"--enable-console-logs\"]"

**Update the “args" value as below to configure sensor without persistent storage with docker as runtime**

	args: "[\"--k8s-mode\", \"--log-level\", \"3\", \"--sensor-without-persistent-storage\", \"--enable-console-logs\"]"

See page 45 from [container sensor deployment guide](https://www.qualys.com/docs/qualys-container-sensor-deployment-guide.pdf) to find our more information about “args” values. 
