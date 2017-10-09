---
title: "kişisel veri raporlama araçları Azure ile aaaDocument koruma | Microsoft Docs"
description: "nasıl toouse Azure Raporlama Hizmetleri ve teknolojileriyle toohelp kişisel verilerin gizliliği koruyun."
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 3230d26ed308a8a0e72421c001793be06334a7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a>Kişisel veri raporlama araçları Azure ile belge koruması

Bu makalede Azure raporlama toouse hizmetleri nasıl ele alınacaktır ve teknolojileri toohelp kişisel verilerin gizliliği koruyun.

## <a name="scenario"></a>Senaryo

Merhaba Amerika Birleşik Devletleri'nde yönetim büyük seyahat şirket, kendi işlemleri toooffer programlarıyla hello Akdeniz, Adriatic ve Baltık seas yanı sıra hello İngiliz Adaları arasında içinde genişletmektedir. toohelp bu çaba İtalya, dayanarak birkaç küçük seyahat satırları geçirmiş Almanya, Danimarka ve hello İngiltere

Merhaba şirket işleme ve şirket verilerinin depolanması için Microsoft Azure kullanır. Bu ad, adres, telefon numaraları gibi kişisel olarak tanımlanabilir bilgileri ve genel müşteri tabanı, kredi kartı bilgilerini içerir. Ayrıca tüm konumlarda adresleri, telefon numaralarını, vergi kimlik numaraları ve şirket çalışanlarının tıbbi bilgi gibi geleneksel İnsan Kaynakları bilgileri içerir. Merhaba seyahat satır Ayrıca, kişisel bilgi tootrack ilişkileri geçerli ve geçmiş müşterilerle içeren büyük bir veritabanını ödül ve bağlılık programı üyeleri korur.

Şirket çalışanları erişim hello ağdan hello şirketin şubelere ve seyahat aracılar bulunan Merhaba Dünya toosome şirket kaynaklarına sahip.

## <a name="problem-statement"></a>Sorun bildirimi

Hello şirket Azure yönetim ve güvenlik özellikleri tooimpose katı denetimlere erişim tooand kişisel verilerin işlenmesini kullanan ve olmalıdır çok katmanlı güvenlik stratejisi çalışanların ve müşterilerin kişisel verilerine hello gizliliğini korumak gerekir mümkün toodemonstrate kendi koruyucu ölçer toointernal ve dış denetçileridir.

## <a name="company-goal"></a>Şirket hedefi

Kendi savunma güvenlik stratejisinin bir parçası olarak şirket hedef tootrack tüm erişim tooand kişisel verilerin işlemesidir ve kişisel veriler için yeterli gizlilik korumaları belgelerine yer ve çalışır durumda olduğundan emin olun.

## <a name="solutions"></a>Çözümler

Microsoft Azure kapsamlı izleme, günlüğe kaydetme sağlar ve tanılama araçları toohelp izlemek ve etkinlikleri ve erişme ve kişisel veriler, veri ve üçüncü taraf erişim toopersonal veri coğrafi akış işleme ile ilişkili olayları kaydeder. Merhaba bulutta kişisel verilerin güvenliğini paylaşılan sorumluluk olduğundan, Microsoft müşterilerle da sağlar:

- Müşterilerin veri kendi işleme hakkında ayrıntılı bilgi

- Güvenlik önlemleri Microsoft tarafından yönetilen

- Nerede ve nasıl müşterilerin verileri gönderir.

- Microsoft'un kendi gizlilik incelemeler işleminin ayrıntıları

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) Microsoft'un bulut tabanlı, çok kiracılı dizin ve kimlik yönetimi hizmetidir. Hizmetin oturum açma hello ve ayrıntılı oturum açma ve izleyebilir ve uygun erişim toocustomers ve çalışanların kişisel verilerini sağlamak uygulama kullanım etkinlik bilgi toohelp ile denetim raporlama özellikleri, sağlayın.

Etkinlik raporları iki tür vardır:

- Merhaba [denetim etkinlik raporları/günlükleri](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) sistem etkinlikler/görevleri ayrıntılı bir kayıt sağlayın

- Merhaba [gerçekleştirilen oturum açma etkinliği raporu/log](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) hello denetim raporunda listelenen her etkinliği gerçekleştiren gösterir

Merhaba iki birlikte kullanarak, her görevin gerçekleştirilmesi hello geçmişini ve her gerçekleştiren izleyebilirsiniz. Raporlar her iki tür özelleştirilebilir ve filtre uygulanabilir.

#### <a name="how-do-i-access-hello-audit-and-security-logs"></a>Ne erişebilirim hello denetleme ve güvenlik günlüklerini?

Merhaba denetim ve güvenlik günlüklerini hello Active Directory portalından üç farklı yolla erişilebilir: hello aracılığıyla **etkinlik** bölümüne (ya da seçin **denetim günlüklerini** veya **oturum açma işlemleri**), veya **kullanıcılar ve gruplar** veya **kurumsal uygulamalar** altında **Yönet** Active Directory'de. Raporlar ayrıca hello Azure Active Directory erişilebilir raporlama API'si. 

1. Hello Azure portal, seçin **Azure Active Directory.**

2. Merhaba, **etkinlik** bölümünde, select **denetim günlükleri.**

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. Tıklayarak Hello liste görünümü özelleştirmek **sütunları** hello araç.

4.  Bir öğe hakkındaki tüm kullanılabilir ayrıntıları hello liste görünümü toosee seçin.

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

Azure Active Directory raporlama de iki tür güvenlik raporları içerir **bayrak eklenen kullanıcılar için risk** ve **riskli oturum açma işlemleri**, hangi yardımcı olabilir, Azure ortamınızda olası riskleri izleyin.

Hizmet raporlama hello hakkında daha fazla bilgi için bkz: [Azure Active Directory raporlama](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)

Ziyaret [Azure Active Directory etkinlik raporları](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) hello Azure Active Directory içinde kullanılabilir raporlar hakkında daha fazla ayrıntı için. Bu site nasıl hakkında daha fazla ayrıntı içeren tooaccess ve [denetim günlüklerini etkinlik raporları](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) ve [oturum açma etkinliği raporları](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) hello Portalı'nda. Hakkında bilgiler de içerir [bayrak eklenen kullanıcılar için risk](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) ve [riskli oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins) güvenlik raporları.

Merhaba ziyaret [Azure Active Directory denetim API Başvurusu](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) hakkında daha fazla bilgi için site tooconnect tooAzure dizin programlı olarak raporlama.

### <a name="log-analytics"></a>Log Analytics

[Günlük analizi](https://azure.microsoft.com/services/log-analytics/) yapabilirsiniz [Azure İzleyicisi'nden veri toplama](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) toocorrelate, diğer verilerle ve ek çözümleme sağlar. Azure İzleyici toplar ve Azure ortamınız için izleme verilerini analiz eder. 

Tüm ortamınız merkezi analizini sağlayan tüm toplanan verileri karşı günlük analizi analiz araçları günlük aramalar, görünümler ve çözümleri gibi çalışır. Günlük analizi toplamak ve Windows olay günlükleri, IIS günlüklerini ve kişisel veri toounauthorized kullanıcıları maruz bırakabileceğinden olası kişisel veriler ihlallerini belirlemenize yardımcı olabilir Syslog modüllerini analiz edin.

#### <a name="how-do-i-use-log-analytics"></a>Günlük analizi nasıl kullanabilirim?

Günlük analizi hello OMS portalı veya hello Azure portalından, herhangi bir web tarayıcısı üzerinden erişebilirsiniz. Günlük analizi sorgu dili tooquickly alma içerir ve hello deposundaki verileri birleştiremedi. Oluşturma ve günlük aramaları toodirectly hello Portalı'nda veri analiz edin.

toocreate hello Azure portal, günlük analizi çalışma hello aşağıdaki:

1. Seçin **günlük analizi** hello Market Hizmetleri'nde hello listesinden.

2. Seçin **oluşturun,** sonra OMS çalışma hello adını belirtin, abonelik, kaynak grubu, konum seçin ve fiyatlandırma katmanı.

3. Tıklatın **Tamam** toodisplay alanlarınızı listesi.

4. Bir çalışma alanı toosee ayrıntılarını seçin.

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

Merhaba ziyaret [günlük analizi belgeleri](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) toolearn hello hizmeti hakkında daha fazla.

Merhaba ziyaret [günlük analizi çalışma alanı ile çalışmaya başlama](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) öğretici toocreate bir değerlendirme çalışma ve nasıl toouse hello hizmet hello temellerini öğrenin.

Yukarıda açıklanan tooconnect toouse günlük analizi hello ile nasıl oturum açtığında Web sayfaları daha ayrıntılı bilgi için aşağıdaki hello ziyaret edin:

[Windows olay günlüklerini veri kaynaklarında, günlük analizi](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[IIS günlük analizi günlüğe kaydeder](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[Syslog veri kaynaklarında günlük analizi](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a>Azure İzleyici/Azure etkinlik günlüğü 

[Azure İzleyici](https://azure.microsoft.com/services/monitor/) taban düzeyi altyapı ölçümleri ve günlükleri çoğu Microsoft Azure hizmetlerini sağlar.
İzleme Azure uygulamalarınızı hakkında ayrıntılı Öngörüler toogain yardımcı olabilir. Azure İzleyici çoğu uygulama düzeyindeki ölçümlerini ve günlükleri toplamak için hello Azure tanılama uzantısını (Windows veya Linux) kullanır. [Hello Azure etkinlik günlüğü](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) hello kaynakları Azure İzleyicisi ile görüntüleyebilirsiniz biridir. Her API çağrısı izler ve bol miktarda oluşan etkinlikleri hakkında bilgi sağlayan [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).
Hello Azure altyapısı tarafından görülen, kaynak hakkında bilgi için hello etkinlik günlüğü (daha önce işlemsel veya denetim günlüklerini denir) arayabilirsiniz. 

Merhaba bilgilerin büyük bölümünü kaydedilen rağmen hello etkinlik günlüğü tooperformance ve hizmet sistem durumu ilgilidir, verilerin ilgili tooprotection bilgileri bulunmaktadır. Merhaba etkinlik günlüğü kullanarak hello belirleyebilirsiniz "ne, kim, ne zaman ve" herhangi bir yazma işlemleri (PUT, POST, DELETE) Azure aboneliğinizde hello kaynaklar üzerinde gerçekleştirilecek için.

Örneğin, yönetici hello koruma kişisel verilerin etkileyebilir bir ağ güvenlik grubu sildiğinde bir kaydı sağlar. Etkinlik günlüğü girişleri Azure İzleyicisi'nde 90 gün süreyle depolanır.

#### <a name="how-do-i-use-hello-data-collected-by-azure-monitor"></a>Azure İzleyici tarafından toplanan hello verileri nasıl kullanabilirim?

Yolları toouse hello veri hello etkinlik günlüğünde sayısı ve diğer Azure İzleyici kaynaklar vardır.

- Merhaba veri tooother konumları gerçek satırında akışını sağlayabilirsiniz.

- Kullanarak hello Varsayılanları daha uzun süreler için hello veri depolayabilirsiniz bir [Azure depolama hesabı](https://docs.microsoft.com/azure/storage/common/storage-introduction) ve bir bekletme ilkesi ayarlama.

- Hello kullanarak visual hello veri grafikleri ve grafikler, yapabilirsiniz [Azure portal](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), veya üçüncü taraf görselleştirme araçları.

- Hello Azure İzleyici REST API'si, CLI komutları kullanarak hello verileri sorgulayabilir [PowerShell](https://docs.microsoft.com/powershell/) cmdlet'lerini veya .NET SDK'sı hello.

Azure İzleyici ile başlatıldı tooget seçin **daha Hizmetleri** hello Azure Portalı'nda.

1. Çok ilerleyin**İzleyici** hello içinde **izleme ve yönetme** bölümü.

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  İzleyici açar hello **etkinlik günlüğü** görünümü.

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

Oluşturun ve her zaman Ölçütünüzle eşleşen olaylar meydana gelmiş bilirsiniz ortak filtreleri sonra PIN hello en önemli sorguları tooa portal panosu için sorgular kaydedin.

1. Kaynak grubu, timespan ve olay kategorisi hello görünümünü filtreleyebilirsiniz.

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. Merhaba tıklayarak sonra sorguları tooa portalı panosunun sabitleyebilirsiniz **PIN** düğmesi. Bu bilgi işlem verilerini için tek bir kaynağı hizmetlerinizi üzerinde oluşturmanıza yardımcı olur. Merhaba sorgu adı ve sonuç sayısı hello panosunda görüntülenir.

Merhaba İzleyici tooview ölçümleri tüm Azure kaynakları için kullandığınız, tanılama ayarları ve Uyarıları yapılandırmak ve hello günlüğünde arayın. Toouse hello Azure İzleyici ve etkinlik günlüğü nasıl görürüm hakkında daha fazla bilgi için [Azure İzleyicisi ile çalışmaya başlama](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).

### <a name="azure-diagnostics"></a>Azure Tanılama 

azure'da Hello tanılama yeteneği çeşitli kaynaklardan veri koleksiyonunu sağlar. Merhaba güvenlik günlüğü dahil, hello Windows olay günlükleri, izleme ve kişisel verilere yönelik korumayı belgeleme özellikle yararlı olabilir. Merhaba güvenlik günlüğü oturum açma başarılı ve başarısız olaylar yanı sıra izin değişiklikleri, belirli türde bir saldırıları, güvenlikle ilgili ilkelerini yapılan değişiklikler, güvenlik grubu üyeliği değişiklikleri ve daha fazlasını belirten desenleri algılanması izler.

Örneğin, olay kimliği 4695, çalıştı toohello unprotection denetlenebilir korunan verilerin uyarır. Bu toohello özel anahtarlar, depolanan kimlik bilgileri ve diğer gizli bilgileri gibi tooprotect verileri yardımcı olan veri koruma API'ne (DPAPI) içindir.

#### <a name="how-do-i-enable-hello-diagnostics-extension-for-windows-vms"></a>Windows VM'ler için nasıl hello tanılama uzantısını etkinleştirilsin mi?

Bir Windows VM için PowerShell tooenable hello tanılama uzantısını toocollect günlük verileri olarak şekilde kullanabilirsiniz. Bunu yapmak için hello adımlar hangi dağıtım modeline (Resource Manager veya Klasik) kullandığınız bağlıdır. tooenable hello tanılama uzantısını hello Resource Manager dağıtım modeli oluşturulmuş mevcut bir VM'yi, kullanabileceğiniz hello [Set-AzureRMVMDiagnosticsExtension PowerShell cmdlet'ini](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1).

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

*\$diagnosticsconfig_path* içeren hello tanılama yapılandırması XML hello yolu toohello dosyasıdır. Daha ayrıntılı bir VM'de Azure tanılama etkinleştirme yönergeleri için bkz: [Windows çalıştıran bir sanal makinede kullan PowerShell tooenable Azure tanılama.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)

Hello Azure tanılama uzantısını hello toplanan verileri tooan Azure depolama hesabı aktarın veya Application Insights gibi tooservices gönderin. Merhaba veri denetimi için daha sonra kullanabilirsiniz.

#### <a name="how-do-i-store-and-view-diagnostic-data"></a>Nasıl depolamak ve tanılama verilerini görüntüleme?

Önemli tooremember olan Tanılama verileri toohello, Microsoft Azure depolama öykünücüsü ya da tooAzure depolama aktarım sürece kalıcı olarak depolanmaz. Azure Storage toostore ve görünüm Tanılama verileri şu adımları izleyin:

1. Merhaba ServiceConfiguration.cscfg dosyasında bir depolama hesabı belirtin. Azure tanılama hello Blob hizmeti veya hello tablo hizmeti veri hello türüne bağlı olarak kullanabilirsiniz. Windows olay günlükleri, tablo biçiminde depolanır.

2. Merhaba veri aktarın. Merhaba yapılandırma dosyası aracılığıyla tootransfer hello tanılama veri isteyebilir. SDK 2.4 ve önceki, hello isteği program aracılığıyla da yapabilirsiniz.

3. Kullanarak hello verileri görüntüleme [Azure Storage Gezgini](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer), [Sunucu Gezgini](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) Visual Studio'da veya [Azure tanılama Manager](https://www.cerebrata.com/products/azure-diagnostics-manager) Azure Management Studio'da.

Hakkında daha fazla bilgi için bkz tooperform her bu adımları [deposu ve görünüm Tanılama verileri Azure depolama.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)

### <a name="azure-storage-analytics"></a>Azure Depolama Analizi 

Storage Analytics başarılı ve başarısız istekleri tooa depolama birimi hizmeti hakkındaki ayrıntılı bilgileri kaydeder. Bu bilgiler hello hizmetinde depolanan toopersonal verilere erişmek belgeleme yardımcı olabilecek kullanılan toomonitor tek tek isteklerin olabilir. Ancak, depolama çözümlemeleri günlüğü depolama hesabınız için varsayılan olarak etkin değildir. Hello Azure portal etkinleştirebilirsiniz.

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a>İçin bir depolama hesabı izleme nasıl yapılandırabilirim?

bir depolama hesabı için tooconfigure izleme hello aşağıdaki:

1. Seçin **depolama hesapları** hello Azure portal, ardından hello hesabın toomonitor hello adını seçin.

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. Merhaba, **izleme** bölümünde, select **tanılama.**

3.  Select hello **türü** ölçümleri verilerin her hizmet için (Blob, tablo, dosyası) toomonitor istiyor. tooinstruct Azure Storage toosave tanılama günlükleri okuma, yazma ve silme istekleri için hello blob, tablo ve kuyruk hizmetleri seçin **Blob günlükleri, tablo günlükleri** ve **sıraya günlükleri.**

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. Merhaba altındaki Hello kaydırıcıyı kullanarak hello ayarlayın **bekletme** İlkesi gün (1-365 değeri). Merhaba varsayılan yedi gündür.

5. Seçin **kaydetmek** tooapply hello yapılandırma ayarları.

Depolama günlük günlük girişlerinin bireysel istekler hakkında bilgi aşağıdaki hello içerir:

- Başlangıç saati, uçtan uca gecikme süresi ve sunucu gecikme süresi gibi zamanlama bilgileri.

- Merhaba depolama işlemi hello işlem türü gibi ayrıntılarını, hello hello depolama nesnesi hello istemcisinin erişme, başarı veya başarısızlık ve toohello istemci döndürülen hello HTTP durum kodu anahtardır.

- Kullanılan kimlik doğrulama hello istemci hello türü gibi kimlik doğrulama ayrıntıları.

- Merhaba ETag değeri ve en son değiştirilen zaman damgası gibi bilgileri eşzamanlılık.

- Merhaba boyutları hello istek ve yanıt iletileri.

Daha ayrıntılı yönergeler için günlüğe kaydetme, depolama çözümlemeleri tooenable bakın [hello Azure portalında bir depolama hesabında izleyin.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)

### <a name="azure-security-center"></a>Azure Güvenlik Merkezi 

[Azure Güvenlik Merkezi](https://azure.microsoft.com/services/security-center/) izleyiciler hello Azure kaynaklarınızı sipariş tooprevent güvenlik durumunu ve tehditleri algılayabilir ve yanıtlamak için öneriler sağlar. Bu çeşitli şekillerde toohelp belge kişisel veriler hello gizliliğini korumak için güvenlik önlemleri sağlar.

Güvenlik durumunu izleme, güvenlik ilkeleriyle uyumluluğunu olmanıza yardımcı olur. Güvenlik İzleme, kuruluş standartlarıyla veya en iyi yöntemler karşılamayan kaynakları tooidentify sistemlerinizi denetimleri öngörülü bir stratejiye olur. Kaynakları aşağıdaki hello hello güvenlik durumunu izleyebilirsiniz:

- İşlem (sanal makineler ve bulut Hizmetleri)

- Ağ (sanal ağlar)

- Depolama ve verileri (sunucu ve veritabanı denetim ve tehdit algılama, TDE, depolama şifrelemesi)

- Uygulamaları (olası güvenlik sorunlarını)

Aşağıdaki kategorilerden herhangi birinde bulunan güvenlik sorunlarını kişisel verilerin bir tehdit toohello gizliliği tehlikeli olabilecek.

#### <a name="how-do-i-view-hello-security-state-of-my-azure-resources"></a>Azure Kaynaklarım hello güvenlik durumunu nasıl görüntüleyebilirim?

Güvenlik Merkezi düzenli aralıklarla hello Azure kaynaklarınızın güvenlik durumunu çözümler. Hello tanımladığı olası güvenlik açıkları görüntüleyebilirsiniz **önleme** başlangıç Panosu bölümü.

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. Merhaba, **önleme** bölümü, select hello **işlem** döşeme. Burada görürsünüz bir **genel bakış,** hello birlikte **sanal makineleri** tüm sanal makineleri ve güvenlik durumlarını ve hello **bulut hizmetlerini** web ve çalışan rolleri listesi Güvenlik Merkezi tarafından izlenen.

2. Merhaba üzerinde **genel bakış** sekmesinde, daha fazla bilgi bir öneri tooview ikinci.

3. Merhaba üzerinde **sanal makineleri** sekmesinde, bir VM tooview ek Ayrıntılar'ı seçin.

Veri toplamayı Azure Güvenlik Merkezi'nde etkinleştirildiğinde, tüm mevcut hello Microsoft Monitoring Agent otomatik olarak hazırlanmıştır ve desteklenen herhangi bir yeni dağıtılan sanal makineler. Bu Aracıdan toplanan verileri ya da var olan içinde depolanan [günlük analizi](https://azure.microsoft.com/services/log-analytics/) aboneliğinizi veya yeni bir çalışma alanı ile ilişkili çalışma.

[Tehdit yönetim bilgileri raporları](https://docs.microsoft.com/azure/security-center/security-center-threat-report) Güvenlik Merkezi tarafından sağlanır. Bunlar toohelp keşfedilir hello saldırganın kimlik, hedefler, geçerli ve geçmiş saldırı kampanyaları ve taktiği, araçları ve kullanılan yordamlar yararlı bilgiler verir. Azaltma ve düzeltme bilgileri de eklenmiştir.

Bu tehdit raporların Hello birincil amacı olan toohelp, toorespond etkili bir şekilde toohello hemen tehdit ve Yardım Al toomitigate hello sorunu daha sonra ölçer. Raporlama ve denetim amacıyla, olay yanıtlama belgelerken hello bilgi hello raporlarında da yararlı olabilir.

Merhaba tehdit yönetim bilgileri raporları sunulur. Merhaba bulunan bir bağlantı üzerinden erişilen, PDF biçimli **raporları** hello alanını **yürütülen şüpheli işlem** Azure Güvenlik Merkezi'nde her güvenlik uyarısı için dikey.

Nasıl tooview ve kullanım tehdit Intelligence rapor hello daha fazla bilgi için bkz: [Azure Güvenlik Merkezi tehdit Intelligence rapor.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

## <a name="next-steps"></a>Sonraki Adımlar:

[Hello Azure Active Directory raporlama API'si ile çalışmaya başlama](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[Log Analytics nedir?](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[Microsoft Azure'da İzlemeye Genel Bakış](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[Giriş toohello Azure etkinlik günlüğü (video)](https://azure.microsoft.com/resources/videos/intro-activity-log/)
