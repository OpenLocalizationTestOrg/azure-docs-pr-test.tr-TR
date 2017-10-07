---
title: "aaaManage DNS bölgeleri Azure DNS - Azure CLI 2.0 | Microsoft Docs"
description: "DNS bölgelerini Azure CLI 2.0 kullanarak yönetebilirsiniz. Bu makalede nasıl tooupdate, silme ve Azure DNS üzerinde DNS bölgeleri oluşturma gösterilmektedir."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a>Azure DNS kullanarak toomanage DNS bölgeleri Azure CLI 2.0 nasıl hello

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)


Bu kılavuz, Windows, Mac ve Linux için kullanılabilir olduğu hello platformlar arası Azure CLI kullanarak DNS sunucunuzun nasıl toomanage bölgeleri gösterir. DNS bölgelerini kullanarak da yönetebilirsiniz [Azure PowerShell](dns-operations-dnszones.md) ya da Azure portal hello.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi

CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için.

## <a name="introduction"></a>Giriş

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>Azure DNS için Azure CLI 2.0'ı ayarlama

### <a name="before-you-begin"></a>Başlamadan önce

Yapılandırmanıza başlamadan önce aşağıdaki öğelerindeki hello sahip olduğunuzu doğrulayın.

* Azure aboneliği. Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.

* Merhaba hello Azure CLI 2.0, Windows, Linux veya Mac için kullanılabilir en son sürümünü yükleyin Daha fazla bilgi için bkz. [yükleme hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

### <a name="sign-in-tooyour-azure-account"></a>Azure hesabı tooyour içinde oturum

Bir konsol penceresi açın ve kimlik bilgilerinizi girerek kimliğinizi doğrulayın. Daha fazla bilgi için bkz: günlük hello Azure CLI gelen tooAzure içinde

```
az login
```

### <a name="select-hello-subscription"></a>Merhaba aboneliği seçin

Merhaba hesabının Hello abonelikleri kontrol edin.

```
az account list
```

Azure abonelikleri toouse hangisinin seçin.

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır. Ancak, tüm DNS kaynakları global olduğundan, bölgesel değil, kaynak grubu konumu hello seçimine Azure DNS üzerinde hiçbir etkisi olmaz.

Var olan bir kaynak grubunu kullanıyorsanız bu adımı atlayabilirsiniz.

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>Yardım alma

TooAzure DNS ile ilgili tüm CLI 2.0 komutları başlayın `az network dns`. Merhaba kullanan her komut için Yardım kullanılabilir `--help` seçeneği (kısa form `-h`).  Örneğin:

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>DNS bölgesi oluşturma

Bir DNS bölgesi hello kullanılarak oluşturulan `az network dns zone create` komutu. Yardım için bkz. `az network dns zone create -h`.

Merhaba aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* adlı hello kaynak grubunda *MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>bir DNS bölgesini etiketlerle toocreate

Merhaba aşağıdaki örnekte nasıl toocreate bir DNS bölgesi iki gösterir [Azure Resource Manager etiketlerine](dns-zones-records.md#tags), *proje demo =* ve *env = test*, hello kullanarak `--tags` parametre (kısa form `-t`):

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>Bir DNS bölgesini alın

bir DNS bölgesi tooretrieve kullanmak `az network dns zone show`. Yardım için bkz. `az network dns zone show --help`.

Merhaba aşağıdaki örnek verir hello DNS bölgesi *contoso.com* ve ilişkili verileri kaynak grubundan *MyResourceGroup*. 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

Aşağıdaki örnek hello hello yanıt ' dir.

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

DNS kayıtlarını tarafından döndürülen değil Not `az network dns zone show`. toolist DNS kayıtlarını kullanmak `az network dns record-set list`.


## <a name="list-dns-zones"></a>Liste DNS bölgeleri

tooenumerate DNS bölgeleri kullanmak `az network dns zone list`. Yardım için bkz. `az network dns zone list --help`.

Belirten hello kaynak grubu yalnızca hello kaynak grubunda bölgelerini listeler:

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

Atlama hello kaynak grubu hello Abonelikteki tüm bölgeler listeler:

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>Bir DNS bölgesini güncelleştirme

DNS bölge kaynak kullanılarak yapılabilir değişiklikleri tooa `az network dns zone update`. Yardım için bkz. `az network dns zone update --help`.

Bu komut hello DNS kayıt kümelerini hello bölgedeki hiçbirini güncelleştirmez (bkz [nasıl tooManage DNS kayıtlarını](dns-operations-recordsets-cli.md)). Yalnızca kullanılan tooupdate özelliklerini hello bölge kaynağını kendisini olur. Bu özellikleri şu anda sınırlı toohello olan [Azure Resource Manager 'etiketleri'](dns-zones-records.md#tags) hello bölge kaynak için.

Merhaba aşağıdaki örnek bir DNS bölgesinin nasıl tooupdate hello etiketleri gösterir. Merhaba varolan etiketleri belirtilen hello değeriyle değiştirilir.

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>Bir DNS bölgesi Sil

DNS bölgeleri kullanılarak silinebilir `az network dns zone delete`. Yardım için bkz. `az network dns zone delete --help`.

> [!NOTE]
> Bir DNS bölgesi silme hello bölgedeki tüm DNS kayıtlarını siler. Bu işlem geri alınamaz. Merhaba DNS bölgesi kullanımdaysa hello bölge silindiğinde hello bölge kullanarak Hizmetleri başarısız olur.
>
>yanlışlıkla bölge silinmesine karşı tooprotect bkz [nasıl tooprotect DNS bölgeleri ve kayıtları](dns-protect-zones-recordsets.md).

Bu komut onaylamanızı ister. İsteğe bağlı Hello `--yes` anahtar bu istemi gizler.

Merhaba aşağıdaki örnekte nasıl toodelete hello bölge gösterir *contoso.com* kaynak grubundan *MyResourceGroup*.

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>Sonraki adımlar

Nasıl çok öğrenin[kayıt kümelerini ve kayıtları yönetmek](dns-getstarted-create-recordset-cli.md) DNS bölgesinde.

Nasıl çok öğrenin[, etki alanı tooAzure DNS temsilci](dns-domain-delegation.md).

