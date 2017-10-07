---
title: "aaaHosting Azure DNS'de DNS arama bölgeleri ters | Microsoft Docs"
description: "Nasıl toouse Azure DNS toohost hello ters DNS arama bölgeleri IP aralıkları için bilgi edinin"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a>Azure DNS geriye doğru DNS araması bölgelerinde barındırma

Bu makalede, nasıl Azure DNS'de, atanan IP aralıkları için DNS arama bölgeleri ters toohost hello açıklanmaktadır. Merhaba geriye doğru arama bölgesi tarafından temsil edilen hello IP aralıkları tooyour kuruluş, genellikle ISS'niz tarafından atanmış olması gerekir.

tooconfigure DNS geriye doğru Azure ait IP adresi atanmış tooyour Azure hizmeti için bkz: [hello geriye doğru arama ayrılan hello IP adreslerini tooyour Azure hizmeti için yapılandırma](dns-reverse-dns-for-azure-services.md).

Bu makalede okumadan önce bu bilgi sahibi olmanız [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md).

Bu makalede, ilk geriye doğru arama DNS bölgesi ve hello Azure portal, Azure PowerShell, Azure CLI 1.0 veya Azure CLI 2.0 kullanarak kayıt hello adımları toocreate anlatılmaktadır.

## <a name="create-a-reverse-lookup-dns-zone"></a>Geriye doğru arama DNS bölgesi oluşturma

1. İçinde toohello oturum [Azure portalı](https://portal.azure.com)
1. Hello Hub menüsünde, tıklayıp **yeni** > **ağ** > ve ardından **DNS bölgesi** tooopen hello **oluşturma DNS bölgesi**dikey.

   ![DNS bölgesi](./media/dns-reverse-dns-hosting/figure1.png)

1. Merhaba üzerinde **oluşturma DNS bölgesi** dikey penceresinde, DNS bölgenizi adı. Merhaba bölgenin Hello adı farklı IPv4 ve IPv6 önekleri için hazırlanmış. Her iki hello talimatlar için kullanması [IPv4](#ipv4) veya [IPv6](#ipv6) tooname bölgenizi. Tıklatın tamamlandığında **oluşturma** toocreate hello bölgesi.

### <a name="ipv4"></a>IPv4

bir IPv4 geriye doğru arama bölgesi Hello adını temsil ettiği hello IP aralığına dayalıdır. Biçim aşağıdaki hello olmalıdır: `<IPv4 network prefix in reverse order>.in-addr.arpa`. Örnekler için bkz: [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md#ipv4).

> [!NOTE]
> Azure DNS'de Sınıfsız geriye doğru DNS arama bölgeleri oluştururken, kısa çizgi kullanmanız gerekir (`-`) yerine eğik çizgi ('/ ') hello bölge adı.
>
> Örneğin, hello IP aralığı 192.0.2.128/26 için kullanmanız gerekir `128-26.2.0.192.in-addr.arpa` hello bölge adı yerine olarak `128/26.2.0.192.in-addr.arpa`.
>
> Her ikisi de hello DNS standartları tarafından desteklenir, ancak hello eğik içeren adlara DNS bölgesi, bunun nedeni (`/`) karakter Azure DNS'de desteklenmiyor.

Merhaba aşağıdaki örnekte nasıl toocreate 'Sınıfı C' adlı DNS bölgesi ters gösterir `2.0.192.in-addr.arpa` hello Azure Portalı aracılığıyla Azure DNS'de:

 ![DNS bölgesi oluşturma](./media/dns-reverse-dns-hosting/figure2.png)

Merhaba 'Kaynak grubu konumu' hello kaynak grubu için hello konum tanımlar ve hello DNS bölgesi üzerinde hiçbir etkisi olmaz. Merhaba DNS bölgesi konumunu her zaman 'global' dır ve gösterilmiyor.

Merhaba aşağıdaki toocomplete bu nasıl görev ile örnekler Azure PowerShell ve Azure CLI hello:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

bir IPv6 geriye doğru arama bölgesi Hello adını form aşağıdaki hello olmalıdır: `<IPv6 network prefix in reverse order>.ip6.arpa`.  Örnekler için bkz: [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md#ipv6).


Merhaba aşağıdaki örnekte nasıl toocreate bir IPv6 geriye doğru DNS arama bölgesini adlı gösterir `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` hello Azure Portalı aracılığıyla Azure DNS'de:

 ![DNS bölgesi oluşturma](./media/dns-reverse-dns-hosting/figure3.png)

Merhaba 'Kaynak grubu konumu' hello kaynak grubu için hello konum tanımlar ve hello DNS bölgesi üzerinde hiçbir etkisi olmaz. Merhaba DNS bölgesi konumunu her zaman 'global' dır ve gösterilmiyor.

Merhaba aşağıdaki toocomplete bu nasıl görev ile örnekler Azure PowerShell ve Azure CLI hello:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a>AzureCLI 1.0

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a>DNS geriye doğru arama bölgesini temsilci seçme

Geriye doğru DNS araması bölgenizi oluşturduktan, hello üst bölgeden hello bölge temsilcisi olmanız gerekir. DNS temsilcisi geriye doğru DNS araması bölgenizi barındırma hello DNS ad çözümleme işlemi toofind hello ad sunucuları sağlar. Bu ad sunucuları tooanswer DNS geriye doğru sorgularını hello IP adreslerinin adres aralığınızı sağlar.

Bir DNS bölgesi için temsilci seçme işleminin hello açıklanan ileriye doğru arama bölgeleri için [, etki alanı tooAzure DNS temsilci](dns-delegate-domain-azure-dns.md). Geriye doğru arama bölgeleri için temsilci seçme çalışır hello aynı şekilde. Merhaba yalnızca tooconfigure hello ad sunucuları hello etki alanı adı kayıt şirketiniz yerine IP aralığınızı sağlanan ISS ile gerektiğini farktır.

## <a name="create-a-dns-ptr-record"></a>Bir DNS PTR kaydı oluştur

### <a name="ipv4"></a>IPv4

Merhaba aşağıdaki örnek, Azure DNS geriye doğru DNS bölgesinde bir PTR kaydı oluşturma hello işlemi açıklanmaktadır. Diğer kayıt türleri ve toomodify mevcut kayıtları için bkz: [yönetmek DNS kayıtlarını ve kayıt kümelerini kullanarak hello Azure portal](dns-operations-recordsets-portal.md).

1.  Merhaba hello üstündeki **DNS bölgesi** dikey penceresinde, select **+ kayıt kümesine** tooopen hello **kayıt kümesi ekleme** dikey.

 ![DNS bölgesi](./media/dns-reverse-dns-hosting/figure4.png)

1. Merhaba üzerinde **kayıt kümesi ekleme** dikey. 
1. Seçin **PTR** hello kaydından "**türü**" menüsü.  
1. Merhaba bir PTR kaydı hello kayıt kümesi adını toobe hello hello IPv4 adresi geri kalanı ters sırada gerekir. Bu örnekte, hello ilk üç sekizlisinin zaten hello bölge adı (.2.0.192) bir parçası olarak doldurulur. Bu nedenle, yalnızca hello son sekizli hello ad alanına sağlanır. Örneğin, kayıt kümenizi adlandırabilirsiniz "**15**", IP adresi 192.0.2.15 olan bir kaynak için.  
1. Merhaba, "**etki alanı adı**" alanında, hello IP kullanan hello kaynağın hello tam etki alanı adı (FQDN) girin.
1. Seçin **Tamam** hello altındaki hello dikey toocreate hello DNS kaydı.

 ![kayıt kümesi Ekle](./media/dns-reverse-dns-hosting/figure5.png)

Merhaba nasıl örnekler aşağıdadır toocomplete bu görevi, PowerShell ve hello AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a>AzureCLI 1.0

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a>IPv6

Aşağıdaki örnek hello yeni 'PTR' kayıt oluşturma hello işleminde size kılavuzluk eder. Diğer kayıt türleri ve toomodify mevcut kayıtları için bkz: [yönetmek DNS kayıtlarını ve kayıt kümelerini kullanarak hello Azure portal](dns-operations-recordsets-portal.md).

1. Merhaba hello üstündeki **DNS bölge dikey**seçin **+ kayıt kümesine** tooopen hello **kayıt kümesi ekleme** dikey.

  ![DNS bölge dikey penceresi](./media/dns-reverse-dns-hosting/figure6.png)

2. Merhaba üzerinde **kayıt kümesi ekleme** dikey. 
3. Seçin **PTR** hello kaydından "**türü**" menüsü.  
4. Merhaba bir PTR kaydı hello kayıt kümesi adını toobe hello hello IPv6 adresi geri kalanı ters sırada gerekir. Sıfır sıkıştırma eklemeniz gerekir. Bu örnekte, IPv6 zaten hello bölge adı (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa) bir parçası olarak doldurulmuş hello ilk 64 bit hello. Bu nedenle, yalnızca son 64 bit hello hello ad alanına sağlanır. Merhaba hello IP adresinin son 64 bit girilir ters sırada bir süre her onaltılık sayı hello bölücüyü kullanarak. Örneğin, kayıt kümenizi adlandırabilirsiniz "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**", IP adresi 2001:0db8:abdc:0000:f524:10bc:1af9:405e olan bir kaynak için.  
5. Merhaba, "**etki alanı adı**" alanında, hello IP kullanan hello kaynağın hello tam etki alanı adı (FQDN) girin.
6. Seçin **Tamam** hello altındaki hello dikey toocreate hello DNS kaydı.

![kayıt kümesi dikey ekleme](./media/dns-reverse-dns-hosting/figure7.png)

Merhaba nasıl örnekler aşağıdadır toocomplete bu görevi, PowerShell ve hello AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a>AzureCLI 1.0

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a>Kayıtları görüntüleme

oluşturduğunuz tooview hello kayıtları tooyour DNS bölgesinde hello Azure portalına gidin. Merhaba parçası Hello alt **DNS bölgesi** dikey penceresinde hello DNS bölgesi için hello kayıtlarını görebilirsiniz. Her bölgede oluşturulan, hello varsayılan NS ve SOA kayıtları, artı, oluşturduğunuz tüm yeni kayıtlar görmeniz gerekir.

### <a name="ipv4"></a>IPv4

IPv4 PTR kayıtları gösteren DNS bölge dikey penceresinde:

![DNS bölge dikey penceresi](./media/dns-reverse-dns-hosting/figure8.png)

Merhaba aşağıdaki örneklerde PowerShell kullanarak nasıl tooview hello PTR kayıtlarını göster veya Azure CLI hello:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

IPv6 PTR kayıtları gösteren DNS bölge dikey penceresinde:

![DNS bölge dikey penceresi](./media/dns-reverse-dns-hosting/figure9.png)

Merhaba, tooview hello PowerShell ve hello AzureCLI kayıtları nasıl örnekler şunlardır:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a>SSS

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a>Geriye doğru DNS arama bölgeleri my ISS atanan IP blokları Azure DNS üzerinde barındırabilir?

Evet. Azure DNS'de kendi IP aralıkları için Hello (ARPA) geriye doğru arama bölgeleri barındıran tam olarak desteklenir.

Bu makalede anlatıldığı gibi Azure DNS'de Hello geriye doğru arama bölgesi oluşturun, sonra ISS'niz ile çok çalışma[temsilci hello bölge](dns-domain-delegation.md).  Ardından hello PTR kayıtlarını yönetme aynı yolla diğer kayıt türleri hello her geriye doğru arama için.

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a>Ne kadar my ters DNS araması bölge maliyeti barındırma mu?

Azure DNS, ISS atanan IP Blok adresindeki doludur için hello geriye doğru DNS arama bölgesini barındıran [standart Azure DNS ücretler](https://azure.microsoft.com/pricing/details/dns/).

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a>Azure DNS'de IPv4 ve IPv6 adresleri için geriye doğru DNS arama bölgeleri barındıran?

Evet. Bu makalede açıklanır nasıl toocreate IPv4 ve IPv6 geriye doğru DNS arama bölgeleri Azure DNS'de.

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a>Varolan bir geriye doğru DNS araması bölge alabilir miyim?

Evet. Azure DNS'yi hello Azure CLI tooimport var olan DNS bölgeleri kullanabilirsiniz. Bu, ileriye doğru arama bölgeleri ve geriye doğru arama bölgeleri için çalışır.

Daha fazla bilgi için bkz: [içeri ve dışarı aktarma bir DNS bölge dosyasını kullanarak hello Azure CLI](dns-import-export.md).

## <a name="next-steps"></a>Sonraki adımlar

Geriye doğru DNS hakkında daha fazla bilgi için bkz: [wikipedia'da ters DNS araması](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Nasıl çok öğrenin[, Azure Hizmetleri için ters DNS kayıtlarını yönetme](dns-reverse-dns-for-azure-services.md).
