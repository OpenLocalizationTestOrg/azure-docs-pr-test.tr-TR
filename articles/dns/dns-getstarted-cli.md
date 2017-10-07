---
title: "aaaGet Azure Azure CLI 2.0 kullanarak DNS ile başlatılan | Microsoft Docs"
description: "Bilgi nasıl toocreate bir DNS bölgesi ve Azure DNS kaydında. Bu adım adım kılavuzu toocreate ve ilk DNS bölgesi ve kayıt hello Azure CLI 2.0 kullanarak yönetin."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="e6a31-104">Azure CLI 2.0 kullanarak Azure DNS ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e6a31-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6a31-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e6a31-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="e6a31-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6a31-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="e6a31-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e6a31-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="e6a31-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e6a31-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="e6a31-109">Bu makalede ilk DNS bölgenizi hello adımları toocreate anlatılmaktadır ve kaydını kullanarak hello platformlar arası Azure CLI 2.0, Windows, Mac ve Linux için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e6a31-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="e6a31-110">Hello Azure portalında veya Azure PowerShell kullanarak aşağıdaki adımları de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6a31-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="e6a31-111">Bir DNS bölgesi belirli bir etki alanı için kullanılan toohost hello DNS kayıtlarını ' dir.</span><span class="sxs-lookup"><span data-stu-id="e6a31-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="e6a31-112">Azure DNS, etki alanınızda barındırma toostart toocreate bir DNS bölgesi için o etki alanı adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="e6a31-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="e6a31-113">Ardından bu DNS bölgesinde etki alanınız için tüm DNS kayıtları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e6a31-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="e6a31-114">Son olarak, toopublish, DNS bölge toohello Internet tooconfigure hello ad sunucuları hello etki alanı için gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6a31-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="e6a31-115">Bu adımların her biri aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e6a31-115">Each of these steps is described below.</span></span>

<span data-ttu-id="e6a31-116">Bu yönergeler, zaten yüklü ve tooAzure CLI 2.0 imzalı varsayalım.</span><span class="sxs-lookup"><span data-stu-id="e6a31-116">These instructions assume you have already installed and signed in tooAzure CLI 2.0.</span></span> <span data-ttu-id="e6a31-117">Yardım için bkz. [nasıl Azure CLI 2.0 kullanan toomanage DNS bölgeleri](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e6a31-117">For help, see [How toomanage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="e6a31-118">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="e6a31-118">Create hello resource group</span></span>

<span data-ttu-id="e6a31-119">Merhaba DNS bölgesi oluşturmadan önce bir kaynak grubu toocontain hello DNS bölgesi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e6a31-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="e6a31-120">Merhaba aşağıdaki hello komut gösterir.</span><span class="sxs-lookup"><span data-stu-id="e6a31-120">hello following shows hello command.</span></span>

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="e6a31-121">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6a31-121">Create a DNS zone</span></span>

<span data-ttu-id="e6a31-122">Bir DNS bölgesi hello kullanılarak oluşturulan `az network dns zone create` komutu.</span><span class="sxs-lookup"><span data-stu-id="e6a31-122">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="e6a31-123">Bu komutun toosee yardımını yazın `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="e6a31-123">toosee help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="e6a31-124">Merhaba aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* hello kaynak grubunda *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="e6a31-124">hello following example creates a DNS zone called *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="e6a31-125">Merhaba örnek toocreate bir DNS bölgesi Hello değerleri kendinizinkilerle değiştirerek kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6a31-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="e6a31-126">DNS kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6a31-126">Create a DNS record</span></span>

<span data-ttu-id="e6a31-127">toocreate bir DNS kaydı kullanmak hello `az network dns record-set [record type] add-record` komutu.</span><span class="sxs-lookup"><span data-stu-id="e6a31-127">toocreate a DNS record, use hello `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="e6a31-128">Örneğin, A kayıtlarına ilişkin yardım için bkz. `azure network dns record-set A add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="e6a31-128">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="e6a31-129">Merhaba aşağıdaki örnekte bir kayıt hello göreli adı "www" hello "contoso.com", "Contoso.com" kaynak grubunda DNS bölgesi içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e6a31-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="e6a31-130">Merhaba tam hello kayıt kümesi "www.contoso.com" adıdır.</span><span class="sxs-lookup"><span data-stu-id="e6a31-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="e6a31-131">Merhaba kayıt türü "A", "1.2.3.4" IP adresiyle olduğundan ve varsayılan TTL 3600 saniye (1 saat) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e6a31-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="e6a31-132">Alternatif TTL değerleri ve toomodify mevcut kayıtları için birden fazla kayıtla kayıt kümeleri için diğer kayıt türleri için bkz: [yönetmek DNS kayıtlarını ve kayıt kümelerini kullanarak hello Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e6a31-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="e6a31-133">Kayıtları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e6a31-133">View records</span></span>

<span data-ttu-id="e6a31-134">toolist hello DNS kayıtları, bölge içindeki kullanın:</span><span class="sxs-lookup"><span data-stu-id="e6a31-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="e6a31-135">Ad sunucularını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e6a31-135">Update name servers</span></span>

<span data-ttu-id="e6a31-136">Sonra DNS bölgesi ve kayıtları doğru şekilde ayarlanan, tooconfigure gerek memnun, etki alanı adı toouse hello Azure DNS ad sunucuları.</span><span class="sxs-lookup"><span data-stu-id="e6a31-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="e6a31-137">Bu DNS kayıtlarınızı hello Internet toofind üzerindeki diğer kullanıcılarla sağlar.</span><span class="sxs-lookup"><span data-stu-id="e6a31-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="e6a31-138">Merhaba bölgenizin ad sunucuları tarafından hello verilen `az network dns zone show` komutu.</span><span class="sxs-lookup"><span data-stu-id="e6a31-138">hello name servers for your zone are given by hello `az network dns zone show` command.</span></span> <span data-ttu-id="e6a31-139">toosee hello ad sunucusu adlarını hello aşağıdaki örnekte gösterildiği gibi JSON çıkışını kullanın.</span><span class="sxs-lookup"><span data-stu-id="e6a31-139">toosee hello name server names, use JSON output, as shown in hello following example.</span></span>

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="e6a31-140">Bu ad sunucuları hello etki alanı adı kayıt (Merhaba etki alanı adı satın aldığınız yerden) ile yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e6a31-140">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="e6a31-141">Şirketiniz hello seçeneği tooset hello ad sunucuları hello etki alanı için yukarı sunar.</span><span class="sxs-lookup"><span data-stu-id="e6a31-141">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="e6a31-142">Daha fazla bilgi için bkz: [, etki alanı tooAzure DNS temsilci](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="e6a31-142">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="e6a31-143">Tüm kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="e6a31-143">Delete all resources</span></span>
 
<span data-ttu-id="e6a31-144">Bu makalede, adım aşağıdaki Al hello oluşturulan tüm kaynakları toodelete:</span><span class="sxs-lookup"><span data-stu-id="e6a31-144">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="e6a31-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6a31-145">Next steps</span></span>

<span data-ttu-id="e6a31-146">Azure DNS hakkında daha fazla toolearn bkz [Azure DNS'ye genel bakış](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e6a31-146">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="e6a31-147">Azure DNS'de DNS bölgelerini yönetme hakkında daha fazla toolearn bkz [yönetmek DNS bölgeleri Azure CLI 2.0 kullanan Azure DNS'de](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e6a31-147">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="e6a31-148">Azure DNS'de DNS kayıtlarını yönetme hakkında daha fazla toolearn bkz [yönetmek DNS kayıtlarını ve kayıt kümelerini Azure CLI 2.0 kullanan Azure DNS'de](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e6a31-148">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>
