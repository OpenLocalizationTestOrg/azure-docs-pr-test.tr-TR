---
title: Machine Learning Web hizmeti aaaConnect tooa | Microsoft Docs
description: "C# veya Python ile tooan Azure Machine Learning Web hizmeti yetkilendirme anahtarı kullanarak bağlanın."
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
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a><span data-ttu-id="b47e3-103">Tooan Azure Machine Learning Web hizmetine bağlanma</span><span class="sxs-lookup"><span data-stu-id="b47e3-103">Connect tooan Azure Machine Learning Web Service</span></span>
<span data-ttu-id="b47e3-104">Hello Azure Machine Learning geliştirici deneyimi, bir Web hizmeti API toomake tahminleri giriş verilerinden gerçek zamanlı veya toplu iş modunda olur.</span><span class="sxs-lookup"><span data-stu-id="b47e3-104">hello Azure Machine Learning developer experience is a Web service API toomake predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="b47e3-105">Azure Machine Learning Studio toocreate tahminleri kullanın ve bir Azure Machine Learning Web hizmetini dağıtma.</span><span class="sxs-lookup"><span data-stu-id="b47e3-105">You use Azure Machine Learning Studio toocreate predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="b47e3-106">toolearn konusunda toocreate ve Machine Learning Studio kullanarak bir Machine Learning Web hizmetini dağıtma:</span><span class="sxs-lookup"><span data-stu-id="b47e3-106">toolearn about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="b47e3-107">Toocreate Machine Learning Studio'da bir denemeyi nasıl görürüm üzerinde bir öğretici için [ilk denemenizi oluşturma](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="b47e3-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="b47e3-108">Ayrıntılar için toodeploy bir Web hizmeti bkz [Machine Learning Web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="b47e3-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="b47e3-109">Genel olarak, hello Machine Learning hakkında daha fazla bilgi için ziyaret [Machine Learning Belge Merkezi](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="b47e3-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="b47e3-110">Azure Machine Learning Web hizmeti</span><span class="sxs-lookup"><span data-stu-id="b47e3-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="b47e3-111">Hello Azure Machine Learning Web hizmeti ile bir dış uygulama Machine Learning bir iş akışı Puanlama modeli ile gerçek zamanlı iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="b47e3-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="b47e3-112">Bir Machine Learning Web hizmeti çağrısı tooan dış uygulama tahmin sonuçlarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="b47e3-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="b47e3-113">toomake bir Machine Learning Web hizmeti çağrısı, tahmin dağıttığınızda oluşturduğunuz bir API anahtarı geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b47e3-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="b47e3-114">Merhaba Machine Learning Web hizmeti web programlama projeleri için popüler bir mimari seçimi olan REST'i temel alır.</span><span class="sxs-lookup"><span data-stu-id="b47e3-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="b47e3-115">Azure Machine Learning iki tür hizmet içerir:</span><span class="sxs-lookup"><span data-stu-id="b47e3-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="b47e3-116">İstek-yanıt hizmeti (RRS) – düşük gecikme süresi, oluşturulan ve dağıtılan hello Machine Learning Studio toohello durum bilgisi olmayan modellere bir arabirim sağlayan yüksek düzeyde ölçeklenebilir hizmet.</span><span class="sxs-lookup"><span data-stu-id="b47e3-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="b47e3-117">Toplu yürütme hizmeti (BES) – zaman uyumsuz bir hizmet veri kayıtları için toplu iş yapan.</span><span class="sxs-lookup"><span data-stu-id="b47e3-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="b47e3-118">Machine Learning Web Hizmetleri hakkında daha fazla bilgi için bkz: [Machine Learning Web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="b47e3-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="b47e3-119">Bir Azure Machine Learning yetkilendirme anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="b47e3-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="b47e3-120">Denemenizi dağıttığınızda, API anahtarları hello Web hizmeti için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b47e3-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="b47e3-121">Merhaba anahtarları çeşitli konumlardan alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b47e3-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="b47e3-122">Merhaba Microsoft Azure Machine Learning Web Hizmetleri Portalı'ndan</span><span class="sxs-lookup"><span data-stu-id="b47e3-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="b47e3-123">İçinde toohello oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="b47e3-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="b47e3-124">Yeni Machine Learning Web hizmeti için tooretrieve hello API anahtarı:</span><span class="sxs-lookup"><span data-stu-id="b47e3-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="b47e3-125">Hello Azure Machine Learning Web Hizmetleri Portalı'nda tıklatın **Web Hizmetleri** hello üst menü.</span><span class="sxs-lookup"><span data-stu-id="b47e3-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="b47e3-126">Merhaba Web hizmeti tooretrieve hello anahtar istediğiniz'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="b47e3-127">Merhaba üst menüsünde **Tüket**.</span><span class="sxs-lookup"><span data-stu-id="b47e3-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="b47e3-128">Kopyalayın ve hello kaydedin **birincil anahtar**.</span><span class="sxs-lookup"><span data-stu-id="b47e3-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="b47e3-129">tooretrieve hello API anahtarı Klasik Machine Learning Web hizmeti için:</span><span class="sxs-lookup"><span data-stu-id="b47e3-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="b47e3-130">Hello Azure Machine Learning Web Hizmetleri Portalı'nda tıklatın **Klasik Web Hizmetleri** hello üst menü.</span><span class="sxs-lookup"><span data-stu-id="b47e3-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="b47e3-131">Merhaba Web hizmeti ile çalıştığınız'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="b47e3-132">Tooretrieve hello anahtar istediğiniz hello uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="b47e3-133">Merhaba üst menüsünde **Tüket**.</span><span class="sxs-lookup"><span data-stu-id="b47e3-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="b47e3-134">Kopyalayın ve hello kaydedin **birincil anahtar**.</span><span class="sxs-lookup"><span data-stu-id="b47e3-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="b47e3-135">Klasik Web hizmeti</span><span class="sxs-lookup"><span data-stu-id="b47e3-135">Classic Web service</span></span>
 <span data-ttu-id="b47e3-136">Klasik Web hizmeti için bir anahtar, Machine Learning Studio veya hello Klasik Azure portalı de alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b47e3-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="b47e3-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="b47e3-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="b47e3-138">Machine Learning Studio'da tıklatın **WEB Hizmetleri** hello soldaki.</span><span class="sxs-lookup"><span data-stu-id="b47e3-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="b47e3-139">Bir Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-139">Click a Web service.</span></span> <span data-ttu-id="b47e3-140">Merhaba **API anahtarı** hello üzerinde olduğu **PANO** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="b47e3-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="b47e3-141">Klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="b47e3-141">Azure classic portal</span></span>
1. <span data-ttu-id="b47e3-142">Tıklatın **MACHINE LEARNING** hello soldaki.</span><span class="sxs-lookup"><span data-stu-id="b47e3-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="b47e3-143">Web hizmetiniz bulunduğu hello çalışma alanını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="b47e3-144">Tıklatın **WEB Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="b47e3-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="b47e3-145">Bir Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-145">Click a Web service.</span></span>
5. <span data-ttu-id="b47e3-146">Bir uç nokta'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-146">Click an endpoint.</span></span> <span data-ttu-id="b47e3-147">sağ alt hello Hello "API anahtarı" çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="b47e3-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="b47e3-148"><a id="connect"></a>Tooa Machine Learning Web hizmetine bağlanın</span><span class="sxs-lookup"><span data-stu-id="b47e3-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="b47e3-149">Tooa Machine Learning Web hizmeti, HTTP istek ve yanıt destekleyen herhangi bir programlama dili kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b47e3-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="b47e3-150">C#, Python ve R örnekler bir Machine Learning Web hizmeti Yardım sayfasından görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b47e3-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="b47e3-151">**Machine Learning API Yardım** Machine Learning API'si Yardım Web hizmetini dağıttığınızda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b47e3-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="b47e3-152">Bkz: [Azure Machine Learning izlenecek dağıtımı Web hizmeti](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="b47e3-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="b47e3-153">Merhaba Machine Learning API'si Yardım tahmin Web hizmeti hakkındaki ayrıntıları içerir.</span><span class="sxs-lookup"><span data-stu-id="b47e3-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="b47e3-154">Merhaba Web hizmeti ile çalıştığınız'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="b47e3-155">Tooview hello API Yardım sayfasında istediğiniz hello uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="b47e3-156">Merhaba üst menüsünde **Tüket**.</span><span class="sxs-lookup"><span data-stu-id="b47e3-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="b47e3-157">Tıklatın **API Yardım sayfası** hello istek-yanıt ya da toplu iş yürütme bitiş noktaları altında.</span><span class="sxs-lookup"><span data-stu-id="b47e3-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="b47e3-158">**tooview Machine Learning API'si yardımcı olmak için yeni Web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="b47e3-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="b47e3-159">Hello Azure Machine Learning Web Hizmetleri portalı:</span><span class="sxs-lookup"><span data-stu-id="b47e3-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="b47e3-160">Tıklatın **WEB Hizmetleri** hello üst menüsünde.</span><span class="sxs-lookup"><span data-stu-id="b47e3-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="b47e3-161">Merhaba Web hizmeti tooretrieve hello anahtar istediğiniz'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="b47e3-162">Tıklatın **Tüket** tooget hello isteği Reposonse ve toplu yürütme Hizmetleri ve örnek kodda C#, R ve Python için URI hello.</span><span class="sxs-lookup"><span data-stu-id="b47e3-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="b47e3-163">Tıklatın **Swagger API'si** tooget hello API'leri için temel belgelere adlı hello Swagger sağlanan URI.</span><span class="sxs-lookup"><span data-stu-id="b47e3-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="b47e3-164">C# örnek</span><span class="sxs-lookup"><span data-stu-id="b47e3-164">C# Sample</span></span>
<span data-ttu-id="b47e3-165">tooconnect tooa Machine Learning Web hizmeti kullanan bir **HttpClient** ScoreData geçirme.</span><span class="sxs-lookup"><span data-stu-id="b47e3-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="b47e3-166">ScoreData bir FeatureVector hello ScoreData temsil eden bir n boyutlu vektörü sayısal özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="b47e3-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="b47e3-167">Bir API anahtarı ile toohello Machine Learning hizmetinin kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="b47e3-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="b47e3-168">tooconnect tooa Machine Learning Web hizmeti hello **Microsoft.AspNet.WebApi.Client** NuGet paketi yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b47e3-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="b47e3-169">**Microsoft.AspNet.WebApi.Client NuGet Visual Studio yükleme**</span><span class="sxs-lookup"><span data-stu-id="b47e3-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="b47e3-170">Yayımlama Hello indirme UCI kümesinden: yetişkin 2 sınıfı dataset Web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="b47e3-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="b47e3-171">**Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="b47e3-172">Seçin **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="b47e3-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="b47e3-173">**toorun hello kod örneği**</span><span class="sxs-lookup"><span data-stu-id="b47e3-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="b47e3-174">Yayımla "Örnek 1: dataset UCI indirin: yetişkin 2 sınıfı dataset" deneme, hello Machine Learning örnek koleksiyonunun bir parçası.</span><span class="sxs-lookup"><span data-stu-id="b47e3-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="b47e3-175">Apikey ile yapılan bir Web hizmetinden hello anahtarla atayın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="b47e3-176">Bkz: **bir Azure Machine Learning yetkilendirme anahtarı alma** üstünde.</span><span class="sxs-lookup"><span data-stu-id="b47e3-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="b47e3-177">Merhaba istek URI'si ile serviceUri atayın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="b47e3-178">Python örneği</span><span class="sxs-lookup"><span data-stu-id="b47e3-178">Python Sample</span></span>
<span data-ttu-id="b47e3-179">tooconnect tooa Machine Learning Web hizmeti kullanmak hello **urllib2** ScoreData geçirme kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="b47e3-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="b47e3-180">ScoreData bir FeatureVector hello ScoreData temsil eden bir n boyutlu vektörü sayısal özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="b47e3-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="b47e3-181">Bir API anahtarı ile toohello Machine Learning hizmetinin kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="b47e3-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="b47e3-182">**toorun hello kod örneği**</span><span class="sxs-lookup"><span data-stu-id="b47e3-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="b47e3-183">Dağıtma "Örnek 1: dataset UCI indirin: yetişkin 2 sınıfı dataset" deneme, hello Machine Learning örnek koleksiyonunun bir parçası.</span><span class="sxs-lookup"><span data-stu-id="b47e3-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="b47e3-184">Apikey ile yapılan bir Web hizmetinden hello anahtarla atayın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="b47e3-185">Merhaba bkz **bir Azure Machine Learning yetkilendirme anahtarı alma** hello başına bir kısmına bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="b47e3-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="b47e3-186">Merhaba istek URI'si ile serviceUri atayın.</span><span class="sxs-lookup"><span data-stu-id="b47e3-186">Assign serviceUri with hello Request URI.</span></span>

