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
# <a name="network-resource-provider"></a>Ağ Kaynağı Sağlayıcı
Bir underpinning bugünün iş success içinde gerekiyor özelliği toobuild hello ve büyük ölçekli ağ kullanan uygulamalar Çevik, esnek, güvenli ve tekrarlanabilir bir yolla yönetebilirsiniz. Azure Resource Manager, toocreate gibi uygulamalar, kaynakların kaynak grupları tek bir koleksiyon sağlar. Bu tür kaynakları çeşitli kaynak sağlayıcıları altında Kaynak Yöneticisi üzerinden yönetilir.

Azure Resource Manager farklı kaynak sağlayıcıları tooprovide erişim tooyour kaynakları kullanır. Üç ana kaynak sağlayıcıları vardır: ağ, depolama ve işlem. Hello özelliklere ve avantajların yanı sıra hello ağ kaynak sağlayıcısı, bu belgede ele dahil olmak üzere:

* **Meta veri** – etiketleri kullanarak bilgi tooresources ekleyebilirsiniz. Bu etiketler, kaynak grupları ve abonelikler arasında kullanılan tootrack kaynak kullanımı olabilir.
* **Ağınızın daha geniş bir denetim** - ağ kaynaklarına gevşek ve daha ayrıntılı bir şekilde kontrol edebilirsiniz. Başka bir deyişle, hello ağ kaynaklarını yönetme daha fazla esneklik bulunur.
* **Daha hızlı yapılandırma** -ağ kaynaklarına birbirine sıkı şekilde bağlı olduğundan, oluşturabilir ve ağ kaynakları paralel düzenlemek. Bu yapılandırma zamanı önemli ölçüde düşürdü.
* **Rol tabanlı erişim denetimi** -RBAC varsayılan rolleriyle belirli güvenlik kapsamında ek tooallowing hello güvenli yönetimi için özel rollerin oluşturulmasını sağlar.
* **Daha kolay yönetim ve dağıtım** -daha kolay toodeploy olduğundan ve tüm uygulama yığınını tek bir kaynak grubunda kaynaklar koleksiyonu olarak oluşturabileceğiniz beri uygulamalarını yönetme. Ve daha hızlı toodeploy bu yana bir şablon JSON yükü sağlayarak dağıtabilirsiniz.
* **Hızlı özelleştirme** -dağıtımlarının stili bildirim temelli şablonlar tooenable yinelenebilir ve hızlı özelleştirme kullanabilirsiniz.
* **Yinelenebilir özelleştirme** -dağıtımlarının stili bildirim temelli şablonlar tooenable yinelenebilir ve hızlı özelleştirme kullanabilirsiniz.
* **Yönetim arabirimleri** -kaynaklarınızı arabirimleri toomanage aşağıdaki hello birini kullanabilirsiniz:
  * REST tabanlı bir API
  * PowerShell
  * .NET SDK
  * Node.JS SDK'sı
  * Java SDK
  * Azure CLI
  * Önizleme Portalı
  * Resource Manager şablonu dili

## <a name="network-resources"></a>Ağ kaynakları
Tümünü tek işlem kaynağı (bir sanal makine) yönetilen sahip olmak yerine, ağ kaynaklarını bağımsız olarak, artık yönetebilirsiniz. Bu esneklik ve çeviklik bir karmaşık ve büyük ölçekli altyapısında bir kaynak grubu oluşturma, daha yüksek bir düzeyde sağlar.

Çok katmanlı bir uygulama içeren bir örnek dağıtım kavramsal görünümünü aşağıda sunulmuştur. NIC, ortak IP adresleri ve sanal makineleri, gibi görmek her bir kaynağın bağımsız olarak yönetilebilir.

![Ağ kaynak modeli](./media/resource-groups-networking/Figure2.png)

Her kaynak ortak bir özellikler kümesini içerir ve tek tek kendi özelliğini ayarlayın. Merhaba ortak özellikleri şunlardır:

| Özellik | Açıklama | Örnek değerler |
| --- | --- | --- |
| **adı** |Benzersiz kaynak adı. Her kaynak türünün kendi adlandırma kısıtlamaları vardır. |PIP01, VM01, NIC01 |
| **konum** |Kaynak hangi hello bulunduğu azure bölgesi |westus, eastus |
| **Kimliği** |Benzersiz bir URI göre tanımlama |/Subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP |

Hello tek tek aşağıdaki hello bölümlerindeki kaynaklardan özelliklerini kontrol edebilirsiniz.

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

## <a name="management-interfaces"></a>Yönetim arabirimleri
Farklı arabirimleri kullanarak Azure ağ kaynaklarınızı yönetebilir. Bu belgede Biz bu arabirimleri satırındaki odaklanacaktır: REST API ve şablonları.

### <a name="rest-api"></a>REST API
Daha önce belirtildiği gibi ağ kaynaklarına arabirimleri, REST API'si, .NET SDK'sı, Node.JS SDK'sı, Java SDK'sı, PowerShell, CLI, Azure Portal ve şablonları dahil olmak üzere çeşitli yönetilebilir.

Merhaba Rest API'nin toohello HTTP 1.1 protokolü belirtimi uygun. Merhaba genel URI yapısını hello API aşağıda gösterilmiştir:

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

Ve küme ayraçları hello parametrelerinde öğeleri aşağıdaki hello temsil eder:

* **Abonelik kimliği** -Azure abonelik kimliğinizi.
* **Kaynak sağlayıcısı ad** -kullanılan hello sağlayıcısını için ad alanı. Merhaba ağ kaynak sağlayıcısı için Hello değer *Microsoft.Network*.
* **bölge adı** -hello Azure bölge adı

Merhaba aşağıdaki HTTP yöntemleri REST API çağrıları toohello yapılırken desteklenir:

* **PUT** - kullanılan toocreate belirli bir türde bir kaynak bir kaynak özelliği değiştirmek veya kaynakları arasında bir ilişki değiştirin.
* **Alma** -tooretrieve bilgileri sağlanan bir kaynak için kullanılır.
* **SİLME** -toodelete mevcut bir kaynağı kullanılır.

Merhaba istek ve yanıt tooa JSON yükü biçimine uygun. Daha fazla ayrıntı için bkz: [Azure Resource Management API'leri](https://msdn.microsoft.com/library/azure/dn948464.aspx).

### <a name="resource-manager-template-language"></a>Resource Manager şablonu dili
Toplama toomanaging kaynaklarında imperatively (aracılığıyla API'leri veya SDK), bildirim temelli bir programlama stili toobuild kullanın ve ağ kaynaklarına hello Resource Manager şablonu dili kullanarak yönetebilirsiniz.

Bir şablon örnek gösterimini aşağıda verilmiştir:

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

Merhaba, öncelikle bir JSON hello kaynakları ve açıklama parametreleri aracılığıyla eklenen hello örneği değerleri şablonudur. Merhaba örnekte kullanılan toocreate 2 alt ağlar ile bir sanal ağ olabilir.

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

Bir şablon kullanırken hello parametre değerlerini el ile sağlama hello seçeneğiniz veya bir parametre dosyası kullanabilirsiniz. Yukarıdaki hello şablonu ile kullanılan parametre değerleri toobe olası bir dizi Hello örnekte gösterilir:

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


şablonları kullanarak hello ana avantajları şunlardır:

* Bildirim temelli bir stil kaynak grubunda karmaşık bir altyapı oluşturabilir. bağımlılık yönetimi gibi hello kaynakları oluşturma orchestration Merhaba, kaynak yöneticisi tarafından işlenir.
* Merhaba altyapı tekrarlanabilir bir biçimde çeşitli bölgelere ve bir bölge içinde parametreleri değiştirerek oluşturulabilir.
* Merhaba bildirim temelli stili hello şablonları oluşturma ve hello altyapıyı çalışırken tooshorter sağlama süresi yol açar.

Örnek şablonları için bkz: [Azure hızlı başlangıç şablonlarını](https://github.com/Azure/azure-quickstart-templates).

Merhaba Resource Manager şablonu dili hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonu dili](../azure-resource-manager/resource-group-authoring-templates.md).

Merhaba örnek şablonu yukarıdaki hello sanal ağ ve alt ağ kaynaklarını kullanır. Aşağıda listelenen kullanabileceğiniz diğer ağ kaynaklarına vardır:

### <a name="using-a-template"></a>Bir şablon kullanarak
Bir şablondan Hizmetleri tooAzure Github'dan tıklatın toodeploy gerçekleştirerek veya AzureCLI, PowerShell kullanarak dağıtabilirsiniz. github'da, bir şablondan toodeploy Hizmetleri hello aşağıdaki adımları yürütün:

1. Github'dan Hello template3 dosyasını açın. Örnek olarak, açık [iki alt ağ ile sanal ağ](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).
2. Tıklayın **tooAzure dağıtmak**ve toohello üzerinde Azure portal kimlik bilgilerinizle oturum açın.
3. Merhaba şablon doğrulayın ve ardından **kaydetmek**.
4. Tıklatın **Düzenle parametreleri** ve gibi bir konum seçin *Batı ABD*hello vnet ve alt ağları için.
5. Gerekirse, hello değiştirmek **ADDRESSPREFIX** ve **SUBNETPREFIX** parametreleri ve ardından **Tamam**.
6. Tıklatın **bir kaynak grubu seçin** tooadd hello vnet ve alt ağları istediğiniz hello kaynak grubunu tıklayın. Alternatif olarak, tıklatarak yeni bir kaynak grubu oluşturabilirsiniz **veya Yeni Oluştur**.
7. **Oluştur**'a tıklayın. Döşeme görüntüleme hello fark **sağlama şablon dağıtımı**. Merhaba dağıtım tamamlandığında, benzer bir ekran tooone aşağıdaki görürsünüz.

![Örnek şablon dağıtımı](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a>Sonraki adımlar
[Azure Resource Manager şablonu dili](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure ağı – şablonları kullanılan](https://github.com/Azure/azure-quickstart-templates)

[Azure Resource Manager ve klasik dağıtım](../azure-resource-manager/resource-manager-deployment-model.md)

[Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md)

