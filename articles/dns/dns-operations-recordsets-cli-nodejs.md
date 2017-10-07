---
title: "Azure DNS kullanarak aaaManage DNS kayıtları hello Azure CLI 1.0 | Microsoft Docs"
description: "DNS kayıt kümelerini ve Azure DNS kayıtlarını Azure DNS'nin etki alanınızda barındırdığında yönetme. Kayıt kümelerini ve kayıtları işlemleri için tüm CLI 1.0 komutları."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 1f01450b0839f712cb1d96be318766bac581fea1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-in-azure-dns-using-hello-azure-cli-10"></a>Hello Azure CLI 1.0 kullanarak Azure DNS'de DNS kayıtlarını yönetme

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Bu makalede nasıl toomanage DNS kayıtları kullanarak DNS bölgenizi için platformlar arası Azure komut satırı Windows, Mac ve Linux için kullanılabilir olan arabirimi (CLI) hello gösterilmektedir. DNS kayıtlarınızı kullanarak da yönetebilirsiniz [Azure PowerShell](dns-operations-recordsets.md) veya hello [Azure portal](dns-operations-recordsets-portal.md).

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi

CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

* [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için.
* [Azure CLI 2.0](dns-operations-recordsets-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için.

Bu makaledeki Hello örnekler, zaten sahip olduğunuzu varsayar [Merhaba, oturum açan Azure CLI 1.0 yüklü ve bir DNS bölgesi oluşturulan](dns-operations-dnszones-cli-nodejs.md).

## <a name="introduction"></a>Giriş

Azure DNS'de DNS kayıtlarını oluşturmadan önce ilk toounderstand ihtiyacınız nasıl Azure DNS DNS kayıtlarını DNS kayıt kümeleri halinde düzenler.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Azure DNS’deki DNS kayıtları hakkında daha fazla bilgi için bkz. [DNS bölgeleri ve kayıtları](dns-zones-records.md).

## <a name="create-a-dns-record"></a>DNS kaydı oluşturma

toocreate bir DNS kaydı kullanmak hello `azure network dns record-set add-record` komutu. Yardım için bkz. `azure network dns record-set add-record -h`.

Bir kayıt oluştururken, toospecify hello kaynak grubu adı, bölge adı gerekiyor, kayıt adı, hello kayıt türünü ve hello oluşturulmakta hello kaydın ayrıntılarını ayarlayın. Merhaba verilen kayıt kümesi adı olmalıdır bir *göreli* adı, hello bölge adı dışarıda gerekir anlamına gelir.

Merhaba kayıt kümesi zaten mevcut değilse, bu komutu, sizin için oluşturur. Merhaba kayıt kümesi zaten varsa, bu komutu olan hello kayıt toohello varolan bir kayıt kümesini belirtin.

Yeni bir kayıt kümesi oluşturuluyorsa yaşam süresi (TTL) olarak varsayılan 3600 değeri kullanılır. Yönergeler için nasıl toouse farklı TTLs bkz [DNS kayıt kümesi oluşturma](#create-a-dns-record-set).

Merhaba aşağıdaki örnekte oluşturur adlı bir A kaydı *www* hello bölgesinde *contoso.com* hello kaynak grubunda *MyResourceGroup*. Merhaba bir kayıttır hello IP adresini *1.2.3.4*.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

toocreate hello hello bölge tepesinde bir kayıt (Bu durumda, "contoso.com"), hello kayıt adını kullanın "@", hello tırnak işaretleri dahil olmak üzere:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a>DNS kayıt kümesi oluşturma

Örnekleri yukarıda Hello hello DNS kayıt kayıt kümesinde varolan ya da eklenen tooan olduğundan veya hello kayıt kümesi oluşturuldu *örtük olarak*. Merhaba kayıt kümesi de oluşturabilirsiniz *açıkça* önce ekleme tooit kaydeder. Azure DNS, DNS kayıtlarını oluşturmadan önce bir DNS adı bir yer tutucu tooreserve çalışabilmek için 'empty' kayıt kümelerini destekler. Boş kaydı kümeleri Azure DNS düzlemi denetlemek, ancak hello Azure DNS ad sunucuları üzerinde görünmeyen hello görünür.

Kayıt kümeleri hello kullanarak oluşturulur `azure network dns record-set create` komutu. Yardım için bkz. `azure network dns record-set create -h`.

Merhaba kayıt açıkça kümesi oluşturma verir hello gibi toospecify kayıt kümesi özellikleri [yaşam süresi (TTL)](dns-zones-records.md#time-to-live) ve meta verileri. [Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) anahtar-değer çiftleri olarak her bir kayıt kümesi ile kullanılan tooassociate uygulamaya özgü verileri olabilir.

Merhaba aşağıdaki örnekte oluşturur boş bir kayıt hello kullanarak 60 saniye TTL ile kümesi `--ttl` parametre (kısa form `-l`):

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

Merhaba aşağıdaki örnekte iki meta veri girişi ile ayarlanmış bir kayıt oluşturur "Bölüm Finans =" ve "ortam üretim =", hello kullanarak `--metadata` parametre (kısa form `-m`):

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

Boş bir kayıt kümesi oluşturulduktan sonra kayıtları kullanılarak eklenebilir `azure network dns record-set add-record` açıklandığı gibi [bir DNS kaydı oluşturma](#create-a-dns-record).

## <a name="create-records-of-other-types"></a>Diğer türleri kayıtları oluşturma

Ayrıntılı olarak nasıl toocreate 'A' kaydeder, Azure DNS tarafından nasıl toocreate kayıt diğer kayıt türlerinin desteklenen örneklerde aşağıdaki hello görülen.

Merhaba parametreleri veri hello kayıt hello türüne bağlı olarak farklılık toospecify hello kaydı için kullanılmış. Örneğin, için bir kayıt türü "A" Merhaba IPv4 adresi hello parametresiyle belirttiğiniz `-a <IPv4 address>`. Her bir kayıt türü kullanılarak listelenebilir için parametreleri Hello `azure network dns record-set add-record -h`.

Her durumda, gösteriyoruz nasıl toocreate tek bir kaydı. kayıt kümesi varolan eklenen toohello Hello kaydıdır veya bir kayıt kümesini örtük olarak oluşturulmuş. Kayıt kümeleri oluşturma ve kayıt tanımlama hakkında daha fazla bilgi için parametre açıkça, bakın [DNS kayıt kümesi oluşturma](#create-a-dns-record-set).

SOAs oluşturulduğundan bir örnek toocreate bir SOA kayıt kümesi sunuyoruz değil ve her DNS bölge ile silinmiş ve oluşturulamaz veya ayrı olarak silinir. Ancak, [SOA değiştirilebilir, bir sonraki örnekte gösterildiği gibi hello](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record"></a>Bir AAAA kaydı oluşturun

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a>Bir CNAME kaydı oluşturun

> [!NOTE]
> Merhaba DNS standartlarında izin vermiyor CNAME kayıtları hello bir bölgenin tepesinde (`-Name "@"`), ya da birden çok kayıt içeren kayıt kümeleri izin yapın.
> 
> Daha fazla bilgi için bkz: [CNAME kayıtları](dns-zones-records.md#cname-records).

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a>MX kaydı oluşturma

Bu örnekte, hello kayıt kümesi adını kullanıyoruz "@" toocreate hello MX kaydı hello bölge tepesinde (Bu durumda, "contoso.com").

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a>Bir NS kayıt oluşturma

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a>PTR kaydı oluştur

Bu durumda, ' my-arpa-zone.com' hello IP aralığınızı temsil eden ARPA bölge temsil eder. Bu bölgede ayarlamak her PTR kaydı tooan IP adresi bu IP aralığı içinde karşılık gelir.  Merhaba kaydı '10' hello IP adresinin bu kayıt tarafından temsil edilen bu IP aralığı içinde son sekizlisi hello adıdır.

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a>Bir SRV kaydı oluşturun

Oluştururken bir [SRV kayıt kümesi](dns-zones-records.md#srv-records), hello belirtin  *\_hizmet* ve  *\_Protokolü* hello kayıt kümesi adı. Hiçbir gerek tooinclude yok "@" hello kayıt kümesi adı bir SRV kaydı kümesi hello bölgenin tepesinde oluştururken.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a>TXT kaydı oluşturma

Merhaba aşağıdaki örnekte nasıl toocreate bir TXT kaydı gösterilmektedir. TXT kayıtlarının desteklenen hello maksimum dize uzunluğu hakkında daha fazla bilgi için bkz: [TXT kayıtlarının](dns-zones-records.md#txt-records).

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a>Bir kayıt kümesini Al

tooretrieve varolan bir kayıt kümesini kullanma `azure network dns record-set show`. Yardım için bkz. `azure network dns record-set show -h`.

Bir kayıt veya kayıt kümesi oluştururken, hello kayıt kümesinin adı verilen olarak olmalıdır bir *göreli* adı, hello bölge adı dışarıda gerekir anlamına gelir. Toospecify hello kayıt türü de gerekir, hello kayıt içeren hello bölge ayarlamak ve hello bölge içeren kaynak grubunu hello.

Merhaba aşağıdaki örnek hello kaydı alır *www* bölgeden türü a *contoso.com* kaynak grubunda *MyResourceGroup*:

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a>Liste kayıt kümeleri

Hello kullanarak bir DNS bölgedeki tüm kayıtları listeleyebilirsiniz `azure network dns record-set list` komutu. Yardım için bkz. `azure network dns record-set list -h`.

Bu örnekte tüm kayıt kümeleri hello bölgesinde döndürür *contoso.com*, kaynak grubundaki *MyResourceGroup*, adı veya kayıt türü ne olursa olsun:

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

Bu örnek kayıt türü (Bu durumda, 'Bir' kayıtları) verilen hello eşleşen tüm kayıt kümelerinin döndürür:

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-tooan-existing-record-set"></a>Kayıt kümesi varolan bir kayıt tooan Ekle

Kullanabileceğiniz `azure network dns record-set add-record` hem yeni bir kayıt kaydında toocreate ayarlayın veya kayıt tooan varolan bir kaydı tooadd ayarlayın.

Daha fazla bilgi için bkz: [bir DNS kaydı oluşturma](#create-a-dns-record) ve [kayıtlar diğer türleri oluşturma](#create-records-of-other-types) üstünde.

## <a name="remove-a-record-from-an-existing-record-set"></a>Varolan bir kayıt kümesinden bir kaydı kaldırma.

tooremove bir DNS kaydı varolan kayıt kümesinden, kullanım `azure network dns record-set delete-record`. Yardım için bkz. `azure network dns record-set delete-record -h`.

Bu komut, kayıt kümesindeki bir DNS kaydı siler. Bir kayıt kümesindeki Hello son kaydı silinirse, kendisini ayarlamak hello kaydıdır **değil** silindi. Bunun yerine, boş bir kayıt kümesi bırakılır. Bunun yerine, ayarlamak toodelete hello kaydını görmek [bir kayıt kümesini Sil](#delete-a-record-set).

Toospecify ihtiyacınız hello kayıt toobe silinmiş ve onu silinmesi, kullanarak hello bölge kayıt kullanarak oluştururken, aynı parametreleri hello `azure network dns record-set add-record`. Bu parametreler açıklanmaktadır [bir DNS kaydı oluşturma](#create-a-dns-record) ve [kayıtlar diğer türleri oluşturma](#create-records-of-other-types) üstünde.

Bu komut onaylamanızı ister. Bu istemi hello kullanılarak gizlenebilir `--quiet` geçiş (kısa form `-q`).

Aşağıdaki örnek siler hello hello hello kaydından ' 1.2.3.4 adlandırılmış kümesi' içeren bir kaydı *www* hello bölgesinde *contoso.com*, hello kaynak grubunda *MyResourceGroup*. Merhaba onay istemi engellenir.

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a>Varolan bir kayıt kümesini değiştirme

Her bir kayıt kümesi içeren bir [yaşam süresi (TTL)](dns-zones-records.md#time-to-live), [meta veri](dns-zones-records.md#tags-and-metadata)ve DNS kayıtlarını. Merhaba aşağıdaki bölümlerde açıklanmıştır nasıl toomodify her bu özelliklerin.

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a>toomodify bir A, AAAA, MX, NS, PTR, SRV ve TXT kaydı

var olan bir tür A, AAAA, MX, NS, PTR, SRV ve TXT kaydını toomodify, yeni bir kayıt ve ardından silme hello varolan kaydı ilk eklemeniz gerekir. Ayrıntılı yönergeler için toodelete ve kayıtları eklemek için bkz: Merhaba bu makalenin önceki bölümlerinde.

Aşağıdaki örneğine hello nasıl toomodify bir 'A' kaydından IP adresi 1.2.3.4 tooIP adres 5.6.7.8 gösterir:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="toomodify-a-cname-record"></a>toomodify bir CNAME kaydı

toomodify bir CNAME kaydı kullanmak `azure network dns record-set add-record` tooadd hello yeni bir kayıt değeri. Diğer kayıt türlerinin aksine, bir CNAME kayıt kümesi yalnızca tek bir kaydını içerebilir. Bu nedenle, hello varolan kaydıdır *yerini* zaman hello yeni kayıt eklenir ve ayrı ayrı silinmiş toobe gerekli değildir.  Bu değişiklik istendiğinde tooaccept olacaktır.

Merhaba örnek değiştirir hello CNAME kayıt kümesi *www* hello bölgesinde *contoso.com*, kaynak grubundaki *MyResourceGroup*, toopoint çok yerine ' www.fabrikam.net' kendi Mevcut değer:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a>toomodify bir SOA kaydı

Kullanım `azure network dns record-set set-soa-record` belirli bir DNS bölgesi için toomodify hello SOA. Yardım için bkz. `azure network dns record-set set-soa-record -h`.

Merhaba aşağıdaki örnekte nasıl hello SOA tooset hello 'e-posta' özelliği kayıt hello bölgenin gösterir *contoso.com* hello kaynak grubunda *MyResourceGroup*:

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="toomodify-ns-records-at-hello-zone-apex"></a>Merhaba bölge tepesinde toomodify NS kayıtları

Merhaba NS kayıt Hello bölgenin tepesinde kümesi her DNS bölge ile otomatik olarak oluşturulur. Hello Azure DNS ad sunucuları atanan toohello bölgesi hello adlarını içerir.

Ek ad sunucuları toothis NS kayıt kümesi, etki alanları birden fazla DNS sağlayıcınız ile birlikte barındırma toosupport ekleyebilirsiniz. Merhaba TTL ve bu kayıt kümesi için meta verileri de değiştirebilirsiniz. Ancak, kaldırmak veya hello önceden doldurulmuş haldedir Azure DNS ad sunucuları değiştirin.

Bu yalnızca toohello NS kayıt kümesi hello bölge tepesinde en geçerli olduğunu unutmayın. Diğer NS kayıt kümelerinde bölgenizi (olarak kullanılan toodelegate alt bölgeler) kısıtlama değiştirilebilir.

Aşağıdaki örneğine hello tooadd bir ek ad sunucusu toohello NS kaydı hello bölgenin tepesinde nasıl ayarlanacağını gösterir:

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a>toomodify hello varolan bir kaydı TTL Ayarla

Varolan bir kaydı TTL toomodify hello ayarlayabilir, kullanabilir `azure network dns record-set set`. Yardım için bkz. `azure network dns record-set set -h`.

Aşağıdaki örnek hello nasıl toomodify kayıt kümesi TTL, bu durumda too60 saniye gösterir:

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a>Varolan bir kayıt kümesini toomodify hello meta verileri

[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) anahtar-değer çiftleri olarak her bir kayıt kümesi ile kullanılan tooassociate uygulamaya özgü verileri olabilir. Varolan bir kaydı toomodify hello meta verileri ayarlama, kullanın `azure network dns record-set set`. Yardım için bkz. `azure network dns record-set set -h`.

Merhaba aşağıdaki örnek toomodify kayıt iki meta veri girişi ile nasıl ayarlanacağını gösterir "Bölüm Finans =" ve "ortam üretim =", hello kullanarak `--metadata` parametre (kısa form `-m`). Var olan herhangi bir meta veri olduğuna dikkat edin *yerini* verilen hello değerlere göre.

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a>Bir kayıt kümesini Sil

Kayıt kümeleri hello kullanarak silinebilir `azure network dns record-set delete` komutu. Yardım için bkz. `azure network dns record-set delete -h`. Kayıt kümesi siliniyor hello kayıt kümesi içindeki tüm kayıtları siler.

> [!NOTE]
> Merhaba SOA ve NS kayıt kümelerini hello bölge tepesinde adresindeki silemezsiniz (`-Name "@"`).  Bu, ne zaman hello bölge oluşturuldu ve hello bölge silindiğinde otomatik olarak silinir otomatik olarak oluşturulur.

Merhaba aşağıdaki örnek siler hello kayıt adlandırılmış kümesi *www* hello bölgeden türü a *contoso.com* kaynak grubunda *MyResourceGroup*:

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

İstendiğinde tooconfirm hello silme işlemi var. Bu komut istemi toosuppress hello kullanmak `--quiet` geçiş (kısa form `-q`).

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi edinmek [bölgeleri ve Azure DNS kayıtlarında](dns-zones-records.md).
<br>
Nasıl çok öğrenin[bölgeleri ve kayıtları korumak](dns-protect-zones-recordsets.md) Azure DNS kullanırken.
