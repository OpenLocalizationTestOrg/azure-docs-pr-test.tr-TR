---
title: "aaaGet Azure Azure CLI 1.0 kullanarak DNS ile başlatılan | Microsoft Docs"
description: "Bilgi nasıl toocreate bir DNS bölgesi ve Azure DNS kaydında. Bu adım adım kılavuzu toocreate ve ilk DNS bölgesi ve kayıt hello Azure CLI 1.0 kullanarak yönetin."
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
ms.openlocfilehash: e200c848ad261160e593306dbb8a1d92bf26880b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="33587-104">Azure CLI 1.0 kullanarak Azure DNS ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="33587-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="33587-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="33587-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="33587-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="33587-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="33587-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="33587-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="33587-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="33587-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="33587-109">Bu makalede ilk DNS bölgenizi hello adımları toocreate anlatılmaktadır ve kaydını kullanarak hello platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="33587-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="33587-110">Hello Azure portalında veya Azure PowerShell kullanarak aşağıdaki adımları de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33587-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="33587-111">Bir DNS bölgesi belirli bir etki alanı için kullanılan toohost hello DNS kayıtlarını ' dir.</span><span class="sxs-lookup"><span data-stu-id="33587-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="33587-112">Azure DNS, etki alanınızda barındırma toostart toocreate bir DNS bölgesi için o etki alanı adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="33587-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="33587-113">Ardından bu DNS bölgesinde etki alanınız için tüm DNS kayıtları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="33587-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="33587-114">Son olarak, toopublish, DNS bölge toohello Internet tooconfigure hello ad sunucuları hello etki alanı için gerekir.</span><span class="sxs-lookup"><span data-stu-id="33587-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="33587-115">Bu adımların her biri aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="33587-115">Each of these steps is described below.</span></span>

<span data-ttu-id="33587-116">Bu yönergeler, zaten yüklü ve tooAzure CLI 1.0 imzalanan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="33587-116">These instructions assume you have already installed and signed in tooAzure CLI 1.0.</span></span> <span data-ttu-id="33587-117">Yardım için bkz. [nasıl Azure CLI 1.0 kullanarak toomanage DNS bölgeleri](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="33587-117">For help, see [How toomanage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="33587-118">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="33587-118">Create hello resource group</span></span>

<span data-ttu-id="33587-119">Merhaba DNS bölgesi oluşturmadan önce bir kaynak grubu toocontain hello DNS bölgesi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="33587-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="33587-120">Merhaba aşağıdaki hello komut gösterir.</span><span class="sxs-lookup"><span data-stu-id="33587-120">hello following shows hello command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="33587-121">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="33587-121">Create a DNS zone</span></span>

<span data-ttu-id="33587-122">Bir DNS bölgesi hello kullanılarak oluşturulan `azure network dns zone create` komutu.</span><span class="sxs-lookup"><span data-stu-id="33587-122">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="33587-123">Bu komutun toosee yardımını yazın `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="33587-123">toosee help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="33587-124">Merhaba aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* adlı hello kaynak grubunda *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="33587-124">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="33587-125">Merhaba örnek toocreate bir DNS bölgesi Hello değerleri kendinizinkilerle değiştirerek kullanın.</span><span class="sxs-lookup"><span data-stu-id="33587-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="33587-126">DNS kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="33587-126">Create a DNS record</span></span>

<span data-ttu-id="33587-127">toocreate bir DNS kaydı kullanmak hello `azure network dns record-set add-record` komutu.</span><span class="sxs-lookup"><span data-stu-id="33587-127">toocreate a DNS record, use hello `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="33587-128">Yardım için bkz. `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="33587-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="33587-129">Merhaba aşağıdaki örnekte bir kayıt hello göreli adı "www" hello "contoso.com", "Contoso.com" kaynak grubunda DNS bölgesi içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="33587-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="33587-130">Merhaba tam hello kayıt kümesi "www.contoso.com" adıdır.</span><span class="sxs-lookup"><span data-stu-id="33587-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="33587-131">Merhaba kayıt türü "A", "1.2.3.4" IP adresiyle olduğundan ve varsayılan TTL 3600 saniye (1 saat) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="33587-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="33587-132">Alternatif TTL değerleri ve toomodify mevcut kayıtları için birden fazla kayıtla kayıt kümeleri için diğer kayıt türleri için bkz: [yönetmek DNS kayıtlarını ve kayıt kümelerini kullanarak hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="33587-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="33587-133">Kayıtları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="33587-133">View records</span></span>

<span data-ttu-id="33587-134">toolist hello DNS kayıtları, bölge içindeki kullanın:</span><span class="sxs-lookup"><span data-stu-id="33587-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="33587-135">Ad sunucularını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="33587-135">Update name servers</span></span>

<span data-ttu-id="33587-136">Sonra DNS bölgesi ve kayıtları doğru şekilde ayarlanan, tooconfigure gerek memnun, etki alanı adı toouse hello Azure DNS ad sunucuları.</span><span class="sxs-lookup"><span data-stu-id="33587-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="33587-137">Bu DNS kayıtlarınızı hello Internet toofind üzerindeki diğer kullanıcılarla sağlar.</span><span class="sxs-lookup"><span data-stu-id="33587-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="33587-138">Merhaba bölgenizin ad sunucuları tarafından hello verilen `azure network dns zone show` komutu:</span><span class="sxs-lookup"><span data-stu-id="33587-138">hello name servers for your zone are given by hello `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

<span data-ttu-id="33587-139">Bu ad sunucuları hello etki alanı adı kayıt (Merhaba etki alanı adı satın aldığınız yerden) ile yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="33587-139">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="33587-140">Şirketiniz hello seçeneği tooset hello ad sunucuları hello etki alanı için yukarı sunar.</span><span class="sxs-lookup"><span data-stu-id="33587-140">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="33587-141">Daha fazla bilgi için bkz: [, etki alanı tooAzure DNS temsilci](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="33587-141">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="33587-142">Tüm kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="33587-142">Delete all resources</span></span>
 
<span data-ttu-id="33587-143">Bu makalede, adım aşağıdaki Al hello oluşturulan tüm kaynakları toodelete:</span><span class="sxs-lookup"><span data-stu-id="33587-143">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="33587-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="33587-144">Next steps</span></span>

<span data-ttu-id="33587-145">Azure DNS hakkında daha fazla toolearn bkz [Azure DNS'ye genel bakış](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="33587-145">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="33587-146">Azure DNS'de DNS bölgelerini yönetme hakkında daha fazla toolearn bkz [yönetmek DNS bölgeleri Azure CLI 1.0 kullanarak Azure DNS'de](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="33587-146">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="33587-147">Azure DNS'de DNS kayıtlarını yönetme hakkında daha fazla toolearn bkz [yönetmek DNS kayıtlarını ve kayıt kümelerini Azure CLI 1.0 kullanarak Azure DNS'de](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="33587-147">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>

