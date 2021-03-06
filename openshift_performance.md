---

copyright:
  years: 2014, 2021
lastupdated: "2021-02-04"

keywords: openshift, rhoks, roks, rhos, kernel

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}



# Tuning performance
{: #kernel}

If you have specific performance optimization requirements, you can change the default settings for some cluster components in {{site.data.keyword.openshiftlong}}.
{: shortdesc}

If you choose to change the default settings, you are doing so at your own risk. You are responsible for running tests against any changed settings and for any potential disruptions caused by the changed settings in your environment.
{: important}

## Default worker node settings
{: #worker-default}

By default, your worker nodes have the operating system and compute hardware of the [worker node flavor](/docs/openshift?topic=openshift-planning_worker_nodes) that you choose when you create the worker pool.
{: shortdesc}

### Customizing the operating system
{: #worker-default-os}

The following operating systems are available for worker nodes: **RHEL 7**. Your cluster cannot mix operating systems or use different operating systems. 
{: shortdesc}

To optimize your worker nodes, consider the following information.
* **Image and version updates**: Worker node updates, such as security patches to the image or {{site.data.keyword.openshiftshort}} versions, are provided by IBM for you. However, you choose when to apply the updates to the worker nodes. For more information, see [Updating clusters, worker nodes, and cluster components](/docs/openshift?topic=openshift-update).
* **Temporary modifications**: If you log in to a pod or use some other process to modify a worker node setting, the modifications are temporary. Worker node lifecycle operations, such as autorecovery, reloading, updating, or replacing a worker node, change any modifications back to the default settings.
* **Persistent modifications**: For modifications to persist across worker node lifecycle operations, use a daemon set with an init container. For more information, see [Modifying default worker node settings to optimize performance](#worker).

   Modifications to the operating system are not supported. If you modify the default settings, you are responsible for debugging and resolving the issues that might occur.
   {: important}

### Hardware changes
{: #worker-default-hw}

To change the compute hardware, such as the CPU and memory per worker node, choose among the following options.
* [Create a worker pool](/docs/openshift?topic=openshift-add_workers). The instructions vary depending on the type of infrastructure for the cluster, such as classic, VPC, {{site.data.keyword.satelliteshort}}, or gateway clusters.
* [Update the flavor](/docs/openshift?topic=openshift-update#machine_type) in your cluster by creating a worker pool and removing the previous worker pool. 

## Modifying default worker node settings to optimize performance
{: #worker}

If you have specific performance optimization requirements, you can change the default settings for the Linux kernel `sysctl` parameters on worker nodes.
{: shortdesc}

Worker nodes are automatically provisioned with optimized kernel performance, but you can change the default settings by applying a custom [Kubernetes `DaemonSet`](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/){: external} with an [`initContainer`](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/){: external} to your cluster. The daemon set modifies the settings for all existing worker nodes and applies the settings to any new worker nodes that are provisioned in the cluster. The init container makes sure that these modifications occur before other pods are scheduled on the worker node. No pods are affected.

You must have the [**Manager** {{site.data.keyword.cloud_notm}} IAM service role](/docs/openshift?topic=openshift-users#platform) for all namespaces to run the sample privileged `initContainer`. After the containers for the deployments are initialized, the privileges are dropped.
{: note}

Before you begin: [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. Save the following daemon set in a file named `worker-node-kernel-settings.yaml`. In the `spec.template.spec.initContainers` section, add the fields and values for the `sysctl` parameters that you want to tune. This example daemon set changes the default maximum number of connections that are allowed in the environment via the `net.core.somaxconn` setting and the ephemeral port range via the `net.ipv4.ip_local_port_range` setting.

    Depending on the `systctl` settings that you try to change, you might want to configure the security context. For more information, see the [{{site.data.keyword.openshiftshort}} documentation](https://docs.openshift.com/container-platform/4.5/nodes/containers/nodes-containers-sysctls.html){: external}.
    {: note}
    
    ```yaml
    apiVersion: apps/v1
    kind: DaemonSet
    metadata:
      name: kernel-optimization
      namespace: kube-system
      labels:
        tier: management
        app: kernel-optimization
    spec:
      selector:
        matchLabels:
          name: kernel-optimization
      template:
        metadata:
          labels:
            name: kernel-optimization
        spec:
          hostNetwork: true
          hostPID: true
          hostIPC: true
          initContainers:
            - command:
                - sh
                - -c
                - sysctl -w net.ipv4.ip_local_port_range="1025 65535"; sysctl -w net.core.somaxconn=32768;
              image: alpine:3.6
              imagePullPolicy: IfNotPresent
              name: sysctl
              resources: {}
              securityContext:
                privileged: true
                capabilities:
                  add:
                    - NET_ADMIN
              volumeMounts:
                - name: modifysys
                  mountPath: /sys
          containers:
            - resources:
                requests:
                  cpu: 0.01
              image: alpine:3.6
              name: sleepforever
              command: ["/bin/sh", "-c"]
              args:
                - >
                  while true; do
                    sleep 100000;
                  done
          volumes:
            - name: modifysys
              hostPath:
                path: /sys
    ```
    {: codeblock}

2. Apply the daemon set to your worker nodes. The changes are applied immediately.
    ```
    oc apply -f worker-node-kernel-settings.yaml
    ```
    {: pre}

<br />
To revert your worker nodes' `sysctl` parameters to the default values set by {{site.data.keyword.containerlong_notm}}:

1. Delete the daemon set. The `initContainers` that applied the custom settings are removed.
    ```
    oc delete ds kernel-optimization
    ```
    {: pre}

2. [Reboot all worker nodes in the cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot). The worker nodes come back online with the default values applied.

<br />



## Changing the Calico maximum transmission unit (MTU)
{: #calico-mtu}

Increase or decrease the Calico plug-in maximum transmission unit (MTU) to meet the network throughput requirements of your environment.
{: shortdesc}

By default, the Calico network plug-in in your {{site.data.keyword.openshiftlong_notm}} cluster has an MTU of 1480 bytes. For most cases, this default MTU value provides sufficient throughput for packets that are sent and received in your network workloads. Review the following cases in which you might need to modify the default Calico MTU:

* If your cluster uses bare metal worker nodes, and you use jumbo frames on the bare metal worker nodes, the jumbo frames have an MTU value in the range of 1500 to 9000. To ensure that Calico can handle this throughput, you can increase the Calico MTU to match the MTU of the jumbo frames. Note that all worker nodes in the cluster must use the same Calico MTU, so to increase the Calico MTU, all worker nodes in the cluster must be bare metal and use jumbo frames.
* If you have a VPN connection set up for your cluster, some VPN connections require a smaller Calico MTU than the default. Check with the VPN service to determine whether a smaller Calico MTU is required. 
    
To run your {{site.data.keyword.openshiftshort}} cluster, make sure that the MTU is equal to or greater than 1450 bytes. 
{: important} 

You can change the MTU on the tunnel interface `tunl0`, which is used for pod to pod communication, and the MTU on the `caliXXXXXXXX` `veth` interface of each worker node.



### Changing the Calico MTU for version 4 clusters
{: #calico-mtu-43}

Increase the Calico plug-in MTU to meet the network throughput requirements of your environment in an {{site.data.keyword.openshiftshort}} version 4 cluster.
{: shortdesc}

1. Edit the `default` Calico installation resource.
  ```
  oc edit installation default -n calico-system
  ```
  {: pre}

2. In the `spec.calicoNetwork` section, change the value of the `mtu` field.
   ```yaml
   ...
   spec:
     calicoNetwork:
       ipPools:
       - cidr: 172.30.0.0/16
         encapsulation: IPIPCrossSubnet
         natOutgoing: Enabled
         nodeSelector: all()
       mtu: 1500
       nodeAddressAutodetectionV4:
         interface: (^bond0$|^eth0$|^ens6$|^ens3$)
     kubernetesProvider: OpenShift
     registry: registry.ng.bluemix.net/armada-master/
     variant: Calico
   status:
     variant: Calico
   ```
   {: screen}
    
   To run your {{site.data.keyword.openshiftshort}} cluster, make sure that the MTU is equal to or greater than 1450 bytes. 
   {: important}

3. Save and close the file.

4. Apply the MTU changes to your worker nodes by [rebooting all worker nodes in your cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot).

### Changing the Calico MTU for 3.11 clusters
{: #calico-mtu-311}

Increase the Calico plug-in MTU to meet the network throughput requirements of your environment in an {{site.data.keyword.openshiftshort}} version 3.11 cluster.
{: shortdesc}


1. Edit the `calico-config` configmap resource.
  ```
  oc edit cm calico-config -n kube-system
  ```
  {: pre}

2. In the `data` section, add a `calico_mtu_override: "<new_MTU>"` field and specify the new MTU value for Calico. Note that the quotation marks (`"`) around the new MTU value are required.

    Do not change the values of `mtu` or `veth_mtu`.
    {: important}

    ```yaml
    apiVersion: v1
    data:
      calico_backend: bird
      calico_mtu_override: "1600"
      cni_network_config: |-
        {
          "name": "k8s-pod-network",
          "cniVersion": "0.3.1",
          "plugins": [
            {
              "type": "calico",
              "log_level": "info",
              "etcd_endpoints": "__ETCD_ENDPOINTS__",
              "etcd_key_file": "__ETCD_KEY_FILE__",
              "etcd_cert_file": "__ETCD_CERT_FILE__",
              "etcd_ca_cert_file": "__ETCD_CA_CERT_FILE__",
              "mtu": __CNI_MTU__,
              "ipam": {
                  "type": "calico-ipam"
              },
              "container_settings": {
                  "allow_ip_forwarding": true
              },
              "policy": {
                  "type": "k8s"
              },
              "kubernetes": {
                  "kubeconfig": "__KUBECONFIG_FILEPATH__"
              }
            },
            {
              "type": "portmap",
              "snat": true,
              "capabilities": {"portMappings": true}
            }
          ]
        }
      etcd_ca: /calico-secrets/etcd-ca
      etcd_cert: /calico-secrets/etcd-cert
      etcd_endpoints: https://172.20.0.1:2041
      etcd_key: /calico-secrets/etcd-key
      typha_service_name: none
      veth_mtu: "1480"
    kind: ConfigMap
    ...
    ```
    {: codeblock}
    
    To run your {{site.data.keyword.openshiftshort}} cluster, make sure that the MTU is equal to or greater than 1450 bytes.
    {: important} 
    
3. Apply the MTU changes to your cluster master by refreshing the master API server. It might take several minutes for the master to refresh.
  ```
  ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
  ```
  {: pre}

4. Verify that the master refresh is completed. When the refresh is complete, the **Master Status** changes to `Ready`.
  ```
  ibmcloud oc cluster get --cluster <cluster_name_or_ID>
  ```
  {: pre}

5. In the `data` section of the output, verify that the `veth_mtu` field shows the new MTU value for Calico that you specified in step 2.
  ```
  oc get cm -n kube-system calico-config -o yaml
  ```
  {: pre}

  Example output:
  ```yaml
  apiVersion: v1
  data:
    ...
    etcd_ca: /calico-secrets/etcd-ca
    etcd_cert: /calico-secrets/etcd-cert
    etcd_endpoints: https://172.20.0.1:2041
    etcd_key: /calico-secrets/etcd-key
    typha_service_name: none
    veth_mtu: "1600"
  kind: ConfigMap
  ...
  ```
  {: screen}

6. Apply the MTU changes to your worker nodes by [rebooting all worker nodes in your cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot).

<br />

## Disabling the port map plug-in
{: #calico-portmap}

The `portmap` plug-in for the Calico container network interface (CNI) enables you to use a `hostPort` to expose your app pods on a specific port on the worker node. Prevent iptables performance issues by removing the port map plug-in from your cluster's Calico CNI configuration.
{: shortdesc}

When you have a large number of services in your cluster, such as more than 500 services, or a large number of ports on services, such as more than 50 ports per service for 10 or more services, a large number of iptables rules are generated for the Calico and Kubernetes network policies for these services. A large number of iptables rules can lead to performance issues for the port map plug-in, and might prevent future updates of iptables rules or cause the `calico-node` container to restart when no lock is received to make iptables rules updates within a specified time. To prevent these performance issues, you can disable the port map plug-in by removing it from your cluster's Calico CNI configuration.

If you must use `hostPorts`, do not disable the port map plug-in.
{: note}

### Disabling the port map plug-in for version 4 clusters
{: #calico-portmap-43}

Disable the port map plug-in by disabling `hostPorts` for Calico in an {{site.data.keyword.openshiftshort}} version 4 cluster.
{: shortdesc}

1. Edit the `default` Calico installation resource.
  ```
  oc edit installation default -n calico-system
  ```
  {: pre}

2. In the `spec.calicoNetwork` section, change the value of `hostPorts` to `Disabled`.
   ```yaml
   ...
   spec:
     calicoNetwork:
       hostPorts: Disabled
       ipPools:
       - cidr: 172.30.0.0/16
         encapsulation: IPIPCrossSubnet
         natOutgoing: Enabled
         nodeSelector: all()
       mtu: 1480
       nodeAddressAutodetectionV4:
         interface: (^bond0$|^eth0$|^ens6$|^ens3$)
     kubernetesProvider: OpenShift
     registry: registry.ng.bluemix.net/armada-master/
     variant: Calico
   status:
     variant: Calico
   ```
   {: screen}

3. Save and close the file. Your changes are automatically applied.

### Disabling the port map plug-in for 3.11 clusters
{: #calico-portmap-311}

Disable the port map plug-in by disabling `hostPorts` for Calico in an {{site.data.keyword.openshiftshort}} version 3.11 cluster.
{: shortdesc}


1. Edit the `calico-config` configmap resource.
  ```
  oc edit cm calico-config -n kube-system
  ```
  {: pre}

2. In the `data.cni_network_config.plugins` section after the `kubernetes` plug-in, remove the `portmap` plug-in section. After you remove the `portmap` section, the configuration looks like the following:
  ```yaml
  apiVersion: v1
  data:
    calico_backend: bird
    cni_network_config: |-
      {
        "name": "k8s-pod-network",
        "cniVersion": "0.3.1",
        "plugins": [
          {
            "type": "calico",
            "log_level": "info",
            "etcd_endpoints": "__ETCD_ENDPOINTS__",
            "etcd_key_file": "__ETCD_KEY_FILE__",
            "etcd_cert_file": "__ETCD_CERT_FILE__",
            "etcd_ca_cert_file": "__ETCD_CA_CERT_FILE__",
            "mtu": __CNI_MTU__,
            "ipam": {
                "type": "calico-ipam"
            },
            "container_settings": {
                "allow_ip_forwarding": true
            },
            "policy": {
                "type": "k8s"
            },
            "kubernetes": {
                "kubeconfig": "__KUBECONFIG_FILEPATH__"
            }
          }
        ]
      }
    etcd_ca: /calico-secrets/etcd-ca
    ...
  ```
  {: codeblock}

3. Apply the change to your cluster by restarting all `calico-node` pods.
    1. Get the names of the `calico-node` pods in your cluster.
      ```
      oc get pods -n kube-system | grep calico-node
      ```
      {: pre}
    2. Restart all `calico-node` pods by manually deleting them. Separate each pod name with one space.
      ```
      oc delete pods -n kube-system <pod1> <pod2> ...
      ```
      {: pre}
