---
title: "Bir Machine Learning Web hizmetine bağlanma | Microsoft Docs"
description: "C# veya Python ile bir yetkilendirme anahtarı kullanarak bir Azure Machine Learning Web hizmetine bağlanın."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: TRUE
ms.openlocfilehash: 0fc6c7e921b18eb14a95fb737d8fb5ab5cc7e687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-an-azure-machine-learning-web-service"></a><span data-ttu-id="5dc94-103">Azure Machine Learning Web Hizmetine bağlanma</span><span class="sxs-lookup"><span data-stu-id="5dc94-103">Connect to an Azure Machine Learning Web Service</span></span>
<span data-ttu-id="5dc94-104">Azure Machine Learning geliştirici deneyimi tahminleri giriş verilerinden gerçek zamanlı veya toplu iş modunda yapmak için bir Web hizmeti API'dır.</span><span class="sxs-lookup"><span data-stu-id="5dc94-104">The Azure Machine Learning developer experience is a Web service API to make predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="5dc94-105">Azure Machine Learning Studio tahminleri oluşturmak ve bir Azure Machine Learning Web hizmeti dağıtmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-105">You use Azure Machine Learning Studio to create predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="5dc94-106">Oluşturma ve Machine Learning Studio kullanarak bir Machine Learning Web hizmetini dağıtma hakkında bilgi edinmek için:</span><span class="sxs-lookup"><span data-stu-id="5dc94-106">To learn about how to create and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="5dc94-107">Machine Learning Studio'da bir deneme oluşturma konusunda bir öğretici için bkz: [ilk denemenizi oluşturma](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="5dc94-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="5dc94-108">Web hizmetinin nasıl dağıtılacağı hakkında daha fazla bilgi için bkz: [Machine Learning Web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="5dc94-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="5dc94-109">Machine Learning hakkında daha fazla bilgi için genel olarak, ziyaret [Machine Learning Belge Merkezi](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="5dc94-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="5dc94-110">Azure Machine Learning Web hizmeti</span><span class="sxs-lookup"><span data-stu-id="5dc94-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="5dc94-111">Azure Machine Learning Web hizmeti ile bir dış uygulama Machine Learning bir iş akışı Puanlama modeli ile gerçek zamanlı iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="5dc94-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="5dc94-112">Bir Machine Learning Web hizmeti çağrısı bir dış uygulamaya tahmin sonuçlarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="5dc94-112">A Machine Learning Web service call returns prediction results to an external application.</span></span> <span data-ttu-id="5dc94-113">Bir Machine Learning Web hizmeti çağrısı yapmak için bir tahmini dağıttığınızda oluşturduğunuz bir API anahtarı geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dc94-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="5dc94-114">Machine Learning Web hizmeti web programlama projeleri için popüler bir mimari seçimi olan REST'i temel alır.</span><span class="sxs-lookup"><span data-stu-id="5dc94-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="5dc94-115">Azure Machine Learning iki tür hizmet içerir:</span><span class="sxs-lookup"><span data-stu-id="5dc94-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="5dc94-116">İstek-yanıt hizmeti (RRS) – düşük gecikme, Machine Learning Studio'dan oluşturulan ve dağıtılan durum bilgisi olmayan modellere bir arabirim sağlayan yüksek düzeyde ölçeklenebilir hizmet.</span><span class="sxs-lookup"><span data-stu-id="5dc94-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span></span>
* <span data-ttu-id="5dc94-117">Toplu yürütme hizmeti (BES) – zaman uyumsuz bir hizmet veri kayıtları için toplu iş yapan.</span><span class="sxs-lookup"><span data-stu-id="5dc94-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="5dc94-118">Machine Learning Web Hizmetleri hakkında daha fazla bilgi için bkz: [Machine Learning Web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="5dc94-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="5dc94-119">Bir Azure Machine Learning yetkilendirme anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="5dc94-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="5dc94-120">API anahtarları denemenizi dağıttığınızda, Web hizmeti için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5dc94-120">When you deploy your experiment, API keys are generated for the Web service.</span></span> <span data-ttu-id="5dc94-121">Anahtarları çeşitli konumlardan alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dc94-121">You can retrieve the keys from several locations.</span></span>

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="5dc94-122">Microsoft Azure Machine Learning Web Hizmetleri Portalı'ndan</span><span class="sxs-lookup"><span data-stu-id="5dc94-122">From the Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="5dc94-123">Oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="5dc94-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="5dc94-124">Yeni Machine Learning Web hizmeti için API anahtarı almak için:</span><span class="sxs-lookup"><span data-stu-id="5dc94-124">To retrieve the API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="5dc94-125">Azure Machine Learning Web Hizmetleri Portalı'nda tıklatın **Web Hizmetleri** üst menü.</span><span class="sxs-lookup"><span data-stu-id="5dc94-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span></span>
2. <span data-ttu-id="5dc94-126">Anahtar almak istediğiniz Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-126">Click the Web service for which you want to retrieve the key.</span></span>
3. <span data-ttu-id="5dc94-127">Üst menüsünde **Tüket**.</span><span class="sxs-lookup"><span data-stu-id="5dc94-127">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="5dc94-128">Kopyalayıp kaydedin **birincil anahtar**.</span><span class="sxs-lookup"><span data-stu-id="5dc94-128">Copy and save the **Primary Key**.</span></span>

<span data-ttu-id="5dc94-129">Klasik Machine Learning Web hizmeti için API anahtarı almak için:</span><span class="sxs-lookup"><span data-stu-id="5dc94-129">To retrieve the API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="5dc94-130">Azure Machine Learning Web Hizmetleri Portalı'nda tıklatın **Klasik Web Hizmetleri** üst menü.</span><span class="sxs-lookup"><span data-stu-id="5dc94-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span></span>
2. <span data-ttu-id="5dc94-131">Çalıştığınız Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-131">Click the Web service with which you are working.</span></span>
3. <span data-ttu-id="5dc94-132">Anahtar almak istediğiniz uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-132">Click the endpoint for which you want to retrieve the key.</span></span>
4. <span data-ttu-id="5dc94-133">Üst menüsünde **Tüket**.</span><span class="sxs-lookup"><span data-stu-id="5dc94-133">On the top menu, click **Consume**.</span></span>
5. <span data-ttu-id="5dc94-134">Kopyalayıp kaydedin **birincil anahtar**.</span><span class="sxs-lookup"><span data-stu-id="5dc94-134">Copy and save the **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="5dc94-135">Klasik Web hizmeti</span><span class="sxs-lookup"><span data-stu-id="5dc94-135">Classic Web service</span></span>
 <span data-ttu-id="5dc94-136">Klasik Web hizmeti için bir anahtar, Machine Learning Studio veya Azure Klasik portalından da alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dc94-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or the Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="5dc94-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5dc94-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="5dc94-138">Machine Learning Studio'da tıklatın **WEB Hizmetleri** soldaki.</span><span class="sxs-lookup"><span data-stu-id="5dc94-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span></span>
2. <span data-ttu-id="5dc94-139">Bir Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-139">Click a Web service.</span></span> <span data-ttu-id="5dc94-140">**API anahtarı** açık **PANO** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5dc94-140">The **API key** is on the **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="5dc94-141">Klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="5dc94-141">Azure classic portal</span></span>
1. <span data-ttu-id="5dc94-142">Tıklatın **MACHINE LEARNING** soldaki.</span><span class="sxs-lookup"><span data-stu-id="5dc94-142">Click **MACHINE LEARNING** on the left.</span></span>
2. <span data-ttu-id="5dc94-143">Web hizmetiniz bulunduğu çalışma alanına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-143">Click the workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="5dc94-144">Tıklatın **WEB Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="5dc94-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="5dc94-145">Bir Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-145">Click a Web service.</span></span>
5. <span data-ttu-id="5dc94-146">Bir uç nokta'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-146">Click an endpoint.</span></span> <span data-ttu-id="5dc94-147">Sağ alt köşesindeki "API anahtarı" çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="5dc94-147">The “API KEY” is down at the lower-right.</span></span>

## <span data-ttu-id="5dc94-148"><a id="connect"></a>Bir Machine Learning Web hizmetine bağlanma</span><span class="sxs-lookup"><span data-stu-id="5dc94-148"><a id="connect"></a>Connect to a Machine Learning Web service</span></span>
<span data-ttu-id="5dc94-149">HTTP istek ve yanıt destekleyen herhangi bir programlama dili kullanılarak bir Machine Learning Web hizmetine bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5dc94-149">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="5dc94-150">C#, Python ve R örnekler bir Machine Learning Web hizmeti Yardım sayfasından görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dc94-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="5dc94-151">**Machine Learning API Yardım** Machine Learning API'si Yardım Web hizmetini dağıttığınızda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5dc94-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="5dc94-152">Bkz: [Azure Machine Learning izlenecek dağıtımı Web hizmeti](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="5dc94-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="5dc94-153">Machine Learning API'si Yardım tahmin Web hizmeti hakkındaki ayrıntıları içerir.</span><span class="sxs-lookup"><span data-stu-id="5dc94-153">The Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="5dc94-154">Çalıştığınız Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-154">Click the Web service with which you are working.</span></span>
2. <span data-ttu-id="5dc94-155">API Yardım sayfasında görüntülemek istediğiniz uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-155">Click the endpoint for which you want to view the API Help Page.</span></span>
3. <span data-ttu-id="5dc94-156">Üst menüsünde **Tüket**.</span><span class="sxs-lookup"><span data-stu-id="5dc94-156">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="5dc94-157">Tıklatın **API Yardım sayfası** istek-yanıt ya da toplu iş yürütme bitiş noktaları altında.</span><span class="sxs-lookup"><span data-stu-id="5dc94-157">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="5dc94-158">**Machine Learning API görünümüne yeni Web hizmeti için Yardım**</span><span class="sxs-lookup"><span data-stu-id="5dc94-158">**To view Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="5dc94-159">Web Hizmetleri portalı Azure Machine Learning içinde:</span><span class="sxs-lookup"><span data-stu-id="5dc94-159">In the Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="5dc94-160">Tıklatın **WEB Hizmetleri** üst menüsünde.</span><span class="sxs-lookup"><span data-stu-id="5dc94-160">Click **WEB SERVICES** on the top menu.</span></span>
2. <span data-ttu-id="5dc94-161">Anahtar almak istediğiniz Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-161">Click the Web service for which you want to retrieve the key.</span></span>

<span data-ttu-id="5dc94-162">Tıklatın **Tüket** URI'ler isteği Reposonse ve toplu yürütme Hizmetleri ve örnek kod için C#, R ve Python almak için.</span><span class="sxs-lookup"><span data-stu-id="5dc94-162">Click **Consume** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="5dc94-163">Tıklatın **Swagger API'si** Swagger almak için sağlanan URI'ler API çağrısı için belgelerine bağlı.</span><span class="sxs-lookup"><span data-stu-id="5dc94-163">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="5dc94-164">C# örnek</span><span class="sxs-lookup"><span data-stu-id="5dc94-164">C# Sample</span></span>
<span data-ttu-id="5dc94-165">Bir Machine Learning Web hizmetine bağlanmak için bir **HttpClient** ScoreData geçirme.</span><span class="sxs-lookup"><span data-stu-id="5dc94-165">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="5dc94-166">ScoreData bir FeatureVector ScoreData temsil eden bir n boyutlu vektörü sayısal özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="5dc94-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="5dc94-167">Machine Learning hizmetine bir API anahtarı ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="5dc94-167">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="5dc94-168">Machine Learning Web hizmetine bağlanmak için **Microsoft.AspNet.WebApi.Client** NuGet paketi yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5dc94-168">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="5dc94-169">**Microsoft.AspNet.WebApi.Client NuGet Visual Studio yükleme**</span><span class="sxs-lookup"><span data-stu-id="5dc94-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="5dc94-170">UCI indirme kümesinden yayımlama: yetişkin 2 sınıfı dataset Web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="5dc94-170">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="5dc94-171">**Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="5dc94-172">Seçin **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="5dc94-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="5dc94-173">**Kod örneği çalıştırmak için**</span><span class="sxs-lookup"><span data-stu-id="5dc94-173">**To run the code sample**</span></span>

1. <span data-ttu-id="5dc94-174">Yayımla "Örnek 1: dataset UCI indirin: yetişkin 2 sınıfı dataset" deneme, Machine Learning örnek koleksiyonunun bir parçası.</span><span class="sxs-lookup"><span data-stu-id="5dc94-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="5dc94-175">Apikey ile yapılan bir Web hizmetinden anahtarla atayın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-175">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="5dc94-176">Bkz: **bir Azure Machine Learning yetkilendirme anahtarı alma** üstünde.</span><span class="sxs-lookup"><span data-stu-id="5dc94-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="5dc94-177">İstek URI'si ile serviceUri atayın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-177">Assign serviceUri with the Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="5dc94-178">Python örneği</span><span class="sxs-lookup"><span data-stu-id="5dc94-178">Python Sample</span></span>
<span data-ttu-id="5dc94-179">Bir Machine Learning Web hizmetine bağlanmak için **urllib2** ScoreData geçirme kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="5dc94-179">To connect to a Machine Learning Web service, use the **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="5dc94-180">ScoreData bir FeatureVector ScoreData temsil eden bir n boyutlu vektörü sayısal özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="5dc94-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="5dc94-181">Machine Learning hizmetine bir API anahtarı ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="5dc94-181">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="5dc94-182">**Kod örneği çalıştırmak için**</span><span class="sxs-lookup"><span data-stu-id="5dc94-182">**To run the code sample**</span></span>

1. <span data-ttu-id="5dc94-183">Dağıtma "Örnek 1: dataset UCI indirin: yetişkin 2 sınıfı dataset" deneme, Machine Learning örnek koleksiyonunun bir parçası.</span><span class="sxs-lookup"><span data-stu-id="5dc94-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="5dc94-184">Apikey ile yapılan bir Web hizmetinden anahtarla atayın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-184">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="5dc94-185">Bkz: **bir Azure Machine Learning yetkilendirme anahtarı alma** başına bir kısmına bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="5dc94-185">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span></span>
3. <span data-ttu-id="5dc94-186">İstek URI'si ile serviceUri atayın.</span><span class="sxs-lookup"><span data-stu-id="5dc94-186">Assign serviceUri with the Request URI.</span></span>

