---
title: "Olağanüstü durum kurtarma için Azure SQL veritabanı güvenlik aaaConfigure | Microsoft Docs"
description: "Bu konuda, yapılandırma ve veritabanı geri yükleme ya da bir yük devretme tooa ikincil sunucuya hello olay veri merkezi kesintisinden veya diğer olağanüstü durum sonra güvenlik yönetmeye yönelik güvenlik konuları açıklanmaktadır."
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a>Yapılandırma ve coğrafi geri yükleme veya yük devretme için Azure SQL veritabanı güvenlik yönetme 

> [!NOTE]
> [Aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md) tüm hizmet katmanlarında tüm veritabanları için kullanıma sunulmuştur.
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a>Kimlik doğrulama gereksinimlerini olağanüstü durum kurtarma için genel bakış
Bu konuda hello kimlik doğrulama gereksinimleri tooconfigure ve denetim açıklanmaktadır [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md) hello adımlar gerekli tooset kullanıcı erişimi toohello ikincil veritabanını ve. Ayrıca açıklanır kullandıktan sonra erişim toohello kurtarılmış veritabanını nasıl etkinleştirmek [coğrafi geri yükleme](sql-database-recovery-using-backups.md#geo-restore). Kurtarma seçenekleri hakkında daha fazla bilgi için bkz: [iş Sürekliliğine genel bakış](sql-database-business-continuity.md).

## <a name="disaster-recovery-with-contained-users"></a>Kapsanan kullanıcılar ile olağanüstü durum kurtarma
Geleneksel kullanıcılar aksine hello ana veritabanındaki toologins eşlenen hangi olmalıdır, içerilen kullanıcı tamamen hello veritabanının tarafından yönetilir. Bu iki faydası vardır. Merhaba olağanüstü durum kurtarma senaryosunda hello kullanıcıları tooconnect toohello yeni birincil veritabanı veya coğrafi geri yükleme herhangi bir ek yapılandırma olmadan kullanarak hello veritabanı hello kullanıcıları yönetir çünkü kurtarılan hello veritabanı devam edebilir. Ayrıca vardır olası ölçeklenebilirlik ve performans avantajı oturum açma açısından bu yapılandırmasından. Daha fazla bilgi için bkz. [Bağımsız Veritabanı Kullanıcıları - Veritabanınızı Taşınabilir Hale Getirme](https://msdn.microsoft.com/library/ff929188.aspx). 

Merhaba ana dengelemeyi hello olağanüstü durum kurtarma işlemini ölçekte yönetme daha zor olmasıdır. Merhaba kimlik bilgilerini kullanarak koruma aynı oturum açma bulunan bu kullanım hello birden çok veritabanı varsa, birden çok veritabanı kullanıcılar kapsanan kullanıcılar hello yararları negate. Örneğin, tutarlı bir şekilde hello oturumu için başlangıç parolası değiştiriliyor yerine birden çok veritabanları kez hello ana veritabanında değişiklikler olduğunu hello parola döndürme İlkesi gerektirir. Bu kullanım hello birden çok veritabanı varsa, bu nedenle, aynı kullanıcı adı ve parola, kapsanan kullanıcılar kullanarak önerilmez. 

## <a name="how-tooconfigure-logins-and-users"></a>Nasıl tooconfigure oturumlar ve kullanıcılar
Oturumlar ve kullanıcılar kullanıyorsanız (kapsanan kullanıcılar yerine), ek adımlar tooinsure aynı oturumları mevcut bu hello hello ana veritabanında gerçekleştirmeniz gereken. Merhaba aşağıdaki bölümlerde hello adımları söz konusu ve ek ilgili önemli noktalar verilmiştir.

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a>Kullanıcı erişim tooa ikincil veya kurtarılan veritabanı kurun
Bir salt okunur ikincil veritabanını ve coğrafi geri yükleme, kullanma kurtarılan tooensure doğru erişim toohello yeni birincil veritabanı veya Merhaba veritabanını ana hello gibi hello ikincil veritabanı toobe kullanılabilir hello hedef sunucusunun veritabanı hello olması gerekir Merhaba kurtarma önce yerinde uygun güvenlik yapılandırması.

Merhaba özel izinler her adımı için bu konunun ilerleyen bölümlerinde açıklanmıştır.

Kullanıcı erişim tooa hazırlama coğrafi çoğaltma ikincil coğrafi çoğaltma yapılandırma bir parçası olarak gerçekleştirilmelidir. Kullanıcı erişimi toohello coğrafi geri veritabanları hazırlama hello özgün sunucu olduğunda çevrimiçi herhangi bir zamanda gerçekleştirilmelidir (örneğin bir parçası olarak hello DR ayrıntıya).

> [!NOTE]
> Başarısız olursa düzgün yapılandırılmış oturumları yok üzerinden veya coğrafi geri yükleme tooa sunucu erişim tooit sınırlı toohello server yönetici hesabı olacaktır.
> 
> 

Merhaba hedef sunucuda oturum açmalar ayarlama aşağıda açıklanan üç adımdan oluşur:

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a>1. Oturumları erişim toohello birincil veritabanı ile belirler:
Merhaba ilk hello işleminin hangi oturumların hello hedef sunucuda çoğaltılmalıdır toodetermine adımdır. Bu, SELECT deyimi, hello mantıksal asıl veritabanı hello kaynak sunucuda birinde ve birincil veritabanı hello kendisini birinde bir çifti ile gerçekleştirilir.

Yalnızca sunucu yöneticisi veya hello üyesi hello **LoginManager** sunucu rolü ile SELECT deyiminden hello hello oturumları hello kaynak sunucuda belirleyebilir. 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

Yalnızca hello db_owner veritabanı rolü, hello dbo kullanıcısı veya Sunucu Yöneticisi, bir üyesi hello veritabanı kullanıcısı Sorumlular hello birincil veritabanındaki tüm belirleyebilirsiniz.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a>2. 1. adımda tanımlanan hello oturum açma Hello SID bulur:
Merhaba sorgularından hello önceki bölümde ve eşleşen hello SID Hello çıktısını karşılaştırarak hello sunucu oturum açma toodatabase kullanıcı eşleyebilirsiniz. Bir veritabanı kullanıcısı eşleşen SID'e sahip oturumların kullanıcı erişimi toothat veritabanı asıl veritabanı kullanıcı sahip. 

Merhaba aşağıdaki sorguda kullanılan toosee olabilir tüm hello kullanıcı ilkeleri ve bir veritabanında SID'leri. Merhaba, db_owner veritabanı rol veya Sunucu Yöneticisi yalnızca bir üyesi bu sorgu çalıştırabilirsiniz.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> Merhaba **INFORMATION_SCHEMA** ve **sys** kullanıcınız *NULL* SID'ler ve hello **Konuk** SID **0x00**. Merhaba **dbo** SID ile başlayabilir *0x01060000000001648000000000048454*, hello veritabanı oluşturucusu hello Sunucu Yöneticisi yerine bir üyesi ise **DbManager**.
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a>3. Merhaba oturumları hello hedef sunucuda oluşturun:
Merhaba son adımı toogo toohello hedef sunucu veya sunucuları ve hello oturumları hello ile oluşturur uygun SID. Merhaba temel söz dizimi aşağıdaki gibidir.

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> Toogrant kullanıcı erişimi toohello ikincil ancak değil toohello birincil istiyorsanız, söz dizimi aşağıdaki hello kullanarak hello kullanıcı oturum açma hello birincil sunucuda değiştirerek yapabilirsiniz.
> 
> ALTER OTURUM AÇMA <login name> DEVRE DIŞI BIRAK
> 
> Her zaman gerekirse etkinleştirebilirsiniz şekilde devre dışı bırak hello parola değiştirmez.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Veritabanı erişimi ve oturumları yönetme ile ilgili daha fazla bilgi için bkz: [SQL veritabanı güvenlik: veritabanı erişimi ve oturum açma güvenlik yönetmek](sql-database-manage-logins.md).
* Kapsanan veritabanı kullanıcıları hakkında daha fazla bilgi için bkz: [bulunan veritabanı kullanıcıları - yapmadan bilgisayarınızı veritabanı taşınabilir](https://msdn.microsoft.com/library/ff929188.aspx).
* Aktif coğrafi çoğaltma yapılandırma ve kullanma hakkında daha fazla bilgi için bkz: [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md)
* Coğrafi geri yükleme hakkında daha fazla bilgi için bkz: [coğrafi geri yükleme](sql-database-recovery-using-backups.md#geo-restore)

