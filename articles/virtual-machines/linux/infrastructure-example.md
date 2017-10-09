---
title: "aaaExample Azure altyapı gözden geçirme | Microsoft Docs"
description: "Bir örnek altyapısını Azure'a dağıtmak için hello anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
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
ms.openlocfilehash: b6b307c0112203aa83e1fada81966fc265397a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a><span data-ttu-id="d0432-103">Linux VM'ler için örnek Azure altyapı gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="d0432-103">Example Azure infrastructure walkthrough for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="d0432-104">Bu makalede örnek uygulama altyapısı oluşturmaya anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0432-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="d0432-105">Biz tüm hello yönergeleri ve adlandırma kuralları, kullanılabilirlik kümeleri, sanal ağlar ve yük dengeleyici kararları bir araya getirir basit bir çevrimiçi mağaza için bir altyapı tasarlama ve gerçekte sanal makineleri (VM'ler) dağıtma ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0432-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="d0432-106">Örnek iş yükü</span><span class="sxs-lookup"><span data-stu-id="d0432-106">Example workload</span></span>
<span data-ttu-id="d0432-107">Adventure Works Cycles toobuild bir çevrimiçi mağaza uygulamasına oluşan Azure istiyor:</span><span class="sxs-lookup"><span data-stu-id="d0432-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="d0432-108">Bir web katmanı ön uç Hello istemcisi çalıştıran iki nginx sunucuları</span><span class="sxs-lookup"><span data-stu-id="d0432-108">Two nginx servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="d0432-109">Veri ve uygulama katmanına siparişler işleme iki nginx sunucuları</span><span class="sxs-lookup"><span data-stu-id="d0432-109">Two nginx servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="d0432-110">Ürün veri ve siparişler bir veritabanı katmanı depolamak için bir parçalı küme iki MongoDB sunucuları parçası</span><span class="sxs-lookup"><span data-stu-id="d0432-110">Two MongoDB servers part of a sharded cluster for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="d0432-111">Müşteri hesapları ve bir kimlik doğrulama katmanı sağlayıcıları için iki Active Directory etki alanı denetleyicisi</span><span class="sxs-lookup"><span data-stu-id="d0432-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="d0432-112">Tüm hello sunucuları iki alt ağ içinde bulunur:</span><span class="sxs-lookup"><span data-stu-id="d0432-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="d0432-113">Merhaba web sunucuları için ön uç bir alt ağ</span><span class="sxs-lookup"><span data-stu-id="d0432-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="d0432-114">Merhaba uygulama sunucuları, MongoDB küme ve etki alanı denetleyicileri için bir arka uç alt ağ</span><span class="sxs-lookup"><span data-stu-id="d0432-114">a back-end subnet for hello application servers, MongoDB cluster, and domain controllers</span></span>

![Uygulama altyapısı için farklı katmanlara diyagramı](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="d0432-116">Güvenli gelen web trafiği olması hello web sunucuları arasında Yük Dengelemesi müşteriler hello çevrimiçi mağaza göz atın.</span><span class="sxs-lookup"><span data-stu-id="d0432-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="d0432-117">Merhaba Web sunucuları yük hello uygulama sunucuları arasında dengeli gerekir hello biçiminde HTTP trafiği işlem sırası ister.</span><span class="sxs-lookup"><span data-stu-id="d0432-117">Order processing traffic in hello form of HTTP requests from hello web servers must be load-balanced among hello application servers.</span></span> <span data-ttu-id="d0432-118">Ayrıca, hello altyapı yüksek kullanılabilirlik için tasarlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0432-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="d0432-119">Merhaba elde edilen tasarım eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="d0432-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="d0432-120">Bir Azure aboneliği ve hesabı</span><span class="sxs-lookup"><span data-stu-id="d0432-120">An Azure subscription and account</span></span>
* <span data-ttu-id="d0432-121">Tek bir kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="d0432-121">A single resource group</span></span>
* <span data-ttu-id="d0432-122">Azure Yönetilen Diskleri</span><span class="sxs-lookup"><span data-stu-id="d0432-122">Azure Managed Disks</span></span>
* <span data-ttu-id="d0432-123">İki alt ağa sahip bir sanal ağ</span><span class="sxs-lookup"><span data-stu-id="d0432-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="d0432-124">Merhaba VM'ler ile benzer bir rolü için kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="d0432-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="d0432-125">Sanal makineler</span><span class="sxs-lookup"><span data-stu-id="d0432-125">Virtual machines</span></span>

<span data-ttu-id="d0432-126">Yukarıdaki tüm hello adlandırma kurallarına izleyin:</span><span class="sxs-lookup"><span data-stu-id="d0432-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="d0432-127">Adventure Works Cycles kullandığı **[BT iş yükü]-[konum]-[Azure kaynak]** öneki olarak</span><span class="sxs-lookup"><span data-stu-id="d0432-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="d0432-128">Bu örneğin, "**azos**" (Azure çevrimiçi mağaza) iş yükü adı hello ve "**kullanmak**" (Doğu ABD 2) hello konumudur</span><span class="sxs-lookup"><span data-stu-id="d0432-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="d0432-129">Sanal ağları kullanın AZOS kullanım VN**[sayı]**</span><span class="sxs-lookup"><span data-stu-id="d0432-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="d0432-130">Kullanılabilirlik kümeleri kullanan azos-kullanın-olarak-**[rol]**</span><span class="sxs-lookup"><span data-stu-id="d0432-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="d0432-131">Sanal makine adları azos kullanın-kullanın-vm -**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="d0432-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="d0432-132">Azure abonelikleri ve hesapları</span><span class="sxs-lookup"><span data-stu-id="d0432-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="d0432-133">Adventure Works Cycles, Adventure Works Kurumsal abonelik, bu BT iş yükü için faturalama tooprovide adlı kurumsal aboneliğini kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="d0432-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="d0432-134">Depolama</span><span class="sxs-lookup"><span data-stu-id="d0432-134">Storage</span></span>
<span data-ttu-id="d0432-135">Adventure Works Cycles Azure yönetilen diskleri kullanması gerektiğini belirledi.</span><span class="sxs-lookup"><span data-stu-id="d0432-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="d0432-136">Sanal makineleri oluştururken, her iki depolama kullanılabilir depolama katmanları kullanılır:</span><span class="sxs-lookup"><span data-stu-id="d0432-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="d0432-137">**Standart depolama** hello web sunucuları, uygulama sunucuları ve etki alanı denetleyicileri ve kendi veri diskleri için.</span><span class="sxs-lookup"><span data-stu-id="d0432-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="d0432-138">**Premium depolama** hello MongoDB parçalı küme sunucuları ve kendi veri diskleri için.</span><span class="sxs-lookup"><span data-stu-id="d0432-138">**Premium storage** for hello MongoDB sharded cluster servers and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="d0432-139">Sanal ağ ve alt ağlar</span><span class="sxs-lookup"><span data-stu-id="d0432-139">Virtual network and subnets</span></span>
<span data-ttu-id="d0432-140">Merhaba sanal ağ sürekli bağlantı toohello Adventure iş döngüsü şirket içi ağ gerekmediği için bir yalnızca bulut sanal ağda karar verdi.</span><span class="sxs-lookup"><span data-stu-id="d0432-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="d0432-141">Bunlar yalnızca bulut sanal ağ ayarlarını hello Azure portal kullanarak aşağıdaki hello ile oluşturulan:</span><span class="sxs-lookup"><span data-stu-id="d0432-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="d0432-142">Name: Kullanım AZOS VN01</span><span class="sxs-lookup"><span data-stu-id="d0432-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="d0432-143">Konumu: Doğu ABD 2</span><span class="sxs-lookup"><span data-stu-id="d0432-143">Location: East US 2</span></span>
* <span data-ttu-id="d0432-144">Sanal ağ adres alanı: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="d0432-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="d0432-145">İlk alt ağ:</span><span class="sxs-lookup"><span data-stu-id="d0432-145">First subnet:</span></span>
  * <span data-ttu-id="d0432-146">Ad: ön uç</span><span class="sxs-lookup"><span data-stu-id="d0432-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="d0432-147">Adres alanı: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="d0432-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="d0432-148">İkinci alt ağ:</span><span class="sxs-lookup"><span data-stu-id="d0432-148">Second subnet:</span></span>
  * <span data-ttu-id="d0432-149">Ad: arka uç</span><span class="sxs-lookup"><span data-stu-id="d0432-149">Name: BackEnd</span></span>
  * <span data-ttu-id="d0432-150">Adres alanı: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="d0432-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="d0432-151">Kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="d0432-151">Availability sets</span></span>
<span data-ttu-id="d0432-152">Adventure Works Cycles dört kullanılabilirlik kümesi üzerinde kampanyanızın çevrimiçi kendi deposunun tüm dört katmanların toomaintain yüksek kullanılabilirlik:</span><span class="sxs-lookup"><span data-stu-id="d0432-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="d0432-153">**web olarak azos kullanım** hello web sunucuları için</span><span class="sxs-lookup"><span data-stu-id="d0432-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="d0432-154">**uygulama olarak azos kullanım** hello uygulama sunucuları için</span><span class="sxs-lookup"><span data-stu-id="d0432-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="d0432-155">**db olarak azos kullanım** hello MongoDB parçalı kümesindeki hello sunucularına</span><span class="sxs-lookup"><span data-stu-id="d0432-155">**azos-use-as-db** for hello servers in hello MongoDB sharded cluster</span></span>
* <span data-ttu-id="d0432-156">**dc olarak azos kullanım** hello etki alanı denetleyicileri için</span><span class="sxs-lookup"><span data-stu-id="d0432-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="d0432-157">Sanal makineler</span><span class="sxs-lookup"><span data-stu-id="d0432-157">Virtual machines</span></span>
<span data-ttu-id="d0432-158">Adventure Works Cycles Azure Vm'leri için adlarından hello karar:</span><span class="sxs-lookup"><span data-stu-id="d0432-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="d0432-159">**Kullanım vm web01 azos** hello ilk web sunucusu için</span><span class="sxs-lookup"><span data-stu-id="d0432-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="d0432-160">**Kullanım vm web02 azos** hello ikinci web sunucusu için</span><span class="sxs-lookup"><span data-stu-id="d0432-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="d0432-161">**Kullanım vm app01 azos** hello ilk uygulama sunucusu için</span><span class="sxs-lookup"><span data-stu-id="d0432-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="d0432-162">**Kullanım vm app02 azos** hello ikinci uygulama sunucusu için</span><span class="sxs-lookup"><span data-stu-id="d0432-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="d0432-163">**Kullanım vm db01 azos** hello kümesindeki ilk MongoDB sunucu hello için</span><span class="sxs-lookup"><span data-stu-id="d0432-163">**azos-use-vm-db01** for hello first MongoDB server in hello cluster</span></span>
* <span data-ttu-id="d0432-164">**Kullanım vm db02 azos** hello kümesindeki hello ikinci MongoDB sunucu için</span><span class="sxs-lookup"><span data-stu-id="d0432-164">**azos-use-vm-db02** for hello second MongoDB server in hello cluster</span></span>
* <span data-ttu-id="d0432-165">**Kullanım vm dc01 azos** hello ilk etki alanı denetleyicisi için</span><span class="sxs-lookup"><span data-stu-id="d0432-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="d0432-166">**Kullanım vm dc02 azos** hello ikinci etki alanı denetleyicisi için</span><span class="sxs-lookup"><span data-stu-id="d0432-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="d0432-167">Merhaba sonuçta elde edilen yapılandırma aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d0432-167">Here is hello resulting configuration.</span></span>

![Azure üzerinde dağıtılan son uygulama altyapısı](./media/infrastructure-example/example-config.png)

<span data-ttu-id="d0432-169">Bu yapılandırma bir araya getirir:</span><span class="sxs-lookup"><span data-stu-id="d0432-169">This configuration incorporates:</span></span>

* <span data-ttu-id="d0432-170">Bir yalnızca bulut sanal ağla iki alt ağ (ön uç ve arka uç)</span><span class="sxs-lookup"><span data-stu-id="d0432-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="d0432-171">Azure yönetilen standart ve Premium diskleri kullanarak diskleri</span><span class="sxs-lookup"><span data-stu-id="d0432-171">Azure Managed Disks using both Standard and Premium disks</span></span>
* <span data-ttu-id="d0432-172">Bir hello çevrimiçi deposunun her katman için dört kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="d0432-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="d0432-173">Merhaba dört katmanları için Hello sanal makineler</span><span class="sxs-lookup"><span data-stu-id="d0432-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="d0432-174">Bir dış yük dengeli küme hello Internet toohello web sunucularından HTTPS tabanlı web trafiği için</span><span class="sxs-lookup"><span data-stu-id="d0432-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="d0432-175">Bir iç yük dengeli küme hello web sunucuları toohello uygulama sunucularından şifrelenmemiş web trafiği için</span><span class="sxs-lookup"><span data-stu-id="d0432-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="d0432-176">Tek bir kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="d0432-176">A single resource group</span></span>
