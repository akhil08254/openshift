---

copyright:
  years: 2014, 2021
lastupdated: "2021-02-17"

keywords: openshift, roks, rhoks, rhos, version, rhel, update, upgrade

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



# Version information and update actions
{: #openshift_versions}

Review information about the supported {{site.data.keyword.openshiftshort}} versions for {{site.data.keyword.openshiftlong}} clusters.
{: shortdesc}

For more information about the {{site.data.keyword.openshiftshort}} and Kubernetes project versions, review the following information.
* [{{site.data.keyword.openshiftshort}} 4.6 release notes overview](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html){: external}
* [{{site.data.keyword.openshiftshort}} 4.5 release notes overview](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html){: external}
* [{{site.data.keyword.openshiftshort}} 4.4 release notes overview](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html){: external}
* Deprecated: [{{site.data.keyword.openshiftshort}} 4.3 release notes overview](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html){: external}
* Deprecated: [{{site.data.keyword.openshiftshort}} 3.11 release notes overview](https://docs.openshift.com/container-platform/3.11/release_notes/index.html){: external}
* [Kubernetes changelog](https://github.com/kubernetes/kubernetes/tree/master/CHANGELOG){: external}

## Update types
{: #openshift_update_types}

Your {{site.data.keyword.openshiftlong_notm}} cluster has three types of updates: major, minor, and patch. As updates become available, you are notified when you view information about the cluster master or worker nodes, such as with the `ibmcloud oc cluster ls`, `cluster get`, `worker ls`, or `worker get` commands.
{: shortdesc}

You must [update your cluster](/docs/openshift?topic=openshift-update) by using the {{site.data.keyword.openshiftlong_notm}} API, CLI, or console tools. You cannot update your cluster version from OpenShift Container Platform tools such as the {{site.data.keyword.openshiftshort}} web console.
{: note}

|Update type|Examples of version labels|Updated by|Impact
|-----|-----|-----|-----|
|Major|3.x.x|You|Operation changes for clusters, including scripts or deployments.|
|Minor|x.11.x|You|Operation changes for clusters, including scripts or deployments.|
|Patch|x.x.104_1507|IBM and you|{{site.data.keyword.openshiftshort}} patches, as well as other {{site.data.keyword.cloud_notm}} Provider component updates such as security and operating system patches. IBM updates masters automatically, but you apply patches to worker nodes. See more about patches in the following section.|
{: caption="Impacts of {{site.data.keyword.openshiftshort}} updates" caption-side="top"}

<dl>
  <dt>**Major and minor updates (4.5)**</dt>
  <dd><p>First, [update your master node](/docs/openshift?topic=openshift-update#master) and then [update the worker nodes](/docs/openshift?topic=openshift-update#worker_node). Worker nodes cannot run an {{site.data.keyword.openshiftshort}} major or minor version that is greater than the masters. Additionally, your worker nodes can be only one version behind the master version (`n-1`).</p><p class="note">If you use an `oc` or `oc` CLI version that does match at least the `major.minor` version of your clusters, you might experience unexpected results. Make sure to keep your cluster and [CLI versions](/docs/openshift?topic=openshift-openshift-cli#cli_oc) up-to-date.</p></dd>
  <dt>**Patch updates (4.5.24_xxxx_openshift)**</dt>
  <dd><p>Changes across patches are documented in the [Version changelog](/docs/openshift?topic=openshift-openshift_versions). Master patches are applied automatically, but you initiate worker node patches updates. Worker nodes can also run patch versions that are greater than the masters. As updates become available, you are notified when you view information about the master and worker nodes in the {{site.data.keyword.cloud_notm}} console or CLI, such as with the following commands: `ibmcloud oc cluster ls`, `cluster get`, `worker ls`, or `worker get`.</p>
  <p>Patches can be for worker nodes, masters, or both.</p>
  <ul><li>**Worker node patches**: Check monthly to see whether an update is available, and use the `ibmcloud oc worker update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_update) or the `ibmcloud oc worker reload` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) to apply these security and operating system patches. During an update or reload, your worker node machine is reimaged, and data is deleted if not [stored outside the worker node](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview).</li>
  <li>**Master patches**: Master patches are applied automatically over the course of several days, so a master patch version might show up as available before it is applied to your master. The update automation also skips clusters that are in an unhealthy state or have operations currently in progress. Occasionally, IBM might disable automatic updates for a specific master fix pack, as noted in the changelog, such as a patch that is only needed if a master is updated from one minor version to another. In any of these cases, you can choose to safely use the `ibmcloud oc cluster master update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_update) yourself without waiting for the update automation to apply.</li></ul></dd>
</dl>

<br />

## {{site.data.keyword.openshiftshort}} versions
{: #version_types}

{{site.data.keyword.openshiftlong_notm}} supports the following versions of {{site.data.keyword.openshiftshort}}. The worker node operating system is Red Hat Enterprise Linux 7.

* **Latest**: 4.6 (Kubernetes 1.19)
* **Default**: 4.5 (Kubernetes 1.18)
* **Other**: 4.4 (Kubernetes 1.17)
* **Deprecated**: 3.11 (Kubernetes 1.11), 4.3 (Kubernetes 1.16)

To check the Kubernetes server version of a cluster, log in to the cluster and run the following command.

```
oc version
```
{: pre}

Example output:
```
Client Version: 4.5.3
Server Version: 4.5.12
Kubernetes Version: v1.18.2
```
{: screen}

## Release history
{: #openshift_release_history}

The following table records {{site.data.keyword.openshiftlong_notm}} version release history. You can use this information for planning purposes, such as to estimate general time frames when a certain release might become unsupported.
{: shortdesc}

**How soon after an OCP release is the version available in {{site.data.keyword.cloud_notm}}?**

After the Red Hat OpenShift Container Platform community releases a version update, the IBM team begins a process of hardening and testing the release for {{site.data.keyword.openshiftlong_notm}} environments. Availability and unsupported release dates depend on the results of these tests, community updates, security patches, and technology changes between versions. Plan to keep your cluster master and worker node version up-to-date.

**Why is the deprecated version 3.11 supported longer than more recent versions like 4.3?**

In general, the last minor version of a major version is supported longer than other minor versions. Because you cannot update a cluster from one major version to another (such as version 3 to 4), this longer support period gives you time to create clusters at a more recent version. Minor versions of a more recent major version might become unsupported before the last minor version of a deprecated major version because the more recent major version has subsequent minor releases that are supported. For example, version 4.3 becomes unsupported before the deprecated version 3.11 because version 4 has future minor releases, but 3.11 is the last minor version of version 3.

**What is different for deprecated versions?**

Your apps still run, and you can log in to the cluster to manage your {{site.data.keyword.openshiftshort}} resources. You can still manage your cluster lifecycle, such as by adding and reloading worker nodes. However, security patch updates might not be provided. To continue receiving important security updates and the latest functionality, create a cluster at a supported version. You receive a notification in the console and CLI to update your cluster to a supported version about 45 days before the deprecated version becomes unsupported.

Dates that are marked with a dagger (`†`) are tentative and subject to change.
{: important}

<table summary="This table shows the release history for {{site.data.keyword.openshiftlong_notm}}.">
<caption>Release history for {{site.data.keyword.openshiftlong_notm}}.</caption>
<col width="20%" align="center">
<col width="20%">
<col width="30%">
<col width="30%">
<thead>
<tr>
<th>Supported?</th>
<th>{{site.data.keyword.openshiftshort}} / Kubernetes version</th>
<th>{{site.data.keyword.openshiftlong_notm}}<br>release date</th>
<th>{{site.data.keyword.openshiftlong_notm}}<br>unsupported date</th>
</tr>
</thead>
<tbody>
<tr>
  <td><img src="images/checkmark-filled.png" align="left" width="32" style="width:32px;" alt="This version is supported."/></td>
  <td>4.6 / 1.19</td>
  <td>17 Feb 2021</td>
  <td>Nov 2021 `†`</td>
</tr>
<tr>
  <td><img src="images/checkmark-filled.png" align="left" width="32" style="width:32px;" alt="This version is supported."/></td>
  <td>4.5 / 1.18</td>
  <td>13 Oct 2020</td>
  <td>Aug 2021 `†`</td>
</tr>
<tr>
  <td><img src="images/checkmark-filled.png" align="left" width="32" style="width:32px;" alt="This version is supported."/></td>
  <td>4.4 / 1.17</td>
  <td>21 Jul 2020</td>
  <td>31 May 2021 `†`</td>
</tr>
<tr>
  <td><img src="images/warning-filled.png" align="left" width="32" style="width:32px;" alt="This version is deprecated."/></td>
  <td>4.3 / 1.16</td>
  <td>20 Apr 2020</td>
  <td>7 Mar 2021 `†`</td>
</tr>
<tr>
  <td><img src="images/warning-filled.png" align="left" width="32" style="width:32px;" alt="This version is deprecated."/></td>
  <td>3.11 / 1.11</td>
  <td>01 Aug 2019</td>
  <td>Jun 2022 `†`</td>
</tr>
</tbody>
</table>

<br />

## {{site.data.keyword.openshiftshort}} 4.6
{: #ocp46}



Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) that runs {{site.data.keyword.openshiftshort}} 4.5 to {{site.data.keyword.openshiftshort}} 4.6.
{: shortdesc}

### Update before master
{: #46_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- |
| **Unsupported:** Deprecated and removed {{site.data.keyword.openshiftshort}} features | For more information, review the [OpenShift version 4.6 deprecated and removed features](https://docs.openshift.com/container-platform/4.6/release_notes/ocp-4-6-release-notes.html#ocp-4-6-deprecated-removed-features){: external}. |
{: caption="Changes to make before you update the master to {{site.data.keyword.openshiftshort}} 4.6" caption-side="top"}
{: summary="The rows are read from left to right. The type of update action is in the first column, and a description of the update action type is in the second column."}

<br />

## {{site.data.keyword.openshiftshort}} 4.5
{: #ocp45}

<img src="images/certified_kubernetes_1x18.png" style="padding-right: 10px;" align="left" alt="This badge indicates Kubernetes version 1.18 certification for {{site.data.keyword.openshiftlong_notm}}."/> {{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.18 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) that runs {{site.data.keyword.openshiftshort}} 4.4 to {{site.data.keyword.openshiftshort}} 4.5.
{: shortdesc}

You cannot update a cluster that runs 3.11 to a version 4 cluster. [Create a cluster](/docs/openshift?topic=openshift-clusters) and [copy your deployments](/docs/openshift?topic=openshift-update_app#copy_apps_cluster) from the outdated cluster to the new cluster.
{: important}

### Update before master
{: #45_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- |
| {{site.data.keyword.openshiftshort}} update requirements | {{site.data.keyword.openshiftlong_notm}} cluster master updates require worker nodes to be at most 1 minor version behind the cluster master version (`n-1`). Additionally, for cluster master updates to version 4.5, all worker nodes in the cluster must run at least version `4.4.23`. Ensure your workers nodes are running the latest patch version before updating your cluster master. |
| **Unsupported:** Deprecated and removed {{site.data.keyword.openshiftshort}} features | For more information, review the [OpenShift version 4.5 deprecated and removed features](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-deprecated-removed-features){: external}. |
{: caption="Changes to make before you update the master to {{site.data.keyword.openshiftshort}} 4.5" caption-side="top"}
{: summary="The rows are read from left to right. The type of update action is in the first column, and a description of the update action type is in the second column."}

### Update after master
{: #45_after}

The following table shows the actions that you must take after you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- |
| Elasticsearch version upgrade for cluster logging | For more information, see the Elasticsearch version upgrade notes in the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-elasticsearch-6){: external}. |
| Image registry configuration | New version 4.5 clusters that run on the VPC Gen 2 infrastructure provider and use {{site.data.keyword.cos_full_notm}} now proxy container image traffic through the internal registry pods directly to the {{site.data.keyword.cos_short}} endpoints. To configure this proxying for version 4.5 clusters that were updated from a previous version, see [the troubleshooting topic](/docs/openshift?topic=openshift-cs_troubleshoot_app#ts-app-ocr-vpc-push). |
| **Unsupported**: `kubelet` statistics | The `kubelet` statistics that were available via the `/stats` endpoint are unsupported and removed. The cluster insights panel in the cluster console no longer reports statistics from this endpoint. |
| Temporary `oc` and `kubectl` latency | RBAC operations are now performed asynchronously. After you run `ibmcloud oc cluster config` for the first time after the update, `oc` and `kubectl` commands might fail for a few seconds while RBAC synchronizes for the first time. Afterward, `oc` and `kubectl` commands perform as expected. If you use automation to access the cluster with `oc` and `kubectl` commands, add retry logic for `oc` and `kubectl` commands after a `kubeconfig` file is successfully retrieved. |
| `oc adm policy` | The `oc adm policy` commands now manage role-based access control (RBAC) resources rather than modifying security context constraints (SCCs) directly for managing permissions within the cluster. Update any components that rely on direct changes to SCCs to use RBAC to manage permissions. |
| `oc new-app` | For more information, see the `oc new-app` deployment resources notes in the [{{site.data.keyword.openshiftshort}} release notes](https://docs.openshift.com/container-platform/4.5/release_notes/ocp-4-5-release-notes.html#ocp-4-5-oc-new-app-deployment-resources){: external}. |
{: caption="Changes to make after you update the master to {{site.data.keyword.openshiftshort}} 4.5" caption-side="top"}
{: summary="The rows are read from left to right. The type of update action is in the first column, and a description of the update action type is in the second column."}

<br />

## {{site.data.keyword.openshiftshort}} 4.4
{: #ocp44}

<img src="images/certified_kubernetes_1x17.png" style="padding-right: 10px;" align="left" alt="This badge indicates Kubernetes version 1.17 certification for {{site.data.keyword.openshiftlong_notm}}."/> {{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.17 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

Review changes that you might need to make when you [update a cluster](/docs/openshift?topic=openshift-update) that runs {{site.data.keyword.openshiftshort}} 4.3 to {{site.data.keyword.openshiftshort}} 4.4.
{: shortdesc}

With {{site.data.keyword.openshiftshort}} 4.4, you get access to Kubernetes version 1.17 APIs that enable features such as [key management service (KMS)](/docs/openshift?topic=openshift-encryption#keyprotect) integration. For more information, see the [{{site.data.keyword.cloud_notm}} blog](https://www.ibm.com/cloud/blog/announcements/openshift-version-44-now-available-in-red-hat-openshift-on-ibm-cloud){: external}.

You cannot update a cluster that runs 3.11 to a version 4 cluster. [Create a cluster](/docs/openshift?topic=openshift-clusters) and [copy your deployments](/docs/openshift?topic=openshift-update_app#copy_apps_cluster) from the outdated cluster to the new cluster.
{: important}

### Update before master
{: #44_before}

The following table shows the actions that you must take before you [update the cluster master](/docs/openshift?topic=openshift-update#master).
{: shortdesc}

| Type | Description |
| ---- | ----------- |
| Add-ons and plug-ins | For each add-on and plug-in that you installed in your cluster, check for any impacts that might be caused by updating the cluster version. For instructions, see [Steps to update the cluster master](/docs/containers?topic=containers-update#master-steps) and refer to the add-on and plug-in documentation. |
| Temporary `oc` and `kubectl` latency | RBAC operations are now performed asynchronously. After you run `ibmcloud oc cluster config` for the first time after the update, `oc` and `kubectl` commands might fail for a few seconds while RBAC synchronizes for the first time. Afterward, `oc` and `kubectl` commands perform as expected. If you use automation to access the cluster with `oc` and `kubectl` commands, add retry logic for `oc` and `kubectl` commands after a `kubeconfig` file is successfully retrieved. |
| **Unsupported:** Deprecated Kubernetes APIs are removed | Although Kubernetes version 1.16 removed several common, deprecated Kubernetes APIs, {{site.data.keyword.openshiftshort}} version 4.3, which is based on Kubernetes version 1.16, kept these APIs enabled. Now, {{site.data.keyword.openshiftshort}} version 4.4, which is based on Kubernetes version 1.17, removes these Kubernetes APIs that were removed in the Kubernetes 1.16 project. You can take the following steps to mitigate impact to your Kubernetes resources. Note that the blog was written specifically for {{site.data.keyword.containerlong_notm}} clusters, but the tips apply to {{site.data.keyword.openshiftlong_notm}}, too.<ol><li>Follow the [blog update tips](https://www.ibm.com/cloud/blog/announcements/kubernetes-version-1-16-removes-deprecated-apis){: external}.</li><li>Update the configuration files for any impacted Kubernetes resources, such as daemon sets, deployments, replica sets, stateful sets, and network policies.</li><li>If you [add services to your cluster by using Helm charts](/docs/openshift?topic=openshift-helm), update to Helm version 2.15.2 or later.</li></ol>|
| **Unsupported:** Deprecated and removed {{site.data.keyword.openshiftshort}} features | For more information, review the [{{site.data.keyword.openshiftshort}} version 4.4 deprecated and removed features](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-deprecated-removed-features). |
| Kubernetes API server checks client certificates before tokens | For more information, review [`kube-apiserver` checks client certificates before tokens](https://docs.openshift.com/container-platform/4.4/release_notes/ocp-4-4-release-notes.html#ocp-4-4-kube-apiserver-check-certs-before-tokens). |
{: caption="Changes to make before you update the master to {{site.data.keyword.openshiftshort}} 4.4" caption-side="top"}
{: summary="The rows are read from left to right. The type of update action is in the first column, and a description of the update action type is in the second column."}

## Deprecated: {{site.data.keyword.openshiftshort}} 4.3
{: #ocp43}

<img src="images/certified_kubernetes_1x16.png" style="padding-right: 10px;" align="left" alt="This badge indicates Kubernetes version 1.16 certification for {{site.data.keyword.openshiftlong_notm}}."/> {{site.data.keyword.openshiftlong_notm}} is a Certified Kubernetes product for version 1.16 under the CNCF Kubernetes Software Conformance Certification program. _Kubernetes® is a registered trademark of The Linux Foundation in the United States and other countries, and is used pursuant to a license from The Linux Foundation._

{{site.data.keyword.openshiftshort}} version 4.3 is deprecated, and becomes unsupported 7 March 2021 (date subject to change). [Update your clusters](/docs/openshift?topic=openshift-update) to at least {{site.data.keyword.openshiftshort}} version 4.4 as soon as possible.
{: deprecated}

With the release of OpenShift Container Platform 4.3, you get a new experience and capabilities for managing your cluster and its workloads. For more information, see the [{{site.data.keyword.openshiftshort}} blog](https://www.openshift.com/blog/introducing-red-hat-openshift-4-3-to-enhance-kubernetes-security/){: external}.
{: shortdesc}

To create a 4.3 cluster, [try out the tutorial](/docs/openshift?topic=openshift-openshift_tutorial). You cannot update an existing version 3.11 cluster to a 4.3 cluster. Create a cluster and [copy your deployments](/docs/openshift?topic=openshift-update_app#copy_apps_cluster) from the outdated cluster to the new cluster.

Review the following benefit highlights when you use version 4.3 clusters.
*   Ability to use your own [Operators](/docs/openshift?topic=openshift-operators) or operators that are provided by the OperatorHub to package and deploy services for your cluster.
*   New [{{site.data.keyword.openshiftshort}} web console experience](/docs/openshift?topic=openshift-openshift_tutorial#openshift_oc_console) that reorganizes your cluster resources and workflows into two perspectives for the **Administrator** and **Developer**.
*   Update of the underlying Kubernetes API to 1.16 so that you can use new capabilities such as extensibility for core Kubernetes APIs, an updated `kubectl` experience, cluster lifecycle stability enhancements, support for projects such as `kustomize`, persistent local volumes, and custom resource and operator support.
*   [Ingress controllers are integrated into the Ingress Operator](/docs/openshift?topic=openshift-ingress-about-roks4) so that you can use routers to proxy app requests instead of application load balancers (ALBs).

For more information, check out the [comparison table between supported features of 3.11 and 4](/docs/openshift?topic=openshift-cs_ov#3.11_vs_4.3) or review the [service limitations](/docs/openshift?topic=openshift-openshift_limitations#ocp4_limitations).

<br />
