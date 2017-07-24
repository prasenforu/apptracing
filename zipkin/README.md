Installation:

1. First PV & PVC need to create.

oc create -f zipkin-mysql-pvc-openshift-final.yml

2. Then start zipkin & zipkin-mysql service, deployment & router for zipkin

oc create -f zipkin-openshift-final.yml

-----------

YML repo folder

http://repo1.maven.org/maven2/io/fabric8/zipkin/
