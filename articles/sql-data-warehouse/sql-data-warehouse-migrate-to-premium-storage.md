---
title: "aaaMigrate, var olan Azure veri ambarı toopremium depolama | Microsoft Docs"
description: "Varolan bir veri ambarı toopremium depolama geçirmek için yönergeler"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a><span data-ttu-id="9fb19-103">Veri ambarı toopremium deponuzda geçirme</span><span class="sxs-lookup"><span data-stu-id="9fb19-103">Migrate your data warehouse toopremium storage</span></span>
<span data-ttu-id="9fb19-104">En yeni Azure SQL Data Warehouse [büyük performans öngörülebilirlik için premium depolama][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="9fb19-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="9fb19-105">Mevcut veri ambarları şu anda standart depolama artık olabilir toopremium depolama geçişi.</span><span class="sxs-lookup"><span data-stu-id="9fb19-105">Existing data warehouses currently on standard storage can now be migrated toopremium storage.</span></span> <span data-ttu-id="9fb19-106">Otomatik geçiş yararlanabilir veya toocontrol tercih ederseniz, (hangi miktar kapalı kalma süresi içerir) toomigrate yapabileceğiniz geçiş kendiniz hello.</span><span class="sxs-lookup"><span data-stu-id="9fb19-106">You can take advantage of automatic migration, or if you prefer toocontrol when toomigrate (which does involve some downtime), you can do hello migration yourself.</span></span>

<span data-ttu-id="9fb19-107">Birden fazla veri ambarı varsa, hello kullanın [otomatik geçiş zamanlama] [ automatic migration schedule] de geçirilecek zaman toodetermine.</span><span class="sxs-lookup"><span data-stu-id="9fb19-107">If you have more than one data warehouse, use hello [automatic migration schedule][automatic migration schedule] toodetermine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="9fb19-108">Depolama türü belirlenemiyor</span><span class="sxs-lookup"><span data-stu-id="9fb19-108">Determine storage type</span></span>
<span data-ttu-id="9fb19-109">Veri ambarı tarihleri aşağıdaki hello önce oluşturduysanız, standart depolama kullanmakta olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="9fb19-109">If you created a data warehouse before hello following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="9fb19-110">**Bölge**</span><span class="sxs-lookup"><span data-stu-id="9fb19-110">**Region**</span></span> | <span data-ttu-id="9fb19-111">**Bu tarihten önce oluşturulan veri ambarı**</span><span class="sxs-lookup"><span data-stu-id="9fb19-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="9fb19-112">Avustralya Doğu</span><span class="sxs-lookup"><span data-stu-id="9fb19-112">Australia East</span></span> |<span data-ttu-id="9fb19-113">Premium depolama henüz kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="9fb19-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="9fb19-114">Çin Doğu</span><span class="sxs-lookup"><span data-stu-id="9fb19-114">China East</span></span> |<span data-ttu-id="9fb19-115">1 Kasım 2016</span><span class="sxs-lookup"><span data-stu-id="9fb19-115">November 1, 2016</span></span> |
| <span data-ttu-id="9fb19-116">Çin Kuzey</span><span class="sxs-lookup"><span data-stu-id="9fb19-116">China North</span></span> |<span data-ttu-id="9fb19-117">1 Kasım 2016</span><span class="sxs-lookup"><span data-stu-id="9fb19-117">November 1, 2016</span></span> |
| <span data-ttu-id="9fb19-118">Almanya Orta</span><span class="sxs-lookup"><span data-stu-id="9fb19-118">Germany Central</span></span> |<span data-ttu-id="9fb19-119">1 Kasım 2016</span><span class="sxs-lookup"><span data-stu-id="9fb19-119">November 1, 2016</span></span> |
| <span data-ttu-id="9fb19-120">Almanya Kuzeydoğu</span><span class="sxs-lookup"><span data-stu-id="9fb19-120">Germany Northeast</span></span> |<span data-ttu-id="9fb19-121">1 Kasım 2016</span><span class="sxs-lookup"><span data-stu-id="9fb19-121">November 1, 2016</span></span> |
| <span data-ttu-id="9fb19-122">Hindistan Batı</span><span class="sxs-lookup"><span data-stu-id="9fb19-122">India West</span></span> |<span data-ttu-id="9fb19-123">Premium depolama henüz kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="9fb19-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="9fb19-124">Japonya Batı</span><span class="sxs-lookup"><span data-stu-id="9fb19-124">Japan West</span></span> |<span data-ttu-id="9fb19-125">Premium depolama henüz kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="9fb19-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="9fb19-126">Orta Kuzey ABD</span><span class="sxs-lookup"><span data-stu-id="9fb19-126">North Central US</span></span> |<span data-ttu-id="9fb19-127">10 Kasım 2016</span><span class="sxs-lookup"><span data-stu-id="9fb19-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="9fb19-128">Otomatik geçiş ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="9fb19-128">Automatic migration details</span></span>
<span data-ttu-id="9fb19-129">Varsayılan olarak, biz veritabanınız için 6: 00'dan 6: 00'da, bölgenin yerel saat arasındaki hello sırasında geçiş yapacağınız [otomatik geçiş zamanlama][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="9fb19-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during hello [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="9fb19-130">Mevcut veri ambarınız hello geçiş sırasında kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="9fb19-130">Your existing data warehouse will be unusable during hello migration.</span></span> <span data-ttu-id="9fb19-131">Merhaba geçiş veri ambarına terabayt depolama alanı başına yaklaşık bir saat sürer.</span><span class="sxs-lookup"><span data-stu-id="9fb19-131">hello migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="9fb19-132">Hello otomatik geçiş herhangi bir kısmının sırasında ücret alınmaz.</span><span class="sxs-lookup"><span data-stu-id="9fb19-132">You will not be charged during any portion of hello automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="9fb19-133">Merhaba geçiş tamamlandığında, veri Ambarınızı tekrar çevrimiçi ve kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9fb19-133">When hello migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="9fb19-134">Microsoft, aşağıdaki adımları toocomplete hello geçiş (Bu tüm katılımı yapmanıza gerek yoktur) hello sürüyor.</span><span class="sxs-lookup"><span data-stu-id="9fb19-134">Microsoft is taking hello following steps toocomplete hello migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="9fb19-135">Bu örnekte, var olan veri ambarınız standart depolama üzerinde şu anda "MyDW." adlı düşünün</span><span class="sxs-lookup"><span data-stu-id="9fb19-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="9fb19-136">Microsoft "MyDW" çok yeniden adlandırır "MyDW_DO_NOT_USE_ [zaman damgası]."</span><span class="sxs-lookup"><span data-stu-id="9fb19-136">Microsoft renames “MyDW” too“MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="9fb19-137">Microsoft duraklatır "MyDW_DO_NOT_USE_ [zaman damgası]."</span><span class="sxs-lookup"><span data-stu-id="9fb19-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="9fb19-138">Bu süre boyunca, bir yedekleme gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9fb19-138">During this time, a backup is taken.</span></span> <span data-ttu-id="9fb19-139">Biz bu işlem sırasında herhangi bir sorunla karşılaşırsanız, birden çok duraklatır ve sürdürür görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fb19-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="9fb19-140">Microsoft, "2. adımda alınan MyDW" premium depolama hello yedekten adlı yeni bir veri ambarını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9fb19-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from hello backup taken in step 2.</span></span> <span data-ttu-id="9fb19-141">Merhaba geri yükleme tamamlandıktan sonra "MyDW" kadar görünmez.</span><span class="sxs-lookup"><span data-stu-id="9fb19-141">“MyDW” will not appear until after hello restore is complete.</span></span>
4. <span data-ttu-id="9fb19-142">Merhaba geri yükleme tamamlandıktan sonra "MyDW" aynı veri ambarı birimlerini ve durum toohello (duraklatılmış ya da etkin) döndürür hello geçişten önce olan.</span><span class="sxs-lookup"><span data-stu-id="9fb19-142">After hello restore is complete, “MyDW” returns toohello same data warehouse units and state (paused or active) that it was before hello migration.</span></span>
5. <span data-ttu-id="9fb19-143">Merhaba geçiş tamamlandıktan sonra Microsoft "MyDW_DO_NOT_USE_ [zaman damgası]" siler.</span><span class="sxs-lookup"><span data-stu-id="9fb19-143">After hello migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="9fb19-144">Merhaba aşağıdaki ayarları hello geçişin bir parçası taşınmaz:</span><span class="sxs-lookup"><span data-stu-id="9fb19-144">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="9fb19-145">Merhaba veritabanı düzeyinde denetimi yeniden etkin toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fb19-145">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="9fb19-146">Merhaba veritabanı düzeyinde güvenlik duvarı kuralları yeniden eklendi toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fb19-146">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="9fb19-147">Merhaba sunucu düzeyinde güvenlik duvarı kuralları etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="9fb19-147">Firewall rules at hello server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="9fb19-148">Otomatik geçiş zamanlama</span><span class="sxs-lookup"><span data-stu-id="9fb19-148">Automatic migration schedule</span></span>
<span data-ttu-id="9fb19-149">Otomatik geçişler 6:00 ile 6: 00'da (her bölge yerel saat) arasında kesinti zamanlama uyarınca hello sırasında oluşur.</span><span class="sxs-lookup"><span data-stu-id="9fb19-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during hello following outage schedule.</span></span>

| <span data-ttu-id="9fb19-150">**Bölge**</span><span class="sxs-lookup"><span data-stu-id="9fb19-150">**Region**</span></span> | <span data-ttu-id="9fb19-151">**Tahmini Başlangıç tarihi**</span><span class="sxs-lookup"><span data-stu-id="9fb19-151">**Estimated start date**</span></span> | <span data-ttu-id="9fb19-152">**Tahmini Bitiş tarihi**</span><span class="sxs-lookup"><span data-stu-id="9fb19-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="9fb19-153">Avustralya Doğu</span><span class="sxs-lookup"><span data-stu-id="9fb19-153">Australia East</span></span> |<span data-ttu-id="9fb19-154">Henüz karar değil</span><span class="sxs-lookup"><span data-stu-id="9fb19-154">Not determined yet</span></span> |<span data-ttu-id="9fb19-155">Henüz karar değil</span><span class="sxs-lookup"><span data-stu-id="9fb19-155">Not determined yet</span></span> |
| <span data-ttu-id="9fb19-156">Çin Doğu</span><span class="sxs-lookup"><span data-stu-id="9fb19-156">China East</span></span> |<span data-ttu-id="9fb19-157">9 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="9fb19-157">January 9, 2017</span></span> |<span data-ttu-id="9fb19-158">13 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="9fb19-158">January 13, 2017</span></span> |
| <span data-ttu-id="9fb19-159">Çin Kuzey</span><span class="sxs-lookup"><span data-stu-id="9fb19-159">China North</span></span> |<span data-ttu-id="9fb19-160">9 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="9fb19-160">January 9, 2017</span></span> |<span data-ttu-id="9fb19-161">13 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="9fb19-161">January 13, 2017</span></span> |
| <span data-ttu-id="9fb19-162">Almanya Orta</span><span class="sxs-lookup"><span data-stu-id="9fb19-162">Germany Central</span></span> |<span data-ttu-id="9fb19-163">9 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="9fb19-163">January 9, 2017</span></span> |<span data-ttu-id="9fb19-164">13 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="9fb19-164">January 13, 2017</span></span> |
| <span data-ttu-id="9fb19-165">Almanya Kuzeydoğu</span><span class="sxs-lookup"><span data-stu-id="9fb19-165">Germany Northeast</span></span> |<span data-ttu-id="9fb19-166">9 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="9fb19-166">January 9, 2017</span></span> |<span data-ttu-id="9fb19-167">13 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="9fb19-167">January 13, 2017</span></span> |
| <span data-ttu-id="9fb19-168">Hindistan Batı</span><span class="sxs-lookup"><span data-stu-id="9fb19-168">India West</span></span> |<span data-ttu-id="9fb19-169">Henüz karar değil</span><span class="sxs-lookup"><span data-stu-id="9fb19-169">Not determined yet</span></span> |<span data-ttu-id="9fb19-170">Henüz karar değil</span><span class="sxs-lookup"><span data-stu-id="9fb19-170">Not determined yet</span></span> |
| <span data-ttu-id="9fb19-171">Japonya Batı</span><span class="sxs-lookup"><span data-stu-id="9fb19-171">Japan West</span></span> |<span data-ttu-id="9fb19-172">Henüz karar değil</span><span class="sxs-lookup"><span data-stu-id="9fb19-172">Not determined yet</span></span> |<span data-ttu-id="9fb19-173">Henüz karar değil</span><span class="sxs-lookup"><span data-stu-id="9fb19-173">Not determined yet</span></span> |
| <span data-ttu-id="9fb19-174">Orta Kuzey ABD</span><span class="sxs-lookup"><span data-stu-id="9fb19-174">North Central US</span></span> |<span data-ttu-id="9fb19-175">9 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="9fb19-175">January 9, 2017</span></span> |<span data-ttu-id="9fb19-176">13 Ocak 2017</span><span class="sxs-lookup"><span data-stu-id="9fb19-176">January 13, 2017</span></span> |

## <a name="self-migration-toopremium-storage"></a><span data-ttu-id="9fb19-177">Kendi kendine geçiş toopremium depolama</span><span class="sxs-lookup"><span data-stu-id="9fb19-177">Self-migration toopremium storage</span></span>
<span data-ttu-id="9fb19-178">Kapalı kalma süresi ortaya çıktığında toocontrol istiyorsanız, adımları toomigrate mevcut bir veri ambarı standart depolama toopremium depolama alanında aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fb19-178">If you want toocontrol when your downtime will occur, you can use hello following steps toomigrate an existing data warehouse on standard storage toopremium storage.</span></span> <span data-ttu-id="9fb19-179">Bu seçeneği seçerseniz, bu bölgede hello otomatik geçiş başlamadan önce hello kendi kendine geçiş tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fb19-179">If you choose this option, you must complete hello self-migration before hello automatic migration begins in that region.</span></span> <span data-ttu-id="9fb19-180">Bu herhangi bir çakışmasına neden hello otomatik geçiş riskini önlemek sağlar (toohello başvuran [otomatik geçiş zamanlama][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="9fb19-180">This ensures that you avoid any risk of hello automatic migration causing a conflict (refer toohello [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="9fb19-181">Kendi kendine geçiş yönergeleri</span><span class="sxs-lookup"><span data-stu-id="9fb19-181">Self-migration instructions</span></span>
<span data-ttu-id="9fb19-182">Verilerinizi kendiniz ambar, hello yedekleme ve geri yükleme özellikleri toomigrate.</span><span class="sxs-lookup"><span data-stu-id="9fb19-182">toomigrate your data warehouse yourself, use hello backup and restore features.</span></span> <span data-ttu-id="9fb19-183">Merhaba geri yükleme hello Geçiş beklenen tootake yaklaşık bir saat başına veri ambarına başına depolama terabayt bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="9fb19-183">hello restore portion of hello migration is expected tootake around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="9fb19-184">Geçiş tamamlandıktan sonra aynı adı tookeep hello istiyorsanız hello izleyin [adımları toorename geçiş sırasında][steps toorename during migration].</span><span class="sxs-lookup"><span data-stu-id="9fb19-184">If you want tookeep hello same name after migration is complete, follow hello [steps toorename during migration][steps toorename during migration].</span></span>

1. <span data-ttu-id="9fb19-185">[Duraklatma] [ Pause] , veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="9fb19-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="9fb19-186">Otomatik yedekleme alır.</span><span class="sxs-lookup"><span data-stu-id="9fb19-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="9fb19-187">[Geri yükleme] [ Restore] en son anlık.</span><span class="sxs-lookup"><span data-stu-id="9fb19-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="9fb19-188">Mevcut veri ambarınız standart depolama silin.</span><span class="sxs-lookup"><span data-stu-id="9fb19-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="9fb19-189">**Bu adımı toodo başarısız olursa, hem veri ambarlarında için sizden ücret alınır.**</span><span class="sxs-lookup"><span data-stu-id="9fb19-189">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="9fb19-190">Merhaba aşağıdaki ayarları hello geçişin bir parçası taşınmaz:</span><span class="sxs-lookup"><span data-stu-id="9fb19-190">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="9fb19-191">Merhaba veritabanı düzeyinde denetimi yeniden etkin toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fb19-191">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="9fb19-192">Merhaba veritabanı düzeyinde güvenlik duvarı kuralları yeniden eklendi toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fb19-192">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="9fb19-193">Merhaba sunucu düzeyinde güvenlik duvarı kuralları etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="9fb19-193">Firewall rules at hello server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="9fb19-194">Veri ambarı (isteğe bağlı) geçiş sırasında yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="9fb19-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="9fb19-195">İki veritabanı aynı mantıksal sunucu olamaz hello üzerinde hello aynı adı.</span><span class="sxs-lookup"><span data-stu-id="9fb19-195">Two databases on hello same logical server cannot have hello same name.</span></span> <span data-ttu-id="9fb19-196">SQL veri ambarı artık hello özelliği toorename bir veri ambarı destekler.</span><span class="sxs-lookup"><span data-stu-id="9fb19-196">SQL Data Warehouse now supports hello ability toorename a data warehouse.</span></span>

<span data-ttu-id="9fb19-197">Bu örnekte, var olan veri ambarınız standart depolama üzerinde şu anda "MyDW." adlı düşünün</span><span class="sxs-lookup"><span data-stu-id="9fb19-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="9fb19-198">"MyDW" ALTER DATABASE komutu aşağıdaki hello kullanarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="9fb19-198">Rename "MyDW" by using hello following ALTER DATABASE command.</span></span> <span data-ttu-id="9fb19-199">(Bu örnekte, biz "MyDW_BeforeMigration." yeniden adlandırmadan)  Bu komut, tüm mevcut işlemleri durdurur ve hello ana veritabanı toosucceed yapılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fb19-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in hello master database toosucceed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="9fb19-200">[Duraklatma] [ Pause] "MyDW_BeforeMigration."</span><span class="sxs-lookup"><span data-stu-id="9fb19-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="9fb19-201">Otomatik yedekleme alır.</span><span class="sxs-lookup"><span data-stu-id="9fb19-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="9fb19-202">[Geri yükleme] [ Restore] , en son anlık hello ada sahip yeni bir veritabanı toobe (örneğin, "MyDW") kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9fb19-202">[Restore][Restore] from your most recent snapshot a new database with hello name it used toobe (for example, "MyDW").</span></span>
4. <span data-ttu-id="9fb19-203">"MyDW_BeforeMigration." Sil</span><span class="sxs-lookup"><span data-stu-id="9fb19-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="9fb19-204">**Bu adımı toodo başarısız olursa, hem veri ambarlarında için sizden ücret alınır.**</span><span class="sxs-lookup"><span data-stu-id="9fb19-204">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="9fb19-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9fb19-205">Next steps</span></span>
<span data-ttu-id="9fb19-206">Toopremium depolama Hello ile değiştirmek, veritabanı blob dosyaları sayısının artması hello temel alınan veri ambarınız mimarisinde de.</span><span class="sxs-lookup"><span data-stu-id="9fb19-206">With hello change toopremium storage, you also have an increased number of database blob files in hello underlying architecture of your data warehouse.</span></span> <span data-ttu-id="9fb19-207">Bu değişikliğin toomaximize hello performans avantajı, kümelenmiş columnstore dizinleri yeniden betik aşağıdaki hello kullanarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9fb19-207">toomaximize hello performance benefits of this change, rebuild your clustered columnstore indexes by using hello following script.</span></span> <span data-ttu-id="9fb19-208">mevcut veri toohello ek bloblarınızın bazıları zorlayarak Hello betik çalışır.</span><span class="sxs-lookup"><span data-stu-id="9fb19-208">hello script works by forcing some of your existing data toohello additional blobs.</span></span> <span data-ttu-id="9fb19-209">Hiçbir eylemde bulunmamanız halinde, tablolara daha fazla veri yükleme gibi hello veri zamanla doğal olarak dağıtan.</span><span class="sxs-lookup"><span data-stu-id="9fb19-209">If you take no action, hello data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="9fb19-210">**Ön koşullar:**</span><span class="sxs-lookup"><span data-stu-id="9fb19-210">**Prerequisites:**</span></span>

- <span data-ttu-id="9fb19-211">Merhaba veri ambarı 1.000 data warehouse birimleri veya sonrası çalıştırmanız gerekir (bkz [işlem güç ölçeklendirme][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="9fb19-211">hello data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="9fb19-212">Merhaba hello betiği yürütülürken kullanıcı hello olmalıdır [mediumrc rol] [ mediumrc role] ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="9fb19-212">hello user executing hello script should be in hello [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="9fb19-213">bir kullanıcı toothis rolü tooadd hello aşağıdakileri yürütün:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="9fb19-213">tooadd a user toothis role, execute hello following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

<span data-ttu-id="9fb19-214">Veri ambarınız ile herhangi bir sorunla karşılaştığınızda [destek bileti oluşturma] [ create a support ticket] ve başvuru "geçiş toopremium depolama" Merhaba olası neden olarak.</span><span class="sxs-lookup"><span data-stu-id="9fb19-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration toopremium storage” as hello possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
