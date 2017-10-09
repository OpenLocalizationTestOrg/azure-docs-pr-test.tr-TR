---
title: "aaaMulti öğeli kimlik doğrulama - Azure SQL | Microsoft Docs"
description: "Kimlik doğrulaması çoklu oluşturmak SSMS ile SQL veritabanı ve SQL Data Warehouse için kullanın."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: fbd6e644-0520-439c-8304-2e4fb6d6eb91
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2017
ms.author: rickbyh
ms.openlocfilehash: 57ef63b7c7f2c5cf64c3e1ee194d865ee5b14177
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="universal-authentication-with-sql-database-and-sql-data-warehouse-ssms-support-for-mfa"></a>SQL Database ve SQL Data Warehouse (MFA desteği SSMS) ile Evrensel kimlik doğrulaması
Azure SQL Database ve Azure SQL Data Warehouse desteği SQL Server Management Studio (SSMS) kullanarak bağlantıları *Active Directory Evrensel kimlik doğrulaması*. 
**İndirme son SSMS hello** - hello istemci bilgisayarda hello SSMS, en son sürümünü indirin [karşıdan SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Merhaba, tüm özellikler için bu konudaki en az Temmuz 2017, sürüm 17,2 kullanın.  Merhaba en son bağlantı iletişim kutusu, şöyle görünür: ![1mfa Evrensel bağlanmak](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png "Completes hello kullanıcı adı kutusunu.")  

## <a name="hello-five-authentication-options"></a>Merhaba beş kimlik doğrulama seçenekleri  
- Active Directory Evrensel kimlik doğrulaması hello iki etkileşimli olmayan kimlik doğrulama yöntemlerini destekler (`Active Directory - Password` kimlik doğrulama ve `Active Directory - Integrated` kimlik doğrulaması). Etkileşimli olmayan `Active Directory - Password` ve `Active Directory - Integrated` birçok farklı uygulamalarda (ADO.NET, JDBC, ODBC, vb.) kimlik doğrulama yöntemleri kullanılabilir. Bu iki yöntem hiçbir zaman açılır iletişim kutularında neden.

- `Active Directory - Universal with MFA`kimlik doğrulama yöntemidir de destekleyen bir etkileşimli *Azure çok faktörlü kimlik doğrulaması* (MFA). Azure MFA kullanıcı talebine basit bir oturum açma işlemi için buluştururken koruma erişim toodata ve uygulamaları yardımcı olur. İzin verme kullanıcılar toochoose hello yöntemi tercih kolay doğrulama seçeneklerini (telefon araması, SMS mesajı, akıllı kart PIN ya da mobil uygulama bildirimi ile), aralıklı güçlü kimlik doğrulaması sunar. Azure AD ile etkileşimli MFA doğrulama için bir açılır iletişim kutusu neden olabilir.

Çok faktörlü kimlik doğrulaması açıklaması için bkz: [çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md).
Yapılandırma adımları için bkz: [SQL Server Management Studio Azure SQL veritabanını yapılandırma çok faktörlü kimlik doğrulamasını](sql-database-ssms-mfa-authentication-configure.md).

### <a name="azure-ad-domain-name-or-tenant-id-parameter"></a>Azure AD etki alanı adı veya Kiracı kimliği parametresi   

İle başlayarak [SSMS sürümü 17](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), hello içeri aktarılan kullanıcılar Konuk kullanıcılar gibi diğer Azure Active dizinleri geçerli Active Directory'den hello Azure AD etki alanı adı sağlayın, veya bağlandıklarında kimlik Kiracı. Konuk kullanıcılar diğer Azure reklam, outlook.com, hotmail.com, live.com gibi Microsoft hesapları ya da gmail.com gibi diğer hesapları davet kullanıcıları içerir. Bu bilgiler verir **Active Directory Evrensel MFA kimlik doğrulaması ile** tooidentify hello yetkilisi kimlik doğrulaması doğru. Bu seçenek, aynı zamanda outlook.com, hotmail.com, live.com veya MSA olmayan hesapları gibi gerekli toosupport Microsoft hesaplarını (MSA) olur. Evrensel kimlik doğrulaması kullanılarak kimlik doğrulaması toobe kendi Azure AD etki alanı adı veya Kiracı girmelisiniz. istediğiniz tüm bu kullanıcıların kimliği Bu parametre hello geçerli Azure AD etki alanı adı/Kiracı kimliği hello Azure sunucusu ile bağlantılı temsil eder. Örneğin, Azure sunucusu Azure AD etki alanı ile ilişkili ise `contosotest.onmicrosoft.com` burada kullanıcı `joe@contosodev.onmicrosoft.com` Azure AD etki alanından alınan bir kullanıcı olarak barındırılan `contosodev.onmicrosoft.com`, bu kullanıcının etki alanı adı gerekli tooauthenticate hello `contosotest.onmicrosoft.com`. Merhaba kullanıcı hello Azure AD bağlı tooAzure sunucu, yerel kullanıcı ve MSA hesabı değil, etki alanı adı veya Kiracı Kimliği gereklidir. Merhaba tooenter hello parametresi (SSMS sürümü 17,2 başlayarak), **tooDatabase bağlanmak** iletişim kutusu, tam hello iletişim kutusu, seçme **Active Directory - Evrensel MFA ile** kimlik doğrulaması tıklatın **seçenekleri**, tam hello **kullanıcı adı** kutusuna ve ardından hello tıklatın **bağlantı özelliklerini** sekmesi. Merhaba denetleyin **AD etki alanı adı veya Kiracı kimliği** kutusunda ve hello etki alanı adı gibi kimlik doğrulama yetkisi sağlayın (**contosotest.onmicrosoft.com**) veya GUID hello Kiracı kimliğinin hello  
   ![mfa Kiracı ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   

### <a name="azure-ad-business-toobusiness-support"></a>Azure AD iş toobusiness desteği   
Konuk kullanıcı olarak Azure AD B2B senaryolarını desteklenen azure AD kullanıcıları (bkz [Azure B2B işbirliği nedir](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)) tooSQL veritabanı ve SQL Data Warehouse yalnızca geçerli Azure AD'de oluşturulan ve el ile eşleştirilmiş bir grubun üyeleri bir parçası olarak bağlanabilir Merhaba Transact-SQL kullanarak `CREATE USER` verilen bir veritabanı deyiminde. Örneğin, varsa `steve@gmail.com` davet edilen tooAzure AD olduğu `contosotest` (hello Azure Ad etki alanı ile `contosotest.onmicrosoft.com`), gibi Azure AD grup `usergroup` hello hello içeren Azure AD oluşturulmalıdır `steve@gmail.com` üyesi. Ardından, bu grubun belirli bir veritabanı (yani Veritabanım) için Azure AD SQL yönetici ya da Azure AD DBO tarafından bir Transact-SQL yürüterek oluşturulmalıdır `CREATE USER [usergroup] FROM EXTERNAL PROVIDER` deyimi. Merhaba veritabanı kullanıcısı oluşturulduktan sonra kullanıcı hello `steve@gmail.com` çok oturum açabileceğiniz`MyDatabase` hello SSMS kimlik doğrulaması seçeneği kullanılarak `Active Directory – Universal with MFA support`. Merhaba usergroup, varsayılan olarak, yalnızca izni ve hello verilen toobe gerekir herhangi başka bir veri erişim bağlanmak hello sahip normal şekilde. Lütfen bu kullanıcının Not `steve@gmail.com` Konuk kullanıcı hello kutuyu işaretleyin ve hello AD etki alanı adı ekleme gibi `contosotest.onmicrosoft.com` hello SSMS içinde **bağlantı özelliği** iletişim kutusu. Merhaba **AD etki alanı adı veya Kiracı kimliği** seçeneği hello Evrensel MFA bağlantı seçenekleri ile için desteklenen yalnızca, aksi takdirde, devre dışı.

## <a name="universal-authentication-limitations-for-sql-database-and-sql-data-warehouse"></a>SQL Database ve SQL Data Warehouse için evrensel kimlik doğrulama kısıtlamaları
* SSMS ve SqlPackage.exe Active Directory Evrensel kimlik doğrulaması üzerinden MFA için şu anda etkin hello yalnızca araçlardır.
* SSMS sürümü 17,2, çok kullanıcılı eş zamanlı erişim MFA ile Evrensel kimlik doğrulaması kullanarak destekler. Sürüm 17,0 ve 17,1, Evrensel kimlik doğrulama tooa tek Azure Active Directory hesabı kullanarak SSMS örneği için bir oturum açma kısıtlı. başka bir Azure AD hesabı olarak toolog içinde SSMS başka bir örneğini kullanmanız gerekir. (Bu kısıtlama sınırlı tooActive Directory Evrensel kimlik doğrulaması; toodifferent sunucuları Active Directory parola kimlik doğrulaması, Active Directory tümleşik kimlik doğrulaması veya SQL Server kimlik doğrulaması kullanarak oturum açabilir).
* SSMS Nesne Gezgini, sorgu Düzenleyicisi'ni ve sorgu deposu görselleştirme için Active Directory Evrensel kimlik doğrulamasını destekler.
* SSMS sürümü 17,2 Extract/dışa aktarma/dağıtma veri veritabanı için DacFx Sihirbazı desteği sağlar. Belirli bir kullanıcı hello ilk kimlik doğrulaması iletişim kutusundan Evrensel kimlik doğrulamasını kullanarak kimlik doğrulaması gerçekleştikten sonra hello DacFx Sihirbazı işlevleri aynı hello şekilde diğer tüm kimlik doğrulama yöntemleri için bunu yapar.
* Merhaba SSMS Tablo Tasarımcısı Evrensel kimlik doğrulamasını desteklemez.
* SSMS desteklenen bir sürümünü kullanmanız gerekir ancak bu Active Directory Evrensel kimlik doğrulaması için ek yazılım gereksinimi yoktur.  
* Merhaba Active Directory Authentication Library (ADAL) sürüm Evrensel kimlik doğrulaması için güncelleştirilmiş tooits en son yayımlanan ADAL.dll 3.13.9 kullanılabilir sürüm oluştu. Bkz: [Active Directory Authentication Library 3.14.1](http://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).


## <a name="next-steps"></a>Sonraki adımlar

- Yapılandırma adımları için bkz: [SQL Server Management Studio Azure SQL veritabanını yapılandırma çok faktörlü kimlik doğrulamasını](sql-database-ssms-mfa-authentication-configure.md).
- Başkalarının tooyour veritabanına erişim izni: [SQL veritabanı kimlik doğrulaması ve yetkilendirme: erişim verme](sql-database-manage-logins.md)  
- Başkalarının hello güvenlik duvarı üzerinden bağlanabilir emin olun: [yapılandırma bir Azure SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı kullanarak hello Azure portalı](sql-database-configure-firewall-settings.md)  
- [Yapılandırma ve SQL Database veya SQL Data Warehouse ile Azure Active Directory kimlik doğrulaması yönetme](sql-database-aad-authentication-configure.md)  
- [Microsoft SQL Server veri katmanı uygulaması çerçevesi (17.0.0 GA)](https://www.microsoft.com/download/details.aspx?id=55088)  
- [SQLPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)  
- [Bir BACPAC dosya tooa alma yeni Azure SQL veritabanı](../sql-database/sql-database-import.md)  
- [Bir Azure SQL veritabanı tooa BACPAC dosyası dışarı aktarma](../sql-database/sql-database-export.md)  
- C# arabirimi [IUniversalAuthProvider arabirimi](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)  
