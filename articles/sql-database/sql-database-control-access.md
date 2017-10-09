---
title: "aaaGranting erişim tooAzure SQL veritabanı | Microsoft Docs"
description: "Azure SQL veritabanına erişim tooMicrosoft verme hakkında bilgi edinin."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 8e71b04c-bc38-4153-8f83-f2b14faa31d9
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/06/2017
ms.author: rickbyh
ms.openlocfilehash: 4c32fafa7e98b731ff2f9bf4666da7e4a3145286
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-access-control"></a>Azure SQL Veritabanı erişim denetimi
kendi kimlik ve yetkilendirme mekanizmaları kullanıcıların toospecific Eylemler ve verileri sınırlama tooprovide güvenliği, SQL veritabanı bağlantısı IP adresine göre kimlik doğrulama mekanizmaları kullanıcıların tooprove gerektiren sınırlayarak güvenlik duvarı kuralları ile erişimini denetler. 

> [!IMPORTANT]
> Merhaba SQL veritabanı güvenlik özelliklerine genel bakış için bkz: [SQL güvenliğine genel bakış](sql-database-security-overview.md). Bir öğretici için bkz: [Azure SQL veritabanınıza güvenli](sql-database-security-tutorial.md).

## <a name="firewall-and-firewall-rules"></a>Güvenlik duvarı ve güvenlik duvarı kuralları
Microsoft Azure SQL Veritabanı, Azure ile diğer İnternet tabanlı uygulamalar için ilişkisel veritabanı hizmeti sunar. toohelp verilerinizi korumaya, hangi bilgisayarların izniniz belirtmediğiniz sürece tüm erişim tooyour veritabanı sunucusu güvenlik duvarları engellemek. Merhaba Güvenlik Duvarı'nı her istek IP adresi kaynaklanan hello üzerinde dayalı erişim toodatabases verir. Daha fazla bilgi için bkz. [Azure SQL Veritabanı güvenlik duvarı kurallarına genel bakış](sql-database-firewall-configure.md)

Hello Azure SQL veritabanı hizmetinin yalnızca TCP bağlantı noktası 1433 ' kullanılabilir. bir SQL veritabanı bilgisayarınızdan tooaccess emin olun, istemci bilgisayar güvenlik duvarının TCP bağlantı noktası 1433 üzerinde giden TCP iletişimi sağlar. Başka uygulamalar için gerekli değilse 1433 numaralı bağlantı noktasından gelen TCP bağlantılarını engelleyin. 

Merhaba bağlantı işleminin bir parçası olarak, Azure sanal makinelerden yeniden yönlendirilen tooa farklı bir IP adresi ve bağlantı noktası, her çalışan rolü için benzersiz bağlantılardır. 11000 too11999 hello aralığında başlangıç bağlantı noktası numarası değil. TCP bağlantı noktaları hakkında daha fazla bilgi için bkz: [1433 ADO.NET 4.5 ve SQL Database2 dışındaki bağlantı noktaları](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="authentication"></a>Kimlik Doğrulaması

SQL Veritabanı iki kimlik doğrulaması türünü destekler:

* **SQL Kimlik Doğrulaması**: Kullanıcı adı ve parola kullanır. Veritabanınız için hello mantıksal sunucu oluşturduğunuzda, bir kullanıcı adı ve parola bir "sunucusuna yönetici" oturum açma belirttiniz. Bu kimlik bilgilerini kullanarak, tooany veritabanı hello veritabanı sahibi ya da "dbo." olarak bu sunucu üzerinde doğrulanabilir 
* **Azure Active Directory Kimlik Doğrulaması**: Azure Active Directory tarafından yönetilen kimlikleri kullanır, yönetilen ve tümleşik etki alanları ile kullanılabilir. [Mümkün olduğunda](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) Active Directory kimlik doğrulamasını (tümleşik güvenlik) kullanın. Azure Active Directory kimlik doğrulaması toouse istiyorsanız, hello "tooadminister Azure AD kullanıcıları ve grupları izin Azure AD yönetim," adlı başka bir sunucu yöneticisinin oluşturmanız gerekir. Bu yönetici normal bir sunucu yöneticisinin gerçekleştirebileceği tüm işlemleri yapabilir. Bkz: [tooSQL veritabanı tarafından kullanarak Azure Active Directory kimlik doğrulaması bağlanma](sql-database-aad-authentication.md) nasıl bir kılavuz için toocreate Azure AD yönetim tooenable Azure Active Directory kimlik doğrulaması.

Merhaba veritabanı altyapısı 30 dakikadan fazla boşta kalabileceği bağlantıları kapatır. Merhaba bağlantı kullanılabilmesi için önce oturum açma yeniden gerekir. Sürekli olarak (Merhaba veritabanı altyapısı tarafından gerçekleştirilen) yeniden kimlik doğrulama gerektiren etkin bağlantıları tooSQL veritabanı en az 10 saatte bir. Merhaba veritabanı altyapısı hello başlangıçta gönderilen parola kullanarak yeniden kimlik doğrulama girişimleri ve kullanıcının herhangi bir giriş gereklidir. SQL veritabanı'nda bir parola sıfırlama performans nedenleriyle hello bağlantı değil yeniden kimlik doğrulaması, bile tooconnection havuzu son hello bağlantıyı sıfırlar. Bu şirket içi SQL Server'ın hello davranışından farklıdır. Merhaba parola Hello bağlantı ilk başta yetkilendirildi beri değiştirilmişse hello bağlantısı sonlandırıldı ve hello yeni parolayı kullanarak yeni bir bağlantı oluşturulmasıyla. Merhaba sahip bir kullanıcı `KILL DATABASE CONNECTION` izni açıkça sonlandırmak bağlantı tooSQL veritabanı hello kullanarak [KILL](https://docs.microsoft.com/sql/t-sql/language-elements/kill-transact-sql) komutu.

Kullanıcı hesapları hello ana veritabanında oluşturulabilir ve hello sunucudaki tüm veritabanlarına izin verilebilir veya hello veritabanında kendisini (kapsanan kullanıcılar olarak adlandırılır) oluşturulabilir. Oturum açma bilgisi oluşturma ve yönetme hakkında bilgi için bkz. [Oturum açma bilgilerini yönetme](sql-database-manage-logins.md). tooenhance taşınabilirlik ve scalabilty, kapsanan veritabanı kullanıcıları tooenhance ölçeklenebilirlik kullanın. Bağımsız kullanıcılar hakkında daha fazla bilgi için bkz. [Bağımsız Veritabanı Kullanıcıları - Veritabanınızı Taşınabilir Hale Getirme](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), [CREATE USER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-user-transact-sql) ve [Bağımsız Veritabanları](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases).

En iyi uygulama olarak, uygulamanızı bir adanmış hesap tooauthenticate--toohello uygulama hello izinler sınırlayabilir ve güvenlik açığı tooa SQL ekleme, uygulama kodunuzun olması durumunda kötü amaçlı etkinliğin hello riskleri azaltmak bu şekilde kullanmanız gerekir saldırı. Merhaba önerilen yaklaşımdır toocreate bir [kapsanan veritabanı kullanıcı](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), uygulama tooauthenticate sağlayan doğrudan toohello veritabanı. 

## <a name="authorization"></a>Yetkilendirme

Yetkilendirme başvuruyor toowhat bir kullanıcı bir Azure SQL veritabanı içinde yapabilirsiniz ve bu kullanıcı hesabınızın veritabanı tarafından denetlenen [rol üyeliklerini](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) ve [nesne düzeyi izinleri](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine). En iyi uygulama, gerekli en düşük ayrıcalık kullanıcılar hello vermeniz gerekir. Merhaba server yönetici hesabı ile bağlanan yetkilisi toodo hello veritabanı içinde herhangi bir şey sahip db_owner üyesidir. Bu hesabı şema yükseltmeleri ve diğer yönetimsel işlemlerde kullanmak üzere saklayın. Merhaba ile uygulama toohello veritabanından daha kısıtlı izinleri tooconnect ile Merhaba "ApplicationUser" hesabı kullanmak, uygulamanız tarafından gerekli en düşük ayrıcalık. Daha fazla bilgi için bkz. [Oturum açma bilgilerini yönetme](sql-database-manage-logins.md).

Genellikle, yalnızca Yöneticiler toohello erişim `master` veritabanı. Rutin erişim tooeach kullanıcı veritabanı her veritabanında oluşturulan yönetici olmayan kapsanan veritabanı kullanıcıları arasında olmalıdır. Kapsanan veritabanı kullanıcıları kullandığınızda, hello toocreate oturumlar gerekmez `master` veritabanı. Daha fazla bilgi için bkz. [Bağımsız Veritabanı Kullanıcıları - Veritabanınızı Taşınabilir Hale Getirme](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable).

Kendiniz kullanılan toolimit ya da izinleri yükseltmesine özellikler aşağıdaki hello ile kazanmalısınız:   
* [Kimliğe bürünme](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server) ve [imzalama Modülü](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/signing-stored-procedures-in-sql-server) olması kullanılan toosecurely yükseltmesine izinleri geçici olarak.
* [Satır Düzeyinde Güvenlik](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) ile bir kullanıcının erişebileceği satırlar sınırlandırılabilir.
* [Veri maskeleme](sql-database-dynamic-data-masking-get-started.md) gizli verilerin açığa kullanılan toolimit olabilir.
* [Saklı yordamlar](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) kullanılan toolimit hello veritabanı üzerinde gerçekleştirilecek hello eylemler olabilir.

## <a name="next-steps"></a>Sonraki adımlar

- Merhaba SQL veritabanı güvenlik özelliklerine genel bakış için bkz: [SQL güvenliğine genel bakış](sql-database-security-overview.md).
- güvenlik duvarı kuralları hakkında daha fazla toolearn bkz [güvenlik duvarı kuralları](sql-database-firewall-configure.md).
- Kullanıcılar ve oturumları hakkındaki toolearn bkz [oturumları yönetme](sql-database-manage-logins.md). 
- Öngörülü izleme hakkında bilgi için bkz [veritabanı denetimi](sql-database-auditing.md) ve [SQL veritabanı tehdit algılama](sql-database-threat-detection.md).
- Bir öğretici için bkz: [Azure SQL veritabanınıza güvenli](sql-database-security-tutorial.md).
