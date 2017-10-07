---
title: "aaaSecure erişim tooAzure Logic Apps | Microsoft Docs"
description: "Erişim tootriggers, girişleri ve çıkışları, eylem parametrelerini ve iş akışlarıyla Azure Logic Apps içinde kullanılan hizmetler korumaya yönelik güvenlik ekleyin."
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
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a><span data-ttu-id="002a8-103">Tooyour logic apps güvenli erişim</span><span class="sxs-lookup"><span data-stu-id="002a8-103">Secure access tooyour logic apps</span></span>

<span data-ttu-id="002a8-104">Mantıksal uygulamanızı güvenli birçok Araçlar kullanılabilir toohelp vardır.</span><span class="sxs-lookup"><span data-stu-id="002a8-104">There are many tools available toohelp you secure your logic app.</span></span>

* <span data-ttu-id="002a8-105">Bir mantıksal uygulama (HTTP isteği tetikleyici) erişim tootrigger güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="002a8-105">Securing access tootrigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="002a8-106">Erişim toomanage güvenli hale getirme, düzenleme veya bir mantıksal uygulama okuma</span><span class="sxs-lookup"><span data-stu-id="002a8-106">Securing access toomanage, edit, or read a logic app</span></span>
* <span data-ttu-id="002a8-107">Erişim toocontents girişleri ve çıkışları bir çalışması için güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="002a8-107">Securing access toocontents of inputs and outputs for a run</span></span>
* <span data-ttu-id="002a8-108">Parametreleri ya da bir iş akışında Eylemler içinde girişleri güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="002a8-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="002a8-109">Bir iş akışından isteklerini alacak erişim tooservices güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="002a8-109">Securing access tooservices that receive requests from a workflow</span></span>

## <a name="secure-access-tootrigger"></a><span data-ttu-id="002a8-110">Güvenli erişim tootrigger</span><span class="sxs-lookup"><span data-stu-id="002a8-110">Secure access tootrigger</span></span>

<span data-ttu-id="002a8-111">Bir HTTP isteğiyle tetiklenen bir mantıksal uygulama ile çalışırken ([isteği](../connectors/connectors-native-reqres.md) veya [Web kancası](../connectors/connectors-native-webhook.md)), böylece yalnızca yetkili istemcilerin hello mantıksal uygulama tetikleyebilir erişimi kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="002a8-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire hello logic app.</span></span> <span data-ttu-id="002a8-112">Bir mantıksal uygulama içinde tüm istekleri şifrelenir ve SSL güvenli.</span><span class="sxs-lookup"><span data-stu-id="002a8-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="002a8-113">Paylaşılan erişim imzası</span><span class="sxs-lookup"><span data-stu-id="002a8-113">Shared Access Signature</span></span>

<span data-ttu-id="002a8-114">Her istek uç noktası için bir mantıksal uygulama içeren bir [paylaşılan erişim imzası (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello URL'SİNİN bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="002a8-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of hello URL.</span></span> <span data-ttu-id="002a8-115">Her URL içeren bir `sp`, `sv`, ve `sig` sorgu parametresi.</span><span class="sxs-lookup"><span data-stu-id="002a8-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="002a8-116">İzinleri tarafından belirtilen `sp`, ve izin verilen, tooHTTP yöntemleri karşılık `sv` hello kullanılan sürümü toogenerate olan ve `sig` kullanılan tooauthenticate erişim tootrigger değil.</span><span class="sxs-lookup"><span data-stu-id="002a8-116">Permissions are specified by `sp`, and correspond tooHTTP methods allowed, `sv` is hello version used toogenerate, and `sig` is used tooauthenticate access tootrigger.</span></span> <span data-ttu-id="002a8-117">Merhaba imza, gizli bir anahtar tüm hello URL yollarını ve özellikleri ile Merhaba SHA256 algoritması kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="002a8-117">hello signature is generated using hello SHA256 algorithm with a secret key on all hello URL paths and properties.</span></span> <span data-ttu-id="002a8-118">Merhaba gizli anahtar hiçbir zaman kullanıma sunulan ve yayımlanan ve şifrelenmiş ve hello mantığı uygulamanın parçası olarak depolanan tutulur.</span><span class="sxs-lookup"><span data-stu-id="002a8-118">hello secret key is never exposed and published, and is kept encrypted and stored as part of hello logic app.</span></span> <span data-ttu-id="002a8-119">Mantıksal uygulamanızı yalnızca hello gizli anahtarı ile oluşturulan geçerli bir imzası içeren Tetikleyicileri yetkilendirir.</span><span class="sxs-lookup"><span data-stu-id="002a8-119">Your logic app only authorizes triggers that contain a valid signature created with hello secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="002a8-120">Erişim anahtarlarını yeniden oluştur</span><span class="sxs-lookup"><span data-stu-id="002a8-120">Regenerate access keys</span></span>

<span data-ttu-id="002a8-121">Yeni güvenli bir anahtar adresindeki hello REST API veya Azure portalı üzerinden dilediğiniz zaman yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="002a8-121">You can regenerate a new secure key at anytime through hello REST API or Azure portal.</span></span> <span data-ttu-id="002a8-122">Merhaba eski anahtarı kullanarak önceden oluşturulan tüm geçerli URL'ler geçersiz ve artık yetkili toofire hello mantıksal uygulama ' dir.</span><span class="sxs-lookup"><span data-stu-id="002a8-122">All current URLs that were generated previously using hello old key are invalidated and no longer authorized toofire hello logic app.</span></span>

1. <span data-ttu-id="002a8-123">Hello Azure portal, tooregenerate bir anahtar istediğiniz hello mantıksal uygulama açın</span><span class="sxs-lookup"><span data-stu-id="002a8-123">In hello Azure portal, open hello logic app you want tooregenerate a key</span></span>
1. <span data-ttu-id="002a8-124">Merhaba tıklatın **erişim tuşları** menü öğesi altında **ayarları**</span><span class="sxs-lookup"><span data-stu-id="002a8-124">Click hello **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="002a8-125">Merhaba anahtar tooregenerate ve tam hello işlemi seçin</span><span class="sxs-lookup"><span data-stu-id="002a8-125">Choose hello key tooregenerate and complete hello process</span></span>

<span data-ttu-id="002a8-126">Yeniden oluşturma tamamlandıktan sonra alma URL'leri hello yeni erişim anahtarı ile imzalanmış.</span><span class="sxs-lookup"><span data-stu-id="002a8-126">URLs you retrieve after regeneration are signed with hello new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="002a8-127">Geri çağırma URL'leri bir sona erme tarihi ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="002a8-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="002a8-128">Diğer kuruluşlarla hello URL paylaşıyorsanız, özel anahtarları ve gerektiği gibi sona erme tarihleri ile URL'leri oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="002a8-128">If you are sharing hello URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="002a8-129">Daha sonra sorunsuzca anahtarları alma, veya bir uygulamaya erişim toofire sağlamak belirli timespan kısıtlı tooa değil.</span><span class="sxs-lookup"><span data-stu-id="002a8-129">You can then seamlessly roll keys, or ensure access toofire an app is restricted tooa certain timespan.</span></span> <span data-ttu-id="002a8-130">Merhaba aracılığıyla bir URL'ye ilişkin bir sona erme tarihi belirtebilirsiniz [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="002a8-130">You can specify an expiration date for a URL through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="002a8-131">Merhaba gövdesinde hello özelliğini içeren `NotAfter` bir JSON tarih dizesi döndüren hello kadar yalnızca geçerli bir geri çağırma URL'si `NotAfter` tarih ve saat.</span><span class="sxs-lookup"><span data-stu-id="002a8-131">In hello body, include hello property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until hello `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="002a8-132">Birincil veya ikincil gizli anahtarla URL'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="002a8-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="002a8-133">Oluşturmak veya istek tabanlı tetikleyiciler için geri çağırma URL'lerin listesi, hangi anahtar toouse toosign hello URL de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="002a8-133">When you generate or list callback URLs for request-based triggers, you can also specify which key toouse toosign hello URL.</span></span>  <span data-ttu-id="002a8-134">Merhaba aracılığıyla belirli bir anahtarı tarafından imzalanan bir URL oluşturabileceğiniz [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) gibi:</span><span class="sxs-lookup"><span data-stu-id="002a8-134">You can generate a URL signed by a specific key through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="002a8-135">Merhaba gövdesinde hello özelliğini içeren `KeyType` olarak `Primary` veya `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="002a8-135">In hello body, include hello property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="002a8-136">Merhaba güvenli anahtar belirtilen tarafından imzalanmış bir URL döndürür.</span><span class="sxs-lookup"><span data-stu-id="002a8-136">This returns a URL signed by hello secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="002a8-137">Gelen IP adreslerini kısıtlamak</span><span class="sxs-lookup"><span data-stu-id="002a8-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="002a8-138">Ayrıca toohello paylaşılan erişim imzası, yalnızca belirli istemcilerinden bir mantıksal uygulama çağırma toorestrict isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="002a8-138">In addition toohello Shared Access Signature, you may wish toorestrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="002a8-139">Örneğin, uç noktanızı Azure API Management üzerinden yönetiyorsanız, hello mantığı kısıtlayabilirsiniz uygulama tooonly hello isteği hello API Management örneği IP adres geldiğinde hello isteğini kabul.</span><span class="sxs-lookup"><span data-stu-id="002a8-139">For example, if you manage your endpoint through Azure API Management, you can restrict hello logic app tooonly accept hello request when hello request comes from hello API Management instance IP address.</span></span>

<span data-ttu-id="002a8-140">Bu ayar hello mantığını uygulaması ayarları içinde yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="002a8-140">This setting can be configured within hello logic app settings:</span></span>

1. <span data-ttu-id="002a8-141">Hello Azure portal, tooadd IP adresi sınırlamaları istediğiniz hello mantıksal uygulama açın</span><span class="sxs-lookup"><span data-stu-id="002a8-141">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="002a8-142">Merhaba tıklatın **erişim denetimini yapılandırma** menü öğesi altında **ayarları**</span><span class="sxs-lookup"><span data-stu-id="002a8-142">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="002a8-143">IP adresi aralıkları toobe hello tetik tarafından kabul Hello listesini belirtin</span><span class="sxs-lookup"><span data-stu-id="002a8-143">Specify hello list of IP address ranges toobe accepted by hello trigger</span></span>

<span data-ttu-id="002a8-144">Geçerli bir IP aralığı hello biçimini alır `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="002a8-144">A valid IP range takes hello format `192.168.1.1/255`.</span></span> <span data-ttu-id="002a8-145">Merhaba mantığı uygulama tooonly yangın iç içe geçmiş mantıksal uygulama olarak istiyorsanız hello seçin **yalnızca diğer logic apps** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="002a8-145">If you want hello logic app tooonly fire as a nested logic app, select hello **Only other logic apps** option.</span></span> <span data-ttu-id="002a8-146">Bu seçenek yalnızca çağrılarından hello kendisini (üst mantıksal uygulamalar) yangın başarıyla hizmet anlamına boş dizi toohello kaynak yazar.</span><span class="sxs-lookup"><span data-stu-id="002a8-146">This option writes an empty array toohello resource, meaning only calls from hello service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="002a8-147">Hala bir mantıksal uygulama isteği tetikleyici ile Merhaba REST API çalıştırabilirsiniz / Yönetim `/triggers/{triggerName}/run` IP ne olursa olsun.</span><span class="sxs-lookup"><span data-stu-id="002a8-147">You can still run a logic app with a request trigger through hello REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="002a8-148">Bu senaryo hello Azure REST API'sine karşı kimlik doğrulamasını gerektirir ve tüm olayları hello Azure denetim günlüğünü görünür.</span><span class="sxs-lookup"><span data-stu-id="002a8-148">This scenario requires authentication against hello Azure REST API, and all events would appear in hello Azure Audit Log.</span></span> <span data-ttu-id="002a8-149">Set erişim ilkelerini uygun şekilde denetler.</span><span class="sxs-lookup"><span data-stu-id="002a8-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="002a8-150">IP aralıklarını hello kaynak tanımı'nda ayarlama</span><span class="sxs-lookup"><span data-stu-id="002a8-150">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="002a8-151">Kullanıyorsanız bir [dağıtım şablonu](logic-apps-create-deploy-template.md) tooautomate hello IP aralığı ayarlarını dağıtımlarınızı hello kaynak şablonuna yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="002a8-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

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

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="002a8-152">Azure Active Directory, OAuth veya diğer güvenlik ekleme</span><span class="sxs-lookup"><span data-stu-id="002a8-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="002a8-153">Daha fazla yetkilendirme protokolleri bir mantıksal uygulama üstünde tooadd [Azure API Management](https://azure.microsoft.com/services/api-management/) zengin izleme, güvenlik, ilke ve belgeleri hello yetenek tooexpose ile herhangi bir uç nokta için bir mantıksal uygulama olarak bir API sunar.</span><span class="sxs-lookup"><span data-stu-id="002a8-153">tooadd more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with hello capability tooexpose a logic app as an API.</span></span> <span data-ttu-id="002a8-154">Azure API Management genel veya özel uç noktası için Azure Active Directory, sertifika, OAuth veya diğer güvenlik standartları kullanabilirsiniz hello mantıksal uygulama getirebilir.</span><span class="sxs-lookup"><span data-stu-id="002a8-154">Azure API Management can expose a public or private endpoint for hello logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="002a8-155">Bir istek alındığında, Azure API Management hello isteği toohello mantıksal uygulama (herhangi bir gerekli dönüşümleri veya kısıtlamaları yürütülen gerçekleştirerek) iletir.</span><span class="sxs-lookup"><span data-stu-id="002a8-155">When a request is received, Azure API Management forwards hello request toohello logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="002a8-156">Merhaba mantığı uygulama tooonly ayarlarını hello mantığı uygulama toobe tetiklenen API Yönetimi'nden izin hello gelen IP aralığı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="002a8-156">You can use hello incoming IP range settings on hello logic app tooonly allow hello logic app toobe triggered from API Management.</span></span>

## <a name="secure-access-toomanage-or-edit-logic-apps"></a><span data-ttu-id="002a8-157">Toomanage veya düzenleme logic apps güvenli erişim</span><span class="sxs-lookup"><span data-stu-id="002a8-157">Secure access toomanage or edit logic apps</span></span>

<span data-ttu-id="002a8-158">Yalnızca belirli kullanıcılara veya gruplara hello kaynak mümkün tooperform işlemleri; böylece bir mantıksal uygulama erişim toomanagement işlemlerine kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="002a8-158">You can restrict access toomanagement operations on a logic app so that only specific users or groups are able tooperform operations on hello resource.</span></span> <span data-ttu-id="002a8-159">Logic apps kullanmak hello Azure [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md) özellik ve hello ile özelleştirilebilir aynı araçları.</span><span class="sxs-lookup"><span data-stu-id="002a8-159">Logic apps use hello Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with hello same tools.</span></span>  <span data-ttu-id="002a8-160">Abonelik tooas üyeleri de atayabilirsiniz birkaç yerleşik roller vardır:</span><span class="sxs-lookup"><span data-stu-id="002a8-160">There are a few built-in roles you can assign members of your subscription tooas well:</span></span>

* <span data-ttu-id="002a8-161">**Mantığı uygulamasını katkıda bulunan** -erişim tooview, düzenleme ve güncelleştirme bir mantıksal uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="002a8-161">**Logic App Contributor** - Provides access tooview, edit, and update a logic app.</span></span>  <span data-ttu-id="002a8-162">Merhaba kaynak kaldıramaz veya yönetim işlemleri.</span><span class="sxs-lookup"><span data-stu-id="002a8-162">Cannot remove hello resource or perform admin operations.</span></span>
* <span data-ttu-id="002a8-163">**Mantıksal uygulama işleci** - görüntüleyebilir hello mantıksal uygulama ve çalıştırma geçmişi ve etkinleştir/devre dışı bırak.</span><span class="sxs-lookup"><span data-stu-id="002a8-163">**Logic App Operator** - Can view hello logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="002a8-164">Düzenleyemez veya hello tanımını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="002a8-164">Cannot edit or update hello definition.</span></span>

<span data-ttu-id="002a8-165">Aynı zamanda [Azure kaynak kilidi](../azure-resource-manager/resource-group-lock-resources.md) değiştirme veya silme logic apps tooprevent.</span><span class="sxs-lookup"><span data-stu-id="002a8-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) tooprevent changing or deleting logic apps.</span></span> <span data-ttu-id="002a8-166">Bu özellik değerli tooprevent üretim kaynaklardan değişiklikleri ya da silme işlemleri olur.</span><span class="sxs-lookup"><span data-stu-id="002a8-166">This capability is valuable tooprevent production resources from changes or deletions.</span></span>

## <a name="secure-access-toocontents-of-hello-run-history"></a><span data-ttu-id="002a8-167">Güvenli erişim toocontents çalıştırma geçmişi Merhaba</span><span class="sxs-lookup"><span data-stu-id="002a8-167">Secure access toocontents of hello run history</span></span>

<span data-ttu-id="002a8-168">Önceki çalışır toospecific IP adres aralıklarının erişim toocontents girişleri veya çıkışları kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="002a8-168">You can restrict access toocontents of inputs or outputs from previous runs toospecific IP address ranges.</span></span>  

<span data-ttu-id="002a8-169">Yoldaki ve bekleyen iş akışı çalışması içinde tüm veriler şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="002a8-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="002a8-170">Bir arama toorun geçmişini yapıldığında, hello hizmet hello isteğin kimliğini doğrular ve bağlantıları toohello istek ve yanıt girişleri ve çıkışları sağlar.</span><span class="sxs-lookup"><span data-stu-id="002a8-170">When a call toorun history is made, hello service authenticates hello request and provides links toohello request and response inputs and outputs.</span></span> <span data-ttu-id="002a8-171">Bu bağlantı, atanan IP adres aralığından gelen tooview içeriği döndürmesi hello içeriği korumalı böylece yalnızca istekleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="002a8-171">This link can be protected so only requests tooview content from a designated IP address range return hello contents.</span></span> <span data-ttu-id="002a8-172">Ek erişim denetimi için bu özelliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="002a8-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="002a8-173">Bir IP adresi gibi bile belirtebilirsiniz `0.0.0.0` hiç bir girdi/çıktı erişebilecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="002a8-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="002a8-174">Merhaba olasılığı için 'just-in-time' erişim tooworkflow içerik sağlama yalnızca yönetici izinlerine sahip olan kişi bu kısıtlama kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="002a8-174">Only someone with admin permissions could remove this restriction, providing hello possibility for 'just-in-time' access tooworkflow contents.</span></span>

<span data-ttu-id="002a8-175">Bu ayar hello kaynak ayarlarını hello Azure portalı içinde yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="002a8-175">This setting can be configured within hello resource settings of hello Azure portal:</span></span>

1. <span data-ttu-id="002a8-176">Hello Azure portal, tooadd IP adresi sınırlamaları istediğiniz hello mantıksal uygulama açın</span><span class="sxs-lookup"><span data-stu-id="002a8-176">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="002a8-177">Merhaba tıklatın **erişim denetimini yapılandırma** menü öğesi altında **ayarları**</span><span class="sxs-lookup"><span data-stu-id="002a8-177">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="002a8-178">IP adresi aralıkları için erişim toocontent Hello listesini belirtin</span><span class="sxs-lookup"><span data-stu-id="002a8-178">Specify hello list of IP address ranges for access toocontent</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="002a8-179">IP aralıklarını hello kaynak tanımı'nda ayarlama</span><span class="sxs-lookup"><span data-stu-id="002a8-179">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="002a8-180">Kullanıyorsanız bir [dağıtım şablonu](logic-apps-create-deploy-template.md) tooautomate hello IP aralığı ayarlarını dağıtımlarınızı hello kaynak şablonuna yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="002a8-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

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

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="002a8-181">Güvenli parametreleri ve iş akışı içinde girişleri</span><span class="sxs-lookup"><span data-stu-id="002a8-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="002a8-182">Dağıtım için bir iş akışı tanımı bazı yönlerini tooparameterize ortamlar genelinde isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="002a8-182">You might want tooparameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="002a8-183">Ayrıca, bazı parametreler gibi bir istemci kimliği ve istemci parolası için bir iş akışı düzenlerken tooappear istemiyorsanız güvenli parametreler olabilir [Azure Active Directory kimlik doğrulaması](../connectors/connectors-native-http.md#authentication) bir HTTP eylem.</span><span class="sxs-lookup"><span data-stu-id="002a8-183">Also, some parameters might be secure parameters you don't want tooappear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="002a8-184">Parametreleri ve güvenli parametrelerini kullanma</span><span class="sxs-lookup"><span data-stu-id="002a8-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="002a8-185">tooaccess hello çalışma zamanında kaynak parametresinin değeri hello [iş akışı tanımlama dili](http://aka.ms/logicappsdocs) sağlayan bir `@parameters()` işlemi.</span><span class="sxs-lookup"><span data-stu-id="002a8-185">tooaccess hello value of a resource parameter at runtime, hello [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="002a8-186">Ayrıca, [hello kaynak dağıtım şablonu parametrelerini belirtin](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="002a8-186">Also, you can [specify parameters in hello resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="002a8-187">Ancak başlangıç parametresi türü olarak belirtirseniz, `securestring`, hello parametresi hello hello kaynak tanımı kalanıyla döndürülen olmaz ve dağıtımdan sonra hello kaynak görüntüleyerek erişilebilir olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="002a8-187">But if you specify hello parameter type as `securestring`, hello parameter won't be returned with hello rest of hello resource definition, and won't be accessible by viewing hello resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="002a8-188">Parametreniz hello üstbilgilerinde veya bir istek gövdesi kullanılırsa, hello parametre görünür hello çalıştırma geçmişi ve giden HTTP istek erişerek olabilir.</span><span class="sxs-lookup"><span data-stu-id="002a8-188">If your parameter is used in hello headers or body of a request, hello parameter might be visible by accessing hello run history and outgoing HTTP request.</span></span> <span data-ttu-id="002a8-189">Emin tooset içerik erişim ilkelerinizi buna göre yapın.</span><span class="sxs-lookup"><span data-stu-id="002a8-189">Make sure tooset your content access policies accordingly.</span></span>
> <span data-ttu-id="002a8-190">Yetkilendirme üstbilgileri hiçbir zaman girişleri veya çıkışları görünür.</span><span class="sxs-lookup"><span data-stu-id="002a8-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="002a8-191">Bu nedenle Hello gizli var. kullanılıyorsa hello gizli alınabilir değil.</span><span class="sxs-lookup"><span data-stu-id="002a8-191">So if hello secret is being used there, hello secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="002a8-192">Gizli anahtarlarla kaynak dağıtım şablonu</span><span class="sxs-lookup"><span data-stu-id="002a8-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="002a8-193">Merhaba aşağıdaki örnekte güvenli parametresinin başvuruda bulunan bir dağıtım gösterir `secret` çalışma zamanında.</span><span class="sxs-lookup"><span data-stu-id="002a8-193">hello following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="002a8-194">Ayrı Parametreler dosyasında hello hello ortamı değerini belirtebilirsiniz `secret`, veya [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) adresindeki tooretrieve gizli dağıtmak zaman.</span><span class="sxs-lookup"><span data-stu-id="002a8-194">In a separate parameters file, you could specify hello environment value for hello `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve secrets at deploy time.</span></span>

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
                "body": "This is hello request"
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

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a><span data-ttu-id="002a8-195">Bir iş akışı alma isteklerini tooservices güvenli erişim</span><span class="sxs-lookup"><span data-stu-id="002a8-195">Secure access tooservices receiving requests from a workflow</span></span>

<span data-ttu-id="002a8-196">Herhangi bir uç nokta hello mantığı uygulama tooaccess gereken güvenli birçok yolu toohelp vardır.</span><span class="sxs-lookup"><span data-stu-id="002a8-196">There are many ways toohelp secure any endpoint hello logic app needs tooaccess.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="002a8-197">Giden isteklerinde kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="002a8-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="002a8-198">Bir HTTP, HTTP + Swagger (açık API) veya Web kancası eylemi ile çalışırken, kimlik doğrulama toohello isteği gönderilen ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="002a8-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication toohello request being sent.</span></span> <span data-ttu-id="002a8-199">Temel kimlik doğrulaması, sertifika kimlik doğrulaması veya Azure Active Directory kimlik doğrulaması dahil olabilir.</span><span class="sxs-lookup"><span data-stu-id="002a8-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="002a8-200">Bu kimlik doğrulama tooconfigure nasıl bulunabilir Ayrıntılar [bu makalede](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="002a8-200">Details on how tooconfigure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-toologic-app-ip-addresses"></a><span data-ttu-id="002a8-201">Erişim toologic uygulama IP adreslerine kısıtlama</span><span class="sxs-lookup"><span data-stu-id="002a8-201">Restricting access toologic app IP addresses</span></span>

<span data-ttu-id="002a8-202">Logic apps gelen tüm çağrıları belirli bir IP adresleri her bölge kümesini gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="002a8-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="002a8-203">Ek filtreleme ekleyebilirsiniz tooonly bu IP adreslerini belirlenmiş gelen istekleri kabul edin.</span><span class="sxs-lookup"><span data-stu-id="002a8-203">You can add additional filtering tooonly accept requests from those designated IP addresses.</span></span> <span data-ttu-id="002a8-204">Bu IP adresleri listesi için bkz: [mantığı uygulama sınırlarını ve yapılandırmasını](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="002a8-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="002a8-205">Şirket içi bağlantı</span><span class="sxs-lookup"><span data-stu-id="002a8-205">On-premises connectivity</span></span>

<span data-ttu-id="002a8-206">Logic apps birkaç Hizmetleri tooprovide güvenli ve güvenilir ile tümleştirme içi iletişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="002a8-206">Logic apps provide integration with several services tooprovide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="002a8-207">Şirket içi veri ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="002a8-207">On-premises data gateway</span></span>

<span data-ttu-id="002a8-208">Birçok yönetilen bağlayıcılar mantıksal uygulamalar için güvenli bağlantı tooon içi sistemleri, dosya sistemi, SQL, SharePoint, DB2 ve daha fazlası da dahil olmak üzere sağlar.</span><span class="sxs-lookup"><span data-stu-id="002a8-208">Many managed connectors for logic apps provide secure connectivity tooon-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="002a8-209">Merhaba ağ geçidi şifrelenmiş kanalda hello Azure Service Bus aracılığıyla şirket içi kaynaklardan veri aktarır.</span><span class="sxs-lookup"><span data-stu-id="002a8-209">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="002a8-210">Güvenli giden trafiği hello ağ geçidi aracısından olarak tüm trafiğin kaynaklandığı.</span><span class="sxs-lookup"><span data-stu-id="002a8-210">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="002a8-211">Daha fazla bilgi edinmek [hello veri ağ geçidi nasıl çalıştığını](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="002a8-211">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="002a8-212">Azure API Management</span><span class="sxs-lookup"><span data-stu-id="002a8-212">Azure API Management</span></span>

<span data-ttu-id="002a8-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) güvenli proxy ve iletişim tooon içi sistemler için siteden siteye VPN ve ExpressRoute tümleştirme de dahil olmak üzere şirket içi bağlantı seçenekleri vardır.</span><span class="sxs-lookup"><span data-stu-id="002a8-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication tooon-premises systems.</span></span> <span data-ttu-id="002a8-214">Hello mantığı Uygulama Tasarımcısı'de, hızlı bir şekilde tooon içi sistemleri hızlı erişim sağlayan Azure API Yönetimi'nden bir iş akışı içinde kullanıma sunulan bir API'yi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="002a8-214">In hello Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access tooon-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="002a8-215">Karma bağlantılar Azure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="002a8-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="002a8-216">Azure API ve Web uygulamaları toocommunicate şirket içi hello şirket içi karma bağlantı özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="002a8-216">You can use hello on-premises hybrid connection feature for Azure API and Web apps toocommunicate on-premises.</span></span>  <span data-ttu-id="002a8-217">Karma bağlantılar ve tooconfigure nasıl bulunabilir hakkında ayrıntılar [bu makalede](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="002a8-217">Details on hybrid connections and how tooconfigure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="002a8-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="002a8-218">Next steps</span></span>
[<span data-ttu-id="002a8-219">Bir dağıtım şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="002a8-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="002a8-220">Özel durum işleme</span><span class="sxs-lookup"><span data-stu-id="002a8-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="002a8-221">Mantıksal uygulamalarınızı izleyin</span><span class="sxs-lookup"><span data-stu-id="002a8-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="002a8-222">Mantıksal uygulama hatalarını ve sorunlarını tanılama</span><span class="sxs-lookup"><span data-stu-id="002a8-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
