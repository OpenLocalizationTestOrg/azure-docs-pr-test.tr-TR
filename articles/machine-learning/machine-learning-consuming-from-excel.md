---
title: Bir Machine Learning Web hizmeti Excel'den kullanma | Microsoft Docs
description: Bir Azure Machine Learning Web hizmeti Excel'den kullanma
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: 9f1aac04d54221888ee9374317be339400dcf085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="1ba30-103">Bir Azure Machine Learning Web Hizmetini Excel’den kullanma</span><span class="sxs-lookup"><span data-stu-id="1ba30-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="1ba30-104">Azure Machine Learning Studio, web hizmetleri doğrudan kod yazmaya gerek kalmadan Excel çağırmanıza kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="1ba30-104">Azure Machine Learning Studio makes it easy to call web services directly from Excel without the need to write any code.</span></span>

<span data-ttu-id="1ba30-105">Excel 2013 (veya üstü) veya Excel Online'da kullandığınız sonra Excel kullanmanızı öneririz [Excel eklentisi](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="1ba30-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use the Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="1ba30-106">Adımlar</span><span class="sxs-lookup"><span data-stu-id="1ba30-106">Steps</span></span>
<span data-ttu-id="1ba30-107">Bir web hizmeti yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="1ba30-107">Publish a web service.</span></span> <span data-ttu-id="1ba30-108">[Bu sayfayı](machine-learning-walkthrough-5-publish-web-service.md) nasıl yapılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="1ba30-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how to do it.</span></span> <span data-ttu-id="1ba30-109">Şu anda Excel çalışma kitabı özelliği yalnızca tek bir çıktı (diğer bir deyişle, tek bir Puanlama etiketi) sahip istek/yanıt Hizmetleri için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="1ba30-109">Currently the Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="1ba30-110">Bir web hizmeti oluşturduktan sonra tıklayın **WEB Hizmetleri** bölümünde Studio'nun sol tarafta ve Excel'den kullanmak için web hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="1ba30-110">Once you have a web service, click on the **WEB SERVICES** section on the left of the studio, and then select the web service to consume from Excel.</span></span>

<span data-ttu-id="1ba30-111">**Klasik Web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="1ba30-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="1ba30-112">Üzerinde **PANO** web hizmeti için bir satır için sekme **istek/yanıt** hizmet.</span><span class="sxs-lookup"><span data-stu-id="1ba30-112">On the **DASHBOARD** tab for the web service is a row for the **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="1ba30-113">Bu hizmet tek bir çıktı olsaydı görmeniz gerekir **karşıdan Excel çalışma kitabı** o satırdaki bağlantı.</span><span class="sxs-lookup"><span data-stu-id="1ba30-113">If this service had a single output, you should see the **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="1ba30-114">Tıklayın **karşıdan Excel çalışma kitabı**.</span><span class="sxs-lookup"><span data-stu-id="1ba30-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="1ba30-115">**Yeni Web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="1ba30-115">**New Web Service**</span></span>

1. <span data-ttu-id="1ba30-116">Azure Machine Learning Web hizmeti Portalı'nda seçin **Tüket**.</span><span class="sxs-lookup"><span data-stu-id="1ba30-116">In the Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="1ba30-117">Tüket sayfasında içinde **Web hizmeti tüketim seçenekleri** bölümünde, Excel simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1ba30-117">On the Consume page, in the **Web service consumption options** section, click the Excel icon.</span></span>

<span data-ttu-id="1ba30-118">**Çalışma kitabı kullanma**</span><span class="sxs-lookup"><span data-stu-id="1ba30-118">**Using the workbook**</span></span>

1. <span data-ttu-id="1ba30-119">Çalışma kitabını açın.</span><span class="sxs-lookup"><span data-stu-id="1ba30-119">Open the workbook.</span></span>
2. <span data-ttu-id="1ba30-120">Bir güvenlik uyarısı görüntülenmez; tıklayın **düzenlemeyi etkinleştir** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1ba30-120">A Security Warning appears; click on the **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="1ba30-121">Bir güvenlik uyarısı görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="1ba30-121">A Security Warning appears.</span></span> <span data-ttu-id="1ba30-122">Tıklayın **içeriği etkinleştir** makroları, elektronik tablo üzerinde çalıştırmak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1ba30-122">Click on the **Enable Content** button to run macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="1ba30-123">Makrolar etkinleştirildikten sonra bir tablo oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1ba30-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="1ba30-124">Mavi olan sütunlarda gerekli giriş RRS web hizmeti olarak veya **parametreleri**.</span><span class="sxs-lookup"><span data-stu-id="1ba30-124">Columns in blue are required as input into the RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="1ba30-125">RRS hizmet çıktısını Not **ÖNGÖRÜLEN değerleri** yeşil.</span><span class="sxs-lookup"><span data-stu-id="1ba30-125">Note the output of the RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="1ba30-126">Belirli bir satır için tüm sütunları dolduğunda, çalışma kitabını otomatik olarak Puanlama API çağrılarının ve puanlanmış sonuçları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1ba30-126">When all columns for a given row are filled, the workbook automatically calls the scoring API, and displays the scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="1ba30-127">Birden fazla satır Puanlama amacıyla dolgu ikinci satırın veriler ve tahmin edilen değerler ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1ba30-127">To score more than one row, fill the second row with data and the predicted values are produced.</span></span> <span data-ttu-id="1ba30-128">Aynı anda birden çok satır bile yapıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ba30-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="1ba30-129">Verileri görselleştirin yardımcı olmak için tahmin edilen değerlere sahip (grafikleri, güç harita, koşullu biçimlendirme, vb.) Excel özelliklerinden herhangi birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ba30-129">You can use any of the Excel features (graphs, power map, conditional formatting, etc.) with the predicted values to help visualize the data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="1ba30-130">Çalışma kitabınız paylaşımı</span><span class="sxs-lookup"><span data-stu-id="1ba30-130">Sharing your workbook</span></span>
<span data-ttu-id="1ba30-131">Makrolar çalışmak API anahtarınıza elektronik tablonun parçası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ba30-131">For the macros to work, your API Key must be part of the spreadsheet.</span></span> <span data-ttu-id="1ba30-132">Bu çalışma kitabını yalnızca varlıklar/güvendiğiniz kişilerle paylaşmalıdır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1ba30-132">That means that you should share the workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="1ba30-133">Otomatik güncelleştirmeler</span><span class="sxs-lookup"><span data-stu-id="1ba30-133">Automatic updates</span></span>
<span data-ttu-id="1ba30-134">Bir RRS çağrı bu iki durumlarda yapılmıştır:</span><span class="sxs-lookup"><span data-stu-id="1ba30-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="1ba30-135">İlk kez bir satır var içerik tümünde kendi **parametreleri**</span><span class="sxs-lookup"><span data-stu-id="1ba30-135">The first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="1ba30-136">Herhangi birini zaman **parametreleri** tümüne sahip olan bir satır değişiklikleri kendi **parametreleri** girildi.</span><span class="sxs-lookup"><span data-stu-id="1ba30-136">Any time any of the **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
