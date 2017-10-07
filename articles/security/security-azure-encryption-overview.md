---
title: "aaaAzure şifreleme genel bakış | Microsoft Docs"
description: "Azure içindeki çeşitli şifreleme seçenekleri hakkında bilgi edinin"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/18/2017
ms.author: barclayn
ms.openlocfilehash: ef9ab46de32b857e99e8fe628a61386b95cf197f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-overview"></a>Azure şifreleme genel bakış

Bu makalede, şifreleme Microsoft Azure'da nasıl kullanıldığını genel bir bakış sağlar. Bekleyen şifreleme, şifreleme uçuş ve anahtar kasası ile anahtar yönetimi dahil olmak üzere şifreleme hello temel alanları kapsamaktadır. Her bölüm daha ayrıntılı bilgi için bağlantılar içerir.

## <a name="encryption-of-data-at-rest"></a>Bekleyen verilerin şifrelenmesi

Rest verileri dijital biçimi fiziksel medyada kalıcı depolama alanında bulunan bilgileri içerir. Bu, manyetik veya optik medya, arşivlenen verileri ve veri yedeklemeleri dosyalarını içerir. Microsoft Azure veri depolama çözümleri toomeet çeşitli dosya, disk, blob ve tablo depolama da dahil olmak üzere farklı gereksinimleri sunar. Microsoft ayrıca şifreleme tooprotect sağlar [Azure SQL veritabanı](../sql-database/sql-database-technical-overview.md), [CosmosDB](../cosmos-db/introduction.md)ve Azure Data Lake.

Bekleyen verileri şifreleme kullanılabilir hizmetler için hello Azure yazılım olarak-hizmet (SaaS)-olarak-hizmet Platform (PaaS) ve altyapı olarak-hizmet (Iaas) bulut modeller. Bu belge özetler ve kaynakları toohelp sağlayan Azure'nın şifreleme seçenekleri kullanın.

Rest verileri Azure'da nasıl şifrelenir, tartışma ayrıntılı için başlıklı hello belgesine bakın [Azure veri şifreleme çalışmıyorken-](azure-security-encryption-atrest.md)

## <a name="azure-encryption-models"></a>Azure şifreleme modelleri

Azure hizmet tarafından yönetilen tuşlarını kullanarak, müşteri tarafından yönetilen anahtarları Azure anahtar kasası veya müşteri tarafından yönetilen anahtarları müşteri tarafından denetlenen donanımda kullanarak sunucu tarafı şifreleme dahil olmak üzere çeşitli şifreleme modellerini destekler. İstemci tarafı şifreleme toomanage ve depolama anahtarları şirket içi veya başka bir programda konumu güvenli sağlar.

### <a name="client-side-encryption"></a>İstemci Tarafında Şifreleme

İstemci tarafı şifreleme Azure dışında gerçekleştirilir. İstemci tarafı şifreleme içerir:

- Merhaba Müşteri'nin veri merkezinde çalışan bir uygulama tarafından veya bir hizmet uygulaması tarafından şifrelenmiş verileri
- Azure tarafından alındığında zaten şifrelenmiş veriler.

İstemci tarafı şifreleme ile Merhaba bulut hizmeti sağlayıcısı erişim toohello şifreleme anahtarları yoktur ve bu verilerin şifresini çözemez. Merhaba anahtarların tam denetimi korumak.

### <a name="server-side-encryption"></a>Sunucu tarafı şifreleme

Merhaba üç sunucu tarafı şifreleme modeli gereksinimlerinizi seçilebilir farklı anahtar yönetimi özellikleri sunar.

- **Hizmet tarafından yönetilen anahtarları** denetim ve kullanışlı bir bileşimini düşük yükü ile sağlayın

- **Müşteri tarafından yönetilen anahtarları** kendi anahtarları (BYOK) veya yenilerini toogenerate hello özelliği toobring dahil olmak üzere hello anahtarları üzerinde denetim sağlar.

- **Ccustomer controlledhardware hizmeti yönetilen anahtarlarında** toomanage anahtarları, Microsoft'un denetimi dışında olan özel deponuzun sağlar. Bu ana bilgisayarınızı kendi anahtarını Taşı (HYOK) denir. Ancak, yapılandırma karmaşıktır ve çoğu Azure Hizmetleri bu modeli desteklemez.

### <a name="azure-disk-encryption"></a>Azure Disk Şifrelemesi

Windows ve Linux sanal makineleri kullanarak korunabilir [Azure Disk şifrelemesi](azure-security-disk-encryption.md), hello kullanan [Windows BitLocker](https://technet.microsoft.com/library/cc766295(v=ws.10).aspx) teknolojisi ve Linux [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) tooprotect işletim sistemi disklerinde ve tam birim şifrelemesi ile veri diskleri için.

Şifreleme anahtarları ve gizli anahtarları içinde korunması, [Azure anahtar kasası](../key-vault/key-vault-whatis.md) abonelik. Yedekleme ve hello Azure Yedekleme hizmetini kullanarak hello KEK yapılandırmayla şifrelenmiş şifrelenmiş VM'ler geri yükleyebilirsiniz.

### <a name="azure-storage-service-encryption"></a>Azure depolama hizmeti şifrelemesi

Veri deposunda kalan Azure (hem Blob hem de dosya), sunucu tarafı ve istemci tarafı senaryolarda şifrelenebilir.

[Azure depolama hizmeti şifrelemesi](../storage/storage-service-encryption.md) (SSE) otomatik olarak şifreleme veri önce depolanır ve bunu, tamamen saydam kullanıcılar işlem hello yapmadan almak zaman, otomatik olarak çözer. Depolama hizmeti şifrelemesi kullanır 256 bit [AES şifreleme](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), hangi hello güçlü blok şifrelemeler biridir ve şifreleme, şifre çözme ve anahtar yönetimi saydam bir şekilde işler.

### <a name="client-side-encryption-of-azure-blobs"></a>İstemci tarafı şifreleme Azure BLOB

İstemci tarafı şifreleme Azure BLOB farklı şekillerde gerçekleştirilebilir.

İstemci, uygulamaları önceki toouploading içinde hello Azure Storage istemci kitaplığı için .NET NuGet paketi tooencrypt verileri kullanabilirsiniz, tooAzure depolama.

toolearn hakkında daha fazla bilgi ve .NET NuGet paketi için yükleme hello Azure Storage istemci kitaplığı Bkz başlıklı hello belge [Windows Azure depolama 8.3.0](https://www.nuget.org/packages/WindowsAzure.Storage)

İstemci tarafı şifreleme Azure anahtar kasası ile kullandığınızda, verilerinizi bir kerelik simetrik içerik şifreleme anahtarı (hello Azure Storage istemci SDK'sı tarafından oluşturulan CEK) kullanılarak şifrelenir. Merhaba CEK, bir simetrik anahtar veya asimetrik anahtar çifti olabilen anahtar şifreleme anahtarı (KEK) kullanılarak şifrelenir. Yerel olarak yönetin veya Azure anahtar kasası depolar. Merhaba şifrelenmiş verileri ise tooAzure depolama birimi hizmeti karşıya yüklendi.

Azure anahtar kasası ile istemci tarafı şifreleme hakkında daha fazla toolearn ve nasıl tooinstructions ile çalışmaya başlama, başlıklı hello belgesine bakın [Öğreticisi: şifrelemek ve şifresini çözmek Azure anahtar kasası kullanılarak Microsoft Azure Storage blobları](../storage/storage-encrypt-decrypt-blobs-key-vault.md)

Son olarak, veri tooAzure depolama ve toodecrypt hello veri toohello istemci yüklerken karşıya yüklemeden önce Java tooperform istemci tarafı şifreleme için hello Azure Storage istemci kitaplığı kullanabilirsiniz. Bu kitaplığı ile tümleştirme de destekler [Azure anahtar kasası](https://azure.microsoft.com/services/key-vault/) depolama hesabı anahtarı yönetimi için.

### <a name="encryption-of-data-at-rest-with-azure-sql-database"></a>Azure SQL Database rest verileri şifreleme

[Azure SQL veritabanı](../sql-database/sql-database-technical-overview.md) bir ilişkisel veri, uzamsal, JSON ve XML gibi yapıları destekleyen Microsoft Azure genel amaçlı ilişkisel veritabanı hizmetidir. Azure SQL sunucu tarafı şifreleme hello saydam veri şifreleme (TDE) özelliği aracılığıyla ve istemci tarafı şifreleme hello her zaman şifreli özelliği aracılığıyla destekler.

#### <a name="transparent-data-encryption"></a>Saydam veri şifrelemesi

[TDE saydam veri şifreleme](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) kullanılan tooencrypt olan [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016), [Azure SQL veritabanı](../sql-database/sql-database-technical-overview.md), ve [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) gerçek zamanlı veri dosyaları Kullanılabilirlik hello veritabanı önyükleme kaydının Kurtarma sırasında depolanan bir veritabanı şifreleme anahtarı (DEK) kullanıyor.

TDE, AES ve 3DES şifreleme algoritmaları kullanarak veri ve günlük dosyalarını korur. Şifreleme hello veritabanı dosyasının hello sayfa düzeyinde gerçekleştirilir; şifrelenmiş bir veritabanı Hello sayfalarında toodisk yazılmadan önce şifrelenir ve belleğe okurken, şifresi çözülür. TDE, artık yeni oluşturulan Azure SQL veritabanı üzerinde varsayılan olarak etkindir.

#### <a name="always-encrypted"></a>Always encrypted

Merhaba [her zaman şifreli](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) Özelliği Azure SQL Azure SQL veritabanında istemci uygulamaları önceki toostoring içinde tooencrypt veri sağlar ve şirket içi veritabanı yönetim toothird tooenable temsilcisi sağlar taraflarla ve kullanıcılar kendi ve hello verileri ve yönetme ancak erişim tooit sahip olmaması gereken olanlar görüntüleyebilir arasında ayrım korumak.

#### <a name="cellcolumn-level-encryption"></a>Hücre/sütun düzeyinde şifreleme

Azure SQL Database Transact-SQL kullanarak veri tooapply simetrik şifreleme tooa sütununu sağlar. Bu adlı [düzeyinde şifreleme veya sütun düzeyinde şifreleme hücre](https://docs.microsoft.com/sql/relational-databases/security/encryption/encrypt-a-column-of-data) (Temizle) olduğundan bunu tooencrypt belirli sütunları veya hatta belirli hücreleri verilerin farklı şifreleme anahtarları ile kullanabilirsiniz. Bu sayfa verileri şifreler TDE'den daha ayrıntılı şifreleme özelliği sağlar.

Temizle simetrik ya da asimetrik anahtarlar, bir sertifikanın ortak anahtarının hello veya 3DES kullanılarak bir parola kullanarak tooencrypt veri kullanabileceğiniz yerleşik işlevler vardır.

### <a name="cosmos-db-database-encryption"></a>Cosmos DB veritabanı şifreleme

[Azure Cosmos DB](../cosmos-db/database-encryption-at-rest.md) Microsoft'un Genel dağıtılmış birden çok model veritabanıdır. Cosmos DB'de geçici olmayan depolama (katı hal sürücüsü) depolanan kullanıcı verileri varsayılan olarak şifrelenir; hiçbir denetimleri tooturn vardır ya da devre dışı. Bekleyen şifreleme, güvenli anahtar depolama sistemleri, şifrelenmiş ağlar ve şifreleme API'leri dahil güvenlik teknolojileri çeşitli kullanılarak uygulanır. Şifreleme anahtarları, Microsoft tarafından yönetilir ve Microsoft'un iç yönergelerine göre döndürülür.

### <a name="at-rest-encryption-in-azure-data-lake"></a>Azure Data Lake çalışmıyorken şifreleme

[Azure Data Lake](../data-lake-store/data-lake-store-encryption.md) bir kuruluş genelinde her veri türü bir tek konumdan önceki tooany resmi tanımında gereksinimleri veya şema toplanan deposudur. Azure Data Lake Store destekler "üzerinde varsayılan olarak," hesabınızı hello oluşturma sırasında ayarlanan bekleyen verilerin saydam şifreleme. Varsayılan olarak, Data Lake Store hello anahtarları tarafından yönetilir ancak hello seçeneği toomanage sahip bunları kendiniz.

Üç tür anahtarlarını, şifreleme ve verilerin şifresini çözmek kullanılır: ana şifreleme anahtarı (MEK), veri şifreleme anahtarı (DEK) ve blok şifreleme anahtarı (BEK) hello. Merhaba MEK kullanılan tooencrypt hello kalıcı medyada depolanır, DEK olan ve hello BEK hello DEK ve hello veri bloğu türetilir. Kendi anahtarları yönetiyorsanız, hello MEK döndürebilirsiniz.

## <a name="encryption-of-data-in-transit"></a>Aktarımdaki verileri şifreleme

Azure tek bir konumda tooanother hareket ederken verileri gizliliğini korumak için birçok mekanizma sunar.

### <a name="tlsssl-encryption-in-azure"></a>TLS/SSL şifreleme Azure

Microsoft kullanır hello [Aktarım Katmanı Güvenliği](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) protokol tooprotect veri hello bulut Hizmetleri ile müşterileri arasında seyahat halindeyken. Microsoft'un veri merkezlerinin tooAzure Hizmetleri bağlanan istemci sistemleri TLS bağlantıyla anlaşmaları. TLS, güçlü kimlik doğrulaması, ileti gizliliği ve bütünlük (ileti oynama, kişiler tarafından ele ve sahtekarlığı saptama etkinleştirme), birlikte çalışabilirlik, algoritma esnekliği, dağıtım ve kullanım kolaylığı sağlar.

[Kusursuz iletme gizliliği](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) olan müşterilerin istemci sistemleri ve Microsoft'un bulut hizmetleri arasında bağlantılar benzersiz anahtarlara göre korur. Bağlantıları da RSA tabanlı 2.048 bit şifreleme anahtar uzunluklarını kullanın. Bu birleşim birisi için aktarım sırasında toointercept ve verilere zorlaştırır.

### <a name="azure-storage-transactions"></a>Azure depolama işlemleri

Hello Azure portalı Azure Storage ile etkileşim kurduklarında, tüm işlemleri HTTPS üzerinden gerçekleşir. Azure Storage ile HTTPS toointeract üzerinden hello Storage REST API de kullanabilirsiniz. Merhaba REST API'leri tooaccess nesneleri depolama hesaplarında hello depolama hesabı için gerekli güvenli aktarımı etkinleştirerek çağrılırken HTTPS hello kullanılmasını zorunlu kılabilir.

Paylaşılan erişim imzası ([SAS](../storage/storage-dotnet-shared-access-signature-part-1.md)), kullanılan toodelegate olabilen tooAzure depolama nesnelere erişmek, HTTPS protokolünü kullanılabilir paylaşılan erişim imzaları kullanırken, yalnızca hello seçeneği toospecify içerir. Bu herkes SAS belirteci bağlantılarıyla dışarı gönderme hello uygun protokolünü kullanan sağlar.

[SMB 3.0](https://technet.microsoft.com/library/dn551363(v=ws.11).aspx#BKMK_SMBEncryption) kullanılan tooaccess Azure dosya paylaşımları Şifreleme destekler ve Windows Server 2012 R2, Windows 8, Windows 8.1 ve Windows 10, çapraz bölge erişimine kullanılabilir ve hello masaüstünde'bile erişim.

TooAzure depolama gönderdi önce hello ağ üzerinden geçen olarak şifrelenir, böylece istemci tarafı şifreleme hello verileri şifreler.

### <a name="smb-encryption-over-azure-virtual-networks"></a>Azure sanal ağlar üzerinden SMB şifrelemesi 

[SMB 3.0](https://support.microsoft.com/help/2709568/new-smb-3-0-features-in-the-windows-server-2012-file-server) Azure Windows Server 2012 çalıştıran VM'ler ve üzeri sürümlerindeki özelliği toomake veri aktarımlarını güvenli Azure sanal ağlar üzerinden Aktarımdaki verileri şifreleyerek hello sağlar, izinsiz ve gizli dinleme karşı tooprotect saldırıları. Yöneticiler, hello tüm sunucu ya da yalnızca belirli paylaşımları için SMB şifrelemesi etkinleştirebilirsiniz.

SMB şifrelemesi bir paylaşımı veya sunucu için açıldıktan sonra varsayılan olarak, yalnızca SMB 3 istemciler tooaccess şifrelenmiş hello paylaşımları izin verilir.

## <a name="in-transit-encryption-in-azure-virtual-machines"></a>Azure sanal makinelerde aktarım sırasında şifreleme

Aktarım için gelen ve Azure Windows çalıştıran VM'ler arasında verileri çeşitli yollarla hello bağlantı hello doğasına bağlı olarak şifrelenir.

### <a name="rdp-sessions"></a>RDP oturumları

Bağlanabilir ve tooan üzerinde Azure VM hello kullanarak oturum [Uzak Masaüstü Protokolü](https://msdn.microsoft.com/library/aa383015(v=vs.85).aspx) (RDP) bir Windows istemci bilgisayarı veya bir RDP istemcisinin yüklü Mac. RDP oturumlarda hello ağ üzerinden Aktarım verileri TLS tarafından korunabilir.

Uzak Masaüstü tooconnect tooa Linux VM Azure üzerinde de kullanabilirsiniz.

### <a name="secure-access-toolinux-vms-with-ssh"></a>SSH ile tooLinux VM'ler güvenli erişim

Kullanabileceğiniz [Secure Shell](../virtual-machines/linux/ssh-from-windows.md) (SSH) tooconnect tooLinux VM'ler uzaktan yönetim için Azure'da çalışan. SSH güvenli olmayan bağlantıları üzerinden güvenli oturum açma bilgileri veren bir şifreli bir bağlantı protokolüdür. Bunu hello varsayılan bağlantı Azure'da barındırılan Linux VM'ler için protokolüdür. Kimlik doğrulaması için SSH anahtarları kullanılarak parolaları toolog hello gereksinimini ortadan kaldırmak. SSH kimlik doğrulaması için bir ortak/özel anahtar çifti (asimetrik şifreleme) kullanır.

## <a name="azure-vpn-encryption"></a>Azure VPN şifreleme

Merhaba ağ üzerinden gönderilen hello verilerin güvenli tünel tooprotect hello gizliliğini oluşturan bir sanal özel ağ üzerinden tooAzure bağlanabilir.

### <a name="azure-vpn-gateway"></a>Azure VPN Gateway

[Azure VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md) kullanılan toosend şifrelenmiş trafiği sanal ağınızdaki ortak bağlantısı üzerinden şirket içi konumunuz arasındaki ya da sanal ağlar arasında trafiği toosend olabilir.

Siteden siteye VPN kullanan [IPSec](https://en.wikipedia.org/wiki/IPsec) aktarım şifreleme için. Azure VPN ağ geçitleri varsayılan teklifleri kümesi kullanır. Azure VPN ağ geçitleri toouse belirli şifreleme algoritmaları ve anahtar gücü ile özel bir IPSec/IKE ilkesini yapılandırmak yerine, Azure varsayılan ilkeyi ayarlar hello.

### <a name="point-to-site-vpn"></a>Noktadan siteye VPN

Noktadan siteye VPN'lerde izin tek bir istemci bilgisayarları tooan Azure sanal ağ erişim. [Merhaba Güvenli Yuva Tünel Protokolü](https://technet.microsoft.com/library/2007.06.cableguy.aspx) (SSTP) kullanılan toocreate hello VPN tüneli ve (Merhaba tünel bir HTTPS bağlantısı olarak görünür) güvenlik duvarlarından geçebilir. Noktadan siteye bağlanabilirlik için kendi iç PKI kök CA'yı kullanabilirsiniz.

Hello Azure portal sertifika kimlik doğrulaması veya PowerShell kullanarak bir noktadan siteye VPN bağlantısı tooa sanal ağ yapılandırabilirsiniz.

Noktadan siteye VPN bağlantıları tooAzure sanal ağlar, hakkında daha fazla toolearn bakın: [bir noktadan siteye bağlantı tooa VNet yapılandırma sertifika kimlik doğrulaması kullanarak: Azure portal](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md) ve

[Bir noktadan siteye bağlantı tooa VNet yapılandırma sertifika kimlik doğrulaması kullanarak: PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="site-to-site-vpn"></a>Siteden siteye VPN 

Kullanılan tooconnect bir siteden siteye VPN gateway bağlantısı olan bir IPSec/IKE (Ikev1 veya Ikev2) VPN tüneli üzerinden tooan Azure sanal ağı şirket içi ağ. Bağlantı bu tür bir VPN cihazı bulunan dışarıya dönük bir genel IP adresi atanmış tooit olan şirket içi gerektirir.

Hello Azure portal, PowerShell veya hello Azure komut satırı arabirimi (CLI) kullanarak siteden siteye VPN bağlantısı tooa sanal ağ yapılandırabilirsiniz.

Daha fazla bilgi için bu okuyun:

[Hello Azure portalında bir siteden siteye bağlantı oluşturma](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

[Siteden siteye bağlantı oluşturma](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

[CLI kullanarak siteden siteye VPN bağlantısı olan bir sanal ağ oluşturma](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="in-transit-encryption-in-azure-data-lake"></a>Azure Data Lake aktarım sırasında şifreleme

Data Lake Store'da aktarımdaki (diğer adıyla hareket halindeki) veriler de her zaman şifrelenir. Ayrıca tooencrypting veri önceki toostoring toopersistent medya hello veri ayrıca her zaman aktarım sırasında HTTPS kullanılarak korunmaktadır. HTTPS için Data Lake Store REST arabirimleri hello desteklenir hello tek protokoldür.

Azure Data Lake, aktarım sırasında veri şifreleme hakkında daha fazla toolearn bkz başlıklı hello belge [Azure Data Lake Store'da verilerin şifrelenmesi.](../data-lake-store/data-lake-store-encryption.md)

## <a name="key-management-with-azure-key-vault"></a>Azure anahtar kasası anahtar yönetimi

Uygun koruması ve Yönetimi hello anahtarların şifreleme gereksiz işlenir. Azure anahtar kasası yönetmek ve bulut Hizmetleri tarafından kullanılan erişim tooencryption anahtarlarını denetlemek için Microsoft'un önerilen çözümdür. İzinleri tooaccess anahtarları tooservices veya Azure Active Directory hesaplarını aracılığıyla toousers atanabilir.

Azure anahtar kasası hafifletir kuruluşlar hello gerek tooconfigure, düzeltme eki ve donanım güvenlik modülleri (HSM'ler) ve anahtar yönetimi yazılımı korumak. Azure anahtar kasası ile Microsoft anahtarlarınızı hiçbir zaman görür ve doğrudan erişim toothem uygulamanız yok; denetimi korumak. Ayrıca, alma veya HSM'ler içinde anahtarları oluştur.

## <a name="next-steps"></a>Sonraki adımlar

- [Azure güvenliğine genel bakış](security-get-started-overview.md)
- [Azure ağ güvenliğine genel bakış](security-network-overview.md)
- [Azure veritabanı güvenliğine genel bakış](azure-database-security-overview.md)
- [Azure sanal makineleri güvenliğine genel bakış](security-virtual-machines-overview.md)
- [Bekleme sırasında veri şifrelemesi](azure-security-encryption-atrest.md)
- [Veri güvenliği ve şifreleme için en iyi uygulamalar](azure-security-data-encryption-best-practices.md)
