---
title: SQL Data warehouse'da aaaTransactions | Microsoft Docs
description: "Çözümleri geliştirme için Azure SQL Data Warehouse'da işlemleri uygulamak için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="d69a4-103">SQL veri ambarı işlemleri</span><span class="sxs-lookup"><span data-stu-id="d69a4-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="d69a4-104">Beklediğiniz gibi SQL veri ambarı işlemleri hello veri ambarı iş yükü bir parçası olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="d69a4-104">As you would expect, SQL Data Warehouse supports transactions as part of hello data warehouse workload.</span></span> <span data-ttu-id="d69a4-105">Ancak, SQL Data Warehouse tooensure hello performansını karşılaştırılan tooSQL sunucu bazı özellikleri sınırlıdır ölçekte korunur.</span><span class="sxs-lookup"><span data-stu-id="d69a4-105">However, tooensure hello performance of SQL Data Warehouse is maintained at scale some features are limited when compared tooSQL Server.</span></span> <span data-ttu-id="d69a4-106">Bu makalede hello farklar vurgular ve listeleri başkalarının hello.</span><span class="sxs-lookup"><span data-stu-id="d69a4-106">This article highlights hello differences and lists hello others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="d69a4-107">İşlem yalıtım düzeyi</span><span class="sxs-lookup"><span data-stu-id="d69a4-107">Transaction isolation levels</span></span>
<span data-ttu-id="d69a4-108">SQL veri ambarı ACID işlemlerini uygular.</span><span class="sxs-lookup"><span data-stu-id="d69a4-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="d69a4-109">Bununla birlikte, hello yalıtım hello işlem desteği, çok sınırlıdır`READ UNCOMMITTED` ve bu değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="d69a4-109">However, hello Isolation of hello transactional support is limited too`READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="d69a4-110">Bu sizin için önemliyse tooprevent kirli verilerini okur kodlama yöntemleri sayısı uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d69a4-110">You can implement a number of coding methods tooprevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="d69a4-111">Merhaba en popüler yöntemleri hem CTAS hem de (genellikle kayan pencere düzenini hello olarak bilinir) tabloda bölüm değiştirme yararlanan tooprevent kullanıcıların hala hazırlanan veri sorgulama.</span><span class="sxs-lookup"><span data-stu-id="d69a4-111">hello most popular methods leverage both CTAS and table partition switching (often known as hello sliding window pattern) tooprevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="d69a4-112">Filtre öncesi hello verileri de popüler bir yaklaşım olduğu görünümleri.</span><span class="sxs-lookup"><span data-stu-id="d69a4-112">Views that pre-filter hello data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="d69a4-113">İşlem boyutu</span><span class="sxs-lookup"><span data-stu-id="d69a4-113">Transaction size</span></span>
<span data-ttu-id="d69a4-114">Bir tek veri değişikliği işlem boyutu sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="d69a4-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="d69a4-115">Merhaba sınır Bugün "dağıtım" uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d69a4-115">hello limit today is applied "per distribution".</span></span> <span data-ttu-id="d69a4-116">Bu nedenle, hello toplam ayırma hello dağıtım sayısına göre hello sınırı çarpılmasıyla hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="d69a4-116">Therefore, hello total allocation can be calculated by multiplying hello limit by hello distribution count.</span></span> <span data-ttu-id="d69a4-117">tooapproximate hello satır sayısının üst sınırını hello işlemde hello dağıtım cap hello tarafından her satırın toplam boyutu bölün.</span><span class="sxs-lookup"><span data-stu-id="d69a4-117">tooapproximate hello maximum number of rows in hello transaction divide hello distribution cap by hello total size of each row.</span></span> <span data-ttu-id="d69a4-118">Değişken uzunlukta sütunlar için hello en büyük boyutu kullanmak yerine bir ortalama sütun uzunluğu alma göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="d69a4-118">For variable length columns consider taking an average column length rather than using hello maximum size.</span></span>

<span data-ttu-id="d69a4-119">Merhaba aşağıda hello tablosundaki aşağıdaki varsayımlar yapılmıştır:</span><span class="sxs-lookup"><span data-stu-id="d69a4-119">In hello table below hello following assumptions have been made:</span></span>

* <span data-ttu-id="d69a4-120">Bir dağılmış verilerinizin oluştu</span><span class="sxs-lookup"><span data-stu-id="d69a4-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="d69a4-121">Merhaba ortalama satır uzunluğu 250 bayttır</span><span class="sxs-lookup"><span data-stu-id="d69a4-121">hello average row length is 250 bytes</span></span>

| <span data-ttu-id="d69a4-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="d69a4-122">[DWU][DWU]</span></span> | <span data-ttu-id="d69a4-123">Dağıtım (GiB) cap</span><span class="sxs-lookup"><span data-stu-id="d69a4-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="d69a4-124">Dağıtımların sayısı</span><span class="sxs-lookup"><span data-stu-id="d69a4-124">Number of Distributions</span></span> | <span data-ttu-id="d69a4-125">En fazla işlem boyutu (GiB)</span><span class="sxs-lookup"><span data-stu-id="d69a4-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="d69a4-126"># Dağıtım başına satır</span><span class="sxs-lookup"><span data-stu-id="d69a4-126"># Rows per distribution</span></span> | <span data-ttu-id="d69a4-127">İşlem başına en fazla satır</span><span class="sxs-lookup"><span data-stu-id="d69a4-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="d69a4-128">DW100</span><span class="sxs-lookup"><span data-stu-id="d69a4-128">DW100</span></span> |<span data-ttu-id="d69a4-129">1</span><span class="sxs-lookup"><span data-stu-id="d69a4-129">1</span></span> |<span data-ttu-id="d69a4-130">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-130">60</span></span> |<span data-ttu-id="d69a4-131">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-131">60</span></span> |<span data-ttu-id="d69a4-132">4,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-132">4,000,000</span></span> |<span data-ttu-id="d69a4-133">240,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-133">240,000,000</span></span> |
| <span data-ttu-id="d69a4-134">DW200</span><span class="sxs-lookup"><span data-stu-id="d69a4-134">DW200</span></span> |<span data-ttu-id="d69a4-135">1.5</span><span class="sxs-lookup"><span data-stu-id="d69a4-135">1.5</span></span> |<span data-ttu-id="d69a4-136">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-136">60</span></span> |<span data-ttu-id="d69a4-137">90</span><span class="sxs-lookup"><span data-stu-id="d69a4-137">90</span></span> |<span data-ttu-id="d69a4-138">6,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-138">6,000,000</span></span> |<span data-ttu-id="d69a4-139">360,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-139">360,000,000</span></span> |
| <span data-ttu-id="d69a4-140">DW300</span><span class="sxs-lookup"><span data-stu-id="d69a4-140">DW300</span></span> |<span data-ttu-id="d69a4-141">2.25</span><span class="sxs-lookup"><span data-stu-id="d69a4-141">2.25</span></span> |<span data-ttu-id="d69a4-142">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-142">60</span></span> |<span data-ttu-id="d69a4-143">135</span><span class="sxs-lookup"><span data-stu-id="d69a4-143">135</span></span> |<span data-ttu-id="d69a4-144">9,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-144">9,000,000</span></span> |<span data-ttu-id="d69a4-145">540,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-145">540,000,000</span></span> |
| <span data-ttu-id="d69a4-146">DW400</span><span class="sxs-lookup"><span data-stu-id="d69a4-146">DW400</span></span> |<span data-ttu-id="d69a4-147">3</span><span class="sxs-lookup"><span data-stu-id="d69a4-147">3</span></span> |<span data-ttu-id="d69a4-148">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-148">60</span></span> |<span data-ttu-id="d69a4-149">180</span><span class="sxs-lookup"><span data-stu-id="d69a4-149">180</span></span> |<span data-ttu-id="d69a4-150">12,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-150">12,000,000</span></span> |<span data-ttu-id="d69a4-151">720,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-151">720,000,000</span></span> |
| <span data-ttu-id="d69a4-152">DW500</span><span class="sxs-lookup"><span data-stu-id="d69a4-152">DW500</span></span> |<span data-ttu-id="d69a4-153">3.75</span><span class="sxs-lookup"><span data-stu-id="d69a4-153">3.75</span></span> |<span data-ttu-id="d69a4-154">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-154">60</span></span> |<span data-ttu-id="d69a4-155">225</span><span class="sxs-lookup"><span data-stu-id="d69a4-155">225</span></span> |<span data-ttu-id="d69a4-156">15,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-156">15,000,000</span></span> |<span data-ttu-id="d69a4-157">900,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-157">900,000,000</span></span> |
| <span data-ttu-id="d69a4-158">DW600</span><span class="sxs-lookup"><span data-stu-id="d69a4-158">DW600</span></span> |<span data-ttu-id="d69a4-159">4.5</span><span class="sxs-lookup"><span data-stu-id="d69a4-159">4.5</span></span> |<span data-ttu-id="d69a4-160">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-160">60</span></span> |<span data-ttu-id="d69a4-161">270</span><span class="sxs-lookup"><span data-stu-id="d69a4-161">270</span></span> |<span data-ttu-id="d69a4-162">18,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-162">18,000,000</span></span> |<span data-ttu-id="d69a4-163">1,080,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-163">1,080,000,000</span></span> |
| <span data-ttu-id="d69a4-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="d69a4-164">DW1000</span></span> |<span data-ttu-id="d69a4-165">7.5</span><span class="sxs-lookup"><span data-stu-id="d69a4-165">7.5</span></span> |<span data-ttu-id="d69a4-166">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-166">60</span></span> |<span data-ttu-id="d69a4-167">450</span><span class="sxs-lookup"><span data-stu-id="d69a4-167">450</span></span> |<span data-ttu-id="d69a4-168">30,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-168">30,000,000</span></span> |<span data-ttu-id="d69a4-169">1,800,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-169">1,800,000,000</span></span> |
| <span data-ttu-id="d69a4-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="d69a4-170">DW1200</span></span> |<span data-ttu-id="d69a4-171">9</span><span class="sxs-lookup"><span data-stu-id="d69a4-171">9</span></span> |<span data-ttu-id="d69a4-172">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-172">60</span></span> |<span data-ttu-id="d69a4-173">540</span><span class="sxs-lookup"><span data-stu-id="d69a4-173">540</span></span> |<span data-ttu-id="d69a4-174">36,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-174">36,000,000</span></span> |<span data-ttu-id="d69a4-175">2,160,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-175">2,160,000,000</span></span> |
| <span data-ttu-id="d69a4-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="d69a4-176">DW1500</span></span> |<span data-ttu-id="d69a4-177">11.25</span><span class="sxs-lookup"><span data-stu-id="d69a4-177">11.25</span></span> |<span data-ttu-id="d69a4-178">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-178">60</span></span> |<span data-ttu-id="d69a4-179">675</span><span class="sxs-lookup"><span data-stu-id="d69a4-179">675</span></span> |<span data-ttu-id="d69a4-180">45,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-180">45,000,000</span></span> |<span data-ttu-id="d69a4-181">2,700,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-181">2,700,000,000</span></span> |
| <span data-ttu-id="d69a4-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="d69a4-182">DW2000</span></span> |<span data-ttu-id="d69a4-183">15</span><span class="sxs-lookup"><span data-stu-id="d69a4-183">15</span></span> |<span data-ttu-id="d69a4-184">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-184">60</span></span> |<span data-ttu-id="d69a4-185">900</span><span class="sxs-lookup"><span data-stu-id="d69a4-185">900</span></span> |<span data-ttu-id="d69a4-186">60,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-186">60,000,000</span></span> |<span data-ttu-id="d69a4-187">3,600,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-187">3,600,000,000</span></span> |
| <span data-ttu-id="d69a4-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="d69a4-188">DW3000</span></span> |<span data-ttu-id="d69a4-189">22.5</span><span class="sxs-lookup"><span data-stu-id="d69a4-189">22.5</span></span> |<span data-ttu-id="d69a4-190">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-190">60</span></span> |<span data-ttu-id="d69a4-191">1,350</span><span class="sxs-lookup"><span data-stu-id="d69a4-191">1,350</span></span> |<span data-ttu-id="d69a4-192">90,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-192">90,000,000</span></span> |<span data-ttu-id="d69a4-193">5,400,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-193">5,400,000,000</span></span> |
| <span data-ttu-id="d69a4-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="d69a4-194">DW6000</span></span> |<span data-ttu-id="d69a4-195">45</span><span class="sxs-lookup"><span data-stu-id="d69a4-195">45</span></span> |<span data-ttu-id="d69a4-196">60</span><span class="sxs-lookup"><span data-stu-id="d69a4-196">60</span></span> |<span data-ttu-id="d69a4-197">2,700</span><span class="sxs-lookup"><span data-stu-id="d69a4-197">2,700</span></span> |<span data-ttu-id="d69a4-198">180,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-198">180,000,000</span></span> |<span data-ttu-id="d69a4-199">10,800,000,000</span><span class="sxs-lookup"><span data-stu-id="d69a4-199">10,800,000,000</span></span> |

<span data-ttu-id="d69a4-200">Merhaba işlem boyut sınırı, işlem veya işlem uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d69a4-200">hello transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="d69a4-201">Tüm eşzamanlı işlemler arasında uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="d69a4-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="d69a4-202">Bu nedenle her bir işlem olduğundan toowrite bu miktarda veri toohello günlük izin verilir.</span><span class="sxs-lookup"><span data-stu-id="d69a4-202">Therefore each transaction is permitted toowrite this amount of data toohello log.</span></span> 

<span data-ttu-id="d69a4-203">toooptimize ve hello toohello günlüğüne yazılan veri miktarını en aza toohello başvurun [işlemleri en iyi uygulamalar] [ Transactions best practices] makalesi.</span><span class="sxs-lookup"><span data-stu-id="d69a4-203">toooptimize and minimize hello amount of data written toohello log please refer toohello [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="d69a4-204">Hello için KARMA işlem boyutu yalnızca elde edilebilir veya dağıtılmış ROUND_ROBIN tabloları, burada hello yayılan veri hello maksimum bile.</span><span class="sxs-lookup"><span data-stu-id="d69a4-204">hello maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where hello spread of hello data is even.</span></span> <span data-ttu-id="d69a4-205">Merhaba işlem toohello dağıtımları çarpık bir şekilde veri yazma, hello sınırı önceki toohello maksimum hareket boyut üst sınırına büyük olasılıkla toobe yoktur.</span><span class="sxs-lookup"><span data-stu-id="d69a4-205">If hello transaction is writing data in a skewed fashion toohello distributions then hello limit is likely toobe reached prior toohello maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="d69a4-206">İşlem durumu</span><span class="sxs-lookup"><span data-stu-id="d69a4-206">Transaction state</span></span>
<span data-ttu-id="d69a4-207">SQL veri ambarı hello XACT_STATE() işlevi tooreport hello değerini -2 kullanarak başarısız bir işlem kullanır.</span><span class="sxs-lookup"><span data-stu-id="d69a4-207">SQL Data Warehouse uses hello XACT_STATE() function tooreport a failed transaction using hello value -2.</span></span> <span data-ttu-id="d69a4-208">Bu hello işlem başarısız oldu ve yalnızca geri almak için işaretlenmiş anlamına gelir</span><span class="sxs-lookup"><span data-stu-id="d69a4-208">This means that hello transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="d69a4-209">Merhaba -2 hello XACT_STATE işlevi toodenote başarısız işlem temsil farklı bir davranış tooSQL sunucusu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d69a4-209">hello use of -2 by hello XACT_STATE function toodenote a failed transaction represents different behavior tooSQL Server.</span></span> <span data-ttu-id="d69a4-210">SQL Server hello -1 değeri toorepresent kaydedilemez bir işlem kullanır.</span><span class="sxs-lookup"><span data-stu-id="d69a4-210">SQL Server uses hello value -1 toorepresent an un-committable transaction.</span></span> <span data-ttu-id="d69a4-211">SQL Server, olarak kaydedilemez işaretlenmiş toobe sahip bir işlemin içindeki bazı hatalar dayanabilir.</span><span class="sxs-lookup"><span data-stu-id="d69a4-211">SQL Server can tolerate some errors inside a transaction without it having toobe marked as un-committable.</span></span> <span data-ttu-id="d69a4-212">Örneğin `SELECT 1/0` hataya neden, ancak bir işlem kaydedilemez bir duruma zorla sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="d69a4-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="d69a4-213">SQL Server hello kaydedilemez işlemde de okuma izin verir.</span><span class="sxs-lookup"><span data-stu-id="d69a4-213">SQL Server also permits reads in hello un-committable transaction.</span></span> <span data-ttu-id="d69a4-214">Ancak, SQL Data Warehouse, bunun izin vermez.</span><span class="sxs-lookup"><span data-stu-id="d69a4-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="d69a4-215">Merhaba -2 durumu otomatik olarak girer ve mümkün toomake olmaz bir SQL Data Warehouse işlem içinde bir hata oluşursa, hello deyimi geri kadar daha fazla deyimleri seçin.</span><span class="sxs-lookup"><span data-stu-id="d69a4-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter hello -2 state and you will not be able toomake any further select statements until hello statement has been rolled back.</span></span> <span data-ttu-id="d69a4-216">Bu nedenle, XACT_STATE() gibi kullanıyorsa, uygulama kodu toosee toomake kod değişikliklerini gerekebilir önemli toocheck olur.</span><span class="sxs-lookup"><span data-stu-id="d69a4-216">It is therefore important toocheck that your application code toosee if it uses  XACT_STATE() as you may need toomake code modifications.</span></span>
> 
> 

<span data-ttu-id="d69a4-217">Örneğin, SQL Server'da şuna benzer bir işlem görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d69a4-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="d69a4-218">Ardından yukarıda olduğu gibi kodunuzu değiştirmeden bırakırsanız hello aşağıdaki hata iletisini alırsınız:</span><span class="sxs-lookup"><span data-stu-id="d69a4-218">If you leave your code as it is above then you will get hello following error message:</span></span>

<span data-ttu-id="d69a4-219">Msg 111233, Level 16, State 1, 1 satır 111233; hello işlem iptal ve bekleyen tüm değişiklikleri geri alındığından geçerli.</span><span class="sxs-lookup"><span data-stu-id="d69a4-219">Msg 111233, Level 16, State 1, Line 1 111233;hello current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="d69a4-220">Neden: Bir işlemi yalnızca geri alma durumunda açıkça DDL, DML veya SELECT deyimi önce geri alınmadı.</span><span class="sxs-lookup"><span data-stu-id="d69a4-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="d69a4-221">Ayrıca hello çıktı hello ERROR_ * işlevlerin almazsınız.</span><span class="sxs-lookup"><span data-stu-id="d69a4-221">You will also not get hello output of hello ERROR_* functions.</span></span>

<span data-ttu-id="d69a4-222">SQL veri ambarı'nda hello kod biraz değiştirilmiş toobe gerekir:</span><span class="sxs-lookup"><span data-stu-id="d69a4-222">In SQL Data Warehouse hello code needs toobe slightly altered:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="d69a4-223">Merhaba, şimdi davranış gözlenir bekleniyordu.</span><span class="sxs-lookup"><span data-stu-id="d69a4-223">hello expected behavior is now observed.</span></span> <span data-ttu-id="d69a4-224">Merhaba hata hello işlemde yönetilir ve beklendiği gibi hello ERROR_ * işlevleri değerler sağlayın.</span><span class="sxs-lookup"><span data-stu-id="d69a4-224">hello error in hello transaction is managed and hello ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="d69a4-225">Değişen tek şey, hello `ROLLBACK` hello hello hata bilgilerinin hello okumadan önce hello işleme toohappen sahipti. `CATCH` bloğu.</span><span class="sxs-lookup"><span data-stu-id="d69a4-225">All that has changed is that hello `ROLLBACK` of hello transaction had toohappen before hello read of hello error information in hello `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="d69a4-226">Error_Line() işlevi</span><span class="sxs-lookup"><span data-stu-id="d69a4-226">Error_Line() function</span></span>
<span data-ttu-id="d69a4-227">Ayrıca, SQL Data Warehouse uygulama ya da hello ERROR_LINE() işlevini destekler olduğunu dikkate değerdir.</span><span class="sxs-lookup"><span data-stu-id="d69a4-227">It is also worth noting that SQL Data Warehouse does not implement or support hello ERROR_LINE() function.</span></span> <span data-ttu-id="d69a4-228">Bu, kodunuzda varsa tooremove gerekir, toobe SQL Data Warehouse ile uyumlu.</span><span class="sxs-lookup"><span data-stu-id="d69a4-228">If you have this in your code you will need tooremove it toobe compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="d69a4-229">Sorgu etiketleri, kodunuzda, bunun yerine tooimplement eşdeğer işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d69a4-229">Use query labels in your code instead tooimplement equivalent functionality.</span></span> <span data-ttu-id="d69a4-230">Lütfen toohello bakın [etiket] [ LABEL] bu özellik hakkında daha fazla ayrıntı için makale.</span><span class="sxs-lookup"><span data-stu-id="d69a4-230">Please refer toohello [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="d69a4-231">THROW ve RAISERROR kullanma</span><span class="sxs-lookup"><span data-stu-id="d69a4-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="d69a4-232">THROW SQL Data warehouse'da özel durumlarını oluşturma için daha modern uygulama hello ancak RAISERROR de desteklenen değildir.</span><span class="sxs-lookup"><span data-stu-id="d69a4-232">THROW is hello more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="d69a4-233">Dikkat toohowever ödeme değer olan bazı farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="d69a4-233">There are a few differences that are worth paying attention toohowever.</span></span>

* <span data-ttu-id="d69a4-234">Kullanıcı tanımlı hata iletileri sayı hello THROW 100.000 150.000 aralığının olamaz</span><span class="sxs-lookup"><span data-stu-id="d69a4-234">User defined error messages numbers cannot be in hello 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="d69a4-235">RAISERROR hata iletileri 50.000 düzeltilen</span><span class="sxs-lookup"><span data-stu-id="d69a4-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="d69a4-236">Sistem iletilerinde kullanımı desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="d69a4-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="d69a4-237">Limitiations</span><span class="sxs-lookup"><span data-stu-id="d69a4-237">Limitiations</span></span>
<span data-ttu-id="d69a4-238">SQL veri ambarı tootransactions ilgili diğer bazı kısıtlamalar sahip.</span><span class="sxs-lookup"><span data-stu-id="d69a4-238">SQL Data Warehouse does have a few other restrictions that relate tootransactions.</span></span>

<span data-ttu-id="d69a4-239">Bunlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d69a4-239">They are as follows:</span></span>

* <span data-ttu-id="d69a4-240">Dağıtılmış işlem</span><span class="sxs-lookup"><span data-stu-id="d69a4-240">No distributed transactions</span></span>
* <span data-ttu-id="d69a4-241">İzin verilen hiçbir iç içe geçmiş işlemler</span><span class="sxs-lookup"><span data-stu-id="d69a4-241">No nested transactions permitted</span></span>
* <span data-ttu-id="d69a4-242">İzin verilen noktaları kaydetme</span><span class="sxs-lookup"><span data-stu-id="d69a4-242">No save points allowed</span></span>
* <span data-ttu-id="d69a4-243">Adlandırılmış işlem</span><span class="sxs-lookup"><span data-stu-id="d69a4-243">No named transactions</span></span>
* <span data-ttu-id="d69a4-244">İşaretli işlem</span><span class="sxs-lookup"><span data-stu-id="d69a4-244">No marked transactions</span></span>
* <span data-ttu-id="d69a4-245">DDL gibi desteği `CREATE TABLE` işlem içinde bir kullanıcı tanımlı</span><span class="sxs-lookup"><span data-stu-id="d69a4-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="d69a4-246">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d69a4-246">Next steps</span></span>
<span data-ttu-id="d69a4-247">işlemler, en iyi duruma getirme hakkında daha fazla toolearn bkz [işlemleri en iyi uygulamalar][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="d69a4-247">toolearn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="d69a4-248">toolearn diğer SQL Data Warehouse en iyi uygulamalar hakkında bkz [SQL veri ambarı en iyi yöntemler][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="d69a4-248">toolearn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
