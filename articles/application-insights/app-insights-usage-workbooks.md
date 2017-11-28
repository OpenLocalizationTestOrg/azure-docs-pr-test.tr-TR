---
title: "Araştırmak ve kullanım verilerini Azure Application Insights etkileşimli çalışma kitaplarında paylaşma | Microsoft docs"
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
ms.openlocfilehash: 75028b4fbda43d90f56690a33c7eb624fce049c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="549e1-103">Araştırmak ve kullanım verilerini Application Insights etkileşimli çalışma kitaplarında paylaşın</span><span class="sxs-lookup"><span data-stu-id="549e1-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="549e1-104">Çalışma kitapları birleştirmek [Azure Application Insights](app-insights-overview.md) veri görselleştirmeleri [analitik sorguları](app-insights-analytics.md)ve etkileşimli belgeleri metin.</span><span class="sxs-lookup"><span data-stu-id="549e1-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="549e1-105">Çalışma kitapları aynı Azure kaynak erişimi olan diğer takım üyeleri tarafından düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="549e1-105">Workbooks are editable by other team members with access to the same Azure resource.</span></span> <span data-ttu-id="549e1-106">Bu, sorgular ve bir çalışma kitabı oluşturmak için kullanılan denetimleri, keşfetme, genişletmenizi ve hataları olup olmadığını denetleyin kolaylaşır çalışma kitabı okuma diğer kişilerin kullanılabilir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="549e1-106">This means the queries and controls used to create a workbook are available to other people reading the workbook, making them easy to explore, extend, and check for mistakes.</span></span>

<span data-ttu-id="549e1-107">Çalışma kitapları gibi senaryolar için yararlı olur:</span><span class="sxs-lookup"><span data-stu-id="549e1-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="549e1-108">İlgilenilen ölçümleri önceden tanımadığınız olduğunda, uygulamanızın kullanımını keşfetme: kullanıcılar, saklama hızları, dönüştürme oranları vb. sayısı. Application ınsights'ta diğer kullanım analiz araçları çalışma kitapları, Görselleştirme ve çözümlemeleri de serbest biçimli araştırması bu tür için harika yapmadan birden çok türde birleştirmek olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="549e1-108">Exploring the usage of your app when you don't know the metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="549e1-109">Ekibiniz için yeni yayımlanan bir özelliğin nasıl gerçekleştirmekte açıklanması, gösteren kullanıcı tarafından anahtar etkileşimleri ve diğer ölçümleri sayar.</span><span class="sxs-lookup"><span data-stu-id="549e1-109">Explaining to your team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="549e1-110">Bir A sonuçlarını paylaşımı / B denemeler ekibinizin diğer üyeleriyle, uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="549e1-110">Sharing the results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="549e1-111">Denemeyi metinle amaçlarını açıklayan sonra her bir kullanım ölçümü ve Temizle çağrı-her ölçümü üstüne veya altına-hedefi olup için aşımı ayarlarına birlikte deneme değerlendirmek için kullanılan Analytics sorgu göster.</span><span class="sxs-lookup"><span data-stu-id="549e1-111">You can explain the goals for the experiment with text, then show each usage metric and Analytics query used to evaluate the experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="549e1-112">Bir kesinti etkisini veri, açıklama metnini ve gelecekte kesintileri önlemek için sonraki adımlar tartışması birleştirme uygulamanızı kullanımı hakkında raporlama.</span><span class="sxs-lookup"><span data-stu-id="549e1-112">Reporting the impact of an outage on the usage of your app, combining data, text explanation, and a discussion of next steps to prevent outages in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="549e1-113">Application Insights kaynağınıza, sayfa görünümleri veya çalışma kitaplarını kullanmak için özel olaylar içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="549e1-113">Your Application Insights resource must contain page views or custom events to use workbooks.</span></span> <span data-ttu-id="549e1-114">[Sayfa görünümleri Application Insights JavaScript SDK'sı ile otomatik olarak toplamak için uygulamanızı ayarlayın öğrenin](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="549e1-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="549e1-115">Düzenleme, yeniden düzenleme, kopyalama ve çalışma kitabını bölümleri silme</span><span class="sxs-lookup"><span data-stu-id="549e1-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="549e1-116">Bir çalışma kitabı bölümlerini yapılmış bir durumda: bağımsız olarak düzenlenebilir kullanım görselleştirmeleri, grafikler, tablolar, metin veya Analytics sorgu sonuçları.</span><span class="sxs-lookup"><span data-stu-id="549e1-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="549e1-117">Çalışma kitabı bölümünün içeriğini düzenlemek için tıklatın **Düzenle** aşağıda ve çalışma kitabı bölümü sağındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="549e1-117">To edit the contents of a workbook section, click the **Edit** button below and to the right of the workbook section.</span></span>

![Düzenleme denetimleri uygulama Öngörüler çalışma kitaplarını bölümü](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="549e1-119">Bitirdiğinizde bölüm düzenleme, tıklatın **yapılan düzenleme** bölümünün sol alt köşedeki içinde.</span><span class="sxs-lookup"><span data-stu-id="549e1-119">When you're done editing a section, click **Done Editing** in the bottom left corner of the section.</span></span>

2. <span data-ttu-id="549e1-120">Bir bölümün bir kopyasını oluşturmak için tıklatın **bu bölümü kopyalama** simgesi.</span><span class="sxs-lookup"><span data-stu-id="549e1-120">To create a duplicate of a section, click the **Clone this section** icon.</span></span> <span data-ttu-id="549e1-121">Yinelenen bölümleri oluşturma mükemmel bir sorguyu temel önceki yineleme kaybetmeden yinelemek şekilde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="549e1-121">Creating duplicate sections is a great to way to iterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="549e1-122">Bir çalışma kitabı bölümünde yukarı taşımak için tıklatın **Yukarı Taşı** veya **Aşağı Taşı** simgesi.</span><span class="sxs-lookup"><span data-stu-id="549e1-122">To move up a section in a workbook, click the **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="549e1-123">Bir bölümün kalıcı olarak kaldırmak için tıklatın **kaldırmak** simgesi.</span><span class="sxs-lookup"><span data-stu-id="549e1-123">To remove a section permanently, click the **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="549e1-124">Kullanım verileri görselleştirme bölümleri ekleme</span><span class="sxs-lookup"><span data-stu-id="549e1-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="549e1-125">Çalışma kitapları yerleşik kullanım analizi görselleştirmeleri dört tür sunar.</span><span class="sxs-lookup"><span data-stu-id="549e1-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="549e1-126">Her bir soru kullanımı hakkında uygulamanızın yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="549e1-126">Each answers a common question about the usage of your app.</span></span> <span data-ttu-id="549e1-127">Tablolar ve grafikler dışında bu dört bölüm eklemek için Analytics sorgu bölümleri (aşağıda görebilirsiniz) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="549e1-127">To add tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="549e1-128">Bir kullanıcı eklemek için oturum, olayları veya bekletme bölümünde kitabınıza kullanım **Kullanıcı Ekle** veya diğer karşılık gelen bir düğme çalışma kitabının altındaki ya da herhangi bir bölümü altındaki.</span><span class="sxs-lookup"><span data-stu-id="549e1-128">To add a Users, Sessions, Events, or Retention section to your workbook, use the **Add Users** or other corresponding button at the bottom of the workbook, or at the bottom of any section.</span></span>

![Kullanıcılar bölümünde çalışma kitapları](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="549e1-130">**Kullanıcıların** bölümleri yanıt "kaç kullanıcının bazı sayfa görüntülenemez veya Sitem bazı özelliği kullanılan?"</span><span class="sxs-lookup"><span data-stu-id="549e1-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="549e1-131">**Oturumları** bölümleri yanıt "kaç oturumları kullanıcılar bazı sayfa görüntüleme veya Sitem bazı özelliğini kullanarak harcamanız?"</span><span class="sxs-lookup"><span data-stu-id="549e1-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="549e1-132">**Olayları** bölümleri yanıt "kaç kez kullanıcılar bazı sayfasını görüntüleyebilir veya Sitem bazı özelliğini kullanın?"</span><span class="sxs-lookup"><span data-stu-id="549e1-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="549e1-133">Bu üç bölüm türleri denetimleri ve görselleştirmeleri aynı kümesi sunar:</span><span class="sxs-lookup"><span data-stu-id="549e1-133">Each of these three section types offers the same sets of controls and visualizations:</span></span>

* [<span data-ttu-id="549e1-134">Kullanıcıları, oturumlar ve olayları bölümleri düzenleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="549e1-134">Learn more about editing Users, Sessions, and Events sections</span></span>](app-insights-usage-segmentation.md)
* <span data-ttu-id="549e1-135">Ana grafik, çubuk grafik kılavuzları, otomatik Öngörüler ve örnek kullanıcılar görselleştirmeleri kullanarak geçiş **Göster grafik**, **Göster kılavuz**, **Göster Öngörüler**ve **Bu kullanıcılar örnek** onay kutularını her bölümün üstünde.</span><span class="sxs-lookup"><span data-stu-id="549e1-135">Toggle the main chart, histogram grids, automatic insights, and sample users visualizations using the **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at the top of each section.</span></span>

![Çalışma kitapları bekletme bölümünde](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="549e1-137">**Bekletme** bölümleri yanıt "bazı sayfa görüntülenemez veya bir gün veya hafta bazı özellik kullanılan kişiler kaç tane geri bir sonraki gün veya hafta gelen?"</span><span class="sxs-lookup"><span data-stu-id="549e1-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* [<span data-ttu-id="549e1-138">Bekletme bölümleri düzenleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="549e1-138">Learn more about editing Retention sections</span></span>](app-insights-usage-retention.md)
* <span data-ttu-id="549e1-139">İsteğe bağlı genel saklama grafiğiyle geçiş **Göster genel saklama grafik** bölümünün üst onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="549e1-139">Toggle the optional Overall Retention chart using the **Show overall retention chart** checkbox at the top of the section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="549e1-140">Uygulama Öngörüler Analytics bölümleri ekleme</span><span class="sxs-lookup"><span data-stu-id="549e1-140">Adding Application Insights Analytics sections</span></span>

![Çalışma kitapları Analytics bölümünde](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="549e1-142">Çalışma kitabınıza bir uygulama Öngörüler Analytics sorgu bölümü eklemek için kullanın **eklemek Analytics sorgu** çalışma kitabının altındaki ya da herhangi bir bölümü altındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="549e1-142">To add an Application Insights Analytics query section to your workbook, use the **Add Analytics query** button at the bottom of the workbook, or at the bottom of any section.</span></span>

<span data-ttu-id="549e1-143">Analytics sorgu bölümleri rasgele sorguları Application Insights verilerinizi çalışma kitaplarına eklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="549e1-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="549e1-144">Bu esneklik, siteniz kullanıcıları, oturumlar, olayları ve bekletme, gibi yukarıda dört dışında hakkında tüm sorulara yanıt verilmesi için gidilecek Analytics sorgu bölümleri olmalıdır anlamına gelir:</span><span class="sxs-lookup"><span data-stu-id="549e1-144">This flexibility means Analytics query sections should be your go-to for answering any questions about your site other than the four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="549e1-145">Kaç tane özel durumlar Reddet kullanımı ile aynı süre boyunca, sitenizi oluşturma?</span><span class="sxs-lookup"><span data-stu-id="549e1-145">How many exceptions did your site throw during the same time period as a decline in usage?</span></span>
* <span data-ttu-id="549e1-146">Sayfa yükleme sürelerinin kullanıcılar bazı sayfasını görüntülemek için dağıtım neydi?</span><span class="sxs-lookup"><span data-stu-id="549e1-146">What was the distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="549e1-147">Kaç kullanıcının bazı sayfalar kümesi sitenizde görüntülenebilir, ancak olmayan bazı diğer sayfalarında ayarlamak?</span><span class="sxs-lookup"><span data-stu-id="549e1-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="549e1-148">Bu, sitenizin işlevselliğin farklı alt kümelerini kullanan kullanıcılar, kümeleri olup olmadığını anlamak kullanışlı olabilir (kullanmak `join` işleciyle `kind=leftanti` günlük analizi sorgu dili değiştiricisi).</span><span class="sxs-lookup"><span data-stu-id="549e1-148">This can be useful to understand if you have clusters of users who use different subsets of your site's functionality (use the `join` operator with the `kind=leftanti` modifier in the Log Analytics query language).</span></span>

<span data-ttu-id="549e1-149">Kullanım [günlük analizi sorgu dili başvurusu](https://docs.loganalytics.io/) sorguları yazma hakkında daha fazla bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="549e1-149">Use the [Log Analytics query language reference](https://docs.loganalytics.io/) to learn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="549e1-150">Metin ve Markdown bölümleri ekleme</span><span class="sxs-lookup"><span data-stu-id="549e1-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="549e1-151">Başlıklar, açıklamalar ve yorumlar, çalışma kitaplarına ekleme yardımcı tablolar ve grafikler kümesi biçiminde anlatı açın.</span><span class="sxs-lookup"><span data-stu-id="549e1-151">Adding headings, explanations, and commentary to your workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="549e1-152">Çalışma kitapları destek metin bölümlerde [Markdown söz dizimi](https://daringfireball.net/projects/markdown/) başlıklar, kalın, italik ve madde işaretli listeler gibi biçimlendirme metin.</span><span class="sxs-lookup"><span data-stu-id="549e1-152">Text sections in workbooks support the [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="549e1-153">Çalışma kitabınıza metin bölümü eklemek için kullanın **metin eklemek** çalışma kitabının altındaki ya da herhangi bir bölümü altındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="549e1-153">To add a text section to your workbook, use the **Add text** button at the bottom of the workbook, or at the bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="549e1-154">Kaydetme ve takımınızla çalışma kitaplarını paylaşma</span><span class="sxs-lookup"><span data-stu-id="549e1-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="549e1-155">Çalışma kitapları, bir Application Insights kaynağı içindeki kaydedilir **raporlarım** size veya içinde özel bölümü **paylaşılan raporları** erişimi olan herkes için erişilebilir bölümü Uygulama Insights kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="549e1-155">Workbooks are saved within an Application Insights resource, either in the **My Reports** section that's private to you or in the **Shared Reports** section that's accessible to everyone with access to the Application Insights resource.</span></span> <span data-ttu-id="549e1-156">Kaynak tüm çalışma kitaplarını görüntülemek için **açık** eylem çubuğunda düğmesi.</span><span class="sxs-lookup"><span data-stu-id="549e1-156">To view all the workbooks in the resource, click the **Open** button in the action bar.</span></span>

<span data-ttu-id="549e1-157">Şu anda kullanımda bir çalışma kitabını paylaşmak için **raporlarım**:</span><span class="sxs-lookup"><span data-stu-id="549e1-157">To share a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="549e1-158">Tıklatın **açık** eylem çubuğunda</span><span class="sxs-lookup"><span data-stu-id="549e1-158">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="549e1-159">Paylaşmak istediğiniz çalışma kitabının yanındaki "..." düğmesini tıklatın</span><span class="sxs-lookup"><span data-stu-id="549e1-159">Click the "..." button beside the workbook you want to share</span></span>
3. <span data-ttu-id="549e1-160">Tıklatın **taşımak için paylaşılan raporları**.</span><span class="sxs-lookup"><span data-stu-id="549e1-160">Click **Move to Shared Reports**.</span></span>

<span data-ttu-id="549e1-161">Bir çalışma kitabı bir bağlantıyla ya da e-posta ile paylaşmak için tıklatın **paylaşmak** eylem çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="549e1-161">To share a workbook with a link or via email, click **Share** in the action bar.</span></span> <span data-ttu-id="549e1-162">Bağlantının alıcıları çalışma kitabını görüntülemek için Azure Portalı'nda bu kaynağa erişim gerektiğini aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="549e1-162">Keep in mind that recipients of the link need access to this resource in the Azure portal to view the workbook.</span></span> <span data-ttu-id="549e1-163">Gereken en az alıcılar düzenlemeleri yapmak için kaynak için katkıda bulunan izinleri.</span><span class="sxs-lookup"><span data-stu-id="549e1-163">To make edits, recipients need at least Contributor permissions for the resource.</span></span>

<span data-ttu-id="549e1-164">Bir Azure Panoya bir çalışma kitabı bağlantısını sabitlemek için:</span><span class="sxs-lookup"><span data-stu-id="549e1-164">To pin a link to a workbook to an Azure Dashboard:</span></span>

1. <span data-ttu-id="549e1-165">Tıklatın **açık** eylem çubuğunda</span><span class="sxs-lookup"><span data-stu-id="549e1-165">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="549e1-166">Sabitlemek istediğiniz çalışma kitabının yanındaki "..." düğmesini tıklatın</span><span class="sxs-lookup"><span data-stu-id="549e1-166">Click the "..." button beside the workbook you want to pin</span></span>
3. <span data-ttu-id="549e1-167">Tıklatın **panoya Sabitle**.</span><span class="sxs-lookup"><span data-stu-id="549e1-167">Click **Pin to dashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="549e1-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="549e1-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="549e1-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="549e1-169">Next steps</span></span>
- <span data-ttu-id="549e1-170">Kullanımı deneyimleri etkinleştirmek için göndermeye Başla [özel olaylar](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) veya [sayfa görünümleri](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="549e1-170">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="549e1-171">Özel olaylar veya sayfa görünümleri zaten gönderirseniz, kullanıcıların hizmetinizin kullanımını öğrenmek için kullanım araçları keşfedin.</span><span class="sxs-lookup"><span data-stu-id="549e1-171">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="549e1-172">Kullanıcılar, Oturumlar, Etkinlikler</span><span class="sxs-lookup"><span data-stu-id="549e1-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="549e1-173">Huniler</span><span class="sxs-lookup"><span data-stu-id="549e1-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="549e1-174">Bekletme</span><span class="sxs-lookup"><span data-stu-id="549e1-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="549e1-175">Kullanıcı Akışları</span><span class="sxs-lookup"><span data-stu-id="549e1-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="549e1-176">Kullanıcı bağlamı Ekle</span><span class="sxs-lookup"><span data-stu-id="549e1-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
