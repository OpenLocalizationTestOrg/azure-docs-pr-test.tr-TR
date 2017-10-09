---
title: "Web hizmeti tooAzure Market öğrenme aaa(deprecated) Yayımla makine | Microsoft Docs"
description: "(kullanım dışı) Nasıl toopublish, Azure Machine Learning Web hizmeti toohello Azure Market"
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
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a><span data-ttu-id="9f5c8-103">(kullanım dışı) Azure Machine Learning Web hizmeti toohello Azure Marketi'nde yayımlama</span><span class="sxs-lookup"><span data-stu-id="9f5c8-103">(deprecated) Publish Azure Machine Learning Web Service toohello Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="9f5c8-104">DataMarket ve Veri Hizmetleri Çekildi ve mevcut abonelikleri kullanımdan kaldırılır ve başlangıç iptal 31/3/2017.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="9f5c8-105">Sonuç olarak, bu makalede onaylanmaz.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="9f5c8-106">Alternatif olarak, Machine Learning denemeleri toohello yayımlayabilirsiniz [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/) hello veri bilimi topluluğunun hello avantajı için.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-106">As an alternative, you can publish your Machine Learning experiments toohello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for hello benefit of hello data science community.</span></span> <span data-ttu-id="9f5c8-107">Daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="9f5c8-107">For more information, see [Share and discover resources in hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="9f5c8-108">Hello Azure Marketi hello toopublish Azure Machine Learning web hizmetleri ücretli olarak sağlayabilir veya dış müşterilere göre tüketimi için Hizmetleri boşaltın.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-108">hello Azure Marketplace provides hello ability toopublish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="9f5c8-109">Bu makalede başlattığınız bağlantılar tooguidelines tooget bu işlemine genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-109">This article provides an overview of that process with links tooguidelines tooget you started.</span></span> <span data-ttu-id="9f5c8-110">Bu işlemi kullanarak, web hizmetlerinizi diğer geliştiriciler tooconsume için kullanılabilir uygulamalarında yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-110">By using this process, you can make your web services available for other developers tooconsume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a><span data-ttu-id="9f5c8-111">İşlem yayımlama hello genel bakış</span><span class="sxs-lookup"><span data-stu-id="9f5c8-111">Overview of hello publishing process</span></span>
<span data-ttu-id="9f5c8-112">Merhaba, bir Azure Machine Learning web hizmeti tooAzure Market yayımlama hello adımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9f5c8-112">hello following are hello steps for publishing an Azure Machine Learning web service tooAzure Marketplace:</span></span>

1. <span data-ttu-id="9f5c8-113">Oluşturma ve makine öğrenme istek-yanıt hizmeti (RRS) yayımlama</span><span class="sxs-lookup"><span data-stu-id="9f5c8-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="9f5c8-114">Merhaba hizmet tooproduction dağıtmak ve hello API anahtarı ve OData uç nokta bilgileri alın.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-114">Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="9f5c8-115">Hello kullan hello URL'sini yayımlanan web hizmeti toopublish çok[Azure Marketi (veri Pazar)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="9f5c8-115">Use hello URL of hello published web service toopublish too[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="9f5c8-116">Sonra gönderildi, teklifiniz incelenir ve bu satın alma, müşterilerinizin önce onaylanan toobe başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-116">Once submitted, your offer is reviewed and needs toobe approved before your customers can start purchasing it.</span></span> <span data-ttu-id="9f5c8-117">Merhaba yayımlama işlemi birkaç iş gün sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-117">hello publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="9f5c8-118">İzlenecek yol</span><span class="sxs-lookup"><span data-stu-id="9f5c8-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="9f5c8-119">1. adım: Oluşturma ve makine öğrenme istek-yanıt hizmeti (RRS) yayımlama</span><span class="sxs-lookup"><span data-stu-id="9f5c8-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="9f5c8-120">Siz bunu zaten yapmadıysanız, lütfen bu göz atın [size yol](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9f5c8-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a><span data-ttu-id="9f5c8-121">2. adım: hello hizmet tooproduction dağıtmak ve hello API anahtarı ve OData uç nokta bilgileri alın</span><span class="sxs-lookup"><span data-stu-id="9f5c8-121">Step 2: Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information</span></span>
1. <span data-ttu-id="9f5c8-122">Merhaba gelen [Klasik Azure portalı](http://manage.windowsazure.com)seçin hello **MACHINE LEARNING** seçeneği hello sol gezinti çubuğunda ve çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-122">From hello [Azure Classic Portal](http://manage.windowsazure.com), select hello **MACHINE LEARNING** option from hello left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="9f5c8-123">Tıklatın hello üzerinde **WEB Hizmetleri** sekmesi ve toopublish toohello Market istediğinizi seçin hello web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-123">Click on hello **WEB SERVICES** tab, and select hello web service you would like toopublish toohello marketplace.</span></span>
   
    ![Azure Market][workspace]
3. <span data-ttu-id="9f5c8-125">Select hello uç noktası, toohave hello Market gibi kullanır.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-125">Select hello endpoint you would like toohave hello marketplace consume.</span></span> <span data-ttu-id="9f5c8-126">Ek uç nokta oluşturmadıysanız hello seçebilirsiniz **varsayılan** uç noktası.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-126">If you have not created any additional endpoints, you can select hello **Default** endpoint.</span></span>
4. <span data-ttu-id="9f5c8-127">Merhaba noktadaki tıklattıktan sonra mümkün toosee hello olacaktır **API anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-127">Once you have clicked on hello endpoint, you will be able toosee hello **API KEY**.</span></span> <span data-ttu-id="9f5c8-128">Bu parça gerekir adım 3'te daha sonra daha fazla bilgi için bu nedenle bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Market][apikey]
5. <span data-ttu-id="9f5c8-130">Tıklatın hello üzerinde **istek/yanıt** değil destekliyoruz yayımlama toplu iş yürütme bu noktada yöntemi toohello Market Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-130">Click on hello **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services toohello marketplace.</span></span> <span data-ttu-id="9f5c8-131">Sizi hello istek/yanıt yöntemi yönelik toohello API yardım sayfasına götürür.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-131">That will take you toohello API help page for hello Request/Response method.</span></span>
6. <span data-ttu-id="9f5c8-132">Kopya hello **OData uç noktası adresi**, adım 3'te daha sonra bu bilgilere ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-132">Copy hello **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Market][odata]

<span data-ttu-id="9f5c8-134">Merhaba hizmeti üretime dağıtma.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-134">deploy hello service into production.</span></span>

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a><span data-ttu-id="9f5c8-135">3. adım: Web hizmeti toopublish tooAzure Market (DataMarket) hello kullan hello URL'sini yayımlanan</span><span class="sxs-lookup"><span data-stu-id="9f5c8-135">Step 3: Use hello URL of hello published web service toopublish tooAzure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="9f5c8-136">Çok gidin[Azure Marketi (veri Pazar)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="9f5c8-136">Navigate too[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="9f5c8-137">Tıklatın hello üzerinde **Yayımla** hello sayfanın üst kısmındaki hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-137">Click on hello **Publish** link at hello top of hello page.</span></span> <span data-ttu-id="9f5c8-138">Bu toohello sürecek [Microsoft Azure yayımlama portalında](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="9f5c8-138">This will take you toohello [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="9f5c8-139">Tıklatın hello üzerinde **yayımcılar** bölüm tooregister bir yayımcı olarak.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-139">Click on hello **publishers** section tooregister as a publisher.</span></span>
4. <span data-ttu-id="9f5c8-140">Yeni bir teklif oluştururken seçin **Veri Hizmetleri**, ardından **yeni bir veri hizmeti oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Market][image1]
   
   <br />
5. <span data-ttu-id="9f5c8-142">Altında **planları** fiyatlandırma planı dahil olmak üzere, teklifi hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="9f5c8-143">Boş ya da Ücretli bir hizmet sunacaktır varsa karar verin.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="9f5c8-144">Ücretli, tooget banka ve vergi bilgilerinizi gibi ödeme bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-144">tooget paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="9f5c8-145">Altında **pazarlama** teklifiniz için hello başlık ve açıklama gibi teklifiniz hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-145">Under **Marketing** provide information about your offer, such as hello title and description for your offer.</span></span>
7. <span data-ttu-id="9f5c8-146">Altında **fiyatlandırma** planlarınızı belirli ülkeler için için hello fiyat ayarlayabilir veya hello sistem "autoprice" teklifiniz olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-146">Under **Pricing** you can set hello price for your plans for specific countries, or let hello system "autoprice" your offer.</span></span>
8. <span data-ttu-id="9f5c8-147">Merhaba üzerinde **veri hizmeti** sekmesini tıklatın, **Web hizmeti** hello olarak **veri kaynağı**.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-147">On hello **Data Service** tab, click **Web Service** as hello **Data Source**.</span></span>
   
    ![Azure Market][image2]
9. <span data-ttu-id="9f5c8-149">Merhaba, web hizmeti URL'sini ve API anahtarını yukarıda 2. adımda açıklandığı gibi Klasik Azure portalı, hello alın.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-149">Get hello web service URL and API key from hello Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="9f5c8-150">Merhaba Market veri hizmeti Kurulumu iletişim kutusunda, hello OData uç noktası adresi hello yapıştırma **hizmeti URL'si** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-150">In hello Marketplace Data Service setup dialog box, paste hello OData endpoint address into hello **Service URL** text box.</span></span>
11. <span data-ttu-id="9f5c8-151">İçin **kimlik doğrulaması**, seçin **üstbilgi** hello olarak **kimlik doğrulama düzeni**.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-151">For **Authentication**, choose **Header** as hello **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="9f5c8-152">"Yetkilendirme" Merhaba girin **üstbilgi adı**.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-152">Enter "Authorization" for hello **Header Name**.</span></span>
    * <span data-ttu-id="9f5c8-153">Hello için **üstbilgi değeri**, "Bearer" (Merhaba tırnak işaretleri olmadan) girin, hello tıklatın **alanı** çubuk ve hello API anahtarını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-153">For hello **Header Value**, enter "Bearer" (without hello quotation marks), click hello **Space** bar, and then paste hello API key.</span></span>
    * <span data-ttu-id="9f5c8-154">Select hello **bu hizmetidir OData** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-154">Select hello **This Service is OData** check box.</span></span>
    * <span data-ttu-id="9f5c8-155">Tıklatın **Bağlantıyı Sına** tootest hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-155">Click **Test Connection** tootest hello connection.</span></span>
12. <span data-ttu-id="9f5c8-156">Altında **kategorileri**, olun **Machine Learning** seçilir.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="9f5c8-157">İşiniz bittiğinde meta verileri hello tüm girme teklifiniz hakkında tıklayın **Yayımla**ve ardından **anında tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-157">When you are done entering all hello metadata about your offer, click on **Publish**, and then **Push tooStaging**.</span></span> <span data-ttu-id="9f5c8-158">Bu noktada, tüm kalan sorunlarını toofix gerektiğini bildirilir.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-158">At this point, you will be notified of any remaining issues that you need toofix.</span></span>
14. <span data-ttu-id="9f5c8-159">Tüm hello bekleyen sorunları tamamlanmasından doğruladıktan sonra tıklatın **isteği onay toopush tooProduction**.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-159">After you have ensured completion of all hello outstanding issues, click on **Request approval toopush tooProduction**.</span></span> <span data-ttu-id="9f5c8-160">Merhaba yayımlama işlemi birkaç iş gün sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9f5c8-160">hello publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

