---
title: "aaaGet Azure PowerShell kullanarak DNS ile başlatılan | Microsoft Docs"
description: "Bilgi nasıl toocreate bir DNS bölgesi ve Azure DNS kaydında. Bu adım adım kılavuzu toocreate ve ilk DNS bölgenizi yönetmek ve PowerShell kullanarak kaydedin."
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
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="12ea7-104">PowerShell ile Azure DNS’i kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="12ea7-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="12ea7-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="12ea7-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="12ea7-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12ea7-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="12ea7-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="12ea7-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="12ea7-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="12ea7-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="12ea7-109">Bu makalede, ilk DNS bölgesi ve Azure PowerShell kullanarak kaydı hello adımları toocreate anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="12ea7-109">This article walks you through hello steps toocreate your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="12ea7-110">Ayrıca, hello Azure portal kullanarak aşağıdaki adımları gerçekleştirin veya platformlar arası Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="12ea7-110">You can also perform these steps using hello Azure portal or hello cross-platform Azure CLI.</span></span>

<span data-ttu-id="12ea7-111">Bir DNS bölgesi belirli bir etki alanı için kullanılan toohost hello DNS kayıtlarını ' dir.</span><span class="sxs-lookup"><span data-stu-id="12ea7-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="12ea7-112">Azure DNS, etki alanınızda barındırma toostart toocreate bir DNS bölgesi için o etki alanı adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="12ea7-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="12ea7-113">Ardından bu DNS bölgesinde etki alanınız için tüm DNS kayıtları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="12ea7-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="12ea7-114">Son olarak, toopublish, DNS bölge toohello Internet tooconfigure hello ad sunucuları hello etki alanı için gerekir.</span><span class="sxs-lookup"><span data-stu-id="12ea7-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="12ea7-115">Bu adımların her biri aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="12ea7-115">Each of these steps is described below.</span></span>

<span data-ttu-id="12ea7-116">Bu yönergeler, zaten yüklü ve tooAzure PowerShell imzalı varsayalım.</span><span class="sxs-lookup"><span data-stu-id="12ea7-116">These instructions assume you have already installed and signed in tooAzure PowerShell.</span></span> <span data-ttu-id="12ea7-117">Yardım için bkz. [PowerShell kullanarak nasıl toomanage DNS bölgeleri](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="12ea7-117">For help, see [How toomanage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="12ea7-118">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="12ea7-118">Create hello resource group</span></span>

<span data-ttu-id="12ea7-119">Merhaba DNS bölgesi oluşturmadan önce bir kaynak grubu toocontain hello DNS bölgesi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="12ea7-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="12ea7-120">Merhaba aşağıdaki hello komut gösterir.</span><span class="sxs-lookup"><span data-stu-id="12ea7-120">hello following shows hello command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="12ea7-121">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="12ea7-121">Create a DNS zone</span></span>

<span data-ttu-id="12ea7-122">Bir DNS bölgesi hello kullanılarak oluşturulan `New-AzureRmDnsZone` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="12ea7-122">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="12ea7-123">Merhaba aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* adlı hello kaynak grubunda *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="12ea7-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="12ea7-124">Merhaba örnek toocreate bir DNS bölgesi Hello değerleri kendinizinkilerle değiştirerek kullanın.</span><span class="sxs-lookup"><span data-stu-id="12ea7-124">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="12ea7-125">DNS kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="12ea7-125">Create a DNS record</span></span>

<span data-ttu-id="12ea7-126">Hello kullanarak kayıt kümeleri oluşturma `New-AzureRmDnsRecordSet` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="12ea7-126">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="12ea7-127">Merhaba aşağıdaki örnekte bir kayıt hello göreli adı "www" hello "contoso.com", "Contoso.com" kaynak grubunda DNS bölgesi içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="12ea7-127">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="12ea7-128">Merhaba tam hello kayıt kümesi "www.contoso.com" adıdır.</span><span class="sxs-lookup"><span data-stu-id="12ea7-128">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="12ea7-129">Merhaba kayıt türü "A", "1.2.3.4" IP adresiyle, ve hello TTL 3600 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="12ea7-129">hello record type is "A", with IP address "1.2.3.4", and hello TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="12ea7-130">Diğer kayıt türleri için birden fazla kayıt ve toomodify mevcut kayıtları ile kayıt kümeleri için bkz: [yönetmek DNS kayıtlarını ve kayıt kümelerini Azure PowerShell kullanarak](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="12ea7-130">For other record types, for record sets with more than one record, and toomodify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="12ea7-131">Kayıtları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="12ea7-131">View records</span></span>

<span data-ttu-id="12ea7-132">toolist hello DNS kayıtları, bölge içindeki kullanın:</span><span class="sxs-lookup"><span data-stu-id="12ea7-132">toolist hello DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="12ea7-133">Ad sunucularını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="12ea7-133">Update name servers</span></span>

<span data-ttu-id="12ea7-134">Sonra DNS bölgesi ve kayıtları doğru şekilde ayarlanan, tooconfigure gerek memnun, etki alanı adı toouse hello Azure DNS ad sunucuları.</span><span class="sxs-lookup"><span data-stu-id="12ea7-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="12ea7-135">Bu DNS kayıtlarınızı hello Internet toofind üzerindeki diğer kullanıcılarla sağlar.</span><span class="sxs-lookup"><span data-stu-id="12ea7-135">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="12ea7-136">Merhaba bölgenizin ad sunucuları tarafından hello verilen `Get-AzureRmDnsZone` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="12ea7-136">hello name servers for your zone are given by hello `Get-AzureRmDnsZone` cmdlet:</span></span>

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

<span data-ttu-id="12ea7-137">Bu ad sunucuları hello etki alanı adı kayıt (Merhaba etki alanı adı satın aldığınız yerden) ile yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="12ea7-137">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="12ea7-138">Şirketiniz hello seçeneği tooset hello ad sunucuları hello etki alanı için yukarı sunar.</span><span class="sxs-lookup"><span data-stu-id="12ea7-138">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="12ea7-139">Daha fazla bilgi için bkz: [, etki alanı tooAzure DNS temsilci](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="12ea7-139">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="12ea7-140">Tüm kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="12ea7-140">Delete all resources</span></span>

<span data-ttu-id="12ea7-141">Bu makalede, adım aşağıdaki Al hello oluşturulan tüm kaynakları toodelete:</span><span class="sxs-lookup"><span data-stu-id="12ea7-141">toodelete all resources created in this article, take hello following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="12ea7-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="12ea7-142">Next steps</span></span>

<span data-ttu-id="12ea7-143">Azure DNS hakkında daha fazla toolearn bkz [Azure DNS'ye genel bakış](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="12ea7-143">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="12ea7-144">Azure DNS'de DNS bölgelerini yönetme hakkında daha fazla toolearn bkz [Azure PowerShell kullanarak DNS yönetme DNS bölgelerini](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="12ea7-144">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="12ea7-145">Azure DNS'de DNS kayıtlarını yönetme hakkında daha fazla toolearn bkz [yönetmek DNS kayıtlarını ve kayıt kümelerini PowerShell kullanarak Azure DNS'de](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="12ea7-145">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

