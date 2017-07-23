#!/bin/sh

# Update configmap script

NAMESPACE=${NAMESPACE:-default}
KUBECTL="kubectl ${KUBECTL_PARAMS} --namespace=\"${NAMESPACE}\""

eval "${KUBECTL} replace -f fluentd-config-map.yml" &
echo "Waiting for configmap volume to be updated..."
eval "${KUBECTL} exec $(eval "${KUBECTL} get pods -l app=fluentd -o jsonpath={.items..metadata.name}") -- sh -c 'A=\`stat -Lc %Z /etc/fluent/..data\`; while true; do B=\`stat -Lc %Z /etc/fluent/..data\`; [ \$A != \$B ] && break || printf . && sleep 0.5; done; killall -HUP fluentd'"
echo "Updated"
