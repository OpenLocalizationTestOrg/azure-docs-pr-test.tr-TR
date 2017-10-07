---
title: "aaaUse otomatik ölçeklendirme eylemleri toosend e-posta ve Web kancası uyarı bildirimleri. | Microsoft Belgeleri"
description: "Nasıl toouse otomatik ölçeklendirme eylemleri toocall URL'leri web veya Azure İzleyicisi'nde e-posta bildirimleri gönderin konusuna bakın. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="96c22-104">Otomatik ölçeklendirme eylemleri toosend e-posta ve Web kancası uyarı bildirimleri Azure İzleyicisi'nde kullanın</span><span class="sxs-lookup"><span data-stu-id="96c22-104">Use autoscale actions toosend email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="96c22-105">Bu makalede, böylece belirli web URL'leri çağrısı veya Azure otomatik ölçeklendirme eylemleri göre e-postalar göndermek Tetikleyicileri nasıl ayarlama gösterilir.</span><span class="sxs-lookup"><span data-stu-id="96c22-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="96c22-106">Web kancaları</span><span class="sxs-lookup"><span data-stu-id="96c22-106">Webhooks</span></span>
<span data-ttu-id="96c22-107">Web kancası tooroute hello Azure uyarı bildirimleri tooother sistemleri işlem sonrası veya özel bildirimleri için izin verir.</span><span class="sxs-lookup"><span data-stu-id="96c22-107">Webhooks allow you tooroute hello Azure alert notifications tooother systems for post-processing or custom notifications.</span></span> <span data-ttu-id="96c22-108">Örneğin, bir gelen web isteği toosend SMS günlük hataları işleyebileceği yönlendirme hello uyarı tooservices Sohbeti kullanarak veya hizmetleri Mesajlaşma takım bildir, vb. hello Web kancası URI geçerli bir HTTP veya HTTPS uç noktası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="96c22-108">For example, routing hello alert tooservices that can handle an incoming web request toosend SMS, log bugs, notify a team using chat or messaging services, etc. hello webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="96c22-109">E-posta</span><span class="sxs-lookup"><span data-stu-id="96c22-109">Email</span></span>
<span data-ttu-id="96c22-110">Tooany geçerli e-posta adresine e-posta gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="96c22-110">Email can be sent tooany valid email address.</span></span> <span data-ttu-id="96c22-111">Yöneticiler ve hello kural çalıştığı hello aboneliğin ortak yöneticileri aynı zamanda bildirilecek.</span><span class="sxs-lookup"><span data-stu-id="96c22-111">Administrators and co-administrators of hello subscription where hello rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="96c22-112">Bulut Hizmetleri ve Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="96c22-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="96c22-113">Azure portal hello bulut Hizmetleri ve sunucu grupları (Web uygulamaları) için katılımı.</span><span class="sxs-lookup"><span data-stu-id="96c22-113">You can opt-in from hello Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="96c22-114">Merhaba seçin **göre ölçeklendirmeniz** ölçüm.</span><span class="sxs-lookup"><span data-stu-id="96c22-114">Choose hello **scale by** metric.</span></span>

![tarafından ölçeklendirme](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="96c22-116">Sanal makine ölçekleme kümeleri</span><span class="sxs-lookup"><span data-stu-id="96c22-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="96c22-117">Yeni Kaynak Yöneticisi (sanal makine ölçek kümeleri) ile oluşturulan sanal makineler için bunu REST API, Resource Manager şablonları, PowerShell ve CLI kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96c22-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="96c22-118">Bir portal arabirimi henüz kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="96c22-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="96c22-119">Hello REST API veya Resource Manager şablonunu kullandığınızda, aşağıdaki seçenekleri şu hello ile Merhaba bildirimleri öğesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="96c22-119">When using hello REST API or Resource Manager template, include hello notifications element with hello following options.</span></span>

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| <span data-ttu-id="96c22-120">Alan</span><span class="sxs-lookup"><span data-stu-id="96c22-120">Field</span></span> | <span data-ttu-id="96c22-121">Zorunlu?</span><span class="sxs-lookup"><span data-stu-id="96c22-121">Mandatory?</span></span> | <span data-ttu-id="96c22-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="96c22-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="96c22-123">işlemi</span><span class="sxs-lookup"><span data-stu-id="96c22-123">operation</span></span> |<span data-ttu-id="96c22-124">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-124">yes</span></span> |<span data-ttu-id="96c22-125">değerin "Ölçek" olması gerekir</span><span class="sxs-lookup"><span data-stu-id="96c22-125">value must be "Scale"</span></span> |
| <span data-ttu-id="96c22-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="96c22-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="96c22-127">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-127">yes</span></span> |<span data-ttu-id="96c22-128">değer "true" veya "false" olmalıdır</span><span class="sxs-lookup"><span data-stu-id="96c22-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="96c22-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="96c22-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="96c22-130">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-130">yes</span></span> |<span data-ttu-id="96c22-131">değer "true" veya "false" olmalıdır</span><span class="sxs-lookup"><span data-stu-id="96c22-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="96c22-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="96c22-132">customEmails</span></span> |<span data-ttu-id="96c22-133">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-133">yes</span></span> |<span data-ttu-id="96c22-134">değer null [] veya e-postaların dize dizisi olabilir</span><span class="sxs-lookup"><span data-stu-id="96c22-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="96c22-135">Web kancaları</span><span class="sxs-lookup"><span data-stu-id="96c22-135">webhooks</span></span> |<span data-ttu-id="96c22-136">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-136">yes</span></span> |<span data-ttu-id="96c22-137">değer null veya geçerli URI olabilir</span><span class="sxs-lookup"><span data-stu-id="96c22-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="96c22-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="96c22-138">serviceUri</span></span> |<span data-ttu-id="96c22-139">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-139">yes</span></span> |<span data-ttu-id="96c22-140">Geçerli bir https URI</span><span class="sxs-lookup"><span data-stu-id="96c22-140">a valid https Uri</span></span> |
| <span data-ttu-id="96c22-141">properties</span><span class="sxs-lookup"><span data-stu-id="96c22-141">properties</span></span> |<span data-ttu-id="96c22-142">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-142">yes</span></span> |<span data-ttu-id="96c22-143">Değer boş {} olması gerekir veya anahtar-değer çiftleri içerebilir</span><span class="sxs-lookup"><span data-stu-id="96c22-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="96c22-144">Web kancası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="96c22-144">Authentication in webhooks</span></span>
<span data-ttu-id="96c22-145">Merhaba Web kancası hello Web kancası URI sorgu parametresi olarak bir belirteç kimliği ile kaydettiğiniz belirteç tabanlı kimlik doğrulamasını kullanarak kimlik doğrulaması yapabilir.</span><span class="sxs-lookup"><span data-stu-id="96c22-145">hello webhook can authenticate using token-based authentication, where you save hello webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="96c22-146">Örneğin, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="96c22-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="96c22-147">Otomatik ölçeklendirme bildirim Web kancası yükü şeması</span><span class="sxs-lookup"><span data-stu-id="96c22-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="96c22-148">Merhaba otomatik ölçeklendirme bildirim oluşturulduğunda hello aşağıdaki meta verileri hello Web kancası yükünde eklenmiştir:</span><span class="sxs-lookup"><span data-stu-id="96c22-148">When hello autoscale notification is generated, hello following metadata is included in hello webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| <span data-ttu-id="96c22-149">Alan</span><span class="sxs-lookup"><span data-stu-id="96c22-149">Field</span></span> | <span data-ttu-id="96c22-150">Zorunlu?</span><span class="sxs-lookup"><span data-stu-id="96c22-150">Mandatory?</span></span> | <span data-ttu-id="96c22-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="96c22-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="96c22-152">durum</span><span class="sxs-lookup"><span data-stu-id="96c22-152">status</span></span> |<span data-ttu-id="96c22-153">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-153">yes</span></span> |<span data-ttu-id="96c22-154">otomatik ölçeklendirme eylemi oluşturulan gösterir hello durumu</span><span class="sxs-lookup"><span data-stu-id="96c22-154">hello status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="96c22-155">işlemi</span><span class="sxs-lookup"><span data-stu-id="96c22-155">operation</span></span> |<span data-ttu-id="96c22-156">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-156">yes</span></span> |<span data-ttu-id="96c22-157">Artışı örnekleri için "Ölçeği Genişlet" olur ve bir düşüş için örnekleri, "Ölçek içinde" olacaktır</span><span class="sxs-lookup"><span data-stu-id="96c22-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="96c22-158">bağlam</span><span class="sxs-lookup"><span data-stu-id="96c22-158">context</span></span> |<span data-ttu-id="96c22-159">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-159">yes</span></span> |<span data-ttu-id="96c22-160">Merhaba otomatik ölçeklendirme eylem bağlamı</span><span class="sxs-lookup"><span data-stu-id="96c22-160">hello autoscale action context</span></span> |
| <span data-ttu-id="96c22-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="96c22-161">timestamp</span></span> |<span data-ttu-id="96c22-162">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-162">yes</span></span> |<span data-ttu-id="96c22-163">Merhaba otomatik ölçeklendirme eylemi tetiklendiğinde zaman damgası</span><span class="sxs-lookup"><span data-stu-id="96c22-163">Time stamp when hello autoscale action was triggered</span></span> |
| <span data-ttu-id="96c22-164">id</span><span class="sxs-lookup"><span data-stu-id="96c22-164">id</span></span> |<span data-ttu-id="96c22-165">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-165">Yes</span></span> |<span data-ttu-id="96c22-166">Resource Manager Kimliğini hello otomatik ölçeklendirme ayarı</span><span class="sxs-lookup"><span data-stu-id="96c22-166">Resource Manager ID of hello autoscale setting</span></span> |
| <span data-ttu-id="96c22-167">ad</span><span class="sxs-lookup"><span data-stu-id="96c22-167">name</span></span> |<span data-ttu-id="96c22-168">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-168">Yes</span></span> |<span data-ttu-id="96c22-169">Hello hello otomatik ölçeklendirme ayarı adı</span><span class="sxs-lookup"><span data-stu-id="96c22-169">hello name of hello autoscale setting</span></span> |
| <span data-ttu-id="96c22-170">Ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="96c22-170">details</span></span> |<span data-ttu-id="96c22-171">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-171">Yes</span></span> |<span data-ttu-id="96c22-172">Otomatik ölçeklendirme hizmet hello hello eylem açıklaması sürdü ve hello değiştirmek hello örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="96c22-172">Explanation of hello action that hello autoscale service took and hello change in hello instance count</span></span> |
| <span data-ttu-id="96c22-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="96c22-173">subscriptionId</span></span> |<span data-ttu-id="96c22-174">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-174">Yes</span></span> |<span data-ttu-id="96c22-175">Abonelik kimliği ölçeklendirilir hello hedef kaynak</span><span class="sxs-lookup"><span data-stu-id="96c22-175">Subscription ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="96c22-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="96c22-176">resourceGroupName</span></span> |<span data-ttu-id="96c22-177">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-177">Yes</span></span> |<span data-ttu-id="96c22-178">Genişletilmiş hello hedef kaynak kaynak grubu adı</span><span class="sxs-lookup"><span data-stu-id="96c22-178">Resource Group name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="96c22-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="96c22-179">resourceName</span></span> |<span data-ttu-id="96c22-180">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-180">Yes</span></span> |<span data-ttu-id="96c22-181">Genişletilmiş hello hedef kaynağın adı</span><span class="sxs-lookup"><span data-stu-id="96c22-181">Name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="96c22-182">Kaynak türü</span><span class="sxs-lookup"><span data-stu-id="96c22-182">resourceType</span></span> |<span data-ttu-id="96c22-183">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-183">Yes</span></span> |<span data-ttu-id="96c22-184">Merhaba üç desteklenen değerler: "microsoft.classiccompute/domainnames/slots/roles" - bulut hizmeti rolleri, "microsoft.compute/virtualmachinescalesets" - sanal makine ölçek kümeleri ve "Microsoft.Web/serverfarms" - Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="96c22-184">hello three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="96c22-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="96c22-185">resourceId</span></span> |<span data-ttu-id="96c22-186">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-186">Yes</span></span> |<span data-ttu-id="96c22-187">Genişletilmiş hello hedef kaynak Resource Manager kimliği</span><span class="sxs-lookup"><span data-stu-id="96c22-187">Resource Manager ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="96c22-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="96c22-188">portalLink</span></span> |<span data-ttu-id="96c22-189">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-189">Yes</span></span> |<span data-ttu-id="96c22-190">Azure portal bağlantısı toohello Özet sayfasında hello hedef kaynak</span><span class="sxs-lookup"><span data-stu-id="96c22-190">Azure portal link toohello summary page of hello target resource</span></span> |
| <span data-ttu-id="96c22-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="96c22-191">oldCapacity</span></span> |<span data-ttu-id="96c22-192">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-192">Yes</span></span> |<span data-ttu-id="96c22-193">bir ölçek eylemi otomatik ölçeklendirme geçen zaman hello geçerli (eski) örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="96c22-193">hello current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="96c22-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="96c22-194">newCapacity</span></span> |<span data-ttu-id="96c22-195">Evet</span><span class="sxs-lookup"><span data-stu-id="96c22-195">Yes</span></span> |<span data-ttu-id="96c22-196">otomatik ölçeklendirme hello kaynak çok ölçeklendirilmiş hello yeni örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="96c22-196">hello new instance count that Autoscale scaled hello resource too</span></span>|
| <span data-ttu-id="96c22-197">Özellikler</span><span class="sxs-lookup"><span data-stu-id="96c22-197">Properties</span></span> |<span data-ttu-id="96c22-198">Hayır</span><span class="sxs-lookup"><span data-stu-id="96c22-198">No</span></span> |<span data-ttu-id="96c22-199">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="96c22-199">Optional.</span></span> <span data-ttu-id="96c22-200">< Anahtar, değer > kümesi çiftleri (örneğin, sözlük < dize, dize >).</span><span class="sxs-lookup"><span data-stu-id="96c22-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="96c22-201">Merhaba özellikleri alan isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="96c22-201">hello properties field is optional.</span></span> <span data-ttu-id="96c22-202">Özel kullanıcı arabirimi veya mantığı tabanlı uygulama iş akışı, anahtarlar ve hello yükü kullanılarak geçirilebilir değerler girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96c22-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using hello payload.</span></span> <span data-ttu-id="96c22-203">Toouse hello Web kancası URI kendisini (gibi sorgu parametrelerini) toopass özel özellikler toohello giden Web kancası çağrı başa alternatif bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="96c22-203">An alternate way toopass custom properties back toohello outgoing webhook call is toouse hello webhook URI itself (as query parameters)</span></span> |
