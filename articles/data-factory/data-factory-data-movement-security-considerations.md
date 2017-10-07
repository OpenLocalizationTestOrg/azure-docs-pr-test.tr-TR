---
title: "Azure Data factory'de veri taşımayı aaaSecurity dikkate alınacak noktalar | Microsoft Docs"
description: "Azure Data factory'de veri taşımayı güvenliğini sağlama hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 4bfce8884df14ad5b94e28ad3dfcf7025e2130a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---security-considerations-for-data-movement"></a>Azure Data Factory - veri taşıma için güvenlik konuları
## <a name="introduction"></a>Giriş
Bu makalede Azure Data Factory veri taşıma hizmetleri verilerinizi toosecure kullanan temel güvenlik altyapısı açıklanmaktadır. Azure veri fabrikası yönetim kaynakları Azure güvenlik altyapı üzerine kurulmuş ve Azure tarafından sunulan tüm olası güvenlik önlemleri kullanın.

Bir Data Factory çözümünde bir veya daha fazla [işlem hattı](data-factory-create-pipelines.md) oluşturursunuz. İşlem hattı, bir araya geldiğinde bir görev gerçekleştiren mantıksal etkinlik grubudur. Bu ardışık düzen hello veri fabrikası oluşturulduğu hello bölgede yer alır. 

Data Factory yalnızca kullanılabilir olsa bile **Batı ABD**, **Doğu ABD**, ve **Kuzey Avrupa** bölgeler, hello veri taşıma hizmeti kullanılabilir [içinde genel olarak birkaç bölgeleri](data-factory-data-movement-activities.md#global). Data Factory hizmeti sağlar veri coğrafi bölgeye bırakmaz / bölge açıkça toplamasını sürece hello hizmet toouse alternatif bir bölge hello veri taşıma hizmeti değilse toothat Bölge henüz dağıtılmamış. 

Azure Data Factory'nin kendisi sertifikalar kullanılarak şifrelenmiş bulut veri depoları için bağlı hizmet kimlik bilgilerini dışında herhangi bir veriyi depolamaz. Veri temelli iş akışlarını arasında veri tooorchestrate hareketini oluşturmanızı sağlar [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) ve verileri kullanarak işleme [işlem Hizmetleri](data-factory-compute-linked-services.md) başka bölgelerde veya şirket içi ortam. Ayrıca çok tanır[izlemek ve iş akışlarını yönetme](data-factory-monitor-manage-pipelines.md) programlı her ikisini kullanarak kullanıcı Arabirimi mekanizmalarını.

Azure Data Factory kullanarak veri taşıma süredir **sertifikalı** için:
-   [HIPAA/HITECH](https://www.microsoft.com/en-us/trustcenter/Compliance/HIPAA)  
-   [ISO/IEC 27001](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27001)  
-   [ISO/IEC 27018](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27018) 
-   [CSA YILDIZ](https://www.microsoft.com/en-us/trustcenter/Compliance/CSA-STAR-Certification)
     
Azure uyumluluk ve Azure kendi altyapısını nasıl korur ilgileniyorsanız hello ziyaret [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx). 

Bu makalede, iki veri taşıma senaryoları aşağıdaki hello güvenlik konuları inceleyin: 

- **Bulut senaryosu**-Bu senaryoda, hem kaynak hem de hedef Internet üzerinden genel olarak erişilebilir. Bunlar Azure Storage, Azure SQL Data Warehouse, Azure SQL Database, Azure Data Lake Store, Amazon S3, Amazon Redshift Salesforce gibi SaaS Hizmetleri ve FTP ve OData gibi web protokoller gibi yönetilen bulut depolama hizmetlerine içerir. Desteklenen veri kaynaklarının tam listesi bulabilirsiniz [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats).
- **Karma senaryo**- Bu senaryoda, kaynak veya hedef bir güvenlik duvarı ardında veya bir şirket içi Kurumsal ağa veya hello içindeki verileri deposu özel bir ağda / sanal ağ (çoğunlukla hello kaynağı) ve genel olarak erişilebilir değil . Sanal makineler üzerinde barındırılan veritabanı sunucularını da bu senaryoya ayrılır.

## <a name="cloud-scenarios"></a>Bulut senaryoları
###<a name="securing-data-store-credentials"></a>Veri deposu kimlik güvenliğini sağlama
Azure Data Factory ile veri deposu kimlik bilgilerinizi korur **şifreleme** kullanarak bunları **Microsoft tarafından yönetilen sertifikaları**. Bu sertifikalar Döndürülmüş her **iki yıllık** (içeren sertifikanın yenilenmesini ve kimlik bilgilerini geçişini). Bu şifrelenmiş kimlik bilgileri güvenli bir şekilde depolanır bir **Azure Storage, Azure Data Factory Yönetim Hizmetleri tarafından yönetilen**. Azure Storage güvenliği hakkında daha fazla bilgi için bkz [Azure depolama güvenliğine genel bakış](../security/security-storage-overview.md).

### <a name="data-encryption-in-transit"></a>Aktarımdaki verileri şifreleme
Merhaba bulut veri deposu HTTPS veya TLS destekliyorsa, tüm veri aktarımlarını veri fabrikasında veri taşıma hizmetleri arasında ve bir bulut veri deposu olan güvenli kanal HTTPS veya TLS.

> [!NOTE]
> Tüm bağlantılar çok**Azure SQL veritabanı** ve **Azure SQL Data Warehouse** transit tooand hello veritabanından veri olarak kullanılırken her zaman şifreleme (SSL/TLS) gerektirir. Bir JSON Düzenleyicisi'ni kullanarak bir işlem hattı yazarken hello eklemek **şifreleme** özelliği ve çok ayarlayın**true** hello içinde **bağlantı dizesi**. Merhaba kullandığınızda [Kopyalama Sihirbazı'nı](data-factory-azure-copy-wizard.md), Başlangıç Sihirbazı'nı bu özellik varsayılan olarak ayarlar. İçin **Azure Storage**, kullanabileceğiniz **HTTPS** hello bağlantı dizesinde.

### <a name="data-encryption-at-rest"></a>Bekleme sırasında veri şifrelemesi
Rest verileri destek şifrelenmesi bazı verileri depolar. Bu veri depoları için veri şifreleme mekanizması etkinleştirmenizi öneririz. 

#### <a name="azure-sql-data-warehouse"></a>Azure SQL Veri Ambarı
Azure SQL Data warehouse'da saydam veri şifreleme (TDE) kötü amaçlı etkinliği hello tehdide karşı gerçek zamanlı şifreleme ve şifre çözme REST verilerinizin gerçekleştirerek ile korumaya yardımcı olur. Bu davranış saydam toohello istemcidir. Daha fazla bilgi için bkz: [SQL veri ambarı veritabanında güvenli](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md).

#### <a name="azure-sql-database"></a>Azure SQL Database
Azure SQL veritabanı, gerçek zamanlı şifreleme ve şifre çözme hello veri değişiklikleri toohello uygulama gerek kalmadan gerçekleştirerek kötü amaçlı etkinliği hello tehdide karşı koruma ile yardımcı olan, saydam veri şifreleme (TDE) da destekler. Bu davranış saydam toohello istemcidir. Daha fazla bilgi için bkz: [saydam veri şifrelemesi ile Azure SQL veritabanı](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database). 

#### <a name="azure-data-lake-store"></a>Azure Data Lake Store
Azure Data Lake store ayrıca hello hesabında depolanan veriler için şifreleme sağlar. Etkinleştirildiğinde, Data Lake store, otomatik olarak devam ettirmeden önce verileri şifreler ve hello verilere erişme saydam toohello istemci yaparak alma önce şifresini çözer. Daha fazla bilgi için bkz: [Azure Data Lake Store'da güvenlik](../data-lake-store/data-lake-store-security-overview.md). 

#### <a name="azure-blob-storage-and-azure-table-storage"></a>Azure Blob Depolama ve Azure tablo depolaması
Azure Blob Depolama ve Azure Table storage kalıcı toostorage önce verilerinizi ve alma önce şifrelerinin çözülmesi otomatik olarak şifreler depolama hizmeti Şifrelemesi'ne (SSE) destekler. Daha fazla bilgi için bkz: [bekleyen veri için Azure depolama hizmeti şifrelemesi](../storage/common/storage-service-encryption.md).

#### <a name="amazon-s3"></a>Amazon S3
Amazon S3 REST verilerin istemci ve sunucu şifrelenmesini destekler. Daha fazla bilgi için bkz: [koruma verileri kullanarak şifreleme](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingEncryption.html). Şu anda, veri fabrikası sanal özel bulut (VPC) içinde Amazon S3 desteklemiyor.

#### <a name="amazon-redshift"></a>Amazon Redshift
Amazon Redshift küme şifreleme bekleyen veri için destekler. Daha fazla bilgi için bkz: [Amazon Redshift veritabanı şifreleme](http://docs.aws.amazon.com/redshift/latest/mgmt/working-with-db-encryption.html). Şu anda, veri fabrikası Amazon Redshift bir VPC içinde desteklemiyor. 

#### <a name="salesforce"></a>Salesforce
Salesforce Shield Platform şifreleme'de, tüm dosyaları ekler, özel alanlar şifrelemeye izin destekler. Daha fazla bilgi için bkz: [anlama hello Web sunucusu OAuth kimlik doğrulama akışı](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_web_server_oauth_flow.htm).  

## <a name="hybrid-scenarios-using-data-management-gateway"></a>Karma senaryolar (veri yönetimi ağ geçidi kullanarak)
Karma senaryolar bir şirket ağında veya bir sanal ağ (Azure) veya bir sanal özel bulut (Amazon) içinde yüklü veri yönetimi ağ geçidi toobe gerektirir. Merhaba ağ geçidi mümkün tooaccess hello yerel veri depolarına olması gerekir. Merhaba ağ geçidi hakkında daha fazla bilgi için bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md). 

![Veri Yönetimi ağ geçidi kanalları](media/data-factory-data-movement-security-considerations/data-management-gateway-channels.png)

Merhaba **komut kanalı** veri fabrikasında veri taşıma hizmetleri ve veri yönetimi ağ geçidi arasında iletişime olanak sağlar. Merhaba iletişim bilgilerini içeren ilgili toohello etkinlik. Merhaba veri kanalı, şirket içi veri depoları ve bulut veri depoları arasında veri aktarımı için kullanılır.    

### <a name="on-premises-data-store-credentials"></a>Şirket içi veri deposu kimlik
Şirket içi veri depolarına Hello kimlik bilgileri yerel olarak depolanır (bulutta olmayan hello). Üç farklı yolla ayarlanabilir. 

- Kullanarak **düz metin** (daha az güvenli) Azure portalından HTTPS üzerinden / Kopyalama Sihirbazı. Merhaba kimlik bilgileri düz metin toohello şirket içi ağ geçidi aktarılır.
- Kullanarak **JavaScript şifreleme Kopyalama Sihirbazı'nı kitaplıktan**.
- Kullanarak **tıklatın-kimlik bilgileri Yöneticisi uygulamasının temel sonra**. Merhaba tıklatın-sonra uygulama erişim toohello ağ geçidi ve hello veri deposu için kimlik bilgilerini ayarlar hello şirket içi makinede yürütür. Bu seçenek ve hello sonraki bir olan en güvenli seçenekleri hello. Merhaba kimlik bilgisi Yöneticisi uygulama, varsayılan olarak, güvenli iletişim için ağ geçidi ile Merhaba makinedeki hello bağlantı noktası 8050 kullanır.  
- Kullanım [yeni AzureRmDataFactoryEncryptValue](/powershell/module/azurerm.datafactories/New-AzureRmDataFactoryEncryptValue) PowerShell cmdlet tooencrypt kimlik bilgileri. Merhaba cmdlet hello sertifikasını bu ağ geçidi yapılandırılmış toouse tooencrypt hello kimlik bilgilerini kullanır. Bu cmdlet tarafından döndürülen şifreli hello kimlik bilgilerini kullanın ve çok eklemek**EncryptedCredential** hello öğesinin **connectionString** hello ile kullandığınız hello JSON dosyasında [ AzureRmDataFactoryLinkedService yeni](/powershell/module/azurerm.datafactories/new-azurermdatafactorylinkedservice) cmdlet'ini veya hello Portal'daki Data Factory Düzenleyici hello hello JSON parçacığında. Bu seçenek ve hello tıklatın-uygulama olduktan sonra hello en güvenli seçenekleri. 

#### <a name="javascript-cryptography-library-based-encryption"></a>JavaScript şifreleme kitaplığı tabanlı şifreleme
Veri deposu kimlik bilgilerini kullanarak şifreleyebilirsiniz [JavaScript şifreleme Kitaplığı](https://www.microsoft.com/download/details.aspx?id=52439) hello gelen [Kopyalama Sihirbazı'nı](data-factory-copy-wizard.md). Bu seçeneği belirlediğinizde, hello Kopyalama Sihirbazı'nı ağ geçidi hello ortak anahtarını alır ve tooencrypt hello veri deposu kimlik kullanır. Merhaba kimlik hello ağ geçidi makinesi tarafından şifresi çözülür ve Windows tarafından korunan [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx).

**Desteklenen tarayıcılar:** IE8, IE9, ıe10, IE11, Microsoft Edge ve en son Firefox, Chrome, Opera, Safari tarayıcı. 

#### <a name="click-once-credentials-manager-app"></a>Tıklatın-bir kez kimlik bilgileri Yöneticisi uygulama
Merhaba tıklatın başlatabilirsiniz-ardışık düzen yazarken kimlik bilgisi Yöneticisi uygulamasından Azure portal/Kopyalama Sihirbazı'nı temel sonra. Bu uygulama kimlik bilgileri düz metin olarak hello kablo üzerinden aktarılmayan sağlar. Varsayılan olarak, başlangıç bağlantı noktası kullanır **8050** makinede hello ağ geçidi ile güvenli iletişim için. Gerekirse, bu bağlantı noktası değiştirilebilir.  
  
![Merhaba ağ geçidi için HTTPS bağlantı noktası](media/data-factory-data-movement-security-considerations/https-port-for-gateway.png)

Şu anda veri yönetimi ağ geçidi tek bir kullanır **sertifika**. Bu sertifika hello ağ geçidi yükleme işlemi sırasında oluşturulan (Yönetimi ağ geçidi Kasım 2016 sonrasında oluşturulan tooData ve sürüm 2.4.xxxx.x uygulanır veya üstü). Bu sertifika, kendi SSL/TLS sertifika ile değiştirebilir. Bu sertifika hello tıklatın tarafından kullanılan-kimlik bilgisi Yöneticisi uygulama toosecurely bağlandıktan sonra veri deposu kimlik bilgilerini ayarlamak için toohello ağ geçidi makinesi. Verilerini depolayan depolama kimlik bilgileri güvenli bir şekilde şirket içi hello Windows kullanarak [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx) hello makinede ağ geçidi ile. 

> [!NOTE]
> Kasım 2016 önce veya sürüm 2.3.xxxx.x yüklenmiş olan eski ağ geçitleri şifrelenir ve bulutta depolanan kimlik bilgileri toouse devam edin. Merhaba ağ geçidi toohello en son sürümüne yükseltmek olsa bile hello kimlik geçirilen tooan şirket içi makineyi olup olmadığı    
  
| Ağ geçidi sürümü (sırasında oluşturma) | Depolanan kimlik bilgileri | Kimlik bilgisi şifreleme / güvenlik | 
| --------------------------------- | ------------------ | --------- |  
| < 2.3.xxxx.x = | Bulutta | Sertifika (Merhaba bir kimlik bilgisi Yöneticisi uygulama tarafından kullanılan farklı) kullanılarak şifrelenir | 
| > = 2.4.xxxx.x | Şirket içinde | DPAPI güvenli | 
  

### <a name="encryption-in-transit"></a>Aktarımdaki şifreleme
Tüm veri aktarımlarını güvenli kanal olan **HTTPS** ve **TLS üzerinden TCP** tooprevent man-in--middle saldırıları Azure Hizmetleri ile iletişim sırasında.
 
Aynı zamanda [IPSec VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md) veya [hızlı rota](../expressroute/expressroute-introduction.md) toofurther güvenli hello iletişim kanalını şirket içi ağınız ve Azure arasında.

Sanal ağ hello bulut ağınızdaki mantıksal bir gösterimidir. IPSec VPN (siteden siteye) veya hızlı rota (özel eşleme) ayarlayarak bir şirket içi ağ tooyour Azure sanal ağı (VNet) bağlanabilir       

Merhaba aşağıdaki tabloda karma veri taşıma için kaynak ve hedef konumların farklı birleşimlerine göre hello ağ ve ağ geçidi yapılandırması önerileri özetler.

| Kaynak | Hedef | Ağ yapılandırması | Ağ geçidi Kurulumu |
| ------ | ----------- | --------------------- | ------------- | 
| Şirket içi | Sanal makineler ve sanal ağlarda dağıtılan bulut Hizmetleri | IPSec VPN (noktadan siteye veya siteden siteye) | Ağ geçidi olabilir ya da şirket içi yüklü veya bir Azure sanal üzerinde (VM) içinde sanal makine | 
| Şirket içi | Sanal makineler ve sanal ağlarda dağıtılan bulut Hizmetleri | ExpressRoute (özel eşleme) | Ağ geçidi olabilir ya da şirket içi yüklü veya bir Azure VM VNet içinde | 
| Şirket içi | Genel bir uç nokta sahip azure tabanlı Hizmetleri | ExpressRoute (ortak eşleme) | Ağ geçidi içi yüklü olması gerekir | 

Merhaba aşağıdaki görüntüleri hello kullanım veri yönetimi ağ geçidi şirket içi veritabanı ile hızlı rota ve IPSec VPN (ile sanal ağ) kullanarak Azure hizmetleri arasında veri taşımak için Göster:

**Hızlı rota:**
 
![Expressroute ağ geçidi ile kullanma](media/data-factory-data-movement-security-considerations/express-route-for-gateway.png) 

**IPSec VPN:**

![IPSec VPN ağ geçidi ile](media/data-factory-data-movement-security-considerations/ipsec-vpn-for-gateway.png)

### <a name="firewall-configurations-and-whitelisting-ip-address-of-gateway"></a>Güvenlik duvarı yapılandırmaları ve ağ geçidi uygulamaları güvenilir listeye almayı IP adresi

#### <a name="firewall-requirements-for-on-premisesprivate-network"></a>Şirket içi/özel ağ için güvenlik duvarı gereksinimleri  
Bir kuruluşta bir **Kurumsal Güvenlik Duvarı** hello merkezi hello kuruluş yönlendiricisinde çalıştırır. Ve **Windows Güvenlik Duvarı** ağ geçidinin hangi hello üzerinde yüklü hello yerel makinede bir arka plan programı gibi çalışır. 

Merhaba aşağıdaki tabloda verilmiştir **giden bağlantı noktası** ve etki alanı gereksinimleri hello için **Kurumsal Güvenlik Duvarı**.

| Etki alanı adları | Giden bağlantı noktaları | Açıklama |
| ------------ | -------------- | ----------- | 
| `*.servicebus.windows.net` | 443, 80 | Merhaba ağ geçidi tooconnect toodata taşıma hizmetleri veri fabrikası'nda gerekli |
| `*.core.windows.net` | 443 | Merhaba kullandığınızda hello ağ geçidi tooconnect tooAzure depolama hesabı tarafından kullanılan [kopyalama hazırlanan](data-factory-copy-activity-performance.md#staged-copy) özelliği. | 
| `*.frontend.clouddatahub.net` | 443 | Merhaba ağ geçidi tooconnect toohello Azure Data Factory hizmeti tarafından gerekli. | 
| `*.database.windows.net` | 1433   | (İsteğe bağlı) gerekli Hedefinizi Azure SQL veritabanı olduğunda / Azure SQL veri ambarı. Kullanım hello hello 1433 numaralı bağlantı noktasını açmaya gerek kalmadan kopyalama özelliği toocopy veri tooAzure SQL veritabanı/Azure SQL Data Warehouse hazırlanır. | 
| `*.azuredatalakestore.net` | 443 | (İsteğe bağlı), hedef Azure Data Lake deposu olduğunda gerekli | 

> [!NOTE] 
> Toomanage bağlantı noktaları olabilir / uygulamaları güvenilir listeye almayı etki alanları, gerekli olarak kurumsal güvenlik duvarı düzeyi ilgili veri kaynakları tarafından hello. Bu tablo yalnızca Azure SQL Database, Azure SQL Data Warehouse, Azure Data Lake Store örnek olarak kullanır.   

Merhaba aşağıdaki tabloda verilmiştir **gelen bağlantı noktası** hello gereksinimleri **windows güvenlik duvarı**.

| Gelen bağlantı noktaları | Açıklama | 
| ------------- | ----------- | 
| 8050 (TCP) | Merhaba kimlik bilgisi Yöneticisi uygulama toosecurely kimlik bilgilerinin ayarlanması için şirket içi veri depolarına hello ağ geçidinde gerekli. | 

![Ağ geçidi bağlantı noktası gereksinimleri](media\data-factory-data-movement-security-considerations/gateway-port-requirements.png) 

#### <a name="ip-configurations-whitelisting-in-data-store"></a>IP yapılandırmaları / uygulamaları güvenilir listeye almayı veri deposu
Bazı veri depolarına hello bulutta ayrıca erişmesini hello makinenin IP adresinin uygulamaları güvenilir listeye almayı gerektirir. Başlangıç IP adresi hello ağ geçidi makinesinin Güvenilenler listesine / Güvenlik Duvarı'nda uygun şekilde yapılandırılmış emin olun.

Merhaba aşağıdaki bulut veri depolarına hello ağ geçidi makinenin IP adresinin uygulamaları güvenilir listeye almayı gerektirir. Varsayılan olarak, bu veri depolarına bazıları uygulamaları güvenilir listeye almayı hello IP adresinin gerektirmeyebilir. 

- [Azure SQL Veritabanı](../sql-database/sql-database-firewall-configure.md) 
- [Azure SQL Veri Ambarı](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal)
- [Azure Data Lake Store](../data-lake-store/data-lake-store-secure-data.md#set-ip-address-range-for-data-access)
- [Azure Cosmos DB](../documentdb/documentdb-firewall-support.md)
- [Amazon Redshift](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) 

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

**Soru:** hello ağ geçidi farklı veri fabrikaları arasında paylaşılabilir?
**Yanıt:** bu özellik bir henüz desteklemiyoruz. Etkin olarak üzerinde çalışıyoruz.

**Soru:** hello ağ geçidi toowork hello bağlantı noktası gereksinimleri nelerdir?
**Yanıt:** ağ geçidi yapar HTTP tabanlı bağlantılar tooopen Internet. Merhaba **giden bağlantı noktası 443 ve 80** için ağ geçidi toomake bu bağlantının açılması gerekir. Açık **gelen bağlantı noktası 8050** yalnızca düzeyinde hello makine (düzeyinde Kurumsal güvenlik duvarı) için kimlik bilgisi Yöneticisi uygulaması. Azure SQL Database veya Azure SQL Data Warehouse kullanılıyorsa olarak kaynak / hedef, sonra gerek tooopen **1433** de bağlantı noktası. Daha fazla bilgi için bkz: [güvenlik duvarı yapılandırmaları ve uygulamaları güvenilir listeye almayı IP adreslerini](#firewall-configurations-and-whitelisting-ip-address-of gateway) bölümü. 

**Soru:** ağ geçidi için sertifika gereksinimleri nelerdir?
**Yanıt:** geçerli ağ geçidi hello kimlik bilgisi Yöneticisi uygulaması tarafından veri deposu kimlik güvenli bir şekilde ayarlamak için kullanılan bir sertifika gerektirir. Bu sertifika oluşturduktan ve yapılandırdıktan hello ağ geçidi kurulum tarafından otomatik olarak imzalanan bir sertifikadır. Kendi TLS kullanabilir / SSL sertifika yerine. Daha fazla bilgi için bkz: [tıklatın-manager uygulamasını bir kez kimlik bilgisi](#click-once-credentials-manager-app) bölümü. 

## <a name="next-steps"></a>Sonraki adımlar
Kopya etkinliği performansının hakkında daha fazla bilgi için bkz: [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md).

 
