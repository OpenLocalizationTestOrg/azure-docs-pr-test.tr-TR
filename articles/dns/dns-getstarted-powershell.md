---
title: "PowerShell ile Azure DNS kullanmaya başlama | Microsoft Docs"
description: "Azure DNS'te DNS bölgesi ve kaydı oluşturma hakkında bilgi edinin. Bu kılavuzda, PowerShell kullanarak ilk DNS bölgenizi ve kaydınızı oluşturup yönetmeniz için adım adım talimatlar sunulmaktadır."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 48f7ba325f61b4a91c0208b4c99058da801bee19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="43546-104">PowerShell ile Azure DNS’i kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="43546-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="43546-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="43546-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="43546-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43546-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="43546-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="43546-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="43546-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="43546-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="43546-109">Bu makalede, Azure PowerShell kullanarak ilk DNS bölgesi ve kaydınızı oluşturma adımları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="43546-109">This article walks you through the steps to create your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="43546-110">Ayrıca, Azure portal veya platformlar arası Azure CLI kullanarak aşağıdaki adımları gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43546-110">You can also perform these steps using the Azure portal or the cross-platform Azure CLI.</span></span>

<span data-ttu-id="43546-111">DNS bölgesi belirli bir etki alanıyla ilgili DNS kayıtlarını barındırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="43546-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="43546-112">Etki alanınızı Azure DNS'de barındırmaya başlamak için bir DNS bölgesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="43546-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="43546-113">Ardından bu DNS bölgesinde etki alanınız için tüm DNS kayıtları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="43546-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="43546-114">Son olarak, DNS bölgenizi Internet'te yayımlamak için etki alanının ad sunucularını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="43546-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="43546-115">Bu adımların her biri aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="43546-115">Each of these steps is described below.</span></span>

<span data-ttu-id="43546-116">Bu yönergeler, Azure PowerShell’i zaten yüklediğinizi ve oturum açtığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="43546-116">These instructions assume you have already installed and signed in to Azure PowerShell.</span></span> <span data-ttu-id="43546-117">Yardım için bkz. [PowerShell ile DNS bölgelerini yönetme](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="43546-117">For help, see [How to manage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="43546-118">Kaynak grubunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="43546-118">Create the resource group</span></span>

<span data-ttu-id="43546-119">DNS bölgesini oluşturmadan önce, DNS Bölgesi’ni içerecek bir kaynak grubu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="43546-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="43546-120">Aşağıda, komut gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="43546-120">The following shows the command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="43546-121">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="43546-121">Create a DNS zone</span></span>

<span data-ttu-id="43546-122">DNS bölgesi, `New-AzureRmDnsZone` cmdlet’i kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="43546-122">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="43546-123">Aşağıdaki örnek, *MyResourceGroup* adlı kaynak grubunda *contoso.com* adlı bir DNS bölgesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="43546-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="43546-124">Değerleri kendinizinkilerle değiştirerek DNS bölgesini oluşturmak için örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="43546-124">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="43546-125">DNS kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="43546-125">Create a DNS record</span></span>

<span data-ttu-id="43546-126">`New-AzureRmDnsRecordSet` cmdlet’ini kullanarak kayıt kümeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43546-126">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="43546-127">Aşağıdaki örnekte, "MyResourceGroup" kaynak grubu içindeki "contoso.com" DNS Bölgesinde göreli adı "www" olan bir kaynak oluşturulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="43546-127">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="43546-128">"www.contoso.com", kayıt kümesinin tam adıdır.</span><span class="sxs-lookup"><span data-stu-id="43546-128">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="43546-129">Kayıt türü "A", IP adresi "1.2.3.4" ve TTL 3600 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="43546-129">The record type is "A", with IP address "1.2.3.4", and the TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="43546-130">Diğer kayıt türleri, birden fazla kayıt içerek kayıt kümeleri ve var olan kayıtların değiştirilmesi hakkında bilgi için bkz. [Azure PowerShell kullanarak DNS kayıtlarını ve kayıt kümelerini yönetme](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="43546-130">For other record types, for record sets with more than one record, and to modify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="43546-131">Kayıtları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="43546-131">View records</span></span>

<span data-ttu-id="43546-132">Bölgenizdeki DNS kayıtlarını listelemek için şu seçenekleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="43546-132">To list the DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="43546-133">Ad sunucularını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="43546-133">Update name servers</span></span>

<span data-ttu-id="43546-134">DNS bölgenizin ve kayıtlarınızın doğru şekilde ayarlandığına karar verdikten sonra, Azure DNS ad sunucularını kullanmak için etki alanınızın adını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="43546-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="43546-135">Bunun yapılması, İnternet üzerindeki diğer kullanıcıların DNS kayıtlarınızı bulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="43546-135">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="43546-136">Bölgenizin ad sunucuları `Get-AzureRmDnsZone` cmdlet’i tarafından belirtilir:</span><span class="sxs-lookup"><span data-stu-id="43546-136">The name servers for your zone are given by the `Get-AzureRmDnsZone` cmdlet:</span></span>

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

<span data-ttu-id="43546-137">Bu ad sunucuları, etki alanı adı kayıt şirketi (etki alanı adını satın aldığınız şirket) ile birlikte yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="43546-137">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="43546-138">Kayıt şirketiniz, etki alanı için ad sunucularını ayarlama seçeneğini sunar.</span><span class="sxs-lookup"><span data-stu-id="43546-138">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="43546-139">Daha fazla bilgi için bkz. [Etki alanınızı Azure DNS’e devretme](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="43546-139">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="43546-140">Tüm kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="43546-140">Delete all resources</span></span>

<span data-ttu-id="43546-141">Bu makalede oluşturulan tüm kaynakları silmek için, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="43546-141">To delete all resources created in this article, take the following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="43546-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="43546-142">Next steps</span></span>

<span data-ttu-id="43546-143">Azure DNS hakkında daha fazla bilgi için bkz. [Azure DNS'e genel bakış](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43546-143">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="43546-144">Azure DNS’te DNS bölgelerini yönetme hakkında daha fazla bilgi için bkz. [PowerShell ile Azure DNS’te DNS bölgelerini yönetme](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="43546-144">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="43546-145">Azure DNS’te DNS kayıtlarını yönetme hakkında daha fazla bilgi için bkz. [PowerShell ile Azure DNS’te DNS kayıtlarını yönetme](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="43546-145">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

