---
title: "E-posta ve Web kancası uyarı bildirimleri göndermek için otomatik ölçeklendirme eylemlerini kullanın. | Microsoft Belgeleri"
description: "Otomatik ölçeklendirme eylemleri web URL'leri arayın veya Azure İzleyicisi'nde e-posta bildirimleri göndermek için nasıl kullanılacağını bakın. "
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
ms.openlocfilehash: 16caf14028494800e9259f0296c292b606d0210a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-autoscale-actions-to-send-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="527b7-104">E-posta ve Web kancası Azure İzleyicisi'nde uyarı bildirimleri göndermek için otomatik ölçeklendirme eylemleri kullanın</span><span class="sxs-lookup"><span data-stu-id="527b7-104">Use autoscale actions to send email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="527b7-105">Bu makalede, böylece belirli web URL'leri çağrısı veya Azure otomatik ölçeklendirme eylemleri göre e-postalar göndermek Tetikleyicileri nasıl ayarlama gösterilir.</span><span class="sxs-lookup"><span data-stu-id="527b7-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="527b7-106">Web kancaları</span><span class="sxs-lookup"><span data-stu-id="527b7-106">Webhooks</span></span>
<span data-ttu-id="527b7-107">Web kancası, diğer sistemlere işlem sonrası veya özel bildirimleri için Azure uyarı bildirimleri yönlendirmek izin verir.</span><span class="sxs-lookup"><span data-stu-id="527b7-107">Webhooks allow you to route the Azure alert notifications to other systems for post-processing or custom notifications.</span></span> <span data-ttu-id="527b7-108">Örneğin, uyarıyı sohbet kullanarak veya Mesajlaşma bir team services SMS, günlük hataları, bildirim göndermek için gelen bir web isteği işleyebilecek services, vb. için yönlendirme. Web kancası URI geçerli bir HTTP veya HTTPS uç noktası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="527b7-108">For example, routing the alert to services that can handle an incoming web request to send SMS, log bugs, notify a team using chat or messaging services, etc. The webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="527b7-109">E-posta</span><span class="sxs-lookup"><span data-stu-id="527b7-109">Email</span></span>
<span data-ttu-id="527b7-110">Tüm geçerli e-posta adresine e-posta gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="527b7-110">Email can be sent to any valid email address.</span></span> <span data-ttu-id="527b7-111">Yöneticiler ve kural çalıştığı abonelik ortak yöneticileri aynı zamanda bildirilecek.</span><span class="sxs-lookup"><span data-stu-id="527b7-111">Administrators and co-administrators of the subscription where the rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="527b7-112">Bulut Hizmetleri ve Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="527b7-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="527b7-113">Azure portalından bulut Hizmetleri ve sunucu grupları (Web uygulamaları) için katılımı.</span><span class="sxs-lookup"><span data-stu-id="527b7-113">You can opt-in from the Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="527b7-114">Seçin **göre ölçeklendirmeniz** ölçüm.</span><span class="sxs-lookup"><span data-stu-id="527b7-114">Choose the **scale by** metric.</span></span>

![tarafından ölçeklendirme](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="527b7-116">Sanal makine ölçekleme kümeleri</span><span class="sxs-lookup"><span data-stu-id="527b7-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="527b7-117">Yeni Kaynak Yöneticisi (sanal makine ölçek kümeleri) ile oluşturulan sanal makineler için bunu REST API, Resource Manager şablonları, PowerShell ve CLI kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="527b7-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="527b7-118">Bir portal arabirimi henüz kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="527b7-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="527b7-119">REST API veya Resource Manager şablonu kullanırken, aşağıdaki seçeneklere sahip bildirimleri öğesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="527b7-119">When using the REST API or Resource Manager template, include the notifications element with the following options.</span></span>

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
| <span data-ttu-id="527b7-120">Alan</span><span class="sxs-lookup"><span data-stu-id="527b7-120">Field</span></span> | <span data-ttu-id="527b7-121">Zorunlu?</span><span class="sxs-lookup"><span data-stu-id="527b7-121">Mandatory?</span></span> | <span data-ttu-id="527b7-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="527b7-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="527b7-123">işlemi</span><span class="sxs-lookup"><span data-stu-id="527b7-123">operation</span></span> |<span data-ttu-id="527b7-124">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-124">yes</span></span> |<span data-ttu-id="527b7-125">değerin "Ölçek" olması gerekir</span><span class="sxs-lookup"><span data-stu-id="527b7-125">value must be "Scale"</span></span> |
| <span data-ttu-id="527b7-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="527b7-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="527b7-127">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-127">yes</span></span> |<span data-ttu-id="527b7-128">değer "true" veya "false" olmalıdır</span><span class="sxs-lookup"><span data-stu-id="527b7-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="527b7-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="527b7-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="527b7-130">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-130">yes</span></span> |<span data-ttu-id="527b7-131">değer "true" veya "false" olmalıdır</span><span class="sxs-lookup"><span data-stu-id="527b7-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="527b7-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="527b7-132">customEmails</span></span> |<span data-ttu-id="527b7-133">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-133">yes</span></span> |<span data-ttu-id="527b7-134">değer null [] veya e-postaların dize dizisi olabilir</span><span class="sxs-lookup"><span data-stu-id="527b7-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="527b7-135">Web kancaları</span><span class="sxs-lookup"><span data-stu-id="527b7-135">webhooks</span></span> |<span data-ttu-id="527b7-136">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-136">yes</span></span> |<span data-ttu-id="527b7-137">değer null veya geçerli URI olabilir</span><span class="sxs-lookup"><span data-stu-id="527b7-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="527b7-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="527b7-138">serviceUri</span></span> |<span data-ttu-id="527b7-139">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-139">yes</span></span> |<span data-ttu-id="527b7-140">Geçerli bir https URI</span><span class="sxs-lookup"><span data-stu-id="527b7-140">a valid https Uri</span></span> |
| <span data-ttu-id="527b7-141">properties</span><span class="sxs-lookup"><span data-stu-id="527b7-141">properties</span></span> |<span data-ttu-id="527b7-142">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-142">yes</span></span> |<span data-ttu-id="527b7-143">Değer boş {} olması gerekir veya anahtar-değer çiftleri içerebilir</span><span class="sxs-lookup"><span data-stu-id="527b7-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="527b7-144">Web kancası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="527b7-144">Authentication in webhooks</span></span>
<span data-ttu-id="527b7-145">Web kancası Web kancası URI sorgu parametresi olarak bir belirteç kimliği ile kaydettiğiniz belirteç tabanlı kimlik doğrulamasını kullanarak kimlik doğrulaması yapabilir.</span><span class="sxs-lookup"><span data-stu-id="527b7-145">The webhook can authenticate using token-based authentication, where you save the webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="527b7-146">Örneğin, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="527b7-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="527b7-147">Otomatik ölçeklendirme bildirim Web kancası yükü şeması</span><span class="sxs-lookup"><span data-stu-id="527b7-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="527b7-148">Otomatik ölçeklendirme bildirim oluşturulduğunda, aşağıdaki meta verileri Web kancası yükünde eklenmiştir:</span><span class="sxs-lookup"><span data-stu-id="527b7-148">When the autoscale notification is generated, the following metadata is included in the webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' to capacity '2'",
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


| <span data-ttu-id="527b7-149">Alan</span><span class="sxs-lookup"><span data-stu-id="527b7-149">Field</span></span> | <span data-ttu-id="527b7-150">Zorunlu?</span><span class="sxs-lookup"><span data-stu-id="527b7-150">Mandatory?</span></span> | <span data-ttu-id="527b7-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="527b7-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="527b7-152">durum</span><span class="sxs-lookup"><span data-stu-id="527b7-152">status</span></span> |<span data-ttu-id="527b7-153">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-153">yes</span></span> |<span data-ttu-id="527b7-154">Otomatik ölçeklendirme eylemi oluşturulan gösteren durum</span><span class="sxs-lookup"><span data-stu-id="527b7-154">The status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="527b7-155">işlemi</span><span class="sxs-lookup"><span data-stu-id="527b7-155">operation</span></span> |<span data-ttu-id="527b7-156">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-156">yes</span></span> |<span data-ttu-id="527b7-157">Artışı örnekleri için "Ölçeği Genişlet" olur ve bir düşüş için örnekleri, "Ölçek içinde" olacaktır</span><span class="sxs-lookup"><span data-stu-id="527b7-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="527b7-158">bağlam</span><span class="sxs-lookup"><span data-stu-id="527b7-158">context</span></span> |<span data-ttu-id="527b7-159">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-159">yes</span></span> |<span data-ttu-id="527b7-160">Otomatik ölçeklendirme eylem bağlamı</span><span class="sxs-lookup"><span data-stu-id="527b7-160">The autoscale action context</span></span> |
| <span data-ttu-id="527b7-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="527b7-161">timestamp</span></span> |<span data-ttu-id="527b7-162">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-162">yes</span></span> |<span data-ttu-id="527b7-163">Otomatik ölçeklendirme eylemi tetiklendiğinde zaman damgası</span><span class="sxs-lookup"><span data-stu-id="527b7-163">Time stamp when the autoscale action was triggered</span></span> |
| <span data-ttu-id="527b7-164">id</span><span class="sxs-lookup"><span data-stu-id="527b7-164">id</span></span> |<span data-ttu-id="527b7-165">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-165">Yes</span></span> |<span data-ttu-id="527b7-166">Otomatik ölçeklendirme ayarında Resource Manager kimliği</span><span class="sxs-lookup"><span data-stu-id="527b7-166">Resource Manager ID of the autoscale setting</span></span> |
| <span data-ttu-id="527b7-167">ad</span><span class="sxs-lookup"><span data-stu-id="527b7-167">name</span></span> |<span data-ttu-id="527b7-168">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-168">Yes</span></span> |<span data-ttu-id="527b7-169">Otomatik ölçeklendirme ayarı adı</span><span class="sxs-lookup"><span data-stu-id="527b7-169">The name of the autoscale setting</span></span> |
| <span data-ttu-id="527b7-170">Ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="527b7-170">details</span></span> |<span data-ttu-id="527b7-171">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-171">Yes</span></span> |<span data-ttu-id="527b7-172">Otomatik ölçeklendirme hizmet sürdü eylem ve örnek sayısı değişikliği açıklaması</span><span class="sxs-lookup"><span data-stu-id="527b7-172">Explanation of the action that the autoscale service took and the change in the instance count</span></span> |
| <span data-ttu-id="527b7-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="527b7-173">subscriptionId</span></span> |<span data-ttu-id="527b7-174">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-174">Yes</span></span> |<span data-ttu-id="527b7-175">Genişletilmiş hedef kaynak abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="527b7-175">Subscription ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="527b7-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="527b7-176">resourceGroupName</span></span> |<span data-ttu-id="527b7-177">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-177">Yes</span></span> |<span data-ttu-id="527b7-178">Genişletilmiş hedef kaynak kaynak grubu adı</span><span class="sxs-lookup"><span data-stu-id="527b7-178">Resource Group name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="527b7-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="527b7-179">resourceName</span></span> |<span data-ttu-id="527b7-180">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-180">Yes</span></span> |<span data-ttu-id="527b7-181">Genişletilmiş hedef kaynağın adı</span><span class="sxs-lookup"><span data-stu-id="527b7-181">Name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="527b7-182">Kaynak türü</span><span class="sxs-lookup"><span data-stu-id="527b7-182">resourceType</span></span> |<span data-ttu-id="527b7-183">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-183">Yes</span></span> |<span data-ttu-id="527b7-184">Üç desteklenen değerler: "microsoft.classiccompute/domainnames/slots/roles" - bulut hizmeti rolleri, "microsoft.compute/virtualmachinescalesets" - sanal makine ölçek kümeleri ve "Microsoft.Web/serverfarms" - Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="527b7-184">The three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="527b7-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="527b7-185">resourceId</span></span> |<span data-ttu-id="527b7-186">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-186">Yes</span></span> |<span data-ttu-id="527b7-187">Genişletilmiş hedef kaynak Resource Manager kimliği</span><span class="sxs-lookup"><span data-stu-id="527b7-187">Resource Manager ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="527b7-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="527b7-188">portalLink</span></span> |<span data-ttu-id="527b7-189">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-189">Yes</span></span> |<span data-ttu-id="527b7-190">Hedef kaynak Özet sayfasında Azure portalı bağlantı</span><span class="sxs-lookup"><span data-stu-id="527b7-190">Azure portal link to the summary page of the target resource</span></span> |
| <span data-ttu-id="527b7-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="527b7-191">oldCapacity</span></span> |<span data-ttu-id="527b7-192">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-192">Yes</span></span> |<span data-ttu-id="527b7-193">Bir ölçek eylemi otomatik ölçeklendirme geçen zaman geçerli (eski) örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="527b7-193">The current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="527b7-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="527b7-194">newCapacity</span></span> |<span data-ttu-id="527b7-195">Evet</span><span class="sxs-lookup"><span data-stu-id="527b7-195">Yes</span></span> |<span data-ttu-id="527b7-196">Otomatik ölçeklendirme kaynağa ölçeklendirilmiş yeni örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="527b7-196">The new instance count that Autoscale scaled the resource to</span></span> |
| <span data-ttu-id="527b7-197">Özellikler</span><span class="sxs-lookup"><span data-stu-id="527b7-197">Properties</span></span> |<span data-ttu-id="527b7-198">Hayır</span><span class="sxs-lookup"><span data-stu-id="527b7-198">No</span></span> |<span data-ttu-id="527b7-199">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="527b7-199">Optional.</span></span> <span data-ttu-id="527b7-200">< Anahtar, değer > kümesi çiftleri (örneğin, sözlük < dize, dize >).</span><span class="sxs-lookup"><span data-stu-id="527b7-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="527b7-201">Özellikler alanı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="527b7-201">The properties field is optional.</span></span> <span data-ttu-id="527b7-202">Özel kullanıcı arabirimi veya mantığı tabanlı uygulama iş akışı, anahtarlar ve yük kullanılarak geçirilebilir değerler girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="527b7-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using the payload.</span></span> <span data-ttu-id="527b7-203">Web kancası URI kendisini (gibi sorgu parametrelerini) kullanmak için özel özellikler giden Web kancası çağrı geçirmek için alternatif bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="527b7-203">An alternate way to pass custom properties back to the outgoing webhook call is to use the webhook URI itself (as query parameters)</span></span> |
