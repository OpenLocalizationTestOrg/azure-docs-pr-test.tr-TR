---
title: "Örnek Azure altyapı gözden geçirme | Microsoft Docs"
description: "Bir örnek altyapısını Azure'a dağıtmak için anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b18be0d81d6fad7328edb47c9b69af4eecd3b971
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a><span data-ttu-id="6aead-103">Linux VM'ler için örnek Azure altyapı gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="6aead-103">Example Azure infrastructure walkthrough for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="6aead-104">Bu makalede örnek uygulama altyapısı oluşturmaya anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6aead-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="6aead-105">Biz yönergeleri ve adlandırma kuralları, kullanılabilirlik kümeleri, sanal ağlar ve yük dengeleyici kararları bir araya getirir basit bir çevrimiçi mağaza için bir altyapı tasarlama ve gerçekte sanal makineleri (VM'ler) dağıtma ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6aead-105">We detail designing an infrastructure for a simple on-line store that brings together all the guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="6aead-106">Örnek iş yükü</span><span class="sxs-lookup"><span data-stu-id="6aead-106">Example workload</span></span>
<span data-ttu-id="6aead-107">Adventure Works Cycles, azure'da oluşan bir çevrimiçi mağaza uygulama oluşturmak ister:</span><span class="sxs-lookup"><span data-stu-id="6aead-107">Adventure Works Cycles wants to build an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="6aead-108">Bir web katmanı ön uç istemcisi çalıştıran iki nginx sunucuları</span><span class="sxs-lookup"><span data-stu-id="6aead-108">Two nginx servers running the client front-end in a web tier</span></span>
* <span data-ttu-id="6aead-109">Veri ve uygulama katmanına siparişler işleme iki nginx sunucuları</span><span class="sxs-lookup"><span data-stu-id="6aead-109">Two nginx servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="6aead-110">Ürün veri ve siparişler bir veritabanı katmanı depolamak için bir parçalı küme iki MongoDB sunucuları parçası</span><span class="sxs-lookup"><span data-stu-id="6aead-110">Two MongoDB servers part of a sharded cluster for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="6aead-111">Müşteri hesapları ve bir kimlik doğrulama katmanı sağlayıcıları için iki Active Directory etki alanı denetleyicisi</span><span class="sxs-lookup"><span data-stu-id="6aead-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="6aead-112">Tüm sunucular iki alt ağ içinde bulunur:</span><span class="sxs-lookup"><span data-stu-id="6aead-112">All the servers are located in two subnets:</span></span>
  * <span data-ttu-id="6aead-113">web sunucuları için ön uç bir alt ağ</span><span class="sxs-lookup"><span data-stu-id="6aead-113">a front-end subnet for the web servers</span></span> 
  * <span data-ttu-id="6aead-114">uygulama sunucuları, MongoDB küme ve etki alanı denetleyicileri için bir arka uç alt ağ</span><span class="sxs-lookup"><span data-stu-id="6aead-114">a back-end subnet for the application servers, MongoDB cluster, and domain controllers</span></span>

![Uygulama altyapısı için farklı katmanlara diyagramı](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="6aead-116">Güvenli gelen web trafiği gerekir yük dengeli web sunucular arasında müşteriler çevrimiçi mağaza gezinirken.</span><span class="sxs-lookup"><span data-stu-id="6aead-116">Incoming secure web traffic must be load-balanced among the web servers as customers browse the on-line store.</span></span> <span data-ttu-id="6aead-117">Sunucular-uygulama sunucuları arasında dengeli yük gerekir Web trafiği HTTP biçiminde işlem sırası ister.</span><span class="sxs-lookup"><span data-stu-id="6aead-117">Order processing traffic in the form of HTTP requests from the web servers must be load-balanced among the application servers.</span></span> <span data-ttu-id="6aead-118">Ayrıca, altyapı yüksek kullanılabilirlik için tasarlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6aead-118">Additionally, the infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="6aead-119">Sonuçta elde edilen tasarım eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6aead-119">The resulting design must incorporate:</span></span>

* <span data-ttu-id="6aead-120">Bir Azure aboneliği ve hesabı</span><span class="sxs-lookup"><span data-stu-id="6aead-120">An Azure subscription and account</span></span>
* <span data-ttu-id="6aead-121">Tek bir kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="6aead-121">A single resource group</span></span>
* <span data-ttu-id="6aead-122">Azure Yönetilen Diskleri</span><span class="sxs-lookup"><span data-stu-id="6aead-122">Azure Managed Disks</span></span>
* <span data-ttu-id="6aead-123">İki alt ağa sahip bir sanal ağ</span><span class="sxs-lookup"><span data-stu-id="6aead-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="6aead-124">Benzer bir rolü olan VM'ler için kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="6aead-124">Availability sets for the VMs with a similar role</span></span>
* <span data-ttu-id="6aead-125">Sanal makineler</span><span class="sxs-lookup"><span data-stu-id="6aead-125">Virtual machines</span></span>

<span data-ttu-id="6aead-126">Tüm yukarıdaki adlandırma kurallarına izleyin:</span><span class="sxs-lookup"><span data-stu-id="6aead-126">All the above follow these naming conventions:</span></span>

* <span data-ttu-id="6aead-127">Adventure Works Cycles kullandığı **[BT iş yükü]-[konum]-[Azure kaynak]** öneki olarak</span><span class="sxs-lookup"><span data-stu-id="6aead-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="6aead-128">Bu örneğin, "**azos**" (Azure çevrimiçi) deposudur BT iş yükü adı ve "**kullanmak**" (Doğu ABD 2) konumudur</span><span class="sxs-lookup"><span data-stu-id="6aead-128">For this example, "**azos**" (Azure On-line Store) is the IT workload name and "**use**" (East US 2) is the location</span></span>
* <span data-ttu-id="6aead-129">Sanal ağları kullanın AZOS kullanım VN**[sayı]**</span><span class="sxs-lookup"><span data-stu-id="6aead-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="6aead-130">Kullanılabilirlik kümeleri kullanan azos-kullanın-olarak-**[rol]**</span><span class="sxs-lookup"><span data-stu-id="6aead-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="6aead-131">Sanal makine adları azos kullanın-kullanın-vm -**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="6aead-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="6aead-132">Azure abonelikleri ve hesapları</span><span class="sxs-lookup"><span data-stu-id="6aead-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="6aead-133">Adventure Works Cycles, bu BT iş yükü için fatura sağlamak için Adventure Works Kurumsal aboneliği adlı kurumsal aboneliğini kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="6aead-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, to provide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="6aead-134">Depolama</span><span class="sxs-lookup"><span data-stu-id="6aead-134">Storage</span></span>
<span data-ttu-id="6aead-135">Adventure Works Cycles Azure yönetilen diskleri kullanması gerektiğini belirledi.</span><span class="sxs-lookup"><span data-stu-id="6aead-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="6aead-136">Sanal makineleri oluştururken, her iki depolama kullanılabilir depolama katmanları kullanılır:</span><span class="sxs-lookup"><span data-stu-id="6aead-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="6aead-137">**Standart depolama** web sunucuları, uygulama sunucuları ve etki alanı denetleyicileri ve kendi veri diskleri için.</span><span class="sxs-lookup"><span data-stu-id="6aead-137">**Standard storage** for the web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="6aead-138">**Premium depolama** MongoDB parçalı küme sunucuları ve kendi veri diskleri için.</span><span class="sxs-lookup"><span data-stu-id="6aead-138">**Premium storage** for the MongoDB sharded cluster servers and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="6aead-139">Sanal ağ ve alt ağlar</span><span class="sxs-lookup"><span data-stu-id="6aead-139">Virtual network and subnets</span></span>
<span data-ttu-id="6aead-140">Sanal ağ Adventure iş döngüsü şirket ağına sürekli bağlantı gerekmediği için bir yalnızca bulut sanal ağda karar verdi.</span><span class="sxs-lookup"><span data-stu-id="6aead-140">Because the virtual network does not need ongoing connectivity to the Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="6aead-141">Azure Portalı'nı kullanarak aşağıdaki ayarlara sahip bir yalnızca bulut sanal ağ oluşturma:</span><span class="sxs-lookup"><span data-stu-id="6aead-141">They created a cloud-only virtual network with the following settings using the Azure portal:</span></span>

* <span data-ttu-id="6aead-142">Name: Kullanım AZOS VN01</span><span class="sxs-lookup"><span data-stu-id="6aead-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="6aead-143">Konumu: Doğu ABD 2</span><span class="sxs-lookup"><span data-stu-id="6aead-143">Location: East US 2</span></span>
* <span data-ttu-id="6aead-144">Sanal ağ adres alanı: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="6aead-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="6aead-145">İlk alt ağ:</span><span class="sxs-lookup"><span data-stu-id="6aead-145">First subnet:</span></span>
  * <span data-ttu-id="6aead-146">Ad: ön uç</span><span class="sxs-lookup"><span data-stu-id="6aead-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="6aead-147">Adres alanı: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="6aead-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="6aead-148">İkinci alt ağ:</span><span class="sxs-lookup"><span data-stu-id="6aead-148">Second subnet:</span></span>
  * <span data-ttu-id="6aead-149">Ad: arka uç</span><span class="sxs-lookup"><span data-stu-id="6aead-149">Name: BackEnd</span></span>
  * <span data-ttu-id="6aead-150">Adres alanı: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="6aead-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="6aead-151">Kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="6aead-151">Availability sets</span></span>
<span data-ttu-id="6aead-152">Çevrimiçi depolarındaki tüm dört katmanların yüksek kullanılabilirliği sürdürmek için Adventure Works Cycles dört kullanılabilirlik kümeleri hakkında karar:</span><span class="sxs-lookup"><span data-stu-id="6aead-152">To maintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="6aead-153">**web olarak azos kullanım** web sunucuları için</span><span class="sxs-lookup"><span data-stu-id="6aead-153">**azos-use-as-web** for the web servers</span></span>
* <span data-ttu-id="6aead-154">**uygulama olarak azos kullanım** uygulama sunucuları için</span><span class="sxs-lookup"><span data-stu-id="6aead-154">**azos-use-as-app** for the application servers</span></span>
* <span data-ttu-id="6aead-155">**db olarak azos kullanım** MongoDB parçalı kümesindeki sunucular için</span><span class="sxs-lookup"><span data-stu-id="6aead-155">**azos-use-as-db** for the servers in the MongoDB sharded cluster</span></span>
* <span data-ttu-id="6aead-156">**dc olarak azos kullanım** etki alanı denetleyicileri</span><span class="sxs-lookup"><span data-stu-id="6aead-156">**azos-use-as-dc** for the domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="6aead-157">Sanal makineler</span><span class="sxs-lookup"><span data-stu-id="6aead-157">Virtual machines</span></span>
<span data-ttu-id="6aead-158">Adventure Works Cycles Azure Vm'leri için aşağıdaki adlar karar:</span><span class="sxs-lookup"><span data-stu-id="6aead-158">Adventure Works Cycles decided on the following names for their Azure VMs:</span></span>

* <span data-ttu-id="6aead-159">**Kullanım vm web01 azos** ilk web sunucusu için</span><span class="sxs-lookup"><span data-stu-id="6aead-159">**azos-use-vm-web01** for the first web server</span></span>
* <span data-ttu-id="6aead-160">**Kullanım vm web02 azos** ikinci web sunucusu için</span><span class="sxs-lookup"><span data-stu-id="6aead-160">**azos-use-vm-web02** for the second web server</span></span>
* <span data-ttu-id="6aead-161">**Kullanım vm app01 azos** için ilk uygulama sunucusu</span><span class="sxs-lookup"><span data-stu-id="6aead-161">**azos-use-vm-app01** for the first application server</span></span>
* <span data-ttu-id="6aead-162">**Kullanım vm app02 azos** ikinci uygulama sunucusu için</span><span class="sxs-lookup"><span data-stu-id="6aead-162">**azos-use-vm-app02** for the second application server</span></span>
* <span data-ttu-id="6aead-163">**Kullanım vm db01 azos** kümedeki ilk MongoDB sunucu için</span><span class="sxs-lookup"><span data-stu-id="6aead-163">**azos-use-vm-db01** for the first MongoDB server in the cluster</span></span>
* <span data-ttu-id="6aead-164">**Kullanım vm db02 azos** kümedeki ikinci MongoDB sunucu için</span><span class="sxs-lookup"><span data-stu-id="6aead-164">**azos-use-vm-db02** for the second MongoDB server in the cluster</span></span>
* <span data-ttu-id="6aead-165">**Kullanım vm dc01 azos** ilk etki alanı denetleyicisi</span><span class="sxs-lookup"><span data-stu-id="6aead-165">**azos-use-vm-dc01** for the first domain controller</span></span>
* <span data-ttu-id="6aead-166">**Kullanım vm dc02 azos** ikinci etki alanı denetleyicisi</span><span class="sxs-lookup"><span data-stu-id="6aead-166">**azos-use-vm-dc02** for the second domain controller</span></span>

<span data-ttu-id="6aead-167">Sonuçta elde edilen yapılandırma aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6aead-167">Here is the resulting configuration.</span></span>

![Azure üzerinde dağıtılan son uygulama altyapısı](./media/infrastructure-example/example-config.png)

<span data-ttu-id="6aead-169">Bu yapılandırma bir araya getirir:</span><span class="sxs-lookup"><span data-stu-id="6aead-169">This configuration incorporates:</span></span>

* <span data-ttu-id="6aead-170">Bir yalnızca bulut sanal ağla iki alt ağ (ön uç ve arka uç)</span><span class="sxs-lookup"><span data-stu-id="6aead-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="6aead-171">Azure yönetilen standart ve Premium diskleri kullanarak diskleri</span><span class="sxs-lookup"><span data-stu-id="6aead-171">Azure Managed Disks using both Standard and Premium disks</span></span>
* <span data-ttu-id="6aead-172">Bir çevrimiçi mağaza, her katman için dört kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="6aead-172">Four availability sets, one for each tier of the on-line store</span></span>
* <span data-ttu-id="6aead-173">Sanal makineler için dört katman</span><span class="sxs-lookup"><span data-stu-id="6aead-173">The virtual machines for the four tiers</span></span>
* <span data-ttu-id="6aead-174">Internet'ten HTTPS tabanlı web trafiği web sunucuları için bir dış yük dengeli küme</span><span class="sxs-lookup"><span data-stu-id="6aead-174">An external load balanced set for HTTPS-based web traffic from the Internet to the web servers</span></span>
* <span data-ttu-id="6aead-175">Bir iç yük dengeli küme web sunucularından şifrelenmemiş web trafiği uygulama sunucuları için</span><span class="sxs-lookup"><span data-stu-id="6aead-175">An internal load balanced set for unencrypted web traffic from the web servers to the application servers</span></span>
* <span data-ttu-id="6aead-176">Tek bir kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="6aead-176">A single resource group</span></span>
