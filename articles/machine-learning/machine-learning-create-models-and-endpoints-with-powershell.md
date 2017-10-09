---
title: "aaaCreate bir deneme birden çok modellerinden | Microsoft Docs"
description: "Birden çok Machine Learning modellerini PowerShell toocreate kullanın ve web hizmeti uç hello ile aynı algoritmanın ancak farklı eğitim veri kümeleri."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="ae549-103">PowerShell kullanarak bir denemeden çok sayıda Machine Learning modeli ve web hizmeti uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ae549-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="ae549-104">Bir ortak makine öğrenimi sorun şudur: hello birçok modelleri toocreate istediğiniz aynı eğitim iş akışı ve kullanım hello aynı algoritması, ancak giriş olarak farklı eğitim veri kümeleri.</span><span class="sxs-lookup"><span data-stu-id="ae549-104">Here's a common machine learning problem: You want toocreate many models that have hello same training workflow and use hello same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="ae549-105">Bu makale size nasıl gösterir toodo bu yalnızca bir deneme kullanarak Azure Machine Learning Studio'daki ölçekte.</span><span class="sxs-lookup"><span data-stu-id="ae549-105">This article shows you how toodo this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="ae549-106">Örneğin, bir genel bisiklet kiralama Acentelik işletme sahibi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="ae549-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="ae549-107">Regresyon modeli toopredict hello kiralama isteğe bağlı geçmiş verilere dayanan toobuild istiyor.</span><span class="sxs-lookup"><span data-stu-id="ae549-107">You want toobuild a regression model toopredict hello rental demand based on historic data.</span></span> <span data-ttu-id="ae549-108">Merhaba dünya genelindeki 1.000 kiralama konumunuz varsa ve her tarih, saat, hava durumu gibi önemli özellikler içeren konumu ve belirli tooeach konumunun trafiği için bir veri kümesi derledik.</span><span class="sxs-lookup"><span data-stu-id="ae549-108">You have 1,000 rental locations across hello world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific tooeach location.</span></span>

<span data-ttu-id="ae549-109">Bir kez tüm konumlar arasında tüm hello veri kümeleri birleştirilmiş bir sürümünü kullanarak modelinizi eğitmek.</span><span class="sxs-lookup"><span data-stu-id="ae549-109">You could train your model once using a merged version of all hello datasets across all locations.</span></span> <span data-ttu-id="ae549-110">Konumların her bir benzersiz ortamı olduğundan, daha iyi bir yaklaşım olur, ancak ayrı ayrı her konum için hello veri kümesini kullanarak, regresyon modeli tootrain olabilir.</span><span class="sxs-lookup"><span data-stu-id="ae549-110">But because each of your locations has a unique environment, a better approach would be tootrain your regression model separately using hello dataset for each location.</span></span> <span data-ttu-id="ae549-111">Bu şekilde, her eğitilen model ele geçirebilir hesap hello farklı depolama boyutları, birim, coğrafi konum, popülasyon, bisiklet kolay trafiği ortamı *vb.*.</span><span class="sxs-lookup"><span data-stu-id="ae549-111">That way, each trained model could take into account hello different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="ae549-112">Merhaba en iyi yaklaşımı olabilir ancak her bir benzersiz bir konumu temsil eden toocreate 1.000 eğitim denemeler Azure Machine learning'de istemiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="ae549-112">That may be hello best approach, but you don't want toocreate 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="ae549-113">Bunaltıcı görev olmasının yanı sıra, aynı zamanda olup her deneme tüm hello eğitim veri kümesi dışında aynı bileşenleri hello olacağından oldukça verimsiz gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="ae549-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all hello same components except for hello training dataset.</span></span>

<span data-ttu-id="ae549-114">Neyse ki, biz bu hello kullanarak gerçekleştirebilirsiniz [Azure Machine Learning yeniden eğitme API](machine-learning-retrain-models-programmatically.md) ve otomatik otomatikleştirme hello görevle [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="ae549-114">Fortunately, we can accomplish this by using hello [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating hello task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ae549-115">toomake bizim örnek çalıştırmak daha hızlı, biz 1.000 too10 konumlardan hello sayısını azaltın.</span><span class="sxs-lookup"><span data-stu-id="ae549-115">toomake our sample run faster, we'll reduce hello number of locations from 1,000 too10.</span></span> <span data-ttu-id="ae549-116">Ancak hello aynı ilkeleri ve yordamları too1, 000 konumları uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ae549-116">But hello same principles and procedures apply too1,000 locations.</span></span> <span data-ttu-id="ae549-117">Merhaba yalnızca 1.000 veri kümelerinden tootrain istiyorsanız, aşağıdaki PowerShell betikleri paralel hello çalışan toothink istemenizdir farktır.</span><span class="sxs-lookup"><span data-stu-id="ae549-117">hello only difference is that if you want tootrain from 1,000 datasets you probably want toothink of running hello following PowerShell scripts in parallel.</span></span> <span data-ttu-id="ae549-118">Nasıl bu makalede, ancak hello kapsamı dışındadır toodo PowerShell örnekleri çoklu iş parçacığı hello Internet üzerinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae549-118">How toodo that is beyond hello scope of this article, but you can find examples of PowerShell multi-threading on hello Internet.</span></span>  
> 
> 

## <a name="set-up-hello-training-experiment"></a><span data-ttu-id="ae549-119">Merhaba eğitim denemenizi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ae549-119">Set up hello training experiment</span></span>
<span data-ttu-id="ae549-120">Toouse örneği yapacağız [eğitim denemenizi](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) , hello zaten oluşturduk [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="ae549-120">We're going toouse an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="ae549-121">Bu deneme açın, [Azure Machine Learning Studio](https://studio.azureml.net) çalışma.</span><span class="sxs-lookup"><span data-stu-id="ae549-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="ae549-122">Bu örnek ile birlikte sipariş toofollow içinde boş bir çalışma alanı yerine standart bir çalışma alanı toouse isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae549-122">In order toofollow along with this example, you may want toouse a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="ae549-123">Biz bir uç nokta - 10 uç noktaları - toplam her müşteri için oluşturursunuz ve boş bir çalışma alanı sınırlı too3 uç noktaları olduğundan, standart bir çalışma alanı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ae549-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited too3 endpoints.</span></span> <span data-ttu-id="ae549-124">Yalnızca bir ücretsiz çalışma alanı varsa, yalnızca hello betikleri tooallow yalnızca 3 konumları için aşağıda değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ae549-124">If you only have a free workspace, just modify hello scripts below tooallow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="ae549-125">Merhaba deneme kullanan bir **veri içeri aktarma** modülü tooimport hello eğitim veri kümesi *customer001.csv* bir Azure depolama hesabından.</span><span class="sxs-lookup"><span data-stu-id="ae549-125">hello experiment uses an **Import Data** module tooimport hello training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="ae549-126">Biz tüm bisiklet kiralama konumlardan toplanan eğitim veri kümeleri ve bunları aynı blob depolama konumu dosya adları arasında değişen ile Merhaba depolanan varsayalım *rentalloc001.csv* çok*rentalloc10.csv* .</span><span class="sxs-lookup"><span data-stu-id="ae549-126">Let's assume we have collected training datasets from all bike rental locations and stored them in hello same blob storage location with file names ranging from *rentalloc001.csv* too*rentalloc10.csv*.</span></span>

![Görüntü](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="ae549-128">Unutmayın bir **Web hizmeti çıkış** modülü toohello eklendi **Train Model** modülü.</span><span class="sxs-lookup"><span data-stu-id="ae549-128">Note that a **Web Service Output** module has been added toohello **Train Model** module.</span></span>
<span data-ttu-id="ae549-129">Bu deneme bir web hizmeti olarak dağıtıldığında, o çıktıyla ilişkili hello endpoint hello eğitilen model hello .ilearner dosyası biçiminde döndürür.</span><span class="sxs-lookup"><span data-stu-id="ae549-129">When this experiment is deployed as a web service, hello endpoint associated with that output will return hello trained model in hello format of a .ilearner file.</span></span>

<span data-ttu-id="ae549-130">Ayrıca bu hello hello URL'sini bir web hizmeti parametresini ayarlar olduğunu unutmayın **veri içeri aktarma** modülü kullanır.</span><span class="sxs-lookup"><span data-stu-id="ae549-130">Also note that we set up a web service parameter for hello URL that hello **Import Data** module uses.</span></span> <span data-ttu-id="ae549-131">Bu bize toouse hello parametresi toospecify tek tek eğitim veri kümeleri tootrain hello modeli her konum için olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ae549-131">This allows us toouse hello parameter toospecify individual training datasets tootrain hello model for each location.</span></span>
<span data-ttu-id="ae549-132">Biz yapılan bu, bir SQL sorgusu verilerle bir web hizmeti parametresi tooget bir SQL Azure veritabanı veya yalnızca kullanarak gibi diğer yolları bir **Web hizmeti girişi** modülü toopass dataset toohello içinde web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ae549-132">There are other ways we could have done this, such as using a SQL query with a web service parameter tooget data from a SQL Azure database, or simply using a  **Web Service Input** module toopass in a dataset toohello web service.</span></span>

![Görüntü](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="ae549-134">Şimdi, hello varsayılan değerini kullanarak bu eğitim denemenizi Şimdi Çalıştır *rental001.csv* eğitim veri kümesi hello gibi.</span><span class="sxs-lookup"><span data-stu-id="ae549-134">Now, let's run this training experiment using hello default value *rental001.csv* as hello training dataset.</span></span> <span data-ttu-id="ae549-135">Merhaba hello çıktısını görüntülerseniz **değerlendir** Modülü (Merhaba çıkış tıklayın ve **Görselleştir**), biz alma, iyi bir performans görebilirsiniz *AUC* 0.91 =.</span><span class="sxs-lookup"><span data-stu-id="ae549-135">If you view hello output of hello **Evaluate** module (click hello output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="ae549-136">Bu noktada, hazır toodeploy Bu eğitim denemenizi dışında bir web hizmeti olarak çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="ae549-136">At this point, we're ready toodeploy a web service out of this training experiment.</span></span>

## <a name="deploy-hello-training-and-scoring-web-services"></a><span data-ttu-id="ae549-137">Merhaba eğitim ve puanlama web hizmetlerini dağıtma</span><span class="sxs-lookup"><span data-stu-id="ae549-137">Deploy hello training and scoring web services</span></span>
<span data-ttu-id="ae549-138">toodeploy hello web hizmeti, eğitim tıklatın hello **Web hizmetinin ayarı** hello deneme tuvalinin düğmesine tıklayın ve ardından **Web hizmeti Dağıt**.</span><span class="sxs-lookup"><span data-stu-id="ae549-138">toodeploy hello training web service, click hello **Set Up Web Service** button below hello experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="ae549-139">"" Bisiklet kiralama Eğitim". Bu web hizmeti çağrısı</span><span class="sxs-lookup"><span data-stu-id="ae549-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="ae549-140">Şimdi toodeploy hello Puanlama web hizmeti gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae549-140">Now we need toodeploy hello scoring web service.</span></span>
<span data-ttu-id="ae549-141">toodo Bu, biz tıklatabilirsiniz **Web hizmetinin ayarı** hello tuvale ve seçin **Tahmine dayalı Web hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="ae549-141">toodo this, we can click **Set Up Web Service** below hello canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="ae549-142">Bu bir Puanlama deneme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ae549-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="ae549-143">Biz toomake birkaç küçük ayarlamalar toomake giriş hello Etiket sütununda "cnt" Merhaba kaldırma ve hello çıktı tooonly hello örnek kimliği ve hello karşılık gelen sınırlama değeri tahmin gibi bir web hizmeti olarak çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae549-143">We'll need toomake a few minor adjustments toomake it work as a web service, such as removing hello label column "cnt" from hello input data and limiting hello output tooonly hello instance id and hello corresponding predicted value.</span></span>

<span data-ttu-id="ae549-144">toosave çalışma, kendiniz hello açabilirler [Tahmine dayalı denemeye](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) hello zaten hazırlanır galeri içinde.</span><span class="sxs-lookup"><span data-stu-id="ae549-144">toosave yourself that work, you can simply open hello [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in hello Gallery that's already been prepared.</span></span>

<span data-ttu-id="ae549-145">toodeploy hello web hizmeti Hello Tahmine dayalı denemeyi çalıştırın, ardından hello **Web hizmeti Dağıt** hello tuvale aşağıdaki düğmesine.</span><span class="sxs-lookup"><span data-stu-id="ae549-145">toodeploy hello web service, run hello predictive experiment, then click hello **Deploy Web Service** button below hello canvas.</span></span> <span data-ttu-id="ae549-146">Web hizmeti "Bisiklet kiralama Puanlama" Puanlama adı hello ".</span><span class="sxs-lookup"><span data-stu-id="ae549-146">Name hello scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="ae549-147">PowerShell ile 10 aynı web hizmeti uç noktalarını oluşturma</span><span class="sxs-lookup"><span data-stu-id="ae549-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="ae549-148">Bu web Hizmeti'nin varsayılan uç noktası ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="ae549-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="ae549-149">Ancak güncelleştirilemiyor bu yana hello varsayılan uç olarak ilgi değiliz.</span><span class="sxs-lookup"><span data-stu-id="ae549-149">But we're not as interested in hello default endpoint since it can't be updated.</span></span> <span data-ttu-id="ae549-150">Ne ihtiyacımız toodo olan toocreate 10 ek uç noktalar, her konum için bir tane.</span><span class="sxs-lookup"><span data-stu-id="ae549-150">What we need toodo is toocreate 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="ae549-151">Biz bu PowerShell ile gerçekleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae549-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="ae549-152">İlk olarak, PowerShell ortamımızda ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="ae549-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="ae549-153">Ardından, hello aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ae549-153">Then, run hello following PowerShell command:</span></span>

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="ae549-154">Şimdi 10 uç noktaları oluşturduk ve aynı eğitilen model eğitilmiş hello içerirler *customer001.csv*.</span><span class="sxs-lookup"><span data-stu-id="ae549-154">Now we've created 10 endpoints and they all contain hello same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="ae549-155">Bunları hello Azure Yönetim Portalı görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae549-155">You can view them in hello Azure Management Portal.</span></span>

![Görüntü](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a><span data-ttu-id="ae549-157">PowerShell kullanarak hello uç noktaları toouse ayrı eğitim veri kümelerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ae549-157">Update hello endpoints toouse separate training datasets using PowerShell</span></span>
<span data-ttu-id="ae549-158">Merhaba sonraki tooupdate hello uç benzersiz olarak her müşterinin ayrı veri üzerinde eğitilmiş modeller ile adımdır.</span><span class="sxs-lookup"><span data-stu-id="ae549-158">hello next step is tooupdate hello endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="ae549-159">Ancak tooproduce hello Bu modellerden ilk ihtiyacımız **bisiklet kiralama eğitim** web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ae549-159">But first we need tooproduce these models from hello **Bike Rental Training** web service.</span></span> <span data-ttu-id="ae549-160">Geri toohello edelim **bisiklet kiralama eğitim** web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ae549-160">Let's go back toohello **Bike Rental Training** web service.</span></span> <span data-ttu-id="ae549-161">Kendi BES noktayla 10 kez sipariş tooproduce 10 farklı modelleri 10 farklı eğitim kümelerinde toocall ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="ae549-161">We need toocall its BES endpoint 10 times with 10 different training datasets in order tooproduce 10 different models.</span></span> <span data-ttu-id="ae549-162">Merhaba kullanacağız **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo bu.</span><span class="sxs-lookup"><span data-stu-id="ae549-162">We'll use hello **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo this.</span></span>

<span data-ttu-id="ae549-163">Blob depolama hesabınız için tooprovide kimlik bilgileri gerekir `$configContent`, yani, hello alanlarındaki `AccountName`, `AccountKey` ve `RelativeLocation`.</span><span class="sxs-lookup"><span data-stu-id="ae549-163">You will also need tooprovide credentials for your blob storage account into `$configContent`, namely, at hello fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="ae549-164">Merhaba `AccountName` hello görüldüğü gibi hesap adlarını biri olabilir **Klasik Azure Yönetim Portalı** (*depolama* sekmesi).</span><span class="sxs-lookup"><span data-stu-id="ae549-164">hello `AccountName` can be one of your account names, as seen in hello **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="ae549-165">Bir depolama hesabında tıkladığınızda, `AccountKey` tuşuna basarak hello tarafından bulunabilir **erişim anahtarlarını Yönet** hello alt ve hello kopyalama düğmesini *birincil erişim anahtarını*.</span><span class="sxs-lookup"><span data-stu-id="ae549-165">Once you click on a storage account, its `AccountKey` can be found by pressing hello **Manage Access Keys** button at hello bottom and copying hello *Primary Access Key*.</span></span> <span data-ttu-id="ae549-166">Merhaba `RelativeLocation` yeni bir model depolanacağı hello yolu göreli tooyour depolama değil.</span><span class="sxs-lookup"><span data-stu-id="ae549-166">hello `RelativeLocation` is hello path relative tooyour storage where a new model will be stored.</span></span> <span data-ttu-id="ae549-167">Örneği için hello yolu `hai/retrain/bike_rental/` adlı noktaları tooa kapsayıcı aşağıda hello betikteki `hai`, ve `/retrain/bike_rental/` alt klasörler.</span><span class="sxs-lookup"><span data-stu-id="ae549-167">For instance, hello path `hai/retrain/bike_rental/` in hello script below points tooa container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="ae549-168">Şu anda, alt klasörler hello portalı kullanıcı Arabirimi üzerinden oluşturamaz, ancak vardır [birkaç Azure depolama gezginleri](../storage/common/storage-explorers.md) olanak tanıyacak şekilde toodo şekilde.</span><span class="sxs-lookup"><span data-stu-id="ae549-168">Currently, you cannot create subfolders through hello portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you toodo so.</span></span> <span data-ttu-id="ae549-169">Yeni bir kapsayıcı, depolama toostore hello yeni eğitilmiş modeller (.ilearner dosyaları) şu şekilde oluşturmanız önerilir: hello üzerinde depolama sayfanızdan tıklatın **Ekle** düğmesini hello altındaki ve adlandırın `retrain`.</span><span class="sxs-lookup"><span data-stu-id="ae549-169">It is recommended that you create a new container in your storage toostore hello new trained models (.ilearner files) as follows: from your storage page, click on hello **Add** button at hello bottom and name it `retrain`.</span></span> <span data-ttu-id="ae549-170">Özet olarak, hello gerekli değişiklikleri toohello aşağıdaki komut dosyası ilgilidir çok`AccountName`, `AccountKey` ve `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="ae549-170">In summary, hello necassary changes toohello script below pertain too`AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> <span data-ttu-id="ae549-171">Merhaba BES endpoint hello modu bu işlem için yalnızca desteklenir. ' dir.</span><span class="sxs-lookup"><span data-stu-id="ae549-171">hello BES endpoint is hello only supported mode for this operation.</span></span> <span data-ttu-id="ae549-172">RRS eğitilmiş modeller üretmek için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="ae549-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="ae549-173">10 farklı BES iş yapılandırma json dosyalarını oluşturmak yerine, yukarıda gördüğünüz gibi biz dinamik olarak hello yapılandırma dizesi oluşturun ve toohello akış *jobConfigString* hello parametresinin  **InvokeAmlWebServceBESEndpoint** disk üzerinde bir kopyasını gerçekten gerek tookeep olduğundan cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ae549-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create hello config string instead and feed it toohello *jobConfigString* parameter of hello **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need tookeep a copy on disk.</span></span>

<span data-ttu-id="ae549-174">Her şey yolunda giderse, bir süre sonra 10 .ilearner dosyaları, gelen görmelisiniz *model001.ilearner* çok*model010.ilearner*, Azure depolama hesabınızdaki.</span><span class="sxs-lookup"><span data-stu-id="ae549-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* too*model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="ae549-175">Hazır tooupdate ki artık web Puanlama bizim 10 uç noktaları hello kullanarak bu modeller ile hizmet **düzeltme eki AmlWebServiceEndpoint** PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ae549-175">Now we're ready tooupdate our 10 scoring web service endpoints with these models using hello **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="ae549-176">Yeniden biz yalnızca hello varsayılan olmayan uç noktaları programlı olarak daha önce oluşturduğumuz düzeltme eki olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ae549-176">Remember again that we can only patch hello non-default endpoints we programmatically created earlier.</span></span>

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="ae549-177">Bu oldukça hızlı bir şekilde çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae549-177">This should run fairly quickly.</span></span> <span data-ttu-id="ae549-178">Merhaba yürütme sona erdiğinde, başarılı bir şekilde 10 Tahmine dayalı web hizmeti uç noktaları, her biri benzersiz şekilde hello dataset belirli tooa kiralama konumdan, tüm tek eğitim denemenizi üzerinde eğitilmiş bir modeli içeren oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="ae549-178">When hello execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on hello dataset specific tooa rental location, all from a single training experiment.</span></span> <span data-ttu-id="ae549-179">tooverify bunu hello kullanarak bu uç noktalarını çağırma deneyebilirsiniz **InvokeAmlWebServiceRRSEndpoint** cmdlet, bunları sağlama hello ile aynı verileri girin ve hello modelleri olduğundan toosee farklı tahmin sonuçlarını beklemeniz gerekir farklı eğitim kümeleriyle eğitildi.</span><span class="sxs-lookup"><span data-stu-id="ae549-179">tooverify this, you can try calling these endpoints using hello **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with hello same input data, and you should expect toosee different prediction results since hello models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="ae549-180">Tam PowerShell Betiği</span><span class="sxs-lookup"><span data-stu-id="ae549-180">Full PowerShell script</span></span>
<span data-ttu-id="ae549-181">Merhaba tam kaynak kodu hello listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="ae549-181">Here's hello listing of hello full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
