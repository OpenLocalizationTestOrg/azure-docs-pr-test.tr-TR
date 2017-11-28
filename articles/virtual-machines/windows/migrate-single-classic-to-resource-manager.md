---
title: "aaaMigrate Klasik VM tooan ARM yönetilen Disk VM | Microsoft Docs"
description: "Tek bir Azure VM'ye hello Klasik dağıtımını geçirdikten tooManaged diskleri hello Resource Manager dağıtım modelinde model."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a><span data-ttu-id="96674-103">Klasik VM tooa el ile geçirme yeni ARM yönetilen diski sanal makineden hello VHD</span><span class="sxs-lookup"><span data-stu-id="96674-103">Manually migrate a Classic VM tooa new ARM Managed Disk VM from hello VHD</span></span> 


<span data-ttu-id="96674-104">Bu bölümde, toomigrate mevcut Azure Vm'leriniz hello Klasik dağıtım modelinden çok yardımcı[yönetilen diskleri](managed-disks-overview.md) hello Resource Manager dağıtım modelinde.</span><span class="sxs-lookup"><span data-stu-id="96674-104">This section helps you toomigrate your existing Azure VMs from hello classic deployment model too[Managed Disks](managed-disks-overview.md) in hello Resource Manager deployment model.</span></span>


## <a name="plan-for-hello-migration-toomanaged-disks"></a><span data-ttu-id="96674-105">Plan hello geçiş için tooManaged diskleri</span><span class="sxs-lookup"><span data-stu-id="96674-105">Plan for hello migration tooManaged Disks</span></span>

<span data-ttu-id="96674-106">Bu bölümde, VM ve disk türleri hakkında toomake hello en iyi karar yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="96674-106">This section helps you toomake hello best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="96674-107">Konum</span><span class="sxs-lookup"><span data-stu-id="96674-107">Location</span></span>

<span data-ttu-id="96674-108">Azure yönetilen diskleri kullanılabildiği bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="96674-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="96674-109">TooPremium yönetilen diskleri geçiriyorsanız, ayrıca Premium depolama burada toomigrate için planlama hello bölgede kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="96674-109">If you are migrating tooPremium Managed Disks, also ensure that Premium storage is available in hello region where you are planning toomigrate to.</span></span> <span data-ttu-id="96674-110">Bkz: [Azure Hizmetleri byRegion](https://azure.microsoft.com/regions/#services) kullanılabilir konumları hakkında güncel bilgi.</span><span class="sxs-lookup"><span data-stu-id="96674-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="96674-111">VM boyutları</span><span class="sxs-lookup"><span data-stu-id="96674-111">VM sizes</span></span>

<span data-ttu-id="96674-112">TooPremium yönetilen diskleri geçiriyorsanız, VM bulunduğu hello bölgede tooupdate hello hello VM tooPremium depolama özellikli boyutu kullanılabilir boyutuna sahip.</span><span class="sxs-lookup"><span data-stu-id="96674-112">If you are migrating tooPremium Managed Disks, you have tooupdate hello size of hello VM tooPremium Storage capable size available in hello region where VM is located.</span></span> <span data-ttu-id="96674-113">Premium depolama özellikli hello VM boyutları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="96674-113">Review hello VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="96674-114">Hello Azure VM boyutu belirtimleri içinde listelenen [sanal makineler için Boyutlar](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="96674-114">hello Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="96674-115">Premium Storage ile birlikte çalışmak ve işleminizi iş yükü en çok uyan hello en uygun VM boyutunu seçin sanal makineleri Hello performans özellikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="96674-115">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="96674-116">Yeterli bant genişliği kullanılabilir VM toodrive hello disk trafiğinde bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="96674-116">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="96674-117">Disk boyutları</span><span class="sxs-lookup"><span data-stu-id="96674-117">Disk sizes</span></span>

<span data-ttu-id="96674-118">**Premium yönetilen diskleri**</span><span class="sxs-lookup"><span data-stu-id="96674-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="96674-119">Yedi disk türleri için VM ile kullanılabilen premium yönetilen vardır ve her belirli IOPS ve üretilen iş sahip sınırlar.</span><span class="sxs-lookup"><span data-stu-id="96674-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="96674-120">Bu sınırlar yoğun yükler ve kapasite, performans, ölçeklenebilirlik açısından, uygulamanızın hello gereksinimlerine hello Premium disk türü, VM için temel seçerken göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="96674-120">Consider these limits when choosing hello Premium disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="96674-121">Premium diskler türü</span><span class="sxs-lookup"><span data-stu-id="96674-121">Premium Disks Type</span></span>  | <span data-ttu-id="96674-122">P4</span><span class="sxs-lookup"><span data-stu-id="96674-122">P4</span></span>    | <span data-ttu-id="96674-123">P6</span><span class="sxs-lookup"><span data-stu-id="96674-123">P6</span></span>    | <span data-ttu-id="96674-124">P10</span><span class="sxs-lookup"><span data-stu-id="96674-124">P10</span></span>   | <span data-ttu-id="96674-125">P20</span><span class="sxs-lookup"><span data-stu-id="96674-125">P20</span></span>   | <span data-ttu-id="96674-126">P30</span><span class="sxs-lookup"><span data-stu-id="96674-126">P30</span></span>   | <span data-ttu-id="96674-127">P40</span><span class="sxs-lookup"><span data-stu-id="96674-127">P40</span></span>   | <span data-ttu-id="96674-128">P50</span><span class="sxs-lookup"><span data-stu-id="96674-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="96674-129">Disk boyutu</span><span class="sxs-lookup"><span data-stu-id="96674-129">Disk size</span></span>           | <span data-ttu-id="96674-130">128 GB</span><span class="sxs-lookup"><span data-stu-id="96674-130">128 GB</span></span>| <span data-ttu-id="96674-131">512 GB</span><span class="sxs-lookup"><span data-stu-id="96674-131">512 GB</span></span>| <span data-ttu-id="96674-132">128 GB</span><span class="sxs-lookup"><span data-stu-id="96674-132">128 GB</span></span>| <span data-ttu-id="96674-133">512 GB</span><span class="sxs-lookup"><span data-stu-id="96674-133">512 GB</span></span>            | <span data-ttu-id="96674-134">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="96674-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="96674-135">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="96674-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="96674-136">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="96674-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="96674-137">Disk başına IOPS</span><span class="sxs-lookup"><span data-stu-id="96674-137">IOPS per disk</span></span>       | <span data-ttu-id="96674-138">120</span><span class="sxs-lookup"><span data-stu-id="96674-138">120</span></span>   | <span data-ttu-id="96674-139">240</span><span class="sxs-lookup"><span data-stu-id="96674-139">240</span></span>   | <span data-ttu-id="96674-140">500</span><span class="sxs-lookup"><span data-stu-id="96674-140">500</span></span>   | <span data-ttu-id="96674-141">2300</span><span class="sxs-lookup"><span data-stu-id="96674-141">2300</span></span>              | <span data-ttu-id="96674-142">5000</span><span class="sxs-lookup"><span data-stu-id="96674-142">5000</span></span>              | <span data-ttu-id="96674-143">7500</span><span class="sxs-lookup"><span data-stu-id="96674-143">7500</span></span>              | <span data-ttu-id="96674-144">7500</span><span class="sxs-lookup"><span data-stu-id="96674-144">7500</span></span>              | 
| <span data-ttu-id="96674-145">Disk başına aktarım hızı</span><span class="sxs-lookup"><span data-stu-id="96674-145">Throughput per disk</span></span> | <span data-ttu-id="96674-146">Saniye başına 25 MB</span><span class="sxs-lookup"><span data-stu-id="96674-146">25 MB per second</span></span>  | <span data-ttu-id="96674-147">Saniye başına 50 MB</span><span class="sxs-lookup"><span data-stu-id="96674-147">50 MB per second</span></span>  | <span data-ttu-id="96674-148">Saniyede 100 MB</span><span class="sxs-lookup"><span data-stu-id="96674-148">100 MB per second</span></span> | <span data-ttu-id="96674-149">150 MB / saniye</span><span class="sxs-lookup"><span data-stu-id="96674-149">150 MB per second</span></span> | <span data-ttu-id="96674-150">200 MB / saniye</span><span class="sxs-lookup"><span data-stu-id="96674-150">200 MB per second</span></span> | <span data-ttu-id="96674-151">Saniye başına 250 MB</span><span class="sxs-lookup"><span data-stu-id="96674-151">250 MB per second</span></span> | <span data-ttu-id="96674-152">Saniye başına 250 MB</span><span class="sxs-lookup"><span data-stu-id="96674-152">250 MB per second</span></span> | 

<span data-ttu-id="96674-153">**Standart yönetilen disk**</span><span class="sxs-lookup"><span data-stu-id="96674-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="96674-154">VM ile kullanılabilecek standart yönetilen disk yedi türü vardır.</span><span class="sxs-lookup"><span data-stu-id="96674-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="96674-155">Bunların her biri farklı kapasiteye sahip ancak aynı IOPS ve üretilen iş sınırı vardır.</span><span class="sxs-lookup"><span data-stu-id="96674-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="96674-156">Standart yönetilen disk uygulamanızın hello kapasite gereksinimlerine göre Hello türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="96674-156">Choose hello type of Standard Managed disks based on hello capacity needs of your application.</span></span>

| <span data-ttu-id="96674-157">Standart Disk Türü</span><span class="sxs-lookup"><span data-stu-id="96674-157">Standard Disk Type</span></span>  | <span data-ttu-id="96674-158">S4</span><span class="sxs-lookup"><span data-stu-id="96674-158">S4</span></span>               | <span data-ttu-id="96674-159">S6</span><span class="sxs-lookup"><span data-stu-id="96674-159">S6</span></span>               | <span data-ttu-id="96674-160">S10</span><span class="sxs-lookup"><span data-stu-id="96674-160">S10</span></span>              | <span data-ttu-id="96674-161">S20</span><span class="sxs-lookup"><span data-stu-id="96674-161">S20</span></span>              | <span data-ttu-id="96674-162">S30</span><span class="sxs-lookup"><span data-stu-id="96674-162">S30</span></span>              | <span data-ttu-id="96674-163">S40</span><span class="sxs-lookup"><span data-stu-id="96674-163">S40</span></span>              | <span data-ttu-id="96674-164">S50</span><span class="sxs-lookup"><span data-stu-id="96674-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="96674-165">Disk boyutu</span><span class="sxs-lookup"><span data-stu-id="96674-165">Disk size</span></span>           | <span data-ttu-id="96674-166">30 GB</span><span class="sxs-lookup"><span data-stu-id="96674-166">30 GB</span></span>            | <span data-ttu-id="96674-167">64 GB</span><span class="sxs-lookup"><span data-stu-id="96674-167">64 GB</span></span>            | <span data-ttu-id="96674-168">128 GB</span><span class="sxs-lookup"><span data-stu-id="96674-168">128 GB</span></span>           | <span data-ttu-id="96674-169">512 GB</span><span class="sxs-lookup"><span data-stu-id="96674-169">512 GB</span></span>           | <span data-ttu-id="96674-170">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="96674-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="96674-171">2048 GB (2TB)</span><span class="sxs-lookup"><span data-stu-id="96674-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="96674-172">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="96674-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="96674-173">Disk başına IOPS</span><span class="sxs-lookup"><span data-stu-id="96674-173">IOPS per disk</span></span>       | <span data-ttu-id="96674-174">500</span><span class="sxs-lookup"><span data-stu-id="96674-174">500</span></span>              | <span data-ttu-id="96674-175">500</span><span class="sxs-lookup"><span data-stu-id="96674-175">500</span></span>              | <span data-ttu-id="96674-176">500</span><span class="sxs-lookup"><span data-stu-id="96674-176">500</span></span>              | <span data-ttu-id="96674-177">500</span><span class="sxs-lookup"><span data-stu-id="96674-177">500</span></span>              | <span data-ttu-id="96674-178">500</span><span class="sxs-lookup"><span data-stu-id="96674-178">500</span></span>              | <span data-ttu-id="96674-179">500</span><span class="sxs-lookup"><span data-stu-id="96674-179">500</span></span>             | <span data-ttu-id="96674-180">500</span><span class="sxs-lookup"><span data-stu-id="96674-180">500</span></span>              | 
| <span data-ttu-id="96674-181">Disk başına aktarım hızı</span><span class="sxs-lookup"><span data-stu-id="96674-181">Throughput per disk</span></span> | <span data-ttu-id="96674-182">Saniye başına 60 MB</span><span class="sxs-lookup"><span data-stu-id="96674-182">60 MB per second</span></span> | <span data-ttu-id="96674-183">Saniye başına 60 MB</span><span class="sxs-lookup"><span data-stu-id="96674-183">60 MB per second</span></span> | <span data-ttu-id="96674-184">Saniye başına 60 MB</span><span class="sxs-lookup"><span data-stu-id="96674-184">60 MB per second</span></span> | <span data-ttu-id="96674-185">Saniye başına 60 MB</span><span class="sxs-lookup"><span data-stu-id="96674-185">60 MB per second</span></span> | <span data-ttu-id="96674-186">Saniye başına 60 MB</span><span class="sxs-lookup"><span data-stu-id="96674-186">60 MB per second</span></span> | <span data-ttu-id="96674-187">Saniye başına 60 MB</span><span class="sxs-lookup"><span data-stu-id="96674-187">60 MB per second</span></span> | <span data-ttu-id="96674-188">Saniye başına 60 MB</span><span class="sxs-lookup"><span data-stu-id="96674-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="96674-189">Önbellek İlkesi disk</span><span class="sxs-lookup"><span data-stu-id="96674-189">Disk caching policy</span></span> 

<span data-ttu-id="96674-190">**Premium yönetilen diskleri**</span><span class="sxs-lookup"><span data-stu-id="96674-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="96674-191">Varsayılan olarak, ilke önbelleğe alma disktir *salt okunur* tüm Premium diskleri hello için ve *okuma-yazma* hello Premium işletim sistemi diski için toohello VM bağlı.</span><span class="sxs-lookup"><span data-stu-id="96674-191">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="96674-192">Bu yapılandırma ayarının tooachieve hello en iyi performans için uygulamanızın IOs önerilir.</span><span class="sxs-lookup"><span data-stu-id="96674-192">This configuration setting is recommended tooachieve hello optimal performance for your application’s IOs.</span></span> <span data-ttu-id="96674-193">(SQL Server günlük dosyaları gibi) ağır yazma ya da salt yazılır veri diskleri için daha iyi uygulama performansı elde etmek için disk önbelleğe almayı devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="96674-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="96674-194">Fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="96674-194">Pricing</span></span>

<span data-ttu-id="96674-195">Gözden geçirme hello [yönetilen diskler için fiyatlandırma](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="96674-195">Review hello [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="96674-196">Premium diskler yönetilen fiyatlandırma hello Premium yönetilmeyen diskleri aynıdır.</span><span class="sxs-lookup"><span data-stu-id="96674-196">Pricing of Premium Managed Disks is same as hello Premium Unmanaged Disks.</span></span> <span data-ttu-id="96674-197">Ancak standart yönetilen disk için fiyatlandırma standart yönetilmeyen disklerden farklı.</span><span class="sxs-lookup"><span data-stu-id="96674-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="96674-198">Denetim listesi</span><span class="sxs-lookup"><span data-stu-id="96674-198">Checklist</span></span>

1.  <span data-ttu-id="96674-199">TooPremium yönetilen diskleri geçiriyorsanız, bu için geçirdiğiniz hello bölgede kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="96674-199">If you are migrating tooPremium Managed Disks, make sure it is available in hello region you are migrating to.</span></span>

2.  <span data-ttu-id="96674-200">Merhaba, kullanarak yeni VM dizisi karar verin.</span><span class="sxs-lookup"><span data-stu-id="96674-200">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="96674-201">TooPremium yönetilen diskleri geçiriyorsanız, Premium depolama özelliğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="96674-201">It should be a Premium Storage capable if you are migrating tooPremium Managed Disks.</span></span>

3.  <span data-ttu-id="96674-202">Geçirmekte olduğunuz hello bölgede kullanılabilir olan kullanacağınız hello tam VM boyutu karar verin.</span><span class="sxs-lookup"><span data-stu-id="96674-202">Decide hello exact VM size you will use which are available in hello region you are migrating to.</span></span> <span data-ttu-id="96674-203">VM boyutu toobe büyüklükte toosupport hello sahip veri diski sayısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="96674-203">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="96674-204">Örneğin, dört veri diski varsa, hello VM iki veya daha fazla çekirdek olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96674-204">For example, if you have four data disks, hello VM must have two or more cores.</span></span> <span data-ttu-id="96674-205">Ayrıca, işlemci gücü, bellek göz önünde bulundurun ve ağ bant genişliği gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="96674-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="96674-206">Merhaba geçerli VM ayrıntıları hello disklerin listesini ve karşılık gelen VHD BLOB'ları da dahil olmak üzere kullanışlı vardır.</span><span class="sxs-lookup"><span data-stu-id="96674-206">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="96674-207">Uygulamanızı kapalı kalma süresi için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="96674-207">Prepare your application for downtime.</span></span> <span data-ttu-id="96674-208">toodo temiz bir geçiş, toostop hello geçerli sistemi tüm hello işleme sahip.</span><span class="sxs-lookup"><span data-stu-id="96674-208">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="96674-209">Ancak bundan sonra geçirebileceğiniz tooconsistent durumu alabilirsiniz toohello yeni platformu.</span><span class="sxs-lookup"><span data-stu-id="96674-209">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="96674-210">Kapalı kalma süresi hello hello diskleri toomigrate veri miktarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="96674-210">Downtime duration depends on hello amount of data in hello disks toomigrate.</span></span>


## <a name="migrate-hello-vm"></a><span data-ttu-id="96674-211">Merhaba VM geçirme</span><span class="sxs-lookup"><span data-stu-id="96674-211">Migrate hello VM</span></span>

<span data-ttu-id="96674-212">Uygulamanızı kapalı kalma süresi için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="96674-212">Prepare your application for downtime.</span></span> <span data-ttu-id="96674-213">toodo temiz bir geçiş, toostop hello geçerli sistemi tüm hello işleme sahip.</span><span class="sxs-lookup"><span data-stu-id="96674-213">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="96674-214">Ancak bundan sonra geçirebileceğiniz tooconsistent durumu alabilirsiniz toohello yeni platformu.</span><span class="sxs-lookup"><span data-stu-id="96674-214">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="96674-215">Kapalı kalma süresi hello hello diskleri toomigrate veri miktarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="96674-215">Downtime duration depends hello amount of data in hello disks toomigrate.</span></span>


1.  <span data-ttu-id="96674-216">İlk olarak, hello ortak parametreleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="96674-216">First, set hello common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="96674-217">Merhaba VHD hello gelen kullanarak yönetilen bir işletim sistemi diski oluşturma Klasik VM.</span><span class="sxs-lookup"><span data-stu-id="96674-217">Create a managed OS disk using hello VHD from hello classic VM.</span></span>

    <span data-ttu-id="96674-218">Merhaba tamamlamak sağlanan hello OS VHD toohello $osVhdUri parametresi URI'sini, olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="96674-218">Ensure that you have provided hello complete URI of hello OS VHD toohello $osVhdUri parameter.</span></span> <span data-ttu-id="96674-219">Ayrıca, girin **- AccountType** olarak **PremiumLRS** veya **StandardLRS** temel diskleri (Premium veya standart) türüne için geçirdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="96674-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="96674-220">Merhaba işletim sistemi disk toohello ekleme yeni VM.</span><span class="sxs-lookup"><span data-stu-id="96674-220">Attach hello OS disk toohello new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="96674-221">Yönetilen veri diski hello veri VHD dosyası oluşturun ve toohello ekleyin yeni VM.</span><span class="sxs-lookup"><span data-stu-id="96674-221">Create a managed data disk from hello data VHD file and add it toohello new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="96674-222">Oluşturma genel IP, sanal ağ ve NIC ayarlayarak yeni VM hello</span><span class="sxs-lookup"><span data-stu-id="96674-222">Create hello new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="96674-223">Ek adımlar gerekli toosupport olabilir, uygulama değil Bu kılavuz kapsamında.</span><span class="sxs-lookup"><span data-stu-id="96674-223">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="96674-224">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96674-224">Next steps</span></span>

- <span data-ttu-id="96674-225">Toohello sanal makineye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="96674-225">Connect toohello virtual machine.</span></span> <span data-ttu-id="96674-226">Yönergeler için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96674-226">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

