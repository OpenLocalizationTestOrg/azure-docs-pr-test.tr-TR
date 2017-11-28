---
title: "Microsoft Power BI Embedded ile çalışmaya aaaGet"
description: "Power BI Embedded, iş zekası uygulamanıza etkileşimli Power BI raporları ekler"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="b0503-103">Microsoft Power BI Embedded kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b0503-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="b0503-104">**Power BI Embedded** etkileşimli Power BI raporları kendi uygulamalarınızı bu etkinleştirir uygulama geliştiricilerin tooadd bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="b0503-104">**Power BI Embedded** is an Azure service that enables application developers tooadd interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="b0503-105">**Power BI Embedded** yeniden tasarlanması gerek veya hello şekilde kullanıcıları için değiştirme olmadan mevcut uygulamalarla works oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b0503-105">**Power BI Embedded** works with existing applications without needing redesign or changing hello way users sign in.</span></span>

<span data-ttu-id="b0503-106">Kaynaklar için **Microsoft Power BI Embedded** hello sağlanan [Azure ARM API'leri](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0503-106">Resources for **Microsoft Power BI Embedded** are provisioned through hello [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="b0503-107">Bu durumda, sağlamanız hello kaynaktır bir **Power BI çalışma alanı koleksiyonu**.</span><span class="sxs-lookup"><span data-stu-id="b0503-107">In this case, hello resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="b0503-108">Çalışma alanı koleksiyonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0503-108">Create a workspace collection</span></span>

<span data-ttu-id="b0503-109">A **çalışma alanı koleksiyonu** hello üst düzey Azure kaynağı ve uygulamanızda katıştırılmış hello içerik için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="b0503-109">A **Workspace Collection** is hello top-level Azure resource and a container for hello content that will be embedded in your application.</span></span> <span data-ttu-id="b0503-110">**Çalışma Alanı Koleksiyonu** iki şekilde oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="b0503-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="b0503-111">Hello Azure Portal kullanarak el ile</span><span class="sxs-lookup"><span data-stu-id="b0503-111">Manually using hello Azure Portal</span></span>
* <span data-ttu-id="b0503-112">Hello Azure Resource Manager(ARM) API'lerini program aracılığıyla kullanma</span><span class="sxs-lookup"><span data-stu-id="b0503-112">Programmatically using hello Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="b0503-113">Şimdi hello adımları toobuild yol bir **çalışma alanı koleksiyonu** hello Azure Portal kullanarak.</span><span class="sxs-lookup"><span data-stu-id="b0503-113">Let's walk through hello steps toobuild a **Workspace Collection** using hello Azure Portal.</span></span>

1. <span data-ttu-id="b0503-114">**Azure Portal**’ı açın ve oturum açın: [http://portal.azure.com](http://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b0503-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="b0503-115">Tıklatın **+ yeni** hello üst panelde.</span><span class="sxs-lookup"><span data-stu-id="b0503-115">Click **+ New** on hello top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="b0503-116">**Veri + Analiz** altında **Power BI Embedded**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0503-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="b0503-117">Merhaba üzerinde **çalışma alanı koleksiyonu dikey**, hello gerekli bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="b0503-117">On hello **Workspace Collection Blade**, enter hello required information.</span></span> <span data-ttu-id="b0503-118">**Fiyatlandırma** için bkz. [Power BI Embedded fiyatlandırması](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="b0503-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="b0503-119">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b0503-119">Click **Create**.</span></span>

<span data-ttu-id="b0503-120">Merhaba **çalışma alanı koleksiyonu** birkaç dakika sonra tooprovision olur.</span><span class="sxs-lookup"><span data-stu-id="b0503-120">hello **Workspace Collection** will take a few moments tooprovision.</span></span> <span data-ttu-id="b0503-121">Tamamlandığında, toohello gidersiniz **çalışma alanı koleksiyonu dikey**.</span><span class="sxs-lookup"><span data-stu-id="b0503-121">When completed, you'll be taken toohello **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="b0503-122">Merhaba **oluşturma dikey penceresi** toocall hello çalışma alanları oluşturma ve içerik toothem dağıtan API'leri ihtiyacınız hello bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="b0503-122">hello **Creation Blade** contains hello information you need toocall hello APIs that create workspaces and deploy content toothem.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="b0503-123">Power BI API’si erişim anahtarlarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b0503-123">View Power BI API access keys</span></span>

<span data-ttu-id="b0503-124">Merhaba gerekli bilgileri toocall parçalarını hello Power BI API'lerini en önemli biri hello **erişim tuşları**.</span><span class="sxs-lookup"><span data-stu-id="b0503-124">One of hello most important pieces of information needed toocall hello Power BI REST APIs are hello **Access Keys**.</span></span> <span data-ttu-id="b0503-125">Kullanılan toogenerate hello bunlar **uygulama belirteçleri** kullanılan tooauthenticate olan API isteklerinizin.</span><span class="sxs-lookup"><span data-stu-id="b0503-125">These are used toogenerate hello **app tokens** that are used tooauthenticate your API requests.</span></span> <span data-ttu-id="b0503-126">tooview, **erişim tuşları**, tıklatın **erişim tuşları** hello üzerinde **ayarlar dikey**.</span><span class="sxs-lookup"><span data-stu-id="b0503-126">tooview your **Access Keys**, click **Access Keys** on hello **Settings Blade**.</span></span> <span data-ttu-id="b0503-127">**Uygulama belirteçleri** hakkında daha fazla bilgi için bkz. [Power BI Embedded ile kimlik doğrulama ve yetkilendirme](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="b0503-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="b0503-128">İki anahtarınız olduğunu fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b0503-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="b0503-129">Bu anahtarları kopyalayın ve uygulamanızda güvenli bir şekilde depolayın.</span><span class="sxs-lookup"><span data-stu-id="b0503-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="b0503-130">Bir parola gibi erişim tooall hello içeriğinde sağlarız olduğundan, bu anahtarlar kabul olduğunu çok önemlidir, **çalışma alanı koleksiyonu**.</span><span class="sxs-lookup"><span data-stu-id="b0503-130">It's very important that you treat these keys as you would a password, because they'll provide access tooall hello content in your **Workspace Collection**.</span></span>

<span data-ttu-id="b0503-131">İki anahtar listelenmekle birlikte, belirli bir seferde yalnızca bir anahtar gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0503-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="b0503-132">Merhaba ikinci anahtar anahtarları erişim toohello hizmeti kesintiye uğratmadan düzenli aralıklarla yeniden oluşturabilmeniz için sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b0503-132">hello second key is provided so you can periodically regenerate keys without interrupting access toohello service.</span></span>

<span data-ttu-id="b0503-133">Artık uygulamanız için bir Power BI örneğine ve **Erişim Anahtarları**’na sahip olduğunuza göre, kendi uygulamanıza bir rapor aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0503-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="b0503-134">Önce nasıl tooimport raporu, hello sonraki bölümde bir uygulamaya oluşturma Power BI veri kümelerini ve raporları tooembed açıklar öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b0503-134">Before you learn how tooimport a report, hello next section describes creating Power BI datasets and reports tooembed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="b0503-135">Çalışma alanları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="b0503-135">Working with workspaces</span></span>

<span data-ttu-id="b0503-136">Çalışma alanı koleksiyonu oluşturduktan sonra raporları ve veri kümelerini barındırmak bir çalışma alanı toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0503-136">After you have created your workspace collection, you will need toocreate a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="b0503-137">toocreate bir çalışma alanı, toouse hello gerekir [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0503-137">toocreate a workspace, you will need toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="b0503-138">Power BI Desktop kullanarak uygulamaya Power BI veri kümelerini ve raporları tooembed oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0503-138">Create Power BI datasets and reports tooembed into an app using Power BI Desktop</span></span>

<span data-ttu-id="b0503-139">Artık, uygulamanız için Power BI örneğini oluşturduğunuz ve sahip **erişim tuşları**, toocreate hello Power BI veri kümeleri ve raporları tooembed istediğiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0503-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need toocreate hello Power BI datasets and reports that you want tooembed.</span></span> <span data-ttu-id="b0503-140">Veri kümeleri ve raporlar **Power BI Desktop** kullanarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="b0503-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="b0503-141">[Power BI Desktop’u ücretsiz olarak](https://go.microsoft.com/fwlink/?LinkId=521662) indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0503-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="b0503-142">Veya, tooquickly Başlarken, hello indirebilirsiniz [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="b0503-142">Or, tooquickly get started, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="b0503-143">toolearn nasıl hakkında daha fazla toouse **Power BI Desktop**, bkz: [Power BI Desktop ile çalışmaya başlama](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="b0503-143">toolearn more about how toouse **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="b0503-144">İle **Power BI Desktop**, hello verilerin bir kopyasını alarak tooyour veri kaynağına bağlanmak **Power BI Desktop** veya toohello verileri doğrudan bağlanma kullanarak kaynak **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="b0503-144">With **Power BI Desktop**, you connect tooyour data source by importing a copy of hello data into **Power BI Desktop** or connecting directly toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="b0503-145">Kullanarak arasındaki farklar hello işte **alma** ve **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="b0503-145">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="b0503-146">İçeri Aktarma</span><span class="sxs-lookup"><span data-stu-id="b0503-146">Import</span></span> | <span data-ttu-id="b0503-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="b0503-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="b0503-148">Tablolar, sütunlar *ve veriler* **Power BI Desktop**’a aktarılır veya kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="b0503-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="b0503-149">Görselleştirmeleri ile çalışırken **Power BI Desktop** hello verilerin bir kopyasını sorgular.</span><span class="sxs-lookup"><span data-stu-id="b0503-149">As you work with visualizations, **Power BI Desktop** queries a copy of hello data.</span></span> <span data-ttu-id="b0503-150">toosee bu oluştu toohello temel alınan veri değişiklikleri, yenileme veya alma, bir tam, güncel veri kümesini yeniden.</span><span class="sxs-lookup"><span data-stu-id="b0503-150">toosee any changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="b0503-151">Yalnızca *tablolar ve sütunlar* ve **Power BI Desktop**’a aktarılır veya kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="b0503-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="b0503-152">Görselleştirmeleri ile çalışırken **Power BI Desktop** sorguları hello her zaman görüntülemekte olduğunuz geçerli verileri anlamına gelir temel alınan veri kaynağı.</span><span class="sxs-lookup"><span data-stu-id="b0503-152">As you work with visualizations, **Power BI Desktop** queries hello underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="b0503-153">Bağlantı tooa veri kaynağı hakkında daha fazla bilgi için bkz: [Bağlan tooa veri kaynağı](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="b0503-153">For more about connecting tooa data source, see [Connect tooa data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="b0503-154">Çalışmanızı **Power BI Desktop**’a kaydettikten sonra, PBIX dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b0503-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="b0503-155">Bu dosya raporunuzu içerir.</span><span class="sxs-lookup"><span data-stu-id="b0503-155">This file contains your report.</span></span> <span data-ttu-id="b0503-156">PBIX içeren veri hello içe aktarıyorsanız, ayrıca, tüm veri kümesini hello veya kullanıyorsanız **DirectQuery**, hello PBIX yalnızca veri kümesi şemasını içerir.</span><span class="sxs-lookup"><span data-stu-id="b0503-156">In addition, if you import data hello PBIX contains hello complete dataset, or if you use **DirectQuery**, hello PBIX contains just a dataset schema.</span></span> <span data-ttu-id="b0503-157">Program aracılığıyla hello PBIX hello kullanarak çalışma alanınıza dağıttığınız [Power BI içeri aktarma API'si](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0503-157">You programmatically deploy hello PBIX into your workspace using hello [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="b0503-158">**Power BI Embedded** ek API'leri toochange hello sunucu varsa ve Veri kümenizi dataset hello bir hizmet hesabı kimlik bilgisi tooand kümesi işaret ettiğinden veritabanı tooconnect tooyour veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="b0503-158">**Power BI Embedded** has additional APIs toochange hello server and database that your dataset is pointing tooand set a service account credential that hello dataset will use tooconnect tooyour database.</span></span> <span data-ttu-id="b0503-159">Bkz. e [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) ve [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0503-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="b0503-160">API kullanarak Power BI veri kümeleri ve raporları oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0503-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="b0503-161">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="b0503-161">Datsets</span></span>

<span data-ttu-id="b0503-162">Power BI hello REST API kullanarak katıştırılmış içinde veri kümeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0503-162">You can create datasets within Power BI Embedded using hello REST API.</span></span> <span data-ttu-id="b0503-163">Daha sonra verileri veri kümenize gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0503-163">You can then push data into your dataset.</span></span> <span data-ttu-id="b0503-164">Bu, Power BI Desktop, hello gerek kalmadan verilerle toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0503-164">This allows you toowork with data without hello need of Power BI Desktop.</span></span> <span data-ttu-id="b0503-165">Daha fazla bilgi için bkz. [Veri Kümeleri Gönderme](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0503-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="b0503-166">Reports</span><span class="sxs-lookup"><span data-stu-id="b0503-166">Reports</span></span>

<span data-ttu-id="b0503-167">Bir veri kümesinden hello JavaScript API kullanarak doğrudan uygulamanıza bir rapor oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0503-167">You can create a report from a dataset directly in your application using hello JavaScript API.</span></span> <span data-ttu-id="b0503-168">Daha fazla bilgi için bkz. [Power BI Embedded’de bir veri kümesinden yeni bir rapor oluşturma](power-bi-embedded-create-report-from-dataset.md).</span><span class="sxs-lookup"><span data-stu-id="b0503-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b0503-169">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="b0503-169">See Also</span></span>

[<span data-ttu-id="b0503-170">Bir örnek ile kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b0503-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="b0503-171">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="b0503-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="b0503-172">Rapor ekleme</span><span class="sxs-lookup"><span data-stu-id="b0503-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="b0503-173">[Power BI Embedded’de bir veri kümesinden yeni bir rapor oluşturma](power-bi-embedded-create-report-from-dataset.md)
[Raporları kaydetme](power-bi-embedded-save-reports.md)</span><span class="sxs-lookup"><span data-stu-id="b0503-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="b0503-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="b0503-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="b0503-175">JavaScript Örnek Ekleme</span><span class="sxs-lookup"><span data-stu-id="b0503-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="b0503-176">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="b0503-176">More questions?</span></span> [<span data-ttu-id="b0503-177">Merhaba Power BI topluluk deneyin</span><span class="sxs-lookup"><span data-stu-id="b0503-177">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

