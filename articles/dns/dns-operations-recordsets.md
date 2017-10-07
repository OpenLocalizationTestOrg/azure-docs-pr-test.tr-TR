---
title: "aaaManage DNS kayıtları Azure PowerShell kullanarak Azure DNS'de | Microsoft Docs"
description: "DNS kayıt kümelerini ve Azure DNS kayıtlarını Azure DNS'nin etki alanınızda barındırdığında yönetme. Kayıt kümelerini ve kayıtları işlemleri için tüm PowerShell komutları."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a>DNS kayıtlarını ve kayıt kümeleri Azure PowerShell kullanarak Azure DNS'de yönetme

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Bu makalede, Azure PowerShell kullanarak DNS bölgesi için kayıt toomanage DNS kayıtları gösterilmektedir. DNS kayıtlarını da yönetilebilir hello platformlar arası kullanarak [Azure CLI](dns-operations-recordsets-cli.md) veya hello [Azure portal](dns-operations-recordsets-portal.md).

Bu makaledeki Hello örnekler, zaten sahip olduğunuzu varsayar [, oturum açan Azure PowerShell yüklenmiş ve bir DNS bölgesi oluşturulan](dns-operations-dnszones.md).

## <a name="introduction"></a>Giriş

Azure DNS'de DNS kayıtlarını oluşturmadan önce ilk toounderstand ihtiyacınız nasıl Azure DNS DNS kayıtlarını DNS kayıt kümeleri halinde düzenler.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Azure DNS’deki DNS kayıtları hakkında daha fazla bilgi için bkz. [DNS bölgeleri ve kayıtları](dns-zones-records.md).


## <a name="create-a-new-dns-record"></a>Yeni bir DNS kaydı oluşturun

Aynı ad ve tür var olan bir kaydı hello yeni kaydınız varsa, çok ihtiyacınız[toohello varolan bir kayıt kümesini eklemek](#add-a-record-to-an-existing-record-set). Yeni kaydınız kayıtları varolan farklı bir ad ve tür tooall varsa toocreate yeni bir kayıt kümesi gerekir. 

### <a name="create-a-records-in-a-new-record-set"></a>Yeni bir kayıt kümesinde 'Bir' kayıtları oluşturma

Hello kullanarak kayıt kümeleri oluşturma `New-AzureRmDnsRecordSet` cmdlet'i. Kayıt kümesi oluştururken, gereksinim duyduğunuz toospecify hello kayıt kümesi adı, hello bölge, toolive (TTL), hello kayıt türünü ve hello kayıtları toobe oluşturulan hello zamanı.

kayıtları tooa kayıt kümesi eklemek için hello parametreler hello kayıt kümesi hello türüne bağlı olarak değişir. Örneğin, 'A' türündeki kayıt kümesini kullanırken hello parametresini kullanarak toospecify başlangıç IP adresi ihtiyacınız `-IPv4Address`. Diğer parametreler diğer kayıt türleri için kullanılır. Bkz: [ek kayıt türü örnekleri](#additional-record-type-examples) Ayrıntılar için.

Merhaba aşağıdaki örnek bir kayıt hello göreli adlı hello "contoso.com" DNS bölgesi içinde ' www' kümesi oluşturur. Merhaba tam hello kayıt kümesinin 'www.contoso.com' adıdır. 'A' Hello kayıt türü olan ve hello TTL 3600 saniyedir. Merhaba kayıt kümesi '1.2.3.4' IP adresiyle tek bir kayıt içerir.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

toocreate bir kayıt kümesinin bir bölge ' tepesinde' hello (Bu durumda, "contoso.com"), hello kayıt kümesi adını kullan ' @' (tırnak işaretleri hariç):

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

Bir kayıt kümesinin birden çok kayıt içeren toocreate gerekiyorsa, önce yerel bir dizi oluşturup hello kayıtları ekleyin, ardından hello dizi çok geçirmek`New-AzureRmDnsRecordSet` gibi:

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) anahtar-değer çiftleri olarak her bir kayıt kümesi ile kullanılan tooassociate uygulamaya özgü verileri olabilir. Merhaba aşağıdaki örnek toocreate kayıt iki meta veri girişi ile nasıl ayarlanacağını gösterir ' bölüm Finans =' ve ' ortam Üretim ='.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

Azure DNS, ayrıca DNS kayıtlarını oluşturmadan önce bir DNS adı bir yer tutucu tooreserve çalışabilmek için 'empty' kayıt kümelerini destekler. Boş kaydı kümeleri hello Azure DNS denetim düzlemi görünür, ancak hello Azure DNS ad sunucuları üzerinde görüntülenir. Aşağıdaki örnek hello boş bir kayıt kümesi oluşturur:

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a>Diğer türleri kayıtları oluşturma

Ayrıntılı olarak nasıl toocreate 'A' kayıtları, aşağıdaki örneklerde gösterildiği nasıl toocreate kayıtları, diğer kayıt türleri Azure DNS sunucuları tarafından desteklenen hello görülen.

Her durumda, tek bir kayıt içeren bir kayıt toocreate nasıl ayarlanacağını gösterir. Merhaba önceki örnekler 'Bir' kayıtları için meta veriler ile birden çok kayıt içeren diğer türleri kayıt kümelerini uyarlanmış toocreate olabilir veya toocreate boş kaydı ayarlar.

SOAs oluşturulduğundan bir örnek toocreate bir SOA kayıt kümesi sunuyoruz değil ve her DNS bölge ile silinmiş ve oluşturulamaz veya ayrı olarak silinir. Ancak, [SOA değiştirilebilir, bir sonraki örnekte gösterildiği gibi hello](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record-set-with-a-single-record"></a>Tek kayıtlı bir AAAA kayıt kümesi oluşturma

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a>Tek kayıtlı bir CNAME kayıt kümesi oluşturma

> [!NOTE]
> Merhaba DNS standartlarında izin vermiyor CNAME kayıtları hello bir bölgenin tepesinde (`-Name '@'`), ya da birden çok kayıt içeren kayıt kümeleri izin yapın.
> 
> Daha fazla bilgi için bkz: [CNAME kayıtları](dns-zones-records.md#cname-records).


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a>Tek kayıtlı bir MX kayıt kümesi oluşturma

Bu örnekte, hello kayıt kümesi adını kullanıyoruz ' @' toocreate bir MX kaydı hello bölge tepesinde (Bu durumda, "contoso.com").


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a>Tek kayıtlı bir NS kayıt kümesi oluşturma

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a>Tek kayıtlı bir PTR kaydı kümesi oluşturma

Bu durumda, ' my-arpa-zone.com' hello IP aralığınızı temsil eden ARPA geriye doğru arama bölgesi temsil eder. Bu bölgede ayarlamak her PTR kaydı tooan IP adresi bu IP aralığı içinde karşılık gelir. Merhaba kaydı '10' hello IP adresinin bu kayıt tarafından temsil edilen bu IP aralığı içinde son sekizlisi hello adıdır.

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a>Tek kayıtlı bir SRV kayıt kümesi oluşturma

Oluştururken bir [SRV kayıt kümesi](dns-zones-records.md#srv-records), hello belirtin  *\_hizmet* ve  *\_Protokolü* hello kayıt kümesi adı. Hiçbir gerek tooinclude yok ' @' hello kayıt kümesi adı bir SRV kaydı kümesi hello bölgenin tepesinde oluştururken.

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a>Bir tek kayıtlı bir TXT kayıt kümesi oluşturma

Merhaba aşağıdaki örnekte nasıl toocreate bir TXT kaydı gösterilmektedir. TXT kayıtlarının desteklenen hello maksimum dize uzunluğu hakkında daha fazla bilgi için bkz: [TXT kayıtlarının](dns-zones-records.md#txt-records).

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a>Bir kayıt kümesini Al

tooretrieve varolan bir kayıt kümesini kullanma `Get-AzureRmDnsRecordSet`. Bu cmdlet hello kayıt Azure DNS'de kümesi temsil eden yerel bir nesne döndürür.

İle `New-AzureRmDnsRecordSet`, verilen hello kayıt kümesi adı olmalıdır bir *göreli* adı, hello bölge adı dışarıda gerekir anlamına gelir. Ayrıca toospecify hello kayıt türünü ve hello kayıt kümesi içeren hello bölge gerekir.

Merhaba aşağıdaki örnek bir kayıt tooretrieve nasıl ayarlanacağını gösterir. Bu örnekte, hello bölge hello kullanarak belirtilen `-ZoneName` ve `-ResourceGroupName` parametreleri.

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Alternatif olarak, aynı zamanda hello kullanılarak geçirilen bir bölge nesnesi kullanarak hello bölgesi belirtebilirsiniz `-Zone` parametresi.

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a>Liste kayıt kümeleri

Aynı zamanda `Get-AzureRmDnsZone` toolist kaydı hello kaldırarak bir bölgede ayarlar `-Name` ve/veya `-RecordType` parametreleri.

Merhaba aşağıdaki örnek hello bölgesinde tüm kayıt kümeleri döndürür:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Merhaba aşağıdaki örnekte nasıl tüm kayıt kümeleri belirli bir türde gösterir hello kaydı atlama kümesi adı sırada hello kayıt türü belirterek alınabilir:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

verilen ada sahip tüm kayıt kümeleri tooretrieve kayıt türleri arasında tooretrieve tüm kayıt kümelerini ve ardından filtre hello sonuçları gerekir:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

Örnekler yukarıdaki tüm hello, hello bölge olabilir hello kullanarak ya da belirtilen `-ZoneName` ve `-ResourceGroupName`parametreleri (gösterildiği gibi) veya bir bölge nesnesi belirterek:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a>Kayıt kümesi varolan bir kayıt tooan Ekle

tooadd kayıt tooan varolan bir kaydı ayarlayın, hello aşağıdaki üç adımları izleyin:

1. Merhaba mevcut kayıt kümesini Al

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Merhaba yeni kayıt toohello yerel kayıt kümesi ekleyin. Bu çevrimdışı bir işlemdir.

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Merhaba değişikliği geri toohello Azure DNS hizmeti uygulayın. 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

Kullanarak `Set-AzureRmDnsRecordSet` *değiştirir* mevcut kayıt Azure DNS (ve içerdiği tüm kayıtları) belirtilen hello kayıt kümesiyle kümesi hello. [ETag denetimleri](dns-zones-records.md#etags) kullanılan tooensure eşzamanlı değişiklikleri yazılmaz. İsteğe bağlı hello kullanabilirsiniz `-Overwrite` bu denetimleri toosuppress geçin.

Bu işlem dizisi de olabilir *yöneltilen*, parametre olarak geçirme yerine hello kanal kullanarak hello kayıt kümesi nesnesi geçirdiğiniz anlamına gelir:

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

Yukarıdaki Hello örnekler nasıl tooadd 'Bir' kayıt tooan varolan bir kayıt kümesinin türü 'A' gösterir. Benzer işlemleri kullanılan tooadd kayıtları toorecord hello değiştirerek diğer türleri kümesi dizisidir `-Ipv4Address` parametresinin `Add-AzureRmDnsRecordConfig` diğer parametreleri belirli tooeach kayıt türüne sahip. Merhaba her kayıt türü için parametreler olan hello aynı olduğu gibi hello `New-AzureRmDnsRecordConfig` gösterildiği gibi cmdlet [ek kayıt türü örnekleri](#additional-record-type-examples) üstünde.

Kayıt kümeleri 'CNAME' veya 'SOA' türünde birden fazla kayıt içeremez. Bu sınırlama hello DNS standartları ortaya çıkar. Azure DNS sınırlandırılmasıdır değil.

## <a name="remove-a-record-from-an-existing-record-set"></a>Varolan bir kayıt kümesinden bir kaydı kaldırma

Merhaba işlem tooremove kayıt kümesinden bir kaydı olan mevcut kayıt tooan benzer toohello işlem tooadd kayıt kümesi:

1. Merhaba mevcut kayıt kümesini Al

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Merhaba kaydını hello yerel kayıt kümesi nesnesinden kaldırın. Bu çevrimdışı bir işlemdir. kaldırılmakta hello kaydı varolan bir kayıtla tam bir eşleşme tüm parametreleri arasında olmalıdır.

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Merhaba değişikliği geri toohello Azure DNS hizmeti uygulayın. İsteğe bağlı kullanım hello `-Overwrite` geçiş toosuppress [Etag denetler](dns-zones-records.md#etags) eşzamanlı değişiklikleri.

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

Merhaba dizisi tooremove hello son kaydından bir kayıt kümesini yukarıdaki kullanarak hello kayıt kümesi silinmez, bunun yerine boş bir kayıt kümesi bırakır. bir kayıt kümesinin tamamen tooremove bkz [bir kayıt kümesini Sil](#delete-a-record-set).

Benzer şekilde tooadding kayıtları tooa kayıt kümesi, bir kayıt kümesini de yöneltilen işlemleri tooremove hello dizisi:

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

Farklı kayıt türleri hello uygun türe özgü parametreler çok geçirerek desteklenir`Remove-AzureRmDnsRecordSet`. Merhaba her kayıt türü için parametreler olan hello aynı olduğu gibi hello `New-AzureRmDnsRecordConfig` gösterildiği gibi cmdlet [ek kayıt türü örnekleri](#additional-record-type-examples) üstünde.


## <a name="modify-an-existing-record-set"></a>Varolan bir kayıt kümesini değiştirme

Varolan bir kayıt kümesini değiştirme hello adımlar, ekleme veya kayıt kümesindeki kayıt kaldırırken benzer toohello adımlar şunlardır:

1. Merhaba mevcut kayıt kullanarak kümesi almak `Get-AzureRmDnsRecordSet`.
2. Merhaba yerel kayıt kümesi nesnesi tarafından değiştirin:
    * Ekleme veya kayıt kaldırma
    * Merhaba parametrelerinin varolan kayıtları değiştirme
    * Merhaba kaydı değiştirme meta verileri ve toolive süresi (TTL) ayarlayın
3. Hello kullanarak, değişiklikleri `Set-AzureRmDnsRecordSet` cmdlet'i. Bu *değiştirir* mevcut kayıt hello kayıt kümesi belirtilen ile Azure DNS'de kümesi hello.

Kullanırken `Set-AzureRmDnsRecordSet`, [Etag denetler](dns-zones-records.md#etags) kullanılan tooensure eşzamanlı değişiklikleri yazılmaz. İsteğe bağlı hello kullanabilirsiniz `-Overwrite` bu denetimleri toosuppress geçin.

### <a name="tooupdate-a-record-in-an-existing-record-set"></a>Varolan bir kaydı bir kayıtta tooupdate ayarlayın

Bu örnekte, varolan 'Bir' kayıt başlangıç IP adresi değiştirin:

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a>toomodify bir SOA kaydı

Ekleme veya SOA kaydına hello bölgenin tepesinde Ayarla otomatik olarak oluşturulan hello kayıtları kaldırın (`-Name "@"`, tırnak işaretleri dahil olmak üzere). Ancak, hello SOA kaydı (dışında "ana bilgisayar") içinde hello parametrelerinden herhangi birini değiştirmek ve TTL hello kayıt ayarlayın.

örnekte gösterildiği nasıl aşağıdaki hello toochange hello *e-posta* SOA kaydına hello özelliği:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>Merhaba bölge tepesinde toomodify NS kayıtları

Merhaba NS kayıt Hello bölgenin tepesinde kümesi her DNS bölge ile otomatik olarak oluşturulur. Hello Azure DNS ad sunucuları atanan toohello bölgesi hello adlarını içerir.

Ek ad sunucuları toothis NS kayıt kümesi, etki alanları birden fazla DNS sağlayıcınız ile birlikte barındırma toosupport ekleyebilirsiniz. Merhaba TTL ve bu kayıt kümesi için meta verileri de değiştirebilirsiniz. Ancak, kaldırmak veya hello önceden doldurulmuş haldedir Azure DNS ad sunucuları değiştirin.

Bu yalnızca toohello NS kayıt kümesi hello bölge tepesinde en geçerli olduğunu unutmayın. Diğer NS kayıt kümelerinde bölgenizi (olarak kullanılan toodelegate alt bölgeler) kısıtlama değiştirilebilir.

Aşağıdaki örneğine hello tooadd bir ek ad sunucusu toohello NS kaydı hello bölgenin tepesinde nasıl ayarlanacağını gösterir:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a>meta veri toomodify kayıt kümesi

[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) anahtar-değer çiftleri olarak her bir kayıt kümesi ile kullanılan tooassociate uygulamaya özgü verileri olabilir.

Merhaba aşağıdaki örnek varolan bir kaydı toomodify hello meta verileri nasıl ayarlanacağını gösterir:

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a>Bir kayıt kümesini Sil

Kayıt kümeleri hello kullanarak silinebilir `Remove-AzureRmDnsRecordSet` cmdlet'i. Kayıt kümesi siliniyor hello kayıt kümesi içindeki tüm kayıtları siler.

> [!NOTE]
> Merhaba SOA ve NS kayıt kümelerini hello bölge tepesinde adresindeki silemezsiniz (`-Name '@'`).  Azure DNS Hello bölge oluşturuldu ve hello bölge silindiğinde bunları otomatik olarak siler. Bunlar otomatik olarak oluşturulur.

Merhaba aşağıdaki örnek bir kayıt toodelete nasıl ayarlanacağını gösterir. Bu örnekte, hello kayıt kümesi adını, kayıt kümesi türü, bölge adını ve kaynak grubu her açıkça belirtilmiş.

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Alternatif olarak, hello kayıt kümesi adı ve türü ile belirtilebilir ve hello bölge belirtilen nesneyi kullanarak:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

Üçüncü seçenek olarak, bir kayıt kümesi nesnesi kullanılarak hello kayıt kendisini kümesi belirtilebilir:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

Merhaba kayıt kümesinin bir kayıt kümesi nesnesi kullanarak silinmiş toobe belirttiğinizde [Etag denetler](dns-zones-records.md#etags) kullanılan tooensure eşzamanlı değişiklikleri silinmez. İsteğe bağlı hello kullanabilirsiniz `-Overwrite` bu denetimleri toosuppress geçin.

Merhaba kayıt kümesi nesnesi bir parametre olarak geçirilen yerine de yöneltilen:

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a>Onay istekleri

Merhaba `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, ve `Remove-AzureRmDnsRecordSet` cmdlet'leri tüm destek onay ister.

Merhaba, her cmdlet için onay ister `$ConfirmPreference` PowerShell tercih değişkeni değerine sahip `Medium` veya daha düşük. Merhaba varsayılan değeri itibaren `$ConfirmPreference` olan `High`, bu komut istemlerini hello varsayılan PowerShell ayarlarını kullanırken verilmez.

Merhaba geçerli kılabilirsiniz `$ConfirmPreference` hello kullanarak ayarını `-Confirm` parametresi. Belirtirseniz `-Confirm` veya `-Confirm:$True` , hello cmdlet sizden, önce onay çalıştırır. Belirtirseniz `-Confirm:$False` , hello cmdlet istenmez sizin için onay. 

Hakkında daha fazla bilgi için `-Confirm` ve `$ConfirmPreference`, bkz: [tercih değişkenleri hakkında](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi edinmek [bölgeleri ve Azure DNS kayıtlarında](dns-zones-records.md).
<br>
Nasıl çok öğrenin[bölgeleri ve kayıtları korumak](dns-protect-zones-recordsets.md) Azure DNS kullanırken.
<br>
Gözden geçirme hello [Azure DNS PowerShell başvuru belgeleri](/powershell/module/azurerm.dns).
