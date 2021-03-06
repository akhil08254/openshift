---

copyright:
  years: 2014, 2021
lastupdated: "2021-02-11"

keywords: openshift, roks, rhoks, rhos, clusters

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


# Accessing {{site.data.keyword.openshiftshort}} clusters
{: #access_cluster}
{: help}
{: support}

After your {{site.data.keyword.openshiftlong}} cluster is created, you can begin working with your cluster by accessing the cluster.
{: shortdesc}

## Prerequisites
{: #prereqs}

1. [Install the required CLI tools](/docs/openshift?topic=openshift-openshift-cli), including the {{site.data.keyword.cloud_notm}} CLI, {{site.data.keyword.containershort_notm}} plug-in alias for {{site.data.keyword.openshiftshort}} (`ibmcloud oc`), and {{site.data.keyword.openshiftshort}} CLI (`oc`).
2. [Create your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-clusters).
3. If your network is protected by a company firewall, [allow access](/docs/openshift?topic=openshift-firewall#corporate) to the {{site.data.keyword.cloud_notm}} and {{site.data.keyword.openshiftlong_notm}} API endpoints and ports. For private service endpoint-only clusters, you cannot test the connection to your cluster until you expose the private service endpoint of the master to the cluster by using a [private NLB](#access_private_se).
4. Check that your cluster is in a healthy state by running `ibmcloud oc cluster get -c <cluster_name_or_ID>`. If your cluster is not in a healthy state, review the [Debugging clusters](/docs/openshift?topic=openshift-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall).
5. Find your cluster's service endpoint.
  * **Classic or VPC clusters**: In the output of the cluster details from the previous step, check the **Public** or **Private Service Endpoint** URL of the cluster.
      *  Public Service Endpoint URL only: Continue with [Accessing {{site.data.keyword.openshiftshort}} clusters through the public service endpoint](#access_public_se).
      *  Private Service Endpoint URL only: If your cluster has only a private service endpoint enabled, continue with [Accessing {{site.data.keyword.openshiftshort}} clusters through the private service endpoint](#access_private_se).
      *  Both service endpoint URLs: You can access your cluster either through the [public](#access_public_se) or the [private](#access_private_se) service endpoint.
  * **{{site.data.keyword.satellitelong_notm}} clusters**: Continue with [Accessing {{site.data.keyword.openshiftshort}} clusters on {{site.data.keyword.satelliteshort}}](#access_cluster_sat).

<br />

## Accessing {{site.data.keyword.openshiftshort}} clusters through the public service endpoint
{: #access_public_se}

For {{site.data.keyword.openshiftshort}} clusters with a public service endpoint, you can log in to your cluster from the console or CLI.
{: shortdesc}

### Connecting to the cluster from the console
{: #access_oc_console}

You can quickly access your {{site.data.keyword.openshiftlong_notm}} cluster from the console.
{: shortdesc}

1.  In the [{{site.data.keyword.openshiftlong_notm}} console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the cluster that you want to access.
2.  Click **{{site.data.keyword.openshiftshort}} web console**.
3.  To continue working in the command line, click your profile name, such as `IAM#name@email.com`, and then click **Copy Login Command**. Depending on your cluster version, log in to your cluster from the command line as follows.
    *  **Version 3.11**: Paste the copied `oc login` command into your command line.
    *  **Version 4**: Click **Display Token**, copy the `oc login` command, and paste the command into your command line.

**What's next?** Try [Deploying apps through the console](/docs/openshift?topic=openshift-deploy_app#deploy_apps_ui).

### Connecting to the cluster from the CLI
{: #access_oc_cli}

In most cases, you can use the {{site.data.keyword.openshiftshort}} web console to get the `oc login` token to access your cluster. If you cannot or do not want to open the {{site.data.keyword.openshiftshort}} console, choose among the following options to log in to your {{site.data.keyword.openshiftlong_notm}} cluster by using the CLI.
{: shortdesc}

Choose from the following options.
*   **Log in as admin**:
    1.  Make sure that you have the [**Administrator** platform role for the cluster](/docs/openshift?topic=openshift-users#add_users).
    2.  Set your command line context for the cluster and download the TLS certificates and permission files for the administrator.
        ```
        ibmcloud oc cluster config -c <cluster_name_or_ID> --admin
        ```
        {: pre}
*   **Log in with an API key**: See [Using an API key to log in to {{site.data.keyword.openshiftshort}}](/docs/openshift?topic=openshift-access_cluster#access_api_key).
*   **Log in with {{site.data.keyword.cloud_notm}} passcode**:
    1.  Get the **Master URL** of your cluster in the output of the following command.
        ```
        ibmcloud oc cluster get -c <cluster_name_or_ID>
        ```
        {: pre}
    2.  In your browser, open the following {{site.data.keyword.cloud_notm}} IAM passcode website.
        ```
        https://iam.cloud.ibm.com/identity/passcode
        ```
        {: codeblock}
    3.  Log in with your IBMid and copy the passcode.
    4.  Log in to your cluster with the passcode.
        ```
        oc login -u passcode -p <iam_passcode> --server=<master_URL>
        ```
        {: pre}

**What's next?** Try [Deploying apps through the CLI](/docs/openshift?topic=openshift-deploy_app#deploy_apps_cli).

<br />

## Accessing {{site.data.keyword.openshiftshort}} clusters through the private service endpoint
{: #access_private_se}

This information is applicable for version 3.11 clusters or version 4 clusters on VPC compute infrastructure. The private service endpoint cannot be enabled on version 4 clusters on classic infrastructure.
{: note}

The {{site.data.keyword.openshiftshort}} master is accessible through the private service endpoint if authorized cluster users are in your {{site.data.keyword.cloud_notm}} private network or are connected to the private network through a [VPC VPN connection](/docs/vpc?topic=vpc-vpn-onprem-example) for VPC infrastructure, or for classic infrastructure, a [VPN connection](/docs/iaas-vpn?topic=iaas-vpn-getting-started) or [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl). However, communication with the Kubernetes master over the private service endpoint must go through the <code>166.X.X.X</code> IP address range, which is not routable from a VPN connection or through {{site.data.keyword.dl_full_notm}}. You can expose the private service endpoint of the master for your cluster users by using a private network load balancer (NLB). The private NLB exposes the private service endpoint of the master as an internal <code>10.X.X.X</code> IP address range that users can access with the VPN or {{site.data.keyword.dl_full_notm}} connection. If you enable only the private service endpoint, you can use the {{site.data.keyword.openshiftshort}} web console to create the private NLB.
{: shortdesc}

### Accessing version 4 VPC clusters through the private service endpoint
{: #vpc_private_se}

1. Set up your {{site.data.keyword.vpc_short}} VPN and connect to your private network through the VPN.
  1. [Configure a VPN gateway on your local machine](/docs/vpc?topic=vpc-vpn-onprem-example#configuring-onprem-gateway). For example, you might choose to set up StrongSwan on your machine.
  2. [Create a VPN gateway in your VPC, and create the connection between the VPC VPN gateway and your local VPN gateway](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console#vpn-ui). If you have a multizone cluster, you must create a VPC gateway on a subnet in each zone where you have worker nodes.
  3. Verify that you are connected to the private network through your {{site.data.keyword.vpc_short}} VPN connection.

2. Get the private service endpoint URL and port for your cluster.
  ```
  ibmcloud oc cluster get -c <cluster_name_or_ID>
  ```
  {: pre}

  In this example output, the **Private Service Endpoint URL** is `https://c1.private.us-east.containers.cloud.ibm.com:31144`.
  ```
  Name:                           setest
  ID:                             b8dcc56743394fd19c9f3db7b990e5e3
  State:                          normal
  Status:                         healthy cluster
  Created:                        2019-04-25T16:03:34+0000
  Location:                       wdc04
  Pod Subnet:                     172.30.0.0/16
  Service Subnet:                 172.21.0.0/16
  Master URL:                     https://c1-e.us-east.containers.cloud.ibm.com:31144
  Public Service Endpoint URL:    https://c1-e.us-east.containers.cloud.ibm.com:31144
  Private Service Endpoint URL:   https://c1.private.us-east.containers.cloud.ibm.com:31144
  Master Location:                Washington D.C.
  ...
  ```
  {: screen}

3. Create a YAML file that is named `oc-api-via-nlb.yaml`. This YAML creates a private `LoadBalancer` service and exposes the private service endpoint through that NLB. Replace `<private_service_endpoint_port>` with the port you found in the previous step.
   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: oc-api-via-nlb
     annotations:
       service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: private
     namespace: default
   spec:
     type: LoadBalancer
     ports:
     - protocol: TCP
       port: <private_service_endpoint_port>
       targetPort: <private_service_endpoint_port>
   ---
   kind: Endpoints
   apiVersion: v1
   metadata:
     name: oc-api-via-nlb
     namespace: default
   subsets:
     - addresses:
         - ip: 172.20.0.1
       ports:
         - port: 2040
   ```
   {: codeblock}

4. To create the private NLB, you must be connected to the cluster master. Because you cannot yet connect through the private service endpoint from a VPN or {{site.data.keyword.dl_full_notm}}, you must connect to the cluster master and create the NLB by using the public service endpoint or {{site.data.keyword.openshiftshort}} web console.
  * Public service endpoint enabled: You already have access to the master.
    1. Apply the configuration file that you previously created.
      ```
      oc apply -f oc-api-via-nlb.yaml
      ```
      {: pre}
    2. Verify that the `oc-api-via-nlb` NLB is created. In the output, note the `10.x.x.x` **EXTERNAL-IP** address. This IP address exposes the private service endpoint for the cluster master on the port that you specified in your YAML file.
      ```
      oc get svc -o wide
      ```
      {: pre}

      In this example output, the IP address for the private service endpoint of the master is `10.186.92.42`.
      ```
      NAME                     TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)          AGE   SELECTOR
      oc-api-via-nlb           LoadBalancer   172.21.150.118   10.186.92.42     443:32235/TCP    10m   <none>
      ...
      ```
      {: screen}
  * Private service endpoint enabled only: Use the {{site.data.keyword.openshiftshort}} web console dashboard to create the NLB. The web console automatically routes all requests to the private service endpoint of the master.
    1. From the [{{site.data.keyword.openshiftlong_notm}} console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, select your {{site.data.keyword.openshiftshort}} cluster, then click **{{site.data.keyword.openshiftshort}} web console**.
    2. In the **Networking** tab, click **Services**
    3. Click **Create Service**.
    4. Paste the contents of the `kube-api-via-nlb.yaml` file, and click **Create**.
    5. In the **Overview** page, verify that the `kube-api-via-nlb` service is created and copy the `10.x.x.x` address. This IP address exposes the private service endpoint for the cluster master on the port that you specified in your YAML file.

5. To log in to your cluster, choose from the following options.
  * **Log in as admin**:
      1.  Make sure that you have the [**Administrator** platform role for the cluster](/docs/openshift?topic=openshift-users#add_users).
      2.  Set your command line context for the cluster and download the TLS certificates and permission files for the administrator.
          ```
          ibmcloud oc cluster config -c <cluster_name_or_ID> --admin --endpoint private
          ```
          {: pre}
  * **Log in with an API key**: See [Using an API key to log in to {{site.data.keyword.openshiftshort}}](/docs/openshift?topic=openshift-access_cluster#access_api_key).
  * **Log in with {{site.data.keyword.cloud_notm}} passcode**:
      1.  Get the **Private Service Endpoint URL** of your cluster in the output of the following command.
          ```
          ibmcloud oc cluster get -c <cluster_name_or_ID>
          ```
          {: pre}
      2.  In your browser, open the following {{site.data.keyword.cloud_notm}} IAM passcode website.
          ```
          https://iam.cloud.ibm.com/identity/passcode
          ```
          {: codeblock}
      3.  Log in with your IBMid and copy the passcode.
      4.  Log in to your cluster with the passcode.
          ```
          oc login -u passcode -p <iam_passcode> --server=<private_service_endpoint_URL>
          ```
          {: pre}

6. Verify that the `oc` commands run properly with your cluster through the private service endpoint by checking the version.
  ```
  oc version
  ```
  {: pre}

  Example output:

  ```
  Client Version: 4.5.0-0.okd-2020-09-04-180756
  Kubernetes Version: v1.17.1+45f8ddb
  ```
  {: screen}

### Accessing 3.11 clusters through the private service endpoint
{: #classic_private_se}

1. Log in to your [{{site.data.keyword.openshiftshort}} cluster by using the public service endpoint](#access_public_se).

2. Get the private service endpoint URL and port for your cluster.
  ```
  ibmcloud oc cluster get -c <cluster_name_or_ID>
  ```
  {: pre}

  In this example output, the **Private Service Endpoint URL** is `https://c1.private.us-east.containers.cloud.ibm.com:31144`.
  ```
  Name:                           setest
  ID:                             b8dcc56743394fd19c9f3db7b990e5e3
  State:                          normal
  Status:                         healthy cluster
  Created:                        2019-04-25T16:03:34+0000
  Location:                       wdc04
  Pod Subnet:                     172.30.0.0/16
  Service Subnet:                 172.21.0.0/16
  Master URL:                     https://c1-e.us-east.containers.cloud.ibm.com:31144
  Public Service Endpoint URL:    https://c1-e.us-east.containers.cloud.ibm.com:31144
  Private Service Endpoint URL:   https://c1.private.us-east.containers.cloud.ibm.com:31144
  Master Location:                Washington D.C.
  ...
  ```
  {: screen}

3. Create a YAML file that is named `oc-api-via-nlb.yaml`. This YAML creates a private `LoadBalancer` service and exposes the private service endpoint through that NLB. Replace `<private_service_endpoint_port>` with the port you found in the previous step.
   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: oc-api-via-nlb
     annotations:
       service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: private
     namespace: default
   spec:
     type: LoadBalancer
     ports:
     - protocol: TCP
       port: <private_service_endpoint_port>
       targetPort: <private_service_endpoint_port>
   ---
   kind: Endpoints
   apiVersion: v1
   metadata:
     name: oc-api-via-nlb
     namespace: default
   subsets:
     - addresses:
         - ip: 172.20.0.1
       ports:
         - port: 2040
   ```
   {: codeblock}

4. To create the private NLB and endpoint:
   1. Apply the configuration file that you previously created.
      ```
      oc apply -f oc-api-via-nlb.yaml
      ```
      {: pre}
   2. Verify that the `oc-api-via-nlb` NLB is created. In the output, note the `10.x.x.x` **EXTERNAL-IP** address. This IP address exposes the private service endpoint for the cluster master on the port that you specified in your YAML file.
      ```
      oc get svc -o wide
      ```
      {: pre}

      In this example output, the IP address for the private service endpoint of the master is `10.186.92.42`.
      ```
      NAME                     TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)          AGE   SELECTOR
      oc-api-via-nlb           LoadBalancer   172.21.150.118   10.186.92.42     443:32235/TCP    10m   <none>
      ...
      ```
      {: screen}

5. On the client machines where you or your users run `oc` commands, add the NLB IP address and the private service endpoint URL to the `/etc/hosts` file. Do not include any ports in the IP address and URL and do not include `https://` in the URL.
  * For macOS and Linux users:
    ```
    sudo nano /etc/hosts
    ```
    {: pre}
  * For Windows users:
    ```
    notepad C:\Windows\System32\drivers\etc\hosts
    ```
    {: pre}

    Depending on your local machine permissions, you might need to run Notepad as an administrator to edit the hosts file.
    {: tip}

    Example text to add:
    ```
    10.186.92.42      c1.private.us-east.containers.cloud.ibm.com
    ```
    {: codeblock}

6. Verify that you are connected to the private network through a [VPN](/docs/iaas-vpn?topic=iaas-vpn-getting-started) or [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) connection.

7. Log in to your cluster by choosing from one of the following options.
  * **Log in as admin**:
      1.  Make sure that you have the [**Administrator** platform role for the cluster](/docs/openshift?topic=openshift-users#add_users).
      2.  Set your command line context for the cluster and download the TLS certificates and permission files for the administrator.
          ```
          ibmcloud oc cluster config -c <cluster_name_or_ID> --admin --endpoint private
          ```
          {: pre}
  * **Log in with an API key**: See [Using an API key to log in to {{site.data.keyword.openshiftshort}}](/docs/openshift?topic=openshift-access_cluster#access_api_key).
  * **Log in with {{site.data.keyword.cloud_notm}} passcode**:
      1.  Get the **Private Service Endpoint URL** of your cluster in the output of the following command.
          ```
          ibmcloud oc cluster get -c <cluster_name_or_ID>
          ```
          {: pre}
      2.  In your browser, open the following {{site.data.keyword.cloud_notm}} IAM passcode website.
          ```
          https://iam.cloud.ibm.com/identity/passcode
          ```
          {: codeblock}
      3.  Log in with your IBMid and copy the passcode.
      4.  Log in to your cluster with the passcode.
          ```
          oc login -u passcode -p <iam_passcode> --server=<private_service_endpoint_URL>
          ```
          {: pre}

8. Verify that the `oc` commands run properly with your cluster through the private service endpoint by checking the version.
    ```
    oc version
    ```
    {: pre}

    Example output:

    ```
    oc v3.11.0+0cbc58b
    kubernetes v1.11.0+d4cacc0
    features: Basic-Auth

    Server https://c1.private.us-east.containers.cloud.ibm.com:31144
    openshift v3.11.98
    kubernetes v1.11.0+d4cacc0
    ```
    {: screen}

<br />


### Creating an allowlist for the private service endpoint
{: #private-se-allowlist}

Control access to your private service endpoint by creating a subnet allowlist.
{: shortdesc}

After you [grant users access to your cluster through {{site.data.keyword.cloud_notm}} IAM](/docs/openshift?topic=openshift-users#platform), you can add a secondary layer of security by creating an allowlist for the private service endpoint. Only authorized requests to your cluster master that originate from subnets in the allowlist are permitted through the cluster's private service endpoint.

For example, to access your cluster's private service endpoint, you must connect to your {{site.data.keyword.cloud_notm}} classic network or your VPC network through a VPN or {{site.data.keyword.dl_full_notm}}. You can add the subnet for the VPN or {{site.data.keyword.dl_short}} tunnel so that authorized users in your organization can only access the private service endpoint from that subnet.

A private service endpoint allowlist can also help prevent users from accessing your cluster after their authorization is revoked. When a user leaves your organization, you remove their {{site.data.keyword.cloud_notm}} IAM permissions that grant them access to the cluster. However, the user might have copied the API key that contains a functional ID's credentials, which contain the necessary IAM permissions for you cluster. That user can still use those credentials and the private service endpoint address to access your cluster from a different subnet, such as from a different {{site.data.keyword.cloud_notm}} account. If you create an allowlist that includes only the subnets for your VPN tunnel in your organization's {{site.data.keyword.cloud_notm}} account, the user's attempted access from another {{site.data.keyword.cloud_notm}} account is denied.

Worker node subnets are automatically added to and removed from your allowlist so that worker nodes can always access the master through the private service endpoint.

If the public service endpoint is enabled for your cluster, authorized requests are still permitted through the public service endpoint. Therefore, the private service endpoint allowlist is most effective for controlling access to clusters that have only the private service endpoint enabled.
{: note}

Before you begin:
* [Access your cluster through the private service endpoint](#access_private_se).
* [Grant users access to your cluster through {{site.data.keyword.cloud_notm}} IAM](/docs/openshift?topic=openshift-users#platform).

To create a private service endpoint allowlist:

1. Get the subnets that you want to add to the allowlist. For example, you might get the subnet for the connection through your VPN or {{site.data.keyword.dl_short}} tunnel to your {{site.data.keyword.cloud_notm}} private network.

2. Enable the subnet allowlist feature for a cluster's private service endpoint. Now, access to the cluster via the private service endpoint is blocked for any requests that originate from a subnet that is not in the allowlist. Your worker nodes continue to run and have access to the master.
  ```
  ibmcloud oc cluster master private-service-endpoint allowlist enable --cluster <cluster_name_or_ID>
  ```
  {: pre}

3. Add subnets from which authorized users can access your private service endpoint to the allowlist.
  ```
  ibmcloud oc cluster master private-service-endpoint allowlist add --cluster <cluster_name_or_ID> --subnet <subnet_CIDR> [--subnet <subnet_CIDR> ...]
  ```
  {: pre}

4. Verify that the subnets in your allowlist are correct. The allowlist includes subnets that you manually added and subnets that are automatically added and managed by IBM, such as worker node subnets.
  ```
  ibmcloud oc cluster master private-service-endpoint allowlist get --cluster <cluster_name_or_ID>
  ```
  {: pre}

Your authorized users can now continue with [Accessing {{site.data.keyword.openshiftshort}} clusters through the private service endpoint](#access_private_se).


## Accessing {{site.data.keyword.openshiftshort}} clusters on {{site.data.keyword.satelliteshort}}
{: #access_cluster_sat}

After you [create a {{site.data.keyword.openshiftshort}} cluster in your {{site.data.keyword.satelliteshort}} location](/docs/openshift?topic=openshift-satellite-clusters), you can begin working with your cluster by accessing the cluster.
{: shortdesc}

### Accessing clusters through the cluster service URL
{: #access_cluster_sat_se}

Connect to your cluster through its service URL. This URL is one of your {{site.data.keyword.satelliteshort}} location subdomains and a node port, which is formatted such as `https://p1iuql40jam23qiuxt833-q9err0fiffbsar61e78vv6e7ds8ne1tx-ce00.us-east.satellite.appdomain.cloud:30710`.
{: shortdesc}

If you use hosts that have private network connectivity only for your location, you must be connected to your hosts' private network, such as through VPN access, to connect to your cluster and access the {{site.data.keyword.openshiftshort}} web console.
{: note}

You can quickly access your {{site.data.keyword.openshiftlong_notm}} cluster from the console.
1.  In the [{{site.data.keyword.openshiftlong_notm}} console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the cluster that you want to access.
2.  Click **{{site.data.keyword.openshiftshort}} web console**.
3.  Click your profile name, such as `IAM#name@email.com`, and then click **Copy Login Command**.
4.  Click **Display Token**, and copy the `oc login` command.
5.  Paste the command into your command line.

If you cannot or do not want to open the {{site.data.keyword.openshiftshort}} console, choose among the following options to log in to your {{site.data.keyword.openshiftlong_notm}} cluster by using the CLI.
*   **Log in as admin**:
    1.  Make sure that you have the [**Administrator** IAM platform role for the cluster](/docs/openshift?topic=openshift-users#add_users).
    2.  Set your command line context for the cluster and download the TLS certificates and permission files for the administrator. For more information, see the [CLI documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_config).
        ```
        ibmcloud oc cluster config -c <cluster_name_or_ID> --admin
        ```
        {: pre}
*   **Log in with an API key**: See [Using an API key to log in to {{site.data.keyword.openshiftshort}}](/docs/openshift?topic=openshift-access_cluster#access_api_key).

### Accessing clusters from within the {{site.data.keyword.cloud_notm}} private network
{: #access_cluster_sat_link}

If you are connected to the {{site.data.keyword.cloud_notm}} private network, you can use the {{site.data.keyword.satelliteshort}} Link endpoint that is automatically generated for your cluster. This endpoint allows you to connect through the secured Link tunnel server to the cluster's master in your location control plane. The endpoint consists of the Link tunnel server hostname and a node port, which is formatted such as `c-02.<region>.link.satellite.cloud.ibm.com:<port>`.
{: shortdesc}

1.  Make sure that you have the [**Administrator** IAM platform role for the cluster](/docs/openshift?topic=openshift-users#add_users).
2.  Set your command line context for the cluster by using the Link endpoint and download the TLS certificates and permission files for the administrator. For more information, see the [CLI documentation](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_config).
    ```
    ibmcloud oc cluster config -c <cluster_name_or_ID> --endpoint link --admin
    ```
    {: pre}

<br />

## Accessing clusters from automation tools by using an API key
{: #access_automation}

{{site.data.keyword.openshiftlong_notm}} is integrated with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). With IAM, you can authenticate users and services by using their IAM identities and authorize actions with access roles and policies. When you authenticate as a user through the {{site.data.keyword.openshiftshort}} console, your IAM identity is used to generate an {{site.data.keyword.openshiftshort}} login token that you can use to log in to the command line. You can automate logging in to your cluster by creating an IAM API key or service ID to use for the `oc login` command.
{: shortdesc}

### Using an API key to log in to clusters
{: #access_api_key}

You can create an {{site.data.keyword.cloud_notm}} IAM API key and then use the API key to log in to an {{site.data.keyword.openshiftshort}} cluster. With API keys, you can use the credentials of one user or shared account to access a cluster, instead of logging in individually. You might also create an API key for a [service ID](#access_service_id). For more information, see [Understanding API keys](/docs/account?topic=account-manapikey).
{: shortdesc}

1.  Create an {{site.data.keyword.cloud_notm}} API key.<p class="important">Save your API key in a secure location. You cannot retrieve the API key again. If you want to export the output to a file on your local machine, include the `--file <path>/<file_name>` flag.</p>
    ```
    ibmcloud iam api-key-create <name>
    ```
    {: pre}
2.  Configure your cluster to add the API key user to your cluster RBAC policies and to set your session context to your cluster server.
    1.  Log in to {{site.data.keyword.cloud_notm}} with the API key credentials.
        ```
        ibmcloud login --apikey <API_key>
        ```
        {: pre}
    2.  Download and add the `kubeconfig` configuration file for your cluster to your existing `kubeconfig` in `~/.kube/config` or the last file in the `KUBECONFIG` environment variable. **Note**: If you enabled the private service endpoint and want to use it for the cluster context, include the `--endpoint private` flag. To use the private service endpoint to connect to your cluster, you must be in your {{site.data.keyword.cloud_notm}} private network or connected to the private network through a [VPC VPN connection](/docs/vpc?topic=vpc-vpn-onprem-example), or for classic infrastructure, a [classic VPN connection](/docs/iaas-vpn?topic=iaas-vpn-getting-started) or [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl).
        ```
        ibmcloud oc cluster config -c <cluster_name_or_ID> [--endpoint private]
        ```
        {: pre}
3.  Exchange your {{site.data.keyword.cloud_notm}} IAM API key credentials for an {{site.data.keyword.openshiftshort}} access token. You can log in from the CLI or API. For more information, see the [{{site.data.keyword.openshiftshort}} docs](https://docs.openshift.com/container-platform/4.5/authentication/configuring-internal-oauth.html){: external}.

    **Log in by using the `oc` CLI**:
    Log in to your cluster with the `oc login` command. The username (`-u`) is `apikey` and the password (`-p`) is your {{site.data.keyword.cloud_notm}} IAM API key value. To use the private service endpoint, include the `--server=<private_service_endpoint>` flag.
    ```
    oc login -u apikey -p <API_key> [--server=<private_service_endpoint>]
    ```
    {: pre}

    **Log in by running {{site.data.keyword.openshiftshort}} API requests directly against your cluster**:
    Log in to your cluster with the API such as via a curl request.

    1.  Get the **Master URL** of your cluster.
        ```
        ibmcloud oc cluster get -c <cluster_name_or_ID>
        ```
        {: pre}

        Example output:
        ```
        Name:                           mycluster
        ID:                             1234567
        State:                          normal
        Created:                        2020-01-22T19:22:16+0000
        Location:                       dal10
        Master URL:                     https://c100-e.<region>.containers.cloud.ibm.com:<port>
        ...

        ```
        {: screen}
    2.  <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> **{{site.data.keyword.openshiftshort}} version 4 only**: Get the token endpoint of the {{site.data.keyword.openshiftshort}} `oauth` server.
        ```
        curl <master_URL>/.well-known/oauth-authorization-server | jq -r .token_endpoint
        ```
        {: pre}

        Example output:
        ```
        <token_endpoint>/oauth/token
        ```
    3.  Log in to the cluster with the endpoint that you previously retrieved.
        * <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> **{{site.data.keyword.openshiftshort}} version 4**: Replace `<URL>` with the `<token_endpoint>` of the `oauth` server.
        * <img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> **{{site.data.keyword.openshiftshort}} version 3.11**: Replace `<URL>` with the master URL.

        Example curl request:
        ```
        curl -u 'apikey:<API_key>' -H "X-CSRF-Token: a" '<URL>/oauth/authorize?client_id=openshift-challenging-client&response_type=token' -vvv
        ```
        {: pre}
    4.  In the **Location** response, find the `access_token`, such as in the following example.
        ```
        < HTTP/1.1 302 Found
        < Cache-Control: no-cache, no-store, max-age=0, must-revalidate
        < Cache-Control: no-cache, no-store, max-age=0, must-revalidate
        < Expires: 0
        < Expires: Fri, 01 Jan 1990 00:00:00 GMT
        < Location: <token_endpoint>/oauth/token/implicit#access_token=<access_token>&expires_in=86400&scope=user%3Afull&token_type=Bearer
        ...
        ```
        {: screen}
    5.  Use your cluster master URL and the access token to access the {{site.data.keyword.openshiftshort}} API, such as to list all the pods in your cluster.

        Example curl request:
        ```
        curl -H "Authorization: Bearer <access_token>" '<master_URL>/api/v1/pods'
        ```
        {: pre}

### Using a service ID to log in to clusters
{: #access_service_id}

You can create an {{site.data.keyword.cloud_notm}} IAM service ID, make an API key for the service ID, and then use the API key to log in to an {{site.data.keyword.openshiftshort}} cluster. You might use service IDs so that apps that are hosted in other clusters or clouds can access your cluster's services. Because service IDs are not tied to a specific user, your apps can authenticate if individual users leave your account. For more information, see [Creating and working with service IDs](/docs/account?topic=account-serviceids).
{: shortdesc}

1.  Create an {{site.data.keyword.cloud_notm}} IAM service ID for your cluster that is used for the IAM policies and API key credentials. Be sure to give the service ID a description that helps you retrieve the service ID later, such as including the cluster name.
    ```
    ibmcloud iam service-id-create <cluster_name>-id --description "Service ID for {{site.data.keyword.openshiftlong_notm}} cluster <cluster_name>"
    ```
    {: pre}

    Example output:
    ```
    Name          <cluster_name>-id
    Description   Service ID for {{site.data.keyword.openshiftlong_notm}} cluster <cluster_name>
    CRN           crn:v1:bluemix:public:iam-identity::a/1aa111aa1a11111aaa1a1111aa1aa111::serviceid:ServiceId-bbb2b2b2-2bb2-2222-b222-b2b2b2222b22
    Bound To      crn:v1:bluemix:public:::a/1aa111aa1a11111aaa1a1111aa1aa111:::
    Version       1-c3c333333333ccccc33333c33cc3cc33
    Locked        false
    UUID          ServiceId-bbb2b2b2-2bb2-2222-b222-b2b2b2222b22
    ```
    {: screen}
2.  Create a custom {{site.data.keyword.cloud_notm}} IAM policy for your cluster service ID that grants access to {{site.data.keyword.openshiftlong_notm}}.
    ```
    ibmcloud iam service-policy-create <cluster_service_ID> --service-name containers-kubernetes --roles <service_access_role> --service-instance <cluster_ID>
    ```
    {: pre}
    <table summary="The columns are read from left to right. The first column has the parameter of the command. The second column describes the parameter.">
    <caption>Understanding this command's components</caption>
    <col width="25%">
    <thead>
    <th>Parameter</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td><code><em>&lt;cluster_service_ID&gt;</em></code></td>
    <td>Required. Enter the service ID that you previously created for your {{site.data.keyword.openshiftshort}} cluster.</td>
    </tr>
    <tr>
    <td><code>--service-name <em>containers-kubernetes</em></code></td>
    <td>Required. Enter `containers-kubernetes` so that the IAM policy is for {{site.data.keyword.openshiftlong_notm}} clusters.</td>
    </tr>
    <tr>
    <td><code>--roles <em>&lt;service_access_role&gt;</em></code></td>
    <td>Required. Enter the access role that you want the service ID to have to your {{site.data.keyword.openshiftshort}} cluster. [Platform roles](/docs/openshift?topic=openshift-access_reference#iam_platform) permit cluster management activities such as creating worker nodes. [Service roles](/docs/openshift?topic=openshift-access_reference#service) correspond to RBAC roles that permit {{site.data.keyword.openshiftshort}} management activities within the cluster, such as for Kubernetes resources like pods and namespaces. For multiple roles, include a comma-separated list. Possible values are `Administrator`, `Operator`, `Editor`, and `Viewer` (platform roles); and `Reader`, `Writer`, and `Manager` (service roles).</td>
    </tr>
    <tr>
      <td><code>--service-instance <em>&lt;cluster_ID&gt;</em></code></td>
      <td>To restrict the policy to a particular cluster, enter the cluster's ID. To get your cluster ID, run `ibmcloud oc clusters`.<p class="note">If you do not include the service instance, the access policy grants the service ID access to all your clusters, Kubernetes and {{site.data.keyword.openshiftshort}}. You can also scope the access policy to a region (`--region`) or resource group (`--resource-group-name`).</td>
    </tr>
    </tbody></table>
3.  Create an API key for the service ID. Name the API key similar to your service ID, and include the service ID that you previously created, `<cluster_name>-id`. Be sure to give the API key a description that helps you retrieve the key later.<p class="important">Save your API key in a secure location. You cannot retrieve the API key again. If you want to export the output to a file on your local machine, include the `--file <path>/<file_name>` flag.</p>
    ```
    ibmcloud iam service-api-key-create <cluster_name>-key <service_ID> --description "API key for service ID <service_ID> in {{site.data.keyword.openshiftshort}} cluster <cluster_name>"
    ```
    {: pre}

    Example output:
    ```
    Please preserve the API key! It cannot be retrieved after it's created.

    Name          <cluster_name>-key
    Description   API key for service ID <service_ID> in {{site.data.keyword.openshiftshort}} cluster <cluster_name>
    Bound To      crn:v1:bluemix:public:iam-identity::a/1bb222bb2b33333ddd3d3333ee4ee444::serviceid:ServiceId-ff55555f-5fff-6666-g6g6-777777h7h7hh
    Created At    2019-02-01T19:06+0000
    API Key       i-8i88ii8jjjj9jjj99kkkkkkkkk_k9-llllll11mmm1
    Locked        false
    UUID          ApiKey-222nn2n2-o3o3-3o3o-4p44-oo444o44o4o4
    ```
    {: screen}
4.  Configure your cluster to add the service ID user to your cluster RBAC policies and to set your session context to your cluster server.
    1.  Log in to {{site.data.keyword.cloud_notm}} with the service ID's API key credentials.
        ```
        ibmcloud login --apikey <API_key>
        ```
        {: pre}
    2.  Download and add the `kubeconfig` configuration file for your cluster to your existing `kubeconfig` in `~/.kube/config` or the last file in the `KUBECONFIG` environment variable. **Note**: If you enabled the private service endpoint and want to use it for the cluster context, include the `--endpoint private` flag. To use the private service endpoint to connect to your cluster, you must be in your {{site.data.keyword.cloud_notm}} private network or connected to the private network through a [VPC VPN connection](/docs/vpc?topic=vpc-vpn-onprem-example), or for classic infrastructure, a [classic VPN connection](/docs/iaas-vpn?topic=iaas-vpn-getting-started) or [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl).
        ```
        ibmcloud oc cluster config -c <cluster_name_or_ID> [--endpoint private]
        ```
        {: pre}
5.  [Use the service ID's API key to log in to your {{site.data.keyword.openshiftshort}} cluster](#access_api_key). The username (`-u`) is `apikey` and the password (`-p`) is your API key value. To use the private service endpoint, include the `--server=<private_service_endpoint>` flag.
    ```
    oc login -u apikey -p <API_key> [--server=<private_service_endpoint>]
    ```
    {: pre}
6.  Verify that the service ID can perform the actions that you authorized.

    Example: If you assigned a `Reader` service role, the service ID can list pods in your {{site.data.keyword.openshiftshort}} project.
    ```
    oc get pods
    ```
    {: pre}

    Example: If you assigned a `Manager` service role, the service ID can list the users in your {{site.data.keyword.openshiftshort}} cluster. The ID of your IAM service ID is in the **Identities** output. Other individual users might be identified by their email address and IBMid.
    ```
    oc get users
    ```
    {: pre}

    Example output:
    ```
    NAME                           UID                                    FULL NAME   IDENTITIES
    IAM#                           dd44ddddd-d4dd-44d4-4d44-4d44d444d444              IAM:iam-ServiceId-bbb2b2b2-2bb2-2222-b222-b2b2b2222b22
    IAM#first.last@email.com       55555ee5-e555-55e5-e5e5-555555ee55ee               IAM:IBMid-666666FFF6
    ```
    {: screen}

<br />

## Accessing the cluster master via admission controllers and webhooks
{: #access_webhooks}

Admission controllers intercept authorized API requests from various Kubernetes resources before the requests reach the API server that runs in your {{site.data.keyword.openshiftlong_notm}} cluster master. Mutating admission webhooks might modify the request, and validating admission webhooks check the request. If either webhook rejects a request, the entire request fails. Advanced features, whether built-in or added on, often require admission controllers as a security precaution and to control what requests are sent to the API server. For more information, see [Using Admission Controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/){: external} and [Dynamic Admission Control](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} in the Kubernetes documentation.


**Can I create my own admission controllers?**

Yes, see the [Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} and [{{site.data.keyword.openshiftshort}}](https://docs.openshift.com/container-platform/4.5/architecture/admission-plug-ins.html){: external} documentation for more information.

As noted in the Kubernetes documentation, you can use admission controllers for operations that are otherwise handled by the control plane. As such, take great caution when you configure a custom admission controller. You are responsible for any changes that happen in your cluster because of a custom admission controller.
{: important}

Keep in mind the following considerations when you configure a webhook.

* Create [replica pods](/docs/openshift?topic=openshift-openshift_apps#replicaset) for the webhook so that if one pod goes down, the webhook can still process requests from your resources. Spread the replica pods across zones, if possible.
* Set appropriate CPU and memory [resource requests and limits](/docs/openshift?topic=openshift-openshift_apps#resourcereq) for your webhook.
* Add [liveness and readiness probes](/docs/openshift?topic=openshift-openshift_apps#probe) to help make sure your webhook container is running and ready to serve requests.
* Set pod [anti-affinity scheduling rules](/docs/openshift?topic=openshift-openshift_apps#affinity) to prefer that your webhook pods run on different worker nodes and zones when possible. In clusters that run {{site.data.keyword.openshiftshort}} version 4.4 or later, you might use [pod topology](https://kubernetes.io/docs/concepts/workloads/pods/pod-topology-spread-constraints/){: external} instead. However, avoid [taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external} or forced affinity that might restrict where the webhook pods can be scheduled.
* [Set pod priority](/docs/openshift?topic=openshift-pod_priority) to `system-cluster-critical` for the webhook pods so that other pods cannot take resources from your webhook pods.
* Scope your webhook to the appropriate project. Avoid webhooks that process resources that run in system-critical projects that are set up in your cluster by default, such as `kube-system`, `ibm-system`, `ibm-operators`, `calico-system`, `tigera-operator` and `openshift-*` projects.
* Make sure that the worker nodes in your cluster are [the right size for running your webhook applications](/docs/openshift?topic=openshift-strategy#sizing). For example, if your pods request more CPU or memory than the worker node can provide, the pods are not scheduled.

<br>

**What other types of apps use admission controllers?**

Many cluster add-ons, plug-ins, and other third-party extensions create custom admission controllers. Some common ones include:
*   [Portieris](https://github.com/IBM/portieris){: external}

<br>

**I need help with a broken webhook. What can I do?**

See [Cluster cannot update because of broken webhook](/docs/openshift?topic=openshift-cs_troubleshoot#webhooks_update).
