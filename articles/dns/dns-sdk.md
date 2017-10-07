---
title: "aaaCreate DNS bölgeleri ve kullanarak Azure DNS kayıt kümelerini hello .NET SDK'sı | Microsoft Docs"
description: "Nasıl toocreate DNS bölgeleri ve kayıt kümelerini Azure DNS'de hello .NET SDK kullanarak."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a>DNS bölgeleri ve hello .NET SDK kullanarak kayıt kümeleri oluşturma

.NET DNS Yönetim kitaplığıyla DNS SDK kullanılarak işlemleri toocreate, delete veya update DNS bölgeleri, kayıt kümelerini ve kayıtları otomatikleştirebilirsiniz. Tam bir Visual Studio projesi kullanılabilir [burada.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)

## <a name="create-a-service-principal-account"></a>Bir hizmet sorumlusu hesabı oluşturun

Genellikle, tooAzure kaynaklarına programlı erişim verilir, kendi kullanıcı kimlik bilgilerini yerine adanmış bir hesap. Bu ayrılmış hesapları 'hizmet sorumlusu' hesapları adı verilir. toouse hello Azure DNS SDK örnek proje, ilk toocreate bir hizmet sorumlusu hesabı gerekir ve hello doğru izinleri atayın.

1. İzleyin [bu yönergeleri](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate bir hizmet sorumlusu hesabı (hello Azure DNS SDK örnek proje parola tabanlı kimlik doğrulama varsayar.)
2. Bir kaynak grubu oluşturun ([burada nasıl](../azure-resource-manager/resource-group-template-deploy-portal.md)).
3. Kullanım Azure RBAC toogrant hello hizmet asıl hesabı 'DNS bölge katkıda bulunan' izinleri toohello kaynak grubu ([burada nasıl](../active-directory/role-based-access-control-configure.md).)
4. Hello Azure DNS SDK örnek proje kullanıyorsanız, aşağıdaki gibi hello 'program.cs' dosyasını düzenleyin:

   * Merhaba Tenantıd, istemci kimliği (hesap kimliği olarak da bilinir), gizliliği (hizmet sorumlusu hesabı parola) ve 1. adımda kullanılan Subscriptionıd için doğru değerleri Hello ekleyin.
   * 2. adımda seçilen hello kaynak grubu adı girin.
   * Tercih ettiğiniz bir DNS bölgesi ad girin.

## <a name="nuget-packages-and-namespace-declarations"></a>NuGet paketleri ve ad alanı bildirimleri

toouse hello Azure DNS .NET SDK'sı, gereksinim duyduğunuz tooinstall hello **Azure DNS Yönetimi Kitaplığı** NuGet paketi ve diğer gerekli Azure paketler.

1. İçinde **Visual Studio**, bir proje veya yeni bir proje açın.
2. Çok Git**Araçları** ** > ** **NuGet Paket Yöneticisi** ** > ** **için NuGet paketlerini Yönet Çözüm... **.
3. Tıklatın **Gözat**, hello etkinleştirmek **INCLUDE yayın öncesi** onay kutusunu ve türü **Microsoft.Azure.Management.Dns** hello arama kutusuna.
4. Merhaba paketi seçin ve **yükleme** tooadd, tooyour Visual Studio projesi.
5. Paketleri aşağıdaki tooalso yükleme hello yukarıda Hello işlemi tekrarlayın: **Microsoft.Rest.ClientRuntime.Azure.Authentication** ve **Microsoft.Azure.Management.ResourceManager**.

## <a name="add-namespace-declarations"></a>Ad alanı bildirimleri ekleme

Ad alanı bildirimleri aşağıdaki hello ekleme

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a>Merhaba DNS yönetim istemcisi başlatılamadı

Merhaba *DnsManagementClient* hello yöntemleri ve DNS bölgeleri ve kayıt kümeleri yönetmek için gerekli özellikleri içerir.  Merhaba aşağıdaki kodu toohello hizmet asıl hesabı'nda günlüğe kaydeder ve bir DnsManagementClient nesnesi oluşturur.

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a>Bir DNS bölgesi güncelle

toocreate bir DNS bölgesi, ilk toocontain hello DNS bölge parametrelerini "Bölgesine" nesnesi oluşturulur. DNS bölgelerini değil bağlantılı tooa belirli bir bölge olduğundan, hello konum too'global ayarlanır '. Bu örnekte, bir [Azure Resource Manager 'etiketinin'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) toohello bölge de eklenir.

tooactually oluşturma veya güncelleştirme hello bölge Azure DNS'de hello bölge parametrelerini içeren hello bölge nesnesi toohello geçirilen *DnsManagementClient.Zones.CreateOrUpdateAsyc* yöntemi.

> [!NOTE]
> DnsManagementClient işlemi üç modlarını destekler: eşzamanlı ('CreateOrUpdate'), zaman uyumsuz ('CreateOrUpdateAsync'), ya da erişim toohello HTTP yanıtı ('CreateOrUpdateWithHttpMessagesAsync') ile uyumsuz.  Uygulamanızın gereksinimlerine bağlı olarak bu modlarından birini seçebilirsiniz.

Azure DNS destekler adlı iyimser eşzamanlılık [Etag'ler](dns-getstarted-create-dnszone.md). Bu örnekte belirtme "*" bir zaten mevcut değilse hello 'If-None-Match' üstbilgi Azure DNS toocreate bir DNS bölgesi söyler. için.  kaynak grubu verilen hello hello verilen ada sahip bir bölge zaten varsa hello çağrı başarısız olur.

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a>DNS kayıt kümelerini ve kayıtları oluşturma

DNS kayıtlarını kayıt kümesi yönetilir. Kayıt kümesi aynı ad ve kayıt hello kayıtlarıyla kümesidir bir bölgedeki türü.  Merhaba kayıt kümesi adı göreli toohello bölge adı, tam DNS adı hello değil.

toocreate veya güncelleştirme bir kayıt kümesi, "Kayıt kümesi" parametreleri nesnesi oluşturulur ve çok geçirilen*DnsManagementClient.RecordSets.CreateOrUpdateAsync*. DNS bölgeleri ile olmadığından işlem üç modu: eşzamanlı ('CreateOrUpdate'), zaman uyumsuz ('CreateOrUpdateAsync'), ya da erişim toohello HTTP yanıtı ('CreateOrUpdateWithHttpMessagesAsync') ile uyumsuz.

DNS bölgeleri gibi ile kayıt kümeleri üzerinde işlem iyimser eşzamanlılık desteği içerir.  'If-Match' ne 'If-None-Match' belirtilmiş olduğundan, bu örnekte, her zaman hello kayıt kümesi oluşturulur.  Bu çağrı ile aynı ad ve kayıt hello ayarlamak varolan bir kaydı üzerine yazar bu DNS bölgesinde türü.

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a>Get bölgeleri ve kayıt kümeleri

Merhaba *DnsManagementClient.Zones.Get* ve *DnsManagementClient.RecordSets.Get* yöntemleri tek başına bölgeleri ve kayıt kümelerini sırasıyla alma. Kayıt kümeleri kendi türü, adı ve bunlar mevcut hello bölgesi ve kaynak grubu tarafından tanımlanır. Bölgeler, bunlar mevcut kendi adı ve hello kaynak grubu tarafından tanımlanır.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a>Varolan bir kayıt kümesini güncelleştir

tooupdate varolan bir DNS kaydı kümesi, güncelleştirme hello kayıt içeriği sonra hello değişiklik Gönder sonra hello kayıt kümesi, ilk alma.  Bu örnekte, hello ' Etag'den' kayıt kümesi hello 'If-Match' parametresinde alınan hello belirtin. eşzamanlı işlem hello kayıt hello sırada kümesi değiştirilirse hello çağrı başarısız olur.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a>Liste bölgeleri ve kayıt kümeleri

toolist bölgeleri kullanmak hello *DnsManagementClient.Zones.List... * belirtilen kaynak grubunun tüm bölgelerde ya da belirli Azure abonelik (üzerinden kaynak gruplarını.) toolist kayıt kümesindeki tüm bölgeler listeleme desteği yöntemleri kullanın *DnsManagementClient.RecordSets.List... * belirli bir bölgedeki tüm kayıt kümelerinin ya da bu kaydı kümeleri yalnızca belirli bir türdeki listeleme destek yöntemleri.

Bölgeleri listelerken not alın ve sonuçları kayıt kümelerini anlatır.  örnekte gösterildiği nasıl aşağıdaki hello sonuçlarının hello sayfaları aracılığıyla tooiterate. (Bir yapay küçük sayfa boyutu '2' kullanılan tooforce disk belleği; yöntem bu parametre, alınmamalıdır ve varsayılan sayfa boyutu kullanılan hello.)

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a>Sonraki adımlar

Merhaba karşıdan [Azure DNS .NET SDK örnek proje](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), nasıl toouse hello diğer DNS kayıt türleri için örnekler dahil olmak üzere Azure DNS .NET SDK hakkında daha fazla örnekleri içerir.
