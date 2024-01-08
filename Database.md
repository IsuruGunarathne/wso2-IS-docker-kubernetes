get the source code for the kubernetes member ship scheme from the link bellow and build it
https://github.com/wso2/kubernetes-common/tags

build the kubernetes membership scheme and copy the jar file to the dropins folder of the carbon server<br>
run `mvn clean package` from within the kubernetes-membership-scheme directory<br>
if you have a java version that is not java8
use `JAVA_HOME=/path/to/jdk17/ mvn clean package`<br>
eg `JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64 mvn clean package`<br>

copy the jar file from the target directory to the dropins directory at `<IS_HOME>/repository/components/dropins/`<br>
