# acm

![Version: 0.1.6-clusterbackup](https://img.shields.io/badge/Version-0.1.6--clusterbackup-informational?style=flat-square)

A Helm chart to configure Advanced Cluster Manager for OpenShift.

This chart is used by the Validated Patterns to configure ACM and manage remote clusters

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| acm.backup | object | Backup operator is not enabled | Used to control backup and restore of ACM |
| acm.backup.enableAutomaticImport | bool | `false` | Enables the managed service account component which allows auto-import of managed clusters during restores |
| acm.backup.enabled | bool | `false` | Enable the backup operator. This will lead to OpenShift ADP operator being installed into the  open-cluster-management-backup if AWS Security Token Service (STS) has not been enabled |
| acm.backup.oadpSubscriptionSpec | string | Not configured and uses the correlated default OADP version linked to the ACM version | Custom OADP subscription specification (Optional) |
| acm.backup.schedule | object | Create a schedule that runs every 2 hours with an expiration time of 120 hours | Configures a backupschedule (Optional) |
| acm.backup.schedule.veleroSchedule | string | `"0 */2 * * *"` | Cron schedule to perform backups |
| acm.backup.schedule.veleroTtl | string | `"120h"` | Expiration time for a scheduled backup resource (Optional) |
| acm.mce_operator | object | Uses the official redhat sources | Just used for IIB testing, drives the source and channel for the MCE subscription triggered by ACM |
| clusterGroup | object | depends on the individual settings | Dictionary of all the clustergroups of the pattern |
| clusterGroup.managedClusterGroups | object | `{}` | The set of cluters managed by ACM which is running inside this clusterGroup |
| clusterGroup.subscriptions | object | `{"acm":{"source":"redhat-operators"}}` | Dictionary of subscriptions for this specific clusterGroup |
| clusterGroup.subscriptions.acm | object | `{"source":"redhat-operators"}` | Name of the subscription |
| clusterGroup.subscriptions.acm.source | string | `"redhat-operators"` | The catalog source for this subscription |
| global.extraValueFiles | list | `[]` | List of additional value files to be passed to the pattern |
| global.options.applicationRetryLimit | int | `20` |  |
| global.pattern | string | `"none"` |  |
| global.repoURL | string | `"none"` | Repository URL pointing to the pattern |
| global.secretStore.backend | string | `"vault"` |  |
| global.targetRevision | string | `"main"` | The branch or Git reference to use to deploy the pattern |
| main.gitops.channel | string | `"gitops-1.15"` | Default gitops channel to install on remote clusters |
| secretStore | object | depends on the individual settings | Default secretstore configuration variables |
| secretStore.name | string | `"vault-backend"` | Name of the clustersecretstore to be used for secrets |

