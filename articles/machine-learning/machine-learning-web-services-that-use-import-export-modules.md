---
title: "Azure Machine Learning web Hizmetleri içinde aaaUsing içeri/dışarı aktarma veri | Microsoft Docs"
description: "Nasıl toouse veri içeri aktarma ve dışarı aktarma veri modülleri toosend hello ve bir web hizmetinden veri alma öğrenin."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="602f8-103">Veri Alma ve Veri Gönderme modüllerini kullanan Azure ML web hizmetleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="602f8-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="602f8-104">Tahmine dayalı bir deneme oluştururken, bir web hizmeti giriş ve çıkış genellikle ekleyin.</span><span class="sxs-lookup"><span data-stu-id="602f8-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="602f8-105">Merhaba deneme dağıttığınızda, Tüketicileri gönderebilir ve hello girişleri ve çıkışları aracılığıyla hello web hizmetinden veri alma.</span><span class="sxs-lookup"><span data-stu-id="602f8-105">When you deploy hello experiment, consumers can send and receive data from hello web service through hello inputs and outputs.</span></span> <span data-ttu-id="602f8-106">Bazı uygulamalar için bir tüketicinin verileri veri akışlarından kullanılabilir veya zaten Azure Blob Depolama alanı gibi bir dış veri kaynağında bulunan.</span><span class="sxs-lookup"><span data-stu-id="602f8-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="602f8-107">Bu durumlarda, bunlar web hizmeti girişleri ve çıkışları kullanarak veri okumak veya yazmak zorunda değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="602f8-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="602f8-108">Bunlar, bunun yerine, hello toplu yürütme hizmeti (BES) tooread veri hello veri kaynağından veri içeri aktarma modülü kullanılarak kullanabilir ve sonuçları bir dışarı aktarma veri modülünü kullanarak tooa farklı veri konumu Puanlama hello yazma.</span><span class="sxs-lookup"><span data-stu-id="602f8-108">They can, instead, use hello Batch Execution Service (BES) tooread data from hello data source using an Import Data module and write hello scoring results tooa different data location using an Export Data module.</span></span>

<span data-ttu-id="602f8-109">Merhaba veri içeri aktarma ve dışarı aktarma veri modüller, gelen okuyabilir ve konumlar gibi Web URL HTTP, Hive sorgusu, bir Azure SQL veritabanı, Azure Table storage, Azure Blob Depolama, veri akışı aracılığıyla sağlayan toovarious verileri veya bir şirket içi SQL veritabanına yazma.</span><span class="sxs-lookup"><span data-stu-id="602f8-109">hello Import Data and Export data modules, can read from and write toovarious data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="602f8-110">Bu konuda hello kullanır "örnek 5: Eğitimi, Test, değerlendir ikili sınıflandırma: yetişkinlere yönelik veri kümesi" örnek ve hello veri kümesi zaten yüklü censusdata adlı bir Azure SQL tablosuna varsayar.</span><span class="sxs-lookup"><span data-stu-id="602f8-110">This topic uses hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes hello dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-hello-training-experiment"></a><span data-ttu-id="602f8-111">Merhaba eğitim denemenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="602f8-111">Create hello training experiment</span></span>
<span data-ttu-id="602f8-112">Merhaba açtığınızda "örnek 5: Eğitimi, Test, değerlendir ikili sınıflandırma: yetişkinlere yönelik veri kümesi" kullandığı hello örnek yetişkin Census gelir ikili sınıflandırma dataset örnek.</span><span class="sxs-lookup"><span data-stu-id="602f8-112">When you open hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses hello sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="602f8-113">Ve hello tuvale hello denemesinde görüntü aşağıdaki benzer toohello arar:</span><span class="sxs-lookup"><span data-stu-id="602f8-113">And hello experiment in hello canvas will look similar toohello following image:</span></span>

![Merhaba deneme'nin ilk yapılandırması.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="602f8-115">hello Azure SQL tablosuna tooread hello veri:</span><span class="sxs-lookup"><span data-stu-id="602f8-115">tooread hello data from hello Azure SQL table:</span></span>

1. <span data-ttu-id="602f8-116">Merhaba dataset modülü silin.</span><span class="sxs-lookup"><span data-stu-id="602f8-116">Delete hello dataset module.</span></span>
2. <span data-ttu-id="602f8-117">Merhaba bileşenleri arama kutusunda, içeri aktarma yazın.</span><span class="sxs-lookup"><span data-stu-id="602f8-117">In hello components search box, type import.</span></span>
3. <span data-ttu-id="602f8-118">Merhaba sonuçları listesinden bir *veri içeri aktarma* modülü toohello deneme tuvaline.</span><span class="sxs-lookup"><span data-stu-id="602f8-118">From hello results list, add an *Import Data* module toohello experiment canvas.</span></span>
4. <span data-ttu-id="602f8-119">Merhaba çıkışına bağlayın *veri içeri aktarma* hello modülü hello girişi *Clean Missing Data* modülü.</span><span class="sxs-lookup"><span data-stu-id="602f8-119">Connect output of hello *Import Data* module hello input of hello *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="602f8-120">Özellikler bölmesinde seçin **Azure SQL veritabanı** hello içinde **veri kaynağı** açılır.</span><span class="sxs-lookup"><span data-stu-id="602f8-120">In properties pane, select **Azure SQL Database** in hello **Data Source** dropdown.</span></span>
6. <span data-ttu-id="602f8-121">Merhaba, **veritabanı sunucusu adı**, **veritabanı adı**, **kullanıcı adı**, ve **parola** alanlar için uygun bilgileri hello girin Veritabanınızı.</span><span class="sxs-lookup"><span data-stu-id="602f8-121">In hello **Database server name**, **Database name**, **User name**, and **Password** fields, enter hello appropriate information for your database.</span></span>
7. <span data-ttu-id="602f8-122">Merhaba veritabanı sorgu alanına sorgu aşağıdaki hello girin.</span><span class="sxs-lookup"><span data-stu-id="602f8-122">In hello Database query field, enter hello following query.</span></span>
   
     <span data-ttu-id="602f8-123">[yaş] seçin</span><span class="sxs-lookup"><span data-stu-id="602f8-123">select [age],</span></span>
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     <span data-ttu-id="602f8-124">dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="602f8-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="602f8-125">Merhaba deneme tuvalinin Hello altındaki tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="602f8-125">At hello bottom of hello experiment canvas, click **Run**.</span></span>

## <a name="create-hello-predictive-experiment"></a><span data-ttu-id="602f8-126">Merhaba tahmini deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="602f8-126">Create hello predictive experiment</span></span>
<span data-ttu-id="602f8-127">Sonraki hello Tahmine dayalı denemeye, web hizmetini dağıtma ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="602f8-127">Next you set up hello predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="602f8-128">Merhaba deneme tuvalinin Hello altındaki tıklatın **Web hizmetinin ayarı** seçip **Tahmine dayalı Web hizmeti [önerilen]**.</span><span class="sxs-lookup"><span data-stu-id="602f8-128">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="602f8-129">Merhaba kaldırmak *Web hizmeti girişi* ve *Web hizmeti çıkış modülleri* hello Tahmine dayalı denemeye gelen.</span><span class="sxs-lookup"><span data-stu-id="602f8-129">Remove hello *Web Service Input* and *Web Service Output modules* from hello predictive experiment.</span></span> 
3. <span data-ttu-id="602f8-130">Dışarı aktarma Hello bileşenleri arama kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="602f8-130">In hello components search box, type export.</span></span>
4. <span data-ttu-id="602f8-131">Merhaba sonuçları listesinden bir *verileri dışa aktar* modülü toohello deneme tuvaline.</span><span class="sxs-lookup"><span data-stu-id="602f8-131">From hello results list, add an *Export Data* module toohello experiment canvas.</span></span>
5. <span data-ttu-id="602f8-132">Merhaba çıkışına bağlayın *Score Model* hello modülü hello girişi *verileri dışa aktar* modülü.</span><span class="sxs-lookup"><span data-stu-id="602f8-132">Connect output of hello *Score Model* module hello input of hello *Export Data* module.</span></span> 
6. <span data-ttu-id="602f8-133">Özellikler bölmesinde seçin **Azure SQL veritabanı** hello veri hedef açılır içinde.</span><span class="sxs-lookup"><span data-stu-id="602f8-133">In properties pane, select **Azure SQL Database** in hello data destination dropdown.</span></span>
7. <span data-ttu-id="602f8-134">Merhaba, **veritabanı sunucusu adı**, **veritabanı adı**, **Server kullanıcı hesabı adı**, ve **Server kullanıcı hesabı parolasını** alanları girin Merhaba veritabanınız için uygun bilgileri.</span><span class="sxs-lookup"><span data-stu-id="602f8-134">In hello **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter hello appropriate information for your database.</span></span>
8. <span data-ttu-id="602f8-135">Merhaba, **virgülle ayrılmış kaydedilmiş sütunları toobe listesi** alan, skoru etiketleri yazın.</span><span class="sxs-lookup"><span data-stu-id="602f8-135">In hello **Comma separated list of columns toobe saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="602f8-136">Merhaba, **veri tablo adı alanı**, dbo yazın. ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="602f8-136">In hello **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="602f8-137">Merhaba tablo mevcut değilse hello deneme çalıştırdığınızda veya hello web hizmeti adlı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="602f8-137">If hello table does not exist, it is created when hello experiment is run or hello web service is called.</span></span>
10. <span data-ttu-id="602f8-138">Merhaba, **virgülle ayrılmış datatable sütunlar listesi** alan, ScoredLabels yazın.</span><span class="sxs-lookup"><span data-stu-id="602f8-138">In hello **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="602f8-139">Bir uygulama çağrıları son web hizmeti hello yazdığınızda, çalışma zamanında farklı bir giriş sorgu veya hedef tablo toospecify isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="602f8-139">When you write an application that calls hello final web service, you may want toospecify a different input query or destination table at run time.</span></span> <span data-ttu-id="602f8-140">tooconfigure bu girişleri ve çıkışları, kullanın hello Web hizmeti parametreleri özellik tooset hello *veri içeri aktarma* Modülü *veri kaynağı* özelliği ve hello *verileri dışa aktar* modu veri hedef özelliği.</span><span class="sxs-lookup"><span data-stu-id="602f8-140">tooconfigure these inputs and outputs, use hello Web Service Parameters feature tooset hello *Import Data* module *Data source* property and hello *Export Data* mode data destination property.</span></span>  <span data-ttu-id="602f8-141">Merhaba Web hizmeti parametreleri hakkında daha fazla bilgi için bkz: [AzureML Web hizmeti parametreleri girişi](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) hello Cortana Intelligence ve makine öğrenme blogu.</span><span class="sxs-lookup"><span data-stu-id="602f8-141">For more information on Web Service Parameters, see hello [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on hello Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="602f8-142">Merhaba alma sorgu ve hello hedef tablo için tooconfigure hello Web hizmeti parametreleri:</span><span class="sxs-lookup"><span data-stu-id="602f8-142">tooconfigure hello Web Service Parameters for hello import query and hello destination table:</span></span>

1. <span data-ttu-id="602f8-143">Hello için hello Özellikler bölmesinde *veri içeri aktarma* modülü, hello hello simgesini tıklatın top hello sağındaki **veritabanı sorgusu** alan ve seçin **web hizmeti parametresi ayarlamak**.</span><span class="sxs-lookup"><span data-stu-id="602f8-143">In hello properties pane for hello *Import Data* module, click hello icon at hello top right of hello **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="602f8-144">Hello için hello Özellikler bölmesinde *verileri dışa aktar* modülü, hello hello simgesini tıklatın top hello sağındaki **veri tablo adı** alan ve seçin **web hizmeti parametresi ayarlanmış**.</span><span class="sxs-lookup"><span data-stu-id="602f8-144">In hello properties pane for hello *Export Data* module, click hello icon at hello top right of hello **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="602f8-145">Hello hello sonundaki *verileri dışa aktar* hello de modülü Özellikler bölmesinde **Web hizmeti parametreleri** bölümünde veritabanı sorgusu tıklayın ve sorguyu yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="602f8-145">At hello bottom of hello *Export Data* module properties pane, in hello **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="602f8-146">Tıklatın **veri tablo adı** ve yeniden adlandırmak **tablo**.</span><span class="sxs-lookup"><span data-stu-id="602f8-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="602f8-147">İşiniz bittiğinde, denemenizi benzer toohello görüntü aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="602f8-147">When you are done, your experiment should look similar toohello following image:</span></span>

![Deneme son görünümünü.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="602f8-149">Artık hello deneme bir web hizmeti olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="602f8-149">Now you can deploy hello experiment as a web service.</span></span>

## <a name="deploy-hello-web-service"></a><span data-ttu-id="602f8-150">Merhaba web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="602f8-150">Deploy hello web service</span></span>
<span data-ttu-id="602f8-151">Klasik veya yeni bir web hizmeti tooeither dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="602f8-151">You can deploy tooeither a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="602f8-152">Klasik Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="602f8-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="602f8-153">Klasik Web hizmeti olarak toodeploy ve bir uygulama tooconsume oluşturun bunu:</span><span class="sxs-lookup"><span data-stu-id="602f8-153">toodeploy as a Classic Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="602f8-154">Merhaba deneme tuvalinin Hello altındaki Çalıştır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="602f8-154">At hello bottom of hello experiment canvas, click Run.</span></span>
2. <span data-ttu-id="602f8-155">Çalıştırma hello tamamlandığında tıklayın **Web hizmeti Dağıt** seçip **Web hizmeti Dağıt [Klasik]**.</span><span class="sxs-lookup"><span data-stu-id="602f8-155">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="602f8-156">Merhaba web hizmeti panosunda API anahtarınızı bulun.</span><span class="sxs-lookup"><span data-stu-id="602f8-156">On hello web service dashboard, locate your API key.</span></span> <span data-ttu-id="602f8-157">Kopyalayın ve daha sonra toouse kaydedin.</span><span class="sxs-lookup"><span data-stu-id="602f8-157">Copy and save it toouse later.</span></span>
4. <span data-ttu-id="602f8-158">Merhaba, **varsayılan uç nokta** tablo, hello tıklatın **toplu iş yürütme** bağlantı tooopen hello API Yardım sayfası.</span><span class="sxs-lookup"><span data-stu-id="602f8-158">In hello **Default Endpoint** table, click hello **Batch Execution** link tooopen hello API Help Page.</span></span>
5. <span data-ttu-id="602f8-159">Visual Studio'da bir C# konsol uygulaması oluşturun: **yeni** > **proje** > **Visual C#** > **Windows Klasik Masaüstü** > **konsol uygulaması (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="602f8-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="602f8-160">Merhaba Hello API Yardım sayfası, bulma **örnek kod** hello sayfanın hello kısmına.</span><span class="sxs-lookup"><span data-stu-id="602f8-160">On hello API Help Page, find hello **Sample Code** section at hello bottom of hello page.</span></span>
7. <span data-ttu-id="602f8-161">Kopyalama ve hello C# örnek kodu, Program.cs dosyasına yapıştırın ve tüm başvuruları toohello blob depolama kaldırın.</span><span class="sxs-lookup"><span data-stu-id="602f8-161">Copy and paste hello C# sample code into your Program.cs file, and remove all references toohello blob storage.</span></span>
8. <span data-ttu-id="602f8-162">Merhaba Hello değerini güncelleştirmek *apikey ile yapılan* daha önce kaydedilmiş hello API anahtarıyla değişken.</span><span class="sxs-lookup"><span data-stu-id="602f8-162">Update hello value of hello *apiKey* variable with hello API key saved earlier.</span></span>
9. <span data-ttu-id="602f8-163">Merhaba istek bildirim ve güncelleştirme hello parametrelerinin değerleri Web hizmeti toohello geçirilen bulun *veri içeri aktarma* ve *verileri dışa aktar* modüller.</span><span class="sxs-lookup"><span data-stu-id="602f8-163">Locate hello request declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="602f8-164">Bu durumda, hello özgün sorgu kullanır, ancak yeni bir tablo adı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="602f8-164">In this case, you use hello original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="602f8-165">Merhaba uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="602f8-165">Run hello application.</span></span> 

<span data-ttu-id="602f8-166">Çalıştırma hello tamamlama sonrasında yeni bir tablo sonuçları Puanlama hello içeren toohello veritabanına eklenir.</span><span class="sxs-lookup"><span data-stu-id="602f8-166">On completion of hello run, a new table is added toohello database containing hello scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="602f8-167">Yeni bir Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="602f8-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="602f8-168">toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="602f8-168">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="602f8-169">Daha fazla bilgi için bkz: [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="602f8-169">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="602f8-170">Yeni bir Web hizmeti olarak toodeploy ve bir uygulama tooconsume oluşturun bunu:</span><span class="sxs-lookup"><span data-stu-id="602f8-170">toodeploy as a New Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="602f8-171">Merhaba deneme tuvalinin Hello altındaki tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="602f8-171">At hello bottom of hello experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="602f8-172">Çalıştırma hello tamamlandığında tıklayın **Web hizmeti Dağıt** seçip **Web hizmeti dağıtma [Yeni]**.</span><span class="sxs-lookup"><span data-stu-id="602f8-172">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="602f8-173">Merhaba dağıtmak deneme sayfasında, web hizmetiniz için bir ad girin ve bir fiyatlandırma planı seçin ve ardından **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="602f8-173">On hello Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="602f8-174">Merhaba üzerinde **Hızlı Başlangıç** sayfasında, **Tüket**.</span><span class="sxs-lookup"><span data-stu-id="602f8-174">On hello **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="602f8-175">Merhaba, **örnek kod** 'yi tıklatın **toplu**.</span><span class="sxs-lookup"><span data-stu-id="602f8-175">In hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="602f8-176">Visual Studio'da bir C# konsol uygulaması oluşturun: **yeni** > **proje** > **Visual C#** > **Windows Klasik Masaüstü** > **konsol uygulaması (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="602f8-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="602f8-177">Merhaba C# örnek kodu kopyalayıp Program.cs dosyanıza yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="602f8-177">Copy and paste hello C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="602f8-178">Merhaba Hello değerini güncelleştirmek *apikey ile yapılan* hello ile değişken **birincil anahtar** hello bulunan **temel tüketim bilgileri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="602f8-178">Update hello value of hello *apiKey* variable with hello **Primary Key** located in hello **Basic consumption info** section.</span></span>
9. <span data-ttu-id="602f8-179">Merhaba bulun *scoreRequest* bildirim ve güncelleştirme hello parametrelerinin değerleri Web hizmeti toohello geçirilen *veri içeri aktarma* ve *verileri dışa aktar* modüller.</span><span class="sxs-lookup"><span data-stu-id="602f8-179">Locate hello *scoreRequest* declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="602f8-180">Bu durumda, hello özgün sorgu kullanır, ancak yeni bir tablo adı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="602f8-180">In this case, you use hello original query, but define a new table name.</span></span>
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. <span data-ttu-id="602f8-181">Merhaba uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="602f8-181">Run hello application.</span></span> 

