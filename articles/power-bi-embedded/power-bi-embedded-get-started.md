---
title: "Microsoft Power BI Embedded kullanmaya başlama"
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
ms.openlocfilehash: 4afa8d2c7f8ec1942521ba5fa131967dfd581c91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="8f4e5-103">Microsoft Power BI Embedded kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8f4e5-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="8f4e5-104">**Power BI Embedded**, uygulama geliştiricilerin kendi uygulamalarına etkileşimli Power BI raporları eklemelerini sağlayan bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-104">**Power BI Embedded** is an Azure service that enables application developers to add interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="8f4e5-105">**Power BI Embedded** kullanıcıların oturum açma yöntemini yeniden tasarlamaya veya değiştirmeye gerek kalmadan var olan uygulamalarla birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-105">**Power BI Embedded** works with existing applications without needing redesign or changing the way users sign in.</span></span>

<span data-ttu-id="8f4e5-106">**Microsoft Power BI Embedded** kaynakları [Azure ARM API’leri](https://msdn.microsoft.com/library/mt712306.aspx) aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-106">Resources for **Microsoft Power BI Embedded** are provisioned through the [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="8f4e5-107">Bu örnekte, sağladığınız kaynak **Power BI Çalışma Alanı Koleksiyonu**’dur.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-107">In this case, the resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="8f4e5-108">Çalışma alanı koleksiyonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f4e5-108">Create a workspace collection</span></span>

<span data-ttu-id="8f4e5-109">**Çalışma Alanı Koleksiyonu**, uygulamanıza eklenecek içerik için üst düzey Azure kaynağı ve kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-109">A **Workspace Collection** is the top-level Azure resource and a container for the content that will be embedded in your application.</span></span> <span data-ttu-id="8f4e5-110">**Çalışma Alanı Koleksiyonu** iki şekilde oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="8f4e5-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="8f4e5-111">Azure Portal’ı el ile kullanarak</span><span class="sxs-lookup"><span data-stu-id="8f4e5-111">Manually using the Azure Portal</span></span>
* <span data-ttu-id="8f4e5-112">Azure Resource Manager(ARM) API’lerini program aracılığıyla kullanarak</span><span class="sxs-lookup"><span data-stu-id="8f4e5-112">Programmatically using the Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="8f4e5-113">Şimdi Azure Portal kullanarak **Çalışma Alanı Koleksiyonu** oluşturma adımlarını inceleyelim.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-113">Let's walk through the steps to build a **Workspace Collection** using the Azure Portal.</span></span>

1. <span data-ttu-id="8f4e5-114">**Azure Portal**’ı açın ve oturum açın: [http://portal.azure.com](http://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="8f4e5-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="8f4e5-115">Üst panelde **+ Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-115">Click **+ New** on the top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="8f4e5-116">**Veri + Analiz** altında **Power BI Embedded**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="8f4e5-117">**Çalışma Alanı Koleksiyonu Dikey Penceresi**’ne gerekli bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-117">On the **Workspace Collection Blade**, enter the required information.</span></span> <span data-ttu-id="8f4e5-118">**Fiyatlandırma** için bkz. [Power BI Embedded fiyatlandırması](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="8f4e5-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="8f4e5-119">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-119">Click **Create**.</span></span>

<span data-ttu-id="8f4e5-120">**Çalışma Alanı Koleksiyonu**’nun sağlanması birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-120">The **Workspace Collection** will take a few moments to provision.</span></span> <span data-ttu-id="8f4e5-121">Tamamlandığında **Çalışma Alanı Koleksiyonu Dikey Penceresi**’ne götürülürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-121">When completed, you'll be taken to the **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="8f4e5-122">**Oluşturma Dikey Penceresi** çalışma alanlarını oluşturan ve bunlara içerik dağıtan API’leri çağırmak için size gereken bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-122">The **Creation Blade** contains the information you need to call the APIs that create workspaces and deploy content to them.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="8f4e5-123">Power BI API’si erişim anahtarlarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="8f4e5-123">View Power BI API access keys</span></span>

<span data-ttu-id="8f4e5-124">Power BI API’lerini çağırmanın en önemli parçalarından biri **Erişim Anahtarları**’dır.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-124">One of the most important pieces of information needed to call the Power BI REST APIs are the **Access Keys**.</span></span> <span data-ttu-id="8f4e5-125">Bunlar API isteklerinizin kimlik doğrulaması için kullanılan **uygulama belirteçlerini** oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-125">These are used to generate the **app tokens** that are used to authenticate your API requests.</span></span> <span data-ttu-id="8f4e5-126">**Erişim Anahtarları**’nızı görüntülemek için **Ayarlar Dikey Penceresi**’nde **Erişim Anahtarları**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-126">To view your **Access Keys**, click **Access Keys** on the **Settings Blade**.</span></span> <span data-ttu-id="8f4e5-127">**Uygulama belirteçleri** hakkında daha fazla bilgi için bkz. [Power BI Embedded ile kimlik doğrulama ve yetkilendirme](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="8f4e5-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="8f4e5-128">İki anahtarınız olduğunu fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="8f4e5-129">Bu anahtarları kopyalayın ve uygulamanızda güvenli bir şekilde depolayın.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="8f4e5-130">**Çalışma Alanı Koleksiyonu**’nuzdaki tüm içeriği erişim imkanı sağlayacağından bu anahtarları bir parolaymış gibi ele almanız çok önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-130">It's very important that you treat these keys as you would a password, because they'll provide access to all the content in your **Workspace Collection**.</span></span>

<span data-ttu-id="8f4e5-131">İki anahtar listelenmekle birlikte, belirli bir seferde yalnızca bir anahtar gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="8f4e5-132">İkinci anahtar, hizmete erişimi kesintiye uğratmadan anahtarları dönemsel olarak yeniden oluşturabilmeniz için verilir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-132">The second key is provided so you can periodically regenerate keys without interrupting access to the service.</span></span>

<span data-ttu-id="8f4e5-133">Artık uygulamanız için bir Power BI örneğine ve **Erişim Anahtarları**’na sahip olduğunuza göre, kendi uygulamanıza bir rapor aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="8f4e5-134">Bir raporu içeri aktarmayı öğrenmeden önce, sonraki bölümde bir uygulamaya eklemek için Power BI veri kümeleri ve raporları oluşturma açıklanır.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-134">Before you learn how to import a report, the next section describes creating Power BI datasets and reports to embed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="8f4e5-135">Çalışma alanları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="8f4e5-135">Working with workspaces</span></span>

<span data-ttu-id="8f4e5-136">Çalışma alanı koleksiyonunuzu oluşturduktan sonra, raporlarınızı ve veri kümelerinizi barındıracak bir çalışma alanı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-136">After you have created your workspace collection, you will need to create a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="8f4e5-137">Bir çalışma alanı oluşturmak için [Post Worksapce REST API’sini](https://msdn.microsoft.com/library/azure/mt711503.aspx) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-137">To create a workspace, you will need to use the [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-to-embed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="8f4e5-138">Power BI Desktop kullanarak bir uygulamaya eklemek için Power BI veri kümeleri ve raporları oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f4e5-138">Create Power BI datasets and reports to embed into an app using Power BI Desktop</span></span>

<span data-ttu-id="8f4e5-139">Artık, uygulamanız için Power BI örneğini oluşturduğunuza ve**Erişim Anahtarları**’na sahip olduğunuza göre, eklemek istediğiniz Power BI veri kümelerini ve raporlarını oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need to create the Power BI datasets and reports that you want to embed.</span></span> <span data-ttu-id="8f4e5-140">Veri kümeleri ve raporlar **Power BI Desktop** kullanarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="8f4e5-141">[Power BI Desktop’u ücretsiz olarak](https://go.microsoft.com/fwlink/?LinkId=521662) indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="8f4e5-142">Hızlı bir şekilde kullanmaya başlamak için [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)’i de indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-142">Or, to quickly get started, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="8f4e5-143">**Power BI Desktop** kullanma hakkında daha fazla bilgi için bkz. [Power BI Desktop kullanmaya başlama](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="8f4e5-143">To learn more about how to use **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="8f4e5-144">**Power BI Desktop** ile, verilerin bir kopyasını **Power BI Desktop**’a aktararak ya da **DirectQuery** kullanarak doğrudan veri kaynağına bağlayarak veri kaynağınıza bağlanırsınız.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-144">With **Power BI Desktop**, you connect to your data source by importing a copy of the data into **Power BI Desktop** or connecting directly to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="8f4e5-145">**İçeri Aktarma** ve **DirectQuery**.arasındaki farklar burada yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-145">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="8f4e5-146">İçeri Aktarma</span><span class="sxs-lookup"><span data-stu-id="8f4e5-146">Import</span></span> | <span data-ttu-id="8f4e5-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="8f4e5-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="8f4e5-148">Tablolar, sütunlar *ve veriler* **Power BI Desktop**’a aktarılır veya kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="8f4e5-149">Görselleştirmelerle çalışırken, **Power BI Desktop** verilerin bir kopyasını sorgular.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-149">As you work with visualizations, **Power BI Desktop** queries a copy of the data.</span></span> <span data-ttu-id="8f4e5-150">Temel alınan verilerde meydana gelen değişiklikleri görmek için, tam, güncel veri kümesini tekrar yenilemeli ya da içeri aktarmalısınız.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-150">To see any changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="8f4e5-151">Yalnızca *tablolar ve sütunlar* ve **Power BI Desktop**’a aktarılır veya kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="8f4e5-152">Görselleştirmelerle çalışırken, **Power BI Desktop** temel alınan veri kaynağını sorgular, bu da her zaman güncel verileri görüntülediğiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-152">As you work with visualizations, **Power BI Desktop** queries the underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="8f4e5-153">Veri kaynağına bağlanma hakkında daha fazla bilgi için bkz. [Veri kaynağına bağlanma](power-bi-embedded-connect-datasource.md)</span><span class="sxs-lookup"><span data-stu-id="8f4e5-153">For more about connecting to a data source, see [Connect to a data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="8f4e5-154">Çalışmanızı **Power BI Desktop**’a kaydettikten sonra, PBIX dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="8f4e5-155">Bu dosya raporunuzu içerir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-155">This file contains your report.</span></span> <span data-ttu-id="8f4e5-156">Ayrıca, verileri içeri aktarırsanız PBIX tüm veri kümesini içerir ya da **DirectQuery** kullanırsanız PBIX yalnızca veri kümesi şemasını içerir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-156">In addition, if you import data the PBIX contains the complete dataset, or if you use **DirectQuery**, the PBIX contains just a dataset schema.</span></span> <span data-ttu-id="8f4e5-157">[Power BI İçeri Aktarma API’si](https://msdn.microsoft.com/library/mt711504.aspx) kullanarak PBIX’i program kullanarak çalışma alanınıza dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-157">You programmatically deploy the PBIX into your workspace using the [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="8f4e5-158">**Power BI Embedded**, veri kümenizin işaret ettiği sunucuyu ve veri tabanını değiştirmek ve veri kümesinin veri tabanınıza bağlanmak için kullanacağı bir hizmet hesabı kimlik bilgisi ayarlamak üzere ek API’lere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-158">**Power BI Embedded** has additional APIs to change the server and database that your dataset is pointing to and set a service account credential that the dataset will use to connect to your database.</span></span> <span data-ttu-id="8f4e5-159">Bkz. e [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) ve [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f4e5-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="8f4e5-160">API kullanarak Power BI veri kümeleri ve raporları oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f4e5-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="8f4e5-161">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="8f4e5-161">Datsets</span></span>

<span data-ttu-id="8f4e5-162">REST API kullanarak Power BI Embedded içinde veri kümeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-162">You can create datasets within Power BI Embedded using the REST API.</span></span> <span data-ttu-id="8f4e5-163">Daha sonra verileri veri kümenize gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-163">You can then push data into your dataset.</span></span> <span data-ttu-id="8f4e5-164">Bu, Power BI Desktop olmadan verilerinizle çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-164">This allows you to work with data without the need of Power BI Desktop.</span></span> <span data-ttu-id="8f4e5-165">Daha fazla bilgi için bkz. [Veri Kümeleri Gönderme](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f4e5-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="8f4e5-166">Reports</span><span class="sxs-lookup"><span data-stu-id="8f4e5-166">Reports</span></span>

<span data-ttu-id="8f4e5-167">JavaScript API kullanarak doğrudan uygulamanızda bir veri kümesinden rapor oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-167">You can create a report from a dataset directly in your application using the JavaScript API.</span></span> <span data-ttu-id="8f4e5-168">Daha fazla bilgi için bkz. [Power BI Embedded’de bir veri kümesinden yeni bir rapor oluşturma](power-bi-embedded-create-report-from-dataset.md).</span><span class="sxs-lookup"><span data-stu-id="8f4e5-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="8f4e5-169">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8f4e5-169">See Also</span></span>

[<span data-ttu-id="8f4e5-170">Bir örnek ile kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8f4e5-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="8f4e5-171">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="8f4e5-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="8f4e5-172">Rapor ekleme</span><span class="sxs-lookup"><span data-stu-id="8f4e5-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="8f4e5-173">[Power BI Embedded’de bir veri kümesinden yeni bir rapor oluşturma](power-bi-embedded-create-report-from-dataset.md)
[Raporları kaydetme](power-bi-embedded-save-reports.md)</span><span class="sxs-lookup"><span data-stu-id="8f4e5-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="8f4e5-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="8f4e5-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="8f4e5-175">JavaScript Örnek Ekleme</span><span class="sxs-lookup"><span data-stu-id="8f4e5-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="8f4e5-176">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="8f4e5-176">More questions?</span></span> [<span data-ttu-id="8f4e5-177">Power BI Topluluğu'nu deneyin</span><span class="sxs-lookup"><span data-stu-id="8f4e5-177">Try the Power BI Community</span></span>](http://community.powerbi.com/)

