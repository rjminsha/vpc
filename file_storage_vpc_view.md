---

copyright:
  years: 2021
lastupdated: "2021-04-07"

keywords: file storage, virtual private cloud, file share, mount target

subcollection: vpc

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:important: .important}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:beta: .beta}
{:external: target="_blank" .external}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}
{:api: .ph data-hd-interface='api'}

# Viewing file shares and mount targets (beta)
{: #file-storage-view}

View all file shares and mount targets by using the UI, CLI, or API. Also view details of a single file share or mount target.
{:shortdesc}

This service is available only to accounts with a special approval to preview this beta feature. 
{:beta}

## View file shares and mount targets using the UI
{: #file-storage-view-shares-targets-ui}
{: ui}

### View all file shares using the UI
{: #fs-view-all-shares-ui}

1. In the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}/vpc-ext){: external}, go to **Menu icon ![Menu icon](../../icons/icon_hamburger.svg) > VPC Infrastructure > Storage > File Shares**.
1. The File Shares for VPC list page shows all file shares created in that zone. Overflow menu options let you manage the shares. Table 1 describes the information and actions on the list page.

| Field | Value |
|-------|-------|
| Region | Account region for the file share. Select a different region to see file shares for zones in that region. |
| Name  | The share name. Click on the name to see details about that share. |
| Status | For a list of statuses for file shares, see [File storage lifecycle states](/docs/vpc?topic=vpc-file-storage-managing#file-storage-vpc-status). |
| Resource groups | Resource groups associated with the file share in your account. |
| Zone | Zone in which the file share was created and resides (for example, _US South 2_). |
| Mount targets | Number of mount targets associated with the file share.You can have one mount target per VPC per file share. |
| Size | Size of the file share, in GBs. |
| Encryption Type | Shows encryption type of the file share. |
| Overflow menu (hellipsis) | Options for managing the file share, depending on its state. For example, for a file share in a _stable_ state, you can Delete a file share. |
{: caption="Table 1. File shares list page" caption-side="top"}

### View details of a single file share using the UI
{: #fs-view-single-share-ui}

1. Navigate to the list of all file shares. From the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}/vpc-ext){: external}, go to **Menu icon ![Menu icon](../../icons/icon_hamburger.svg) > VPC Infrastructure > Storage > File Shares**.

1. Click on the name of a file share to see the details page. The editable name and [status](/docs/vpc?topic=vpc-file-storage-managing#file-storage-vpc-status) of the file share is shown. Table 2 describes the information on this page.

| Field | Value |
|-------|-------|
| Name  | The share name. Click on the pencil icon to change the name. |
| Resource group | Resource groups associated with the file share in your account. |
| ID | The UUID generated when you created the share. |
| Created | Date the file share was created. |
| Zone | Zone in which the file share was created and resides (for example, _US South 2_). |
| Size | Size of the file share, in GBs. |
| IOPS tier | [IOPS tier profile](/docs/vpc?topic=vpc-file-storage-profiles#fs-tiers) defining the share performance (for example 3 IOPS/GB). |
| Max IOPS | Maximum IOPS for the IOPS tier profile associated with the share. |
| Mount targets | Number of mount targets associated with the file share. You can have one mount target per VPC per file share.<br> You can create more mount targets for other VPCs.<br>Click the **Virtual private cloud** to go to the details page for that VPC, where you can see a [list of file shares](#fs-view-shares-vpc) that have a mount target to the VPC]. |
| Overflow menu (hellipsis) | Options for managing the file share, depending on its state. For example, for a file share in a _stable_ state, you can delete a file share. |
{: caption="Table 2. File shares details page" caption-side="top"}

### View all file shares for a VPC using the UI
{: #fs-view-shares-vpc}

You can see all file shares that have a mount target to a VPC by viewing the VPC details page.

1. Navigate to a VPC:

  1. From the [file shares details page](#fs-view-single-share), click the VPC link in the list of mount targets.
  2. From the UI, go to **Menu icon ![Menu icon](../../icons/icon_hamburger.svg) > VPC Infrastructure > > Network > VPCs**. Click on the name of a VPC in the list.

2. On the VPC details page, scroll to **File shares in this VPC**.


## View file share and mount targets using the CLI
{: #file-storage-view-shares-targets-cli}
{: cli}

### View mount targets for a file share from the CLI
{: #fs-view-targets-shares-cli}

Run the `share-targets` command and specify the file share ID to see all mount targets for a file share.

```
ibmcloud is share-targets SHARE_ID [--output JSON] [-q, --quiet]
```
{:pre}


### View all file shares from the CLI
{: #fs-view-all-shares-cli}

Run the `shares` command to list all file shares in a region.

```
ibmcloud is shares [--resource-group-id RESOURCE_GROUP_ID | --resource-group-name RESOURCE_GROUP_NAME | --all-resource-groups] [--output JSON] [-q, --quiet]
```
{:pre}

## View file shares and mount targets from the API
{: #file-storage-view-shares-targets-api}
{: api}

### View all file shares from the API
{: #fs-view-all-shares-api}

This request lists all shares for a region. 

```curl
curl -X GET \ 
"$vpc_api_endpoint/v1/shares?version=2021-03-16&generation=2" \
-H "Authorization: $iam_token"
```
{: pre}

A successful response will look like this:

```json
{
  "first": {
    "href": "$vpc_api_endpoint/v1/shares?limit=50"
  },
  "limit": 50,
  "shares": [
    {
      "created_at": "2021-03-30T13:02:17Z",
      "crn": "crn:[...]",
      "encryption": "provider_managed",
      "href": "$vpc_api_endpoint/v1/shares/51bba578-0dce-4f8a-aa6e-f06c899e2c8e",
      "id": "51bba578-0dce-4f8a-aa6e-f06c899e2c8e",
      "iops": 3000,
      "lifecycle_state": "stable",
      "name": "share-name1",
      "profile": {
        "href": "$vpc_api_endpoint/v1/share/profiles/tier-10iops",
        "name": "tier-10iops",
        "resource_type": "share_profile"
      },
      "resource_group": {
        "crn": "crn:[...]",
        "href": "https://resource-controller.cloud.ibm.com/v2/resource_groups/60fc731a-1794-4f5d-ba51-ea24b5357207",
        "id": "60fc731a-1794-4f5d-ba51-ea24b5357207",
        "name": "Default"
      },
      "resource_type": "share",
      "size": 40,
      "targets": [
        {
          "href": "$vpc_api_endpoint/v1/shares/51bba578-0dce-4f8a-aa6e-f06c899e2c8e/targets/d5fd8173-f519-4ff7-8f63-0ead23ecf1f4",
          "id": "d5fd8173-f519-4ff7-8f63-0ead23ecf1f4",
          "name": "target-name1",
          "resource_type": "share_target",
          "vpc": {
            "crn": "crn:[...]",
            "href": "$vpc_api_endpoint/v1/vpcs/c2d941de-27f5-432c-b4d0-37a8491c3216",
            "id": "c2d941de-27f5-432c-b4d0-37a8491c3216",
            "name": "vpc-name1",
            "resource_type": "vpc"
          }
        }
      ],
      "zone": {
        "href": "$vpc_api_endpoint/v1/regions/us-south/zones/us-south-1",
        "name": "us-south-1"
      }
    }
  ]
}
```
{:codeblock}

### View a single file share from the API
{: #fs-single-file-shares-api}

This request gets the information of a single file share.

```curl
curl -X GET \ 
"$vpc_api_endpoint/v1/shares/$share_id?version=2021-03-16&generation=2" \
-H "Authorization: $iam_token"
```
{:pre}

A successful response will look like this:

```json
{
  "created_at": "2021-03-31T23:31:59Z",
  "crn": "crn:[...]",
  "encryption": "provider_managed",
  "href": "$vpc_api_endpoint/v1/shares/199d78ec-b971-4a5c-a904-8f37ae710c63",
  "id": "199d78ec-b971-4a5c-a904-8f37ae710c63",
  "iops": 3000,
  "lifecycle_state": "stable",
  "name": "share-name1",
  "profile": {
    "href": "$vpc_api_endpoint/v1/share/profiles/tier-10iops",
    "name": "tier-10iops",
    "resource_type": "share_profile"
  },
  "resource_group": {
    "crn": "crn:[...]",
    "href": "https://resource-controller.cloud.ibm.com/v2/resource_groups/678523bcbe2b4eada913d32640909956",
    "id": "678523bcbe2b4eada913d32640909956",
    "name": "Default"
  },
  "resource_type": "share",
  "size": 100,
  "targets": [
    {
      "href": "$vpc_api_endpoint/v1/shares/199d78ec-b971-4a5c-a904-8f37ae710c63/targets/d5fd8173-f519-4ff7-8f63-0ead23ecf1f4",
      "id": "d5fd8173-f519-4ff7-8f63-0ead23ecf1f4",
      "name": "target-name1",
      "resource_type": "share_target",
      "vpc": {
        "crn": "crn:[...]",
        "href": "$vpc_api_endpoint/v1/vpcs/c2d941de-27f5-432c-b4d0-37a8491c3216",
        "id": "c2d941de-27f5-432c-b4d0-37a8491c3216",
        "name": "vpc-name1",
        "resource_type": "vpc"
      }
    }
  ],
  "zone": {
    "href": "$vpc_api_endpoint/v1/regions/us-south/zones/us-south-1",
    "name": "us-south-1"
  }
}
```
{:codeblock}

### List all mount targets of a share from the API
{: #fs-list-targets-api}

This request lists all mount targets of a share.

Example:

```curl
curl -X GET \ 
"$vpc_api_endpoint/v1/shares/$share_id/targets?version=2020-08-01&generation=2" \
-H "Authorization: $iam_token"
```
{:pre}

A successful response will look like this:

```json
{
  "first": {
    "href": "$vpc_api_endpoint/v1/shares/199d78ec-b971-4a5c-a904-8f37ae710c63/targets?limit=50"
  },
  "limit": 50,
  "targets": [
    {
      "created_at": "2021-03-31T23:31:59Z",
      "href": "$vpc_api_endpoint/v1/shares/199d78ec-b971-4a5c-a904-8f37ae710c63/targets/d5fd8173-f519-4ff7-8f63-0ead23ecf1f4",
      "id": "d5fd8173-f519-4ff7-8f63-0ead23ecf1f4",
      "lifecycle_state": "stable",
      "mount_path": "domain.com:/abc_2891fd0a_63aa_4deb_9ed5_1159e37cb5aa",
      "name": "target-name1",
      "resource_type": "share_target",
      "vpc": {
        "crn": "crn:[...]",
        "href": "$vpc_api_endpoint/v1/vpcs/c2d941de-27f5-432c-b4d0-37a8491c3216",
        "id": "c2d941de-27f5-432c-b4d0-37a8491c3216",
        "name": "vpc-name1",
        "resource_type": "vpc"
      }
    }
  ],
  "total_count": 1
}
```
{:codeblock}

### ### View a single mount target from the API
{: #fs-get-target-api}

This request gets the information of a single mount target of a share. This call will have the mount path information. Use the mount path to attach a file share to VSIs.

Example:

```curl
curl -X GET \ 
"$vpc_api_endpoint/v1/shares/$share_id/targets/$target_id?version=2020-08-01&generation=2" \
-H "Authorization: $iam_token"
```
{:pre}

A successful response will look like this:

```json
{
  "created_at": "2021-03-31T23:31:59Z",
  "href": "$vpc_api_endpoint/v1/shares/199d78ec-b971-4a5c-a904-8f37ae710c63/targets/d5fd8173-f519-4ff7-8f63-0ead23ecf1f4",
  "id": "d5fd8173-f519-4ff7-8f63-0ead23ecf1f4",
  "lifecycle_state": "stable",
  "mount_path": "domain.com:/vol_xyz_2891fd0a_64ea_4deb_9ed5_1159e37cb5aa",
  "name": "target-name1",
  "resource_type": "share_target",
  "vpc": {
    "crn": "crn:[...]",
    "href": "$vpc_api_endpoint/v1/vpcs/c2d941de-27f5-432c-b4d0-37a8491c3216",
    "id": "c2d941de-27f5-432c-b4d0-37a8491c3216",
    "name": "vpc-name1",
    "resource_type": "vpc"
  }
}
```
{:codeblock}

## Next steps
{: #fs-view-next-steps}

* [Create new file shares and mount targets](/docs/vpc?topic=vpc-file-storage-create)
* [Manage your file shares](/docs/vpc?topic=vpc-file-storage-managing)
