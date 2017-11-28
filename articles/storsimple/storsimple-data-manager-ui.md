---
title: "Azure StorSimple veri Yöneticisi kullanıcı Arabirimi aaaMicrosoft | Microsoft Docs"
description: "Açıklar nasıl toouse StorSimple veri Yöneticisi hizmetini UI (özel olarak incelenmektedir)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="19b64-103">Merhaba StorSimple veri Yöneticisi hizmeti kullanıcı Arabirimi (özel olarak incelenmektedir) kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="19b64-103">Manage using hello StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="19b64-104">Bu makalede hello StorSimple 8000 serisi cihazlar üzerinde bulunan verileri hello StorSimple veri Yöneticisi kullanıcı Arabirimi tooperform veri dönüştürme nasıl kullanabileceğiniz açıklanır.</span><span class="sxs-lookup"><span data-stu-id="19b64-104">This article explains how you can use hello StorSimple Data Manager UI tooperform data transformation on data residing on hello StorSimple 8000 series devices.</span></span> <span data-ttu-id="19b64-105">Merhaba dönüştürülen veriler sonra Azure Media Services, Azure Hdınsight, Azure Machine Learning ve Azure Search gibi Azure diğer hizmetler tarafından kullanılabilecek.</span><span class="sxs-lookup"><span data-stu-id="19b64-105">hello transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="19b64-106">StorSimple veri dönüşümü kullanın</span><span class="sxs-lookup"><span data-stu-id="19b64-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="19b64-107">Merhaba StorSimple Data Manager içinde veri dönüştürme oluşturulabilir hello kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="19b64-107">hello StorSimple Data Manager is hello resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="19b64-108">Merhaba veri dönüştürme hizmeti, StorSimple şirket içi cihaz tooblobs Azure storage'da veri taşıma olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="19b64-108">hello Data Transformation service lets you move data from your StorSimple on-premises device tooblobs in Azure storage.</span></span> <span data-ttu-id="19b64-109">Bu nedenle, iş akışında, toospecify hello ayrıntıları StorSimple cihaz ve hello verilerinizi toomove toohello depolama hesabı istediğiniz ilgi hakkında gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b64-109">Hence, in workflow you need toospecify hello details about your StorSimple device and hello data of interest that you want toomove toohello storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="19b64-110">Bir StorSimple veri Yöneticisi hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="19b64-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="19b64-111">Aşağıdaki adımları toocreate bir StorSimple veri Yöneticisi hizmeti hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="19b64-111">Perform hello following steps toocreate a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="19b64-112">toocreate bir StorSimple veri Yöneticisi hizmeti Git çok[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span><span class="sxs-lookup"><span data-stu-id="19b64-112">toocreate a StorSimple Data Manager service, go too[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="19b64-113">Merhaba tıklatın ** + ** simgesi ve StorSimple veri Yöneticisi arama.</span><span class="sxs-lookup"><span data-stu-id="19b64-113">Click hello **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="19b64-114">StorSimple veri Yöneticisi hizmetinize tıklayın ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="19b64-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="19b64-115">Bu hizmet oluşturmak için aboneliğinizi etkinse, dikey penceresinde aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="19b64-115">If your subscription is enabled for creating this service, you see hello following blade.</span></span>

    ![StorSimple veri yöneticilerini kaynak oluşturma](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="19b64-117">Merhaba girişleri girin ve tıklayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="19b64-117">Enter hello inputs and click **Create**.</span></span> <span data-ttu-id="19b64-118">konum, depolama hesaplarınızı ve StorSimple Yöneticisi hizmetiniz barındıran bir hello olmalıdır Hello belirtildi.</span><span class="sxs-lookup"><span data-stu-id="19b64-118">hello specified location should be hello one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="19b64-119">Şu anda yalnızca Batı ABD ve Batı Avrupa bölgeleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="19b64-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="19b64-120">Bu nedenle, StorSimple Yöneticisi hizmeti, veri Yöneticisi hizmeti ve hello depolama hesabı tüm desteklenen hello önceki bölgelerde olmalıdır ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="19b64-120">Hence, your StorSimple Manager service, Data Manager service, and hello associated storage account should all be in hello preceding supported regions.</span></span> <span data-ttu-id="19b64-121">Bir dakika toocreate hello hizmeti hakkında alır.</span><span class="sxs-lookup"><span data-stu-id="19b64-121">It takes about a minute toocreate hello service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="19b64-122">Veri dönüştürme iş tanımı oluştur</span><span class="sxs-lookup"><span data-stu-id="19b64-122">Create a data transformation job definition</span></span>

<span data-ttu-id="19b64-123">Bir StorSimple Data Manager Hizmeti'nde toocreate veri dönüştürme iş tanımı gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b64-123">Within a StorSimple Data Manager service, you need toocreate a data transformation job definition.</span></span> <span data-ttu-id="19b64-124">Bir iş tanımı hello yerel biçiminde bir depolama hesabı taşınmasını ilgilendiğiniz hello veri ayrıntılarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="19b64-124">A job definition specifies details of hello data that you are interested in moving into a storage account in hello native format.</span></span> 

<span data-ttu-id="19b64-125">Aşağıdaki adımları toocreate yeni bir veri dönüştürme işi tanımı hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="19b64-125">Perform hello following steps toocreate a new data transformation job definition.</span></span>

1.  <span data-ttu-id="19b64-126">Oluşturduğunuz toohello hizmete gidin.</span><span class="sxs-lookup"><span data-stu-id="19b64-126">Navigate toohello service that you created.</span></span> <span data-ttu-id="19b64-127">Tıklatın **+ iş tanımı**.</span><span class="sxs-lookup"><span data-stu-id="19b64-127">Click **+ Job Definition**.</span></span>

    ![Tıklatın + iş tanımı](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="19b64-129">Merhaba yeni iş tanımı bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="19b64-129">hello new job definition blade opens up.</span></span> <span data-ttu-id="19b64-130">İş tanımı bir ad verin ve tıklatın **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="19b64-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="19b64-131">Merhaba, **yapılandırma veri kaynağı** dikey penceresinde, StorSimple Cihazınızı hello ayrıntılarını belirtin ve hello verileri.</span><span class="sxs-lookup"><span data-stu-id="19b64-131">In hello **Configure data source** blade, specify hello details of your StorSimple device and hello data of interest.</span></span>

    ![İş tanımı oluştur](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. <span data-ttu-id="19b64-133">Bu yeni bir veri Yöneticisi hizmeti olduğundan, hiçbir veri depoları yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="19b64-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="19b64-134">tooadd, bir veri deposu olarak StorSimple Yöneticisi **yeni Ekle** hello veri deposu açılır ve ardından **eklemek veri deposu**.</span><span class="sxs-lookup"><span data-stu-id="19b64-134">tooadd your StorSimple Manager as a data repository, click **Add new** in hello data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="19b64-135">Seçin **StorSimple 8000 serisi Yöneticisi** hello deposu olarak yazın ve hello özelliklerini girin, **StorSimple Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="19b64-135">Choose **StorSimple 8000 series Manager** as hello repository type and enter hello properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="19b64-136">Hello için **kaynak kimliği** alan, hello önce tooenter hello numarasını ihtiyacınız **:** hello kayıt anahtarı, StorSimple Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="19b64-136">For hello **Resource Id** field, you need tooenter hello number before hello **:** in hello registration key of your StorSimple manager.</span></span>

    ![Veri kaynağı oluşturun](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="19b64-138">Tıklatın **Tamam** bittiğinde.</span><span class="sxs-lookup"><span data-stu-id="19b64-138">Click **OK** when done.</span></span> <span data-ttu-id="19b64-139">Bu veri deponuz kaydeder ve bu StorSimple Yöneticisi diğer iş tanımları bu parametreler tekrar girmeden yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="19b64-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="19b64-140">Tıklattıktan sonra birkaç saniye sürer **Tamam** hello hello açılır listesinde, StorSimple Yöneticisi tooshow yedeklemek için.</span><span class="sxs-lookup"><span data-stu-id="19b64-140">It takes a few seconds after you click **OK** for hello StorSimple Manager tooshow up in hello dropdown.</span></span>

6.  <span data-ttu-id="19b64-141">Merhaba, **yapılandırma veri kaynağı** dikey penceresinde hello aygıt adı girin ve hello verilerinizi ilgi birim adı.</span><span class="sxs-lookup"><span data-stu-id="19b64-141">In hello **Configure data source** blade, enter hello device name and hello volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="19b64-142">Merhaba, **filtre** alt bölüm, verilerinizi ilgi içeren hello kök dizini girin (Bu alan ile başlaması gereken bir `\`).</span><span class="sxs-lookup"><span data-stu-id="19b64-142">In hello **Filter** subsection, enter hello root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="19b64-143">Dosya filtreleri burada da ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19b64-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="19b64-144">Merhaba veri dönüştürme hizmeti Azure toohello anlık görüntüleri gönderilen hello veri çalışır.</span><span class="sxs-lookup"><span data-stu-id="19b64-144">hello data transformation service works on hello data that is pushed up toohello Azure via snapshots.</span></span> <span data-ttu-id="19b64-145">Bu iş çalışırken, bu işi (en son verileri toowork) çalıştırın veya toouse hello hello bulutta son varolan yedekleme (bazı arşivlenmiş veriler üzerinde çalışıyorsanız) her zaman tootake bir yedekleme seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19b64-145">When running this job, you can choose tootake a backup every time this job is run (toowork on latest data) or toouse hello last existing backup in hello cloud (if you are working on some archived data).</span></span>

    ![Yeni veri kaynağı ayrıntıları](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="19b64-147">Ardından, hello hedef ayarları yapılandırılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b64-147">Next, hello Target settings need toobe configured.</span></span> <span data-ttu-id="19b64-148">Desteklenen hedefleri – Azure Storage ve Azure Media Services hesapları 2 tür vardır.</span><span class="sxs-lookup"><span data-stu-id="19b64-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="19b64-149">Depolama hesapları, bu hesaptaki BLOB'lar içine tooput dosyaları seçin.</span><span class="sxs-lookup"><span data-stu-id="19b64-149">Choose storage accounts tooput files into blobs in that account.</span></span> <span data-ttu-id="19b64-150">Media services hesabı tooput dosyaları bu hesaptaki varlıklar'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="19b64-150">Choose media services account tooput files into assets in that account.</span></span> <span data-ttu-id="19b64-151">Yeniden tooadd depo gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b64-151">Again, we need tooadd a repository.</span></span> <span data-ttu-id="19b64-152">Merhaba açılır menüde seçin **yeni Ekle** ve ardından **ayarlarını yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="19b64-152">In hello dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![Veri havuzu oluşturma](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="19b64-154">Burada, hello deposuyla ilişkili diğer parametreleri tooadd ve hello istediğiniz havuz hello türü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19b64-154">Here, you can select hello type of repository you want tooadd and hello other parameters associated with hello repository.</span></span> <span data-ttu-id="19b64-155">Merhaba işi çalıştığında, her iki durumda da, bir depolama kuyruğu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="19b64-155">In both cases, a storage queue is created when hello job runs.</span></span> <span data-ttu-id="19b64-156">Bu kuyruk, hazır olduğunda dönüştürülen bloblar hakkında iletilerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="19b64-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="19b64-157">Bu sıranın Hello adı olduğu hello hello iş tanımı hello adı ile aynı.</span><span class="sxs-lookup"><span data-stu-id="19b64-157">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="19b64-158">Seçerseniz **Media Services** hello depo türü, sonra da depolama hesabının kimlik bilgilerini hello Sıranın oluşturulduğu girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19b64-158">If you select **Media Services** as hello repo type, then you can also enter storage account credentials where hello queue is created.</span></span>

    ![Yeni veri havuzu ayrıntıları](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="19b64-160">(Bu, birkaç saniye sürer) hello veri deposu ekledikten sonra hello hello açılır, hello depodaki bulabilirsiniz **hedef hesap adı**.</span><span class="sxs-lookup"><span data-stu-id="19b64-160">After adding hello data repository (which takes a few seconds), you will find hello repo in hello dropdown in hello **Target account name**.</span></span>  <span data-ttu-id="19b64-161">Gereksinim duyduğunuz hello hedef seçin.</span><span class="sxs-lookup"><span data-stu-id="19b64-161">Choose hello target that you need.</span></span>

12. <span data-ttu-id="19b64-162">Tıklatın **Tamam** toocreate hello iş tanımı.</span><span class="sxs-lookup"><span data-stu-id="19b64-162">Click **OK** toocreate hello job definition.</span></span> <span data-ttu-id="19b64-163">İş tanımı şimdi ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="19b64-163">Your job definition is now set up.</span></span> <span data-ttu-id="19b64-164">Bu iş tanımı birden çok kez aracılığıyla hello kullanıcı Arabirimi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19b64-164">You can use this job definition multiple times via hello UI.</span></span>

    ![Yeni iş tanımı Ekle](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a><span data-ttu-id="19b64-166">Merhaba iş tanımı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="19b64-166">Run hello job definition</span></span>

<span data-ttu-id="19b64-167">StorSimple toohello depolama hesabından hello iş tanımında belirtilen toomove veri ihtiyaç duyduğunuzda tooinvoke gerekir.</span><span class="sxs-lookup"><span data-stu-id="19b64-167">Whenever you need toomove data from StorSimple toohello storage account that you have specified in hello job definition, you will need tooinvoke it.</span></span> <span data-ttu-id="19b64-168">Merhaba parametrelerinin değiştirilmesi hello iş çağırma her zaman biraz esneklik vardır.</span><span class="sxs-lookup"><span data-stu-id="19b64-168">There is some flexibility in changing hello parameters every time you invoke hello job.</span></span> <span data-ttu-id="19b64-169">Merhaba adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="19b64-169">hello steps are as follows:</span></span>

1. <span data-ttu-id="19b64-170">StorSimple Data Manager hizmetinizi seçin ve çok Git**izleme**.</span><span class="sxs-lookup"><span data-stu-id="19b64-170">Select your StorSimple Data Manager service and go too**Monitoring**.</span></span> <span data-ttu-id="19b64-171">Tıklatın **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="19b64-171">Click **Run Now**.</span></span>

    ![Tetikleyici iş tanımı](./media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="19b64-173">Merhaba iş tanımı seçin toorun istiyor.</span><span class="sxs-lookup"><span data-stu-id="19b64-173">Choose hello job definition that you want toorun.</span></span> <span data-ttu-id="19b64-174">Tıklatın **çalışma ayarları** toomodify bu işi çalıştırmak için toochange isteyebilirsiniz herhangi bir ayarı.</span><span class="sxs-lookup"><span data-stu-id="19b64-174">Click **Run settings** toomodify any settings that you might want toochange for this job run.</span></span>

    ![Çalışma proje ayarları](./media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="19b64-176">Tıklatın **Tamam** ve ardından **çalıştırmak** toolaunch işinizi.</span><span class="sxs-lookup"><span data-stu-id="19b64-176">Click **OK** and then click **Run** toolaunch your job.</span></span> <span data-ttu-id="19b64-177">toomonitor bu iş, Git toohello **işleri** sayfası, StorSimple veri Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="19b64-177">toomonitor this job, go toohello **Jobs** page in your StorSimple Data Manager.</span></span>

    ![İşlerini listesi ve durumu](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="19b64-179">Merhaba içinde toplama toomonitoring içinde **işleri** dikey penceresinde, ayrıca dinlemesi hello depolama kuyruğu burada bir ileti eklenen her zaman bir dosya StorSimple toohello depolama hesabından taşınır.</span><span class="sxs-lookup"><span data-stu-id="19b64-179">In addition toomonitoring in hello **Jobs** blade, you can also listen on hello storage queue where a message is added every time a file is moved from StorSimple toohello storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="19b64-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19b64-180">Next steps</span></span>

<span data-ttu-id="19b64-181">[.NET SDK'sı toolaunch StorSimple Data Manager işleri](storsimple-data-manager-dotnet-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="19b64-181">[Use .NET SDK toolaunch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>
