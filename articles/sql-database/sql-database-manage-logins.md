---
title: "aaaAzure SQL oturumları ve kullanıcıları | Microsoft Docs"
description: "Bilgi SQL veritabanı güvenlik yönetimi hakkında özellikle nasıl toomanage veritabanı hello sunucu düzeyinde asıl hesap üzerinden erişim ve oturum açma güvenlik."
keywords: "sql veritabanı güvenliği,veritabanı güvenliği yönetimi,oturum açma güvenliği,veritabanı güvenliği,veritabanı erişimi"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 0a65a93f-d5dc-424b-a774-7ed62d996f8c
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/23/2017
ms.author: rickbyh
ms.openlocfilehash: dff889b9fed09146a10008c0d11ca9e71d91df5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-and-granting-database-access"></a>Denetleme ve veritabanına erişim izni verme

Güvenlik duvarı kuralları yapılandırıldığında, kişiler tooa SQL veritabanı hello yönetici hesapları biri olarak, hello veritabanı sahibi veya hello veritabanındaki bir veritabanı kullanıcısı olarak bağlanabilir.  

>  [!NOTE]  
>  Bu konu, tooAzure SQL server ve hello Azure SQL sunucusunda oluşturulan tooboth SQL Database ve SQL veri ambarı veritabanlarını geçerlidir. Kolaylık olması için SQL veritabanı tooboth SQL Database ve SQL Data Warehouse söz konusu olduğunda kullanılır. 
>

> [!TIP]
> Bir öğretici için bkz: [Azure SQL veritabanınıza güvenli](sql-database-security-tutorial.md).
>


## <a name="unrestricted-administrative-accounts"></a>Kısıtlanmamış yönetici hesapları
Yönetici işlevlerine sahip iki yönetici hesabı (**Sunucu yöneticisi** ve **Active Directory yöneticisi**) vardır. Bu yönetici hesapları, SQL server için tooidentify açmak Azure portal hello ve SQL server'ınızdaki toohello özelliklerini gidin.

![SQL Server Yöneticileri](./media/sql-database-manage-logins/sql-admins.png)

- **Sunucu yöneticisi**   
Bir Azure SQL sunucusu oluşturduğunuzda **Sunucu yöneticisi oturum açma bilgileri** belirlemeniz gerekir. SQL server bu hesabı hello ana veritabanında bir oturum olarak oluşturur. Bu hesap SQL Server kimlik doğrulaması (kullanıcı adı ve parola) kullanarak bağlanır. Bu hesaplardan yalnızca biri mevcut olabilir.   
- **Azure Active Directory yöneticisi**   
Ayrıca, Azure Active Directory’deki bir adet kişi veya güvenlik grubu hesabı da yönetici olarak yapılandırılabilir. İsteğe bağlı tooconfigure Azure AD yönetici değil, ancak toouse Azure AD hesapları tooconnect tooSQL veritabanı istiyorsanız, Azure AD yönetici yapılandırılması gerekir. Azure Active Directory erişimi yapılandırma hakkında daha fazla bilgi için bkz: [bağlanıyor tooSQL veritabanı veya SQL veri ambarı tarafından kullanarak Azure Active Directory kimlik doğrulaması](sql-database-aad-authentication.md) ve [SSMS ile SQL Azure AD MFA için destekler. Veritabanı ve SQL Data Warehouse](sql-database-ssms-mfa-authentication.md).
 

Merhaba **sunucu yöneticisinin** ve **Azure AD Yönetim** hesaplarına hello aşağıdaki özelliklere sahip:
- Bunlar tooany SQL veritabanı hello sunucusunda otomatik olarak bağlanabilir hello yalnızca hesaplarıdır. (tooconnect tooa kullanıcı veritabanı, diğer hesapları olmalıdır hello hello sahibi veritabanı ya da hello kullanıcı veritabanında bir kullanıcı hesabına sahip.)
- Bu hesapları kullanıcı veritabanlarını hello girin `dbo` kullanıcı ve bunlar hello kullanıcı veritabanlarında tüm hello izinlere sahiptir. (bir kullanıcı veritabanı hello sahibi hello da hello veritabanı girer `dbo` kullanıcı.) 
- Bu hesapları hello girmeyin `master` veritabanı hello olarak `dbo` kullanıcı ve ana izinleri sınırlıdır. 
- Bu hesapları hello üyesi olmayan standart SQL Server `sysadmin` SQL veritabanında kullanılamaz sabit sunucu rolü.  
- Bu hesaplar, veritabanlarını, oturum açma bilgilerini, ana veritabanındaki kullanıcıları ve sunucu düzeyinde güvenlik duvarı kurallarını oluşturabilir, değiştirebilir ve kaldırabilir.
- Bu hesapları ekleme ve üyeleri toohello kaldırma `dbmanager` ve `loginmanager` rolleri.
- Bu hesapları hello görüntüleyebilirsiniz `sys.sql_logins` sistem tablosu.

### <a name="configuring-hello-firewall"></a>Merhaba güvenlik duvarını yapılandırma
Merhaba sunucu düzeyinde güvenlik duvarı tek tek bir IP adresi veya aralığı için yapılandırıldığında, hello **SQL server yönetici** ve hello **Azure Active Directory Yöneticisi** toohello asıl veritabanını ve tüm hello bağlanabilir kullanıcı veritabanları. Merhaba ilk sunucu düzeyinde güvenlik duvarı hello yapılandırılabilir [Azure portal](sql-database-get-started-portal.md)kullanarak [PowerShell](sql-database-get-started-powershell.md) veya hello kullanarak [REST API](https://msdn.microsoft.com/library/azure/dn505712.aspx). Bağlantı kurulduktan sonra [Transact-SQL](sql-database-configure-firewall-settings.md) kullanarak ek sunucu düzeyi güvenlik duvarı kuralları yapılandırılabilir.

### <a name="administrator-access-path"></a>Yönetici erişim yolu
Merhaba sunucu düzeyinde güvenlik duvarı düzgün şekilde yapılandırıldığında, hello **SQL server yönetici** ve hello **Azure Active Directory Yöneticisi** gibi SQL Server Management Studio veya SQL istemci araçları kullanarak bağlanabilir Server veri araçları. Yalnızca hello en yeni araçlara tüm hello özellik ve yetenekler sağlar. Merhaba Aşağıdaki diyagramda hello için tipik bir yapılandırma iki yönetici hesapları gösterir.

![Yönetici erişim yolu](./media/sql-database-manage-logins/1sql-db-administrator-access.png)

Açık bir bağlantı noktası hello sunucu düzeyinde Güvenlik Duvarı'nda kullanırken, yöneticiler tooany SQL veritabanına bağlanabilir.

### <a name="connecting-tooa-database-by-using-sql-server-management-studio"></a>SQL Server Management Studio'yu kullanarak tooa veritabanına bağlanma
Bir sunucu, bir veritabanı, sunucu düzeyinde güvenlik duvarı kuralları oluşturma ve SQL Server Management Studio tooquery bir veritabanını kullanarak bir kılavuz için bkz: [hello Azure portal kullanarak Azure SQL veritabanı sunucularının, veritabanları ve güvenlik duvarı kuralları kullanmaya başlama ve SQL Server Management Studio](sql-database-get-started-portal.md).

> [!IMPORTANT]
> Her zaman hello kullanmanız önerilir Management Studio tooremain en son sürümünü Azure ve SQL veritabanı güncelleştirmeleri tooMicrosoft ile eşitlenir. [SQL Server Management Studio’yu güncelleyin](https://msdn.microsoft.com/library/mt238290.aspx).


## <a name="additional-server-level-administrative-roles"></a>Ek sunucu düzeyinde yönetim rolleri
Ayrıca daha önce ele alınan toohello sunucu düzeyinde yönetim rolleri, SQL veritabanı iki kısıtlı yönetici rolleri hello ana veritabanı toowhich kullanıcı hesaplarında tooeither veritabanları oluşturma veya yönetme izinleri vermek eklenebilir sağlar oturum açma bilgileri.

### <a name="database-creators"></a>Veritabanı oluşturucuları
Bu yönetici rolleri biri hello **dbmanager** rol. Bu rolün üyeleri yeni veritabanları oluşturabilir. toouse bu rol, bir kullanıcı hello oluşturduğunuz `master` veritabanı ve hello kullanıcı toohello ekleme **dbmanager** veritabanı rolü. toocreate bir veritabanı, kullanıcı hello ana veritabanındaki bir SQL Server oturumu dayalı veya bir Azure Active Directory kullanıcı tabanlı veritabanı kullanıcısı bulunan hello kullanıcı olmalıdır.

1. Yönetici hesabı kullanarak, toohello ana veritabanına bağlanır.
2. İsteğe bağlı adım: hello kullanarak bir SQL Server kimlik doğrulama oturumu oluşturmak [oluşturma oturum açma](https://msdn.microsoft.com/library/ms189751.aspx) deyimi. Örnek deyim:
   
   ```
   CREATE LOGIN Mary WITH PASSWORD = '<strong_password>';
   ```
   
   > [!NOTE]
   > Oturum açma bilgileri veya bağımsız veritabanı kullanıcısı oluştururken güçlü bir parola kullanın. Daha fazla bilgi için bkz. [Güçlü Parolalar](https://msdn.microsoft.com/library/ms161962.aspx).
    
   tooimprove performans oturumları (sunucu düzeyi ilkeleri) geçici olarak hello veritabanı düzeyinde önbelleğe alınır. toorefresh hello kimlik doğrulama önbelleğini bkz [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx).

3. Merhaba ana veritabanında hello kullanarak bir kullanıcı oluşturun [kullanıcı oluştur](https://msdn.microsoft.com/library/ms173463.aspx) deyimi. Merhaba kullanıcı (ortamınız Azure AD kimlik doğrulaması için yapılandırdıysanız) bir Azure Active Directory kimlik doğrulaması bulunan veritabanı kullanıcısı, bir SQL Server kimlik doğrulaması bulunan veritabanı kullanıcısı veya bir SQL Server kimlik doğrulama kullanıcı bir SQL tabanlı olabilir Sunucu kimlik doğrulaması oturum açma (Merhaba önceki adımda oluşturduğunuz.) Örnek deyimler:
   
   ```
   CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
   CREATE USER Tran WITH PASSWORD = '<strong_password>';
   CREATE USER Mary FROM LOGIN Mary; 
   ```

4. Merhaba yeni kullanıcı, toohello eklemek **dbmanager** hello kullanarak veritabanı rolü [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx) deyimi. Örnek deyimler:
   
   ```
   ALTER ROLE dbmanager ADD MEMBER Mary; 
   ALTER ROLE dbmanager ADD MEMBER [mike@contoso.com];
   ```
   
   > [!NOTE]
   > Merhaba dbmanager veritabanı rolü ana veritabanında olduğundan yalnızca bir veritabanı kullanıcı toohello dbmanager rolü ekleyebilirsiniz. Bir sunucu düzeyindeki login toodatabase düzeyi rol ekleyemezsiniz.
    
5. Gerekirse, bir güvenlik duvarı kuralı tooallow hello yeni kullanıcı tooconnect yapılandırın. (Merhaba yeni kullanıcı var olan bir güvenlik duvarı kuralı tarafından ele.)

Şimdi hello kullanıcı toohello ana veritabanına bağlanabilir ve yeni veritabanları oluşturabilirsiniz. Merhaba veritabanı oluşturma hello hesabı hello veritabanının hello sahibi olur.

### <a name="login-managers"></a>Oturum açma yöneticileri
Merhaba diğer yönetim hello oturum açma yöneticisi rolü rolüdür. Bu rolün üyeleri hello ana veritabanında yeni oturumlar oluşturabilirsiniz. İsterseniz, tamamlayabilirsiniz hello aynı adımları (oturum açma ve kullanıcı oluşturun ve bir kullanıcı toohello ekleyin **loginmanager** rolü) tooenable bir kullanıcı toocreate hello ana yeni oturum açma bilgileri. Genellikle oturumları sırasında hello kimlik doğrulaması kapsanan veritabanı kullanıcıları kullanarak Microsoft önerir veritabanı oturum temel alarak kullanıcılara kullanmak yerine düzeyi gibi gerekli değildir. Daha fazla bilgi için bkz. [Bağımsız Veritabanı Kullanıcıları - Veritabanınızı Taşınabilir Hale Getirme](https://msdn.microsoft.com/library/ff929188.aspx).

## <a name="non-administrator-users"></a>Yönetici olmayan kullanıcılar
Genellikle, yönetici olmayan bir hesap toohello ana veritabanı erişmez. Hello kullanarak hello veritabanı düzeyinde kapsanan veritabanı kullanıcıları oluşturun [kullanıcı oluştur (Transact-SQL)](https://msdn.microsoft.com/library/ms173463.aspx) deyimi. Merhaba kullanıcı (ortamınız Azure AD kimlik doğrulaması için yapılandırdıysanız) bir Azure Active Directory kimlik doğrulaması bulunan veritabanı kullanıcısı, bir SQL Server kimlik doğrulaması bulunan veritabanı kullanıcısı veya bir SQL Server kimlik doğrulama kullanıcı bir SQL tabanlı olabilir Sunucu kimlik doğrulaması oturum açma (Merhaba önceki adımda oluşturduğunuz.) Daha fazla bilgi için bkz. [Bağımsız Veritabanı Kullanıcıları - Veritabanınızı Taşınabilir Hale Getirme](https://msdn.microsoft.com/library/ff929188.aspx). 

toocreate kullanıcılar toohello veritabanına bağlanmak ve örnekler aşağıdaki deyimleri benzer toohello yürütün:

```
CREATE USER Mary FROM LOGIN Mary; 
CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
```

Başlangıçta, yalnızca biri hello Yöneticiler veya hello veritabanının hello sahibi kullanıcıların oluşturabilirsiniz. tooauthorize ek kullanıcılar toocreate yeni kullanıcılara, vermek, seçilen kullanıcı hello `ALTER ANY USER` gibi bir deyimi kullanarak izni:

```
GRANT ALTER ANY USER tooMary;
```

toogive ek kullanıcılar tam denetim hello veritabanının hello üyesi olmalarını **db_owner** hello kullanarak sabit veritabanı rolünün `ALTER ROLE` deyimi.

> [!NOTE]
> Merhaba, oturum tabanlı en yaygın nedeni toocreate veritabanı kullanıcı sayısıdır toomultiple veritabanlarına erişim SQL Server kimlik doğrulaması kullanıcıların olduğunda. Oturum tabanlı bağlı toohello oturum açma ve bu oturum açma için korunur yalnızca bir parola kullanıcılardır. Ayrı veritabanlarındaki bağımsız veritabanı kullanıcıları, ayrı varlıklardır ve her biri kendi parolasına sahiptir. Bu durum, tüm veritabanları için aynı parolayı kullanmayan bağımsız veritabanı kullanıcıları için kafa karıştırıcı olabilir.

### <a name="configuring-hello-database-level-firewall"></a>Merhaba veritabanı düzeyi güvenlik duvarını yapılandırma
En iyi uygulama, yönetici olmayan kullanıcılar yalnızca kullandıkları hello güvenlik duvarı toohello veritabanları üzerinden erişimi olmalıdır. Kendi IP yetkilendirme yerine hello sunucu düzeyi aracılığıyla adresleri güvenlik duvarı ve erişim tooall veritabanları, onların hello kullan [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) deyimi tooconfigure hello veritabanı düzeyinde güvenlik duvarı. Merhaba veritabanı düzeyinde güvenlik duvarı hello portal kullanılarak yapılandırılamaz.

### <a name="non-administrator-access-path"></a>Yönetici olmayan kullanıcılar için erişim yolu
Merhaba veritabanı düzeyinde güvenlik duvarı düzgün şekilde yapılandırıldığında, hello veritabanı kullanıcıları SQL Server Management Studio gibi istemci araçlarını veya SQL Server veri araçları kullanarak bağlanabilir. Yalnızca hello en yeni araçlara tüm hello özellik ve yetenekler sağlar. Aşağıdaki diyagramda hello tipik yönetici olmayan erişim yolunu gösterir.

![Yönetici olmayan kullanıcılar için erişim yolu](./media/sql-database-manage-logins/2sql-db-nonadmin-access.png)

## <a name="groups-and-roles"></a>Gruplar ve roller
Etkili erişim yönetimi toogroups ve tek tek kullanıcılar yerine rolleri atanmış izinleri kullanır. 

- Azure Active Directory kimlik doğrulaması kullandığınızda Azure Active Directory kullanıcılarını bir Azure Active Directory grubuna ekleyin. Merhaba grup için bir kapsanan veritabanı kullanıcı oluşturun. Bir veya daha fazla veritabanı kullanıcıları içine yerleştirin bir [veritabanı rolü](https://msdn.microsoft.com/library/ms189121) ve atayın [izinleri](https://msdn.microsoft.com/library/ms191291.aspx) toohello veritabanı rolü.

- SQL Server kimlik doğrulamasını kullanırken, hello veritabanında kapsanan veritabanı kullanıcıları oluşturun. Bir veya daha fazla veritabanı kullanıcıları içine yerleştirin bir [veritabanı rolü](https://msdn.microsoft.com/library/ms189121) ve atayın [izinleri](https://msdn.microsoft.com/library/ms191291.aspx) toohello veritabanı rolü.

Merhaba veritabanı rolleri olabilir hello yerleşik roller gibi **db_owner**, **db_ddladmin**, **db_datawriter**, **db_datareader**, **db_denydatawriter**, ve **db_denydatareader**. **db_owner** yaygın olarak kullanılan toogrant tam izinleri tooonly birkaç kullanıcı sayısıdır. Merhaba diğer sabit veritabanı rollerinin basit bir veritabanı geliştirme hızlı bir şekilde almak için yararlıdır, ancak çoğu üretim veritabanları için önerilmez. Örneğin, hello **db_datareader** sabit veritabanı rolünün verir okuma erişimi tooevery genellikle hello veritabanı tablosunda birden fazla kesinlikle gerekli. Çok daha iyi toouse hello olan [ROL Oluştur](https://msdn.microsoft.com/library/ms187936.aspx) deyimi toocreate kendi kullanıcı tarafından tanımlanan veritabanı rolleri ve dikkatle her rol hello hello iş gereksinimini gerekli en az izinleri verin. Bir kullanıcı birden fazla rollerinin bir üyesi olduğunda, bunların tümünü hello izinleriyle toplama.

## <a name="permissions"></a>İzinler
SQL Veritabanında ayrı ayrı verilebilen veya reddedilebilen 100'den fazla izin vardır. Bu izinlerin çoğu iç içe geçmiş haldedir. Örneğin, hello `UPDATE` bir şema izni içeren hello `UPDATE` bu şeması içindeki her bir tablo izni. Çoğu izin sistemi olduğu gibi bir grant izni hello Reddi geçersiz kılar. İç içe geçmiş hello yapısı ve izinleri hello sayısı nedeniyle olay incelemesi toodesign uygun izni sistem tooproperly korumak veritabanınızı dikkatli alabilir. İzinler hello listesi ile başlar [izinleri (veritabanı altyapısı)](https://msdn.microsoft.com/library/ms191291.aspx) ve hello gözden [posteri boyutu grafik](http://go.microsoft.com/fwlink/?LinkId=229142) hello izinleri.


### <a name="considerations-and-restrictions"></a>Dikkat edilmesi gerekenler ve kısıtlamalar
Oturumlar ve kullanıcılar SQL veritabanında yönetirken hello aşağıdakileri göz önünde bulundurun:

* Bağlı toohello olmalıdır **ana** veritabanı hello yürütülürken `CREATE/ALTER/DROP DATABASE` deyimleri.   
* veritabanı kullanıcı karşılık gelen toohello hello **sunucu yöneticisinin** oturum açma değiştirilmiş veya bırakılmış. 
* ABD İngilizcesi hello hello varsayılan dili olan **sunucu yöneticisinin** oturum açma.
* Yalnızca Yöneticiler hello (**sunucu yöneticisinin** oturum açma veya Azure AD Yöneticisi) ve hello hello üyeleri **dbmanager** hello veritabanı rolünün **ana** veritabanına sahip izni tooexecute hello `CREATE DATABASE` ve `DROP DATABASE` deyimleri.
* Merhaba yürütürken bağlı toohello ana veritabanı olmalıdır `CREATE/ALTER/DROP LOGIN` deyimleri. Ancak oturum açma bilgilerinin kullanılması önerilmez. Bunun yerine bağımsız veritabanı kullanıcılarını kullanmanız önerilir.
* tooconnect tooa kullanıcı veritabanı hello bağlantı dizesinde hello veritabanının hello adı sağlamanız gerekir.
* Yalnızca sunucu düzeyinde asıl oturum açma ve hello üyeleri hello hello **loginmanager** hello veritabanı rolünün **ana** veritabanına sahip izni tooexecute hello `CREATE LOGIN`, `ALTER LOGIN`, ve `DROP LOGIN` deyimleri.
* Merhaba yürütülürken `CREATE/ALTER/DROP LOGIN` ve `CREATE/ALTER/DROP DATABASE` deyimleri ADO.NET uygulamada Parametreli Komutlar izin verilmez. Daha fazla bilgi için bkz. [Komutlar ve Parametreler](https://msdn.microsoft.com/library/ms254953.aspx).
* Merhaba yürütülürken `CREATE/ALTER/DROP DATABASE` ve `CREATE/ALTER/DROP LOGIN` deyimleri, her biri bu deyimleri olması gerekir yalnızca bir Transact-SQL toplu deyiminde hello. Aksi takdirde bir hata oluşur. Örneğin, aşağıdaki Transact-SQL hello veritabanının var olup olmadığını denetler hello. Varsa, bir `DROP DATABASE` deyimi tooremove hello veritabanı çağrılır. Çünkü hello `DROP DATABASE` deyimi hello toplu işlemdeki yegane deyim hello değil, hello aşağıdaki yürütme Transact-SQL deyimi bir hatayla sonuçlanır.

  ```
  IF EXISTS (SELECT [name]
           FROM   [sys].[databases]
           WHERE  [name] = N'database_name')
  DROP DATABASE [database_name];
  GO
  ```

* Merhaba yürütülürken `CREATE USER` hello deyimiyle `FOR/FROM LOGIN` seçeneği, yalnızca bir Transact-SQL toplu deyiminde hello olmalıdır.
* Merhaba yürütülürken `ALTER USER` hello deyimiyle `WITH LOGIN` seçeneği, yalnızca bir Transact-SQL toplu deyiminde hello olmalıdır.
* çok`CREATE/ALTER/DROP` hello bir kullanıcının gerektiren `ALTER ANY USER` hello veritabanı izni.
* Bir veritabanı rolü Hello sahibi tooadd veya gruptan başka bir veritabanı kullanıcı tooor veritabanı rolüne Kaldır çalıştığında, aşağıdaki hata hello oluşabilir: **kullanıcı veya rol 'Name' Bu veritabanında yok.** Merhaba kullanıcı görünür toohello sahip olmadığından bu hata oluşur. tooresolve Bu sorun, grant hello rol sahibi hello `VIEW DEFINITION` hello kullanıcı izni. 


## <a name="next-steps"></a>Sonraki adımlar

- güvenlik duvarı kuralları hakkında daha fazla toolearn bkz [Azure SQL veritabanı Güvenlik Duvarı](sql-database-firewall-configure.md).
- Tüm hello SQL veritabanı güvenlik özelliklerine genel bakış için bkz: [SQL güvenliğine genel bakış](sql-database-security-overview.md).
- Bir öğretici için bkz: [Azure SQL veritabanınıza güvenli](sql-database-security-tutorial.md).
- Görünümler ve saklı yordamlar hakkında bilgi için bkz. [Görünüm ve saklı yordam oluşturma](https://msdn.microsoft.com/library/ms365311.aspx)
- Access tooa veritabanı nesnesi verme hakkında daha fazla bilgi için bkz: [erişim verme tooa veritabanı nesnesi](https://msdn.microsoft.com/library/ms365327.aspx)
