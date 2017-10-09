---
title: "aaaIssuer adı ve verenin anahtarı BizTalk Services | Microsoft Docs"
description: "Bilgi tooretrieve verenle nasıl ve verenin anahtarı için hizmet veri yolu veya BizTalk Services erişim denetimi (ACS). MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="95795-104">BizTalk Services: Verenin Adı ve Verenin Anahtarı</span><span class="sxs-lookup"><span data-stu-id="95795-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="95795-105">Azure BizTalk Services hello hizmet veri yolu verenin adı ve verenin anahtarı ve hello erişim denetimi verenin adı ve verenin anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="95795-105">Azure BizTalk Services uses hello Service Bus Issuer Name and Issuer Key, and hello Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="95795-106">Bu avantajlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="95795-106">Specifically:</span></span>

| <span data-ttu-id="95795-107">Görev</span><span class="sxs-lookup"><span data-stu-id="95795-107">Task</span></span> | <span data-ttu-id="95795-108">Hangi verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="95795-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="95795-109">Uygulamanızı Visual Studio'dan dağıtma</span><span class="sxs-lookup"><span data-stu-id="95795-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="95795-110">Erişim denetimi verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="95795-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="95795-111">Hello Azure BizTalk Services portalı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="95795-111">Configuring hello Azure BizTalk Services Portal</span></span> |<span data-ttu-id="95795-112">Erişim denetimi verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="95795-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="95795-113">LOB geçişler hello Visual Studio'da BizTalk Bağdaştırıcısı hizmetleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="95795-113">Creating LOB Relays with hello BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="95795-114">Hizmet veri yolu verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="95795-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="95795-115">Bu konu, hello adımları tooretrieve hello verenin adı ve verenin anahtarı listeler.</span><span class="sxs-lookup"><span data-stu-id="95795-115">This topic lists hello steps tooretrieve hello Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="95795-116">Erişim denetimi verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="95795-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="95795-117">Merhaba erişim denetimi verenin adı ve verenin anahtarı hello aşağıdaki tarafından kullanılır:</span><span class="sxs-lookup"><span data-stu-id="95795-117">hello Access Control Issuer Name and Issuer Key are used by hello following:</span></span>

* <span data-ttu-id="95795-118">Visual Studio'da oluşturulan Azure BizTalk hizmeti uygulamanız: toosuccessfully BizTalk hizmeti uygulamanızda Visual Studio tooAzure dağıtmak, hello erişim denetimi verenin adı ve verenin anahtarı girin.</span><span class="sxs-lookup"><span data-stu-id="95795-118">Your Azure BizTalk Service application created in Visual Studio: toosuccessfully deploy your BizTalk Service application in Visual Studio tooAzure, you enter hello Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="95795-119">Hello Azure BizTalk Services portalı: BizTalk hizmeti oluşturma ve hello BizTalk Services portalı, erişim denetimi veren adınızı açın ve verenin anahtarı, dağıtımlar için kayıtlı otomatik olarak aynı erişim denetimi değerleri hello.</span><span class="sxs-lookup"><span data-stu-id="95795-119">hello Azure BizTalk Services  Portal: When you create a BizTalk Service and open hello BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with hello same Access Control values.</span></span>

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="95795-120">Alma erişim denetimi verenin adı ve verenin anahtarı hello</span><span class="sxs-lookup"><span data-stu-id="95795-120">Get hello Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="95795-121">kimlik doğrulaması ve get toouse ACS Merhaba verenin adı ve verenin anahtarı değerlerini, hello genel adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="95795-121">toouse ACS for authentication, and get hello Issuer Name and Issuer Key values, hello overall steps include:</span></span>

1. <span data-ttu-id="95795-122">Merhaba yüklemek [Azure Powershell cmdlet'lerini](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="95795-122">Install hello [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="95795-123">Azure hesabınızda ekleyin:`Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="95795-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="95795-124">Abonelik adı döndürün:`get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="95795-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="95795-125">Aboneliğinizi seçin:`select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="95795-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="95795-126">Yeni bir ad alanı oluşturun:`new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="95795-126">Create a new namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="95795-127">Örnek:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="95795-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="95795-128">Merhaba yeni ACS ad alanı (Bu, birkaç dakika sürebilir) oluşturulduğunda hello verenin adı ve verenin anahtarı değerlerini hello bağlantı dizesinde listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="95795-128">When hello new ACS namespace is created (which can take several minutes), hello Issuer Name and Issuer Key values are listed in hello connection string:</span></span> 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

<span data-ttu-id="95795-129">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="95795-129">toosummarize:</span></span>  
<span data-ttu-id="95795-130">Verenin adı SharedSecretIssuer =</span><span class="sxs-lookup"><span data-stu-id="95795-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="95795-131">Verenin anahtarı SharedSecretKey =</span><span class="sxs-lookup"><span data-stu-id="95795-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="95795-132">Merhaba hakkında daha fazla [yeni AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="95795-132">More on hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="95795-133">Hizmet veri yolu verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="95795-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="95795-134">Hizmet veri yolu verenin adı ve verenin anahtarı BizTalk Bağdaştırıcısı Hizmetleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="95795-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="95795-135">Visual Studio'da, BizTalk Services projenizdeki hello BizTalk Bağdaştırıcısı Hizmetleri tooconnect tooan şirket içi iş kolu (LOB) sistemine kullanın.</span><span class="sxs-lookup"><span data-stu-id="95795-135">In your BizTalk Services project in Visual Studio, you use hello BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="95795-136">tooconnect, hello LOB geçiş oluşturun ve LOB Sistem bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="95795-136">tooconnect, you create hello LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="95795-137">Bunu yaparken hello hizmet veri yolu verenin adı ve verenin anahtarı da girin.</span><span class="sxs-lookup"><span data-stu-id="95795-137">When doing this, you also enter hello Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="95795-138">tooretrieve hello hizmet veri yolu verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="95795-138">tooretrieve hello Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="95795-139">İçinde toohello oturum [Klasik Azure portalı](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="95795-139">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="95795-140">Merhaba sol gezinti bölmesinde seçin **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="95795-140">In hello left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="95795-141">Ad alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="95795-141">Select your namespace.</span></span> <span data-ttu-id="95795-142">Merhaba görev çubuğunda seçin **bağlantı bilgilerini**.</span><span class="sxs-lookup"><span data-stu-id="95795-142">In hello task bar, select **Connection Information**.</span></span> <span data-ttu-id="95795-143">Bu hello görüntüler **varsayılan veren** (verenin adı) ve **varsayılan anahtar** (verenin anahtarı).</span><span class="sxs-lookup"><span data-stu-id="95795-143">This displays hello **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="95795-144">Değerlerine kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="95795-144">Their values can be copied.</span></span>  

<span data-ttu-id="95795-145">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="95795-145">toosummarize:</span></span>  
<span data-ttu-id="95795-146">Verenin adı varsayılan veren =</span><span class="sxs-lookup"><span data-stu-id="95795-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="95795-147">Verenin anahtarı = varsayılan anahtar</span><span class="sxs-lookup"><span data-stu-id="95795-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="95795-148">Sonraki</span><span class="sxs-lookup"><span data-stu-id="95795-148">Next</span></span>
<span data-ttu-id="95795-149">Ek Azure BizTalk Services konuları:</span><span class="sxs-lookup"><span data-stu-id="95795-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="95795-150">Hello Azure BizTalk Services SDK'sını yükleme</span><span class="sxs-lookup"><span data-stu-id="95795-150">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="95795-151">Öğretici: Azure BizTalk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="95795-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="95795-152">I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello</span><span class="sxs-lookup"><span data-stu-id="95795-152">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="95795-153">Azure BizTalk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="95795-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="95795-154">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="95795-154">See Also</span></span>
* [<span data-ttu-id="95795-155">Nasıl yapılır: kullanım ACS yönetim hizmeti tooConfigure hizmet kimlikleri</span><span class="sxs-lookup"><span data-stu-id="95795-155">How to: Use ACS Management Service tooConfigure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="95795-156">BizTalk Services: Geliştirici, temel, standart ve Premium sürümler grafiği</span><span class="sxs-lookup"><span data-stu-id="95795-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="95795-157">BizTalk Services: Klasik portalı kullanarak Azure hazırlama</span><span class="sxs-lookup"><span data-stu-id="95795-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="95795-158">BizTalk Services: Durum Grafiğini hazırlama</span><span class="sxs-lookup"><span data-stu-id="95795-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="95795-159">BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri</span><span class="sxs-lookup"><span data-stu-id="95795-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="95795-160">BizTalk Services: Yedekleme ve Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="95795-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="95795-161">BizTalk Services: Azaltma</span><span class="sxs-lookup"><span data-stu-id="95795-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

