---
title: Deploy Azure landing zones
description: Deployment options for platform and application landing zones in Azure.
author: robbagby
categories:
  - management-and-governance
  - devops
  - networking
  - security
ms.author: robbag
ms.date: 09/20/2022
ms.topic: conceptual
ms.service: architecture-center
ms.subservice: guide
azureCategories: 
  - devops
  - hybrid
  - management-and-governance
  - networking
  - security
products:
  - azure
  - azure-resource-manager
  - azure-policy
  - azure-rbac
  - azure-virtual-network
---

# Deploy Azure landing zones

This article discusses the options available to you to deploy both platform and application landing zones. Platform landing zones provide centralized services used by workloads whereas application landing zones are environments deployed for the workloads themselves.

> [!IMPORTANT]
> For more information about platform vs. application landing zones definitions, see the article [What is an Azure landing zone?](/azure/cloud-adoption-framework/ready/landing-zone/#platform-vs-application-landing-zones) in the Cloud Adoption Framework (CAF) documentation.

The article begins by covering common roles and responsibilities for differing cloud operating models. It continues by listing deployment options for platform and application landing zones.

## Cloud operating model roles and responsibilities

The Cloud Adoption Framework describes four [common cloud operating models](/azure/cloud-adoption-framework/operating-model/compare). The [Azure identity and access for landing zones](/azure/cloud-adoption-framework/ready/landing-zone/design-area/identity-access-landing-zones#rbac-recommendations) recommends five role definitions (Roles) you should consider if your organizations cloud operating model requires customized Role Based Access Control (RBAC). If your organization has more decentralized operations, the Azure [built-in roles](/azure/role-based-access-control/role-definitions-list) may be sufficient.

The table below outlines the key roles for each of the cloud operating models.

| Role | Decentralized operations | Centralized operations | Enterprise operations | Distributed operations |
| --- | --- | --- | --- | --- |
| Azure platform owner (such as the built-in Owner role) | [Workload team](/azure/cloud-adoption-framework/organize/cloud-adoption.md) | [Central cloud strategy](/azure/cloud-adoption-framework/organize/cloud-strategy.md) | [Enterprise architect](/azure/cloud-adoption-framework/organize/cloud-strategy) in [CCoE](/azure/cloud-adoption-framework/organize/cloud-center-of-excellence.md)  | Based on portfolio analysis - see [Business alignment](/azure/cloud-adoption-framework/manage/considerations/business-alignment) and [Business commitments](/azure/cloud-adoption-framework/manage/considerations/commitment.md) |
| Network management (NetOps) | [Workload team](/azure/cloud-adoption-framework/organize/cloud-adoption.md) | [Central IT](/azure/cloud-adoption-framework/organize/central-it.md) | [Central Networking](/azure/cloud-adoption-framework/organize/central-it) in [CCoE](/azure/cloud-adoption-framework/organize/cloud-center-of-excellence.md) | [Central Networking for each distributed team](/azure/cloud-adoption-framework/organize/central-it) + [CCoE](/azure/cloud-adoption-framework/organize/cloud-center-of-excellence.md) |
| Security operations (SecOps) | [Workload team](/azure/cloud-adoption-framework/organize/cloud-adoption.md) | [Security operations center (SOC)](/azure/cloud-adoption-framework/organize/cloud-security-operations-center.md) | [CCoE](/azure/cloud-adoption-framework/organize/cloud-center-of-excellence.md) + [SOC](/azure/cloud-adoption-framework/organize/cloud-security-operations-center.md) | Mixed - see: [Define a security strategy](/azure/cloud-adoption-framework/strategy/define-security-strategy) |
| Subscription owner | [Workload team](/azure/cloud-adoption-framework/organize/cloud-adoption.md) | [Central IT](/azure/cloud-adoption-framework/organize/central-it.md) | [Central IT](/azure/cloud-adoption-framework/organize/central-it.md) + [Application Owners](/azure/cloud-adoption-framework/organize/central-it) | [CCoE](/azure/cloud-adoption-framework/organize/cloud-center-of-excellence.md) + [Application Owners](/azure/cloud-adoption-framework/organize/central-it) |
| Application owners (DevOps, AppOps) | [Workload team](/azure/cloud-adoption-framework/organize/cloud-adoption.md) | [Workload team](/azure/cloud-adoption-framework/organize/cloud-adoption.md) | [Central IT](/azure/cloud-adoption-framework/organize/central-it.md) + [Application Owners](/azure/cloud-adoption-framework/organize/central-it) | [CCoE](/azure/cloud-adoption-framework/organize/cloud-center-of-excellence.md) + [Application Owners](/azure/cloud-adoption-framework/organize/central-it) |

## Platform

The options below provide an opinionated approach to deploy and operate the [Azure landing zone conceptual architecture](/azure/cloud-adoption-framework/ready/landing-zone#azure-landing-zone-conceptual-architecture) as detailed in the Cloud Adoption Framework (CAF). It's important to note that, depending upon customizations, the resulting architecture might not be the same for all the options listed below. The differences between the options are how you deploy the architecture. They use differing technologies, take different approaches and are customized differently.

| Deployment option | Description |
| --- | ---|
| [Azure landing zone Portal accelerator](/azure/cloud-adoption-framework/ready/landing-zone/#azure-landing-zone-accelerator) | An Azure portal-based deployment that provides a full implementation of the conceptual architecture, along with opinionated configurations for key components such as management groups and policies. |
| [Azure landing zone Terraform accelerator](terraform/landing-zone-terraform.md) | This accelerator provides an orchestrator module, but also allows you to deploy each capability individually or in part. |
| [Azure landing zone Bicep accelerator](bicep/landing-zone-bicep.md)  | A modular accelerator where each module encapsulates a core capability of the [Azure landing zone conceptual architecture](/azure/cloud-adoption-framework/ready/landing-zone#azure-landing-zone-conceptual-architecture). While the modules can be deployed individually, the design proposes the use of orchestrator modules to encapsulate the complexity of deploying different topologies with the modules. |

## Application

Application landing zones are one or more subscriptions that are deployed as environments for workloads or applications. These workloads can take advantage of services deployed in platform landing zones. The application landing zones can be centrally managed applications, decentralized workloads, or technology platforms such as Azure Kubernetes Service that host applications.

You can use the options below to deploy and manage applications or workloads in an application landing zone.

| Application | Description |
| --- | --- |
| [AKS landing zone accelerator](/azure/cloud-adoption-framework/scenarios/app-platform/aks/landing-zone-accelerator) | An open-source collection of ARM, Bicep, and Terraform templates that represent the strategic design path and target technical state for an Azure Kubernetes Service (AKS) deployment. |
| [Azure App Service landing zone accelerator](/azure/cloud-adoption-framework/scenarios/app-platform/app-services/landing-zone-accelerator) | Proven recommendations and considerations across both multi-tenant and App Service Environment use cases with a reference implementation for ASEv3-based deployment  |
| [Azure API Management landing zone accelerator](/azure/cloud-adoption-framework/scenarios/app-platform/api-management/landing-zone-accelerator) | Proven recommendations and considerations for deploying APIM management with a reference implementation showcasing App Gateway with internal APIM instance backed Azure Functions as backend. |
| [SAP on Azure landing zone accelerator](/azure/cloud-adoption-framework/scenarios/sap/enterprise-scale-landing-zone) | Terraform and Ansible templates that accelerate SAP workload deployments using Azure Landing Zone best practices, including the creation of Infrastructure components like Compute, Networking, Storage, Monitoring & build of SAP systems. |
| [HPC landing zone accelerator](/azure/cloud-adoption-framework/scenarios/azure-vmware/enterprise-scale-landing-zone) | An end-to-end HPC cluster solution in Azure using tools like Terraform, Ansible, and Packer. It addresses Azure Landing Zone best practices, including implementing identity, Jump-box access, and autoscale. |
| [Azure VMware Solution landing zone accelerator](/azure/cloud-adoption-framework/scenarios/azure-vmware/enterprise-scale-landing-zone) | ARM, Bicep, and Terraform templates that accelerate VMware deployments, including AVS private cloud, jumpbox, networking, monitoring and add-ons. |
| [Azure Virtual Desktop Landing Zone Accelerator](/azure/cloud-adoption-framework/scenarios/wvd/enterprise-scale-landing-zone) | ARM, Bicep, and Terraform templates that accelerate Azure Virtual Desktop deployments, including creation of host pools, networking, storage, monitoring and add-ons. |
| [Azure Red Hat OpenShift landing zone accelerator](/azure/cloud-adoption-framework/scenarios/app-platform/azure-red-hat-openshift/landing-zone-accelerator) | An open source collection of Terraform templates that represent an optimal Azure Red Hat OpenShift (ARO) deployment that is comprised of both Azure and Red Hat resources. |
| [Azure Arc landing zone accelerator for hybrid and multicloud](/azure/cloud-adoption-framework/scenarios/hybrid/enterprise-scale-landing-zone) | Arc enabled Servers, Kubernetes, and Arc-enabled SQL Managed Instance see the Jumpstart ArcBox overview. |
