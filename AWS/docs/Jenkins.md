To check the status of Jenkins from a script or the command line, you can use one of the following methods:

### 1. **Using systemctl (Linux)**
```sh
sudo systemctl status jenkins
```

### 2. **Using Jenkins REST API**
You can check Jenkins status with a simple HTTP request:
```sh
curl -s http://<jenkins-server>:8080/api/json | jq '.mode, .quietingDown, .useCrumbs'
```
Or just check if Jenkins is up:
```sh
curl -I http://<jenkins-server>:8080
```
A `200 OK` response means Jenkins is running.

### 3. **From a Jenkins Pipeline**
You can add a stage to your Jenkinsfile to check Jenkins status:
````groovy
stage('Check Jenkins Status') {
    steps {
        sh 'curl -I http://localhost:8080'
    }
}
````

Let me know if you want to automate this check in your Node.js or Groovy code!
