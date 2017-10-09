---
title: "aaaDNS bölgeleri ve genel bakış - Azure DNS kayıtlarını | Microsoft Docs"
description: "DNS bölgeleri ve Microsoft Azure DNS kayıtlarını barındırmak için destek genel bakış."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: be4580d7-aa1b-4b6b-89a3-0991c0cda897
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: jonatul
ms.openlocfilehash: f214c3e2e810a80a000281820acd35f0aaf5a7e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-dns-zones-and-records"></a>DNS bölgeleri ve kayıtları'na genel bakış

Bu sayfa, etki alanları, DNS bölgeleri ve DNS kayıtlarını ve kayıt kümelerini ve Azure DNS'de nasıl desteklenen anahtar kavramlarını hello açıklar.

## <a name="domain-names"></a>Etki alanı adları

Merhaba etki alanı adı sistemi, etki alanları hiyerarşisidir. Merhaba hiyerarşi adı olan basitçe hello 'kök' etki alanından başlar '**.**'.  Bunun altında "com", "net", "org", "uk" veya "jp" gibi en üst düzey etki alanları bulunur.  Bunların altında "org.uk" veya "co.jp" gibi ikinci düzey etki alanları bulunur. Merhaba DNS hiyerarşisindeki Hello etki alanlarının genel olarak, Merhaba dünya genelindeki DNS ad sunucuları tarafından barındırılan dağıtılır.

Bir etki alanı adı kayıt toopurchase "contoso.com" gibi bir etki alanı adı sağlayan bir kuruluş olan.  Bir etki alanı satın alma sağ toocontrol hello DNS hiyerarşi örneğin toodirect 'www.contoso.com' hello adı tooyour şirketinizin web sitesi izin vererek bu adla hello adı sağlar. Merhaba Kaydedici hello etki alanında kendi ad sunucuları sizin adınıza ana bilgisayar veya toospecify alternatif ad sunucuları izin vermez.

Azure DNS yapabileceğiniz bir genel dağıtılmış, yüksek kullanılabilirlik adı sunucu altyapısı sağlar toohost etki alanınızı kullanacak. Azure DNS'de etki alanlarınızı barındırarak DNS kayıtlarınızı hello ile yönetebilmeniz için aynı kimlik bilgileri, API'leri, Araçlar, faturalama ve diğer Azure hizmetlerinizi desteği.

Azure DNS, etki alanı adlarını satın alma şu anda desteklemiyor. Bir etki alanı adı toopurchase istiyorsanız toouse bir üçüncü taraf etki alanı adı kayıt gerekir. Merhaba Kaydedici genellikle küçük bir yıllık ücret ister. Merhaba etki alanları için DNS kayıtlarını Yönetimi sonra Azure DNS'de barındırılabilir. Bkz: [bir etki alanı tooAzure DNS temsilci](dns-domain-delegation.md) Ayrıntılar için.

## <a name="dns-zones"></a>DNS bölgeleri

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a>DNS kayıtları

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a>Yaşam süresi

toolive Hello süresi veya TTL, ne kadar süreyle her kayıt istemciler tarafından yeniden sorgulanmadan önce önbelleğe alınacağını belirtir. Yukarıdaki örnek Hello hello TTL 3600 saniye veya 1 saat değil.

Azure DNS'de hello TTL her kayıt için değil hello kayıt kümesi için belirtilen şekilde hello bu kaydından tüm kayıtlar için aynı değer kullanılır ayarlayın.  Herhangi bir TTL değeri 1 ile 2.147.483.647 saniye arasında bir değer belirtebilirsiniz.

### <a name="wildcard-records"></a>Joker karakter kayıtları

Azure DNS [joker kayıtlarını](https://en.wikipedia.org/wiki/Wildcard_DNS_record) destekler. (Bir joker karakter olmayan kayıt kümesinden daha yakın bir eşleşme olmadıkça) joker kayıtlarını eşleşen ada sahip bir yanıt tooany sorgusunda döndürülür. Azure DNS joker karakter kaydı kümeleri NS ve SOA dışında tüm kayıt türleri için destekler.

toocreate bir joker karakter kaydı kümesi, hello kayıt kümesi adını kullanın '\*'. Alternatif olarak, aynı zamanda bir adla kullanabilirsiniz '\*'olarak kendi en solundaki etiketle, örneğin,'\*.foo'.

### <a name="cname-records"></a>CNAME kayıtları

CNAME kaydı kümeleri birlikte bulunamaz hello diğer kayıt kümeleri ile aynı adı. Örneğin, kümesi hello göreli adı 'www' ile bir CNAME kaydı oluşturamazsınız ve bir A kaydı hello adresindeki hello göreli adı 'www' ile aynı saat.

Çünkü hello bölge tepesinde (ad = ' @') her zaman hello NS ve SOA kaydı içeren hello bölge oluşturulduğunda oluşturulan kümeleri, CNAME kaydı hello bölgenin tepesinde kümesi oluşturamıyor.

Bu kısıtlamaların hello DNS standartları kaynaklıdır ve Azure DNS sınırlamaları değildir.

### <a name="ns-records"></a>NS kayıtları

Merhaba NS kayıt kümesi hello bölgenin tepesinde (ad ' @') her DNS bölge ile otomatik olarak oluşturulur ve hello bölge silindiğinde otomatik olarak silinir (ayrı olarak silinemez).

Bu kayıt kümesinin hello Azure DNS ad sunucuları atanan toohello bölgesi hello adlarını içerir. Ek ad sunucuları toothis NS kayıt kümesi, etki alanları birden fazla DNS sağlayıcınız ile birlikte barındırma toosupport ekleyebilirsiniz. Merhaba TTL ve bu kayıt kümesi için meta verileri de değiştirebilirsiniz. Ancak, kaldırmak veya hello önceden doldurulmuş haldedir Azure DNS ad sunucuları değiştirin. 

Bu yalnızca toohello NS kayıt kümesi hello bölge tepesinde en geçerli olduğunu unutmayın. Diğer NS kayıt kümelerinde bölgenizi (olarak kullanılan toodelegate alt bölgeler) oluşturulmuş, değiştirilebilir ve kısıtlama silinir.

### <a name="soa-records"></a>SOA kayıtları

SOA kayıt kümesi hello her bölge tepesinde otomatik olarak oluşturulur (ad = ' @') ve hello bölge silindiğinde otomatik olarak silinir.  SOA kayıtları oluşturulamıyor veya ayrı olarak silinir.

Merhaba SOA kaydına hello Azure DNS tarafından sağlanan önceden yapılandırılmış toorefer toohello birincil sunucu adı olan 'ana' özellik dışında tüm özelliklerini değiştirebilirsiniz.

### <a name="spf-records"></a>SPF kayıtlarının

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a>SRV kayıtları

[SRV kayıtları](https://en.wikipedia.org/wiki/SRV_record) çeşitli hizmetler toospecify sunucu konumlar tarafından kullanılır. Bir SRV kaydı Azure DNS'de belirtirken:

* Merhaba *hizmet* ve *Protokolü* hello kayıt kümesi adı bir parçası olarak belirtilen, alt çizgi ile önek.  Örneğin, '\_SIP.\_ TCP.Name'.  Merhaba bölge tepesinde bir kaydı için gerek toospecify yok ' @' hello kayıt adında, yalnızca hello hizmet ve protokol, örneğin kullanmak '\_SIP.\_ TCP'.
* Merhaba *öncelik*, *ağırlık*, *bağlantı noktası*, ve *hedef* hello kayıt kümesindeki her bir kaydı parametrelerinin olarak belirtilir.

### <a name="txt-records"></a>TXT kayıtları

TXT, kullanılan toomap etki alanı adları tooarbitrary metin dizelerini kayıtlarıdır. Birden çok uygulamalarında hello gibi özellikle ilgili tooemail yapılandırma kullanılan [gönderen ilke Çerçevesi'ı (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) ve [DomainKeys tanımlanan posta (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail).

Merhaba DNS standartları her biri yukarı too254 karakter uzunluğunda olabilir, birden çok dizeyi tek bir TXT kaydı toocontain izin verir. Birden çok dizenin kullanıldığı durumlarda, bunlar istemciler tarafından birleştirilmiş ve tek bir dize kabul edilir.

Hello Azure DNS REST API'si çağrılırken, toospecify her TXT dize ayrı olarak gerekir.  PowerShell veya CLI arabirimleri Hello Azure portalı kullanırken, gerekirse 254 karakter parçaya otomatik olarak bölünür kayıt başına tek bir dize belirtmeniz gerekir.

bir DNS kaydı birden çok dizelerde ile karıştırılmamalıdır hello TXT kayıt kümesi içinde birden çok TXT kayıt hello.  TXT kayıt kümesi birden fazla kayıt içerebilir *her biri* birden çok dizenin içerebilir.  Azure DNS too1024 karakterleri yukarı toplam dize uzunluğu (Birleşik ayarlanmış tüm kayıtları arasında) her bir TXT kaydı destekler.

## <a name="tags-and-metadata"></a>Etiketleri ve meta veriler

### <a name="tags"></a>Etiketler

Etiketleri ad-değer çiftlerinin listesini ve Azure Resource Manager toolabel kaynaklar tarafından kullanılır.  Azure Resource Manager Azure faturasını etiketleri filtre tooenable görünümlerini kullanır ve ayrıca, hangi etiketlerin ilke gereklidir tooset sağlar. Etiketler hakkında daha fazla bilgi için bkz: [kullanarak Azure kaynaklarınızı tooorganize etiketler](../azure-resource-manager/resource-group-using-tags.md).

Azure DNS, DNS bölge kaynakları Azure Resource Manager etiketleri kullanarak destekler.  Alternatif 'meta verileri' desteklenir gibi DNS kaydı aşağıda açıklandığı gibi ayarlar ancak DNS kayıt kümelerini üzerinde etiketleri desteklemez.

### <a name="metadata"></a>Meta Veriler

Bir alternatif toorecord kümesi etiketleri gibi Azure DNS kayıt kümelerini 'meta verileri' kullanarak açıklanmasını destekler.  Benzer tootags, tooassociate ad-değer çiftleri her kayıt kümesi ile meta veri sağlar.  Bu yararlı olabilir, örneğin her kayıt toorecord hello amacı ayarlayın.  Etiketler, farklı meta verileri kullanılan tooprovide Azure faturasını filtre uygulanmış bir görünümünü olamaz ve bir Azure Resource Manager ilkesinde belirtilemez.

## <a name="etags"></a>Etag'ler

İki kişinin iki işlem toomodify deneyin varsayalım bir DNS kaydı sırasında hello aynı saat. Hangisinin WINS? Ve başkaları tarafından oluşturulan değişikliklerin üzerine hello kazanan bilir?

Azure DNS kullanır Etag'ler toohandle eşzamanlı değişiklikleri toohello aynı kaynak güvenle. Etag'ler ayrı [Azure Resource Manager 'Etiketleri'](#tags). Her DNS kaynak (bölge veya kayıt kümesi) ilişkili bir ETag değerine sahip. Bir kaynak alınır olduğunda, kendi Etag de alınır. Bir kaynak güncelleştirirken Azure DNS, ' % s'hello Etag hello sunucu eşleşmeleri üzerinde doğrulayabilmeniz için geri toopass Etag hello seçebilirsiniz. Her güncelleştirme tooa kaynak hello yeniden Etag sonuçları olduğundan, bir Etag uyuşmazlığı eşzamanlı bir değişiklik oluştuğunu gösterir. Etag'ler hello kaynak zaten mevcut değilse yeni bir kaynak tooensure oluşturulurken kullanılabilir.

Varsayılan olarak, Azure DNS PowerShell Etag'ler tooblock eşzamanlı değişiklikleri toozones ve kayıt kümelerini kullanır. İsteğe bağlı Hello *-üzerine* anahtar kullanılan toosuppress Etag denetimleri olabilir, her eşzamanlı durumda oluşan değişikliklerin üzerine yazılır.

Hello Azure DNS REST API'si Hello düzeyinde Etag'ler HTTP üstbilgileri kullanılarak belirtilir.  Aşağıdaki tablonun hello davranışları verilmiştir:

| Üstbilgi | Davranışı |
| --- | --- |
| None |PUT (Etag denetimleri) her zaman başarılı |
| IF-match<etag> |PUT yalnızca kaynak var ve Etag eşleşiyorsa başarılı |
| IF-match * |Kaynak varsa PUT yalnızca başarılı |
| IF-none-match * |Kaynak yoksa, PUT yalnızca başarılı |


## <a name="limits"></a>Sınırlar

Azure DNS kullanarak varsayılan sınırları aşağıdaki hello uygulayın:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a>Sonraki adımlar

* Azure DNS kullanarak toostart öğrenin nasıl çok[bir DNS bölgesi oluşturma](dns-getstarted-create-dnszone-portal.md) ve [DNS kayıtlarını oluşturun](dns-getstarted-create-recordset-portal.md).
* Varolan bir DNS bölgesi toomigrate öğrenin nasıl çok[içeri ve dışarı aktarma bir DNS bölge dosyasına](dns-import-export.md).
