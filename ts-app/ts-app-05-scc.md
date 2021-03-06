---

copyright:
  years: 2014, 2020
lastupdated: "2020-09-17"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Why does pod not build with a permission denied error because of security context constraint (SCC)?
{: #ts-app-scc}
{: troubleshoot}

**Infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

{: tsSymptoms}
A system pod or other pod that uses a security context constraint (SCC) has an operation that keeps retrying but fails with a `permission denied` error. For example, you might log in to the internal `image-registry` pod and try to run `docker push`.

Example error message when pushing an image to the internal registry:
```
error: build error: Failed to push image: error copying layers and metadata
```
{: screen}

{: tsCauses}
The pod might use an SCC or belong to a system group that uses an SCC without the correct permission. You might have added a system group to an SCC by running `oc adm policy add-scc-to-group <scc> system:<group>`. If the pod mounts a volume, the pod's permissions that are authorized by the SCC might no longer allow the pod to read or write data to the volume.

For example, the internal registry mounts a volume to read and write image data to a file storage instance. If the `system:authenticated` group that the internal registry belongs to changes the SCC from `restricted` to `anyuid`, then the pod runs with a different UID. The different UID prevents the internal registry pod from pushing or pulling images from the storage device.

{: tsResolve}
Change the pod's SCC permissions.

1.  Describe the pod and check the `openshift.io/scc: <scc>` security context constraint in the **Annotations** section.
    ```
    oc describe pod -n <project> <pod>
    ```
    {: pre}

    Example output:
    ```
    Name:               image-registry-1234567
    Namespace:          openshift-image-registry
    Priority:           2000000000
    PriorityClassName:  system-cluster-critical
    Node:               10.xxx.xx.xxx/10.xxx.xx.xxx
    Start Time:         Wed, 19 Feb 2020 15:38:53 -0500
    Labels:             docker-registry=default
    Annotations:        openshift.io/scc: anyuid
    ```
    {: screen}
2.  Describe the security context constraint and check the user and groups in the **Access** section.
    ```
    oc describe scc <scc>
    ```
    {: pre}

    Example output:
    ```
    Name:						anyuid
    Priority:					<none>
    Access:						
        Users:					<none>
        Groups:					system:authenticated
    ```
    {: screen}
3.  If you do not want the user or group to have the permissions of the SCC, remove the user or group from the SCC. For more information, review the default [{{site.data.keyword.openshiftshort}}](/docs/openshift?topic=openshift-openshift_scc#oc_sccs) and [{{site.data.keyword.cloud_notm}}](/docs/openshift?topic=openshift-openshift_scc#ibm_sccs) SCCs that are set in the cluster.
    ```
    oc adm policy remove-scc-from-group <scc> <(user|group)>
    ```
    {: pre}
4.  Add the user or group to the SCC with the appropriate permissions.
    ```
    oc adm policy add-scc-to-group <scc> <(user|group)>
    ```
    {: pre}
5.  Delete the pod so that the pod is rescheduled with the new SCC permissions.
    ```
    oc delete pod -n <project> <pod>
    ```
    {: pre}