---
title: "Azure kaynak İlkesi RequestDisallowedByPolicy hatasıyla | Microsoft Docs"
description: "RequestDisallowedByPolicy hatanın nedenini açıklar."
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
ms.openlocfilehash: 182a27e444c2f5db66d518a1a0c608d3e319d553
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="1db1e-103">Azure kaynak ilkesiyle RequestDisallowedByPolicy hata</span><span class="sxs-lookup"><span data-stu-id="1db1e-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="1db1e-104">RequestDisallowedByPolicy hatanın nedeni, bu makalede, ayrıca bu hata için çözüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="1db1e-104">This article describes the cause of the RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="1db1e-105">Belirti</span><span class="sxs-lookup"><span data-stu-id="1db1e-105">Symptom</span></span>

<span data-ttu-id="1db1e-106">Dağıtım sırasında bir eylem yapmak çalıştığınızda alabileceğiniz bir **RequestDisallowedByPolicy** engellediğini hata gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="1db1e-106">When you try to do an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents the action be performed.</span></span> <span data-ttu-id="1db1e-107">Hatanın bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1db1e-107">The following is a sample of the error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="1db1e-108">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="1db1e-108">Troubleshooting</span></span>

<span data-ttu-id="1db1e-109">Dağıtımınızı engellenen İlkesi hakkındaki ayrıntıları almak için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="1db1e-109">To retrieve details about the policy that blocked your deployment, use the following one of the methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="1db1e-110">Yöntem 1</span><span class="sxs-lookup"><span data-stu-id="1db1e-110">Method 1</span></span>

<span data-ttu-id="1db1e-111">Bu ilke tanımlayıcısı olarak PowerShell'de sağlamak **kimliği** dağıtımınızı engellenen İlkesi hakkındaki ayrıntıları almak için parametre.</span><span class="sxs-lookup"><span data-stu-id="1db1e-111">In PowerShell, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="1db1e-112">Yöntem 2</span><span class="sxs-lookup"><span data-stu-id="1db1e-112">Method 2</span></span> 

<span data-ttu-id="1db1e-113">Azure CLI 2. 0'ilke tanımı adını sağlayın:</span><span class="sxs-lookup"><span data-stu-id="1db1e-113">In Azure CLI 2.0, provide the name of the policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="1db1e-114">Çözüm</span><span class="sxs-lookup"><span data-stu-id="1db1e-114">Solution</span></span>

<span data-ttu-id="1db1e-115">Güvenlik veya uyumluluk, BT departmanınızın genel IP adresleri, ağ güvenlik grupları, kullanıcı tanımlı yollar veya yönlendirme tabloları oluşturma yasaklar kaynak İlkesi zorlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1db1e-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="1db1e-116">"Belirtiler" bölümünde açıklanan hata iletisi örnek adlı ilke **regionPolicyDefinition**, ancak farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1db1e-116">In the sample of the error message that is described in the "Symptoms" section, the policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="1db1e-117">Bu sorunu gidermek için kaynak ilkelerini gözden geçirmek için BT departmanınıza çalışır ve bu ilkeleri ile uyumlu istenen eylemi gerçekleştirmek nasıl belirleyin.</span><span class="sxs-lookup"><span data-stu-id="1db1e-117">To resolve this problem, work with your IT department to review the resource policies, and determine how to perform the requested action in compliance with those policies.</span></span>


<span data-ttu-id="1db1e-118">Daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="1db1e-118">For more information, see the following articles:</span></span>

- [<span data-ttu-id="1db1e-119">Kaynak ilkesine genel bakış</span><span class="sxs-lookup"><span data-stu-id="1db1e-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="1db1e-120">Ortak dağıtım RequestDisallowedByPolicy hataları</span><span class="sxs-lookup"><span data-stu-id="1db1e-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


