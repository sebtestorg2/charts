# Epinio PaaS

Opinionated platform that runs on Kubernetes to take you from Code to URL in one step.

__Attention__:

  - Requires `cert-manager` as dependency.
  - Requires `helm-controller` as dependency.

## Upgrading to Kubernetes v1.25+

Starting in Kubernetes v1.25, [Pod Security Policies](https://kubernetes.io/docs/concepts/security/pod-security-policy/)
have been removed from the Kubernetes API.

As a result, __before upgrading to Kubernetes v1.25__ (or on a fresh install in a Kubernetes v1.25+
cluster), users are expected to perform an in-place upgrade of this chart with
`global.cattle.psp.enabled` set to `false` if it has been previously set to `true`.

​> __Note:__
> In this chart release, any previous field that was associated with any PSP resources have been
> removed in favor of a single global field: `global.cattle.psp.enabled`.

> __Note:__
> If you upgrade your cluster to Kubernetes v1.25+ before removing PSPs via a `helm upgrade` (even
> if you manually clean up resources), __it will leave the Helm release in a broken state within the
> cluster such that further Helm operations will not work (`helm uninstall`, `helm upgrade`,
> etc.).__
>
> If your charts get stuck in this state, please consult the Rancher docs on how to clean up your
> Helm release secrets.

Upon setting `global.cattle.psp.enabled` to false, the chart will remove any PSP resources deployed
on its behalf from the cluster. This is the default setting for this chart.  ​

As a replacement for PSPs, [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/)
should be used. Please consult the Rancher docs for more details on how to configure your chart
release namespaces to work with the new Pod Security Admission and apply Pod Security Standards.
