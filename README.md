# What is this

Very simple setup to get alerting on openshift worker node disk fills to slack 

## How to use

1. `oc apply -f node-disk-alert.yaml`
2. Update `alertmanager.yaml` with appropriate slack webhook
3. Patch the alertmanager secret
    ```
    oc create secret generic alertmanager-main --namespace=openshift-monitoring  \
    --from-literal=alertmanager.yaml="$(< alertmanager.yaml)"    --dry-run -oyaml \ 
    |  oc replace secret    --namespace=openshift-monitoring    --filename=-
    ```
