---
title: "(kullanım dışı) Machine learning yayımlama web hizmeti Azure Marketi'nde | Microsoft Docs"
description: "(kullanım dışı) Azure Machine Learning Web hizmetinizi Azure Marketinde yayımlama"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: TRUE
ms.openlocfilehash: 3e3420872f0c604e027d1f309a6de6f52a5a788c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-to-the-azure-marketplace"></a><span data-ttu-id="9a7bb-103">(kullanım dışı) Azure Machine Learning Web hizmeti Azure Marketi'nde yayımlama</span><span class="sxs-lookup"><span data-stu-id="9a7bb-103">(deprecated) Publish Azure Machine Learning Web Service to the Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="9a7bb-104">DataMarket ve Veri Hizmetleri Çekildi ve mevcut abonelikleri kullanımdan kaldırılır ve başlangıç iptal 31/3/2017.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="9a7bb-105">Sonuç olarak, bu makalede onaylanmaz.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="9a7bb-106">Alternatif olarak, Machine Learning denemelerini yayımlayabilirsiniz [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/) veri bilimi topluluk yararlanması.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="9a7bb-107">Daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="9a7bb-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="9a7bb-108">Azure Market Ücretli gibi Azure Machine Learning web hizmetleri yayımlamak ya da dış müşterilere göre tüketimi için Hizmetleri serbest özelliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-108">The Azure Marketplace provides the ability to publish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="9a7bb-109">Bu makalede başlamanıza yardımcı olacak yönergeler için bağlantılar ile birlikte bu işlemine genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-109">This article provides an overview of that process with links to guidelines to get you started.</span></span> <span data-ttu-id="9a7bb-110">Bu işlemi kullanarak, web hizmetlerinizi diğer geliştiricilerin uygulamalarında kullanmak kullanılabilir yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-110">By using this process, you can make your web services available for other developers to consume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-the-publishing-process"></a><span data-ttu-id="9a7bb-111">Yayımlama işlemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="9a7bb-111">Overview of the publishing process</span></span>
<span data-ttu-id="9a7bb-112">Bir Azure Machine Learning web hizmeti Azure Marketinde yayımlama için adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9a7bb-112">The following are the steps for publishing an Azure Machine Learning web service to Azure Marketplace:</span></span>

1. <span data-ttu-id="9a7bb-113">Oluşturma ve makine öğrenme istek-yanıt hizmeti (RRS) yayımlama</span><span class="sxs-lookup"><span data-stu-id="9a7bb-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="9a7bb-114">Hizmeti üretime dağıtmak ve API anahtarı ve OData uç nokta bilgileri alın.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-114">Deploy the service to production, and obtain the API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="9a7bb-115">Yayımlamak için yayımlanan web hizmetinin URL'sini kullanın [Azure Marketi (veri Pazar)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="9a7bb-115">Use the URL of the published web service to publish to [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="9a7bb-116">Sonra gönderildi, teklifiniz incelenir ve müşterilerinizin önce onaylanması, satın almayı başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-116">Once submitted, your offer is reviewed and needs to be approved before your customers can start purchasing it.</span></span> <span data-ttu-id="9a7bb-117">Yayımlama işlemi birkaç iş gün sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-117">The publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="9a7bb-118">İzlenecek yol</span><span class="sxs-lookup"><span data-stu-id="9a7bb-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="9a7bb-119">1. adım: Oluşturma ve makine öğrenme istek-yanıt hizmeti (RRS) yayımlama</span><span class="sxs-lookup"><span data-stu-id="9a7bb-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="9a7bb-120">Siz bunu zaten yapmadıysanız, lütfen bu göz atın [size yol](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9a7bb-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-the-service-to-production-and-obtain-the-api-key-and-odata-endpoint-information"></a><span data-ttu-id="9a7bb-121">Adım 2: hizmeti üretime dağıtmak ve API anahtarı ve OData uç nokta bilgileri elde etmek</span><span class="sxs-lookup"><span data-stu-id="9a7bb-121">Step 2: Deploy the service to production, and obtain the API Key and OData endpoint information</span></span>
1. <span data-ttu-id="9a7bb-122">Gelen [Klasik Azure portalı](http://manage.windowsazure.com)seçin **MACHINE LEARNING** seçeneği sol gezinti çubuğu'ndan ve çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-122">From the [Azure Classic Portal](http://manage.windowsazure.com), select the **MACHINE LEARNING** option from the left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="9a7bb-123">Tıklayın **WEB Hizmetleri** sekmesini tıklatın ve Market'te yayımlamak istediğiniz web hizmetini seçin.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-123">Click on the **WEB SERVICES** tab, and select the web service you would like to publish to the marketplace.</span></span>
   
    ![Azure Market][workspace]
3. <span data-ttu-id="9a7bb-125">Tüketen Market olmasını istediğiniz uç nokta seçin.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-125">Select the endpoint you would like to have the marketplace consume.</span></span> <span data-ttu-id="9a7bb-126">Ek uç nokta oluşturmadıysanız, seçebileceğiniz **varsayılan** uç noktası.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-126">If you have not created any additional endpoints, you can select the **Default** endpoint.</span></span>
4. <span data-ttu-id="9a7bb-127">Uç noktada tıklattıktan sonra görmeye olacaktır **API anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-127">Once you have clicked on the endpoint, you will be able to see the **API KEY**.</span></span> <span data-ttu-id="9a7bb-128">Bu parça gerekir adım 3'te daha sonra daha fazla bilgi için bu nedenle bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Market][apikey]
5. <span data-ttu-id="9a7bb-130">Tıklayın **istek/yanıt** değil destekliyoruz Marketi'nde yayımlama toplu iş yürütme Hizmetleri bu noktada yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-130">Click on the **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services to the marketplace.</span></span> <span data-ttu-id="9a7bb-131">Sizi istek/yanıt yöntemi için API yardım sayfasına götürür.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-131">That will take you to the API help page for the Request/Response method.</span></span>
6. <span data-ttu-id="9a7bb-132">Kopya **OData uç noktası adresi**, adım 3'te daha sonra bu bilgilere ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-132">Copy the **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Market][odata]

<span data-ttu-id="9a7bb-134">Hizmet üretime dağıtma.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-134">deploy the service into production.</span></span>

### <a name="step-3-use-the-url-of-the-published-web-service-to-publish-to-azure-marketplace-datamarket"></a><span data-ttu-id="9a7bb-135">3. adım: Azure Marketi (DataMarket) yayımlamak için yayımlanan web hizmetinin URL'sini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-135">Step 3: Use the URL of the published web service to publish to Azure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="9a7bb-136">Gidin [Azure Market (veri Pazar)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="9a7bb-136">Navigate to [Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="9a7bb-137">Tıklayın **Yayımla** sayfanın üst kısmındaki bağlantı.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-137">Click on the **Publish** link at the top of the page.</span></span> <span data-ttu-id="9a7bb-138">Bu, olanak sürecek [Microsoft Azure yayımlama portalında](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="9a7bb-138">This will take you to the [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="9a7bb-139">Tıklayın **yayımcılar** bir yayımcı olarak kaydetmek için bölüm.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-139">Click on the **publishers** section to register as a publisher.</span></span>
4. <span data-ttu-id="9a7bb-140">Yeni bir teklif oluştururken seçin **Veri Hizmetleri**, ardından **yeni bir veri hizmeti oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Market][image1]
   
   <br />
5. <span data-ttu-id="9a7bb-142">Altında **planları** fiyatlandırma planı dahil olmak üzere, teklifi hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="9a7bb-143">Boş ya da Ücretli bir hizmet sunacaktır varsa karar verin.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="9a7bb-144">Ücretli için Banka ve vergi bilgilerinizi gibi ödeme bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-144">To get paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="9a7bb-145">Altında **pazarlama** başlığı ve açıklamayı teklifiniz için gibi teklifiniz hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-145">Under **Marketing** provide information about your offer, such as the title and description for your offer.</span></span>
7. <span data-ttu-id="9a7bb-146">Altında **fiyatlandırma** planlarınızı belirli ülkeler için fiyat ayarlamak veya "autoprice" Sistem teklifiniz olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-146">Under **Pricing** you can set the price for your plans for specific countries, or let the system "autoprice" your offer.</span></span>
8. <span data-ttu-id="9a7bb-147">Üzerinde **veri hizmeti** sekmesini tıklatın, **Web hizmeti** olarak **veri kaynağı**.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-147">On the **Data Service** tab, click **Web Service** as the **Data Source**.</span></span>
   
    ![Azure Market][image2]
9. <span data-ttu-id="9a7bb-149">Yukarıdaki 2. adımda açıklandığı gibi web hizmeti URL'sini ve API anahtarını Azure Klasik portalından alın.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-149">Get the web service URL and API key from the Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="9a7bb-150">OData uç nokta adresine Market veri hizmeti Kurulumu iletişim kutusuna yapıştırın **hizmeti URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-150">In the Marketplace Data Service setup dialog box, paste the OData endpoint address into the **Service URL** text box.</span></span>
11. <span data-ttu-id="9a7bb-151">İçin **kimlik doğrulaması**, seçin **üstbilgi** olarak **kimlik doğrulama düzeni**.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-151">For **Authentication**, choose **Header** as the **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="9a7bb-152">"Yetkilendirme" girin **üstbilgi adı**.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-152">Enter "Authorization" for the **Header Name**.</span></span>
    * <span data-ttu-id="9a7bb-153">İçin **üstbilgi değeri**, "Bearer" (tırnak işaretleri olmadan) girin, tıklatın **alanı** çubuk ve API anahtarını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-153">For the **Header Value**, enter "Bearer" (without the quotation marks), click the **Space** bar, and then paste the API key.</span></span>
    * <span data-ttu-id="9a7bb-154">Seçin **bu hizmetidir OData** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-154">Select the **This Service is OData** check box.</span></span>
    * <span data-ttu-id="9a7bb-155">Tıklatın **Bağlantıyı Sına** test edin.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-155">Click **Test Connection** to test the connection.</span></span>
12. <span data-ttu-id="9a7bb-156">Altında **kategorileri**, olun **Machine Learning** seçilir.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="9a7bb-157">İşiniz bittiğinde, teklif hakkında tüm meta veri girme tıklatın **Yayımla**ve ardından **anında hazırlık**.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-157">When you are done entering all the metadata about your offer, click on **Publish**, and then **Push to Staging**.</span></span> <span data-ttu-id="9a7bb-158">Bu noktada, düzeltmek için gereken tüm kalan sorunlarını bildirilir.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-158">At this point, you will be notified of any remaining issues that you need to fix.</span></span>
14. <span data-ttu-id="9a7bb-159">Tüm bekleyen sorunları tamamlanmasından doğruladıktan sonra tıklatın **üretime gönderme için onay isteği**.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-159">After you have ensured completion of all the outstanding issues, click on **Request approval to push to Production**.</span></span> <span data-ttu-id="9a7bb-160">Yayımlama işlemi birkaç iş gün sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9a7bb-160">The publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

