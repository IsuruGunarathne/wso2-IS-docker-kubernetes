### add kubernetest membership scheme

get the source code for the kubernetes member ship scheme from the link bellow and build it
https://github.com/wso2/kubernetes-common/tags

build the kubernetes membership scheme and copy the jar file to the dropins folder of the carbon server<br>
run `mvn clean package` from within the kubernetes-membership-scheme directory<br>
if you have a java version that is not java8
use `JAVA_HOME=/path/to/jdk17/ mvn clean package`<br>
eg `JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64 mvn clean package`<br>

copy the jar file from the target directory to the dropins directory at `<IS_HOME>/repository/components/dropins/`<br>

### Update the deployment.yaml file

Add the following to the deployment.yaml file

[clustering]
membership_scheme = "kubernetes"
local_member_host = "172.17.0.2"
local_member_port = "4000"

[clustering.properties]
membershipSchemeClassName = "org.wso2.carbon.membership.scheme.kubernetes.KubernetesMembershipScheme"
KUBERNETES_NAMESPACE = "wso2"
KUBERNETES_SERVICES = "is-service"
KUBERNETES_MASTER_SKIP_SSL_VERIFICATION = true
USE_DNS = false

### Namespace and service accounts

create a namespace for the deployment
`kubectl create namespace wso2` OR `kubectl create -f namespace.yaml` namespace.yaml file is in the service-account directory<br>
use `kubectl get namespaces` to view all namespaces<br>
use `kubectl delete namespace wso2` to delete the namespace<br>

### caching

add the following to the deployment.yaml file

```
[server]
force_local_cache = true
```

### load balancer

add the following to the deployment.yaml file

```
[transport.http.properties]
proxyPort = 80
[transport.https.properties]
proxyPort = 443
```

### change host name (optional)

add the following to the deployment.yaml file

```
[server]
hostname = "wso2.is"
```

Note : for this to take effect the ip of the cluster should be added to the /etc/hosts file of the host machine
