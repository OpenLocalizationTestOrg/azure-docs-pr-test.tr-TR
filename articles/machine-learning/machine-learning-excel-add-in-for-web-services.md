---
title: "Machine Learning Web Hizmetleri için aaaExcel eklenti | Microsoft Docs"
description: "Nasıl herhangi bir kod yazmak zorunda kalmadan doğrudan Excel'de toouse Azure Machine Learning Web Hizmetleri."
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
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="d383f-103">Azure Machine Learning web hizmetleri için Excel Eklentisi</span><span class="sxs-lookup"><span data-stu-id="d383f-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="d383f-104">Herhangi bir kod toowrite Hello gerek olmadan Excel kolay toocall web hizmetleri doğrudan kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="d383f-104">Excel makes it easy toocall web services directly without hello need toowrite any code.</span></span>

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a><span data-ttu-id="d383f-105">Adımları tooUse hello çalışma kitabı varolan web hizmetinde</span><span class="sxs-lookup"><span data-stu-id="d383f-105">Steps tooUse an Existing web service in hello Workbook</span></span>

1. <span data-ttu-id="d383f-106">Açık hello [örnek Excel dosyası](http://aka.ms/amlexcel-sample-2)içeren hello Excel eklentisi ve yolcu hakkındaki verileri hello Titanic.</span><span class="sxs-lookup"><span data-stu-id="d383f-106">Open hello [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains hello Excel add-in and data about passengers on hello Titanic.</span></span>
2. <span data-ttu-id="d383f-107">Tıklayarak Hello web hizmeti seçin-"Titanic hayatta bir göstergesi olduğu (Excel Eklentisi örneği) [Sonuç]" Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="d383f-107">Choose hello web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Web hizmetini seçin][01]
3. <span data-ttu-id="d383f-109">Bu toohello sürer **Predıct** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d383f-109">This takes you toohello **Predict** section.</span></span>  <span data-ttu-id="d383f-110">Bu çalışma kitabı zaten örnek veri içeriyor, ancak için boş bir çalışma kitabını Excel'de bir hücre seçin ve'ı tıklatın **örnek verileri kullanın**.</span><span class="sxs-lookup"><span data-stu-id="d383f-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="d383f-111">Üst bilgileri ile Merhaba verileri seçin ve hello giriş verisi aralığı simgesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d383f-111">Select hello data with headers and click hello input data range icon.</span></span>  <span data-ttu-id="d383f-112">Merhaba "Verilerimin üstbilgileri var" onay kutusunun seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d383f-112">Make sure hello "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="d383f-113">Altında **çıkış**, burada çıkış toobe, örneğin "H1" Merhaba istediğiniz hello hücre numarasını girin.</span><span class="sxs-lookup"><span data-stu-id="d383f-113">Under **Output**, enter hello cell number where you want hello output toobe, for example "H1" here.</span></span>
6. <span data-ttu-id="d383f-114">Tıklatın **tahmin**.</span><span class="sxs-lookup"><span data-stu-id="d383f-114">Click **Predict**.</span></span>
   
    ![Bölüm tahmin etme][02]

<span data-ttu-id="d383f-116">Bir web hizmetini dağıtma veya var olan bir Web hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d383f-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="d383f-117">Bir web hizmeti dağıtma hakkında daha fazla bilgi için bkz: [gözden geçirme adım 5: hello Azure Machine Learning Web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="d383f-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="d383f-118">Web hizmetiniz için Hello API anahtarı edinin.</span><span class="sxs-lookup"><span data-stu-id="d383f-118">Get hello API key for your web service.</span></span> <span data-ttu-id="d383f-119">Gerçekleştirdiğiniz burada yeni Machine Learning web hizmeti bir Klasik Machine Learning web hizmeti olup yayımlanan Bu eylem bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d383f-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="d383f-120">**Klasik web hizmetini kullanın**</span><span class="sxs-lookup"><span data-stu-id="d383f-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="d383f-121">Machine Learning Studio'da hello tıklatın **WEB Hizmetleri** bölümünde hello sol bölmede ve hello web hizmetini seçin.</span><span class="sxs-lookup"><span data-stu-id="d383f-121">In Machine Learning Studio, click hello **WEB SERVICES** section in hello left pane, and then select hello web service.</span></span>
   
    ![Bir Web hizmeti Studio seçin][04]
2. <span data-ttu-id="d383f-123">Merhaba web hizmeti Hello API anahtarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d383f-123">Copy hello API key for hello web service.</span></span>
   
    ![Studio API anahtarı][05]
3. <span data-ttu-id="d383f-125">Merhaba üzerinde **PANO** hello web hizmeti için sekmesini ve ardından hello **istek/yanıt** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="d383f-125">On hello **DASHBOARD** tab for hello web service, click hello **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="d383f-126">Merhaba Ara **istek URI'si** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d383f-126">Look for hello **Request URI** section.</span></span>  <span data-ttu-id="d383f-127">Kopyalayın ve hello URL kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d383f-127">Copy and save hello URL.</span></span>

> [!NOTE]
> <span data-ttu-id="d383f-128">Merhaba içine olası toosign sunulmuştur [Azure Machine Learning Web Hizmetleri](https://services.azureml.net) Klasik Machine Learning web hizmeti için portal tooobtain hello API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="d383f-128">It is now possible toosign into hello [Azure Machine Learning Web Services](https://services.azureml.net) portal tooobtain hello API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="d383f-129">**Yeni bir web hizmetini kullanın**</span><span class="sxs-lookup"><span data-stu-id="d383f-129">**Use a New web service**</span></span>

1. <span data-ttu-id="d383f-130">Merhaba, [Azure Machine Learning Web Hizmetleri](https://services.azureml.net) portal tıklatın **Web Hizmetleri**, web hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="d383f-130">In hello [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="d383f-131">Tıklatın **tüketen**.</span><span class="sxs-lookup"><span data-stu-id="d383f-131">Click **Consume**.</span></span>
3. <span data-ttu-id="d383f-132">Merhaba Ara **temel tüketim bilgileri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d383f-132">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="d383f-133">Kopyalayın ve hello kaydedin **birincil anahtar** ve hello **istek-yanıt** URL.</span><span class="sxs-lookup"><span data-stu-id="d383f-133">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>

## <a name="steps-tooadd-a-new-web-service"></a><span data-ttu-id="d383f-134">Adımları tooAdd yeni bir web hizmeti</span><span class="sxs-lookup"><span data-stu-id="d383f-134">Steps tooAdd a New web service</span></span>

1. <span data-ttu-id="d383f-135">Bir web hizmetini dağıtma veya var olan bir Web hizmetini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d383f-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="d383f-136">Bir web hizmeti dağıtma hakkında daha fazla bilgi için bkz: [gözden geçirme adım 5: hello Azure Machine Learning Web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="d383f-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="d383f-137">Tıklatın **tüketen**.</span><span class="sxs-lookup"><span data-stu-id="d383f-137">Click **Consume**.</span></span>
3. <span data-ttu-id="d383f-138">Merhaba Ara **temel tüketim bilgileri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="d383f-138">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="d383f-139">Kopyalayın ve hello kaydedin **birincil anahtar** ve hello **istek-yanıt** URL.</span><span class="sxs-lookup"><span data-stu-id="d383f-139">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>
4. <span data-ttu-id="d383f-140">Excel'de toohello Git **Web Hizmetleri** bölümüne (hello varsa **Predıct** bölümünde, web hizmetleri hello geri ok toogo toohello listeye tıklayın).</span><span class="sxs-lookup"><span data-stu-id="d383f-140">In Excel, go toohello **Web Services** section (if you are in hello **Predict** section, click hello back arrow toogo toohello list of web services).</span></span>
   
    ![TooWeb hizmet seçimi gidin][03]
5. <span data-ttu-id="d383f-142">Tıklatın **Web hizmeti Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d383f-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="d383f-143">Excel eklentisi metin kutusu etiketli hello hello URL yapıştırın **URL**.</span><span class="sxs-lookup"><span data-stu-id="d383f-143">Paste hello URL into hello Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="d383f-144">Yapıştır hello API/birincil anahtarı olarak etiketlenmiş hello metin kutusuna **API anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="d383f-144">Paste hello API/Primary key into hello text box labeled **API key**.</span></span>
8. <span data-ttu-id="d383f-145">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d383f-145">Click **Add**.</span></span>
   
    ![Klasik Web hizmeti URL'sini ve API anahtarı.][06]
9. <span data-ttu-id="d383f-147">toouse hello web hizmeti, hello önceki yönergeleri izleyin, "tooUse varolan web hizmeti adımları."</span><span class="sxs-lookup"><span data-stu-id="d383f-147">toouse hello web service, follow hello preceding directions, "Steps tooUse an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="d383f-148">Çalışma kitabınız paylaşımı</span><span class="sxs-lookup"><span data-stu-id="d383f-148">Sharing Your Workbook</span></span>
<span data-ttu-id="d383f-149">Çalışma kitabınız kaydederseniz, eklediğiniz hello web hizmetleri için hello API/birincil anahtar da kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d383f-149">If you save your workbook, then hello API/Primary key for hello web services you have added is also saved.</span></span> <span data-ttu-id="d383f-150">Merhaba çalışma kitabını yalnızca güvendiğiniz kişilerle paylaşması gerekir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d383f-150">That means you should only share hello workbook with individuals you trust.</span></span>

<span data-ttu-id="d383f-151">Merhaba Açıklama bölümüne aşağıdaki veya üzerinde herhangi bir sorunuz isteyin bizim [Forumu](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d383f-151">Ask any questions in hello following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
