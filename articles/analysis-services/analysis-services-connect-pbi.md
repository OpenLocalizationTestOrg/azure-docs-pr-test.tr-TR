---
title: aaaConnect tooAzure Power BI Analysis Services | Microsoft Docs
description: "Nasıl tooconnect tooan Azure Analysis Services öğrenin Power BI kullanarak sunucu."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="ab1fb-103">Power BI ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="ab1fb-103">Connect with Power BI</span></span>

<span data-ttu-id="ab1fb-104">Bir sunucusu Azure içinde oluşturulan ve dağıtılan bir tablo modeli tooit sonra kuruluşunuzdaki kullanıcılar hazır tooconnect ve veri araştırmaya başlamak.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-104">Once you've created a server in Azure, and deployed a tabular model tooit, users in your organization are ready tooconnect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="ab1fb-105">Emin toouse hello en son sürümüne sahip olmanız [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="ab1fb-105">Be sure toouse hello latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="ab1fb-106">Power BI Desktop'ta Bağlan</span><span class="sxs-lookup"><span data-stu-id="ab1fb-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="ab1fb-107">Power BI Desktop'ta tıklatın **Veri Al** > **Azure** > **Azure Analysis Services veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="ab1fb-108">İçinde **Server**, hello sunucu adı girin.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-108">In **Server**, enter hello server name.</span></span> 
    
    <span data-ttu-id="ab1fb-109">Emin tooinclude hello tam URL olabilir.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-109">Be sure tooinclude hello full URL.</span></span> <span data-ttu-id="ab1fb-110">Örneğin, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="ab1fb-111">İçinde **veritabanı**, hello tablolu model veritabanı veya buraya yapıştırmak için tooconnect istediğiniz perspektif hello adını biliyorsanız.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-111">In **Database**, if you know hello name of hello tabular model database or perspective you want tooconnect to, paste it here.</span></span> <span data-ttu-id="ab1fb-112">Aksi takdirde, bu alanı boş bırakın ve daha sonra bir veritabanı veya perspektif seçin.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="ab1fb-113">Merhaba varsayılan adı bırakın **Bağlan canlı** seçeneğini ve ardından basın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-113">Leave hello default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="ab1fb-114">İstenirse, oturum açma kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="ab1fb-115">İçinde **Gezgini**, hello sunucuyu genişletin ve ardından hello model veya perspektif ardından için tooconnect istediğiniz **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-115">In **Navigator**, expand hello server, then select hello model or perspective you want tooconnect to, then click **Connect**.</span></span> <span data-ttu-id="ab1fb-116">Bir model veya perspektif tooshow tüm hello nesneler bu görünüm için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-116">Click  a model or perspective tooshow all hello objects for that view.</span></span>

    <span data-ttu-id="ab1fb-117">Merhaba modeli Power BI Desktop'ta rapor görünümü boş bir rapor ile açılır.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-117">hello model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="ab1fb-118">Merhaba alanlar listesinde tüm gizli olmayan model nesneleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-118">hello Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="ab1fb-119">Bağlantı durumu hello sağ alt köşesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-119">Connection status is displayed in hello lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="ab1fb-120">Power BI (hizmeti) bağlanma</span><span class="sxs-lookup"><span data-stu-id="ab1fb-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="ab1fb-121">Sunucunuz üzerinde bir dinamik bağlantı tooyour modeli olan bir Power BI Desktop dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-121">Create a Power BI Desktop file that has a live connection tooyour model on your server.</span></span>
2. <span data-ttu-id="ab1fb-122">İçinde [Power BI](https://powerbi.microsoft.com), tıklatın **Veri Al** > **dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="ab1fb-123">Dosyasını bulup seçin.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="ab1fb-124">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="ab1fb-124">See also</span></span>
<span data-ttu-id="ab1fb-125">[TooAzure Analysis Services Bağlan](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="ab1fb-125">[Connect tooAzure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="ab1fb-126">İstemci kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="ab1fb-126">Client libraries</span></span>](analysis-services-data-providers.md)

