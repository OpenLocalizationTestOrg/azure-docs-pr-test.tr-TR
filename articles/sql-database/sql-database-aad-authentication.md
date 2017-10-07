---
title: "aaaAzure Active Directory kimlik doğrulama - Azure SQL (genel bakış) | Microsoft Docs"
description: "Hakkında bilgi edinin SQL Database ve SQL Data Warehouse ile kimlik doğrulaması için Azure Active Directory toouse"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/11/2017
ms.author: rickbyh
ms.openlocfilehash: 7a63a162653b65294e11d3fa5bf39c320e742854
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-active-directory-authentication-for-authentication-with-sql-database-or-sql-data-warehouse"></a>SQL Database veya SQL Data Warehouse ile kimlik doğrulaması için Azure Active Directory kimlik doğrulaması kullanma
Azure Active Directory kimlik doğrulama mekanizmasıdır tooMicrosoft Azure SQL veritabanına bağlanma bir ve [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) kimlikleri Azure Active Directory (Azure AD) kullanarak. Azure AD kimlik doğrulaması ile veritabanı kullanıcıları hello kimlikleri ve diğer Microsoft Hizmetleri tek bir merkezi konumda merkezi olarak yönetebilir. Merkezi kimlik yönetimi toomanage veritabanı kullanıcıları tek bir yer sağlar ve izin yönetimini basitleştirir. Merhaba aşağıdaki yararları:

* Bir alternatif tooSQL sunucu kimlik doğrulaması sağlar.
* Yardımcı veritabanı sunucuları arasında kullanıcı kimlikleri hello artışı durdurun.
* Tek bir yerde parola döndürme sağlar
* Müşteriler, dış (AAD) gruplarını kullanarak veritabanı izinlerini yönetebilir.
* Tümleşik Windows kimlik doğrulaması ve Azure Active Directory tarafından desteklenen kimlik doğrulama başka biçimlerde etkinleştirerek bunu depolanmasını parolaları ortadan kaldırabilirsiniz.
* Azure AD kimlik doğrulaması kapsanan veritabanı kullanıcıları tooauthenticate kimlikleri hello veritabanı düzeyinde kullanır.
* Azure AD tooSQL veritabanına bağlanan uygulamalar için belirteç tabanlı kimlik doğrulamasını destekler.
* Azure AD kimlik doğrulaması, bir yerel Azure Active Directory etki alanı eşitleme olmadan için ADFS (etki alanı Federasyonu) veya yerel kullanıcı/parola kimlik doğrulamasını destekler.  
* Azure AD, Active Directory Evrensel çok faktörlü kimlik doğrulama (MFA) içeren kimlik doğrulaması kullanan SQL Server Management Studio bağlantılarını destekler.  MFA kolay doğrulama seçeneklerini aralıklı güçlü kimlik doğrulaması içerir — telefon araması, SMS mesajı, akıllı kartlar ve PIN ya da mobil uygulama bildirimi. Daha fazla bilgi için bkz: [SSMS desteklemek için SQL Database ve SQL Data Warehouse ile Azure AD MFA](sql-database-ssms-mfa-authentication.md).  

>  [!NOTE]  
>  Bir Azure VM çalıştıran sunucu bir Azure Active Directory hesabı kullanarak desteklenmiyor tooSQL bağlanılıyor. Etki alanı Active Directory hesabı kullanın.  

Hello yapılandırma adımları aşağıdaki yordamları tooconfigure hello içerir ve Azure Active Directory kimlik doğrulaması kullanın.

1. Oluşturma ve Azure AD doldurabilirsiniz.
2. İsteğe bağlı: İlişkilendirmek veya şu anda Azure aboneliğinizle ilişkili hello active directory değiştirin.
3. Azure SQL server için Azure Active Directory Yöneticisi oluşturmak veya [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
4. İstemci bilgisayarları yapılandırın.
5. Kapsanan veritabanı kullanıcıları AD kimlikleri, eşlenen veritabanı tooAzure oluşturun.
6. Tooyour veritabanı Azure AD kimlikleri kullanarak bağlanın.

> [!NOTE]
> toolearn nasıl toocreate ve Azure AD doldurmak ve ardından Azure SQL Database ve SQL Data Warehouse ile Azure AD yapılandırmak için bkz [yapılandırma Azure AD ile Azure SQL veritabanı](sql-database-aad-authentication-configure.md).
>

## <a name="trust-architecture"></a>Güven mimarisi
üst düzey diyagramı aşağıdaki hello Azure SQL veritabanı ile Azure AD kimlik doğrulaması kullanarak hello çözüm mimarisi özetler. Merhaba aynı kavramlar tooSQL veri ambarı uygulanır. toosupport Azure AD yerel kullanıcı parolası, yalnızca hello bulut bölümünün ve Azure AD/Azure SQL veritabanı olarak kabul edilir. toosupport federe kimlik doğrulaması (veya kullanıcı/parola için Windows kimlik bilgileri) ADFS bloğu ile Merhaba iletişim gereklidir. Merhaba okları iletişimi yollarıyla gösterir.

![aad kimlik doğrulama diyagramı][1]

Merhaba Aşağıdaki diyagramda hello federasyon güven ve barındırma bir belirteç göndererek istemci tooconnect tooa veritabanı olanak ilişkileri gösterir. Merhaba belirteci bir Azure AD tarafından kimlik doğrulaması ve hello veritabanı tarafından güvenilir. Müşteri 1, yerel kullanıcıları olan bir Azure Active Directory veya bir Azure AD ile Federasyon kullanıcıları temsil edebilir. Müşteri 2 içeri aktarılan kullanıcılar dahil olmak üzere olası bir çözüm temsil eder; Bu örnekte, bir Federasyon Azure Active Directory'den Azure Active Directory ile eşitlenmesini ADFS ile geliyor. Azure AD kimlik doğrulaması kullanarak tooa veritabanına erişim toounderstand abonelik barındırma bu hello ilişkili toohello Azure AD gerektirir önemlidir. Merhaba aynı abonelik kullanılan toocreate hello SQL Server barındırma hello Azure SQL Database veya SQL Data Warehouse olması gerekir.

![Abonelik ilişkisi][2]

## <a name="administrator-structure"></a>Yönetici yapısı
Azure AD kimlik doğrulaması kullanırken, hello SQL veritabanı sunucusu için iki yönetici hesapları vardır; Özgün SQL Server Yöneticisi ve hello Azure AD yönetici hello. Merhaba aynı kavramlar tooSQL veri ambarı uygulanır. Yalnızca bir Azure AD hesabına göre hello Yöneticisi hello ilk yer alan Azure AD veritabanı kullanıcısı kullanıcı veritabanında oluşturabilir. Hello Azure AD yönetici oturum açma adı, bir Azure AD kullanıcısının veya bir Azure AD grubu olabilir. Hello Yöneticisi bir grup hesabı olduğunda hello SQL Server örneği için birden çok Azure AD yöneticilerin sağlayarak, herhangi bir grup üyesi tarafından kullanılabilir. Yönetici toocentrally tanıyarak yönetilebilirliği geliştirir gibi grup hesabını kullanarak ekleyin ve hello kullanıcıları veya SQL veritabanı izinleri değiştirmeden Azure AD'de Grup üyeleri kaldırın. Herhangi bir anda yalnızca bir Azure AD Yöneticisi (kullanıcı veya grup) yapılandırılabilir.

![Yönetici yapısı][3]

## <a name="permissions"></a>İzinler
toocreate yeni kullanıcılara, hello olmalıdır `ALTER ANY USER` hello veritabanındaki izni. Merhaba `ALTER ANY USER` iznine tooany veritabanı kullanıcısı sahip. Merhaba `ALTER ANY USER` izni hello server yönetici hesabı ve hello olan veritabanı kullanıcılar tarafından tutulan de `CONTROL ON DATABASE` veya `ALTER ON DATABASE` izni bu veritabanı için ve hello üyeleri tarafından `db_owner` veritabanı rolü.

toocreate bir kapsanan veritabanı kullanıcı Azure SQL Database veya SQL Data Warehouse, Azure AD kimlik kullanarak toohello veritabanı bağlanmanız gerekir. toocreate hello ilk kapsanan veritabanı kullanıcı, (Merhaba veritabanı hello sahibi) Azure AD yönetici kullanarak toohello veritabanı bağlanmanız gerekir. Bu adım 4 ve 5 aşağıda gösterilmiştir. Herhangi bir Azure AD kimlik doğrulaması, yalnızca Azure SQL Database veya SQL veri ambarı sunucusu için hello Azure AD yönetim oluşturulduysa mümkündür. Hello Azure Active Directory Yöneticisi hello sunucudan kaldırdıysanız, SQL Server içinde daha önce oluşturduğunuz var olan Azure Active Directory Kullanıcıları artık Azure Active Directory kimlik bilgilerini kullanarak toohello veritabanı bağlanabilir.

## <a name="azure-ad-features-and-limitations"></a>Azure AD özellikleri ve sınırlamaları
Azure AD üyeleri aşağıdaki hello Azure SQL server veya SQL Data Warehouse sağlanabilir:

* Yerel üyeleri: Azure AD'de oluşturulan hello yönetilen etki alanında veya bir müşteri etki alanının bir üyesi. Daha fazla bilgi için bkz: [kendi etki alanı adı tooAzure AD eklemek](../active-directory/active-directory-add-domain.md).
* Federasyon etki alanı üyeleri: federe bir etki alanı ile Azure AD'de oluşturulan üyesi. Daha fazla bilgi için bkz: [Microsoft Azure artık Windows Server Active Directory ile Federasyon destekler](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/).
* Yerel veya Federasyon etki alanına üye olan alınan üyelerinden diğer Azure AD.
* Active Directory grupları güvenlik grupları oluşturuldu.

Microsoft hesapları (örneğin, outlook.com, hotmail.com, live.com) veya diğer Konuk hesapları (örneğin gmail.com, yahoo.com) desteklenmez. Çok oturum açabilir,[https://login.live.com](https://login.live.com) bir Microsoft hesabı kullanarak hello hesap ve parola kullanılarak, desteklenmeyen Azure AD kimlik doğrulaması Azure SQL Database veya Azure SQL Data Warehouse için.

## <a name="connecting-using-azure-ad-identities"></a>Azure AD kimlikleri kullanarak bağlanma

Azure Active Directory kimlik doğrulama yöntemleri kullanarak Azure AD kimlikleri bağlanan tooa veritabanının aşağıdaki hello destekler:

* Tümleşik Windows kimlik doğrulaması kullanma
* Bir Azure AD asıl adı ve parola kullanarak
* Uygulama belirteci kimlik doğrulaması kullanma

### <a name="additional-considerations"></a>Diğer konular

* tooenhance yönetilebilirlik önerilir adanmış bir Azure AD sağlamak yönetici olarak grup.   
* Yalnızca bir Azure AD Yöneticisi (kullanıcı veya grup) herhangi bir zamanda bir Azure SQL server ya da Azure SQL Data Warehouse için yapılandırılabilir.   
* Yalnızca SQL Server için Azure AD yönetici başlangıçta toohello Azure SQL server veya Azure SQL Data Warehouse bir Azure Active Directory hesabı kullanarak bağlanabilir. Merhaba Active Directory Yöneticisi sonraki Azure AD yapılandırabilir veritabanı kullanıcılar.   
* Merhaba bağlantı zaman aşımı too30 saniye ayarı öneririz.   
* SQL Server 2016 Management Studio'yu ve SQL Server veri araçları Visual Studio 2015 (2016 veya sonraki sürüm 14.0.60311.1April) için Azure Active Directory kimlik doğrulamasını destekler. (Azure AD kimlik doğrulaması hello tarafından desteklenen **SqlServer için .NET Framework veri sağlayıcısı**; en az sürüm .NET Framework 4.6). Bu nedenle bu araçların yeni sürümlerin hello ve veri katmanı uygulamaları (DAC ve .bacpac) Azure AD kimlik doğrulaması kullanabilirsiniz.   
* [ODBC sürüm 13,1](https://www.microsoft.com/download/details.aspx?id=53339) Azure Active Directory kimlik doğrulaması ancak destekler `bcp.exe` daha eski bir ODBC sağlayıcısını kullandığından Azure Active Directory kimlik doğrulaması kullanarak bağlanamıyor.   
* `sqlcmd`Azure Active Directory kimlik doğrulaması başına 13,1 hello kullanılabilir sürümüyle destekleyen [Yükleme Merkezi'nden](http://go.microsoft.com/fwlink/?LinkID=825643).   
* SQL Server veri araçları Visual Studio 2015 için en azından hello Nisan 2016 sürümünü hello veri Araçları (sürüm 14.0.60311.1). Şu anda Azure AD kullanıcılarının SSDT nesne Gezgini'nde gösterilmez. Geçici bir çözüm olarak hello kullanıcılar görüntülemek [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).   
* [SQL Server için Microsoft JDBC sürücüsü 6.0](https://www.microsoft.com/download/details.aspx?id=11774) destekleyen Azure AD kimlik doğrulama. Ayrıca bkz [hello bağlantı özelliklerini ayarlama](https://msdn.microsoft.com/library/ms378988.aspx).   
* PolyBase, Azure AD kimlik doğrulama kullanarak kimlik doğrulaması yapamaz.   
* Azure AD kimlik doğrulama SQL veritabanı için Azure portal hello tarafından desteklenen **alma veritabanı** ve **verme veritabanı** dikey pencereleri. İçeri ve dışarı aktarma Azure AD kimlik doğrulaması kullanarak hello PowerShell komutunu da desteklenir.   
* Azure AD kimlik doğrulaması, CLI kullanarak SQL Database ve SQL Data Warehouse için desteklenir. Daha fazla bilgi için bkz: [yapılandırma ve SQL Database veya SQL Data Warehouse ile Azure Active Directory kimlik doğrulamasını yönetmek](sql-database-aad-authentication-configure.md) ve [SQL Server - az sql server](https://docs.microsoft.com/en-us/cli/azure/sql/server).

## <a name="next-steps"></a>Sonraki adımlar
- toolearn nasıl toocreate ve Azure AD doldurmak ve ardından Azure SQL Database veya Azure SQL Data Warehouse ile Azure AD yapılandırmak için bkz [yapılandırma ve SQL Database veya SQL Data Warehouse ile Azure Active Directory kimlik doğrulamasını yönetmek](sql-database-aad-authentication-configure.md).
- SQL Veritabanında erişim ve denetime genel bakış için bkz. [SQL Veritabanında erişim ve denetim](sql-database-control-access.md).
- SQL Veritabanındaki oturum açma bilgileri, kullanıcılar ve veritabanı rollerine genel bakış için bkz. [Oturum açma bilgileri, kullanıcılar ve veritabanı rolleri](sql-database-manage-logins.md).
- Veritabanı sorumluları hakkında daha fazla bilgi için bkz. [Sorumlular](https://msdn.microsoft.com/library/ms181127.aspx).
- Veritabanı rolleri hakkında daha fazla bilgi için bkz. [Veritabanı rolleri](https://msdn.microsoft.com/library/ms189121.aspx).
- SQL Veritabanındaki güvenlik duvarı kuralları hakkında daha fazla bilgi için bkz. [SQL Veritabanı güvenlik duvarı kuralları](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[9]: ./media/sql-database-aad-authentication/9ad-settings.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/11connect-using-int-auth.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db.png

