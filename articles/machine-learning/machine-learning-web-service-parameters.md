---
title: Azure Machine Learning Web hizmeti parametreleri aaaUse | Microsoft Docs
description: "Nasıl toouse Azure Machine Learning Web hizmeti parametreleri toomodify hello modelinizi davranışını hello web hizmeti erişildiğinde."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a><span data-ttu-id="f4d22-103">Azure Machine Learning Web Hizmeti Parametrelerini kullanma</span><span class="sxs-lookup"><span data-stu-id="f4d22-103">Use Azure Machine Learning Web Service Parameters</span></span>
<span data-ttu-id="f4d22-104">Bir Azure Machine Learning web hizmetini yapılandırılabilir parametrelerle modülleri içeren bir denemeyi yayımlayarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f4d22-104">An Azure Machine Learning web service is created by publishing an experiment that contains modules with configurable parameters.</span></span> <span data-ttu-id="f4d22-105">Bazı durumlarda, Hello web hizmeti çalışırken toochange hello modülü davranışı isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4d22-105">In some cases, you may want toochange hello module behavior while hello web service is running.</span></span> <span data-ttu-id="f4d22-106">*Web hizmeti parametreleri* toodo izin bu görev.</span><span class="sxs-lookup"><span data-stu-id="f4d22-106">*Web Service Parameters* allow you toodo this task.</span></span> 

<span data-ttu-id="f4d22-107">Yaygın bir örnek hello ayarı [veri içeri aktarma] [ reader] hello web hizmeti erişildiğinde web hizmeti, bu hello kullanıcıyı hello yayımlanan şekilde modülü farklı bir veri kaynağına belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4d22-107">A common example is setting up hello [Import Data][reader] module so that hello user of hello published web service can specify a different data source when hello web service is accessed.</span></span> <span data-ttu-id="f4d22-108">Veya hello yapılandırma [verileri dışa aktar] [ writer] modülü böylece farklı bir hedef belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="f4d22-108">Or configuring hello [Export Data][writer] module so that a different destination can be specified.</span></span> <span data-ttu-id="f4d22-109">Bazı diğer hello BITS hello sayısını değiştirme örnekler [özellik karma] [ feature-hashing] hello için istenen özelliklerini modül veya hello sayısı [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] modülü.</span><span class="sxs-lookup"><span data-stu-id="f4d22-109">Some other examples include changing hello number of bits for hello [Feature Hashing][feature-hashing] module or hello number of desired features for hello [Filter-Based Feature Selection][filter-based-feature-selection] module.</span></span> 

<span data-ttu-id="f4d22-110">Web hizmeti parametreleri ayarlayabilir ve bunları bir veya daha fazla modülü parametrelerle denemenizde ilişkilendirmeyi ve gerekli veya isteğe bağlı oldukları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4d22-110">You can set Web Service Parameters and associate them with one or more module parameters in your experiment, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="f4d22-111">Merhaba web hizmetini çağırdığınızda hello kullanıcı hello web hizmetinin bu parametreler için değerler sonra sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="f4d22-111">hello user of hello web service can then provide values for these parameters when they call hello web service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a><span data-ttu-id="f4d22-112">Nasıl tooset ve kullanım Web hizmeti parametreleri</span><span class="sxs-lookup"><span data-stu-id="f4d22-112">How tooset and use Web Service Parameters</span></span>
<span data-ttu-id="f4d22-113">Bir modül hello simgesi sonraki toohello parametresi tıklatıp "web hizmeti parametresi Ayarla" seçerek bir Web hizmeti parametre tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="f4d22-113">You define a Web Service Parameter by clicking hello icon next toohello parameter for a module and selecting "Set as web service parameter".</span></span> <span data-ttu-id="f4d22-114">Bu yeni bir Web hizmeti parametre oluşturur ve toothat modülü parametre bağlanır.</span><span class="sxs-lookup"><span data-stu-id="f4d22-114">This creates a new Web Service Parameter and connects it toothat module parameter.</span></span> <span data-ttu-id="f4d22-115">Sonra hello web hizmeti erişildiğinde hello kullanıcı hello Web hizmeti parametresi için bir değer belirtebilirsiniz ve uygulanan toohello modülü parametresi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f4d22-115">Then, when hello web service is accessed, hello user can specify a value for hello Web Service Parameter and it is applied toohello module parameter.</span></span>

<span data-ttu-id="f4d22-116">Bir Web hizmeti parametresi tanımladıktan sonra kullanılabilir tooany olan hello deneme başka bir modül parametre.</span><span class="sxs-lookup"><span data-stu-id="f4d22-116">Once you define a Web Service Parameter, it's available tooany other module parameter in hello experiment.</span></span> <span data-ttu-id="f4d22-117">Bir modül için bir parametre ile ilişkili bir Web hizmeti parametresi tanımlarsanız, aynı değerini yazın hello hello parametre bekliyor sürece, aynı Web hizmeti parametresi diğer herhangi bir modül için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4d22-117">If you define a Web Service Parameter associated with a parameter for one module, you can use that same Web Service Parameter for any other module, as long as hello parameter expects hello same type of value.</span></span> <span data-ttu-id="f4d22-118">Merhaba Web hizmeti parametresi bir sayısal değer ise, örneğin, daha sonra yalnızca sayısal bir değer beklediğiniz modülü parametreleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f4d22-118">For example, if hello Web Service Parameter is a numeric value, then it can only be used for module parameters that expect a numeric value.</span></span> <span data-ttu-id="f4d22-119">Merhaba kullanıcı hello Web hizmeti parametresi için bir değer ayarlar ilişkili uygulanan tooall modülü parametreleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f4d22-119">When hello user sets a value for hello Web Service Parameter, it will be applied tooall associated module parameters.</span></span>

<span data-ttu-id="f4d22-120">Karar verebilirsiniz tooprovide varsayılan hello Web hizmeti parametresi için değer olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="f4d22-120">You can decide whether tooprovide a default value for hello Web Service Parameter.</span></span> <span data-ttu-id="f4d22-121">Ardından Merhaba varsa parametre hello web hizmeti hello kullanıcı için isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f4d22-121">If you do, then hello parameter is optional for hello user of hello web service.</span></span> <span data-ttu-id="f4d22-122">Varsayılan değer sağlamazsanız, hello web hizmeti erişildiğinde hello kullanıcı gerekli tooenter bir değer ise.</span><span class="sxs-lookup"><span data-stu-id="f4d22-122">If you don't provide a default value, then hello user is required tooenter a value when hello web service is accessed.</span></span>

<span data-ttu-id="f4d22-123">Merhaba hello web hizmeti için API belgeleri nasıl toospecify hello Web hizmeti parametresi program aracılığıyla hello web hizmeti erişirken üzerinde hello web hizmeti kullanıcı için bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="f4d22-123">hello API documentation for hello web service includes information for hello web service user on how toospecify hello Web Service Parameter programmatically when accessing hello web service.</span></span>

> [!NOTE]
> <span data-ttu-id="f4d22-124">Merhaba sağlanan bir Klasik web hizmeti için API belgelerine hello **API Yardım sayfası** hello web hizmeti bağlantı **PANO** Machine Learning Studio'da.</span><span class="sxs-lookup"><span data-stu-id="f4d22-124">hello API documentation for a classic web service is provided through hello **API help page** link in hello web service **DASHBOARD** in Machine Learning Studio.</span></span> <span data-ttu-id="f4d22-125">Yeni bir web hizmeti ile Merhaba sağlanan için API belgelerine hello [Azure Machine Learning Web Hizmetleri](https://services.azureml.net/Quickstart) hello portalını **Tüket** ve **Swagger API'si** için sayfaları, Web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="f4d22-125">hello API documentation for a new web service is provided through hello [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portal on hello **Consume** and **Swagger API** pages for your web service.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="f4d22-126">Örnek</span><span class="sxs-lookup"><span data-stu-id="f4d22-126">Example</span></span>
<span data-ttu-id="f4d22-127">Bir örnek, bir deneme ile sahibiz varsayalım bir [verileri dışa aktar] [ writer] bilgi tooAzure blob depolamaya gönderir modülü.</span><span class="sxs-lookup"><span data-stu-id="f4d22-127">As an example, let's assume we have an experiment with an [Export Data][writer] module that sends information tooAzure blob storage.</span></span> <span data-ttu-id="f4d22-128">Web hizmeti "yol Blob" adlı bir parametre tanımlama olasılığınız yüksektir hello hizmet erişildiğinde hello web hizmeti kullanıcı toochange hello yolu toohello blob depolama veren.</span><span class="sxs-lookup"><span data-stu-id="f4d22-128">We'll define a Web Service Parameter named "Blob path" that allows hello web service user toochange hello path toohello blob storage when hello service is accessed.</span></span>

1. <span data-ttu-id="f4d22-129">Machine Learning Studio'da hello tıklatın [verileri dışa aktar] [ writer] modülü tooselect.</span><span class="sxs-lookup"><span data-stu-id="f4d22-129">In Machine Learning Studio, click hello [Export Data][writer] module tooselect it.</span></span> <span data-ttu-id="f4d22-130">Itanium tabanlı sistemler için hello Özellikler bölmesinde toohello hello deneme tuvalinin sağında içinde özelliklerini gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f4d22-130">Its properties are shown in hello Properties pane toohello right of hello experiment canvas.</span></span>
2. <span data-ttu-id="f4d22-131">Merhaba depolama türünü belirtin:</span><span class="sxs-lookup"><span data-stu-id="f4d22-131">Specify hello storage type:</span></span>
   
   * <span data-ttu-id="f4d22-132">Altında **Lütfen verileri hedef belirtin**, "Azure Blob Storage" seçin.</span><span class="sxs-lookup"><span data-stu-id="f4d22-132">Under **Please specify data destination**, select "Azure Blob Storage".</span></span>
   * <span data-ttu-id="f4d22-133">Altında **Lütfen kimlik doğrulama türünü belirtin**, "Hesap" seçin.</span><span class="sxs-lookup"><span data-stu-id="f4d22-133">Under **Please specify authentication type**, select "Account".</span></span>
   * <span data-ttu-id="f4d22-134">Hello Azure blob depolama için Hello hesap bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="f4d22-134">Enter hello account information for hello Azure blob storage.</span></span> 
     <p /><span data-ttu-id="f4d22-135">
3.Merhaba simgesi toohello hello sağına tıklayın **kapsayıcı parametresi tooblob başlayan yol**.</span><span class="sxs-lookup"><span data-stu-id="f4d22-135">
3. Click hello icon toohello right of hello **Path tooblob beginning with container parameter**.</span></span> <span data-ttu-id="f4d22-136">Şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="f4d22-136">It looks like this:</span></span>
   
   ![Web hizmeti parametresi simgesi][icon]
   
   <span data-ttu-id="f4d22-138">"Web hizmeti parametresi Ayarla" seçin.</span><span class="sxs-lookup"><span data-stu-id="f4d22-138">Select "Set as web service parameter".</span></span>
   
   <span data-ttu-id="f4d22-139">Bir giriş altında eklenen **Web hizmeti parametreleri** hello Özellikler bölmesinde hello adı "yol tooblob ile başlayan kapsayıcı" Merhaba sonundaki.</span><span class="sxs-lookup"><span data-stu-id="f4d22-139">An entry is added under **Web Service Parameters** at hello bottom of hello Properties pane with hello name "Path tooblob beginning with container".</span></span> <span data-ttu-id="f4d22-140">Merhaba artık Web hizmeti parametresi budur bununla ilişkili [verileri dışa aktar] [ writer] modülü parametresi.</span><span class="sxs-lookup"><span data-stu-id="f4d22-140">This is hello Web Service Parameter that is now associated with this [Export Data][writer] module parameter.</span></span>
4. <span data-ttu-id="f4d22-141">toorename Web hizmeti parametresi Merhaba, hello adına tıklayın, "yol Blob" girin ve basın hello **Enter** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="f4d22-141">toorename hello Web Service Parameter, click hello name, enter "Blob path", and press hello **Enter** key.</span></span> 
5. <span data-ttu-id="f4d22-142">tooprovide hello Web hizmeti parametresi için varsayılan bir değer hello simgesi toohello hello adını sağ tıklatın, "varsayılan değer sağla" seçin, bir değer (örneğin, "container1/output1.csv") girin ve basın hello **Enter** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="f4d22-142">tooprovide a default value for hello Web Service Parameter, click hello icon toohello right of hello name, select "Provide default value", enter a value (for example, "container1/output1.csv"), and press hello **Enter** key.</span></span>
   
   ![Web hizmeti parametresi][parameter]
6. <span data-ttu-id="f4d22-144">**Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f4d22-144">Click **Run**.</span></span> 
7. <span data-ttu-id="f4d22-145">Tıklatın **Web hizmeti Dağıt** seçip **Web hizmeti Dağıt [Klasik]** veya **Web hizmeti dağıtma [Yeni]** toodeploy hello web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="f4d22-145">Click **Deploy Web Service** and select **Deploy Web Service [Classic]** or **Deploy Web Service [New]** toodeploy hello web service.</span></span>

> [!NOTE] 
> <span data-ttu-id="f4d22-146">toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4d22-146">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="f4d22-147">Daha fazla bilgi için [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="f4d22-147">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="f4d22-148">Merhaba web hizmetinin Hello kullanıcı artık hello için yeni bir hedef belirtin [verileri dışa aktar] [ writer] hello web hizmeti erişirken modülü.</span><span class="sxs-lookup"><span data-stu-id="f4d22-148">hello user of hello web service can now specify a new destination for hello [Export Data][writer] module when accessing hello web service.</span></span>

## <a name="more-information"></a><span data-ttu-id="f4d22-149">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="f4d22-149">More information</span></span>
<span data-ttu-id="f4d22-150">Merhaba daha ayrıntılı bir örnek için bkz: [Web hizmeti parametreleri](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) hello girişi [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4d22-150">For a more detailed example, see hello [Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entry in hello [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span></span>

<span data-ttu-id="f4d22-151">Machine Learning web hizmetine erişim ile ilgili daha fazla bilgi için bkz: [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="f4d22-151">For more information on accessing a Machine Learning web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

