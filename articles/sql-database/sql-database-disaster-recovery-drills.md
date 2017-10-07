---
title: "aaaSQL veritabanı olağanüstü durum kurtarma ayrıntılarını | Microsoft Docs"
description: "Yönerge ve Azure SQL veritabanı tooperform olağanüstü durum kurtarma ayrıntısına toohelp Koru kullanmak için en iyi uygulamalar, görev kritik iş uygulamaları dayanıklı toofailures ve kesintileri öğrenin."
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
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a><span data-ttu-id="31c1d-103">Olağanüstü durum kurtarma ayrıntıya gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="31c1d-103">Performing Disaster Recovery Drill</span></span>
<span data-ttu-id="31c1d-104">Kurtarma iş akışı için uygulama hazırlık doğrulanması düzenli aralıklarla gerçekleştirilen önerilir.</span><span class="sxs-lookup"><span data-stu-id="31c1d-104">It is recommended that validation of application readiness for recovery workflow is performed periodically.</span></span> <span data-ttu-id="31c1d-105">Bu yük devretme doğrulanıyor hello uygulama davranışına ve veri kaybı ve/veya başlangıç engellemeyi etkilerini içerir iyi bir mühendislik uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="31c1d-105">Verifying hello application behavior and implications of data loss and/or hello disruption that failover involves is a good engineering practice.</span></span> <span data-ttu-id="31c1d-106">Ayrıca, çoğu endüstri standartlarına göre gerekli iş sürekliliği sertifika kapsamında değildir.</span><span class="sxs-lookup"><span data-stu-id="31c1d-106">It is also a requirement by most industry standards as part of business continuity certification.</span></span>

<span data-ttu-id="31c1d-107">Bir olağanüstü durum kurtarma ayrıntıya gerçekleştirme oluşur:</span><span class="sxs-lookup"><span data-stu-id="31c1d-107">Performing a disaster recovery drill consists of:</span></span>

* <span data-ttu-id="31c1d-108">Benzetirme veri katmanı kesinti</span><span class="sxs-lookup"><span data-stu-id="31c1d-108">Simulating data tier outage</span></span>
* <span data-ttu-id="31c1d-109">Kurtarma</span><span class="sxs-lookup"><span data-stu-id="31c1d-109">Recovering</span></span>
* <span data-ttu-id="31c1d-110">Uygulama bütünlüğü post kurtarma doğrula</span><span class="sxs-lookup"><span data-stu-id="31c1d-110">Validate application integrity post recovery</span></span>

<span data-ttu-id="31c1d-111">Nasıl bağlı olarak, [uygulamanız iş sürekliliği için tasarlanmış](sql-database-business-continuity.md), hello iş akışı tooexecute hello ayrıntıya farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="31c1d-111">Depending on how you [designed your application for business continuity](sql-database-business-continuity.md), hello workflow tooexecute hello drill can vary.</span></span> <span data-ttu-id="31c1d-112">Aşağıda Azure SQL veritabanı hello bağlamında bir olağanüstü durum kurtarma ayrıntıya gerçekleştirme hello en iyi uygulamaları açıklar.</span><span class="sxs-lookup"><span data-stu-id="31c1d-112">Below we describe hello best practices conducting a disaster recovery drill in hello context of Azure SQL Database.</span></span>

## <a name="geo-restore"></a><span data-ttu-id="31c1d-113">Coğrafi Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="31c1d-113">Geo-restore</span></span>
<span data-ttu-id="31c1d-114">bir olağanüstü durum kurtarma ayrıntıya yürütülürken tooprevent hello olası veri kaybı hello üretim ortamında bir kopyası oluşturuluyor ve kullanılarak test ortamı kullanarak hello ayrıntıya gerçekleştirme tooverify hello uygulamanın yük devretme iş akışı öneririz.</span><span class="sxs-lookup"><span data-stu-id="31c1d-114">tooprevent hello potential data loss when conducting a disaster recovery drill, we recommend performing hello drill using a test environment by creating a copy of hello production environment and using it tooverify hello application’s failover workflow.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="31c1d-115">Kesinti benzetimi</span><span class="sxs-lookup"><span data-stu-id="31c1d-115">Outage simulation</span></span>
<span data-ttu-id="31c1d-116">toosimulate kesinti Merhaba, silebilir veya hello kaynak veritabanını yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="31c1d-116">toosimulate hello outage, you can delete or rename hello source database.</span></span> <span data-ttu-id="31c1d-117">Bu uygulama bağlantısı hataları neden olur.</span><span class="sxs-lookup"><span data-stu-id="31c1d-117">This causes application connectivity failures.</span></span>

#### <a name="recovery"></a><span data-ttu-id="31c1d-118">Kurtarma</span><span class="sxs-lookup"><span data-stu-id="31c1d-118">Recovery</span></span>
* <span data-ttu-id="31c1d-119">Açıklandığı gibi Hello coğrafi geri yükleme hello veritabanı farklı bir sunucu gerçekleştirmeniz [burada](sql-database-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="31c1d-119">Perform hello geo-restore of hello database into a different server as described [here](sql-database-disaster-recovery.md).</span></span>
* <span data-ttu-id="31c1d-120">Değişiklik hello uygulama yapılandırma tooconnect toohello kurtarılan veritabanı ve izleme hello [bir veritabanını kurtarma işleminden sonra yapılandırma](sql-database-disaster-recovery.md) toocomplete hello Kurtarma Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="31c1d-120">Change hello application configuration tooconnect toohello recovered database and follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="31c1d-121">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="31c1d-121">Validation</span></span>
* <span data-ttu-id="31c1d-122">Merhaba uygulama bütünlüğü post Kurtarma (bağlantı dizeleri, oturum açma bilgileri, temel işlevselliğini test etme veya diğer standart uygulama signoffs yordamları doğrulamaları parçası dahil) doğrulama tam hello detaya gitme.</span><span class="sxs-lookup"><span data-stu-id="31c1d-122">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="geo-replication"></a><span data-ttu-id="31c1d-123">Coğrafi çoğaltma</span><span class="sxs-lookup"><span data-stu-id="31c1d-123">Geo-replication</span></span>
<span data-ttu-id="31c1d-124">Coğrafi çoğaltma hello ayrıntıya kullanarak korunan bir veritabanı için planlanan yük devretme toohello ikincil veritabanı alıştırma içerir.</span><span class="sxs-lookup"><span data-stu-id="31c1d-124">For a database that is protected using geo-replication hello drill exercise involves planned failover toohello secondary database.</span></span> <span data-ttu-id="31c1d-125">Merhaba planlı yük devretme hello rolleri anahtarlı zaman hello birincil ve ikincil veritabanlarıyla hello eşitlenmiş kalmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="31c1d-125">hello planned failover ensures that hello primary and hello secondary databases remain in sync when hello roles are switched.</span></span> <span data-ttu-id="31c1d-126">Aksine planlanmamış yük devretme Merhaba, hello ayrıntıya hello üretim ortamında gerçekleştirilebilir şekilde bu işlem veri kaybına yol değil.</span><span class="sxs-lookup"><span data-stu-id="31c1d-126">Unlike hello unplanned failover, this operation does not result in data loss, so hello drill can be performed in hello production environment.</span></span>

#### <a name="outage-simulation"></a><span data-ttu-id="31c1d-127">Kesinti benzetimi</span><span class="sxs-lookup"><span data-stu-id="31c1d-127">Outage simulation</span></span>
<span data-ttu-id="31c1d-128">toosimulate hello kesinti Merhaba web uygulaması veya sanal makineye bağlı toohello veritabanı devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31c1d-128">toosimulate hello outage, you can disable hello web application or virtual machine connected toohello database.</span></span> <span data-ttu-id="31c1d-129">Bu hello bağlantı hataları hello web istemcileri için sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="31c1d-129">This results in hello connectivity failures for hello web clients.</span></span>

#### <a name="recovery"></a><span data-ttu-id="31c1d-130">Kurtarma</span><span class="sxs-lookup"><span data-stu-id="31c1d-130">Recovery</span></span>
* <span data-ttu-id="31c1d-131">Hangi hello hale hello DR bölge noktaları toohello eski ikincil emin hello uygulama yapılandırması olun tamamen erişilebilir yeni birincil.</span><span class="sxs-lookup"><span data-stu-id="31c1d-131">Make sure hello application configuration in hello DR region points toohello former secondary which becomes hello fully accessible new primary.</span></span>
* <span data-ttu-id="31c1d-132">Gerçekleştirmek [planlanan yük devretme](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello ikincil yeni birincil veritabanı</span><span class="sxs-lookup"><span data-stu-id="31c1d-132">Perform [planned failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello secondary database a new primary</span></span>
* <span data-ttu-id="31c1d-133">Merhaba izleyin [bir veritabanını kurtarma işleminden sonra yapılandırma](sql-database-disaster-recovery.md) toocomplete hello Kurtarma Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="31c1d-133">Follow hello [Configure a database after recovery](sql-database-disaster-recovery.md) guide toocomplete hello recovery.</span></span>

#### <a name="validation"></a><span data-ttu-id="31c1d-134">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="31c1d-134">Validation</span></span>
* <span data-ttu-id="31c1d-135">Merhaba uygulama bütünlüğü post Kurtarma (bağlantı dizeleri, oturum açma bilgileri, temel işlevselliğini test etme veya diğer standart uygulama signoffs yordamları doğrulamaları parçası dahil) doğrulama tam hello detaya gitme.</span><span class="sxs-lookup"><span data-stu-id="31c1d-135">Complete hello drill by verifying hello application integrity post recovery (including connection strings, logins, basic functionality testing or other validations part of standard application signoffs procedures).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31c1d-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="31c1d-136">Next steps</span></span>
* <span data-ttu-id="31c1d-137">toolearn iş sürekliliği senaryoları hakkında bkz [sürekliliği senaryoları](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="31c1d-137">toolearn about business continuity scenarios, see [Continuity scenarios](sql-database-business-continuity.md)</span></span>
* <span data-ttu-id="31c1d-138">Azure SQL veritabanı otomatik yedeklemeler hakkında toolearn bakın [SQL veritabanı otomatik yedeklemeler](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="31c1d-138">toolearn about Azure SQL Database automated backups, see [SQL Database automated backups](sql-database-automated-backups.md)</span></span>
* <span data-ttu-id="31c1d-139">Kurtarma için otomatik yedeklemeler kullanma hakkında toolearn bakın [bir veritabanı hello hizmeti tarafından başlatılan yedeklerden geri yükleme](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="31c1d-139">toolearn about using automated backups for recovery, see [restore a database from hello service-initiated backups](sql-database-recovery-using-backups.md)</span></span>
* <span data-ttu-id="31c1d-140">toolearn daha hızlı kurtarma seçenekleri hakkında bkz [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="31c1d-140">toolearn about faster recovery options, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>  
