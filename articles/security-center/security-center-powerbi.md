---
title: "Power BI ile Azure Güvenlik Merkezi verilerinden aaaGet ınsights | Microsoft Docs"
description: "Hello Azure Güvenlik Merkezi Power BI içerik paketi kolay toofind güvenlik uyarılarının, önerilerin kolaylaştırır, kaynakların saldırıya ve eğilimlerin, raporlama için oluşturulmuş bir veri kümesini temel."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: af68aef626034fe03d793c36b515a3f26619e5f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a><span data-ttu-id="1a162-103">Power BI ile Azure Güvenlik Merkezi verilerinden öngörü edinme</span><span class="sxs-lookup"><span data-stu-id="1a162-103">Get insights from Azure Security Center data with Power BI</span></span>
<span data-ttu-id="1a162-104">Merhaba [Power BI panosuna](http://aka.ms/azure-security-center-power-bi) toovisualize sağlayan Azure Güvenlik Merkezi için çözümleme ve öneriler ve güvenlik uyarılarını her yerden, mobil cihazınız dahil filtre.</span><span class="sxs-lookup"><span data-stu-id="1a162-104">hello [Power BI Dashboard](http://aka.ms/azure-security-center-power-bi) for Azure Security Center enables you toovisualize, analyze, and filter recommendations and security alerts from anywhere, including your mobile device.</span></span> <span data-ttu-id="1a162-105">Desenler - kaynak veya kaynak IP adresine göre güvenlik uyarılarını ve kaynak ya da yaşa göre olmayan güvenlik risklerini saldırılara ve Hello Power BI Panosu tooreveal eğilimleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1a162-105">Use hello Power BI dashboard tooreveal trends and attack patterns - view security alerts by resource or source IP address and unaddressed security risks by resource or age.</span></span>

<span data-ttu-id="1a162-106">Ayrıca, Güvenlik Merkezi önerilerini ve güvenlik uyarılarını, örneğin [Azure Denetim Günlükleri](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) ve [Azure SQL Veritabanı Denetimi](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/)’nden alınan verileri kullanarak, ilginç bir şekilde diğer verilerle birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a162-106">You can also mash up Security Center recommendations and security alerts with other data in interesting ways, for example using data from [Azure Audit Logs](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) and [Azure SQL Database Auditing](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/).</span></span> <span data-ttu-id="1a162-107">Her ikisi de Power BI panolarını sunan ve kolay bulut kaynaklarınızın güvenlik durumuna hello raporlama için bu veri tooExcel dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a162-107">Both offer Power BI Dashboards, and you can also export this data tooExcel for easy reporting on hello security state of your cloud resources.</span></span>

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a><span data-ttu-id="1a162-108">Azure Güvenlik Merkezi Panosu tooaccess Power BI kullanma</span><span class="sxs-lookup"><span data-stu-id="1a162-108">Using Azure Security Center dashboard tooaccess Power BI</span></span>
<span data-ttu-id="1a162-109">Hello Azure Güvenlik Merkezi Panosu tooaccess Power BI raporları de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a162-109">You can also use hello Azure Security Center dashboard tooaccess Power BI reports.</span></span> <span data-ttu-id="1a162-110">Bu görev Hello adımları tooperform izleyin:</span><span class="sxs-lookup"><span data-stu-id="1a162-110">Follow hello steps tooperform this task:</span></span>

1. <span data-ttu-id="1a162-111">Merhaba, **Azure Güvenlik Merkezi** panoyu tıklatın **Power BI** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1a162-111">In hello **Azure Security Center** dashboard, click **Power BI** button.</span></span>

    ![TooAzure Güvenlik Merkezi Power BI kullanarak bağlan](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. <span data-ttu-id="1a162-113">Merhaba **Power BI** hello ekran aşağıdaki gösterildiği gibi hello sağ tarafta bir dikey pencere açılır:</span><span class="sxs-lookup"><span data-stu-id="1a162-113">hello **Power BI** blade opens on hello right side as shown in hello following screen:</span></span>

    ![TooAzure Güvenlik Merkezi Power BI kullanarak bağlan](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. <span data-ttu-id="1a162-115">Merhaba hello Power BI panosunu ilk kez oluşturuyorsanız, hello aşağıdaki seçenekleri hello seçebilirsiniz **Power bı'da araştırma** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="1a162-115">If you are creating hello Power BI dashboard for hello first time, you can choose one of hello following options in hello **Explore in Power BI** blade:</span></span>

   * <span data-ttu-id="1a162-116">**Güvenlik öngörüleri Panosu**: toocreate güvenlik durumunu, tehditleri ve algılamaları içeren bir Pano istiyorsanız bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="1a162-116">**Security insights dashboard**: choose this option if you want toocreate a dashboard that includes security status, threads, and detections.</span></span> <span data-ttu-id="1a162-117">Bu seçenek, aboneliklerde algılanan uyarıları ve koruma durumlarını çözümlemekle sorumlu olan DevOps rolü için daha yaygın kullanılan bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="1a162-117">This option is a more common for DevOps role that is responsible for analyzing their protection status and detected alerts across subscriptions.</span></span>
   * <span data-ttu-id="1a162-118">**İlke yönetimi Panosu**: tooexplore yönetim ve zorlama ilkesini istiyorsanız bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="1a162-118">**Policy management dashboard**: choose this option if you want tooexplore management and enforcement policy.</span></span>  <span data-ttu-id="1a162-119">Bu seçenek, daha çok idare üzerine odaklanan Merkezi BT için yaygın kullanılan bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="1a162-119">This option is a more common for Central IT who are more focused on governance.</span></span> <span data-ttu-id="1a162-120">Bunlar bu Pano toogain görünürlük ve öngörü güvenlik ilkesi uygunluğuna kuruluşlarındaki kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a162-120">They can use this dashboard toogain visibility and insights on security policy adherence across their organization.</span></span>
   * <span data-ttu-id="1a162-121">Power BI Panosu zaten varsa, tıklatın **Git tooyour geçerli Power BI panosuna**.</span><span class="sxs-lookup"><span data-stu-id="1a162-121">If you already have a Power BI dashboard, click **Go tooyour current Power BI dashboard**.</span></span>
4. <span data-ttu-id="1a162-122">Bu örnek için **Güvenlik öngörüleri panosu** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1a162-122">For this example, click **Security insights dashboard** option.</span></span> <span data-ttu-id="1a162-123">Bu hello ilk kez kullanıyorsanız, Güvenlik Merkezi olduğunuz tooinstall hello içerik paketi istenir için Power BI panosuna oluşturuyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="1a162-123">If this is hello first time, you are creating a Power BI dashboard for Security Center you are prompted tooinstall hello content pack.</span></span> <span data-ttu-id="1a162-124">Tıklatın **almak** hello düğmesini **için Power BI içerik paketleri** hello ekran aşağıdaki gösterildiği gibi penceresi:</span><span class="sxs-lookup"><span data-stu-id="1a162-124">Click **Get** button in hello **Content packs for Power BI** window as shown in hello following screen:</span></span>

    ![Azure Güvenlik Merkezi Güvenlik Öngörüleri panosu](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. <span data-ttu-id="1a162-126">Merhaba **tooAzure Güvenlik Merkezi güvenlik öngörüleri bağlanmak** penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="1a162-126">hello **Connect tooAzure Security Center Security Insights** window appear.</span></span> <span data-ttu-id="1a162-127">Merhaba emin olun **kimlik doğrulaması** yöntemi **oAuth2** aşağıda gösterildiği gibi tıklatıp **oturum** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1a162-127">Make sure hello **Authentication** method is **oAuth2** as shown below and click **Sign in** button.</span></span>

    ![Kimlik Doğrulaması](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. <span data-ttu-id="1a162-129">Tooauthenticate yeniden Azure kimlik bilgilerinizle istenebilir.</span><span class="sxs-lookup"><span data-stu-id="1a162-129">You may be asked tooauthenticate again with your Azure credentials.</span></span> <span data-ttu-id="1a162-130">Kimlik doğrulamasından sonra panonuz oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1a162-130">After authenticating your dashboard will be created.</span></span> <span data-ttu-id="1a162-131">Merhaba Pano oluşturulduktan sonra hello ekran aşağıdaki gösterildiği gibi hello benzer yapıya sahip bir rapor bakın:</span><span class="sxs-lookup"><span data-stu-id="1a162-131">Once hello dashboard is created you see a report with hello similar structure as shown in hello following screen:</span></span>

    ![Power BI Panosu](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> <span data-ttu-id="1a162-133">Merhaba rapor yenileme, günlük olarak zamanlanan tootake yerdir.</span><span class="sxs-lookup"><span data-stu-id="1a162-133">A refresh of hello report is scheduled tootake place on a daily basis.</span></span> <span data-ttu-id="1a162-134">Bu yenilemede bir hatasıyla karşılaşan durumda okuma [hello Azure Güvenlik Merkezi Power BI ile olası yenileme sorunları](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), hakkında daha fazla bilgi için tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="1a162-134">In case you experience a failure on this refresh, read [Potential Refresh Issues with hello Azure Security Center Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), for more information on how tootroubleshoot.</span></span>
>
>

<span data-ttu-id="1a162-135">Burada VM'ler, Azure SQL veritabanı ve Azure Güvenlik Merkezi tarafından izlenen ağ kaynaklarına hello sayısı yanı sıra güvenlik uyarısı ve öneri hello sayısını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a162-135">Here you can see hello number of security alerts and recommendations, as well as hello number of VMs, Azure SQL databases, and network resources being monitored by Azure Security Center.</span></span>

<span data-ttu-id="1a162-136">Bağlantı tooAzure Güvenlik Merkezi, Azure portal toohello yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="1a162-136">A link tooAzure Security Center redirects you toohello Azure portal.</span></span> <span data-ttu-id="1a162-137">Merhaba grafikleri kolay toovisualize bilgilerini güvenlik önerileri ve uyarılar, dahil olmak üzere kolaylaştırır:</span><span class="sxs-lookup"><span data-stu-id="1a162-137">hello charts make it easy toovisualize information about security recommendations and alerts, including:</span></span>

* <span data-ttu-id="1a162-138">Kaynak Güvenlik Durumu</span><span class="sxs-lookup"><span data-stu-id="1a162-138">Resource Security State</span></span>
* <span data-ttu-id="1a162-139">Bekleyen Öneriler</span><span class="sxs-lookup"><span data-stu-id="1a162-139">Pending Recommendations</span></span>
* <span data-ttu-id="1a162-140">VM Önerileri</span><span class="sxs-lookup"><span data-stu-id="1a162-140">VM Recommendations</span></span>
* <span data-ttu-id="1a162-141">Süreçteki Uyarılar</span><span class="sxs-lookup"><span data-stu-id="1a162-141">Alerts over Time</span></span>
* <span data-ttu-id="1a162-142">Saldırıya Uğrayan Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="1a162-142">Attacked Resources</span></span>
* <span data-ttu-id="1a162-143">Saldırıya Uğrayan IP'ler</span><span class="sxs-lookup"><span data-stu-id="1a162-143">Attacked IPs</span></span>

<span data-ttu-id="1a162-144">Her grafiğin arkasında ek öngörüler vardır.</span><span class="sxs-lookup"><span data-stu-id="1a162-144">Behind each chart, there are additional insights.</span></span> <span data-ttu-id="1a162-145">Döşeme toosee daha fazla bilgi seçin.</span><span class="sxs-lookup"><span data-stu-id="1a162-145">Select a tile toosee more information.</span></span> <span data-ttu-id="1a162-146">Örneğin, hello **kaynak güvenlik durumu** kutucuğunda gösterilir ek ayrıntılar hakkında öneriler kaynaklar tarafından hello ekran aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="1a162-146">For example, hello **Resource Security State** tile shows you additional details about pending recommendations by resources as shown in hello following screen:</span></span>

![Öneriler](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

<span data-ttu-id="1a162-148">Bu grafikteki herhangi bir satıra tıklarsanız, hello başkalarının toogray çıkışı ve odaklanmanıza yalnızca bir seçtiğiniz hello üzerinde adımıdır.</span><span class="sxs-lookup"><span data-stu-id="1a162-148">If you click on any line of this graph, hello others are going toogray out and you focus only on hello one you selected.</span></span> <span data-ttu-id="1a162-149">tooreturn toohello Pano tıklatın **Azure Güvenlik Merkezi** hello altında **panolar** bu sayfanın hello sol bölmedeki seçeneği.</span><span class="sxs-lookup"><span data-stu-id="1a162-149">tooreturn toohello dashboard, click **Azure Security Center** under hello **Dashboards** option on hello left pane of this page.</span></span>

> [!NOTE]
> <span data-ttu-id="1a162-150">Toocustomize isterseniz, raporlarınızı ilave alanlar ekleyerek veya var olan görselleri değiştirerek hello raporu düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a162-150">If you’d like toocustomize your reports by adding additional fields or changing existing visuals, you can edit hello report.</span></span> <span data-ttu-id="1a162-151">Daha fazla bilgi için [Power BI'da Görünüm Düzenleme seçeneğindeki bir rapor ile etkileşimde bulunma](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) bölümünü okuyun.</span><span class="sxs-lookup"><span data-stu-id="1a162-151">Read [Interact with a report in Editing View in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) for more information.</span></span>
>
>

<span data-ttu-id="1a162-152">Merhaba **süreçteki uyarı, Saldırıya uğrayan kaynaklar** ve **saldırgan IP'ler** döşeme her biri, üzerine tıkladığınızda hello benzer bir çıktıya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1a162-152">hello **Alerts over Time, Attacked Resources** and **Attacker IPs** tiles will have hello similar output when you click on each one of it.</span></span> <span data-ttu-id="1a162-153">Merhaba rapor bu üç değişkenin ilgili bilgileri toplar ve çağırır Bunun nedeni **Saldırıya uğrayan kaynaklar** hello ekran aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="1a162-153">This happens because hello report aggregates information regarding all those three variables and calls it **Resources under Attack** as shown in hello following screen:</span></span>

![Saldırıya uğrayan kaynaklar](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

<span data-ttu-id="1a162-155">Bu noktada Ayrıca bu raporun bir kopyasını kaydetmek, yazdırmak veya hello hello seçenekleri kullanarak hello Web'de Yayımlama **dosya** menüsü.</span><span class="sxs-lookup"><span data-stu-id="1a162-155">At this point you can also save a copy of this report, print it or publish it on hello web by using hello options available in hello **File** menu.</span></span>

![Dosya menüsü](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a><span data-ttu-id="1a162-157">Power BI hizmetleri ile Azure Güvenlik Merkezi verilerinizi araştırma</span><span class="sxs-lookup"><span data-stu-id="1a162-157">Exploring your Azure Security Center data with Power BI services</span></span>
<span data-ttu-id="1a162-158">Toohello bağlanmak [Power BI içerik paketi Hizmetleri](https://msit.powerbi.com/groups/me/getdata/services) Power bı'da ve aşağıdaki adımları hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="1a162-158">Connect toohello [Power BI Content Pack Services](https://msit.powerbi.com/groups/me/getdata/services) in Power BI and execute hello following steps:</span></span>

1. <span data-ttu-id="1a162-159">Merhaba, **Power BI için içerik paketi** penceresi aşağıda gösterildiği gibi iki seçenek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1a162-159">In hello **Content Pack for Power BI** window you will see two options as shown below.</span></span>

    ![Power BI için içerik paketi](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > <span data-ttu-id="1a162-161">Zaten bu makalenin ilk bölümü hello yürütülürse Azure Güvenlik Merkezi ilke yönetimi, yalnızca bir seçeneğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1a162-161">If already executed hello first part of this article you will see only one option, which is Azure Security Center Policy Management.</span></span>
   >
   >
2. <span data-ttu-id="1a162-162">Bu örnek Hello amaçla tıklatın **almak** hello içinde **Azure Güvenlik Merkezi ilke yönetimi** döşeme.</span><span class="sxs-lookup"><span data-stu-id="1a162-162">For hello purpose of this example, click **Get** in hello **Azure Security Center Policy Management** tile.</span></span>
3. <span data-ttu-id="1a162-163">Merhaba, **tooAzure Güvenlik Merkezi ilke yönetimi bağlanmak** penceresinde, yapma emin tooselect **oAuth2** altında **kimlik doğrulama yöntemini** aşağıda gösterildiği gibi aşağı bırakın ve'ı tıklatın **Oturum** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1a162-163">In hello **Connect tooAzure Security Center Policy Management** window, make sure tooselect **oAuth2** under **Authentication Method** drop down as shown below and click **Sign in** button.</span></span>

    ![İlke Yönetimi penceresi](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. <span data-ttu-id="1a162-165">Burada, tooconnect tooAzure Güvenlik Merkezi'ni kullanma hello kimlik bilgilerini yazmanız gereken yeniden yönlendirilen tooan kimlik doğrulaması sayfası olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1a162-165">You will be redirected tooan authentication page where you should type hello credentials that you are using tooconnect tooAzure Security Center.</span></span> <span data-ttu-id="1a162-166">Merhaba kimlik doğrulama işlemi tamamlandıktan sonra Power BI veri toobuild içeri aktarmaya raporlarınızı başlar.</span><span class="sxs-lookup"><span data-stu-id="1a162-166">After hello authentication process is complete, Power BI will start importing data toobuild your reports.</span></span> <span data-ttu-id="1a162-167">Bu süre boyunca hello sağ köşesindeki tarayıcınız üzerinde iletiden hello görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1a162-167">During this time you may see hello following message on hello right corner of your browser:</span></span>

    ![TooAzure Güvenlik Merkezi Power BI kullanarak bağlan](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > <span data-ttu-id="1a162-169">ilk kez Merhaba Hello Pano oluşturulduğunda çoğunlukla birden fazla aboneliğine sahip olduğu senaryolar için normalden daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="1a162-169">when hello dashboard is being created for hello first time it can take longer than usual, mainly for scenarios where you have multiple subscriptions.</span></span>
   >
   >
5. <span data-ttu-id="1a162-170">Merhaba işlemi tamamlandıktan sonra Azure Güvenlik Merkezi Power BI panonuz hello ile yükleyecek **İlkesi Yönetimi** benzer toohello aşağıda gösterilene bildirin:</span><span class="sxs-lookup"><span data-stu-id="1a162-170">Once hello process is finished, your Azure Security Center Power BI dashboard will load with hello **Policy Management** report similar toohello one shown below:</span></span>

    ![İlke Yönetimi panosu](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a><span data-ttu-id="1a162-172">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="1a162-172">See also</span></span>
<span data-ttu-id="1a162-173">Bu belgede, nasıl öğrenilen toouse Azure Güvenlik Merkezi'nde Power BI.</span><span class="sxs-lookup"><span data-stu-id="1a162-173">In this document, you learned how toouse Power BI in Azure Security Center.</span></span> <span data-ttu-id="1a162-174">Azure Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="1a162-174">toolearn more about Azure Security Center, see hello following:</span></span>

* <span data-ttu-id="1a162-175">[Azure Güvenlik Merkezi planlama ve işlemler Kılavuzu](security-center-planning-and-operations-guide.md) — öğrenin nasıl tooplan Azure Güvenlik Merkezi'ni benimsemeyi.</span><span class="sxs-lookup"><span data-stu-id="1a162-175">[Azure Security Center Planning and Operations Guide](security-center-planning-and-operations-guide.md) — Learn how tooplan Azure Security Center adoption.</span></span>
* <span data-ttu-id="1a162-176">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) — öğrenin nasıl tooconfigure Azure Güvenlik Merkezi'nde güvenlik ayarları</span><span class="sxs-lookup"><span data-stu-id="1a162-176">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security settings in Azure Security Center</span></span>
* <span data-ttu-id="1a162-177">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) — öğrenin nasıl toomanage ve yanıt toosecurity uyarıları</span><span class="sxs-lookup"><span data-stu-id="1a162-177">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts</span></span>
* <span data-ttu-id="1a162-178">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1a162-178">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service</span></span>
* <span data-ttu-id="1a162-179">[Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1a162-179">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance</span></span>
