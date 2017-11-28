---
title: "Veri Yönetimi ağ geçidi için aaaRelease notları | Microsoft Docs"
description: "Veri Yönetimi ağ geçidi yazı sürüm notları"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="8ea90-103">Veri Yönetimi Ağ Geçidi için sürüm notları</span><span class="sxs-lookup"><span data-stu-id="8ea90-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="8ea90-104">Merhaba zorluklar modern veri tümleştirme için şirket içi toocloud gelen toomove veri tooand biridir.</span><span class="sxs-lookup"><span data-stu-id="8ea90-104">One of hello challenges for modern data integration is toomove data tooand from on-premises toocloud.</span></span> <span data-ttu-id="8ea90-105">Data Factory veri yönetimi, şirket içi tooenable karma veri taşıma yükleyebilmek için bir aracı olan ağ geçidi ile tümleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ea90-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises tooenable hybrid data movement.</span></span>

<span data-ttu-id="8ea90-106">Makaleler veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için aşağıdaki hello bakın ve nasıl toouse onu:</span><span class="sxs-lookup"><span data-stu-id="8ea90-106">See hello following articles for detailed information about Data Management Gateway and how toouse it:</span></span>

*  [<span data-ttu-id="8ea90-107">Veri Yönetimi Ağ Geçidi</span><span class="sxs-lookup"><span data-stu-id="8ea90-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="8ea90-108">Şirket içi arasında veri taşıyabilir ve Azure Data Factory kullanarak bulut</span><span class="sxs-lookup"><span data-stu-id="8ea90-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="8ea90-109">GEÇERLİ SÜRÜM (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="8ea90-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="8ea90-110">Geliştirmeler-</span><span class="sxs-lookup"><span data-stu-id="8ea90-110">Enhancements-</span></span>
- <span data-ttu-id="8ea90-111">Uygulamaları güvenilir listeye almayı yerine DNS girişlerini toowhitelist hizmet veri yolu tüm Azure IP adresleri, Güvenlik Duvarı (gerekirse) ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ea90-111">You can add DNS entries toowhitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="8ea90-112">Azure Portal'da ilgili DNS girişi bulabilirsiniz (Data Factory -> 'Geliştir ve Dağıt' -> 'Ağ geçidi' -> (JSON içinde) "serviceUrls"</span><span class="sxs-lookup"><span data-stu-id="8ea90-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="8ea90-113">HDFS bağlayıcı kendinden imzalı bir ortak sertifika SSL Doğrulamayı atla izin vererek olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="8ea90-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="8ea90-114">Sabit: Ağ geçidi çevrimdışı (son tooclock eğriltme) güncelleştirme sorun</span><span class="sxs-lookup"><span data-stu-id="8ea90-114">Fixed: Issue with gateway offline during update (due tooclock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="8ea90-115">Önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="8ea90-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="8ea90-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="8ea90-117">Geliştirmeler-</span><span class="sxs-lookup"><span data-stu-id="8ea90-117">Enhancements-</span></span>
-   <span data-ttu-id="8ea90-118">Uygulamaları güvenilir listeye almayı yerine DNS girişlerini toowhitelist Service Bus tüm Azure IP adresleri, Güvenlik Duvarı (gerekirse) ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ea90-118">You can add DNS entries toowhitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="8ea90-119">Daha fazla ayrıntı burada.</span><span class="sxs-lookup"><span data-stu-id="8ea90-119">More details here.</span></span>
-   <span data-ttu-id="8ea90-120">Şimdi tek blok blobu too4.75 blok blobu hello desteklenen en büyük boyutu TB yukarı/gruptan veri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ea90-120">You can now copy data to/from a single block blob up too4.75 TB, which is hello max supported size of block blob.</span></span> <span data-ttu-id="8ea90-121">(önceki sınırı 195 GB'den okunurdu).</span><span class="sxs-lookup"><span data-stu-id="8ea90-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="8ea90-122">Sabit: Kopyalama etkinliği sırasında birkaç küçük dosyalar unzipping çalışırken bellek sorununu dışı.</span><span class="sxs-lookup"><span data-stu-id="8ea90-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="8ea90-123">Sabit: Dizin belge DB tooan kopyalama sırasında aralığı sorunu dışında SQL Server benzersizlik özelliği ile şirket içi.</span><span class="sxs-lookup"><span data-stu-id="8ea90-123">Fixed: Index out of range issue while copying from Document DB tooan on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="8ea90-124">Sabit: SQL temizleme betiğini Kopyalama Sihirbazı'ndan şirket içi SQL Server ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="8ea90-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="8ea90-125">Sabit: Hello sonunda boşluk sütun adıyla kopyalama etkinliği çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="8ea90-125">Fixed: Column name with space at hello end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="8ea90-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="8ea90-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="8ea90-127">Geliştirmeler-</span><span class="sxs-lookup"><span data-stu-id="8ea90-127">Enhancements-</span></span>
- <span data-ttu-id="8ea90-128">Sabit: ağ geçidi makinenin yeniden başlatılmasını kimlik bilgileri eksik olan sorun.</span><span class="sxs-lookup"><span data-stu-id="8ea90-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="8ea90-129">Sabit: Kayıt sırasında ağ geçidi ile ilgili sorun geri yedekleme dosyası kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8ea90-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="8ea90-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="8ea90-131">Geliştirmeler-</span><span class="sxs-lookup"><span data-stu-id="8ea90-131">Enhancements-</span></span>
- <span data-ttu-id="8ea90-132">Sabit: Kaynak olarak Oracle arasında ondalık null değer yanlış okuyun.</span><span class="sxs-lookup"><span data-stu-id="8ea90-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="8ea90-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="8ea90-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="8ea90-134">Yenilikler</span><span class="sxs-lookup"><span data-stu-id="8ea90-134">What’s new</span></span>
- <span data-ttu-id="8ea90-135">Müşteri geri bildirim deneyimi kaydetme ağ geçidinde sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="8ea90-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="8ea90-136">Yeni bir sıkıştırma biçimi destekler: ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="8ea90-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="8ea90-137">Geliştirmeler-</span><span class="sxs-lookup"><span data-stu-id="8ea90-137">Enhancements-</span></span>
- <span data-ttu-id="8ea90-138">Oracle havuz, HDFS kaynak için performans geliştirmesi.</span><span class="sxs-lookup"><span data-stu-id="8ea90-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="8ea90-139">Ağ geçidi işleme kapasitesi paralel hata düzeltmesi için ağ geçidi otomatik güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="8ea90-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="8ea90-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="8ea90-141">Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-141">Enhancements</span></span>
- <span data-ttu-id="8ea90-142">Daha güçlü ve geliştirilmiş ağ geçidi kayıt deneyimi hello kayıt deneyimi daha iyi yanıt kılan hello ağ geçidi kayıt işlemi sırasında ilerleme durumunu izleyebilirsiniz artık-.</span><span class="sxs-lookup"><span data-stu-id="8ea90-142">Improved and more robust Gateway registration experience- Now you can track progress status during hello Gateway registration process, which makes hello registration experience more responsive.</span></span>
- <span data-ttu-id="8ea90-143">Bu güncelleştirme ile Merhaba ağ geçidi yedekleme dosyası yoksa bile gelişme ağ geçidi geri yükleme işlem, ağ geçidi kurtarmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ea90-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have hello gateway backup file with this update.</span></span> <span data-ttu-id="8ea90-144">Bu, Portal tooreset bağlantılı hizmet kimlik bilgileri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8ea90-144">This would require you tooreset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="8ea90-145">Hata düzeltmesi.</span><span class="sxs-lookup"><span data-stu-id="8ea90-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="8ea90-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="8ea90-147">Yenilikler</span><span class="sxs-lookup"><span data-stu-id="8ea90-147">What’s new</span></span>

- <span data-ttu-id="8ea90-148">Şimdi veri kaynağı kimlik bilgileri yerel olarak depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ea90-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="8ea90-149">Merhaba kimlik bilgileri şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="8ea90-149">hello credentials are encrypted.</span></span> <span data-ttu-id="8ea90-150">Merhaba veri kaynağı kimlik bilgileri kurtarılabilir ve ağ geçidi, tüm şirket içi varolan hello aktarılabilir hello yedekleme dosyasını kullanarak geri.</span><span class="sxs-lookup"><span data-stu-id="8ea90-150">hello data source credentials can be recovered and restored using hello backup file that can be exported from hello existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="8ea90-151">Geliştirmeler-</span><span class="sxs-lookup"><span data-stu-id="8ea90-151">Enhancements-</span></span>

- <span data-ttu-id="8ea90-152">Geliştirilmiş ve daha sağlam ağ geçidi kayıt deneyimi.</span><span class="sxs-lookup"><span data-stu-id="8ea90-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="8ea90-153">Otomatik algılama quotechar özelliğine yapılandırmasının Kopyalama Sihirbazı'nı metin biçiminde destek ve hello geliştirmek genel, algılama doğruluğu biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="8ea90-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve hello overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="8ea90-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="8ea90-154">2.3.6100.2</span></span>

- <span data-ttu-id="8ea90-155">Metin dosyaları kopyalama Sihirbazı'nda firstRowAsHeader ve SkipLineCount otomatik algılama şirket içi dosya sistemi ve HDFS'i destekler.</span><span class="sxs-lookup"><span data-stu-id="8ea90-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="8ea90-156">Ağ geçidi ile Service Bus arasındaki ağ bağlantısının Hello kararlılığını geliştirmek</span><span class="sxs-lookup"><span data-stu-id="8ea90-156">Enhance hello stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="8ea90-157">Birkaç hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="8ea90-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-158">2.2.6072.1</span></span>

*  <span data-ttu-id="8ea90-159">Merhaba ağ geçidi Yapılandırma Yöneticisi'ni kullanarak hello ağ geçidi için HTTP proxy ayarını destekler.</span><span class="sxs-lookup"><span data-stu-id="8ea90-159">Supports setting HTTP proxy for hello gateway using hello Gateway Configuration Manager.</span></span> <span data-ttu-id="8ea90-160">Yapılandırılmışsa, Azure Blob, Azure Table, Azure Data Lake ve belge DB HTTP proxy üzerinden erişilir.</span><span class="sxs-lookup"><span data-stu-id="8ea90-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="8ea90-161">TextFormat için veri kopyalama işlemi sırasında işleme destekler üstbilgi / tooAzure Blob, Azure Data Lake Store, şirket içi dosya sistemi ve şirket içi HDFS.</span><span class="sxs-lookup"><span data-stu-id="8ea90-161">Supports header handling for TextFormat when copying data from/tooAzure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="8ea90-162">Veri ekleme Blob ve sayfa blobu hello birlikte zaten kopyalama destekler blok blobu desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8ea90-162">Supports copying data from Append Blob and Page Blob along with hello already supported Block Blob.</span></span>
*  <span data-ttu-id="8ea90-163">Yeni bir ağ geçidi durumu tanıtır **çevrimiçi (sınırlı)**, o hello ana işlevlerini hello ağ geçidi belirten çalışır hello etkileşimli işlemi Kopyalama Sihirbazı'nı desteği dışında.</span><span class="sxs-lookup"><span data-stu-id="8ea90-163">Introduces a new gateway status **Online (Limited)**, which indicates that hello main functionality of hello gateway works except hello interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="8ea90-164">Kayıt anahtarı kullanarak ağ geçidi kaydı Hello sağlamlık geliştirir.</span><span class="sxs-lookup"><span data-stu-id="8ea90-164">Enhances hello robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="8ea90-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="8ea90-165">2.1.6040.</span></span>

*  <span data-ttu-id="8ea90-166">DB2 sürücüsü hello ağ geçidi yükleme paketini artık dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8ea90-166">DB2 driver is included in hello gateway installation package now.</span></span> <span data-ttu-id="8ea90-167">Tooinstall gerekmez, ayrı olarak.</span><span class="sxs-lookup"><span data-stu-id="8ea90-167">You do not need tooinstall it separately.</span></span>
*  <span data-ttu-id="8ea90-168">DB2 sürücüsü artık destekliyor z/OS ve DB2 için t (AS / 400) zaten desteklenen hello platformlar (Linux, Unix ve Windows) ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="8ea90-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with hello platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="8ea90-169">Azure Cosmos DB şirket içi veri depoları için bir kaynak veya hedef olarak kullanılmasını destekler</span><span class="sxs-lookup"><span data-stu-id="8ea90-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="8ea90-170">Merhaba birlikte veri öğesinden/toocold/hot blob depolama zaten kopyalama destekler, genel amaçlı depolama hesabı desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="8ea90-170">Supports copying data from/toocold/hot blob storage along with hello already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="8ea90-171">Tooconnect tooon içi sağlayan uzak oturum açma ayrıcalıklarına sahip ağ geçidi üzerinden SQL Server'a.</span><span class="sxs-lookup"><span data-stu-id="8ea90-171">Allows you tooconnect tooon-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="8ea90-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-172">2.0.6013.1</span></span>

*  <span data-ttu-id="8ea90-173">El ile yükleme sırasında bir ağ geçidi tarafından kullanılan hello dil/kültür toobe seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ea90-173">You can select hello language/culture toobe used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="8ea90-174">Ağ geçidi beklendiği gibi çalışmaz, son yedi gün tooMicrosoft toofacilitate hello sorun giderme toosend gateway günlükleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ea90-174">When gateway does not work as expected, you can choose toosend gateway logs of last seven days tooMicrosoft toofacilitate troubleshooting of hello issue.</span></span> <span data-ttu-id="8ea90-175">Ağ geçidi değilse bağlı toohello bulut hizmeti, toosave seçin ve ağ geçidi günlüklerini arşivleyin.</span><span class="sxs-lookup"><span data-stu-id="8ea90-175">If gateway is not connected toohello cloud service, you can choose toosave and archive gateway logs.</span></span>  

*  <span data-ttu-id="8ea90-176">Ağ geçidi Yapılandırma Yöneticisi için kullanıcı arabirimi iyileştirmeleri:</span><span class="sxs-lookup"><span data-stu-id="8ea90-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="8ea90-177">Ağ geçidi durumu daha görünür hello Giriş sekmesinde yapın.</span><span class="sxs-lookup"><span data-stu-id="8ea90-177">Make gateway status more visible on hello Home tab.</span></span>

    *  <span data-ttu-id="8ea90-178">Yeniden düzenlenen ve Basitleştirilmiş denetler.</span><span class="sxs-lookup"><span data-stu-id="8ea90-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="8ea90-179">Hello kullanarak bir depolama biriminden veri kopyalayabilirsiniz [Kodsuz kopya önizleme aracını](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8ea90-179">You can copy data from a storage using hello [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="8ea90-180">Bkz: [hazırlanan kopyalama](data-factory-copy-activity-performance.md#staged-copy) bu hakkındaki ayrıntılar için özelliklere genel.</span><span class="sxs-lookup"><span data-stu-id="8ea90-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="8ea90-181">Veri Yönetimi ağ geçidi tooingress verileri doğrudan bir şirket içi SQL Server veritabanını Azure Machine Learning kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ea90-181">You can use Data Management Gateway tooingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="8ea90-182">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-182">Performance improvements</span></span>

    * <span data-ttu-id="8ea90-183">Şema/Önizleme SQL sunucusuna karşı Kodsuz kopyalama Önizleme aracında görüntüleme performansı.</span><span class="sxs-lookup"><span data-stu-id="8ea90-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="8ea90-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-184">1.12.5953.1</span></span>

*  <span data-ttu-id="8ea90-185">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="8ea90-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-186">1.11.5918.1</span></span>

*  <span data-ttu-id="8ea90-187">Merhaba ağ geçidi olay günlüğünün en büyük boyutu 1 MB too40 MB'den çıkarılmıştır.</span><span class="sxs-lookup"><span data-stu-id="8ea90-187">Maximum size of hello gateway event log has been increased from 1 MB too40 MB.</span></span>

*  <span data-ttu-id="8ea90-188">Ağ geçidi otomatik güncelleştirme sırasında yeniden başlatma gerektiğinde bir uyarı iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8ea90-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="8ea90-189">Sonra ya da daha sonra toorestart sağ seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ea90-189">You can choose toorestart right then or later.</span></span>

*  <span data-ttu-id="8ea90-190">Otomatik güncelleştirme başarısız olursa, otomatik güncelleştirme en fazla üç kez konumundaki ağ geçidi yükleyicisi yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="8ea90-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="8ea90-191">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-191">Performance improvements</span></span>

    * <span data-ttu-id="8ea90-192">Şirket içi sunucudan Kodsuz kopyalama senaryosu büyük tabloları yüklenmesi için performansı.</span><span class="sxs-lookup"><span data-stu-id="8ea90-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="8ea90-193">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="8ea90-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-194">1.10.5892.1</span></span>

*  <span data-ttu-id="8ea90-195">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-195">Performance improvements</span></span>

*  <span data-ttu-id="8ea90-196">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="8ea90-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="8ea90-197">1.9.5865.2</span></span>

*  <span data-ttu-id="8ea90-198">Sıfır dokunma otomatik güncelleştirme özelliği</span><span class="sxs-lookup"><span data-stu-id="8ea90-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="8ea90-199">Ağ geçidi Durum göstergeleri ile yeni Tepsi simgesi</span><span class="sxs-lookup"><span data-stu-id="8ea90-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="8ea90-200">Özelliği çok "güncelleştir şimdi" Merhaba istemciden</span><span class="sxs-lookup"><span data-stu-id="8ea90-200">Ability too“Update now” from hello client</span></span>
*  <span data-ttu-id="8ea90-201">Özelliği tooset güncelleştirme zamanlama süresi</span><span class="sxs-lookup"><span data-stu-id="8ea90-201">Ability tooset update schedule time</span></span>
*  <span data-ttu-id="8ea90-202">Otomatik güncelleştirmeyi Aç/Kapat geçiş için PowerShell Betiği</span><span class="sxs-lookup"><span data-stu-id="8ea90-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="8ea90-203">JSON biçimi desteği</span><span class="sxs-lookup"><span data-stu-id="8ea90-203">Support for JSON format</span></span>  
*  <span data-ttu-id="8ea90-204">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-204">Performance improvements</span></span>
*  <span data-ttu-id="8ea90-205">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="8ea90-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-206">1.8.5822.1</span></span>

*  <span data-ttu-id="8ea90-207">Sorun giderme deneyimini geliştirmeye</span><span class="sxs-lookup"><span data-stu-id="8ea90-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="8ea90-208">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-208">Performance improvements</span></span>
*  <span data-ttu-id="8ea90-209">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="8ea90-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-210">1.7.5795.1</span></span>

*  <span data-ttu-id="8ea90-211">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-211">Performance improvements</span></span>
*  <span data-ttu-id="8ea90-212">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="8ea90-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-213">1.7.5764.1</span></span>

*  <span data-ttu-id="8ea90-214">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-214">Performance improvements</span></span>
*  <span data-ttu-id="8ea90-215">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="8ea90-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-216">1.6.5735.1</span></span>

*  <span data-ttu-id="8ea90-217">Şirket içi HDFS kaynak/havuz desteği</span><span class="sxs-lookup"><span data-stu-id="8ea90-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="8ea90-218">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-218">Performance improvements</span></span>
*  <span data-ttu-id="8ea90-219">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="8ea90-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-220">1.6.5696.1</span></span>

*  <span data-ttu-id="8ea90-221">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-221">Performance improvements</span></span>
*  <span data-ttu-id="8ea90-222">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="8ea90-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-223">1.6.5676.1</span></span>

*  <span data-ttu-id="8ea90-224">Configuration Manager Destek Tanılama araçları</span><span class="sxs-lookup"><span data-stu-id="8ea90-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="8ea90-225">Tablo sütunları tablo veri kaynakları için Azure Data Factory için destek.</span><span class="sxs-lookup"><span data-stu-id="8ea90-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="8ea90-226">Azure Data Factory SQL DW desteği</span><span class="sxs-lookup"><span data-stu-id="8ea90-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="8ea90-227">Azure veri fabrikası için BlobSource ve FileSource Reclusive desteği</span><span class="sxs-lookup"><span data-stu-id="8ea90-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="8ea90-228">Destek CopyBehavior – MergeFiles, PreserveHierarchy ve BlobSink ve Azure veri fabrikası için ikili kopyayla FileSink FlattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="8ea90-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="8ea90-229">Kopya etkinliği Azure Data Factory için ilerleme durumu raporlama desteği</span><span class="sxs-lookup"><span data-stu-id="8ea90-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="8ea90-230">Azure veri fabrikası için destek veri kaynağı bağlantısı doğrulama</span><span class="sxs-lookup"><span data-stu-id="8ea90-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="8ea90-231">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="8ea90-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-232">1.6.5672.1</span></span>

*  <span data-ttu-id="8ea90-233">ODBC veri kaynağı için tablo adı için Azure Data Factory destek</span><span class="sxs-lookup"><span data-stu-id="8ea90-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="8ea90-234">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-234">Performance improvements</span></span>
*  <span data-ttu-id="8ea90-235">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="8ea90-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-236">1.6.5658.1</span></span>

*  <span data-ttu-id="8ea90-237">Destek dosyası havuz için Azure veri fabrikası</span><span class="sxs-lookup"><span data-stu-id="8ea90-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="8ea90-238">Hiyerarşi için Azure Data Factory ikili kopyasında koruma desteği</span><span class="sxs-lookup"><span data-stu-id="8ea90-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="8ea90-239">Azure veri fabrikası için kopyalama etkinliği benzersizlik desteği</span><span class="sxs-lookup"><span data-stu-id="8ea90-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="8ea90-240">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="8ea90-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-241">1.6.5640.1</span></span>

*  <span data-ttu-id="8ea90-242">3 daha fazla veri kaynakları (ODBC, OData, HDFS) Azure Data Factory için destek</span><span class="sxs-lookup"><span data-stu-id="8ea90-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="8ea90-243">Azure Data Factory için csv ayrıştırıcısını tırnak işareti karakteri desteği</span><span class="sxs-lookup"><span data-stu-id="8ea90-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="8ea90-244">Sıkıştırma desteği (Bzıp2)</span><span class="sxs-lookup"><span data-stu-id="8ea90-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="8ea90-245">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="8ea90-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-246">1.5.5612.1</span></span>

*  <span data-ttu-id="8ea90-247">Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata ve Sybase) için beş ilişkisel veritabanlarını destekler</span><span class="sxs-lookup"><span data-stu-id="8ea90-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="8ea90-248">Sıkıştırma desteği (Gzip ve Deflate)</span><span class="sxs-lookup"><span data-stu-id="8ea90-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="8ea90-249">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-249">Performance improvements</span></span>
*  <span data-ttu-id="8ea90-250">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="8ea90-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-251">1.4.5549.1</span></span>

*  <span data-ttu-id="8ea90-252">Azure Data Factory için Oracle veri kaynağı destek ekleme</span><span class="sxs-lookup"><span data-stu-id="8ea90-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="8ea90-253">Performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-253">Performance improvements</span></span>
*  <span data-ttu-id="8ea90-254">Hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="8ea90-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="8ea90-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-255">1.4.5492.1</span></span>

*  <span data-ttu-id="8ea90-256">Microsoft Azure veri fabrikası ve Office 365 Power BI hizmetlerini destekleyen birleşik ikili</span><span class="sxs-lookup"><span data-stu-id="8ea90-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="8ea90-257">Merhaba yapılandırma kullanıcı Arabirimi ve kayıt işlemini daraltın</span><span class="sxs-lookup"><span data-stu-id="8ea90-257">Refine hello Configuration UI and registration process</span></span>
*  <span data-ttu-id="8ea90-258">Azure Data Factory – Azure giriş ve çıkış desteklemek için SQL Server veri kaynağı</span><span class="sxs-lookup"><span data-stu-id="8ea90-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="8ea90-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="8ea90-259">1.2.5303.1</span></span>

*  <span data-ttu-id="8ea90-260">Zaman aşımı sorunu toosupport daha uzun süren veri kaynağı bağlantılarını düzeltin.</span><span class="sxs-lookup"><span data-stu-id="8ea90-260">Fix timeout issue toosupport more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="8ea90-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="8ea90-261">1.1.5526.8</span></span>

*  <span data-ttu-id="8ea90-262">.NET Framework 4.5.1 Kurulum sırasında bir önkoşul olarak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8ea90-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="8ea90-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="8ea90-263">1.0.5144.2</span></span>

*  <span data-ttu-id="8ea90-264">Azure Data Factory senaryoları etkileyen değişiklik yok.</span><span class="sxs-lookup"><span data-stu-id="8ea90-264">No changes that affect Azure Data Factory scenarios.</span></span>
