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

# Planning your file shares (beta)
{: #file-storage-planning}

When you're planning a to create file shares on your VPC, you might find this checklist helpful to set up and use the file service.
{:shortdesc}

This service is available only to accounts with special approval to preview this beta feature.
{:beta}

Before you get started, make sure that you created a [VPC](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console).
{:important}

## Planning for creating file shares
{: #planning-for-file-shares}

Consider the following prerequisites before you set up File Storage for VPC.

|        Considerations|
|-------------------|
|__ Evaluate your [IAM access permissions](/docs/vpc?topic=vpc-file-storage-managing) to create file shares. |
|__ Evaluate the capacity and performance you need by [selecting a predefined IOPS tier and size](/docs/vpc?topic=vpc-file-storage-profiles). |
|__ Choose the UI, CLI, or API for creating and managing your file shares. |
|__ Evaluate how you plan to use your file shares. |
|__ Make sure you have a unique name for your file shares that easily identify the file share as your list of shares grows. Associate it with a resource group in your IBM Cloud customer account. |
|__ When creating a file share, decide when to create a mount target. You can create additional mount targets separate from file share creation. |
|__ To mount a file share on a target, you must create at least one mount target. |
|__ To create a mount target you must have a VPC. Identify an existing VPC or create a new one. |
{: caption="Table 1. Checklist for planning file shares" caption-side="top"}

## Next Steps
{: #file-storage-vpc-planning-next-steps}

[Create file shares and mount points](/docs/vpc?topic=vpc-file-storage-create).
