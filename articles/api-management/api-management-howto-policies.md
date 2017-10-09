---
title: Azure API Management'te aaaPolicies | Microsoft Docs
description: "Nasıl toocreate, düzenlemek ve API yönetimi ilkelerini yapılandırma öğrenin."
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
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="a7b60-103">Azure API Management ilkeleri</span><span class="sxs-lookup"><span data-stu-id="a7b60-103">Policies in Azure API Management</span></span>
<span data-ttu-id="a7b60-104">Azure API Management'te hello publisher toochange hello davranışını yapılandırma yoluyla hello API izin hello sisteminin güçlü bir özellik ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="a7b60-104">In Azure API Management, policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="a7b60-105">Merhaba istek üzerinde sırayla yürütülen deyimlerin bir koleksiyon veya bir API yanıtını ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="a7b60-105">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="a7b60-106">Sık kullanılan deyimler XML tooJSON biçimi dönüştürme içerir ve bir geliştiriciden gelen çağrıların toorestrict hello miktarını sınırlamak oranı çağırın.</span><span class="sxs-lookup"><span data-stu-id="a7b60-106">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="a7b60-107">Çok daha fazla ilke hello kutu dışı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a7b60-107">Many more policies are available out of hello box.</span></span>

<span data-ttu-id="a7b60-108">Merhaba bkz [İlkesi başvurusu] [ Policy Reference] ilke deyimleri ve ayarlarının tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="a7b60-108">See hello [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="a7b60-109">İlkeler, yönetilen hello API hello API tüketici arasında bulunur hello ağ geçidi içinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="a7b60-109">Policies are applied inside hello gateway which sits between hello API consumer and hello managed API.</span></span> <span data-ttu-id="a7b60-110">Merhaba ağ geçidi tüm istekleri alır ve bunları değiştirilmemiş genellikle iletir API temel toohello.</span><span class="sxs-lookup"><span data-stu-id="a7b60-110">hello gateway receives all requests and usually forwards them unaltered toohello underlying API.</span></span> <span data-ttu-id="a7b60-111">Ancak bir ilke değişiklikleri tooboth hello gelen istek ve giden yanıt uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7b60-111">However a policy can apply changes tooboth hello inbound request and outbound response.</span></span>

<span data-ttu-id="a7b60-112">Merhaba ilke aksini belirtmedikçe ilke ifadelerini öznitelik değerleri ya da metin değerleri hello API Management ilkeleri olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a7b60-112">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="a7b60-113">Hello gibi bazı ilkeler [kontrol akışı] [ Control flow] ve [değişken Ayarla] [ Set variable] ilkeler ilke ifadelerini temel alarak.</span><span class="sxs-lookup"><span data-stu-id="a7b60-113">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="a7b60-114">Daha fazla bilgi için bkz: [ilkeleri Gelişmiş] [ Advanced policies] ve [ilke ifadelerini][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="a7b60-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="a7b60-115"><a name="scopes"></a>Nasıl tooconfigure ilkeleri</span><span class="sxs-lookup"><span data-stu-id="a7b60-115"><a name="scopes"> </a>How tooconfigure policies</span></span>
<span data-ttu-id="a7b60-116">Genel veya hello kapsamını ilkeleri yapılandırılabilir bir [ürün][Product], [API] [ API] veya [işlemi] [Operation].</span><span class="sxs-lookup"><span data-stu-id="a7b60-116">Policies can be configured globally or at hello scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="a7b60-117">bir ilke tooconfigure toohello ilkeleri Düzenleyicisi'nde hello yayımcı portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="a7b60-117">tooconfigure a policy, navigate toohello Policies editor in hello publisher portal.</span></span>

![İlkeleri menüsü][policies-menu]

<span data-ttu-id="a7b60-119">Merhaba ilkeleri Düzenleyicisi üç ana bölümden oluşur: Merhaba burada ilkeleri düzenlenmesi (soldaki) ve hello deyimleri listesinde (sağdaki) ilke kapsamı (üst) hello İlkesi tanımı:</span><span class="sxs-lookup"><span data-stu-id="a7b60-119">hello policies editor consists of three main sections: hello policy scope (top), hello policy definition where policies are edited (left) and hello statements list (right):</span></span>

![İlke Düzenleyicisi][policies-editor]

<span data-ttu-id="a7b60-121">önce hangi hello İlkesi uygulamalıdır hello kapsam seçmeniz gerekir. bir ilke yapılandırma toobegin.</span><span class="sxs-lookup"><span data-stu-id="a7b60-121">toobegin configuring a policy you must first select hello scope at which hello policy should apply.</span></span> <span data-ttu-id="a7b60-122">Merhaba ekran görüntüsü aşağıda hello **Starter** ürün seçilidir.</span><span class="sxs-lookup"><span data-stu-id="a7b60-122">In hello screenshot below hello **Starter** product is selected.</span></span> <span data-ttu-id="a7b60-123">Bu hello kare simgesi sonraki toohello ilkesi adı bir ilke zaten bu düzeyde uygulandığını gösterir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a7b60-123">Note that hello square symbol next toohello policy name indicates that a policy is already applied at this level.</span></span>

![Kapsam][policies-scope]

<span data-ttu-id="a7b60-125">Bir ilke uygulanmış olduğundan, hello yapılandırma hello tanımı görünümünde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a7b60-125">Since a policy has already been applied, hello configuration is shown in hello definition view.</span></span>

![Yapılandırma][policies-configure]

<span data-ttu-id="a7b60-127">salt okunur Hello İlkesi görüntülenen ilk.</span><span class="sxs-lookup"><span data-stu-id="a7b60-127">hello policy is displayed read-only at first.</span></span> <span data-ttu-id="a7b60-128">Sipariş tooedit hello tanımı tıklatın hello **ilkesini yapılandırma** eylem.</span><span class="sxs-lookup"><span data-stu-id="a7b60-128">In order tooedit hello definition click hello **Configure Policy** action.</span></span>

![Düzenle][policies-edit]

<span data-ttu-id="a7b60-130">Merhaba ilke tanımı gelen ve giden ifadeler tanımlayan basit bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="a7b60-130">hello policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="a7b60-131">doğrudan hello tanımı penceresinde Hello XML düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="a7b60-131">hello XML can be edited directly in hello definition window.</span></span> <span data-ttu-id="a7b60-132">Deyimleri listesini sağ toohello ve deyimleri geçerli toohello geçerli kapsam etkin ve vurgulanmış sağlanır; Merhaba tarafından gösterildiği gibi **çağrı hızını sınırla** hello ekran yukarıdaki deyiminde.</span><span class="sxs-lookup"><span data-stu-id="a7b60-132">A list of statements is provided toohello right and statements applicable toohello current scope are enabled and highlighted; as demonstrated by hello **Limit Call Rate** statement in hello screenshot above.</span></span>

<span data-ttu-id="a7b60-133">Etkin bir deyimi tıklatarak ekleyecek hello imlecin hello tanımı görünümünde hello konumda uygun XML hello.</span><span class="sxs-lookup"><span data-stu-id="a7b60-133">Clicking an enabled statement will add hello appropriate XML at hello location of hello cursor in hello definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="a7b60-134">Tooadd istediğiniz hello ilkesi etkin değilse, bu ilkeye hello doğru kapsamında olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a7b60-134">If hello policy that you want tooadd is not enabled, ensure that you are in hello correct scope for that policy.</span></span> <span data-ttu-id="a7b60-135">Her ilke bildirimi, bazı kapsamlar ve ilke bölümler kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a7b60-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="a7b60-136">tooreview hello İlkesi bölümler için bir ilke kapsamı denetleyip hello **kullanım** bölüm hello söz konusu ilkenin [İlkesi başvurusu][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="a7b60-136">tooreview hello policy sections and scopes for a policy, check hello **Usage** section for that policy in hello [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="a7b60-137">İlke deyimleri tam listesi ve ayarlarına hello kullanılabilir [İlkesi başvurusu][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="a7b60-137">A full list of policy statements and their settings are available in hello [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="a7b60-138">Örneğin, toospecified IP adreslerini tooadd yeni bir deyim toorestrict gelen istekleri, yalnızca hello Merhaba içeriğine içinde hello imleci `inbound` XML öğesi ve tıklatın hello **sınırla çağıran IP'leri** deyimi.</span><span class="sxs-lookup"><span data-stu-id="a7b60-138">For example, tooadd a new statement toorestrict incoming requests toospecified IP addresses, place hello cursor just inside hello content of hello `inbound` XML element and click hello **Restrict caller IPs** statement.</span></span>

![Kısıtlama ilkeleri][policies-restrict]

<span data-ttu-id="a7b60-140">Bu bir XML parçacığını toohello ekler `inbound` öğesi nasıl tooconfigure hello üzerinde deyimi rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7b60-140">This will add an XML snippet toohello `inbound` element that provides guidance on how tooconfigure hello statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="a7b60-141">toolimit istekleri Gelen ve kabul yalnızca bir IP adresinden, 1.2.3.4 hello XML aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="a7b60-141">toolimit inbound requests and accept only those from an IP address of 1.2.3.4 modify hello XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Kaydet][policies-save]

<span data-ttu-id="a7b60-143">Tamamlandığında hello deyimleri hello ilkesi için yapılandırma, tıklayın **kaydetmek** ve hello değişiklikleri yayılan toohello API Yönetimi ağ geçidi hemen.</span><span class="sxs-lookup"><span data-stu-id="a7b60-143">When complete configuring hello statements for hello policy, click **Save** and hello changes will be propagated toohello API Management gateway immediately.</span></span>

## <span data-ttu-id="a7b60-144"><a name="sections"></a>Anlama ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a7b60-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="a7b60-145">Bir ilke için bir istek ve yanıt sırayla yürütmek deyimleri dizisidir.</span><span class="sxs-lookup"><span data-stu-id="a7b60-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="a7b60-146">Merhaba yapılandırma bölündüğü uygun şekilde `inbound`, `backend`, `outbound`, ve `on-error` bölümler hello yapılandırma aşağıdaki gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="a7b60-146">hello configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in hello following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="a7b60-147">Merhaba bir isteğin işlenmesi sırasında bir hata varsa, tüm kalan hello adımları `inbound`, `backend`, veya `outbound` bölümleri atlanır ve yürütme atlar hello toohello deyimlerinde `on-error` bölümü.</span><span class="sxs-lookup"><span data-stu-id="a7b60-147">If there is an error during hello processing of a request, any remaining steps in hello `inbound`, `backend`, or `outbound` sections are skipped and execution jumps toohello statements in hello `on-error` section.</span></span> <span data-ttu-id="a7b60-148">Hello İlkesi deyimleri yerleştirerek `on-error` gözden geçirebileceğiniz hello hata hello kullanarak bölüm `context.LastError` özelliği, inceleyin ve hello kullanarak hello hata yanıtı özelleştirme `set-body` İlkesi ve bir hata oluşursa ne olacağını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a7b60-148">By placing policy statements in hello `on-error` section you can review hello error by using hello `context.LastError` property, inspect and customize hello error response using hello `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="a7b60-149">Hata kodları yerleşik adımları ve ilke deyimleri hello işlenmesi sırasında oluşabilecek hatalar için vardır.</span><span class="sxs-lookup"><span data-stu-id="a7b60-149">There are error codes for built-in steps and for errors that may occur during hello processing of policy statements.</span></span> <span data-ttu-id="a7b60-150">Daha fazla bilgi için bkz: [hata API Management ilkeleri işleme](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="a7b60-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="a7b60-151">İlkeleri farklı düzeylerde (Genel, ürün, API ve işlem) belirtilebilir beri hello yapılandırma yolu sizin için toospecify hello sipariş hello ilke tanımının deyimlerini saygı toohello üst ilkesiyle yürütmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7b60-151">Since policies can be specified at different levels (global, product, api and operation) hello configuration provides a way for you toospecify hello order in which hello policy definition's statements execute with respect toohello parent policy.</span></span> 

<span data-ttu-id="a7b60-152">İlke kapsamları sırasının hello değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="a7b60-152">Policy scopes are evaluated in hello following order.</span></span>

1. <span data-ttu-id="a7b60-153">Genel kapsamlı</span><span class="sxs-lookup"><span data-stu-id="a7b60-153">Global scope</span></span>
2. <span data-ttu-id="a7b60-154">Ürün kapsamı</span><span class="sxs-lookup"><span data-stu-id="a7b60-154">Product scope</span></span>
3. <span data-ttu-id="a7b60-155">API kapsamı</span><span class="sxs-lookup"><span data-stu-id="a7b60-155">API scope</span></span>
4. <span data-ttu-id="a7b60-156">İşlem kapsamı</span><span class="sxs-lookup"><span data-stu-id="a7b60-156">Operation scope</span></span>

<span data-ttu-id="a7b60-157">Merhaba deyimleri bunları içinde hello toohello yerleşimini göre değerlendirilir `base` varsa, öğesi.</span><span class="sxs-lookup"><span data-stu-id="a7b60-157">hello statements within them are evaluated according toohello placement of hello `base` element, if it is present.</span></span> <span data-ttu-id="a7b60-158">Genel ilke sahip hiç üst İlkesi ve hello kullanarak `<base>` öğesi içindeki etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="a7b60-158">Global policy has no parent policy and using hello `<base>` element in it has no effect.</span></span>

<span data-ttu-id="a7b60-159">Merhaba genel düzeyinde ve bir API için yapılandırılmış bir ilke bir ilke varsa, API'nin kullanıldığı her Örneğin, ardından her iki ilke uygulanır.</span><span class="sxs-lookup"><span data-stu-id="a7b60-159">For example, if you have a policy at hello global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="a7b60-160">API Management belirleyici hello temel öğe aracılığıyla birleşik İlkesi deyimlerinin sıralama için sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7b60-160">API Management allows for deterministic ordering of combined policy statements via hello base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="a7b60-161">Merhaba örnek ilke tanımı'nda yukarıdaki, hello `cross-domain` deyimini yürütün, sırayla misiniz tüm yüksek ilkeleri uyulması önce hello tarafından `find-and-replace` ilkesi.</span><span class="sxs-lookup"><span data-stu-id="a7b60-161">In hello example policy definition above, hello `cross-domain` statement would execute before any higher policies which would in turn, be followed by hello `find-and-replace` policy.</span></span> 

<span data-ttu-id="a7b60-162">hello İlkesi Düzenleyicisi'nde hello geçerli kapsamdaki toosee hello ilkeleri **yeniden hesapla seçili kapsam için etkin ilke**.</span><span class="sxs-lookup"><span data-stu-id="a7b60-162">toosee hello policies in hello current scope in hello policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7b60-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7b60-163">Next steps</span></span>
<span data-ttu-id="a7b60-164">İlke ifadelerini temel video aşağıdaki çıkışı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a7b60-164">Check out following video on policy expressions.</span></span>

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
