---
title: "SQL veri ambarı veritabanında aaaSecure | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL veri ambarı veritabanında güvenliğini sağlamaya yönelik ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 5ef4d760e00be46bfe7808bc95dbe1e4b3a51165
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>SQL veri ambarı veritabanında güvenli
> [!div class="op_single_selector"]
> * [Güvenlik genel bakış](sql-data-warehouse-overview-manage-security.md)
> * [Kimlik doğrulaması](sql-data-warehouse-authentication.md)
> * [Şifreleme (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Şifreleme (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

Bu makalede, Azure SQL Data Warehouse veritabanınızın güvenliğini sağlama hello temellerini anlatılmaktadır. Özellikle, bu makalede, erişimi sınırlamak için kaynaklar başlama verileri koruma ve bir veritabanı etkinliklerini izleme.

## <a name="connection-security"></a>Bağlantı güvenliği
Bağlantı güvenliği kısıtlamak ve güvenlik duvarı kuralları ve bağlantı şifreleme kullanarak bağlantıları tooyour veritabanını güvenli toohow başvuruyor.

Güvenlik duvarı kuralları, her iki hello sunucu ve hello veritabanı tooreject bağlantı denemeleri açıkça Güvenilenler listesine edilmemiş IP adreslerinden tarafından kullanılır. tooallow bağlantıları uygulamanızı veya istemci makinenin ortak IP adresi, ilk hello Azure Portal, REST API veya PowerShell kullanarak bir sunucu düzeyinde güvenlik duvarı kuralı oluşturmanız gerekir. Bir en iyi uygulama olarak, sunucu güvenlik duvarı aracılığıyla mümkün olduğunca izin hello IP adres aralıklarını kısıtlamanız gerekir.  tooaccess Azure SQL Data Warehouse, yerel bilgisayarınızdan olun ağ ve yerel bilgisayar hello güvenlik duvarının TCP bağlantı noktası 1433 giden iletişime olanak sağlar.  Daha fazla bilgi için bkz: [Azure SQL veritabanı Güvenlik Duvarı][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule], ve [sp_set_database_ firewall_rule][sp_set_database_firewall_rule].

Bağlantıları tooyour SQL veri ambarı varsayılan olarak şifrelenir.  Bağlantı ayarlarını toodisable değiştirme şifreleme yok sayılır.

## <a name="authentication"></a>Kimlik Doğrulaması
Kimlik doğrulama toohello veritabanına bağlanırken, kimliğini kanıtlamak toohow başvuruyor. SQL veri ambarı SQL Server kimlik doğrulamasını bir kullanıcı adı ve parola yanı sıra Azure Active Directory şu anda destekler. 

Veritabanınız için hello mantıksal sunucu oluşturduğunuzda, bir kullanıcı adı ve parola bir "sunucusuna yönetici" oturum açma belirttiniz. Bu kimlik bilgilerini kullanarak, tooany veritabanı hello veritabanı sahibi ya da SQL Server kimlik doğrulaması yoluyla "dbo" olarak bu sunucuda kimlik doğrulaması yapabilir.

Ancak, en iyi uygulama, kuruluşunuzdaki kullanıcılar farklı bir hesap tooauthenticate kullanmanız gerekir. Bu şekilde hello izinler toohello uygulama sınırlayabilir ve güvenlik açığı tooa SQL ekleme saldırısında, uygulama kodunuzun olması durumunda kötü amaçlı etkinliğin hello riskleri azaltın. 

SQL Server kimliği doğrulanmış bir kullanıcı toocreate bağlanmak toohello **ana** veritabanı, Sunucu Yöneticisi oturum açma ile sunucunuzdaki ve yeni bir sunucu oturum açma oluşturun.  Ayrıca, hello ana veritabanını Azure SQL Data Warehouse kullanıcılar için iyi bir fikir toocreate bir kullanıcı olarak. Master kullanıcı oluşturma, bir veritabanı adı belirtmeden SSMS gibi araçları kullanarak bir kullanıcı toologin sağlar.  Ayrıca bunları toouse hello Nesne Gezgini tooview tüm veritabanları SQL server üzerinde sağlar.

```sql
-- Connect toomaster database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Ardından, tooyour bağlanmak **SQL Data Warehouse veritabanı** , Sunucu Yöneticisi oturum açma ile oluşturduğunuz hello sunucu oturum açma tabanlı bir veritabanı kullanıcısı oluşturmalıdır.

```sql
-- Connect tooSQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Bir kullanıcı oturumu açma oluşturma veya yeni veritabanları oluşturma gibi ek işlemleri yapacaksanız, bunlar atanan toobe toohello de gerekir `Loginmanager` ve `dbmanager` hello ana veritabanı rolleri. Bu ilave roller ve kimlik doğrulama tooa SQL veritabanı ile ilgili daha fazla bilgi için bkz [veritabanları ve Azure SQL veritabanında oturumları yönetme][Managing databases and logins in Azure SQL Database].  SQL veri ambarı için Azure AD hakkında daha fazla bilgi için bkz: [tooSQL veri ambarı tarafından kullanarak Azure Active Directory kimlik doğrulaması bağlanma][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication].

## <a name="authorization"></a>Yetkilendirme
Yetkilendirme başvuruyor toowhat içinde bir Azure SQL Data Warehouse veritabanı yapabilirsiniz ve bu kullanıcı hesabınızın rol üyeliklerini ve izinleri tarafından denetlenir. En iyi uygulama, gerekli en düşük ayrıcalık kullanıcılar hello vermeniz gerekir. Azure SQL veri ambarı Bu kolay toomanage rolleriyle T-SQL yapar:

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser tooread data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser toowrite data
```

Merhaba server yönetici hesabı ile bağlanan yetkilisi toodo hello veritabanı içinde herhangi bir şey sahip db_owner üyesidir. Bu hesabı şema yükseltmeleri ve diğer yönetimsel işlemlerde kullanmak üzere saklayın. Merhaba ile uygulama toohello veritabanından daha kısıtlı izinleri tooconnect ile Merhaba "ApplicationUser" hesabı kullanmak, uygulamanız tarafından gerekli en düşük ayrıcalık.

Bir kullanıcı Azure SQL veritabanı ile neler yapabileceğinizi yolları toofurther sınırı vardır:

* Ayrıntılı [izinleri] [ Permissions] denetim yapabileceğiniz işlemleri ayrı ayrı sütunlarda tabloları, görünümleri, yordamlar ve diğer nesneleri hello veritabanındaki olanak tanır. Kullanım ayrıntılı izinler toohave çoğu denetim hello ve hello gerekli minimum izinleri verin. Hello ayrıntılı izin sistemi biraz karmaşıktır ve bazı incelemesi toouse etkili bir şekilde gerektirir.
* [Veritabanı rolleri] [ Database roles] db_datareader ve db_datawriter kullanılan toocreate olabilir dışında daha güçlü uygulama kullanıcı hesapları veya daha az güçlü yönetim. Merhaba yerleşik sabit veritabanı rollerinin kolay bir yolu toogrant izinleri sağlar, ancak gerekenden daha fazla izin verme neden olabilir.
* [Saklı yordamlar] [ Stored procedures] kullanılan toolimit hello veritabanı üzerinde gerçekleştirilecek hello eylemler olabilir.

Veritabanları ve mantıksal sunucu hello Klasik Azure Portalı ' yönetmek veya hello Azure Kaynak Yöneticisi API'si kullanılarak portal kullanıcı hesabınızın rol atamalarını tarafından denetlenir. Bu konu hakkında daha fazla bilgi için bkz: [Azure portalında rol tabanlı erişim denetimi][Role-based access control in Azure Portal].

## <a name="encryption"></a>Şifreleme
Azure SQL veri ambarı saydam veri şifreleme (TDE'nin) gerçek zamanlı şifreleme ve şifre çözme REST verilerinizin gerçekleştirerek kötü amaçlı etkinliği hello tehdide karşı korunmasına yardımcı olur.  Veritabanınızı şifrelerken, ilişkili yedeklemeler ve işlem günlüğü dosyalarını herhangi bir değişiklik tooyour uygulama gerek kalmadan şifrelenir. TDE, bir simetrik anahtar adlı hello veritabanı şifreleme anahtarı kullanarak veritabanının tamamını hello depolanmasını şifreler. SQL veritabanı'nda hello veritabanı şifreleme anahtarını bir yerleşik bir sunucu sertifikası tarafından korunur. Merhaba yerleşik bir sunucu sertifikası her SQL veritabanı sunucusu için benzersizdir. Microsoft, bu sertifikalar otomatik olarak en az 90 günde döndürür. SQL veri ambarı tarafından kullanılan hello şifreleme algoritması AES-256'dır. TDE genel bir açıklaması için bkz [saydam veri şifreleme][Transparent Data Encryption].

Hello kullanarak veritabanını şifreleyebilirsiniz [Azure Portal] [ Encryption with Portal] veya [T-SQL][Encryption with TSQL].

## <a name="next-steps"></a>Sonraki adımlar
Ayrıntılar ve tooyour SQL Data Warehouse farklı protokolleriyle bağlayan ilişkin örnekler için bkz: [tooSQL veri ambarına bağlanmak][Connect tooSQL Data Warehouse].

<!--Image references-->

<!--Article references-->
[Connect tooSQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
