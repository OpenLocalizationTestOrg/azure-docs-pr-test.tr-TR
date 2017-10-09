---
title: bir Machine Learning Web hizmeti Excel'den aaaConsume | Microsoft Docs
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
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="2e258-103">Bir Azure Machine Learning Web Hizmetini Excel’den kullanma</span><span class="sxs-lookup"><span data-stu-id="2e258-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="2e258-104">Azure Machine Learning Studio'da herhangi bir kod toowrite Hello gerek olmadan kolayca toocall web hizmetleri doğrudan Excel'den kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="2e258-104">Azure Machine Learning Studio makes it easy toocall web services directly from Excel without hello need toowrite any code.</span></span>

<span data-ttu-id="2e258-105">Excel 2013 (veya üstü) veya Excel Online'da kullandığınız sonra hello Excel kullanmanızı öneririz [Excel eklentisi](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="2e258-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use hello Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="2e258-106">Adımlar</span><span class="sxs-lookup"><span data-stu-id="2e258-106">Steps</span></span>
<span data-ttu-id="2e258-107">Bir web hizmeti yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="2e258-107">Publish a web service.</span></span> <span data-ttu-id="2e258-108">[Bu sayfayı](machine-learning-walkthrough-5-publish-web-service.md) açıklar nasıl toodo onu.</span><span class="sxs-lookup"><span data-stu-id="2e258-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how toodo it.</span></span> <span data-ttu-id="2e258-109">Şu anda hello Excel çalışma kitabı özelliği yalnızca tek bir çıktı (diğer bir deyişle, tek bir Puanlama etiketi) sahip istek/yanıt Hizmetleri için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="2e258-109">Currently hello Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="2e258-110">Bir web hizmeti olduktan sonra üzerinde hello tıklatın **WEB Hizmetleri** bölümünde hello studio hello sol tarafta ve ardından hello web hizmeti tooconsume Excel'den seçin.</span><span class="sxs-lookup"><span data-stu-id="2e258-110">Once you have a web service, click on hello **WEB SERVICES** section on hello left of hello studio, and then select hello web service tooconsume from Excel.</span></span>

<span data-ttu-id="2e258-111">**Klasik Web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="2e258-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="2e258-112">Merhaba üzerinde **PANO** hello web hizmetidir hello için bir satır sekmesi **istek/yanıt** hizmet.</span><span class="sxs-lookup"><span data-stu-id="2e258-112">On hello **DASHBOARD** tab for hello web service is a row for hello **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="2e258-113">Bu hizmet tek bir çıktı olsaydı hello görmelisiniz **karşıdan Excel çalışma kitabı** o satırdaki bağlantı.</span><span class="sxs-lookup"><span data-stu-id="2e258-113">If this service had a single output, you should see hello **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="2e258-114">Tıklayın **karşıdan Excel çalışma kitabı**.</span><span class="sxs-lookup"><span data-stu-id="2e258-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="2e258-115">**Yeni Web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="2e258-115">**New Web Service**</span></span>

1. <span data-ttu-id="2e258-116">Hello Azure Machine Learning Web hizmeti Portalı'nda seçin **Tüket**.</span><span class="sxs-lookup"><span data-stu-id="2e258-116">In hello Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="2e258-117">Merhaba Tüket sayfasında, hello **Web hizmeti tüketim seçenekleri** bölümünde, hello Excel simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2e258-117">On hello Consume page, in hello **Web service consumption options** section, click hello Excel icon.</span></span>

<span data-ttu-id="2e258-118">**Merhaba çalışma kitabı kullanma**</span><span class="sxs-lookup"><span data-stu-id="2e258-118">**Using hello workbook**</span></span>

1. <span data-ttu-id="2e258-119">Açık hello çalışma kitabı.</span><span class="sxs-lookup"><span data-stu-id="2e258-119">Open hello workbook.</span></span>
2. <span data-ttu-id="2e258-120">Bir güvenlik uyarısı görüntülenmez; Merhaba üzerinde tıklatın **düzenlemeyi etkinleştir** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2e258-120">A Security Warning appears; click on hello **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="2e258-121">Bir güvenlik uyarısı görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="2e258-121">A Security Warning appears.</span></span> <span data-ttu-id="2e258-122">Tıklatın hello üzerinde **içeriği etkinleştir** düğmesini toorun makroları, elektronik tablo.</span><span class="sxs-lookup"><span data-stu-id="2e258-122">Click on hello **Enable Content** button toorun macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="2e258-123">Makrolar etkinleştirildikten sonra bir tablo oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2e258-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="2e258-124">Mavi olan sütunlarda gerekli hello giriş olarak RRS web hizmeti veya **parametreleri**.</span><span class="sxs-lookup"><span data-stu-id="2e258-124">Columns in blue are required as input into hello RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="2e258-125">Not hello RR hizmet hello çıktısını **ÖNGÖRÜLEN değerleri** yeşil.</span><span class="sxs-lookup"><span data-stu-id="2e258-125">Note hello output of hello RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="2e258-126">Belirli bir satır için tüm sütunları dolduğunda, hello çalışma kitabı otomatik olarak API Puanlama hello çağıran ve sonuçları skoru hello görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2e258-126">When all columns for a given row are filled, hello workbook automatically calls hello scoring API, and displays hello scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="2e258-127">tooscore birden fazla bir satır, veriler ve hello ile dolgu hello ikinci satır değerleri üretilen tahmin.</span><span class="sxs-lookup"><span data-stu-id="2e258-127">tooscore more than one row, fill hello second row with data and hello predicted values are produced.</span></span> <span data-ttu-id="2e258-128">Aynı anda birden çok satır bile yapıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e258-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="2e258-129">Hello Excel özelliklerinden (grafikleri, güç harita, koşullu biçimlendirme, vs.) herhangi birini tahmin hello ile kullanabileceğiniz değerleri toohelp hello verileri görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="2e258-129">You can use any of hello Excel features (graphs, power map, conditional formatting, etc.) with hello predicted values toohelp visualize hello data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="2e258-130">Çalışma kitabınız paylaşımı</span><span class="sxs-lookup"><span data-stu-id="2e258-130">Sharing your workbook</span></span>
<span data-ttu-id="2e258-131">Merhaba makroları toowork için API anahtarınıza hello elektronik tablonun parçası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e258-131">For hello macros toowork, your API Key must be part of hello spreadsheet.</span></span> <span data-ttu-id="2e258-132">Yalnızca varlıklar/güvenilir kişiler ile Merhaba çalışma kitabı paylaşmalıdır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2e258-132">That means that you should share hello workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="2e258-133">Otomatik güncelleştirmeler</span><span class="sxs-lookup"><span data-stu-id="2e258-133">Automatic updates</span></span>
<span data-ttu-id="2e258-134">Bir RRS çağrı bu iki durumlarda yapılmıştır:</span><span class="sxs-lookup"><span data-stu-id="2e258-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="2e258-135">Merhaba ilk kez bir satır var içerik tümünde kendi **parametreleri**</span><span class="sxs-lookup"><span data-stu-id="2e258-135">hello first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="2e258-136">Hello hiçbirini kurduğunda **parametreleri** tümüne sahip olan bir satır değişiklikleri kendi **parametreleri** girildi.</span><span class="sxs-lookup"><span data-stu-id="2e258-136">Any time any of hello **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
