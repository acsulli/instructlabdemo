Installing OpenShift Virtualization - Installing \|
Virtualization \| OpenShift Container Platform
4.15

> Installing OpenShiftVirtualization
>
> <u>Installing the OpenShift Virtualization Operator</u>
>
> <u>Installing the OpenShift Virtualization Operator by using the web
> console</u> <u>Installing the OpenShift Virtualization Operator b</u>y
> <u>using</u> <u>the command</u> <u>line</u>
>
> <u>Next steps</u>
>
> Install OpenShift Virtualization to add virtualization functionality
> to your OpenShift Container Platform cluster.
>
> If you install OpenShift Virtualization in a restricted environment
>
> with no internet connectivity, you must [<u>configure
> Operator</u>](https://docs.openshift.com/container-platform/4.15/operators/admin/olm-restricted-networks.html#olm-restricted-networks)
>  [<u>Lifecycle Manager (OLM) for restricted
> networks</u>.](https://docs.openshift.com/container-platform/4.15/operators/admin/olm-restricted-networks.html#olm-restricted-networks)
>
> If you have limited internet connectivity, you can [<u>configure
> prox</u>y](https://docs.openshift.com/container-platform/4.15/operators/admin/olm-configuring-proxy-support.html#olm-configuring-proxy-support)
>
> [<u>support in
> OLM</u>](https://docs.openshift.com/container-platform/4.15/operators/admin/olm-configuring-proxy-support.html#olm-configuring-proxy-support)
> to access the OperatorHub.
>
> Installing theOpenShiftVirtualizationOperator
>
> Install the OpenShift Virtualization Operator by using the OpenShift
> Container Platform web console or the command line.
>
> Installing theOpenShiftVirtualizationOperatorby usingthe webconsole
>
> You can deploy the OpenShift Virtualization Operator by using the
> OpenShift Container Platform web console.
>
> Prerequisites
>
> Install OpenShift Container Platform 4.15 on your cluster.

https://docs.openshift.com/container-platform/4.15/virt/install/installing-virt.html#virt-installing-virt-operator_installing-virt
1/6

Installing OpenShift Virtualization - Installing \|
Virtualization \| OpenShift Container Platform 4.15

> Log in to the OpenShift Container Platform web console as a user with
> cluster-admin permissions.
>
> Procedure
>
> From the Administrator perspective, click Operators → OperatorHub.
>
> In the Filter by keyword field, type Virtualization.
>
> Select the OpenShift Virtualization Operator tile with the Red Hat
> source label.
>
> Read the information about the Operator and click Install.
>
> On the Install Operator page:
>
> Select stable from the list of available Update Channel options. This
> ensures that you install the version of OpenShift Virtualization that
> is compatible with your OpenShift Container Platform version.
>
> For Installed Namespace, ensure that the Operator recommended
> namespace option is selected. This installs the Operator in the
> mandatory openshift-cnv namespace, which is automatically created if
> it does not exist.
>
> Attempting to install the OpenShift Virtualization  Operator in a
> namespace other than openshift-cnv
>
> causes the installation to fail.
>
> For Approval Strategy, it is highly recommended that you select
> Automatic, which is the default value, so that OpenShift
> Virtualization
>
> automatically updates when a new version is available in the stable
> update channel.
>
> While it is possible to select the Manual approval strategy, this is
> inadvisable because of the high risk that it presents to the
> supportability and functionality of your cluster. Only select Manual
> if you fully understand these risks and cannot use Automatic.

https://docs.openshift.com/container-platform/4.15/virt/install/installing-virt.html#virt-installing-virt-operator_installing-virt
2/6

 Installing OpenShift Virtualization - Installing \|
Virtualization \| OpenShift Container Platform 4.15

> 

Because OpenShift Virtualization is only supported when used with the
corresponding OpenShift Container Platform version, missing OpenShift
Virtualization

updates can cause your cluster to become unsupported.

> Click Install to make the Operator available to the openshift-cnv
> namespace.
>
> When the Operator installs successfully, click Create HyperConverged.
>
> Optional: Configure Infra and Workloads node placement options for
> OpenShift Virtualization components.
>
> Click Create to launch OpenShift Virtualization.
>
> Verification
>
> Navigate to the Workloads → Pods page and monitor the OpenShift
> Virtualization pods until they are all Running. After all the pods
> display the
>
> Running state, you can use OpenShift Virtualization.
>
> Installing theOpenShiftVirtualizationOperatorby usingthe commandline
>
> Subscribe to the OpenShift Virtualization catalog and install the
> OpenShift Virtualization Operator by applying manifests to your
> cluster.
>
> Subscribing totheOpenShiftVirtualizationcatalogby using theCLI
>
> Before you install OpenShift Virtualization, you must subscribe to the
> OpenShift Virtualization catalog. Subscribing gives the openshift-cnv
> namespace access to the OpenShift Virtualization Operators.
>
> To subscribe, configure Namespace , OperatorGroup , and Subscription
> objects by applying a single manifest to your cluster.
>
> Prerequisites
>
> Install OpenShift Container Platform 4.15 on your cluster.
>
> Install the OpenShift CLI ( oc ).

https://docs.openshift.com/container-platform/4.15/virt/install/installing-virt.html#virt-installing-virt-operator_installing-virt
3/6

 Installing OpenShift Virtualization - Installing \|
Virtualization \| OpenShift Container Platform 4.15

> Log in as a user with cluster-admin privileges.
>
> Procedure
>
> Create a YAML file that contains the following manifest:
>
> apiVersion: v1 kind: Namespace metadata:
>
> name: openshift-cnv ---
>
> apiVersion: operators.coreos.com/v1 kind: OperatorGroup
>
> metadata:
>
> name: kubevirt-hyperconverged-group namespace: openshift-cnv
>
> spec: targetNamespaces:
>
> \- openshift-cnv ---
>
> apiVersion: operators.coreos.com/v1alpha1 kind: Subscription
>
> metadata:
>
> name: hco-operatorhub namespace: openshift-cnv
>
> spec:
>
> source: redhat-operators sourceNamespace: openshift-marketplace name:
> kubevirt-hyperconverged
>
> startingCSV: kubevirt-hyperconverged-operator.v4.15.2 channel:
> "stable" **(1)**
>
> Using the stable channel ensures that you install the version of
>
> 1 OpenShift Virtualization that is compatible with your OpenShift
> Container Platform version.
>
> Create the required Namespace , OperatorGroup , and Subscription
> objects for OpenShift Virtualization by running the following command:
>
> \$ oc apply -f \<file name\>.yaml
>
>  You can [<u>configure certificate
> rotation</u>](https://docs.openshift.com/container-platform/4.15/virt/virtual_machines/advanced_vm_management/virt-configuring-certificate-rotation.html#virt-configuring-certificate-rotation)
> parameters in the YAML file.

https://docs.openshift.com/container-platform/4.15/virt/install/installing-virt.html#virt-installing-virt-operator_installing-virt
4/6

05/06/2024, 14:37 Installing OpenShift Virtualization - Installing \|
Virtualization \| OpenShift Container Platform 4.15

> Deploying theOpenShiftVirtualizationOperatorby usingthe CLI
>
> You can deploy the OpenShift Virtualization Operator by using the oc
> CLI.
>
> Prerequisites
>
> Subscribe to the OpenShift Virtualization catalog in the openshift-cnv
> namespace.
>
> Log in as a user with cluster-admin privileges.
>
> Procedure
>
> Create a YAML file that contains the following manifest:
>
> apiVersion: hco.kubevirt.io/v1beta1 kind: HyperConverged
>
> metadata:
>
> name: kubevirt-hyperconverged namespace: openshift-cnv
>
> spec:
>
> Deploy the OpenShift Virtualization Operator by running the following
> command:
>
> \$ oc apply -f \<file_name\>.yaml
>
> Verification
>
> Ensure that OpenShift Virtualization deployed successfully by watching
> the PHASE of the cluster service version (CSV) in the openshift-cnv
>
> namespace. Run the following command:
>
> \$ watch oc get csv -n openshift-cnv
>
> The following output displays if deployment was successful:
>
> Example output
>
> NAME DISPLAY VERSION REPLACES PHASE
>
> kubevirt-hyperconverged-operator.v4.15.2 OpenShift Virtualization
> 4.15.2 Succeeded

https://docs.openshift.com/container-platform/4.15/virt/install/installing-virt.html#virt-installing-virt-operator_installing-virt
5/6

Installing OpenShift Virtualization - Installing \|
Virtualization \| OpenShift Container Platform 4.15

> Nextsteps
>
> The [<u>hostpath
> provisioner</u>](https://docs.openshift.com/container-platform/4.15/virt/storage/virt-configuring-local-storage-with-hpp.html#virt-creating-hpp-basic-storage-pool_virt-configuring-local-storage-with-hpp)
> is a local storage provisioner designed for OpenShift Virtualization.
> If you want to configure local storage for virtual machines, you must
> enable the hostpath provisioner first.

https://docs.openshift.com/container-platform/4.15/virt/install/installing-virt.html#virt-installing-virt-operator_installing-virt
6/6
