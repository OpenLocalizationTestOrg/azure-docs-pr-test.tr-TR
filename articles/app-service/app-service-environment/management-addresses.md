---
title: "aaaAzure uygulama hizmeti ortamı yönetimi adresleri"
description: "Bir uygulama hizmeti ortamı toocommand kullanılan listeleri hello yönetim adresleri"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="c999b-103">Uygulama hizmeti ortamı yönetimi adresleri</span><span class="sxs-lookup"><span data-stu-id="c999b-103">App Service Environment management addresses</span></span>

<span data-ttu-id="c999b-104">Merhaba App Service Environment(ASE) Azure sanal ağınızda (VNet) bir alt ağ içinde hello Azure App Service dağıtımı ' dir.</span><span class="sxs-lookup"><span data-stu-id="c999b-104">hello App Service Environment(ASE) is a deployment of hello Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="c999b-105">Böylece, yönetilebilmesi için hello ana hello Azure App Service ' erişilebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c999b-105">hello ASE must be accessible from hello Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="c999b-106">Bu ana yönetim trafiği hello kullanıcı tarafından denetlenen ağ erişir.</span><span class="sxs-lookup"><span data-stu-id="c999b-106">This ASE management traffic traverses hello user controlled network.</span></span>  <span data-ttu-id="c999b-107">Merhaba ana ile ilişkili Azure uygulama hizmeti yönetim sunucuları toohello genel VIP geldiği.</span><span class="sxs-lookup"><span data-stu-id="c999b-107">It comes from Azure App Service management servers toohello public VIP that is associated with hello ASE.</span></span>  <span data-ttu-id="c999b-108">Bağımlılıklar ağ hello ana hakkında ayrıntılı bilgi için okuma [ağ konuları ve hello uygulama hizmeti ortamı][networking].</span><span class="sxs-lookup"><span data-stu-id="c999b-108">For details on hello ASE networking dependencies read [Networking considerations and hello App Service Environment][networking].</span></span>  <span data-ttu-id="c999b-109">Merhaba ana hakkında genel bilgi için ile başlatabilirsiniz [giriş toohello uygulama hizmeti ortamı][intro].</span><span class="sxs-lookup"><span data-stu-id="c999b-109">For general information on hello ASE you can start with [Introduction toohello App Service Environment][intro].</span></span>

<span data-ttu-id="c999b-110">Bu belge hello kaynağı IP'leri yönetim trafiğini toohello ana listeler.</span><span class="sxs-lookup"><span data-stu-id="c999b-110">This document lists hello source IPs for management traffic toohello ASE.</span></span> <span data-ttu-id="c999b-111">Bu adresleri toocreate ağ güvenlik grupları toolock gelen trafiği tuşunu kullanın veya bunları gerektiği gibi rota tablolarda kullanın.</span><span class="sxs-lookup"><span data-stu-id="c999b-111">You can use these addresses toocreate Network Security Groups toolock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="c999b-112">toouse toouse bu gerekenler:</span><span class="sxs-lookup"><span data-stu-id="c999b-112">toouse this information you need toouse:</span></span>

* <span data-ttu-id="c999b-113">Tüm bölgeler için listelenen hello IP adresleri</span><span class="sxs-lookup"><span data-stu-id="c999b-113">hello IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="c999b-114">içine, ana dağıtılan o eşleşme toohello bölge Hello IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="c999b-114">hello IP addresses that match toohello region that your ASE is deployed into.</span></span>

<span data-ttu-id="c999b-115">Merhaba gelen yönetim trafiğini bu IP adreslerinden tooports 454 ve 455 gelir.</span><span class="sxs-lookup"><span data-stu-id="c999b-115">hello incoming management traffic comes in from these IP addresses tooports 454 and 455.</span></span>

| <span data-ttu-id="c999b-116">Bölge</span><span class="sxs-lookup"><span data-stu-id="c999b-116">Region</span></span> | <span data-ttu-id="c999b-117">Adresler</span><span class="sxs-lookup"><span data-stu-id="c999b-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="c999b-118">Tüm bölgeler</span><span class="sxs-lookup"><span data-stu-id="c999b-118">All regions</span></span> | <span data-ttu-id="c999b-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="c999b-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="c999b-120">Orta Güney ABD & Kuzey Orta ABD</span><span class="sxs-lookup"><span data-stu-id="c999b-120">South Central US & North Central US</span></span> | <span data-ttu-id="c999b-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="c999b-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="c999b-122">Avustralya Güneydoğu & Avustralya Doğu</span><span class="sxs-lookup"><span data-stu-id="c999b-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="c999b-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="c999b-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="c999b-124">ABD Batı & ABD Doğu</span><span class="sxs-lookup"><span data-stu-id="c999b-124">US West & US East</span></span> | <span data-ttu-id="c999b-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="c999b-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="c999b-126">Batı Avrupa & Kuzey Avrupa</span><span class="sxs-lookup"><span data-stu-id="c999b-126">West Europe & North Europe</span></span> | <span data-ttu-id="c999b-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="c999b-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="c999b-128">Batı Orta ABD & Batı ABD 2</span><span class="sxs-lookup"><span data-stu-id="c999b-128">West Central US & West US 2</span></span> | <span data-ttu-id="c999b-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="c999b-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="c999b-130">Orta ABD & Doğu ABD 2</span><span class="sxs-lookup"><span data-stu-id="c999b-130">Central US & East US 2</span></span> | <span data-ttu-id="c999b-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="c999b-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="c999b-132">Doğu Asya & Güneydoğu Asya</span><span class="sxs-lookup"><span data-stu-id="c999b-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="c999b-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="c999b-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="c999b-134">Japonya Doğu & Japonya Batı</span><span class="sxs-lookup"><span data-stu-id="c999b-134">Japan East & Japan West</span></span> | <span data-ttu-id="c999b-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="c999b-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="c999b-136">Kanada Orta & Doğu Kanada</span><span class="sxs-lookup"><span data-stu-id="c999b-136">Canada Central & Canada East</span></span> | <span data-ttu-id="c999b-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="c999b-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="c999b-138">Birleşik Krallık Batı & Birleşik Krallık Güney</span><span class="sxs-lookup"><span data-stu-id="c999b-138">UK West & UK South</span></span> | <span data-ttu-id="c999b-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="c999b-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="c999b-140">Kore Güney & Kore Merkezi</span><span class="sxs-lookup"><span data-stu-id="c999b-140">Korea South & Korea Central</span></span> | <span data-ttu-id="c999b-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="c999b-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="c999b-142">Brezilya Güney & Orta Güney ABD</span><span class="sxs-lookup"><span data-stu-id="c999b-142">Brazil South & South Central US</span></span>| <span data-ttu-id="c999b-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="c999b-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="c999b-144">Orta Hindistan & Güney Hindistan</span><span class="sxs-lookup"><span data-stu-id="c999b-144">Central India & South India</span></span> | <span data-ttu-id="c999b-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="c999b-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="c999b-146">Batı Hindistan & Güney Hindistan</span><span class="sxs-lookup"><span data-stu-id="c999b-146">West India & South India</span></span> | <span data-ttu-id="c999b-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="c999b-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
