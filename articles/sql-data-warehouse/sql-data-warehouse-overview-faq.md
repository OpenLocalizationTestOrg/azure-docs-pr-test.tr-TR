---
title: "aaaAzure SQL veri ambarı ile ilgili sık sorulan sorular | Microsoft Docs"
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
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="2f168-103">SQL veri ambarı sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="2f168-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="2f168-104">Genel</span><span class="sxs-lookup"><span data-stu-id="2f168-104">General</span></span>

<span data-ttu-id="2f168-105">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-105">Q.</span></span> <span data-ttu-id="2f168-106">Ne SQL DW veri güvenliği için sunar?</span><span class="sxs-lookup"><span data-stu-id="2f168-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="2f168-107">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-107">A.</span></span> <span data-ttu-id="2f168-108">SQL DW TDE gibi verileri korumak ve denetlemek için çeşitli çözümler sunar.</span><span class="sxs-lookup"><span data-stu-id="2f168-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="2f168-109">Daha fazla bilgi için bkz: [güvenlik].</span><span class="sxs-lookup"><span data-stu-id="2f168-109">For more information, see [Security].</span></span>

<span data-ttu-id="2f168-110">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-110">Q.</span></span> <span data-ttu-id="2f168-111">Hangi yasal veya iş standartları SQL DW olduğunu uyumlu nereden bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="2f168-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="2f168-112">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-112">A.</span></span> <span data-ttu-id="2f168-113">Merhaba ziyaret [Microsoft Compliance] ürün SOC ve ISO gibi çeşitli uyumluluk sunumları için sayfa.</span><span class="sxs-lookup"><span data-stu-id="2f168-113">Visit hello [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="2f168-114">İlk uyumluluk başlığı seçin, ardından Azure genişletin hangi hizmetler Azure hizmetlerdir hello içinde kapsam için Microsoft bulut Hizmetleri bölümünde hello sayfa toosee hello sağ tarafında uyumlu.</span><span class="sxs-lookup"><span data-stu-id="2f168-114">First choose by Compliance title, then expand Azure in hello Microsoft in-scope cloud services section on hello right side of hello page toosee what services are Azure services are compliant.</span></span>

<span data-ttu-id="2f168-115">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-115">Q.</span></span> <span data-ttu-id="2f168-116">Powerbı bağlayabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="2f168-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="2f168-117">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-117">A.</span></span> <span data-ttu-id="2f168-118">Evet!</span><span class="sxs-lookup"><span data-stu-id="2f168-118">Yes!</span></span> <span data-ttu-id="2f168-119">SQL DW ile doğrudan sorgu Powerbı destekler ancak çok sayıda kullanıcı veya gerçek zamanlı verileri için tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="2f168-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="2f168-120">Powerbı üretim kullanımı için Azure Analysis Services ya da analiz hizmeti Iaas üstünde Powerbı kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2f168-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="2f168-121">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-121">Q.</span></span> <span data-ttu-id="2f168-122">SQL veri ambarı kapasite sınırları nelerdir?</span><span class="sxs-lookup"><span data-stu-id="2f168-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="2f168-123">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-123">A.</span></span> <span data-ttu-id="2f168-124">Bizim geçerli bkz [kapasite limitlerini] sayfası.</span><span class="sxs-lookup"><span data-stu-id="2f168-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="2f168-125">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-125">Q.</span></span> <span data-ttu-id="2f168-126">Neden my ölçek/Duraklat/Sürdür çok uzun sürüyor?</span><span class="sxs-lookup"><span data-stu-id="2f168-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="2f168-127">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-127">A.</span></span> <span data-ttu-id="2f168-128">Çeşitli etkenlere işlem yönetimi işlemleri için başlangıç saati etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="2f168-128">A variety of factors can influence hello time for compute management operations.</span></span> <span data-ttu-id="2f168-129">Bir ortak işlemleri uzun süre çalışan işlem geri alma için durumda.</span><span class="sxs-lookup"><span data-stu-id="2f168-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="2f168-130">Bir ölçek veya duraklatma işlemi başlatıldığında, tüm gelen oturumları engellenir ve sorguları boşaltmış.</span><span class="sxs-lookup"><span data-stu-id="2f168-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="2f168-131">Bir işlem yeniden başlatılmadan önce sipariş tooleave hello sisteminde tutarlı bir durumda, işlemleri geri alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2f168-131">In order tooleave hello system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="2f168-132">büyük hello sayısını ve işlemleri büyük hello günlük boyutunu Merhaba, hello sistem tooa kararlı durum geri hello uzun hello işlemi durduruldu.</span><span class="sxs-lookup"><span data-stu-id="2f168-132">hello greater hello number and larger hello log size of transactions, hello longer hello operation will be stalled restoring hello system tooa stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="2f168-133">Kullanıcı desteği</span><span class="sxs-lookup"><span data-stu-id="2f168-133">User support</span></span>

<span data-ttu-id="2f168-134">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-134">Q.</span></span> <span data-ttu-id="2f168-135">Özellik isteği burada gönderme sahip miyim?</span><span class="sxs-lookup"><span data-stu-id="2f168-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="2f168-136">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-136">A.</span></span> <span data-ttu-id="2f168-137">Özellik isteği varsa, üzerinde gönderme bizim [UserVoice] sayfası</span><span class="sxs-lookup"><span data-stu-id="2f168-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="2f168-138">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-138">Q.</span></span> <span data-ttu-id="2f168-139">Nasıl yapabilirim x?</span><span class="sxs-lookup"><span data-stu-id="2f168-139">How can I do x?</span></span>

<span data-ttu-id="2f168-140">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-140">A.</span></span> <span data-ttu-id="2f168-141">SQL veri ambarı ile geliştirilmesi konusunda daha fazla yardım için üzerinde sorular sorabilirsiniz bizim [yığın taşması] sayfası.</span><span class="sxs-lookup"><span data-stu-id="2f168-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="2f168-142">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-142">Q.</span></span> <span data-ttu-id="2f168-143">Bir destek bileti nasıl gönderilsin mi?</span><span class="sxs-lookup"><span data-stu-id="2f168-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="2f168-144">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-144">A.</span></span> <span data-ttu-id="2f168-145">[Destek biletlerini Göster] Azure portalı üzerinden kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="2f168-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="2f168-146">SQL dil/özellik desteği</span><span class="sxs-lookup"><span data-stu-id="2f168-146">SQL language/feature support</span></span> 

<span data-ttu-id="2f168-147">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-147">Q.</span></span> <span data-ttu-id="2f168-148">Hangi veri türleri SQL Data Warehouse destekliyor mu?</span><span class="sxs-lookup"><span data-stu-id="2f168-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="2f168-149">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-149">A.</span></span> <span data-ttu-id="2f168-150">SQL veri ambarı bkz [veri türleri].</span><span class="sxs-lookup"><span data-stu-id="2f168-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="2f168-151">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-151">Q.</span></span> <span data-ttu-id="2f168-152">Tablo özellikleri destekliyor?</span><span class="sxs-lookup"><span data-stu-id="2f168-152">What table features do you support?</span></span>

<span data-ttu-id="2f168-153">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-153">A.</span></span> <span data-ttu-id="2f168-154">SQL veri ambarı birçok özellik desteklerken, bazı desteklenmez ve belgelenmiştir [desteklenmeyen Tablo Özellikler].</span><span class="sxs-lookup"><span data-stu-id="2f168-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="2f168-155">Araçları ve yönetim</span><span class="sxs-lookup"><span data-stu-id="2f168-155">Tooling and administration</span></span>

<span data-ttu-id="2f168-156">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-156">Q.</span></span> <span data-ttu-id="2f168-157">Visual Studio veritabanı projelerini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="2f168-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="2f168-158">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-158">A.</span></span> <span data-ttu-id="2f168-159">Şu anda veritabanı projeleri Visual Studio ile SQL Data Warehouse için desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2f168-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="2f168-160">Oy tooget toocast isterseniz bu özelliği, bizim kullanıcı sesi ziyaret [veritabanı projeleri özellik isteği].</span><span class="sxs-lookup"><span data-stu-id="2f168-160">If you'd like toocast a vote tooget this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="2f168-161">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-161">Q.</span></span> <span data-ttu-id="2f168-162">SQL Data Warehouse, REST API'leri destekliyor mu?</span><span class="sxs-lookup"><span data-stu-id="2f168-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="2f168-163">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-163">A.</span></span> <span data-ttu-id="2f168-164">Evet.</span><span class="sxs-lookup"><span data-stu-id="2f168-164">Yes.</span></span> <span data-ttu-id="2f168-165">SQL veritabanı ile kullanılan çoğu REST işlevselliği de SQL Data Warehouse ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2f168-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="2f168-166">REST belge sayfalarının içinde API bilgi bulabilirsiniz veya [MSDN].</span><span class="sxs-lookup"><span data-stu-id="2f168-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="2f168-167">Yükleniyor</span><span class="sxs-lookup"><span data-stu-id="2f168-167">Loading</span></span>

<span data-ttu-id="2f168-168">Q.</span><span class="sxs-lookup"><span data-stu-id="2f168-168">Q.</span></span> <span data-ttu-id="2f168-169">Hangi istemci sürücüleri destekliyor?</span><span class="sxs-lookup"><span data-stu-id="2f168-169">What client drivers do you support?</span></span>

<span data-ttu-id="2f168-170">A.</span><span class="sxs-lookup"><span data-stu-id="2f168-170">A.</span></span> <span data-ttu-id="2f168-171">DW sürücü desteği hello üzerinde bulunabilir [bağlantı dizeleri] sayfası</span><span class="sxs-lookup"><span data-stu-id="2f168-171">Driver support for DW can be found on hello [Connection Strings] page</span></span>

<span data-ttu-id="2f168-172">S: hangi dosya biçimleri, SQL veri ambarı ile PolyBase tarafından desteklenir?</span><span class="sxs-lookup"><span data-stu-id="2f168-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="2f168-173">Y: Orc, RC, Parquet ve düz sınırlandırılmış metin</span><span class="sxs-lookup"><span data-stu-id="2f168-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="2f168-174">S: ne toofrom SQL DW Polybase'i kullanarak bağlanmak?</span><span class="sxs-lookup"><span data-stu-id="2f168-174">Q: What can I connect toofrom SQL DW using PolyBase?</span></span> 

<span data-ttu-id="2f168-175">Y: [Azure Data Lake Store] ve [Azure depolama BLOB'ları]</span><span class="sxs-lookup"><span data-stu-id="2f168-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="2f168-176">S: hesaplama aşağı itme olası tooAzure depolama BLOB veya ADLS bağlanırken mi?</span><span class="sxs-lookup"><span data-stu-id="2f168-176">Q: Is computation pushdown possible  when connecting tooAzure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="2f168-177">A: Hayır SQL DW PolyBase yalnızca hello depolama bileşenleri etkileşim kurar.</span><span class="sxs-lookup"><span data-stu-id="2f168-177">A: No, SQL DW PolyBase only interacts hello storage components.</span></span> 

<span data-ttu-id="2f168-178">S: tooHDI bağlanmak?</span><span class="sxs-lookup"><span data-stu-id="2f168-178">Q: Can I connect tooHDI?</span></span>

<span data-ttu-id="2f168-179">Y: HDI ADLS veya WASB hello HDFS katmanı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f168-179">A: HDI can use either ADLS or WASB as hello HDFS layer.</span></span> <span data-ttu-id="2f168-180">HDFS katmanı olarak ya da varsa, bu verileri SQL DW yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f168-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="2f168-181">Ancak, aşağı itme hesaplama toohello HDI örneği oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="2f168-181">However, you cannot generate pushdown computation toohello HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2f168-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2f168-182">Next steps</span></span>
<span data-ttu-id="2f168-183">Bir bütün olarak SQL Data Warehouse hakkında daha fazla bilgi için bkz: bizim [genel bakış] sayfası.</span><span class="sxs-lookup"><span data-stu-id="2f168-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[bağlantı dizeleri]: ./sql-data-warehouse-connection-strings.md
[yığın taşması]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Destek biletlerini Göster]: ./sql-data-warehouse-get-started-create-support-ticket.md
[güvenlik]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[kapasite limitlerini]: ./sql-data-warehouse-service-capacity-limits.md
[veri türleri]: ./sql-data-warehouse-tables-data-types.md
[desteklenmeyen Tablo Özellikler]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure depolama BLOB'ları]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[veritabanı projeleri özellik isteği]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[genel bakış]: ./sql-data-warehouse-overview-faq.md