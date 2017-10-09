---
title: "Azure Application Insights etkileşimli çalışma kitapları ile aaaInvestigate ve paylaşımı kullanım verilerini | Microsoft docs"
description: "Kullanıcılar, web uygulamanızın demografik analizini."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="fca17-103">Araştırmak ve kullanım verilerini Application Insights etkileşimli çalışma kitaplarında paylaşın</span><span class="sxs-lookup"><span data-stu-id="fca17-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="fca17-104">Çalışma kitapları birleştirmek [Azure Application Insights](app-insights-overview.md) veri görselleştirmeleri [analitik sorguları](app-insights-analytics.md)ve etkileşimli belgeleri metin.</span><span class="sxs-lookup"><span data-stu-id="fca17-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="fca17-105">Çalışma kitapları erişim toohello ile diğer takım üyeleri tarafından düzenlenebilir aynı Azure kaynak.</span><span class="sxs-lookup"><span data-stu-id="fca17-105">Workbooks are editable by other team members with access toohello same Azure resource.</span></span> <span data-ttu-id="fca17-106">Bu hello sorgular ve denetimleri kullanılan toocreate bir çalışma kitabı hello çalışma kitabı okuma kullanılabilir tooother kişiler kolay tooexplore hale gelir, genişletme ve hataları olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="fca17-106">This means hello queries and controls used toocreate a workbook are available tooother people reading hello workbook, making them easy tooexplore, extend, and check for mistakes.</span></span>

<span data-ttu-id="fca17-107">Çalışma kitapları gibi senaryolar için yararlı olur:</span><span class="sxs-lookup"><span data-stu-id="fca17-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="fca17-108">Merhaba ölçümleri ilgi önceden tanımadığınız olduğunda, uygulamanızın hello kullanım keşfetme: kullanıcılar, saklama hızları, dönüştürme oranları vb. sayısı. Application ınsights'ta diğer kullanım analiz araçları çalışma kitapları, Görselleştirme ve çözümlemeleri de serbest biçimli araştırması bu tür için harika yapmadan birden çok türde birleştirmek olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="fca17-108">Exploring hello usage of your app when you don't know hello metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="fca17-109">Yeni yayımlanmış bir özelliğin nasıl gerçekleştirmekte tooyour takım açıklayan, kullanıcı tarafından gösteren anahtar etkileşimleri ve diğer ölçümleri için sayar.</span><span class="sxs-lookup"><span data-stu-id="fca17-109">Explaining tooyour team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="fca17-110">Merhaba sonuçlarını bir paylaşım / B denemeler ekibinizin diğer üyeleriyle, uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="fca17-110">Sharing hello results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="fca17-111">Hello hello hedeflerini metinle denemeler yapın ve ardından her kullanım ölçümü Göster ve analizi sorgu tooevaluate hello deneme Temizle çağrı-her ölçümü üstüne veya altına-hedefi olup için aşımı ayarlarına birlikte kullanılan açıklayabilir.</span><span class="sxs-lookup"><span data-stu-id="fca17-111">You can explain hello goals for hello experiment with text, then show each usage metric and Analytics query used tooevaluate hello experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="fca17-112">Bir kesinti Hello etkisini hello kullanım verileri, açıklama metnini ve sonraki adımları tooprevent kesilmelerini hello gelecekteki tartışması birleştirerek, uygulamanızın raporlama.</span><span class="sxs-lookup"><span data-stu-id="fca17-112">Reporting hello impact of an outage on hello usage of your app, combining data, text explanation, and a discussion of next steps tooprevent outages in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="fca17-113">Application Insights kaynağınıza, sayfa görünümleri veya özel olaylar toouse çalışma kitaplarını içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fca17-113">Your Application Insights resource must contain page views or custom events toouse workbooks.</span></span> <span data-ttu-id="fca17-114">[Uygulama toocollect sayfasını tooset hello Application Insights JavaScript SDK'sı ile otomatik olarak nasıl görünümleri öğrenin](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="fca17-114">[Learn how tooset up your app toocollect page views automatically with hello Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="fca17-115">Düzenleme, yeniden düzenleme, kopyalama ve çalışma kitabını bölümleri silme</span><span class="sxs-lookup"><span data-stu-id="fca17-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="fca17-116">Bir çalışma kitabı bölümlerini yapılmış bir durumda: bağımsız olarak düzenlenebilir kullanım görselleştirmeleri, grafikler, tablolar, metin veya Analytics sorgu sonuçları.</span><span class="sxs-lookup"><span data-stu-id="fca17-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="fca17-117">bir çalışma kitabı bölümü tooedit Merhaba içeriğine tıklatın hello **Düzenle** düğmeye ve hello çalışma kitabı bölümünün sağ toohello.</span><span class="sxs-lookup"><span data-stu-id="fca17-117">tooedit hello contents of a workbook section, click hello **Edit** button below and toohello right of hello workbook section.</span></span>

![Düzenleme denetimleri uygulama Öngörüler çalışma kitaplarını bölümü](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="fca17-119">Tamamladığınızda, bir bölümü düzenleme'ı tıklatın **yapılan düzenleme** hello sol alt köşesindeki hello bölüm içinde.</span><span class="sxs-lookup"><span data-stu-id="fca17-119">When you're done editing a section, click **Done Editing** in hello bottom left corner of hello section.</span></span>

2. <span data-ttu-id="fca17-120">toocreate yinelenen bir bölümün tıklatın hello **bu bölümü kopyalama** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fca17-120">toocreate a duplicate of a section, click hello **Clone this section** icon.</span></span> <span data-ttu-id="fca17-121">Yinelenen bölümleri oluşturma harika tooway tooiterate önceki yineleme kaybetmeden sorguda bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fca17-121">Creating duplicate sections is a great tooway tooiterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="fca17-122">bir çalışma kitabı bölümünde yukarı toomove tıklatın hello **Yukarı Taşı** veya **Aşağı Taşı** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fca17-122">toomove up a section in a workbook, click hello **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="fca17-123">tooremove bölüm kalıcı olarak hello tıklatın **kaldırmak** simgesi.</span><span class="sxs-lookup"><span data-stu-id="fca17-123">tooremove a section permanently, click hello **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="fca17-124">Kullanım verileri görselleştirme bölümleri ekleme</span><span class="sxs-lookup"><span data-stu-id="fca17-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="fca17-125">Çalışma kitapları yerleşik kullanım analizi görselleştirmeleri dört tür sunar.</span><span class="sxs-lookup"><span data-stu-id="fca17-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="fca17-126">Her bir soru hello kullanımı hakkında uygulamanızın yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="fca17-126">Each answers a common question about hello usage of your app.</span></span> <span data-ttu-id="fca17-127">tooadd tablolar ve grafikler bu dört bölüm dışında Analytics sorgu bölümleri (aşağıda görebilirsiniz) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fca17-127">tooadd tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="fca17-128">tooadd kullanıcılar, oturumlar, olayları veya bekletme bölümünde tooyour çalışma kitabı, kullanım hello **Kullanıcı Ekle** veya diğer karşılık gelen bir düğme hello çalışma kitabının hello altındaki ya da hello altındaki herhangi bir bölümü.</span><span class="sxs-lookup"><span data-stu-id="fca17-128">tooadd a Users, Sessions, Events, or Retention section tooyour workbook, use hello **Add Users** or other corresponding button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

![Kullanıcılar bölümünde çalışma kitapları](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="fca17-130">**Kullanıcıların** bölümleri yanıt "kaç kullanıcının bazı sayfa görüntülenemez veya Sitem bazı özelliği kullanılan?"</span><span class="sxs-lookup"><span data-stu-id="fca17-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="fca17-131">**Oturumları** bölümleri yanıt "kaç oturumları kullanıcılar bazı sayfa görüntüleme veya Sitem bazı özelliğini kullanarak harcamanız?"</span><span class="sxs-lookup"><span data-stu-id="fca17-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="fca17-132">**Olayları** bölümleri yanıt "kaç kez kullanıcılar bazı sayfasını görüntüleyebilir veya Sitem bazı özelliğini kullanın?"</span><span class="sxs-lookup"><span data-stu-id="fca17-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="fca17-133">Bu üç bölüm türleri hello denetimleri ve görselleştirmeleri aynı kümesi sunar:</span><span class="sxs-lookup"><span data-stu-id="fca17-133">Each of these three section types offers hello same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="fca17-134">Kullanıcıları, oturumlar ve olayları bölümleri düzenleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="fca17-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="fca17-135">Geçiş hello ana grafik, çubuk grafik kılavuzları, otomatik Öngörüler ve örnek kullanıcılar görselleştirmeleri hello kullanarak **Göster grafik**, **Göster kılavuz**, **Göster Öngörüler**ve **Bu kullanıcılar örnek** onay kutularını her bölümün hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="fca17-135">Toggle hello main chart, histogram grids, automatic insights, and sample users visualizations using hello **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at hello top of each section.</span></span>

![Çalışma kitapları bekletme bölümünde](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="fca17-137">**Bekletme** bölümleri yanıt "bazı sayfa görüntülenemez veya bir gün veya hafta bazı özellik kullanılan kişiler kaç tane geri bir sonraki gün veya hafta gelen?"</span><span class="sxs-lookup"><span data-stu-id="fca17-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="fca17-138">Bekletme bölümleri düzenleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="fca17-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="fca17-139">Hello kullanarak geçiş hello isteğe bağlı genel saklama grafik **Göster genel saklama grafik** onay kutusunu hello bölümünün hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="fca17-139">Toggle hello optional Overall Retention chart using hello **Show overall retention chart** checkbox at hello top of hello section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="fca17-140">Uygulama Öngörüler Analytics bölümleri ekleme</span><span class="sxs-lookup"><span data-stu-id="fca17-140">Adding Application Insights Analytics sections</span></span>

![Çalışma kitapları Analytics bölümünde](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="fca17-142">tooadd bir uygulama Öngörüler Analytics sorgu bölüm tooyour çalışma kitabı, hello kullan **eklemek Analytics sorgu** düğmesi hello çalışma kitabının hello altındaki ya da hello altındaki herhangi bir bölümü.</span><span class="sxs-lookup"><span data-stu-id="fca17-142">tooadd an Application Insights Analytics query section tooyour workbook, use hello **Add Analytics query** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

<span data-ttu-id="fca17-143">Analytics sorgu bölümleri rasgele sorguları Application Insights verilerinizi çalışma kitaplarına eklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="fca17-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="fca17-144">Bu esneklik Analytics sorgu bölümleri siteniz hello kullanıcıları, oturumlar, olayları ve bekletme, gibi yukarıda dört dışında hakkında tüm sorulara yanıt verilmesi, Git toofor olmalıdır anlamına gelir:</span><span class="sxs-lookup"><span data-stu-id="fca17-144">This flexibility means Analytics query sections should be your go-toofor answering any questions about your site other than hello four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="fca17-145">Kaç tane özel durumların mı, site throw hello sırasında aynı zaman dilimi kullanımı Reddet olarak?</span><span class="sxs-lookup"><span data-stu-id="fca17-145">How many exceptions did your site throw during hello same time period as a decline in usage?</span></span>
* <span data-ttu-id="fca17-146">Kullanıcılar bazı sayfasını görüntülemek için sayfa yükleme sürelerinin hello dağıtımını neydi?</span><span class="sxs-lookup"><span data-stu-id="fca17-146">What was hello distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="fca17-147">Kaç kullanıcının bazı sayfalar kümesi sitenizde görüntülenebilir, ancak olmayan bazı diğer sayfalarında ayarlamak?</span><span class="sxs-lookup"><span data-stu-id="fca17-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="fca17-148">Sitenizin işlevselliğin farklı alt kümelerini kullanan kullanıcılar, kümeleri varsa, bu yararlı toounderstand olabilir (Merhaba kullanmak `join` hello işleciyle `kind=leftanti` hello günlük analizi sorgu dili değiştiricisi).</span><span class="sxs-lookup"><span data-stu-id="fca17-148">This can be useful toounderstand if you have clusters of users who use different subsets of your site's functionality (use hello `join` operator with hello `kind=leftanti` modifier in hello Log Analytics query language).</span></span>

<span data-ttu-id="fca17-149">Kullanım hello [günlük analizi sorgu dili başvurusu](https://docs.loganalytics.io/) toolearn sorguları yazma hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="fca17-149">Use hello [Log Analytics query language reference](https://docs.loganalytics.io/) toolearn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="fca17-150">Metin ve Markdown bölümleri ekleme</span><span class="sxs-lookup"><span data-stu-id="fca17-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="fca17-151">Başlıklar, açıklamalar ve Yorumlar tooyour çalışma kitaplarına ekleme, tablolar ve grafikler kümesi biçiminde anlatı kapatma yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="fca17-151">Adding headings, explanations, and commentary tooyour workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="fca17-152">Çalışma kitapları metin bölümlerde destek hello [Markdown söz dizimi](https://daringfireball.net/projects/markdown/) başlıklar, kalın, italik ve madde işaretli listeler gibi biçimlendirme metin.</span><span class="sxs-lookup"><span data-stu-id="fca17-152">Text sections in workbooks support hello [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="fca17-153">tooadd bir metin bölüm tooyour çalışma kullanmak hello **metin ekleme** düğmesi hello çalışma kitabının hello altındaki ya da hello altındaki herhangi bir bölümü.</span><span class="sxs-lookup"><span data-stu-id="fca17-153">tooadd a text section tooyour workbook, use hello **Add text** button at hello bottom of hello workbook, or at hello bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="fca17-154">Kaydetme ve takımınızla çalışma kitaplarını paylaşma</span><span class="sxs-lookup"><span data-stu-id="fca17-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="fca17-155">Çalışma kitapları, Application Insights kaynağı, ya da hello içinde kaydedilir **raporlarım** özel tooyou bölümüne veya hello **paylaşılan raporları** erişimi olan erişilebilir tooeveryone bölümü toohello Application Insights kaynağı.</span><span class="sxs-lookup"><span data-stu-id="fca17-155">Workbooks are saved within an Application Insights resource, either in hello **My Reports** section that's private tooyou or in hello **Shared Reports** section that's accessible tooeveryone with access toohello Application Insights resource.</span></span> <span data-ttu-id="fca17-156">tooview hello kaynak tüm hello kitaplarında tıklatın hello **açık** hello eylem çubuğunda düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fca17-156">tooview all hello workbooks in hello resource, click hello **Open** button in hello action bar.</span></span>

<span data-ttu-id="fca17-157">şu anda kullanımda bir çalışma kitabı tooshare **raporlarım**:</span><span class="sxs-lookup"><span data-stu-id="fca17-157">tooshare a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="fca17-158">Tıklatın **açık** hello eylem çubuğunda</span><span class="sxs-lookup"><span data-stu-id="fca17-158">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="fca17-159">Merhaba "..." düğmesini tıklatın tooshare istediğiniz hello çalışma kitabı</span><span class="sxs-lookup"><span data-stu-id="fca17-159">Click hello "..." button beside hello workbook you want tooshare</span></span>
3. <span data-ttu-id="fca17-160">Tıklatın **taşıma tooShared raporları**.</span><span class="sxs-lookup"><span data-stu-id="fca17-160">Click **Move tooShared Reports**.</span></span>

<span data-ttu-id="fca17-161">tooshare bir çalışma kitabını bir bağlantıyla veya e-posta, yoluyla tıklatın **paylaşımı** hello eylem çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="fca17-161">tooshare a workbook with a link or via email, click **Share** in hello action bar.</span></span> <span data-ttu-id="fca17-162">Merhaba bağlantının alıcıları hello Azure portal tooview hello çalışma kitabındaki toothis kaynağa erişim aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="fca17-162">Keep in mind that recipients of hello link need access toothis resource in hello Azure portal tooview hello workbook.</span></span> <span data-ttu-id="fca17-163">toomake düzenlemeler, alıcılar gereken en az hello kaynak katkıda bulunan izinleri.</span><span class="sxs-lookup"><span data-stu-id="fca17-163">toomake edits, recipients need at least Contributor permissions for hello resource.</span></span>

<span data-ttu-id="fca17-164">bir bağlantı tooa çalışma kitabı tooan Azure Pano toopin:</span><span class="sxs-lookup"><span data-stu-id="fca17-164">toopin a link tooa workbook tooan Azure Dashboard:</span></span>

1. <span data-ttu-id="fca17-165">Tıklatın **açık** hello eylem çubuğunda</span><span class="sxs-lookup"><span data-stu-id="fca17-165">Click **Open** in hello action bar</span></span>
2. <span data-ttu-id="fca17-166">Merhaba "..." düğmesini tıklatın toopin istediğiniz hello çalışma kitabı</span><span class="sxs-lookup"><span data-stu-id="fca17-166">Click hello "..." button beside hello workbook you want toopin</span></span>
3. <span data-ttu-id="fca17-167">Tıklatın **PIN toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="fca17-167">Click **Pin toodashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fca17-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fca17-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="fca17-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fca17-169">Next steps</span></span>
- <span data-ttu-id="fca17-170">tooenable kullanımı deneyimleri, göndermeye Başla [özel olaylar](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) veya [sayfa görünümleri](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="fca17-170">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="fca17-171">Özel olaylar ya da sayfa görünümleri keşfedin hello kullanım araçları toolearn zaten gönderirseniz kullanıcılar hizmetinizi kullanma.</span><span class="sxs-lookup"><span data-stu-id="fca17-171">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="fca17-172">Kullanıcılar, Oturumlar, Etkinlikler</span><span class="sxs-lookup"><span data-stu-id="fca17-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="fca17-173">Huniler</span><span class="sxs-lookup"><span data-stu-id="fca17-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="fca17-174">Bekletme</span><span class="sxs-lookup"><span data-stu-id="fca17-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="fca17-175">Kullanıcı Akışları</span><span class="sxs-lookup"><span data-stu-id="fca17-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="fca17-176">Kullanıcı bağlamı Ekle</span><span class="sxs-lookup"><span data-stu-id="fca17-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
