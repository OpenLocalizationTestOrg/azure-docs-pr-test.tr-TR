---
title: "Azure şablonu aaaDefine alt kaynak | Microsoft Docs"
description: "Tooset nasıl hello kaynak türü ve Azure Resource Manager şablonu alt kaynağın adını gösterir"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a>Alt kaynak için ad ve tür Resource Manager şablonunda ayarlayın
Bir şablon oluştururken, sık tooinclude ilgili tooa üst kaynak bir alt kaynak gerekir. Örneğin, şablonunuza bir SQL server ve veritabanı içerebilir. Merhaba SQL server hello üst kaynak ve hello alt kaynak hello veritabanıdır. 

Merhaba alt kaynak türünün Hello biçimdedir:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`

Merhaba alt kaynak adın Hello biçimdedir:`{parent-resource-name}/{child-resource-name}`

Ancak, hello türü ve bir şablon adı farklı içindeki hello üst kaynak olup olmadığını iç içe yerleştirilmiş üzerinde veya kendi hello en üst düzeyde göre belirtin. Bu konu, her iki toohandle nasıl yaklaşıyor gösterir.

Tam başvuru tooa kaynak oluştururken hello sipariş toocombine hello türünden kesim ve ad hello iki yalnızca bir birleşimini değil.  Bunun yerine, bir dizi hello ad alanından sonra kullanın *türü/adı* az belirli toomost belirli çiftlerinden:

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

Örneğin:

`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`doğru `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` doğru değil

## <a name="nested-child-resource"></a>İç içe alt kaynak
Merhaba en kolay yolu toodefine alt kaynak olan toonest hello üst kaynak içinde. Merhaba aşağıdaki örnek bir SQL Server içinde iç içe geçmiş bir SQL veritabanı gösterir.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

Merhaba alt kaynak için çok hello türü ayarlanmış`databases` ancak kendi tam kaynak türü `Microsoft.Sql/servers/databases`. Sunmaz `Microsoft.Sql/servers/` hello üst kaynak türünden varsayıldığından. Merhaba alt kaynak adı olarak ayarlanmış çok`exampledatabase` ancak hello tam ad hello üst adı içerir. Sunmaz `exampleserver` hello üst kaynaktan varsayıldığından.

## <a name="top-level-child-resource"></a>Üst düzey alt kaynak
Merhaba en üst düzeyinde hello alt kaynak tanımlayabilirsiniz. Merhaba üst kaynak hello dağıtılmamışsa, bu yaklaşım kullanabilir aynı şablonu veya toouse istiyorsanız `copy` toocreate birden çok alt kaynakları. Bu yaklaşımda, hello tam kaynak türü sağlayın ve hello üst kaynak adı hello alt kaynak adında gerekir.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

aynı hello şablonunda düzey hello üzerinde tanımlı olsa bile hello veritabanı bir alt kaynak toohello sunucusudur.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl hakkında öneriler için bkz: toocreate şablonları [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](resource-manager-template-best-practices.md).
* Birden çok alt kaynakları oluşturma örneği için bkz: [Azure Resource Manager şablonları kaynaklarında birden çok örneğini dağıtmak](resource-group-create-multiple.md).
