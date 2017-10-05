---
title: Azure API Management ilkeleri | Microsoft Docs
description: "Oluşturma, düzenleme ve API yönetimi ilkelerini yapılandırma öğrenin."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7c1f235343074ec11c635097f2b094a10f3fe781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="20769-103">Azure API Management ilkeleri</span><span class="sxs-lookup"><span data-stu-id="20769-103">Policies in Azure API Management</span></span>
<span data-ttu-id="20769-104">Azure API Management'te yapılandırma yoluyla API'nin davranışını değiştirmek yayımcının sisteminin güçlü bir özellik ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="20769-104">In Azure API Management, policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="20769-105">İstek üzerinde sırayla yürütülen deyimlerin bir koleksiyon veya bir API yanıtını ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="20769-105">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="20769-106">Sık kullanılan deyimler, XML'den JSON biçimi dönüştürme içerir ve bir geliştiriciden gelen çağrıların miktarını sınırlamak için hız sınırı çağırın.</span><span class="sxs-lookup"><span data-stu-id="20769-106">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="20769-107">Kutudan çıktığında çok daha fazla ilke kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="20769-107">Many more policies are available out of the box.</span></span>

<span data-ttu-id="20769-108">Bkz: [İlkesi başvurusu] [ Policy Reference] ilke deyimleri ve ayarlarının tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="20769-108">See the [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="20769-109">İlkeler, yönetilen API API tüketici arasında bulunur geçidi içinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="20769-109">Policies are applied inside the gateway which sits between the API consumer and the managed API.</span></span> <span data-ttu-id="20769-110">Ağ geçidi, tüm istekleri alır ve bunları temel API değiştirilmemiş genellikle iletir.</span><span class="sxs-lookup"><span data-stu-id="20769-110">The gateway receives all requests and usually forwards them unaltered to the underlying API.</span></span> <span data-ttu-id="20769-111">Ancak bir ilke gelen talep ve giden yanıt için değişiklikleri uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20769-111">However a policy can apply changes to both the inbound request and outbound response.</span></span>

<span data-ttu-id="20769-112">İlke ifadeleri herhangi bir API Management ilkesinde, ilke aksini belirtmedikçe, öznitelik değerleri ya da metin değerleri olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="20769-112">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="20769-113">Gibi bazı ilkeler [kontrol akışı] [ Control flow] ve [değişken Ayarla] [ Set variable] ilkeler ilke ifadelerini temel alarak.</span><span class="sxs-lookup"><span data-stu-id="20769-113">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="20769-114">Daha fazla bilgi için bkz: [ilkeleri Gelişmiş] [ Advanced policies] ve [ilke ifadelerini][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="20769-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="20769-115"><a name="scopes"></a>İlkelerinin nasıl yapılandırılacağını</span><span class="sxs-lookup"><span data-stu-id="20769-115"><a name="scopes"> </a>How to configure policies</span></span>
<span data-ttu-id="20769-116">Genel veya kapsamını ilkeleri yapılandırılabilir bir [ürün][Product], [API] [ API] veya [işlemi] [Operation].</span><span class="sxs-lookup"><span data-stu-id="20769-116">Policies can be configured globally or at the scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="20769-117">Bir ilke yapılandırmak için İlke Düzenleyicisi'nde yayımcı portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="20769-117">To configure a policy, navigate to the Policies editor in the publisher portal.</span></span>

![İlkeleri menüsü][policies-menu]

<span data-ttu-id="20769-119">İlke Düzenleyicisi'ni üç ana bölümden oluşur: ilke kapsamı (üst), burada ilkeleri düzenlenmesi (soldaki) ve deyimleri (sağdaki) listesinde ilke tanımı:</span><span class="sxs-lookup"><span data-stu-id="20769-119">The policies editor consists of three main sections: the policy scope (top), the policy definition where policies are edited (left) and the statements list (right):</span></span>

![İlke Düzenleyicisi][policies-editor]

<span data-ttu-id="20769-121">Bir ilke yapılandırmaya başlamak için ilkenin uygulanacağı kapsamı seçin.</span><span class="sxs-lookup"><span data-stu-id="20769-121">To begin configuring a policy you must first select the scope at which the policy should apply.</span></span> <span data-ttu-id="20769-122">Aşağıdaki ekran görüntüsünde **Starter** ürün seçilidir.</span><span class="sxs-lookup"><span data-stu-id="20769-122">In the screenshot below the **Starter** product is selected.</span></span> <span data-ttu-id="20769-123">İlke adı yanındaki kare simgesini bir ilke zaten bu düzeyde uygulanan olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="20769-123">Note that the square symbol next to the policy name indicates that a policy is already applied at this level.</span></span>

![Kapsam][policies-scope]

<span data-ttu-id="20769-125">Bir ilke uygulanmış olduğundan, yapılandırma tanımı görünümünde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="20769-125">Since a policy has already been applied, the configuration is shown in the definition view.</span></span>

![Yapılandırma][policies-configure]

<span data-ttu-id="20769-127">İlke salt okunur görüntülenen ilk.</span><span class="sxs-lookup"><span data-stu-id="20769-127">The policy is displayed read-only at first.</span></span> <span data-ttu-id="20769-128">Tanımı öğesini düzenlemek için **ilkesini yapılandırma** eylem.</span><span class="sxs-lookup"><span data-stu-id="20769-128">In order to edit the definition click the **Configure Policy** action.</span></span>

![Düzenle][policies-edit]

<span data-ttu-id="20769-130">İlke tanımı gelen ve giden ifadeler tanımlayan basit bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="20769-130">The policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="20769-131">XML tanımı penceresinden doğrudan düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="20769-131">The XML can be edited directly in the definition window.</span></span> <span data-ttu-id="20769-132">Deyimleri listesini sağa sağlanır ve deyimleri geçerli kapsam için geçerli etkin ve vurgulanmış; tarafından gösterildiği gibi **çağrı hızını sınırla** deyimi yukarıdaki ekran görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="20769-132">A list of statements is provided to the right and statements applicable to the current scope are enabled and highlighted; as demonstrated by the **Limit Call Rate** statement in the screenshot above.</span></span>

<span data-ttu-id="20769-133">Etkin bir deyimi tıklatarak uygun XML tanım görünümü imlecin konumda ekler.</span><span class="sxs-lookup"><span data-stu-id="20769-133">Clicking an enabled statement will add the appropriate XML at the location of the cursor in the definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="20769-134">Eklemek istediğiniz ilke etkin değilse, bu ilkeye doğru kapsamında olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="20769-134">If the policy that you want to add is not enabled, ensure that you are in the correct scope for that policy.</span></span> <span data-ttu-id="20769-135">Her ilke bildirimi, bazı kapsamlar ve ilke bölümler kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="20769-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="20769-136">İlke bölüm ve bir ilke kapsamları gözden geçirmek için kontrol **kullanım** bölüm söz konusu ilkenin [İlkesi başvurusu][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="20769-136">To review the policy sections and scopes for a policy, check the **Usage** section for that policy in the [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="20769-137">İlke deyimleri tam listesi ve bunların ayarları kullanılabilir olan [İlkesi başvurusu][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="20769-137">A full list of policy statements and their settings are available in the [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="20769-138">Örneğin, gelen istekleri belirtilen IP adreslerini kısıtlamak için yeni bir sistem eklemek için imleci hemen içeriğini iç koyun `inbound` XML öğesi tıklatıp **sınırla çağıran IP'leri** deyimi.</span><span class="sxs-lookup"><span data-stu-id="20769-138">For example, to add a new statement to restrict incoming requests to specified IP addresses, place the cursor just inside the content of the `inbound` XML element and click the **Restrict caller IPs** statement.</span></span>

![Kısıtlama ilkeleri][policies-restrict]

<span data-ttu-id="20769-140">Bu bir XML parçacığını ekler `inbound` öğesi deyim yapılandırma hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="20769-140">This will add an XML snippet to the `inbound` element that provides guidance on how to configure the statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="20769-141">Gelen istekleri sınırlamak ve kabul etmek için yalnızca bir IP adresinden, 1.2.3.4 XML aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="20769-141">To limit inbound requests and accept only those from an IP address of 1.2.3.4 modify the XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Kaydet][policies-save]

<span data-ttu-id="20769-143">Tamamlandığında deyimleri ilke için yapılandırma, tıklayın **kaydetmek** ve değişiklikleri API Yönetimi ağ geçidi hemen yayılır.</span><span class="sxs-lookup"><span data-stu-id="20769-143">When complete configuring the statements for the policy, click **Save** and the changes will be propagated to the API Management gateway immediately.</span></span>

## <span data-ttu-id="20769-144"><a name="sections"></a>Anlama ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="20769-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="20769-145">Bir ilke için bir istek ve yanıt sırayla yürütmek deyimleri dizisidir.</span><span class="sxs-lookup"><span data-stu-id="20769-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="20769-146">Yapılandırma uygun şekilde bölünür `inbound`, `backend`, `outbound`, ve `on-error` bölümler aşağıdaki yapılandırmada gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="20769-146">The configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements to be applied to the request go here -->
  </inbound>
  <backend>
    <!-- statements to be applied before the request is forwarded to 
         the backend service go here -->
  </backend>
  <outbound>
    <!-- statements to be applied to the response go here -->
  </outbound>
  <on-error>
    <!-- statements to be applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="20769-147">Bir isteğin işlenmesi sırasında bir hata varsa, tüm kalan adımları `inbound`, `backend`, veya `outbound` bölümleri atlanır ve yürütme atlar ifadeler için `on-error` bölümü.</span><span class="sxs-lookup"><span data-stu-id="20769-147">If there is an error during the processing of a request, any remaining steps in the `inbound`, `backend`, or `outbound` sections are skipped and execution jumps to the statements in the `on-error` section.</span></span> <span data-ttu-id="20769-148">İlke deyimlerinde yerleştirerek `on-error` gözden geçirebileceğiniz hata kullanarak bölüm `context.LastError` özelliği inceleyebilir ve hata yanıtı kullanarak özelleştirin `set-body` İlkesi ve bir hata oluşursa ne olacağını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="20769-148">By placing policy statements in the `on-error` section you can review the error by using the `context.LastError` property, inspect and customize the error response using the `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="20769-149">Hata kodları ve ilke deyimleri işleme sırasında oluşabilecek hatalar için yerleşik adımları vardır.</span><span class="sxs-lookup"><span data-stu-id="20769-149">There are error codes for built-in steps and for errors that may occur during the processing of policy statements.</span></span> <span data-ttu-id="20769-150">Daha fazla bilgi için bkz: [hata API Management ilkeleri işleme](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="20769-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="20769-151">Yapılandırma ilkeleri farklı düzeylerde (Genel, ürün, API ve işlem) belirtilebilir bu yana ilke tanımının deyimleri göre üst ilkesi yürütme sırasını belirlemek bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="20769-151">Since policies can be specified at different levels (global, product, api and operation) the configuration provides a way for you to specify the order in which the policy definition's statements execute with respect to the parent policy.</span></span> 

<span data-ttu-id="20769-152">İlke kapsamları aşağıdaki sırayla değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="20769-152">Policy scopes are evaluated in the following order.</span></span>

1. <span data-ttu-id="20769-153">Genel kapsamlı</span><span class="sxs-lookup"><span data-stu-id="20769-153">Global scope</span></span>
2. <span data-ttu-id="20769-154">Ürün kapsamı</span><span class="sxs-lookup"><span data-stu-id="20769-154">Product scope</span></span>
3. <span data-ttu-id="20769-155">API kapsamı</span><span class="sxs-lookup"><span data-stu-id="20769-155">API scope</span></span>
4. <span data-ttu-id="20769-156">İşlem kapsamı</span><span class="sxs-lookup"><span data-stu-id="20769-156">Operation scope</span></span>

<span data-ttu-id="20769-157">Bunların içindeki deyimleri yerleşimini göre değerlendirilir `base` varsa, öğesi.</span><span class="sxs-lookup"><span data-stu-id="20769-157">The statements within them are evaluated according to the placement of the `base` element, if it is present.</span></span> <span data-ttu-id="20769-158">Genel ilke üst öğeye sahip İlkesi ve kullanarak `<base>` öğesi içindeki etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="20769-158">Global policy has no parent policy and using the `<base>` element in it has no effect.</span></span>

<span data-ttu-id="20769-159">Genel düzeyinde ve bir API için yapılandırılmış bir ilke bir ilke varsa, API'nin kullanıldığı her Örneğin, ardından her iki ilke uygulanır.</span><span class="sxs-lookup"><span data-stu-id="20769-159">For example, if you have a policy at the global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="20769-160">API Management belirleyici temel öğe aracılığıyla birleşik İlkesi deyimlerinin sıralama için sağlar.</span><span class="sxs-lookup"><span data-stu-id="20769-160">API Management allows for deterministic ordering of combined policy statements via the base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="20769-161">Yukarıdaki örnek ilke tanımı'ndaki `cross-domain` hangi sırayla, misiniz yüksek ilkeleri tarafından uyulması önce deyimi yürütün `find-and-replace` ilkesi.</span><span class="sxs-lookup"><span data-stu-id="20769-161">In the example policy definition above, the `cross-domain` statement would execute before any higher policies which would in turn, be followed by the `find-and-replace` policy.</span></span> 

<span data-ttu-id="20769-162">İlkeler ilke düzenleyicisinde geçerli kapsamdaki görmek için tıklatın **yeniden hesapla seçili kapsam için etkin ilke**.</span><span class="sxs-lookup"><span data-stu-id="20769-162">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20769-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20769-163">Next steps</span></span>
<span data-ttu-id="20769-164">İlke ifadelerini temel video aşağıdaki çıkışı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="20769-164">Check out following video on policy expressions.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
