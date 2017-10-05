---
title: Bir Azure Machine Learning Web hizmetini kullanma | Microsoft Docs
description: "Machine learning hizmeti dağıtıldıktan sonra gerçek zamanlı istek-yanıt hizmeti veya toplu yürütme hizmeti olarak kullanılabilir hale getirileceğini RESTFul Web hizmeti tüketilebilir."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: eec9f637b4b2306ab4a888dbd5ef5b9a021bcac5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-consume-an-azure-machine-learning-web-service"></a><span data-ttu-id="2160c-103">Bir Azure Machine Learning Web hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="2160c-103">How to consume an Azure Machine Learning Web service</span></span>

<span data-ttu-id="2160c-104">Bir Azure Machine Learning Tahmine dayalı modeli bir Web hizmeti olarak dağıttığınızda, veri göndermek ve Öngörüler elde etmek için bir REST API'si kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2160c-104">Once you deploy an Azure Machine Learning predictive model as a Web service, you can use a REST API to send it data and get predictions.</span></span> <span data-ttu-id="2160c-105">Gerçek zamanlı veya toplu iş modunda veriler gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="2160c-105">You can send the data in real-time or in batch mode.</span></span>

<span data-ttu-id="2160c-106">Oluştur ve buraya Machine Learning Studio kullanarak bir Machine Learning Web hizmetini dağıtma hakkında daha fazla bilgi bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2160c-106">You can find more information about how to create and deploy a Machine Learning Web service using Machine Learning Studio here:</span></span>

* <span data-ttu-id="2160c-107">Machine Learning Studio'da bir deneme oluşturma konusunda bir öğretici için bkz: [ilk denemenizi oluşturma](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="2160c-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="2160c-108">Web hizmetinin nasıl dağıtılacağı hakkında daha fazla bilgi için bkz: [Machine Learning Web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="2160c-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="2160c-109">Machine Learning hakkında daha fazla bilgi için genel olarak, ziyaret [Machine Learning Belge Merkezi](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="2160c-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="2160c-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2160c-110">Overview</span></span>
<span data-ttu-id="2160c-111">Azure Machine Learning Web hizmeti ile bir dış uygulama Machine Learning bir iş akışı Puanlama modeli ile gerçek zamanlı iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="2160c-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="2160c-112">Bir Machine Learning Web hizmeti çağrısı bir dış uygulamaya tahmin sonuçlarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="2160c-112">A Machine Learning Web service call returns prediction results to an external application.</span></span> <span data-ttu-id="2160c-113">Bir Machine Learning Web hizmeti çağrısı yapmak için bir tahmini dağıttığınızda oluşturduğunuz bir API anahtarı geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2160c-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="2160c-114">Machine Learning Web hizmeti web programlama projeleri için popüler bir mimari seçimi olan REST'i temel alır.</span><span class="sxs-lookup"><span data-stu-id="2160c-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="2160c-115">Azure Machine Learning iki tür hizmet içerir:</span><span class="sxs-lookup"><span data-stu-id="2160c-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="2160c-116">İstek-yanıt hizmeti (RRS) – düşük gecikme, Machine Learning Studio'dan oluşturulan ve dağıtılan durum bilgisi olmayan modellere bir arabirim sağlayan yüksek düzeyde ölçeklenebilir hizmet.</span><span class="sxs-lookup"><span data-stu-id="2160c-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span></span>
* <span data-ttu-id="2160c-117">Toplu yürütme hizmeti (BES) – zaman uyumsuz bir hizmet veri kayıtları için toplu iş yapan.</span><span class="sxs-lookup"><span data-stu-id="2160c-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="2160c-118">Machine Learning Web Hizmetleri hakkında daha fazla bilgi için bkz: [Machine Learning Web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="2160c-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="2160c-119">Bir Azure Machine Learning yetkilendirme anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="2160c-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="2160c-120">API anahtarları denemenizi dağıttığınızda, Web hizmeti için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2160c-120">When you deploy your experiment, API keys are generated for the Web service.</span></span> <span data-ttu-id="2160c-121">Anahtarları çeşitli konumlardan alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2160c-121">You can retrieve the keys from several locations.</span></span>

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="2160c-122">Microsoft Azure Machine Learning Web Hizmetleri Portalı'ndan</span><span class="sxs-lookup"><span data-stu-id="2160c-122">From the Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="2160c-123">Oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="2160c-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="2160c-124">Yeni Machine Learning Web hizmeti için API anahtarı almak için:</span><span class="sxs-lookup"><span data-stu-id="2160c-124">To retrieve the API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="2160c-125">Azure Machine Learning Web Hizmetleri Portalı'nda tıklatın **Web Hizmetleri** üst menü.</span><span class="sxs-lookup"><span data-stu-id="2160c-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span></span>
2. <span data-ttu-id="2160c-126">Anahtar almak istediğiniz Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2160c-126">Click the Web service for which you want to retrieve the key.</span></span>
3. <span data-ttu-id="2160c-127">Üst menüsünde **Tüket**.</span><span class="sxs-lookup"><span data-stu-id="2160c-127">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="2160c-128">Kopyalayıp kaydedin **birincil anahtar**.</span><span class="sxs-lookup"><span data-stu-id="2160c-128">Copy and save the **Primary Key**.</span></span>

<span data-ttu-id="2160c-129">Klasik Machine Learning Web hizmeti için API anahtarı almak için:</span><span class="sxs-lookup"><span data-stu-id="2160c-129">To retrieve the API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="2160c-130">Azure Machine Learning Web Hizmetleri Portalı'nda tıklatın **Klasik Web Hizmetleri** üst menü.</span><span class="sxs-lookup"><span data-stu-id="2160c-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span></span>
2. <span data-ttu-id="2160c-131">Çalıştığınız Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2160c-131">Click the Web service with which you are working.</span></span>
3. <span data-ttu-id="2160c-132">Anahtar almak istediğiniz uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2160c-132">Click the endpoint for which you want to retrieve the key.</span></span>
4. <span data-ttu-id="2160c-133">Üst menüsünde **Tüket**.</span><span class="sxs-lookup"><span data-stu-id="2160c-133">On the top menu, click **Consume**.</span></span>
5. <span data-ttu-id="2160c-134">Kopyalayıp kaydedin **birincil anahtar**.</span><span class="sxs-lookup"><span data-stu-id="2160c-134">Copy and save the **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="2160c-135">Klasik Web hizmeti</span><span class="sxs-lookup"><span data-stu-id="2160c-135">Classic Web service</span></span>
 <span data-ttu-id="2160c-136">Klasik Web hizmeti için bir anahtar, Machine Learning Studio veya Azure Klasik portalından da alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2160c-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or the Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="2160c-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="2160c-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="2160c-138">Machine Learning Studio'da tıklatın **WEB Hizmetleri** soldaki.</span><span class="sxs-lookup"><span data-stu-id="2160c-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span></span>
2. <span data-ttu-id="2160c-139">Bir Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2160c-139">Click a Web service.</span></span> <span data-ttu-id="2160c-140">**API anahtarı** açık **PANO** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2160c-140">The **API key** is on the **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="2160c-141">Klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="2160c-141">Azure classic portal</span></span>
1. <span data-ttu-id="2160c-142">Tıklatın **MACHINE LEARNING** soldaki.</span><span class="sxs-lookup"><span data-stu-id="2160c-142">Click **MACHINE LEARNING** on the left.</span></span>
2. <span data-ttu-id="2160c-143">Web hizmetiniz bulunduğu çalışma alanına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2160c-143">Click the workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="2160c-144">Tıklatın **WEB Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="2160c-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="2160c-145">Bir Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2160c-145">Click a Web service.</span></span>
5. <span data-ttu-id="2160c-146">Bir uç nokta'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2160c-146">Click an endpoint.</span></span> <span data-ttu-id="2160c-147">Sağ alt köşesindeki "API anahtarı" çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="2160c-147">The “API KEY” is down at the lower-right.</span></span>

## <span data-ttu-id="2160c-148"><a id="connect"></a>Bir Machine Learning Web hizmetine bağlanma</span><span class="sxs-lookup"><span data-stu-id="2160c-148"><a id="connect"></a>Connect to a Machine Learning Web service</span></span>
<span data-ttu-id="2160c-149">HTTP istek ve yanıt destekleyen herhangi bir programlama dili kullanılarak bir Machine Learning Web hizmetine bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2160c-149">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="2160c-150">C#, Python ve R örnekler bir Machine Learning Web hizmeti Yardım sayfasından görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2160c-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="2160c-151">**Machine Learning API Yardım** Machine Learning API'si Yardım Web hizmetini dağıttığınızda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2160c-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="2160c-152">Bkz: [Azure Machine Learning izlenecek dağıtımı Web hizmeti](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="2160c-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="2160c-153">Machine Learning API'si Yardım tahmin Web hizmeti hakkındaki ayrıntıları içerir.</span><span class="sxs-lookup"><span data-stu-id="2160c-153">The Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="2160c-154">Çalıştığınız Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2160c-154">Click the Web service with which you are working.</span></span>
2. <span data-ttu-id="2160c-155">API Yardım sayfasında görüntülemek istediğiniz uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2160c-155">Click the endpoint for which you want to view the API Help Page.</span></span>
3. <span data-ttu-id="2160c-156">Üst menüsünde **Tüket**.</span><span class="sxs-lookup"><span data-stu-id="2160c-156">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="2160c-157">Tıklatın **API Yardım sayfası** istek-yanıt ya da toplu iş yürütme bitiş noktaları altında.</span><span class="sxs-lookup"><span data-stu-id="2160c-157">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="2160c-158">**Machine Learning API görünümüne yeni Web hizmeti için Yardım**</span><span class="sxs-lookup"><span data-stu-id="2160c-158">**To view Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="2160c-159">Web Hizmetleri portalı Azure Machine Learning içinde:</span><span class="sxs-lookup"><span data-stu-id="2160c-159">In the Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="2160c-160">Tıklatın **WEB Hizmetleri** üst menüsünde.</span><span class="sxs-lookup"><span data-stu-id="2160c-160">Click **WEB SERVICES** on the top menu.</span></span>
2. <span data-ttu-id="2160c-161">Anahtar almak istediğiniz Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2160c-161">Click the Web service for which you want to retrieve the key.</span></span>

<span data-ttu-id="2160c-162">Tıklatın **Tüket** URI'ler isteği Reposonse ve toplu yürütme Hizmetleri ve örnek kod için C#, R ve Python almak için.</span><span class="sxs-lookup"><span data-stu-id="2160c-162">Click **Consume** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="2160c-163">Tıklatın **Swagger API'si** Swagger almak için sağlanan URI'ler API çağrısı için belgelerine bağlı.</span><span class="sxs-lookup"><span data-stu-id="2160c-163">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="2160c-164">C# örnek</span><span class="sxs-lookup"><span data-stu-id="2160c-164">C# Sample</span></span>
<span data-ttu-id="2160c-165">Bir Machine Learning Web hizmetine bağlanmak için bir **HttpClient** ScoreData geçirme.</span><span class="sxs-lookup"><span data-stu-id="2160c-165">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="2160c-166">ScoreData bir FeatureVector ScoreData temsil eden bir n boyutlu vektörü sayısal özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="2160c-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="2160c-167">Machine Learning hizmetine bir API anahtarı ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="2160c-167">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="2160c-168">Machine Learning Web hizmetine bağlanmak için **Microsoft.AspNet.WebApi.Client** NuGet paketi yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2160c-168">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="2160c-169">**Microsoft.AspNet.WebApi.Client NuGet Visual Studio yükleme**</span><span class="sxs-lookup"><span data-stu-id="2160c-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="2160c-170">UCI indirme kümesinden yayımlama: yetişkin 2 sınıfı dataset Web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="2160c-170">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="2160c-171">**Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2160c-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="2160c-172">Seçin **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="2160c-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="2160c-173">**Kod örneği çalıştırmak için**</span><span class="sxs-lookup"><span data-stu-id="2160c-173">**To run the code sample**</span></span>

1. <span data-ttu-id="2160c-174">Yayımla "Örnek 1: dataset UCI indirin: yetişkin 2 sınıfı dataset" deneme, Machine Learning örnek koleksiyonunun bir parçası.</span><span class="sxs-lookup"><span data-stu-id="2160c-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="2160c-175">Apikey ile yapılan bir Web hizmetinden anahtarla atayın.</span><span class="sxs-lookup"><span data-stu-id="2160c-175">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="2160c-176">Bkz: **bir Azure Machine Learning yetkilendirme anahtarı alma** üstünde.</span><span class="sxs-lookup"><span data-stu-id="2160c-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="2160c-177">İstek URI'si ile serviceUri atayın.</span><span class="sxs-lookup"><span data-stu-id="2160c-177">Assign serviceUri with the Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="2160c-178">Python örneği</span><span class="sxs-lookup"><span data-stu-id="2160c-178">Python Sample</span></span>
<span data-ttu-id="2160c-179">Bir Machine Learning Web hizmetine bağlanmak için **urllib2** ScoreData geçirme kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="2160c-179">To connect to a Machine Learning Web service, use the **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="2160c-180">ScoreData bir FeatureVector ScoreData temsil eden bir n boyutlu vektörü sayısal özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="2160c-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="2160c-181">Machine Learning hizmetine bir API anahtarı ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="2160c-181">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="2160c-182">**Kod örneği çalıştırmak için**</span><span class="sxs-lookup"><span data-stu-id="2160c-182">**To run the code sample**</span></span>

1. <span data-ttu-id="2160c-183">Dağıtma "Örnek 1: dataset UCI indirin: yetişkin 2 sınıfı dataset" deneme, Machine Learning örnek koleksiyonunun bir parçası.</span><span class="sxs-lookup"><span data-stu-id="2160c-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="2160c-184">Apikey ile yapılan bir Web hizmetinden anahtarla atayın.</span><span class="sxs-lookup"><span data-stu-id="2160c-184">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="2160c-185">Bkz: **bir Azure Machine Learning yetkilendirme anahtarı alma** başına bir kısmına bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="2160c-185">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span></span>
3. <span data-ttu-id="2160c-186">İstek URI'si ile serviceUri atayın.</span><span class="sxs-lookup"><span data-stu-id="2160c-186">Assign serviceUri with the Request URI.</span></span>

