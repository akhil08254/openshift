---

copyright:
  years: 2014, 2021
lastupdated: "2021-02-04"

keywords: kubernetes, openshift, roks, rhoks, rhos

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



# Deploying apps in OpenShift clusters
{: #deploy_app}

With {{site.data.keyword.openshiftlong}} clusters, you can deploy apps from a remote file or repository such as GitHub with a single command. Also, your clusters come with various built-in services that you can use to help operate your cluster.
{: shortdesc}

## Moving your apps to {{site.data.keyword.openshiftshort}}
{: #openshift_move_apps}

To create an app in your {{site.data.keyword.openshiftlong_notm}} cluster, you can use the {{site.data.keyword.openshiftshort}} console or CLI.
{: shortdesc}

Seeing errors when you deploy your app? {{site.data.keyword.openshiftshort}} has different default settings than community Kubernetes, such as stricter security context constraints. Review the [common scenarios where you might need to modify your apps](/docs/openshift?topic=openshift-plan_deploy#openshift_move_apps_scenarios) so that you can deploy them on {{site.data.keyword.openshiftshort}} clusters.
{: tip}

### Deploying apps through the console
{: #deploy_apps_ui}

You can create apps through various methods in the {{site.data.keyword.openshiftshort}} console by using the **Developer** perspective. For more information, see the [{{site.data.keyword.openshiftshort}} documentation](http://docs.openshift.com/container-platform/4.5/applications/application_life_cycle_management/odc-creating-applications-using-developer-perspective.html){: external}.
{: shortdesc}

1.  From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select your cluster.
2.  Click **{{site.data.keyword.openshiftshort}} web console**.
3.  From the perspective switcher, select **Developer**. The {{site.data.keyword.openshiftshort}} web console switches to the Developer perspective, and the menu now offers items such as **+Add**, **Topology**, and **Builds**.
4.  Click **+Add**.
5.  In the **Add** pane menu bar, select the **Project** that you want to create your app in from the drop-down list.
6.  Click the method that you want to use to add your app, and follow the instructions. For example, click **From Git**.

### Deploying apps through the CLI
{: #deploy_apps_cli}

To create an app in your {{site.data.keyword.openshiftlong_notm}} cluster, use the `oc new-app` [command](https://docs.openshift.com/container-platform/4.5/cli_reference/openshift_cli/developer-cli-commands.html#new-app){: external}. For example, you might refer to a public GitHub repo, a public GitLab repo with a URL that ends in `.git`, or another local or remote repo. For more information, [try out the tutorial](/docs/openshift?topic=openshift-openshift_tutorial#openshift_deploy_app) and review the [{{site.data.keyword.openshiftshort}} documentation](http://docs.openshift.com/container-platform/4.5/applications/application_life_cycle_management/creating-applications-using-cli.html){: external}.
{: shortdesc}

```
oc new-app --name <app_name> https://github.com/<path_to_app_repo> [--context-dir=<subdirectory>]
```
{: pre}

**What does the `new-app` command do?**

The `new-app` command creates a build configuration and app image from the source code, a deployment configuration to deploy the container to pods in your cluster, and a service to expose the app within the cluster. For more information about the build process and other sources besides Git, see the [{{site.data.keyword.openshiftshort}} documentation](http://docs.openshift.com/container-platform/4.5/applications/application_life_cycle_management/creating-applications-using-cli.html){: external}.

<br />

## Deploying apps to specific worker nodes by using labels
{: #node_affinity}

When you deploy an app, the app pods indiscriminately deploy to various worker nodes in your cluster. In some cases, you might want to restrict the worker nodes that the app pods to deploy to. For example, you might want app pods to deploy to only worker nodes in a certain worker pool because those worker nodes are on bare metal machines. To designate the worker nodes that app pods must deploy to, add an affinity rule to your app deployment.
{: shortdesc}

Before you begin:
*   [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
*   Make sure that you are assigned a [service role](/docs/openshift?topic=openshift-users#platform) that grants the appropriate Kubernetes RBAC role so that you can work with Kubernetes resources in the {{site.data.keyword.openshiftshort}} project.
*  **Optional**: [Set a label for the worker pool](/docs/openshift?topic=openshift-add_workers#worker_pool_labels) that you want to run the app on.

To deploy apps to specific worker nodes:

1.  Get the ID of the worker pool that you want to deploy app pods to.
    ```
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

2.  List the worker nodes that are in the worker pool, and note one of the **Private IP** addresses.
    ```
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
    ```
    {: pre}

3.  Describe the worker node. In the **Labels** output, note the worker pool ID label, `ibm-cloud.kubernetes.io/worker-pool-id`.

    <p class="tip">The steps in this topic use a worker pool ID to deploy app pods only to worker nodes within that worker pool. To deploy app pods to specific worker nodes by using a different label, note this label instead. For example, to deploy app pods only to worker nodes on a specific private VLAN, use the `privateVLAN=` label.</p>

    ```
    oc describe node <worker_node_private_IP>
    ```
    {: pre}

    Example output:
    ```
    Name:               10.xxx.xx.xxx
    Roles:              <none>
    Labels:             arch=amd64
                        beta.kubernetes.io/arch=amd64
                        beta.kubernetes.io/instance-type=b3c.4x16.encrypted
                        beta.kubernetes.io/os=linux
                        failure-domain.beta.kubernetes.io/region=us-south
                        failure-domain.beta.kubernetes.io/zone=dal10
                        ibm-cloud.kubernetes.io/encrypted-docker-data=true
                        ibm-cloud.kubernetes.io/ha-worker=true
                        ibm-cloud.kubernetes.io/iaas-provider=softlayer
                        ibm-cloud.kubernetes.io/machine-type=b3c.4x16.encrypted
                        ibm-cloud.kubernetes.io/sgx-enabled=false
                        ibm-cloud.kubernetes.io/worker-pool-id=00a11aa1a11aa11a1111a1111aaa11aa-11a11a
                        ibm-cloud.kubernetes.io/worker-version=1.18.15_1534
                        kubernetes.io/hostname=10.xxx.xx.xxx
                        privateVLAN=1234567
                        publicVLAN=7654321
    Annotations:        node.alpha.kubernetes.io/ttl=0
    ...
    ```
    {: screen}

4. [Add an affinity rule](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/){: external} for the worker pool ID label to the app deployment.

    Example YAML:

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: with-node-affinity
    spec:
      template:
        spec:
          affinity:
            nodeAffinity:
              requiredDuringSchedulingIgnoredDuringExecution:
                nodeSelectorTerms:
                - matchExpressions:
                  - key: ibm-cloud.kubernetes.io/worker-pool-id
                    operator: In
                    values:
                    - <worker_pool_ID>
    ...
    ```
    {: codeblock}

    In the **affinity** section of the example YAML, `ibm-cloud.kubernetes.io/worker-pool-id` is the `key` and `<worker_pool_ID>` is the `value`.

5. Apply the updated deployment configuration file.
    ```
    oc apply -f with-node-affinity.yaml
    ```
    {: pre}

6. Verify that the app pods deployed to the correct worker nodes.

    1. List the pods in your cluster.
        ```
        oc get pods -o wide
        ```
        {: pre}

        Example output:
        ```
        NAME                   READY     STATUS              RESTARTS   AGE       IP               NODE
        cf-py-d7b7d94db-vp8pq  1/1       Running             0          15d       172.30.xxx.xxx   10.176.48.78
        ```
        {: screen}

    2. In the output, identify a pod for your app. Note the **NODE** private IP address of the worker node that the pod is on.

        In the previous example output, the app pod `cf-py-d7b7d94db-vp8pq` is on a worker node with the IP address `10.xxx.xx.xxx`.

    3. List the worker nodes in the worker pool that you designated in your app deployment.

        ```
        ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name_or_ID>
        ```
        {: pre}

        Example output:

        ```
        ID                                                 Public IP       Private IP     Machine Type      State    Status  Zone    Version
        kube-dal10-crb20b637238bb471f8b4b8b881bbb4962-w7   169.xx.xxx.xxx  10.176.48.78   b3c.4x16          normal   Ready   dal10   1.8.6_1504
        kube-dal10-crb20b637238bb471f8b4b8b881bbb4962-w8   169.xx.xxx.xxx  10.176.48.83   b3c.4x16          normal   Ready   dal10   1.8.6_1504
        kube-dal12-crb20b637238bb471f8b4b8b881bbb4962-w9   169.xx.xxx.xxx  10.176.48.69   b3c.4x16          normal   Ready   dal12   1.8.6_1504
        ```
        {: screen}

        If you created an app affinity rule based on another factor, get that value instead. For example, to verify that the app pod deployed to a worker node on a specific VLAN, view the VLAN that the worker node is on by running `ibmcloud oc worker get --cluster <cluster_name_or_ID> --worker <worker_ID>`.
        {: tip}

    4. In the output, verify that the worker node with the private IP address that you identified in the previous step is deployed in this worker pool.

<br />



## Deploying an app on a GPU machine
{: #gpu_app}

If you have a [bare metal graphics processing unit (GPU) machine type](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes), you can schedule mathematically intensive workloads onto the worker node. For example, you might run a 3D app that uses the Compute Unified Device Architecture (CUDA) platform to share the processing load across the GPU and CPU to increase performance.
{: shortdesc}

In the following steps, you learn how to deploy workloads that require the GPU. You can also deploy apps that don't need to process their workloads across both the GPU and CPU. After, you might find it useful to play around with mathematically intensive workloads such as the [TensorFlow](https://www.tensorflow.org/){: external} machine learning framework with [this Kubernetes demo](https://github.com/pachyderm/pachyderm/tree/master/examples/ml/tensorflow){: external}.

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> GPU machines are available only for clusters that run {{site.data.keyword.openshiftshort}} version 4 on classic infrastructure.
{: note}

Before you begin:
* Create a [cluster](/docs/openshift?topic=openshift-clusters#clusters_standard) or [worker pool](/docs/openshift?topic=openshift-add_workers#add_pool) that uses a GPU bare metal flavor. Keep in mind that setting up a bare metal machine can take more than one business day to complete.
* Make sure that you are assigned a [service role](/docs/openshift?topic=openshift-users#platform) that grants the appropriate Kubernetes RBAC role so that you can work with Kubernetes resources in the cluster.
* [Install the Node Feature Discovery and NVIDIA GPU operators for you cluster version](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/getting-started.html){: external}.
  
  You must use NVIDIA GPU operator version 1.3.1 or later. When you install the Node Feature Discovery operator, select the update channel that matches your {{site.data.keyword.openshiftshort}} cluster version. Do not install the operators through another method, such as a Helm chart.
  {: important}

To execute a workload on a GPU machine:
1.  Create a YAML file. In this example, a `Job` YAML manages batch-like workloads by making a short-lived pod that runs until the command that it is scheduled to complete successfully terminates.

    For GPU workloads, you must always provide the `resources: limits: nvidia.com/gpu` field in the YAML specification.
    {: note}

    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
      name: nvidia-smi
      labels:
        name: nvidia-smi
    spec:
      template:
        metadata:
          labels:
            name: nvidia-smi
        spec:
          containers:
          - name: nvidia-smi
            image: nvidia/cuda:9.1-base-ubuntu16.04
            command: [ "/usr/test/nvidia-smi" ]
            imagePullPolicy: IfNotPresent
            resources:
              limits:
                nvidia.com/gpu: 2
            volumeMounts:
            - mountPath: /usr/test
              name: nvidia0
          volumes:
            - name: nvidia0
              hostPath:
                path: /usr/bin
          restartPolicy: Never
    ```
    {: codeblock}

    <table summary="A table that describes in Column 1 the YAML file fields and in Column 2 how to fill out those fields.">
    <caption>YAML components</caption>
    <thead>
    <col width="25%">
    <th>Component</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td>Metadata and label names</td>
    <td>Give a name and a label for the job, and use the same name in both the file's metadata and the `spec template` metadata. For example, `nvidia-smi`.</td>
    </tr>
    <tr>
    <td><code>containers.image</code></td>
    <td>Provide the image that the container is a running instance of. In this example, the value is set to use the DockerHub CUDA image:<code>nvidia/cuda:9.1-base-ubuntu16.04</code></td>
    </tr>
    <tr>
    <td><code>containers.command</code></td>
    <td>Specify a command to run in the container. In this example, the <code>[ "/usr/test/nvidia-smi" ]</code>command refers to a binary file that is on the GPU machine, so you must also set up a volume mount.</td>
    </tr>
    <tr>
    <td><code>containers.imagePullPolicy</code></td>
    <td>To pull a new image only if the image is not currently on the worker node, specify <code>IfNotPresent</code>.</td>
    </tr>
    <tr>
    <td><code>resources.limits</code></td>
    <td>For GPU machines, you must specify the resource limit. The Kubernetes [Device Plug-in ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/device-plugins/) sets the default resource request to match the limit.
    <ul><li>You must specify the key as <code>nvidia.com/gpu</code>.</li>
    <li>Enter the whole number of GPUs that you request, such as <code>2</code>. <strong>Note</strong>: Container pods do not share GPUs and GPUs cannot be overcommitted. For example, if you have only 1 `mg1c.16x128` machine, then you have only 2 GPUs in that machine and can specify a maximum of `2`.</li></ul></td>
    </tr>
    <tr>
    <td><code>volumeMounts</code></td>
    <td>Name the volume that is mounted onto the container, such as <code>nvidia0</code>. Specify the <code>mountPath</code> on the container for the volume. In this example, the path <code>/usr/test</code> matches the path that is used in the job container command.</td>
    </tr>
    <tr>
    <td><code>volumes</code></td>
    <td>Name the job volume, such as <code>nvidia0</code>. In the GPU worker node's <code>hostPath</code>, specify the volume's <code>path</code> on the host, in this example, <code>/usr/bin</code>. The container <code>mountPath</code> is mapped to the host volume <code>path</code>, which gives this job access to the NVIDIA binaries on the GPU worker node for the container command to run.</td>
    </tr>
    </tbody></table>

2.  Apply the YAML file. For example:

    ```
    oc apply -f nvidia-smi.yaml
    ```
    {: pre}

3.  Check the job pod by filtering your pods by the `nvidia-sim` label. Verify that the **STATUS** is **Completed**.

    ```
    oc get pod -a -l 'name in (nvidia-sim)'
    ```
    {: pre}

    Example output:
    ```
    NAME                  READY     STATUS      RESTARTS   AGE
    nvidia-smi-ppkd4      0/1       Completed   0          36s
    ```
    {: screen}

4.  Describe the pod to see how the GPU device plug-in scheduled the pod.
    * In the `Limits` and `Requests` fields, see that the resource limit that you specified matches the request that the device plug-in automatically set.
    * In the events, verify that the pod is assigned to your GPU worker node.

    ```
    oc describe pod nvidia-smi-ppkd4
    ```
    {: pre}

    Example output:
    ```
    Name:           nvidia-smi-ppkd4
    Namespace:      default
    ...
    Limits:
     nvidia.com/gpu:  2
    Requests:
     nvidia.com/gpu:  2
    ...
    Events:
    Type    Reason                 Age   From                     Message
    ----    ------                 ----  ----                     -------
    Normal  Scheduled              1m    default-scheduler        Successfully assigned nvidia-smi-ppkd4 to 10.xxx.xx.xxx
    ...
    ```
    {: screen}

5.  To verify that the job used the GPU to compute its workload, you can check the logs. The `[ "/usr/test/nvidia-smi" ]` command from the job queried the GPU device state on the GPU worker node.

    ```
    oc logs nvidia-sim-ppkd4
    ```
    {: pre}

    Example output:
    ```
    +-----------------------------------------------------------------------------+
    | NVIDIA-SMI 390.12                 Driver Version: 390.12                    |
    |-------------------------------+----------------------+----------------------+
    | GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
    | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
    |===============================+======================+======================|
    |   0  Tesla K80           Off  | 00000000:83:00.0 Off |                  Off |
    | N/A   37C    P0    57W / 149W |      0MiB / 12206MiB |      0%      Default |
    +-------------------------------+----------------------+----------------------+
    |   1  Tesla K80           Off  | 00000000:84:00.0 Off |                  Off |
    | N/A   32C    P0    63W / 149W |      0MiB / 12206MiB |      1%      Default |
    +-------------------------------+----------------------+----------------------+

    +-----------------------------------------------------------------------------+
    | Processes:                                                       GPU Memory |
    |  GPU       PID   Type   Process name                             Usage      |
    |=============================================================================|
    |  No running processes found                                                 |
    +-----------------------------------------------------------------------------+
    ```
    {: screen}

    In this example, you see that both GPUs were used to execute the job because both the GPUs were scheduled in the worker node. If the limit is set to 1, only 1 GPU is shown.

Now that you deployed a test GPU workload, you might want to set up your cluster to run a tool that relies on GPU processing, such as [IBM Maximo Visual Inspection](https://www.ibm.com/products/ibm-maximo-visual-inspection){: external}.



<br />

## Deploying Cloud Paks, licensed software, and other integrations
{: #openshift_app_cloud_paks}

You can deploy IBM Cloud Paks&trade;, licensed software, and other 3rd party integrations to {{site.data.keyword.openshiftlong_notm}} clusters. You have various tools to deploy integrations, such as {{site.data.keyword.cloud_notm}} service binding, managed add-ons, Helm charts, and more. After you install an integration, follow that product's documentation for configuration settings and other instructions to integrate with your apps. For more information, see [Enhancing cluster capabilities with integrations](/docs/openshift?topic=openshift-supported_integrations).
{: shortdesc}

<br />

## Accessing the {{site.data.keyword.openshiftshort}} web console
{: #openshift_console}

You can use the {{site.data.keyword.openshiftshort}} console to manage your apps, deploy apps from the catalog, and access built-in functionality to help you operate your cluster. The {{site.data.keyword.openshiftshort}} console is deployed to your cluster by default, instead of the Kubernetes dashboard as in community Kubernetes clusters.
{: shortdesc}

For more information about the console, see the [{{site.data.keyword.openshiftshort}} documentation](http://docs.openshift.com/container-platform/4.5/applications/application_life_cycle_management/odc-creating-applications-using-developer-perspective.html){: external}.

1.  From the [{{site.data.keyword.openshiftlong_notm}} console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select your {{site.data.keyword.openshiftshort}} cluster, then click **OpenShift web console**.
2.  Explore the different areas of the {{site.data.keyword.openshiftshort}} web console, as described in the following tabbed table.

    <table class="simple-tab-table" id="console1" tab-title="OCP 4" tab-group="console-version" aria-describedby="tableSummary-19ecbef4c01853826b42de82471b9035">
    <caption caption-side="top">
      <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> {{site.data.keyword.openshiftshort}} console overview<br>
      <span class="table-summary" id="tableSummary-19ecbef4c01853826b42de82471b9035">The rows are read from left to right. The area of the console is in the first column, the location in the console is in the second column, and the description of the console area in the third column. You can change between {{site.data.keyword.openshiftshort}} console versions by toggling the tabs at the beginning of the table.</span>
    </caption>
    <thead>
    <tr>
    <th>Area</th>
    <th>Location in console</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td>Administrator perspective</td>
    <td>Side navigation menu perspective switcher.</td>
    <td>From the Administrator perspective, you can manage and set up the components that your team needs to run your apps, such as projects for your workloads, networking, and operators for integrating IBM, Red Hat, 3rd party, and custom services into the cluster. For more information, see [Viewing cluster information](http://docs.openshift.com/container-platform/4.5/web_console/using-dashboard-to-get-cluster-information.html){: external} in the {{site.data.keyword.openshiftshort}} documentation.</td>
    </tr>
    <tr>
    <td>Developer perspective</td>
    <td>Side navigation menu perspective switcher.</td>
    <td>From the Developer perspective, you can add apps to your cluster in a variety of ways, such as from Git repositories,container images, drag-and-drop or uploaded YAML files, operator catalogs, and more. The **Topology** view presents a unique way to visualize the workloads that run in a project and navigate their components from sidebars that aggregate related resources, including pods, services, routes, and metadata. For more information, see [Developer perspective](http://docs.openshift.com/container-platform/4.5/web_console/odc-about-developer-perspective.html){: external} in the {{site.data.keyword.openshiftshort}} documentation.</td>
    </tr>
    </tbody>
    </table>
    <table class="simple-tab-table" id="console2" tab-title="OCP 3" tab-group="console-version" aria-describedby="tableSummary-a4edc48da30a2a6943cabb6b3a128df4">
    <caption caption-side="top">
      <img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> {{site.data.keyword.openshiftshort}} console overview<br>
      <span class="table-summary" id="tableSummary-a4edc48da30a2a6943cabb6b3a128df4">The rows are read from left to right. The area of the console is in the first column, the location in the console is in the second column, and the description of the console area in the third column. You can change between {{site.data.keyword.openshiftshort}} console versions by toggling the tabs at the beginning of the table.</span>
    </caption>
    <thead>
    <tr>
    <th>Area</th>
    <th>Location in console</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td>Service Catalog</td>
    <td>Dropdown menu in the **OpenShift Container Platform** menu bar.</td>
    <td>Browse the catalog of built-in services that you can deploy on {{site.data.keyword.openshiftshort}}. For example, if you already have a `node.js` app that is hosted on GitHub, you can click the **Languages** tab and deploy a **JavaScript** app. The **My Projects** pane provides a quick view of all the projects that you have access to, and clicking on a project takes you to the Application Console. For more information, see the [{{site.data.keyword.openshiftshort}} Web Console Walkthrough](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html){: external} in the {{site.data.keyword.openshiftshort}} documentation.</td>
    </tr>
    <tr>
    <td>Application Console</td>
    <td>Dropdown menu in the **OpenShift Container Platform** menu bar.</td>
    <td>For each project that you have access to, you can manage your {{site.data.keyword.openshiftshort}} resources such as pods, services, routes, builds, images or persistent volume claims. You can also view and analyze logs for these resources, or add services from the catalog to the project. For more information, see the [{{site.data.keyword.openshiftshort}} Web Console Walkthrough](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html){: external} in the {{site.data.keyword.openshiftshort}} documentation.</td>
    </tr>
    <tr>
    <td>Cluster Console</td>
    <td>Dropdown menu in the **OpenShift Container Platform** menu bar.</td>
    <td>For cluster-wide administrators across all the projects in the cluster, you can manage projects, service accounts,RBAC roles, role bindings, and resource quotas. You can also see the status and events for resources within the cluster in a combined view. For more information, see the [{{site.data.keyword.openshiftshort}} Web Console Walkthrough](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html){: external} in the {{site.data.keyword.openshiftshort}} documentation.</td>
    </tr>
    </tbody>
    </table><p></p>
3.  To work with your cluster in the CLI, click your profile **IAM#user.name@email.com > Copy Login Command**. Display and copy the `oc login` token command into your command line to authenticate via the CLI.

<br />
