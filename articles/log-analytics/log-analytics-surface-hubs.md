---
title: "Surface Hubs Azure günlük analizi ile aaaMonitor | Microsoft Docs"
description: "Merhaba Surface Hub çözüm tootrack hello durumunu, Surface hub'larınız kullanın ve nasıl kullanıldıkları anlayın."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a><span data-ttu-id="50335-103">Surface hub'ları ile günlük analizi tootrack durumlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="50335-103">Monitor Surface Hubs with Log Analytics tootrack their health</span></span>

![Yüzey Hub simgesi](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="50335-105">Bu makalede, günlük analizi toomonitor Microsoft Surface Hub cihazları hello Microsoft Operations Management Suite (OMS) ile Merhaba Surface Hub çözümü nasıl kullanabileceğiniz açıklanır.</span><span class="sxs-lookup"><span data-stu-id="50335-105">This article describes how you can use hello Surface Hub solution in Log Analytics toomonitor Microsoft Surface Hub devices with hello Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="50335-106">Oturum yanı sıra bunların nasıl kullanıldığını anlamak, Surface hub'larınız hello sağlığını izlemek Analytics yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="50335-106">Log Analytics helps you track hello health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="50335-107">Her Surface Hub Microsoft izleme aracısı yüklü hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="50335-107">Each Surface Hub has hello Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="50335-108">Kendi aracılığıyla hello Aracısı, Surface Hub tooOMS veri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="50335-108">Its through hello agent that you can send data from your Surface Hub tooOMS.</span></span> <span data-ttu-id="50335-109">Günlük dosyaları, Surface hub'ları ve misiniz okuma sonra toohello OMS hizmetine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="50335-109">Log files are read from your Surface Hubs and are then are sent toohello OMS service.</span></span> <span data-ttu-id="50335-110">Sorunları çevrimdışı olan sunucuları hello gibi takvim değil eşitleniyor veya Skype içine oluşturulamıyor toolog hello cihaz hesabı ise, OMS içinde hello Surface Hub panosunda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="50335-110">Issues like servers being offline, hello calendar not syncing, or if hello device account is unable toolog into Skype are shown in OMS in hello Surface Hub dashboard.</span></span> <span data-ttu-id="50335-111">Merhaba panosunda Hello verileri kullanarak, çalışmıyor veya başka sorunlara sahip olduğunu ve potansiyel olarak algılanan hello sorunlarını giderir uygulamak aygıtlar tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50335-111">By using hello data in hello dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for hello detected issues.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="50335-112">Yükleme ve yapılandırma hello çözümü</span><span class="sxs-lookup"><span data-stu-id="50335-112">Installing and configuring hello solution</span></span>
<span data-ttu-id="50335-113">Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="50335-113">Use hello following information tooinstall and configure hello solution.</span></span> <span data-ttu-id="50335-114">Sipariş toomanage, Surface hub'larından hello Microsoft Operations Management Suite (OMS) aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="50335-114">In order toomanage your Surface Hubs from hello Microsoft Operations Management Suite (OMS), you'll need hello following:</span></span>

* <span data-ttu-id="50335-115">Geçerli bir abonelik çok[OMS](http://www.microsoft.com/oms).</span><span class="sxs-lookup"><span data-stu-id="50335-115">A valid subscription too[OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="50335-116">Bir [OMS abonelik](https://azure.microsoft.com/pricing/details/log-analytics/) hello numarası destekleyecek düzeyi aygıtların toomonitor istiyor.</span><span class="sxs-lookup"><span data-stu-id="50335-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support hello number of devices you want toomonitor.</span></span> <span data-ttu-id="50335-117">OMS fiyatlandırma kaç aygıtlar kaydedilir ve ne kadar veri bağlı olarak bu işlemlerin değişir.</span><span class="sxs-lookup"><span data-stu-id="50335-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="50335-118">Tootake bu dikkate, Surface Hub dağıtımı planlarken isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="50335-118">You'll want tootake this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="50335-119">Ardından, bir OMS abonelik tooyour mevcut Microsoft Azure aboneliği ekleme ya da hello OMS Portalı aracılığıyla doğrudan yeni bir çalışma alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="50335-119">Next, you will either add an OMS subscription tooyour existing Microsoft Azure subscription or create a new workspace directly through hello OMS portal.</span></span> <span data-ttu-id="50335-120">Her iki yöntemi kullanarak altındadır için ayrıntılı yönergeler [günlük Analytics ile çalışmaya başlama](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="50335-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="50335-121">Merhaba OMS abonelik ayarlandıktan sonra Surface Hub cihazları iki yolu tooenroll vardır:</span><span class="sxs-lookup"><span data-stu-id="50335-121">Once hello OMS subscription is set up, there are two ways tooenroll your Surface Hub devices:</span></span>

* <span data-ttu-id="50335-122">Otomatik olarak Intune aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="50335-122">Automatically through Intune</span></span>
* <span data-ttu-id="50335-123">El ile **ayarları** , Surface Hub Cihazınızda.</span><span class="sxs-lookup"><span data-stu-id="50335-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="50335-124">İlkenin trafiği çevrimdışı durumdaki barındırılan hizmetlere</span><span class="sxs-lookup"><span data-stu-id="50335-124">Set up monitoring</span></span>
<span data-ttu-id="50335-125">Merhaba durumu ve etkinliği, Surface Hub içinde OMS günlük analizi kullanarak izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50335-125">You can monitor hello health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="50335-126">Merhaba OMS Surface Hub Intune kullanarak veya kullanarak yerel olarak kaydedebilir **ayarları** hello Surface Hub üzerinde.</span><span class="sxs-lookup"><span data-stu-id="50335-126">You can enroll hello Surface Hub in OMS by using Intune, or locally by using **Settings** on hello Surface Hub.</span></span>

## <a name="connect-surface-hubs-toooms-through-intune"></a><span data-ttu-id="50335-127">Surface Hubs tooOMS Intune aracılığıyla bağlanma</span><span class="sxs-lookup"><span data-stu-id="50335-127">Connect Surface Hubs tooOMS through Intune</span></span>
<span data-ttu-id="50335-128">Çalışma alanı kimliği ve çalışma alanı anahtarınız, Surface hub'larınız yönetecek hello OMS çalışma alanı için hello.</span><span class="sxs-lookup"><span data-stu-id="50335-128">You'll need hello workspace ID and workspace key for hello OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="50335-129">Bu hello OMS Portalı'ndan elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50335-129">You can get those from hello OMS portal.</span></span>

<span data-ttu-id="50335-130">Intune toocentrally sağlayan bir Microsoft ürünü uygulanan tooone veya daha fazla aygıtlarınızı hello OMS yapılandırma ayarlarını yönetmek olan.</span><span class="sxs-lookup"><span data-stu-id="50335-130">Intune is a Microsoft product that allows you toocentrally manage hello OMS configuration settings that are applied tooone or more of your devices.</span></span> <span data-ttu-id="50335-131">Bu adımları tooconfigure cihazlarınızı Intune aracılığıyla izleyin:</span><span class="sxs-lookup"><span data-stu-id="50335-131">Follow these steps tooconfigure your devices through Intune:</span></span>

1. <span data-ttu-id="50335-132">TooIntune oturum açın.</span><span class="sxs-lookup"><span data-stu-id="50335-132">Sign in tooIntune.</span></span>
2. <span data-ttu-id="50335-133">Çok gidin**ayarları** > **bağlı kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="50335-133">Navigate too**Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="50335-134">Oluşturabilir veya hello Surface Hub şablona dayalı bir ilke düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50335-134">Create or edit a policy based on hello Surface Hub template.</span></span>
4. <span data-ttu-id="50335-135">Hello İlkesi toohello OMS (Azure operasyonel Öngörüler) bölümüne gidin ve hello eklemek *çalışma alanı kimliği* ve *çalışma alanı anahtarı* toohello ilkesi.</span><span class="sxs-lookup"><span data-stu-id="50335-135">Navigate toohello OMS (Azure Operational Insights) section of hello policy, and add hello *Workspace ID* and *Workspace Key* toohello policy.</span></span>
5. <span data-ttu-id="50335-136">Hello İlkesi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="50335-136">Save hello policy.</span></span>
6. <span data-ttu-id="50335-137">Hello İlkesi hello uygun aygıtları grubuyla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="50335-137">Associate hello policy with hello appropriate group of devices.</span></span>

   ![Intune İlkesi](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="50335-139">Intune hello OMS ayarları hello hedef grubu, OMS çalışma alanınızda kaydetme hello aygıtlarla sonra eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="50335-139">Intune then syncs hello OMS settings with hello devices in hello target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a><span data-ttu-id="50335-140">Surface Hubs tooOMS Hello ayarları uygulamasını kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="50335-140">Connect Surface Hubs tooOMS using hello Settings app</span></span>
<span data-ttu-id="50335-141">Çalışma alanı kimliği ve çalışma alanı anahtarınız, Surface hub'larınız yönetecek hello OMS çalışma alanı için hello.</span><span class="sxs-lookup"><span data-stu-id="50335-141">You'll need hello workspace ID and workspace key for hello OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="50335-142">Bu hello OMS Portalı'ndan elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50335-142">You can get those from hello OMS portal.</span></span>

<span data-ttu-id="50335-143">Ortamınızı Intune toomanage kullanmıyorsanız, cihazları el ile kaydedebilirsiniz **ayarları** her Surface Hub üzerinde:</span><span class="sxs-lookup"><span data-stu-id="50335-143">If you don't use Intune toomanage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="50335-144">Surface Hub'açmak **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="50335-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="50335-145">İstendiğinde hello aygıt yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="50335-145">Enter hello device admin credentials when prompted.</span></span>
3. <span data-ttu-id="50335-146">Tıklatın **bu aygıt**ve altında hello **izleme**, tıklatın **OMS ayarlarını yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="50335-146">Click **This device**, and hello under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="50335-147">Seçin **izlemeyi etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="50335-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="50335-148">Merhaba OMS Ayarları iletişim kutusunda, hello yazın **çalışma alanı kimliği** ve türü hello **çalışma alanı anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="50335-148">In hello OMS settings dialog, type hello **Workspace ID** and type hello **Workspace Key**.</span></span>  
   <span data-ttu-id="50335-149">![Ayarlar](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="50335-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="50335-150">Tıklatın **Tamam** toocomplete hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="50335-150">Click **OK** toocomplete hello configuration.</span></span>

<span data-ttu-id="50335-151">Bir onay olsun veya olmasın OMS yapılandırması başarıyla hello toohello aygıt uygulanan söyleyen görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="50335-151">A confirmation appears telling you whether or not hello OMS configuration was successfully applied toohello device.</span></span> <span data-ttu-id="50335-152">İse, bu hello aracı toohello OMS hizmetine başarıyla bağlandı belirten bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="50335-152">If it was, a message appears stating that hello agent successfully connected toohello OMS service.</span></span> <span data-ttu-id="50335-153">Merhaba cihaz ardından burada görüntüleyebilir ve onun üzerinde işlem veri tooOMS göndermeye başlar.</span><span class="sxs-lookup"><span data-stu-id="50335-153">hello device then starts sending data tooOMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="50335-154">Surface Hubs İzleyicisi</span><span class="sxs-lookup"><span data-stu-id="50335-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="50335-155">Surface hub'larınız izleme OMS çok diğer kaydedilen cihazların izleme gibi kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="50335-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="50335-156">İçinde toohello OMS portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="50335-156">Sign in toohello OMS portal.</span></span>
2. <span data-ttu-id="50335-157">Toohello Surface Hub çözüm paketi Panosu gidin.</span><span class="sxs-lookup"><span data-stu-id="50335-157">Navigate toohello Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="50335-158">Cihazınızın sistem durumu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="50335-158">Your device's health is displayed.</span></span>

   ![Yüzey Hub Panosu](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="50335-160">Oluşturabileceğiniz [uyarıları](log-analytics-alerts.md) mevcut veya özel günlük aramaları tabanlı.</span><span class="sxs-lookup"><span data-stu-id="50335-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="50335-161">Surface hub'larından OMS toplar hello veri hello kullanarak, sorunları ve uyarı aygıtlarınız için tanımladığınız hello koşullara için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50335-161">Using hello data hello OMS collects from your Surface Hubs, you can search for issues and alert on hello conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50335-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="50335-162">Next steps</span></span>
* <span data-ttu-id="50335-163">Kullanım [günlük analizi aramaları oturum](log-analytics-log-searches.md) tooview ayrıntılı Surface Hub veri.</span><span class="sxs-lookup"><span data-stu-id="50335-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Surface Hub data.</span></span>
* <span data-ttu-id="50335-164">Oluşturma [uyarıları](log-analytics-alerts.md) toonotify, Surface hub'larıyla sorunları ortaya çıktığında.</span><span class="sxs-lookup"><span data-stu-id="50335-164">Create [alerts](log-analytics-alerts.md) toonotify you when issues occur with your Surface Hubs.</span></span>
