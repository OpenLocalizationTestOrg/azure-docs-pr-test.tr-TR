---
title: "aaaManage DNS bölgeleri Azure DNS - Azure CLI 1.0 | Microsoft Docs"
description: "DNS bölgelerini Azure CLI 1.0 kullanarak yönetebilirsiniz. Bu makalede nasıl tooupdate, silme ve Azure DNS üzerinde DNS bölgeleri oluşturma gösterilmektedir."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a>Azure DNS kullanarak toomanage DNS bölgeleri Azure CLI 1.0 nasıl hello

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

Bu kılavuz, nasıl toomanage hello platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanarak DNS bölgeleri gösterir. DNS bölgelerini kullanarak da yönetebilirsiniz [Azure PowerShell](dns-operations-dnszones.md) ya da Azure portal hello.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi

CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için.

## <a name="introduction"></a>Giriş

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a>Yardım alma

TooAzure DNS ile ilgili tüm CLI 1.0 komutları başlayın `azure network dns`. Merhaba kullanan her komut için Yardım kullanılabilir `--help` seçeneği (kısa form `-h`).  Örneğin:

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a>DNS bölgesi oluşturma

Bir DNS bölgesi hello kullanılarak oluşturulan `azure network dns zone create` komutu. Yardım için bkz. `azure network dns zone create -h`.

Merhaba aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* adlı hello kaynak grubunda *MyResourceGroup*:

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>bir DNS bölgesini etiketlerle toocreate

Merhaba aşağıdaki örnekte nasıl toocreate bir DNS bölgesi iki gösterir [Azure Resource Manager etiketlerine](dns-zones-records.md#tags), *proje demo =* ve *env = test*, hello kullanarak `--tags` parametre (kısa form `-t`):

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a>Bir DNS bölgesini alın

bir DNS bölgesi tooretrieve kullanmak `azure network dns zone show`. Yardım için bkz. `azure network dns zone show -h`.

Merhaba aşağıdaki örnek verir hello DNS bölgesi *contoso.com* ve ilişkili verileri kaynak grubundan *MyResourceGroup*. 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

Aşağıdaki örnek hello hello yanıt ' dir.

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

DNS kayıtlarını tarafından döndürülen değil Not `azure network dns zone show`. toolist DNS kayıtlarını kullanmak `azure network dns record-set list`.


## <a name="list-dns-zones"></a>Liste DNS bölgeleri

tooenumerate DNS bölgeleri kullanmak `azure network dns zone list`. Yardım için bkz. `azure network dns zone list -h`.

Belirten hello kaynak grubu yalnızca hello kaynak grubunda bölgelerini listeler:

```azurecli
azure network dns zone list MyResourceGroup
```

Atlama hello kaynak grubu hello Abonelikteki tüm bölgeler listeler:

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a>Bir DNS bölgesini güncelleştirme

DNS bölge kaynak kullanılarak yapılabilir değişiklikleri tooa `azure network dns zone set`. Yardım için bkz. `azure network dns zone set -h`.

Bu komut hello DNS kayıt kümelerini hello bölgedeki hiçbirini güncelleştirmez (bkz [nasıl tooManage DNS kayıtlarını](dns-operations-recordsets-cli-nodejs.md)). Yalnızca kullanılan tooupdate özelliklerini hello bölge kaynağını kendisini olur. Bu özellikleri şu anda sınırlı toohello olan [Azure Resource Manager 'etiketleri'](dns-zones-records.md#tags) hello bölge kaynak için.

Merhaba aşağıdaki örnek bir DNS bölgesinin nasıl tooupdate hello etiketleri gösterir. Merhaba varolan etiketleri belirtilen hello değeriyle değiştirilir.

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a>Bir DNS bölgesi Sil

DNS bölgeleri kullanılarak silinebilir `azure network dns zone delete`. Yardım için bkz. `azure network dns zone delete -h`.

> [!NOTE]
> Bir DNS bölgesi silme hello bölgedeki tüm DNS kayıtlarını siler. Bu işlem geri alınamaz. Merhaba DNS bölgesi kullanımdaysa hello bölge silindiğinde hello bölge kullanarak Hizmetleri başarısız olur.
>
>yanlışlıkla bölge silinmesine karşı tooprotect bkz [nasıl tooprotect DNS bölgeleri ve kayıtları](dns-protect-zones-recordsets.md).

Bu komut onaylamanızı ister. İsteğe bağlı Hello `--quiet` geçiş (kısa form `-q`) bu istemi gizler.

Merhaba aşağıdaki örnekte nasıl toodelete hello bölge gösterir *contoso.com* kaynak grubundan *MyResourceGroup*.

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a>Sonraki adımlar

Nasıl çok öğrenin[kayıt kümelerini ve kayıtları yönetmek](dns-getstarted-create-recordset-cli-nodejs.md) DNS bölgesinde.

Nasıl çok öğrenin[, etki alanı tooAzure DNS temsilci](dns-domain-delegation.md).

