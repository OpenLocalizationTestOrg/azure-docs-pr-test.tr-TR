---
title: Azure Machine Learning Web hizmeti parametreleri kullanarak | Microsoft Docs
description: "Web hizmeti erişilen modelinizin davranışını değiştirmek için Azure Machine Learning Web hizmeti parametreleri kullanma"
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
ms.openlocfilehash: 482726c1dae5385964e08b720e529817d5907537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a><span data-ttu-id="38cbc-103">Azure Machine Learning Web Hizmeti Parametrelerini kullanma</span><span class="sxs-lookup"><span data-stu-id="38cbc-103">Use Azure Machine Learning Web Service Parameters</span></span>
<span data-ttu-id="38cbc-104">Bir Azure Machine Learning web hizmetini yapılandırılabilir parametrelerle modülleri içeren bir denemeyi yayımlayarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="38cbc-104">An Azure Machine Learning web service is created by publishing an experiment that contains modules with configurable parameters.</span></span> <span data-ttu-id="38cbc-105">Bazı durumlarda, web hizmetinin çalıştığı sırada modülü davranışı değiştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38cbc-105">In some cases, you may want to change the module behavior while the web service is running.</span></span> <span data-ttu-id="38cbc-106">*Web hizmeti parametreleri* bu görevi yapmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="38cbc-106">*Web Service Parameters* allow you to do this task.</span></span> 

<span data-ttu-id="38cbc-107">Yaygın bir örnek ayarlama [veri içeri aktarma] [ reader] modülü böylece web hizmeti erişildiğinde yayımlanan web hizmeti kullanıcı farklı bir veri kaynağına belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38cbc-107">A common example is setting up the [Import Data][reader] module so that the user of the published web service can specify a different data source when the web service is accessed.</span></span> <span data-ttu-id="38cbc-108">Veya yapılandırma [verileri dışa aktar] [ writer] modülü böylece farklı bir hedef belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="38cbc-108">Or configuring the [Export Data][writer] module so that a different destination can be specified.</span></span> <span data-ttu-id="38cbc-109">Bazı diğer BITS sayısını değiştirme örnekler [özellik karma] [ feature-hashing] modül veya sayısı istenen özellikleri [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] modülü.</span><span class="sxs-lookup"><span data-stu-id="38cbc-109">Some other examples include changing the number of bits for the [Feature Hashing][feature-hashing] module or the number of desired features for the [Filter-Based Feature Selection][filter-based-feature-selection] module.</span></span> 

<span data-ttu-id="38cbc-110">Web hizmeti parametreleri ayarlayabilir ve bunları bir veya daha fazla modülü parametrelerle denemenizde ilişkilendirmeyi ve gerekli veya isteğe bağlı oldukları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38cbc-110">You can set Web Service Parameters and associate them with one or more module parameters in your experiment, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="38cbc-111">Web hizmeti çağırdığınızda web hizmeti kullanıcı ardından bu parametreler için değerler sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="38cbc-111">The user of the web service can then provide values for these parameters when they call the web service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-to-set-and-use-web-service-parameters"></a><span data-ttu-id="38cbc-112">Ayarlama ve Web hizmeti parametreleri kullanma</span><span class="sxs-lookup"><span data-stu-id="38cbc-112">How to set and use Web Service Parameters</span></span>
<span data-ttu-id="38cbc-113">Parametresi için bir modül yanındaki simgeyi tıklatarak ve "web hizmeti parametresi Ayarla" seçerek bir Web hizmeti parametre tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="38cbc-113">You define a Web Service Parameter by clicking the icon next to the parameter for a module and selecting "Set as web service parameter".</span></span> <span data-ttu-id="38cbc-114">Bu yeni bir Web hizmeti parametre oluşturur ve bu modülü parametreye bağlanır.</span><span class="sxs-lookup"><span data-stu-id="38cbc-114">This creates a new Web Service Parameter and connects it to that module parameter.</span></span> <span data-ttu-id="38cbc-115">Ardından, web hizmeti erişildiğinde kullanıcı Web hizmeti parametresi için bir değer belirtebilir ve modülü parametresi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="38cbc-115">Then, when the web service is accessed, the user can specify a value for the Web Service Parameter and it is applied to the module parameter.</span></span>

<span data-ttu-id="38cbc-116">Bir Web hizmeti parametresi tanımladıktan sonra başka bir modül parametre denemede için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="38cbc-116">Once you define a Web Service Parameter, it's available to any other module parameter in the experiment.</span></span> <span data-ttu-id="38cbc-117">Bir modül için bir parametre ile ilişkili bir Web hizmeti parametresi tanımlarsanız, aynı türde bir değer parametresini beklemektedir sürece, aynı Web hizmeti parametresi diğer herhangi bir modül için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38cbc-117">If you define a Web Service Parameter associated with a parameter for one module, you can use that same Web Service Parameter for any other module, as long as the parameter expects the same type of value.</span></span> <span data-ttu-id="38cbc-118">Web hizmeti parametresi bir sayısal değer ise, örneğin, daha sonra yalnızca sayısal bir değer beklediğiniz modülü parametreleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="38cbc-118">For example, if the Web Service Parameter is a numeric value, then it can only be used for module parameters that expect a numeric value.</span></span> <span data-ttu-id="38cbc-119">Kullanıcı Web hizmeti parametresi için bir değer ayarlar, tüm ilişkilendirilmiş modülü parametreleri uygulanır.</span><span class="sxs-lookup"><span data-stu-id="38cbc-119">When the user sets a value for the Web Service Parameter, it will be applied to all associated module parameters.</span></span>

<span data-ttu-id="38cbc-120">Web hizmeti parametresi için varsayılan bir değer sağlamak karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38cbc-120">You can decide whether to provide a default value for the Web Service Parameter.</span></span> <span data-ttu-id="38cbc-121">Bunu yaparsanız, parametre web hizmeti kullanıcı için isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="38cbc-121">If you do, then the parameter is optional for the user of the web service.</span></span> <span data-ttu-id="38cbc-122">Varsayılan değer sağlamazsanız, kullanıcı web hizmeti erişildiğinde bir değer girmesini gereklidir.</span><span class="sxs-lookup"><span data-stu-id="38cbc-122">If you don't provide a default value, then the user is required to enter a value when the web service is accessed.</span></span>

<span data-ttu-id="38cbc-123">Web hizmeti için API belgeleri web hizmeti kullanıcı için Web hizmeti parametresi program aracılığıyla web hizmeti erişirken nasıl belirtileceği hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="38cbc-123">The API documentation for the web service includes information for the web service user on how to specify the Web Service Parameter programmatically when accessing the web service.</span></span>

> [!NOTE]
> <span data-ttu-id="38cbc-124">Klasik web hizmeti için API belgeleri sağlanır **API Yardım sayfası** web hizmeti bağlantı **PANO** Machine Learning Studio'da.</span><span class="sxs-lookup"><span data-stu-id="38cbc-124">The API documentation for a classic web service is provided through the **API help page** link in the web service **DASHBOARD** in Machine Learning Studio.</span></span> <span data-ttu-id="38cbc-125">Yeni bir web hizmeti için API belgeleri sağlanır [Azure Machine Learning Web Hizmetleri](https://services.azureml.net/Quickstart) portalını **Tüket** ve **Swagger API'si** web hizmetiniz için sayfa.</span><span class="sxs-lookup"><span data-stu-id="38cbc-125">The API documentation for a new web service is provided through the [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portal on the **Consume** and **Swagger API** pages for your web service.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="38cbc-126">Örnek</span><span class="sxs-lookup"><span data-stu-id="38cbc-126">Example</span></span>
<span data-ttu-id="38cbc-127">Bir örnek, bir deneme ile sahibiz varsayalım bir [verileri dışa aktar] [ writer] bilgileri Azure blob depolama alanına gönderir modülü.</span><span class="sxs-lookup"><span data-stu-id="38cbc-127">As an example, let's assume we have an experiment with an [Export Data][writer] module that sends information to Azure blob storage.</span></span> <span data-ttu-id="38cbc-128">Web hizmeti "yol Blob" adlı bir parametre tanımlama olasılığınız yüksektir hizmet erişildiğinde blob depolama alanına yolunu değiştirmek web hizmeti kullanıcı verir.</span><span class="sxs-lookup"><span data-stu-id="38cbc-128">We'll define a Web Service Parameter named "Blob path" that allows the web service user to change the path to the blob storage when the service is accessed.</span></span>

1. <span data-ttu-id="38cbc-129">Machine Learning Studio'da tıklatın [verileri dışa aktar] [ writer] modülü seçin.</span><span class="sxs-lookup"><span data-stu-id="38cbc-129">In Machine Learning Studio, click the [Export Data][writer] module to select it.</span></span> <span data-ttu-id="38cbc-130">Özelliklerini deneme tuvaline sağındaki Özellikler bölmesinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="38cbc-130">Its properties are shown in the Properties pane to the right of the experiment canvas.</span></span>
2. <span data-ttu-id="38cbc-131">Depolama türünü belirtin:</span><span class="sxs-lookup"><span data-stu-id="38cbc-131">Specify the storage type:</span></span>
   
   * <span data-ttu-id="38cbc-132">Altında **Lütfen verileri hedef belirtin**, "Azure Blob Storage" seçin.</span><span class="sxs-lookup"><span data-stu-id="38cbc-132">Under **Please specify data destination**, select "Azure Blob Storage".</span></span>
   * <span data-ttu-id="38cbc-133">Altında **Lütfen kimlik doğrulama türünü belirtin**, "Hesap" seçin.</span><span class="sxs-lookup"><span data-stu-id="38cbc-133">Under **Please specify authentication type**, select "Account".</span></span>
   * <span data-ttu-id="38cbc-134">Azure blob depolama hesabı bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="38cbc-134">Enter the account information for the Azure blob storage.</span></span> 
     <p /><span data-ttu-id="38cbc-135">
3.Simgesine sağ tarafındaki **kapsayıcı parametresi ile başlayan blob yolu**.</span><span class="sxs-lookup"><span data-stu-id="38cbc-135">
3. Click the icon to the right of the **Path to blob beginning with container parameter**.</span></span> <span data-ttu-id="38cbc-136">Şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="38cbc-136">It looks like this:</span></span>
   
   ![Web hizmeti parametresi simgesi][icon]
   
   <span data-ttu-id="38cbc-138">"Web hizmeti parametresi Ayarla" seçin.</span><span class="sxs-lookup"><span data-stu-id="38cbc-138">Select "Set as web service parameter".</span></span>
   
   <span data-ttu-id="38cbc-139">Bir giriş altında eklenen **Web hizmeti parametreleri** alt kısmındaki "kapsayıcı ile başlayan blob yolu" adıyla Özellikler bölmesi.</span><span class="sxs-lookup"><span data-stu-id="38cbc-139">An entry is added under **Web Service Parameters** at the bottom of the Properties pane with the name "Path to blob beginning with container".</span></span> <span data-ttu-id="38cbc-140">Bu Web hizmeti, şu anda parametredir bununla ilişkili [verileri dışa aktar] [ writer] modülü parametresi.</span><span class="sxs-lookup"><span data-stu-id="38cbc-140">This is the Web Service Parameter that is now associated with this [Export Data][writer] module parameter.</span></span>
4. <span data-ttu-id="38cbc-141">Web hizmeti parametresi yeniden adlandırmak için adına tıklayın, "Blob yolu" girin ve basın **Enter** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="38cbc-141">To rename the Web Service Parameter, click the name, enter "Blob path", and press the **Enter** key.</span></span> 
5. <span data-ttu-id="38cbc-142">Web hizmeti parametresi için varsayılan bir değer sağlamak için adının sağındaki simgesini tıklatın, "varsayılan değer sağla" seçin, (örneğin, "container1/output1.csv"), bir değer girin ve basın **Enter** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="38cbc-142">To provide a default value for the Web Service Parameter, click the icon to the right of the name, select "Provide default value", enter a value (for example, "container1/output1.csv"), and press the **Enter** key.</span></span>
   
   ![Web hizmeti parametresi][parameter]
6. <span data-ttu-id="38cbc-144">**Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38cbc-144">Click **Run**.</span></span> 
7. <span data-ttu-id="38cbc-145">Tıklatın **Web hizmeti Dağıt** seçip **Web hizmeti Dağıt [Klasik]** veya **Web hizmeti dağıtma [Yeni]** web hizmeti dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="38cbc-145">Click **Deploy Web Service** and select **Deploy Web Service [Classic]** or **Deploy Web Service [New]** to deploy the web service.</span></span>

> [!NOTE] 
> <span data-ttu-id="38cbc-146">Yeni bir web hizmeti dağıtmak için yeterli izinleri olan Abonelikteki, web hizmetini dağıtma olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="38cbc-146">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="38cbc-147">Daha fazla bilgi için [Azure Machine Learning Web Hizmetleri Portalı'nı kullanarak bir Web hizmetini yönetmek](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="38cbc-147">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="38cbc-148">Web hizmeti kullanıcı için yeni bir hedef artık belirtebilirsiniz [verileri dışa aktar] [ writer] web hizmeti erişirken modülü.</span><span class="sxs-lookup"><span data-stu-id="38cbc-148">The user of the web service can now specify a new destination for the [Export Data][writer] module when accessing the web service.</span></span>

## <a name="more-information"></a><span data-ttu-id="38cbc-149">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="38cbc-149">More information</span></span>
<span data-ttu-id="38cbc-150">Daha ayrıntılı bir örnek için bkz: [Web hizmeti parametreleri](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) girişi [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span><span class="sxs-lookup"><span data-stu-id="38cbc-150">For a more detailed example, see the [Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entry in the [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span></span>

<span data-ttu-id="38cbc-151">Machine Learning web hizmetine erişim ile ilgili daha fazla bilgi için bkz: [bir Azure Machine Learning Web hizmeti kullanmak nasıl](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="38cbc-151">For more information on accessing a Machine Learning web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

