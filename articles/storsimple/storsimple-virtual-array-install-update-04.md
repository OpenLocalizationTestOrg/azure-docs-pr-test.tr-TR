---
title: "StorSimple sanal dizisinde güncelleştirmeleri yükle | Microsoft Docs"
description: "StorSimple sanal dizinin web kullanıcı Arabirimi Azure portal ve düzeltme yöntemini kullanarak güncelleştirmeleri uygulamak için nasıl kullanılacağını açıklar"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/07/2017
ms.author: alkohli
ms.openlocfilehash: 3fb246b1515e7a637e6cff6499bf324c3f80dd45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-04-on-your-storsimple-virtual-array"></a><span data-ttu-id="f408f-103">StorSimple sanal dizinizi üzerinde güncelleştirme 0.4 yükleyin</span><span class="sxs-lookup"><span data-stu-id="f408f-103">Install Update 0.4 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="f408f-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f408f-104">Overview</span></span>

<span data-ttu-id="f408f-105">Bu makalede, yerel web kullanıcı Arabirimi aracılığıyla ve Azure portalı üzerinden, StorSimple sanal dizisindeki 0.4 güncelleştirmeyi yüklemek için gereken adımlar açıklanır.</span><span class="sxs-lookup"><span data-stu-id="f408f-105">This article describes the steps required to install Update 0.4 on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="f408f-106">Yazılım güncelleştirmelerini veya düzeltmeleri StorSimple sanal dizinizi güncel tutmak için uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f408f-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="f408f-107">Bir güncelleştirme veya düzeltme yükleme, aygıt yeniden unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f408f-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="f408f-108">Bir tek düğümlü cihaz StorSimple sanal dizinin olması koşuluyla, devam eden tüm g/ç kesintiye ve kapalı kalma süresi Cihazınızı karşılaştığında.</span><span class="sxs-lookup"><span data-stu-id="f408f-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="f408f-109">Bir güncelleştirmeyi uygulamadan önce birimler veya paylaşımlar çevrimdışı konakta ilk almanızı öneririz ve ardından cihaz.</span><span class="sxs-lookup"><span data-stu-id="f408f-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="f408f-110">Bu veri bozulması olasılığını en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="f408f-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f408f-111">Güncelleştirme 0.1 veya GA yazılım sürümleri çalıştırıyorsanız, update 0.3 yüklemek için yerel web kullanıcı Arabirimi aracılığıyla düzeltme yöntemini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f408f-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="f408f-112">Daha sonra öneririz veya güncelleştirme 0.2 çalıştırıyorsanız Azure Portalı aracılığıyla güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f408f-112">If you are running Update 0.2 or later, we recommend that you install the updates via the Azure portal.</span></span>
 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="f408f-113">Yerel web kullanıcı arabirimini kullanın</span><span class="sxs-lookup"><span data-stu-id="f408f-113">Use the local web UI</span></span>

<span data-ttu-id="f408f-114">Yerel web kullanıcı arabirimini kullanırken iki adımı vardır:</span><span class="sxs-lookup"><span data-stu-id="f408f-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="f408f-115">Güncelleştirmeyi veya düzeltmeyi indirin</span><span class="sxs-lookup"><span data-stu-id="f408f-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="f408f-116">Güncelleştirmeyi veya düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="f408f-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="f408f-117">Güncelleştirmeyi veya düzeltmeyi indirin</span><span class="sxs-lookup"><span data-stu-id="f408f-117">Download the update or the hotfix</span></span>

<span data-ttu-id="f408f-118">Microsoft Update Kataloğu'ndan yazılım güncelleştirmesi indirmek için aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="f408f-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="f408f-119">Güncelleştirmeyi veya düzeltmeyi indirmek için</span><span class="sxs-lookup"><span data-stu-id="f408f-119">To download the update or the hotfix</span></span>

1. <span data-ttu-id="f408f-120">Internet Explorer'ı başlatın ve [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com) adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="f408f-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="f408f-121">Microsoft Update Kataloğu’nu bu bilgisayarda ilk kez kullanıyorsanız, sorulduğunda **Yükle**’ye tıklayarak Microsoft Update Kataloğu eklentisini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f408f-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="f408f-122">Microsoft Update Kataloğu arama kutusuna, yüklemek istediğiniz düzeltme Bilgi Bankası (KB) sayısını girin.</span><span class="sxs-lookup"><span data-stu-id="f408f-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="f408f-123">Girin **3216577** 0.4 güncelleştirmesi için ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="f408f-123">Enter **3216577** for Update 0.4, and then click **Search**.</span></span>
   
    <span data-ttu-id="f408f-124">Düzeltme listesi göründüğünde, örneğin, **StorSimple sanal dizinin güncelleştirme 0.4**.</span><span class="sxs-lookup"><span data-stu-id="f408f-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.4**.</span></span>
   
    ![Katalogda arama](./media/storsimple-virtual-array-install-update-04/download1.png)

4. <span data-ttu-id="f408f-126">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f408f-126">Click **Add**.</span></span> <span data-ttu-id="f408f-127">Güncelleştirme sepete eklenir.</span><span class="sxs-lookup"><span data-stu-id="f408f-127">The update is added to the basket.</span></span>

5. <span data-ttu-id="f408f-128">**Sepeti Görüntüle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f408f-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="f408f-129">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f408f-129">Click **Download**.</span></span> <span data-ttu-id="f408f-130">İndirilen öğelerin görünmesini istediğiniz yerel konumu belirtin veya **Gözat** seçeneğiyle konumu bulun.</span><span class="sxs-lookup"><span data-stu-id="f408f-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="f408f-131">Güncelleştirmeler belirtilen konuma indirilir ve güncelleştirme ile aynı adı taşıyan alt klasöre yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f408f-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="f408f-132">Klasör, cihazdan erişilebilen bir ağ paylaşımına da kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="f408f-132">The folder can also be copied to a network share that is reachable from the device.</span></span>

7. <span data-ttu-id="f408f-133">Kopyalanan klasörünü açın, bir Microsoft Update tek başına paket dosyası görmelisiniz `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="f408f-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="f408f-134">Bu dosya, güncelleştirme veya düzeltme yüklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f408f-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="f408f-135">Güncelleştirmeyi veya düzeltmeyi yükleyin</span><span class="sxs-lookup"><span data-stu-id="f408f-135">Install the update or the hotfix</span></span>

<span data-ttu-id="f408f-136">Güncelleştirme veya düzeltme yükleme önce bir ağ paylaşımı üzerinden erişilebilir veya güncelleştirmeye sahip veya ana bilgisayarınız yerel olarak ya da düzeltmeyi indirdiğiniz olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f408f-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="f408f-137">GA çalıştıran bir cihazda güncelleştirmeleri yüklemek veya 0,1 yazılım sürümleri güncelleştirmek için bu yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="f408f-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="f408f-138">Bu yordamı tamamlamak için değerinden 2 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="f408f-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="f408f-139">Güncelleştirme veya düzeltme yüklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="f408f-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="f408f-140">Güncelleştirme veya düzeltme yüklemek için</span><span class="sxs-lookup"><span data-stu-id="f408f-140">To install the update or the hotfix</span></span>

1. <span data-ttu-id="f408f-141">Yerel web kullanıcı Arabirimi, Git **Bakım** > **yazılım güncelleştirmesi**.</span><span class="sxs-lookup"><span data-stu-id="f408f-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="f408f-143">İçinde **güncelleştirme dosya yolu**, güncelleştirme veya düzeltme için dosya adı girin.</span><span class="sxs-lookup"><span data-stu-id="f408f-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="f408f-144">Ayrıca, bir ağ paylaşımında girdiyseniz güncelleştirme veya düzeltme yükleme dosyasına göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f408f-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="f408f-145">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f408f-145">Click **Apply**.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="f408f-147">Bir uyarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f408f-147">A warning is displayed.</span></span> <span data-ttu-id="f408f-148">Bir tek düğümlü aygıt güncelleştirme uygulanana, aygıt yeniden başladıktan sonra kapalı kalma süresi budur.</span><span class="sxs-lookup"><span data-stu-id="f408f-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="f408f-149">Onay simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f408f-149">Click the check icon.</span></span>
   
   ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="f408f-151">Güncelleştirme başlatır.</span><span class="sxs-lookup"><span data-stu-id="f408f-151">The update starts.</span></span> <span data-ttu-id="f408f-152">Cihaz başarıyla güncelleştirildikten sonra yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="f408f-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="f408f-153">Yerel kullanıcı arabirimini bu süre içinde erişilebilir durumda değil.</span><span class="sxs-lookup"><span data-stu-id="f408f-153">The local UI is not accessible in this duration.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="f408f-155">Yeniden başlatma tamamlandıktan sonra gittiğiniz **oturum** sayfası.</span><span class="sxs-lookup"><span data-stu-id="f408f-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="f408f-156">Aygıt yazılımı, yerel web kullanıcı Arabirimi, güncelleştirilmiş olduğunu doğrulamak için Git **Bakım** > **yazılım güncelleştirmesi**.</span><span class="sxs-lookup"><span data-stu-id="f408f-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="f408f-157">Görüntülenen yazılım sürümü olmalıdır **10.0.0.0.0.10289.0** 0.4 güncelleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="f408f-157">The displayed software version should be **10.0.0.0.0.10289.0** for Update 0.4.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f408f-158">Yazılım sürümlerini yerel web kullanıcı Arabirimi biraz farklı bir şekilde hem de Azure portalında bildirin.</span><span class="sxs-lookup"><span data-stu-id="f408f-158">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="f408f-159">Örneğin, yerel web kullanıcı Arabirimi raporları **10.0.0.0.0.10289** ve Azure portal raporları **10.0.10289.0** aynı sürüm için.</span><span class="sxs-lookup"><span data-stu-id="f408f-159">For example, the local web UI reports **10.0.0.0.0.10289** and the Azure portal reports **10.0.10289.0** for the same version.</span></span>
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-the-azure-portal"></a><span data-ttu-id="f408f-161">Azure portalı kullanma</span><span class="sxs-lookup"><span data-stu-id="f408f-161">Use the Azure portal</span></span>

<span data-ttu-id="f408f-162">Güncelleştirme 0.2 ve sonraki sürümleri çalışıyorsa, Azure portal aracılığıyla güncelleştirmeleri yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="f408f-162">If running Update 0.2 and later, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="f408f-163">Portal yordamı tarama, indirme ve güncelleştirmeleri yüklemek kullanıcının gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f408f-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="f408f-164">Bu yordamı tamamlamak için yaklaşık 7 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="f408f-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="f408f-165">Güncelleştirme veya düzeltme yüklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="f408f-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="f408f-166">(Olarak % 100 İş durumu tarafından gösterilen) yükleme tamamlandıktan sonra StorSimple cihaz Yöneticisi hizmetinize gidin.</span><span class="sxs-lookup"><span data-stu-id="f408f-166">After the installation is complete (as indicated by job status at 100 %), go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="f408f-167">Seçin **aygıtları** seçin ve bu hizmete bağlı aygıtlar listesinde güncelleştirmek istediğiniz cihaza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f408f-167">Select **Devices** and then select and click the device you want to update from the list of devices connected to this service.</span></span> <span data-ttu-id="f408f-168">İçinde **ayarları** dikey penceresinde, Git **Yönet** bölümünde ve seçin **aygıt güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="f408f-168">In the **Settings** blade, go to **Manage** section and select **Device updates**.</span></span> <span data-ttu-id="f408f-169">Görüntülenen yazılım sürümü olmalıdır **10.0.10289.0**.</span><span class="sxs-lookup"><span data-stu-id="f408f-169">The displayed software version should be **10.0.10289.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f408f-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f408f-170">Next steps</span></span>

<span data-ttu-id="f408f-171">Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="f408f-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

