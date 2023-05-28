# k8sexam
# PART-1 - K8s exam:
---
1. Deploy a pod named nginx-pod using the nginx:alpine image. Name: 
nginx-pod-yourname Image: nginx:alpine

---
    apiVersion: v1
    kind: Pod
    metadata:
    creationTimestamp: null
    labels:
        run: nginx-pod-roi
    name: nginx-pod-roi
    spec:
    containers:
    - image: nginx:alpine
        name: nginx-pod-roi
        resources: {}
    dnsPolicy: ClusterFirst
    restartPolicy: Always
    status: {}
---

2. Deploy a messaging pod using the redis:alpine image with the labels set to tier=msg. Pod Name: messaging Image: redis:alpine Labels: tier=msg 

---
    apiVersion: v1
    kind: Pod
    metadata:
    creationTimestamp: null
    labels:
        tier: msg
    name: messaging
    spec:
    containers:
    - image: redis:alpine
        name: messaging
        resources: {}
    dnsPolicy: ClusterFirst
    restartPolicy: Always
    status: {}
---
3. Create a namespace named apx-x998-yourname
---

    apiVersion: v1
    kind: Namespace
    metadata:
    creationTimestamp: null
    name: apx-x998-roi
    spec: {}
    status: {}
---
4. Get the list of nodes in JSON format and store it in a file at /tmp/nodes-yourname
---
    kubectl get nodes -o json > /tmp/nodes-roi
---
5. Create a service messaging-service to expose the messaging application within the
cluster on port 6379. a. Use imperative commands - kubectl b. Service: messaging-service c. Port: 6379 d. Type: ClusterIp e. Use the right labels
---
    kubectl expose pod messaging --port=6379 --name=messaging-service --type=ClusterIP
---
6. Create a service messaging-service to expose the messaging application within the cluster on port 6379. a. Service: messaging-service b. Port: 6379 c. Type: ClusterIp d. Use the right labels
---
    apiVersion: v1
    kind: Service
    metadata:
    creationTimestamp: null
    labels:
        tier: msg
    name: messaging-service
    spec:
    ports:
    - port: 6379
        protocol: TCP
        targetPort: 6379
    selector:
        tier: msg
    type: ClusterIP
    status:
    loadBalancer: {}
---
7. Create a deployment named hr-web-app using the image kodekloud/webapp-color with 2 replicas a. Name: hr-web-app b. Image: kodekloud/webapp-color c. Replicas: 2
---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
    creationTimestamp: null
    labels:
        app: hr-web-app
    name: hr-web-app
    spec:
    replicas: 2
    selector:
        matchLabels:
        app: hr-web-app
    strategy: {}
    template:
        metadata:
        creationTimestamp: null
        labels:
            app: hr-web-app
        spec:
        containers:
        - image: kodekloud/webapp-color
            name: webapp-color
            resources: {}
    status: {}
---
8. Create a static pod named static-busybox on the master node that uses the busybox image and the command sleep 1000 a. Name: static-busybox b. Image: busybox
---
    apiVersion: v1
    kind: Pod
    metadata:
    name: static-busybox
    spec:
    containers:
    - name: busybox-container
        image: busybox
        command: ["sleep", "1000"]
        resources: {}
---
9. Create a POD in the finance-yourname namespace named temp-bus with the image redis:alpine a. Name: temp-bus b. Image Name: redis:alpine
---
    apiVersion: v1
    kind: Namespace
    metadata:
    creationTimestamp: null
    name: finance-roi
    spec: {}
    status: {}
---
    apiVersion: v1
    kind: Pod
    metadata:
    creationTimestamp: null
    labels:
        run: temp-bus
    name: temp-bus
    namespace: finance-roi
    spec:
    containers:
    - image: redis:alpine
        name: temp-bus
        resources: {}
    dnsPolicy: ClusterFirst
    restartPolicy: Always
    status: {}
---
10. Create a Persistent Volume with the given specification a. Volume Name: pv-analytics b. Storage: 100Mi c. Access modes: ReadWriteMany d. Host Path: /pv/data-analytics 
---
    apiVersion: v1
    kind: PersistentVolume
    metadata:
    name: pv-analytics
    spec:
    storageClassName: manual
    capacity:
        storage: 100Mi
    accessModes:
        - ReadWriteMany
    hostPath:
        path: "/pv/data-analytics"
---
11. Create a Pod called redis-storage-yourname with image: redis:alpine with a Volume of type emptyDir that lasts for the life of the Pod. specs:. a. Pod named 'redis-storage-yourname'  b. Pod 'redis-storage-yourname' uses Volume type of emptyDir c. Pod 'redis-storage-yourname' uses volumeMount with mountPath = /data/redis
---
    apiVersion: v1
    kind: Pod
    metadata:
    name: redis-storage-roi
    spec:
    containers:
    - image: redis:alpine
        name: test-container
        volumeMounts:
        - mountPath: /data/redis
        name: cache-volume
    volumes:
    - name: cache-volume
        emptyDir:
        sizeLimit: 500Mi
---
12. Create this pod and attached it a persistent volume called pv-1 a. Make sure the PV mountPath is hostbase : /data
---
    metadata:
    labels:
        run: use-pv
    name: use-pvspec-roi
    spec:
    containers:
    - image: nginx
        name: use-pv
        volumeMounts:
        - mountPath: /data
        name: pv-1
    volumes:
    - name: pv-1
        hostPath:
        path: /tmp
        type: Directory
---
13. Create a new deployment called nginx-deploy, with image nginx:1.16 and 1 replica. Record the version. Next upgrade the deployment to version 1.17 using rolling update. Make sure that the version upgrade is recorded in the resource annotation. a. Deployment : nginx-deploy. Image: nginx:1.16 b. Image: nginx:1.16 c. Task: Upgrade the version of the deployment to 1:17 d. Task: Record the changes for the image upgrade
---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
    creationTimestamp: null
    labels:
        app: nginx-deploy
    name: nginx-deploy
    spec:
    replicas: 1
    selector:
        matchLabels:
        app: nginx-deploy
    strategy: {}
    template:
        metadata:
        creationTimestamp: null
        labels:
            app: nginx-deploy
        spec:
        containers:
        - image: nginx:1.16
            name: nginx
            resources: {}
    status: {}
---
14. Create an nginx pod called nginx-resolver using image nginx, expose it internally with a service called nginx-resolver-service. Test that you are able to look up the service and pod names from within the cluster. Use the image: busybox:1.28 for dns lookup. Record results in /root/nginx-yourname.svc and /root/nginx-yourname.pod
---
    apiVersion: v1
    kind: Pod
    metadata:
    name: dns-lookup
    spec:
    containers:
    - name: busybox
        image: progrium/busybox
        command:
        - sleep
        - "3600"
        imagePullPolicy: IfNotPresent
    restartPolicy: Never
    dns-lookup
---
    apiVersion: v1
    kind: Service
    metadata:
    creationTimestamp: null
    labels:
        run: nginx-resolver
    name: nginx-resolver
    spec:
    ports:
    - port: 80
        protocol: TCP
        targetPort: 80
    selector:
        run: nginx-resolver
    status:
    loadBalancer: {}
---
    apiVersion: v1
    kind: Pod
    metadata:
    name: dns-lookup
    spec:
    containers:
    - name: busybox
        image: progrium/busybox
        command:
        - sleep
        - "3600"
        imagePullPolicy: IfNotPresent
    restartPolicy: Never
    dns-lookup
---
    > GET / HTTP/1.1
    > Host: nginx-resolver.default.svc.cluster.local
    > User-Agent: curl/8.1.1
    > Accept: */*
    >
    < HTTP/1.1 200 OK
    < Server: nginx/1.25.0
    < Date: Sun, 28 May 2023 07:58:51 GMT
    < Content-Type: text/html
    < Content-Length: 615
    < Last-Modified: Tue, 23 May 2023 15:08:20 GMT
    < Connection: keep-alive
    < ETag: "646cd6e4-267"
    < Accept-Ranges: bytes
    <
    <!DOCTYPE html>
    <html>
    <head>
    <title>Welcome to nginx!</title>
    <style>
    html { color-scheme: light dark; }
    body { width: 35em; margin: 0 auto;
    font-family: Tahoma, Verdana, Arial, sans-serif; }
    </style>
    </head>
    <body>
    <h1>Welcome to nginx!</h1>
    <p>If you see this page, the nginx web server is successfully installed and
    working. Further configuration is required.</p>

    <p>For online documentation and support please refer to
    <a href="http://nginx.org/">nginx.org</a>.<br/>
    Commercial support is available at
    <a href="http://nginx.com/">nginx.com</a>.</p>

    <p><em>Thank you for using nginx.</em></p>
    </body>
    </html>
---
15. Create a static pod on node01 called nginx-critical with image nginx. Create this pod on node01 and make sure that it is recreated/restarted automatically in case of a failure.
---
    apiVersion: v1
    kind: Pod
    metadata:
    creationTimestamp: null
    labels:
        run: nginx-critical
    name: nginx-critical
    spec:
    containers:
    - image: nginx
        name: nginx-critical
        resources: {}
    dnsPolicy: ClusterFirst
    restartPolicy: Always
    status: {}

---
16. Create a pod called multi-pod with two containers. Container 1, name: alpha, image: nginx Container 2: beta, image: busybox, command sleep 4800. a. Environment Variables: i. container 1: ii. name: alpha  iii. Container 2: iv. name: beta
---
    apiVersion: v1
    kind: Pod
    metadata:
    name: multi-pod
    spec:
    containers:
    - name: alpha
        image: nginx
        env:
        - name: NAME
        value: "alpha"
    - name: beta
        image: busybox
        command: ["sleep", "4800"]
        env:
        - name: NAME
        value: "beta"
---
# PART-2 - Pod Design Questions:

1. Get pods with label information
---
    kubectl get pods --show-labels
---
2. Create 5 nginx pods in which two of them is labeled env=prod and three of them is labeled env=dev
---
    kubectl run nginx-pod-prod-1 --image=nginx --labels=env=prod
    kubectl run nginx-pod-prod-2 --image=nginx --labels=env=prod
    kubectl run nginx-pod-dev-1 --image=nginx --labels=env=dev
    kubectl run nginx-pod-dev-2 --image=nginx --labels=env=dev
    kubectl run nginx-pod-dev-3 --image=nginx --labels=env=dev
---
3. Verify all the pods are created with correct labels 
---
    kubectl get pods --show-labels
---
4. Get the pods with label env=dev
---
    kubectl get pods -l=env=dev
---
5. Get the pods with label env=dev and also output the labels
---
    kubectl get pods -l=env=dev --show-labels
---
6. Get the pods with label env=prod
---
    kubectl get pods -l=env=prod
---
7. Get the pods with label env=prod and also output the labels
---
    kubectl get pods -l=env=prod --show-labels
---
8. Get the pods with label env
---
    kubectl get pods -l=env
---
9. Get the pods with labels env=dev and env=prod
---
    kubectl get pods -l=env=dev -l=env=prod
---
10. Get the pods with labels env=dev and env=prod and output the labels as well
---
    kubectl get pods -l=env=dev -l=env=prod --show-labels
---
11. Change the label for one of the pod to env=uat and list all the pods to verify
---
    kubectl label pod nginx-pod-dev-1 env=uat --overwrite
    kubectl get pods --show-labels
---
12. Remove the labels for the pods that we created now and verify all the labels are removed 
---
    kubectl label pod nginx-pod-dev-1 env-
    kubectl label pod nginx-pod-dev-2 env-
    kubectl label pod nginx-pod-dev-3 env-
    kubectl label pod nginx-pod-prod-1 env-
    kubectl label pod nginx-pod-prod-2 env-
    kubectl get pods --show-labels
---
13. Let’s add the label app=nginx for all the pods and verify (using kubectl) 
---
    kubectl label pod nginx-pod-dev-1 app=nginx
    kubectl label pod nginx-pod-dev-2 app=nginx
    kubectl label pod nginx-pod-dev-3 app=nginx
    kubectl label pod nginx-pod-prod-1 app=nginx
    kubectl label pod nginx-pod-prod-2 app=nginx
    kubectl get pods --show-labels
---
14. Get all the nodes with labels (if using minikube you would get only master node)
---
    kubectl get nodes --show-labels
---
15. Label the worker node nodeName=nginxnode
---
    kubectl label nodes worker-node-01 nodeName=nginxnode
---
16. Create a Pod that will be deployed on the worker node with the label nodeName=nginxnode
---
    apiVersion: v1
    kind: Pod
    metadata:
    creationTimestamp: null
    labels:
        run: nginx
    name: nginx
    spec:
    containers:
    - image: nginx
        name: nginx
        resources: {}
    dnsPolicy: ClusterFirst
    restartPolicy: Never
    nodeSelector:
        nodeName: nginxnode
    status: {}
---
17. Verify the pod that it is scheduled with the node selector on the right node... fix it if it’s not behind scheduled.
---
    kubectl get pods -o wide
---
18. Verify the pod nginx that we just created has this label
---
    kubectl get pods -l=run=nginx
---
# PART-3 - Deployments:

1. Create a deployment called webapp with image nginx with 5 replicas a. Use the below command to create a yaml file.
kubectl create deploy webapp --image=nginx --dry-run -o yaml > webapp.yaml  ii. Edit it and add 5 replica’s
---
    kubectl create -f webapp.yaml
    kubectl scale deployment webapp --replicas=10
---
2. Get the deployment rollout status
---
    kubectl rollout status deployment webapp
---
3. Get the replicaset that created with this deployment
---
    kubectl get replicasets.apps webapp
---
4. EXPORT the yaml of the replicaset and pods of this deployment
---
    kubectl get replicasets.apps -o yaml > webapp-replicaset.yaml
---
5. Delete the deployment you just created and watch all the pods are also being deleted
---
    kubectl delete deployments.apps webapp
---
6. Create a deployment of webapp with image nginx:1.17.1 with container port 80 and verify the image version a. kubectl create deploy webapp --image=nginx:1.17.1 --dry-run -o yaml > webapp.yaml b. add the port section (80)  and create the deployment 
---
    kubectl create deploy webapp --image=nginx:1.17.1 --port=80 --dry-run=client -o yaml > webapp.yaml
---
7. Update the deployment with the image version 1.17.4 and verify
---
    kubectl set image deployment/webapp nginx=nginx:1.17.4
    kubectl rollout history deployment webapp
    kubectl rollout status deployment webapp
---
8. Check the rollout history and make sure everything is ok after the update 
---
    kubectl rollout history deployment webapp
---
9. Undo the deployment to the previous version 1.17.1 and verify Image has the previous version
---
    kubectl rollout undo deployment webapp
    kubectl describe deployments.apps webapp | grep -i image
---
10. Update the deployment with the wrong image version 1.100 and verify something is wrong with the deployment a. 
Expect: kubectl get pods (ImagePullErr) b.  Undo the deployment with the previous version and verify everything is Ok c. 
kubectl rollout history deploy webapp --revision=7 d. Check the history of the specific revision of that deployment e. 
update the deployment with the image version latest and check the history and verify nothing is going on 
---
    kubectl set image deployment/webapp nginx=nginx:1.100
    kubectl get pods
    kubectl rollout undo deployment webapp
    kubectl rollout history deploy webapp --revision=7
    kubectl set image deployment/webapp nginx=nginx
    kubectl rollout history deployment webapp
---
11. Apply the autoscaling to this deployment with minimum 10 and maximum 20 replicas and target CPU of 85% and verify hpa is created and replicas are increased to 10 from 1
---
    SKIP
---
12.
---
    SKIP
---
13. Clean the cluster by deleting deployment and hpa you just create
---
    kubectl delete deployments.apps webapp
---

14. Create a job and make it run 10 times one after one (run > exit > run >exit ..) using the following configuration:
kubectl create job hello-job --image=busybox --dry-run -o yaml -- echo "Hello I am from job" > hello-job.yaml”
a. Add to the above job completions: 10 inside the yaml
---
    apiVersion: batch/v1
    kind: Job
    metadata:
    creationTimestamp: null
    name: hello-job
    spec:
    completions: 10
    template:
        metadata:
        creationTimestamp: null
        spec:
        containers:
            - image: busybox
            name: busybox
            command: ["/bin/sh", "-c", "echo 'Hello I am from job'"]
        restartPolicy: Never
    status: {}

---

# PART-4 - CONFIGMAP:

1. Create a file called config.txt with two values key1=value1 and key2=value2 and verify the file
---
    cat >> config.txt << EOF key1=value1 key2=value2 EOF cat config.txt
---
2.  Create a configmap named keyvalcfgmap and read data from the file config.txt and verify that configmap is created correctly
---
    kubectl create configmap keyvalcfgmap --from-file config.txt
    kubectl get configmaps keyvalcfgmap -o yaml
---
    apiVersion: v1
    data:
    config.txt: "key1=value1 \nkey2=value2\n"
    kind: ConfigMap
    metadata:
    creationTimestamp: "2023-05-28T14:28:19Z"
    name: keyvalcfgmap
    namespace: default
    resourceVersion: "839148"
    uid: 8783a83a-ae18-4503-b1e1-b1424d4f26
---
3. Create an nginx pod and load environment values from the above configmap keyvalcfgmap and exec into the pod and verify the environment variables
 and delete the pod
first run this command to save the pod yml 
kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml > nginx-pod.yml 

---
    apiVersion: v1
    kind: Pod
    metadata:
    creationTimestamp: null
    labels:
        run: nginx
    name: nginx
    spec:
    containers:
    - image: nginx
        name: nginx
        env:
        - name: KEY1
            valueFrom:
            configMapKeyRef:
                name: keyvalcfgmap
                key: key1
        - name: KEY2
            valueFrom:
            configMapKeyRef:
                name: keyvalcfgmap
                key: key2
        resources: {}
    dnsPolicy: ClusterFirst
    restartPolicy: Never
    status: {}
---
