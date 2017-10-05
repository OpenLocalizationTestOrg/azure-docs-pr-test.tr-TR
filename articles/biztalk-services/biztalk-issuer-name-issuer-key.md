---
title: "Verenin adı ve verenin anahtarı BizTalk Services | Microsoft Docs"
description: "Hizmet veri yolu veya BizTalk Services erişim denetimi (ACS) verenin adı ve verenin anahtarı almak öğrenin. MABS, WABS"
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
ms.openlocfilehash: b9fd985c23558596408e78eadae00dd0f95c4214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="d4682-104">BizTalk Services: Verenin Adı ve Verenin Anahtarı</span><span class="sxs-lookup"><span data-stu-id="d4682-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="d4682-105">Azure BizTalk Services, hizmet veri yolu verenin adı ve verenin anahtarı ve erişim denetimi verenin adı ve verenin anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4682-105">Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="d4682-106">Bu avantajlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d4682-106">Specifically:</span></span>

| <span data-ttu-id="d4682-107">Görev</span><span class="sxs-lookup"><span data-stu-id="d4682-107">Task</span></span> | <span data-ttu-id="d4682-108">Hangi verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="d4682-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="d4682-109">Uygulamanızı Visual Studio'dan dağıtma</span><span class="sxs-lookup"><span data-stu-id="d4682-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="d4682-110">Erişim denetimi verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="d4682-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="d4682-111">Azure BizTalk Services Portalı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d4682-111">Configuring the Azure BizTalk Services Portal</span></span> |<span data-ttu-id="d4682-112">Erişim denetimi verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="d4682-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="d4682-113">Visual Studio'da BizTalk Bağdaştırıcısı hizmetleriyle LOB geçişler oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4682-113">Creating LOB Relays with the BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="d4682-114">Hizmet veri yolu verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="d4682-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="d4682-115">Bu konu verenin adı ve verenin anahtarı almak için adımlar listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d4682-115">This topic lists the steps to retrieve the Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="d4682-116">Erişim denetimi verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="d4682-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="d4682-117">Erişim denetimi verenin adı ve verenin anahtarı aşağıdaki tarafından kullanılır:</span><span class="sxs-lookup"><span data-stu-id="d4682-117">The Access Control Issuer Name and Issuer Key are used by the following:</span></span>

* <span data-ttu-id="d4682-118">Visual Studio'da oluşturulan Azure BizTalk hizmeti uygulamanız: başarıyla Visual Studio'da BizTalk hizmeti uygulamanızı Azure'a dağıtmak için erişim denetimi verenin adı ve verenin anahtarı girin.</span><span class="sxs-lookup"><span data-stu-id="d4682-118">Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="d4682-119">Azure BizTalk Services portalı: BizTalk hizmeti oluşturma ve BizTalk Services Portalı'nı açın, erişim denetimi verenin adı ve verenin anahtarı otomatik olarak dağıtımlarınızın aynı erişim denetimi değerleri ile kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d4682-119">The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.</span></span>

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="d4682-120">Erişim denetimi verenin adı ve verenin anahtarı edinin</span><span class="sxs-lookup"><span data-stu-id="d4682-120">Get the Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="d4682-121">ACS kimlik doğrulaması için kullanmak ve verenin adı ve verenin anahtarı değerlerini almak için genel adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="d4682-121">To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:</span></span>

1. <span data-ttu-id="d4682-122">Yükleme [Azure Powershell cmdlet'lerini](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="d4682-122">Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="d4682-123">Azure hesabınızda ekleyin:`Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="d4682-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="d4682-124">Abonelik adı döndürün:`get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="d4682-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="d4682-125">Aboneliğinizi seçin:`select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="d4682-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="d4682-126">Yeni bir ad alanı oluşturun:`new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="d4682-126">Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="d4682-127">Örnek:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="d4682-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="d4682-128">Yeni ACS ad alanı (Bu, birkaç dakika sürebilir) oluşturulduğunda, verenin adı ve verenin anahtarı değerlerini bağlantı dizesinde listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="d4682-128">When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string:</span></span> 

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

<span data-ttu-id="d4682-129">Özetlemek için:</span><span class="sxs-lookup"><span data-stu-id="d4682-129">To summarize:</span></span>  
<span data-ttu-id="d4682-130">Verenin adı SharedSecretIssuer =</span><span class="sxs-lookup"><span data-stu-id="d4682-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="d4682-131">Verenin anahtarı SharedSecretKey =</span><span class="sxs-lookup"><span data-stu-id="d4682-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="d4682-132">Daha açık [yeni AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="d4682-132">More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="d4682-133">Hizmet veri yolu verenin adı ve verenin anahtarı</span><span class="sxs-lookup"><span data-stu-id="d4682-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="d4682-134">Hizmet veri yolu verenin adı ve verenin anahtarı BizTalk Bağdaştırıcısı Hizmetleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d4682-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="d4682-135">BizTalk Services projenizde Visual Studio, bir şirket içi iş kolu (LOB) sistemine bağlamak için BizTalk Bağdaştırıcısı Hizmetleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4682-135">In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="d4682-136">Bağlanmak için LOB geçişi oluşturmak ve LOB Sistem bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="d4682-136">To connect, you create the LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="d4682-137">Bunu yaparken hizmet veri yolu verenin adı ve verenin anahtarı da girin.</span><span class="sxs-lookup"><span data-stu-id="d4682-137">When doing this, you also enter the Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="d4682-138">Hizmet veri yolu verenin adı ve verenin anahtarı almak için</span><span class="sxs-lookup"><span data-stu-id="d4682-138">To retrieve the Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="d4682-139">[Klasik Azure portalında](http://go.microsoft.com/fwlink/p/?LinkID=213885) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d4682-139">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d4682-140">Sol gezinti bölmesinde seçin **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="d4682-140">In the left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="d4682-141">Ad alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="d4682-141">Select your namespace.</span></span> <span data-ttu-id="d4682-142">Görev çubuğunda seçin **bağlantı bilgilerini**.</span><span class="sxs-lookup"><span data-stu-id="d4682-142">In the task bar, select **Connection Information**.</span></span> <span data-ttu-id="d4682-143">Bu görüntüler **varsayılan veren** (verenin adı) ve **varsayılan anahtar** (verenin anahtarı).</span><span class="sxs-lookup"><span data-stu-id="d4682-143">This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="d4682-144">Değerlerine kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="d4682-144">Their values can be copied.</span></span>  

<span data-ttu-id="d4682-145">Özetlemek için:</span><span class="sxs-lookup"><span data-stu-id="d4682-145">To summarize:</span></span>  
<span data-ttu-id="d4682-146">Verenin adı varsayılan veren =</span><span class="sxs-lookup"><span data-stu-id="d4682-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="d4682-147">Verenin anahtarı = varsayılan anahtar</span><span class="sxs-lookup"><span data-stu-id="d4682-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="d4682-148">Sonraki</span><span class="sxs-lookup"><span data-stu-id="d4682-148">Next</span></span>
<span data-ttu-id="d4682-149">Ek Azure BizTalk Services konuları:</span><span class="sxs-lookup"><span data-stu-id="d4682-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="d4682-150">Azure BizTalk Services SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="d4682-150">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="d4682-151">Öğretici: Azure BizTalk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="d4682-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="d4682-152">Azure BizTalk Services SDK'sını Kullanmaya Nasıl Başlarım</span><span class="sxs-lookup"><span data-stu-id="d4682-152">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="d4682-153">Azure BizTalk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="d4682-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="d4682-154">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="d4682-154">See Also</span></span>
* [<span data-ttu-id="d4682-155">Nasıl yapılır: hizmet kimlikleri yapılandırmak için ACS yönetim hizmeti kullanın</span><span class="sxs-lookup"><span data-stu-id="d4682-155">How to: Use ACS Management Service to Configure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="d4682-156">BizTalk Services: Geliştirici, temel, standart ve Premium sürümler grafiği</span><span class="sxs-lookup"><span data-stu-id="d4682-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="d4682-157">BizTalk Services: Klasik portalı kullanarak Azure hazırlama</span><span class="sxs-lookup"><span data-stu-id="d4682-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="d4682-158">BizTalk Services: Durum Grafiğini hazırlama</span><span class="sxs-lookup"><span data-stu-id="d4682-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="d4682-159">BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri</span><span class="sxs-lookup"><span data-stu-id="d4682-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="d4682-160">BizTalk Services: Yedekleme ve Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="d4682-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="d4682-161">BizTalk Services: Azaltma</span><span class="sxs-lookup"><span data-stu-id="d4682-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

