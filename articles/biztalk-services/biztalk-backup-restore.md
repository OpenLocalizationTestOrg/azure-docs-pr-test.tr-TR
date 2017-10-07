---
title: "aaaCreate ve BizTalk Services bir yedeğini geri | Microsoft Docs"
description: "BizTalk Services yedekleme ve geri yüklemeyi içerir. Bilgi nasıl toocreate bir yedeğini geri yükleyin ve ne yedeklenir belirleyin. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="c3c21-105">BizTalk Services: Yedekleme ve Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="c3c21-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="c3c21-106">Azure BizTalk Services yedekleme ve geri yükleme özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="c3c21-107">Bu konu, Klasik Azure portalı nasıl toobackup ve geri yükleme BizTalk kullanarak Hizmetleri hello açıklar.</span><span class="sxs-lookup"><span data-stu-id="c3c21-107">This topic describes how toobackup and restore BizTalk Services using hello Azure classic portal.</span></span>

<span data-ttu-id="c3c21-108">BizTalk Services hello kullanarak da yedekleyebilirsiniz [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="c3c21-108">You can also back up BizTalk Services using hello [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="c3c21-109">Karma bağlantılar, Edition hello bağımsız olarak yedeklenmiş değil.</span><span class="sxs-lookup"><span data-stu-id="c3c21-109">Hybrid Connections are NOT backed up, regardless of hello Edition.</span></span> <span data-ttu-id="c3c21-110">Karma bağlantılar yeniden oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="c3c21-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="c3c21-111">Before you Begin</span></span>
* <span data-ttu-id="c3c21-112">Yedekleme ve geri yükleme tüm sürümleri için kullanılamayabilir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="c3c21-113">Bkz: [BizTalk Services: sürümler grafiği](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="c3c21-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="c3c21-114">Merhaba Klasik Azure portalı kullanarak bir talep üzerine yedekleme oluşturmak veya zamanlanmış yedekleme oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="c3c21-114">Using hello Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="c3c21-115">Yedekleme içeriği geri yüklenen toohello aynı BizTalk hizmeti veya tooa olabilir yeni BizTalk hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c3c21-115">Backup content can be restored toohello same BizTalk Service or tooa new BizTalk Service.</span></span> <span data-ttu-id="c3c21-116">toorestore hello aynı adı, BizTalk hizmeti varolan hello silinmelidir hello kullanarak BizTalk hizmeti ve hello adı kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-116">toorestore hello BizTalk Service using hello same name, hello existing BizTalk Service must be deleted and hello name must be available.</span></span> <span data-ttu-id="c3c21-117">BizTalk hizmeti sildikten sonra Merhaba aynı istedik daha uzun zaman alabilir adı toobe kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-117">After you delete a BizTalk Service, it can take longer time than wanted for hello same name toobe available.</span></span> <span data-ttu-id="c3c21-118">Merhaba bekleyemiyorsanız aynı toobe kullanılabilir olarak adlandırın ve ardından tooa geri yeni BizTalk hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c3c21-118">If you cannot wait for hello same name toobe available, then restore tooa new BizTalk Service.</span></span>
* <span data-ttu-id="c3c21-119">BizTalk Services, geri yüklenen toohello olabilir aynı sürümü veya daha yüksek bir sürüme.</span><span class="sxs-lookup"><span data-stu-id="c3c21-119">BizTalk Services can be restored toohello same edition or a higher edition.</span></span> <span data-ttu-id="c3c21-120">BizTalk Services tooa geri zaman hello yedeğin alındığı, gelen alt sürümü desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c3c21-120">Restoring BizTalk Services tooa lower edition, from when hello backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="c3c21-121">Örneğin, temel Edition olabilir hello kullanarak bir yedekleme toohello Premium Edition geri.</span><span class="sxs-lookup"><span data-stu-id="c3c21-121">For example, a backup using hello Basic Edition can be restored toohello Premium Edition.</span></span> <span data-ttu-id="c3c21-122">Premium Edition olamaz hello kullanarak bir yedekleme toohello Standard Edition geri.</span><span class="sxs-lookup"><span data-stu-id="c3c21-122">A backup using hello Premium Edition cannot be restored toohello Standard Edition.</span></span>
* <span data-ttu-id="c3c21-123">Merhaba EDI denetim numaraları hello denetim numaraları toomaintain sürekliliği desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-123">hello EDI Control numbers are backed up toomaintain continuity of hello control numbers.</span></span> <span data-ttu-id="c3c21-124">Merhaba son yedeklemeden sonra işlenen iletileri, bu yedekleme içeriğin geri yinelenen denetim numaraları neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-124">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="c3c21-125">Bir toplu etkin iletileri varsa, hello toplu işlem **önce** bir yedekleme çalıştırılıyor.</span><span class="sxs-lookup"><span data-stu-id="c3c21-125">If a batch has active messages, process hello batch **before** running a backup.</span></span> <span data-ttu-id="c3c21-126">Bir yedekleme (gerekli veya zamanlanmış olarak) oluştururken, toplu iletiler hiçbir zaman saklanır.</span><span class="sxs-lookup"><span data-stu-id="c3c21-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="c3c21-127">**Bir yedekleme toplu etkin iletilerle alınmışsa, bu iletiler yedeklenmez ve bu nedenle kaybolur.**</span><span class="sxs-lookup"><span data-stu-id="c3c21-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="c3c21-128">İsteğe bağlı: hello BizTalk Services Portalı'da, herhangi bir yönetim işlemini durdurun.</span><span class="sxs-lookup"><span data-stu-id="c3c21-128">Optional: In hello BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="c3c21-129">Bir yedekleme oluşturun</span><span class="sxs-lookup"><span data-stu-id="c3c21-129">Create a backup</span></span>
<span data-ttu-id="c3c21-130">Bir yedekleme herhangi bir zamanda alınabilir ve sizin tarafınızdan tamamen denetlenir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="c3c21-131">Bu bölümde hello Azure Klasik kullanarak hello adımları toocreate yedeklemeler listelenir portal dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="c3c21-131">This section lists hello steps toocreate backups using hello Azure classic portal, including:</span></span>

[<span data-ttu-id="c3c21-132">İsteğe bağlı bir yedekleme</span><span class="sxs-lookup"><span data-stu-id="c3c21-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="c3c21-133">Yedeklemeyi zamanlama</span><span class="sxs-lookup"><span data-stu-id="c3c21-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="c3c21-134"><a name="backupnow"></a>İsteğe bağlı bir yedekleme</span><span class="sxs-lookup"><span data-stu-id="c3c21-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="c3c21-135">Hello Klasik Azure portalı, seçin **BizTalk Services**, ve ardından BizTalk toobackup istediğiniz hizmetleri seçin hello.</span><span class="sxs-lookup"><span data-stu-id="c3c21-135">In hello Azure classic portal, select **BizTalk Services**, and then select hello BizTalk Service you want toobackup.</span></span>
2. <span data-ttu-id="c3c21-136">Merhaba, **Pano** sekmesine **yedekleme** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="c3c21-136">In hello **Dashboard** tab, select **Back up** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="c3c21-137">Yedek bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="c3c21-137">Enter a backup name.</span></span> <span data-ttu-id="c3c21-138">Örneğin *myBizTalkService*BU*tarih*.</span><span class="sxs-lookup"><span data-stu-id="c3c21-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="c3c21-139">Bir blob storage hesabı ve select hello onay işareti toostart hello yedeklemeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="c3c21-139">Choose a blob storage account and select hello checkmark toostart hello backup.</span></span>

<span data-ttu-id="c3c21-140">Hello Yedekleme tamamlandıktan sonra bir kapsayıcı girdiğiniz hello yedek adı ile Merhaba depolama hesabı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c3c21-140">Once hello backup completes, a container with hello backup name you enter is created in hello storage account.</span></span> <span data-ttu-id="c3c21-141">Bu kapsayıcı, BizTalk hizmeti yedekleme yapılandırmanızı içerir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="c3c21-142"><a name="backupschedule"></a>Yedeklemeyi zamanlama</span><span class="sxs-lookup"><span data-stu-id="c3c21-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="c3c21-143">Hello Klasik Azure portalı, seçin **BizTalk Services**, select hello tooschedule hello yedekleme istediğiniz ve hello ardından BizTalk hizmeti adını **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="c3c21-143">In hello Azure classic portal, select **BizTalk Services**, select hello BizTalk Service name you want tooschedule hello backup, and then select hello **Configure** tab.</span></span>
2. <span data-ttu-id="c3c21-144">Set hello **yedekleme durumu** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="c3c21-144">Set hello **Backup Status** too**Automatic**.</span></span> 
3. <span data-ttu-id="c3c21-145">Select hello **depolama hesabı** toostore yedekleme Merhaba, hello girin **sıklığı** toocreate hello yedeklemeleri ve ne kadar süreyle tookeep hello yedeklemeleri (**bekletme gün**):</span><span class="sxs-lookup"><span data-stu-id="c3c21-145">Select hello **Storage Account** toostore hello backup, enter hello **Frequency** toocreate hello backups, and how long tookeep hello backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="c3c21-146">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="c3c21-146">**Notes**</span></span>     
   
   * <span data-ttu-id="c3c21-147">İçinde **bekletme gün**, hello saklama dönemi hello yedekleme sıklığı büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c3c21-147">In **Retention Days**, hello retention period must be greater than hello backup frequency.</span></span>
   * <span data-ttu-id="c3c21-148">Seçin **her zaman en az bir yedekleme tutun**, hello saklama süresi olsa bile.</span><span class="sxs-lookup"><span data-stu-id="c3c21-148">Select **Always keep at least one backup**, even if it is past hello retention period.</span></span>
4. <span data-ttu-id="c3c21-149">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="c3c21-149">Select **Save**.</span></span>

<span data-ttu-id="c3c21-150">Zamanlanmış bir yedekleme işini çalıştırdığında, girdiğiniz hello depolama hesabında bir kapsayıcı (toostore yedekleme verilerini) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3c21-150">When a scheduled backup job runs, it creates a container (toostore backup data) in hello storage account you entered.</span></span> <span data-ttu-id="c3c21-151">Merhaba hello kapsayıcının adını adlandırılan *BizTalk hizmeti adı-tarih-saat*.</span><span class="sxs-lookup"><span data-stu-id="c3c21-151">hello name of hello container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="c3c21-152">Merhaba BizTalk hizmeti Pano gösterirse bir **başarısız** durumu:</span><span class="sxs-lookup"><span data-stu-id="c3c21-152">If hello BizTalk Service dashboard shows a **Failed** status:</span></span>

![Zamanlanan son yedekleme durumu][BackupStatus] 

<span data-ttu-id="c3c21-154">Merhaba bağlantı hello Yönetim Hizmetleri işlem günlükleri toohelp sorun giderme açar.</span><span class="sxs-lookup"><span data-stu-id="c3c21-154">hello link opens hello Management Services Operation Logs toohelp troubleshoot.</span></span> <span data-ttu-id="c3c21-155">Bkz: [BizTalk Services: işlem günlükleri kullanarak sorun giderme](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="c3c21-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="c3c21-156">Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="c3c21-156">Restore</span></span>
<span data-ttu-id="c3c21-157">Merhaba Klasik Azure portalı veya hello yedeklerini geri [geri BizTalk hizmeti REST API'si](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="c3c21-157">You can restore backups from hello Azure classic portal or from hello [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="c3c21-158">Bu bölümde hello Klasik portalı kullanarak hello adımları toorestore listelenir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-158">This section lists hello steps toorestore using hello classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="c3c21-159">Bir yedeği geri yüklemeden önce</span><span class="sxs-lookup"><span data-stu-id="c3c21-159">Before restoring a backup</span></span>
* <span data-ttu-id="c3c21-160">Yeni izleme, arşivleme ve depoları izleme BizTalk hizmeti geri yüklenirken girilebilir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="c3c21-161">Merhaba aynı EDI çalışma zamanı verileri geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-161">hello same EDI Runtime data is restored.</span></span> <span data-ttu-id="c3c21-162">Merhaba EDI çalışma zamanı yedekleme hello denetim numaraları depolar.</span><span class="sxs-lookup"><span data-stu-id="c3c21-162">hello EDI Runtime backup stores hello control numbers.</span></span> <span data-ttu-id="c3c21-163">geri hello denetim hello yedekleme hello saati sırayla numaralarıdır.</span><span class="sxs-lookup"><span data-stu-id="c3c21-163">hello restored control numbers are in sequence from hello time of hello backup.</span></span> <span data-ttu-id="c3c21-164">Merhaba son yedeklemeden sonra işlenen iletileri, bu yedekleme içeriğin geri yinelenen denetim numaraları neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-164">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="c3c21-165">Yedeği geri yükleme</span><span class="sxs-lookup"><span data-stu-id="c3c21-165">Restore a backup</span></span>
1. <span data-ttu-id="c3c21-166">Hello Klasik Azure portalı, seçin **yeni** > **uygulama hizmetleri** > **BizTalk hizmeti** > **geri yükleme** :</span><span class="sxs-lookup"><span data-stu-id="c3c21-166">In hello Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Yedeği geri yükleme][Restore]
2. <span data-ttu-id="c3c21-168">İçinde **yedekleme URL**hello klasör simgesini seçin ve depoları BizTalk hizmeti yapılandırma yedeği hello hello Azure depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="c3c21-168">In **Backup URL**, select hello folder icon and expand hello Azure storage account that stores hello BizTalk Service configuration backup.</span></span> <span data-ttu-id="c3c21-169">Merhaba kapsayıcısını genişletin ve geri .txt dosyasının yedeğini karşılık gelen hello hello sağ bölmede seçin.</span><span class="sxs-lookup"><span data-stu-id="c3c21-169">Expand hello container and in hello right pane, select hello corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="c3c21-170">Seçin **açık**.</span><span class="sxs-lookup"><span data-stu-id="c3c21-170">Select **Open**.</span></span>
3. <span data-ttu-id="c3c21-171">Merhaba üzerinde **geri yükleme BizTalk hizmeti** want bir **BizTalk hizmeti adı** ve hello doğrulayın **etki alanı URL'si**, **Edition**ve **Bölge** hello BizTalk hizmeti geri için.</span><span class="sxs-lookup"><span data-stu-id="c3c21-171">On hello **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify hello **Domain URL**, **Edition**, and **Region** for hello restored BizTalk Service.</span></span> <span data-ttu-id="c3c21-172">**Yeni bir SQL veritabanı oluştur** veritabanı izleme hello için:</span><span class="sxs-lookup"><span data-stu-id="c3c21-172">**Create a new SQL database instance** for hello tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="c3c21-173">Merhaba İleri okunu seçin.</span><span class="sxs-lookup"><span data-stu-id="c3c21-173">Select hello next arrow.</span></span>
4. <span data-ttu-id="c3c21-174">Merhaba hello SQL veritabanı adını doğrulayın, bu sunucu için hello fiziksel sunucu hello SQL veritabanının oluşturulacağı ve bir kullanıcı adı/parola girin.</span><span class="sxs-lookup"><span data-stu-id="c3c21-174">Verify hello name of hello SQL database, enter hello physical server where hello SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="c3c21-175">Tooconfigure hello SQL veritabanı sürümü, boyutu ve diğer özellikleri istiyorsanız seçin **Gelişmiş veritabanı ayarlarını yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="c3c21-175">If you want tooconfigure hello SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="c3c21-176">Merhaba İleri okunu seçin.</span><span class="sxs-lookup"><span data-stu-id="c3c21-176">Select hello next arrow.</span></span>

1. <span data-ttu-id="c3c21-177">Yeni bir depolama hesabı oluşturun veya hello BizTalk hizmeti için mevcut bir depolama hesabını girin.</span><span class="sxs-lookup"><span data-stu-id="c3c21-177">Create a new storage account or enter an existing storage account for hello BizTalk Service.</span></span>
2. <span data-ttu-id="c3c21-178">Merhaba onay işareti toostart hello geri seçin.</span><span class="sxs-lookup"><span data-stu-id="c3c21-178">Select hello checkmark toostart hello restore.</span></span>

<span data-ttu-id="c3c21-179">Merhaba geri yükleme başarıyla tamamlandıktan sonra yeni bir BizTalk hizmeti askıya alınmış durumda hello Klasik Azure Portalı'ndaki hello BizTalk Services sayfasında listelenir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-179">Once hello restoration successfully completes, a new BizTalk Service is listed in a suspended state on hello BizTalk Services page in hello Azure classic portal.</span></span>

### <span data-ttu-id="c3c21-180"><a name="postrestore"></a>Bir yedekleme geri yükledikten sonra</span><span class="sxs-lookup"><span data-stu-id="c3c21-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="c3c21-181">Merhaba BizTalk hizmeti her zaman içinde geri bir **askıya** durumu.</span><span class="sxs-lookup"><span data-stu-id="c3c21-181">hello BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="c3c21-182">Bu durumda, önce Hello yeni ortam işlevsel dahil olmak üzere yapılandırma değişiklikleri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c3c21-182">In this state, you can make any configuration changes before hello new environment is functional, including:</span></span>

* <span data-ttu-id="c3c21-183">BizTalk hizmeti uygulamalarını hello Azure BizTalk Services SDK'sını kullanarak oluşturduysanız, bu uygulamaları toowork geri hello ortamıyla tootooupdate hello erişim denetimi (ACS) kimlik bilgileri gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-183">If you created BizTalk Service applications using hello Azure BizTalk Services SDK, you may need tootooupdate hello Access Control (ACS) credentials in those applications toowork with hello restored environment.</span></span>
* <span data-ttu-id="c3c21-184">BizTalk hizmeti tooreplicate mevcut bir BizTalk hizmeti ortamına geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c3c21-184">You restore a BizTalk Service tooreplicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="c3c21-185">Bir kaynak FTP klasörü kullanmak hello özgün BizTalk Services Portalı'nda yapılandırılmış anlaşmaları varsa, bu durumda, yeni geri hello ortamı toouse farklı kaynak FTP klasörü tooupdate hello sözleşmelerde gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-185">In this situation, if there are agreements configured in hello original BizTalk Services portal that use a source FTP folder, you may need tooupdate hello agreements in hello newly restored environment toouse a different source FTP folder.</span></span> <span data-ttu-id="c3c21-186">Aksi takdirde olabilir toopull çalışırken iki farklı anlaşmaları hello aynı ileti.</span><span class="sxs-lookup"><span data-stu-id="c3c21-186">Otherwise, there may be two different agreements trying toopull hello same message.</span></span>
* <span data-ttu-id="c3c21-187">Birden çok BizTalk hizmeti ortamları toohave geri yüklediyseniz, hello Visual Studio uygulamaları, PowerShell cmdlet'leri, REST API'leri veya ticari ortak Yönetimi OM API'leri doğru ortamında hello hedef emin olun.</span><span class="sxs-lookup"><span data-stu-id="c3c21-187">If you restored toohave multiple BizTalk Service environments, make sure you target hello correct environment in hello Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="c3c21-188">İyi bir uygulama tooconfigure otomatik yedeklemeler yeni geri hello BizTalk hizmeti ortamda olur.</span><span class="sxs-lookup"><span data-stu-id="c3c21-188">It's a good practice tooconfigure automated backups on hello newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="c3c21-189">Merhaba Klasik Azure portalı select hello toostart hello BizTalk hizmeti geri BizTalk hizmeti ve select **Sürdür** hello görev çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="c3c21-189">toostart hello BizTalk Service in hello Azure classic portal, select hello restored BizTalk Service and select **Resume** in hello task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="c3c21-190">Ne yedeklenir</span><span class="sxs-lookup"><span data-stu-id="c3c21-190">What gets backed up</span></span>
<span data-ttu-id="c3c21-191">Bir yedek oluşturulduğunda hello aşağıdaki öğeleri yedeklenir:</span><span class="sxs-lookup"><span data-stu-id="c3c21-191">When a backup is created, hello following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="c3c21-192">Yedeklenecek öğe</span><span class="sxs-lookup"><span data-stu-id="c3c21-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="c3c21-193">
 <strong>Azure BizTalk Services portalı</strong></span><span class="sxs-lookup"><span data-stu-id="c3c21-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="c3c21-194">Yapılandırma ve çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="c3c21-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="c3c21-195">İş ortakları ve profili ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="c3c21-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="c3c21-196">Ortak sözleşmeleri</span><span class="sxs-lookup"><span data-stu-id="c3c21-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="c3c21-197">Dağıtılan özel derlemeler</span><span class="sxs-lookup"><span data-stu-id="c3c21-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="c3c21-198">Dağıtılan köprüleri</span><span class="sxs-lookup"><span data-stu-id="c3c21-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="c3c21-199">Sertifikalar</span><span class="sxs-lookup"><span data-stu-id="c3c21-199">Certificates</span></span></li>
<li><span data-ttu-id="c3c21-200">Dağıtılan dönüşümler</span><span class="sxs-lookup"><span data-stu-id="c3c21-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="c3c21-201">İşlem hatları</span><span class="sxs-lookup"><span data-stu-id="c3c21-201">Pipelines</span></span></li>
<li><span data-ttu-id="c3c21-202">Oluşturulan ve hello BizTalk Services portalı kaydedilen şablonları</span><span class="sxs-lookup"><span data-stu-id="c3c21-202">Templates created and saved in hello BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="c3c21-203">X12 ST01 ve GS01 eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="c3c21-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="c3c21-204">Denetim numaraları (EDI)</span><span class="sxs-lookup"><span data-stu-id="c3c21-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="c3c21-205">AS2 ileti MIC değerleri</span><span class="sxs-lookup"><span data-stu-id="c3c21-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="c3c21-206">
 <strong>Azure BizTalk hizmeti</strong></span><span class="sxs-lookup"><span data-stu-id="c3c21-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="c3c21-207">SSL sertifikası</span><span class="sxs-lookup"><span data-stu-id="c3c21-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="c3c21-208">SSL sertifikası verileri</span><span class="sxs-lookup"><span data-stu-id="c3c21-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="c3c21-209">SSL sertifika parolası</span><span class="sxs-lookup"><span data-stu-id="c3c21-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="c3c21-210">BizTalk hizmeti ayarları</span><span class="sxs-lookup"><span data-stu-id="c3c21-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="c3c21-211">Ölçek birimi sayısı</span><span class="sxs-lookup"><span data-stu-id="c3c21-211">Scale unit count</span></span></li>
<li><span data-ttu-id="c3c21-212">Sürüm</span><span class="sxs-lookup"><span data-stu-id="c3c21-212">Edition</span></span></li>
<li><span data-ttu-id="c3c21-213">Ürün sürümü:</span><span class="sxs-lookup"><span data-stu-id="c3c21-213">Product Version</span></span></li>
<li><span data-ttu-id="c3c21-214">Bölge/veri merkezi</span><span class="sxs-lookup"><span data-stu-id="c3c21-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="c3c21-215">Erişim denetimi Hizmeti'nden (ACS) ad alanı ve anahtarı</span><span class="sxs-lookup"><span data-stu-id="c3c21-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="c3c21-216">Veritabanı bağlantı dizesi izleme</span><span class="sxs-lookup"><span data-stu-id="c3c21-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="c3c21-217">Depolama hesabı bağlantı dizesi arşivleme</span><span class="sxs-lookup"><span data-stu-id="c3c21-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="c3c21-218">Depolama hesabı bağlantı dizesi izleme</span><span class="sxs-lookup"><span data-stu-id="c3c21-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="c3c21-219">
 <strong>Ek öğeler</strong></span><span class="sxs-lookup"><span data-stu-id="c3c21-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="c3c21-220">Veritabanı izleme</span><span class="sxs-lookup"><span data-stu-id="c3c21-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="c3c21-221">Merhaba BizTalk hizmeti oluşturulduğunda, hello Azure SQL veritabanı sunucusu ve hello izleme veritabanı adı dahil olmak üzere hello izleme veritabanı ayrıntıları girilir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-221">When hello BizTalk Service is created, hello Tracking Database details are entered, including hello Azure SQL Database Server and hello Tracking Database name.</span></span> <span data-ttu-id="c3c21-222">Merhaba izleme veritabanı otomatik olarak yedeklenmez.</span><span class="sxs-lookup"><span data-stu-id="c3c21-222">hello Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="c3c21-223">
<strong>Önemli</strong></span><span class="sxs-lookup"><span data-stu-id="c3c21-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="c3c21-224">Merhaba izleme veritabanı silinir ve kurtarılan veritabanının gereksinimlerine Merhaba, önceki bir yedekleme mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-224">If hello Tracking Database is deleted and hello database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="c3c21-225">Bir yedek yoksa, hello izleme veritabanı ve veri kurtarılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-225">If a backup does not exist, hello Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="c3c21-226">Bu durumda, yeni bir izleme veritabanı ile Merhaba oluşturmak aynı veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="c3c21-226">In this situation, create a new Tracking Database with hello same database name.</span></span> <span data-ttu-id="c3c21-227">Coğrafi çoğaltma önerilir.</span><span class="sxs-lookup"><span data-stu-id="c3c21-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="c3c21-228">Sonraki</span><span class="sxs-lookup"><span data-stu-id="c3c21-228">Next</span></span>
<span data-ttu-id="c3c21-229">toocreate Azure BizTalk Services hello Azure Klasik portal, Git çok[BizTalk Services: sağlama kullanarak Azure Klasik portalı](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="c3c21-229">toocreate Azure BizTalk Services in hello Azure classic portal, go too[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="c3c21-230">uygulamaları, Git çok oluşturma toostart[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="c3c21-230">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="c3c21-231">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="c3c21-231">See Also</span></span>
* [<span data-ttu-id="c3c21-232">BizTalk hizmeti yedekleme</span><span class="sxs-lookup"><span data-stu-id="c3c21-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="c3c21-233">BizTalk hizmeti yedekten geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="c3c21-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="c3c21-234">BizTalk Services: Geliştirici, temel, standart ve Premium sürümler grafiği</span><span class="sxs-lookup"><span data-stu-id="c3c21-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="c3c21-235">BizTalk Services: Klasik portalı kullanarak Azure hazırlama</span><span class="sxs-lookup"><span data-stu-id="c3c21-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="c3c21-236">BizTalk Services: Durum Grafiğini hazırlama</span><span class="sxs-lookup"><span data-stu-id="c3c21-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="c3c21-237">BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri</span><span class="sxs-lookup"><span data-stu-id="c3c21-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="c3c21-238">BizTalk Services: Azaltma</span><span class="sxs-lookup"><span data-stu-id="c3c21-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="c3c21-239">BizTalk Services: Verenin Adı ve Verenin Anahtarı</span><span class="sxs-lookup"><span data-stu-id="c3c21-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="c3c21-240">I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello</span><span class="sxs-lookup"><span data-stu-id="c3c21-240">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

