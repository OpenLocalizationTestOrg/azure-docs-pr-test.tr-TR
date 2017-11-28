---
title: "aaaExample Azure altyapı gözden geçirme | Microsoft Docs"
description: "Bir örnek altyapısını Azure'a dağıtmak için hello anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a><span data-ttu-id="58155-103">Windows VM'ler için örnek Azure altyapı gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="58155-103">Example Azure infrastructure walkthrough for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="58155-104">Bu makalede örnek uygulama altyapısı oluşturmaya anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="58155-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="58155-105">Biz tüm hello yönergeleri ve adlandırma kuralları, kullanılabilirlik kümeleri, sanal ağlar ve yük dengeleyici kararları bir araya getirir basit bir çevrimiçi mağaza için bir altyapı tasarlama ve gerçekte sanal makineleri (VM'ler) dağıtma ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="58155-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="58155-106">Örnek iş yükü</span><span class="sxs-lookup"><span data-stu-id="58155-106">Example workload</span></span>
<span data-ttu-id="58155-107">Adventure Works Cycles toobuild bir çevrimiçi mağaza uygulamasına oluşan Azure istiyor:</span><span class="sxs-lookup"><span data-stu-id="58155-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="58155-108">Bir web katmanı ön uç Hello istemci çalıştıran iki IIS sunucuları</span><span class="sxs-lookup"><span data-stu-id="58155-108">Two IIS servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="58155-109">Veri ve uygulama katmanına siparişler işleme iki IIS sunucuları</span><span class="sxs-lookup"><span data-stu-id="58155-109">Two IIS servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="58155-110">Ürün veri ve siparişler bir veritabanı katmanı depolamak için AlwaysOn Kullanılabilirlik grupları (iki SQL sunucuları ve Çoğunluk düğüm tanığı) ile iki Microsoft SQL Server örnekleri</span><span class="sxs-lookup"><span data-stu-id="58155-110">Two Microsoft SQL Server instances with AlwaysOn availability groups (two SQL Servers and a majority node witness) for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="58155-111">Müşteri hesapları ve bir kimlik doğrulama katmanı sağlayıcıları için iki Active Directory etki alanı denetleyicisi</span><span class="sxs-lookup"><span data-stu-id="58155-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="58155-112">Tüm hello sunucuları iki alt ağ içinde bulunur:</span><span class="sxs-lookup"><span data-stu-id="58155-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="58155-113">Merhaba web sunucuları için ön uç bir alt ağ</span><span class="sxs-lookup"><span data-stu-id="58155-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="58155-114">Merhaba uygulama sunucuları, SQL kümesi ve etki alanı denetleyicileri için bir arka uç alt ağ</span><span class="sxs-lookup"><span data-stu-id="58155-114">a back-end subnet for hello application servers, SQL cluster, and domain controllers</span></span>

![Uygulama altyapısı için farklı katmanlara diyagramı](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="58155-116">Güvenli gelen web trafiği olması hello web sunucuları arasında Yük Dengelemesi müşteriler hello çevrimiçi mağaza göz atın.</span><span class="sxs-lookup"><span data-stu-id="58155-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="58155-117">Merhaba biçiminde hello Web sunucuları hello uygulama sunucuları arasında dengelenmelidir HTTP isteklerini işleme trafiği sipariş.</span><span class="sxs-lookup"><span data-stu-id="58155-117">Order processing traffic in hello form of HTTP requests from hello web servers must be balanced among hello application servers.</span></span> <span data-ttu-id="58155-118">Ayrıca, hello altyapı yüksek kullanılabilirlik için tasarlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="58155-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="58155-119">Merhaba elde edilen tasarım eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="58155-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="58155-120">Bir Azure aboneliği ve hesabı</span><span class="sxs-lookup"><span data-stu-id="58155-120">An Azure subscription and account</span></span>
* <span data-ttu-id="58155-121">Tek bir kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="58155-121">A single resource group</span></span>
* <span data-ttu-id="58155-122">Azure Yönetilen Diskleri</span><span class="sxs-lookup"><span data-stu-id="58155-122">Azure Managed Disks</span></span>
* <span data-ttu-id="58155-123">İki alt ağa sahip bir sanal ağ</span><span class="sxs-lookup"><span data-stu-id="58155-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="58155-124">Merhaba VM'ler ile benzer bir rolü için kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="58155-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="58155-125">Sanal makineler</span><span class="sxs-lookup"><span data-stu-id="58155-125">Virtual machines</span></span>

<span data-ttu-id="58155-126">Yukarıdaki tüm hello adlandırma kurallarına izleyin:</span><span class="sxs-lookup"><span data-stu-id="58155-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="58155-127">Adventure Works Cycles kullandığı **[BT iş yükü]-[konum]-[Azure kaynak]** öneki olarak</span><span class="sxs-lookup"><span data-stu-id="58155-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="58155-128">Bu örneğin, "**azos**" (Azure çevrimiçi mağaza) iş yükü adı hello ve "**kullanmak**" (Doğu ABD 2) hello konumudur</span><span class="sxs-lookup"><span data-stu-id="58155-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="58155-129">Sanal ağları kullanın AZOS kullanım VN**[sayı]**</span><span class="sxs-lookup"><span data-stu-id="58155-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="58155-130">Kullanılabilirlik kümeleri kullanan azos-kullanın-olarak-**[rol]**</span><span class="sxs-lookup"><span data-stu-id="58155-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="58155-131">Sanal makine adları azos kullanın-kullanın-vm -**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="58155-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="58155-132">Azure abonelikleri ve hesapları</span><span class="sxs-lookup"><span data-stu-id="58155-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="58155-133">Adventure Works Cycles, Adventure Works Kurumsal abonelik, bu BT iş yükü için faturalama tooprovide adlı kurumsal aboneliğini kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="58155-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="58155-134">Depolama</span><span class="sxs-lookup"><span data-stu-id="58155-134">Storage</span></span>
<span data-ttu-id="58155-135">Adventure Works Cycles Azure yönetilen diskleri kullanması gerektiğini belirledi.</span><span class="sxs-lookup"><span data-stu-id="58155-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="58155-136">Sanal makineleri oluştururken, her iki depolama kullanılabilir depolama katmanları kullanılır:</span><span class="sxs-lookup"><span data-stu-id="58155-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="58155-137">**Standart depolama** hello web sunucuları, uygulama sunucuları ve etki alanı denetleyicileri ve kendi veri diskleri için.</span><span class="sxs-lookup"><span data-stu-id="58155-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="58155-138">**Premium depolama** hello SQL Server VM'ler ve kendi veri diskleri için.</span><span class="sxs-lookup"><span data-stu-id="58155-138">**Premium storage** for hello SQL Server VMs and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="58155-139">Sanal ağ ve alt ağlar</span><span class="sxs-lookup"><span data-stu-id="58155-139">Virtual network and subnets</span></span>
<span data-ttu-id="58155-140">Merhaba sanal ağ sürekli bağlantı toohello Adventure iş döngüsü şirket içi ağ gerekmediği için bir yalnızca bulut sanal ağda karar verdi.</span><span class="sxs-lookup"><span data-stu-id="58155-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="58155-141">Bunlar yalnızca bulut sanal ağ ayarlarını hello Azure portal kullanarak aşağıdaki hello ile oluşturulan:</span><span class="sxs-lookup"><span data-stu-id="58155-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="58155-142">Name: Kullanım AZOS VN01</span><span class="sxs-lookup"><span data-stu-id="58155-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="58155-143">Konumu: Doğu ABD 2</span><span class="sxs-lookup"><span data-stu-id="58155-143">Location: East US 2</span></span>
* <span data-ttu-id="58155-144">Sanal ağ adres alanı: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="58155-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="58155-145">İlk alt ağ:</span><span class="sxs-lookup"><span data-stu-id="58155-145">First subnet:</span></span>
  * <span data-ttu-id="58155-146">Ad: ön uç</span><span class="sxs-lookup"><span data-stu-id="58155-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="58155-147">Adres alanı: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="58155-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="58155-148">İkinci alt ağ:</span><span class="sxs-lookup"><span data-stu-id="58155-148">Second subnet:</span></span>
  * <span data-ttu-id="58155-149">Ad: arka uç</span><span class="sxs-lookup"><span data-stu-id="58155-149">Name: BackEnd</span></span>
  * <span data-ttu-id="58155-150">Adres alanı: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="58155-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="58155-151">Kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="58155-151">Availability sets</span></span>
<span data-ttu-id="58155-152">Adventure Works Cycles dört kullanılabilirlik kümesi üzerinde kampanyanızın çevrimiçi kendi deposunun tüm dört katmanların toomaintain yüksek kullanılabilirlik:</span><span class="sxs-lookup"><span data-stu-id="58155-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="58155-153">**web olarak azos kullanım** hello web sunucuları için</span><span class="sxs-lookup"><span data-stu-id="58155-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="58155-154">**uygulama olarak azos kullanım** hello uygulama sunucuları için</span><span class="sxs-lookup"><span data-stu-id="58155-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="58155-155">**sql olarak azos kullanım** hello SQL sunucuları için</span><span class="sxs-lookup"><span data-stu-id="58155-155">**azos-use-as-sql** for hello SQL Servers</span></span>
* <span data-ttu-id="58155-156">**dc olarak azos kullanım** hello etki alanı denetleyicileri için</span><span class="sxs-lookup"><span data-stu-id="58155-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="58155-157">Sanal makineler</span><span class="sxs-lookup"><span data-stu-id="58155-157">Virtual machines</span></span>
<span data-ttu-id="58155-158">Adventure Works Cycles Azure Vm'leri için adlarından hello karar:</span><span class="sxs-lookup"><span data-stu-id="58155-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="58155-159">**Kullanım vm web01 azos** hello ilk web sunucusu için</span><span class="sxs-lookup"><span data-stu-id="58155-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="58155-160">**Kullanım vm web02 azos** hello ikinci web sunucusu için</span><span class="sxs-lookup"><span data-stu-id="58155-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="58155-161">**Kullanım vm app01 azos** hello ilk uygulama sunucusu için</span><span class="sxs-lookup"><span data-stu-id="58155-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="58155-162">**Kullanım vm app02 azos** hello ikinci uygulama sunucusu için</span><span class="sxs-lookup"><span data-stu-id="58155-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="58155-163">**Kullanım vm sql01 azos** hello küme hello ilk SQL Server sunucusu için</span><span class="sxs-lookup"><span data-stu-id="58155-163">**azos-use-vm-sql01** for hello first SQL Server server in hello cluster</span></span>
* <span data-ttu-id="58155-164">**Kullanım vm sql02 azos** hello küme hello ikinci SQL Server sunucusu için</span><span class="sxs-lookup"><span data-stu-id="58155-164">**azos-use-vm-sql02** for hello second SQL Server server in hello cluster</span></span>
* <span data-ttu-id="58155-165">**Kullanım vm dc01 azos** hello ilk etki alanı denetleyicisi için</span><span class="sxs-lookup"><span data-stu-id="58155-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="58155-166">**Kullanım vm dc02 azos** hello ikinci etki alanı denetleyicisi için</span><span class="sxs-lookup"><span data-stu-id="58155-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="58155-167">Merhaba sonuçta elde edilen yapılandırma aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="58155-167">Here is hello resulting configuration.</span></span>

![Azure üzerinde dağıtılan son uygulama altyapısı](./media/infrastructure-example/example-config.png)

<span data-ttu-id="58155-169">Bu yapılandırma bir araya getirir:</span><span class="sxs-lookup"><span data-stu-id="58155-169">This configuration incorporates:</span></span>

* <span data-ttu-id="58155-170">Bir yalnızca bulut sanal ağla iki alt ağ (ön uç ve arka uç)</span><span class="sxs-lookup"><span data-stu-id="58155-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="58155-171">Azure yönetilen diskleri standart ve Premium diskleri</span><span class="sxs-lookup"><span data-stu-id="58155-171">Azure Managed Disks with both Standard and Premium disks</span></span>
* <span data-ttu-id="58155-172">Bir hello çevrimiçi deposunun her katman için dört kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="58155-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="58155-173">Merhaba dört katmanları için Hello sanal makineler</span><span class="sxs-lookup"><span data-stu-id="58155-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="58155-174">Bir dış yük dengeli küme hello Internet toohello web sunucularından HTTPS tabanlı web trafiği için</span><span class="sxs-lookup"><span data-stu-id="58155-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="58155-175">Bir iç yük dengeli küme hello web sunucuları toohello uygulama sunucularından şifrelenmemiş web trafiği için</span><span class="sxs-lookup"><span data-stu-id="58155-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="58155-176">Tek bir kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="58155-176">A single resource group</span></span>