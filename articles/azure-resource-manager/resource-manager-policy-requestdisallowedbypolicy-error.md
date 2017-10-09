---
title: "Azure kaynak İlkesi aaaRequestDisallowedByPolicy hatasıyla | Microsoft Docs"
description: "Merhaba RequestDisallowedByPolicy hata Hello nedenini açıklar."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 7870e40205cf433ccb4ba02376b5fe809f20d0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="e3a35-103">Azure kaynak ilkesiyle RequestDisallowedByPolicy hata</span><span class="sxs-lookup"><span data-stu-id="e3a35-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="e3a35-104">Merhaba hello RequestDisallowedByPolicy hatanın nedenini bu makalede, ayrıca bu hata için çözüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3a35-104">This article describes hello cause of hello RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="e3a35-105">Belirti</span><span class="sxs-lookup"><span data-stu-id="e3a35-105">Symptom</span></span>

<span data-ttu-id="e3a35-106">Toodo dağıtımı sırasında bir eylem çalıştığınızda alabileceğiniz bir **RequestDisallowedByPolicy** hello engellediğini hata gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e3a35-106">When you try toodo an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents hello action be performed.</span></span> <span data-ttu-id="e3a35-107">Merhaba, hello hata örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="e3a35-107">hello following is a sample of hello error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="e3a35-108">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e3a35-108">Troubleshooting</span></span>

<span data-ttu-id="e3a35-109">Dağıtımınız, engellenen hello İlkesi tooretrieve ayrıntılarını hello yöntemlerden birini aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="e3a35-109">tooretrieve details about hello policy that blocked your deployment, use hello following one of hello methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="e3a35-110">Yöntem 1</span><span class="sxs-lookup"><span data-stu-id="e3a35-110">Method 1</span></span>

<span data-ttu-id="e3a35-111">Bu ilke tanımlayıcısı hello olarak PowerShell'de sağlamak **kimliği** parametresi tooretrieve dağıtımınızı engellenen hello ilkesi ayrıntılarını.</span><span class="sxs-lookup"><span data-stu-id="e3a35-111">In PowerShell, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="e3a35-112">Yöntem 2</span><span class="sxs-lookup"><span data-stu-id="e3a35-112">Method 2</span></span> 

<span data-ttu-id="e3a35-113">Azure CLI 2. 0'hello ilke tanımı hello adını sağlayın:</span><span class="sxs-lookup"><span data-stu-id="e3a35-113">In Azure CLI 2.0, provide hello name of hello policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="e3a35-114">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e3a35-114">Solution</span></span>

<span data-ttu-id="e3a35-115">Güvenlik veya uyumluluk, BT departmanınızın genel IP adresleri, ağ güvenlik grupları, kullanıcı tanımlı yollar veya yönlendirme tabloları oluşturma yasaklar kaynak İlkesi zorlayabilir.</span><span class="sxs-lookup"><span data-stu-id="e3a35-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="e3a35-116">Merhaba "Belirtiler" bölümünde açıklanan hello hata iletisinin Hello örnek hello İlkesi adlı **regionPolicyDefinition**, ancak farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e3a35-116">In hello sample of hello error message that is described in hello "Symptoms" section, hello policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="e3a35-117">tooresolve Bu sorun, BT departmanı tooreview hello kaynak ilkeleriyle çalışmak ve nasıl tooperform hello İstenen eyleme bu ilkeleri ile uyumlu belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e3a35-117">tooresolve this problem, work with your IT department tooreview hello resource policies, and determine how tooperform hello requested action in compliance with those policies.</span></span>


<span data-ttu-id="e3a35-118">Daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e3a35-118">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="e3a35-119">Kaynak ilkesine genel bakış</span><span class="sxs-lookup"><span data-stu-id="e3a35-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="e3a35-120">Ortak dağıtım RequestDisallowedByPolicy hataları</span><span class="sxs-lookup"><span data-stu-id="e3a35-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


