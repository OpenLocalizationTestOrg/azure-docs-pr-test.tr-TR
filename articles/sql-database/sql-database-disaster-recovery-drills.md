---
title: "SQL veritabanı olağanüstü durum kurtarma ayrıntılarını | Microsoft Docs"
description: "Kılavuzu ve Azure SQL veritabanı kullanarak, görev kritik tutmaya yardımcı olmak için olağanüstü durum kurtarma ayrıntılarını gerçekleştirmek için en iyi yöntemleri öğrenin iş uygulamaları dayanıklı hataları ve kesintileri."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: 1b1d65a41a794a566287dcffe3581ac58e2a965f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="18da4-103">Olağanüstü durum kurtarma ayrıntıya gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="18da4-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="18da4-104">Kurtarma iş akışı için uygulama hazırlık doğrulanması düzenli aralıklarla gerçekleştirilen önerilir.</span><span class="sxs-lookup"><span data-stu-id="18da4-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="18da4-105">Uygulama davranışına ve etkileri doğrulama veri kaybına ve/veya kesintisi Bu yük devretme içerir iyi bir mühendislik uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="18da4-105">Verifying the application behavior and implications of data loss and/or the disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="18da4-106">Ayrıca, çoğu endüstri standartlarına göre gerekli iş sürekliliği sertifika kapsamında değildir.</span><span class="sxs-lookup"><span data-stu-id="18da4-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="18da4-107">Bir olağanüstü durum kurtarma ayrıntıya gerçekleştirme oluşur:</span><span class="sxs-lookup"><span data-stu-id="18da4-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="18da4-108">Benzetirme veri katmanı kesinti</span><span class="sxs-lookup"><span data-stu-id="18da4-108">Simulating data tier outage</span></span>
* <span data-ttu-id="18da4-109">Kurtarma</span><span class="sxs-lookup"><span data-stu-id="18da4-109">Recovering</span></span>
* <span data-ttu-id="18da4-110">Uygulama bütünlüğü post kurtarma doğrula</span><span class="sxs-lookup"><span data-stu-id="18da4-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="18da4-111">Nasıl bağlı olarak, [uygulamanız iş sürekliliği için tasarlanmış](sql-database-business-continuity.md), ayrıntıya yürütmek için iş akışı değişebilir.</span><span class="sxs-lookup"><span data-stu-id="18da4-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), the workflow to execute the drill can vary.</span></span> <span data-ttu-id="18da4-112">Aşağıda Azure SQL veritabanı bağlamında bir olağanüstü durum kurtarma ayrıntıya gerçekleştirme en iyi uygulamaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="18da4-112">Below we describe the best practices conducting a disaster recovery drill in the context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="18da4-113">Coğrafi Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="18da4-113">Geo-restore</span></span>
<span data-ttu-id="18da4-114">Bir olağanüstü durum kurtarma ayrıntıya yürütülürken olası veri kaybını önlemek için üretim ortamında bir kopyasını oluşturarak ve uygulamanın yük devretme iş akışı doğrulamak için kullanılarak bir test ortamı kullanarak ayrıntıya gerçekleştirme öneririz.</span><span class="sxs-lookup"><span data-stu-id="18da4-114">To prevent the potential data loss when conducting a disaster recovery drill, we recommend performing the drill using a test environment by creating a copy of the production environment and using it to verify the application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="18da4-115">Kesinti benzetimi</span><span class="sxs-lookup"><span data-stu-id="18da4-115">Outage simulation</span></span>
<span data-ttu-id="18da4-116">Kesinti benzetimini yapmak için silebilir veya kaynak veritabanını yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="18da4-116">To simulate the outage, you can delete or rename the source database.</span></span> <span data-ttu-id="18da4-117">Bu uygulama bağlantısı hataları neden olur.</span><span class="sxs-lookup"><span data-stu-id="18da4-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="18da4-118">Kurtarma</span><span class="sxs-lookup"><span data-stu-id="18da4-118">Recovery</span></span>
* <span data-ttu-id="18da4-119">Açıklandığı gibi farklı bir sunucu veritabanının coğrafi geri yükleme gerçekleştirmek [burada](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="18da4-119">Perform the geo-restore of the database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="18da4-120">Kurtarılan veritabanına bağlanmak ve izlenmesi uygulama yapılandırmasını değiştirme [bir veritabanını kurtarma işleminden sonra yapılandırma](sql-database-disaster-recovery.md) kurtarma işlemini tamamlamak için kılavuz.</span><span class="sxs-lookup"><span data-stu-id="18da4-120">Change the application configuration to connect to the recovered database and follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="18da4-121">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="18da4-121">Validation</span></span>
* <span data-ttu-id="18da4-122">Ayrıntıya (bağlantı dizeleri, oturum açma bilgileri, temel işlevselliğini test etme veya diğer standart uygulama signoffs yordamları doğrulamaları parçası dahil) uygulama bütünlüğü post kurtarma doğrulayarak tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="18da4-122">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="18da4-123">Coğrafi çoğaltma</span><span class="sxs-lookup"><span data-stu-id="18da4-123">Geo-replication</span></span>
<span data-ttu-id="18da4-124">Coğrafi çoğaltma kullanılarak korunan bir veritabanı için planlanan yük devretme ikincil veritabanına ayrıntıya alıştırma içerir.</span><span class="sxs-lookup"><span data-stu-id="18da4-124">For a database that is protected using geo-replication the drill exercise involves planned failover to the secondary database.</span></span> <span data-ttu-id="18da4-125">Planlanmış yük devretme rolleri anahtarlı zaman birincil ve ikincil veritabanlarıyla eşitlenmiş kalmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="18da4-125">The planned failover ensures that the primary and the secondary databases remain in sync when the roles are switched.</span></span> <span data-ttu-id="18da4-126">Üretim ortamında ayrıntıya gerçekleştirilebilir şekilde planlanmamış yük devretme farklı olarak bu işlem veri kaybına oluşmaz.</span><span class="sxs-lookup"><span data-stu-id="18da4-126">Unlike the unplanned failover, this operation does not result in data loss, so the drill can be performed in the production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="18da4-127">Kesinti benzetimi</span><span class="sxs-lookup"><span data-stu-id="18da4-127">Outage simulation</span></span>
<span data-ttu-id="18da4-128">Kesinti benzetimini yapmak için web uygulaması ya da sanal makinenin veritabanına bağlı devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18da4-128">To simulate the outage, you can disable the web application or virtual machine connected to the database.</span></span> <span data-ttu-id="18da4-129">Bu web istemcileri için bağlantı hataları sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="18da4-129">This results in the connectivity failures for the web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="18da4-130">Kurtarma</span><span class="sxs-lookup"><span data-stu-id="18da4-130">Recovery</span></span>
* <span data-ttu-id="18da4-131">Uygulama yapılandırması DR bölgede hangi tamamen erişilebilir yeni birincil hale eski ikincil işaret ettiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="18da4-131">Make sure the application configuration in the DR region points to the former secondary which becomes the fully accessible new primary.</span></span>
* <span data-ttu-id="18da4-132">Gerçekleştirmek [planlanan yük devretme](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) ikincil veritabanını yeni bir birincil yapmak için</span><span class="sxs-lookup"><span data-stu-id="18da4-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) to make the secondary database a new primary</span></span>
* <span data-ttu-id="18da4-133">İzleyin [bir veritabanını kurtarma işleminden sonra yapılandırma](sql-database-disaster-recovery.md) kurtarma işlemini tamamlamak için kılavuz.</span><span class="sxs-lookup"><span data-stu-id="18da4-133">Follow the [Configure a database after recovery](sql-database-disaster-recovery.md) guide to complete the recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="18da4-134">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="18da4-134">Validation</span></span>
* <span data-ttu-id="18da4-135">Ayrıntıya (bağlantı dizeleri, oturum açma bilgileri, temel işlevselliğini test etme veya diğer standart uygulama signoffs yordamları doğrulamaları parçası dahil) uygulama bütünlüğü post kurtarma doğrulayarak tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="18da4-135">Complete the drill by verifying the application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18da4-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="18da4-136">Next steps</span></span>
* <span data-ttu-id="18da4-137">İş sürekliliği senaryoları hakkında bilgi edinmek için [sürekliliği senaryoları](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="18da4-137">To learn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="18da4-138">Veritabanı Yedeklemeleri otomatik Azure SQL hakkında bilgi edinmek için bkz: [SQL veritabanı otomatik yedeklemeler](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="18da4-138">To learn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="18da4-139">Kurtarma için otomatik yedeklemeler kullanma hakkında bilgi edinmek için bkz: [bir veritabanı hizmeti tarafından başlatılan yedeklerden geri yükleme](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="18da4-139">To learn about using automated backups for recovery, see [restore a database from the service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="18da4-140">Daha hızlı kurtarma seçenekleri hakkında bilgi edinmek için [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="18da4-140">To learn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
