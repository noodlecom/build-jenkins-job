# Build jenkins job from Github Action :rocket:

This action builds a jenkins job with parameters. (Single Job)

## Inputs

### `jenkins-token`
https://www.jenkins.io/blog/2018/07/02/new-api-token-system/
**(Required)**
 
### `jenkins-url`
**i.e** https://your-jenkins-site.com
**(Required)** 

### `jenkins-user`
user owner of the token
**(Required)** 

### `jenkins-job`
Jenkins job name

**i.e** Production-deployment-pipeline
**(Required)** 

### `jenkins-wait-job`
**Not mandatory**

Wait for the job build status

**values**
```
 "wait" #Default
 "no-wait"
``` 

### `jenkins-job-params`

**Not mandatory**

Set jenkins params as JSON string:  

**i.e**
```
 "{'param1': 'value1', 'param2': 'value2'}"
``` 

### `jenkins-ssl-verify`

**Not mandatory**

Defaults to `true`. Ignores errors and warning about SSL certificates if set to `false`.
Doing so is insecure, but for self-hosted runners with self-signed certificates if may be useful.

## Outputs

###  `status/result`

* FAILURE
* SUCCESS
* ABORTED
* EXECUTED


## Example usage
```
    - name: Build single job
      uses: noodlecom/build-jenkins-job@master
      with:
        jenkins-url: ${{ secrets.JENKINS_URL }}
        jenkins-token: ${{ secrets.JENKINS_TOKEN }}
        jenkins-user: ${{ secrets.JENKINS_USER }}
        jenkins-job: ${{ secrets.JENKINS_JOB }}
        jenkins-job-params: "{'stringparam': 'stringvalue', 'booleanparam': false}"
        jenkins-wait-job: "no-wait"
        jenkins-ssl-verify: "true"
```

## Notes:
If your job needs params and you want to use the default params, you will need to set Jenkins-job-params: "{'any_param': 'any_value'}"
otherwise, you will receive a 400 Bad request error.
