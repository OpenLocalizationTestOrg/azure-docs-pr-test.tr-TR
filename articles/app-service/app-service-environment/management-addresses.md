---
title: "Azure uygulama hizmeti ortamı yönetimi adresleri"
description: "Bir uygulama hizmeti ortamı komutu için kullanılan yönetim adreslerini listeler"
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
ms.openlocfilehash: e97a084772fd16252d925b62498d2e696629a25d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="cfb21-103">Uygulama hizmeti ortamı yönetimi adresleri</span><span class="sxs-lookup"><span data-stu-id="cfb21-103">App Service Environment management addresses</span></span>

<span data-ttu-id="cfb21-104">Uygulama hizmeti Environment(ASE) Azure uygulama hizmeti dağıtımı Azure sanal ağınızda (VNet) bir alt ağ içinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="cfb21-104">The App Service Environment(ASE) is a deployment of the Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="cfb21-105">Böylece, yönetilebilmesi için ana Azure App hizmetinden erişilebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cfb21-105">The ASE must be accessible from the Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="cfb21-106">Bu ana yönetim trafiği, kullanıcı tarafından denetlenen ağ erişir.</span><span class="sxs-lookup"><span data-stu-id="cfb21-106">This ASE management traffic traverses the user controlled network.</span></span>  <span data-ttu-id="cfb21-107">Azure uygulama hizmeti yönetim sunucularından ana ile ilişkili ortak VIP için gelir.</span><span class="sxs-lookup"><span data-stu-id="cfb21-107">It comes from Azure App Service management servers to the public VIP that is associated with the ASE.</span></span>  <span data-ttu-id="cfb21-108">Ana hakkında ayrıntılı bilgi için ağ okuma bağımlılıkları [ağ konuları ve uygulama hizmeti ortamı][networking].</span><span class="sxs-lookup"><span data-stu-id="cfb21-108">For details on the ASE networking dependencies read [Networking considerations and the App Service Environment][networking].</span></span>  <span data-ttu-id="cfb21-109">Ana hakkında genel bilgi için ile başlatabilirsiniz [uygulama hizmeti ortamı giriş][intro].</span><span class="sxs-lookup"><span data-stu-id="cfb21-109">For general information on the ASE you can start with [Introduction to the App Service Environment][intro].</span></span>

<span data-ttu-id="cfb21-110">Bu belge, yönetim trafiği için ana IP'leri kaynak listeler.</span><span class="sxs-lookup"><span data-stu-id="cfb21-110">This document lists the source IPs for management traffic to the ASE.</span></span> <span data-ttu-id="cfb21-111">Bu adreslerden gelen trafiği kilitlemek veya bunları gerektiği gibi rota tablolarda kullanmak için ağ güvenlik grupları oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cfb21-111">You can use these addresses to create Network Security Groups to lock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="cfb21-112">Bu bilgileri kullanmak için kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="cfb21-112">To use this information you need to use:</span></span>

* <span data-ttu-id="cfb21-113">Tüm bölgeler için listelenen IP adresleri</span><span class="sxs-lookup"><span data-stu-id="cfb21-113">the IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="cfb21-114">içine, ana dağıtılan bölge için aynı IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="cfb21-114">the IP addresses that match to the region that your ASE is deployed into.</span></span>

<span data-ttu-id="cfb21-115">Gelen yönetim trafiğini bu IP adreslerinden 454 ve 455 bağlantı noktalarına gelir.</span><span class="sxs-lookup"><span data-stu-id="cfb21-115">The incoming management traffic comes in from these IP addresses to ports 454 and 455.</span></span>

| <span data-ttu-id="cfb21-116">Bölge</span><span class="sxs-lookup"><span data-stu-id="cfb21-116">Region</span></span> | <span data-ttu-id="cfb21-117">Adresler</span><span class="sxs-lookup"><span data-stu-id="cfb21-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="cfb21-118">Tüm bölgeler</span><span class="sxs-lookup"><span data-stu-id="cfb21-118">All regions</span></span> | <span data-ttu-id="cfb21-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="cfb21-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="cfb21-120">Orta Güney ABD & Kuzey Orta ABD</span><span class="sxs-lookup"><span data-stu-id="cfb21-120">South Central US & North Central US</span></span> | <span data-ttu-id="cfb21-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="cfb21-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="cfb21-122">Avustralya Güneydoğu & Avustralya Doğu</span><span class="sxs-lookup"><span data-stu-id="cfb21-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="cfb21-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="cfb21-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="cfb21-124">ABD Batı & ABD Doğu</span><span class="sxs-lookup"><span data-stu-id="cfb21-124">US West & US East</span></span> | <span data-ttu-id="cfb21-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="cfb21-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="cfb21-126">Batı Avrupa & Kuzey Avrupa</span><span class="sxs-lookup"><span data-stu-id="cfb21-126">West Europe & North Europe</span></span> | <span data-ttu-id="cfb21-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="cfb21-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="cfb21-128">Batı Orta ABD & Batı ABD 2</span><span class="sxs-lookup"><span data-stu-id="cfb21-128">West Central US & West US 2</span></span> | <span data-ttu-id="cfb21-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="cfb21-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="cfb21-130">Orta ABD & Doğu ABD 2</span><span class="sxs-lookup"><span data-stu-id="cfb21-130">Central US & East US 2</span></span> | <span data-ttu-id="cfb21-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="cfb21-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="cfb21-132">Doğu Asya & Güneydoğu Asya</span><span class="sxs-lookup"><span data-stu-id="cfb21-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="cfb21-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="cfb21-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="cfb21-134">Japonya Doğu & Japonya Batı</span><span class="sxs-lookup"><span data-stu-id="cfb21-134">Japan East & Japan West</span></span> | <span data-ttu-id="cfb21-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="cfb21-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="cfb21-136">Kanada Orta & Doğu Kanada</span><span class="sxs-lookup"><span data-stu-id="cfb21-136">Canada Central & Canada East</span></span> | <span data-ttu-id="cfb21-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="cfb21-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="cfb21-138">Birleşik Krallık Batı & Birleşik Krallık Güney</span><span class="sxs-lookup"><span data-stu-id="cfb21-138">UK West & UK South</span></span> | <span data-ttu-id="cfb21-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="cfb21-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="cfb21-140">Kore Güney & Kore Merkezi</span><span class="sxs-lookup"><span data-stu-id="cfb21-140">Korea South & Korea Central</span></span> | <span data-ttu-id="cfb21-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="cfb21-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="cfb21-142">Brezilya Güney & Orta Güney ABD</span><span class="sxs-lookup"><span data-stu-id="cfb21-142">Brazil South & South Central US</span></span>| <span data-ttu-id="cfb21-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="cfb21-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="cfb21-144">Orta Hindistan & Güney Hindistan</span><span class="sxs-lookup"><span data-stu-id="cfb21-144">Central India & South India</span></span> | <span data-ttu-id="cfb21-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="cfb21-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="cfb21-146">Batı Hindistan & Güney Hindistan</span><span class="sxs-lookup"><span data-stu-id="cfb21-146">West India & South India</span></span> | <span data-ttu-id="cfb21-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="cfb21-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
