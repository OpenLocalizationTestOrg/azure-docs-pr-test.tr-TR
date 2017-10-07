---
title: "bir bulut hizmeti tooa aaaConnect özel etki alanı denetleyicisi | Microsoft Docs"
description: "Bilgi nasıl tooconnect web/çalışan rolleri tooa özel AD etki alanı PowerShell ve AD etki alanı uzantısı kullanma"
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
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="6cfa6-103">Azure bulut Hizmetleri rolleri tooa özel AD etki alanı denetleyicisi Azure'da barındırılan bağlanma</span><span class="sxs-lookup"><span data-stu-id="6cfa6-103">Connecting Azure Cloud Services Roles tooa custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="6cfa6-104">Sanal ağ (VNet) İlk Azure içinde ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="6cfa6-105">Bir Active Directory etki alanı denetleyicisi (bir Azure sanal makinede barındırılan) toohello VNet sonra ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) toohello VNet.</span></span> <span data-ttu-id="6cfa6-106">Ardından, biz mevcut bulut hizmeti rolleri toohello VNet önceden oluşturulmuş ekleyin, sonra toohello etki alanı denetleyicisine bağlanma.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-106">Next, we will add existing cloud service roles toohello pre-created VNet, then connect them toohello Domain Controller.</span></span>

<span data-ttu-id="6cfa6-107">Başlamadan önce birkaç şey tookeep unutmayın:</span><span class="sxs-lookup"><span data-stu-id="6cfa6-107">Before we get started, couple of things tookeep in mind:</span></span>

1. <span data-ttu-id="6cfa6-108">Bu öğreticide PowerShell kullanır, böylece Azure PowerShell yüklenmiş olması ve toogo hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready toogo.</span></span> <span data-ttu-id="6cfa6-109">Azure PowerShell ayar tooget Yardımı'na bakın [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6cfa6-109">tooget help with setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="6cfa6-110">AD etki alanı denetleyicisi ve Web/çalışan rolü örneklerinizi hello VNet toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-110">Your AD Domain Controller and Web/Worker Role instances need toobe in hello VNet.</span></span>

<span data-ttu-id="6cfa6-111">Bu adım adım kılavuz izleyin ve herhangi bir sorunla çalıştırırsanız, bize hello hello makalenin sonunda bir yorum yazın.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at hello end of hello article.</span></span> <span data-ttu-id="6cfa6-112">Birisi tooyou geri alırsınız (Evet, biz yorumları okuma).</span><span class="sxs-lookup"><span data-stu-id="6cfa6-112">Someone will get back tooyou (yes, we do read comments).</span></span>

<span data-ttu-id="6cfa6-113">Merhaba bulut hizmeti tarafından başvurulan hello ağ olmalıdır bir **Klasik sanal ağ**.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-113">hello network that is referenced by hello cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="6cfa6-114">Bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="6cfa6-114">Create a Virtual Network</span></span>
<span data-ttu-id="6cfa6-115">Azure'da hello Azure portal veya PowerShell kullanarak bir sanal ağ oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-115">You can create a Virtual Network in Azure using hello Azure portal or PowerShell.</span></span> <span data-ttu-id="6cfa6-116">Bu öğretici için PowerShell kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="6cfa6-117">kullanarak bir sanal ağ toocreate hello Azure portal, bkz: [sanal ağ oluştur](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="6cfa6-117">toocreate a Virtual Network using hello Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="6cfa6-118">Bir Sanal Makine Oluşturun</span><span class="sxs-lookup"><span data-stu-id="6cfa6-118">Create a Virtual Machine</span></span>
<span data-ttu-id="6cfa6-119">Merhaba sanal ağ kurmayı tamamladıktan sonra toocreate bir AD etki alanı denetleyicisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-119">Once you have completed setting up hello Virtual Network, you will need toocreate an AD Domain Controller.</span></span> <span data-ttu-id="6cfa6-120">Bu öğretici için size bir AD etki alanı denetleyicisi üzerinde bir Azure sanal makine ayarlarını yapacak.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="6cfa6-121">toodo Bu, PowerShell komutlarını aşağıdaki hello kullanarak aracılığıyla bir sanal makine oluşturun:</span><span class="sxs-lookup"><span data-stu-id="6cfa6-121">toodo this, create a virtual machine through PowerShell using hello following commands:</span></span>

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

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a><span data-ttu-id="6cfa6-122">Sanal makine tooa etki alanı denetleyicisine Yükselt</span><span class="sxs-lookup"><span data-stu-id="6cfa6-122">Promote your Virtual Machine tooa Domain Controller</span></span>
<span data-ttu-id="6cfa6-123">tooconfigure hello sanal makine bir AD etki alanı denetleyicisi toohello VM toolog ve gerekir yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-123">tooconfigure hello Virtual Machine as an AD Domain Controller, you will need toolog in toohello VM and configure it.</span></span>

<span data-ttu-id="6cfa6-124">toolog toohello VM içinde kullanım hello komutları aşağıdaki PowerShell aracılığıyla hello RDP dosyasını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6cfa6-124">toolog in toohello VM, you can get hello RDP file through PowerShell, use hello following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="6cfa6-125">Toohello VM oturumunuz sonra sanal makineniz aşağıdaki hello adım adım kılavuzu bir AD etki alanı denetleyicisi olarak ayarlamak [nasıl müşteriniz AD etki alanı denetleyicisi yukarı tooset](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="6cfa6-125">Once you are signed in toohello VM, set up your Virtual Machine as an AD Domain Controller by following hello step-by-step guide on [How tooset up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-toohello-virtual-network"></a><span data-ttu-id="6cfa6-126">Bulut hizmeti toohello sanal ağ ekleme</span><span class="sxs-lookup"><span data-stu-id="6cfa6-126">Add your Cloud Service toohello Virtual Network</span></span>
<span data-ttu-id="6cfa6-127">Ardından, bulut hizmeti dağıtım toohello tooadd gerekir yeni VNet.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-127">Next, you need tooadd your cloud service deployment toohello new VNet.</span></span> <span data-ttu-id="6cfa6-128">toodo Bu, Visual Studio kullanarak hello ilgili bölümlerine tooyour cscfg ekleyerek, bulut hizmeti cscfg değiştirebilir veya hello düzenleyiciyi.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-128">toodo this, modify your cloud service cscfg by adding hello relevant sections tooyour cscfg using Visual Studio or hello editor of your choice.</span></span>

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

<span data-ttu-id="6cfa6-129">Sonraki bulut Hizmetleri projeyi oluşturun ve tooAzure dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-129">Next build your cloud services project and deploy it tooAzure.</span></span> <span data-ttu-id="6cfa6-130">Bulut Hizmetleri paket tooAzure dağıtma ile tooget Yardımı'na bakın [nasıl tooCreate ve bir bulut hizmeti dağıtma](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="6cfa6-130">tooget help with deploying your cloud services package tooAzure, see [How tooCreate and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-toohello-domain"></a><span data-ttu-id="6cfa6-131">Web/çalışan rolleri toohello etki alanınızın Bağlan</span><span class="sxs-lookup"><span data-stu-id="6cfa6-131">Connect your web/worker roles toohello domain</span></span>
<span data-ttu-id="6cfa6-132">Bulut hizmeti projenizi Azure üzerinde dağıtıldığında, başlangıç AD etki alanı uzantısını kullanarak rol örnekleri toohello özel AD etki alanınızın bağlayın.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-132">Once your cloud service project is deployed on Azure, connect your role instances toohello custom AD domain using hello AD Domain Extension.</span></span> <span data-ttu-id="6cfa6-133">tooadd hello AD etki alanı uzantısı tooyour mevcut bulut Hizmetleri dağıtımı ve hello özel etki alanına katılma, PowerShell komutlarını aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="6cfa6-133">tooadd hello AD Domain Extension tooyour existing cloud services deployment and join hello custom domain, execute hello following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="6cfa6-134">Ve bu kadar.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-134">And that's it.</span></span>

<span data-ttu-id="6cfa6-135">Bulut hizmetlerinizi birleştirilmiş tooyour özel etki alanı denetleyicisi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-135">Your cloud services should be joined tooyour custom domain controller.</span></span> <span data-ttu-id="6cfa6-136">Kullanılabilir farklı seçenekler hakkında daha fazla hello toolearn isterseniz tooconfigure AD etki alanı uzantısını kullanım hello PowerShell nasıl yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="6cfa6-136">If you would like toolearn more about hello different options available for how tooconfigure AD Domain Extension, use hello PowerShell help.</span></span> <span data-ttu-id="6cfa6-137">Örnekler izleyin birkaç:</span><span class="sxs-lookup"><span data-stu-id="6cfa6-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
