---
title: "Excel eklentisi Machine Learning Web Hizmetleri için | Microsoft Docs"
description: "Azure Machine Learning Web hizmetlerini doğrudan Excel'de herhangi bir kod yazmak zorunda kalmadan nasıl kullanacağınızı."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: 0d60dd87bbdd4d3eafac0f8876cc9e41412a53ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="81f55-103">Azure Machine Learning web hizmetleri için Excel Eklentisi</span><span class="sxs-lookup"><span data-stu-id="81f55-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="81f55-104">Excel web hizmetleri herhangi bir kod yazmak zorunda kalmadan doğrudan çağırmak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="81f55-104">Excel makes it easy to call web services directly without the need to write any code.</span></span>

## <a name="steps-to-use-an-existing-web-service-in-the-workbook"></a><span data-ttu-id="81f55-105">Çalışma kitabını bir varolan web hizmetini kullanmak için adımları</span><span class="sxs-lookup"><span data-stu-id="81f55-105">Steps to Use an Existing web service in the Workbook</span></span>

1. <span data-ttu-id="81f55-106">Açık [örnek Excel dosyası](http://aka.ms/amlexcel-sample-2), Excel eklentisi ve Titanic üzerinde yolcu hakkındaki verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="81f55-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span></span>
2. <span data-ttu-id="81f55-107">Web hizmeti tıklayarak seçin-"Titanic hayatta bir göstergesi olduğu (Excel Eklentisi örneği) [Sonuç]" Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="81f55-107">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Web hizmetini seçin][01]
3. <span data-ttu-id="81f55-109">Bu, olanak sürer **Predıct** bölümü.</span><span class="sxs-lookup"><span data-stu-id="81f55-109">This takes you to the **Predict** section.</span></span>  <span data-ttu-id="81f55-110">Bu çalışma kitabı zaten örnek veri içeriyor, ancak için boş bir çalışma kitabını Excel'de bir hücre seçin ve'ı tıklatın **örnek verileri kullanın**.</span><span class="sxs-lookup"><span data-stu-id="81f55-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="81f55-111">Üst bilgileri ile verileri seçin ve giriş verilerini aralığı simgesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="81f55-111">Select the data with headers and click the input data range icon.</span></span>  <span data-ttu-id="81f55-112">"Verilerimin üstbilgileri var" kutunun işaretli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="81f55-112">Make sure the "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="81f55-113">Altında **çıkış**, olması için örneğin "H1" Buraya çıkış istediğiniz hücre sayısını girin.</span><span class="sxs-lookup"><span data-stu-id="81f55-113">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span></span>
6. <span data-ttu-id="81f55-114">Tıklatın **tahmin**.</span><span class="sxs-lookup"><span data-stu-id="81f55-114">Click **Predict**.</span></span>
   
    ![Bölüm tahmin etme][02]

<span data-ttu-id="81f55-116">Bir web hizmetini dağıtma veya var olan bir Web hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="81f55-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="81f55-117">Bir web hizmeti dağıtma hakkında daha fazla bilgi için bkz: [gözden geçirme adım 5: Azure Machine Learning Web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="81f55-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="81f55-118">Web hizmeti için API anahtarı edinin.</span><span class="sxs-lookup"><span data-stu-id="81f55-118">Get the API key for your web service.</span></span> <span data-ttu-id="81f55-119">Gerçekleştirdiğiniz burada yeni Machine Learning web hizmeti bir Klasik Machine Learning web hizmeti olup yayımlanan Bu eylem bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="81f55-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="81f55-120">**Klasik web hizmetini kullanın**</span><span class="sxs-lookup"><span data-stu-id="81f55-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="81f55-121">Machine Learning Studio'da tıklatın **WEB Hizmetleri** bölümünde sol bölmede ve web hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="81f55-121">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span></span>
   
    ![Bir Web hizmeti Studio seçin][04]
2. <span data-ttu-id="81f55-123">Web hizmeti API anahtarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="81f55-123">Copy the API key for the web service.</span></span>
   
    ![Studio API anahtarı][05]
3. <span data-ttu-id="81f55-125">Üzerinde **PANO** web hizmeti için sekmesini tıklatın, **istek/yanıt** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="81f55-125">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="81f55-126">Ara **istek URI'si** bölümü.</span><span class="sxs-lookup"><span data-stu-id="81f55-126">Look for the **Request URI** section.</span></span>  <span data-ttu-id="81f55-127">Kopyalayın ve URL kaydedin.</span><span class="sxs-lookup"><span data-stu-id="81f55-127">Copy and save the URL.</span></span>

> [!NOTE]
> <span data-ttu-id="81f55-128">Oturumu açmak artık mümkündür [Azure Machine Learning Web Hizmetleri](https://services.azureml.net) Klasik Machine Learning web hizmeti için API anahtarını elde etmek üzere portalı.</span><span class="sxs-lookup"><span data-stu-id="81f55-128">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="81f55-129">**Yeni bir web hizmetini kullanın**</span><span class="sxs-lookup"><span data-stu-id="81f55-129">**Use a New web service**</span></span>

1. <span data-ttu-id="81f55-130">İçinde [Azure Machine Learning Web Hizmetleri](https://services.azureml.net) portal tıklatın **Web Hizmetleri**, web hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="81f55-130">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="81f55-131">Tıklatın **tüketen**.</span><span class="sxs-lookup"><span data-stu-id="81f55-131">Click **Consume**.</span></span>
3. <span data-ttu-id="81f55-132">Ara **temel tüketim bilgileri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="81f55-132">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="81f55-133">Kopyalayıp kaydedin **birincil anahtar** ve **istek-yanıt** URL.</span><span class="sxs-lookup"><span data-stu-id="81f55-133">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>

## <a name="steps-to-add-a-new-web-service"></a><span data-ttu-id="81f55-134">Yeni bir web hizmeti ekleme adımları</span><span class="sxs-lookup"><span data-stu-id="81f55-134">Steps to Add a New web service</span></span>

1. <span data-ttu-id="81f55-135">Bir web hizmetini dağıtma veya var olan bir Web hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="81f55-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="81f55-136">Bir web hizmeti dağıtma hakkında daha fazla bilgi için bkz: [gözden geçirme adım 5: Azure Machine Learning Web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="81f55-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="81f55-137">Tıklatın **tüketen**.</span><span class="sxs-lookup"><span data-stu-id="81f55-137">Click **Consume**.</span></span>
3. <span data-ttu-id="81f55-138">Ara **temel tüketim bilgileri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="81f55-138">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="81f55-139">Kopyalayıp kaydedin **birincil anahtar** ve **istek-yanıt** URL.</span><span class="sxs-lookup"><span data-stu-id="81f55-139">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>
4. <span data-ttu-id="81f55-140">Excel'de Git **Web Hizmetleri** bölümüne (içinde olup olmadığını **Predıct** bölümünde, web hizmetleri listesine dönmek için geri oku tıklatın).</span><span class="sxs-lookup"><span data-stu-id="81f55-140">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span></span>
   
    ![Web hizmeti seçimi gidin][03]
5. <span data-ttu-id="81f55-142">Tıklatın **Web hizmeti Ekle**.</span><span class="sxs-lookup"><span data-stu-id="81f55-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="81f55-143">Eklenti metin kutusu etiketli Excel'e URL'sini yapıştırın **URL**.</span><span class="sxs-lookup"><span data-stu-id="81f55-143">Paste the URL into the Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="81f55-144">API/birincil anahtarı etiketli metin kutusuna yapıştırın **API anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="81f55-144">Paste the API/Primary key into the text box labeled **API key**.</span></span>
8. <span data-ttu-id="81f55-145">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f55-145">Click **Add**.</span></span>
   
    ![Klasik Web hizmeti URL'sini ve API anahtarı.][06]
9. <span data-ttu-id="81f55-147">Web hizmeti kullanmak için "varolan web hizmeti kullanmak için adımlar." önceki yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="81f55-147">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="81f55-148">Çalışma kitabınız paylaşımı</span><span class="sxs-lookup"><span data-stu-id="81f55-148">Sharing Your Workbook</span></span>
<span data-ttu-id="81f55-149">Çalışma kitabınız kaydederseniz, eklediğiniz web hizmetleri için API/birincil anahtar da kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="81f55-149">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span></span> <span data-ttu-id="81f55-150">Bu çalışma kitabını yalnızca güvendiğiniz kişilerle paylaşması gerekir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="81f55-150">That means you should only share the workbook with individuals you trust.</span></span>

<span data-ttu-id="81f55-151">Herhangi bir sorunuz aşağıdaki Açıklama bölümünde veya üzerinde isteyin bizim [Forumu](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="81f55-151">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
