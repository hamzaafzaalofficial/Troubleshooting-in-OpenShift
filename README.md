# Troubleshooting-in-OpenShift
Objectives:
Diagnose and troubleshoot common container and pod issues.
Understand cluster events and alerts and how to respond to them.
Utilize OpenShift documentation effectively for troubleshooting.


Task 1: Simulate Common Pod Failures and Practice Troubleshooting
Objective:
Simulate common pod failures and practice troubleshooting to build effective diagnostic skills.

Explanation:
Understanding how to diagnose and resolve common pod failures is essential for maintaining the stability and reliability of applications running in an OpenShift cluster.

oc create deployment my-deployment --image=nginx:8
oc get pods 
Now to see the logs of the pod: 



oc logs pod/your_pod_name




Now, to set the correct image:



oc set image deployment/my-deployment nginx=nginx:latest 




Task 2: Monitor Cluster Events and Set Up Alerts
Objective:
Learn to monitor cluster events and set up alerts for potential issues.

Explanation:
Monitoring cluster events and setting up alerts enables proactive identification and resolution of potential problems, ensuring optimal cluster health.



oc get events 
# or for more specific those that are failed: 
oc get events | grep -i failed 


To set up an alert for the events of the pods: 

Create an alert.yaml file: 

apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
  name: my-alert
  namespace: openshift-monitoring
spec:
  groups:
  - name: event-alerts
    rules:
    - alert: NormalEventDetected
      expr: kube_event_type == "Normal"
      for: 1m
      labels:
        severity: info
      annotations:
        summary: "A Normal event has been detected"
        description: "A Normal event has occurred: {{ $labels.message }}" 


And then create it: 

oc create -f alert.yaml






Task 3: Use OpenShift Documentation to Resolve a Simulated Cluster Issue
Objective:
Practice using OpenShift documentation to resolve a simulated cluster issue.

Explanation:
Effectively utilizing documentation is a key skill in troubleshooting. You will learn how to navigate documentation to find solutions to common problems.





Utilize the documentation of RedHat OpenShift
