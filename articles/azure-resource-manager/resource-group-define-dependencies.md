---
title: "Azure kaynakları için dağıtım sırasını Ayarla | Microsoft Docs"
description: "Bir kaynak olarak başka bir kaynağa bağımlı kaynakları doğru sırayla dağıtılan emin olmak için dağıtım sırasında nasıl kurulacağı açıklanmaktadır."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 3d6a46116ae9d7d940bc10dfa832540f42c0af7e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="define-the-order-for-deploying-resources-in-azure-resource-manager-templates"></a>Azure Resource Manager şablonları kaynaklarında dağıtmak için sipariş tanımlayın
Belirli bir kaynak için kaynak dağıtılmadan önce bulunmalıdır diğer kaynaklara olabilir. Örneğin, bir SQL server SQL veritabanı dağıtmayı denemeden önce mevcut olması gerekir. Bir kaynağı başka kaynaklara bağlı olarak işaretleyerek bu ilişkiyi tanımlayabilirsiniz. Bir bağımlılıkla tanımladığınız **dependsOn** öğesini kullanarak veya **başvuru** işlevi. 

Resource Manager kaynakları arasındaki bağımlılıkları değerlendirir ve bunların bağımlı sırası dağıtır. Kaynakları birbirlerine bağımlı olmadıkları zaman Resource Manager bunları paralel olarak dağıtır. Yalnızca bağımlılıkları dağıtılan kaynaklar için aynı şablonu tanımlamanız gerekir. 

## <a name="dependson"></a>dependsOn
Şablonunuzu içinde dependsOn öğesi bir veya daha fazla kaynak bağlı olarak bir kaynak tanımlamanızı sağlar. Kaynak adlarının virgülle ayrılmış bir liste değeri olabilir. 

Aşağıdaki örnek, bir yük dengeleyici, sanal ağ ve birden çok depolama hesabı oluşturur bir döngü bağlıdır bir sanal makine ölçek kümesini gösterir. Aşağıdaki örnekte bu diğer kaynakları gösterilmez, ancak başka bir yerde şablonda bulunması gerekir.

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

Önceki örnekte, bir bağımlılık adlı bir kopya döngü oluşturulan kaynakları içindedir **storageLoop**. Bir örnek için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).

Bağımlılıklar tanımlarken, Karışıklığı önlemek için kaynak türü ve kaynak sağlayıcısı ad alanı dahil edebilirsiniz. Örneğin, bir yük dengeleyici ve diğer kaynakları aynı adları olabilir sanal ağ açıklamak için aşağıdaki biçimi kullanın:

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

DependsOn kaynaklarınız arasındaki ilişkileri eşlemek için kullanılacak inclined, ancak neden yaptığınız anlamak önemlidir. Örneğin, kaynakları nasıl bağlandığına belgelemek için dependsOn sağ yaklaşım değildir. Dağıtımdan sonra hangi kaynaklara dependsOn öğesinde tanımlanan sorgulayamıyor. Resource Manager bağımlılığı olan paralel iki kaynakları dağıtmayan gerektiğinden dependsOn kullanarak, potansiyel olarak dağıtım süresini etkiler. Kaynakları arasındaki ilişkileri belge, bunun yerine kullanmak için [kaynak bağlama](/rest/api/resources/resourcelinks).

## <a name="child-resources"></a>Alt kaynakları
Kaynaklar özellik tanımlanmakta kaynak ilgili alt kaynakları belirtmenize olanak tanır. Alt kaynakları yalnızca tanımlı beş düzey derinliğinde olabilir. Dolaylı bir bağımlılığı alt kaynağına ve üst arasında oluşturulmaz dikkate almak önemlidir. Üst kaynak sonra dağıtılacak alt kaynak ihtiyacınız varsa, bu bağımlılık dependsOn özelliğiyle açıkça belirtmelidir. 

Her bir üst kaynağın yalnızca belirli kaynak türleri alt kaynakları kabul eder. Kabul edilen kaynak türleri belirtilen [şablon şeması](https://github.com/Azure/azure-resource-manager-schemas) üst kaynak. Üst kaynak türünün adı gibi alt kaynak türü adını içeren **Microsoft.Web/sites/config** ve **Microsoft.Web/sites/extensions** her iki alt kaynakları olan **Microsoft.Web/sites**.

Aşağıdaki örnek, bir SQL server ve SQL veritabanı gösterir. Veritabanı sunucusunun bir alt olsa bile açık bağımlılığı SQL database ve SQL server arasında tanımlanır dikkat edin.

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a>başvuru işlevi
[Başvuru işlevi](resource-group-template-functions-resource.md#reference) ifadenin değerini diğer JSON ad ve değer çiftlerini veya çalışma zamanı kaynakları türetmemize olanak sağlar. Başvuru ifadeleri örtük olarak bir kaynak üzerinde başka bir bağlıdır bildirin. Genel biçimi şöyledir:

```json
reference('resourceName').propertyPath
```

Aşağıdaki örnekte, bir CDN uç noktası açıkça CDN profili bağlıdır ve örtük olarak bir web uygulamasında bağlıdır.

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

Bağımlılıklar belirtmek için bu öğeyi veya dependsOn öğesini kullanabilirsiniz, ancak aynı bağımlı kaynak için her ikisini de kullanmanız gerekmez. Mümkün olduğunda, gereksiz bir bağımlılık ekleme önlemek için dolaylı bir başvuru kullanın.

Daha fazla bilgi için bkz: [başvuru işlevi](resource-group-template-functions-resource.md#reference).

## <a name="recommendations-for-setting-dependencies"></a>Bağımlılıklarını ayarlama önerileri

Ayarlamak için hangi bağımlılıkları karar verirken aşağıdaki yönergeleri kullanın:

* Mümkün olduğunca az bağımlılıkları ayarlayın.
* Bir alt kaynak kendi üst kaynağına bağımlı olarak ayarlayın.
* Kullanım **başvuru** bir özellik paylaşmak için gereken kaynaklar arasında örtük bağımlılıkları ayarlamak üzere işlevi. Açık bir bağımlılık eklemeyin (**dependsOn**) ne zaman önceden tanımladığınız dolaylı bir bağımlılığı. Bu yaklaşım, gereksiz bağımlılıklara sahip olma riskini azaltır. 
* Bir kaynak bulunamadığında bir bağımlılık ayarlama **oluşturulan** başka bir kaynaktan işlevselliği olmadan. Kaynakları yalnızca etkileşimde dağıtımdan sonra bir bağımlılık ayarlı değil.
* Açıkça ayarlamadan basamaklı bağımlılıkları olanak tanır. Örneğin, sanal makinenize bir sanal ağ arabiriminde bağlıdır ve sanal ağ arabirimi bir sanal ağ ve genel IP adreslerine bağlıdır. Bu nedenle, sanal makine dağıtılan tüm üç kaynakları bağlıdır, ancak açıkça sanal makinenin tüm üç kaynaklara bağlı olarak ayarlı değil. Bu yaklaşım, bağımlılık sırası açıklar ve daha sonra şablonu değiştirmek kolaylaştırır.
* Dağıtım öncesinde bir değer belirlenebilir, bir bağımlılık olmadan kaynağın dağıtmayı deneyin. Örneğin, bir yapılandırma değeri başka bir kaynak adı gerekiyorsa, bir bağımlılık gerekmeyebilir. Bazı kaynaklar diğer kaynak varlığını doğrulamak için bu yönergeleri her zaman çalışmaz. Bir hata alırsanız, bir bağımlılık ekleyin. 

Resource Manager şablonu doğrulama sırasında döngüsel bağımlılıklar tanımlar. Döngüsel bağımlılık var olduğunu bildiren bir hata alırsanız, şablonunuzu bağımlılıkları gerekmeyen ve Kaldırılabilir olmadığını değerlendirin. Bağımlılıklarını kaldırma çalışmazsa, bazı dağıtım işlemlerini döngüsel bağımlılık kaynakları sonra dağıtılan alt kaynakları taşınmasını tarafından döngüsel bağımlılıklar önleyebilirsiniz. Örneğin, iki sanal makine dağıtıyorsanız, ancak diğer başvuran her birine özelliklerini ayarlamanız gerekir varsayalım. Bunları şu sırayla dağıtabilirsiniz:

1. VM1
2. vm2
3. Vm1 uzantısı vm1 ve vm2 bağlıdır. Uzantı vm2 alır vm1 değerlerini ayarlar.
4. Vm2 uzantısı vm1 ve vm2 bağlıdır. Uzantı vm1 alır vm2 değerlerini ayarlar.

Dağıtım sırası değerlendirmek ve bağımlılık hataları çözümleme hakkında daha fazla bilgi için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).

## <a name="next-steps"></a>Sonraki adımlar
* Dağıtım sırasında bağımlılıkları sorun giderme hakkında bilgi edinmek için [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).
* Azure Resource Manager şablonları oluşturma hakkında bilgi edinmek için [şablonları yazma](resource-group-authoring-templates.md). 
* Bir şablon kullanılabilir işlevlerin listesi için bkz [şablon işlevleri](resource-group-template-functions.md).

