---
title: "aaaTroubleshoot ortak Azure dağıtım hataları | Microsoft Docs"
description: "Açıklar nasıl kaynakları tooAzure Azure Kaynak Yöneticisi'ni kullanarak dağıttığınızda tooresolve sık karşılaşılan hatalar."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Dağıtım hatası, azure dağıtım tooazure dağıtma"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>Ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme
Bu konu, bazı ortak nasıl çözebilirsiniz açıklar karşılaşabileceğiniz Azure dağıtım hataları.

hata kodları aşağıdaki hello bu konuda açıklanan:

* [AccountNameInvalid](#accountnameinvalid)
* [Yetkilendirme başarısız oldu](#authorization-failed)
* [BadRequest](#badrequest)
* [DeploymentFailed](#deploymentfailed)
* [DisallowedOperation](#disallowedoperation)
* [InvalidContentLink](#invalidcontentlink)
* [InvalidTemplate](#invalidtemplate)
* [MissingSubscriptionRegistration](#noregisteredproviderfound)
* [NotFound](#notfound)
* [NoRegisteredProviderFound](#noregisteredproviderfound)
* [OperationNotAllowed](#quotaexceeded)
* [ParentResourceNotFound](#parentresourcenotfound)
* [QuotaExceeded](#quotaexceeded)
* [RequestDisallowedByPolicy](#requestdisallowedbypolicy)
* [ResourceNotFound](#notfound)
* [SkuNotAvailable](#skunotavailable)
* [StorageAccountAlreadyExists](#storagenamenotunique)
* [StorageAccountAlreadyTaken](#storagenamenotunique)

## <a name="deploymentfailed"></a>DeploymentFailed

Bu hata kodu genel dağıtım hatası gösterir, ancak toostart sorun giderme ihtiyacınız hello hata kodu değil. gerçekte hello sorunu gidermenize yardımcı olacak hello hata genellikle bir düzey altında bu hata kodudur. Örneğin, hello aşağıdaki görüntüde hello gösterir **RequestDisallowedByPolicy** hello dağıtım hata altında hata kodu.

![Hata Kodu Göster](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a>SkuNotAvailable

Bir kaynak (genellikle bir sanal makine) dağıtırken hello aşağıdaki hata kodu ve hata iletisini alabilirsiniz:

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

Hello kaynak (VM boyutu gibi) seçtiniz SKU seçmiş olduğunuz hello konum için kullanılabilir değilse, bu hatayı alırsınız. tooresolve Bu sorun bir bölgede kullanılabilir SKU'lar toodetermine gerekir. PowerShell, hello portalı veya REST işlemi toofind kullanabileceğiniz kullanılabilir SKU'ları.

- İçin PowerShell kullanın [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) ve konuma göre filtre. Merhaba PowerShell'in en son sürümünü bu komutun olması gerekir.

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  Merhaba sonuçları SKU'ları listesi hello konumu için ve SKU yönelik kısıtlamaları içerir.

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- toouse hello [portal](https://portal.azure.com), toohello Portalı'nda oturum açın ve hello arabirimi aracılığıyla bir kaynak ekleyin. Merhaba değerleri ayarlamak hello görmeniz kaynağı için kullanılabilir SKU'lar. Toocomplete hello dağıtım gerekli değildir.

    ![kullanılabilir SKU'lar](./media/resource-manager-common-deployment-errors/view-sku.png)

- sanal makineler için toouse hello REST API isteği aşağıdaki hello gönder:

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  Kullanılabilir SKU'ları ve bölgeler biçimini izleyen hello döndürür:

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

Yüklenemiyor toofind bu bölge veya iş gereksinimlerinize uygun bir alternatif bölgede uygun bir SKU varsa, gönderme bir [SKU isteği](https://aka.ms/skurestriction) tooAzure desteği.

## <a name="disallowedoperation"></a>DisallowedOperation

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

Bu hata alırsanız, kullanmakta olduğunuz değil bir abonelik Azure Active Directory dışındaki herhangi bir Azure hizmeti tooaccess izin verilir. Tooaccess hello Klasik portal gerekir, ancak toodeploy kaynakları izin verilmiyor durumlarda bu tür aboneliği olabilir. tooresolve bu sorunu izni toodeploy kaynaklara sahip bir abonelik kullanmanız gerekir.  

tooview kullanılabilir aboneliklerinizi PowerShell ile kullanın:

```powershell
Get-AzureRmSubscription
```

Ve tooset hello geçerli abonelik, kullanın:

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

tooview kullanılabilir aboneliklerinizi Azure CLI 2.0 ile birlikte kullanın:

```azurecli
az account list
```

Ve tooset hello geçerli abonelik, kullanın:

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a>InvalidTemplate
Bu hata, birkaç farklı türlerinden hataları neden olabilir.

- Sözdizimi hatası

   Merhaba başarısız şablonu doğrulama bildiren bir hata iletisi alırsanız, şablonunuzun söz dizimi sorunu olabilir.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   Bu hata kolay toomake çünkü şablon ifadeleri karmaşık olabilir. Örneğin, hello aşağıdaki ad ataması bir depolama hesabı için bir dizi köşeli ayraçlar, üç işlevi, parantez üç kümesi, tek tırnaklı bir dizi ve bir özellik içerir:

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   Merhaba eşleştirme sözdizimi sağlamazsanız hello şablon amacınız farklı bir değer oluşturur.

   Bu tür hatalara aldığınızda, hello ifade sözdizimini dikkatle gözden geçirin. Bir JSON Düzenleyicisi gibi kullanmayı [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) veya [Visual Studio Code](resource-manager-vs-code.md), hangi uyar, söz dizimi hataları hakkında.

- Yanlış segment uzunluklarına

   Merhaba kaynak adı hello doğru biçimde değil başka bir geçersiz şablon hata oluşur.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   Kök düzeyinde kaynak daha az bir kesim hello adından hello kaynak türünde olması gerekir. Her segmentinde bir eğik çizgiyle Ayrıştırılan. Aşağıdaki örneğine hello hello türü iki bölümü vardır ve hello ada sahip bir segment, dolayısıyla bir **geçerli ad**.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   Ancak hello sonraki örnek **geçerli bir ad değil** hello sahip olduğu aynı sayıda hello türü kesimleri.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   Alt kaynakları için hello hello türü ve ada sahip aynı sayıda kesimleri. Hello üst ad ve tür Hello tam adı ve hello alt türü içerdiği için bu segment sayısına mantıklıdır. Bu nedenle, hello tam adı hala hello tam türünü daha küçük bir kesim içeriyor.

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   Alma hello kesimleri doğru kaynak sağlayıcıları uygulanan Resource Manager türleriyle zor olabilir. Örneğin, bir kaynak kilit tooa web sitesi uygulama dört kesimine sahip bir türü gerektirir. Bu nedenle, üç kesimleri hello adıdır:

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- Kopya dizini beklenmiyor

   Bu karşılaştığınız **InvalidTemplate** hello uygulandığında hata **kopyalama** öğesi tooa bu öğe desteklemiyor hello şablonunun parçası. Merhaba kopyalama öğesi tooa kaynak türü yalnızca uygulayabilirsiniz. İçinde bir kaynak türü kopya tooa özelliği uygulanamıyor. Örneğin, kopyalama tooa sanal makine geçerli, ancak bir sanal makine için işletim sistemi toohello diskleri uygulanamıyor. Bazı durumlarda, bir alt kaynak tooa üst kaynak toocreate kopyalama döngüsü dönüştürebilirsiniz. Kopya kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).

- Parametre geçerli değil

   Bir parametre için izin verilen değerler Hello şablonu belirtir ve bu değerlerden biri olmayan bir değer sağlayın, aşağıdaki hata iletisini benzer toohello alırsınız:

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   Çift onay hello hello şablonunda izin verilen değerler ve dağıtımı sırasında sağlayın.

- Döngüsel bağımlılık algılandı

   Birbirine bağımlı kaynakları hello dağıtım başlatılmasını engelleyen bir şekilde, bu hatayı alırsınız. Ayrıca bekleyen için diğer kaynaklar bekleyin iki veya daha fazla kaynak bağımlılıklarını bileşimini yapar. Örneğin, üzerinde resource3 resource1 bağlıdır, üzerinde resource1 switch2 bağlıdır ve üzerinde switch2 resource3 bağlıdır. Genellikle, gereksiz bağımlılıkları kaldırarak bu sorunu çözebilirsiniz. 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a>NotFound ve ResourceNotFound
Şablonunuzu hello çözümlenemeyen kaynağın adını içerdiğinde, benzer bir hata alırsınız:

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

Merhaba şablon kaynağında eksik toodeploy hello çalışıyorsanız, tooadd bir bağımlılık gerekli olup olmadığını denetleyin. Resource Manager kaynakları paralel olarak, mümkün olduğunda oluşturarak dağıtım en iyi duruma getirir. Bir kaynak sonra başka bir kaynak dağıtılmalıdır, toouse hello gerekir **dependsOn** , şablon toocreate bağımlı bir öğedeki hello diğer kaynak. Örneğin, bir web uygulaması dağıtırken hello uygulama hizmeti planı bulunması gerekir. Bu başlangıç web uygulaması uygulama hizmeti planı hello üzerinde bağlıdır belirtmediyseniz, Resource Manager her iki kaynağın hello oluşturur. aynı anda. Bunu henüz tooset özellik hello web uygulaması üzerinde çalışırken var olmadığından uygulama hizmeti planı kaynak bulunamadı, bu hello bildiren bir hata alırsınız. Bu hata hello web uygulamasında hello bağımlılık ayarlayarak engeller.

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

Bağımlılık hatalarında sorun giderme hakkında daha fazla bilgi için bkz: [denetleyin dağıtım sırası](#check-deployment-sequence).

Farklı bir kaynak grubunda biri için dağıtılan hello daha Hello kaynak mevcut olduğunda bu hata Ayrıca bkz. Bu durumda, hello kullan [ResourceId işlevi](resource-group-template-functions-resource.md#resourceid) tooget hello hello kaynağın tam adı.

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

Toouse hello çalışırsanız [başvuru](resource-group-template-functions-resource.md#reference) veya [listKeys](resource-group-template-functions-resource.md#listkeys) işlevleri bir kaynakla aşağıdaki hata hello aldığınız çözümlenemiyor:

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

Merhaba içeren bir ifade Ara **başvuru** işlevi. Çift hello parametre değerlerini doğru olup olmadıklarını denetleyin.

## <a name="parentresourcenotfound"></a>ParentResourceNotFound

Bir kaynak üst tooanother kaynak olduğunda hello üst kaynak hello alt kaynak oluşturmadan önce mevcut olması gerekir. Henüz yoksa, aşağıdaki hata hello alırsınız:

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

Merhaba hello alt kaynağın adını hello üst adı içerir. Örneğin, bir SQL veritabanı olarak tanımlanabilir:

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

Ancak, bir bağımlılık hello üst kaynakta belirtmezseniz hello alt kaynak hello üst önce dağıtılan. tooresolve bu hata, bir bağımlılık içerir.

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a>StorageAccountAlreadyExists ve StorageAccountAlreadyTaken
Depolama hesapları için Azure arasında benzersizdir hello kaynak için bir ad sağlamanız gerekir. Benzersiz bir ad belirtmezseniz, benzer bir hata alırsınız:

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

Adlandırma kuralınızın hello hello sonucu ile birleştirerek benzersiz bir ad oluşturabilirsiniz [uniqueString](resource-group-template-functions-string.md#uniquestring) işlevi.

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

Merhaba depolama hesabıyla dağıtırsanız aynı aboneliğinizde var olan bir depolama hesabı adı, ancak farklı bir konum sağlar; belirten hello depolama hesabı zaten var. farklı bir konumda bir hata alırsınız. Merhaba var olan depolama hesabını silmek ya da sağlamak varolan depolama hesabı hello gibi aynı konuma hello.

## <a name="accountnameinvalid"></a>AccountNameInvalid
Merhaba gördüğünüz **AccountNameInvalid** çalışırken toogive bir depolama hesabını içeren bir adı yasaklanmış karakterleri sırasında hata oluştu. Depolama hesabı adları 3 ile 24 karakter uzunluğunda olmalıdır ve rakamlar ve yalnızca küçük harfler kullanmanız gerekir. Merhaba [uniqueString](resource-group-template-functions-string.md#uniquestring) işlevi 13 karakter döndürür. Bir önek toohello birleştirmek, **uniqueString** neden, 11 karakterdir bir önek sağlayın veya daha az.

## <a name="badrequest"></a>BadRequest

Özelliği için geçersiz bir değer sağlarsanız, bir BadRequest durum karşılaşabilirsiniz. Örneğin, bir depolama hesabı için hatalı bir SKU değer sağlarsanız, hello dağıtımı başarısız olur. özelliği için geçerli değerler toodetermine Ara hello [REST API](/rest/api) dağıttığınız hello kaynak türü için.

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a>NoRegisteredProviderFound ve MissingSubscriptionRegistration
Kaynak dağıtırken, hata kodu aşağıdaki hello almak ve ileti:

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

Veya bildiren benzer bir ileti alabilirsiniz:

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

Üç nedenden biri için bu hataları alırsınız:

1. Merhaba kaynak sağlayıcısı, aboneliğiniz için kayıtlı değil
2. API sürümü Hello kaynak türü için desteklenmiyor
3. Konum Hello kaynak türü için desteklenmiyor

Merhaba hata iletisi desteklenen hello konumları ve API sürümleri için öneriler vermesi gerekir. Merhaba, şablon tooone değiştirebilirsiniz önerilen değerleri. Çoğu sağlayıcıları hello Azure portal veya hello komut satırı kullanmakta olduğunuz arabirimi, ancak tüm tarafından otomatik olarak kaydedilir. Belirli kaynak sağlayıcısı önce kullanmadıysanız, bu sağlayıcıyı tooregister gerekebilir. PowerShell veya Azure CLI aracılığıyla kaynak sağlayıcıları hakkında daha fazla bulabilir.

**Portal**

Merhaba kayıt durumunu görmek ve bir kaynak sağlayıcısı ad alanı hello portal üzerinden kaydedin.

1. Aboneliğiniz için seçin **kaynak sağlayıcıları**.

   ![kaynak sağlayıcıları seç](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. Kaynak sağlayıcıları hello listenin bakın ve gerekiyorsa, seçin hello **kaydetmek** bağlantı tooregister hello kaynak sağlayıcısı hello türü toodeploy çalışıyorsunuz.

   ![kaynak sağlayıcıları Listele](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

**PowerShell**

toosee kullanın, kayıt durumunu **Get-AzureRmResourceProvider**.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

tooregister bir sağlayıcı kullanmak **Register-AzureRmResourceProvider** hello ad hello kaynak sağlayıcısı tooregister istiyor.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

belirli bir kaynak türü için tooget desteklenen hello konumlarını kullanın:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

belirli bir kaynak, kullanım türü için desteklenen API sürümleri tooget hello:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

**Azure CLI**

toosee hello sağlayıcısı kayıtlı olup olmadığını hello kullan `azure provider list` komutu.

```azurecli
az provider list
```

tooregister bir kaynak sağlayıcısı kullanın hello `azure provider register` komut ve hello belirtin *ad alanı* tooregister.

```azurecli
az provider register --namespace Microsoft.Cdn
```

toosee hello desteklenen konumlar ve API sürümleri için bir kaynak türünü kullanın:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a>QuotaExceeded ve OperationNotAllowed
Dağıtım kaynak grubu, abonelikler, hesapları ve diğer kapsamları olabilecek bir kota aştığında sorunları olabilir. Örneğin, aboneliğiniz olabilir toolimit hello bir bölge için çekirdek sayısı yapılandırılmış. Toodeploy hello tutar izin verilenden daha fazla çekirdek sahip bir sanal makine çalışırsanız belirten hello kotası aşıldı bir hata alıyorsunuz.
Tam kota bilgi için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).

tooexamine aboneliğinizin kotaları çekirdek için hello kullanabilirsiniz `azure vm list-usage` hello Azure CLI komutu. ücretsiz bir deneme hesabı 4 için aşağıdaki örneğine hello bu hello çekirdek kotası gösterilmektedir:

```azurecli
az vm list-usage --location "South Central US"
```

Hangi döndürür:

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

Merhaba Batı ABD bölgesinde dörtten fazla çekirdek oluşturan bir şablonu dağıtmak, benzer bir dağıtım hatası alırsınız:

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

Veya, PowerShell'de hello kullanabilirsiniz **Get-AzureRmVMUsage** cmdlet'i.

```powershell
Get-AzureRmVMUsage
```

Hangi döndürür:

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

Bu durumlarda, toohello portal gidin ve kota toodeploy istediğiniz hello bölge için bir destek sorunu tooraise dosya gerekir.

> [!NOTE]
> Kaynak grupları için hello tüm abonelik için tek tek her bölge için hello kota olduğunu unutmayın. Batı ABD 30 çekirdeğini toodeploy gerekiyorsa, Batı ABD 30 Resource Manager çekirdekleri tooask sahip. Herhangi bir hello bölgeleri toowhich toodeploy 30 çekirdek ihtiyacınız varsa, tüm bölgelerde 30 Resource Manager çekirdekleri istemelisiniz erişebilirsiniz.
>
>

## <a name="invalidcontentlink"></a>InvalidContentLink
Ne zaman hello hata iletisini alıyorsunuz:

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

Büyük olasılıkla kullanılamıyor toolink tooa iç içe geçmiş şablon denediniz. Çift onay hello hello iç içe geçmiş şablonu için sağlanan URI. Merhaba şablon bir depolama hesabı varsa, hello URI erişilebilir olduğundan emin olun. Toopass bir SAS belirteci gerekebilir. Daha fazla bilgi için bkz. [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).

## <a name="requestdisallowedbypolicy"></a>RequestDisallowedByPolicy
Aboneliğinizi dağıtımı sırasında tooperform çalıştığınız eylem engelleyen bir kaynak İlkesi içerdiğinde bu hatayı alırsınız. Merhaba hata iletisinde hello İlkesi tanımlayıcısı arayın.

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

İçinde **PowerShell**, bu ilke tanımlayıcısı hello olarak sağlamak **kimliği** parametresi tooretrieve dağıtımınızı engellenen hello ilkesi ayrıntıları.

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

İçinde **Azure CLI**, hello ilke tanımı hello adını sağlayın:

```azurecli
az policy definition show --name regionPolicyAssignment
```

Daha fazla bilgi için aşağıdaki makaleler hello bakın:

- [RequestDisallowedByPolicy hatası](resource-manager-policy-requestdisallowedbypolicy-error.md)
- [İlke toomanage kaynakları kullanın ve erişimi denetlemenize](resource-manager-policy.md).

## <a name="authorization-failed"></a>Yetkilendirme başarısız oldu
Merhaba hesabı ya da hizmet sorumlusu toodeploy hello kaynakları çalışırken erişim tooperform bu eylemleri sahip olmadığından, dağıtım sırasında bir hata alabilirsiniz. Azure Active Directory veya hangi kimlikleri duyarlık önemli ölçüde ile hangi kaynaklara erişebilir, yönetici toocontrol sağlar. Örneğin, hesabınıza toohello okuyucu rolüne atanan, değil mümkün toocreate kaynakları demektir. Bu durumda, yetkilendirme başarısız olduğunu belirten bir hata iletisi görürsünüz.

Rol tabanlı erişim denetimi hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).


## <a name="next-steps"></a>Sonraki adımlar
* Eylemler, Denetim hakkında toolearn bkz [denetim işlemleri Resource Manager ile](resource-group-audit.md).
* dağıtım sırasında Eylemler toodetermine hello hatalarla ilgili toolearn bkz [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).
