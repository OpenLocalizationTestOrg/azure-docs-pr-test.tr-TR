---
title: "Ortak Azure dağıtım hatalarını giderme | Microsoft Docs"
description: "Azure Kaynak Yöneticisi'ni kullanarak Azure kaynakları dağıttığınızda sık karşılaşılan hataların nasıl çözüleceği açıklanmaktadır."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Dağıtım hatası, azure dağıtım azure'a dağıtma"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 30adc10d01290f14a3e116813b19916fa36ab0bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>Ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme
Bu konu, bazı ortak nasıl çözebilirsiniz açıklar karşılaşabileceğiniz Azure dağıtım hataları.

Bu konuda aşağıdaki hata kodları açıklanmaktadır:

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

Bu hata kodu genel dağıtım hatası gösterir, ancak sorun giderme başlatmak için gereken hata kodu değil. Aslında, sorunu gidermenize yardımcı olacak hata genellikle bir düzey altında bu hata kodudur. Örneğin, aşağıdaki gösterir görüntü **RequestDisallowedByPolicy** altında dağıtım hata hata kodu.

![Hata Kodu Göster](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a>SkuNotAvailable

Bir kaynak (genellikle bir sanal makine) dağıtırken şu hata kodu ve hata iletisini alabilirsiniz:

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

(VM boyutu gibi) seçtiniz SKU kaynak seçtiğiniz konum için kullanılabilir olmadığında bu hatayı alırsınız. Bu sorunu çözmek için SKU'ları bir bölgede kullanılabilir olan belirlemeniz gerekir. Kullanılabilir SKU'lar bulmak için PowerShell, portalı veya REST işlemini kullanın.

- İçin PowerShell kullanın [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) ve konuma göre filtre. Bu komut için PowerShell en son sürümünü olması gerekir.

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  Sonuçlar SKU'ları listesi için konum ve SKU yönelik kısıtlamaları içerir.

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- Kullanılacak [portal](https://portal.azure.com), portalda oturum açın ve kaynak arabirimi üzerinden ekleyin. Değerleri ayarlama gibi bu kaynak için kullanılabilir SKU'lar bakın. Dağıtımın tamamlanması gerekmez.

    ![kullanılabilir SKU'lar](./media/resource-manager-common-deployment-errors/view-sku.png)

- Sanal makineler için REST API kullanmak için aşağıdaki isteği gönder:

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  Kullanılabilir SKU'ları ve bölgeler şu biçimde döndürür:

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

Bu bölgede uygun SKU bulamıyor veya işletmenizin karşılayan bir alternatif bölge gönderme gereksinimlerini bir [SKU isteği](https://aka.ms/skurestriction) Azure desteği.

## <a name="disallowedoperation"></a>DisallowedOperation

```
Code: DisallowedOperation
Message: The current subscription type is not permitted to perform operations on any provider 
namespace. Please use a different subscription.
```

Bu hata alırsanız, Azure Active Directory dışındaki herhangi bir Azure hizmeti erişim izni olmayan bir aboneliği kullanıyorsunuz. Klasik Portalı'nı erişmeniz gerekir, ancak kaynaklar dağıtmak için izin verilmiyor durumlarda bu tür aboneliği olabilir. Bu sorunu çözmek için kaynakları dağıtmak için izne sahip bir abonelik kullanmanız gerekir.  

PowerShell ile kullanılabilir aboneliklerinizi görüntülemek için kullanın:

```powershell
Get-AzureRmSubscription
```

Ve şu anki aboneliği ayarlamak için kullanın:

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

Azure CLI 2.0 ile birlikte kullanılabilir aboneliklerinizi görüntülemek için kullanın:

```azurecli
az account list
```

Ve şu anki aboneliği ayarlamak için kullanın:

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a>InvalidTemplate
Bu hata, birkaç farklı türlerinden hataları neden olabilir.

- Sözdizimi hatası

   Şablon başarısız doğrulama bildiren bir hata iletisi alırsanız, şablonunuzun söz dizimi sorunu olabilir.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   Bu hata, şablon ifadeleri karmaşık olabileceğinden yapmak kolaydır. Örneğin, aşağıdaki ad ataması bir depolama hesabı için bir dizi köşeli ayraçlar, üç işlevi, parantez üç kümesi, tek tırnak bir dizi ve bir özellik içerir:

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   Eşleştirme sözdizimi belirtmezseniz, şablon amacınız farklı bir değer oluşturur.

   Bu tür hatalara aldığınızda, ifade sözdizimini dikkatle gözden geçirin. Bir JSON Düzenleyicisi gibi kullanmayı [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) veya [Visual Studio Code](resource-manager-vs-code.md), hangi uyar, söz dizimi hataları hakkında.

- Yanlış segment uzunluklarına

   Kaynak adı doğru biçimde değil başka bir geçersiz şablon hata oluşur.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'The template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   Kök düzeyinde kaynak daha az bir kesim adından kaynak türünde olması gerekir. Her segmentinde bir eğik çizgiyle Ayrıştırılan. Aşağıdaki örnekte, iki bölümü türü ve dolayısıyla bir kesim adına sahip bir **geçerli ad**.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   Ancak sonraki örnek **geçerli bir ad değil** türü aynı sayıda Segment içerdiğinden.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   Alt kaynakları için kesimleri ile aynı sayıda türü ve ada sahip. Tam adı ve alt türü içerdiği için üst adını ve türünü Segment sayısı mantıklıdır. Bu nedenle, tam adı, tam türünü daha küçük bir kesim hala vardır.

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

   Segment sağ alma kaynak sağlayıcıları uygulanan Resource Manager türleriyle zor olabilir. Örneğin, bir web sitesi için bir kaynak kilidi uygulama dört kesimine sahip bir türü gerektirir. Bu nedenle, üç kesimleri adıdır:

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- Kopya dizini beklenmiyor

   Bu karşılaştığınız **InvalidTemplate** uygulandığında hata **kopya** bu öğe desteklemiyor şablonunun parçası öğesi. Yalnızca bir kaynak türü kopya öğesi uygulayabilirsiniz. Bir kaynak türü içinde bir özellik kopyalama uygulayamazsınız. Örneğin, kopya bir sanal makine için geçerli, ancak bir sanal makine için işletim sistemi disklere uygulanamıyor. Bazı durumlarda, kopyalama döngüsü oluşturmak için bir üst kaynağına bağımlı kaynak dönüştürebilirsiniz. Kopya kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](resource-group-create-multiple.md).

- Parametre geçerli değil

   İzin verilen değerler bir parametre için kullanılacak şablonu belirtir ve bu değerlerden biri olmayan bir değer sağlayın, aşağıdakine benzer bir ileti alırsınız:

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'The provided value {parameter value}
  for the template parameter {parameter name} is not valid. The parameter value is not
  part of the allowed values
  ``` 

   Double şablondaki izin verilen değerler denetleyin ve dağıtım sırasında bir sağlayın.

- Döngüsel bağımlılık algılandı

   Birbirine bağımlı kaynakları dağıtım başlatılmasını engelleyen bir şekilde, bu hatayı alırsınız. Ayrıca bekleyen için diğer kaynaklar bekleyin iki veya daha fazla kaynak bağımlılıklarını bileşimini yapar. Örneğin, üzerinde resource3 resource1 bağlıdır, üzerinde resource1 switch2 bağlıdır ve üzerinde switch2 resource3 bağlıdır. Genellikle, gereksiz bağımlılıkları kaldırarak bu sorunu çözebilirsiniz. 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a>NotFound ve ResourceNotFound
Şablonunuzu çözümlenemeyen kaynağın adını içerdiğinde, benzer bir hata alırsınız:

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

Şablon eksik kaynak dağıtmak çalışıyorsunuz, bir bağımlılık eklemeniz gerekip gerekmediğini denetleyin. Resource Manager kaynakları paralel olarak, mümkün olduğunda oluşturarak dağıtım en iyi duruma getirir. Bir kaynak sonra başka bir kaynak dağıtılmalıdır, kullanmanıza gerek **dependsOn** öğesi şablonunuzda diğer kaynak üzerinde bir bağımlılık oluşturun. Örneğin, bir web uygulaması dağıtımını yaparken, uygulama hizmeti planı bulunması gerekir. Web uygulaması uygulama hizmeti plan üzerinde bağlıdır belirtmediyseniz, Resource Manager aynı anda hem de kaynaklar oluşturur. Bunu henüz web uygulamasında bir özellik Ayarla girişiminde bulunulduğunda var olmadığından uygulama hizmeti planı kaynağın bulunamadığını bildiren bir hata alırsınız. Bu hata, web uygulamasında bağımlılık ayarlayarak engeller.

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

İçin dağıtılan olandan farklı bir kaynak grubundaki kaynak mevcut olduğunda bu hata Ayrıca bkz. Bu durumda, kullanın [ResourceId işlevi](resource-group-template-functions-resource.md#resourceid) kaynak tam adını almak için.

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

Kullanmayı denerseniz, [başvuru](resource-group-template-functions-resource.md#reference) veya [listKeys](resource-group-template-functions-resource.md#listkeys) işlevleri bir kaynakla aşağıdaki hata iletisini çözümlenemiyor:

```
Code=ResourceNotFound;
Message=The Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

İçeren bir ifade Ara **başvuru** işlevi. Parametre değerleri doğru olduğunu kontrol edin.

## <a name="parentresourcenotfound"></a>ParentResourceNotFound

Bir kaynağı başka bir kaynak için bir üst olduğunda, üst kaynak alt kaynak oluşturmadan önce mevcut olması gerekir. Henüz yoksa, aşağıdaki hatayı alırsınız:

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

Alt kaynağın adını üst adı içerir. Örneğin, bir SQL veritabanı olarak tanımlanabilir:

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

Ancak, bir bağımlılık üst kaynakta belirtmezseniz, alt kaynak önce üst dağıtılan. Bu hatayı gidermek için bir bağımlılık ekleyin.

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a>StorageAccountAlreadyExists ve StorageAccountAlreadyTaken
Depolama hesapları için Azure arasında benzersiz kaynak için bir ad sağlamanız gerekir. Benzersiz bir ad belirtmezseniz, benzer bir hata alırsınız:

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

Adlandırma kuralınızın sonucu ile birleştirerek benzersiz bir ad oluşturabilirsiniz [uniqueString](resource-group-template-functions-string.md#uniquestring) işlevi.

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

Aboneliğinizde var olan bir depolama hesabıyla aynı ada sahip bir depolama hesabı dağıtmak, ancak farklı bir konum sağlayın, depolama hesabı zaten var. farklı bir konumda belirten bir hata alırsınız. Var olan depolama hesabını silmek ya da var olan depolama hesabı ile aynı konumda sağlayın.

## <a name="accountnameinvalid"></a>AccountNameInvalid
Gördüğünüz **AccountNameInvalid** yasaklanmış karakterleri içeren bir adı bir depolama hesabı verin girişimi sırasında hata oluştu. Depolama hesabı adları 3 ile 24 karakter uzunluğunda olmalıdır ve rakamlar ve yalnızca küçük harfler kullanmanız gerekir. [UniqueString](resource-group-template-functions-string.md#uniquestring) işlevi 13 karakter döndürür. Bir önek birleştirmek, **uniqueString** neden, 11 karakterdir bir önek sağlayın veya daha az.

## <a name="badrequest"></a>BadRequest

Özelliği için geçersiz bir değer sağlarsanız, bir BadRequest durum karşılaşabilirsiniz. Örneğin, bir depolama hesabı için hatalı bir SKU değer sağlarsanız, dağıtım başarısız olur. Özellik için geçerli değerler belirlemek için bakmak [REST API](/rest/api) dağıttığınız kaynak türü için.

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a>NoRegisteredProviderFound ve MissingSubscriptionRegistration
Kaynak dağıtırken şu hata kodu ve ileti alabilirsiniz:

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

Veya bildiren benzer bir ileti alabilirsiniz:

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

Üç nedenden biri için bu hataları alırsınız:

1. Kaynak sağlayıcısı, aboneliğiniz için kayıtlı değil
2. API sürümü kaynak türü için desteklenmiyor
3. Kaynak türü için desteklenmeyen konumu

Hata iletisi desteklenen konumlar ve API sürümleri için öneriler vermesi gerekir. Şablonunuzu önerilen değerlerden birine değiştirebilirsiniz. Azure portal ya da kullandığınız komut satırı arabirimi tarafından otomatik olarak kayıtlı ancak tüm çoğu sağlayıcıları. Belirli kaynak sağlayıcısı önce kullanmadıysanız, bu sağlayıcıyı kaydetmeniz gerekebilir. PowerShell veya Azure CLI aracılığıyla kaynak sağlayıcıları hakkında daha fazla bulabilir.

**Portal**

Kayıt durumunu görmek ve bir kaynak sağlayıcısı ad alanı Portalı aracılığıyla kaydedin.

1. Aboneliğiniz için seçin **kaynak sağlayıcıları**.

   ![kaynak sağlayıcıları seç](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. Kaynak sağlayıcıları listesi bakın ve gerekiyorsa, seçin **kaydetmek** kayıt kaynak sağlayıcısı dağıtmaya çalıştığınız türü için bağlantı.

   ![kaynak sağlayıcıları Listele](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

**PowerShell**

Kayıt durumunu görmek için **Get-AzureRmResourceProvider**.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

Bir sağlayıcı kaydetmek için kullanın **Register-AzureRmResourceProvider** ve kaydetmek istediğiniz kaynak sağlayıcısının adını sağlayın.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

Belirli bir kaynak türü için desteklenen konumlardan almak için kullanın:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Belirli bir kaynak türü için desteklenen API sürümleri almak için kullanın:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

**Azure CLI**

Sağlayıcı kayıtlı olup olmadığını görmek için `azure provider list` komutu.

```azurecli
az provider list
```

Bir kaynak sağlayıcısı kaydetmek için kullanın `azure provider register` komut ve belirtin *ad alanı* kaydetmek için.

```azurecli
az provider register --namespace Microsoft.Cdn
```

Desteklenen konumlar ve bir kaynak türü için API sürümlerini görmek için kullanın:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a>QuotaExceeded ve OperationNotAllowed
Dağıtım kaynak grubu, abonelikler, hesapları ve diğer kapsamları olabilecek bir kota aştığında sorunları olabilir. Örneğin, aboneliğinizi bir bölge için çekirdek sayısını sınırlamak için yapılandırılabilir. İzin verilen miktardan daha fazla çekirdeğe sahip bir sanal makineyi dağıtma girişiminde, kota aşıldı bildiren bir hata alırsınız.
Tam kota bilgi için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).

Aboneliğinizin kotaları çekirdekleri incelemek için kullanabileceğiniz `azure vm list-usage` Azure CLI komutu. Aşağıdaki örnek, ücretsiz bir deneme hesabı için çekirdek kota 4 olduğunu gösterir:

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

Batı ABD bölgesinde dörtten fazla çekirdek oluşturan bir şablonu dağıtmak, benzer bir dağıtım hatası alırsınız:

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

Veya PowerShell içinde kullandığınız **Get-AzureRmVMUsage** cmdlet'i.

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

Bu durumlarda, Portalı'na gidin ve dağıtmak istediğiniz bölgeyi için kotayı artırmak için bir destek sorununu dosya gerekir.

> [!NOTE]
> Kaynak grupları için tüm abonelik için tek tek her bölge için kota olduğunu unutmayın. Batı ABD 30 çekirdeğini dağıtımı yapmanız gerekirse, Batı ABD 30 Resource Manager çekirdekleri yapmasını istemek zorunda. Hangi bölgeleri hiçbirinde erişiminiz 30 çekirdek dağıtımı yapmanız gerekirse, tüm bölgelerde 30 Resource Manager çekirdekleri istemeniz gerekir.
>
>

## <a name="invalidcontentlink"></a>InvalidContentLink
Ne zaman hata iletisini alıyorsunuz:

```
Code=InvalidContentLink
Message=Unable to download deployment content from ...
```

Büyük olasılıkla kullanılamıyor iç içe geçmiş bir şablon bağlantı denediniz. İç içe geçmiş şablon için sağladığınız URI kontrol edin. Şablon bir depolama hesabı varsa, URI erişilebilir olduğundan emin olun. Bir SAS belirteci geçmesi gerekebilir. Daha fazla bilgi için bkz. [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).

## <a name="requestdisallowedbypolicy"></a>RequestDisallowedByPolicy
Aboneliğinizi dağıtımı sırasında gerçekleştirmeye eylem engelleyen bir kaynak İlkesi içerdiğinde bu hatayı alırsınız. Hata iletisinde için ilke tanımlayıcısı arayın.

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

İçinde **PowerShell**, bu ilke tanımlayıcısı olarak sağlamak **kimliği** dağıtımınızı engellenen İlkesi hakkındaki ayrıntıları almak için parametre.

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

İçinde **Azure CLI**, ilke tanımı adını sağlayın:

```azurecli
az policy definition show --name regionPolicyAssignment
```

Daha fazla bilgi için aşağıdaki makalelere bakın:

- [RequestDisallowedByPolicy hatası](resource-manager-policy-requestdisallowedbypolicy-error.md)
- [Kaynakları yönetme ve erişimi denetlemek için ilke kullanma](resource-manager-policy.md).

## <a name="authorization-failed"></a>Yetkilendirme başarısız oldu
Bu eylemleri gerçekleştirmek için erişim hesabı ya da hizmet sorumlusu kaynakları dağıtma denemesi sahip olmadığından, dağıtım sırasında bir hata alabilirsiniz. Azure Active Directory sağlar veya hangi kimlikleri denetlemek için yöneticinize duyarlık önemli ölçüde ile hangi kaynaklara erişebilir. Hesabınızı okuyucu rolüne atanırsa, örneğin, kaynakları oluşturmak mümkün değildir. Bu durumda, yetkilendirme başarısız olduğunu belirten bir hata iletisi görürsünüz.

Rol tabanlı erişim denetimi hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).


## <a name="next-steps"></a>Sonraki adımlar
* Eylemler denetleme hakkında bilgi edinmek için [denetim işlemleri Resource Manager ile](resource-group-audit.md).
* Dağıtım sırasında hataları belirlemek için Eylemler hakkında bilgi edinmek için [görüntülemek dağıtım işlemlerini](resource-manager-deployment-operations.md).
