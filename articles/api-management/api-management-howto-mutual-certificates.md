---
title: "Arka uç hizmetlerini kullanan istemci güvenli sertifika kimlik doğrulaması - Azure API Management | Microsoft Docs"
description: "Azure API Management'te istemci sertifikası kimlik doğrulaması kullanarak arka uç hizmetlerini güvence altına alma hakkında bilgi edinin."
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
ms.openlocfilehash: 2ebe71c96fd9076a48f689041634dbd23d3d8414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="d94e4-103">Arka uç hizmetlerini kullanan istemci sertifikası kimlik doğrulaması Azure API Management'te güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="d94e4-103">How to secure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="d94e4-104">API Management istemci sertifikalarını kullanan güvenli bir API'nin arka uç hizmetine erişim olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d94e4-104">API Management provides the capability to secure access to the back-end service of an API using client certificates.</span></span> <span data-ttu-id="d94e4-105">Bu kılavuz, API yayımcı portalına sertifikaları yönetme ve arka uç hizmetine erişmek için bir sertifika kullanmak üzere bir API yapılandırma gösterir.</span><span class="sxs-lookup"><span data-stu-id="d94e4-105">This guide shows how to manage certificates in the API publisher portal, and how to configure an API to use a certificate to access its back-end service.</span></span>

<span data-ttu-id="d94e4-106">API Management REST API kullanarak sertifikaların yönetilmesi hakkında daha fazla bilgi için bkz: [Azure API Management REST API sertifikası varlık][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="d94e4-106">For information about managing certificates using the API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="d94e4-107"><a name="prerequisites"></a>Önkoşulları</span><span class="sxs-lookup"><span data-stu-id="d94e4-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="d94e4-108">Bu kılavuz bir API arka uç hizmetine erişim için istemci sertifikası kimlik doğrulamasını kullanmak için API Management hizmet örneği yapılandırmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="d94e4-108">This guide shows you how to configure your API Management service instance to use client certificate authentication to access the back-end service for an API.</span></span> <span data-ttu-id="d94e4-109">Bu konudaki adımları izlemeden önce arka uç hizmeti istemci sertifikası kimlik doğrulaması için yapılandırılmış olması gerekir ([Azure Web siteleri sertifika kimlik doğrulaması yapılandırmak için bu makalesine başvurun][to configure certificate authentication in Azure WebSites refer to this article]), ve sertifika ve parola için API Management yayımcı Portalı'nda yüklemeyle sertifikanın erişebilir.</span><span class="sxs-lookup"><span data-stu-id="d94e4-109">Before following the steps in this topic, you should have your back-end service configured for client certificate authentication ([to configure certificate authentication in Azure WebSites refer to this article][to configure certificate authentication in Azure WebSites refer to this article]), and have access to the certificate and the password for the certificate for uploading in the API Management publisher portal.</span></span>

## <span data-ttu-id="d94e4-110"><a name="step1"></a>Bir istemci sertifikasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="d94e4-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="d94e4-111">Kullanmaya başlamak için API Management hizmetiniz için Azure Portal'da **Yayımcı portalı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d94e4-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="d94e4-112">Bu sizi API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="d94e4-112">This takes you to the API Management publisher portal.</span></span>

![API yayımcı portalı][api-management-management-console]

> <span data-ttu-id="d94e4-114">Henüz bir API Management hizmeti örneği oluşturmadıysanız, [Azure API Management'i kullanmaya başlama][Get started with Azure API Management] öğreticisinde [API Management hizmet örneği oluşturma][Create an API Management service instance]'ya bakın.</span><span class="sxs-lookup"><span data-stu-id="d94e4-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="d94e4-115">Tıklatın **güvenlik** gelen **API Management** sol ve tıklatın menüsünde **istemci sertifikalarını**.</span><span class="sxs-lookup"><span data-stu-id="d94e4-115">Click **Security** from the **API Management** menu on the left, and click **Client certificates**.</span></span>

![İstemci sertifikaları][api-management-security-client-certificates]

<span data-ttu-id="d94e4-117">Yeni sertifikayı karşıya yüklemek için tıklayın **karşıya yükleme sertifika**.</span><span class="sxs-lookup"><span data-stu-id="d94e4-117">To upload a new certificate, click **Upload certificate**.</span></span>

![Sertifikayı karşıya yükleme][api-management-upload-certificate]

<span data-ttu-id="d94e4-119">Sertifikanızı göz atın ve sonra sertifikanın parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="d94e4-119">Browse to your certificate, and then enter the password for the certificate.</span></span>

> <span data-ttu-id="d94e4-120">Sertifika olmalıdır **.pfx** biçimi.</span><span class="sxs-lookup"><span data-stu-id="d94e4-120">The certificate must be in **.pfx** format.</span></span> <span data-ttu-id="d94e4-121">Otomatik olarak imzalanan sertifikalar izin verilir.</span><span class="sxs-lookup"><span data-stu-id="d94e4-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Sertifikayı karşıya yükleme][api-management-upload-certificate-form]

<span data-ttu-id="d94e4-123">Tıklatın **karşıya** sertifikayı karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="d94e4-123">Click **Upload** to upload the certificate.</span></span>

> <span data-ttu-id="d94e4-124">Sertifika parolası şu anda doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="d94e4-124">The certificate password is validated at this time.</span></span> <span data-ttu-id="d94e4-125">Yanlış ise, bir hata iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d94e4-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Karşıya sertifika][api-management-certificate-uploaded]

<span data-ttu-id="d94e4-127">Sertifika yüklendikten sonra göründüğü **istemci sertifikalarını** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d94e4-127">Once the certificate is uploaded, it appears on the **Client certificates** tab.</span></span> <span data-ttu-id="d94e4-128">Birden fazla sertifika varsa, konu not ya da parmak izi sertifikalarını kullanmak için bir API aşağıdakileri anlatıldığı gibi yapılandırırken sertifikayı seçmek için kullanılan son dört karakterini olun [bir API Ağ Geçidi kimlik doğrulaması için bir istemci sertifikası kullanacak şekilde yapılandırma] [ Configure an API to use a client certificate for gateway authentication] bölümü.</span><span class="sxs-lookup"><span data-stu-id="d94e4-128">If you have multiple certificates, make a note of the subject, or the last four characters of the thumbprint, which are used to select the certificate when configuring an API to use certificates, as covered in the following [Configure an API to use a client certificate for gateway authentication][Configure an API to use a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="d94e4-129">Sertifika zinciri doğrulamasını devre dışı, örneğin, kullanırken otomatik olarak imzalanan bir sertifika açmak için bu SSS bölümünde açıklanan adımları izleyin [öğesi](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span><span class="sxs-lookup"><span data-stu-id="d94e4-129">To turn off certificate chain validation when using, for example, a self-signed certificate, follow the steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="d94e4-130"><a name="step1a"></a>Bir istemci sertifikası silme</span><span class="sxs-lookup"><span data-stu-id="d94e4-130"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="d94e4-131">Bir sertifikayı silmek için tıklatın **silmek** istenen sertifikanın yanındaki.</span><span class="sxs-lookup"><span data-stu-id="d94e4-131">To delete a certificate, click **Delete** beside the desired certificate.</span></span>

![Sertifikayı Sil][api-management-certificate-delete]

<span data-ttu-id="d94e4-133">Tıklatın **Evet, silmeden** onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="d94e4-133">Click **Yes, delete it** to confirm.</span></span>

![Silmeyi onayla][api-management-confirm-delete]

<span data-ttu-id="d94e4-135">Sertifika bir API tarafından kullanılıyorsa, bir uyarı ekranı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d94e4-135">If the certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="d94e4-136">Sertifikayı silmek için sertifika kullanmak üzere yapılandırılmış tüm API'lerinin kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d94e4-136">To delete the certificate you must first remove the certificate from any APIs that are configured to use it.</span></span>

![Silmeyi onayla][api-management-confirm-delete-policy]

## <span data-ttu-id="d94e4-138"><a name="step2"></a>Bir API Ağ Geçidi kimlik doğrulaması için bir istemci sertifikası kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d94e4-138"><a name="step2"> </a>Configure an API to use a client certificate for gateway authentication</span></span>
<span data-ttu-id="d94e4-139">Tıklatın **API'leri** gelen **API Management** , soldaki menüde istenen API adına tıklayın ve'ı tıklatın **güvenlik** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d94e4-139">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, and click the **Security** tab.</span></span>

![API Güvenlik][api-management-api-security]

<span data-ttu-id="d94e4-141">Seçin **istemci sertifikalarını** gelen **kimlik bilgileriyle** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="d94e4-141">Select **Client certificates** from the **With credentials** drop-down list.</span></span>

![İstemci sertifikaları][api-management-mutual-certificates]

<span data-ttu-id="d94e4-143">İstediğiniz sertifikayı seçin **istemci sertifikası** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="d94e4-143">Select the desired certificate from the **Client certificate** drop-down list.</span></span> <span data-ttu-id="d94e4-144">Birden fazla sertifika varsa doğru sertifikayı belirlemek için konu veya önceki bölümünde belirtildiği gibi parmak izi son dört karakterini bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d94e4-144">If there are multiple certificates you can look at the subject or the last four characters of the thumbprint as noted in the previous section to determine the correct certificate.</span></span>

![Sertifika Seç][api-management-select-certificate]

<span data-ttu-id="d94e4-146">Tıklatın **kaydetmek** API için yapılandırma değişikliği kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="d94e4-146">Click **Save** to save the configuration change to the API.</span></span>

> <span data-ttu-id="d94e4-147">Bu değişikliği hemen etkili olur ve bu API'nin işlemlerini çağrıları arka uç sunucusunda kimlik doğrulaması için sertifika kullanır.</span><span class="sxs-lookup"><span data-stu-id="d94e4-147">This change is effective immediately, and calls to operations of that API will use the certificate to authenticate on the back-end server.</span></span>
> 
> 

![API Değişiklikleri Kaydet][api-management-save-api]

> <span data-ttu-id="d94e4-149">Ağ Geçidi kimlik doğrulaması bir API için arka uç hizmeti için bir sertifika belirtildiğinde, bu API için ilkesinin bir parçası olur ve İlke Düzenleyicisi'nde görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="d94e4-149">When a certificate is specified for gateway authentication for the back-end service of an API, it becomes part of the policy for that API, and can be viewed in the policy editor.</span></span>
> 
> 

![Sertifika İlkesi][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="d94e4-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d94e4-151">Next steps</span></span>
<span data-ttu-id="d94e4-152">HTTP temel veya paylaşılan gizli kimlik doğrulaması gibi arka uç hizmetinizin güvenliğini sağlamak için diğer yöntemler hakkında daha fazla bilgi için aşağıdaki videoya bakın.</span><span class="sxs-lookup"><span data-stu-id="d94e4-152">For more information on other ways to secure your backend service, such as HTTP basic or shared secret authentication, see the following video.</span></span>

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



[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[to configure certificate authentication in Azure WebSites refer to this article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API to use a client certificate for gateway authentication]: #step2
[Test the configuration by calling an operation in the Developer Portal]: #step3
[Next steps]: #next-steps



