---
title: "Azure AD Connect Health eşitleme ile aaaUsing | Microsoft Docs"
description: "Bu, nasıl toomonitor Azure AD Connect eşitleme ele alınacaktır hello Azure AD Connect Health sayfasıdır."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a><span data-ttu-id="7265e-103">Azure AD Connect eşitlemesini Azure AD Connect Health ile izleme</span><span class="sxs-lookup"><span data-stu-id="7265e-103">Monitor Azure AD Connect sync with Azure AD Connect Health</span></span>
<span data-ttu-id="7265e-104">Belge aşağıdaki hello belirli toomonitoring Azure AD Connect (eşitleme) Azure AD Connect Health ile olur.</span><span class="sxs-lookup"><span data-stu-id="7265e-104">hello following documentation is specific toomonitoring Azure AD Connect (Sync) with Azure AD Connect Health.</span></span>  <span data-ttu-id="7265e-105">Azure Connect Health ile AD FS'yi izleme hakkında bilgi almak için bkz. [Azure AD Connect Health'i AD FS ile kullanma](active-directory-aadconnect-health-adfs.md).</span><span class="sxs-lookup"><span data-stu-id="7265e-105">For information on monitoring AD FS with Azure AD Connect Health see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span></span> <span data-ttu-id="7265e-106">Ek olarak, Active Directory Etki Alanı Hizmetleri’ni Azure AD Connect Health ile izleme hakkında bilgi için bkz. [AD DS ile Azure AD Connect Health Kullanma](active-directory-aadconnect-health-adds.md).</span><span class="sxs-lookup"><span data-stu-id="7265e-106">Additionally, for information on monitoring Active Directory Domain Services with Azure AD Connect Health see [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md).</span></span>

![Eşitleme için Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a><span data-ttu-id="7265e-108">Eşitleme için Azure AD Connect Health uyarıları</span><span class="sxs-lookup"><span data-stu-id="7265e-108">Alerts for Azure AD Connect Health for sync</span></span>
<span data-ttu-id="7265e-109">Hello Azure AD Connect Health uyarıları eşitleme bölümü için etkin uyarıların listesi hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="7265e-109">hello Azure AD Connect Health Alerts for sync section provides you hello list of active alerts.</span></span> <span data-ttu-id="7265e-110">Her uyarı ilgili bilgileri, çözüm adımları ve bağlantıları toorelated belgeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="7265e-110">Each alert includes relevant information, resolution steps, and links toorelated documentation.</span></span> <span data-ttu-id="7265e-111">Etkin veya çözümlenmiş bir uyarıyı seçtiğinizde tooresolve hello uyarı ve bağlantıları tooadditional belgelerine atabileceğiniz adımlar yanı sıra ek bilgiler içeren yeni bir dikey pencere görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7265e-111">By selecting an active or resolved alert you will see a new blade with additional information, as well as steps you can take tooresolve hello alert, and links tooadditional documentation.</span></span> <span data-ttu-id="7265e-112">Ayrıca, geçmiş verileri hello geçmişte çözümlenen uyarıları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7265e-112">You can also view historical data on alerts that were resolved in hello past.</span></span>

<span data-ttu-id="7265e-113">Adımları yanı sıra ek bilgiler sağlanacak bir uyarıyı seçtiğinizde tooadditional belgelerine tooresolve hello uyarı ve bağlantıları alabilir.</span><span class="sxs-lookup"><span data-stu-id="7265e-113">By selecting an alert you will be provided with additional information as well as steps you can take tooresolve hello alert and links tooadditional documentation.</span></span>

![Azure AD Connect eşitleme hatası](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a><span data-ttu-id="7265e-115">Sınırlı Uyarı Değerlendirmesi</span><span class="sxs-lookup"><span data-stu-id="7265e-115">Limited Evaluation of Alerts</span></span>
<span data-ttu-id="7265e-116">Azure AD Connect (örneğin, öznitelik filtrelemesi hello varsayılan yapılandırma tooa özel yapılandırma değiştirildiyse) hello varsayılan yapılandırmayı kullanmıyorsa, ardından hello Azure AD Connect Health Aracısı hello hata olayları ilgili tooAzure karşıya yüklemez AD bağlanın.</span><span class="sxs-lookup"><span data-stu-id="7265e-116">If Azure AD Connect is NOT using hello default configuration (for example, if Attribute Filtering is changed from hello default configuration tooa custom configuration), then hello Azure AD Connect Health agent will not upload hello error events related tooAzure AD Connect.</span></span>

<span data-ttu-id="7265e-117">Bu uyarı hello değerlendirmesi hello hizmeti tarafından sınırlar.</span><span class="sxs-lookup"><span data-stu-id="7265e-117">This limits hello evaluation of alerts by hello service.</span></span> <span data-ttu-id="7265e-118">Hello Azure Portal'da hizmetinizin altında bu koşulu belirten bir başlık görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7265e-118">You'd will see a banner that indicates this condition in hello Azure Portal under your service.</span></span>

![Eşitleme için Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner.png)

<span data-ttu-id="7265e-120">Bu, "Ayarlar" a tıklayarak ve Azure AD Connect Health Aracısı tooupload tüm hata günlüklerini vererek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7265e-120">You can change this by clicking "Settings" and allowing Azure AD Connect Health agent tooupload all error logs.</span></span>

![Eşitleme için Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a><span data-ttu-id="7265e-122">Eşitleme Öngörüsü</span><span class="sxs-lookup"><span data-stu-id="7265e-122">Sync Insight</span></span>
<span data-ttu-id="7265e-123">Sık yöneticileri, tooknow toosync değişiklikleri tooAzure AD ve gerçekleşmesini değişiklikleri hello miktarını hello süresini hakkında istiyor.</span><span class="sxs-lookup"><span data-stu-id="7265e-123">Admins Frequently want tooknow about hello time it takes toosync changes tooAzure AD and hello amount of changes taking place.</span></span> <span data-ttu-id="7265e-124">Bu özellik bir kolay bir yolu toovisualize bu grafikleri aşağıda hello kullanarak aşağıdakileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="7265e-124">This feature provides an easy way toovisualize this using hello below graphs:</span></span>   

* <span data-ttu-id="7265e-125">Eşitleme işlemlerinin gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="7265e-125">Latency of sync operations</span></span>
* <span data-ttu-id="7265e-126">Nesne Değişikliği eğilimi</span><span class="sxs-lookup"><span data-stu-id="7265e-126">Object Change trend</span></span>

### <a name="sync-latency"></a><span data-ttu-id="7265e-127">Eşitleme Gecikme Süresi</span><span class="sxs-lookup"><span data-stu-id="7265e-127">Sync Latency</span></span>
<span data-ttu-id="7265e-128">Bu özellik, gecikme hello eşitleme işlemlerinin (içeri aktarma, dışarı aktarma, vb.) bağlayıcıların grafik eğilimini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7265e-128">This feature provides a graphical trend of latency of hello sync operations (import, export, etc.) for connectors.</span></span>  <span data-ttu-id="7265e-129">Bu hızlı sağlar ve kolay bir yolu toounderstand daha fazla incelenmesi gerekebilecek hello gecikme süresi içinde değil yalnızca işlemlerinizin (çok sayıda değişikliğinizin varsa, daha büyük) de bir şekilde toodetect anormallikleri gecikme hello.</span><span class="sxs-lookup"><span data-stu-id="7265e-129">This provides a quick and easy way toounderstand not only hello latency of your operations (larger if you have a large set of changes occurring) but also a way toodetect anomalies in hello latency that may require further investigation.</span></span>

![Eşitleme Gecikme Süresi](./media/active-directory-aadconnect-health-sync/synclatency02.png)

<span data-ttu-id="7265e-131">Varsayılan olarak, yalnızca hello 'Verme' işlemi'hello Azure AD Bağlayıcısı için hello gecikme gösterilir.</span><span class="sxs-lookup"><span data-stu-id="7265e-131">By default, only hello latency of hello 'Export' operation for hello Azure AD connector is shown.</span></span>  <span data-ttu-id="7265e-132">toosee hello bağlayıcı üzerinde daha fazla işlem veya diğer bağlayıcılara tooview işlemleri hello grafikte sağ grafiği Düzenle öğesini seçmeniz veya hello "Gecikmesi grafiği Düzenle" düğmesine tıklayın ve hello belirli işlemi ve bağlayıcıları seçin.</span><span class="sxs-lookup"><span data-stu-id="7265e-132">toosee more operations on hello connector or tooview operations from other connectors, right-click on hello chart,  select Edit Chart or click on hello "Edit Latency Chart" button and choose hello specific operation and connectors.</span></span>

### <a name="sync-object-changes"></a><span data-ttu-id="7265e-133">Eşitleme Nesnesi Değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="7265e-133">Sync Object Changes</span></span>
<span data-ttu-id="7265e-134">Bu özellik, değerlendirilen ve tooAzure AD dışarı değişiklikleri hello sayısının grafik eğilimini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7265e-134">This feature provides a graphical trend of hello number of changes that are being evaluated and exported tooAzure AD.</span></span>  <span data-ttu-id="7265e-135">Bugün, çalışırken toogather bu bilgileri hello eşitleme günlüklerinden zordur.</span><span class="sxs-lookup"><span data-stu-id="7265e-135">Today, trying toogather this information from hello sync logs is difficult.</span></span>  <span data-ttu-id="7265e-136">Merhaba grafik, ortamınızda oluşan değişiklik hello sayısı, aynı zamanda yaşanan hello hataları görsel görünümünü İzleme yalnızca daha basit bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="7265e-136">hello chart gives you, not only a simpler way of monitoring hello number of changes that are occurring in your environment, but also a visual view of hello failures that are occurring.</span></span>

![Eşitleme Gecikme Süresi](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a><span data-ttu-id="7265e-138">Nesne Düzeyinde Eşitleme Hata Raporu (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="7265e-138">Object Level Synchronization Error Report (Preview)</span></span>
<span data-ttu-id="7265e-139">Bu özellik, kimlik verileri Azure AD Connect kullanılarak Windows Server AD ile Azure AD arasında eşitlenirken oluşabilecek eşitleme hataları hakkında bir rapor sağlar.</span><span class="sxs-lookup"><span data-stu-id="7265e-139">This feature provides a report about synchronization errors that can occur when identity data is synchronized between Windows Server AD and Azure AD using Azure AD Connect.</span></span>

* <span data-ttu-id="7265e-140">Merhaba raporun kapsadığı hello eşitleme istemcisi tarafından kaydedilen hataları (Azure AD Connect sürüm 1.1.281.0 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="7265e-140">hello report covers errors recorded by hello sync client (Azure AD Connect version 1.1.281.0 or higher)</span></span>
* <span data-ttu-id="7265e-141">Merhaba eşitleme altyapısı hello son eşitleme işlemi oluştu hello hataları içerir.</span><span class="sxs-lookup"><span data-stu-id="7265e-141">It includes hello errors that occurred in hello last synchronization operation on hello sync engine.</span></span> <span data-ttu-id="7265e-142">("Merhaba Azure AD Bağlayıcısı üzerinde ver.")</span><span class="sxs-lookup"><span data-stu-id="7265e-142">("Export" on hello Azure AD Connector.)</span></span>
* <span data-ttu-id="7265e-143">Eşitleme için Azure AD Connect Health aracısını hello rapor tooinclude hello en son veriler için giden bağlantı gerekli toohello bitiş noktası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7265e-143">Azure AD Connect Health agent for sync must have outbound connectivity toohello required end points for hello report tooinclude hello latest data.</span></span>
* <span data-ttu-id="7265e-144">Merhaba rapor **her 30 dakika sonra güncelleştirilmiş** hello verileri kullanarak eşitleme için Azure AD Connect Health aracısı tarafından yüklendi. Aşağıdaki temel işlevler hello sağlar</span><span class="sxs-lookup"><span data-stu-id="7265e-144">hello report is **updated after every 30 minutes** using hello data uploaded by Azure AD Connect Health agent for sync. It provides hello following key capabilities</span></span>

  * <span data-ttu-id="7265e-145">Hataların kategorilere ayrılması</span><span class="sxs-lookup"><span data-stu-id="7265e-145">Categorization of errors</span></span>
  * <span data-ttu-id="7265e-146">Kategoriye göre hatalı nesnelerin listesi</span><span class="sxs-lookup"><span data-stu-id="7265e-146">List of objects with error per category</span></span>
  * <span data-ttu-id="7265e-147">Tek bir yerde hello hatalarını ilgili tüm hello verileri</span><span class="sxs-lookup"><span data-stu-id="7265e-147">All hello data about hello errors at one place</span></span>
  * <span data-ttu-id="7265e-148">Yan yana tooa çakışması nedeniyle hatasıyla nesnelerin yan karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="7265e-148">Side by side comparison of Objects with error due tooa conflict</span></span>
  * <span data-ttu-id="7265e-149">Merhaba hata raporu (yakında) CVS karşıdan yükle</span><span class="sxs-lookup"><span data-stu-id="7265e-149">Download hello error report as a CVS (coming soon)</span></span>

### <a name="categorization-of-errors"></a><span data-ttu-id="7265e-150">Hataların Kategorilere Ayrılması</span><span class="sxs-lookup"><span data-stu-id="7265e-150">Categorization of Errors</span></span>
<span data-ttu-id="7265e-151">Merhaba rapor kategorileri aşağıdaki hello hello mevcut eşitleme hatalarının gruplandırır:</span><span class="sxs-lookup"><span data-stu-id="7265e-151">hello report categorizes hello existing synchronization errors in hello following categories:</span></span>

| <span data-ttu-id="7265e-152">Kategori</span><span class="sxs-lookup"><span data-stu-id="7265e-152">Category</span></span> | <span data-ttu-id="7265e-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7265e-153">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7265e-154">Yinelenen Öznitelik</span><span class="sxs-lookup"><span data-stu-id="7265e-154">Duplicate Attribute</span></span> |<span data-ttu-id="7265e-155">Azure AD Connect, bir Kiracıda benzersiz olması gereken ve Azure AD Connect’te bulunan bir veya daha fazla özniteliğin (proxyAddresses ve UserPrincipalName gibi) yinelenen değerleri ile nesneler oluşturmaya veya güncelleştirmeye çalıştığında oluşan hatalar.</span><span class="sxs-lookup"><span data-stu-id="7265e-155">Errors when Azure AD Connect attempts create or update objects with duplicated values of one or more attributes in Azure AD that must be unique in a Tenant, such as proxyAddresses, UserPrincipalName.</span></span> |
| <span data-ttu-id="7265e-156">Veri Uyuşmazlığı</span><span class="sxs-lookup"><span data-stu-id="7265e-156">Data Mismatch</span></span> |<span data-ttu-id="7265e-157">Eşitleme hatalarına neden toomatch nesneleri Hello soft-match başarısız olduğunda hataları.</span><span class="sxs-lookup"><span data-stu-id="7265e-157">Errors when hello soft-match fails toomatch objects that result in synchronization errors.</span></span> |
| <span data-ttu-id="7265e-158">Veri Doğrulama Hatası</span><span class="sxs-lookup"><span data-stu-id="7265e-158">Data Validation Failure</span></span> |<span data-ttu-id="7265e-159">Hataları UserPrincipalName gibi kritik öznitelikleri desteklenmeyen karakterler gibi tooinvalid verileri nedeniyle başarısız Azure AD'de yazılmakta önce doğrulama hatalarını biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="7265e-159">Errors due tooinvalid data, such as unsupported characters in critical attributes such as UserPrincipalName, format errors that fail validation before being written in Azure AD.</span></span> |
| <span data-ttu-id="7265e-160">Büyük Öznitelik</span><span class="sxs-lookup"><span data-stu-id="7265e-160">Large Attribute</span></span> |<span data-ttu-id="7265e-161">Bir veya daha fazla öznitelik hello büyük olduğunda hataları izin verilen boyutu, uzunluk veya sayısı.</span><span class="sxs-lookup"><span data-stu-id="7265e-161">Errors when one or more attributes are larger than hello allowed size, length or count.</span></span> |
| <span data-ttu-id="7265e-162">Diğer</span><span class="sxs-lookup"><span data-stu-id="7265e-162">Other</span></span> |<span data-ttu-id="7265e-163">Kategoriler yukarıda hello uymayan tüm diğer hatalar.</span><span class="sxs-lookup"><span data-stu-id="7265e-163">All other errors that don't fit in hello above categories.</span></span> <span data-ttu-id="7265e-164">Bu kategori, geri bildirimleriniz temel alınarak alt kategorilere ayrılacaktır.</span><span class="sxs-lookup"><span data-stu-id="7265e-164">Based on feedback, this category will be split in sub categories.</span></span> |

<span data-ttu-id="7265e-165">![Eşitleme Hata Raporu Özeti](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Eşitleme Hata Raporu Kategorileri](./media/active-directory-aadconnect-health-sync/errorreport02.png)</span><span class="sxs-lookup"><span data-stu-id="7265e-165">![Sync Error Report Summary](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Sync Error Report Categories](./media/active-directory-aadconnect-health-sync/errorreport02.png)</span></span>

### <a name="list-of-objects-with-error-per-category"></a><span data-ttu-id="7265e-166">Kategoriye göre hatalı nesnelerin listesi</span><span class="sxs-lookup"><span data-stu-id="7265e-166">List of objects with error per category</span></span>
<span data-ttu-id="7265e-167">Her kategoride ayrıntılara hello hata kategoriye sahip nesneleri hello listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7265e-167">Drilling into each category will provide hello list of objects having hello error in that category.</span></span>
<span data-ttu-id="7265e-168">![Eşitleme Hata Raporu Listesi](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span><span class="sxs-lookup"><span data-stu-id="7265e-168">![Sync Error Report List](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span></span>

### <a name="error-details"></a><span data-ttu-id="7265e-169">Hata Ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="7265e-169">Error Details</span></span>
<span data-ttu-id="7265e-170">Veri aşağıdaki kullanılabilir hello ayrıntılı görünümü her hata için</span><span class="sxs-lookup"><span data-stu-id="7265e-170">Following data is available in hello detailed view for each error</span></span>

* <span data-ttu-id="7265e-171">Merhaba tanımlayıcıları *AD nesne* söz konusu</span><span class="sxs-lookup"><span data-stu-id="7265e-171">Identifiers for hello *AD Object* involved</span></span>
* <span data-ttu-id="7265e-172">Merhaba tanımlayıcıları *Azure AD nesne* (uygun şekilde) dahil</span><span class="sxs-lookup"><span data-stu-id="7265e-172">Identifiers for hello *Azure AD Object* involved (as applicable)</span></span>
* <span data-ttu-id="7265e-173">Hata açıklaması ve nasıl toofix</span><span class="sxs-lookup"><span data-stu-id="7265e-173">Error description and how toofix</span></span>
* <span data-ttu-id="7265e-174">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="7265e-174">Related articles</span></span>

![Eşitleme Hata Raporu Ayrıntıları](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a><span data-ttu-id="7265e-176">Merhaba hata raporu CSV olarak indir</span><span class="sxs-lookup"><span data-stu-id="7265e-176">Download hello error report as CSV</span></span>
<span data-ttu-id="7265e-177">Merhaba seçerek "tüm hello hataları ile ilgili tüm hello ayrıntıları içeren CSV dosyası indirebilirsiniz dışa aktarma düğmesi".</span><span class="sxs-lookup"><span data-stu-id="7265e-177">By selecting hello "Export" button you can download a CSV file with all hello details about all hello errors.</span></span>

## <a name="related-links"></a><span data-ttu-id="7265e-178">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="7265e-178">Related links</span></span>
* [<span data-ttu-id="7265e-179">Eşitleme sırasında karşılaşılan Hataları giderme</span><span class="sxs-lookup"><span data-stu-id="7265e-179">Troubleshooting Errors during synchronization</span></span>](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [<span data-ttu-id="7265e-180">Yinelenen Öznitelik Dayanıklılığı</span><span class="sxs-lookup"><span data-stu-id="7265e-180">Duplicate Attribute Resiliency</span></span>](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [<span data-ttu-id="7265e-181">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="7265e-181">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="7265e-182">Azure AD Connect Health Aracısı Yüklemesi</span><span class="sxs-lookup"><span data-stu-id="7265e-182">Azure AD Connect Health Agent Installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="7265e-183">Azure AD Connect Health İşlemleri</span><span class="sxs-lookup"><span data-stu-id="7265e-183">Azure AD Connect Health Operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="7265e-184">Azure AD Connect Health'i AD FS ile Kullanma</span><span class="sxs-lookup"><span data-stu-id="7265e-184">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="7265e-185">Azure AD Connect Health'i AD DS ile Kullanma</span><span class="sxs-lookup"><span data-stu-id="7265e-185">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="7265e-186">Azure AD Connect Health ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="7265e-186">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="7265e-187">Azure AD Connect Health Sürüm Geçmişi</span><span class="sxs-lookup"><span data-stu-id="7265e-187">Azure AD Connect Health Version History</span></span>](active-directory-aadconnect-health-version-history.md)