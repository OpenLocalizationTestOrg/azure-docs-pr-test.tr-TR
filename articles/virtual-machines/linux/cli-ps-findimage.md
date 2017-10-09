---
title: "aaaSelect Linux VM görüntüleri hello Azure CLI ile | Microsoft Docs"
description: "Toouse nasıl hello Azure CLI toodetermine hello yayımcı, teklif, SKU ve sürümü Market VM görüntüleri öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a>Nasıl hello Azure CLI ile Azure Marketi hello içinde toofind Linux VM görüntüleri
Bu konuda nasıl toouse hello Azure CLI 2.0 toofind VM görüntüleri hello Azure Marketi açıklanmaktadır. Bir Linux VM oluşturduğunuzda, bu bilgileri toospecify bir Market görüntüsü kullanın.

Merhaba son yüklü olduğundan emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabı günlüğe kaydedilir (`az login`).

## <a name="terminology"></a>Terminoloji

Market görüntülerini hello CLI ve diğer Azure Araçları tooa hiyerarşi göre tanımlanır:

* **Yayımcı** -hello hello görüntüyü oluşturan kuruluş. Örnek: kurallı
* **Teklif** -bir yayımcı tarafından oluşturulan ilgili görüntüler grubudur. Örnek: Ubuntu Server
* **SKU** - bir dağıtım büyük sürümü gibi bir teklif ait bir örnek. Örnek: 16.04-LTS
* **Sürüm** -hello görüntünün SKU sürüm numarası. Merhaba görüntü belirtirken, hangi hello dağıtım en son sürümünü hello seçer hello sürüm numarasıyla "son" değiştirebilirsiniz.

toospecify bir Market görüntüsü, genellikle kullandığınız hello görüntü *URN*. Merhaba URN hello iki nokta üst üste (:) karakteriyle ayrılmış bu değerleri birleştirir: *yayımcı*:*teklif*:*Sku*:*sürüm*. 


## <a name="list-popular-images"></a>Liste popüler görüntüleri

Merhaba çalıştırmak [az vm görüntü listesi](/cli/azure/vm/image#list) hello olmadan komutu `--all` seçeneği, popüler VM listesini görüntüleri hello Azure Marketi toosee. Örneğin, komut toodisplay aşağıdaki hello önbelleğe alınmış popüler görüntüleri listesini tablo biçiminde çalıştırın:

```azurecli
az vm image list --output table
```

Merhaba çıktı hello URN içerir (Merhaba hello değerinde *Urn* sütun), hangi toospecify hello görüntü kullanın. Bir VM Bu popüler Market görüntülerden birini oluştururken, alternatif olarak hello URN diğer gibi belirleyebilirsiniz *UbuntuLTS*.

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a>Belirli görüntüleri bulma

toofind hello Market, belirli bir VM görüntüsündeki kullanmak hello `az vm image list` hello komutunu `--all` seçeneği. Merhaba komutunun bu sürümü, bazı zaman toocomplete alır ve genellikle hello listeyi filtrelemek için uzun çıkış döndürebilirsiniz `--publisher` veya başka bir parametre. 

Örneğin, komutu aşağıdaki hello tüm Debian teklifleri görüntüler (Merhaba unutmayın `--all` geçiş, yalnızca ortak görüntülerinin hello yerel önbelleği arar):

```azurecli
az vm image list --offer Debian --all --output table 

```

Kısmi çıktı: 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

Merhaba ile benzer filtre uygulamak `--location`, `--publisher`, ve `--sku` seçenekleri. Kısmi eşleşmeler arama gibi bir filtre bile gerçekleştirebileceğiniz `--offer Deb` toofind tüm Debian görüntüler.

Belirli bir konuma hello ile belirtmezseniz `--location` seçeneğini hello değerlerini `westus` varsayılan olarak döndürülür. (Çalıştırarak farklı varsayılan konumunu ayarla `az configure --defaults location=<location>`.)

Örneğin, tüm Debian 8 SKU'ları, komutu aşağıdaki hello listeler `westeurope`:

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

Kısmi çıktı:

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-hello-images"></a>Merhaba görüntüleri gidin 
Başka bir şekilde toofind görüntünün bir konumda toorun hello olan [az vm görüntü listesi-yayımcılar](/cli/azure/vm/image#list-publishers), [az vm görüntü listesi-teklifleri](/cli/azure/vm/image#list-offers), ve [az vm görüntü listesi-SKU'ları](/cli/azure/vm/image#list-skus) komutları sırayla. Bu komutları ile bu değerler belirler:

1. Liste hello görüntü yayımcılar.
2. Belirli bir yayımcı varsa yayımcının tekliflerini listeleyin.
3. Belirli bir teklif varsa SKU’larını listeleyin.


Örneğin, hello aşağıdaki komut hello Batı ABD konumu hello görüntü yayımcıları listeler:

```azurecli
az vm image list-publishers --location westus --output table
```

Kısmi çıktı:

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
Bu bilgi toofind belirli bir yayımcıdan sunar kullanın. Canonical hello Batı ABD konumu görüntü Publisher'da ise, örneğin, kendi teklifleri çalıştırarak bulabileceğiniz `azure vm image list-offers`. Merhaba konumunu ve örnek aşağıdaki hello olduğu gibi hello yayımcı geçirin:

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

Çıktı:

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
Merhaba Batı ABD bölgesinde hello Canonical yayımlar gördüğünüz **UbuntuServer** Azure üzerinde sunar. Ancak hangi SKU'ları? Bu değerleri tooget çalıştırmak `azure vm image list-skus` ve hello konumu, yayımcı ve bulunan teklif ayarlayın:

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

Çıktı:

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

Son olarak, hello kullan `az vm image list` komutu toofind hello SKU istediğiniz, örneğin, belirli bir sürümünü **16.04 LTS**:

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

Çıktı:

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a>Sonraki adımlar
Tam olarak hello görüntüsünü seçebilirsiniz artık alma Not hello URN değeri tarafından toouse istiyor. Bu değeri hello ile geçirmek `--image` bir VM ile Merhaba oluşturduğunuzda parametresi [az vm oluşturma](/cli/azure/vm#create) komutu. "Son" Merhaba URN hello sürüm numarası isteğe bağlı olarak değiştirebilirsiniz unutmayın. Bu her zaman en son sürümünü hello dağıtım hello sürümüdür. toocreate hello URN bilgileri kullanarak hızlı bir şekilde bir sanal makine bkz [oluşturma ve yönetme Linux VM'ler hello Azure CLI ile](tutorial-manage-vm.md).
