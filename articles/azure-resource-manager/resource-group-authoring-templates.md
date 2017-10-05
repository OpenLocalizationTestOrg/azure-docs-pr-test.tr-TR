---
title: "Azure Resource Manager şablonu yapısı ve sözdizimi | Microsoft Docs"
description: "Yapı ve bildirim temelli JSON sözdizimini kullanarak Azure Resource Manager şablonları özelliklerini açıklar."
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
ms.openlocfilehash: dc9b64062d7f68c83aa090eec96744819a5ca423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-the-structure-and-syntax-of-azure-resource-manager-templates"></a>Yapı ve Azure Resource Manager şablonları sözdizimi anlama
Bu konu, bir Azure Resource Manager şablonu yapısını açıklar. Bir şablon ve bu bölümlerdeki özellikler farklı bölümlerini gösterir. JSON ve dağıtımınız için değerleri oluşturmada kullanabileceğiniz ifadeler, şablon oluşur. Şablon oluşturmanın adım adım öğretici için bkz [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md).

## <a name="template-format"></a>Şablon biçimi
En basit yapısını şablon aşağıdaki öğeleri içerir:

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
| $schema |Evet |Şablon dili sürümü açıklanmaktadır JSON Şeması dosyasının konumu. Önceki örnekte gösterilen URL'yi kullanın. |
| contentVersion |Evet |Şablon (örneğin, 1.0.0.0) sürümü. Bu öğe için herhangi bir değer sağlayabilir. Şablonu kullanarak kaynak dağıtırken, bu değer doğru şablonu kullanılmakta olduğunu emin olmak için kullanılabilir. |
| Parametreleri |Hayır |Dağıtım kaynağı dağıtım özelleştirmek için yürütüldüğünde, sağlanan değerler. |
| değişkenleri |Hayır |Şablondaki JSON parçaları olarak şablon dili ifadeleri basitleştirmek için kullanılan değerler. |
| Kaynakları |Evet |Dağıtılan veya bir kaynak grubunda güncelleştirilmiş kaynak türleri. |
| Çıkışları |Hayır |Dağıtımdan sonra döndürülen değer. |

Her öğe ayarlayabileceğiniz özellikler içerir. Aşağıdaki örnek, bir şablon için tam söz dizimi içerir:

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
                "description": "<description-of-the parameter>" 
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

Bu konunun ilerleyen bölümlerinde daha ayrıntılı şablon bölümlerini inceleyeceğiz.

## <a name="expressions-and-functions"></a>İfadeler ve işlevleri
Şablonun temel sözdizimi JSON şeklindedir. Ancak, ifadeler ve işlevleri şablonu içinde kullanılabilir olan JSON değerlerin genişletir.  İfadeler, ilk JSON dize değişmez değerleri içinde yazılır ve son karakterler olan ayraçlar: `[` ve `]`sırasıyla. Şablon dağıtıldığında ifade değeri değerlendirilir. Bir dize yazılmış olsa da, ifade değerlendirme sonucu gibi bir dizi veya tamsayı, gerçek ifade bağlı olarak farklı bir JSON türde olabilir.  Başlangıç noktası ile sabit değerli bir dize olması `[`, ancak olmayan bir ifade olarak yorumlanır olması, dizesiyle başlatmak için ek bir köşeli ayraç eklemek `[[`.

Genellikle, ifadeler işlevleriyle dağıtım yapılandırma işlemleri gerçekleştirmek için kullanın. JavaScript'te, işlev çağrıları olarak biçimlendirilmiş gibi yalnızca `functionName(arg1,arg2,arg3)`. Nokta ve [dizin] işleçleri kullanarak özellikleri başvuru.

Aşağıdaki örnek değerleri oluşturulurken, çeşitli işlevleri kullanmayı gösterir:

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

Şablon işlevleri tam listesi için bkz: [Azure Resource Manager şablonu işlevleri](resource-group-template-functions.md). 

## <a name="parameters"></a>Parametreler
Şablon parametreleri bölümünde kaynakları dağıtırken giriş hangi değerlerini belirtin. Bu parametre değerleri (örneğin, geliştirme, test ve üretim) belirli bir ortam için uyarlanabilir değerleri sağlayarak dağıtım özelleştirmenize olanak sağlar. Şablonunuzdaki parametreleri sağlamak zorunda değildir, ancak parametre olmadan şablonunuzu her zaman aynı kaynakları adları, konumları ve özellikleri ile dağıtmak için kullanacağınız.

Şu yapıda parametrelerini tanımlayın:

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
            "description": "<description-of-the parameter>" 
        }
    }
}
```

| Öğe adı | Gerekli | Açıklama |
|:--- |:--- |:--- |
| parameterName |Evet |Parametrenin adı. Geçerli bir JavaScript tanımlayıcı olması gerekir. |
| type |Evet |Parametre değeri türü. İzin verilen türleri listesini sonra bu tabloya bakın. |
| defaultValue |Hayır |Parametresi için hiçbir değer sağlanmazsa parametre için varsayılan değer. |
| allowedValues |Hayır |Doğru değeri sağlandığından emin olmak parametresi için izin verilen değerleri dizisi. |
| MinValue |Hayır |İnt türü parametreler için minimum değeri, bu kapsayıcı değerdir. |
| MaxValue |Hayır |İnt türü parametreleri için maksimum değeri, bu kapsayıcı değerdir. |
| minLength |Hayır |Dize, secureString ve dizi türü parametreler için minimum uzunluk, bu kapsayıcı değerdir. |
| maxLength |Hayır |Dize, secureString ve dizi türü parametreleri için en fazla uzunluk, bu kapsayıcı değerdir. |
| Açıklama |Hayır |Portal aracılığıyla kullanıcılara görüntülenen parametre açıklaması. |

İzin verilen türleri ve değerleri şunlardır:

* **dize**
* **secureString**
* **int**
* **bool**
* **Nesne** 
* **secureObject**
* **dizi**

Parametre isteğe bağlı olarak belirtmek için (boş bir dize olabilir) bir defaultValue sağlayın. 

Şablonunuzdaki şablonu dağıtmak için komut bir parametre ile eşleşen bir parametre adı belirtirseniz, olası karışıklığı sağladığınız değerleri hakkında yoktur. Resource Manager sonek ekleyerek bu karışıklığı çözümler **FromTemplate** şablon parametresi için. Örneğin, adlı bir parametre dahil ederseniz **ResourceGroupName** ile çakıştığı şablonunuzda, **ResourceGroupName** parametresinde [New-AzureRmResourceGroupDeployment ](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet'i. Dağıtım sırasında için bir değer sağlamanız istenir **ResourceGroupNameFromTemplate**. Genel olarak, Karışıklığı önlemek için bu parametreleri dağıtım işlemleri için kullanılan parametreleri aynı ada sahip adlandırılmasıyla değil kaçınmalısınız.

> [!NOTE]
> Tüm parolalar, anahtarlar ve diğer parolaları kullanması gereken **secureString** türü. Bir JSON nesnesinde hassas verileri geçirdiğiniz kullanırsanız **secureObject** türü. Şablon parametreleri secureString veya secureObject türleriyle kaynak dağıtımdan sonra okunamıyor. 
> 
> Örneğin, dağıtım geçmişi dosyasında şu girişi değeri bir dize ve nesne için kullanılabilir ancak secureString ve secureObject gösterir.
>
> ![Dağıtım değerlerini göster](./media/resource-group-authoring-templates/show-parameters.png)  
>

Aşağıdaki örnek, parametreleri tanımlayan gösterilmektedir:

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

Dağıtım sırasında parametre değerlerini giriş nasıl için [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md). 

## <a name="variables"></a>Değişkenler
Değişkenler bölümünde şablonunuzu kullanılabilir değerleri oluşturun. Değişkenleri tanımlayın gerekmez, ancak bunlar karmaşık ifadeler azaltarak genellikle şablonunuzu basitleştirin.

Şu yapıda değişkenleri tanımlayın:

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

Aşağıdaki örnekte, iki parametre değerlerinin oluşturulan bir değişkeni tanımlamak gösterilmektedir:

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

Sonraki örnek karmaşık bir JSON türe sahip bir değişken ve diğer değişkenlerinden oluşturulan değişkenleri gösterir:

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
Kaynaklar bölümünde dağıtılan veya güncelleştirilen kaynakları tanımlayın. Sağ değerlerini sağlamak için dağıtıyorsanız türlerini anlamanız gerekir çünkü bu bölümde karmaşık elde edebilirsiniz. Ayarlamak için gereken kaynak özgü değerleri için (apiVersion, türü ve özellikleri), bkz: [kaynakları tanımlayan Azure Resource Manager şablonları](/azure/templates/). 

Aşağıdaki Yapı kaynaklarını tanımlayın:

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
| Koşul | Hayır | Kaynak dağıtılabilir olup olmadığını gösteren Boole değeri. |
| apiVersion |Evet |Kaynak oluşturmak için kullanmak için REST API sürümü. |
| type |Evet |Kaynak türü. Bu değer, kaynak sağlayıcısı ve kaynak türü ad birleşimidir (gibi **Microsoft.Storage/storageAccounts**). |
| ad |Evet |Kaynağın adı. Ad RFC3986 içinde tanımlanan URI bileşeni kısıtlamaları izlemelidir. Ayrıca, emin olmak için adı dışında tarafların doğrulamak için kaynak adı kullanıma Azure Hizmetleri değil başka bir kimlik aldatma girişimi. |
| location |Değişir |Sağlanan kaynak coğrafi konumda desteklenmiyor. Kullanılabilir konumlardan herhangi birinden seçebilirsiniz, ancak genellikle kullanıcılarınızın yakın olan bir seçmek için mantıklıdır. Genellikle, bu da aynı bölgede birbiriyle etkileşimde kaynakları yerleştirin mantıklıdır. Çoğu kaynak türleri bir konum gerektirir, ancak bazı türleri (örneğin, bir rol ataması) bir konum gerektirmez. Bkz: [Azure Resource Manager şablonları kaynak konumunu ayarla](resource-manager-template-location.md). |
| etiketler |Hayır |Kaynakla ilişkilendirilmiş etiketler. Bkz: [Azure Resource Manager'da kaynakları etiketi](resource-manager-template-tags.md). |
| Açıklamaları |Hayır |Şablonunuzda kaynaklar belgeleme için notları |
| Kopyalama |Hayır |Birden fazla örneği gerekirse oluşturmak için kaynak sayısı. Paralel varsayılan moddur. Tüm kullanmak istemiyorsanız, seri modu veya aynı anda dağıtmak amacıyla kaynaklarınızı belirtin. Daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md). |
| dependsOn |Hayır |Bu kaynak dağıtılmadan önce dağıtılmalıdır kaynaklar. Resource Manager kaynakları arasındaki bağımlılıkları değerlendirir ve doğru sırada dağıtır. Kaynakları birbirlerine bağımlı olmadıkları zaman bunların paralel olarak dağıtılır. Değer bir kaynağın virgülle ayrılmış bir liste olabilir adları veya kaynak benzersiz tanımlayıcıları. Yalnızca bu şablonda dağıtılan kaynakları listeler. Bu şablonda tanımlı değil kaynakları önceden var olmalıdır. Dağıtımınızı yavaş ve döngüsel bağımlılıklar oluşturma gibi gereksiz bağımlılıkları eklemekten kaçının. Bağımlılıklarını ayarlama hakkında yönergeler için bkz [Azure Resource Manager'da bağımlılıkları tanımlama](resource-group-define-dependencies.md). |
| properties |Hayır |Kaynak özgü yapılandırma ayarları. Özelliklerine ilişkin değerleri kaynak oluşturmak REST API işlemi için (PUT yöntemini) istek gövdesinde sağladığınız değerleri ile aynıdır. Ayrıca bir özelliği birden çok örneğini oluşturmak için bir kopya dizisi belirtebilirsiniz. Daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md). |
| Kaynakları |Hayır |Tanımlanan kaynağına bağımlı alt kaynakları. Yalnızca üst kaynak şema tarafından izin verilen kaynak türleri sağlar. Tam olarak nitelenmiş tür alt kaynağının üst kaynak türü gibi içerir **Microsoft.Web/sites/extensions**. Üst Kaynak bağımlılığı kullanılmaz. Bu bağımlılık açıkça tanımlamanız gerekir. |

Kaynaklar bölümünde dağıtmak amacıyla kaynaklarınızı dizisi içerir. Her kaynak içinde bir dizi alt kaynakları da tanımlayabilirsiniz. Bu nedenle, kaynakları bölümünüzü gibi bir yapıya sahip:

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

**Koşulu** öğesi kaynak dağıtılabilir olup olmadığını belirtir. Bu öğe için değer true veya false değerine çözümler. Örneğin, yeni bir depolama hesabı dağıtılabilir olup olmadığını belirtmek için kullanın:

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

Bir sanal makine bir parola veya SSH anahtarı ile birlikte dağıtılabilir olup olmadığını belirlemek için iki sürümünü sanal makine, şablon ve kullanım tanımlama **koşulu** kullanım ayırt etmek için. Dağıtmak için hangi senaryonun belirten bir parametre geçirin.

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

Sanal makineyi dağıtmak için bir parola veya SSH anahtarı kullanarak bir örnek için bkz: [kullanıcı adı veya SSH koşul şablon](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="outputs"></a>Çıkışları
Çıkış bölümünde dağıtımından döndürülen değerlerini belirtin. Örneğin, dağıtılan bir kaynağa erişmek için URI döndürebilirsiniz.

Aşağıdaki örnek bir çıktı tanımının yapısını gösterir:

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
| outputName |Evet |Çıkış değeri adı. Geçerli bir JavaScript tanımlayıcı olması gerekir. |
| type |Evet |Çıktı değerin türü. Şablon giriş parametreleri aynı türlerine çıkış değerlerini destekler. |
| değer |Evet |Hesaplanan ve çıktı değeri olarak döndürülen şablon dili ifadesi. |

Aşağıdaki örnek çıkış bölümünde döndürülen bir değer gösterir.

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

Şablonunuzu 1 MB ve her parametre dosyası 64 KB boyutu sınırı. Yinelemeli Kaynak tanımları ve değişkenleri ve parametreleri için değerler ile genişletilmiştir sonra 1 MB sınırını şablonunun son durumuna uygulanır. 

Ayrıca için sınırlıdır:

* 256 parametreleri
* 256 değişkenleri
* 800 kaynakları (kopya sayısı dahil)
* 64 çıkış değerleri
* bir şablon ifadesinde 24.576 karakterleri

İç içe geçmiş bir şablon kullanarak bazı şablonu sınırı aşabilir. Daha fazla bilgi için bkz: [Azure kaynaklarını dağıtırken bağlı şablonları kullanma](resource-group-linked-templates.md). Parametreler, değişkenleri veya çıkışları sayısını azaltmak için değerlerden bir nesnede birleştirebilirsiniz. Daha fazla bilgi için bkz: [nesneleri parametreleri olarak](resource-manager-objects-as-parameters.md).

## <a name="next-steps"></a>Sonraki adımlar
* Farklı türlerde çözümler için tam şablonları görüntülemek üzere bkz. [Azure Hızlı Başlangıç Şablonları](https://azure.microsoft.com/documentation/templates/).
* Kullanabileceğiniz gelen bir şablonda işlevleri hakkında daha fazla ayrıntı için bkz: [Azure Resource Manager şablonu işlevleri](resource-group-template-functions.md).
* Birden fazla şablon dağıtımı sırasında birleştirmek için bkz: [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).
* Farklı bir kaynak grubu içinde mevcut kaynakları kullanmanız gerekebilir. Bu senaryo, depolama hesapları veya birden çok kaynak grupları arasında paylaşılan sanal ağlar ile çalışırken yaygındır. Daha fazla bilgi için bkz: [ResourceId işlevi](resource-group-template-functions-resource.md#resourceid).
