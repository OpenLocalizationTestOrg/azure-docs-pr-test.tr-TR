---
title: "aaaAzure Resource Manager şablonu yapısı ve sözdizimi | Microsoft Docs"
description: "Merhaba yapısı ve bildirim temelli JSON sözdizimini kullanarak Azure Resource Manager şablonları özelliklerini açıklar."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a>Merhaba yapısı ve Azure Resource Manager şablonları sözdizimi anlama
Bu konu, bir Azure Resource Manager şablonu hello yapısını açıklar. Bu bölümlerdeki kullanılabilir olan bir şablonu ve özelliklerinin hello hello farklı bölümleri gösterir. JSON ve dağıtımınız için tooconstruct değerleri kullanabileceğiniz ifadeler Hello şablonu oluşur. Şablon oluşturmanın adım adım öğretici için bkz [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md).

## <a name="template-format"></a>Şablon biçimi
Basit yapısını bir şablon hello aşağıdaki öğeleri içerir:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| Öğe adı | Gerekli | Açıklama |
|:--- |:--- |:--- |
| $schema |Evet |Merhaba şablon dili hello sürümü açıklanmaktadır hello JSON Şeması dosyasının konumu. Örnek önceki hello gösterilen hello URL kullanın. |
| contentVersion |Evet |Merhaba şablonu (örneğin, 1.0.0.0) sürümü. Bu öğe için herhangi bir değer sağlayabilir. Merhaba şablonu kullanarak kaynak dağıtırken, bu değer kullanılan toomake hello sağ şablon kullanıldığından emin olabilir. |
| parametreler |Hayır |Dağıtım olduğunda, sağlanan değerler toocustomize kaynak dağıtım yürütüldü. |
| değişkenleri |Hayır |JSON parçalanma hello şablonu toosimplify şablon dili ifadeleri olarak kullanılan değerler. |
| Kaynakları |Evet |Dağıtılan veya bir kaynak grubunda güncelleştirilmiş kaynak türleri. |
| Çıkışları |Hayır |Dağıtımdan sonra döndürülen değer. |

Her öğe ayarlayabileceğiniz özellikler içerir. Aşağıdaki örneğine hello hello bir şablon için tam söz dizimi içeriyor:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

Bu konunun ilerleyen bölümlerinde daha ayrıntılı hello şablon hello bölümlerini inceleyeceğiz.

## <a name="expressions-and-functions"></a>İfadeler ve işlevleri
Merhaba temel sözdizimi hello şablonunun JSON şeklindedir. Ancak, ifadeler ve işlevleri hello JSON değerleri hello şablonu içinde kullanılabilir genişletir.  İfadeler, ilk JSON dize değişmez değerleri içinde yazılır ve son karakterlerdir hello köşeli: `[` ve `]`sırasıyla. Merhaba şablon dağıtıldığında hello ifade hello değeri değerlendirilir. Bir dize yazılmış olsa da, hello ifade değerlendirme sonucunu hello gibi bir dizi veya tamsayı hello gerçek ifade bağlı olarak farklı bir JSON türde olabilir.  sabit değerli bir dize Başlat köşeli ayraç ile toohave `[`, ancak değil bir ifade olarak yorumlanır olması, fazladan ayraç toostart hello dizesiyle eklemek `[[`.

Genellikle, hello dağıtım yapılandırma işlevleri tooperform işlemleri içeren ifadeler kullanın. JavaScript'te, işlev çağrıları olarak biçimlendirilmiş gibi yalnızca `functionName(arg1,arg2,arg3)`. Özellikler hello nokta ve [dizin] işleçleri kullanarak başvuru.

örnekte gösterildiği nasıl birkaç işlevleri oluşturulurken toouse değerleri hello:

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

Merhaba tam şablon işlevlerin listesi için bkz: [Azure Resource Manager şablonu işlevleri](resource-group-template-functions.md). 

## <a name="parameters"></a>Parametreler
Merhaba Parametreler bölümünde hello şablonunun dağıtırken giriş hangi değerlerin kaynakları hello belirtin. Bu parametre değerleri (örneğin, geliştirme, test ve üretim) belirli bir ortam için uyarlanabilir değerleri sağlayarak toocustomize hello dağıtımını etkinleştirin. Şablonunuzda tooprovide parametrelere sahip değildir, ancak parametre olmadan şablonunuzu her zaman hello dağıtmak için kullanacağınız aynı kaynaklarla hello aynı adları, konumları ve özellikler.

Yapı izlenerek hello ile parametrelerini tanımlayın:

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| Öğe adı | Gerekli | Açıklama |
|:--- |:--- |:--- |
| parameterName |Evet |Merhaba parametresinin adı. Geçerli bir JavaScript tanımlayıcı olması gerekir. |
| type |Evet |Merhaba parametre değeri türü. İzin verilen türleri Hello listesi sonra bu tabloya bakın. |
| defaultValue |Hayır |Merhaba parametresi için hiçbir değer sağlanmazsa hello parametresinin varsayılan değeri. |
| allowedValues |Hayır |Merhaba parametresi toomake hello sağ değer sağlandığından emin izin verilen değerleri dizisi. |
| MinValue |Hayır |Merhaba int türü parametreler için minimum değeri, bu kapsayıcı değerdir. |
| MaxValue |Hayır |Merhaba int türü parametreleri için en büyük değer, bu kapsayıcı değerdir. |
| minLength |Hayır |Merhaba dize, secureString ve dizi türü parametreler için minimum uzunluk, bu kapsayıcı değerdir. |
| maxLength |Hayır |Merhaba dize, secureString ve dizi türü parametreleri için en fazla uzunluk, bu kapsayıcı değerdir. |
| açıklama |Hayır |Olan hello parametre açıklaması hello portal üzerinden toousers görüntülenir. |

Merhaba izin verilen türleri ve değerleri şunlardır:

* **dize**
* **secureString**
* **int**
* **bool**
* **Nesne** 
* **secureObject**
* **dizi**

toospecify parametre isteğe bağlı olarak (boş bir dize olabilir) bir defaultValue sağlar. 

Şablonunuzdaki hello komutu toodeploy hello şablonu içindeki bir parametre ile eşleşen bir parametre adı belirtirseniz, olası karışıklığı sağladığınız hello değerleri hakkında yoktur. Resource Manager hello sonek ekleyerek bu karışıklığı çözümler **FromTemplate** toohello şablon parametresi. Örneğin, adlı bir parametre dahil ederseniz **ResourceGroupName** isteğe bağlı olarak, şablonunuzda hello ile çakışıyor **ResourceGroupName** hello parametresinde [ Yeni-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet'i. Dağıtım sırasında istendiğinde tooprovide için bir değer olduğunuz **ResourceGroupNameFromTemplate**. Genel olarak, aynı dağıtım işlemleri için kullanılan parametreler olarak ad hello parametrelerle adlandırılmasıyla değil Bu Karışıklığı önlemek.

> [!NOTE]
> Tüm parolalar, anahtarlar ve diğer parolaları hello kullanması gereken **secureString** türü. Bir JSON nesnesinde hassas verileri geçirirseniz, hello kullan **secureObject** türü. Şablon parametreleri secureString veya secureObject türleriyle kaynak dağıtımdan sonra okunamıyor. 
> 
> Örneğin, hello hello dağıtım geçmişi dosyasında şu girişi hello değeri bir dize ve nesne için kullanılabilir ancak secureString ve secureObject gösterir.
>
> ![Dağıtım değerlerini göster](./media/resource-group-authoring-templates/show-parameters.png)  
>

örnekte gösterildiği nasıl aşağıdaki hello toodefine Parametreler:

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

Tooinput hello parametre dağıtım sırasında nasıl değerleri için bkz: [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md). 

## <a name="variables"></a>Değişkenler
Merhaba değişkenler bölümünde şablonunuzu kullanılabilir değerleri oluşturun. Toodefine değişkenleri gerekmez, ancak bunlar karmaşık ifadeler azaltarak genellikle şablonunuzu basitleştirin.

Yapı izlenerek hello ile değişkenleri tanımlayın:

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

örnekte gösterildiği nasıl aşağıdaki hello toodefine iki parametre değerlerinin oluşturulan bir değişkeni:

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

Merhaba sonraki örnek karmaşık bir JSON türe sahip bir değişken ve diğer değişkenlerinden oluşturulan değişkenleri gösterir:

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a>Kaynaklar
Merhaba kaynaklar bölümünde dağıtılan veya güncelleştirilen hello kaynakları tanımlayın. Merhaba türlerini anlamanız gerekir çünkü bu bölümde karmaşık alabilirsiniz tooprovide hello doğru değerleri dağıtma. Tooset gereken hello kaynak özgü değerlerini (apiVersion, türü ve özellikleri), görmek [kaynakları tanımlayan Azure Resource Manager şablonları](/azure/templates/). 

Yapı izlenerek hello ile kaynakları tanımlayın:

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| Öğe adı | Gerekli | Açıklama |
|:--- |:--- |:--- |
| Koşul | Hayır | Merhaba kaynak dağıtılabilir olup olmadığını gösteren Boole değeri. |
| apiVersion |Evet |Merhaba kaynak oluşturmak için REST API toouse hello sürümü. |
| type |Evet |Merhaba kaynak türü. Bu değer hello kaynak sağlayıcısı ve hello kaynak türü hello ad birleşimidir (gibi **Microsoft.Storage/storageAccounts**). |
| ad |Evet |Merhaba kaynağın adı. Merhaba adı RFC3986 içinde tanımlanan URI bileşeni kısıtlamaları izlemeniz gerekir. Ayrıca, hello kaynak adı toooutside tarafların kullanıma Azure Hizmetleri hello adı toomake girişimi toospoof olmadığından emin doğrula başka bir kimlik. |
| location |Değişir |Merhaba, desteklenen coğrafi konumda kaynak sağlanır. Merhaba kullanılabilir konumlardan herhangi birinden seçebilirsiniz, ancak genellikle algılama toopick Kapat tooyour kullanıcıları olan bir kolaylaştırır. Genellikle, ayrıca hello aynı birbiriyle etkileşimde tooplace kaynakları mantıklıdır bölgesi. Çoğu kaynak türleri bir konum gerektirir, ancak bazı türleri (örneğin, bir rol ataması) bir konum gerektirmez. Bkz: [Azure Resource Manager şablonları kaynak konumunu ayarla](resource-manager-template-location.md). |
| etiketler |Hayır |Merhaba kaynakla ilişkilendirilmiş etiketler. Bkz: [Azure Resource Manager'da kaynakları etiketi](resource-manager-template-tags.md). |
| Açıklamaları |Hayır |Şablonunuzda hello kaynakları belgeleme için notları |
| Kopyalama |Hayır |Birden fazla örneği gerekiyorsa, kaynakları toocreate sayısı hello. Merhaba varsayılan paralel moddur. Değil tüm veya istediğinizde hello hello adresindeki kaynakları toodeploy seri modunu belirtin aynı anda. Daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md). |
| dependsOn |Hayır |Bu kaynak dağıtılmadan önce dağıtılmalıdır kaynaklar. Resource Manager kaynakları arasındaki hello bağımlılıkları değerlendirir ve hello doğru sırayla dağıtır. Kaynakları birbirlerine bağımlı olmadıkları zaman bunların paralel olarak dağıtılır. Merhaba değeri olan bir kaynağın virgülle ayrılmış bir liste olabilir adları veya kaynak benzersiz tanımlayıcıları. Yalnızca bu şablonda dağıtılan kaynakları listeler. Bu şablonda tanımlı değil kaynakları önceden var olmalıdır. Dağıtımınızı yavaş ve döngüsel bağımlılıklar oluşturma gibi gereksiz bağımlılıkları eklemekten kaçının. Bağımlılıklarını ayarlama hakkında yönergeler için bkz [Azure Resource Manager'da bağımlılıkları tanımlama](resource-group-define-dependencies.md). |
| properties |Hayır |Kaynak özgü yapılandırma ayarları. Merhaba özelliklerinin Hello değerlerini olduğunuz hello aynı hello istek gövdesinde hello REST API işlemi (PUT yöntemini) toocreate hello kaynağı için sağladığınız hello değerleri olarak. Kopya dizi toocreate bir özelliği birden çok örneğini de belirtebilirsiniz. Daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md). |
| Kaynakları |Hayır |Tanımlanan hello kaynağına bağımlı alt kaynakları. Yalnızca hello üst kaynak hello şema tarafından izin verilen kaynak türleri sağlar. Merhaba hello alt kaynağının tam olarak nitelenmiş tür hello üst kaynak türü, gibi içerir **Microsoft.Web/sites/extensions**. Merhaba üst Kaynak bağımlılığı kullanılmaz. Bu bağımlılık açıkça tanımlamanız gerekir. |

Merhaba kaynaklar bölümünde hello kaynakları toodeploy dizisi içerir. Her kaynak içinde bir dizi alt kaynakları da tanımlayabilirsiniz. Bu nedenle, kaynakları bölümünüzü gibi bir yapıya sahip:

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

Alt kaynakları tanımlama hakkında daha fazla bilgi için bkz: [Resource Manager şablonunda alt kaynak için ad ve tür ayarlamak](resource-manager-template-child-resource.md).

Merhaba **koşulu** öğesi hello kaynak dağıtılabilir olup olmadığını belirtir. Bu öğe için başlangıç değerini tootrue ya da yanlış çözümler. Örneğin, yeni bir depolama hesabı dağıtmış olup olmadığını toospecify kullanın:

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

Yeni veya mevcut bir kaynağı kullanarak bir örnek için bkz: [yeni veya varolan bir koşul şablonu](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).

toospecify bir parola veya SSH anahtarı, bir sanal makinenin dağıtıldığı olup olmadığını tanımlayın iki sürümü hello sanal makine, şablon ve kullanım **koşulu** toodifferentiate kullanımı. Hangi senaryo toodeploy belirten bir parametre geçirin.

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

Bir parola veya SSH anahtar toodeploy sanal makine kullanarak bir örnek için bkz: [kullanıcı adı veya SSH koşul şablon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="outputs"></a>Çıkışları
Merhaba çıkışları bölümünde dağıtımından döndürülen değerlerini belirtin. Örneğin, dağıtılmış bir kaynak hello URI tooaccess döndürebilirsiniz.

Merhaba aşağıdaki örnek bir çıktı tanımının hello yapısını gösterir:

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| Öğe adı | Gerekli | Açıklama |
|:--- |:--- |:--- |
| outputName |Evet |Merhaba çıkış değeri adı. Geçerli bir JavaScript tanımlayıcı olması gerekir. |
| type |Evet |Merhaba çıkış değerini yazın. Çıkış değerleri aynı şablon giriş parametreleri olarak türleri hello destekler. |
| değer |Evet |Hesaplanan ve çıktı değeri olarak döndürülen şablon dili ifadesi. |

Merhaba aşağıdaki örnek hello çıkışları bölümünde döndürülen bir değer gösterir.

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

Çıktı ile çalışma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları durumda paylaşımı](best-practices-resource-manager-state.md).

## <a name="template-limits"></a>Şablon sınırları

Merhaba boyut sınırı, şablon too1 MB ve her bir parametreyi too64 KB dosya. yinelemeli Kaynak tanımları ve değişkenleri ve parametreleri için değerler ile genişletilmiştir sonra hello 1 MB sınırını toohello son durum hello şablonunun uygulanır. 

Ayrıca için sınırlıdır:

* 256 parametreleri
* 256 değişkenleri
* 800 kaynakları (kopya sayısı dahil)
* 64 çıkış değerleri
* bir şablon ifadesinde 24.576 karakterleri

İç içe geçmiş bir şablon kullanarak bazı şablonu sınırı aşabilir. Daha fazla bilgi için bkz: [Azure kaynaklarını dağıtırken bağlı şablonları kullanma](resource-group-linked-templates.md). tooreduce hello numarası parametreleri, değişkenleri veya çıkışları, değerlerden bir nesnesinde birleştirebilirsiniz. Daha fazla bilgi için bkz: [nesneleri parametreleri olarak](resource-manager-objects-as-parameters.md).

## <a name="next-steps"></a>Sonraki adımlar
* tooview tam şablonları farklı türlerde çözümler için bkz: hello [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/).
* Kullanabileceğiniz gelen bir şablonda hello işlevleri hakkında daha fazla ayrıntı için bkz: [Azure Resource Manager şablonu işlevleri](resource-group-template-functions.md).
* dağıtım işlemi sırasında birden fazla şablon toocombine bkz [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).
* Farklı bir kaynak grubu içinde mevcut toouse kaynakları gerekebilir. Bu senaryo, depolama hesapları veya birden çok kaynak grupları arasında paylaşılan sanal ağlar ile çalışırken yaygındır. Daha fazla bilgi için bkz: Merhaba [ResourceId işlevi](resource-group-template-functions-resource.md#resourceid).
