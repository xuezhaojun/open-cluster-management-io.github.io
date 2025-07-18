---
title: Releases
weight: 6
---

Open Cluster Management has approximately a three to four month release cycle. The current release is `v1.0.0`.
Continue reading to view upcoming releases:

## `1.0.0`, 20 June 2025

🎉 **Milestone Release: Open Cluster Management v1.0.0** 🎉

The Open Cluster Management team is thrilled to announce the release of OCM v1.0.0! This milestone release
represents a significant achievement in our journey to provide a robust, production-ready multi-cluster management
platform. With enhanced stability, new powerful features, and improved developer experience, v1.0.0 marks OCM's
readiness for enterprise-scale deployments.

### 🌟 Key Highlights

**Enhanced Cluster Management:**
- **CEL Selector Support**: Advanced cluster selection using Common Expression Language (CEL) for more
flexible and powerful placement decisions
- **About-API Integration**: New cluster properties API enabling better cluster discovery and
metadata management
- **Workload Conditions**: Enhanced status reporting with detailed workload condition tracking
- **Deletion Policies**: Introduced deletionPolicy for ManifestWorkReplicaSets to control the deletion strategy.

**Developer Experience Improvements:**
- **Resource Requirements Configuration**: Fine-grained control over addon agent resource requirements
- **Bundle Version Overrides**: Flexible version management with `--bundle-version-overrides` flag in clusteradm
- **ManagedCluster Annotations**: Expose cluster annotations during join operations for better cluster labeling

**Stability & Performance:**
- **Resource Cleanup**: ResourceCleanup feature gate enabled by default for better resource lifecycle management
- **Configurable Status Sync**: Adjustable work status sync intervals for optimized performance
- **Memory Usage Optimization**: Reduced memory footprint through filtered resource watching
- **Hub QPS/Burst Configuration**: Configurable rate limiting for better hub cluster protection

**ArgoCD Integration:**
- **ArgoCD Pull Model**: New ArgoCD pull model addon replacing the legacy application-manager
- **Simplified Setup**: Enhanced clusteradm CLI support for easier ArgoCD integration setup

### 🔧 Breaking Changes

- **ResourceCleanup Feature Gate**: Now enabled by default - ensures proper cleanup of resources when ManifestWorks are deleted
- **Lease Checking Removal**: Removed hub-side lease checking for improved performance
- **API Updates**: Several API fields made optional for better flexibility (hubAcceptsClient, taint timeAdded)

### 📊 Community Growth

This release includes contributions from **25 contributors** across all repositories, with **8 new contributors** joining our community:

**New Contributors:**
- [@gnana997](https://github.com/gnana997) - API improvements and sigs.k8s.io support
- [@Ankit152](https://github.com/Ankit152) - Go 1.23 upgrade and k8s.io packages updates
- [@o-farag](https://github.com/o-farag) - ClusterClaimConfiguration API enhancements
- [@bhperry](https://github.com/bhperry) - Workload conditions and CEL evaluation functions
- [@gitatractivo](https://github.com/gitatractivo) - Helm chart implementation and documentation
- [@jeffw17](https://github.com/jeffw17) - Sync labels support and AWS IRSA documentation
- [@ivan-cai](https://github.com/ivan-cai) - Hub QPS/Burst configuration improvements
- [@arturshadnik](https://github.com/arturshadnik) - ManagedCluster annotations support
- [@ahmad-ibra](https://github.com/ahmad-ibra) - AWS EKS managed cluster ARN support

We extend our heartfelt gratitude to all contributors who made this milestone release possible!

### 📦 Core Components

- **api** v1.0.0 [changelog](https://github.com/open-cluster-management-io/api/releases/tag/v1.0.0)
- **ocm** v1.0.0 [changelog](https://github.com/open-cluster-management-io/ocm/releases/tag/v1.0.0)
- **addon-framework** v1.0.0 [changelog](https://github.com/open-cluster-management-io/addon-framework/releases/tag/v1.0.0)
- **clusteradm** v1.0.0 [changelog](https://github.com/open-cluster-management-io/clusteradm/releases/tag/v1.0.0)

We hope this release helps you better manage your Kubernetes clusters, and we look forward to your feedback and
contributions! If you have any questions, please don’t hesitate to contact us in our community channels or log issues
on our repositories.

Thank you to all contributors for your hard work and to the community for your continued support!
Let's keep the momentum going.

Stay connected and happy managing clusters!

---

## `0.16.0`, 16 March 2025
The Open Cluster Management team is exicted to announce the release of OCM v0.16.0 with many new
features:

Breaking Changes:
- Addon is defaulted to be managed by addon-manager: this is the part of addon evolution work starting
  from release 0.14.0, and the self-managed installation of addons is disabled in `v0.16.0`. Each addon
  will need to upgrade the addon-framework to a version equal or higher than `v0.8.2`
- (Policy framework) The compliance history API has been removed due to lack of interest.
- (Policy framework) Kubernetes v1.16 is no longer supported with the removal of the `v1beta1`
  CustomResourceDefinition manifests.

Notable features:
- Register cluster to EKS hub: user can now use an EKS cluster as a hub cluster and register other
  EKS clusters with it, utilizing [EKS IRSA](https://docs.aws.amazon.com/eks/latest/userguide/iam-roles-for-service-accounts.html)
  and [EKS Access Entries](https://docs.aws.amazon.com/eks/latest/userguide/access-entries.html) features in AWS,
  see this [doc](https://github.com/open-cluster-management-io/ocm/tree/main/solutions/joining-hub-and-spoke-with-aws-auth)
  on how to enable and use this feature.
- Auto register CAPI cluster: user can install the CAPI management plane on the OCM hub, and enable
  the `ClusterImporter` feature gate on the `ClusterManager`. The CAPI cluster after successfully provisioned
  will be automatically registered into the OCM hub.
- Ignore fields update in `ManifestWorks`: when user uses the `ServerSideApply` strategy in Manifestwork, user
  can now specify certain fields to be ignored during resource update/override, to avoid apply conflict error.
- Support wildcard of ManifestConfigs in `ManifestWorks`: the `ResourceIdentifier` field in `ManifestWorks` can
  now recognize `*` as the wildcard marker, so if there are multiple resources need to use the same `ManifestConfigs`,
  user can now set one `ManifestConfig` with a wildcard `ResourceIdentifier`
- (Policy framework) `OperatorPolicy`: Enhanced operator handling, including approving dependent packages and raising
  operator deprecation.
- (Policy framework) `ConfigurationPolicy`: An `objectSelector` is added, allowing users to iterate over objects by
  label without needing `object-templates-raw`. For further filtering, users can invoke the `{{ skipObject }}` Go
  template function to conditionally skip a particular object template.
- (Policy framework) `ConfigurationPolicy`: The `ObjectName` and `ObjectNamespace` Go template variables are added.
  The `ObjectNamespace` inherits its value from the `namespaceSelector` while the `ObjectName` inherits its value
  from the new `objectSelector`.
- (Policy framework) The new `governance-standalone-hub-templating` addon enables hub Go templates
  (i.e. `{{hub ... hub}}`) for "standalone" policies. This new addon is a further enablement for users to deploy
  policies using GitOps pointed directly at managed clusters rather that propagating policies through the hub.

### Core components
- ocm v0.16.0 [changelog](https://github.com/open-cluster-management-io/ocm/releases/tag/v0.16.0)
- addon-framework v0.12.0 [changelog](https://github.com/open-cluster-management-io/addon-framework/releases/tag/v0.12.0)
- clusteradm v0.11.0 [changelog](https://github.com/open-cluster-management-io/clusteradm/releases/tag/v0.11.0)

### Addons
- config-policy-controller v0.16.0 [changelog](https://github.com/open-cluster-management-io/config-policy-controller/releases/tag/v0.16.0)
- governance-policy-framework-addon v0.16.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-framework-addon/releases/tag/v0.16.0)
- governance-policy-propagator v0.16.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-propagator/releases/tag/v0.16.0)
- governance-policy-addon-controller v0.16.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-addon-controller/releases/tag/v0.16.0)
- multicloud-operators-subscription v0.16.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-subscription/releases/tag/v0.16.0)
- multicloud-operators-channel v0.16.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-channel/releases/tag/v0.16.0)
- managed-serviceaccount v0.8.0 [changelog](https://github.com/open-cluster-management-io/managed-serviceaccount/releases/tag/v0.8.0)
- cluster-proxy v0.7.0 [changelog](https://github.com/open-cluster-management-io/cluster-proxy/releases/tag/v0.7.0)


## `0.15.0`, 24 Oct. 2024

The Open Cluster Management team is proud to announce the release of OCM v0.15.0!

- Cluster Manager and Klusterlet helm chart: user can now install cluster manager and klusterlet using helm by
  adding the `https://open-cluster-management.io/helm-charts` into the helm repo.
- Multiple hubs: by enabling the `MultipleHubs` feature gate on the klusterlet, the klusterlet can switch
  the connection among multiple hubs if the hub server is down, or when user explictly sets `hubAcceptClient` to `false`
  on the `ManagedCluster`. See [solution](https://github.com/open-cluster-management-io/ocm/tree/main/solutions/multiplehubs)
  on how to use this feature to handle disaster recovery.
- Addon support multiple configurations with the same kind: user can now set multiple configurations
  with the same kind on the `ManagedClusterAddon` and `ClusterManagementAddon`. Which specific configuration
  is used by the addon is decided by the addon.
- Add configured condition in `ManagedClusterAddon`: the addon-manager will set condition with the type of `Configured`
  on the `ManagedClusterAddon` when the configuration of the addon is determined by the addon-manager. This is to avoid
  an out of date configuration being picked to deploy the addon agent.
- Sync between ManagedCluster and cluster inventory API: We introduce the cluster inventory API
  from sig-multicluster and sync between ManagedCluster and ClusterProfile API. See
  [here](https://github.com/kubernetes-sigs/cluster-inventory-api) for more details on cluster inventory API.
- (Policy framework) Event-driven `ConfigurationPolicy` evaluations: By default, `ConfigurationPolicy` reconciles are
  now event-driven, lowering resource consumption and increasing efficiency. Users can set a policy to reconcile on an
  interval as they were previously by configuring `spec.evaluationInterval`.
- (Policy framework) Custom `ConfigurationPolicy` compliance messages: Policy authors can now define Go templates to be
  used for compliance messages, including `.DefaultMessage` and `.Policy` fields available for parsing relevant information.
- (Policy framework) `dryrun` CLI: A `dryrun` CLI is available to reconcile `ConfigurationPolicy` locally, allowing you
  to view the compliance and diff resulting from a `ConfigurationPolicy` without deploying it to a cluster:
  ```
  go install open-cluster-management.io/config-policy-controller/cmd/dryrun@latest
  ```
- (Policy framework) Customizable hub cluster template access: Users can now set `spec.hubTemplateOptions.serviceAccountName`
  to leverage a service account in the root policy namespace to resolve hub templates. Without the service account, hub
  templates are only able to access objects in the same namespace as the policy.

### Core components
- ocm v0.15.0 [changelog](https://github.com/open-cluster-management-io/ocm/releases/tag/v0.15.0)
- addon-framework v0.11.0 [changelog](https://github.com/open-cluster-management-io/addon-framework/releases/tag/v0.11.0)
- clusteradm v0.10.0 [changelog](https://github.com/open-cluster-management-io/clusteradm/releases/tag/v0.10.0)

### Addons
- config-policy-controller v0.15.0 [changelog](https://github.com/open-cluster-management-io/config-policy-controller/releases/tag/v0.15.0)
- governance-policy-framework-addon v0.15.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-framework-addon/releases/tag/v0.15.0)
- governance-policy-propagator v0.15.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-propagator/releases/tag/v0.15.0)
- governance-policy-addon-controller v0.15.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-addon-controller/releases/tag/v0.15.0)
- multicloud-operators-subscription v0.15.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-subscription/releases/tag/v0.15.0)
- multicloud-operators-channel v0.15.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-channel/releases/tag/v0.15.0)
- managed-serviceaccount v0.7.0 [changelog](https://github.com/open-cluster-management-io/managed-serviceaccount/releases/tag/v0.7.0)
- cluster-proxy v0.6.0 [changelog](https://github.com/open-cluster-management-io/cluster-proxy/releases/tag/v0.6.0)

## `0.14.0`, 21 Jun. 2024

The Open Cluster Management team is proud to announce the release of OCM v0.14.0!

- Exclude terminating clusters from PlacementDecision: now cluster in terminating state will not be picked by the
  placement.
- Send available condition events for managed cluster: klusterlet agent will send a Kubenerte event to the cluster
  namespace upon status change, which makes it eaiser for user to check the state change of the managed cluster.
- Set install namespace of AddonTemplate from AddonDeploymentConfig: consumers of AddonTemplate API can now use
  AddonDeploymentConfig API to set the installation namespace of the agent.
- Configurable controller replicas and master node selector: user can now set flags `--deployment-replicas` and
`--control-plane-node-label-selector` on klusterlet-operator to customize the replicas of the klusterlet agent.
- Add CAPI into join flow: user can now use the join command to add a Cluster API provisioned cluster into OCM hub
  from Cluster API management cluster with `--capi-import` and  `--capi-cluster-name` flag.
- (Policy Framework) `OperatorPolicy` enhancement and stabilization: OperatorPolicy can now be set to `mustnothave`
  to perform cleanup, alongside stabilization improvements.
- (Policy Framework) Add `ConfigurationPolicy` diff to the status: Adds a `recordDiff: InStatus` as the default value
  if it's not set. In this mode, the difference between the policy and the object on the managed is returned in the
  status. Sensitive data types are not displayed unless `InStatus` is explicitly provided.
- (Policy Framework) Add `recreateOption` to `ConfigurationPolicy`: When a user needs to update an object with
  immutable fields, the object must be replaced. In this case, `recreateOption` can be set to either `ifRequired` or
  `Always` depending on the requirements.

### Core components
- ocm v0.14.0 [changelog](https://github.com/open-cluster-management-io/ocm/releases/tag/v0.14.0)
- addon-framework v0.10.0 [changelog](https://github.com/open-cluster-management-io/addon-framework/releases/tag/v0.10.0)
- clusteradm v0.9.0 [changelog](https://github.com/open-cluster-management-io/clusteradm/releases/tag/v0.9.0)

### Addons
- config-policy-controller v0.14.0 [changelog](https://github.com/open-cluster-management-io/config-policy-controller/releases/tag/v0.14.0)
- governance-policy-framework-addon v0.14.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-framework-addon/releases/tag/v0.14.0)
- governance-policy-propagator v0.14.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-propagator/releases/tag/v0.14.0)
- governance-policy-addon-controller v0.14.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-addon-controller/releases/tag/v0.14.0)
- multicloud-operators-subscription v0.14.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-subscription/releases/tag/v0.14.0)
- multicloud-operators-channel v0.14.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-channel/releases/tag/v0.14.0)
- managed-serviceaccount v0.6.0 [changelog](https://github.com/open-cluster-management-io/managed-serviceaccount/releases/tag/v0.6.0)
- cluster-proxy v0.5.0 [changelog](https://github.com/open-cluster-management-io/cluster-proxy/releases/tag/v0.5.0)

## `0.13.0`, 6 Mar. 2024

The Open Cluster Management team is proud to announce the release of OCM v0.13.0! There are a bunch of new features
added into this release.

- Rollout API: we built a common rollout API that has been adopted in `ClusterManagementAddon` and `ManifestWorkReplicaSet`,
  and will be also used in the policy addon in a future release. The API provides users a way to define a workload/addon rolling upgrade strategy
  across multiple clusters. See [here](https://open-cluster-management.io/concepts/addon/#add-on-rollout-strategy) for more
  details.
- More install configurations in Klusterlet: we enhanced the `Klusterlet` API by adding more configuration fields, including
  resource requests, QPS/Burst and priority class.
- Cloudevent support: an experimental feature to wire the work agent with a message broker using the cloudevent protocol. This enables
  a work agent running in a highly scalable mode. See [here](
  https://github.com/open-cluster-management-io/enhancements/tree/main/enhancements/sig-architecture/224-event-based-manifestwork)
  for more details.
- Addon-framework is upgraded to v0.9.0 to better support the generic addon-manager and addon rolling out strategy. It is highly
  recommended for addons to upgrade the addon-framework dependency to version v0.8.1 or higher. Also, it should be noted that
  an RBAC update of the addon hub controller (adding PATCH verbs for resource `clustermanagementaddons`) is required during
  the upgrade.
- Application add-on `Subscription` API can now aggregate and report managed clusters' kustomization errors.
- New OperatorPolicy to handle OLM operators: A new OperatorPolicy is added, managed by the `config-policy-controller` Pod,
  aimed at easing the management of OLM deployments.
- (Policy framework) Add diff logging to `ConfigurationPolicy`: A `recordDiff` parameter is added to `ConfigurationPolicy`
  to enable the diff between the object on the cluster and the policy definition, to be logged in the `config-policy-controller` Pod logs.
- (Policy framework) New `OperatorPolicy` to handle OLM operators: A new OperatorPolicy is added, managed by the
  `config-policy-controller` Pod, aimed at easing the management of OLM deployments.
- (Policy framework) New Compliance History API: A Compliance History API is added to the policy framework. The compliance
  history in the policy on the cluster is limited to a non-configurable 10 statuses. The Compliance History API introduces
  a query-able database to keep track of history over a longer period as well as updates to a given policy.

### Core components
- ocm v0.13.0 [changelog](https://github.com/open-cluster-management-io/ocm/releases/tag/v0.13.0)
- clusteradm  v0.8.0 [changelog](https://github.com/open-cluster-management-io/clusteradm/blob/v0.8.0/CHANGELOG.md)

### Addons
- config-policy-controller v0.13.0 [changelog](https://github.com/open-cluster-management-io/config-policy-controller/releases/tag/v0.13.0)
- governance-policy-framework-addon v0.13.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-framework-addon/releases/tag/v0.13.0)
- governance-policy-propagator v0.13.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-propagator/releases/tag/v0.13.0)
- governance-policy-addon-controller v0.13.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-addon-controller/releases/tag/v0.13.0)
- multicloud-operators-subscription v0.13.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-subscription/releases/tag/v0.13.0)
- multicloud-operators-channel v0.13.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-channel/releases/tag/v0.13.0)
- multicloud-integrations v0.13.0 [changelog](https://github.com/open-cluster-management-io/multicloud-integrations/releases/tag/v0.13.0)
- managed-serviceaccount v0.5.0 [changelog](https://github.com/open-cluster-management-io/managed-serviceaccount/releases/tag/v0.5.0)
- cluster-proxy v0.4.0 [changelog](https://github.com/open-cluster-management-io/cluster-proxy/releases/tag/v0.4.0)

## `0.12.0`, 11 Oct. 2023

The Open Cluster Management team is proud to announce the release of OCM v0.12.0! We have made architecture refactors and added several features in
this release:

- Component consolidation: we made a big code refactor to merge code in registration, work, placement and registration-operator into the [ocm](https://github.com/open-cluster-management-io/ocm) repo.
  The original separated code repos are currently used for maintaining old releases only. This code consolidation allows us to build more robust e2e tests, and build a single
  agent binary to reduce the footprint in managed clusters.
- Addon Template API: A new `addontemplate` API is introduced to ease the development of addons. Users will not need to write code and run an addon-manager
  controller on the hub cluster. Instead, they only need to define the `addontemplate` API to create an addon. `clusteradm` also has a new command
  `clusteradm addon create ...` to create an addon from resource manifests files. See more details about `addontemplate` in the
  [addon documentation](https://open-cluster-management.io/developer-guides/addon/#build-an-addon-with-addon-template).
- Singleton agent mode: users can now choose to start the agent as a single pod using the `Singleton` mode in the klusterlet.
- ManagedClusterSet/ManagedClusterSetBinding v1beta1 API is removed.
- `ConfigurationPolicy`: Add the `informOnly` option to `remediationAction` in `ConfigurationPolicy`, signaling that the remediation action set
  on the `Policy` should not override the `ConfigurationPolicy`'s remediation action.
- Policy framework: Security, performance, and stability improvements in controllers on both the hub and managed clusters.
- `ClusterPermission`: New custom resource that enables administrators to automatically distribute RBAC resources to managed
  clusters and manage the lifecycle of those resources. See the [ClusterPermission repo](https://github.com/open-cluster-management-io/cluster-permission) for more details.

### Core components
- ocm v0.12.0 [changelog](https://github.com/open-cluster-management-io/ocm/releases/tag/v0.12.0)
- clusteradm  v0.7.0 [changelog](https://github.com/open-cluster-management-io/clusteradm/blob/v0.6.0/CHANGELOG.md)

### Addons
- config-policy-controller v0.12.0 [changelog](https://github.com/open-cluster-management-io/config-policy-controller/releases/tag/v0.12.0)
- governance-policy-framework-addon v0.12.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-framework-addon/releases/tag/v0.12.0)
- governance-policy-propagator v0.12.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-propagator/releases/tag/v0.12.0)
- governance-policy-addon-controller v0.12.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-addon-controller/releases/tag/v0.12.0)
- multicloud-operators-subscription v0.12.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-subscription/releases/tag/v0.12.0)
- multicloud-operators-channel v0.12.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-channel/releases/tag/v0.12.0)
- multicloud-integrations v0.12.0 [changelog](https://github.com/open-cluster-management-io/multicloud-integrations/releases/tag/v0.12.0)
- managed-serviceaccount v0.4.0 [changelog](https://github.com/open-cluster-management-io/managed-serviceaccount/releases/tag/v0.4.0)

## `0.11.0`, 1, June 2023

The Open Cluster Management team is proud to announce the release of OCM v0.11.0! There are a bunch of new features added into this release

- Addon install strategy and rolling upgrade: a new component `addon-manager` is introduced to handle the addon installation and upgrade.
  User can specify the installation and upgrade strategy of the addon by referencing placement on `ClusterManagementAddon` API. The
  feature is in the alpha stage and can be enabled by setting `feature-gates=AddonManagement=true` when running `clusteradm init`.
- ManifestWorkReplicaSet: it is a new API introduced in this release to deploy `ManifestWork` to multiple clusters by placement. Users can
  create a `ManifestWorkReplicaSet` together with `Placement` in the same namespace to spread the `ManifestWork` to multiple clusters, or
  use the command `clusteradm create work <work name> -f <manifest yaml> --placement <namespace>/<placement name> -r`. The
  feature is in the alpha stage and can be enabled by setting `feature-gates=ManifestWorkReplicaSet=true` when running `clusteradm init`.
- Registration auto approve: user can configure a list of user id to auto approve the registration which makes cluster registration simpler
  in some scenarios. The feature is in the alpha stage and can be enabled by setting `feature-gates=ManagedClusterAutoApproval=true` when running `clusteradm init`.
  With this feautre enabled, the user does not need to run `accept` command on hub after `join` command.
- ManifestWork can return structured result: previously the feedback mechanism in `ManifestWork` can only return scalar value. In this
  release, we add the support to return a structured value in the format of json string. To enable this feature, user can add `feature-gates=RawFeedbackJsonString=true`
  when running `clusteradm join` command.
- Policies added support for syncing [Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/) manifests directly (previously a ConfigurationPolicy was needed to sync Gatekeeper manifests).
- Templates were enhanced to lookup objects by label, and added `copySecretData` and `copyConfigMapData` functions to fetch the entire `data` contents of the respective object.
- Improved the integration of the ArgoCD pull model by aggregating the status of deployed resources in the managed clusters and presenting it in the hub cluster's `MulticlusterApplicationSetReport` custom resource.

### Core components
- registration v0.11.0 [changelog](https://github.com/open-cluster-management-io/registration/blob/v0.11.0/CHANGELOG/CHANGELOG-v0.11.md)
- work v0.11.0 [changelog](https://github.com/open-cluster-management-io/work/blob/v0.11.0/CHANGELOG/CHANGELOG-v0.11.md)
- placement v0.11.0 [changelog](https://github.com/open-cluster-management-io/placement/blob/v0.11.0/CHANGELOG/CHANGELOG-v0.11.md)
- addon-framework v0.7.0 [changelog](https://github.com/open-cluster-management-io/addon-framework/blob/v0.7.0/CHANGELOG/CHANGELOG-v0.7.md)
- registration-operator v0.11.0 [changelog](https://github.com/open-cluster-management-io/registration-operator/blob/v0.11.0/CHANGELOG/CHANGELOG-v0.11.md)
- clusteradm  v0.6.0 [changelog](https://github.com/open-cluster-management-io/clusteradm/blob/v0.6.0/CHANGELOG.md)

### Addons
- cluster-proxy v0.3.0 [repo](https://github.com/open-cluster-management-io/cluster-proxy)
- managed-serviceaccount v0.3.0 [repo](https://github.com/open-cluster-management-io/managed-serviceaccount)
- config-policy-controller v0.11.0 [changelog](https://github.com/open-cluster-management-io/config-policy-controller/releases/tag/v0.11.0)
- governance-policy-framework-addon v0.11.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-framework-addon/releases/tag/v0.11.0)
- governance-policy-propagator v0.11.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-propagator/releases/tag/v0.11.0)
- governance-policy-addon-controller v0.11.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-addon-controller/releases/tag/v0.11.0)
- multicloud-operators-subscription v0.11.0 [release note](https://github.com/open-cluster-management-io/multicloud-operators-subscription/releases/tag/v0.11.0)
- multicloud-operators-channel v0.11.0 [release note](https://github.com/open-cluster-management-io/multicloud-operators-channel/releases/tag/v0.11.0)
- multicloud-integrations v0.11.0 [release note](https://github.com/open-cluster-management-io/multicloud-integrations/releases/tag/v0.11.0)

We are pleased to welcome several new contributors to the community: @aii-nozomu-oki, @serngawy, @maleck13, @fgiloux, @USER0308, @youhangwang, @TheRealJon, @skitt, @yiraeChristineKim
@iranzo, @nirs, @akram, @pajikos, @Arhell, @levenhagen, @eemurphy, @bellpr, @o-farag. Thanks for your contributions!

## `0.10.0`, 17th, Feb 2023

The Open Cluster Management team is proud to announce the release of OCM v0.10.0! We mainly focused on bug fixes, code refactoring, and code stability
in this release. Also we worked on several important design proposals on addon lifecycle enhancement and manifestwork
orchestration which will be implemented in the next release. Here are some main features included in this release:
- Argo CD hub-spoke / pull model application delivery integration. See [argocd-pull-integration repo](https://github.com/open-cluster-management-io/argocd-pull-integration) for more details.
- Policy templating is enhanced so that when a referenced object is updated, the template is also updated.
- A Policy or ConfigurationPolicy can specify dependencies on another policy having a specified status before taking action.
- A raw string with go templates can be provided in `object-templates-raw` to the ConfigurationPolicy, allowing dynamically generated objects through the use of functions like `{{ range ... }}`.

### Core components
- registration v0.10.0 [changelog](https://github.com/open-cluster-management-io/registration/blob/v0.10.0/CHANGELOG/CHANGELOG-v0.10.md)
- work v0.10.0[changelog](https://github.com/open-cluster-management-io/work/blob/v0.10.0/CHANGELOG/CHANGELOG-v0.10.md)
- placement v0.10.0 [changelog](https://github.com/open-cluster-management-io/placement/blob/v0.10.0/CHANGELOG/CHANGELOG-v0.10.md)
- addon-framework v0.6.0 [changelog](https://github.com/open-cluster-management-io/addon-framework/blob/v0.6.0/CHANGELOG/CHANGELOG-v0.6.md)
- registration-operator v0.9.0 [changelog](https://github.com/open-cluster-management-io/registration-operator/blob/v0.10.0/CHANGELOG/CHANGELOG-v0.10.md)
- clusteradm  v0.5.1 [changelog](https://github.com/open-cluster-management-io/clusteradm/blob/v0.5.1/CHANGELOG.md)

### Addons
- config-policy-controller v0.10.0 [changelog](https://github.com/open-cluster-management-io/config-policy-controller/releases/tag/v0.10.0)
- governance-policy-framework-addon v0.10.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-framework-addon/releases/tag/v0.10.0)
- governance-policy-propagator v0.10.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-propagator/releases/tag/v0.10.0)
- governance-policy-addon-controller v0.10.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-addon-controller/releases/tag/v0.10.0)
- multicloud-operators-subscription v0.10.0 [release note](https://github.com/open-cluster-management-io/multicloud-operators-subscription/releases/tag/v0.10.0)
- multicloud-operators-channel v0.10.0 [release note](https://github.com/open-cluster-management-io/multicloud-operators-channel/releases/tag/v0.10.0)

## `v0.9.0`, 21st, October 2022

Open Cluster Management team is proud to announce the release of OCM v0.9.0! Here are some main features included in this release:

- De-escalate Work Agent Privilege on Managed Clusters
  In previous iterations of OCM, the Work Agent process is run with admin privileges on managed clusters. This release, to exercise the principle of least privilege, OCM supports defining a non-root identity within each ManifestWork object, allowing end users to give the agent only necessary permissions to interact with the clusters which they manage.
- Support referencing the AddOn configuration with AddOn APIs
  For some add-ons, they want to run with configuration, we enhance the add-on APIs to support reference add-on configuration, and in add-on framework, we support to trigger re-rendering the add-on deployment if its configuration is changed
- Allow Targeting Specific Services within Managed Clusters
  The cluster-proxy add-on supports the exposure of services from within managed clusters to hub clusters, even across Virtual Private Clouds. Originally all traffic was routed through the Kubernetes API server on each managed cluster, increasing load on the node hosting the API server. Now the proxy agent  add-on supports specifying a particular target service within a cluster, allowing for better load balancing of requests made by hub clusters and more granular control of what resources/APIs are exposed to hub clusters.
- Upgraded ManagedClusterSet API to v1beta2
  Update the ClusterSet API and gradually remove legacy custom resources, as well as allow for transformation of legacy resources into analogous v1beta2 resources. v1alpha1 APIs are removed.
- Consolidate the policy add-on template, status, and spec synchronization controllers into a single repository, [governance-policy-framework-addon](https://github.com/open-cluster-management-io/governance-policy-framework-addon)
- Application add-on is now able to expose custom Prometheus metrics via the Git subscription. See the [metric documentation](https://github.com/open-cluster-management-io/multicloud-operators-subscription/blob/v0.9.0/docs/metrics.md) for more details.

### Core components
- registration v0.9.0 [changelog](https://github.com/open-cluster-management-io/registration/blob/v0.9.0/CHANGELOG/CHANGELOG-v0.9.md)
- work v0.9.0 [changelog](https://github.com/open-cluster-management-io/work/blob/v0.9.0/CHANGELOG/CHANGELOG-v0.9.md)
- placement v0.9.0 [changelog](https://github.com/open-cluster-management-io/placement/blob/v0.9.0/CHANGELOG/CHANGELOG-v0.9.md)
- addon-framework v0.5.0 [changelog](https://github.com/open-cluster-management-io/addon-framework/blob/v0.5.0/CHANGELOG/CHANGELOG-v0.5.md)
- registration-operator v0.9.0 [changelog](https://github.com/open-cluster-management-io/registration-operator/blob/v0.9.0/CHANGELOG/CHANGELOG-v0.9.md)

### Addons
- config-policy-controller v0.9.0 [changelog](https://github.com/open-cluster-management-io/config-policy-controller/blob/main/CHANGELOG/CHANGELOG-v0.9.0.md)
- governance-policy-framework-addon v0.9.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-framework-addon/blob/main/CHANGELOG/CHANGELOG-v0.9.0.md)
- governance-policy-propagator v0.9.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-propagator/blob/main/CHANGELOG/CHANGELOG-v0.9.0.md)
- governance-policy-addon-controller v0.9.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-addon-controller/blob/main/CHANGELOG/CHANGELOG-v0.9.0.md)
- multicloud-operators-subscription v0.9.0 [release note](https://github.com/open-cluster-management-io/multicloud-operators-subscription/releases/tag/v0.9.0)
- multicloud-operators-channel v0.9.0 [release note](https://github.com/open-cluster-management-io/multicloud-operators-channel/releases/tag/v0.9.0)
- multicloud-integrations v0.9.0 [release note](https://github.com/open-cluster-management-io/multicloud-integrations/releases/tag/v0.9.0)

The release annoucement is also publishded in [blog](https://www.cncf.io/blog/2022/10/31/open-cluster-management-november-2022-update/). Thanks for all your contribution!

## `v0.8.0`, 8th, July 2022
Open Cluster Management team is proud to annouce the release of OCM v0.8.0! It includes several enhancement on core components and addons.
Notable changes including:

- `ManifestWork` update strategy: now user can set `ServerSideApply` or `CreateOnly` as the manifest update strategy to resolve potential
  resource conflict in `ManifestWork`.
- Global ClusterSet: when user enable the `DefaultClusterSet` feature gate, a global `ManagedClusterSet` will be auto-created including all
  `ManagedCluster`s
- Configuring feature gates for `klusterlet` and `cluster manager`: user can set feature gates when starting `klusterlet` and `cluster manager`.
- Support host alaises for `klusterlet`: user can now set host aliases for `klusterlet`, it is especially useful in on-prem environment.
- Running policy addon using `clusteradm`: user can now run policy addon directly using `clusteradm`

Also we have added two new sub projects:

- [multicluster-mesh](https://github.com/open-cluster-management-io/multicluster-mesh) is an addon to deploy and configure istio across the clusters.
- [ocm-vscode-extention](https://github.com/open-cluster-management-io/ocm-vscode-extension) is a vscode extension to operator/develop ocm project easily in vscode.

See details in the release changelogs:

### Core components
- registration v0.8.0 [changelog](https://github.com/open-cluster-management-io/registration/blob/v0.8.0/CHANGELOG/CHANGELOG-v0.8.md)
- work v0.8.0 [changelog](https://github.com/open-cluster-management-io/work/blob/v0.8.0/CHANGELOG/CHANGELOG-v0.8.md)
- placement v0.8.0 [changelog](https://github.com/open-cluster-management-io/placement/blob/v0.8.0/CHANGELOG/CHANGELOG-v0.8.md)
- addon-framework v0.4.0 [changelog](https://github.com/open-cluster-management-io/addon-framework/blob/v0.4.0/CHANGELOG/CHANGELOG-v0.4.md)
- registration-operator v0.8.0 [changelog](https://github.com/open-cluster-management-io/registration-operator/blob/v0.8.0/CHANGELOG/CHANGELOG-v0.8.md)

### Addons

- multicloud-operators-subscription v0.8.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-subscription/releases/tag/v0.8.0)
- multicloud-operators-channel v0.8.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-channel/releases/tag/v0.8.0)
- cluster-proxy v0.2.2 [changelog](https://github.com/open-cluster-management-io/cluster-proxy/releases/tag/v0.2.2)
- multicluster-mesh v0.0.1 [changelog](https://github.com/open-cluster-management-io/multicluster-mesh/releases/tag/v0.0.1)
- config-policy-controller v0.8.0 [changelog](https://github.com/open-cluster-management-io/config-policy-controller/blob/main/CHANGELOG/CHANGELOG-v0.8.0.md)
- governance-policy-spec-sync v0.8.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-spec-sync/blob/main/CHANGELOG/CHANGELOG-v0.8.0.md)
- governance-policy-template-sync v0.8.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-template-sync/blob/main/CHANGELOG/CHANGELOG-v0.8.0.md)
- governance-policy-status-sync v0.8.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-status-sync/blob/main/CHANGELOG/CHANGELOG-v0.8.0.md)
- governance-policy-propagator v0.8.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-propagator/blob/main/CHANGELOG/CHANGELOG-v0.8.0.md)
- governance-policy-addon-controller v0.8.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-addon-controller/blob/main/CHANGELOG/CHANGELOG-v0.8.0.md)

### CLI extentions

- clusteradm v0.3.0 [changelog](https://github.com/open-cluster-management-io/clusteradm/releases/tag/v0.3.0)
- ocm-vscode-extension 0.1.0 [changelog](https://github.com/open-cluster-management-io/ocm-vscode-extension/releases/tag/1.0.0)

There are 30+ contributors making contributions in this release, they are, @ChunxiAlexLuo, @dhaiducek, @elgnay, @haoqing0110, @itdove, @ilan-pinto, @ivan-cai, @jichenjc, @JustinKuli, @ldpliu, @mikeshng, @mgold1234, @morvencao, @mprahl, @nathanweatherly, @philipwu08, @panguicai008, @Promacanthus, @qiujian16, @rokej, @skeeey, @SataQiu, @vbelouso, @xauthulei, @xiangjingli, @xuezhaojun, @ycyaoxdu, @yue9944882, @zhujian7, @zhiweiyin318. Thanks for your contributions!

## `v0.7.0`, on 6th, April 2022

The Open Cluster Management team is excited to announce the release of OCM v0.7.0! We mainly focused on enhancing user experience in this release by introducing a bunch of new commands in `clusteradm`. Notable changes including:

 - APIs including `placement`, `placementdecision`, `managedclusterset` and `managedclustersetbinding` are upgraded to `v1beta1`, `v1alpha1` version of these APIs are deprecated and will be removed in the future.
 - User can now use `clusteradm` to:
   - create, bind and view `clusterset`
   - create and view `work`
   - check the controlplane status by using `hub-info` and `klusterlet-info` sub commands.
   - upgrade hub and klusterlet
- A default `managedclusterset` is created automatically and all clusters will be added to default `managedclusterset` by default. This feature can be disabled with feature gate `DefaultClusterSet` on registration controller.
- Add the new `policyset` API that provides a way to logically group `policy` objects from a namespace, share placement, and report on overall status for the set in policy addon.

See details in the release changelogs::
- registration v0.7.0 [changelog](https://github.com/open-cluster-management-io/registration/blob/v0.7.0/CHANGELOG/CHANGELOG-v0.7.md)
- work v0.7.0 [changelog](https://github.com/open-cluster-management-io/work/blob/v0.7.0/CHANGELOG/CHANGELOG-v0.7.md)
- placement v0.4.0 [changelog](https://github.com/open-cluster-management-io/placement/blob/v0.4.0/CHANGELOG/CHANGELOG-v0.4.md)
- addon-framework v0.3.0 [changelog](https://github.com/open-cluster-management-io/addon-framework/blob/v0.3.0/CHANGELOG/CHANGELOG-v0.3.md)
- registration-operator v0.7.0 [changelog](https://github.com/open-cluster-management-io/registration-operator/blob/v0.7.0/CHANGELOG/CHANGELOG-v0.7.md)
- cluster-proxy v0.2.0 [repo](https://github.com/open-cluster-management-io/cluster-proxy)
- managed-serviceaccount v0.2.0 [repo](https://github.com/open-cluster-management-io/managed-serviceaccount)
- clusteradm v0.2.0 [changelog](https://github.com/open-cluster-management-io/clusteradm/releases/tag/v0.2.0)
- multicloud-operators-subscription v0.7.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-subscription/releases/tag/v0.7.0)
- multicloud-operators-channel v0.7.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-channel/releases/tag/v0.7.0)
- governance policy propagator v0.7.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-propagator/blob/main/CHANGELOG/CHANGELOG-v0.7.0.md)
- config policy controller v0.7.0 [changelog](https://github.com/open-cluster-management-io/config-policy-controller/blob/main/CHANGELOG/CHANGELOG-v0.7.0.md)
- policy spec sync controller v0.7.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-spec-sync/blob/main/CHANGELOG/CHANGELOG-v0.7.0.md)
- policy template sync controller v0.7.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-template-sync/blob/main/CHANGELOG/CHANGELOG-v0.7.0.md)
- policy status sync controller v0.7.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-status-sync/blob/main/CHANGELOG/CHANGELOG-v0.7.0.md)


There are 30+ contributors making contributions in this release, they are, @ChunxiAlexLuo, @dhaiducek, @elgnay, @haoqing0110, @hanqiuzh, @ilan-pinto, @ivan-cai, @JiahaoWei-RH, @jichenjc, @JustinKuli, @ldpliu, @mikeshng, @mgold1234, @morvencao, @mprahl, @nathanweatherly, @philipwu08, @qiujian16, @rcarrillocruz, @rokej, @skeeey, @TheRealHaoLiu, @vbelouso, @vMaroon, @TomerFi, @xauthulei, @xiangjingli, @xuezhaojun, @ycyaoxdu, @yue9944882, @zhujian7, @zhiweiyin318. Thanks for your contributions!

## `v0.6.0`, on 21st, January 2022

The Open Cluster Management team is proud to announce the release of OCM v0.6.0! We made many enhancements on core components and introduced some new addons.

- [First release of cluster-proxy addon](https://github.com/open-cluster-management-io/cluster-proxy), Cluster-Proxy addon is to provide a reverse tunnel from the managed cluster to the hub using `apiserver-network-proxy`, so user can easily visit the apiserver of the managedcluster from the hub without complicated infrstructure configuration. See [here]({{< ref "docs/scenarios/pushing-kube-api-requests" >}}) on how to use cluster-proxy in OCM.
- [First release of managed-serviceaccount addon](https://github.com/open-cluster-management-io/managed-serviceaccount), Managed-Servicesaccount addon provides a mechanism to project a service account on a managed cluster to the hub. The user can then use this projected account to visit services on the managed cluster.
- [Sync status of applied resources in ManifestWork](https://github.com/open-cluster-management-io/enhancements/tree/main/enhancements/sig-architecture/29-manifestwork-status-feedback), The users can specify the status field of the applied resource they want to explore in the ManifestWork spec, and get results from the status of the ManifestWork. See [here](https://open-cluster-management.io/concepts/manifestwork/#fine-grained-field-values-tracking) on how to use this feature in Manifestwork.
- [Placement extensible scheduling](https://github.com/open-cluster-management-io/enhancements/blob/main/enhancements/sig-architecture/32-extensiblescheduling), a new API AddonPlacementScore is added which allows third party controllers to score the clusters based on various metrics. The user can specify what score should be used in the Placement API to select clusters.
- [Helm chart interface for addon framework](https://github.com/open-cluster-management-io/addon-framework/pull/62), a new interface is added in addon framework with which the developer can build an addon agent from a helm chart. See [example](https://github.com/open-cluster-management-io/addon-framework/tree/main/examples/helloworld_helm) on how to build an addon agent from the helm chart.
- [Placement API support for multicloud-operators-subscription](https://github.com/open-cluster-management-io/multicloud-operators-subscription/pull/55), subscription now supports Placement API and can leverage all new features in Placement API to deploy application packages.

We also added many new functions in [clusteradm](https://github.com/open-cluster-management-io/clusteradm) and enhanced the website documentation.

See details in the release changelogs::
- registration v0.6.0 [changelog](https://github.com/open-cluster-management-io/registration/blob/v0.6.0/CHANGELOG/CHANGELOG-v0.6.md)
- work v0.6.0 [changelog](https://github.com/open-cluster-management-io/work/blob/v0.6.0/CHANGELOG/CHANGELOG-v0.6.md)
- placement v0.3.0 [changelog](https://github.com/open-cluster-management-io/placement/blob/v0.3.0/CHANGELOG/CHANGELOG-v0.3.md)
- addon-framework v0.2.0 [changelog](https://github.com/open-cluster-management-io/addon-framework/blob/v0.2.0/CHANGELOG/CHANGELOG-v0.2.md)
- registration-operator v0.6.0 [changelog](https://github.com/open-cluster-management-io/registration-operator/blob/v0.6.0/CHANGELOG/CHANGELOG-v0.6.md)
- multicloud-operators-subscription v0.6.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-subscription/blob/v0.6.0/CHANGELOG/CHANGELOG-v0.6.md)
- cluster-proxy v0.1.3 [repo](https://github.com/open-cluster-management-io/cluster-proxy)
- managed-serviceaccount v0.1.0 [repo](https://github.com/open-cluster-management-io/managed-serviceaccount)
- clusteradm v0.1.0 [changelog](https://github.com/open-cluster-management-io/clusteradm/blob/v0.1.0/CHANGELOG)
- config-policy-controller v0.6.0 [changelog](https://github.com/open-cluster-management-io/config-policy-controller/blob/main/CHANGELOG/CHANGELOG-v0.6.0.md)
- governance-policy-propagator v0.6.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-propagator/blob/main/CHANGELOG/CHANGELOG-v0.6.0.md)
- governance-policy-status-sync v0.6.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-status-sync/blob/main/CHANGELOG/CHANGELOG-v0.6.0%20.md)
- governance-policy-spec-sync v0.6.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-spec-sync/blob/main/CHANGELOG/CHANGELOG-v0.6.0.md)
- governance-policy-template-sync v0.6.0 [changelog](https://github.com/open-cluster-management-io/governance-policy-template-sync/blob/main/CHANGELOG/CHANGELOG-v0.6.0.md)
- ocm-kustomize-generator-plugins v1.3.0 [changelog](https://github.com/open-cluster-management-io/ocm-kustomize-generator-plugins/blob/main/CHANGELOG/CHANGELOG-v1.3.0.md)

There are 20+ contributors making contributions in this release, they are @champly, @ChunxiAlexLuo, @dhaiducek, @elgnay, @haoqing0110, @ilan-pinto, @mikeshng, @morvencao, @mprahl, @nathanweatherly, @qiujian16, @rokej, @skeeey, @TheRealHaoLiu, @serngawy, @suigh, @xauthulei, @xiangjingli, @xuezhaojun, @ycyaoxdu, @yue9944882, @zhujian7, @zhiweiyin318. Thanks for your contributions!

## `v0.5.0`, on 8th, November 2021

Open Cluster Management team is proud to announce the release of OCM v0.5.0! We made several enhancements on APIs
and addons which include:

- [Support deleteOption in ManifestWork.](https://github.com/open-cluster-management-io/enhancements/tree/main/enhancements/sig-architecture/10-deletepropagationstrategy)
- [Introduce plugin mechanism in Placement API and add resource based scheduling.](https://github.com/open-cluster-management-io/enhancements/tree/main/enhancements/sig-architecture/15-resourcebasedscheduling)
- ManagedClusterSet API is upgraded from v1alpha1 to v1beta1.
- Scalability improvement on application manager.

In addition, we also release the first version of [clusteradm](https://github.com/open-cluster-management-io/clusteradm)
to ease the installation of OCM, and [addon-framework](https://github.com/open-cluster-management-io/addon-framework) to
ease the development of management addons on OCM.

To see details of the changelogs in this release:
- registration v0.5.0 [changelog](https://github.com/open-cluster-management-io/registration/blob/v0.5.0/CHANGELOG/CHANGELOG-v0.5.md)
- work v0.5.0 [changelog](https://github.com/open-cluster-management-io/work/blob/v0.5.0/CHANGELOG/CHANGELOG-v0.5.md)
- placement v0.2.0 [changelog](https://github.com/open-cluster-management-io/placement/blob/v0.2.0/CHANGELOG/CHANGELOG-v0.2.md)
- addon-framework v0.1.0 [changelog](https://github.com/open-cluster-management-io/addon-framework/blob/v0.1.0/CHANGELOG/CHANGELOG-v0.1.md)
- registration-operator v0.5.0 [changelog](https://github.com/open-cluster-management-io/registration-operator/blob/v0.5.0/CHANGELOG/CHANGELOG-v0.5.md)
- multicloud-operators-subscription v0.5.0 [changelog](https://github.com/open-cluster-management-io/multicloud-operators-subscription/blob/v0.5.0/CHANGELOG/CHANGELOG-v0.5.md)

There are 20+ contributors making contributions in this release, they are @elgnay, @haoqing0110, @hchenxa, @huiwq1990, @itdove, @kim-fitness, @mikeshng, @panpan0000, @philipwu08, @porridge, @qiujian16, @rokej, @skeeey, @suigh, @vincent-pli, @wzhanw, @xauthulei, @xiangjingli, @xuezhaojun, @yue9944882, @zhujian7, @zhiweiyin318. Thanks for your contributions!

## `v0.4.0` on August 2021
