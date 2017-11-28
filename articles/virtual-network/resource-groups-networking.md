---
title: "aaaNetwork kaynak sağlayıcısı genel bakış | Microsoft Docs"
description: "Merhaba hakkında bilgi edinin yeni ağ kaynak sağlayıcısı Azure Kaynak Yöneticisi'nde"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 81b8f51fe8ee180d8f7885c6e04eb953904d7be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="1577d-103">Ağ Kaynağı Sağlayıcı</span><span class="sxs-lookup"><span data-stu-id="1577d-103">Network Resource Provider</span></span>
<span data-ttu-id="1577d-104">Bir underpinning bugünün iş success içinde gerekiyor özelliği toobuild hello ve büyük ölçekli ağ kullanan uygulamalar Çevik, esnek, güvenli ve tekrarlanabilir bir yolla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1577d-104">An underpinning need in today’s business success, is hello ability toobuild and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="1577d-105">Azure Resource Manager, toocreate gibi uygulamalar, kaynakların kaynak grupları tek bir koleksiyon sağlar.</span><span class="sxs-lookup"><span data-stu-id="1577d-105">Azure Resource Manager enables you toocreate such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="1577d-106">Bu tür kaynakları çeşitli kaynak sağlayıcıları altında Kaynak Yöneticisi üzerinden yönetilir.</span><span class="sxs-lookup"><span data-stu-id="1577d-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="1577d-107">Azure Resource Manager farklı kaynak sağlayıcıları tooprovide erişim tooyour kaynakları kullanır.</span><span class="sxs-lookup"><span data-stu-id="1577d-107">Azure Resource Manager relies on different resource providers tooprovide access tooyour resources.</span></span> <span data-ttu-id="1577d-108">Üç ana kaynak sağlayıcıları vardır: ağ, depolama ve işlem.</span><span class="sxs-lookup"><span data-stu-id="1577d-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="1577d-109">Hello özelliklere ve avantajların yanı sıra hello ağ kaynak sağlayıcısı, bu belgede ele dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="1577d-109">This document discusses hello characteristics and benefits of hello Network Resource Provider, including:</span></span>

* <span data-ttu-id="1577d-110">**Meta veri** – etiketleri kullanarak bilgi tooresources ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1577d-110">**Metadata** – you can add information tooresources using tags.</span></span> <span data-ttu-id="1577d-111">Bu etiketler, kaynak grupları ve abonelikler arasında kullanılan tootrack kaynak kullanımı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1577d-111">These tags can be used tootrack resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="1577d-112">**Ağınızın daha geniş bir denetim** - ağ kaynaklarına gevşek ve daha ayrıntılı bir şekilde kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1577d-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="1577d-113">Başka bir deyişle, hello ağ kaynaklarını yönetme daha fazla esneklik bulunur.</span><span class="sxs-lookup"><span data-stu-id="1577d-113">This means you have more flexibility in managing hello networking resources.</span></span>
* <span data-ttu-id="1577d-114">**Daha hızlı yapılandırma** -ağ kaynaklarına birbirine sıkı şekilde bağlı olduğundan, oluşturabilir ve ağ kaynakları paralel düzenlemek.</span><span class="sxs-lookup"><span data-stu-id="1577d-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="1577d-115">Bu yapılandırma zamanı önemli ölçüde düşürdü.</span><span class="sxs-lookup"><span data-stu-id="1577d-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="1577d-116">**Rol tabanlı erişim denetimi** -RBAC varsayılan rolleriyle belirli güvenlik kapsamında ek tooallowing hello güvenli yönetimi için özel rollerin oluşturulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="1577d-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition tooallowing hello creation of custom roles for secure management.</span></span>
* <span data-ttu-id="1577d-117">**Daha kolay yönetim ve dağıtım** -daha kolay toodeploy olduğundan ve tüm uygulama yığınını tek bir kaynak grubunda kaynaklar koleksiyonu olarak oluşturabileceğiniz beri uygulamalarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="1577d-117">**Easier management and deployment** - it’s easier toodeploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="1577d-118">Ve daha hızlı toodeploy bu yana bir şablon JSON yükü sağlayarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1577d-118">And faster toodeploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="1577d-119">**Hızlı özelleştirme** -dağıtımlarının stili bildirim temelli şablonlar tooenable yinelenebilir ve hızlı özelleştirme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1577d-119">**Rapid customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="1577d-120">**Yinelenebilir özelleştirme** -dağıtımlarının stili bildirim temelli şablonlar tooenable yinelenebilir ve hızlı özelleştirme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1577d-120">**Repeatable customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="1577d-121">**Yönetim arabirimleri** -kaynaklarınızı arabirimleri toomanage aşağıdaki hello birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1577d-121">**Management interfaces** - you can use any of hello following interfaces toomanage your resources:</span></span>
  * <span data-ttu-id="1577d-122">REST tabanlı bir API</span><span class="sxs-lookup"><span data-stu-id="1577d-122">REST based API</span></span>
  * <span data-ttu-id="1577d-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1577d-123">PowerShell</span></span>
  * <span data-ttu-id="1577d-124">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="1577d-124">.NET SDK</span></span>
  * <span data-ttu-id="1577d-125">Node.JS SDK'sı</span><span class="sxs-lookup"><span data-stu-id="1577d-125">Node.JS SDK</span></span>
  * <span data-ttu-id="1577d-126">Java SDK</span><span class="sxs-lookup"><span data-stu-id="1577d-126">Java SDK</span></span>
  * <span data-ttu-id="1577d-127">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1577d-127">Azure CLI</span></span>
  * <span data-ttu-id="1577d-128">Önizleme Portalı</span><span class="sxs-lookup"><span data-stu-id="1577d-128">Preview Portal</span></span>
  * <span data-ttu-id="1577d-129">Resource Manager şablonu dili</span><span class="sxs-lookup"><span data-stu-id="1577d-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="1577d-130">Ağ kaynakları</span><span class="sxs-lookup"><span data-stu-id="1577d-130">Network resources</span></span>
<span data-ttu-id="1577d-131">Tümünü tek işlem kaynağı (bir sanal makine) yönetilen sahip olmak yerine, ağ kaynaklarını bağımsız olarak, artık yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1577d-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="1577d-132">Bu esneklik ve çeviklik bir karmaşık ve büyük ölçekli altyapısında bir kaynak grubu oluşturma, daha yüksek bir düzeyde sağlar.</span><span class="sxs-lookup"><span data-stu-id="1577d-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="1577d-133">Çok katmanlı bir uygulama içeren bir örnek dağıtım kavramsal görünümünü aşağıda sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="1577d-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="1577d-134">NIC, ortak IP adresleri ve sanal makineleri, gibi görmek her bir kaynağın bağımsız olarak yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="1577d-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Ağ kaynak modeli](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="1577d-136">Her kaynak ortak bir özellikler kümesini içerir ve tek tek kendi özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1577d-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="1577d-137">Merhaba ortak özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1577d-137">hello common properties are:</span></span>

| <span data-ttu-id="1577d-138">Özellik</span><span class="sxs-lookup"><span data-stu-id="1577d-138">Property</span></span> | <span data-ttu-id="1577d-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1577d-139">Description</span></span> | <span data-ttu-id="1577d-140">Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="1577d-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1577d-141">**adı**</span><span class="sxs-lookup"><span data-stu-id="1577d-141">**name**</span></span> |<span data-ttu-id="1577d-142">Benzersiz kaynak adı.</span><span class="sxs-lookup"><span data-stu-id="1577d-142">Unique resource name.</span></span> <span data-ttu-id="1577d-143">Her kaynak türünün kendi adlandırma kısıtlamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="1577d-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="1577d-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="1577d-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="1577d-145">**konum**</span><span class="sxs-lookup"><span data-stu-id="1577d-145">**location**</span></span> |<span data-ttu-id="1577d-146">Kaynak hangi hello bulunduğu azure bölgesi</span><span class="sxs-lookup"><span data-stu-id="1577d-146">Azure region in which hello resource resides</span></span> |<span data-ttu-id="1577d-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="1577d-147">westus, eastus</span></span> |
| <span data-ttu-id="1577d-148">**Kimliği**</span><span class="sxs-lookup"><span data-stu-id="1577d-148">**id**</span></span> |<span data-ttu-id="1577d-149">Benzersiz bir URI göre tanımlama</span><span class="sxs-lookup"><span data-stu-id="1577d-149">Unique URI based identification</span></span> |<span data-ttu-id="1577d-150">/Subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="1577d-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="1577d-151">Hello tek tek aşağıdaki hello bölümlerindeki kaynaklardan özelliklerini kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1577d-151">You can check hello individual properties of resources in hello sections below.</span></span>

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a><span data-ttu-id="1577d-152">Yönetim arabirimleri</span><span class="sxs-lookup"><span data-stu-id="1577d-152">Management interfaces</span></span>
<span data-ttu-id="1577d-153">Farklı arabirimleri kullanarak Azure ağ kaynaklarınızı yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="1577d-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="1577d-154">Bu belgede Biz bu arabirimleri satırındaki odaklanacaktır: REST API ve şablonları.</span><span class="sxs-lookup"><span data-stu-id="1577d-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="1577d-155">REST API</span><span class="sxs-lookup"><span data-stu-id="1577d-155">REST API</span></span>
<span data-ttu-id="1577d-156">Daha önce belirtildiği gibi ağ kaynaklarına arabirimleri, REST API'si, .NET SDK'sı, Node.JS SDK'sı, Java SDK'sı, PowerShell, CLI, Azure Portal ve şablonları dahil olmak üzere çeşitli yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="1577d-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="1577d-157">Merhaba Rest API'nin toohello HTTP 1.1 protokolü belirtimi uygun.</span><span class="sxs-lookup"><span data-stu-id="1577d-157">hello Rest API’s conform toohello HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="1577d-158">Merhaba genel URI yapısını hello API aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1577d-158">hello general URI structure of hello API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="1577d-159">Ve küme ayraçları hello parametrelerinde öğeleri aşağıdaki hello temsil eder:</span><span class="sxs-lookup"><span data-stu-id="1577d-159">And hello parameters in braces represent hello following elements:</span></span>

* <span data-ttu-id="1577d-160">**Abonelik kimliği** -Azure abonelik kimliğinizi.</span><span class="sxs-lookup"><span data-stu-id="1577d-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="1577d-161">**Kaynak sağlayıcısı ad** -kullanılan hello sağlayıcısını için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="1577d-161">**resource-provider-namespace** - namespace for hello provider being used.</span></span> <span data-ttu-id="1577d-162">Merhaba ağ kaynak sağlayıcısı için Hello değer *Microsoft.Network*.</span><span class="sxs-lookup"><span data-stu-id="1577d-162">hello value for hello network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="1577d-163">**bölge adı** -hello Azure bölge adı</span><span class="sxs-lookup"><span data-stu-id="1577d-163">**region-name** - hello Azure region name</span></span>

<span data-ttu-id="1577d-164">Merhaba aşağıdaki HTTP yöntemleri REST API çağrıları toohello yapılırken desteklenir:</span><span class="sxs-lookup"><span data-stu-id="1577d-164">hello following HTTP methods are supported when making calls toohello REST API:</span></span>

* <span data-ttu-id="1577d-165">**PUT** - kullanılan toocreate belirli bir türde bir kaynak bir kaynak özelliği değiştirmek veya kaynakları arasında bir ilişki değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1577d-165">**PUT** - used toocreate a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="1577d-166">**Alma** -tooretrieve bilgileri sağlanan bir kaynak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1577d-166">**GET** - used tooretrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="1577d-167">**SİLME** -toodelete mevcut bir kaynağı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1577d-167">**DELETE** - used toodelete an existing resource.</span></span>

<span data-ttu-id="1577d-168">Merhaba istek ve yanıt tooa JSON yükü biçimine uygun.</span><span class="sxs-lookup"><span data-stu-id="1577d-168">Both hello request and response conform tooa JSON payload format.</span></span> <span data-ttu-id="1577d-169">Daha fazla ayrıntı için bkz: [Azure Resource Management API'leri](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="1577d-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="1577d-170">Resource Manager şablonu dili</span><span class="sxs-lookup"><span data-stu-id="1577d-170">Resource Manager template language</span></span>
<span data-ttu-id="1577d-171">Toplama toomanaging kaynaklarında imperatively (aracılığıyla API'leri veya SDK), bildirim temelli bir programlama stili toobuild kullanın ve ağ kaynaklarına hello Resource Manager şablonu dili kullanarak yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1577d-171">In addition toomanaging resources imperatively (via APIs or SDK), you can also use a declarative programming style toobuild and manage network resources by using hello Resource Manager Template Language.</span></span>

<span data-ttu-id="1577d-172">Bir şablon örnek gösterimini aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1577d-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="1577d-173">Merhaba, öncelikle bir JSON hello kaynakları ve açıklama parametreleri aracılığıyla eklenen hello örneği değerleri şablonudur.</span><span class="sxs-lookup"><span data-stu-id="1577d-173">hello template is primarily a JSON description of hello resources and hello instance values injected via parameters.</span></span> <span data-ttu-id="1577d-174">Merhaba örnekte kullanılan toocreate 2 alt ağlar ile bir sanal ağ olabilir.</span><span class="sxs-lookup"><span data-stu-id="1577d-174">hello example below can be used toocreate a virtual network with 2 subnets.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

<span data-ttu-id="1577d-175">Bir şablon kullanırken hello parametre değerlerini el ile sağlama hello seçeneğiniz veya bir parametre dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1577d-175">You have hello option of providing hello parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="1577d-176">Yukarıdaki hello şablonu ile kullanılan parametre değerleri toobe olası bir dizi Hello örnekte gösterilir:</span><span class="sxs-lookup"><span data-stu-id="1577d-176">hello example below shows a possible set of parameter values toobe used with hello template above:</span></span>

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


<span data-ttu-id="1577d-177">şablonları kullanarak hello ana avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1577d-177">hello main advantages of using templates are:</span></span>

* <span data-ttu-id="1577d-178">Bildirim temelli bir stil kaynak grubunda karmaşık bir altyapı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="1577d-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="1577d-179">bağımlılık yönetimi gibi hello kaynakları oluşturma orchestration Merhaba, kaynak yöneticisi tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="1577d-179">hello orchestration of creating hello resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="1577d-180">Merhaba altyapı tekrarlanabilir bir biçimde çeşitli bölgelere ve bir bölge içinde parametreleri değiştirerek oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="1577d-180">hello infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="1577d-181">Merhaba bildirim temelli stili hello şablonları oluşturma ve hello altyapıyı çalışırken tooshorter sağlama süresi yol açar.</span><span class="sxs-lookup"><span data-stu-id="1577d-181">hello declarative style leads tooshorter lead time in building hello templates and rolling out hello infrastructure.</span></span>

<span data-ttu-id="1577d-182">Örnek şablonları için bkz: [Azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="1577d-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="1577d-183">Merhaba Resource Manager şablonu dili hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonu dili](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1577d-183">For more information on hello Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="1577d-184">Merhaba örnek şablonu yukarıdaki hello sanal ağ ve alt ağ kaynaklarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="1577d-184">hello sample template above uses hello virtual network and subnet resources.</span></span> <span data-ttu-id="1577d-185">Aşağıda listelenen kullanabileceğiniz diğer ağ kaynaklarına vardır:</span><span class="sxs-lookup"><span data-stu-id="1577d-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="1577d-186">Bir şablon kullanarak</span><span class="sxs-lookup"><span data-stu-id="1577d-186">Using a template</span></span>
<span data-ttu-id="1577d-187">Bir şablondan Hizmetleri tooAzure Github'dan tıklatın toodeploy gerçekleştirerek veya AzureCLI, PowerShell kullanarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1577d-187">You can deploy services tooAzure from a template by using PowerShell, AzureCLI, or by performing a click toodeploy from GitHub.</span></span> <span data-ttu-id="1577d-188">github'da, bir şablondan toodeploy Hizmetleri hello aşağıdaki adımları yürütün:</span><span class="sxs-lookup"><span data-stu-id="1577d-188">toodeploy services from a template in GitHub, execute hello following steps:</span></span>

1. <span data-ttu-id="1577d-189">Github'dan Hello template3 dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="1577d-189">Open hello template3 file from GitHub.</span></span> <span data-ttu-id="1577d-190">Örnek olarak, açık [iki alt ağ ile sanal ağ](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="1577d-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="1577d-191">Tıklayın **tooAzure dağıtmak**ve toohello üzerinde Azure portal kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1577d-191">Click on **Deploy tooAzure**, and then sign in on toohello Azure portal with your credentials.</span></span>
3. <span data-ttu-id="1577d-192">Merhaba şablon doğrulayın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="1577d-192">Verify hello template, and then click **Save**.</span></span>
4. <span data-ttu-id="1577d-193">Tıklatın **Düzenle parametreleri** ve gibi bir konum seçin *Batı ABD*hello vnet ve alt ağları için.</span><span class="sxs-lookup"><span data-stu-id="1577d-193">Click **Edit parameters** and select a location, such as *West US*, for hello vnet and subnets.</span></span>
5. <span data-ttu-id="1577d-194">Gerekirse, hello değiştirmek **ADDRESSPREFIX** ve **SUBNETPREFIX** parametreleri ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1577d-194">If necessary, change hello **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="1577d-195">Tıklatın **bir kaynak grubu seçin** tooadd hello vnet ve alt ağları istediğiniz hello kaynak grubunu tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1577d-195">Click **Select a resource group** and then click on hello resource group you want tooadd hello vnet and subnets to.</span></span> <span data-ttu-id="1577d-196">Alternatif olarak, tıklatarak yeni bir kaynak grubu oluşturabilirsiniz **veya Yeni Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="1577d-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="1577d-197">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1577d-197">Click **Create**.</span></span> <span data-ttu-id="1577d-198">Döşeme görüntüleme hello fark **sağlama şablon dağıtımı**.</span><span class="sxs-lookup"><span data-stu-id="1577d-198">Notice hello tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="1577d-199">Merhaba dağıtım tamamlandığında, benzer bir ekran tooone aşağıdaki görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1577d-199">Once hello deployment is done, you will see a screen similar tooone below.</span></span>

![Örnek şablon dağıtımı](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="1577d-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1577d-201">Next steps</span></span>
[<span data-ttu-id="1577d-202">Azure Resource Manager şablonu dili</span><span class="sxs-lookup"><span data-stu-id="1577d-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="1577d-203">Azure ağı – şablonları kullanılan</span><span class="sxs-lookup"><span data-stu-id="1577d-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="1577d-204">Azure Resource Manager ve klasik dağıtım</span><span class="sxs-lookup"><span data-stu-id="1577d-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="1577d-205">Azure Resource Manager'a genel bakış</span><span class="sxs-lookup"><span data-stu-id="1577d-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

