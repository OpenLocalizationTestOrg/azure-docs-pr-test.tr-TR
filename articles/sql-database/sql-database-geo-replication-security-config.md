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
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="83c45-103">Yapılandırma ve coğrafi geri yükleme veya yük devretme için Azure SQL veritabanı güvenlik yönetme</span><span class="sxs-lookup"><span data-stu-id="83c45-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="83c45-104">[Aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md) tüm hizmet katmanlarında tüm veritabanları için kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="83c45-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="83c45-105">Kimlik doğrulama gereksinimlerini olağanüstü durum kurtarma için genel bakış</span><span class="sxs-lookup"><span data-stu-id="83c45-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="83c45-106">Bu konuda hello kimlik doğrulama gereksinimleri tooconfigure ve denetim açıklanmaktadır [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md) hello adımlar gerekli tooset kullanıcı erişimi toohello ikincil veritabanını ve.</span><span class="sxs-lookup"><span data-stu-id="83c45-106">This topic describes hello authentication requirements tooconfigure and control [active geo-replication](sql-database-geo-replication-overview.md) and hello steps required tooset up user access toohello secondary database.</span></span> <span data-ttu-id="83c45-107">Ayrıca açıklanır kullandıktan sonra erişim toohello kurtarılmış veritabanını nasıl etkinleştirmek [coğrafi geri yükleme](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="83c45-107">It also describes how enable access toohello recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="83c45-108">Kurtarma seçenekleri hakkında daha fazla bilgi için bkz: [iş Sürekliliğine genel bakış](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="83c45-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="83c45-109">Kapsanan kullanıcılar ile olağanüstü durum kurtarma</span><span class="sxs-lookup"><span data-stu-id="83c45-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="83c45-110">Geleneksel kullanıcılar aksine hello ana veritabanındaki toologins eşlenen hangi olmalıdır, içerilen kullanıcı tamamen hello veritabanının tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="83c45-110">Unlike traditional users, which must be mapped toologins in hello master database, a contained user is managed completely by hello database itself.</span></span> <span data-ttu-id="83c45-111">Bu iki faydası vardır.</span><span class="sxs-lookup"><span data-stu-id="83c45-111">This has two benefits.</span></span> <span data-ttu-id="83c45-112">Merhaba olağanüstü durum kurtarma senaryosunda hello kullanıcıları tooconnect toohello yeni birincil veritabanı veya coğrafi geri yükleme herhangi bir ek yapılandırma olmadan kullanarak hello veritabanı hello kullanıcıları yönetir çünkü kurtarılan hello veritabanı devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="83c45-112">In hello disaster recovery scenario, hello users can continue tooconnect toohello new primary database or hello database recovered using geo-restore without any additional configuration, because hello database manages hello users.</span></span> <span data-ttu-id="83c45-113">Ayrıca vardır olası ölçeklenebilirlik ve performans avantajı oturum açma açısından bu yapılandırmasından.</span><span class="sxs-lookup"><span data-stu-id="83c45-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="83c45-114">Daha fazla bilgi için bkz. [Bağımsız Veritabanı Kullanıcıları - Veritabanınızı Taşınabilir Hale Getirme](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="83c45-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="83c45-115">Merhaba ana dengelemeyi hello olağanüstü durum kurtarma işlemini ölçekte yönetme daha zor olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="83c45-115">hello main trade-off is that managing hello disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="83c45-116">Merhaba kimlik bilgilerini kullanarak koruma aynı oturum açma bulunan bu kullanım hello birden çok veritabanı varsa, birden çok veritabanı kullanıcılar kapsanan kullanıcılar hello yararları negate.</span><span class="sxs-lookup"><span data-stu-id="83c45-116">When you have multiple databases that use hello same login, maintaining hello credentials using contained users in multiple databases may negate hello benefits of contained users.</span></span> <span data-ttu-id="83c45-117">Örneğin, tutarlı bir şekilde hello oturumu için başlangıç parolası değiştiriliyor yerine birden çok veritabanları kez hello ana veritabanında değişiklikler olduğunu hello parola döndürme İlkesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="83c45-117">For example, hello password rotation policy requires that changes be made consistently in multiple databases rather than changing hello password for hello login once in hello master database.</span></span> <span data-ttu-id="83c45-118">Bu kullanım hello birden çok veritabanı varsa, bu nedenle, aynı kullanıcı adı ve parola, kapsanan kullanıcılar kullanarak önerilmez.</span><span class="sxs-lookup"><span data-stu-id="83c45-118">For this reason, if you have multiple databases that use hello same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-tooconfigure-logins-and-users"></a><span data-ttu-id="83c45-119">Nasıl tooconfigure oturumlar ve kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="83c45-119">How tooconfigure logins and users</span></span>
<span data-ttu-id="83c45-120">Oturumlar ve kullanıcılar kullanıyorsanız (kapsanan kullanıcılar yerine), ek adımlar tooinsure aynı oturumları mevcut bu hello hello ana veritabanında gerçekleştirmeniz gereken.</span><span class="sxs-lookup"><span data-stu-id="83c45-120">If you are using logins and users (rather than contained users), you must take extra steps tooinsure that hello same logins exist in hello master database.</span></span> <span data-ttu-id="83c45-121">Merhaba aşağıdaki bölümlerde hello adımları söz konusu ve ek ilgili önemli noktalar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="83c45-121">hello following sections outline hello steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a><span data-ttu-id="83c45-122">Kullanıcı erişim tooa ikincil veya kurtarılan veritabanı kurun</span><span class="sxs-lookup"><span data-stu-id="83c45-122">Set up user access tooa secondary or recovered database</span></span>
<span data-ttu-id="83c45-123">Bir salt okunur ikincil veritabanını ve coğrafi geri yükleme, kullanma kurtarılan tooensure doğru erişim toohello yeni birincil veritabanı veya Merhaba veritabanını ana hello gibi hello ikincil veritabanı toobe kullanılabilir hello hedef sunucusunun veritabanı hello olması gerekir Merhaba kurtarma önce yerinde uygun güvenlik yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="83c45-123">In order for hello secondary database toobe usable as a read-only secondary database, and tooensure proper access toohello new primary database or hello database recovered using geo-restore, hello master database of hello target server must have hello appropriate security configuration in place before hello recovery.</span></span>

<span data-ttu-id="83c45-124">Merhaba özel izinler her adımı için bu konunun ilerleyen bölümlerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="83c45-124">hello specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="83c45-125">Kullanıcı erişim tooa hazırlama coğrafi çoğaltma ikincil coğrafi çoğaltma yapılandırma bir parçası olarak gerçekleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="83c45-125">Preparing user access tooa geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="83c45-126">Kullanıcı erişimi toohello coğrafi geri veritabanları hazırlama hello özgün sunucu olduğunda çevrimiçi herhangi bir zamanda gerçekleştirilmelidir (örneğin bir parçası olarak hello DR ayrıntıya).</span><span class="sxs-lookup"><span data-stu-id="83c45-126">Preparing user access toohello geo-restored databases should be performed at any time when hello original server is online (e.g. as part of hello DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="83c45-127">Başarısız olursa düzgün yapılandırılmış oturumları yok üzerinden veya coğrafi geri yükleme tooa sunucu erişim tooit sınırlı toohello server yönetici hesabı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="83c45-127">If you fail over or geo-restore tooa server that does not have properly configured logins, access tooit will be limited toohello server admin account.</span></span>
> 
> 

<span data-ttu-id="83c45-128">Merhaba hedef sunucuda oturum açmalar ayarlama aşağıda açıklanan üç adımdan oluşur:</span><span class="sxs-lookup"><span data-stu-id="83c45-128">Setting up logins on hello target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a><span data-ttu-id="83c45-129">1. Oturumları erişim toohello birincil veritabanı ile belirler:</span><span class="sxs-lookup"><span data-stu-id="83c45-129">1. Determine logins with access toohello primary database:</span></span>
<span data-ttu-id="83c45-130">Merhaba ilk hello işleminin hangi oturumların hello hedef sunucuda çoğaltılmalıdır toodetermine adımdır.</span><span class="sxs-lookup"><span data-stu-id="83c45-130">hello first step of hello process is toodetermine which logins must be duplicated on hello target server.</span></span> <span data-ttu-id="83c45-131">Bu, SELECT deyimi, hello mantıksal asıl veritabanı hello kaynak sunucuda birinde ve birincil veritabanı hello kendisini birinde bir çifti ile gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="83c45-131">This is accomplished with a pair of SELECT statements, one in hello logical master database on hello source server and one in hello primary database itself.</span></span>

<span data-ttu-id="83c45-132">Yalnızca sunucu yöneticisi veya hello üyesi hello **LoginManager** sunucu rolü ile SELECT deyiminden hello hello oturumları hello kaynak sunucuda belirleyebilir.</span><span class="sxs-lookup"><span data-stu-id="83c45-132">Only hello server admin or a member of hello **LoginManager** server role can determine hello logins on hello source server with hello following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="83c45-133">Yalnızca hello db_owner veritabanı rolü, hello dbo kullanıcısı veya Sunucu Yöneticisi, bir üyesi hello veritabanı kullanıcısı Sorumlular hello birincil veritabanındaki tüm belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83c45-133">Only a member of hello db_owner database role, hello dbo user, or server admin, can determine all of hello database user principals in hello primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a><span data-ttu-id="83c45-134">2. 1. adımda tanımlanan hello oturum açma Hello SID bulur:</span><span class="sxs-lookup"><span data-stu-id="83c45-134">2. Find hello SID for hello logins identified in step 1:</span></span>
<span data-ttu-id="83c45-135">Merhaba sorgularından hello önceki bölümde ve eşleşen hello SID Hello çıktısını karşılaştırarak hello sunucu oturum açma toodatabase kullanıcı eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83c45-135">By comparing hello output of hello queries from hello previous section and matching hello SIDs, you can map hello server login toodatabase user.</span></span> <span data-ttu-id="83c45-136">Bir veritabanı kullanıcısı eşleşen SID'e sahip oturumların kullanıcı erişimi toothat veritabanı asıl veritabanı kullanıcı sahip.</span><span class="sxs-lookup"><span data-stu-id="83c45-136">Logins that have a database user with a matching SID have user access toothat database as that database user principal.</span></span> 

<span data-ttu-id="83c45-137">Merhaba aşağıdaki sorguda kullanılan toosee olabilir tüm hello kullanıcı ilkeleri ve bir veritabanında SID'leri.</span><span class="sxs-lookup"><span data-stu-id="83c45-137">hello following query can be used toosee all of hello user principals and their SIDs in a database.</span></span> <span data-ttu-id="83c45-138">Merhaba, db_owner veritabanı rol veya Sunucu Yöneticisi yalnızca bir üyesi bu sorgu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83c45-138">Only a member of hello db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="83c45-139">Merhaba **INFORMATION_SCHEMA** ve **sys** kullanıcınız *NULL* SID'ler ve hello **Konuk** SID **0x00**.</span><span class="sxs-lookup"><span data-stu-id="83c45-139">hello **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and hello **guest** SID is **0x00**.</span></span> <span data-ttu-id="83c45-140">Merhaba **dbo** SID ile başlayabilir *0x01060000000001648000000000048454*, hello veritabanı oluşturucusu hello Sunucu Yöneticisi yerine bir üyesi ise **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="83c45-140">hello **dbo** SID may start with *0x01060000000001648000000000048454*, if hello database creator was hello server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a><span data-ttu-id="83c45-141">3. Merhaba oturumları hello hedef sunucuda oluşturun:</span><span class="sxs-lookup"><span data-stu-id="83c45-141">3. Create hello logins on hello target server:</span></span>
<span data-ttu-id="83c45-142">Merhaba son adımı toogo toohello hedef sunucu veya sunucuları ve hello oturumları hello ile oluşturur uygun SID.</span><span class="sxs-lookup"><span data-stu-id="83c45-142">hello last step is toogo toohello target server, or servers, and generate hello logins with hello appropriate SIDs.</span></span> <span data-ttu-id="83c45-143">Merhaba temel söz dizimi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="83c45-143">hello basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="83c45-144">Toogrant kullanıcı erişimi toohello ikincil ancak değil toohello birincil istiyorsanız, söz dizimi aşağıdaki hello kullanarak hello kullanıcı oturum açma hello birincil sunucuda değiştirerek yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83c45-144">If you want toogrant user access toohello secondary, but not toohello primary, you can do that by altering hello user login on hello primary server by using hello following syntax.</span></span>
> 
> <span data-ttu-id="83c45-145">ALTER OTURUM AÇMA <login name> DEVRE DIŞI BIRAK</span><span class="sxs-lookup"><span data-stu-id="83c45-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="83c45-146">Her zaman gerekirse etkinleştirebilirsiniz şekilde devre dışı bırak hello parola değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="83c45-146">DISABLE doesn’t change hello password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="83c45-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="83c45-147">Next steps</span></span>
* <span data-ttu-id="83c45-148">Veritabanı erişimi ve oturumları yönetme ile ilgili daha fazla bilgi için bkz: [SQL veritabanı güvenlik: veritabanı erişimi ve oturum açma güvenlik yönetmek](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="83c45-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="83c45-149">Kapsanan veritabanı kullanıcıları hakkında daha fazla bilgi için bkz: [bulunan veritabanı kullanıcıları - yapmadan bilgisayarınızı veritabanı taşınabilir](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="83c45-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="83c45-150">Aktif coğrafi çoğaltma yapılandırma ve kullanma hakkında daha fazla bilgi için bkz: [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="83c45-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="83c45-151">Coğrafi geri yükleme hakkında daha fazla bilgi için bkz: [coğrafi geri yükleme](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="83c45-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

