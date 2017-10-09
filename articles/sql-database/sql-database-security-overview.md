---
title: "aaaAzure SQL veritabanı güvenlik genel bakış | Microsoft Docs"
description: "Tooauthentication, yetkilendirme, bağlantı güvenliği, şifreleme ve uyumluluk geldiğinde hello farklarını hello Bulut ve şirket içi SQL Server dahil olmak üzere Azure SQL Database ve SQL Server güvenliği hakkında bilgi edinin."
services: sql-database
documentationcenter: 
author: tmullaney
manager: jhubbard
editor: 
ms.assetid: a012bb85-7fb4-4fde-a2fc-cf426c0a56bb
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/05/2017
ms.author: thmullan;jackr
ms.openlocfilehash: 7b0b0d1b59ec4018d9fb668bc8b6b56c9907e982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-your-sql-database"></a>SQL Veritabanınızı güvenli hale getirme

Bu makalede, Azure SQL veritabanı kullanarak bir uygulamanın hello veri katmanı güvenliği hello temellerini anlatılmaktadır. Bu makalede özellikle veri koruma, erişim denetimi ve öngörülebilir izleme kaynakları için başlangıç bilgileri sunulmaktadır. 

Merhaba SQL tüm türdeki kullanılabilir güvenlik özelliklerini eksiksiz bir genel bakış için bkz: [SQL Server veritabanı altyapısı ve Azure SQL veritabanı için Güvenlik Merkezi](https://msdn.microsoft.com/library/bb510589). Ek bilgi sağlanmıştır ayrıca hello [güvenlik ve Azure SQL veritabanı teknik incelemeyi](https://download.microsoft.com/download/A/C/3/AC305059-2B3F-4B08-9952-34CDCA8115A9/Security_and_Azure_SQL_Database_White_paper.pdf) (PDF).

## <a name="protect-data"></a>Veri koruma
SQL Veritabanı, hareket halindeki verileriniz için [Aktarım Katmanı Güvenliği](https://support.microsoft.com/kb/3135244), bekleyen veriler için [Saydam Veri Şifrelemesi](http://go.microsoft.com/fwlink/?LinkId=526242) ve kullanılan veriler için [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx) kullanarak verilerinizi şifreler ve güvenliğini sağlar. 

> [!IMPORTANT]
>Tüm bağlantılar tooAzure SQL veritabanı şifreleme gerektir (SSL/TLS) her zaman "aktarımda" Merhaba veritabanından tooand olsa da veri. Uygulamanızın bağlantı dizesinde parametreleri tooencrypt hello bağlantı belirtmeniz gerekir ve *değil* tootrust hello sunucu sertifikası, (Bu işlem dışı bağlantı dizenizi kopyalarsanız, Klasik Azure portalı hello için) Aksi takdirde hello bağlantı hello hello sunucusunun kimliğini doğrulamaz ve çok "man-in--middle" saldırılarına maruz kalabilir olacaktır. Merhaba ADO.NET sürücüsü için örneğin, bu bağlantı dizesi parametreleri olan **şifrele = True** ve **TrustServerCertificate = False**. 

Diğer yolları tooencrypt için verilerinizi göz önünde bulundurun:

* [Hücre düzeyi şifreleme](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt belirli sütunları veya hatta farklı şifreleme anahtarları ile veri hücrelerinin.
* Donanım Güvenlik Modülüne veya şifreleme anahtarı hiyerarşinizi bir noktadan yönetmeye ihtiyacınız varsa [Azure VM'de SQL Server ile Azure Anahtar Kasası](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx)'nı kullanın.

## <a name="control-access"></a>Erişim denetimi
SQL veritabanı güvenlik duvarı kuralları, kullanıcıların tooprove kendi kimlik ve yetkilendirme toodata üyeliklerini rol tabanlı ve izinleri aracılığıyla yanı sıra aracılığıyla gerektiren kimlik doğrulama mekanizmaları kullanarak erişim tooyour veritabanı sınırlandırarak verilerinizi korur satır düzeyi güvenlik ve dinamik veri maskeleme. Erişim denetimi özellikleri SQL veritabanında hello kullanımını tartışma için bkz [erişimi denetlemenize](sql-database-control-access.md).

> [!IMPORTANT]
> Azure’daki veritabanlarının ve mantıksal sunucuların yönetilmesi, portal kullanıcısı hesabınıza atanan rollerle denetlenir. Bu konu hakkında daha fazla bilgi için bkz. [Azure portalında rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md).
>

### <a name="firewall-and-firewall-rules"></a>Güvenlik duvarı ve güvenlik duvarı kuralları
toohelp verilerinizi korumaya, güvenlik duvarları kullanma iznine sahip olan bilgisayarları belirtmediğiniz sürece tüm erişim tooyour veritabanı sunucusu engellemek [güvenlik duvarı kuralları](sql-database-firewall-configure.md). Merhaba Güvenlik Duvarı'nı her istek IP adresi kaynaklanan hello üzerinde dayalı erişim toodatabases verir.

### <a name="authentication"></a>Kimlik Doğrulaması
SQL veritabanı kimlik doğrulaması toohello veritabanına bağlanırken, kimliğini kanıtlamak toohow başvuruyor. SQL Veritabanı iki kimlik doğrulaması türünü destekler:

* **SQL Kimlik Doğrulaması**: Kullanıcı adı ve parola kullanır. Veritabanınız için hello mantıksal sunucu oluşturduğunuzda, bir kullanıcı adı ve parola bir "sunucusuna yönetici" oturum açma belirttiniz. Bu kimlik bilgilerini kullanarak, tooany veritabanı hello veritabanı sahibi ya da "dbo." olarak bu sunucu üzerinde doğrulanabilir 
* **Azure Active Directory Kimlik Doğrulaması**: Azure Active Directory tarafından yönetilen kimlikleri kullanır, yönetilen ve tümleşik etki alanları ile kullanılabilir. [Mümkün olduğunda](https://msdn.microsoft.com/library/ms144284.aspx) Active Directory kimlik doğrulamasını (tümleşik güvenlik) kullanın. Azure Active Directory kimlik doğrulaması toouse istiyorsanız, hello "tooadminister Azure AD kullanıcıları ve grupları izin Azure AD yönetim," adlı başka bir sunucu yöneticisinin oluşturmanız gerekir. Bu yönetici normal bir sunucu yöneticisinin gerçekleştirebileceği tüm işlemleri yapabilir. Bkz: [tooSQL veritabanı tarafından kullanarak Azure Active Directory kimlik doğrulaması bağlanma](sql-database-aad-authentication.md) nasıl bir kılavuz için toocreate Azure AD yönetim tooenable Azure Active Directory kimlik doğrulaması.

### <a name="authorization"></a>Yetkilendirme
Yetkilendirme başvuruyor toowhat bir kullanıcı, bir Azure SQL veritabanı içinde yapabilir ve bu kullanıcı hesabınızın veritabanı rol üyeliklerini tarafından denetlenen ve nesne düzeyi izinleri. En iyi uygulama, gerekli en düşük ayrıcalık kullanıcılar hello vermeniz gerekir. Merhaba server yönetici hesabı ile bağlanan yetkilisi toodo hello veritabanı içinde herhangi bir şey sahip db_owner üyesidir. Bu hesabı şema yükseltmeleri ve diğer yönetimsel işlemlerde kullanmak üzere saklayın. Merhaba ile uygulama toohello veritabanından daha kısıtlı izinleri tooconnect ile Merhaba "ApplicationUser" hesabı kullanmak, uygulamanız tarafından gerekli en düşük ayrıcalık.

### <a name="row-level-security"></a>Satır düzeyi güvenlik
Satır düzeyi güvenlik (örneğin, grubu üyeliği veya yürütme bağlamı) sorgu yürütülürken hello kullanıcı hello özellikler temelinde bir veritabanı tablosundaki müşteriler toocontrol erişim toorows sağlar. Daha fazla bilgi için bkz. [Satır düzeyi güvenlik](https://msdn.microsoft.com/library/dn765131).

### <a name="data-masking"></a>Veri maskeleme 
SQL veritabanı dinamik veri maskeleme toonon ayrıcalıklı kullanıcılar maskeleyerek gizli verilerin açığa sınırlar. Dinamik veri maskeleme otomatik olarak Azure SQL veritabanındaki olası hassas verileri bulur ve uygulanabilir öneriler toomask hello uygulama katmanı üzerinde en az etkiyle bu alanlar sağlar. Merhaba verileri hello veritabanında değişip değişmediğini sırada hello hassas verileri sorgu hello sonuç kümesinde belirlenen veritabanı alanları obfuscating tarafından çalışır. Daha fazla bilgi için bkz: [SQL veritabanını dinamik veri maskeleme ile çalışmaya başlama](sql-database-dynamic-data-masking-get-started.md) gizli verilerin açığa kullanılan toolimit olabilir.

## <a name="proactive-monitoring"></a>Öngörülebilir izleme
SQL Veritabanı, denetim ve tehdit algılama özellikleriyle verilerinizi korur. 

### <a name="auditing"></a>Denetim
SQL veritabanı denetimi veritabanı etkinliklerini izler ve Azure depolama hesabınızdaki veritabanı olayları tooan denetim günlüğü kaydederek toomaintain Mevzuat uyumluluğu, yardımcı olur. Denetim toounderstand devam eden veritabanı etkinliklerini sağlar, yanı sıra çözümlemek ve etkinlik geçmişini tooidentify olası tehditler veya şüpheli Uygunsuz kullanım ve güvenlik ihlallerini inceleyin. Daha fazla bilgi için bkz. [SQL Veritabanı Denetimini kullanmaya başlayın](sql-database-auditing.md).  

### <a name="threat-detection"></a>Tehdit algılama
Tehdit algılama, denetleme, olağan dışı ve zararlı denemeleri tooaccess veya yararlanma veritabanlarını algılar hello Azure SQL Database hizmetinde yerleşik güvenlik Intelligence ek katmanı sağlayarak tamamlar. Kuşkulu etkinlikler, olası güvenlik açıkları ve SQL ekleme saldırıları, yanı sıra hakkında anormal veritabanı erişimi desenleri uyarı alırsınız. Tehdit algılama uyarıları, gelen görüntülenebilir [Azure Güvenlik Merkezi](https://azure.microsoft.com/services/security-center/) ve şüpheli etkinlik ayrıntılarını sağlayın ve eylem nasıl önerilir tooinvestigate ve hello tehdidi azaltmak. Tehdit algılama $15/sunucu/ay maliyetleri. Merhaba ücretsiz ilk 60 gün olur. Daha fazla bilgi için bkz. [SQL Veritabanı Tehdit Algılamayı kullanmaya başlayın](sql-database-threat-detection.md).
 
### <a name="data-masking"></a>Veri Maskeleme 
SQL veritabanı dinamik veri maskeleme toonon ayrıcalıklı kullanıcılar maskeleyerek gizli verilerin açığa sınırlar. Dinamik veri maskeleme otomatik olarak Azure SQL veritabanındaki olası hassas verileri bulur ve uygulanabilir öneriler toomask hello uygulama katmanı üzerinde en az etkiyle bu alanlar sağlar. Merhaba verileri hello veritabanında değişip değişmediğini sırada hello hassas verileri sorgu hello sonuç kümesinde belirlenen veritabanı alanları obfuscating tarafından çalışır. Daha fazla bilgi için bkz: ile çalışmaya başlama [SQL veritabanını dinamik veri maskeleme](sql-database-dynamic-data-masking-get-started.md)
 
## <a name="compliance"></a>Uyumluluk
Ayrıca toohello özellikleri ve çeşitli güvenlik, Azure SQL veritabanı da gereksinimlerini uygulamanızı yardımcı olan işlevselliği yukarıda içinde normal denetimleri katılan ve uyumluluk standartlarına çeşitli karşı sertifikalı. Merhaba daha fazla bilgi için bkz: [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/), hello en güncel listesini bulabilirsiniz burada [SQL veritabanı uyumluluk sertifikalarından](https://azure.microsoft.com/support/trust-center/services/).

## <a name="next-steps"></a>Sonraki adımlar

- Erişim denetimi özellikleri SQL veritabanında hello kullanımını tartışma için bkz [erişimi denetlemenize](sql-database-control-access.md).
- Veritabanı denetim bir tartışma için bkz: [SQL veritabanı denetimi](sql-database-auditing.md).
- Tehdit algılama tartışma için bkz [SQL veritabanı tehdit algılama](sql-database-threat-detection.md).
