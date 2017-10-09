---
title: "SQL veri ambarı aaaConcurrency ve iş yükü yönetimi | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse eşzamanlılık ve iş yükü yönetimi anlayın."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a><span data-ttu-id="19bc3-103">SQL veri ambarı eşzamanlılık ve iş yükü yönetimi</span><span class="sxs-lookup"><span data-stu-id="19bc3-103">Concurrency and workload management in SQL Data Warehouse</span></span>
<span data-ttu-id="19bc3-104">ölçekli olarak Microsoft Azure SQL Data Warehouse toodeliver tahmin edilebilir performans yardımcı olan denetim eşzamanlılık düzeyleri ve bellek ve CPU önceliği gibi kaynak ayırma.</span><span class="sxs-lookup"><span data-stu-id="19bc3-104">toodeliver predictable performance at scale, Microsoft Azure SQL Data Warehouse helps you control concurrency levels and resource allocations like memory and CPU prioritization.</span></span> <span data-ttu-id="19bc3-105">Bu makalede nasıl her iki özellik uygulanan ve nasıl veri ambarında denetlenebilecek açıklayan eşzamanlılık ve iş yükü yönetimi toohello kavramları tanıtır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-105">This article introduces you toohello concepts of concurrency and workload management, explaining how both features have been implemented and how you can control them in your data warehouse.</span></span> <span data-ttu-id="19bc3-106">SQL veri ambarı iş yükü çok kullanıcılı ortamlar destek hedeflenen toohelp yönetimidir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-106">SQL Data Warehouse workload management is intended toohelp you support multi-user environments.</span></span> <span data-ttu-id="19bc3-107">Çoklu kiracı iş yükleri için tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-107">It is not intended for multi-tenant workloads.</span></span>

## <a name="concurrency-limits"></a><span data-ttu-id="19bc3-108">Eşzamanlılık sınırları</span><span class="sxs-lookup"><span data-stu-id="19bc3-108">Concurrency limits</span></span>
<span data-ttu-id="19bc3-109">SQL veri ambarı too1, 024 eşzamanlı bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="19bc3-109">SQL Data Warehouse allows up too1,024 concurrent connections.</span></span> <span data-ttu-id="19bc3-110">Tüm 1.024 bağlantıları sorguları eşzamanlı olarak gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19bc3-110">All 1,024 connections can submit queries concurrently.</span></span> <span data-ttu-id="19bc3-111">Ancak, SQL Data Warehouse toooptimize üretilen işi her sorgu en az bellek ataması aldığını bazı sorgular tooensure sırası.</span><span class="sxs-lookup"><span data-stu-id="19bc3-111">However, toooptimize throughput, SQL Data Warehouse may queue some queries tooensure that each query receives a minimal memory grant.</span></span> <span data-ttu-id="19bc3-112">Queuing sorgu yürütme sırasında oluşur.</span><span class="sxs-lookup"><span data-stu-id="19bc3-112">Queuing occurs at query execution time.</span></span> <span data-ttu-id="19bc3-113">Eşzamanlılık sınırları ulaşıldığında, SQL Data Warehouse artırabilirsiniz olduğunda queuing sorgular tarafından bellek kaynaklarının etkin sorgular erişim toocritically elde etmenizi sağlayarak toplam verimlilik gereklidir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-113">By queuing queries when concurrency limits are reached, SQL Data Warehouse can increase total throughput by ensuring that active queries get access toocritically needed memory resources.</span></span>  

<span data-ttu-id="19bc3-114">Eşzamanlılık sınırları iki kavramları tarafından yönetilir: *eş zamanlı sorguları* ve *eşzamanlılık yuvaları*.</span><span class="sxs-lookup"><span data-stu-id="19bc3-114">Concurrency limits are governed by two concepts: *concurrent queries* and *concurrency slots*.</span></span> <span data-ttu-id="19bc3-115">Bir sorgu tooexecute için hello sorgu eşzamanlılık sınırı ve hello eşzamanlılık yuvası ayırma içinde yürütülmelidir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-115">For a query tooexecute, it must execute within both hello query concurrency limit and hello concurrency slot allocation.</span></span>

* <span data-ttu-id="19bc3-116">Eş zamanlı sorgular olan hello sorguları aynı hello yürütme süresi.</span><span class="sxs-lookup"><span data-stu-id="19bc3-116">Concurrent queries are hello queries executing at hello same time.</span></span> <span data-ttu-id="19bc3-117">SQL veri ambarı too32 eşzamanlı hello daha büyük DWU boyutları sorgulamaları yukarı destekler.</span><span class="sxs-lookup"><span data-stu-id="19bc3-117">SQL Data Warehouse supports up too32 concurrent queries on hello larger DWU sizes.</span></span>
* <span data-ttu-id="19bc3-118">Eşzamanlılık yuvaları üzerinde DWU göre ayrılır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-118">Concurrency slots are allocated based on DWU.</span></span> <span data-ttu-id="19bc3-119">Her 100 DWU 4 eşzamanlılık yuvası sağlar.</span><span class="sxs-lookup"><span data-stu-id="19bc3-119">Each 100 DWU provides 4 concurrency slots.</span></span> <span data-ttu-id="19bc3-120">Örneğin, bir DW100 4 eşzamanlılık yuvası ayırır ve 40 DW1000 ayırır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-120">For example, a DW100 allocates 4 concurrency slots and DW1000 allocates 40.</span></span> <span data-ttu-id="19bc3-121">Bir veya daha fazla eşzamanlılık yuvaları, üzerinde hello bağımlı her sorgu tüketir [kaynak sınıfı](#resource-classes) hello sorgu.</span><span class="sxs-lookup"><span data-stu-id="19bc3-121">Each query consumes one or more concurrency slots, dependent on hello [resource class](#resource-classes) of hello query.</span></span> <span data-ttu-id="19bc3-122">Merhaba smallrc kaynak sınıfında çalışan sorguları bir eşzamanlılık yuvası kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-122">Queries running in hello smallrc resource class consume one concurrency slot.</span></span> <span data-ttu-id="19bc3-123">Sorguları daha yüksek bir kaynak sınıfında çalıştırma başka eşzamanlılık yuva kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-123">Queries running in a higher resource class consume more concurrency slots.</span></span>

<span data-ttu-id="19bc3-124">Merhaba aşağıdaki tabloda hello sınırları eş zamanlı sorgular ve hello adresindeki eşzamanlılık yuvaları için çeşitli DWU boyutları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-124">hello following table describes hello limits for both concurrent queries and concurrency slots at hello various DWU sizes.</span></span>

### <a name="concurrency-limits"></a><span data-ttu-id="19bc3-125">Eşzamanlılık sınırları</span><span class="sxs-lookup"><span data-stu-id="19bc3-125">Concurrency limits</span></span>
| <span data-ttu-id="19bc3-126">DWU</span><span class="sxs-lookup"><span data-stu-id="19bc3-126">DWU</span></span> | <span data-ttu-id="19bc3-127">En fazla eş zamanlı sorgular</span><span class="sxs-lookup"><span data-stu-id="19bc3-127">Max concurrent queries</span></span> | <span data-ttu-id="19bc3-128">Ayrılmış eşzamanlılık yuvaları</span><span class="sxs-lookup"><span data-stu-id="19bc3-128">Concurrency slots allocated</span></span> |
|:--- |:---:|:---:|
| <span data-ttu-id="19bc3-129">DW100</span><span class="sxs-lookup"><span data-stu-id="19bc3-129">DW100</span></span> |<span data-ttu-id="19bc3-130">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-130">4</span></span> |<span data-ttu-id="19bc3-131">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-131">4</span></span> |
| <span data-ttu-id="19bc3-132">DW200</span><span class="sxs-lookup"><span data-stu-id="19bc3-132">DW200</span></span> |<span data-ttu-id="19bc3-133">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-133">8</span></span> |<span data-ttu-id="19bc3-134">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-134">8</span></span> |
| <span data-ttu-id="19bc3-135">DW300</span><span class="sxs-lookup"><span data-stu-id="19bc3-135">DW300</span></span> |<span data-ttu-id="19bc3-136">12</span><span class="sxs-lookup"><span data-stu-id="19bc3-136">12</span></span> |<span data-ttu-id="19bc3-137">12</span><span class="sxs-lookup"><span data-stu-id="19bc3-137">12</span></span> |
| <span data-ttu-id="19bc3-138">DW400</span><span class="sxs-lookup"><span data-stu-id="19bc3-138">DW400</span></span> |<span data-ttu-id="19bc3-139">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-139">16</span></span> |<span data-ttu-id="19bc3-140">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-140">16</span></span> |
| <span data-ttu-id="19bc3-141">DW500</span><span class="sxs-lookup"><span data-stu-id="19bc3-141">DW500</span></span> |<span data-ttu-id="19bc3-142">20</span><span class="sxs-lookup"><span data-stu-id="19bc3-142">20</span></span> |<span data-ttu-id="19bc3-143">20</span><span class="sxs-lookup"><span data-stu-id="19bc3-143">20</span></span> |
| <span data-ttu-id="19bc3-144">DW600</span><span class="sxs-lookup"><span data-stu-id="19bc3-144">DW600</span></span> |<span data-ttu-id="19bc3-145">24</span><span class="sxs-lookup"><span data-stu-id="19bc3-145">24</span></span> |<span data-ttu-id="19bc3-146">24</span><span class="sxs-lookup"><span data-stu-id="19bc3-146">24</span></span> |
| <span data-ttu-id="19bc3-147">DW1000</span><span class="sxs-lookup"><span data-stu-id="19bc3-147">DW1000</span></span> |<span data-ttu-id="19bc3-148">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-148">32</span></span> |<span data-ttu-id="19bc3-149">40</span><span class="sxs-lookup"><span data-stu-id="19bc3-149">40</span></span> |
| <span data-ttu-id="19bc3-150">DW1200</span><span class="sxs-lookup"><span data-stu-id="19bc3-150">DW1200</span></span> |<span data-ttu-id="19bc3-151">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-151">32</span></span> |<span data-ttu-id="19bc3-152">48</span><span class="sxs-lookup"><span data-stu-id="19bc3-152">48</span></span> |
| <span data-ttu-id="19bc3-153">DW1500</span><span class="sxs-lookup"><span data-stu-id="19bc3-153">DW1500</span></span> |<span data-ttu-id="19bc3-154">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-154">32</span></span> |<span data-ttu-id="19bc3-155">60</span><span class="sxs-lookup"><span data-stu-id="19bc3-155">60</span></span> |
| <span data-ttu-id="19bc3-156">DW2000</span><span class="sxs-lookup"><span data-stu-id="19bc3-156">DW2000</span></span> |<span data-ttu-id="19bc3-157">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-157">32</span></span> |<span data-ttu-id="19bc3-158">80</span><span class="sxs-lookup"><span data-stu-id="19bc3-158">80</span></span> |
| <span data-ttu-id="19bc3-159">DW3000</span><span class="sxs-lookup"><span data-stu-id="19bc3-159">DW3000</span></span> |<span data-ttu-id="19bc3-160">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-160">32</span></span> |<span data-ttu-id="19bc3-161">120</span><span class="sxs-lookup"><span data-stu-id="19bc3-161">120</span></span> |
| <span data-ttu-id="19bc3-162">DW6000</span><span class="sxs-lookup"><span data-stu-id="19bc3-162">DW6000</span></span> |<span data-ttu-id="19bc3-163">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-163">32</span></span> |<span data-ttu-id="19bc3-164">240</span><span class="sxs-lookup"><span data-stu-id="19bc3-164">240</span></span> |

<span data-ttu-id="19bc3-165">Bu eşikler biri karşılandığında yeni sorgular sıraya ve bir ilk giren ilk çıkar özelliğine sahip temelinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="19bc3-165">When one of these thresholds is met, new queries are queued and executed on a first-in, first-out basis.</span></span>  <span data-ttu-id="19bc3-166">Sıraya alınan sorguları bir sorguları tamamlandıktan ve hello sınırları hello sayısı sorgular ve yuvaları denk olarak yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-166">As a queries finishes and hello number of queries and slots falls below hello limits, queued queries are released.</span></span> 

> [!NOTE]  
> <span data-ttu-id="19bc3-167">*Seçin* sorguları özel olarak üzerinde yürütme (Dmv'leri) dinamik yönetim görünümleri veya Katalog görünümleri değil yönetilir hello eşzamanlılık sınırları biriyle.</span><span class="sxs-lookup"><span data-stu-id="19bc3-167">*Select* queries executing exclusively on dynamic management views (DMVs) or catalog views are not governed by any of hello concurrency limits.</span></span> <span data-ttu-id="19bc3-168">Merhaba sistem hello sorguları üzerinde yürütme sayısı bağımsız olarak izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19bc3-168">You can monitor hello system regardless of hello number of queries executing on it.</span></span>
> 
> 

## <a name="resource-classes"></a><span data-ttu-id="19bc3-169">Kaynak sınıfları</span><span class="sxs-lookup"><span data-stu-id="19bc3-169">Resource classes</span></span>
<span data-ttu-id="19bc3-170">Kaynak bellek ayırma ve CPU döngülerini tooa sorgu verilen denetlemenize yardımcı olur sınıfları.</span><span class="sxs-lookup"><span data-stu-id="19bc3-170">Resource classes help you control memory allocation and CPU cycles given tooa query.</span></span> <span data-ttu-id="19bc3-171">İki tür kaynak sınıfları tooa kullanıcı veritabanı rolleri hello biçiminde atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19bc3-171">You can assign two types of resource classes tooa user in hello form of database roles.</span></span> <span data-ttu-id="19bc3-172">iki tür kaynak sınıfı Hello aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="19bc3-172">hello two types of resource classes are as follows:</span></span>
1. <span data-ttu-id="19bc3-173">Dinamik kaynak sınıflar (**smallrc, mediumrc, largerc, xlargerc**) bir değişken hello bağlı olarak bellek miktarını tahsis geçerli DWU.</span><span class="sxs-lookup"><span data-stu-id="19bc3-173">Dynamic Resource Classes (**smallrc, mediumrc, largerc, xlargerc**) allocate a variable amount of memory depending on hello current DWU.</span></span> <span data-ttu-id="19bc3-174">Bunun anlamı tooa ölçeklendirdiğinizde büyük DWU sorgularınızı otomatik olarak daha fazla bellek alın.</span><span class="sxs-lookup"><span data-stu-id="19bc3-174">This means that when you scale up tooa larger DWU, your queries automatically get more memory.</span></span> 
2. <span data-ttu-id="19bc3-175">Statik kaynak sınıflar (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) hello tahsis bellek bakılmaksızın aynı miktarda hello geçerli DWU (koşuluyla DWU kendisini hello yeterli bellek olduğundan).</span><span class="sxs-lookup"><span data-stu-id="19bc3-175">Static Resource Classes (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) allocate hello same amount of memory regardless of hello current DWU (provided that hello DWU itself has enough memory).</span></span> <span data-ttu-id="19bc3-176">Bu büyük Dwu üzerinde size daha fazla sorguları her kaynak sınıfında eşzamanlı olarak çalıştırabileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-176">This means that on larger DWUs, you can run more queries in each resource class concurrently.</span></span>

<span data-ttu-id="19bc3-177">Kullanıcılar **smallrc** ve **staticrc10** daha az miktarda belleğe verilir ve daha yüksek eşzamanlılık avantajından yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19bc3-177">Users in **smallrc** and **staticrc10** are given a smaller amount of memory and can take advantage of higher concurrency.</span></span> <span data-ttu-id="19bc3-178">Kullanıcılar buna karşılık, atanan çok**xlargerc** veya **staticrc80** büyük miktarlarda bellek, verilir ve bu nedenle daha az sorgularını çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-178">In contrast, users assigned too**xlargerc** or **staticrc80** are given large amounts of memory, and therefore fewer of their queries can run concurrently.</span></span>

<span data-ttu-id="19bc3-179">Varsayılan olarak, her kullanıcı hello küçük bir kaynak sınıfı üyesidir **smallrc**.</span><span class="sxs-lookup"><span data-stu-id="19bc3-179">By default, each user is a member of hello small resource class, **smallrc**.</span></span> <span data-ttu-id="19bc3-180">Merhaba yordamı `sp_addrolemember` olan tooincrease hello kaynak sınıfı, kullanılan ve `sp_droprolemember` olan toodecrease hello kaynak sınıfı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-180">hello procedure `sp_addrolemember` is used tooincrease hello resource class, and `sp_droprolemember` is used toodecrease hello resource class.</span></span> <span data-ttu-id="19bc3-181">Örneğin, bu komut loaduser hello kaynak sınıfının çok artırır**largerc**:</span><span class="sxs-lookup"><span data-stu-id="19bc3-181">For example, this command would increase hello resource class of loaduser too**largerc**:</span></span>

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a><span data-ttu-id="19bc3-182">Kaynak sınıfları getirmiyor sorguları</span><span class="sxs-lookup"><span data-stu-id="19bc3-182">Queries that do not honor resource classes</span></span>

<span data-ttu-id="19bc3-183">Birkaç daha büyük bir bellek ayırma faydalanmaz sorgu türleri vardır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-183">There are a few types of queries that do not benefit from a larger memory allocation.</span></span> <span data-ttu-id="19bc3-184">Merhaba sistem kendi kaynak sınıfı ayırma yoksayar ve her zaman bu sorgular hello küçük kaynak sınıfında yerine çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="19bc3-184">hello system ignores their resource class allocation and always run these queries in hello small resource class instead.</span></span> <span data-ttu-id="19bc3-185">Bu sorguları her zaman hello küçük kaynak sınıfında çalıştırırsanız, olduğunda eşzamanlılık yuvaları baskısı altında ve gerekli olandan daha fazla yuvaları tüketmemesidir çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19bc3-185">If these queries always run in hello small resource class, they can run when concurrency slots are under pressure and they won't consume more slots than needed.</span></span> <span data-ttu-id="19bc3-186">Bkz: [kaynak sınıf özel durumları](#query-exceptions-to-concurrency-limits) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="19bc3-186">See [Resource class exceptions](#query-exceptions-to-concurrency-limits) for more information.</span></span>

## <a name="details-on-resource-class-assignment"></a><span data-ttu-id="19bc3-187">Kaynak sınıf ataması ilgili ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="19bc3-187">Details on resource class assignment</span></span>


<span data-ttu-id="19bc3-188">Kaynak sınıfı birkaç daha fazla bilgi:</span><span class="sxs-lookup"><span data-stu-id="19bc3-188">A few more details on resource class:</span></span>

* <span data-ttu-id="19bc3-189">*Rol alter* izni gereklidir, bir kullanıcının toochange hello kaynak sınıfı.</span><span class="sxs-lookup"><span data-stu-id="19bc3-189">*Alter role* permission is required toochange hello resource class of a user.</span></span>
* <span data-ttu-id="19bc3-190">Bir kullanıcı tooone veya daha fazla hello daha yüksek kaynak sınıfları ekleyebilirsiniz, ancak dinamik kaynak sınıfları statik kaynak sınıfları önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-190">Although you can add a user tooone or more of hello higher resource classes, dynamic resource classes take precedence over static resource classes.</span></span> <span data-ttu-id="19bc3-191">Diğer bir deyişle, bir kullanıcı tooboth atanmışsa **mediumrc**(dinamik) ve **staticrc80**(statik) **mediumrc** uygulanır hello kaynak sınıfı.</span><span class="sxs-lookup"><span data-stu-id="19bc3-191">That is, if a user is assigned tooboth **mediumrc**(dynamic) and **staticrc80**(static), **mediumrc** is hello resource class that is honored.</span></span>
 * <span data-ttu-id="19bc3-192">Bir kullanıcı belirli bir kaynak sınıfı türü (birden fazla dinamik kaynak sınıfı veya birden çok statik kaynak sınıfı) bir kaynak sınıfında daha toomore atandığında, hello en yüksek kaynak sınıfı uygulanır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-192">When a user is assigned toomore than one resource class in a specific resource class type (more than one dynamic resource class or more than one static resource class), hello highest resource class is honored.</span></span> <span data-ttu-id="19bc3-193">Diğer bir deyişle, bir kullanıcı tooboth mediumrc ve largerc atanmışsa hello daha yüksek kaynak sınıfı (largerc) uygulanır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-193">That is, if a user is assigned tooboth mediumrc and largerc, hello higher resource class (largerc) is honored.</span></span> <span data-ttu-id="19bc3-194">Ve bir kullanıcı tooboth atanmışsa **staticrc20** ve **statirc80**, **staticrc80** ayardaki değil.</span><span class="sxs-lookup"><span data-stu-id="19bc3-194">And if a user is assigned tooboth **staticrc20** and **statirc80**, **staticrc80** is honored.</span></span>
* <span data-ttu-id="19bc3-195">Merhaba sistem yönetici kullanıcı Hello kaynak sınıfının değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="19bc3-195">hello resource class of hello system administrative user cannot be changed.</span></span>

<span data-ttu-id="19bc3-196">Ayrıntılı bir örnek için bkz: [değiştirme kullanıcı kaynak sınıfı örneği](#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="19bc3-196">For a detailed example, see [Changing user resource class example](#changing-user-resource-class-example).</span></span>

## <a name="memory-allocation"></a><span data-ttu-id="19bc3-197">Bellek ayırma</span><span class="sxs-lookup"><span data-stu-id="19bc3-197">Memory allocation</span></span>
<span data-ttu-id="19bc3-198">Bir kullanıcının kaynak sınıfı Artıları ve eksileri tooincreasing vardır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-198">There are pros and cons tooincreasing a user's resource class.</span></span> <span data-ttu-id="19bc3-199">Bir kullanıcı için bir kaynak sınıfı artırılması, sorgularını daha hızlı sorgu yürütebilir olduğu anlamına gelebilir erişim toomore belleği sağlar.</span><span class="sxs-lookup"><span data-stu-id="19bc3-199">Increasing a resource class for a user, gives their queries access toomore memory, which may mean queries execute faster.</span></span>  <span data-ttu-id="19bc3-200">Ancak, daha yüksek kaynak sınıfları ayrıca çalıştırabilirsiniz eş zamanlı sorguları hello sayısını azaltın.</span><span class="sxs-lookup"><span data-stu-id="19bc3-200">However, higher resource classes also reduce hello number of concurrent queries that can run.</span></span> <span data-ttu-id="19bc3-201">Büyük miktarlarda bellek tooa tek sorgu ayırma veya bellek ayırmaları, aynı anda toorun da gereken diğer sorgular vererek arasında hello dengelemeyi budur.</span><span class="sxs-lookup"><span data-stu-id="19bc3-201">This is hello trade-off between allocating large amounts of memory tooa single query or allowing other queries, which also need memory allocations, toorun concurrently.</span></span> <span data-ttu-id="19bc3-202">Bir kullanıcı bir sorgu için bellek yüksek ayırmaları verilirse, diğer kullanıcıların erişim toothat sahip olmaz aynı bellek toorun bir sorgu.</span><span class="sxs-lookup"><span data-stu-id="19bc3-202">If one user is given high allocations of memory for a query, other users will not have access toothat same memory toorun a query.</span></span>

<span data-ttu-id="19bc3-203">Aşağıdaki tablonun hello hello bellek tooeach dağıtım DWU ve kaynak sınıfı tarafından eşler.</span><span class="sxs-lookup"><span data-stu-id="19bc3-203">hello following table maps hello memory allocated tooeach distribution by DWU and resource class.</span></span>

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a><span data-ttu-id="19bc3-204">Dinamik kaynak sınıfları (MB) için dağıtım başına bellek ayırma</span><span class="sxs-lookup"><span data-stu-id="19bc3-204">Memory allocations per distribution for dynamic resource classes (MB)</span></span>
| <span data-ttu-id="19bc3-205">DWU</span><span class="sxs-lookup"><span data-stu-id="19bc3-205">DWU</span></span> | <span data-ttu-id="19bc3-206">smallrc</span><span class="sxs-lookup"><span data-stu-id="19bc3-206">smallrc</span></span> | <span data-ttu-id="19bc3-207">mediumrc</span><span class="sxs-lookup"><span data-stu-id="19bc3-207">mediumrc</span></span> | <span data-ttu-id="19bc3-208">largerc</span><span class="sxs-lookup"><span data-stu-id="19bc3-208">largerc</span></span> | <span data-ttu-id="19bc3-209">xlargerc</span><span class="sxs-lookup"><span data-stu-id="19bc3-209">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="19bc3-210">DW100</span><span class="sxs-lookup"><span data-stu-id="19bc3-210">DW100</span></span> |<span data-ttu-id="19bc3-211">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-211">100</span></span> |<span data-ttu-id="19bc3-212">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-212">100</span></span> |<span data-ttu-id="19bc3-213">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-213">200</span></span> |<span data-ttu-id="19bc3-214">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-214">400</span></span> |
| <span data-ttu-id="19bc3-215">DW200</span><span class="sxs-lookup"><span data-stu-id="19bc3-215">DW200</span></span> |<span data-ttu-id="19bc3-216">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-216">100</span></span> |<span data-ttu-id="19bc3-217">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-217">200</span></span> |<span data-ttu-id="19bc3-218">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-218">400</span></span> |<span data-ttu-id="19bc3-219">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-219">800</span></span> |
| <span data-ttu-id="19bc3-220">DW300</span><span class="sxs-lookup"><span data-stu-id="19bc3-220">DW300</span></span> |<span data-ttu-id="19bc3-221">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-221">100</span></span> |<span data-ttu-id="19bc3-222">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-222">200</span></span> |<span data-ttu-id="19bc3-223">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-223">400</span></span> |<span data-ttu-id="19bc3-224">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-224">800</span></span> |
| <span data-ttu-id="19bc3-225">DW400</span><span class="sxs-lookup"><span data-stu-id="19bc3-225">DW400</span></span> |<span data-ttu-id="19bc3-226">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-226">100</span></span> |<span data-ttu-id="19bc3-227">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-227">400</span></span> |<span data-ttu-id="19bc3-228">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-228">800</span></span> |<span data-ttu-id="19bc3-229">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-229">1,600</span></span> |
| <span data-ttu-id="19bc3-230">DW500</span><span class="sxs-lookup"><span data-stu-id="19bc3-230">DW500</span></span> |<span data-ttu-id="19bc3-231">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-231">100</span></span> |<span data-ttu-id="19bc3-232">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-232">400</span></span> |<span data-ttu-id="19bc3-233">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-233">800</span></span> |<span data-ttu-id="19bc3-234">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-234">1,600</span></span> |
| <span data-ttu-id="19bc3-235">DW600</span><span class="sxs-lookup"><span data-stu-id="19bc3-235">DW600</span></span> |<span data-ttu-id="19bc3-236">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-236">100</span></span> |<span data-ttu-id="19bc3-237">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-237">400</span></span> |<span data-ttu-id="19bc3-238">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-238">800</span></span> |<span data-ttu-id="19bc3-239">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-239">1,600</span></span> |
| <span data-ttu-id="19bc3-240">DW1000</span><span class="sxs-lookup"><span data-stu-id="19bc3-240">DW1000</span></span> |<span data-ttu-id="19bc3-241">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-241">100</span></span> |<span data-ttu-id="19bc3-242">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-242">800</span></span> |<span data-ttu-id="19bc3-243">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-243">1,600</span></span> |<span data-ttu-id="19bc3-244">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-244">3,200</span></span> |
| <span data-ttu-id="19bc3-245">DW1200</span><span class="sxs-lookup"><span data-stu-id="19bc3-245">DW1200</span></span> |<span data-ttu-id="19bc3-246">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-246">100</span></span> |<span data-ttu-id="19bc3-247">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-247">800</span></span> |<span data-ttu-id="19bc3-248">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-248">1,600</span></span> |<span data-ttu-id="19bc3-249">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-249">3,200</span></span> |
| <span data-ttu-id="19bc3-250">DW1500</span><span class="sxs-lookup"><span data-stu-id="19bc3-250">DW1500</span></span> |<span data-ttu-id="19bc3-251">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-251">100</span></span> |<span data-ttu-id="19bc3-252">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-252">800</span></span> |<span data-ttu-id="19bc3-253">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-253">1,600</span></span> |<span data-ttu-id="19bc3-254">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-254">3,200</span></span> |
| <span data-ttu-id="19bc3-255">DW2000</span><span class="sxs-lookup"><span data-stu-id="19bc3-255">DW2000</span></span> |<span data-ttu-id="19bc3-256">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-256">100</span></span> |<span data-ttu-id="19bc3-257">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-257">1,600</span></span> |<span data-ttu-id="19bc3-258">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-258">3,200</span></span> |<span data-ttu-id="19bc3-259">6,400</span><span class="sxs-lookup"><span data-stu-id="19bc3-259">6,400</span></span> |
| <span data-ttu-id="19bc3-260">DW3000</span><span class="sxs-lookup"><span data-stu-id="19bc3-260">DW3000</span></span> |<span data-ttu-id="19bc3-261">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-261">100</span></span> |<span data-ttu-id="19bc3-262">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-262">1,600</span></span> |<span data-ttu-id="19bc3-263">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-263">3,200</span></span> |<span data-ttu-id="19bc3-264">6,400</span><span class="sxs-lookup"><span data-stu-id="19bc3-264">6,400</span></span> |
| <span data-ttu-id="19bc3-265">DW6000</span><span class="sxs-lookup"><span data-stu-id="19bc3-265">DW6000</span></span> |<span data-ttu-id="19bc3-266">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-266">100</span></span> |<span data-ttu-id="19bc3-267">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-267">3,200</span></span> |<span data-ttu-id="19bc3-268">6,400</span><span class="sxs-lookup"><span data-stu-id="19bc3-268">6,400</span></span> |<span data-ttu-id="19bc3-269">12,800</span><span class="sxs-lookup"><span data-stu-id="19bc3-269">12,800</span></span> |

<span data-ttu-id="19bc3-270">Aşağıdaki tablonun hello tooeach dağıtım DWU ve statik kaynak sınıfı tarafından ayrılmış hello bellek eşler.</span><span class="sxs-lookup"><span data-stu-id="19bc3-270">hello following table maps hello memory allocated tooeach distribution by DWU and static resource class.</span></span> <span data-ttu-id="19bc3-271">Hello daha yüksek kaynak sınıfları kendi belleğe sahip Not toohonor hello genel DWU sınırları azalır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-271">Note that hello higher resource classes have their memory reduced toohonor hello global DWU limits.</span></span>

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a><span data-ttu-id="19bc3-272">Statik kaynak sınıfları (MB) için dağıtım başına bellek ayırma</span><span class="sxs-lookup"><span data-stu-id="19bc3-272">Memory allocations per distribution for static resource classes (MB)</span></span>
| <span data-ttu-id="19bc3-273">DWU</span><span class="sxs-lookup"><span data-stu-id="19bc3-273">DWU</span></span> | <span data-ttu-id="19bc3-274">staticrc10</span><span class="sxs-lookup"><span data-stu-id="19bc3-274">staticrc10</span></span> | <span data-ttu-id="19bc3-275">staticrc20</span><span class="sxs-lookup"><span data-stu-id="19bc3-275">staticrc20</span></span> | <span data-ttu-id="19bc3-276">staticrc30</span><span class="sxs-lookup"><span data-stu-id="19bc3-276">staticrc30</span></span> | <span data-ttu-id="19bc3-277">staticrc40</span><span class="sxs-lookup"><span data-stu-id="19bc3-277">staticrc40</span></span> | <span data-ttu-id="19bc3-278">staticrc50</span><span class="sxs-lookup"><span data-stu-id="19bc3-278">staticrc50</span></span> | <span data-ttu-id="19bc3-279">staticrc60</span><span class="sxs-lookup"><span data-stu-id="19bc3-279">staticrc60</span></span> | <span data-ttu-id="19bc3-280">staticrc70</span><span class="sxs-lookup"><span data-stu-id="19bc3-280">staticrc70</span></span> | <span data-ttu-id="19bc3-281">staticrc80</span><span class="sxs-lookup"><span data-stu-id="19bc3-281">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="19bc3-282">DW100</span><span class="sxs-lookup"><span data-stu-id="19bc3-282">DW100</span></span> |<span data-ttu-id="19bc3-283">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-283">100</span></span> |<span data-ttu-id="19bc3-284">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-284">200</span></span> |<span data-ttu-id="19bc3-285">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-285">400</span></span> |<span data-ttu-id="19bc3-286">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-286">400</span></span> |<span data-ttu-id="19bc3-287">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-287">400</span></span> |<span data-ttu-id="19bc3-288">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-288">400</span></span> |<span data-ttu-id="19bc3-289">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-289">400</span></span> |<span data-ttu-id="19bc3-290">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-290">400</span></span> |
| <span data-ttu-id="19bc3-291">DW200</span><span class="sxs-lookup"><span data-stu-id="19bc3-291">DW200</span></span> |<span data-ttu-id="19bc3-292">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-292">100</span></span> |<span data-ttu-id="19bc3-293">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-293">200</span></span> |<span data-ttu-id="19bc3-294">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-294">400</span></span> |<span data-ttu-id="19bc3-295">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-295">800</span></span> |<span data-ttu-id="19bc3-296">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-296">800</span></span> |<span data-ttu-id="19bc3-297">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-297">800</span></span> |<span data-ttu-id="19bc3-298">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-298">800</span></span> |<span data-ttu-id="19bc3-299">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-299">800</span></span> |
| <span data-ttu-id="19bc3-300">DW300</span><span class="sxs-lookup"><span data-stu-id="19bc3-300">DW300</span></span> |<span data-ttu-id="19bc3-301">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-301">100</span></span> |<span data-ttu-id="19bc3-302">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-302">200</span></span> |<span data-ttu-id="19bc3-303">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-303">400</span></span> |<span data-ttu-id="19bc3-304">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-304">800</span></span> |<span data-ttu-id="19bc3-305">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-305">800</span></span> |<span data-ttu-id="19bc3-306">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-306">800</span></span> |<span data-ttu-id="19bc3-307">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-307">800</span></span> |<span data-ttu-id="19bc3-308">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-308">800</span></span> |
| <span data-ttu-id="19bc3-309">DW400</span><span class="sxs-lookup"><span data-stu-id="19bc3-309">DW400</span></span> |<span data-ttu-id="19bc3-310">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-310">100</span></span> |<span data-ttu-id="19bc3-311">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-311">200</span></span> |<span data-ttu-id="19bc3-312">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-312">400</span></span> |<span data-ttu-id="19bc3-313">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-313">800</span></span> |<span data-ttu-id="19bc3-314">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-314">1,600</span></span> |<span data-ttu-id="19bc3-315">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-315">1,600</span></span> |<span data-ttu-id="19bc3-316">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-316">1,600</span></span> |<span data-ttu-id="19bc3-317">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-317">1,600</span></span> |
| <span data-ttu-id="19bc3-318">DW500</span><span class="sxs-lookup"><span data-stu-id="19bc3-318">DW500</span></span> |<span data-ttu-id="19bc3-319">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-319">100</span></span> |<span data-ttu-id="19bc3-320">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-320">200</span></span> |<span data-ttu-id="19bc3-321">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-321">400</span></span> |<span data-ttu-id="19bc3-322">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-322">800</span></span> |<span data-ttu-id="19bc3-323">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-323">1,600</span></span> |<span data-ttu-id="19bc3-324">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-324">1,600</span></span> |<span data-ttu-id="19bc3-325">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-325">1,600</span></span> |<span data-ttu-id="19bc3-326">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-326">1,600</span></span> |
| <span data-ttu-id="19bc3-327">DW600</span><span class="sxs-lookup"><span data-stu-id="19bc3-327">DW600</span></span> |<span data-ttu-id="19bc3-328">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-328">100</span></span> |<span data-ttu-id="19bc3-329">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-329">200</span></span> |<span data-ttu-id="19bc3-330">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-330">400</span></span> |<span data-ttu-id="19bc3-331">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-331">800</span></span> |<span data-ttu-id="19bc3-332">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-332">1,600</span></span> |<span data-ttu-id="19bc3-333">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-333">1,600</span></span> |<span data-ttu-id="19bc3-334">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-334">1,600</span></span> |<span data-ttu-id="19bc3-335">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-335">1,600</span></span> |
| <span data-ttu-id="19bc3-336">DW1000</span><span class="sxs-lookup"><span data-stu-id="19bc3-336">DW1000</span></span> |<span data-ttu-id="19bc3-337">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-337">100</span></span> |<span data-ttu-id="19bc3-338">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-338">200</span></span> |<span data-ttu-id="19bc3-339">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-339">400</span></span> |<span data-ttu-id="19bc3-340">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-340">800</span></span> |<span data-ttu-id="19bc3-341">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-341">1,600</span></span> |<span data-ttu-id="19bc3-342">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-342">3,200</span></span> |<span data-ttu-id="19bc3-343">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-343">3,200</span></span> |<span data-ttu-id="19bc3-344">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-344">3,200</span></span> |
| <span data-ttu-id="19bc3-345">DW1200</span><span class="sxs-lookup"><span data-stu-id="19bc3-345">DW1200</span></span> |<span data-ttu-id="19bc3-346">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-346">100</span></span> |<span data-ttu-id="19bc3-347">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-347">200</span></span> |<span data-ttu-id="19bc3-348">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-348">400</span></span> |<span data-ttu-id="19bc3-349">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-349">800</span></span> |<span data-ttu-id="19bc3-350">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-350">1,600</span></span> |<span data-ttu-id="19bc3-351">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-351">3,200</span></span> |<span data-ttu-id="19bc3-352">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-352">3,200</span></span> |<span data-ttu-id="19bc3-353">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-353">3,200</span></span> |
| <span data-ttu-id="19bc3-354">DW1500</span><span class="sxs-lookup"><span data-stu-id="19bc3-354">DW1500</span></span> |<span data-ttu-id="19bc3-355">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-355">100</span></span> |<span data-ttu-id="19bc3-356">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-356">200</span></span> |<span data-ttu-id="19bc3-357">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-357">400</span></span> |<span data-ttu-id="19bc3-358">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-358">800</span></span> |<span data-ttu-id="19bc3-359">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-359">1,600</span></span> |<span data-ttu-id="19bc3-360">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-360">3,200</span></span> |<span data-ttu-id="19bc3-361">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-361">3,200</span></span> |<span data-ttu-id="19bc3-362">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-362">3,200</span></span> |
| <span data-ttu-id="19bc3-363">DW2000</span><span class="sxs-lookup"><span data-stu-id="19bc3-363">DW2000</span></span> |<span data-ttu-id="19bc3-364">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-364">100</span></span> |<span data-ttu-id="19bc3-365">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-365">200</span></span> |<span data-ttu-id="19bc3-366">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-366">400</span></span> |<span data-ttu-id="19bc3-367">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-367">800</span></span> |<span data-ttu-id="19bc3-368">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-368">1,600</span></span> |<span data-ttu-id="19bc3-369">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-369">3,200</span></span> |<span data-ttu-id="19bc3-370">6,400</span><span class="sxs-lookup"><span data-stu-id="19bc3-370">6,400</span></span> |<span data-ttu-id="19bc3-371">6,400</span><span class="sxs-lookup"><span data-stu-id="19bc3-371">6,400</span></span> |
| <span data-ttu-id="19bc3-372">DW3000</span><span class="sxs-lookup"><span data-stu-id="19bc3-372">DW3000</span></span> |<span data-ttu-id="19bc3-373">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-373">100</span></span> |<span data-ttu-id="19bc3-374">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-374">200</span></span> |<span data-ttu-id="19bc3-375">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-375">400</span></span> |<span data-ttu-id="19bc3-376">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-376">800</span></span> |<span data-ttu-id="19bc3-377">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-377">1,600</span></span> |<span data-ttu-id="19bc3-378">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-378">3,200</span></span> |<span data-ttu-id="19bc3-379">6,400</span><span class="sxs-lookup"><span data-stu-id="19bc3-379">6,400</span></span> |<span data-ttu-id="19bc3-380">6,400</span><span class="sxs-lookup"><span data-stu-id="19bc3-380">6,400</span></span> |
| <span data-ttu-id="19bc3-381">DW6000</span><span class="sxs-lookup"><span data-stu-id="19bc3-381">DW6000</span></span> |<span data-ttu-id="19bc3-382">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-382">100</span></span> |<span data-ttu-id="19bc3-383">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-383">200</span></span> |<span data-ttu-id="19bc3-384">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-384">400</span></span> |<span data-ttu-id="19bc3-385">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-385">800</span></span> |<span data-ttu-id="19bc3-386">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-386">1,600</span></span> |<span data-ttu-id="19bc3-387">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-387">3,200</span></span> |<span data-ttu-id="19bc3-388">6,400</span><span class="sxs-lookup"><span data-stu-id="19bc3-388">6,400</span></span> |<span data-ttu-id="19bc3-389">12,800</span><span class="sxs-lookup"><span data-stu-id="19bc3-389">12,800</span></span> |

<span data-ttu-id="19bc3-390">Tablo önceki hello DW2000 hello içinde çalışan bir sorgu görebilirsiniz **xlargerc** kaynak sınıfı erişim too6, 400 MB bellek her bir hello 60 dağıtılmış veritabanı içinde sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-390">From hello preceding table, you can see that a query running on a DW2000 in hello **xlargerc** resource class would have access too6,400 MB of memory within each of hello 60 distributed databases.</span></span>  <span data-ttu-id="19bc3-391">SQL veri ambarı'nda 60 dağıtımları vardır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-391">In SQL Data Warehouse, there are 60 distributions.</span></span> <span data-ttu-id="19bc3-392">Bu nedenle, bir sorguda belirtilen kaynak sınıfı, değerleri yukarıda hello için toocalculate hello toplam bellek ayırma 60 çarpılan.</span><span class="sxs-lookup"><span data-stu-id="19bc3-392">Therefore, toocalculate hello total memory allocation for a query in a given resource class, hello above values should be multiplied by 60.</span></span>

### <a name="memory-allocations-system-wide-gb"></a><span data-ttu-id="19bc3-393">Bellek ayırma sistem genelinde (GB)</span><span class="sxs-lookup"><span data-stu-id="19bc3-393">Memory allocations system-wide (GB)</span></span>
| <span data-ttu-id="19bc3-394">DWU</span><span class="sxs-lookup"><span data-stu-id="19bc3-394">DWU</span></span> | <span data-ttu-id="19bc3-395">smallrc</span><span class="sxs-lookup"><span data-stu-id="19bc3-395">smallrc</span></span> | <span data-ttu-id="19bc3-396">mediumrc</span><span class="sxs-lookup"><span data-stu-id="19bc3-396">mediumrc</span></span> | <span data-ttu-id="19bc3-397">largerc</span><span class="sxs-lookup"><span data-stu-id="19bc3-397">largerc</span></span> | <span data-ttu-id="19bc3-398">xlargerc</span><span class="sxs-lookup"><span data-stu-id="19bc3-398">xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="19bc3-399">DW100</span><span class="sxs-lookup"><span data-stu-id="19bc3-399">DW100</span></span> |<span data-ttu-id="19bc3-400">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-400">6</span></span> |<span data-ttu-id="19bc3-401">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-401">6</span></span> |<span data-ttu-id="19bc3-402">12</span><span class="sxs-lookup"><span data-stu-id="19bc3-402">12</span></span> |<span data-ttu-id="19bc3-403">23</span><span class="sxs-lookup"><span data-stu-id="19bc3-403">23</span></span> |
| <span data-ttu-id="19bc3-404">DW200</span><span class="sxs-lookup"><span data-stu-id="19bc3-404">DW200</span></span> |<span data-ttu-id="19bc3-405">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-405">6</span></span> |<span data-ttu-id="19bc3-406">12</span><span class="sxs-lookup"><span data-stu-id="19bc3-406">12</span></span> |<span data-ttu-id="19bc3-407">23</span><span class="sxs-lookup"><span data-stu-id="19bc3-407">23</span></span> |<span data-ttu-id="19bc3-408">47</span><span class="sxs-lookup"><span data-stu-id="19bc3-408">47</span></span> |
| <span data-ttu-id="19bc3-409">DW300</span><span class="sxs-lookup"><span data-stu-id="19bc3-409">DW300</span></span> |<span data-ttu-id="19bc3-410">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-410">6</span></span> |<span data-ttu-id="19bc3-411">12</span><span class="sxs-lookup"><span data-stu-id="19bc3-411">12</span></span> |<span data-ttu-id="19bc3-412">23</span><span class="sxs-lookup"><span data-stu-id="19bc3-412">23</span></span> |<span data-ttu-id="19bc3-413">47</span><span class="sxs-lookup"><span data-stu-id="19bc3-413">47</span></span> |
| <span data-ttu-id="19bc3-414">DW400</span><span class="sxs-lookup"><span data-stu-id="19bc3-414">DW400</span></span> |<span data-ttu-id="19bc3-415">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-415">6</span></span> |<span data-ttu-id="19bc3-416">23</span><span class="sxs-lookup"><span data-stu-id="19bc3-416">23</span></span> |<span data-ttu-id="19bc3-417">47</span><span class="sxs-lookup"><span data-stu-id="19bc3-417">47</span></span> |<span data-ttu-id="19bc3-418">94</span><span class="sxs-lookup"><span data-stu-id="19bc3-418">94</span></span> |
| <span data-ttu-id="19bc3-419">DW500</span><span class="sxs-lookup"><span data-stu-id="19bc3-419">DW500</span></span> |<span data-ttu-id="19bc3-420">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-420">6</span></span> |<span data-ttu-id="19bc3-421">23</span><span class="sxs-lookup"><span data-stu-id="19bc3-421">23</span></span> |<span data-ttu-id="19bc3-422">47</span><span class="sxs-lookup"><span data-stu-id="19bc3-422">47</span></span> |<span data-ttu-id="19bc3-423">94</span><span class="sxs-lookup"><span data-stu-id="19bc3-423">94</span></span> |
| <span data-ttu-id="19bc3-424">DW600</span><span class="sxs-lookup"><span data-stu-id="19bc3-424">DW600</span></span> |<span data-ttu-id="19bc3-425">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-425">6</span></span> |<span data-ttu-id="19bc3-426">23</span><span class="sxs-lookup"><span data-stu-id="19bc3-426">23</span></span> |<span data-ttu-id="19bc3-427">47</span><span class="sxs-lookup"><span data-stu-id="19bc3-427">47</span></span> |<span data-ttu-id="19bc3-428">94</span><span class="sxs-lookup"><span data-stu-id="19bc3-428">94</span></span> |
| <span data-ttu-id="19bc3-429">DW1000</span><span class="sxs-lookup"><span data-stu-id="19bc3-429">DW1000</span></span> |<span data-ttu-id="19bc3-430">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-430">6</span></span> |<span data-ttu-id="19bc3-431">47</span><span class="sxs-lookup"><span data-stu-id="19bc3-431">47</span></span> |<span data-ttu-id="19bc3-432">94</span><span class="sxs-lookup"><span data-stu-id="19bc3-432">94</span></span> |<span data-ttu-id="19bc3-433">188</span><span class="sxs-lookup"><span data-stu-id="19bc3-433">188</span></span> |
| <span data-ttu-id="19bc3-434">DW1200</span><span class="sxs-lookup"><span data-stu-id="19bc3-434">DW1200</span></span> |<span data-ttu-id="19bc3-435">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-435">6</span></span> |<span data-ttu-id="19bc3-436">47</span><span class="sxs-lookup"><span data-stu-id="19bc3-436">47</span></span> |<span data-ttu-id="19bc3-437">94</span><span class="sxs-lookup"><span data-stu-id="19bc3-437">94</span></span> |<span data-ttu-id="19bc3-438">188</span><span class="sxs-lookup"><span data-stu-id="19bc3-438">188</span></span> |
| <span data-ttu-id="19bc3-439">DW1500</span><span class="sxs-lookup"><span data-stu-id="19bc3-439">DW1500</span></span> |<span data-ttu-id="19bc3-440">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-440">6</span></span> |<span data-ttu-id="19bc3-441">47</span><span class="sxs-lookup"><span data-stu-id="19bc3-441">47</span></span> |<span data-ttu-id="19bc3-442">94</span><span class="sxs-lookup"><span data-stu-id="19bc3-442">94</span></span> |<span data-ttu-id="19bc3-443">188</span><span class="sxs-lookup"><span data-stu-id="19bc3-443">188</span></span> |
| <span data-ttu-id="19bc3-444">DW2000</span><span class="sxs-lookup"><span data-stu-id="19bc3-444">DW2000</span></span> |<span data-ttu-id="19bc3-445">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-445">6</span></span> |<span data-ttu-id="19bc3-446">94</span><span class="sxs-lookup"><span data-stu-id="19bc3-446">94</span></span> |<span data-ttu-id="19bc3-447">188</span><span class="sxs-lookup"><span data-stu-id="19bc3-447">188</span></span> |<span data-ttu-id="19bc3-448">375</span><span class="sxs-lookup"><span data-stu-id="19bc3-448">375</span></span> |
| <span data-ttu-id="19bc3-449">DW3000</span><span class="sxs-lookup"><span data-stu-id="19bc3-449">DW3000</span></span> |<span data-ttu-id="19bc3-450">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-450">6</span></span> |<span data-ttu-id="19bc3-451">94</span><span class="sxs-lookup"><span data-stu-id="19bc3-451">94</span></span> |<span data-ttu-id="19bc3-452">188</span><span class="sxs-lookup"><span data-stu-id="19bc3-452">188</span></span> |<span data-ttu-id="19bc3-453">375</span><span class="sxs-lookup"><span data-stu-id="19bc3-453">375</span></span> |
| <span data-ttu-id="19bc3-454">DW6000</span><span class="sxs-lookup"><span data-stu-id="19bc3-454">DW6000</span></span> |<span data-ttu-id="19bc3-455">6</span><span class="sxs-lookup"><span data-stu-id="19bc3-455">6</span></span> |<span data-ttu-id="19bc3-456">188</span><span class="sxs-lookup"><span data-stu-id="19bc3-456">188</span></span> |<span data-ttu-id="19bc3-457">375</span><span class="sxs-lookup"><span data-stu-id="19bc3-457">375</span></span> |<span data-ttu-id="19bc3-458">750</span><span class="sxs-lookup"><span data-stu-id="19bc3-458">750</span></span> |

<span data-ttu-id="19bc3-459">Bu sistem genelinde bellek ayırmaları tablodan hello xlargerc kaynak sınıfında DW2000 üzerinde çalışan bir sorgu 375 GB bellek toplam ayrılır görebilirsiniz (6.400 MB * 60 dağıtımları / 1.024 tooconvert tooGB) SQL veri ambarı hello tamamen üzerinden.</span><span class="sxs-lookup"><span data-stu-id="19bc3-459">From this table of system-wide memory allocations, you can see that a query running on a DW2000 in hello xlargerc resource class is allocated a total of 375 GB of memory (6,400 MB * 60 distributions / 1,024 tooconvert tooGB) over hello entirety of your SQL Data Warehouse.</span></span>

<span data-ttu-id="19bc3-460">Merhaba aynı hesaplama toostatic kaynak sınıfları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-460">hello same calculation applies toostatic resource classes.</span></span>
 
## <a name="concurrency-slot-consumption"></a><span data-ttu-id="19bc3-461">Eşzamanlılık yuvası tüketim</span><span class="sxs-lookup"><span data-stu-id="19bc3-461">Concurrency slot consumption</span></span>  
<span data-ttu-id="19bc3-462">SQL veri ambarını daha yüksek kaynak sınıflarda çalıştıran daha fazla bellek tooqueries verir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-462">SQL Data Warehouse grants more memory tooqueries running in higher resource classes.</span></span> <span data-ttu-id="19bc3-463">Bellek sabit bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-463">Memory is a fixed resource.</span></span>  <span data-ttu-id="19bc3-464">Bu nedenle, daha az sayıda eşzamanlı sorgu yürütebilir hello sorgu daha fazla bellek tahsis hello.</span><span class="sxs-lookup"><span data-stu-id="19bc3-464">Therefore, hello more memory allocated per query, hello fewer concurrent queries can execute.</span></span> <span data-ttu-id="19bc3-465">Merhaba aşağıdaki tabloda tüm DWU tarafından kullanılabilir eşzamanlılık yuvaları ve her kaynak sınıfı tarafından tüketilen hello yuvaları hello sayısını gösterir tek bir görünümde hello önceki kavramlarını reiterates.</span><span class="sxs-lookup"><span data-stu-id="19bc3-465">hello following table reiterates all of hello previous concepts in a single view that shows hello number of concurrency slots available by DWU and hello slots consumed by each resource class.</span></span>  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a><span data-ttu-id="19bc3-466">Ayırma ve dinamik kaynak sınıfları için eşzamanlılık yuva tüketim</span><span class="sxs-lookup"><span data-stu-id="19bc3-466">Allocation and consumption of concurrency slots for dynamic resource classes</span></span>  
| <span data-ttu-id="19bc3-467">DWU</span><span class="sxs-lookup"><span data-stu-id="19bc3-467">DWU</span></span> | <span data-ttu-id="19bc3-468">En fazla eş zamanlı sorgular</span><span class="sxs-lookup"><span data-stu-id="19bc3-468">Maximum concurrent queries</span></span> | <span data-ttu-id="19bc3-469">Ayrılmış eşzamanlılık yuvaları</span><span class="sxs-lookup"><span data-stu-id="19bc3-469">Concurrency slots allocated</span></span> | <span data-ttu-id="19bc3-470">Smallrc tarafından kullanılan yuvaları</span><span class="sxs-lookup"><span data-stu-id="19bc3-470">Slots used by smallrc</span></span> | <span data-ttu-id="19bc3-471">Mediumrc tarafından kullanılan yuvaları</span><span class="sxs-lookup"><span data-stu-id="19bc3-471">Slots used by mediumrc</span></span> | <span data-ttu-id="19bc3-472">Largerc tarafından kullanılan yuvaları</span><span class="sxs-lookup"><span data-stu-id="19bc3-472">Slots used by largerc</span></span> | <span data-ttu-id="19bc3-473">Xlargerc tarafından kullanılan yuvaları</span><span class="sxs-lookup"><span data-stu-id="19bc3-473">Slots used by xlargerc</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="19bc3-474">DW100</span><span class="sxs-lookup"><span data-stu-id="19bc3-474">DW100</span></span> |<span data-ttu-id="19bc3-475">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-475">4</span></span> |<span data-ttu-id="19bc3-476">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-476">4</span></span> |<span data-ttu-id="19bc3-477">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-477">1</span></span> |<span data-ttu-id="19bc3-478">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-478">1</span></span> |<span data-ttu-id="19bc3-479">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-479">2</span></span> |<span data-ttu-id="19bc3-480">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-480">4</span></span> |
| <span data-ttu-id="19bc3-481">DW200</span><span class="sxs-lookup"><span data-stu-id="19bc3-481">DW200</span></span> |<span data-ttu-id="19bc3-482">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-482">8</span></span> |<span data-ttu-id="19bc3-483">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-483">8</span></span> |<span data-ttu-id="19bc3-484">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-484">1</span></span> |<span data-ttu-id="19bc3-485">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-485">2</span></span> |<span data-ttu-id="19bc3-486">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-486">4</span></span> |<span data-ttu-id="19bc3-487">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-487">8</span></span> |
| <span data-ttu-id="19bc3-488">DW300</span><span class="sxs-lookup"><span data-stu-id="19bc3-488">DW300</span></span> |<span data-ttu-id="19bc3-489">12</span><span class="sxs-lookup"><span data-stu-id="19bc3-489">12</span></span> |<span data-ttu-id="19bc3-490">12</span><span class="sxs-lookup"><span data-stu-id="19bc3-490">12</span></span> |<span data-ttu-id="19bc3-491">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-491">1</span></span> |<span data-ttu-id="19bc3-492">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-492">2</span></span> |<span data-ttu-id="19bc3-493">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-493">4</span></span> |<span data-ttu-id="19bc3-494">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-494">8</span></span> |
| <span data-ttu-id="19bc3-495">DW400</span><span class="sxs-lookup"><span data-stu-id="19bc3-495">DW400</span></span> |<span data-ttu-id="19bc3-496">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-496">16</span></span> |<span data-ttu-id="19bc3-497">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-497">16</span></span> |<span data-ttu-id="19bc3-498">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-498">1</span></span> |<span data-ttu-id="19bc3-499">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-499">4</span></span> |<span data-ttu-id="19bc3-500">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-500">8</span></span> |<span data-ttu-id="19bc3-501">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-501">16</span></span> |
| <span data-ttu-id="19bc3-502">DW500</span><span class="sxs-lookup"><span data-stu-id="19bc3-502">DW500</span></span> |<span data-ttu-id="19bc3-503">20</span><span class="sxs-lookup"><span data-stu-id="19bc3-503">20</span></span> |<span data-ttu-id="19bc3-504">20</span><span class="sxs-lookup"><span data-stu-id="19bc3-504">20</span></span> |<span data-ttu-id="19bc3-505">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-505">1</span></span> |<span data-ttu-id="19bc3-506">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-506">4</span></span> |<span data-ttu-id="19bc3-507">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-507">8</span></span> |<span data-ttu-id="19bc3-508">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-508">16</span></span> |
| <span data-ttu-id="19bc3-509">DW600</span><span class="sxs-lookup"><span data-stu-id="19bc3-509">DW600</span></span> |<span data-ttu-id="19bc3-510">24</span><span class="sxs-lookup"><span data-stu-id="19bc3-510">24</span></span> |<span data-ttu-id="19bc3-511">24</span><span class="sxs-lookup"><span data-stu-id="19bc3-511">24</span></span> |<span data-ttu-id="19bc3-512">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-512">1</span></span> |<span data-ttu-id="19bc3-513">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-513">4</span></span> |<span data-ttu-id="19bc3-514">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-514">8</span></span> |<span data-ttu-id="19bc3-515">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-515">16</span></span> |
| <span data-ttu-id="19bc3-516">DW1000</span><span class="sxs-lookup"><span data-stu-id="19bc3-516">DW1000</span></span> |<span data-ttu-id="19bc3-517">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-517">32</span></span> |<span data-ttu-id="19bc3-518">40</span><span class="sxs-lookup"><span data-stu-id="19bc3-518">40</span></span> |<span data-ttu-id="19bc3-519">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-519">1</span></span> |<span data-ttu-id="19bc3-520">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-520">8</span></span> |<span data-ttu-id="19bc3-521">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-521">16</span></span> |<span data-ttu-id="19bc3-522">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-522">32</span></span> |
| <span data-ttu-id="19bc3-523">DW1200</span><span class="sxs-lookup"><span data-stu-id="19bc3-523">DW1200</span></span> |<span data-ttu-id="19bc3-524">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-524">32</span></span> |<span data-ttu-id="19bc3-525">48</span><span class="sxs-lookup"><span data-stu-id="19bc3-525">48</span></span> |<span data-ttu-id="19bc3-526">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-526">1</span></span> |<span data-ttu-id="19bc3-527">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-527">8</span></span> |<span data-ttu-id="19bc3-528">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-528">16</span></span> |<span data-ttu-id="19bc3-529">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-529">32</span></span> |
| <span data-ttu-id="19bc3-530">DW1500</span><span class="sxs-lookup"><span data-stu-id="19bc3-530">DW1500</span></span> |<span data-ttu-id="19bc3-531">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-531">32</span></span> |<span data-ttu-id="19bc3-532">60</span><span class="sxs-lookup"><span data-stu-id="19bc3-532">60</span></span> |<span data-ttu-id="19bc3-533">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-533">1</span></span> |<span data-ttu-id="19bc3-534">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-534">8</span></span> |<span data-ttu-id="19bc3-535">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-535">16</span></span> |<span data-ttu-id="19bc3-536">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-536">32</span></span> |
| <span data-ttu-id="19bc3-537">DW2000</span><span class="sxs-lookup"><span data-stu-id="19bc3-537">DW2000</span></span> |<span data-ttu-id="19bc3-538">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-538">32</span></span> |<span data-ttu-id="19bc3-539">80</span><span class="sxs-lookup"><span data-stu-id="19bc3-539">80</span></span> |<span data-ttu-id="19bc3-540">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-540">1</span></span> |<span data-ttu-id="19bc3-541">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-541">16</span></span> |<span data-ttu-id="19bc3-542">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-542">32</span></span> |<span data-ttu-id="19bc3-543">64</span><span class="sxs-lookup"><span data-stu-id="19bc3-543">64</span></span> |
| <span data-ttu-id="19bc3-544">DW3000</span><span class="sxs-lookup"><span data-stu-id="19bc3-544">DW3000</span></span> |<span data-ttu-id="19bc3-545">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-545">32</span></span> |<span data-ttu-id="19bc3-546">120</span><span class="sxs-lookup"><span data-stu-id="19bc3-546">120</span></span> |<span data-ttu-id="19bc3-547">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-547">1</span></span> |<span data-ttu-id="19bc3-548">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-548">16</span></span> |<span data-ttu-id="19bc3-549">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-549">32</span></span> |<span data-ttu-id="19bc3-550">64</span><span class="sxs-lookup"><span data-stu-id="19bc3-550">64</span></span> |
| <span data-ttu-id="19bc3-551">DW6000</span><span class="sxs-lookup"><span data-stu-id="19bc3-551">DW6000</span></span> |<span data-ttu-id="19bc3-552">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-552">32</span></span> |<span data-ttu-id="19bc3-553">240</span><span class="sxs-lookup"><span data-stu-id="19bc3-553">240</span></span> |<span data-ttu-id="19bc3-554">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-554">1</span></span> |<span data-ttu-id="19bc3-555">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-555">32</span></span> |<span data-ttu-id="19bc3-556">64</span><span class="sxs-lookup"><span data-stu-id="19bc3-556">64</span></span> |<span data-ttu-id="19bc3-557">128</span><span class="sxs-lookup"><span data-stu-id="19bc3-557">128</span></span> |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a><span data-ttu-id="19bc3-558">Ayırma ve statik kaynak sınıfları için eşzamanlılık yuva tüketim</span><span class="sxs-lookup"><span data-stu-id="19bc3-558">Allocation and consumption of concurrency slots for static resource classes</span></span>  
| <span data-ttu-id="19bc3-559">DWU</span><span class="sxs-lookup"><span data-stu-id="19bc3-559">DWU</span></span> | <span data-ttu-id="19bc3-560">En fazla eş zamanlı sorgular</span><span class="sxs-lookup"><span data-stu-id="19bc3-560">Maximum concurrent queries</span></span> | <span data-ttu-id="19bc3-561">Ayrılmış eşzamanlılık yuvaları</span><span class="sxs-lookup"><span data-stu-id="19bc3-561">Concurrency slots allocated</span></span> |<span data-ttu-id="19bc3-562">staticrc10</span><span class="sxs-lookup"><span data-stu-id="19bc3-562">staticrc10</span></span> | <span data-ttu-id="19bc3-563">staticrc20</span><span class="sxs-lookup"><span data-stu-id="19bc3-563">staticrc20</span></span> | <span data-ttu-id="19bc3-564">staticrc30</span><span class="sxs-lookup"><span data-stu-id="19bc3-564">staticrc30</span></span> | <span data-ttu-id="19bc3-565">staticrc40</span><span class="sxs-lookup"><span data-stu-id="19bc3-565">staticrc40</span></span> | <span data-ttu-id="19bc3-566">staticrc50</span><span class="sxs-lookup"><span data-stu-id="19bc3-566">staticrc50</span></span> | <span data-ttu-id="19bc3-567">staticrc60</span><span class="sxs-lookup"><span data-stu-id="19bc3-567">staticrc60</span></span> | <span data-ttu-id="19bc3-568">staticrc70</span><span class="sxs-lookup"><span data-stu-id="19bc3-568">staticrc70</span></span> | <span data-ttu-id="19bc3-569">staticrc80</span><span class="sxs-lookup"><span data-stu-id="19bc3-569">staticrc80</span></span> |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="19bc3-570">DW100</span><span class="sxs-lookup"><span data-stu-id="19bc3-570">DW100</span></span> |<span data-ttu-id="19bc3-571">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-571">4</span></span> |<span data-ttu-id="19bc3-572">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-572">4</span></span> |<span data-ttu-id="19bc3-573">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-573">1</span></span> |<span data-ttu-id="19bc3-574">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-574">2</span></span> |<span data-ttu-id="19bc3-575">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-575">4</span></span> |<span data-ttu-id="19bc3-576">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-576">4</span></span> |<span data-ttu-id="19bc3-577">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-577">4</span></span> |<span data-ttu-id="19bc3-578">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-578">4</span></span> |<span data-ttu-id="19bc3-579">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-579">4</span></span> |<span data-ttu-id="19bc3-580">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-580">4</span></span> |
| <span data-ttu-id="19bc3-581">DW200</span><span class="sxs-lookup"><span data-stu-id="19bc3-581">DW200</span></span> |<span data-ttu-id="19bc3-582">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-582">8</span></span> |<span data-ttu-id="19bc3-583">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-583">8</span></span> |<span data-ttu-id="19bc3-584">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-584">1</span></span> |<span data-ttu-id="19bc3-585">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-585">2</span></span> |<span data-ttu-id="19bc3-586">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-586">4</span></span> |<span data-ttu-id="19bc3-587">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-587">8</span></span> |<span data-ttu-id="19bc3-588">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-588">8</span></span> |<span data-ttu-id="19bc3-589">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-589">8</span></span> |<span data-ttu-id="19bc3-590">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-590">8</span></span> |<span data-ttu-id="19bc3-591">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-591">8</span></span> |
| <span data-ttu-id="19bc3-592">DW300</span><span class="sxs-lookup"><span data-stu-id="19bc3-592">DW300</span></span> |<span data-ttu-id="19bc3-593">12</span><span class="sxs-lookup"><span data-stu-id="19bc3-593">12</span></span> |<span data-ttu-id="19bc3-594">12</span><span class="sxs-lookup"><span data-stu-id="19bc3-594">12</span></span> |<span data-ttu-id="19bc3-595">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-595">1</span></span> |<span data-ttu-id="19bc3-596">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-596">2</span></span> |<span data-ttu-id="19bc3-597">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-597">4</span></span> |<span data-ttu-id="19bc3-598">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-598">8</span></span> |<span data-ttu-id="19bc3-599">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-599">8</span></span> |<span data-ttu-id="19bc3-600">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-600">8</span></span> |<span data-ttu-id="19bc3-601">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-601">8</span></span> |<span data-ttu-id="19bc3-602">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-602">8</span></span> |
| <span data-ttu-id="19bc3-603">DW400</span><span class="sxs-lookup"><span data-stu-id="19bc3-603">DW400</span></span> |<span data-ttu-id="19bc3-604">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-604">16</span></span> |<span data-ttu-id="19bc3-605">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-605">16</span></span> |<span data-ttu-id="19bc3-606">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-606">1</span></span> |<span data-ttu-id="19bc3-607">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-607">2</span></span> |<span data-ttu-id="19bc3-608">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-608">4</span></span> |<span data-ttu-id="19bc3-609">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-609">8</span></span> |<span data-ttu-id="19bc3-610">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-610">16</span></span> |<span data-ttu-id="19bc3-611">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-611">16</span></span> |<span data-ttu-id="19bc3-612">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-612">16</span></span> |<span data-ttu-id="19bc3-613">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-613">16</span></span> |
| <span data-ttu-id="19bc3-614">DW500</span><span class="sxs-lookup"><span data-stu-id="19bc3-614">DW500</span></span> | <span data-ttu-id="19bc3-615">20</span><span class="sxs-lookup"><span data-stu-id="19bc3-615">20</span></span>| <span data-ttu-id="19bc3-616">20</span><span class="sxs-lookup"><span data-stu-id="19bc3-616">20</span></span>| <span data-ttu-id="19bc3-617">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-617">1</span></span>| <span data-ttu-id="19bc3-618">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-618">2</span></span>| <span data-ttu-id="19bc3-619">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-619">4</span></span>| <span data-ttu-id="19bc3-620">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-620">8</span></span>| <span data-ttu-id="19bc3-621">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-621">16</span></span>| <span data-ttu-id="19bc3-622">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-622">16</span></span>| <span data-ttu-id="19bc3-623">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-623">16</span></span>| <span data-ttu-id="19bc3-624">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-624">16</span></span>|
| <span data-ttu-id="19bc3-625">DW600</span><span class="sxs-lookup"><span data-stu-id="19bc3-625">DW600</span></span> | <span data-ttu-id="19bc3-626">24</span><span class="sxs-lookup"><span data-stu-id="19bc3-626">24</span></span>| <span data-ttu-id="19bc3-627">24</span><span class="sxs-lookup"><span data-stu-id="19bc3-627">24</span></span>| <span data-ttu-id="19bc3-628">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-628">1</span></span>| <span data-ttu-id="19bc3-629">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-629">2</span></span>| <span data-ttu-id="19bc3-630">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-630">4</span></span>| <span data-ttu-id="19bc3-631">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-631">8</span></span>| <span data-ttu-id="19bc3-632">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-632">16</span></span>| <span data-ttu-id="19bc3-633">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-633">16</span></span>| <span data-ttu-id="19bc3-634">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-634">16</span></span>| <span data-ttu-id="19bc3-635">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-635">16</span></span>|
| <span data-ttu-id="19bc3-636">DW1000</span><span class="sxs-lookup"><span data-stu-id="19bc3-636">DW1000</span></span> | <span data-ttu-id="19bc3-637">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-637">32</span></span>| <span data-ttu-id="19bc3-638">40</span><span class="sxs-lookup"><span data-stu-id="19bc3-638">40</span></span>| <span data-ttu-id="19bc3-639">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-639">1</span></span>| <span data-ttu-id="19bc3-640">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-640">2</span></span>| <span data-ttu-id="19bc3-641">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-641">4</span></span>| <span data-ttu-id="19bc3-642">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-642">8</span></span>| <span data-ttu-id="19bc3-643">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-643">16</span></span>| <span data-ttu-id="19bc3-644">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-644">32</span></span>| <span data-ttu-id="19bc3-645">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-645">32</span></span>| <span data-ttu-id="19bc3-646">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-646">32</span></span>|
| <span data-ttu-id="19bc3-647">DW1200</span><span class="sxs-lookup"><span data-stu-id="19bc3-647">DW1200</span></span> | <span data-ttu-id="19bc3-648">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-648">32</span></span>| <span data-ttu-id="19bc3-649">48</span><span class="sxs-lookup"><span data-stu-id="19bc3-649">48</span></span>| <span data-ttu-id="19bc3-650">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-650">1</span></span>| <span data-ttu-id="19bc3-651">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-651">2</span></span>| <span data-ttu-id="19bc3-652">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-652">4</span></span>| <span data-ttu-id="19bc3-653">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-653">8</span></span>| <span data-ttu-id="19bc3-654">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-654">16</span></span>| <span data-ttu-id="19bc3-655">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-655">32</span></span>| <span data-ttu-id="19bc3-656">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-656">32</span></span>| <span data-ttu-id="19bc3-657">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-657">32</span></span>|
| <span data-ttu-id="19bc3-658">DW1500</span><span class="sxs-lookup"><span data-stu-id="19bc3-658">DW1500</span></span> | <span data-ttu-id="19bc3-659">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-659">32</span></span>| <span data-ttu-id="19bc3-660">60</span><span class="sxs-lookup"><span data-stu-id="19bc3-660">60</span></span>| <span data-ttu-id="19bc3-661">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-661">1</span></span>| <span data-ttu-id="19bc3-662">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-662">2</span></span>| <span data-ttu-id="19bc3-663">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-663">4</span></span>| <span data-ttu-id="19bc3-664">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-664">8</span></span>| <span data-ttu-id="19bc3-665">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-665">16</span></span>| <span data-ttu-id="19bc3-666">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-666">32</span></span>| <span data-ttu-id="19bc3-667">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-667">32</span></span>| <span data-ttu-id="19bc3-668">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-668">32</span></span>|
| <span data-ttu-id="19bc3-669">DW2000</span><span class="sxs-lookup"><span data-stu-id="19bc3-669">DW2000</span></span> | <span data-ttu-id="19bc3-670">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-670">32</span></span>| <span data-ttu-id="19bc3-671">80</span><span class="sxs-lookup"><span data-stu-id="19bc3-671">80</span></span>| <span data-ttu-id="19bc3-672">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-672">1</span></span>| <span data-ttu-id="19bc3-673">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-673">2</span></span>| <span data-ttu-id="19bc3-674">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-674">4</span></span>| <span data-ttu-id="19bc3-675">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-675">8</span></span>| <span data-ttu-id="19bc3-676">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-676">16</span></span>| <span data-ttu-id="19bc3-677">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-677">32</span></span>| <span data-ttu-id="19bc3-678">64</span><span class="sxs-lookup"><span data-stu-id="19bc3-678">64</span></span>| <span data-ttu-id="19bc3-679">64</span><span class="sxs-lookup"><span data-stu-id="19bc3-679">64</span></span>|
| <span data-ttu-id="19bc3-680">DW3000</span><span class="sxs-lookup"><span data-stu-id="19bc3-680">DW3000</span></span> | <span data-ttu-id="19bc3-681">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-681">32</span></span>| <span data-ttu-id="19bc3-682">120</span><span class="sxs-lookup"><span data-stu-id="19bc3-682">120</span></span>| <span data-ttu-id="19bc3-683">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-683">1</span></span>| <span data-ttu-id="19bc3-684">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-684">2</span></span>| <span data-ttu-id="19bc3-685">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-685">4</span></span>| <span data-ttu-id="19bc3-686">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-686">8</span></span>| <span data-ttu-id="19bc3-687">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-687">16</span></span>| <span data-ttu-id="19bc3-688">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-688">32</span></span>| <span data-ttu-id="19bc3-689">64</span><span class="sxs-lookup"><span data-stu-id="19bc3-689">64</span></span>| <span data-ttu-id="19bc3-690">64</span><span class="sxs-lookup"><span data-stu-id="19bc3-690">64</span></span>|
| <span data-ttu-id="19bc3-691">DW6000</span><span class="sxs-lookup"><span data-stu-id="19bc3-691">DW6000</span></span> | <span data-ttu-id="19bc3-692">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-692">32</span></span>| <span data-ttu-id="19bc3-693">240</span><span class="sxs-lookup"><span data-stu-id="19bc3-693">240</span></span>| <span data-ttu-id="19bc3-694">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-694">1</span></span>| <span data-ttu-id="19bc3-695">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-695">2</span></span>| <span data-ttu-id="19bc3-696">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-696">4</span></span>| <span data-ttu-id="19bc3-697">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-697">8</span></span>| <span data-ttu-id="19bc3-698">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-698">16</span></span>| <span data-ttu-id="19bc3-699">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-699">32</span></span>| <span data-ttu-id="19bc3-700">64</span><span class="sxs-lookup"><span data-stu-id="19bc3-700">64</span></span>| <span data-ttu-id="19bc3-701">128</span><span class="sxs-lookup"><span data-stu-id="19bc3-701">128</span></span>|

<span data-ttu-id="19bc3-702">Bu tablodan en fazla 32 eş zamanlı sorgular ve 40 eşzamanlılık yuvaları toplam DW1000 ayırır gibi SQL veri ambarı çalıştıran görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19bc3-702">From these tables, you can see that SQL Data Warehouse running as DW1000 allocates a maximum of 32 concurrent queries and a total of 40 concurrency slots.</span></span> <span data-ttu-id="19bc3-703">Tüm kullanıcılar smallrc çalıştırıyorsanız, her sorgu 1 eşzamanlılık yuva kullanılmasına neden olur olduğundan 32 eş zamanlı sorguları izin.</span><span class="sxs-lookup"><span data-stu-id="19bc3-703">If all users are running in smallrc, 32 concurrent queries would be allowed because each query would consume 1 concurrency slot.</span></span> <span data-ttu-id="19bc3-704">Tüm kullanıcılar bir DW1000 mediumrc içinde çalışmakta olan, her sorgu 47 GB sorgu başına bir toplam bellek ayırma için dağıtım başına 800 MB ayrılması ve eşzamanlılık sınırlı too5 kullanıcılar olacaktır (40 eşzamanlılık yuvaları / 8 yuvası mediumrc kullanıcı başına).</span><span class="sxs-lookup"><span data-stu-id="19bc3-704">If all users on a DW1000 were running in mediumrc, each query would be allocated 800 MB per distribution for a total memory allocation of 47 GB per query, and concurrency would be limited too5 users (40 concurrency slots / 8 slots per mediumrc user).</span></span>

## <a name="selecting-proper-resource-class"></a><span data-ttu-id="19bc3-705">Doğru kaynak sınıfını seçme</span><span class="sxs-lookup"><span data-stu-id="19bc3-705">Selecting proper resource class</span></span>  
<span data-ttu-id="19bc3-706">İyi bir uygulama, kendi kaynak sınıflarını değiştirmek yerine toopermanently Ata kullanıcıları tooa kaynak sınıfının olur.</span><span class="sxs-lookup"><span data-stu-id="19bc3-706">A good practice is toopermanently assign users tooa resource class rather than changing their resource classes.</span></span> <span data-ttu-id="19bc3-707">Örneğin, yükleri tooclustered columnstore tabloları daha fazla bellek tahsis zaman daha yüksek kaliteli dizinler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="19bc3-707">For example, loads tooclustered columnstore tables create higher-quality indexes when allocated more memory.</span></span> <span data-ttu-id="19bc3-708">yükleri erişim toohigher belleğe sahip, özellikle verileri yüklemek için bir kullanıcı oluşturun ve kalıcı olarak bu kullanıcı tooa daha yüksek kaynak sınıfı atamanız tooensure.</span><span class="sxs-lookup"><span data-stu-id="19bc3-708">tooensure that loads have access toohigher memory, create a user specifically for loading data and permanently assign this user tooa higher resource class.</span></span>
<span data-ttu-id="19bc3-709">En iyi yöntemler toofollow burada birkaç vardır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-709">There are a couple of best practices toofollow here.</span></span> <span data-ttu-id="19bc3-710">Yukarıda belirtildiği gibi SQL DW iki tür kaynak sınıfı türlerini destekler: statik kaynak sınıfları ve dinamik kaynak sınıfları.</span><span class="sxs-lookup"><span data-stu-id="19bc3-710">As mentioned above, SQL DW supports two kinds of resource class types: static resource classes and dynamic resource classes.</span></span>
### <a name="loading-best-practices"></a><span data-ttu-id="19bc3-711">En iyi uygulamaları yükleme</span><span class="sxs-lookup"><span data-stu-id="19bc3-711">Loading best practices</span></span>
1.  <span data-ttu-id="19bc3-712">Merhaba beklentilerini normal veri miktarı ile yükleri varsa, statik kaynak sınıfı iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-712">If hello expectations are loads with regular amount of data, a static resource class is a good choice.</span></span> <span data-ttu-id="19bc3-713">Daha sonra tooget ölçeklendirme daha fazla hesaplama gücüne, hello veri ambarı okuyamayacak zaman toorun daha fazla eşzamanlı out-of--box, hello yük kullanıcı daha fazla bellek tüketmesine değil olarak sorgular.</span><span class="sxs-lookup"><span data-stu-id="19bc3-713">Later, when scaling up tooget more computational power, hello data warehouse will be able toorun more concurrent queries out-of-the-box, as hello load user does not consume more memory.</span></span>
2.  <span data-ttu-id="19bc3-714">Merhaba beklentilerini bazı durumlar büyük yükleri varsa, dinamik kaynak sınıfı iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-714">If hello expectations are bigger loads in some occasions, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="19bc3-715">Daha sonra daha fazla hesaplama gücüne tooget ölçekleme sırasında hello yük kullanıcı daha fazla bellek out-of--box, bu nedenle hello yük tooperform daha hızlı izin alır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-715">Later, when scaling up tooget more computational power, hello load user will get more memory out-of-the-box, hence allowing hello load tooperform faster.</span></span>

<span data-ttu-id="19bc3-716">Merhaba ihtiyaç duyulan bellek tooprocess yüklerini verimli bir şekilde bağlıdır hello tablo yüklenen ve işlenen veri miktarı hello üzerinde hello yapısı.</span><span class="sxs-lookup"><span data-stu-id="19bc3-716">hello memory needed tooprocess loads efficiently depends on hello nature of hello table loaded and hello amount of data processed.</span></span> <span data-ttu-id="19bc3-717">Örneğin, CCI tablolara veri yükleniyor bazı bellek toolet CCI rowgroups en iyi hale getirme ulaşmak gerektirir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-717">For instance, loading data into CCI tables requires some memory toolet CCI rowgroups reach optimality.</span></span> <span data-ttu-id="19bc3-718">Daha fazla ayrıntı için hello Columnstore dizinleri - veri kılavuzu yükleme bakın.</span><span class="sxs-lookup"><span data-stu-id="19bc3-718">For more details, see hello Columnstore indexes - data loading guidance.</span></span>

<span data-ttu-id="19bc3-719">En iyi uygulama, biz toouse tutumunuzu en az 200MB bellek yükler için.</span><span class="sxs-lookup"><span data-stu-id="19bc3-719">As a best practice, we advise you toouse at least 200MB of memory for loads.</span></span>

### <a name="querying-best-practices"></a><span data-ttu-id="19bc3-720">En iyi yöntemler sorgulama</span><span class="sxs-lookup"><span data-stu-id="19bc3-720">Querying best practices</span></span>
<span data-ttu-id="19bc3-721">Sorguları kendi karmaşıklığına bağlı olarak farklı gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-721">Queries have different requirements depending on their complexity.</span></span> <span data-ttu-id="19bc3-722">Sorgu başına bellek artırma veya hello eşzamanlılık artırmayı olan hem de geçerli yolları tooaugment hello sorgu gereksinimlerine bağlı olarak genel üretilen işi.</span><span class="sxs-lookup"><span data-stu-id="19bc3-722">Increasing memory per query or increasing hello concurrency are both valid ways tooaugment overall throughput depending on hello query needs.</span></span>
1.  <span data-ttu-id="19bc3-723">Merhaba beklentilerini normal, karmaşık sorgular varsa (örneğin, toogenerate günlük ve haftalık raporları) ve gerek kalmaz eşzamanlılık tootake avantajı, dinamik kaynak sınıfı iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-723">If hello expectations are regular, complex queries (for instance, toogenerate daily and weekly reports) and do not need tootake advantage of concurrency, a dynamic resource class is a good choice.</span></span> <span data-ttu-id="19bc3-724">Merhaba sistemi daha fazla veri tooprocess varsa, hello veri ambarını ölçeklendirme bu nedenle otomatik olarak hello sorgusu çalıştırarak daha fazla bellek toohello kullanıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="19bc3-724">If hello system has more data tooprocess, scaling up hello data warehouse will therefore automatically provide more memory toohello user running hello query.</span></span>
2.  <span data-ttu-id="19bc3-725">Hello beklentilerini değişkeni ya da diurnal eşzamanlılık desenleri varsa (örneği için hello veritabanı web UI kapsamlı erişilebilir sorgulanan varsa), bir statik kaynak sınıf iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-725">If hello expectations are variable or diurnal concurrency patterns (for instance if hello database is queried through a web UI broadly accessible), a static resource class is a good choice.</span></span> <span data-ttu-id="19bc3-726">Daha sonra toodata ambarı ölçeklendirme sonra hello statik kaynak sınıfıyla ilişkili hello kullanıcı otomatik olarak gerçekleşecek daha fazla eşzamanlı sorguları mümkün toorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-726">Later, when scaling up toodata warehouse, hello user associated with hello static resource class will automatically be able toorun more concurrent queries.</span></span>

<span data-ttu-id="19bc3-727">Sorgunuzu hello ihtiyacına bağlı olarak seçilmesi uygun bellek ataması Önemsiz olmayan, aynıdır hello sorgulanan, veri miktarı gibi birçok faktöre hello tablo şemalarını ve çeşitli birleştirme, seçim ve Grup koşulları hello yapısına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-727">Selecting proper memory grant depending on hello need of your query is non-trivial, as it depends on many factors, such as hello amount of data queried, hello nature of hello table schemas, and various join, selection, and group predicates.</span></span> <span data-ttu-id="19bc3-728">Genel açısından daha fazla bellek ayırma sorguları toocomplete daha hızlı izin verir, ancak azaltmak Genel eşzamanlılık hello.</span><span class="sxs-lookup"><span data-stu-id="19bc3-728">From a general standpoint, allocating more memory will allow queries toocomplete faster, but would reduce hello overall concurrency.</span></span> <span data-ttu-id="19bc3-729">Eşzamanlılık sorunu değilse, aşırı bellek ayırma zarar değil.</span><span class="sxs-lookup"><span data-stu-id="19bc3-729">If concurrency is not an issue, over-allocating memory does not harm.</span></span> <span data-ttu-id="19bc3-730">toofine ayarlama verimlilik, kaynak sınıflarının çeşitli özellikleri çalışırken gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-730">toofine-tune throughput, trying various flavors of resource classes may be required.</span></span>

<span data-ttu-id="19bc3-731">Depolanan hello aşağıdakileri kullanabilirsiniz yordamı toofigure verilen SLO ve hello en yakın iyi kaynak için bir sınıf bellek yoğun CCI tablosu üzerinde işlem bölümlenmemiş CCI belirtilen kaynak sınıfı, kaynak sınıfı başına eşzamanlılık ve bellek verme çıkışı:</span><span class="sxs-lookup"><span data-stu-id="19bc3-731">You can use hello following stored procedure toofigure out concurrency and memory grant per resource class at a given SLO and hello closest best resource class for memory intensive CCI operations on non-partitioned CCI table at a given resource class:</span></span>

#### <a name="description"></a><span data-ttu-id="19bc3-732">Açıklama:</span><span class="sxs-lookup"><span data-stu-id="19bc3-732">Description:</span></span>  
<span data-ttu-id="19bc3-733">Bu saklı yordam hello amacı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="19bc3-733">Here's hello purpose of this stored procedure:</span></span>  
1. <span data-ttu-id="19bc3-734">toohelp kullanıcı şekil verilen SLO kaynak sınıfı başına eşzamanlılık ve bellek verme çıkışı.</span><span class="sxs-lookup"><span data-stu-id="19bc3-734">toohelp user figure out concurrency and memory grant per resource class at a given SLO.</span></span> <span data-ttu-id="19bc3-735">Kullanıcının tooprovide NULL hem şema hem de tablename için bu hello aşağıdaki örnekte gösterildiği gibi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-735">User needs tooprovide NULL for both schema and tablename for this as shown in hello example below.</span></span>  
2. <span data-ttu-id="19bc3-736">toohelp kullanıcı anlayıp hello en yakın iyi kaynak sınıfı hello bellek intensed için belirtilen kaynak sınıfı olmayan bölümlenmiş CCI tablosunda CCI işlemleri (yük, kopyalama tablo yeniden dizin, vb.).</span><span class="sxs-lookup"><span data-stu-id="19bc3-736">toohelp user figure out hello closest best resource class for hello memory intensed CCI operations (load, copy table, rebuild index, etc.) on non partitioned CCI table at a given resource class.</span></span> <span data-ttu-id="19bc3-737">depolanan hello proc tablo şemasını toofind hello gerekli bellek ataması çıkışı bu için kullanır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-737">hello stored proc uses table schema toofind out hello required memory grant for this.</span></span>

#### <a name="dependencies--restrictions"></a><span data-ttu-id="19bc3-738">Bağımlılıklar ve sınırlamalar:</span><span class="sxs-lookup"><span data-stu-id="19bc3-738">Dependencies & Restrictions:</span></span>
- <span data-ttu-id="19bc3-739">Bu saklı yordam bölümlenmiş cci tablosu için tasarlanmış toocalculate bellek gereksinimi değil.</span><span class="sxs-lookup"><span data-stu-id="19bc3-739">This stored proc is not designed toocalculate memory requirement for partitioned-cci table.</span></span>    
- <span data-ttu-id="19bc3-740">Bu saklı yordam hello SELECT Ekle/CTAS-seçin kısmı için bellek gereksinimi dikkate almaz ve toobe basit bir SELECT varsayar.</span><span class="sxs-lookup"><span data-stu-id="19bc3-740">This stored proc doesn't take memory requirement into account for hello SELECT part of CTAS/INSERT-SELECT and assumes it toobe a simple SELECT.</span></span>
- <span data-ttu-id="19bc3-741">Bu saklı yordam hello oturumunda bu kullanılabilir Bu saklı yordam oluşturulduğu geçici bir tablo kullanır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-741">This stored proc uses a temp table so this can be used in hello session where this stored proc was created.</span></span>    
- <span data-ttu-id="19bc3-742">Bu değişiklikler, ardından bu saklı yordam düzgün çalışmayan ve bu saklı yordam hello geçerli tekliflerini (örn. donanım yapılandırması, DMS config) bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-742">This stored proc depends on hello current offerings (e.g. hardware configuration, DMS config) and if any of that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="19bc3-743">Değişiklikler, ardından bu saklı yordam düzgün çalışmayan ve bu saklı yordam varolan sunulan eşzamanlılık sınırı bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-743">This stored proc depends on existing offered concurrency limit and if that changes then this stored proc would not work correctly.</span></span>  
- <span data-ttu-id="19bc3-744">Bu saklı yordam mevcut kaynak sınıfı tekliflerini bağlıdır ve, ardından bu değişip değişmediğini proc wuold çalışmaz doğru bir şekilde depolanır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-744">This stored proc depends on existing resource class offerings and if that changes then this stored proc wuold not work correctly.</span></span>  

>  [!NOTE]  
>  <span data-ttu-id="19bc3-745">Saklı yordam olabilir sonra iki durumda sağlanan parametrelerle yürüttükten sonra çıktı almıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="19bc3-745">If you are not getting output after executing stored procedure with parameters provided then there could be two cases.</span></span> <br /><span data-ttu-id="19bc3-746">1. Her iki DW parametresi geçersiz SLO değeri içeriyor</span><span class="sxs-lookup"><span data-stu-id="19bc3-746">1. Either DW Parameter contains invalid SLO value</span></span> <br /><span data-ttu-id="19bc3-747">2. VEYA yoksa hiçbir eşleşen kaynak sınıfı CCI işlemi için tablo adı sağlandı.</span><span class="sxs-lookup"><span data-stu-id="19bc3-747">2. OR there are no matching resource class for CCI operation if table name was provided.</span></span> <br /><span data-ttu-id="19bc3-748">Örneğin, DW100, en yüksek bellek ataması 400 MB'dir ve tablo şemasını genişse yeterli toocross 400 MB gereksinimi hello.</span><span class="sxs-lookup"><span data-stu-id="19bc3-748">For example, at DW100, highest memory grant available is 400MB and if table schema is wide enough toocross hello requirement of 400MB.</span></span>
      
#### <a name="usage-example"></a><span data-ttu-id="19bc3-749">Kullanım örneği:</span><span class="sxs-lookup"><span data-stu-id="19bc3-749">Usage example:</span></span>
<span data-ttu-id="19bc3-750">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="19bc3-750">Syntax:</span></span>  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. <span data-ttu-id="19bc3-751">@DWU:Ya da NULL parametresi tooextract sağlamak hello DW DB gelen geçerli DWU hello veya desteklenen herhangi bir DWU 'DW100' hello biçiminde sağlayın</span><span class="sxs-lookup"><span data-stu-id="19bc3-751">@DWU: Either provide a NULL parameter tooextract hello current DWU from hello DW DB or provide any supported DWU in hello form of 'DW100'</span></span>
2. <span data-ttu-id="19bc3-752">@SCHEMA_NAME:Merhaba tablonun şema adını sağlayın</span><span class="sxs-lookup"><span data-stu-id="19bc3-752">@SCHEMA_NAME: Provide a schema name of hello table</span></span>
3. <span data-ttu-id="19bc3-753">@TABLE_NAME:Merhaba ilgi bir tablo adı sağlayın</span><span class="sxs-lookup"><span data-stu-id="19bc3-753">@TABLE_NAME: Provide a table name of hello interest</span></span>

<span data-ttu-id="19bc3-754">Bu saklı yordam yürütme örnekler:</span><span class="sxs-lookup"><span data-stu-id="19bc3-754">Examples executing this stored proc:</span></span>  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

<span data-ttu-id="19bc3-755">Merhaba örnekleri yukarıda kullanılan tablo1 aşağıdaki gibi oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="19bc3-755">Table1 used in hello above examples could be created as below:</span></span>  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a><span data-ttu-id="19bc3-756">Merhaba saklı yordamı tanımı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="19bc3-756">Here's hello stored procedure definition:</span></span>
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a><span data-ttu-id="19bc3-757">Sorgu önem derecesi</span><span class="sxs-lookup"><span data-stu-id="19bc3-757">Query importance</span></span>
<span data-ttu-id="19bc3-758">SQL veri ambarı iş yükü gruplarını kullanarak kaynak sınıfları uygular.</span><span class="sxs-lookup"><span data-stu-id="19bc3-758">SQL Data Warehouse implements resource classes by using workload groups.</span></span> <span data-ttu-id="19bc3-759">Merhaba arasında çeşitli DWU boyutları hello kaynak sınıfları hello davranışını denetleyen sekiz iş yükü grupları toplam vardır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-759">There are a total of eight workload groups that control hello behavior of hello resource classes across hello various DWU sizes.</span></span> <span data-ttu-id="19bc3-760">SQL veri ambarı tüm DWU için yalnızca dört hello sekiz iş yükü gruplarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-760">For any DWU, SQL Data Warehouse uses only four of hello eight workload groups.</span></span> <span data-ttu-id="19bc3-761">Her iş yükü grubu tooone dört kaynak sınıfların atanmış olduğundan bu mantıklı: smallrc, mediumrc, largerc, veya xlargerc.</span><span class="sxs-lookup"><span data-stu-id="19bc3-761">This makes sense because each workload group is assigned tooone of four resource classes: smallrc, mediumrc, largerc, or xlargerc.</span></span> <span data-ttu-id="19bc3-762">Merhaba hello iş yükü grupları anlama önemini iş yükü gruplarının bazıları toohigher ayarlanır olan *önem*.</span><span class="sxs-lookup"><span data-stu-id="19bc3-762">hello importance of understanding hello workload groups is that some of these workload groups are set toohigher *importance*.</span></span> <span data-ttu-id="19bc3-763">Önem derecesi CPU için kullanılan planlama.</span><span class="sxs-lookup"><span data-stu-id="19bc3-763">Importance is used for CPU scheduling.</span></span> <span data-ttu-id="19bc3-764">Yüksek öncelikli olarak çalıştırılan sorguların olandan Orta önem düzeyine sahip üç kat daha fazla CPU döngülerini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="19bc3-764">Queries run with high importance will get three times more CPU cycles than those with medium importance.</span></span> <span data-ttu-id="19bc3-765">Bu nedenle, eşzamanlılık yuvası eşlemeleri CPU Öncelik belirler.</span><span class="sxs-lookup"><span data-stu-id="19bc3-765">Therefore, concurrency slot mappings also determine CPU priority.</span></span> <span data-ttu-id="19bc3-766">Bir sorgu 16 veya daha fazla yuvaları tüketir yüksek önem olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-766">When a query consumes 16 or more slots, it runs as high importance.</span></span>

<span data-ttu-id="19bc3-767">Merhaba aşağıdaki tabloda her iş yükü grubu için hello önem eşlemeler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-767">hello following table shows hello importance mappings for each workload group.</span></span>

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a><span data-ttu-id="19bc3-768">İş yükü grubu eşlemeleri tooconcurrency yuvaları ve önem derecesi</span><span class="sxs-lookup"><span data-stu-id="19bc3-768">Workload group mappings tooconcurrency slots and importance</span></span>
| <span data-ttu-id="19bc3-769">İş yükü grupları</span><span class="sxs-lookup"><span data-stu-id="19bc3-769">Workload groups</span></span> | <span data-ttu-id="19bc3-770">Eşzamanlılık yuvası eşleme</span><span class="sxs-lookup"><span data-stu-id="19bc3-770">Concurrency slot mapping</span></span> | <span data-ttu-id="19bc3-771">MB / dağıtım</span><span class="sxs-lookup"><span data-stu-id="19bc3-771">MB / Distribution</span></span> | <span data-ttu-id="19bc3-772">Önem derecesi eşleme</span><span class="sxs-lookup"><span data-stu-id="19bc3-772">Importance mapping</span></span> |
|:--- |:---:|:---:|:--- |
| <span data-ttu-id="19bc3-773">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="19bc3-773">SloDWGroupC00</span></span> |<span data-ttu-id="19bc3-774">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-774">1</span></span> |<span data-ttu-id="19bc3-775">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-775">100</span></span> |<span data-ttu-id="19bc3-776">Orta</span><span class="sxs-lookup"><span data-stu-id="19bc3-776">Medium</span></span> |
| <span data-ttu-id="19bc3-777">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="19bc3-777">SloDWGroupC01</span></span> |<span data-ttu-id="19bc3-778">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-778">2</span></span> |<span data-ttu-id="19bc3-779">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-779">200</span></span> |<span data-ttu-id="19bc3-780">Orta</span><span class="sxs-lookup"><span data-stu-id="19bc3-780">Medium</span></span> |
| <span data-ttu-id="19bc3-781">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="19bc3-781">SloDWGroupC02</span></span> |<span data-ttu-id="19bc3-782">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-782">4</span></span> |<span data-ttu-id="19bc3-783">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-783">400</span></span> |<span data-ttu-id="19bc3-784">Orta</span><span class="sxs-lookup"><span data-stu-id="19bc3-784">Medium</span></span> |
| <span data-ttu-id="19bc3-785">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="19bc3-785">SloDWGroupC03</span></span> |<span data-ttu-id="19bc3-786">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-786">8</span></span> |<span data-ttu-id="19bc3-787">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-787">800</span></span> |<span data-ttu-id="19bc3-788">Orta</span><span class="sxs-lookup"><span data-stu-id="19bc3-788">Medium</span></span> |
| <span data-ttu-id="19bc3-789">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="19bc3-789">SloDWGroupC04</span></span> |<span data-ttu-id="19bc3-790">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-790">16</span></span> |<span data-ttu-id="19bc3-791">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-791">1,600</span></span> |<span data-ttu-id="19bc3-792">Yüksek</span><span class="sxs-lookup"><span data-stu-id="19bc3-792">High</span></span> |
| <span data-ttu-id="19bc3-793">SloDWGroupC05</span><span class="sxs-lookup"><span data-stu-id="19bc3-793">SloDWGroupC05</span></span> |<span data-ttu-id="19bc3-794">32</span><span class="sxs-lookup"><span data-stu-id="19bc3-794">32</span></span> |<span data-ttu-id="19bc3-795">3,200</span><span class="sxs-lookup"><span data-stu-id="19bc3-795">3,200</span></span> |<span data-ttu-id="19bc3-796">Yüksek</span><span class="sxs-lookup"><span data-stu-id="19bc3-796">High</span></span> |
| <span data-ttu-id="19bc3-797">SloDWGroupC06</span><span class="sxs-lookup"><span data-stu-id="19bc3-797">SloDWGroupC06</span></span> |<span data-ttu-id="19bc3-798">64</span><span class="sxs-lookup"><span data-stu-id="19bc3-798">64</span></span> |<span data-ttu-id="19bc3-799">6,400</span><span class="sxs-lookup"><span data-stu-id="19bc3-799">6,400</span></span> |<span data-ttu-id="19bc3-800">Yüksek</span><span class="sxs-lookup"><span data-stu-id="19bc3-800">High</span></span> |
| <span data-ttu-id="19bc3-801">SloDWGroupC07</span><span class="sxs-lookup"><span data-stu-id="19bc3-801">SloDWGroupC07</span></span> |<span data-ttu-id="19bc3-802">128</span><span class="sxs-lookup"><span data-stu-id="19bc3-802">128</span></span> |<span data-ttu-id="19bc3-803">12,800</span><span class="sxs-lookup"><span data-stu-id="19bc3-803">12,800</span></span> |<span data-ttu-id="19bc3-804">Yüksek</span><span class="sxs-lookup"><span data-stu-id="19bc3-804">High</span></span> |

<span data-ttu-id="19bc3-805">Merhaba gelen **ayırma ve kullanımını eşzamanlılık yuva** grafiği, bir DW500 1, 4, 8 ya da 16 eşzamanlılık yuvası smallrc, mediumrc, largerc ve xlargerc, sırasıyla kullandığını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19bc3-805">From hello **Allocation and consumption of concurrency slots** chart, you can see that a DW500 uses 1, 4, 8 or 16 concurrency slots for smallrc, mediumrc, largerc, and xlargerc, respectively.</span></span> <span data-ttu-id="19bc3-806">Bu değerleri grafik toofind hello önem her kaynak sınıfı için önceki hello bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19bc3-806">You can look those values up in hello preceding chart toofind hello importance for each resource class.</span></span>

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a><span data-ttu-id="19bc3-807">Kaynak sınıfları tooimportance DW500 eşleme</span><span class="sxs-lookup"><span data-stu-id="19bc3-807">DW500 mapping of resource classes tooimportance</span></span>
| <span data-ttu-id="19bc3-808">Kaynak sınıfı</span><span class="sxs-lookup"><span data-stu-id="19bc3-808">Resource class</span></span> | <span data-ttu-id="19bc3-809">İş yükü grubu</span><span class="sxs-lookup"><span data-stu-id="19bc3-809">Workload group</span></span> | <span data-ttu-id="19bc3-810">Kullanılan eşzamanlılık yuvaları</span><span class="sxs-lookup"><span data-stu-id="19bc3-810">Concurrency slots used</span></span> | <span data-ttu-id="19bc3-811">MB / dağıtım</span><span class="sxs-lookup"><span data-stu-id="19bc3-811">MB / Distribution</span></span> | <span data-ttu-id="19bc3-812">Önem derecesi</span><span class="sxs-lookup"><span data-stu-id="19bc3-812">Importance</span></span> |
|:--- |:--- |:---:|:---:|:--- |
| <span data-ttu-id="19bc3-813">smallrc</span><span class="sxs-lookup"><span data-stu-id="19bc3-813">smallrc</span></span> |<span data-ttu-id="19bc3-814">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="19bc3-814">SloDWGroupC00</span></span> |<span data-ttu-id="19bc3-815">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-815">1</span></span> |<span data-ttu-id="19bc3-816">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-816">100</span></span> |<span data-ttu-id="19bc3-817">Orta</span><span class="sxs-lookup"><span data-stu-id="19bc3-817">Medium</span></span> |
| <span data-ttu-id="19bc3-818">mediumrc</span><span class="sxs-lookup"><span data-stu-id="19bc3-818">mediumrc</span></span> |<span data-ttu-id="19bc3-819">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="19bc3-819">SloDWGroupC02</span></span> |<span data-ttu-id="19bc3-820">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-820">4</span></span> |<span data-ttu-id="19bc3-821">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-821">400</span></span> |<span data-ttu-id="19bc3-822">Orta</span><span class="sxs-lookup"><span data-stu-id="19bc3-822">Medium</span></span> |
| <span data-ttu-id="19bc3-823">largerc</span><span class="sxs-lookup"><span data-stu-id="19bc3-823">largerc</span></span> |<span data-ttu-id="19bc3-824">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="19bc3-824">SloDWGroupC03</span></span> |<span data-ttu-id="19bc3-825">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-825">8</span></span> |<span data-ttu-id="19bc3-826">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-826">800</span></span> |<span data-ttu-id="19bc3-827">Orta</span><span class="sxs-lookup"><span data-stu-id="19bc3-827">Medium</span></span> |
| <span data-ttu-id="19bc3-828">xlargerc</span><span class="sxs-lookup"><span data-stu-id="19bc3-828">xlargerc</span></span> |<span data-ttu-id="19bc3-829">SloDWGroupC04</span><span class="sxs-lookup"><span data-stu-id="19bc3-829">SloDWGroupC04</span></span> |<span data-ttu-id="19bc3-830">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-830">16</span></span> |<span data-ttu-id="19bc3-831">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-831">1,600</span></span> |<span data-ttu-id="19bc3-832">Yüksek</span><span class="sxs-lookup"><span data-stu-id="19bc3-832">High</span></span> |
| <span data-ttu-id="19bc3-833">staticrc10</span><span class="sxs-lookup"><span data-stu-id="19bc3-833">staticrc10</span></span> |<span data-ttu-id="19bc3-834">SloDWGroupC00</span><span class="sxs-lookup"><span data-stu-id="19bc3-834">SloDWGroupC00</span></span> |<span data-ttu-id="19bc3-835">1</span><span class="sxs-lookup"><span data-stu-id="19bc3-835">1</span></span> |<span data-ttu-id="19bc3-836">100</span><span class="sxs-lookup"><span data-stu-id="19bc3-836">100</span></span> |<span data-ttu-id="19bc3-837">Orta</span><span class="sxs-lookup"><span data-stu-id="19bc3-837">Medium</span></span> |
| <span data-ttu-id="19bc3-838">staticrc20</span><span class="sxs-lookup"><span data-stu-id="19bc3-838">staticrc20</span></span> |<span data-ttu-id="19bc3-839">SloDWGroupC01</span><span class="sxs-lookup"><span data-stu-id="19bc3-839">SloDWGroupC01</span></span> |<span data-ttu-id="19bc3-840">2</span><span class="sxs-lookup"><span data-stu-id="19bc3-840">2</span></span> |<span data-ttu-id="19bc3-841">200</span><span class="sxs-lookup"><span data-stu-id="19bc3-841">200</span></span> |<span data-ttu-id="19bc3-842">Orta</span><span class="sxs-lookup"><span data-stu-id="19bc3-842">Medium</span></span> |
| <span data-ttu-id="19bc3-843">staticrc30</span><span class="sxs-lookup"><span data-stu-id="19bc3-843">staticrc30</span></span> |<span data-ttu-id="19bc3-844">SloDWGroupC02</span><span class="sxs-lookup"><span data-stu-id="19bc3-844">SloDWGroupC02</span></span> |<span data-ttu-id="19bc3-845">4</span><span class="sxs-lookup"><span data-stu-id="19bc3-845">4</span></span> |<span data-ttu-id="19bc3-846">400</span><span class="sxs-lookup"><span data-stu-id="19bc3-846">400</span></span> |<span data-ttu-id="19bc3-847">Orta</span><span class="sxs-lookup"><span data-stu-id="19bc3-847">Medium</span></span> |
| <span data-ttu-id="19bc3-848">staticrc40</span><span class="sxs-lookup"><span data-stu-id="19bc3-848">staticrc40</span></span> |<span data-ttu-id="19bc3-849">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="19bc3-849">SloDWGroupC03</span></span> |<span data-ttu-id="19bc3-850">8</span><span class="sxs-lookup"><span data-stu-id="19bc3-850">8</span></span> |<span data-ttu-id="19bc3-851">800</span><span class="sxs-lookup"><span data-stu-id="19bc3-851">800</span></span> |<span data-ttu-id="19bc3-852">Orta</span><span class="sxs-lookup"><span data-stu-id="19bc3-852">Medium</span></span> |
| <span data-ttu-id="19bc3-853">staticrc50</span><span class="sxs-lookup"><span data-stu-id="19bc3-853">staticrc50</span></span> |<span data-ttu-id="19bc3-854">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="19bc3-854">SloDWGroupC03</span></span> |<span data-ttu-id="19bc3-855">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-855">16</span></span> |<span data-ttu-id="19bc3-856">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-856">1,600</span></span> |<span data-ttu-id="19bc3-857">Yüksek</span><span class="sxs-lookup"><span data-stu-id="19bc3-857">High</span></span> |
| <span data-ttu-id="19bc3-858">staticrc60</span><span class="sxs-lookup"><span data-stu-id="19bc3-858">staticrc60</span></span> |<span data-ttu-id="19bc3-859">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="19bc3-859">SloDWGroupC03</span></span> |<span data-ttu-id="19bc3-860">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-860">16</span></span> |<span data-ttu-id="19bc3-861">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-861">1,600</span></span> |<span data-ttu-id="19bc3-862">Yüksek</span><span class="sxs-lookup"><span data-stu-id="19bc3-862">High</span></span> |
| <span data-ttu-id="19bc3-863">staticrc70</span><span class="sxs-lookup"><span data-stu-id="19bc3-863">staticrc70</span></span> |<span data-ttu-id="19bc3-864">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="19bc3-864">SloDWGroupC03</span></span> |<span data-ttu-id="19bc3-865">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-865">16</span></span> |<span data-ttu-id="19bc3-866">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-866">1,600</span></span> |<span data-ttu-id="19bc3-867">Yüksek</span><span class="sxs-lookup"><span data-stu-id="19bc3-867">High</span></span> |
| <span data-ttu-id="19bc3-868">staticrc80</span><span class="sxs-lookup"><span data-stu-id="19bc3-868">staticrc80</span></span> |<span data-ttu-id="19bc3-869">SloDWGroupC03</span><span class="sxs-lookup"><span data-stu-id="19bc3-869">SloDWGroupC03</span></span> |<span data-ttu-id="19bc3-870">16</span><span class="sxs-lookup"><span data-stu-id="19bc3-870">16</span></span> |<span data-ttu-id="19bc3-871">1,600</span><span class="sxs-lookup"><span data-stu-id="19bc3-871">1,600</span></span> |<span data-ttu-id="19bc3-872">Yüksek</span><span class="sxs-lookup"><span data-stu-id="19bc3-872">High</span></span> |

<span data-ttu-id="19bc3-873">DMV sorgusu toolook bellek kaynağı ayırma ayrıntılı hello farklılıkları hello kaynak İdarecisi hello açısından veya hello iş yükü grupları tooanalyze etkin ve geçmiş kullanımı sırasında sorunlarını giderirken aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19bc3-873">You can use hello following DMV query toolook at hello differences in memory resource allocation in detail from hello perspective of hello resource governor, or tooanalyze active and historic usage of hello workload groups when troubleshooting.</span></span>

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a><span data-ttu-id="19bc3-874">Eşzamanlılık sınırları dikkate sorguları</span><span class="sxs-lookup"><span data-stu-id="19bc3-874">Queries that honor concurrency limits</span></span>
<span data-ttu-id="19bc3-875">Sorguların çoğu kaynak sınıfları tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-875">Most queries are governed by resource classes.</span></span> <span data-ttu-id="19bc3-876">Bu sorguları hello eşzamanlı sorgu ve eşzamanlılık yuvası eşikleri sığması gerekir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-876">These queries must fit inside both hello concurrent query and concurrency slot thresholds.</span></span> <span data-ttu-id="19bc3-877">Bir kullanıcı, bir sorgu hello eşzamanlılık yuvası modelden tooexclude seçemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="19bc3-877">A user cannot choose tooexclude a query from hello concurrency slot model.</span></span>

<span data-ttu-id="19bc3-878">tooreiterate, deyimleri Uy kaynak sınıfları aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="19bc3-878">tooreiterate, hello following statements honor resource classes:</span></span>

* <span data-ttu-id="19bc3-879">INSERT SEÇİN</span><span class="sxs-lookup"><span data-stu-id="19bc3-879">INSERT-SELECT</span></span>
* <span data-ttu-id="19bc3-880">GÜNCELLEŞTİRME</span><span class="sxs-lookup"><span data-stu-id="19bc3-880">UPDATE</span></span>
* <span data-ttu-id="19bc3-881">SİL</span><span class="sxs-lookup"><span data-stu-id="19bc3-881">DELETE</span></span>
* <span data-ttu-id="19bc3-882">(Kullanıcı tablosu sorgulanırken) seçin</span><span class="sxs-lookup"><span data-stu-id="19bc3-882">SELECT (when querying user tables)</span></span>
* <span data-ttu-id="19bc3-883">ALTER INDEX YENİDEN OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="19bc3-883">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="19bc3-884">ALTER INDEX REORGANIZE KOMUTUNU</span><span class="sxs-lookup"><span data-stu-id="19bc3-884">ALTER INDEX REORGANIZE</span></span>
* <span data-ttu-id="19bc3-885">ALTER TABLE YENİDEN OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="19bc3-885">ALTER TABLE REBUILD</span></span>
* <span data-ttu-id="19bc3-886">DİZİN OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="19bc3-886">CREATE INDEX</span></span>
* <span data-ttu-id="19bc3-887">KÜMELENMİŞ COLUMNSTORE DİZİNİ OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="19bc3-887">CREATE CLUSTERED COLUMNSTORE INDEX</span></span>
* <span data-ttu-id="19bc3-888">TABLE AS SELECT (CTAS) OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="19bc3-888">CREATE TABLE AS SELECT (CTAS)</span></span>
* <span data-ttu-id="19bc3-889">Veri yükleme</span><span class="sxs-lookup"><span data-stu-id="19bc3-889">Data loading</span></span>
* <span data-ttu-id="19bc3-890">Veri Taşıma hizmeti (DMS) Hello tarafından gerçekleştirilen veri taşıma işlemleri</span><span class="sxs-lookup"><span data-stu-id="19bc3-890">Data movement operations conducted by hello Data Movement Service (DMS)</span></span>

## <a name="query-exceptions-tooconcurrency-limits"></a><span data-ttu-id="19bc3-891">Sorgu özel durumları tooconcurrency sınırları</span><span class="sxs-lookup"><span data-stu-id="19bc3-891">Query exceptions tooconcurrency limits</span></span>
<span data-ttu-id="19bc3-892">Bazı sorgular hello kaynak getirmiyor sınıfı toowhich hello kullanıcı atanır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-892">Some queries do not honor hello resource class toowhich hello user is assigned.</span></span> <span data-ttu-id="19bc3-893">Belirli bir komut için gereken hello bellek kaynakları genellikle Hello komutu meta veri işlemi olduğundan düşük olduğunda bu özel durumlar toohello eşzamanlılık sınırları yapılır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-893">These exceptions toohello concurrency limits are made when hello memory resources needed for a particular command are low, often because hello command is a metadata operation.</span></span> <span data-ttu-id="19bc3-894">Merhaba bu özel durumları tooavoid büyük bellek ayırmaları hiçbir zaman bunları gerekir sorgular için hedefidir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-894">hello goal of these exceptions is tooavoid larger memory allocations for queries that will never need them.</span></span> <span data-ttu-id="19bc3-895">Bu durumlarda, küçük bir kaynak sınıfı (smallrc) hello gerçek kaynak sınıfı bağımsız olarak her zaman kullanılır hello varsayılan toohello kullanıcı atanır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-895">In these cases, hello default small resource class (smallrc) is always used regardless of hello actual resource class assigned toohello user.</span></span> <span data-ttu-id="19bc3-896">Örneğin, `CREATE LOGIN` smallrc içinde her zaman çalışır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-896">For example, `CREATE LOGIN` will always run in smallrc.</span></span> <span data-ttu-id="19bc3-897">Merhaba gerekli kaynakları toofulfill bu işlem çok düşük algılama tooinclude hello sorgu hello eşzamanlılık yuvası modelinde yapmaz şekilde.</span><span class="sxs-lookup"><span data-stu-id="19bc3-897">hello resources required toofulfill this operation are very low, so it does not make sense tooinclude hello query in hello concurrency slot model.</span></span>  <span data-ttu-id="19bc3-898">Bu sorguları da hello 32 kullanıcı eşzamanlılık sınırı tarafından sınırlı değildir, bu sorguları sınırsız sayıda 1.024 oturumlarının toohello oturum sınırı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19bc3-898">These queries are also not limited by hello 32 user concurrency limit, an unlimited number of these queries can run up toohello session limit of 1,024 sessions.</span></span>

<span data-ttu-id="19bc3-899">deyimlerini aşağıdaki hello kaynak sınıfları getirmiyor:</span><span class="sxs-lookup"><span data-stu-id="19bc3-899">hello following statements do not honor resource classes:</span></span>

* <span data-ttu-id="19bc3-900">DROP TABLE veya oluşturma</span><span class="sxs-lookup"><span data-stu-id="19bc3-900">CREATE or DROP TABLE</span></span>
* <span data-ttu-id="19bc3-901">ALTER TABLE... ANAHTAR, bölme veya bölüm birleştirme</span><span class="sxs-lookup"><span data-stu-id="19bc3-901">ALTER TABLE ... SWITCH, SPLIT, or MERGE PARTITION</span></span>
* <span data-ttu-id="19bc3-902">ALTER INDEX DEVRE DIŞI BIRAK</span><span class="sxs-lookup"><span data-stu-id="19bc3-902">ALTER INDEX DISABLE</span></span>
* <span data-ttu-id="19bc3-903">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="19bc3-903">DROP INDEX</span></span>
* <span data-ttu-id="19bc3-904">OLUŞTURMA, güncelleştirme ya da DROP STATISTICS</span><span class="sxs-lookup"><span data-stu-id="19bc3-904">CREATE, UPDATE, or DROP STATISTICS</span></span>
* <span data-ttu-id="19bc3-905">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="19bc3-905">TRUNCATE TABLE</span></span>
* <span data-ttu-id="19bc3-906">ALTER YETKİLENDİRME</span><span class="sxs-lookup"><span data-stu-id="19bc3-906">ALTER AUTHORIZATION</span></span>
* <span data-ttu-id="19bc3-907">OTURUM AÇMA OLUŞTURUN</span><span class="sxs-lookup"><span data-stu-id="19bc3-907">CREATE LOGIN</span></span>
* <span data-ttu-id="19bc3-908">CREATE, ALTER veya DROP USER</span><span class="sxs-lookup"><span data-stu-id="19bc3-908">CREATE, ALTER or DROP USER</span></span>
* <span data-ttu-id="19bc3-909">OLUŞTURMA, değiştirme veya bırakma yordamı</span><span class="sxs-lookup"><span data-stu-id="19bc3-909">CREATE, ALTER or DROP PROCEDURE</span></span>
* <span data-ttu-id="19bc3-910">OLUŞTURMA veya DROP VIEW</span><span class="sxs-lookup"><span data-stu-id="19bc3-910">CREATE or DROP VIEW</span></span>
* <span data-ttu-id="19bc3-911">DEĞER EKLEME</span><span class="sxs-lookup"><span data-stu-id="19bc3-911">INSERT VALUES</span></span>
* <span data-ttu-id="19bc3-912">Sistem görünümleri ve Dmv'leri seçin</span><span class="sxs-lookup"><span data-stu-id="19bc3-912">SELECT from system views and DMVs</span></span>
* <span data-ttu-id="19bc3-913">AÇIKLANMAKTADIR</span><span class="sxs-lookup"><span data-stu-id="19bc3-913">EXPLAIN</span></span>
* <span data-ttu-id="19bc3-914">DBCC</span><span class="sxs-lookup"><span data-stu-id="19bc3-914">DBCC</span></span>

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <span data-ttu-id="19bc3-915"><a name="changing-user-resource-class-example"></a>Bir kullanıcı kaynak sınıfı örneği değiştirme</span><span class="sxs-lookup"><span data-stu-id="19bc3-915"><a name="changing-user-resource-class-example"></a> Change a user resource class example</span></span>
1. <span data-ttu-id="19bc3-916">**Oturum açma oluşturun:** bağlantı tooyour açmak **ana** veritabanı hello SQL Server'da, SQL veri ambarı veritabanını barındıran ve hello aşağıdaki komutları yürütün.</span><span class="sxs-lookup"><span data-stu-id="19bc3-916">**Create login:** Open a connection tooyour **master** database on hello SQL server hosting your SQL Data Warehouse database and execute hello following commands.</span></span>
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > <span data-ttu-id="19bc3-917">Merhaba ana veritabanını Azure SQL Data Warehouse kullanıcılar için iyi bir fikir toocreate bir kullanıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="19bc3-917">It is a good idea toocreate a user in hello master database for Azure SQL Data Warehouse users.</span></span> <span data-ttu-id="19bc3-918">Master kullanıcı oluşturma, bir veritabanı adı belirtmeden SSMS gibi araçları kullanarak bir kullanıcı toologin sağlar.</span><span class="sxs-lookup"><span data-stu-id="19bc3-918">Creating a user in master allows a user toologin using tools like SSMS without specifying a database name.</span></span>  <span data-ttu-id="19bc3-919">Ayrıca bunları toouse hello Nesne Gezgini tooview tüm veritabanları SQL server üzerinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="19bc3-919">It also allows them toouse hello object explorer tooview all databases on a SQL server.</span></span>  <span data-ttu-id="19bc3-920">Oluşturma ve kullanıcıları yönetme hakkında daha fazla ayrıntı için bkz: [SQL veri ambarı veritabanında güvenli][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="19bc3-920">For more details about creating and managing users, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>
   > 
   > 
2. <span data-ttu-id="19bc3-921">**SQL veri ambarı kullanıcı oluşturun:** bağlantı toohello açmak **SQL Data Warehouse** veritabanı ve hello aşağıdaki komutu yürütün.</span><span class="sxs-lookup"><span data-stu-id="19bc3-921">**Create SQL Data Warehouse user:** Open a connection toohello **SQL Data Warehouse** database and execute hello following command.</span></span>
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. <span data-ttu-id="19bc3-922">**İzinleri verin:** hello örnek verir `CONTROL` hello üzerinde **SQL Data Warehouse** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="19bc3-922">**Grant permissions:** hello following example grants `CONTROL` on hello **SQL Data Warehouse** database.</span></span> <span data-ttu-id="19bc3-923">`CONTROL`Merhaba veritabanı düzeyi olduğu hello SQL Server'daki db_owner eşdeğeridir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-923">`CONTROL` at hello database level is hello equivalent of db_owner in SQL Server.</span></span>
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. <span data-ttu-id="19bc3-924">**Kaynak sınıfı artırmak:** kullanım hello aşağıdaki sorgu tooadd kullanıcı tooa daha yüksek iş yükü yönetim rolü.</span><span class="sxs-lookup"><span data-stu-id="19bc3-924">**Increase resource class:** Use hello following query tooadd a user tooa higher workload management role.</span></span>
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. <span data-ttu-id="19bc3-925">**Kaynak sınıfı azaltın:** kullanım hello aşağıdaki sorgu tooremove bir kullanıcıdan bir iş yükü yönetim rolü.</span><span class="sxs-lookup"><span data-stu-id="19bc3-925">**Decrease resource class:** Use hello following query tooremove a user from a workload management role.</span></span>
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="19bc3-926">Olası tooremove smallrc bir kullanıcı değil.</span><span class="sxs-lookup"><span data-stu-id="19bc3-926">It is not possible tooremove a user from smallrc.</span></span>
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a><span data-ttu-id="19bc3-927">Sıraya alınan sorgu algılama ve diğer Dmv'leri</span><span class="sxs-lookup"><span data-stu-id="19bc3-927">Queued query detection and other DMVs</span></span>
<span data-ttu-id="19bc3-928">Merhaba kullanabilirsiniz `sys.dm_pdw_exec_requests` bir eşzamanlılık sırada bekleyen DMV tooidentify sorgular.</span><span class="sxs-lookup"><span data-stu-id="19bc3-928">You can use hello `sys.dm_pdw_exec_requests` DMV tooidentify queries that are waiting in a concurrency queue.</span></span> <span data-ttu-id="19bc3-929">Sorgular bir eşzamanlılık yuva durumu için bekleyen **askıya**.</span><span class="sxs-lookup"><span data-stu-id="19bc3-929">Queries waiting for a concurrency slot will have a status of **suspended**.</span></span>

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

<span data-ttu-id="19bc3-930">İş yükü yönetim rolleri ile görüntülenebilir `sys.database_principals`.</span><span class="sxs-lookup"><span data-stu-id="19bc3-930">Workload management roles can be viewed with `sys.database_principals`.</span></span>

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

<span data-ttu-id="19bc3-931">Sorgu aşağıdaki hello her kullanıcının atandığı rolü gösterir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-931">hello following query shows which role each user is assigned to.</span></span>

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

<span data-ttu-id="19bc3-932">SQL veri ambarı türleri bekleyin hello aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="19bc3-932">SQL Data Warehouse has hello following wait types:</span></span>

* <span data-ttu-id="19bc3-933">**LocalQueriesConcurrencyResourceType**: hello eşzamanlılık yuvası framework dışında sit sorgular.</span><span class="sxs-lookup"><span data-stu-id="19bc3-933">**LocalQueriesConcurrencyResourceType**: Queries that sit outside of hello concurrency slot framework.</span></span> <span data-ttu-id="19bc3-934">DMV sorgular ve sistem işlevleri gibi `SELECT @@VERSION` yerel sorgular gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-934">DMV queries and system functions such as `SELECT @@VERSION` are examples of local queries.</span></span>
* <span data-ttu-id="19bc3-935">**UserConcurrencyResourceType**: hello eşzamanlılık yuvası framework içinde sit sorgular.</span><span class="sxs-lookup"><span data-stu-id="19bc3-935">**UserConcurrencyResourceType**: Queries that sit inside hello concurrency slot framework.</span></span> <span data-ttu-id="19bc3-936">Son kullanıcı tabloları sorguları bu kaynak türü kullanırsınız örnekleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="19bc3-936">Queries against end-user tables represent examples that would use this resource type.</span></span>
* <span data-ttu-id="19bc3-937">**DmsConcurrencyResourceType**: veri taşıma işlemleri kaynaklanan bekler.</span><span class="sxs-lookup"><span data-stu-id="19bc3-937">**DmsConcurrencyResourceType**: Waits resulting from data movement operations.</span></span>
* <span data-ttu-id="19bc3-938">**BackupConcurrencyResourceType**: Bu bekleme bir veritabanı yedekleniyor olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-938">**BackupConcurrencyResourceType**: This wait indicates that a database is being backed up.</span></span> <span data-ttu-id="19bc3-939">Bu kaynak türü için Hello en büyük değer 1'dir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-939">hello maximum value for this resource type is 1.</span></span> <span data-ttu-id="19bc3-940">Birden çok yedekleme sırasında hello istenmiş, aynı zamanda, diğerleri sıraya hello.</span><span class="sxs-lookup"><span data-stu-id="19bc3-940">If multiple backups have been requested at hello same time, hello others will queue.</span></span>

<span data-ttu-id="19bc3-941">Merhaba `sys.dm_pdw_waits` DMV kullanılan toosee hangi kaynakların bir isteği bekliyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-941">hello `sys.dm_pdw_waits` DMV can be used toosee which resources a request is waiting for.</span></span>

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

<span data-ttu-id="19bc3-942">Merhaba `sys.dm_pdw_resource_waits` DMV belirli bir sorgu tarafından tüketilen hello kaynak bekler gösterir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-942">hello `sys.dm_pdw_resource_waits` DMV shows only hello resource waits consumed by a given query.</span></span> <span data-ttu-id="19bc3-943">Kaynak bekleme süresi yalnızca sağlanan kaynakları toobe için bekleyen hello süreyi ölçer. Bu, karşılıklı toosignal bekleyin gibi hello zamanı zaman SQL sunucuları tooschedule hello hello CPU üzerine sorguyla hello için alır.</span><span class="sxs-lookup"><span data-stu-id="19bc3-943">Resource wait time only measures hello time waiting for resources toobe provided, as opposed toosignal wait time, which is hello time it takes for hello underlying SQL servers tooschedule hello query onto hello CPU.</span></span>

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

<span data-ttu-id="19bc3-944">Merhaba `sys.dm_pdw_wait_stats` DMV bekler geçmiş eğilim analizi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="19bc3-944">hello `sys.dm_pdw_wait_stats` DMV can be used for historic trend analysis of waits.</span></span>

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a><span data-ttu-id="19bc3-945">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19bc3-945">Next steps</span></span>
<span data-ttu-id="19bc3-946">Veritabanı kullanıcıları yönetme ve güvenlik hakkında daha fazla bilgi için bkz: [SQL veri ambarı veritabanında güvenli][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="19bc3-946">For more information about managing database users and security, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span> <span data-ttu-id="19bc3-947">Ne kadar büyük kaynak sınıfları hakkında daha fazla bilgi kümelenmiş columnstore dizini kalitesini artırmak, bkz [dizinleri tooimprove segment kalite yeniden].</span><span class="sxs-lookup"><span data-stu-id="19bc3-947">For more information about how larger resource classes can improve clustered columnstore index quality, see [Rebuilding indexes tooimprove segment quality].</span></span>

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[dizinleri tooimprove segment kalite yeniden]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
