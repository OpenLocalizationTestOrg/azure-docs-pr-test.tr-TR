---
title: "bir StorSimple sanal dizisinde aaaInstall güncelleştirmeleri | Microsoft Docs"
description: "Toouse hello StorSimple sanal dizinin web kullanıcı Arabirimi tooapply hello portal ve düzeltme yöntemi kullanılarak nasıl güncelleştirdiği açıklar"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="544e3-103">StorSimple sanal dizinizi üzerinde güncelleştirmeleri yükle</span><span class="sxs-lookup"><span data-stu-id="544e3-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="544e3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="544e3-104">Overview</span></span>
<span data-ttu-id="544e3-105">Bu makalede, StorSimple sanal dizisindeki hello yerel web kullanıcı Arabirimi aracılığıyla ve hello Klasik Azure Portalı aracılığıyla hello adımları gerekli tooinstall güncelleştirmeleri anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="544e3-105">This article describes hello steps required tooinstall updates on your StorSimple Virtual Array via hello local web UI and via hello Azure classic portal.</span></span> <span data-ttu-id="544e3-106">Tooapply yazılım güncelleştirmeleri veya düzeltmeleri tookeep StorSimple sanal dizinizi güncel gerekir.</span><span class="sxs-lookup"><span data-stu-id="544e3-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="544e3-107">Bir güncelleştirme veya düzeltme yükleme, aygıt yeniden unutmayın.</span><span class="sxs-lookup"><span data-stu-id="544e3-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="544e3-108">Verilen Hello StorSimple sanal dizinin bir tek düğümlü aygıt olduğundan, devam eden tüm g/ç kesintiye ve kapalı kalma süresi Cihazınızı karşılaştığında.</span><span class="sxs-lookup"><span data-stu-id="544e3-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="544e3-109">Bir güncelleştirmeyi uygulamadan önce hello birimlerinin almak veya paylaşımlarında çevrimdışı hello ilk ana bilgisayar ve aygıt hello öneririz.</span><span class="sxs-lookup"><span data-stu-id="544e3-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="544e3-110">Bu veri bozulması olasılığını en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="544e3-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="544e3-111">Güncelleştirme 0.1 veya GA yazılım sürümleri çalıştırıyorsanız, hello düzeltme hello yerel web kullanıcı Arabirimi tooinstall güncelleştirme 0.3 yöntemiyle kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="544e3-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="544e3-112">Güncelleştirme 0.2 çalıştırıyorsanız, hello Klasik Azure Portalı aracılığıyla hello güncelleştirmeleri yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="544e3-112">If you are running Update 0.2, we recommend that you install hello updates via hello Azure classic portal.</span></span>
> 
> 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="544e3-113">Merhaba yerel web kullanıcı arabirimini kullanın</span><span class="sxs-lookup"><span data-stu-id="544e3-113">Use hello local web UI</span></span>
<span data-ttu-id="544e3-114">Merhaba yerel web kullanıcı arabirimini kullanırken iki adımı vardır:</span><span class="sxs-lookup"><span data-stu-id="544e3-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="544e3-115">Merhaba update veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="544e3-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="544e3-116">Merhaba güncelleştirme veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="544e3-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="544e3-117">Merhaba update veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="544e3-117">Download hello update or hello hotfix</span></span>
<span data-ttu-id="544e3-118">Hello Microsoft Update Kataloğu ' adımları toodownload hello yazılım güncelleştirmesi aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="544e3-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="544e3-119">toodownload hello güncelleştirme veya hello düzeltme</span><span class="sxs-lookup"><span data-stu-id="544e3-119">toodownload hello update or hello hotfix</span></span>
1. <span data-ttu-id="544e3-120">Internet Explorer'ı başlatın ve çok gidin[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="544e3-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="544e3-121">Bu bilgisayarda Microsoft Update Kataloğu hello kullanarak ilk kez olursa **yükleme** zaman istendiğinde tooinstall hello Microsoft Update Kataloğu eklentisi.</span><span class="sxs-lookup"><span data-stu-id="544e3-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="544e3-122">Merhaba arama kutusuna hello Microsoft Update Kataloğu hello Bilgi Bankası (KB) numarasını girin hello düzeltme toodownload istiyor.</span><span class="sxs-lookup"><span data-stu-id="544e3-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="544e3-123">Girin **3182061** Update 0.3 ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="544e3-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="544e3-124">Merhaba düzeltme listesi, örneğin, göründüğünde **StorSimple sanal dizinin güncelleştirme 0.3**.</span><span class="sxs-lookup"><span data-stu-id="544e3-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Katalogda arama](./media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="544e3-126">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="544e3-126">Click **Add**.</span></span> <span data-ttu-id="544e3-127">Merhaba güncelleştirme toohello Sepeti eklenir.</span><span class="sxs-lookup"><span data-stu-id="544e3-127">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="544e3-128">**Sepeti Görüntüle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="544e3-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="544e3-129">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="544e3-129">Click **Download**.</span></span> <span data-ttu-id="544e3-130">Belirtin veya **Gözat** tooa yerel konum istediğiniz hello tooappear indirir.</span><span class="sxs-lookup"><span data-stu-id="544e3-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="544e3-131">Merhaba güncelleştirmelerin yükleneceği toohello konumu belirtilen ve alt hello hello update ile aynı ad ile yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="544e3-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="544e3-132">Merhaba klasör de hello aygıttan ulaşılabilir kopyalanan tooa ağ paylaşımı olabilir.</span><span class="sxs-lookup"><span data-stu-id="544e3-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
7. <span data-ttu-id="544e3-133">Açık hello kopyaladığınız klasörü, Microsoft Update tek başına paket dosyası görmelisiniz `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="544e3-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="544e3-134">Bu, kullanılan tooinstall hello güncelleştirme veya düzeltme dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="544e3-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="544e3-135">Merhaba güncelleştirme veya hello düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="544e3-135">Install hello update or hello hotfix</span></span>
<span data-ttu-id="544e3-136">Önceki toohello güncelleştirme veya düzeltme yükleme, bir ağ paylaşımı üzerinden erişilebilir veya hello güncelleştirmeye sahip veya hello düzeltmeyi indirdiğiniz, ana bilgisayarda yerel olarak ya da emin olun.</span><span class="sxs-lookup"><span data-stu-id="544e3-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="544e3-137">Bu yöntem tooinstall güncelleştirmeleri GA çalıştıran bir cihazda kullanmayı veya 0,1 yazılım sürümleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="544e3-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="544e3-138">Bu yordamı 2 dakika toocomplete değerinden alır.</span><span class="sxs-lookup"><span data-stu-id="544e3-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="544e3-139">Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.</span><span class="sxs-lookup"><span data-stu-id="544e3-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="544e3-140">tooinstall hello güncelleştirme veya hello düzeltme</span><span class="sxs-lookup"><span data-stu-id="544e3-140">tooinstall hello update or hello hotfix</span></span>
1. <span data-ttu-id="544e3-141">Merhaba yerel web kullanıcı Arabirimi, çok Git**Bakım** > **yazılım güncelleştirmesi**.</span><span class="sxs-lookup"><span data-stu-id="544e3-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="544e3-143">İçinde **güncelleştirme dosya yolu**, hello güncelleştirmesi hello dosya adı girin veya düzeltme hello.</span><span class="sxs-lookup"><span data-stu-id="544e3-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="544e3-144">Ayrıca, bir ağ paylaşımında girdiyseniz toohello güncelleştirme veya düzeltme yükleme dosyası göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="544e3-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="544e3-145">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="544e3-145">Click **Apply**.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="544e3-147">Bir uyarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="544e3-147">A warning is displayed.</span></span> <span data-ttu-id="544e3-148">Bir tek düğümlü aygıt hello güncelleştirme uygulanana, hello aygıt yeniden başladıktan sonra kapalı kalma süresi budur.</span><span class="sxs-lookup"><span data-stu-id="544e3-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="544e3-149">Merhaba onay simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="544e3-149">Click hello check icon.</span></span>
   
   ![cihaz güncelleştirme](./media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="544e3-151">Merhaba güncelleştirme başlatır.</span><span class="sxs-lookup"><span data-stu-id="544e3-151">hello update starts.</span></span> <span data-ttu-id="544e3-152">Merhaba cihaz başarıyla güncelleştirildikten sonra yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="544e3-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="544e3-153">Merhaba yerel UI bu süre içinde erişilebilir durumda değil.</span><span class="sxs-lookup"><span data-stu-id="544e3-153">hello local UI is not accessible in this duration.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="544e3-155">Merhaba yeniden başlatma tamamlandıktan sonra toohello gerçekleştirilen **oturum** sayfası.</span><span class="sxs-lookup"><span data-stu-id="544e3-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="544e3-156">Merhaba aygıt yazılımı güncelleştirdi, hello yerel web kullanıcı Arabirimi, tooverify Git çok**Bakım** > **yazılım güncelleştirmesi**.</span><span class="sxs-lookup"><span data-stu-id="544e3-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="544e3-157">Görüntülenen hello yazılım sürüm olmalıdır **10.0.0.0.0.10288.0** güncelleştirme 0.3 için.</span><span class="sxs-lookup"><span data-stu-id="544e3-157">hello displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="544e3-158">Biz hello yerel web kullanıcı Arabirimi biraz farklı bir yolla hello yazılım sürümleri rapor ve klasik Azure portalı hello.</span><span class="sxs-lookup"><span data-stu-id="544e3-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure classic portal.</span></span> <span data-ttu-id="544e3-159">Örneğin, yerel web kullanıcı Arabirimi raporları'nı hello **10.0.0.0.0.10288** ve Azure Klasik portalı raporları hello **10.0.10288.0** hello için aynı sürüm.</span><span class="sxs-lookup"><span data-stu-id="544e3-159">For example, hello local web UI reports **10.0.0.0.0.10288** and hello Azure classic portal reports **10.0.10288.0** for hello same version.</span></span> 
   > 
   > 
   
    ![cihaz güncelleştirme](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="544e3-161">Merhaba Klasik Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="544e3-161">Use hello Azure classic portal</span></span>
<span data-ttu-id="544e3-162">Güncelleştirme 0.2 çalıştırılıyorsa hello Klasik Azure Portalı aracılığıyla güncelleştirmeleri yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="544e3-162">If running Update 0.2, we recommend that you install updates through hello Azure classic portal.</span></span> <span data-ttu-id="544e3-163">Merhaba kullanıcı tooscan Hello portal yordamı gerektirir, indirin ve ardından hello güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="544e3-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="544e3-164">Bu yordamı yaklaşık 7 dakika toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="544e3-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="544e3-165">Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.</span><span class="sxs-lookup"><span data-stu-id="544e3-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="544e3-166">Merhaba sonra yükleme (% 100 İş durumu belirtildiği gibi) tamamlandığında, çok Git**cihazlar > bakım > yazılım güncelleştirmelerini**.</span><span class="sxs-lookup"><span data-stu-id="544e3-166">After hello installation is complete (as indicated by job status at 100 %), go too**Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="544e3-167">Görüntülenen hello yazılım sürümü 10.0.10288.0 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="544e3-167">hello displayed software version should be 10.0.10288.0.</span></span>

![cihaz güncelleştirme](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="544e3-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="544e3-169">Next steps</span></span>
<span data-ttu-id="544e3-170">Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="544e3-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

