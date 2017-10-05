---
title: "Azure SQL veri ambarı sık sorulan sorular | Microsoft Docs"
description: "Bu makalede Azure SQL veri ambarı hakkında sık sorulan sorular müşteriler ve geliştiricilerin çıkışı listeler"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 4c00710ecc0c91f8407eca81b78176075fcbd6ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="5c106-103">SQL veri ambarı sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="5c106-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="5c106-104">Genel</span><span class="sxs-lookup"><span data-stu-id="5c106-104">General</span></span>

<span data-ttu-id="5c106-105">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-105">Q.</span></span> <span data-ttu-id="5c106-106">Ne SQL DW veri güvenliği için sunar?</span><span class="sxs-lookup"><span data-stu-id="5c106-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="5c106-107">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-107">A.</span></span> <span data-ttu-id="5c106-108">SQL DW TDE gibi verileri korumak ve denetlemek için çeşitli çözümler sunar.</span><span class="sxs-lookup"><span data-stu-id="5c106-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="5c106-109">Daha fazla bilgi için bkz: [güvenlik].</span><span class="sxs-lookup"><span data-stu-id="5c106-109">For more information, see [Security].</span></span>

<span data-ttu-id="5c106-110">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-110">Q.</span></span> <span data-ttu-id="5c106-111">Hangi yasal veya iş standartları SQL DW olduğunu uyumlu nereden bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="5c106-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="5c106-112">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-112">A.</span></span> <span data-ttu-id="5c106-113">Ziyaret [Microsoft Compliance] ürün SOC ve ISO gibi çeşitli uyumluluk sunumları için sayfa.</span><span class="sxs-lookup"><span data-stu-id="5c106-113">Visit the [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="5c106-114">İlk uyumluluk başlığı seçin, ardından Azure genişletin Microsoft kapsam içinde bulut hizmetlerini bölümünde Azure hangi hizmetlerin olduğunu görmek için sayfanın sağ tarafında Hizmetleri uyumludur.</span><span class="sxs-lookup"><span data-stu-id="5c106-114">First choose by Compliance title, then expand Azure in the Microsoft in-scope cloud services section on the right side of the page to see what services are Azure services are compliant.</span></span>

<span data-ttu-id="5c106-115">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-115">Q.</span></span> <span data-ttu-id="5c106-116">Powerbı bağlayabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="5c106-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="5c106-117">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-117">A.</span></span> <span data-ttu-id="5c106-118">Evet!</span><span class="sxs-lookup"><span data-stu-id="5c106-118">Yes!</span></span> <span data-ttu-id="5c106-119">SQL DW ile doğrudan sorgu Powerbı destekler ancak çok sayıda kullanıcı veya gerçek zamanlı verileri için tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="5c106-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="5c106-120">Powerbı üretim kullanımı için Azure Analysis Services ya da analiz hizmeti Iaas üstünde Powerbı kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="5c106-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="5c106-121">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-121">Q.</span></span> <span data-ttu-id="5c106-122">SQL veri ambarı kapasite sınırları nelerdir?</span><span class="sxs-lookup"><span data-stu-id="5c106-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="5c106-123">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-123">A.</span></span> <span data-ttu-id="5c106-124">Bizim geçerli bkz [kapasite limitlerini] sayfası.</span><span class="sxs-lookup"><span data-stu-id="5c106-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="5c106-125">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-125">Q.</span></span> <span data-ttu-id="5c106-126">Neden my ölçek/Duraklat/Sürdür çok uzun sürüyor?</span><span class="sxs-lookup"><span data-stu-id="5c106-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="5c106-127">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-127">A.</span></span> <span data-ttu-id="5c106-128">İşlem yönetimi işlemleri için süre çeşitli etkenlere etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="5c106-128">A variety of factors can influence the time for compute management operations.</span></span> <span data-ttu-id="5c106-129">Bir ortak işlemleri uzun süre çalışan işlem geri alma için durumda.</span><span class="sxs-lookup"><span data-stu-id="5c106-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="5c106-130">Bir ölçek veya duraklatma işlemi başlatıldığında, tüm gelen oturumları engellenir ve sorguları boşaltmış.</span><span class="sxs-lookup"><span data-stu-id="5c106-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="5c106-131">Bir işlem yeniden başlatılmadan önce sistem kararlı durumda bırakın için işlemleri geri alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c106-131">In order to leave the system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="5c106-132">Büyük sayı ve daha büyük günlük boyutu hareketlerinin, uzun işlemi sistem kararlı bir duruma geri yükleme durduruldu.</span><span class="sxs-lookup"><span data-stu-id="5c106-132">The greater the number and larger the log size of transactions, the longer the operation will be stalled restoring the system to a stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="5c106-133">Kullanıcı desteği</span><span class="sxs-lookup"><span data-stu-id="5c106-133">User support</span></span>

<span data-ttu-id="5c106-134">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-134">Q.</span></span> <span data-ttu-id="5c106-135">Özellik isteği burada gönderme sahip miyim?</span><span class="sxs-lookup"><span data-stu-id="5c106-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="5c106-136">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-136">A.</span></span> <span data-ttu-id="5c106-137">Özellik isteği varsa, üzerinde gönderme bizim [UserVoice] sayfası</span><span class="sxs-lookup"><span data-stu-id="5c106-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="5c106-138">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-138">Q.</span></span> <span data-ttu-id="5c106-139">Nasıl yapabilirim x?</span><span class="sxs-lookup"><span data-stu-id="5c106-139">How can I do x?</span></span>

<span data-ttu-id="5c106-140">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-140">A.</span></span> <span data-ttu-id="5c106-141">SQL veri ambarı ile geliştirilmesi konusunda daha fazla yardım için üzerinde sorular sorabilirsiniz bizim [yığın taşması] sayfası.</span><span class="sxs-lookup"><span data-stu-id="5c106-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="5c106-142">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-142">Q.</span></span> <span data-ttu-id="5c106-143">Bir destek bileti nasıl gönderilsin mi?</span><span class="sxs-lookup"><span data-stu-id="5c106-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="5c106-144">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-144">A.</span></span> <span data-ttu-id="5c106-145">[Destek biletlerini Göster] Azure portalı üzerinden kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="5c106-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="5c106-146">SQL dil/özellik desteği</span><span class="sxs-lookup"><span data-stu-id="5c106-146">SQL language/feature support</span></span> 

<span data-ttu-id="5c106-147">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-147">Q.</span></span> <span data-ttu-id="5c106-148">Hangi veri türleri SQL Data Warehouse destekliyor mu?</span><span class="sxs-lookup"><span data-stu-id="5c106-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="5c106-149">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-149">A.</span></span> <span data-ttu-id="5c106-150">SQL veri ambarı bkz [veri türleri].</span><span class="sxs-lookup"><span data-stu-id="5c106-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="5c106-151">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-151">Q.</span></span> <span data-ttu-id="5c106-152">Tablo özellikleri destekliyor?</span><span class="sxs-lookup"><span data-stu-id="5c106-152">What table features do you support?</span></span>

<span data-ttu-id="5c106-153">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-153">A.</span></span> <span data-ttu-id="5c106-154">SQL veri ambarı birçok özellik desteklerken, bazı desteklenmez ve belgelenmiştir [desteklenmeyen Tablo Özellikler].</span><span class="sxs-lookup"><span data-stu-id="5c106-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="5c106-155">Araçları ve yönetim</span><span class="sxs-lookup"><span data-stu-id="5c106-155">Tooling and administration</span></span>

<span data-ttu-id="5c106-156">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-156">Q.</span></span> <span data-ttu-id="5c106-157">Visual Studio veritabanı projelerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="5c106-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="5c106-158">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-158">A.</span></span> <span data-ttu-id="5c106-159">Şu anda veritabanı projeleri Visual Studio ile SQL Data Warehouse için desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5c106-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="5c106-160">Bu özellik almak için bir oy dönüştürmek istiyorsanız, bizim kullanıcı sesi ziyaret [veritabanı projeleri özellik isteği].</span><span class="sxs-lookup"><span data-stu-id="5c106-160">If you'd like to cast a vote to get this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="5c106-161">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-161">Q.</span></span> <span data-ttu-id="5c106-162">SQL Data Warehouse, REST API'leri destekliyor mu?</span><span class="sxs-lookup"><span data-stu-id="5c106-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="5c106-163">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-163">A.</span></span> <span data-ttu-id="5c106-164">Evet.</span><span class="sxs-lookup"><span data-stu-id="5c106-164">Yes.</span></span> <span data-ttu-id="5c106-165">SQL veritabanı ile kullanılan çoğu REST işlevselliği de SQL Data Warehouse ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5c106-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="5c106-166">REST belge sayfalarının içinde API bilgi bulabilirsiniz veya [MSDN].</span><span class="sxs-lookup"><span data-stu-id="5c106-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="5c106-167">Yükleniyor</span><span class="sxs-lookup"><span data-stu-id="5c106-167">Loading</span></span>

<span data-ttu-id="5c106-168">Q.</span><span class="sxs-lookup"><span data-stu-id="5c106-168">Q.</span></span> <span data-ttu-id="5c106-169">Hangi istemci sürücüleri destekliyor?</span><span class="sxs-lookup"><span data-stu-id="5c106-169">What client drivers do you support?</span></span>

<span data-ttu-id="5c106-170">A.</span><span class="sxs-lookup"><span data-stu-id="5c106-170">A.</span></span> <span data-ttu-id="5c106-171">DW sürücü desteği bulunabilir [bağlantı dizeleri] sayfası</span><span class="sxs-lookup"><span data-stu-id="5c106-171">Driver support for DW can be found on the [Connection Strings] page</span></span>

<span data-ttu-id="5c106-172">S: hangi dosya biçimleri, SQL veri ambarı ile PolyBase tarafından desteklenir?</span><span class="sxs-lookup"><span data-stu-id="5c106-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="5c106-173">Y: Orc, RC, Parquet ve düz sınırlandırılmış metin</span><span class="sxs-lookup"><span data-stu-id="5c106-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="5c106-174">S: ne ı PolyBase kullanarak SQL DW bağlanabilir mi?</span><span class="sxs-lookup"><span data-stu-id="5c106-174">Q: What can I connect to from SQL DW using PolyBase?</span></span> 

<span data-ttu-id="5c106-175">Y: [Azure Data Lake Store] ve [Azure depolama BLOB'ları]</span><span class="sxs-lookup"><span data-stu-id="5c106-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="5c106-176">S: hesaplama aşağı itme Azure Storage Bloblarında veya ADLS bağlanırken mi?</span><span class="sxs-lookup"><span data-stu-id="5c106-176">Q: Is computation pushdown possible  when connecting to Azure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="5c106-177">A: Hayır SQL DW PolyBase yalnızca depolama bileşenleri etkileşim kurar.</span><span class="sxs-lookup"><span data-stu-id="5c106-177">A: No, SQL DW PolyBase only interacts the storage components.</span></span> 

<span data-ttu-id="5c106-178">S: HDI için bağlanabilir?</span><span class="sxs-lookup"><span data-stu-id="5c106-178">Q: Can I connect to HDI?</span></span>

<span data-ttu-id="5c106-179">Y: HDI ADLS veya WASB HDFS katmanı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c106-179">A: HDI can use either ADLS or WASB as the HDFS layer.</span></span> <span data-ttu-id="5c106-180">HDFS katmanı olarak ya da varsa, bu verileri SQL DW yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c106-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="5c106-181">Ancak, aşağı itme hesaplama HDI örneği oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="5c106-181">However, you cannot generate pushdown computation to the HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5c106-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5c106-182">Next steps</span></span>
<span data-ttu-id="5c106-183">Bir bütün olarak SQL Data Warehouse hakkında daha fazla bilgi için bkz: bizim [genel bakış] sayfası.</span><span class="sxs-lookup"><span data-stu-id="5c106-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
<span data-ttu-id="5c106-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span><span class="sxs-lookup"><span data-stu-id="5c106-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span></span>
<span data-ttu-id="5c106-185">[bağlantı dizeleri]: ./sql-data-warehouse-connection-strings.md</span><span class="sxs-lookup"><span data-stu-id="5c106-185">[Connection Strings]: ./sql-data-warehouse-connection-strings.md</span></span>
<span data-ttu-id="5c106-186">[yığın taşması]: http://stackoverflow.com/questions/tagged/azure-sqldw</span><span class="sxs-lookup"><span data-stu-id="5c106-186">[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw</span></span>
<span data-ttu-id="5c106-187">[Destek biletlerini Göster]: ./sql-data-warehouse-get-started-create-support-ticket.md</span><span class="sxs-lookup"><span data-stu-id="5c106-187">[Support Tickets]: ./sql-data-warehouse-get-started-create-support-ticket.md</span></span>
<span data-ttu-id="5c106-188">[güvenlik]: ./sql-data-warehouse-overview-manage-security.md</span><span class="sxs-lookup"><span data-stu-id="5c106-188">[Security]: ./sql-data-warehouse-overview-manage-security.md</span></span>
<span data-ttu-id="5c106-189">[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span><span class="sxs-lookup"><span data-stu-id="5c106-189">[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span></span>
<span data-ttu-id="5c106-190">[kapasite limitlerini]: ./sql-data-warehouse-service-capacity-limits.md</span><span class="sxs-lookup"><span data-stu-id="5c106-190">[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md</span></span>
<span data-ttu-id="5c106-191">[veri türleri]: ./sql-data-warehouse-tables-data-types.md</span><span class="sxs-lookup"><span data-stu-id="5c106-191">[data types]: ./sql-data-warehouse-tables-data-types.md</span></span>
<span data-ttu-id="5c106-192">[desteklenmeyen Tablo Özellikler]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span><span class="sxs-lookup"><span data-stu-id="5c106-192">[Unsupported Table Features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span></span>
<span data-ttu-id="5c106-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span><span class="sxs-lookup"><span data-stu-id="5c106-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span></span>
<span data-ttu-id="5c106-194">[Azure depolama BLOB'ları]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span><span class="sxs-lookup"><span data-stu-id="5c106-194">[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span></span>
<span data-ttu-id="5c106-195">[veritabanı projeleri özellik isteği]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span><span class="sxs-lookup"><span data-stu-id="5c106-195">[Database projects feature request]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span></span>
<span data-ttu-id="5c106-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span><span class="sxs-lookup"><span data-stu-id="5c106-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span></span>
<span data-ttu-id="5c106-197">[genel bakış]: ./sql-data-warehouse-overview-faq.md</span><span class="sxs-lookup"><span data-stu-id="5c106-197">[Overview]: ./sql-data-warehouse-overview-faq.md</span></span>