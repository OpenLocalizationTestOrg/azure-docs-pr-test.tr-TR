---
title: "sanal makine ölçek hakkında aaaLearn şablonları ayarlama | Microsoft Docs"
description: "Sanal makine ölçek kümeleri için şablon toocreate minimum uygun ölçek kümesi öğrenin"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a>Sanal makine ölçek kümesi şablonları hakkında bilgi edinin
[Azure Resource Manager şablonları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) mükemmel şekilde toodeploy ilgili kaynaklar gruplarıdır. Bu öğretici serisi toocreate minimum uygun ölçek şablon ayarlama nasıl ve ne gösterilir toomodify bu şablonu toosuit çeşitli senaryoları. Tüm örnekler öğesinden gelen [GitHub deposunu](https://github.com/gatneil/mvss). 

Hedeflenen toobe basit şablonudur. Ölçek daha kapsamlı örnekleri için şablonlar, hello bakın [Azure hızlı başlangıç şablonlarını GitHub deposunu](https://github.com/Azure/azure-quickstart-templates) ve hello dizesini içeren klasörleri arama `vmss`.

Şablonları oluşturma konusunda bilginiz varsa, nasıl toohello "Sonraki adımlar" bölümüne toosee atlayın toomodify bu şablonu.

## <a name="review-hello-template"></a>Gözden geçirme hello şablonu

GitHub kullanmak tooreview bizim minimum uygun ölçek kümesi şablon [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).

Bu öğreticide, inceleyeceğiz hello fark (`git diff master minimum-viable-scale-set`) toocreate hello minimum uygun ölçek kümesi şablonu tarafından parça parça.

## <a name="define-schema-and-contentversion"></a>$Schema ve contentVersion tanımlayın
İlk olarak, tanımlarız `$schema` ve `contentVersion` hello şablonunda. Merhaba `$schema` öğesi hello şablon dili hello sürümü tanımlar ve Visual Studio söz dizimi vurgulama ve benzer doğrulama özellikleri için kullanılır. Merhaba `contentVersion` öğesi Azure tarafından kullanılmaz. Bunun yerine, hello şablon sürümü izlemenize yardımcı olur.

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a>parametrelerini tanımlayın
Ardından, iki parametre tanımlarız `adminUsername` ve `adminPassword`. Parametreler hello dağıtım sırasında belirttiğiniz değerlerdir. Merhaba `adminUsername` parametredir yalnızca bir `string` türü, ancak çünkü `adminPassword` bir parolası türü sunuyoruz `securestring`. Daha sonra bu parametreler hello ölçek kümesi yapılandırması aktarılır.

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a>Değişkenleri tanımlama
Resource Manager şablonları aynı zamanda, daha sonra hello şablonda kullanılan değişkenleri toobe tanımlamanıza olanak sağlar. Biz hello JSON nesnesi boş sol şekilde örneğimizde herhangi bir değişkeni kullanmaz.

```json
  "variables": {},
```

## <a name="define-resources"></a>Kaynakları tanımlayın
Sonraki hello kaynakları hello şablon bölümüdür. Burada, aslında istediğinizi tanımladığınız toodeploy. Farklı `parameters` ve `variables` (JSON nesnelerinin olan), `resources` JSON nesnelerinin JSON listesidir.

```json
   "resources": [
```

Tüm kaynak gerektiren `type`, `name`, `apiVersion`, ve `location` özellikleri. Bu örneğin ilk kaynak türüne sahip `Microsft.Network/virtualNetwork`, adı `myVnet`ve apiVersion `2016-03-30`. (toofind hello son API sürümü bir kaynak türü için bkz: Merhaba [Azure REST API belgeleri](https://docs.microsoft.com/rest/api/).)

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a>Konumu belirtin
toospecify hello konumu hello sanal ağ için kullandığımız bir [Resource Manager şablonu işlevi](../azure-resource-manager/resource-group-template-functions.md). Bu işlev teklifleri ve bu gibi köşeli ayraçlar içinde alınmalıdır: `"[<template-function>]"`. Bu durumda, hello kullanırız `resourceGroup` işlevi. İçinde bağımsız değişken almayan ve bu dağıtım için dağıtılan hello kaynak grubu hakkındaki meta verileri içeren bir JSON nesnesi döndürür. Merhaba kaynak grubu dağıtım hello aynı anda hello kullanıcı tarafından ayarlanır. Biz sonra bu JSON nesnesinin ile dizine `.location` hello JSON nesnesinde tooget başlangıç konumu.

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a>Sanal ağ özelliklerini belirtin
Her bir Resource Manager kaynak kendi sahip `properties` yapılandırmaları belirli toohello kaynak bölümü. Bu durumda, bu hello sanal ağ hello özel IP adres aralığını kullanarak tek bir alt ağda olması gerektiğini belirtin `10.0.0.0/16`. Ölçek kümesi her zaman bir alt ağ içinde yer alır. Alt ağlar yayılamaz.

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a>DependsOn listeye ekleyin
Ayrıca toohello gerekli `type`, `name`, `apiVersion`, ve `location` özellikleri, her bir kaynağın isteğe bağlı bir olabilir `dependsOn` dize listesi. Bu liste, bu kaynak dağıtmadan önce bu dağıtım diğer kaynaklardan bitmesi gereken belirtir.

Bu durumda, var. yalnızca tek bir öğe hello listesinde hello önceki örnekteki hello sanal ağ Merhaba ağ tooexist ihtiyaçlarını ayarlanmış tüm sanal makineleri oluşturmadan önce Hello ölçek için Biz bu bağımlılık belirtin. Bu şekilde hello ölçek kümesi daha önce hello Ağ özelliklerinde belirtilen başlangıç IP adresi aralığından bu VM'ler özel IP adreslerini verin. Merhaba dependsOn listesindeki her bir dizenin Hello biçimi `<type>/<name>`. Kullanım hello aynı `type` ve `name` hello sanal ağ kaynak tanımı'nda önceden kullanılmış.

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a>Ölçek kümesi özelliklerini belirtin
Ölçek kümeleri hello VM'ler hello ölçek kümesindeki özelleştirmek için birçok özelliği vardır. Bu özelliklerin tam listesi için bkz: Merhaba [ölçek kümesi REST API belgeleri](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set). Bu öğreticide, biz yalnızca birkaç yaygın olarak kullanılan özellikleri ayarlayın.
### <a name="supply-vm-size-and-capacity"></a>VM boyutu ve kapasite sağlayın
Merhaba ölçek gereksinimlerini tooknow VM toocreate ("sku adı") hangi boyutunu ve kaç tane böyle VM'ler toocreate ("sku kapasitesi") ayarlayın. Hangi VM boyutları kullanılabilir toosee bkz hello [VM boyutları belgelerine](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a>Güncelleştirmelerin türünü seçin
Merhaba ölçek kümesini toohandle hello ölçek kümesinde güncelleştirme biçimini tooknow da gerekir. Şu anda iki seçenek vardır `Manual` ve `Automatic`. Merhaba hello iki arasındaki farklar hakkında daha fazla bilgi için üzerinde hello belgelerine bakın. [nasıl tooupgrade bir ölçek kümesi](./virtual-machine-scale-sets-upgrade-scale-set.md).

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a>VM işletim sistemini seçin
Merhaba ölçek gereksinimlerine tooknow hangi işletim sistemi tooput hello Vm'lerinde ayarlayın. Burada, hello VM'ler ile tam olarak düzeltme eki bir Ubuntu 16.04 LTS görüntüsü oluşturuyoruz.

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a>ComputerNamePrefix belirtin
Merhaba ölçek kümesini birden çok VM dağıtır. Her bir VM adı belirtmek yerine, biz belirtin `computerNamePrefix`. hello form VM adlara sahip olacak şekilde hello ölçek kümesini bir dizin toohello öneki her bir VM ekler `<computerNamePrefix>_<auto-generated-index>`.

Aşağıdaki kod parçacığında hello hello ölçek kümesindeki tüm VM'ler için tooset hello yönetici kullanıcı adı ve parola önce hello parametrelerinden kullanın. Merhaba ile bunu `parameters` şablon işlevi. Bu işlev, bu parametre için değer hello hangi parametresi toorefer tooand çıkarır belirten bir dize olarak alır.

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a>VM ağ yapılandırması belirtin
Son olarak, biz hello ölçek kümesindeki hello VM'ler için toospecify hello ağ yapılandırması gerekir. Bu durumda, yalnızca daha önce oluşturduğunuz hello alt toospecify hello kimliği ihtiyacımız var. Bu, hello ölçek tooput hello ağ arabirimleri bu alt ağda kümesi bildirir.

Merhaba sanal ağ hello kullanarak hello alt ağ içeren hello Kimliğini alabilirsiniz `resourceId` şablon işlevi. Bu işlev hello türü ve kaynağın adını alır ve bu kaynağın tam tanımlayıcı döndürür hello. Bu kimliği hello biçime sahiptir:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`

Ancak, hello sanal ağ hello tanıtıcısı yeterli değildir. Ölçek kümesi VM bulunmalıdır hello hello belirli alt belirtmeniz gerekir. toodo Bu, birleştirme `/subnets/mySubnet` hello sanal ağ toohello kimliği. Merhaba, tam olarak nitelenmiş hello hello alt ağ Kimliğini sonucudur. Bu birleştirme hello ile yapmak `concat` dizeleri bir dizi alır ve kendi birleştirme döndüren işlev.

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
