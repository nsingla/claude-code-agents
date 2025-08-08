## Extra Product Requirements

### Supported Version Compatibility
The Kubeflow Pipelines backend has codebase dependencies with Argo Workflows libraries, which in turn have interactions with the deployed Argo Workflows pipeline engine via k8s interfaces (CRs, etc).  In turn, the Data Science Pipelines Application can be deployed with components that have AWF dependencies independent of the deployed Argo Workflows backend.  The consequence of this is that it is possible for the API Server to be out-of-sync or not fully compatible with the deployed Workflow Controller, especially one that is deployed by a user outside of a Data Science Pipelines Application stack.  Therefore, a compatibility matrix will need to be created, documented, tested, and maintained.

Current messaging states that there is no written guarantee that future releases of Argo Workflows are compatible with previous versions, even Z-streams.  However, community maintainers have stated they are working with this in mind and with the intention of introducing a written mandate that z-stream releases will not introduce breaking changes.  Additionally, Argo documentation states patch versions will only contain bug fixes and minor features, which would include breaking changes.  This will help broaden our support matrix and testing strategy so we should work upstream to cultivate and introduce this as quickly as possible.

With that said, there is also no guarantee that Minor releases of Argo Workflows will not introduce breaking changes.  In fact, we have seen multiple occasions where this happens (3.3 to 3.4 upgrade, for instance, required a very non-trivial PR that blocked upstream dependency upgrades for over a year.  In contrast, the 3.4 to 3.5 upgrade was straightforward with no introduced breaking changes. This suggests that minor AWF upgrades will always carry inherent risk and therefore should not be included in the support matrix, at least without extensive testing.

Given these conditions, an example compatibility matrix would look like the following table:

| **ODH Version** | **Supported ArgoWF Version, Current State** | **Supported Range of ArgoWF Versions, upstream z-stream stability mandate accepted** |
|-------------------|---------------------------------------------|--------------------------------------------------------------------------------------|
| 3.4.1             | 3.4.16                                      | 3.4.16                                                                               |
| 3.5.0             | 3.5.14, 3.5.10 - 3.5.13, …                  | 3.5.x                                                                                |
| 3.6.0             | 3.5.14                                      | 3.5.x - 3.5.y                                                                        |

## Test Case Requirements
Add following test cases to the corresponding sections: 
* Test Cases for `Cluster config` section:
    * [Kubernetes Native Mode](https://github.com/kubeflow/pipelines/tree/master/proposals/11551-kubernetes-native-api)
    * FIPS Mode
    * Disconnected Cluster
* Test Cases for `Negative functional tests` section:
    * With conflicts Argo Workflow controller instances (DSP and External controllers coexisting and looking for the same type of events)
    * With DSP and external workflow controller on different RBAC
    * DSP with incompatible workflow schema
* Test Cases for `Positive functional tests` section:
    * With artifacts
    * Without artifacts
    * For Loop
    * Parallel for
    * Custom root kfp
    * Custom python package indexes
    * Custom base images
    * With input
    * Without input
    * With output
    * Without output
    * With iteration count
    * With retry
    * With cert handling
    * etc.
    * Override Pod Spec patch - create separate test cases for the following:
      * Node taint
      * PVC
      * Custom labels
* Test Cases for `Security Tests` section:
  * with different RBAC access with DSP at cluster level and Argo Workflow controller at Namespace level access
* Test Cases for `Miscellaneous Tests` section:
  * Validate a successful run of a simple hello world pipeline With DSP Argo Workflow Controller to coexist with External Argo Workflow controller
* Add Compatibility Test cases under the `Compatibility Matrix Tests` section based on the above defined `Supported Version Compatibility` section
* Test Cases for `Final Regression/Full E2E Tests` section (Run this on a fully deployed RHOAI cluster with latest of all products for that specific release):
  * Run Iris Pipeline on a standard RHOAI Cluster with DB as storage
  * Run Iris Pipeline on a FIPS enabled RHOAI Cluster
  * Run Iris Pipeline on a disconnected RHOAI Cluster
  * Run Iris Pipeline on a standard RHOAI Cluster with K8s Native API Storage

