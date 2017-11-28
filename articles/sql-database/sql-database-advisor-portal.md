---
title: "aaaApply performans önerileri - Azure SQL veritabanı | Microsoft Docs"
description: "Azure SQL Database veya toocorrect performansını en iyi duruma getirebilirsiniz hello Azure portal toofind performans önerileri kullanabilirsiniz, iş yükü tanımlanan bazı sorunun."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="826a2-103">Bul ve performans önerileri uygulayın</span><span class="sxs-lookup"><span data-stu-id="826a2-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="826a2-104">Azure SQL Database veya toocorrect performansını en iyi duruma getirebilirsiniz hello Azure portal toofind performans önerileri kullanabilirsiniz, iş yükü tanımlanan bazı sorunun.</span><span class="sxs-lookup"><span data-stu-id="826a2-104">You can use hello Azure portal toofind performance recommendations that can optimize performance of your Azure SQL Database or toocorrect some issue identified in your workload.</span></span> <span data-ttu-id="826a2-105">**Performans öneri** sayfası Azure portalında olası etkilerini dayalı toofind hello üst olarak öneriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="826a2-105">**Performance recommendation** page in Azure portal enables you toofind hello top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="826a2-106">Öneriler görüntüleme</span><span class="sxs-lookup"><span data-stu-id="826a2-106">Viewing recommendations</span></span>

<span data-ttu-id="826a2-107">tooview ve doğru hello performans önerileri uygulamak [rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md) Azure izinleri.</span><span class="sxs-lookup"><span data-stu-id="826a2-107">tooview and apply performance recommendations, you need hello correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="826a2-108">**Okuyucu**, **SQL DB Katılımcısı** izinlerdir gerekli tooview önerileri ve **sahibi**, **SQL DB Katılımcısı** izinleri gereklidir tooexecute herhangi bir eylem; oluşturma veya dizinleri bırakın ve dizin oluşturmayı iptal et.</span><span class="sxs-lookup"><span data-stu-id="826a2-108">**Reader**, **SQL DB Contributor** permissions are required tooview recommendations, and **Owner**, **SQL DB Contributor** permissions are required tooexecute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="826a2-109">Azure Portal'da aşağıdaki adımları toofind performans önerileri hello kullan:</span><span class="sxs-lookup"><span data-stu-id="826a2-109">Use hello following steps toofind performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="826a2-110">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="826a2-110">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="826a2-111">Çok Git**daha fazla hizmet** > **SQL veritabanları**, veritabanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="826a2-111">Go too**More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="826a2-112">Çok gidin**performans öneri** tooview kullanılabilir önerileri hello Seçilen veritabanı için.</span><span class="sxs-lookup"><span data-stu-id="826a2-112">Navigate too**Performance recommendation** tooview available recommendations for hello selected database.</span></span>

<span data-ttu-id="826a2-113">Performans shonw hello tablo benzer toohello biri üzerinde aşağıdaki şekilde hello gösterilen içinde önerileri:</span><span class="sxs-lookup"><span data-stu-id="826a2-113">Performance recommendations are shonw in hello table similar toohello one shown on hello following figure:</span></span>

![Öneriler](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="826a2-115">Öneriler, olası performans kategorileri aşağıdaki hello içine etkilerini göre sıralanır:</span><span class="sxs-lookup"><span data-stu-id="826a2-115">Recommendations are sorted by their potential impact on performance into hello following categories:</span></span>

| <span data-ttu-id="826a2-116">Etkisi</span><span class="sxs-lookup"><span data-stu-id="826a2-116">Impact</span></span> | <span data-ttu-id="826a2-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="826a2-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="826a2-118">Yüksek</span><span class="sxs-lookup"><span data-stu-id="826a2-118">High</span></span> |<span data-ttu-id="826a2-119">Yüksek etkisi önerileri hello en önemli performans etkisi sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="826a2-119">High impact recommendations should provide hello most significant performance impact.</span></span> |
| <span data-ttu-id="826a2-120">Orta</span><span class="sxs-lookup"><span data-stu-id="826a2-120">Medium</span></span> |<span data-ttu-id="826a2-121">Orta etkisi önerileri performansını artırmak, ancak önemli ölçüde değil.</span><span class="sxs-lookup"><span data-stu-id="826a2-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="826a2-122">Düşük</span><span class="sxs-lookup"><span data-stu-id="826a2-122">Low</span></span> |<span data-ttu-id="826a2-123">Düşük etkisi önerileri olmadan daha iyi performans sağlaması gerekir, ancak geliştirmeleri önemli ölçüde olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="826a2-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="826a2-124">Azure SQL veritabanı toomonitor etkinlikleri en az sipariş tooidentify bir günü için bazı öneriler gerekir.</span><span class="sxs-lookup"><span data-stu-id="826a2-124">Azure SQL Database needs toomonitor activities at least for a day in order tooidentify some recommendations.</span></span> <span data-ttu-id="826a2-125">Bu etkinlik için rastgele yetersiz WINS'e daha hello Azure SQL veritabanı daha kolay tutarlı sorgu desenlerine için en iyi duruma getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="826a2-125">hello Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="826a2-126">Öneriler corrently kullanılabilir değilse, hello **performans öneri** sayfası, nedenini açıklayan bir ileti sağlar.</span><span class="sxs-lookup"><span data-stu-id="826a2-126">If recommendations are not corrently available, hello **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="826a2-127">Merhaba geçmiş işlemleri hello durumunu da görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="826a2-127">You can also view hello status of hello historical operations.</span></span> <span data-ttu-id="826a2-128">Bir öneri veya durum toosee daha fazla ayrıntı seçin.</span><span class="sxs-lookup"><span data-stu-id="826a2-128">Select a recommendation or status toosee  more details.</span></span>

<span data-ttu-id="826a2-129">"Dizin oluşturma" öneri hello Azure portal'ın bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="826a2-129">Here is an example of "Create index" recommendation in hello Azure portal.</span></span>

![Dizin oluşturma](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="826a2-131">Önerileri uygulama</span><span class="sxs-lookup"><span data-stu-id="826a2-131">Applying recommendations</span></span>
<span data-ttu-id="826a2-132">Azure SQL veritabanına nasıl önerilerdir üzerinde tam denetim verir hello aşağıdaki üç seçenekten birini kullanarak etkin:</span><span class="sxs-lookup"><span data-stu-id="826a2-132">Azure SQL Database gives you full control over how recommendations are enabled using any of hello following three options:</span></span> 

* <span data-ttu-id="826a2-133">Tek tek önerileri biri aynı anda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="826a2-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="826a2-134">Etkinleştirme hello otomatik ayarlama tooautomatically önerileri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="826a2-134">Enable hello Automatic tuning tooautomatically apply recommendations.</span></span>
* <span data-ttu-id="826a2-135">tooimplement bir öneri, T-SQL betiği veritabanınızı karşı önerilen hello el ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="826a2-135">tooimplement a recommendation manually, run hello recommended T-SQL script against your database.</span></span>

<span data-ttu-id="826a2-136">Her öneri tooview ayrıntılarını seçin ve ardından **görüntülemek betik** tooreview hello tam ayrıntılarını hello öneri nasıl oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="826a2-136">Select any recommendation tooview its details and then click **View script** tooreview hello exact details of how hello recommendation is created.</span></span>

<span data-ttu-id="826a2-137">Merhaba veritabanı çevrimiçi kalır sırada hello öneri uygulanan--performans öneri veya hiçbir zaman otomatik ayarlama kullanarak bir veritabanını çevrimdışı duruma getirir.</span><span class="sxs-lookup"><span data-stu-id="826a2-137">hello database remains online while hello recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="826a2-138">Tek bir öneriyi</span><span class="sxs-lookup"><span data-stu-id="826a2-138">Apply an individual recommendation</span></span>
<span data-ttu-id="826a2-139">Gözden geçirin ve aynı anda önerileri bir kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="826a2-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="826a2-140">Merhaba üzerinde **önerileri** dikey penceresinde, öneri seçin.</span><span class="sxs-lookup"><span data-stu-id="826a2-140">On hello **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="826a2-141">Merhaba üzerinde **ayrıntıları** dikey penceresinde **Uygula** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="826a2-141">On hello **Details** blade click **Apply** button.</span></span>
   
    ![öneriyi](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="826a2-143">Seçili öneri hello veritabanı üzerinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="826a2-143">Selected recommendation will be applied on hello database.</span></span>

### <a name="removing-recommendations-from-hello-list"></a><span data-ttu-id="826a2-144">Öneriler hello listesinden kaldırılıyor</span><span class="sxs-lookup"><span data-stu-id="826a2-144">Removing recommendations from hello list</span></span>
<span data-ttu-id="826a2-145">Öneriler listesi tooremove hello listeden istediğiniz öğeleri içeriyorsa, hello öneri atabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="826a2-145">If your list of recommendations contains items that you want tooremove from hello list, you can discard hello recommendation:</span></span>

1. <span data-ttu-id="826a2-146">Merhaba listesinde bir öneri seçin **önerileri** tooopen hello ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="826a2-146">Select a recommendation in hello list of **Recommendations** tooopen hello details.</span></span>
2. <span data-ttu-id="826a2-147">Tıklatın **atmak** hello üzerinde **ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="826a2-147">Click **Discard** on hello **Details** blade.</span></span>

<span data-ttu-id="826a2-148">İsterseniz, atılan öğeler geri toohello ekleyebilirsiniz **önerileri** listesi:</span><span class="sxs-lookup"><span data-stu-id="826a2-148">If desired, you can add discarded items back toohello **Recommendations** list:</span></span>

1. <span data-ttu-id="826a2-149">Merhaba üzerinde **önerileri** dikey penceresinde **atılan Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="826a2-149">On hello **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="826a2-150">Atılan bir öğeyi hello listesi tooview ayrıntılarını seçin.</span><span class="sxs-lookup"><span data-stu-id="826a2-150">Select a discarded item from hello list tooview its details.</span></span>
3. <span data-ttu-id="826a2-151">İsteğe bağlı olarak, tıklayın **geri atmak** tooadd hello dizin geri toohello ana listesi **önerileri**.</span><span class="sxs-lookup"><span data-stu-id="826a2-151">Optionally, click **Undo Discard** tooadd hello index back toohello main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="826a2-152">Otomatik ayarlamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="826a2-152">Enable automatic tuning</span></span>
<span data-ttu-id="826a2-153">Hello Azure SQL veritabanı tooimplement önerileri otomatik olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="826a2-153">You can set hello Azure SQL Database tooimplement recommendations automatically.</span></span> <span data-ttu-id="826a2-154">Öneriler kullanılabilir duruma geldiğinde otomatik olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="826a2-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="826a2-155">Olarak hello tarafından yönetilen tüm öneriler hello performans etkisi olumsuz hello öneri ise hizmet geri alınacak.</span><span class="sxs-lookup"><span data-stu-id="826a2-155">As with all recommendations managed by hello service if hello performance impact is negative hello recommendation will be reverted.</span></span>

1. <span data-ttu-id="826a2-156">Merhaba üzerinde **önerileri** dikey penceresinde tıklatın **otomatikleştirme**:</span><span class="sxs-lookup"><span data-stu-id="826a2-156">On hello **Recommendations** blade, click **Automate**:</span></span>
   
    ![Advisor ayarları](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="826a2-158">Eylemler tooautomate seçin:</span><span class="sxs-lookup"><span data-stu-id="826a2-158">Select actions tooautomate:</span></span>
   
    ![Dizinleri önerilir](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a><span data-ttu-id="826a2-160">T-SQL betiği önerilen hello elle çalıştırma</span><span class="sxs-lookup"><span data-stu-id="826a2-160">Manually run hello recommended T-SQL script</span></span>
<span data-ttu-id="826a2-161">Herhangi bir önerisi seçin ve ardından **görüntülemek betik**.</span><span class="sxs-lookup"><span data-stu-id="826a2-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="826a2-162">Bu komut, veritabanına karşı çalışırlar toomanually hello öneriyi uygulamanız.</span><span class="sxs-lookup"><span data-stu-id="826a2-162">Run this script against your database toomanually apply hello recommendation.</span></span>

<span data-ttu-id="826a2-163">*El ile gerçekleştirilen dizinler değil izlenen ve performans etkisi hello hizmeti tarafından doğrulanan* önerilen oluşturma tooverify sonra bu dizinler izlemek için bunlar performans artışı sağlar ve ayarlamak veya onları silin gerekli.</span><span class="sxs-lookup"><span data-stu-id="826a2-163">*Indexes that are manually executed are not monitored and validated for performance impact by hello service* so it is suggested that you monitor these indexes after creation tooverify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="826a2-164">Dizin oluşturma hakkında daha fazla bilgi için bkz: [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="826a2-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="826a2-165">Öneriler iptal etme</span><span class="sxs-lookup"><span data-stu-id="826a2-165">Canceling recommendations</span></span>
<span data-ttu-id="826a2-166">Bulunan önerileri bir **bekleyen**, **doğrulama**, veya **başarı** durumu iptal edilemez.</span><span class="sxs-lookup"><span data-stu-id="826a2-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="826a2-167">Önerileri durumuna sahip bir **Executing** iptal edilemez.</span><span class="sxs-lookup"><span data-stu-id="826a2-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="826a2-168">Bir öneri hello seçin **ayarlama geçmişi** alanı tooopen hello **önerileri ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="826a2-168">Select a recommendation in hello **Tuning History** area tooopen hello **recommendations details** blade.</span></span>
2. <span data-ttu-id="826a2-169">Tıklatın **iptal** tooabort hello işleminin, hello öneri uygulanıyor.</span><span class="sxs-lookup"><span data-stu-id="826a2-169">Click **Cancel** tooabort hello process of applying hello recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="826a2-170">İzleme işlemleri</span><span class="sxs-lookup"><span data-stu-id="826a2-170">Monitoring operations</span></span>
<span data-ttu-id="826a2-171">Bir öneri uygulama eşzamanlı olarak gerçekleşebilir değil.</span><span class="sxs-lookup"><span data-stu-id="826a2-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="826a2-172">Merhaba portal öneri hello durumunu ilişkin ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="826a2-172">hello portal provides details regarding hello status of recommendation.</span></span> <span data-ttu-id="826a2-173">Merhaba, bir dizin olabilir olası durumlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="826a2-173">hello following are possible states that an index can be in:</span></span>

| <span data-ttu-id="826a2-174">Durum</span><span class="sxs-lookup"><span data-stu-id="826a2-174">Status</span></span> | <span data-ttu-id="826a2-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="826a2-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="826a2-176">Beklemede</span><span class="sxs-lookup"><span data-stu-id="826a2-176">Pending</span></span> |<span data-ttu-id="826a2-177">Komut alındı ve çalıştırılmak üzere zamanlanmış öneri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="826a2-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="826a2-178">Yürütme</span><span class="sxs-lookup"><span data-stu-id="826a2-178">Executing</span></span> |<span data-ttu-id="826a2-179">Merhaba öneri uygulanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="826a2-179">hello recommendation is being applied.</span></span> |
| <span data-ttu-id="826a2-180">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="826a2-180">Verifying</span></span> |<span data-ttu-id="826a2-181">Öneri başarıyla uygulandı ve hello hizmet hello avantajları ölçme.</span><span class="sxs-lookup"><span data-stu-id="826a2-181">Recommendation was successfully applied and hello service is measuring hello benefits.</span></span> |
| <span data-ttu-id="826a2-182">Başarılı</span><span class="sxs-lookup"><span data-stu-id="826a2-182">Success</span></span> |<span data-ttu-id="826a2-183">Öneri başarıyla uygulandı ve avantajları ölçülür.</span><span class="sxs-lookup"><span data-stu-id="826a2-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="826a2-184">Hata</span><span class="sxs-lookup"><span data-stu-id="826a2-184">Error</span></span> |<span data-ttu-id="826a2-185">Merhaba öneri uygulama hello işlemi sırasında bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="826a2-185">An error occurred during hello process of applying hello recommendation.</span></span> <span data-ttu-id="826a2-186">Bu geçici bir sorun veya büyük olasılıkla bir şema değişikliği toohello tablosu olabilir ve hello komut dosyası artık geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="826a2-186">This can be a transient issue, or possibly a schema change toohello table and hello script is no longer valid.</span></span> |
| <span data-ttu-id="826a2-187">Geri alma</span><span class="sxs-lookup"><span data-stu-id="826a2-187">Reverting</span></span> |<span data-ttu-id="826a2-188">Merhaba öneri uygulandı, ancak kullanıcı dışı olarak kabul edildi ve otomatik olarak geri döndürülüyor.</span><span class="sxs-lookup"><span data-stu-id="826a2-188">hello recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="826a2-189">Döndürüldü</span><span class="sxs-lookup"><span data-stu-id="826a2-189">Reverted</span></span> |<span data-ttu-id="826a2-190">Merhaba öneri geri döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="826a2-190">hello recommendation was reverted.</span></span> |

<span data-ttu-id="826a2-191">Bir işlemdeki önerisi hello listesi toosee daha fazla ayrıntı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="826a2-191">Click an in-process recommendation from hello list toosee more details:</span></span>

![Dizinleri önerilir](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="826a2-193">Bir öneri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="826a2-193">Reverting a recommendation</span></span>
<span data-ttu-id="826a2-194">Merhaba performans önerileri tooapply hello öneri kullandıysanız hello performans etkisi toobe negatif bulursa (el ile Merhaba T-SQL komut dosyası çalıştırılamadı anlamına gelir), otomatik olarak onu döner.</span><span class="sxs-lookup"><span data-stu-id="826a2-194">If you used hello performance recommendations tooapply hello recommendation (meaning you did not manually run hello T-SQL script) it will automatically revert it if it finds hello performance impact toobe negative.</span></span> <span data-ttu-id="826a2-195">Toorevert yalnızca istediğiniz herhangi bir nedenle bir öneri yapabileceğiniz varsa hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="826a2-195">If for any reason you simply want toorevert a recommendation you can do hello following:</span></span>

1. <span data-ttu-id="826a2-196">Başarıyla uygulandı öneri hello seçin **geçmişi ayarlama** alanı.</span><span class="sxs-lookup"><span data-stu-id="826a2-196">Select a successfully applied recommendation in hello **Tuning history** area.</span></span>
2. <span data-ttu-id="826a2-197">Tıklatın **Revert** hello üzerinde **öneri ayrıntılarını** dikey.</span><span class="sxs-lookup"><span data-stu-id="826a2-197">Click **Revert** on hello **recommendation details** blade.</span></span>

![Dizinleri önerilir](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="826a2-199">Dizin önerileri performans etkisini izleme</span><span class="sxs-lookup"><span data-stu-id="826a2-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="826a2-200">Önerileri başarıyla uygulandıktan sonra (şu anda, dizin işlemleri ve yalnızca sorguları önerileri Parametreleştirme) tıklayabilirsiniz **sorgu öngörüleri** hello öneri Ayrıntılar dikey tooopen üzerinde [sorgu Performansı öngörüleri](sql-database-query-performance.md) ve üst sorgularınızı hello performans etkisini bakın.</span><span class="sxs-lookup"><span data-stu-id="826a2-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on hello recommendation details blade tooopen [Query Performance Insights](sql-database-query-performance.md) and see hello performance impact of your top queries.</span></span>

![İzleyici performansına etkisi](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="826a2-202">Özet</span><span class="sxs-lookup"><span data-stu-id="826a2-202">Summary</span></span>
<span data-ttu-id="826a2-203">Azure SQL veritabanı SQL veritabanı performansı artırmak için öneriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="826a2-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="826a2-204">T-SQL komut dosyaları, tek tek yanı sıra ve tam otomatik, sağlayarak veritabanınızı en iyi duruma getirme ve sonuçta sorgu performansını iyileştirme yararlı bir Yardım alın.</span><span class="sxs-lookup"><span data-stu-id="826a2-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="826a2-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="826a2-205">Next steps</span></span>
<span data-ttu-id="826a2-206">Önerilerinizi izlemek ve tooapply devam bunları toorefine performans.</span><span class="sxs-lookup"><span data-stu-id="826a2-206">Monitor your recommendations and continue tooapply them toorefine performance.</span></span> <span data-ttu-id="826a2-207">Veritabanı iş yüklerini, dinamik ve sürekli olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="826a2-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="826a2-208">Azure SQL veritabanı toomonitor devam edecek ve veritabanınızın performansı artırmak öneriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="826a2-208">Azure SQL Database will continue toomonitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="826a2-209">Bkz: [otomatik ayarlama](sql-database-automatic-tuning.md) hakkında daha fazla bilgi toolearn hello Azure SQL veritabanı'nda otomatik ayarlama.</span><span class="sxs-lookup"><span data-stu-id="826a2-209">See [Automatic tuning](sql-database-automatic-tuning.md) toolearn more about hello automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="826a2-210">Bkz: [performans önerileri](sql-database-advisor.md) Azure SQL veritabanı performans önerileri genel bakış.</span><span class="sxs-lookup"><span data-stu-id="826a2-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="826a2-211">Bkz: [sorgu performansı öngörüleri](sql-database-query-performance.md) üst sorgularınızı hello performans etkisini görüntüleme hakkında toolearn.</span><span class="sxs-lookup"><span data-stu-id="826a2-211">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="826a2-212">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="826a2-212">Additional resources</span></span>
* [<span data-ttu-id="826a2-213">Sorgu deposu</span><span class="sxs-lookup"><span data-stu-id="826a2-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="826a2-214">DİZİN OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="826a2-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="826a2-215">Rol tabanlı erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="826a2-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

