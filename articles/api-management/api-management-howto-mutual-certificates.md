---
title: "İstemci sertifikası kimlik doğrulaması - Azure API Management kullanarak aaaSecure arka uç hizmetlerini | Microsoft Docs"
description: "Nasıl toosecure arka uç hizmetlerini kullanan istemci sertifikası kimlik Azure API Management hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 565bb61044fed1158944202c36e8abe30edf5729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="7232d-103">Nasıl toosecure arka uç hizmetlerini kullanan istemci sertifikası kimlik Azure API Management</span><span class="sxs-lookup"><span data-stu-id="7232d-103">How toosecure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="7232d-104">API Management istemci sertifikalarını kullanan hello yetenek toosecure erişim toohello arka uç hizmetine bir API sağlar.</span><span class="sxs-lookup"><span data-stu-id="7232d-104">API Management provides hello capability toosecure access toohello back-end service of an API using client certificates.</span></span> <span data-ttu-id="7232d-105">Bu kılavuz toomanage hello API yayımcı portalında sertifikaları nasıl ve nasıl gösterir tooconfigure bir API toouse sertifika tooaccess onun arka uç hizmeti.</span><span class="sxs-lookup"><span data-stu-id="7232d-105">This guide shows how toomanage certificates in hello API publisher portal, and how tooconfigure an API toouse a certificate tooaccess its back-end service.</span></span>

<span data-ttu-id="7232d-106">Merhaba API Management REST API kullanarak sertifikaların yönetilmesi hakkında daha fazla bilgi için bkz: [Azure API Management REST API sertifikası varlık][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="7232d-106">For information about managing certificates using hello API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="7232d-107"><a name="prerequisites"></a>Önkoşulları</span><span class="sxs-lookup"><span data-stu-id="7232d-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="7232d-108">Bu kılavuz size nasıl tooconfigure için arka uç hizmeti, API Management hizmet örneği toouse istemci sertifikası kimlik doğrulaması tooaccess hello gösterir. bir API.</span><span class="sxs-lookup"><span data-stu-id="7232d-108">This guide shows you how tooconfigure your API Management service instance toouse client certificate authentication tooaccess hello back-end service for an API.</span></span> <span data-ttu-id="7232d-109">Bu konuda aşağıdaki hello adımları önce istemci sertifikası kimlik doğrulaması için yapılandırılmış, arka uç hizmetine sahip olmanız gerekir ([tooconfigure sertifika kimlik doğrulaması Azure Web sitelerine bakın toothis makale] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), ve erişim toohello sertifika ve hello hello API Management yayımcı portalında yüklemeyle hello sertifikanın parolasını sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7232d-109">Before following hello steps in this topic, you should have your back-end service configured for client certificate authentication ([tooconfigure certificate authentication in Azure WebSites refer toothis article][tooconfigure certificate authentication in Azure WebSites refer toothis article]), and have access toohello certificate and hello password for hello certificate for uploading in hello API Management publisher portal.</span></span>

## <span data-ttu-id="7232d-110"><a name="step1"></a>Bir istemci sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="7232d-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="7232d-111">başlatıldı, tooget tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="7232d-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="7232d-112">Bu toohello API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="7232d-112">This takes you toohello API Management publisher portal.</span></span>

![API yayımcı portalı][api-management-management-console]

> <span data-ttu-id="7232d-114">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7232d-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="7232d-115">Tıklatın **güvenlik** hello gelen **API Management** hello sol ve tıklatın menüsünde **istemci sertifikalarını**.</span><span class="sxs-lookup"><span data-stu-id="7232d-115">Click **Security** from hello **API Management** menu on hello left, and click **Client certificates**.</span></span>

![İstemci sertifikaları][api-management-security-client-certificates]

<span data-ttu-id="7232d-117">Yeni bir sertifika tooupload tıklatın **karşıya yükleme sertifika**.</span><span class="sxs-lookup"><span data-stu-id="7232d-117">tooupload a new certificate, click **Upload certificate**.</span></span>

![Sertifikayı karşıya yükleme][api-management-upload-certificate]

<span data-ttu-id="7232d-119">Tooyour sertifika göz atın ve sonra hello sertifikanın hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="7232d-119">Browse tooyour certificate, and then enter hello password for hello certificate.</span></span>

> <span data-ttu-id="7232d-120">Merhaba sertifika bulunmalıdır **.pfx** biçimi.</span><span class="sxs-lookup"><span data-stu-id="7232d-120">hello certificate must be in **.pfx** format.</span></span> <span data-ttu-id="7232d-121">Otomatik olarak imzalanan sertifikalar izin verilir.</span><span class="sxs-lookup"><span data-stu-id="7232d-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Sertifikayı karşıya yükleme][api-management-upload-certificate-form]

<span data-ttu-id="7232d-123">Tıklatın **karşıya** tooupload hello sertifika.</span><span class="sxs-lookup"><span data-stu-id="7232d-123">Click **Upload** tooupload hello certificate.</span></span>

> <span data-ttu-id="7232d-124">Merhaba sertifika parolası şu anda doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="7232d-124">hello certificate password is validated at this time.</span></span> <span data-ttu-id="7232d-125">Yanlış ise, bir hata iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7232d-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Karşıya sertifika][api-management-certificate-uploaded]

<span data-ttu-id="7232d-127">Merhaba sertifika yüklendikten sonra üzerinde hello göründüğü **istemci sertifikalarını** sekmesi. Birden fazla sertifika varsa, hello konu not edin veya bir API toouse yapılandırma sertifikaları, olan kullanılan tooselect hello sertifika hello aşağıdakileri anlatıldığı gibi son dört karakterini hello parmak izi, hello [yapılandırma bir API toouse Ağ Geçidi kimlik doğrulaması için bir istemci sertifikası] [ Configure an API toouse a client certificate for gateway authentication] bölümü.</span><span class="sxs-lookup"><span data-stu-id="7232d-127">Once hello certificate is uploaded, it appears on hello **Client certificates** tab. If you have multiple certificates, make a note of hello subject, or hello last four characters of hello thumbprint, which are used tooselect hello certificate when configuring an API toouse certificates, as covered in hello following [Configure an API toouse a client certificate for gateway authentication][Configure an API toouse a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="7232d-128">Örneğin, kendinden imzalı bir sertifika kullanırken, sertifika zinciri doğrulamasını devre dışı tooturn olarak bu SSS'de açıklanan hello adımları izleyin [öğesi](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span><span class="sxs-lookup"><span data-stu-id="7232d-128">tooturn off certificate chain validation when using, for example, a self-signed certificate, follow hello steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="7232d-129"><a name="step1a"></a>Bir istemci sertifikası silme</span><span class="sxs-lookup"><span data-stu-id="7232d-129"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="7232d-130">bir sertifika toodelete tıklatın **silmek** hello istenen sertifika yanında.</span><span class="sxs-lookup"><span data-stu-id="7232d-130">toodelete a certificate, click **Delete** beside hello desired certificate.</span></span>

![Sertifikayı Sil][api-management-certificate-delete]

<span data-ttu-id="7232d-132">Tıklatın **Evet, silmeden** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="7232d-132">Click **Yes, delete it** tooconfirm.</span></span>

![Silmeyi onayla][api-management-confirm-delete]

<span data-ttu-id="7232d-134">Merhaba sertifika bir API tarafından kullanılıyorsa, bir uyarı ekranı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7232d-134">If hello certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="7232d-135">Merhaba önce kaldırmalısınız toodelete hello sertifika sertifika yapılandırılmış toouse olan tüm API'lerinin bu.</span><span class="sxs-lookup"><span data-stu-id="7232d-135">toodelete hello certificate you must first remove hello certificate from any APIs that are configured toouse it.</span></span>

![Silmeyi onayla][api-management-confirm-delete-policy]

## <span data-ttu-id="7232d-137"><a name="step2"></a>API toouse Ağ Geçidi kimlik doğrulaması için bir istemci sertifikası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7232d-137"><a name="step2"> </a>Configure an API toouse a client certificate for gateway authentication</span></span>
<span data-ttu-id="7232d-138">Tıklatın **API'leri** hello gelen **API Management** hello menüsünde sol, istenen hello API hello adına tıklayın ve hello tıklatın **güvenlik** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="7232d-138">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, and click hello **Security** tab.</span></span>

![API Güvenlik][api-management-api-security]

<span data-ttu-id="7232d-140">Seçin **istemci sertifikalarını** hello gelen **kimlik bilgileriyle** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="7232d-140">Select **Client certificates** from hello **With credentials** drop-down list.</span></span>

![İstemci sertifikaları][api-management-mutual-certificates]

<span data-ttu-id="7232d-142">Select hello hello istenen sertifika **istemci sertifikası** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="7232d-142">Select hello desired certificate from hello **Client certificate** drop-down list.</span></span> <span data-ttu-id="7232d-143">Birden fazla sertifika varsa hello önceki bölümde toodetermine hello doğru sertifikaya belirtildiği gibi hello parmak izi son dört karakterini hello veya hello konu arayın.</span><span class="sxs-lookup"><span data-stu-id="7232d-143">If there are multiple certificates you can look at hello subject or hello last four characters of hello thumbprint as noted in hello previous section toodetermine hello correct certificate.</span></span>

![Sertifika Seç][api-management-select-certificate]

<span data-ttu-id="7232d-145">Tıklatın **kaydetmek** toosave hello yapılandırma değişikliği toohello API.</span><span class="sxs-lookup"><span data-stu-id="7232d-145">Click **Save** toosave hello configuration change toohello API.</span></span>

> <span data-ttu-id="7232d-146">Bu değişikliği hemen etkili olur ve bu API toooperations kullanacağı çağrıları sertifika tooauthenticate hello arka uç sunucusunda hello.</span><span class="sxs-lookup"><span data-stu-id="7232d-146">This change is effective immediately, and calls toooperations of that API will use hello certificate tooauthenticate on hello back-end server.</span></span>
> 
> 

![API Değişiklikleri Kaydet][api-management-save-api]

> <span data-ttu-id="7232d-148">Ağ Geçidi kimlik doğrulaması bir API için hello arka uç hizmeti için bir sertifika belirtildiğinde, bu API için hello ilkesinin bir parçası olur ve hello İlkesi Düzenleyicisi'nde görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="7232d-148">When a certificate is specified for gateway authentication for hello back-end service of an API, it becomes part of hello policy for that API, and can be viewed in hello policy editor.</span></span>
> 
> 

![Sertifika İlkesi][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="7232d-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7232d-150">Next steps</span></span>
<span data-ttu-id="7232d-151">HTTP temel veya paylaşılan gizli kimlik doğrulaması gibi arka uç hizmetinizin diğer yolları toosecure hakkında daha fazla bilgi için aşağıdaki videoyu hello bakın.</span><span class="sxs-lookup"><span data-stu-id="7232d-151">For more information on other ways toosecure your backend service, such as HTTP basic or shared secret authentication, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[tooconfigure certificate authentication in Azure WebSites refer toothis article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API toouse a client certificate for gateway authentication]: #step2
[Test hello configuration by calling an operation in hello Developer Portal]: #step3
[Next steps]: #next-steps



