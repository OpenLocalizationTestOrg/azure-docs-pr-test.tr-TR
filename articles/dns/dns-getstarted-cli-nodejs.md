---
title: "Azure CLI 1.0 ile Azure DNS kullanmaya başlama | Microsoft Docs"
description: "Azure DNS'te DNS bölgesi ve kaydı oluşturma hakkında bilgi edinin. Bu kılavuzda, Azure CLI 1.0 kullanarak ilk DNS bölgenizi ve kaydınızı oluşturup yönetmeniz için adım adım talimatlar sunulmaktadır."
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
ms.openlocfilehash: f7943b71bbd16c36df09436973d92539eb62b210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="1cd09-104">Azure CLI 1.0 kullanarak Azure DNS ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1cd09-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1cd09-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="1cd09-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="1cd09-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1cd09-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="1cd09-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1cd09-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="1cd09-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1cd09-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="1cd09-109">Bu makale Windows, Mac ve Linux platformlarında kullanılabilen platformlar arası Azure CLI 1.0'ı kullanarak ilk DNS bölgenizi ve kaydınızı oluşturma adımlarında size rehberlik yapacaktır.</span><span class="sxs-lookup"><span data-stu-id="1cd09-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="1cd09-110">Ayrıca, Azure portal veya Azure PowerShell kullanarak aşağıdaki adımları gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cd09-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="1cd09-111">DNS bölgesi belirli bir etki alanıyla ilgili DNS kayıtlarını barındırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1cd09-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="1cd09-112">Etki alanınızı Azure DNS'de barındırmaya başlamak için bir DNS bölgesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cd09-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="1cd09-113">Ardından bu DNS bölgesinde etki alanınız için tüm DNS kayıtları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1cd09-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="1cd09-114">Son olarak, DNS bölgenizi Internet'te yayımlamak için etki alanının ad sunucularını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cd09-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="1cd09-115">Bu adımların her biri aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1cd09-115">Each of these steps is described below.</span></span>

<span data-ttu-id="1cd09-116">Bu yönergeler, Azure CLI 1.0’ı zaten yüklediğinizi ve oturum açtığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="1cd09-116">These instructions assume you have already installed and signed in to Azure CLI 1.0.</span></span> <span data-ttu-id="1cd09-117">Yardım için bkz. [Azure CLI 1.0 ile DNS bölgelerini yönetme](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1cd09-117">For help, see [How to manage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="1cd09-118">Kaynak grubunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cd09-118">Create the resource group</span></span>

<span data-ttu-id="1cd09-119">DNS bölgesini oluşturmadan önce, DNS Bölgesi’ni içerecek bir kaynak grubu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1cd09-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="1cd09-120">Aşağıda, komut gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1cd09-120">The following shows the command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="1cd09-121">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cd09-121">Create a DNS zone</span></span>

<span data-ttu-id="1cd09-122">DNS bölgesi, `azure network dns zone create` komutu kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1cd09-122">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="1cd09-123">Bu komutla ilgili yardım içeriğini görmek için `azure network dns zone create -h` yazın.</span><span class="sxs-lookup"><span data-stu-id="1cd09-123">To see help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="1cd09-124">Aşağıdaki örnek, *MyResourceGroup* adlı kaynak grubunda *contoso.com* adlı bir DNS bölgesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1cd09-124">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="1cd09-125">Değerleri kendinizinkilerle değiştirerek DNS bölgesini oluşturmak için örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="1cd09-125">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="1cd09-126">DNS kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cd09-126">Create a DNS record</span></span>

<span data-ttu-id="1cd09-127">DNS kaydı oluşturmak için `azure network dns record-set add-record` komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1cd09-127">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="1cd09-128">Yardım için bkz. `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="1cd09-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="1cd09-129">Aşağıdaki örnekte, "MyResourceGroup" kaynak grubu içindeki "contoso.com" DNS Bölgesinde göreli adı "www" olan bir kaynak oluşturulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1cd09-129">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="1cd09-130">"www.contoso.com", kayıt kümesinin tam adıdır.</span><span class="sxs-lookup"><span data-stu-id="1cd09-130">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="1cd09-131">Kayıt türü "A", IP adresi "1.2.3.4" ve varsayılan TTL değeri 3600 saniyedir (1 saat).</span><span class="sxs-lookup"><span data-stu-id="1cd09-131">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="1cd09-132">Diğer kayıt türleri, birden fazla kayıt içerek kayıt kümeleri, alternatif TTL değerleri ve var olan kayıtların değiştirilmesi hakkında bilgi için bkz. [Azure CLI 1.0 kullanarak DNS kayıtlarını ve kayıt kümelerini yönetme](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1cd09-132">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="1cd09-133">Kayıtları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="1cd09-133">View records</span></span>

<span data-ttu-id="1cd09-134">Bölgenizdeki DNS kayıtlarını listelemek için şu seçenekleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="1cd09-134">To list the DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="1cd09-135">Ad sunucularını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="1cd09-135">Update name servers</span></span>

<span data-ttu-id="1cd09-136">DNS bölgenizin ve kayıtlarınızın doğru şekilde ayarlandığına karar verdikten sonra, Azure DNS ad sunucularını kullanmak için etki alanınızın adını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cd09-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="1cd09-137">Bunun yapılması, İnternet üzerindeki diğer kullanıcıların DNS kayıtlarınızı bulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="1cd09-137">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="1cd09-138">Bölgenizin ad sunucuları `azure network dns zone show` komutu tarafından belirtilir:</span><span class="sxs-lookup"><span data-stu-id="1cd09-138">The name servers for your zone are given by the `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
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

<span data-ttu-id="1cd09-139">Bu ad sunucuları, etki alanı adı kayıt şirketi (etki alanı adını satın aldığınız şirket) ile birlikte yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1cd09-139">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="1cd09-140">Kayıt şirketiniz, etki alanı için ad sunucularını ayarlama seçeneğini sunar.</span><span class="sxs-lookup"><span data-stu-id="1cd09-140">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="1cd09-141">Daha fazla bilgi için bkz. [Etki alanınızı Azure DNS’e devretme](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="1cd09-141">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="1cd09-142">Tüm kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="1cd09-142">Delete all resources</span></span>
 
<span data-ttu-id="1cd09-143">Bu makalede oluşturulan tüm kaynakları silmek için, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="1cd09-143">To delete all resources created in this article, take the following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="1cd09-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1cd09-144">Next steps</span></span>

<span data-ttu-id="1cd09-145">Azure DNS hakkında daha fazla bilgi için bkz. [Azure DNS'e genel bakış](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1cd09-145">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="1cd09-146">Azure DNS’te DNS bölgelerini yönetme hakkında daha fazla bilgi için bkz. [Azure CLI 1.0 ile Azure DNS’te DNS bölgelerini yönetme](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1cd09-146">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="1cd09-147">Azure DNS’te DNS kayıtlarını yönetme hakkında daha fazla bilgi için bkz. [Azure CLI 1.0 ile Azure DNS’te DNS kayıtlarını yönetme](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1cd09-147">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>

