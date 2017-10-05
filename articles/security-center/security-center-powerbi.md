---
title: "Power BI ile Azure Güvenlik Merkezi verilerinden öngörü edinme | Microsoft Docs"
description: "Azure Güvenlik Merkezi Power BI içerik paketi, raporlama işleminiz için oluşturulan veri kümesi tabanlı güvenlik uyarılarının, önerilerin, saldırıya uğrayan kaynakların ve eğilimlerin bulunmasını kolaylaştırır."
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
ms.openlocfilehash: 10f7b8f20cc41a5ebb1b1376e2bf17be02600ae4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a><span data-ttu-id="804b5-103">Power BI ile Azure Güvenlik Merkezi verilerinden öngörü edinme</span><span class="sxs-lookup"><span data-stu-id="804b5-103">Get insights from Azure Security Center data with Power BI</span></span>
<span data-ttu-id="804b5-104">Azure Güvenlik Merkezi için [Power BI Panosu](http://aka.ms/azure-security-center-power-bi), önerileri ve güvenlik uyarılarını her yerden (mobil cihazınız dahil) görselleştirmenizi, çözümlemenizi ve filtrelemenizi etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="804b5-104">The [Power BI Dashboard](http://aka.ms/azure-security-center-power-bi) for Azure Security Center enables you to visualize, analyze, and filter recommendations and security alerts from anywhere, including your mobile device.</span></span> <span data-ttu-id="804b5-105">Power BI panosunu, eğilimleri ve saldırı desenlerini göstermek için kullanma - Kaynağa veya IP adresine göre güvenlik uyarılarını ve kaynak ya da yaşa göre adresi olmayan güvenlik risklerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="804b5-105">Use the Power BI dashboard to reveal trends and attack patterns - view security alerts by resource or source IP address and unaddressed security risks by resource or age.</span></span>

<span data-ttu-id="804b5-106">Ayrıca, Güvenlik Merkezi önerilerini ve güvenlik uyarılarını, örneğin [Azure Denetim Günlükleri](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) ve [Azure SQL Veritabanı Denetimi](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/)’nden alınan verileri kullanarak, ilginç bir şekilde diğer verilerle birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="804b5-106">You can also mash up Security Center recommendations and security alerts with other data in interesting ways, for example using data from [Azure Audit Logs](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) and [Azure SQL Database Auditing](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/).</span></span> <span data-ttu-id="804b5-107">Her ikisi de Power BI Panoları sunar ve bulut kaynaklarınızın güvenlik durumuna ilişkin kolay raporlama için bu verileri Excel’e de aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="804b5-107">Both offer Power BI Dashboards, and you can also export this data to Excel for easy reporting on the security state of your cloud resources.</span></span>

## <a name="using-azure-security-center-dashboard-to-access-power-bi"></a><span data-ttu-id="804b5-108">Power BI hizmetine erişmek için Azure Güvenlik Merkezi panosunu kullanma</span><span class="sxs-lookup"><span data-stu-id="804b5-108">Using Azure Security Center dashboard to access Power BI</span></span>
<span data-ttu-id="804b5-109">Ayrıca, Power BI raporlarına erişmek için Azure Güvenlik Merkezi panosunu da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="804b5-109">You can also use the Azure Security Center dashboard to access Power BI reports.</span></span> <span data-ttu-id="804b5-110">Bu görevi gerçekleştirmek için adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="804b5-110">Follow the steps to perform this task:</span></span>

1. <span data-ttu-id="804b5-111">**Azure Güvenlik Merkezi** panosunda **Power BI** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="804b5-111">In the **Azure Security Center** dashboard, click **Power BI** button.</span></span>

    ![Power BI'ı kullanarak Azure Güvenlik Merkezi'ne bağlanma](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. <span data-ttu-id="804b5-113">Aşağıdaki ekranda gösterildiği gibi, sağ tarafta **Power BI** dikey penceresi açılır:</span><span class="sxs-lookup"><span data-stu-id="804b5-113">The **Power BI** blade opens on the right side as shown in the following screen:</span></span>

    ![Power BI'ı kullanarak Azure Güvenlik Merkezi'ne bağlanma](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. <span data-ttu-id="804b5-115">Power BI panosunu ilk kez oluşturuyorsanız **Power BI'da Araştır** dikey penceresinde aşağıdaki seçeneklerden birini belirleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="804b5-115">If you are creating the Power BI dashboard for the first time, you can choose one of the following options in the **Explore in Power BI** blade:</span></span>

   * <span data-ttu-id="804b5-116">**Güvenlik öngörüleri panosu**: Güvenlik durumunu, tehditleri ve algılamaları içeren bir pano oluşturmak istiyorsanız bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="804b5-116">**Security insights dashboard**: choose this option if you want to create a dashboard that includes security status, threads, and detections.</span></span> <span data-ttu-id="804b5-117">Bu seçenek, aboneliklerde algılanan uyarıları ve koruma durumlarını çözümlemekle sorumlu olan DevOps rolü için daha yaygın kullanılan bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="804b5-117">This option is a more common for DevOps role that is responsible for analyzing their protection status and detected alerts across subscriptions.</span></span>
   * <span data-ttu-id="804b5-118">**İlke yönetimi panosu**: Yönetim ve zorlama ilkesini araştırmak istiyorsanız bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="804b5-118">**Policy management dashboard**: choose this option if you want to explore management and enforcement policy.</span></span>  <span data-ttu-id="804b5-119">Bu seçenek, daha çok idare üzerine odaklanan Merkezi BT için yaygın kullanılan bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="804b5-119">This option is a more common for Central IT who are more focused on governance.</span></span> <span data-ttu-id="804b5-120">Bu panoyu, kuruluşlarındaki güvenlik ilkesi uygunluğuna ilişkin görünürlük ve öngörü kazanmak için kullanabilirler.</span><span class="sxs-lookup"><span data-stu-id="804b5-120">They can use this dashboard to gain visibility and insights on security policy adherence across their organization.</span></span>
   * <span data-ttu-id="804b5-121">Zaten Power BI panonuz varsa **Geçerli Power BI panosuna git**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="804b5-121">If you already have a Power BI dashboard, click **Go to your current Power BI dashboard**.</span></span>
4. <span data-ttu-id="804b5-122">Bu örnek için **Güvenlik öngörüleri panosu** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="804b5-122">For this example, click **Security insights dashboard** option.</span></span> <span data-ttu-id="804b5-123">Güvenlik Merkezi için ilk kez bir Power BI panosu oluşturuyorsanız içerik paketini yüklemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="804b5-123">If this is the first time, you are creating a Power BI dashboard for Security Center you are prompted to install the content pack.</span></span> <span data-ttu-id="804b5-124">Aşağıdaki ekranda gösterildiği gibi **Power BI içerik paketleri** penceresindeki **Al** düğmesine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="804b5-124">Click **Get** button in the **Content packs for Power BI** window as shown in the following screen:</span></span>

    ![Azure Güvenlik Merkezi Güvenlik Öngörüleri panosu](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. <span data-ttu-id="804b5-126">**Azure Güvenlik Merkezi Güvenlik Öngörüleri** penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="804b5-126">The **Connect to Azure Security Center Security Insights** window appear.</span></span> <span data-ttu-id="804b5-127">**Kimlik Doğrulama** yönteminin aşağıda gösterildiği gibi **oAuth2** olduğundan emin olun ve **Oturum Aç** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="804b5-127">Make sure the **Authentication** method is **oAuth2** as shown below and click **Sign in** button.</span></span>

    ![Kimlik Doğrulaması](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. <span data-ttu-id="804b5-129">Azure kimlik bilgilerinizle yeniden kimlik doğrulaması yapmanız istenebilir.</span><span class="sxs-lookup"><span data-stu-id="804b5-129">You may be asked to authenticate again with your Azure credentials.</span></span> <span data-ttu-id="804b5-130">Kimlik doğrulamasından sonra panonuz oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="804b5-130">After authenticating your dashboard will be created.</span></span> <span data-ttu-id="804b5-131">Pano oluşturulduktan sonra yapısı aşağıdaki ekranda gösterilene benzeyen bir rapor görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="804b5-131">Once the dashboard is created you see a report with the similar structure as shown in the following screen:</span></span>

    ![Power BI Panosu](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> <span data-ttu-id="804b5-133">Rapor için her gün gerçekleşecek bir yenileme işlemi zamanlanır.</span><span class="sxs-lookup"><span data-stu-id="804b5-133">A refresh of the report is scheduled to take place on a daily basis.</span></span> <span data-ttu-id="804b5-134">Bu yenilemede bir arızayla karşılaşmanız durumunda sorun giderme hakkında daha fazla bilgi almak için [Azure Güvenlik Merkezi Power BI’daki Olası Yenileme Sorunları](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/) sayfasını okuyun.</span><span class="sxs-lookup"><span data-stu-id="804b5-134">In case you experience a failure on this refresh, read [Potential Refresh Issues with the Azure Security Center Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), for more information on how to troubleshoot.</span></span>
>
>

<span data-ttu-id="804b5-135">Burada, güvenlik uyarılarının ve önerilerin sayısının yanı sıra Azure Güvenlik Merkezi tarafından izlenen VM, Azure SQL veritabanı ve ağ kaynağı sayısını da görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="804b5-135">Here you can see the number of security alerts and recommendations, as well as the number of VMs, Azure SQL databases, and network resources being monitored by Azure Security Center.</span></span>

<span data-ttu-id="804b5-136">Azure Güvenlik Merkezi'ne bağlantı, sizi Azure portalına yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="804b5-136">A link to Azure Security Center redirects you to the Azure portal.</span></span> <span data-ttu-id="804b5-137">Grafikler; güvenlik önerileri ve uyarılar hakkındaki bilgileri görselleştirmeyi şunlar dahil olmak üzere kolaylaştırır:</span><span class="sxs-lookup"><span data-stu-id="804b5-137">The charts make it easy to visualize information about security recommendations and alerts, including:</span></span>

* <span data-ttu-id="804b5-138">Kaynak Güvenlik Durumu</span><span class="sxs-lookup"><span data-stu-id="804b5-138">Resource Security State</span></span>
* <span data-ttu-id="804b5-139">Bekleyen Öneriler</span><span class="sxs-lookup"><span data-stu-id="804b5-139">Pending Recommendations</span></span>
* <span data-ttu-id="804b5-140">VM Önerileri</span><span class="sxs-lookup"><span data-stu-id="804b5-140">VM Recommendations</span></span>
* <span data-ttu-id="804b5-141">Süreçteki Uyarılar</span><span class="sxs-lookup"><span data-stu-id="804b5-141">Alerts over Time</span></span>
* <span data-ttu-id="804b5-142">Saldırıya Uğrayan Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="804b5-142">Attacked Resources</span></span>
* <span data-ttu-id="804b5-143">Saldırıya Uğrayan IP'ler</span><span class="sxs-lookup"><span data-stu-id="804b5-143">Attacked IPs</span></span>

<span data-ttu-id="804b5-144">Her grafiğin arkasında ek öngörüler vardır.</span><span class="sxs-lookup"><span data-stu-id="804b5-144">Behind each chart, there are additional insights.</span></span> <span data-ttu-id="804b5-145">Daha fazla bilgi için bir kutucuk seçin.</span><span class="sxs-lookup"><span data-stu-id="804b5-145">Select a tile to see more information.</span></span> <span data-ttu-id="804b5-146">Örneğin, **Kaynak Güvenlik Durumu** kutucuğu, aşağıdaki ekranda gösterildiği gibi kaynaklara göre bekleyen öneriler hakkında ek ayrıntılar gösterir:</span><span class="sxs-lookup"><span data-stu-id="804b5-146">For example, the **Resource Security State** tile shows you additional details about pending recommendations by resources as shown in the following screen:</span></span>

![Öneriler](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

<span data-ttu-id="804b5-148">Bu grafikteki herhangi bir satıra tıklarsanız diğer satırlar gri renge dönüşür ve yalnızca seçtiğiniz satıra odaklanırsınız.</span><span class="sxs-lookup"><span data-stu-id="804b5-148">If you click on any line of this graph, the others are going to gray out and you focus only on the one you selected.</span></span> <span data-ttu-id="804b5-149">Panoya dönmek için bu sayfanın sol bölmesindeki **Panolar** seçeneğinin altındaki **Azure Güvenlik Merkezi**'ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="804b5-149">To return to the dashboard, click **Azure Security Center** under the **Dashboards** option on the left pane of this page.</span></span>

> [!NOTE]
> <span data-ttu-id="804b5-150">İlave alanlar ekleyerek veya var olan görselleri değiştirerek raporlarınızı özelleştirmek istiyorsanız raporu düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="804b5-150">If you’d like to customize your reports by adding additional fields or changing existing visuals, you can edit the report.</span></span> <span data-ttu-id="804b5-151">Daha fazla bilgi için [Power BI'da Görünüm Düzenleme seçeneğindeki bir rapor ile etkileşimde bulunma](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) bölümünü okuyun.</span><span class="sxs-lookup"><span data-stu-id="804b5-151">Read [Interact with a report in Editing View in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) for more information.</span></span>
>
>

<span data-ttu-id="804b5-152">**Süreçteki Uyarı, Saldırıya Uğrayan Kaynaklar** ve **Saldırgan IP'ler** kutucuklarının her biri, üzerine tıkladığınızda benzer bir çıktıya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="804b5-152">The **Alerts over Time, Attacked Resources** and **Attacker IPs** tiles will have the similar output when you click on each one of it.</span></span> <span data-ttu-id="804b5-153">Bu durum, rapor bu üç değişkenin hepsiyle ilgili bilgi topladığı ve aşağıdaki ekranda gösterildiği gibi **Saldırıya Uğrayan Kaynaklar** olarak adlandırdığı için oluşur:</span><span class="sxs-lookup"><span data-stu-id="804b5-153">This happens because the report aggregates information regarding all those three variables and calls it **Resources under Attack** as shown in the following screen:</span></span>

![Saldırıya uğrayan kaynaklar](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

<span data-ttu-id="804b5-155">Bu noktada, bu raporun bir kopyasını kaydedebilirsiniz, yazdırabilirsiniz veya **Dosya** menüsünde kullanılabilir seçenekleri belirterek web'de yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="804b5-155">At this point you can also save a copy of this report, print it or publish it on the web by using the options available in the **File** menu.</span></span>

![Dosya menüsü](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a><span data-ttu-id="804b5-157">Power BI hizmetleri ile Azure Güvenlik Merkezi verilerinizi araştırma</span><span class="sxs-lookup"><span data-stu-id="804b5-157">Exploring your Azure Security Center data with Power BI services</span></span>
<span data-ttu-id="804b5-158">Power BI'da [Power BI İçerik Paketi Hizmetleri](https://msit.powerbi.com/groups/me/getdata/services)'ne bağlanın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="804b5-158">Connect to the [Power BI Content Pack Services](https://msit.powerbi.com/groups/me/getdata/services) in Power BI and execute the following steps:</span></span>

1. <span data-ttu-id="804b5-159">**Power BI için İçerik Paketi** penceresinde, aşağıda gösterildiği gibi iki seçenek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="804b5-159">In the **Content Pack for Power BI** window you will see two options as shown below.</span></span>

    ![Power BI için içerik paketi](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > <span data-ttu-id="804b5-161">Bu makalenin ilk bölümünü zaten uyguladıysanız yalnızca Azure Güvenlik Merkezi İlke Yönetimi seçeneğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="804b5-161">If already executed the first part of this article you will see only one option, which is Azure Security Center Policy Management.</span></span>
   >
   >
2. <span data-ttu-id="804b5-162">Bu örneğin amacı doğrultusunda **Azure Güvenlik Merkezi İlke Yönetimi** kutucuğundaki **Al** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="804b5-162">For the purpose of this example, click **Get** in the **Azure Security Center Policy Management** tile.</span></span>
3. <span data-ttu-id="804b5-163">**Azure Güvenlik Merkezi İlke Yönetimi'ne Bağlanma** penceresinde, aşağıda gösterildiği gibi **Kimlik Doğrulama Yöntemi** açılan menüsünün altında **oAuth2** seçeneğini belirttiğinizden emin olun ve **Oturum Aç** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="804b5-163">In the **Connect to Azure Security Center Policy Management** window, make sure to select **oAuth2** under **Authentication Method** drop down as shown below and click **Sign in** button.</span></span>

    ![İlke Yönetimi penceresi](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. <span data-ttu-id="804b5-165">Azure Güvenlik Merkezi'ne bağlanmak için kullandığınız kimlik bilgilerini yazmanız gereken kimlik doğrulama sayfasına yönlendirileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="804b5-165">You will be redirected to an authentication page where you should type the credentials that you are using to connect to Azure Security Center.</span></span> <span data-ttu-id="804b5-166">Kimlik doğrulama işlemi tamamlandıktan sonra Power BI, raporlarınızı oluşturmak için verileri içeri aktarmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="804b5-166">After the authentication process is complete, Power BI will start importing data to build your reports.</span></span> <span data-ttu-id="804b5-167">Bu süre boyunca tarayıcınızın sağ üst köşesinde şu iletiyi görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="804b5-167">During this time you may see the following message on the right corner of your browser:</span></span>

    ![Power BI'ı kullanarak Azure Güvenlik Merkezi'ne bağlanma](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > <span data-ttu-id="804b5-169">Özellikle birden fazla aboneliğine sahip olduğunuz senaryolar için panoyu ilk kez oluşturmak normalden daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="804b5-169">when the dashboard is being created for the first time it can take longer than usual, mainly for scenarios where you have multiple subscriptions.</span></span>
   >
   >
5. <span data-ttu-id="804b5-170">İşlem tamamlandıktan sonra Azure Güvenlik Merkezi Power BI panonuz aşağıdakine benzer **İlke Yönetimi** raporuyla birlikte yüklenir:</span><span class="sxs-lookup"><span data-stu-id="804b5-170">Once the process is finished, your Azure Security Center Power BI dashboard will load with the **Policy Management** report similar to the one shown below:</span></span>

    ![İlke Yönetimi panosu](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a><span data-ttu-id="804b5-172">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="804b5-172">See also</span></span>
<span data-ttu-id="804b5-173">Bu belgede, Azure Güvenlik Merkezi'nde Power BI hizmetini nasıl kullanacağınız hakkında bilgi edindiniz.</span><span class="sxs-lookup"><span data-stu-id="804b5-173">In this document, you learned how to use Power BI in Azure Security Center.</span></span> <span data-ttu-id="804b5-174">Azure Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="804b5-174">To learn more about Azure Security Center, see the following:</span></span>

* <span data-ttu-id="804b5-175">[Azure Güvenlik Merkezi Planlama ve İşlemler Kılavuzu](security-center-planning-and-operations-guide.md) - Azure Güvenlik Merkezi'ni benimsemeyi planlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="804b5-175">[Azure Security Center Planning and Operations Guide](security-center-planning-and-operations-guide.md) — Learn how to plan Azure Security Center adoption.</span></span>
* <span data-ttu-id="804b5-176">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) - Azure Güvenlik Merkezi'nde güvenlik ayarlarını yapılandırma hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="804b5-176">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security settings in Azure Security Center</span></span>
* <span data-ttu-id="804b5-177">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) - Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="804b5-177">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts</span></span>
* <span data-ttu-id="804b5-178">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) - Hizmet kullanımı ile ilgili sık sorulan soruları burada bulabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="804b5-178">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service</span></span>
* <span data-ttu-id="804b5-179">[Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="804b5-179">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance</span></span>
