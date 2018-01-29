---
title: "Azure SQL oturumları ve kullanıcıları | Microsoft Docs"
description: "Özellikle sunucu düzeyindeki asıl hesap aracılığıyla veritabanı erişimini ve oturum açma güvenliğini yönetme olmak üzere SQL Veritabanı güvenlik yönetimi hakkında bilgi edinin."
keywords: "sql veritabanı güvenliği,veritabanı güvenliği yönetimi,oturum açma güvenliği,veritabanı güvenliği,veritabanı erişimi"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 0a65a93f-d5dc-424b-a774-7ed62d996f8c
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Active
ms.date: 01/23/2017
ms.author: carlrab
ms.openlocfilehash: 4963e67317f22140c318e29bcd03bce4b9f57ab6
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/11/2018
---
# <a name="controlling-and-granting-database-access"></a>Denetleme ve veritabanına erişim izni verme

Güvenlik duvarı kuralları yapılandırdıktan sonra kişilerin yönetici hesapları biri olarak, veritabanı sahibi veya veritabanındaki bir veritabanı kullanıcısı olarak bir SQL veritabanına bağlanabilir.  

>  [!NOTE]  
>  Bu konu başlığı, Azure SQL sunucusunun yanı sıra Azure SQL sunucusu üzerinde oluşturulmuş olan SQL Veritabanı ve SQL Veri Ambarı veritabanları için de geçerlidir. Kolaylık açısından, hem SQL Veritabanı hem de SQL Veri Ambarı için SQL Veritabanı terimi kullanılmaktadır. 
>

> [!TIP]
> Bir öğretici için bkz: [Azure SQL veritabanınıza güvenli](sql-database-security-tutorial.md).
>


## <a name="unrestricted-administrative-accounts"></a>Kısıtlanmamış yönetici hesapları
Yönetici işlevlerine sahip iki yönetici hesabı (**Sunucu yöneticisi** ve **Active Directory yöneticisi**) vardır. SQL sunucunuzda bu yönetici hesaplarını tanımlamak için Azure portalını açın ve SQL sunucunuzun özelliklerine gidin.

![SQL Server Yöneticileri](./media/sql-database-manage-logins/sql-admins.png)

- **Sunucu yöneticisi**   
Bir Azure SQL sunucusu oluşturduğunuzda **Sunucu yöneticisi oturum açma bilgileri** belirlemeniz gerekir. SQL Server, bu hesabı ana veritabanında oturum açma bilgileri olarak oluşturur. Bu hesap SQL Server kimlik doğrulaması (kullanıcı adı ve parola) kullanarak bağlanır. Bu hesaplardan yalnızca biri mevcut olabilir.   
- **Azure Active Directory yöneticisi**   
Ayrıca, Azure Active Directory’deki bir adet kişi veya güvenlik grubu hesabı da yönetici olarak yapılandırılabilir. Azure AD yöneticisi yapılandırma adımı isteğe bağlıdır ancak bir SQL Veritabanına bağlanan Azure AD hesapları için kullanmak istiyorsanız bir Azure AD yöneticisi yapılandırmanız gerekir. Azure Active Directory erişimini yapılandırma hakkında daha fazla bilgi için bkz. [Azure Active Directory Kimlik Doğrulamasını Kullanarak SQL Veritabanı’na veya SQL Veri Ambarı’na Bağlanma](sql-database-aad-authentication.md) ve [SQL Veritabanı ve SQL Veri Ambarı ile Azure AD MFA kullanımı için SSMS desteği](sql-database-ssms-mfa-authentication.md).
 

**Sunucu yöneticisi** ve **Azure AD yöneticisi** hesapları şu özelliklere sahiptir:
- Sunucudaki SQL Veritabanlarına yalnızca bu hesaplar otomatik olarak bağlanabilir. (Diğer hesapların, bir kullanıcı veritabanına bağlanabilmek için veritabanının sahibi olmaları veya kullanıcı veritabanında kullanıcı hesabına sahip olmaları gerekir.)
- Bu hesaplar kullanıcı veritabanlarına `dbo` kullanıcısı olarak girer ve kullanıcı veritabanlarında tüm izinlere sahip olur. (Kullanıcı veritabanının sahibi de veritabanına `dbo` kullanıcısı olarak girer.) 
- Bu hesaplar, `master` veritabanına `dbo` kullanıcısı olarak girmez ve ana veritabanında sınırlı izinlere sahiptir. 
- Bu hesaplar, standart SQL Server `sysadmin` sabit sunucu rolünün üyesi değildir. Bu rol, SQL veritabanında kullanılamaz.  
- Bu hesaplar, veritabanlarını, oturum açma bilgilerini, ana veritabanındaki kullanıcıları ve sunucu düzeyinde güvenlik duvarı kurallarını oluşturabilir, değiştirebilir ve kaldırabilir.
- Bu hesaplar, `dbmanager` ve `loginmanager` rollerine üye ekleyebilir ve bu rollerdeki üyeleri kaldırabilir.
- Bu hesaplar, `sys.sql_logins` sistem tablosunu görüntüleyebilir.

### <a name="configuring-the-firewall"></a>Güvenlik duvarını yapılandırma
Sunucu düzeyinde güvenlik duvarı tek bir IP adresi veya aralığı için yapılandırıldığında **SQL sunucu yöneticisi** ve **Azure Active Directory yöneticisi**, ana veritabanına ve tüm kullanıcı veritabanlarına bağlanabilir. İlk sunucu düzeyi güvenlik duvarı [Azure portalı](sql-database-get-started-portal.md) üzerinden [PowerShell](sql-database-get-started-powershell.md) veya [REST API](https://msdn.microsoft.com/library/azure/dn505712.aspx) kullanılarak yapılandırılabilir. Bağlantı kurulduktan sonra [Transact-SQL](sql-database-configure-firewall-settings.md) kullanarak ek sunucu düzeyi güvenlik duvarı kuralları yapılandırılabilir.

### <a name="administrator-access-path"></a>Yönetici erişim yolu
Sunucu düzeyi güvenlik duvarı doğru şekilde yapılandırıldığında **SQL sunucu yöneticisi** ve **Azure Active Directory yöneticisi**, SQL Server Management Studio veya SQL Server Veri Araçları gibi istemci araçlarını kullanarak bağlantı kurabilir. Tüm özellikler ve yetenekler yalnızca en güncel araçlar tarafından sunulur. Aşağıdaki şemada iki yönetici hesabı için tipik yapılandırma gösterilmektedir.

![Yönetici erişim yolu](./media/sql-database-manage-logins/1sql-db-administrator-access.png)

Yöneticiler, sunucu düzeyi güvenlik duvarındaki açık bağlantı noktalarından birini kullanarak tüm SQL Veritabanlarına bağlanabilir.

### <a name="connecting-to-a-database-by-using-sql-server-management-studio"></a>SQL Server Management Studio kullanarak bir veritabanına bağlanma
Sunucu, veritabanı, sunucu düzeyi güvenlik duvarı kuralları oluşturma ve SQL Server Management Studio kullanarak bir veritabanını sorgulama adımları için bkz. [Azure portalını ve SQL Server Management Studio’yu kullanarak Azure SQL Veritabanı sunucuları, veritabanları ve güvenlik duvarı kurallarını oluşturmaya başlayın](sql-database-get-started-portal.md).

> [!IMPORTANT]
> Microsoft Azure ve SQL Veritabanı güncelleştirmeleriyle aynı sürümde olmak için her zaman en güncel Management Studio sürümünü kullanmanız önerilir. [SQL Server Management Studio’yu güncelleyin](https://msdn.microsoft.com/library/mt238290.aspx).


## <a name="additional-server-level-administrative-roles"></a>Ek sunucu düzeyinde yönetim rolleri
Daha önce anlatılan sunucu düzeyi yönetim rollerine ek olarak SQL Veritabanı, ana veritabanında iki adet kısıtlı yönetim rolü sunar. Bu rollere, veritabanı oluşturma veya oturum açma bilgilerini yönetme izinleri veren kullanıcı hesapları eklenebilir.

### <a name="database-creators"></a>Veritabanı oluşturucuları
Bu yönetici rollerinden biri, **dbmanager** rolüdür. Bu rolün üyeleri yeni veritabanları oluşturabilir. Bu rolü kullanmak için `master` veritabanında bir kullanıcı oluşturmanız ve bu kullanıcıyı **dbmanager** veritabanı rolüne eklemeniz gerekir. Bir veritabanı oluşturmak için kullanıcının, ana veritabanındaki SQL Server oturumunu temel alan bir kullanıcı ya da Azure Active Directory kullanıcısını temel alan bağımsız bir veritabanı kullanıcısı olması gerekir.

1. Bir yönetici hesabını kullanarak ana veritabanına bağlanın.
2. İsteğe bağlı adım: [CREATE LOGIN](https://msdn.microsoft.com/library/ms189751.aspx) deyimini kullanarak bir SQL Server kimlik doğrulaması oturum açma bilgisi oluşturun. Örnek deyim:
   
   ```
   CREATE LOGIN Mary WITH PASSWORD = '<strong_password>';
   ```
   
   > [!NOTE]
   > Oturum açma bilgileri veya bağımsız veritabanı kullanıcısı oluştururken güçlü bir parola kullanın. Daha fazla bilgi için bkz. [Güçlü Parolalar](https://msdn.microsoft.com/library/ms161962.aspx).
    
   Performansı artırmak için oturum açma bilgileri (sunucu düzeyi asıl hesaplar) veritabanı düzeyinde geçici olarak önbelleğe alınır. Kimlik doğrulaması önbelleğini yenilemek için bkz. [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx).

3. Ana veritabanında [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) deyimini kullanarak bir kullanıcı oluşturun. Kullanıcı Azure Active Directory kimlik doğrulaması bağımsız veritabanı kullanıcısı (ortamınızı Azure AD kimlik doğrulaması için yapılandırdıysanız) veya SQL Server kimlik doğrulaması bağımsız veritabanı kullanıcısı ya da SQL Server kimlik doğrulaması oturum açma bilgilerini kullanan SQL Server kimlik doğrulaması kullanıcısı (önceki adımda oluşturulan) olabilir. Örnek deyimler:
   
   ```
   CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
   CREATE USER Tran WITH PASSWORD = '<strong_password>';
   CREATE USER Mary FROM LOGIN Mary; 
   ```

4. [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx) deyimini kullanarak yeni kullanıcıyı **dbmanager** veritabanı rolüne ekleyin. Örnek deyimler:
   
   ```
   ALTER ROLE dbmanager ADD MEMBER Mary; 
   ALTER ROLE dbmanager ADD MEMBER [mike@contoso.com];
   ```
   
   > [!NOTE]
   > dbmanager, ana veritabanındaki bir veritabanı rolü olduğu için bu role yalnızca veritabanı kullanıcısı ekleyebilirsiniz. Veritabanı düzeyindeki role sunucu düzeyinde oturum açma bilgisi ekleyemezsiniz.
    
5. Gerekirse, yeni kullanıcının bağlantı kurabilmesi için bir güvenlik duvarı kuralı yapılandırın. (Yeni kullanıcı, mevcut bir güvenlik duvarı kuralı kapsamında olabilir.)

Kullanıcı artık, ana veritabanına bağlanabilir ve yeni veritabanları oluşturabilir. Veritabanını oluşturan hesap, veritabanının sahibi olur.

### <a name="login-managers"></a>Oturum açma yöneticileri
Diğer yönetim rolü ise oturum açma yöneticisi rolüdür. Bu rolün üyeleri ana veritabanında yeni oturum açma bilgileri oluşturabilir. İsterseniz, aynı adımları uygulayarak (oturum açma bilgileri oluşturmak, kullanıcı oluşturmak ve **loginmanager** rolüne kullanıcı eklemek) bir kullanıcının ana veritabanında yeni oturum açma bilgileri oluşturmasını sağlayabilirsiniz. Microsoft, oturum açma bilgisi tabanlı kullanıcılar yerine, veritabanı düzeyinde kimlik doğrulaması yapan bağımsız veritabanı kullanıcılarından yararlanılmasını önerir. Dolayısıyla, oturum açma bilgileri genellikle gerekli değildir. Daha fazla bilgi için bkz. [Bağımsız Veritabanı Kullanıcıları - Veritabanınızı Taşınabilir Hale Getirme](https://msdn.microsoft.com/library/ff929188.aspx).

## <a name="non-administrator-users"></a>Yönetici olmayan kullanıcılar
Çoğu durumda, yönetici olmayan kullanıcıların ana veritabanına erişmesi gerekmez. [CREATE USER (Transact-SQL)](https://msdn.microsoft.com/library/ms173463.aspx) deyimini kullanarak veritabanı düzeyinde bağımsız veritabanı kullanıcıları oluşturun. Kullanıcı Azure Active Directory kimlik doğrulaması bağımsız veritabanı kullanıcısı (ortamınızı Azure AD kimlik doğrulaması için yapılandırdıysanız) veya SQL Server kimlik doğrulaması bağımsız veritabanı kullanıcısı ya da SQL Server kimlik doğrulaması oturum açma bilgilerini kullanan SQL Server kimlik doğrulaması kullanıcısı (önceki adımda oluşturulan) olabilir. Daha fazla bilgi için bkz. [Bağımsız Veritabanı Kullanıcıları - Veritabanınızı Taşınabilir Hale Getirme](https://msdn.microsoft.com/library/ff929188.aspx). 

Kullanıcı oluşturmak için veritabanına bağlanın ve aşağıdaki örneklere benzer deyimleri çalıştırın:

```
CREATE USER Mary FROM LOGIN Mary; 
CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
```

Başlangıçta veritabanı yöneticilerinden yalnızca biri veya veritabanının sahibi kullanıcı oluşturabilir. Daha fazla kullanıcıya yeni kullanıcı oluşturma yetkisi vermek için şunun gibi bir deyim kullanarak `ALTER ANY USER` izni verin:

```
GRANT ALTER ANY USER TO Mary;
```

Daha fazla kullanıcıya veritabanı üzerinde tam denetim vermek için `ALTER ROLE` deyimini kullanarak **db_owner** sabit veritabanı rolünün üyesi yapın.

> [!NOTE]
> Oturum açma bilgisi tabanlı veritabanı kullanıcıları genellikle, birden fazla veritabanına erişmesi gereken SQL Server kimlik doğrulaması kullanıcılarının bulunduğu durumlarda oluşturulur. Oturum açma bilgilerini kullanan kullanıcılar, ilgili oturum açma bilgilerine ve bu oturum açma bilgisi için tutulan tek parolaya bağlıdır. Ayrı veritabanlarındaki bağımsız veritabanı kullanıcıları, ayrı varlıklardır ve her biri kendi parolasına sahiptir. Bu durum, tüm veritabanları için aynı parolayı kullanmayan bağımsız veritabanı kullanıcıları için kafa karıştırıcı olabilir.

### <a name="configuring-the-database-level-firewall"></a>Veritabanı düzeyinde güvenlik duvarını yapılandırma
En iyi uygulamalardan biri, yönetici olmayan kullanıcıların kullandıkları veritabanlarına yalnızca güvenlik duvarı aracılığıyla erişim sağlamasıdır. Bu kullanıcıların IP adreslerini sunucu düzeyinde güvenlik duvarından yetkilendirip tüm veritabanlarına erişim vermek yerine [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) deyimini kullanarak veritabanı düzeyinde güvenlik duvarını yapılandırabilirsiniz. Veritabanı düzeyinde güvenlik duvarı portal kullanılarak yapılandırılamaz.

### <a name="non-administrator-access-path"></a>Yönetici olmayan kullanıcılar için erişim yolu
Veritabanı düzeyinde güvenlik duvarı doğru şekilde yapılandırıldığında veritabanı kullanıcıları SQL Server Management Studio veya SQL Server Veri Araçları gibi istemci araçlarını kullanarak bağlantı kurabilir. Tüm özellikler ve yetenekler yalnızca en güncel araçlar tarafından sunulur. Aşağıdaki şema, yönetici olmayan kullanıcılar için tipik erişim yolunu göstermektedir.

![Yönetici olmayan kullanıcılar için erişim yolu](./media/sql-database-manage-logins/2sql-db-nonadmin-access.png)

## <a name="groups-and-roles"></a>Gruplar ve roller
Verimli erişim yönetimi için bireysel kullanıcılar yerine gruplara ve rollere atanan izinler kullanılır. 

- Azure Active Directory kimlik doğrulaması kullandığınızda Azure Active Directory kullanıcılarını bir Azure Active Directory grubuna ekleyin. Grup için bir bağımsız veritabanı kullanıcısı oluşturun. Bir veya daha fazla veritabanı kullanıcılarını bir [veritabanı rolüne](https://msdn.microsoft.com/library/ms189121) ekleyin ve [izinleri](https://msdn.microsoft.com/library/ms191291.aspx) veritabanı rolüne atayın.

- SQL Server kimlik doğrulamasını kullanırken veritabanında bağımsız veritabanı kullanıcılarını oluşturun. Bir veya daha fazla veritabanı kullanıcılarını bir [veritabanı rolüne](https://msdn.microsoft.com/library/ms189121) ekleyin ve [izinleri](https://msdn.microsoft.com/library/ms191291.aspx) veritabanı rolüne atayın.

Veritabanı rolleri **db_owner**, **db_ddladmin**, **db_datawriter**, **db_datareader**, **db_denydatawriter** ve **db_denydatareader** gibi yerleşik roller olabilir. Birkaç kullanıcıya tam izin vermek için genelde **db_owner** kullanılır. Diğer sabit veritabanı rolleri, geliştirme aşamasında basit bir veritabanını hızlı bir şekilde kullanıma almak için kullanışlıdır ancak çoğu üretim veritabanı için önerilmez. Örneğin **db_datareader** sabit veritabanı rolü, veritabanındaki tüm tablolara okuma izni verir ve bu durum genelde ihtiyaç duyulandan fazlasıdır. [CREATE ROLE](https://msdn.microsoft.com/library/ms187936.aspx) deyimini kullanarak kendi kullanıcı tanımlı veritabanı rollerinizi oluşturmak ve dikkatli bir şekilde her role ihtiyaç duyulan en alt düzeyde izinleri vermek çok daha iyidir. Birden fazla rolün üyesi olan kullanıcılar, tüm rollerin izinlerine sahip olur.

## <a name="permissions"></a>İzinler
SQL Veritabanında ayrı ayrı verilebilen veya reddedilebilen 100'den fazla izin vardır. Bu izinlerin çoğu iç içe geçmiş haldedir. Örneğin, bir şemada için verilen `UPDATE` izni, o şema içindeki tüm tablolar için `UPDATE` iznini de içerir. Çoğu izin sisteminde olduğu gibi bir iznin reddedilmesi, aynı iznin verilme durumunu geçersiz kılar. İç içe geçmiş yapısı ve izin sayısı nedeniyle, veritabanınızı doğru şekilde korumak için uygun bir izin sistemi tasarlamak uzun ve dikkatli bir çalışma gerektirebilir. [İzinler (Veritabanı Altyapısı)](https://msdn.microsoft.com/library/ms191291.aspx) ile başlayın ve izinlerin [poster boyutundaki tablosunu](http://go.microsoft.com/fwlink/?LinkId=229142) inceleyin.


### <a name="considerations-and-restrictions"></a>Dikkat edilmesi gerekenler ve kısıtlamalar
SQL Veritabanında oturum açma bilgilerini ve kullanıcıları yönetirken aşağıdaki noktalara dikkat edin:

* `CREATE/ALTER/DROP DATABASE` deyimlerini yürütürken **ana** veritabanına bağlanmış olmanız gerekir.   
* **Sunucu yöneticisi** oturum açma bilgilerine karşılık gelen veritabanı kullanıcısı değiştirilemez veya kaldırılamaz. 
* **Sunucu yöneticisi** oturum açma bilgilerinin varsayılan dili ABD-İngilizce olarak belirlenmiştir.
* Yalnızca yöneticiler (**Sunucu yöneticisi** oturum açma bilgileri veya Azure AD yöneticisi) ve **ana** veritabanındaki **dbmanager** veritabanı rolünün üyeleri `CREATE DATABASE` ve `DROP DATABASE` deyimlerini yürütme iznine sahiptir.
* `CREATE/ALTER/DROP LOGIN` deyimlerini yürütürken ana veritabanına bağlanmış olmanız gerekir. Ancak oturum açma bilgilerinin kullanılması önerilmez. Bunun yerine bağımsız veritabanı kullanıcılarını kullanmanız önerilir.
* Bir kullanıcı veritabanına bağlanmak için bağlantı dizesinde veritabanının adını belirtmeniz gerekir.
* Yalnızca sunucu düzeyi asıl oturum açma bilgisi ve **ana** veritabanındaki **loginmanager** veritabanı rolünün üyeleri `CREATE LOGIN`,`ALTER LOGIN` ve `DROP LOGIN` deyimlerini yürütme iznine sahiptir.
* Bir ADO.NET uygulamasında `CREATE/ALTER/DROP LOGIN` ve `CREATE/ALTER/DROP DATABASE` deyimlerini yürütürken parametreli komutların kullanılmasına izin verilmez. Daha fazla bilgi için bkz. [Komutlar ve Parametreler](https://msdn.microsoft.com/library/ms254953.aspx).
* `CREATE/ALTER/DROP DATABASE` ve `CREATE/ALTER/DROP LOGIN` deyimlerini yürütürken bu deyimlerin her birinin bir Transact-SQL toplu işindeki tek deyim olması gerekir. Aksi takdirde bir hata oluşur. Örneğin, aşağıdaki Transact-SQL veritabanının mevcut olup olmadığını kontrol eder. Mevcutsa, veritabanını kaldırmak için bir `DROP DATABASE` deyimi çağrılır. `DROP DATABASE` deyimi toplu işteki tek deyim olmadığından aşağıdaki Transact-SQL deyiminin yürütülmesi hatayla sonuçlanacaktır.

  ```
  IF EXISTS (SELECT [name]
           FROM   [sys].[databases]
           WHERE  [name] = N'database_name')
  DROP DATABASE [database_name];
  GO
  ```

* `CREATE USER` deyimini `FOR/FROM LOGIN` seçeneğiyle yürütürken bunun bir Transact-SQL toplu işindeki tek deyim olması gerekir.
* `ALTER USER` deyimini `WITH LOGIN` seçeneğiyle yürütürken bunun bir Transact-SQL toplu işindeki tek deyim olması gerekir.
* Bir kullanıcıda `CREATE/ALTER/DROP` işlemini gerçekleştirmek için veritabanında `ALTER ANY USER` izni gerekir.
* Bir veritabanı rolünün sahibi başka bir kullanıcıyı ilgili veritabanı rolüne eklemeye veya bu rolden kaldırmaya çalıştığında şu hata ortaya çıkabilir: **Kullanıcı veya rol "Ad" bu veritabanında mevcut değil.** Bu hatanın nedeni, kullanıcının rol sahibine görünür olmamasıdır. Bu sorunu çözmek için rol sahibine kullanıcı için `VIEW DEFINITION` iznini verin. 


## <a name="next-steps"></a>Sonraki adımlar

- Güvenlik duvarı kuralları hakkında daha fazla bilgi için bkz. [Azure SQL Veritabanı Güvenlik Duvarı](sql-database-firewall-configure.md).
- SQL Veritabanı güvenlik özelliklerinin tümüne genel bakış için bkz. [SQL Veritabanı güvenliğine genel bakış](sql-database-security-overview.md).
- Bir öğretici için bkz: [Azure SQL veritabanınıza güvenli](sql-database-security-tutorial.md).
- Görünümler ve saklı yordamlar hakkında bilgi için bkz. [Görünüm ve saklı yordam oluşturma](https://msdn.microsoft.com/library/ms365311.aspx)
- Bir veritabanı nesnesine erişim verme hakkında bilgi için bkz. [Bir veritabanı nesnesine erişim verme](https://msdn.microsoft.com/library/ms365327.aspx)
