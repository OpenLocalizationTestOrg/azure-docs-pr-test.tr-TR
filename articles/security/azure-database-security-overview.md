---
title: "aaaAzure veritabanı güvenliğine genel bakış | Microsoft Docs"
description: "Bu makalede hello Azure veritabanı güvenlik özelliklerine genel bakış sağlar."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: TomSh
ms.openlocfilehash: 13f14b99d15800e85e9906a9d167eb0adf2135de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-overview"></a>Azure veritabanı güvenliğine genel bakış

Veritabanları yönetirken güvenlik güvenliğin çok önemli olduğu ve her zaman Azure SQL veritabanı için bir öncelik olmuştur. Azure SQL veritabanı güvenlik duvarı kuralları ve bağlantı şifreleme ile bağlantı güvenliği destekler. Kullanıcı adı ve parola ile kimlik doğrulaması ve Azure Active Directory tarafından yönetilen kimlikleri kullanan Azure Active Directory kimlik doğrulaması, destekler. Yetkilendirme rol tabanlı erişim denetimi kullanır.

Azure SQL veritabanı, gerçek zamanlı şifreleme ve şifre çözme veritabanları, ilişkili yedeklemelerinizi ve geri kalan işlem günlüğü dosyalarını değişiklikleri toohello uygulama gerek kalmadan gerçekleştirerek Şifreleme destekler.

Microsoft tooencrypt kurumsal verilerin ek yollar sağlar:

-   Hücre şifreleme tooencrypt belirli sütunları veya veri bile hücrelerinin farklı şifreleme anahtarları ile düzeyi.
-   Bir donanım güvenlik modülü veya şifreleme anahtar hiyerarşinizdeki Merkezi Yönetim gerekiyorsa, Azure VM'deki SQL Server ile Azure anahtar kasası kullanmayı düşünün.
-   Her zaman şifreli (şu anda önizlemede) şifreleme saydam tooapplications yapar ve SQL Database ile Merhaba şifreleme anahtarları paylaşmadan tooencrypt hassas verileri istemci uygulamalar içinde istemcilerinin sağlar.

Azure SQL veritabanı denetimi kuruluşların toorecord olayları tooan denetim oturum açma Azure depolama sağlar. SQL veritabanı denetimi ayrıca Microsoft Power BI toofacilitate ayrıntıya raporlar ve çözümlemeleri ile tümleştirilir.

 SQL Azure veritabanının sıkı bir şekilde güvenli toosatisfy en yasal veya HIPAA, ISO 27001/27002 ve PCI DSS düzey 1, diğerleri de dahil olmak üzere, güvenlik gereksinimleri olabilir. Geçerli güvenlik uyumluluk sertifikalar listesini hello kullanılabilir [Microsoft Azure Trust Center site](http://azure.microsoft.com/support/trust-center/services/).

Bu makalede, Microsoft Azure SQL veritabanları için yapılandırılmış, tablolu ve ilişkisel veri güvenliği temelleri hello size yol göstermektedir. Bu makalede özellikle veri koruma, erişim denetimi ve öngörülebilir izleme kaynakları için başlangıç bilgileri sunulmaktadır.

Bu Azure veritabanı güvenliğine genel bakış makalesi alanları aşağıdaki hello üzerinde odaklanır:

-   Veri koruma
-   Erişim denetimi
-   Öngörülebilir izleme
-   Merkezi güvenlik yönetimi
-   Azure Market

## <a name="protect-data"></a>Veri koruma

SQL veritabanı hareket kullanarak veriler için şifreleme sağlayarak, verilerinizi korur [Aktarım Katmanı Güvenliği](https://support.microsoft.com/kb/3135244)kullanarak verileri bekletin için [saydam veri şifreleme](http://go.microsoft.com/fwlink/?LinkId=526242)ve kullanım kullanarak verilerin [ Her zaman şifreli](https://msdn.microsoft.com/library/mt163865.aspx).

Bu bölümde, biz hakkında konuşma:

-   Hareketli şifreleme
-   Bekleme sırasında şifreleme
-   Şifreleme kullanımda (istemci)

Diğer yolları tooencrypt için verilerinizi göz önünde bulundurun:

-   [Hücre düzeyi şifreleme](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt belirli sütunları veya hatta farklı şifreleme anahtarları ile veri hücrelerinin.
-   Donanım Güvenlik Modülüne veya şifreleme anahtarı hiyerarşinizi bir noktadan yönetmeye ihtiyacınız varsa [Azure VM'de SQL Server ile Azure Anahtar Kasası](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx)'nı kullanın.

### <a name="encryption-in-motion"></a>Hareketli şifreleme

Tüm istemci/sunucu uygulamaları için ortak bir sorunu gizlilik hello gereksinimini aynıdır ortak ve özel ağlar üzerinden verileri taşır. Bir ağ üzerinden taşımaktan veriler şifrelenmez, yakalanan ve olması yetkisiz kullanıcılar tarafından çalınırsa, hello fırsat yok. Veritabanı Hizmetleri ile ilgilenirken, birbirleriyle ve orta katman uygulamalarıyla iletişim veritabanı sunucuları arasındaki ve hello veritabanı istemci ve sunucu arasında veri şifrelenir emin toomake gerekir.

Ağ yönetirken sorunlardan biri güvenilmeyen bir ağ üzerinden uygulamalar arasında gönderilen verilerin güvenli hale getirir. Kullanabileceğiniz [TLS/SSL](https://docs.microsoft.com/windows-server/security/tls/transport-layer-security-protocol) tooauthenticate sunucularını ve istemcilerini ve hello kimliği doğrulanmış taraflar arasında iletileri tooencrypt kullanın.

Merhaba kimlik doğrulama işleminde, bir TLS/SSL istemcisi bir iletiyi tooa TLS/SSL sunucusuna gönderir ve hello sunucu hello sunucu tooauthenticate kendisini gereken hello bilgilerle yanıt verir. Merhaba istemci ve sunucu, oturum anahtarlarının ek değişimini gerçekleştirir ve kimlik doğrulama iletişim uçları hello. Kimlik doğrulaması tamamlandığında, SSL korumalı iletişim hello sunucuyla hello kimlik doğrulama işlemi sırasında oluşturulmuş simetrik şifreleme anahtarları hello kullanarak hello istemci arasındaki başlayabilirsiniz.

Tüm bağlantılar tooAzure SQL veritabanı şifreleme gerektir (SSL/TLS) her zaman "aktarımda" Merhaba veritabanından tooand olsa da veri. SQL Azure TLS/SSL tooauthenticate sunucularını ve istemcilerini kullanır ve hello kimliği doğrulanmış taraflar arasında iletileri tooencrypt kullanın. Uygulamanızın bağlantı dizesinde gerekir parametreleri tooencrypt hello bağlantı ve (Merhaba Klasik Azure portalı dışında bağlantı dizenizi kopyalarsanız, bu sizin için yapılır) değil tootrust hello sunucu sertifikası belirtin, aksi takdirde bağlantı hello Hello hello sunucusunun kimliğini doğrulamak değil ve çok "man-in--middle" saldırılarına maruz kalabilir olacaktır. Merhaba ADO.NET sürücü, örneğin, bu bağlantı dizesi parametreleri için şifrele = True ve TrustServerCertificate = False.

### <a name="encryption-at-rest"></a>Bekleme sırasında şifreleme
Güvenli bir sistemde tasarlama, gizli varlıklar şifreleme ve bir Güvenlik Duvarı'nı hello veritabanı sunucuları geçici oluşturma gibi birkaç önlemleri toohelp güvenli hello veritabanı alabilir. Ancak, burada hello fiziksel medya (örneğin, sürücüleri veya yedekleme bantlarını) çalınması bir senaryoda, kötü amaçlı bir taraf yalnızca geri yükleme veya hello veritabanını ve hello veri göz atın.

Bir çözüm tooencrypt hello hassas veriler hello veritabanındaki ve kullanılan tooencrypt hello verileri bir sertifika ile Merhaba anahtarları korur. Bu herkes hello anahtarları olmadan hello veri kullanmasını engeller, ancak bu tür bir koruma planlanmalıdır.

Bu sorun, SQL Server ve Azure SQL desteği toosolve [saydam veri şifreleme (TDE)](https://docs.microsoft.com/sql/relational-databases/securityrecryption/transparent-data-encryption-tde). TDE rest şifreleme verileri olarak bilinen SQL Server ve Azure SQL veritabanı veri dosyalarını şifreler.

Azure SQL veritabanı saydam veri şifreleme gerçek zamanlı şifreleme ve şifre çözme hello veritabanının, ilişkili yedeklemelerinizi ve geri kalan işlem günlüğü dosyalarını değişiklik gerektirmeden gerçekleştirerek kötü amaçlı etkinliği hello tehdide karşı korunmasına yardımcı olur toohello uygulama.  

TDE, bir simetrik anahtar adlı hello veritabanı şifreleme anahtarı kullanarak veritabanının tamamını hello depolanmasını şifreler. SQL veritabanı'nda hello veritabanı şifreleme anahtarını bir yerleşik bir sunucu sertifikası tarafından korunur. Merhaba yerleşik bir sunucu sertifikası her SQL veritabanı sunucusu için benzersizdir.

Bir veritabanı GeoDR ilişkisine ise, her bir sunucuda farklı bir anahtar tarafından korunur. İki veritabanı bağlı toohello varsa aynı sunucuya paylaştıkları hello aynı yerleşik sertifika. Microsoft, bu sertifikalar otomatik olarak en az 90 günde döndürür. TDE genel bir açıklaması için bkz [saydam veri şifreleme (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde).

### <a name="encryption-in-use-client"></a>Şifreleme kullanımda (istemci)

Çoğu veri ihlallerini hello hırsızlığı, kredi kartı numaraları veya kişisel olarak tanımlanabilir bilgiler gibi kritik verilerin içerir. Veritabanları hassas bilgilerin treasure troves olabilir. Müşterilerin kişisel verileriniz, gizli rekabet bilgileri ve fikri mülkiyet içerebilirler. Kaybolan veya çalınan verileri, özellikle müşteri, marka zarar, sağlayamazsınız ve ciddi cezalar sonuçlanabilir — bile davaların.

![Always Encrypted](./media/azure-databse-security-overview/azure-database-fig1.png)

[Her zaman şifreli](https://msdn.microsoft.com/library/mt163865.aspx) Azure SQL Database veya SQL Server veritabanlarına depolanan bir özellik tasarlanmış tooprotect hassas veri, kredi kartı numaraları veya Ulusal tanımlama numaraları (örneğin, ABD sosyal güvenlik numarası), gibi. Her zaman şifreli tooencrypt hassas verileri istemci uygulamalar içinde istemcilerin ve hiçbir zaman hello şifreleme anahtarları toohello (SQL veritabanı veya SQL Server) veritabanı altyapısı ortaya.

Her zaman şifreli kullanıcılar kendi hello verileri (ve görüntüleyebileceğini) arasında ayırmayı sağlar ve kişilere hello verileri yönetme (ancak hiçbir erişimi olması gerekir). Şirket içi Veritabanı yöneticileri sağlayarak, veritabanı işleçleri bulut ya da diğer yüksek ayrıcalıklı, yetkisiz kullanıcıların, ancak hello şifrelenmiş verileri erişemiyor

Ayrıca, her zaman şifreli şifreleme saydam tooapplications yapar. Böylece, otomatik olarak şifrelemek ve hello istemci uygulamasında hassas verilerin şifresini hello istemci bilgisayarda yüklü bir her zaman şifreli özellikli sürücüsü. Merhaba sürücü hello veri toohello veritabanı altyapısı geçirmeden önce hassas sütunlardaki hello verileri şifreler ve böylece Merhaba semantiği toohello uygulaması korunur sorguları otomatik olarak yeniden yazar. Benzer şekilde, hello sürücü saydam şifrelenmiş veritabanı sütunlar, sorgu sonuçlarında bulunan depolanan verilerin şifresini çözer.

## <a name="access-control"></a>Erişim denetimi
kendi kimlik ve yetkilendirme mekanizmaları kullanıcıların toospecific Eylemler ve verileri sınırlama tooprovide güvenliği, SQL veritabanı bağlantısı IP adresine göre kimlik doğrulama mekanizmaları kullanıcıların tooprove gerektiren sınırlayarak güvenlik duvarı kuralları ile erişimini denetler.

### <a name="database-access"></a>Veritabanı erişimi

Veri koruma erişim tooyour veri denetleme ile başlar. Merhaba ağ katmanında bir güvenlik duvarı toomanage güvenlik yapılandırabilirsiniz ancak, verilerinizi barındıran hello datacenter fiziksel erişimi yönetir. Ayrıca oturum açma kimlik doğrulaması için yapılandırarak ve sunucu ve veritabanı rolleri için izinleri tanımlama erişimi denetler.

Bu bölümde, biz hakkında konuşma:

-   Güvenlik duvarı ve güvenlik duvarı kuralları
-   Kimlik Doğrulaması
-   Yetkilendirme

#### <a name="firewall-and-firewall-rules"></a>Güvenlik duvarı ve güvenlik duvarı kuralları

Microsoft Azure SQL Veritabanı, Azure ile diğer İnternet tabanlı uygulamalar için ilişkisel veritabanı hizmeti sunar. toohelp verilerinizi korumaya, hangi bilgisayarların izniniz belirtmediğiniz sürece tüm erişim tooyour veritabanı sunucusu güvenlik duvarları engellemek. Merhaba Güvenlik Duvarı'nı her istek IP adresi kaynaklanan hello üzerinde dayalı erişim toodatabases verir. Daha fazla bilgi edinmek için bkz. [Azure SQL Veritabanı güvenlik duvarı kurallarına genel bakış](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

Merhaba [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/) hizmetidir yalnızca TCP bağlantı noktası 1433 ' kullanılabilir. bir SQL veritabanı bilgisayarınızdan tooaccess emin olun, istemci bilgisayar güvenlik duvarının TCP bağlantı noktası 1433 üzerinde giden TCP iletişimi sağlar. Başka uygulamalar için gerekli değilse 1433 numaralı bağlantı noktasından gelen TCP bağlantılarını engelleyin.

#### <a name="authentication"></a>Kimlik Doğrulaması

SQL veritabanı kimlik doğrulaması toohello veritabanına bağlanırken, kimliğini kanıtlamak toohow başvuruyor. SQL Veritabanı iki kimlik doğrulaması türünü destekler:

-   **SQL kimlik doğrulaması:** mantıksal bir SQL örneği oluşturulduğunda hello SQL veritabanı abone hesabı olarak adlandırılan bir tek oturum açma hesabı oluşturulur. Bu hesabı kullanarak bağlanır [SQL Server kimlik doğrulaması](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview) (kullanıcı adı ve parola). Bu hesap, yönetici hello mantıksal sunucu örneğindeki ve tüm kullanıcı veritabanlarında toothat örneği bağlı ' dir. Merhaba abone hesap Hello izinlerini kısıtlanamaz. Bu hesaplardan yalnızca biri mevcut olabilir.
-   **Azure Active Directory kimlik doğrulaması:** [Azure Active Directory kimlik doğrulaması](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication) kimlikleri kullanarak Azure Active Directory (tooMicrosoft Azure SQL Database ve SQL Data Warehouse bağlayan bir mekanizmadır Azure AD). Bu, toocentrally veritabanı kullanıcı kimlikleri yönetmenize olanak tanır.

![Kimlik Doğrulaması](./media/azure-databse-security-overview/azure-database-fig2.png)

 Azure Active Directory kimlik doğrulaması avantajları şunlardır:
  - Bir alternatif tooSQL sunucu kimlik doğrulaması sağlar.
  - Ayrıca kullanıcı kimlikleri hello artışı veritabanı sunucuları arasında engellemeye yardımcı olur & parola döndürme tek bir yerde sağlar.
  - Dış (Azure Active Directory) gruplarını kullanarak veritabanı izinlerini yönetebilir.
  - Tümleşik Windows kimlik doğrulaması ve Azure Active Directory tarafından desteklenen kimlik doğrulama başka biçimlerde etkinleştirerek bunu depolanmasını parolaları ortadan kaldırabilirsiniz.

#### <a name="authorization"></a>Yetkilendirme
[Yetkilendirme](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins) toowhat başvuran bir kullanıcı bir Azure SQL veritabanı içinde yapabilirsiniz ve bu kullanıcı hesabınızın veritabanı tarafından denetlenen [rol üyeliklerini](https://msdn.microsoft.com/library/ms189121) ve [nesne düzeyi izinleri](https://msdn.microsoft.com/library/ms191291.aspx). Yetkilendirme sorumlu erişmek için hangi güvenliği sağlanabilir kaynakları ve işlemleri kaynaklarla için izin verilen belirleme hello işlemidir.

### <a name="application-access"></a>Uygulama erişimi

Bu bölümde, biz hakkında konuşma:

-   Dinamik veri maskeleme
-   Satır düzeyi güvenlik

#### <a name="dynamic-data-masking"></a>Dinamik veri maskeleme
Çağrı merkezinde bir temsilcisiyle arayanlar, sosyal güvenlik numarası veya kredi kartı numarası birkaç rakam tanımlayabilir ancak toohello temsilcisiyle öğeleri tam olarak olmamalıdır bu verilerin açığa.

Tüm maskeleri ancak hello herhangi bir sosyal güvenlik numarası veya kredi kartı numarası hello sonuç kümesindeki herhangi bir sorgu dört basamak son bir maskeleme kuralı tanımlanabilir.

![Dinamik veri maskeleme](./media/azure-databse-security-overview/azure-database-fig3.png)

Bir geliştirici uyumluluk düzenlemeleri ihlal etmeden sorun giderme amacıyla üretim ortamlarında sorgulayabilmesi başka bir örnek olarak, uygun veri maskesi tanımlı tooprotect kişisel bilgileri (PII) verileri olabilir.

[SQL veritabanı dinamik veri maskeleme](https://docs.microsoft.com/azure/sql-database/sql-database-dynamic-data-masking-get-started) toonon ayrıcalıklı kullanıcılar maskeleyerek gizli verilerin açığa sınırlar. Dinamik veri maskeleme hello V12 sürümü Azure SQL veritabanı için desteklenir.

[Dinamik veri maskeleme](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking) toodesignate etkinleştirerek yetkisiz erişim toosensitive veri önlemenize yardımcı olan hello hassas verileri tooreveal hello uygulama katmanı üzerinde en az etkiyle ne kadarının. Bunu hello verileri hello veritabanında değişip değişmediğini sırada, belirlenen veritabanı alanları hello hassas verileri sorgu hello sonuç kümesinde gizler ilke tabanlı güvenlik özelliğidir.


> [!Note]
> Dinamik veri maskeleme hello Azure veritabanı yöneticisi, sunucu yöneticisi veya güvenlik yetkilisi rolleri tarafından yapılandırılabilir.

#### <a name="row-level-security"></a>Satır düzeyi güvenlik
Çok müşterili veritabanları için başka bir ortak güvenlik gereksinimi [satır düzeyi güvenlik](https://msdn.microsoft.com/library/dn765131.aspx). Bu özellik, (örneğin, grubu üyeliği veya yürütme bağlamı) sorgu yürütülürken hello kullanıcı hello özellikler temelinde bir veritabanı tablosundaki toocontrol erişim toorows sağlar.

![Satır düzeyi güvenlik](./media/azure-databse-security-overview/azure-database-fig4.png)

Merhaba erişim kısıtlama mantığı hello veritabanı katmanı bulunan yerine koyma hello verilerden başka bir uygulama katmanı. veri erişimini herhangi bir katmanı denenir her zaman hello veritabanı sistem hello erişim kısıtlamaları uygular. Bu güvenlik sisteminizde daha güvenli ve sağlam güvenlik sisteminizde yüzey alanını hello azaltarak hale getirir.

Satır düzeyi güvenlik koşul tabanlı erişim denetimi sunar. Göz önünde bulundurarak meta verileri veya hello Yöneticisi belirler başka bir ölçüt uygun şekilde sürebilir esnek, merkezi ve koşulu tabanlı değerlendirme özellikleri. Merhaba kullanıcının kullanıcı özniteliklerini temel alarak hello uygun erişim toohello veri sahip olup olmadığına bakılmaksızın hello karşılaştırma ölçütü toodetermine kullanılır. Etiket tabanlı erişim denetimi koşulu tabanlı erişim denetimi kullanarak uygulanabilir.

## <a name="proactive-monitoring"></a>Öngörülebilir izleme
SQL veritabanı sağlayarak, verilerinizi korur **denetim** ve **tehdit algılama** özellikleri.

### <a name="auditing"></a>Denetim
SQL veritabanı denetimi, özelliği toogain fikirler olayları ve güncelleştirmeleri ve hello veri sorguları da dahil olmak üzere hello veritabanındaki meydana gelen değişiklikleri artırır.

[Azure SQL veritabanı denetimi](https://docs.microsoft.com/azure/sql-database/sql-database-auditing-get-started) veritabanı olaylarını izler ve bunları Azure depolama hesabınızdaki tooan denetim günlüğünü yazar. Denetim mevzuatla uyumluluk, veritabanı etkinliğini anlama ve işletme sorunlarını veya şüpheli güvenlik ihlallerini işaret edebilecek farklılıklar ve anormal durumlar hakkında öngörü sahip olmanıza yardımcı olabilir. Denetim sağlar ve bağlılığı toocompliance standartları kolaylaştırır, ancak Uyumluluk garanti etmez.

SQL veritabanı denetimi yapmanıza olanak sağlar:

-   **Korumak** seçili olayların bir denetim izi. Denetlenecek veritabanı Eylemler toobe kategorilerini tanımlayabilirsiniz.
-   **Rapor** veritabanı etkinlik. Önceden yapılandırılmış raporları ve etkinlik ve olay Raporlama ile hızlı şekilde kullanmaya bir Pano tooget kullanabilirsiniz.
-   **Analiz** raporlar. Şüpheli olayları, olağan dışı etkinliği ve eğilimleri bulabilirsiniz.

İki denetim yöntemleri vardır:

-   **BLOB denetimi** -günlükleri tooAzure Blob depolama alanına yazılır. Daha yüksek performans sağlayan, daha yüksek ayrıntı düzeyi nesne düzeyinde denetimi destekler ve daha düşük maliyetli bir yeni denetim yöntem budur.
-   **Tablo denetim** -günlükleri tooAzure Table Storage yazılır.

### <a name="threat-detection"></a>Tehdit algılama
[Azure SQL veritabanı tehdit algılama](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection) olası güvenlik tehditlerini gösteren kuşkulu etkinlikleri algılar. Bunlar ortaya çıktığında tehdit algılama, SQL eklemelerini gibi hello veritabanına toorespond toosuspicious olayları sağlar. Uyarıları sağlar ve hello Azure SQL veritabanı denetimi tooexplore hello şüpheli olayları kullanımına izin verir.

![Tehdit algılama](./media/azure-databse-security-overview/azure-database-fig5.jpg)

Örneğin, SQL ekleme hello ortak Web uygulaması güvenlik sorunlarını hello Internet, veri güdümlü kullanılan tooattack uygulamalar üzerinde biridir. Saldırganlar uygulama güvenlik açıkları tooinject kötü amaçlı SQL deyimlerini uygulama giriş alanlarına ihlal veya hello veritabanındaki verileri değiştirme yararlanın.

Bunlar ortaya çıktığında güvenlik görevlileri veya diğer atanmış yöneticileri şüpheli veritabanı etkinlikleri hakkında anında bildirim edinebilirsiniz. Her bir bildirim hello şüpheli Etkinlik ayrıntıları sağlar ve nasıl toofurther araştırın ve hello tehdidi azaltmak önerir.        

## <a name="centralized-security-management"></a>Merkezi güvenlik yönetimi

[Azure Güvenlik Merkezi](https://azure.microsoft.com/documentation/services/security-center/) engellemenize, algılamanıza ve toothreats yanıt yardımcı olur. Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

[Güvenlik Merkezi](https://docs.microsoft.com/azure/security-center/security-center-sql-database) tüm sunucular ve veritabanları hello güvenliğini görünürlük sağlayarak SQL veritabanındaki verileri korumaya yardımcı olur. Güvenlik Merkezi ile şunları yapabilirsiniz:

-   SQL veritabanı şifreleme ve denetim ilkeleri tanımlar.
-   SQL Database kaynaklarının Hello güvenlik tüm aboneliklerinizi izleyin.
-   Hızlı bir şekilde tanımlamak ve güvenlik sorunları düzeltin.
-   Gelen uyarılar tümleştirmek [Azure SQL veritabanı tehdit algılama](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
-   Güvenlik Merkezi, rol tabanlı erişim destekler.

## <a name="azure-marketplace"></a>Azure Market

Hello Azure Marketi start-ups ve bağımsız yazılım satıcılarının (ISV'ler) toooffer Merhaba Dünya çözümleri tooAzure müşterilerine sağlayan bir çevrimiçi uygulamalar ve hizmetler Market ' dir.
Hello Azure Marketi birleştiren Microsoft Azure iş ortağı ekosistemlerini tek, birleşik platform toobetter içine bizim müşterileri ve ortakları hizmet. Tıklatın [burada](https://azuremarketplace.microsoft.com/marketplace/apps?search=Database%20Security&page=1) tooglance veritabanı güvenlik ürünleri Azure markette üzerinde kullanılabilir.

## <a name="next-steps"></a>Sonraki adımlar

- Daha fazla bilgi edinmek [Azure SQL veritabanınıza güvenli](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
- Daha fazla bilgi edinmek [Azure Güvenlik Merkezi ve Azure SQL Database hizmeti](https://docs.microsoft.com/azure/security-center/security-center-sql-database).
- Tehdit algılama hakkında daha fazla toolearn bkz [SQL veritabanı tehdit algılama](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).
- toolearn daha, fazla [artırmak SQL veritabanı performans](https://docs.microsoft.com/azure/sql-database/sql-database-performance-tutorial). 
