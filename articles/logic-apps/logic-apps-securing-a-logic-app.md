---
title: "Güvenli erişim Azure Logic Apps | Microsoft Docs"
description: "Tetikleyiciler, girişleri ve çıkışları, eylem parametrelerini ve Azure mantıksal uygulamaları'nda iş akışları ile kullanılan hizmetler erişimi korumaya yönelik güvenlik ekleyin."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 0528d660f590e106f61729f10f8f68da3fe58cb7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-access-to-your-logic-apps"></a><span data-ttu-id="bb64e-103">Mantıksal uygulamalarınızı güvenli erişim</span><span class="sxs-lookup"><span data-stu-id="bb64e-103">Secure access to your logic apps</span></span>

<span data-ttu-id="bb64e-104">Mantıksal uygulamanızı güvenliğini sağlamanıza yardımcı olabilecek birçok araç vardır.</span><span class="sxs-lookup"><span data-stu-id="bb64e-104">There are many tools available to help you secure your logic app.</span></span>

* <span data-ttu-id="bb64e-105">Bir mantıksal uygulama (HTTP isteği tetikleyici) tetiklemek için erişim güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="bb64e-105">Securing access to trigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="bb64e-106">Yönetme, düzenleme veya bir mantıksal uygulama okuma erişimi güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="bb64e-106">Securing access to manage, edit, or read a logic app</span></span>
* <span data-ttu-id="bb64e-107">Bir çalıştırma için girişleri ve çıkışları içeriğini erişimi güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="bb64e-107">Securing access to contents of inputs and outputs for a run</span></span>
* <span data-ttu-id="bb64e-108">Parametreleri ya da bir iş akışında Eylemler içinde girişleri güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="bb64e-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="bb64e-109">Bir iş akışından isteklerini alacak hizmetlerine erişim güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="bb64e-109">Securing access to services that receive requests from a workflow</span></span>

## <a name="secure-access-to-trigger"></a><span data-ttu-id="bb64e-110">Tetiklemek için güvenli erişim</span><span class="sxs-lookup"><span data-stu-id="bb64e-110">Secure access to trigger</span></span>

<span data-ttu-id="bb64e-111">Bir HTTP isteğiyle tetiklenen bir mantıksal uygulama ile çalışırken ([isteği](../connectors/connectors-native-reqres.md) veya [Web kancası](../connectors/connectors-native-webhook.md)), böylece yalnızca yetkili istemcilerin mantıksal uygulama tetikleyebilir erişimi kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire the logic app.</span></span> <span data-ttu-id="bb64e-112">Bir mantıksal uygulama içinde tüm istekleri şifrelenir ve SSL güvenli.</span><span class="sxs-lookup"><span data-stu-id="bb64e-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="bb64e-113">Paylaşılan erişim imzası</span><span class="sxs-lookup"><span data-stu-id="bb64e-113">Shared Access Signature</span></span>

<span data-ttu-id="bb64e-114">Her istek uç noktası için bir mantıksal uygulama içeren bir [paylaşılan erişim imzası (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) URL'SİNİN bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="bb64e-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of the URL.</span></span> <span data-ttu-id="bb64e-115">Her URL içeren bir `sp`, `sv`, ve `sig` sorgu parametresi.</span><span class="sxs-lookup"><span data-stu-id="bb64e-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="bb64e-116">İzinleri tarafından belirtilen `sp`ve izin verilen, HTTP yöntemleri karşılık `sv` oluşturmak için kullanılan sürümü ve `sig` tetiklemek için erişimde kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bb64e-116">Permissions are specified by `sp`, and correspond to HTTP methods allowed, `sv` is the version used to generate, and `sig` is used to authenticate access to trigger.</span></span> <span data-ttu-id="bb64e-117">İmza, tüm özellikler ve URL yollarını gizli bir anahtar ile SHA256 algoritmasını kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bb64e-117">The signature is generated using the SHA256 algorithm with a secret key on all the URL paths and properties.</span></span> <span data-ttu-id="bb64e-118">Gizli anahtar hiçbir zaman kullanıma sunulan ve yayımlanan ve şifrelenmiş ve mantığı uygulamanın parçası olarak depolanan tutulur.</span><span class="sxs-lookup"><span data-stu-id="bb64e-118">The secret key is never exposed and published, and is kept encrypted and stored as part of the logic app.</span></span> <span data-ttu-id="bb64e-119">Mantıksal uygulama gizli anahtarı ile oluşturulan geçerli bir imzası içeren Tetikleyicileri yalnızca yetkilendirir.</span><span class="sxs-lookup"><span data-stu-id="bb64e-119">Your logic app only authorizes triggers that contain a valid signature created with the secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="bb64e-120">Erişim anahtarlarını yeniden oluştur</span><span class="sxs-lookup"><span data-stu-id="bb64e-120">Regenerate access keys</span></span>

<span data-ttu-id="bb64e-121">Yeni güvenli bir anahtar, REST API veya Azure Portal'dan dilediğiniz zaman yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-121">You can regenerate a new secure key at anytime through the REST API or Azure portal.</span></span> <span data-ttu-id="bb64e-122">Eski anahtarı kullanarak önceden oluşturulan tüm geçerli URL'ler geçersiz ve artık mantıksal uygulama yangın yetkisine.</span><span class="sxs-lookup"><span data-stu-id="bb64e-122">All current URLs that were generated previously using the old key are invalidated and no longer authorized to fire the logic app.</span></span>

1. <span data-ttu-id="bb64e-123">Azure portalında bir anahtarı yeniden oluşturmak istediğiniz mantıksal uygulama açın</span><span class="sxs-lookup"><span data-stu-id="bb64e-123">In the Azure portal, open the logic app you want to regenerate a key</span></span>
1. <span data-ttu-id="bb64e-124">Tıklatın **erişim tuşları** menü öğesi altında **ayarları**</span><span class="sxs-lookup"><span data-stu-id="bb64e-124">Click the **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="bb64e-125">Yeniden oluşturun ve işlemi tamamlamak için anahtarı seçin</span><span class="sxs-lookup"><span data-stu-id="bb64e-125">Choose the key to regenerate and complete the process</span></span>

<span data-ttu-id="bb64e-126">Yeniden oluşturma tamamlandıktan sonra alma URL'leri yeni erişim anahtarı ile imzalanmış.</span><span class="sxs-lookup"><span data-stu-id="bb64e-126">URLs you retrieve after regeneration are signed with the new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="bb64e-127">Geri çağırma URL'leri bir sona erme tarihi ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb64e-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="bb64e-128">Diğer kuruluşlarla URL paylaşıyorsanız, özel anahtarları ve gerektiği gibi sona erme tarihleri ile URL'leri oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="bb64e-128">If you are sharing the URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="bb64e-129">Sonra sorunsuzca anahtarları alma, veya bir uygulama yangın erişimi belirli bir timespan sınırlı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bb64e-129">You can then seamlessly roll keys, or ensure access to fire an app is restricted to a certain timespan.</span></span> <span data-ttu-id="bb64e-130">Bir URL yolu için bir sona erme tarihi belirtebilirsiniz [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="bb64e-130">You can specify an expiration date for a URL through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="bb64e-131">Özellik gövdesinde dahil `NotAfter` bir JSON tarih dizesi döndüren yalnızca geçerliliğinin bir geri çağırma URL'si `NotAfter` tarih ve saat.</span><span class="sxs-lookup"><span data-stu-id="bb64e-131">In the body, include the property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until the `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="bb64e-132">Birincil veya ikincil gizli anahtarla URL'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb64e-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="bb64e-133">Oluşturmak ya da istek tabanlı tetikleyiciler için geri çağırma URL'leri listesinde URL imzalamak için kullanılan hangi anahtar da belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-133">When you generate or list callback URLs for request-based triggers, you can also specify which key to use to sign the URL.</span></span>  <span data-ttu-id="bb64e-134">Belirli bir anahtarı tarafından imzalanan bir URL oluşturabileceğiniz [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) gibi:</span><span class="sxs-lookup"><span data-stu-id="bb64e-134">You can generate a URL signed by a specific key through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="bb64e-135">Özellik gövdesinde dahil `KeyType` olarak `Primary` veya `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="bb64e-135">In the body, include the property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="bb64e-136">Bu, belirtilen güvenli anahtar tarafından imzalanmış bir URL döndürür.</span><span class="sxs-lookup"><span data-stu-id="bb64e-136">This returns a URL signed by the secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="bb64e-137">Gelen IP adreslerini kısıtlamak</span><span class="sxs-lookup"><span data-stu-id="bb64e-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="bb64e-138">Paylaşılan erişim imzası yanı sıra, yalnızca belirli istemcilerinden bir mantıksal uygulama çağırma sınırlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-138">In addition to the Shared Access Signature, you may wish to restrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="bb64e-139">Örneğin, uç noktanızı Azure API Management üzerinden yönetiyorsanız, yalnızca isteği API Management örneği IP adresinden geldiğinde isteğini kabul etmek için mantıksal uygulama kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-139">For example, if you manage your endpoint through Azure API Management, you can restrict the logic app to only accept the request when the request comes from the API Management instance IP address.</span></span>

<span data-ttu-id="bb64e-140">Bu ayar mantığını uygulaması ayarları içinde yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="bb64e-140">This setting can be configured within the logic app settings:</span></span>

1. <span data-ttu-id="bb64e-141">Azure Portal'da, IP adresi sınırlamaları eklemek istediğiniz mantıksal uygulama açın</span><span class="sxs-lookup"><span data-stu-id="bb64e-141">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="bb64e-142">Tıklatın **erişim denetimini yapılandırma** menü öğesi altında **ayarları**</span><span class="sxs-lookup"><span data-stu-id="bb64e-142">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="bb64e-143">Tetik tarafından kabul edilmesi için IP adres aralıklarına listesini belirtin</span><span class="sxs-lookup"><span data-stu-id="bb64e-143">Specify the list of IP address ranges to be accepted by the trigger</span></span>

<span data-ttu-id="bb64e-144">Geçerli bir IP aralığı biçimini alır `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="bb64e-144">A valid IP range takes the format `192.168.1.1/255`.</span></span> <span data-ttu-id="bb64e-145">Yalnızca bir iç içe geçmiş mantıksal uygulama tetiklenecek mantıksal uygulama istiyorsanız seçin **yalnızca diğer logic apps** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="bb64e-145">If you want the logic app to only fire as a nested logic app, select the **Only other logic apps** option.</span></span> <span data-ttu-id="bb64e-146">Bu seçenek, anlamı yalnızca çağırır hizmetin kendisini (üst mantıksal uygulamalar) kaynak için boş bir dizi Yazar başarıyla tetiklenecek.</span><span class="sxs-lookup"><span data-stu-id="bb64e-146">This option writes an empty array to the resource, meaning only calls from the service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="bb64e-147">Hala bir mantıksal uygulama isteği tetikleyici ile REST API aracılığıyla çalıştırabilirsiniz / Yönetim `/triggers/{triggerName}/run` IP ne olursa olsun.</span><span class="sxs-lookup"><span data-stu-id="bb64e-147">You can still run a logic app with a request trigger through the REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="bb64e-148">Bu senaryo Azure REST API'sine karşı kimlik doğrulaması gerektirir ve tüm olayları Azure denetim günlüğünde görünür.</span><span class="sxs-lookup"><span data-stu-id="bb64e-148">This scenario requires authentication against the Azure REST API, and all events would appear in the Azure Audit Log.</span></span> <span data-ttu-id="bb64e-149">Set erişim ilkelerini uygun şekilde denetler.</span><span class="sxs-lookup"><span data-stu-id="bb64e-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="bb64e-150">Kaynak tanımı'nda IP aralıklarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="bb64e-150">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="bb64e-151">Kullanıyorsanız bir [dağıtım şablonu](logic-apps-create-deploy-template.md) dağıtımlarınızı otomatikleştirmek için IP aralığı ayarlarını kaynak şablonu yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="bb64e-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="bb64e-152">Azure Active Directory, OAuth veya diğer güvenlik ekleme</span><span class="sxs-lookup"><span data-stu-id="bb64e-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="bb64e-153">Bir mantıksal uygulama üzerinde daha fazla yetkilendirme protokolleri eklemek için [Azure API Management](https://azure.microsoft.com/services/api-management/) zengin izleme, güvenlik, İlkesi ve bir mantıksal uygulama bir API olarak kullanıma sunmak için özelliğine sahip herhangi bir uç nokta için belgeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb64e-153">To add more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with the capability to expose a logic app as an API.</span></span> <span data-ttu-id="bb64e-154">Azure API Management genel veya özel uç noktası için Azure Active Directory, sertifika, OAuth veya diğer güvenlik standartları kullanabilirsiniz mantıksal uygulama getirebilir.</span><span class="sxs-lookup"><span data-stu-id="bb64e-154">Azure API Management can expose a public or private endpoint for the logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="bb64e-155">Bir istek alındığında, Azure API Management (herhangi bir gerekli dönüşümleri veya kısıtlamaları yürütülen gerçekleştirerek) mantıksal uygulama isteği iletir.</span><span class="sxs-lookup"><span data-stu-id="bb64e-155">When a request is received, Azure API Management forwards the request to the logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="bb64e-156">Mantıksal uygulama gelen IP aralığı ayarları yalnızca API Yönetimi'nden tetiklenmesi mantıksal uygulama izin vermek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-156">You can use the incoming IP range settings on the logic app to only allow the logic app to be triggered from API Management.</span></span>

## <a name="secure-access-to-manage-or-edit-logic-apps"></a><span data-ttu-id="bb64e-157">Güvenli erişim yönetmek veya logic apps düzenlemek için</span><span class="sxs-lookup"><span data-stu-id="bb64e-157">Secure access to manage or edit logic apps</span></span>

<span data-ttu-id="bb64e-158">Böylece yalnızca belirli kullanıcılara veya gruplara kaynak üzerinde işlem gerçekleştirmek için bir mantıksal uygulama yönetimi işlemleri için erişimi kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-158">You can restrict access to management operations on a logic app so that only specific users or groups are able to perform operations on the resource.</span></span> <span data-ttu-id="bb64e-159">Logic apps kullanan Azure [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md) özellik ve aynı araçları ile özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="bb64e-159">Logic apps use the Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with the same tools.</span></span>  <span data-ttu-id="bb64e-160">Aboneliğinize üyeleri de atayabilirsiniz birkaç yerleşik roller vardır:</span><span class="sxs-lookup"><span data-stu-id="bb64e-160">There are a few built-in roles you can assign members of your subscription to as well:</span></span>

* <span data-ttu-id="bb64e-161">**Mantığı uygulamasını katkıda bulunan** -görüntüleme, düzenleme ve bir mantıksal uygulama güncelleştirmek için erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb64e-161">**Logic App Contributor** - Provides access to view, edit, and update a logic app.</span></span>  <span data-ttu-id="bb64e-162">Kaynak kaldıramaz veya yönetim işlemleri.</span><span class="sxs-lookup"><span data-stu-id="bb64e-162">Cannot remove the resource or perform admin operations.</span></span>
* <span data-ttu-id="bb64e-163">**Mantıksal uygulama işleci** - mantıksal uygulama görüntüleyebilir ve çalıştırma geçmişi ve etkinleştir/devre dışı bırak.</span><span class="sxs-lookup"><span data-stu-id="bb64e-163">**Logic App Operator** - Can view the logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="bb64e-164">Düzenleyemez veya tanımını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bb64e-164">Cannot edit or update the definition.</span></span>

<span data-ttu-id="bb64e-165">Aynı zamanda [Azure kaynak kilidi](../azure-resource-manager/resource-group-lock-resources.md) değiştirme veya silme logic apps önlemek için.</span><span class="sxs-lookup"><span data-stu-id="bb64e-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) to prevent changing or deleting logic apps.</span></span> <span data-ttu-id="bb64e-166">Bu özellik, üretim kaynaklardan değişiklikleri ya da silme işlemleri engellemek için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="bb64e-166">This capability is valuable to prevent production resources from changes or deletions.</span></span>

## <a name="secure-access-to-contents-of-the-run-history"></a><span data-ttu-id="bb64e-167">Çalıştırma geçmişi içeriğini güvenli erişim</span><span class="sxs-lookup"><span data-stu-id="bb64e-167">Secure access to contents of the run history</span></span>

<span data-ttu-id="bb64e-168">Belirli IP adresi aralıkları önceki çalışır gelen girişleri veya çıkışları in içeriğine erişimi kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-168">You can restrict access to contents of inputs or outputs from previous runs to specific IP address ranges.</span></span>  

<span data-ttu-id="bb64e-169">Yoldaki ve bekleyen iş akışı çalışması içinde tüm veriler şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="bb64e-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="bb64e-170">Geçmiş çalıştırmak için bir çağrı yapıldığında, hizmet isteğin kimliğini doğrular ve isteği ve yanıt girişleri ve çıkışları bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb64e-170">When a call to run history is made, the service authenticates the request and provides links to the request and response inputs and outputs.</span></span> <span data-ttu-id="bb64e-171">Belirtilen IP adresi aralığından içeriği görüntülemek için yalnızca istekler içeriği döndürür şekilde bu bağlantıyı korunabilir.</span><span class="sxs-lookup"><span data-stu-id="bb64e-171">This link can be protected so only requests to view content from a designated IP address range return the contents.</span></span> <span data-ttu-id="bb64e-172">Ek erişim denetimi için bu özelliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="bb64e-173">Bir IP adresi gibi bile belirtebilirsiniz `0.0.0.0` hiç bir girdi/çıktı erişebilecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="bb64e-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="bb64e-174">İş akışı içeriği 'just-in-time' erişimi için olasılığını sağlayan yalnızca yönetici izinlerine sahip olan kişi bu kısıtlama kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-174">Only someone with admin permissions could remove this restriction, providing the possibility for 'just-in-time' access to workflow contents.</span></span>

<span data-ttu-id="bb64e-175">Bu ayar, Azure portalında kaynak ayarları içinde yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="bb64e-175">This setting can be configured within the resource settings of the Azure portal:</span></span>

1. <span data-ttu-id="bb64e-176">Azure Portal'da, IP adresi sınırlamaları eklemek istediğiniz mantıksal uygulama açın</span><span class="sxs-lookup"><span data-stu-id="bb64e-176">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="bb64e-177">Tıklatın **erişim denetimini yapılandırma** menü öğesi altında **ayarları**</span><span class="sxs-lookup"><span data-stu-id="bb64e-177">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="bb64e-178">IP adresi aralıkları için içeriğe erişimi için bir liste belirtin</span><span class="sxs-lookup"><span data-stu-id="bb64e-178">Specify the list of IP address ranges for access to content</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="bb64e-179">Kaynak tanımı'nda IP aralıklarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="bb64e-179">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="bb64e-180">Kullanıyorsanız bir [dağıtım şablonu](logic-apps-create-deploy-template.md) dağıtımlarınızı otomatikleştirmek için IP aralığı ayarlarını kaynak şablonu yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="bb64e-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="bb64e-181">Güvenli parametreleri ve iş akışı içinde girişleri</span><span class="sxs-lookup"><span data-stu-id="bb64e-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="bb64e-182">Dağıtım için bir iş akışı tanımı bazı yönlerini ortamlar genelinde Parametreleştirme isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-182">You might want to parameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="bb64e-183">Ayrıca, bazı parametreler gibi bir istemci kimliği ve istemci parolası için bir iş akışı düzenlerken görüntülenmesini istemediğiniz güvenli parametreler olabilir [Azure Active Directory kimlik doğrulaması](../connectors/connectors-native-http.md#authentication) bir HTTP eylem.</span><span class="sxs-lookup"><span data-stu-id="bb64e-183">Also, some parameters might be secure parameters you don't want to appear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="bb64e-184">Parametreleri ve güvenli parametrelerini kullanma</span><span class="sxs-lookup"><span data-stu-id="bb64e-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="bb64e-185">Çalışma zamanında kaynak parametresinin değeri erişmek için [iş akışı tanımlama dili](http://aka.ms/logicappsdocs) sağlayan bir `@parameters()` işlemi.</span><span class="sxs-lookup"><span data-stu-id="bb64e-185">To access the value of a resource parameter at runtime, the [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="bb64e-186">Ayrıca, [kaynak dağıtım şablonu parametrelerini belirtin](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="bb64e-186">Also, you can [specify parameters in the resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="bb64e-187">Ancak parametre türü olarak belirtirseniz, `securestring`, parametre kaynak tanımı geri kalanı ile döndürülen olmaz ve dağıtımdan sonra kaynak görüntüleyerek erişilebilir olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="bb64e-187">But if you specify the parameter type as `securestring`, the parameter won't be returned with the rest of the resource definition, and won't be accessible by viewing the resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="bb64e-188">Parametreniz üstbilgileri ya da bir istek gövdesi kullanılırsa, parametre görünür çalıştırma geçmişi ve giden HTTP istek erişerek olabilir.</span><span class="sxs-lookup"><span data-stu-id="bb64e-188">If your parameter is used in the headers or body of a request, the parameter might be visible by accessing the run history and outgoing HTTP request.</span></span> <span data-ttu-id="bb64e-189">İçerik erişim ilkelerinizi uygun şekilde ayarladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bb64e-189">Make sure to set your content access policies accordingly.</span></span>
> <span data-ttu-id="bb64e-190">Yetkilendirme üstbilgileri hiçbir zaman girişleri veya çıkışları görünür.</span><span class="sxs-lookup"><span data-stu-id="bb64e-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="bb64e-191">Bu nedenle gizli var. kullanılıyorsa, gizli alınabilir değil.</span><span class="sxs-lookup"><span data-stu-id="bb64e-191">So if the secret is being used there, the secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="bb64e-192">Gizli anahtarlarla kaynak dağıtım şablonu</span><span class="sxs-lookup"><span data-stu-id="bb64e-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="bb64e-193">Aşağıdaki örnek, bir secure parametresi başvuruda bulunan bir dağıtım gösterir `secret` çalışma zamanında.</span><span class="sxs-lookup"><span data-stu-id="bb64e-193">The following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="bb64e-194">Ayrı Parametreler dosyasında ortamı değerini belirtebilirsiniz `secret`, veya kullanmak [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) almak için zaman adresindeki gizlilik dağıtın.</span><span class="sxs-lookup"><span data-stu-id="bb64e-194">In a separate parameters file, you could specify the environment value for the `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) to retrieve secrets at deploy time.</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is the request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-to-services-receiving-requests-from-a-workflow"></a><span data-ttu-id="bb64e-195">Bir iş akışından isteklerini almak hizmetlerine güvenli erişim</span><span class="sxs-lookup"><span data-stu-id="bb64e-195">Secure access to services receiving requests from a workflow</span></span>

<span data-ttu-id="bb64e-196">Mantıksal uygulama erişmesi gereken herhangi bir uç nokta güvenliğini sağlamak için birçok yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="bb64e-196">There are many ways to help secure any endpoint the logic app needs to access.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="bb64e-197">Giden isteklerinde kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="bb64e-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="bb64e-198">Bir HTTP, HTTP + Swagger (açık API) veya Web kancası eylemi ile çalışırken, gönderilen isteği kimlik doğrulaması ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication to the request being sent.</span></span> <span data-ttu-id="bb64e-199">Temel kimlik doğrulaması, sertifika kimlik doğrulaması veya Azure Active Directory kimlik doğrulaması dahil olabilir.</span><span class="sxs-lookup"><span data-stu-id="bb64e-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="bb64e-200">Bu kimlik doğrulaması yapılandırma hakkında ayrıntılar bulunabilir [bu makalede](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="bb64e-200">Details on how to configure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-to-logic-app-ip-addresses"></a><span data-ttu-id="bb64e-201">Mantıksal uygulama IP adreslerine erişimi kısıtlama</span><span class="sxs-lookup"><span data-stu-id="bb64e-201">Restricting access to logic app IP addresses</span></span>

<span data-ttu-id="bb64e-202">Logic apps gelen tüm çağrıları belirli bir IP adresleri her bölge kümesini gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="bb64e-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="bb64e-203">Yalnızca bu atanan IP adreslerinden gelen istekleri kabul edecek şekilde filtreleme ek ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-203">You can add additional filtering to only accept requests from those designated IP addresses.</span></span> <span data-ttu-id="bb64e-204">Bu IP adresleri listesi için bkz: [mantığı uygulama sınırlarını ve yapılandırmasını](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="bb64e-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="bb64e-205">Şirket içi bağlantı</span><span class="sxs-lookup"><span data-stu-id="bb64e-205">On-premises connectivity</span></span>

<span data-ttu-id="bb64e-206">Logic apps güvenli ve güvenilir sağlamak üzere birkaç hizmetleriyle tümleştirme içi iletişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb64e-206">Logic apps provide integration with several services to provide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="bb64e-207">Şirket içi veri ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="bb64e-207">On-premises data gateway</span></span>

<span data-ttu-id="bb64e-208">Birçok yönetilen bağlayıcılar mantıksal uygulamalar için şirket içi sistemlere dosya sistemi, SQL, SharePoint, DB2 ve daha fazlası da dahil olmak üzere, güvenli bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb64e-208">Many managed connectors for logic apps provide secure connectivity to on-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="bb64e-209">Ağ geçidi şifrelenmiş kanalda Azure Service Bus aracılığıyla şirket içi kaynaklardan veri aktarır.</span><span class="sxs-lookup"><span data-stu-id="bb64e-209">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="bb64e-210">Ağ geçidi aracısından güvenli giden trafik olarak tüm trafiğin kaynaklandığı.</span><span class="sxs-lookup"><span data-stu-id="bb64e-210">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="bb64e-211">Daha fazla bilgi edinmek [veri ağ geçidinin nasıl çalıştığını](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="bb64e-211">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="bb64e-212">Azure API Management</span><span class="sxs-lookup"><span data-stu-id="bb64e-212">Azure API Management</span></span>

<span data-ttu-id="bb64e-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) güvenli proxy'si için siteden siteye VPN ve ExpressRoute tümleştirme ve şirket içi sistemleriyle iletişim dahil olmak üzere şirket içi bağlantı seçenekleri vardır.</span><span class="sxs-lookup"><span data-stu-id="bb64e-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication to on-premises systems.</span></span> <span data-ttu-id="bb64e-214">Mantıksal Uygulama Tasarımcısı'nda, hızlı bir şekilde şirket içi sistemlere hızlı erişim sağlayan Azure API Yönetimi'nden bir iş akışı içinde kullanıma sunulan bir API seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-214">In the Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access to on-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="bb64e-215">Karma bağlantılar Azure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="bb64e-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="bb64e-216">Şirket içi iletişim kurmak için şirket içi karma bağlantı özelliği Azure API ve Web uygulamaları için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb64e-216">You can use the on-premises hybrid connection feature for Azure API and Web apps to communicate on-premises.</span></span>  <span data-ttu-id="bb64e-217">Karma bağlantılar ve nasıl yapılandırılacağı hakkında ayrıntılı bulunabilir [bu makalede](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bb64e-217">Details on hybrid connections and how to configure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb64e-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bb64e-218">Next steps</span></span>
[<span data-ttu-id="bb64e-219">Bir dağıtım şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb64e-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="bb64e-220">Özel durum işleme</span><span class="sxs-lookup"><span data-stu-id="bb64e-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="bb64e-221">Mantıksal uygulamalarınızı izleyin</span><span class="sxs-lookup"><span data-stu-id="bb64e-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="bb64e-222">Mantıksal uygulama hatalarını ve sorunlarını tanılama</span><span class="sxs-lookup"><span data-stu-id="bb64e-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
