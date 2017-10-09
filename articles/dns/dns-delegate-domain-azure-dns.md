---
title: "aaaDelegate, DNS etki alanı tooAzure | Microsoft Docs"
description: "Nasıl toochange etki alanı temsilcisi kullanımı Azure DNS etki alanı tooprovide barındıran sunucu adı ve anlayın."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a>Bir etki alanı tooAzure DNS temsilci seçme

Azure DNS toohost bir DNS bölgesi sağlar ve azure'de bir etki alanı için DNS kayıtlarını hello yönetin. Bir etki alanı tooreach Azure DNS için DNS sorgularını sırayla hello etki alanı toobe sahip hello üst etki alanından tooAzure DNS temsilcisi. Azure DNS unutmayın hello etki alanı kayıt değil. Bu makalede açıklanır nasıl toodelegate, DNS etki alanı tooAzure.

Bir kayıt şirketinden satın alınan etki alanları için kayıt şirketiniz bu NS kayıtlarını ayarlama seçeneğini tooset hello sunar. Bir etki alanı toocreate bu etki alanı adı ile bir DNS bölgesi durum Azure DNS'de tooown gerekmez. Ancak, tooown hello etki alanı tooset hello temsilci tooAzure DNS yukarı hello kayıt şirketinizle gerekir.

Örneğin, 'contoso.net' hello etki alanı satın alın ve Azure DNS'de hello adı 'contoso.net' ile bir bölge oluşturmanız varsayalım. Merhaba etki alanının Hello sahibi olarak, etki alanınız için seçenek tooconfigure hello ad sunucusu adreslerini (yani, hello NS kayıtları) hello kayıt sunar. Merhaba kayıt şirketi bu NS kayıtlarını bu durumda '.net' hello üst etki alanında depolar. Merhaba Dünya istemciler, ardından 'contoso.net' tooresolve DNS kayıtlarını çalışırken Azure DNS bölgesindeki yönlendirilmiş tooyour etki alanı olabilir.

## <a name="create-a-dns-zone"></a>DNS bölgesi oluşturma

1. Toohello Azure portalında oturum açın
1. Hello Hub menüsünde ve tıklayın **yeni > Ağ iletişimi >** ve ardından **DNS bölgesi** tooopen hello oluşturmak DNS bölge dikey.

    ![DNS bölgesi](./media/dns-domain-delegation/dns.png)

1. Merhaba üzerinde **oluşturma DNS bölgesi** dikey penceresinde hello aşağıdaki değerleri girin ve ardından **oluşturma**:

   | **Ayar** | **Değer** | **Ayrıntılar** |
   |---|---|---|
   |**Ad**|contoso.net|Merhaba DNS bölgesinin Hello adı|
   |**Abonelik**|[Aboneliğiniz]|Bir abonelik toocreate hello uygulama ağ geçidi seçin.|
   |**Kaynak grubu**|**Yeni oluştur:** contosoRG|Bir kaynak grubu oluşturun. Merhaba kaynak grubu adı, seçtiğiniz hello abonelik içinde benzersiz olmalıdır. Merhaba okuyun, kaynak grupları hakkında daha fazla toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) genel bakış makalesi.|
   |**Konum**|Batı ABD||

> [!NOTE]
> Merhaba kaynak grubu hello kaynak grubu toohello konumunu gösterir ve hello DNS bölgesi üzerinde hiçbir etkisi olmaz. Merhaba DNS bölgesi konumunu her zaman "Genel" ve gösterilmiyor.

## <a name="retrieve-name-servers"></a>Ad sunucularını alma

DNS bölge tooAzure DNS temsilci önce ilk tooknow hello ad sunucusu adlarını bölgenizin gerekir. Azure DNS, her bölge oluşturmada bir havuzdan ad sunucuları ayırır.

1. Oluşturulan, hello Azure portal hello DNS bölgesine **Sık Kullanılanlar** bölmesinde, tıklatın **tüm kaynakları**. Merhaba tıklatın **contoso.net** hello DNS bölgesinde **tüm kaynakları** dikey. Merhaba aboneliği zaten içinde birçok kaynak varsa, girebilirsiniz **contoso.net** adına göre filtre hello içinde... kutusunu tooeasily erişim hello uygulama ağ geçidi. 

1. Merhaba ad sunucuları hello DNS bölgesine dikey penceresinden alır. Bu örnekte 'contoso.net' hello bölge ad sunucuları atanmıştır ' ns1-01.azure-dns.com', 'ns2-01.azure-DNS.NET', ' ns3-01.azure-dns.org', ve ' ns4-01.azure-dns.info':

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

Azure DNS, bölgenizi hello atanan ad sunucularını içeren yetkili NS kayıtları otomatik olarak oluşturur.  Azure PowerShell veya Azure CLI toosee hello ad sunucusu adlarını, tooretrieve bu kayıtları yeterlidir.

Merhaba aşağıdaki örneklerde ayrıca hello adımlar tooretrieve hello ad sunucuları, PowerShell ve Azure CLI Azure DNS'de bölge sağlar.

### <a name="powershell"></a>PowerShell

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

Aşağıdaki örnek hello hello yanıt ' dir.

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a>Azure CLI

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

Aşağıdaki örnek hello hello yanıt ' dir.

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-hello-domain"></a>Temsilci hello etki alanı

Merhaba DNS bölgesi oluşturulur ve hello ad sunucuları sahip olduğunuza hello üst etki alanı hello Azure DNS ad sunucuları ile güncelleştirilmiş toobe gerekir. Her kayıt şirketi kendi DNS Yönetim Araçları toochange hello ad sunucusu kayıtları etki alanı var. Merhaba kayıt şirketinizin DNS Yönetim sayfasında, hello NS kayıtlarını düzenleyin ve hello NS kayıtlarını Azure DNS oluşturulan hello olanları ile değiştirin.

Bir etki alanı tooAzure DNS devrederken Azure DNS tarafından sağlanan hello ad sunucusu adlarını kullanmanız gerekir. Tüm toouse önerilen dört sunucu adları, etki alanınızın adını hello bağımsız olarak adlandırın. Etki alanı temsilcisi hello adını sunucu adı toouse gerektirmez hello etki alanınız aynı üst düzey etki alanı.

Bu IP adresleri gelecekte değişebileceği ederken "Birleştirici kayıtlar' toopoint toohello Azure DNS ad sunucusu IP adreslerini, kullanmamanız gerekir. Kendi bölgenizdeki ad sunucusu adlarını kullanan ve bazen "gösterim ad sunucuları" olarak adlandırılan temsilci seçimleri, Azure DNS'de şu anda desteklenmemektedir.

## <a name="verify-name-resolution-is-working"></a>Ad çözümlemesinin çalıştığını doğrulama

Merhaba temsilci seçmeyi tamamladıktan sonra ad çözümlemesi (Merhaba bölge oluşturulduğunda bu da otomatik olarak oluşturulur), bölgenin SOA kaydına 'nslookup' tooquery hello gibi bir araç kullanarak çalıştığını doğrulayabilirsiniz.

Merhaba temsilci doğru hello normal DNS çözümleme işlemi ayarlarsanız hello ad sunucuları otomatik olarak bulur, toospecify hello Azure DNS ad sunucuları sahip.

```
nslookup -type=SOA contoso.com
```

Merhaba, hello komutu önceki örnek yanıttan aşağıdadır:

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a>Azure DNS'de alt etki alanlarını devretme

Tooset ayrı bir alt bölge kurmak istiyorsanız Azure DNS'de bir alt etki alanını devredebilirsiniz. Örneğin, ayarladığınız ve Azure DNS'ye temsilci 'contoso.net' tooset ayrı alt bölge ayarlamak istediğinizi varsayalım 'partners.contoso.net'.

1. Merhaba alt bölge 'partners.contoso.net' Azure DNS'de oluşturun.
2. Merhaba alt bölge tooobtain hello ad sunucuları Azure DNS'deki hello alt bölgeyi barındıran hello yetkili NS kayıtlarını arayın.
3. Merhaba üst bölgede toohello alt bölgeyi işaret eden NS kayıtlarını yapılandırarak hello alt bölge temsilcisi.

### <a name="create-a-dns-zone"></a>DNS bölgesi oluşturma

1. Toohello Azure portalında oturum açın
1. Hello Hub menüsünde ve tıklayın **yeni > Ağ iletişimi >** ve ardından **DNS bölgesi** tooopen hello oluşturmak DNS bölge dikey.

    ![DNS bölgesi](./media/dns-domain-delegation/dns.png)

1. Merhaba üzerinde **oluşturma DNS bölgesi** dikey penceresinde hello aşağıdaki değerleri girin ve ardından **oluşturma**:

   | **Ayar** | **Değer** | **Ayrıntılar** |
   |---|---|---|
   |**Ad**|partners.contoso.net|Merhaba DNS bölgesinin Hello adı|
   |**Abonelik**|[Aboneliğiniz]|Bir abonelik toocreate hello uygulama ağ geçidi seçin.|
   |**Kaynak grubu**|**Varolanı kullan:** contosoRG|Bir kaynak grubu oluşturun. Merhaba kaynak grubu adı, seçtiğiniz hello abonelik içinde benzersiz olmalıdır. Merhaba okuyun, kaynak grupları hakkında daha fazla toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) genel bakış makalesi.|
   |**Konum**|Batı ABD||

> [!NOTE]
> Merhaba kaynak grubu hello kaynak grubu toohello konumunu gösterir ve hello DNS bölgesi üzerinde hiçbir etkisi olmaz. Merhaba DNS bölgesi konumunu her zaman "Genel" ve gösterilmiyor.

### <a name="retrieve-name-servers"></a>Ad sunucularını alma

1. Oluşturulan, hello Azure portal hello DNS bölgesine **Sık Kullanılanlar** bölmesinde, tıklatın **tüm kaynakları**. Merhaba tıklatın **partners.contoso.net** hello DNS bölgesinde **tüm kaynakları** dikey. Merhaba aboneliği zaten içinde birçok kaynak varsa, girebilirsiniz **partners.contoso.net** adına göre filtre hello içinde... kutusunu tooeasily erişim hello DNS bölgesi.

1. Merhaba ad sunucuları hello DNS bölgesine dikey penceresinden alır. Bu örnekte 'contoso.net' hello bölge ad sunucuları atanmıştır ' ns1-01.azure-dns.com', 'ns2-01.azure-DNS.NET', ' ns3-01.azure-dns.org', ve ' ns4-01.azure-dns.info':

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

Azure DNS, bölgenizi hello atanan ad sunucularını içeren yetkili NS kayıtları otomatik olarak oluşturur.  Azure PowerShell veya Azure CLI toosee hello ad sunucusu adlarını, tooretrieve bu kayıtları yeterlidir.

### <a name="create-name-server-record-in-parent-zone"></a>Üst bölgede ad sunucusu kaydı oluşturma

1. Toohello gidin **contoso.net** hello Azure portal DNS bölgesinde.
1. **+ Kayıt kümesi**’ne tıklayın
1. Merhaba üzerinde **kayıt kümesi ekleme** dikey penceresinde hello aşağıdaki değerleri girin ve ardından **Tamam**:

   | **Ayar** | **Değer** | **Ayrıntılar** |
   |---|---|---|
   |**Ad**|iş ortakları|Merhaba alt DNS bölgesinin Hello adı|
   |**Tür**|NS|Ad sunucusu kayıtları için NS kullanın.|
   |**TTL**|1|Saat toolive.|
   |**TTL birimi**|Saat|zaman toolive birim toohours ayarlar|
   |**AD SUNUCUSU**|{partners.contoso.net bölgesinden ad sunucuları}|Merhaba ad sunucuları tüm 4 partners.contoso.net bölgeden girin. |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a>Diğer araçlarla Azure DNS'de alt etki alanlarını devretme

Merhaba aşağıdaki örneklerde hello adımlar toodelegate, PowerShell ve CLI Azure DNS'de alt etki alanlarını sağlar:

#### <a name="powershell"></a>PowerShell

Aşağıdaki PowerShell örneğine hello bunun nasıl çalıştığı gösterilmektedir. aynı adımları hello Azure portal çalıştırılabilir veya platformlar arası Azure CLI aracılığıyla hello hello.

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

Kullanım `nslookup` her şeyin doğru şekilde hello alt bölgenin SOA kaydına hello bakarak ayarlanan tooverify.

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a>Azure CLI

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

Hello için Hello ad sunucularını almak `partners.contoso.net` hello çıkış bölgeden.

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Merhaba kayıt kümesi ve her bir ad sunucusu için NS kayıtları oluşturun.

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a>Tüm kaynakları silme

Bu makalede, aşağıdaki adımları tam hello oluşturulan tüm kaynakları toodelete:

1. Hello Azure portal'ın **Sık Kullanılanlar** bölmesinde tıklatın **tüm kaynakları**. Merhaba tıklatın **contosorg** kaynak tüm kaynaklar dikey penceresinde hello grubu. Merhaba aboneliği zaten içinde birçok kaynak varsa, girebilirsiniz **contosorg** hello içinde **ada göre Filtrele...** kutusunu tooeasily erişim hello kaynak grubu.
1. Merhaba, **contosorg** dikey penceresinde hello tıklatın **silmek** düğmesi.
1. Merhaba portal tootype hello toodelete istediğiniz hello kaynak grubu tooconfirm adını gerektirir. Tür *contosorg* hello kaynak grubu adı için ardından **silmek**. Bu nedenle her zaman emin tooconfirm silmeden önce bir kaynak grubu Merhaba içeriğine olması, bir kaynak grubunu silme hello kaynak grubundaki tüm kaynakları siler. Merhaba portal hello kaynak grubu içinde bulunan tüm kaynakları siler ve sonra hello kaynak grubu kendisini siler. Bu işlem birkaç dakika sürer.

## <a name="next-steps"></a>Sonraki adımlar

[DNS bölgelerini yönetme](dns-operations-dnszones.md)

[DNS kayıtlarını yönetme](dns-operations-recordsets.md)
