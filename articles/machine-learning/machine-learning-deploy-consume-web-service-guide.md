---
title: "Azure Machine Learning Web Hizmetleri: Dağıtım ve kullanım | Microsoft Docs"
description: "Dağıtma ve web hizmetlerini tüketen kaynaklar."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="3edfb-103">Azure Machine Learning Web Hizmetleri: Dağıtım ve kullanım</span><span class="sxs-lookup"><span data-stu-id="3edfb-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="3edfb-104">Azure Machine Learning toodeploy machine learning iş akışları ve modelleri web Hizmetleri olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3edfb-104">You can use Azure Machine Learning toodeploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="3edfb-105">Bu web hizmetleri hello Internet toodo tahminlerin gerçek zamanlı veya toplu iş modunda üzerinden kullanılan toocall hello machine learning modellerini uygulamalardan sonra olabilir.</span><span class="sxs-lookup"><span data-stu-id="3edfb-105">These web services can then be used toocall hello machine-learning models from applications over hello Internet toodo predictions in real time or in batch mode.</span></span> <span data-ttu-id="3edfb-106">Merhaba web hizmetleri RESTful olduğundan, bunları çeşitli programlama dillerini ve .NET ve Java gibi platformları ve Excel gibi uygulamalardan çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3edfb-106">Because hello web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="3edfb-107">bağlantılar toowalkthroughs, kodu ve belgeler toohelp başlamanıza yardımcı Hello sonraki bölümlerde verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3edfb-107">hello next sections provide links toowalkthroughs, code, and documentation toohelp get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="3edfb-108">Bir web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="3edfb-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="3edfb-109">Azure Machine Learning Studio ile</span><span class="sxs-lookup"><span data-stu-id="3edfb-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="3edfb-110">Machine Learning Studio ve hello Microsoft Azure Machine Learning Web Hizmetleri portalı dağıtmak ve bir web hizmeti kod yazmadan yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="3edfb-110">Machine Learning Studio and hello Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="3edfb-111">Merhaba aşağıdaki bağlantılar sağlar hakkında genel bilgi toodeploy yeni bir web hizmeti:</span><span class="sxs-lookup"><span data-stu-id="3edfb-111">hello following links provide general Information about how toodeploy a new web service:</span></span>

* <span data-ttu-id="3edfb-112">Azure kaynak yöneticiyi temel alan yeni bir web hizmeti toodeploy nasıl görürüm hakkında genel bir bakış için [yeni bir web hizmetini dağıtma](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="3edfb-112">For an overview about how toodeploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="3edfb-113">Gözden geçirme konusunda toodeploy bir web hizmeti bkz [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="3edfb-113">For a walkthrough about how toodeploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="3edfb-114">Tam bir gözden geçirme konusunda toocreate ve bir web hizmetini dağıtma, bkz: [gözden geçirme adım 1: Machine Learning çalışma alanı oluşturma](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="3edfb-114">For a full walkthrough about how toocreate and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="3edfb-115">Bir web hizmetini dağıtma belirli örnekler için bkz:</span><span class="sxs-lookup"><span data-stu-id="3edfb-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="3edfb-116">Gözden geçirme adım 5: hello Azure Machine Learning web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="3edfb-116">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="3edfb-117">Nasıl toodeploy bir web hizmeti toomultiple bölgeleri</span><span class="sxs-lookup"><span data-stu-id="3edfb-117">How toodeploy a web service toomultiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="3edfb-118">Web Hizmetleri kaynak sağlayıcı API'leri (Azure Resource Manager API'leri)</span><span class="sxs-lookup"><span data-stu-id="3edfb-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="3edfb-119">web hizmetleri için Hello Azure Machine Learning kaynak sağlayıcısı REST API çağrısı kullanarak dağıtım ve Yönetim web hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="3edfb-119">hello Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="3edfb-120">Daha fazla bilgi için bkz: [Machine Learning Web hizmeti (REST)](/rest/api/machinelearning/index) başvurusu.</span><span class="sxs-lookup"><span data-stu-id="3edfb-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="3edfb-121">PowerShell cmdlet'leri ile</span><span class="sxs-lookup"><span data-stu-id="3edfb-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="3edfb-122">Azure Machine Learning kaynak sağlayıcısı web hizmetleri için dağıtım ve Yönetim web hizmetleri PowerShell cmdlet'lerini kullanarak etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="3edfb-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="3edfb-123">toouse hello cmdlet'leri, gerekir ilk tooyour hello PowerShell ortamında Azure hesabından hello kullanarak oturum [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3edfb-123">toouse hello cmdlets, you must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="3edfb-124">İle hakkında bilginiz yoksa, nasıl toocall PowerShell komutları dayalı kaynak yöneticisi için bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="3edfb-124">If you are unfamiliar with how toocall PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="3edfb-125">tooexport, Tahmine dayalı denemeler, kullanın [Bu örnek kod](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="3edfb-125">tooexport your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="3edfb-126">Merhaba koddan hello .exe dosyasını oluşturduktan sonra yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3edfb-126">After you create hello .exe file from hello code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="3edfb-127">Merhaba uygulaması çalıştıran bir web hizmeti JSON şablonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3edfb-127">Running hello application creates a web service JSON template.</span></span> <span data-ttu-id="3edfb-128">toouse hello şablonu toodeploy bir web hizmeti, aşağıdaki bilgilerle hello eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3edfb-128">toouse hello template toodeploy a web service, you must add hello following information:</span></span>

* <span data-ttu-id="3edfb-129">Depolama hesabı adı ve anahtar</span><span class="sxs-lookup"><span data-stu-id="3edfb-129">Storage account name and key</span></span>

    <span data-ttu-id="3edfb-130">Ya da hello hello depolama hesabı adı ve anahtarınızı edinin [Azure portal](https://portal.azure.com/) veya hello [Klasik Azure portalı](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="3edfb-130">You can get hello storage account name and key from either hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="3edfb-131">Taahhüt plan kimliği</span><span class="sxs-lookup"><span data-stu-id="3edfb-131">Commitment plan ID</span></span>

    <span data-ttu-id="3edfb-132">Hello hello planı kodu alabilirsiniz [Azure Machine Learning Web Hizmetleri](https://services.azureml.net) oturum açma ve bir plan adı tıklatarak portal.</span><span class="sxs-lookup"><span data-stu-id="3edfb-132">You can get hello plan ID from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="3edfb-133">Bunları toohello JSON şablonunu hello alt öğeleri olarak Ekle *özellikleri* hello düğümde aynı düzeydeki hello *MachineLearningWorkspace* düğümü.</span><span class="sxs-lookup"><span data-stu-id="3edfb-133">Add them toohello JSON template as children of hello *Properties* node at hello same level as hello *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="3edfb-134">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3edfb-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="3edfb-135">Makaleler hello bakın ve kod ek ayrıntılar için örnek:</span><span class="sxs-lookup"><span data-stu-id="3edfb-135">See hello following articles and sample code for additional details:</span></span>

* <span data-ttu-id="3edfb-136">[Azure Machine Learning cmdlet'lerini](https://msdn.microsoft.com/library/azure/mt767952.aspx) MSDN'de başvurusu</span><span class="sxs-lookup"><span data-stu-id="3edfb-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="3edfb-137">Örnek [izlenecek](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) github'da</span><span class="sxs-lookup"><span data-stu-id="3edfb-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-hello-web-services"></a><span data-ttu-id="3edfb-138">Merhaba web hizmetlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="3edfb-138">Consume hello web services</span></span>
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="3edfb-139">Azure Machine Learning Web Hizmetleri kullanıcı Arabirimi (test) Hello</span><span class="sxs-lookup"><span data-stu-id="3edfb-139">From hello Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="3edfb-140">Web hizmetiniz hello Azure Machine Learning Web Hizmetleri Portalı'ndan test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3edfb-140">You can test your web service from hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="3edfb-141">Bu test hello istek-yanıt hizmeti (RRS) içerir ve toplu yürütme hizmeti (BES) arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="3edfb-141">This includes testing hello Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="3edfb-142">Yeni bir web hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="3edfb-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="3edfb-143">Bir Azure Machine Learning web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="3edfb-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="3edfb-144">Gözden geçirme adım 5: hello Azure Machine Learning web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="3edfb-144">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="3edfb-145">Excel'den</span><span class="sxs-lookup"><span data-stu-id="3edfb-145">From Excel</span></span>
<span data-ttu-id="3edfb-146">Merhaba web hizmeti tüketen Excel şablonunu indirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3edfb-146">You can download an Excel template that consumes hello web service:</span></span>

* [<span data-ttu-id="3edfb-147">Bir Azure Machine Learning web hizmetini Excel'den kullanma</span><span class="sxs-lookup"><span data-stu-id="3edfb-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="3edfb-148">Azure Machine Learning Web Hizmetleri için Excel Eklentisi</span><span class="sxs-lookup"><span data-stu-id="3edfb-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="3edfb-149">REST tabanlı bir istemciden</span><span class="sxs-lookup"><span data-stu-id="3edfb-149">From a REST-based client</span></span>
<span data-ttu-id="3edfb-150">Azure Machine Learning Web Hizmetleri RESTful API'lerini ' dir.</span><span class="sxs-lookup"><span data-stu-id="3edfb-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="3edfb-151">.NET, Python, R, Java, vb. hello gibi çeşitli platformlarda bu API'lerden tüketebileceği **Tüket** hello üzerinde web hizmeti için sayfa [Microsoft Azure Machine Learning Web Hizmetleri portalı](https://services.azureml.net) örnek içeriyor yardımcı olabilecek kod Başlarken.</span><span class="sxs-lookup"><span data-stu-id="3edfb-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. hello **Consume** page for your web service on hello [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="3edfb-152">Daha fazla bilgi için bkz: [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="3edfb-152">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
