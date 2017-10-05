---
title: "(kullanım dışı) SSS - yayımlama ve Azure Marketi'nde Machine Learning uygulamaları kullanma | Microsoft Docs"
description: "(kullanım dışı) Azure Marketi'nde yayımlama Machine Learning uygulamaları hakkında sık sorulan sorular"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a4631dfeb2f817b3a3c612a8f6af48398e4f2ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-the-azure-marketplace-faq"></a><span data-ttu-id="56283-103">(kullanım dışı) Yayımlama ve Azure Marketi'nde Machine Learning uygulamaları kullanan: sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="56283-103">(deprecated) Publishing and using Machine Learning apps in the Azure Marketplace: FAQ</span></span>

> [!NOTE]
> <span data-ttu-id="56283-104">DataMarket ve Veri Hizmetleri Çekildi ve mevcut abonelikleri kullanımdan kaldırılır ve başlangıç iptal 31/3/2017.</span><span class="sxs-lookup"><span data-stu-id="56283-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="56283-105">Sonuç olarak, bu makalede onaylanmaz.</span><span class="sxs-lookup"><span data-stu-id="56283-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="56283-106">Alternatif olarak, Machine Learning denemelerini yayımlayabilirsiniz [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/) veri bilimi topluluk yararlanması.</span><span class="sxs-lookup"><span data-stu-id="56283-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="56283-107">Daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="56283-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>


## <a name="questions-about-consuming-from-marketplace"></a><span data-ttu-id="56283-108">Marketten kullanma hakkında sorular</span><span class="sxs-lookup"><span data-stu-id="56283-108">Questions about consuming from Marketplace</span></span>
<span data-ttu-id="56283-109">**1. Giriş için web hizmeti girdiğinizde neden aşağıdaki hata iletisini alın:**</span><span class="sxs-lookup"><span data-stu-id="56283-109">**1. Why do I get the following error message after I enter input for the web service:**</span></span>

<span data-ttu-id="56283-110">**İstek bir arka uç zaman aşımı veya arka uç hata ile sonuçlandı. Ekibi sorunu Araştırıyor. Verdiğimiz rahatsızlıktan dolayı özür dileriz. (500)**</span><span class="sxs-lookup"><span data-stu-id="56283-110">**The request resulted in a back-end time out or back-end error. The team is investigating the issue. We are sorry for the inconvenience. (500)**</span></span>

<span data-ttu-id="56283-111">Giriş parametreleri belirli web hizmeti için gerekli biçime uygun olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="56283-111">Your input parameter(s) may not conform to the required format for the specific web service.</span></span> <span data-ttu-id="56283-112">Giriş parametreleri için doğru biçimde ve bu web Hizmeti'nin sınırlamaları bulmak için ilgili belgeleri bağlantısına bakın.</span><span class="sxs-lookup"><span data-stu-id="56283-112">Please refer to the corresponding documentation link to find the correct format for input parameters and the limitations of this web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="56283-113">**2. "Araştır bu veri kümesi" sayfası ve hangi kimlik bilgileri başka bir tarayıcı penceresine gerektiği Yapıştır bkz web hizmeti API bağlantı kopyalarsanız, sonuçları erişmek için kullandığım ve nasıl bunları görüyorum?**</span><span class="sxs-lookup"><span data-stu-id="56283-113">**2. If I copy the API link for the web service that I see on the "Explore this dataset" page and paste it into another browser window, what credentials should I use to access the results, and how do I see them?**</span></span>

<span data-ttu-id="56283-114">Market hesap parolası olarak kullanıcı adı ve birincil hesap anahtarı kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="56283-114">You should use your Marketplace account as the username and the primary account key as the password.</span></span> <span data-ttu-id="56283-115">Birincil hesap anahtarı bulunabilir **bu veri kümesi keşfedin** sayfasında web hizmeti açıklaması altında (tıklatın **Göster** düğmesi).</span><span class="sxs-lookup"><span data-stu-id="56283-115">The primary account key can be found on the **Explore this dataset** page under the description of the web service (click the **show** button).</span></span> <span data-ttu-id="56283-116">Sonucu tarayıcıda görüntüleyebilir veya indirilebilir olabilir, hangi tarayıcıya bağlı olarak, kullanmakta olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="56283-116">The result may display in the browser or it may be available to  download, depending on which browser you are using.</span></span>

<span data-ttu-id="56283-117">**3. Giriş için web hizmeti "Araştır bu veri kümesi" sayfasında girdiğim sonra neden aşağıdaki hata iletisini alın:**</span><span class="sxs-lookup"><span data-stu-id="56283-117">**3. Why do I get the following error message after I enter the input for the web service on the "Explore this dataset" page:**</span></span> 

<span data-ttu-id="56283-118">**İsteğiniz işlenirken beklenmeyen bir hata oluştu. Lütfen yeniden deneyin.**</span><span class="sxs-lookup"><span data-stu-id="56283-118">**An unexpected error occurred while processing your request. Please try again.**</span></span>

<span data-ttu-id="56283-119">Web hizmeti bir veya daha fazla giriş parametreleri uzunluk sınırını aştı Market'te web hizmeti kullanırken **bu veri kümesi keşfedin** sayfası.</span><span class="sxs-lookup"><span data-stu-id="56283-119">One or more input parameters of your web service may have exceeded the length limit when consuming the web service on the marketplace **Explore this dataset** page.</span></span> <span data-ttu-id="56283-120">Hizmetleri artık bir giriş uzunluğunda HTTP POST yöntemleri kullanılarak çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="56283-120">The services can be called with a longer input length by using HTTP POST methods.</span></span> <span data-ttu-id="56283-121">Örnekler için bkz: [örnek R Machine Learning kullanan çözümler ve Markete yayımlanan](machine-learning-r-csharp-web-service-examples.md).</span><span class="sxs-lookup"><span data-stu-id="56283-121">For examples, see [Sample solutions using R on Machine Learning and published to Marketplace](machine-learning-r-csharp-web-service-examples.md).</span></span>

<span data-ttu-id="56283-122">**4. Her şeyi "API'si GEZGİNİ" sekmesini int Klasik Azure portalı deposunda görmemin nedeni değil mi?**</span><span class="sxs-lookup"><span data-stu-id="56283-122">**4. Why do I not see anything in the "API EXPLORER" tab int the Store in the Azure Classic Portal?**</span></span> 

<span data-ttu-id="56283-123">Bu, Azure Klasik portalı Market ile bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="56283-123">This is a known issue with the Azure Classic Portal Marketplace.</span></span> <span data-ttu-id="56283-124">Bu sorunu çözmek için takım çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="56283-124">The team is working to resolve this issue.</span></span> 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a><span data-ttu-id="56283-125">Azure Machine Learning Market'te yayımlama hakkında sorular</span><span class="sxs-lookup"><span data-stu-id="56283-125">Questions about publishing from Azure Machine Learning on Marketplace</span></span>
<span data-ttu-id="56283-126">**1. Neden my hareketleri logolar veya görüntüleri değil web Hizmetimi yenileme?**</span><span class="sxs-lookup"><span data-stu-id="56283-126">**1. Why are my transactions of logos or images not refreshing for my web service?**</span></span> 

<span data-ttu-id="56283-127">Logo ve görüntüleri yayımlama portalında önbelleğe alınır ve yeni logo veya portalda güncelleştirmek için görüntü için 10 güne kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="56283-127">Logos and images are cached in the publishing portal, and it may take up to 10 days for the new logo or image to update on the portal.</span></span>

<span data-ttu-id="56283-128">**2. My web hizmeti bir hata iletisi gösteren Market'te "Ayrıntı" sekmesinde neden oluyor?**</span><span class="sxs-lookup"><span data-stu-id="56283-128">**2. Why is the “Detail" tab of my web service on Marketplace showing an error message?**</span></span>

<span data-ttu-id="56283-129">Azure Machine Learning hizmetinin ayrıntılarını bağlanırken bilinen bir Market sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="56283-129">There is a known Marketplace issue when connecting to Azure Machine Learning for service details.</span></span> <span data-ttu-id="56283-130">Bu sorunu çözmek için takım çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="56283-130">The team is working to resolve this issue.</span></span>

<span data-ttu-id="56283-131">**3. Neden Azure Machine Learning web hizmetleri R örnek kodda pazarında web hizmetlerini tüketen çalışmıyor?**</span><span class="sxs-lookup"><span data-stu-id="56283-131">**3. Why does the R sample code in the Azure Machine Learning web services not work for consuming the web services in Marketplace?**</span></span>

<span data-ttu-id="56283-132">Azure Machine Learning web hizmetleri doğrudan Market üzerinden bu web hizmetlerine bağlanma karşılaştırıldığında bağlanırken kimlik doğrulama sistemleriyle farklıdır.</span><span class="sxs-lookup"><span data-stu-id="56283-132">The authentication systems are different when connecting to Azure Machine Learning web services directly compared to connecting to these web services through the Marketplace.</span></span> <span data-ttu-id="56283-133">Market Hizmetleri'nde OData hizmetler ve GET veya POST yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="56283-133">The services in Marketplace are OData services, and they can be called with GET or POST methods.</span></span> 

<span data-ttu-id="56283-134">**4. My web hizmetinin destek bağlantıları neden olan doğru bazı my teklifleri için güncelleştirilmezse sunar?**</span><span class="sxs-lookup"><span data-stu-id="56283-134">**4. Why are the support links of my web service offers not updating correctly for some of my offers?**</span></span>

<span data-ttu-id="56283-135">Yayımcı başına, Teklif başına değil genel destek bağlantılardır.</span><span class="sxs-lookup"><span data-stu-id="56283-135">The support links are global per publisher, not per offer.</span></span> 

<span data-ttu-id="56283-136">**5. Marketi'nde nasıl toplu işlem giriş modu web hizmetiyle yayımlanacak?**</span><span class="sxs-lookup"><span data-stu-id="56283-136">**5. How do I publish a web service with batch input mode in Marketplace?**</span></span>

<span data-ttu-id="56283-137">Toplu işlem giriş modu Market web hizmetleri şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="56283-137">The batch input mode is currently not supported in Marketplace web services.</span></span>

<span data-ttu-id="56283-138">**6. Kimin ı verileri yayımcısı olma hakkında sorularınız varsa ya da sorunlar yayımlama sırasında varsa Yardım almak için iletişim kuralım?**</span><span class="sxs-lookup"><span data-stu-id="56283-138">**6. Who should I contact to get help if I have questions about becoming a data publisher, or if I have issues during publishing?**</span></span>

<span data-ttu-id="56283-139">Azure Market Ekibi temasa < mailto:datamarketbd@microsoft.com > daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="56283-139">Please contact the Azure Marketplace team at <mailto:datamarketbd@microsoft.com> for more information.</span></span>

