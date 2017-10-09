---
title: "aaaGet Azure portalda Azure Scheduler ile başlatıldı | Microsoft Docs"
description: "Azure portalda Azure Scheduler kullanmaya başlama"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a><span data-ttu-id="325d9-103">Azure portalda Azure Scheduler kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="325d9-103">Get started with Azure Scheduler in Azure portal</span></span>
<span data-ttu-id="325d9-104">Azure scheduler'da zamanlanmış kolay toocreate işleri olur.</span><span class="sxs-lookup"><span data-stu-id="325d9-104">It's easy toocreate scheduled jobs in Azure Scheduler.</span></span> <span data-ttu-id="325d9-105">Bu öğreticide şunları öğreneceksiniz nasıl toocreate bir işi.</span><span class="sxs-lookup"><span data-stu-id="325d9-105">In this tutorial, you'll learn how toocreate a job.</span></span> <span data-ttu-id="325d9-106">Ayrıca Scheduler’ın izleme ve yönetim özelliklerini öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="325d9-106">You'll also learn Scheduler's monitoring and management capabilities.</span></span>

## <a name="create-a-job"></a><span data-ttu-id="325d9-107">Bir iş oluşturma</span><span class="sxs-lookup"><span data-stu-id="325d9-107">Create a job</span></span>
1. <span data-ttu-id="325d9-108">Çok oturum[Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="325d9-108">Sign in too[Azure portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="325d9-109">Tıklatın **+ yeni** > türü *Zamanlayıcı* hello arama kutusuna > seçin **Zamanlayıcı** sonuçlarında > tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="325d9-109">Click **+New** > type *Scheduler* in hello search box >  select **Scheduler** in results > click **Create**.</span></span>
   
    ![][marketplace-create]
3. <span data-ttu-id="325d9-110">Şimdi bir GET isteğiyle http://www.microsoft.com/ adresine işaret eden bir iş oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="325d9-110">Let’s create a job that simply hits http://www.microsoft.com/ with a GET request.</span></span> <span data-ttu-id="325d9-111">Merhaba, **Scheduler işi** ekranında, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="325d9-111">In hello **Scheduler Job** screen, enter hello following information:</span></span>
   
   1. <span data-ttu-id="325d9-112">**Ad:** `getmicrosoft`</span><span class="sxs-lookup"><span data-stu-id="325d9-112">**Name:** `getmicrosoft`</span></span>  
   2. <span data-ttu-id="325d9-113">**Abonelik:** Azure aboneliğiniz</span><span class="sxs-lookup"><span data-stu-id="325d9-113">**Subscription:** Your Azure subscription</span></span>   
   3. <span data-ttu-id="325d9-114">**İş Koleksiyonu:** Mevcut bir iş koleksiyonu seçin veya tıklatın **Yeni Oluştur**’a tıklayın > bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="325d9-114">**Job Collection:** Select an existing job collection, or click **Create New** > enter a name.</span></span>
4. <span data-ttu-id="325d9-115">İleri ' **eylem ayarları**, değerleri aşağıdaki hello tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="325d9-115">Next, in **Action Settings**, define hello following values:</span></span>
   
   1. <span data-ttu-id="325d9-116">**Eylem Türü:** ` HTTP`</span><span class="sxs-lookup"><span data-stu-id="325d9-116">**Action Type:** ` HTTP`</span></span>  
   2. <span data-ttu-id="325d9-117">**Yöntem:** `GET`</span><span class="sxs-lookup"><span data-stu-id="325d9-117">**Method:** `GET`</span></span>  
   3. <span data-ttu-id="325d9-118">**URL:** ` http://www.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="325d9-118">**URL:** ` http://www.microsoft.com`</span></span>  
      
      ![][action-settings]
5. <span data-ttu-id="325d9-119">Son olarak, şimdi bir zamanlama tanımlayalım.</span><span class="sxs-lookup"><span data-stu-id="325d9-119">Finally, let's define a schedule.</span></span> <span data-ttu-id="325d9-120">Merhaba iş bir kerelik iş olarak tanımlanabilir, ancak şimdi bir yineleme zamanlaması seçin:</span><span class="sxs-lookup"><span data-stu-id="325d9-120">hello job could be defined as a one-time job, but let’s pick a recurrence schedule:</span></span>
   
   1. <span data-ttu-id="325d9-121">**Yineleme**: `Recurring`</span><span class="sxs-lookup"><span data-stu-id="325d9-121">**Recurrence**: `Recurring`</span></span>
   2. <span data-ttu-id="325d9-122">**Başlat**: Bugünün tarihi</span><span class="sxs-lookup"><span data-stu-id="325d9-122">**Start**: Today's date</span></span>
   3. <span data-ttu-id="325d9-123">**Yineleme sıklığı**: `12 Hours`</span><span class="sxs-lookup"><span data-stu-id="325d9-123">**Recur every**: `12 Hours`</span></span>
   4. <span data-ttu-id="325d9-124">**Bitiş tarihi**: Bugünden itibaren iki gün</span><span class="sxs-lookup"><span data-stu-id="325d9-124">**End by**: Two days from today's date</span></span>  
      
      ![][recurrence-schedule]
6. <span data-ttu-id="325d9-125">**Oluştur**'a tıklayın</span><span class="sxs-lookup"><span data-stu-id="325d9-125">Click **Create**</span></span>

## <a name="manage-and-monitor-jobs"></a><span data-ttu-id="325d9-126">İşleri yönetme ve izleme</span><span class="sxs-lookup"><span data-stu-id="325d9-126">Manage and monitor jobs</span></span>
<span data-ttu-id="325d9-127">Bir işi oluşturulduktan sonra hello ana Azure panosunda görünür.</span><span class="sxs-lookup"><span data-stu-id="325d9-127">Once a job is created, it appears in hello main Azure dashboard.</span></span> <span data-ttu-id="325d9-128">Hello iş ve yeni bir'ı sekmeleri aşağıdaki hello ile penceresi açılır:</span><span class="sxs-lookup"><span data-stu-id="325d9-128">Click hello job and a new window opens with hello following tabs:</span></span>

1. <span data-ttu-id="325d9-129">Özellikler</span><span class="sxs-lookup"><span data-stu-id="325d9-129">Properties</span></span>  
2. <span data-ttu-id="325d9-130">Eylem Ayarları</span><span class="sxs-lookup"><span data-stu-id="325d9-130">Action Settings</span></span>  
3. <span data-ttu-id="325d9-131">Zamanlama</span><span class="sxs-lookup"><span data-stu-id="325d9-131">Schedule</span></span>  
4. <span data-ttu-id="325d9-132">Geçmiş</span><span class="sxs-lookup"><span data-stu-id="325d9-132">History</span></span>
5. <span data-ttu-id="325d9-133">Kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="325d9-133">Users</span></span>
   
   ![][job-overview]

### <a name="properties"></a><span data-ttu-id="325d9-134">Özellikler</span><span class="sxs-lookup"><span data-stu-id="325d9-134">Properties</span></span>
<span data-ttu-id="325d9-135">Bu salt okunur özellikler hello Scheduler işi için hello yönetim meta verilerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="325d9-135">These read-only properties describe hello management metadata for hello Scheduler job.</span></span>

   ![][job-properties]

### <a name="action-settings"></a><span data-ttu-id="325d9-136">Eylem ayarları</span><span class="sxs-lookup"><span data-stu-id="325d9-136">Action settings</span></span>
<span data-ttu-id="325d9-137">Hello bir projede tıklayarak **işleri** ekran iş tooconfigure sağlar.</span><span class="sxs-lookup"><span data-stu-id="325d9-137">Clicking on a job in hello **Jobs** screen allows you tooconfigure that job.</span></span> <span data-ttu-id="325d9-138">Bu, Gelişmiş ayarları yapılandırmak, hello yapılandırmadıysanız, hızlı Oluşturma sihirbazında sağlar.</span><span class="sxs-lookup"><span data-stu-id="325d9-138">This lets you configure advanced settings, if you didn't configure them in hello quick-create wizard.</span></span>

<span data-ttu-id="325d9-139">Tüm eylem türleri için hello yeniden deneme ilkesi ve hello hata eylemini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="325d9-139">For all action types, you may change hello retry policy and hello error action.</span></span>

<span data-ttu-id="325d9-140">HTTP ve HTTPS iş eylemi türleri için hello yöntemi tooany HTTP eylemine izin değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="325d9-140">For HTTP and HTTPS job action types, you may change hello method tooany allowed HTTP verb.</span></span> <span data-ttu-id="325d9-141">Ayrıca ekleyebilir, silmek veya hello üstbilgileri ve temel kimlik doğrulama bilgilerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="325d9-141">You may also add, delete, or change hello headers and basic authentication information.</span></span>

<span data-ttu-id="325d9-142">Depolama kuyruğu eylem türleri için hello depolama hesabı, kuyruk adı, SAS belirteci ve gövde değişebilir.</span><span class="sxs-lookup"><span data-stu-id="325d9-142">For storage queue action types, you may change hello storage account, queue name, SAS token, and body.</span></span>

<span data-ttu-id="325d9-143">Hizmet veri yolu eylemi türleri için hello ad alanı, konu/kuyruk yolu, kimlik doğrulama ayarları, aktarım türü, ileti özellikleri ve ileti gövdesini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="325d9-143">For service bus action types, you may change hello namespace, topic/queue path, authentication settings, transport type, message properties, and message body.</span></span>

   ![][job-action-settings]

### <a name="schedule"></a><span data-ttu-id="325d9-144">Zamanlama</span><span class="sxs-lookup"><span data-stu-id="325d9-144">Schedule</span></span>
<span data-ttu-id="325d9-145">Bu, hello zamanlamayı yeniden yapılandırın, hello oluşturulan toochange hello zamanlama isterseniz hızlı Oluşturma sihirbazında sağlar.</span><span class="sxs-lookup"><span data-stu-id="325d9-145">This lets you reconfigure hello schedule, if you'd like toochange hello schedule you created in hello quick-create wizard.</span></span>

<span data-ttu-id="325d9-146">Bir fırsat toobuild budur [karmaşık zamanlamalar ve Gelişmiş yineleme işinizde](scheduler-advanced-complexity.md)</span><span class="sxs-lookup"><span data-stu-id="325d9-146">This is an opportunity toobuild [complex schedules and advanced recurrence in your job](scheduler-advanced-complexity.md)</span></span>

<span data-ttu-id="325d9-147">Hello başlangıç tarihi değiştirebilir ve zaman, yineleme zamanlamasını ve hello bitiş tarihi ve (Merhaba iş yineleniyorsa.) süresi</span><span class="sxs-lookup"><span data-stu-id="325d9-147">You may change hello start date and time, recurrence schedule, and hello end date and time (if hello job is recurring.)</span></span>

   ![][job-schedule]

### <a name="history"></a><span data-ttu-id="325d9-148">Geçmiş</span><span class="sxs-lookup"><span data-stu-id="325d9-148">History</span></span>
<span data-ttu-id="325d9-149">Merhaba **geçmişi** sekmesi hello Seçili iş için hello sistemdeki her iş yürütme için seçilen ölçümleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="325d9-149">hello **History** tab displays selected metrics for every job execution in hello system for hello selected job.</span></span> <span data-ttu-id="325d9-150">Bu ölçümler hello Scheduler sistem durumunuz ile ilgili gerçek zamanlı değerleri girin:</span><span class="sxs-lookup"><span data-stu-id="325d9-150">These metrics provide real-time values regarding hello health of your Scheduler:</span></span>

1. <span data-ttu-id="325d9-151">Durum</span><span class="sxs-lookup"><span data-stu-id="325d9-151">Status</span></span>  
2. <span data-ttu-id="325d9-152">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="325d9-152">Details</span></span>  
3. <span data-ttu-id="325d9-153">Yeniden deneme sayısı</span><span class="sxs-lookup"><span data-stu-id="325d9-153">Retry attempts</span></span>
4. <span data-ttu-id="325d9-154">Oluşma 1., 2., 3., vs.</span><span class="sxs-lookup"><span data-stu-id="325d9-154">Occurrence: 1st, 2nd, 3rd, etc.</span></span>
5. <span data-ttu-id="325d9-155">Yürütme başlangıç saati</span><span class="sxs-lookup"><span data-stu-id="325d9-155">Start time of execution</span></span>  
6. <span data-ttu-id="325d9-156">Yürütme bitiş saati</span><span class="sxs-lookup"><span data-stu-id="325d9-156">End time of execution</span></span>
   
   ![][job-history]

<span data-ttu-id="325d9-157">Üzerinde çalışma tooview tıklayabilirsiniz kendi **geçmiş ayrıntıları**, hello her yürütmeye ilişkin tüm yanıtlar dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="325d9-157">You can click on a run tooview its **History Details**, including hello whole response for every execution.</span></span> <span data-ttu-id="325d9-158">Bu iletişim kutusu ayrıca toocopy hello yanıt toohello Pano sağlar.</span><span class="sxs-lookup"><span data-stu-id="325d9-158">This dialog box also allows you toocopy hello response toohello clipboard.</span></span>

   ![][job-history-details]

### <a name="users"></a><span data-ttu-id="325d9-159">Kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="325d9-159">Users</span></span>
<span data-ttu-id="325d9-160">Azure Rol Tabanlı Erişim Denetimi (RBAC), Azure Scheduler için ayrıntılı erişim yönetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="325d9-160">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure Scheduler.</span></span> <span data-ttu-id="325d9-161">toouse hello kullanıcılar sekmesini başvurmak çok nasıl toolearn[Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="325d9-161">toolearn how toouse hello Users tab, refer too[Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="325d9-162">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="325d9-162">See also</span></span>
 [<span data-ttu-id="325d9-163">Scheduler nedir?</span><span class="sxs-lookup"><span data-stu-id="325d9-163">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="325d9-164">Scheduler kavramları, terminolojisi ve varlık hiyerarşisi</span><span class="sxs-lookup"><span data-stu-id="325d9-164">Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="325d9-165">Azure Scheduler’da planlar ve faturalama</span><span class="sxs-lookup"><span data-stu-id="325d9-165">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="325d9-166">Nasıl toobuild karmaşık zamanlar ve Gelişmiş yineleme Azure Scheduler ile</span><span class="sxs-lookup"><span data-stu-id="325d9-166">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="325d9-167">Scheduler REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="325d9-167">Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="325d9-168">Scheduler PowerShell cmdlet’leri başvurusu</span><span class="sxs-lookup"><span data-stu-id="325d9-168">Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="325d9-169">Yüksek Scheduler kullanılabilirliği ve güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="325d9-169">Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="325d9-170">Scheduler sınırları, varsayılanları ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="325d9-170">Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="325d9-171">Scheduler giden bağlantı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="325d9-171">Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
