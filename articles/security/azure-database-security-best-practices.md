---
title: "aaaAzure veritabanı en iyi güvenlik uygulamaları | Microsoft Docs"
description: "Bu makalede Azure veritabanı güvenliği için en iyi yöntemler kümesi sağlar."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: tomsh
ms.openlocfilehash: 78984291e8f74879c7f738e2ce3176c4be18d154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-best-practices"></a>En iyi güvenlik uygulamaları, Azure veritabanı

Veritabanları yönetirken güvenlik güvenliğin çok önemli olduğu ve her zaman Azure SQL veritabanı için bir öncelik olmuştur. Veritabanlarınızı olabilir sıkı bir şekilde güvenli toohelp karşılamak en yasal veya HIPAA, ISO 27001/27002 ve PCI DSS düzey 1, diğerleri de dahil olmak üzere, güvenlik gereksinimleri. Geçerli güvenlik uyumluluk sertifikalar listesini hello kullanılabilir [Microsoft Trust Center site](http://azure.microsoft.com/support/trust-center/services/). Belirli Azure veri merkezleri veritabanınızda yasal düzenleme gereksinimlerine bağlı olarak tooplace de seçebilirsiniz.

Bu makalede, en iyi güvenlik uygulamaları, Azure veritabanı koleksiyonunu aşağıdakiler ele alınacaktır. Bu en iyi uygulamaları ile Azure veritabanı güvenlik bizim deneyimlerden türetilen ve müşterilerin hello deneyimleri bulunun.

En iyi her uygulama için biz açıklamaktadır:

-   Hangi hello en iyi uygulamadır
-   Neden bu en iyi uygulama tooenable istiyor
-   Tooenable hello en iyi yöntem başarısız olursa ne hello sonucu olabilir
-   Tooenable hello en iyi yöntem nasıl öğrenin

Bu Azure veritabanı güvenlik en iyi yöntemler makalesi anlaşma fikir ve Azure platformu özellikleri dayalıdır ve bu makalenin yazıldığı hello aynı anda var özelliğini ayarlar. Bu makalede olacaktır ve görüşlerini ve teknolojileri değiştirmek zaman içinde bu değişiklikleri düzenli olarak tooreflect üzerinde güncelleştirildi.

Bu makalede ele alınan azure veritabanı en iyi yöntemler şunlardır:

-   Güvenlik duvarı kuralları toorestrict veritabanı erişimi kullanın.
-   Veritabanı kimlik doğrulamasını etkinleştir
-   Şifreleme kullanarak verilerinizi koruma
-   Aktarımdaki verileri korumak
-   Veritabanı denetimi etkinleştir
-   Veritabanı tehdit algılama etkinleştir


## <a name="use-firewall-rules-toorestrict-database-access"></a>Güvenlik duvarı kuralları toorestrict veritabanı erişimi kullanın.

Microsoft Azure SQL Veritabanı, Azure ile diğer İnternet tabanlı uygulamalar için ilişkisel veritabanı hizmeti sunar. tooprovide erişim güvenliği, SQL veritabanı erişimi kendi kimlik ve yetkilendirme mekanizmaları kullanıcıların toospecific Eylemler ve verileri sınırlama bağlantısı IP adresine göre kimlik doğrulama mekanizmaları kullanıcıların tooprove gerektiren sınırlayarak güvenlik duvarı kuralları ile kontrol eder. Güvenlik duvarları iznine sahip olan bilgisayarları belirtmediğiniz sürece tüm erişim tooyour veritabanı sunucusu engeller. Merhaba Güvenlik Duvarı'nı her istek IP adresi kaynaklanan hello üzerinde dayalı erişim toodatabases verir.

![Güvenlik duvarı kuralları](./media/azure-database-security-best-practices/azure-database-security-best-practices-Fig1.png)

Hello Azure SQL veritabanı hizmetinin yalnızca TCP bağlantı noktası 1433 ' kullanılabilir. bir SQL veritabanı bilgisayarınızdan tooaccess emin olun, istemci bilgisayar güvenlik duvarının TCP bağlantı noktası 1433 üzerinde giden TCP iletişimi sağlar. Diğer uygulamalar için gerekli değildir, TCP bağlantı noktası 1433 gelen bağlantıları engelle güvenlik duvarı kurallarını kullanma.

Merhaba bağlantı işleminin bir parçası olarak, Azure sanal makinelerden yeniden yönlendirilen tooa farklı bir IP adresi ve bağlantı noktası, her çalışan rolü için benzersiz bağlantılardır. 11000 too11999 hello aralığında başlangıç bağlantı noktası numarası değil. TCP bağlantı noktaları hakkında daha fazla bilgi için bkz: [1433 ADO.NET 4.5 ve SQL Database2 dışındaki bağlantı noktaları](https://docs.microsoft.com/azure/sql-database/sql-database-develop-direct-route-ports-adonet-v12).

> [!Note]
> SQL Veritabanındaki güvenlik duvarı kuralları hakkında daha fazla bilgi için bkz. [SQL Veritabanı güvenlik duvarı kuralları](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

## <a name="enable-database-authentication"></a>Veritabanı kimlik doğrulamasını etkinleştir
SQL veritabanı iki tür kimlik doğrulaması, SQL kimlik doğrulaması ve Azure Active Directory kimlik doğrulaması (Azure AD kimlik doğrulaması) destekler.

**SQL kimlik doğrulaması** aşağıdaki durumlarda önerilir:

-   SQL Azure toosupport ortamları karma işletim sistemlerine sahip olduğu tüm kullanıcılar tarafından bir Windows etki alanı kimlik doğrulaması yapılmıyor sağlar.
-   SQL Azure toosupport eski uygulamaları ve SQL Server kimlik doğrulaması gerektiren üçüncü taraflarca sağlanan uygulamaları sağlar.
-   Bilinmeyen veya güvenilmeyen etki alanlarındaki kullanıcılar tooconnect sağlar. Örneği için kurulmuş müşteriler ile eriştikleri bir uygulama SQL Server oturumları, emirleri tooreceive hello durumu atanır.
-   SQL Azure toosupport Web tabanlı uygulamalar, kullanıcılar kendi kimlikleri oluşturmak sağlar.
-   Yazılım sağlar geliştiriciler toodistribute karmaşık izni hiyerarşi kullanarak kendi uygulamalarında bağlı olarak SQL Server oturumları önceden bilinen.

> [!Note]
> Ancak, SQL Server kimlik doğrulaması, Kerberos güvenlik protokolünü kullanamazsınız.

Kullanırsanız **SQL kimlik doğrulaması** yapmanız gerekir:

-   Merhaba güçlü kimlik bilgileri kendiniz yönetin.
-   Merhaba kimlik hello bağlantı dizesinde koruyun.
-   (Büyük olasılıkla) hello Web sunucusu toohello veritabanından hello ağ üzerinden aktarılan hello kimlik koruyun. Daha fazla bilgi için bkz: [nasıl yapılır: tooSQL kullanarak SQL kimlik doğrulaması, ASP.NET 2.0 bağlanmak](https://msdn.microsoft.com/library/ms998300.aspx).

**Azure Active Directory kimlik doğrulaması** tooMicrosoft Azure SQL veritabanına bağlayan bir mekanizmadır ve [SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) kimlikleri Azure Active Directory (Azure AD) kullanarak. Azure AD kimlik doğrulaması ile veritabanı kullanıcıları hello kimlikleri ve diğer Microsoft Hizmetleri tek bir merkezi konumda merkezi olarak yönetebilir. Merkezi kimlik yönetimi toomanage veritabanı kullanıcıları tek bir yer sağlar ve izin yönetimini basitleştirir. Merhaba aşağıdaki yararları:

-   Bir alternatif tooSQL sunucu kimlik doğrulaması sağlar.
-   Yardımcı veritabanı sunucuları arasında kullanıcı kimlikleri hello artışı durdurun.
-   Tek bir yerde parola döndürme sağlar.
-   Müşteriler, dış (AAD) gruplarını kullanarak veritabanı izinlerini yönetebilir.
-   Tümleşik Windows kimlik doğrulaması ve Azure Active Directory tarafından desteklenen kimlik doğrulama başka biçimlerde etkinleştirerek bunu depolanmasını parolaları ortadan kaldırabilirsiniz.
-   Azure AD kimlik doğrulaması kapsanan veritabanı kullanıcıları tooauthenticate kimlikleri hello veritabanı düzeyinde kullanır.
-   Azure AD tooSQL veritabanına bağlanan uygulamalar için belirteç tabanlı kimlik doğrulamasını destekler.
-   Azure AD kimlik doğrulaması, bir yerel Azure Active Directory etki alanı eşitleme olmadan için ADFS (etki alanı Federasyonu) veya yerel kullanıcı/parola kimlik doğrulamasını destekler.
-   Azure AD, Active Directory Evrensel çok faktörlü kimlik doğrulama (MFA) içeren kimlik doğrulaması kullanan SQL Server Management Studio bağlantılarını destekler. MFA kolay doğrulama seçeneklerini aralıklı güçlü kimlik doğrulaması içerir — telefon araması, SMS mesajı, akıllı kartlar ve PIN ya da mobil uygulama bildirimi. Daha fazla bilgi için bkz: [SSMS desteklemek için SQL Database ve SQL Data Warehouse ile Azure AD MFA](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).

Hello yapılandırma adımları aşağıdaki yordamları tooconfigure hello içerir ve Azure Active Directory kimlik doğrulaması kullanın.

-   Oluşturma ve Azure AD doldurabilirsiniz.
-   İsteğe bağlı: İlişkilendirmek veya şu anda Azure aboneliğinizle ilişkili hello active directory değiştirin.
-   Azure SQL server için Azure Active Directory Yöneticisi oluşturmak veya [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
- İstemci bilgisayarları yapılandırın.
-   Kapsanan veritabanı kullanıcıları AD kimlikleri, eşlenen veritabanı tooAzure oluşturun.
-   Tooyour veritabanı Azure AD kimlikleri kullanarak bağlanın.

Ayrıntılı bilgileri bulabilirsiniz [burada](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

## <a name="protect-your-data-using-encryption"></a>Şifreleme kullanarak verilerinizi koruma

[Azure SQL veritabanında saydam veri şifreleme (TDE)](https://msdn.microsoft.com/library/dn948096.aspx) gerçek zamanlı şifreleme ve şifre çözme hello veritabanının, ilişkili yedeklemelerinizi gerçekleştirerek kötü amaçlı etkinliği hello tehdide karşı korumaya yardımcı olur ve işlem günlüğü dosyalarını REST gerektiren değişiklikler toohello uygulama. TDE, bir simetrik anahtar adlı hello veritabanı şifreleme anahtarı kullanarak veritabanının tamamını hello depolanmasını şifreler.

Merhaba tüm depolama bile şifreli olduğunda tooalso şifrelemek, veritabanınızı çok önemlidir. Bu veri koruması derinliği yaklaşımda hello savunma uygulamasıdır. Azure SQL veritabanı kullanıyorsanız ve kredi kartı veya sosyal güvenlik numarası gibi hassas verileri tooprotect istediğiniz birçok endüstri standartları (örn., HIPAA, hello gereksinimleri karşılayan FIPS 140-2 doğrulanmış 256 bit AES şifreleme veritabanlarıyla şifreleyebilirsiniz. PCI).

Dosyaları toounderstand ilgili çok önemlidir[arabellek havuzu genişletme (BPE)](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension) TDE kullanarak bir veritabanı şifreli olduğunda şifrelenmez. Dosya sistemi düzeyinde şifreleme araçları gibi kullanmalısınız [BitLocker](https://technet.microsoft.com/library/cc732774) veya hello [şifreleme dosya sistemi (EFS)](https://technet.microsoft.com/library/cc700811.aspx) için BPE ilgili dosyaları.

Yetkili bir kullanıcı bu yana gibi bir güvenlik yöneticisi veya bir veritabanı yöneticisi Hello veritabanı ile TDE, şifreli olsa bile hello verilere erişebilir hello önerileri aşağıda da izlemelidir:

-   Merhaba veritabanı düzeyinde SQL kimlik doğrulamasını etkinleştirin.
-   Azure AD kimlik doğrulama kullanarak [RBAC rolleri](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is).
-   Kullanıcılar ve uygulamalar ayrı hesaplar tooauthenticate kullanmanız gerekir. Bu şekilde toousers ve uygulamaları hello izinler sınırlayabilir ve kötü amaçlı etkinliğin hello riskleri azaltın.
-   Uygulama veritabanı düzeyi güvenlik (örneğin, db_datareader veya db_datawriter) sabit veritabanı rollerinin veya kullanarak uygulama toogrant için özel roller izinler tooselected veritabanı nesnelerini oluşturabilirsiniz.

Diğer yolları tooencrypt için verilerinizi göz önünde bulundurun:

-   [Hücre düzeyi şifreleme](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt belirli sütunları veya hatta farklı şifreleme anahtarları ile veri hücrelerinin.
-   Şifreleme her zaman şifreli kullanarak kullanılıyor: [her zaman şifreli](https://msdn.microsoft.com/library/mt163865.aspx) istemcileri tooencrypt hassas verileri istemci uygulamalar içinde ve hiçbir zaman ortaya hello şifreleme anahtarları toohello (SQL veritabanı veya SQL Server) veritabanı altyapısı sağlar. Sonuç olarak, her zaman şifreli kullanıcılar kendi hello verileri (ve görüntüleyebileceğini) arasında ayırmayı sağlar ve kişilere hello verileri yönetme (ancak hiçbir erişimi olması gerekir).
-   Satır düzeyi güvenlik kullanarak: satır düzeyi güvenlik (örneğin, grubu üyeliği veya yürütme bağlamı) sorgu yürütülürken hello kullanıcı hello özellikler temelinde bir veritabanı tablosundaki müşteriler toocontrol erişim toorows sağlar. Daha fazla bilgi için bkz. [Satır düzeyi güvenlik](https://msdn.microsoft.com/library/dn765131).

## <a name="protect-data-in-transit"></a>Aktarımdaki verileri korumak
Aktarımdaki verileri koruma temel veri koruma stratejinizin parçası olmalıdır. Verileri geri ve İleri birçok konumlardan taşıma beri hello genel SSL/TLS protokolleri tooexchange verileri her zaman farklı konumlar arasında kullanmanız önerilir. Bazı durumlarda, şirket içi ve bulut arasındaki tooisolate hello tüm iletişim kanalını isteyebilirsiniz sanal özel ağ (VPN) kullanarak altyapı.

Şirket içi altyapınızı ve Azure arasında taşıma verileri için HTTPS veya VPN gibi uygun güvenlik önlemleri göz önünde bulundurmalısınız.

Birden çok iş istasyonları şirket içi tooAzure toosecure erişimden gereken kuruluşlar için kullanmak [Azure siteden siteye VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Toosecure gereken kuruluşlar bireysel iş istasyonlarında bulunan erişimden şirket içi veya şirket dışı tooAzure, kullanmayı [noktası siteye VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Büyük veri kümeleri taşınabilir ayrılmış bir yüksek hızlı WAN bağlantısı üzerinden gibi [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Toouse ExpressRoute seçerseniz, ayrıca uygulama düzeyi hello kullanarak hello verileri şifreleyebilir [SSL/TLS](https://support.microsoft.com/kb/257591) veya diğer protokoller için ek koruma.

Hello Azure portalı Azure Storage ile etkileşim, tüm işlemleri HTTPS oluşur. [Storage REST API'sini](https://msdn.microsoft.com/library/azure/dd179355.aspx) HTTPS üzerinden de ile kullanılan toointeract olabilir [Azure Storage](https://azure.microsoft.com/services/storage/) ve [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/).

Aktarım tooprotect verileri başarısız kuruluşlar için daha açıktır [man-in--middle saldırıları](https://technet.microsoft.com/library/gg195821.aspx), [gizli dinleme](https://technet.microsoft.com/library/gg195641.aspx) ve oturumu ele geçirme. Bu saldırıların erişim tooconfidential veri sağlamasını hello ilk adımı olabilir.

Merhaba makale okuyarak Azure VPN seçeneği hakkında daha fazla toolearn [planlama ve tasarım VPN ağ geçidi için](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-plan-design).

## <a name="enable-database-auditing"></a>Veritabanı denetimi etkinleştir
SQL Server veritabanı altyapısı hello veya tek bir veritabanının bir örneğini denetim, izleme ve veritabanı altyapısı hello üzerinde meydana gelen olayları günlüğe kaydetme içerir. SQL Server audit, sunucu düzeyi olayları için sunucunun denetim özellikleri ve veritabanı düzeyi olayları için veritabanı denetim belirtimleri içerebilir sunucu denetimleri oluşturmanızı sağlar. Denetlenen olayları, toohello olay günlüklerini veya tooaudit dosyaları yazılabilir.

Kamu veya yüklemenizi standartları gereksinimleri bağlı olarak SQL Server için denetleme birkaç düzeyi vardır. SQL Server Audit hello araçları ve çeşitli sunucu ve veritabanı nesneleri üzerinde tooenable, depolama ve görünüm denetimleri gerekir işlemler sağlar.

[Azure SQL veritabanı denetimi](https://docs.microsoft.com/azure/sql-database/sql-database-auditing) veritabanı olaylarını izler ve bunları Azure depolama hesabınızdaki tooan denetim günlüğünü yazar.

Denetim mevzuatla uyumluluk, veritabanı etkinliğini anlama ve işletme sorunlarını veya şüpheli güvenlik ihlallerini işaret edebilecek farklılıklar ve anormal durumlar hakkında öngörü sahip olmanıza yardımcı olabilir.

Denetim sağlar ve bağlılığı toocompliance standartları kolaylaştırır, ancak Uyumluluk garanti etmez.

toolearn veritabanı denetimi hakkında daha fazla bilgi ve nasıl tooenable, hello makalesini okuyun [etkinleştirmek denetim ve tehdit algılama Azure Güvenlik Merkezi'nde SQL sunucularında](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="enable-database-threat-detection"></a>Veritabanı tehdit algılama etkinleştir
SQL tehdit algılama ve anormal etkinlikler güvenlik uyarıları sağlayarak göründüklerinde toopotential tehditlerine yanıt toodetect sağlar. Şüpheli veritabanı etkinliklerini, olası güvenlik açıkları ve SQL ekleme saldırıları yanı sıra anormal veritabanı erişimi desenleri bağlı bir uyarı alırsınız. SQL tehdit algılama uyarıları şüpheli etkinlik ayrıntılarını sağlayın ve eylem nasıl önerilir tooinvestigate ve hello tehdidi azaltmak.

Örneğin, SQL ekleme hello ortak Web uygulaması güvenlik sorunlarını hello Internet, veri güdümlü kullanılan tooattack uygulamalar üzerinde biridir. Saldırganlar uygulama güvenlik açıkları tooinject kötü amaçlı SQL deyimlerini uygulama giriş alanlarına ihlal veya hello veritabanındaki verileri değiştirme yararlanın.

konusunda toolearn tehdit Algılama'hello Azure portal bakın, veritabanınızdaki için yukarı tooset [SQL veritabanı tehdit algılama](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).

Ayrıca, SQL tehdit algılama uyarıları ile tümleşir [Azure Güvenlik Merkezi](https://azure.microsoft.com/services/security-center/). Tootry davet ediyoruz için 60 gün onu boş.

toolearn veritabanı tehdit algılama hakkında daha fazla bilgi ve nasıl tooenable, hello makalesini okuyun [etkinleştirmek denetim ve tehdit algılama Azure Güvenlik Merkezi'nde SQL sunucularında](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="conclusion"></a>Sonuç
Azure veritabanı birçok kuruluş ve yasal uyumluluk gereksinimlerinin karşılanmasına güvenlik özelliklerinin tam aralıklı bir sağlam veritabanı platformudur. Merhaba fiziksel erişimi tooyour veri denetleme ve hello dosya-, sütun-veya satır düzeyinde saydam veri şifreleme, hücre düzeyi şifreleme veya satır düzeyi güvenlik ile veri güvenliği için çeşitli seçenekler kullanarak verileri korumaya yardımcı olabilir. Her zaman şifreli ayrıca işlemlerini şifrelenmiş veriler karşı uygulama güncelleştirmeleri hello işlemi basitleştirme sağlar. Sırayla, SQL veritabanı etkinliği erişim tooauditing günlükleri sağlar nasıl ve ne zaman verilere erişildiğinde tooknow izin vererek gereksinim hello bilgilerle.

## <a name="next-steps"></a>Sonraki adımlar
- güvenlik duvarı kuralları hakkında daha fazla toolearn bkz [güvenlik duvarı kuralları](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).
- Kullanıcılar ve oturumları hakkındaki toolearn bkz [oturumları yönetme](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).
- Bir öğretici için bkz: [Azure SQL veritabanınıza güvenli](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
