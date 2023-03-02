# uos openjdk1.8

## install
- yum install java-1.8.0-openjdk
- which java
- java -version
- javac
- yum install java-1.8.0-openjdk-devel.x86_64

## config
- vi /etc/profile
`
#java environment
JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.191.b12-1.el7_6.x86_64
JRE_HOME=$JAVA_HOME/jre
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH
`
- source /etc/profile