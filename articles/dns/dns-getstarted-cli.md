---
title: "aaaGet Azure Azure CLI 2.0 kullanarak DNS ile başlatılan | Microsoft Docs"
description: "Bilgi nasıl toocreate bir DNS bölgesi ve Azure DNS kaydında. Bu adım adım kılavuzu toocreate ve ilk DNS bölgesi ve kayıt hello Azure CLI 2.0 kullanarak yönetin."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a>Azure CLI 2.0 kullanarak Azure DNS ile çalışmaya başlama

> [!div class="op_single_selector"]
> * [Azure Portal](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

Bu makalede ilk DNS bölgenizi hello adımları toocreate anlatılmaktadır ve kaydını kullanarak hello platformlar arası Azure CLI 2.0, Windows, Mac ve Linux için kullanılabilir. Hello Azure portalında veya Azure PowerShell kullanarak aşağıdaki adımları de gerçekleştirebilirsiniz.

Bir DNS bölgesi belirli bir etki alanı için kullanılan toohost hello DNS kayıtlarını ' dir. Azure DNS, etki alanınızda barındırma toostart toocreate bir DNS bölgesi için o etki alanı adı gerekiyor. Ardından bu DNS bölgesinde etki alanınız için tüm DNS kayıtları oluşturulur. Son olarak, toopublish, DNS bölge toohello Internet tooconfigure hello ad sunucuları hello etki alanı için gerekir. Bu adımların her biri aşağıda açıklanmıştır.

Bu yönergeler, zaten yüklü ve tooAzure CLI 2.0 imzalı varsayalım. Yardım için bkz. [nasıl Azure CLI 2.0 kullanan toomanage DNS bölgeleri](dns-operations-dnszones-cli.md).

## <a name="create-hello-resource-group"></a>Merhaba kaynak grubu oluştur

Merhaba DNS bölgesi oluşturmadan önce bir kaynak grubu toocontain hello DNS bölgesi oluşturulur. Merhaba aşağıdaki hello komut gösterir.

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a>DNS bölgesi oluşturma

Bir DNS bölgesi hello kullanılarak oluşturulan `az network dns zone create` komutu. Bu komutun toosee yardımını yazın `az network dns zone create -h`.

Merhaba aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* hello kaynak grubunda *MyResourceGroup*. Merhaba örnek toocreate bir DNS bölgesi Hello değerleri kendinizinkilerle değiştirerek kullanın.

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a>DNS kaydı oluşturma

toocreate bir DNS kaydı kullanmak hello `az network dns record-set [record type] add-record` komutu. Örneğin, A kayıtlarına ilişkin yardım için bkz. `azure network dns record-set A add-record -h`.

Merhaba aşağıdaki örnekte bir kayıt hello göreli adı "www" hello "contoso.com", "Contoso.com" kaynak grubunda DNS bölgesi içinde oluşturur. Merhaba tam hello kayıt kümesi "www.contoso.com" adıdır. Merhaba kayıt türü "A", "1.2.3.4" IP adresiyle olduğundan ve varsayılan TTL 3600 saniye (1 saat) kullanılır.

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

Alternatif TTL değerleri ve toomodify mevcut kayıtları için birden fazla kayıtla kayıt kümeleri için diğer kayıt türleri için bkz: [yönetmek DNS kayıtlarını ve kayıt kümelerini kullanarak hello Azure CLI 2.0](dns-operations-recordsets-cli.md).


## <a name="view-records"></a>Kayıtları görüntüleme

toolist hello DNS kayıtları, bölge içindeki kullanın:

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a>Ad sunucularını güncelleştirme

Sonra DNS bölgesi ve kayıtları doğru şekilde ayarlanan, tooconfigure gerek memnun, etki alanı adı toouse hello Azure DNS ad sunucuları. Bu DNS kayıtlarınızı hello Internet toofind üzerindeki diğer kullanıcılarla sağlar.

Merhaba bölgenizin ad sunucuları tarafından hello verilen `az network dns zone show` komutu. toosee hello ad sunucusu adlarını hello aşağıdaki örnekte gösterildiği gibi JSON çıkışını kullanın.

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Bu ad sunucuları hello etki alanı adı kayıt (Merhaba etki alanı adı satın aldığınız yerden) ile yapılandırılmalıdır. Şirketiniz hello seçeneği tooset hello ad sunucuları hello etki alanı için yukarı sunar. Daha fazla bilgi için bkz: [, etki alanı tooAzure DNS temsilci](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Tüm kaynakları silme
 
Bu makalede, adım aşağıdaki Al hello oluşturulan tüm kaynakları toodelete:

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Azure DNS hakkında daha fazla toolearn bkz [Azure DNS'ye genel bakış](dns-overview.md).

Azure DNS'de DNS bölgelerini yönetme hakkında daha fazla toolearn bkz [yönetmek DNS bölgeleri Azure CLI 2.0 kullanan Azure DNS'de](dns-operations-dnszones-cli.md).

Azure DNS'de DNS kayıtlarını yönetme hakkında daha fazla toolearn bkz [yönetmek DNS kayıtlarını ve kayıt kümelerini Azure CLI 2.0 kullanan Azure DNS'de](dns-operations-recordsets-cli.md).
