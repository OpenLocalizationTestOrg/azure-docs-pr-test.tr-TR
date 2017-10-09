---
title: "Azure kaynakları için bir dağıtım sırasıyla aaaSet | Microsoft Docs"
description: "Açıklar nasıl tooset bir kaynak dağıtım tooensure kaynaklarını sırasında başka bir kaynağa bağlı olarak dağıtılan hello doğru sırayla."
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
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a>Azure Resource Manager şablonları kaynaklarında dağıtmak için hello düzenini tanımlayın
Belirli bir kaynak için hello kaynak dağıtılmadan önce bulunmalıdır diğer kaynaklara olabilir. Örneğin, bir SQL server toodeploy bir SQL veritabanı denemeden önce mevcut olması gerekir. Bu ilişki hello bağlı olarak bir kaynak işaretleyerek diğer kaynak tanımlarsınız. Merhaba bir bağımlılıkla tanımladığınız **dependsOn** öğesi veya hello kullanarak **başvuru** işlevi. 

Resource Manager kaynakları arasındaki hello bağımlılıkları değerlendirir ve bunların bağımlı sırası dağıtır. Kaynakları birbirlerine bağımlı olmadıkları zaman Resource Manager bunları paralel olarak dağıtır. Yalnızca toodefine bağımlılıkları hello dağıtılan kaynaklar için gereksinim duyduğunuz aynı şablonu. 

## <a name="dependson"></a>dependsOn
Şablonunuzu içinde hello dependsOn öğesi, toodefine bir kaynak olarak bir veya daha fazla kaynak bağımlı etkinleştirir. Kaynak adlarının virgülle ayrılmış bir liste değeri olabilir. 

Merhaba aşağıdaki örnekte bir yük dengeleyici, sanal ağ ve birden çok depolama hesabı oluşturur bir döngü bağlıdır bir sanal makine ölçek kümesi gösterilmektedir. Bu diğer kaynakları aşağıdaki örneğine hello gösterilmez, ancak başka bir yerde hello şablonunda tooexist gerekir.

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

Örnek önceki hello içinde bir bağımlılık adlı bir kopya döngü oluşturan hello kaynakları içindedir **storageLoop**. Bir örnek için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).

Bağımlılıklar tanımlarken hello kaynak sağlayıcısı ad alanı ve kaynak türü tooavoid belirsizlik içerebilir. Örneğin, bir yük dengeleyici ve aynı kullanım hello aşağıdaki gibi diğer kaynaklar adları hello olabilir sanal ağ biçim tooclarify:

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

Kaynaklarınız arasında eilimli toouse dependsOn toomap ilişkileri olabilir, ancak neden yaptığınız önemli toounderstand var. Örneğin, kaynakları nasıl bağlandığına, toodocument dependsOn hello sağ yaklaşım değildir. Dağıtımdan sonra hangi kaynaklara hello dependsOn öğesinde tanımlanan sorgulayamıyor. Resource Manager bağımlılığı olan paralel iki kaynakları dağıtmayan gerektiğinden dependsOn kullanarak, potansiyel olarak dağıtım süresini etkiler. kaynaklar arasındaki toodocument ilişkileri kullanmanız [kaynak bağlama](/rest/api/resources/resourcelinks).

## <a name="child-resources"></a>Alt kaynakları
Merhaba kaynaklar özellik tanımlanmakta ilgili toohello kaynaktır toospecify alt kaynakları sağlar. Alt kaynakları yalnızca tanımlı beş düzey derinliğinde olabilir. Alt kaynağı ve hello üst kaynağı arasında örtük bir bağımlılığa sahip değilse toonote oluşturulan önemlidir. Alt kaynak toobe hello üst kaynak sonra dağıtılan hello varsa, bu bağımlılık hello dependsOn özelliğiyle açıkça belirtmelidir. 

Her bir üst kaynağın yalnızca belirli kaynak türleri alt kaynakları kabul eder. Merhaba kabul kaynak türleri hello belirtilen [şablon şeması](https://github.com/Azure/azure-resource-manager-schemas) hello üst kaynak. alt kaynak türünün Hello adını içeren hello üst kaynak türünün hello adı gibi **Microsoft.Web/sites/config** ve **Microsoft.Web/sites/extensions** hello ,herikialtkaynakları **Microsoft.Web/sites**.

SQL server ve SQL veritabanı aşağıdaki örneğine hello gösterir. Merhaba veritabanı hello sunucu alt olsa bile açık bağımlılığı hello SQL database ve SQL server arasında tanımlanır dikkat edin.

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
Merhaba [başvuru işlevi](resource-group-template-functions-resource.md#reference) diğer JSON ad ve değer çiftlerini veya çalışma zamanı kaynakları değerini bir deyim tooderive sağlar. Başvuru ifadeleri örtük olarak bir kaynak üzerinde başka bir bağlıdır bildirin. Merhaba genel biçimi şöyledir:

```json
reference('resourceName').propertyPath
```

Hello aşağıdaki örnek, bir CDN uç noktası açıkça CDN profili hello üzerinde bağlıdır ve örtük olarak bir web uygulamasında bağlıdır.

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

Bu öğe veya hello dependsOn öğesi toospecify bağımlılıkları kullanabilirsiniz, ancak Merhaba toouse hem gerekmez aynı bağımlı kaynak. Mümkün olduğunda, gereksiz bir bağımlılık ekleme dolaylı başvuru tooavoid kullanın.

toolearn daha, fazla [başvuru işlevi](resource-group-template-functions-resource.md#reference).

## <a name="recommendations-for-setting-dependencies"></a>Bağımlılıklarını ayarlama önerileri

Hangi bağımlılıkları tooset karar verirken, yönergeleri izleyerek hello kullan:

* Mümkün olduğunca az bağımlılıkları ayarlayın.
* Bir alt kaynak kendi üst kaynağına bağımlı olarak ayarlayın.
* Kullanım hello **başvuru** işlev tooshare bir özellik gereken kaynaklar arasındaki tooset örtük bağımlılıkları. Açık bir bağımlılık eklemeyin (**dependsOn**) ne zaman önceden tanımladığınız dolaylı bir bağımlılığı. Bu yaklaşım, gereksiz bağımlılıklara sahip olmanın hello riskini azaltır. 
* Bir kaynak bulunamadığında bir bağımlılık ayarlama **oluşturulan** başka bir kaynaktan işlevselliği olmadan. Merhaba kaynakları yalnızca dağıtımdan sonra etkileşimde, bir bağımlılık ayarlı değil.
* Açıkça ayarlamadan basamaklı bağımlılıkları olanak tanır. Örneğin, sanal makinenize bir sanal ağ arabiriminde bağlıdır ve hello sanal ağ arabirimi bir sanal ağ ve genel IP adreslerine bağlıdır. Bu nedenle, dağıtılan tüm üç kaynakları hello sanal makine bağlıdır, ancak açıkça hello sanal makinenin tüm üç kaynaklara bağlı olarak ayarlı değil. Bu yaklaşım hello bağımlılık sırası açıklar ve daha sonra daha kolay toochange hello şablon hale getirir.
* Dağıtım öncesinde bir değer belirlenebilir, bir bağımlılık olmadan hello kaynak dağıtmayı deneyin. Örneğin, bir yapılandırma değeri başka bir kaynağın hello adı gerekiyorsa, bir bağımlılık gerekmeyebilir. Bazı kaynaklar diğer kaynak hello hello varlığını doğrulamak için bu yönergeleri her zaman çalışmaz. Bir hata alırsanız, bir bağımlılık ekleyin. 

Resource Manager şablonu doğrulama sırasında döngüsel bağımlılıklar tanımlar. Döngüsel bağımlılık var olduğunu bildiren bir hata alırsanız, bağımlılıkları gerekmeyen ve Kaldırılabilir şablonu toosee değerlendirin. Bağımlılıklarını kaldırma çalışmazsa, bazı dağıtım işlemlerini hello döngüsel bağımlılık sahip hello kaynakları sonra dağıtılan alt kaynakları taşınmasını tarafından döngüsel bağımlılıklar önleyebilirsiniz. Örneğin, iki sanal makine dağıtıyorsanız ancak toohello diğer başvuran her birinin özelliklerini ayarlamalısınız varsayalım. Bunları sırasının hello dağıtabilirsiniz:

1. VM1
2. vm2
3. Vm1 uzantısı vm1 ve vm2 bağlıdır. Merhaba uzantısı vm2 alır vm1 değerlerini ayarlar.
4. Vm2 uzantısı vm1 ve vm2 bağlıdır. Merhaba uzantısı vm1 alır vm2 değerlerini ayarlar.

Merhaba dağıtım sırası değerlendirmek ve bağımlılık hataları çözümleme hakkında daha fazla bilgi için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).

## <a name="next-steps"></a>Sonraki adımlar
* Bağımlılıklar, dağıtım sırasında sorun giderme hakkında toolearn bkz [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).
* Azure Resource Manager şablonları oluşturma hakkında daha fazla toolearn bkz [şablonları yazma](resource-group-authoring-templates.md). 
* Bir şablona hello kullanılabilen işlevlerin listesi için bkz [şablon işlevleri](resource-group-template-functions.md).

