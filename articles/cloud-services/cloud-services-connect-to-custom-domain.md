---
title: "Bir bulut hizmeti bir özel etki alanı denetleyicisine bağlanma | Microsoft Docs"
description: "Web/çalışan rolleri bir özel AD PowerShell ve AD etki alanı uzantısını kullanarak etki alanına bağlayın öğrenin"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 17f6918371678ac849198bff4e3b3eea8678c660
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-azure-cloud-services-roles-to-a-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="3686d-103">Azure bulut Hizmetleri rolleri bir özel AD etki alanı denetleyicisi Azure'da barındırılan bağlanma</span><span class="sxs-lookup"><span data-stu-id="3686d-103">Connecting Azure Cloud Services Roles to a custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="3686d-104">Sanal ağ (VNet) İlk Azure içinde ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="3686d-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="3686d-105">Ardından bir Active Directory etki alanı (bir Azure sanal makinede barındırılan) denetleyicisi Vnet'e ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="3686d-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) to the VNet.</span></span> <span data-ttu-id="3686d-106">Ardından, biz mevcut bulut hizmeti rollerinizi önceden oluşturulmuş Vnet'e ekleyin, sonra etki alanı denetleyicisine bağlanma.</span><span class="sxs-lookup"><span data-stu-id="3686d-106">Next, we will add existing cloud service roles to the pre-created VNet, then connect them to the Domain Controller.</span></span>

<span data-ttu-id="3686d-107">Başlamadan önce birkaç şey göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="3686d-107">Before we get started, couple of things to keep in mind:</span></span>

1. <span data-ttu-id="3686d-108">Bu öğreticide PowerShell kullanır, böylece Azure PowerShell yüklenmiş ve Git hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3686d-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready to go.</span></span> <span data-ttu-id="3686d-109">Azure PowerShell ayarlama konusunda yardım almak için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3686d-109">To get help with setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="3686d-110">AD etki alanı denetleyicisi ve Web/çalışan rolü örneklerinizi ağda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3686d-110">Your AD Domain Controller and Web/Worker Role instances need to be in the VNet.</span></span>

<span data-ttu-id="3686d-111">Bu adım adım kılavuz izleyin ve herhangi bir sorunla çalıştırırsanız, bize makalenin sonunda bir yorum yazın.</span><span class="sxs-lookup"><span data-stu-id="3686d-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at the end of the article.</span></span> <span data-ttu-id="3686d-112">Birisi geri için karşılaşırsınız (Evet, biz yorumları okuma).</span><span class="sxs-lookup"><span data-stu-id="3686d-112">Someone will get back to you (yes, we do read comments).</span></span>

<span data-ttu-id="3686d-113">Bulut hizmeti tarafından başvurulan ağ olmalıdır bir **Klasik sanal ağ**.</span><span class="sxs-lookup"><span data-stu-id="3686d-113">The network that is referenced by the cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="3686d-114">Bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="3686d-114">Create a Virtual Network</span></span>
<span data-ttu-id="3686d-115">Azure portal veya PowerShell kullanarak Azure'da bir sanal ağ oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3686d-115">You can create a Virtual Network in Azure using the Azure portal or PowerShell.</span></span> <span data-ttu-id="3686d-116">Bu öğretici için PowerShell kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="3686d-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="3686d-117">Azure Portalı'nı kullanarak bir sanal ağ oluşturmak için bkz: [sanal ağ oluştur](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="3686d-117">To create a Virtual Network using the Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="3686d-118">Bir Sanal Makine Oluşturun</span><span class="sxs-lookup"><span data-stu-id="3686d-118">Create a Virtual Machine</span></span>
<span data-ttu-id="3686d-119">Sanal ağı kurma tamamladıktan sonra bir AD etki alanı denetleyicisi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3686d-119">Once you have completed setting up the Virtual Network, you will need to create an AD Domain Controller.</span></span> <span data-ttu-id="3686d-120">Bu öğretici için size bir AD etki alanı denetleyicisi üzerinde bir Azure sanal makine ayarlarını yapacak.</span><span class="sxs-lookup"><span data-stu-id="3686d-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="3686d-121">Bunu yapmak için aşağıdaki komutları kullanarak PowerShell aracılığıyla bir sanal makine oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3686d-121">To do this, create a virtual machine through PowerShell using the following commands:</span></span>

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it to the Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-to-a-domain-controller"></a><span data-ttu-id="3686d-122">Sanal makinenize bir etki alanı denetleyicisine Yükselt</span><span class="sxs-lookup"><span data-stu-id="3686d-122">Promote your Virtual Machine to a Domain Controller</span></span>
<span data-ttu-id="3686d-123">Sanal makineyi bir AD etki alanı denetleyicisi olarak yapılandırmak için VM için oturum açın ve yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3686d-123">To configure the Virtual Machine as an AD Domain Controller, you will need to log in to the VM and configure it.</span></span>

<span data-ttu-id="3686d-124">VM oturum açmak için RDP dosyasını PowerShell aracılığıyla almak, aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="3686d-124">To log in to the VM, you can get the RDP file through PowerShell, use the following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="3686d-125">VM oturum açtıktan sonra sanal makineniz adım adım kılavuzu izleyerek bir AD etki alanı denetleyicisi ayarlamak [müşterinizi AD etki alanı denetleyicisi ayarlamak nasıl](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="3686d-125">Once you are signed in to the VM, set up your Virtual Machine as an AD Domain Controller by following the step-by-step guide on [How to set up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-to-the-virtual-network"></a><span data-ttu-id="3686d-126">Bulut hizmetiniz için sanal ağ ekleme</span><span class="sxs-lookup"><span data-stu-id="3686d-126">Add your Cloud Service to the Virtual Network</span></span>
<span data-ttu-id="3686d-127">Ardından, yeni Vnet'in bulut hizmeti dağıtımınızı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3686d-127">Next, you need to add your cloud service deployment to the new VNet.</span></span> <span data-ttu-id="3686d-128">Bunu yapmak için Visual Studio ya da bir düzenleyiciyi kullanarak, cscfg ilgili bölümlerine ekleyerek, bulut hizmeti cscfg değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3686d-128">To do this, modify your cloud service cscfg by adding the relevant sections to your cscfg using Visual Studio or the editor of your choice.</span></span>

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

<span data-ttu-id="3686d-129">Sonraki bulut Hizmetleri projeyi oluşturun ve Azure'a dağıtın.</span><span class="sxs-lookup"><span data-stu-id="3686d-129">Next build your cloud services project and deploy it to Azure.</span></span> <span data-ttu-id="3686d-130">Bulut Hizmetleri paketinizi Azure'a dağıtma konusunda yardım almak için bkz: [nasıl oluşturulacağı ve bir bulut hizmeti dağıtma](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="3686d-130">To get help with deploying your cloud services package to Azure, see [How to Create and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-to-the-domain"></a><span data-ttu-id="3686d-131">Web/çalışan rolleri etki alanına bağlayın</span><span class="sxs-lookup"><span data-stu-id="3686d-131">Connect your web/worker roles to the domain</span></span>
<span data-ttu-id="3686d-132">Bulut hizmeti projenizi Azure üzerinde dağıtıldığında, rolü örneklerinizi AD etki alanı uzantısını kullanarak özel AD etki alanına bağlayın.</span><span class="sxs-lookup"><span data-stu-id="3686d-132">Once your cloud service project is deployed on Azure, connect your role instances to the custom AD domain using the AD Domain Extension.</span></span> <span data-ttu-id="3686d-133">AD etki alanı uzantısı, var olan bulut Hizmetleri dağıtımına eklemek ve özel etki alanına katılmak için PowerShell içinde aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3686d-133">To add the AD Domain Extension to your existing cloud services deployment and join the custom domain, execute the following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension to the cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="3686d-134">Ve bu kadar.</span><span class="sxs-lookup"><span data-stu-id="3686d-134">And that's it.</span></span>

<span data-ttu-id="3686d-135">Bulut Hizmetleri, özel etki alanı denetleyicisine katılması.</span><span class="sxs-lookup"><span data-stu-id="3686d-135">Your cloud services should be joined to your custom domain controller.</span></span> <span data-ttu-id="3686d-136">AD etki alanı uzantısını yapılandırmak nasıl kullanılabilir farklı seçenekler hakkında daha fazla bilgi edinmek istiyorsanız, PowerShell Yardımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3686d-136">If you would like to learn more about the different options available for how to configure AD Domain Extension, use the PowerShell help.</span></span> <span data-ttu-id="3686d-137">Örnekler izleyin birkaç:</span><span class="sxs-lookup"><span data-stu-id="3686d-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
