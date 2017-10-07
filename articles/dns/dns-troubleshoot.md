---
title: "aaaAzure DNS sorun giderme kılavuzu | Microsoft Docs"
description: "Azure DNS ile nasıl tootroubleshoot ortak sorunları"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a>Azure DNS sorun giderme kılavuzu

Bu sayfa, ortak Azure DNS sorular için sorun giderme bilgileri sağlar.

Bu adımları sorununuzu çözmüyorsa, ayrıca arayın veya sorununuzu ileti bizim [MSDN topluluk Destek Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork). Alternatif olarak, bir Azure destek isteği açın.


## <a name="i-cant-create-a-dns-zone"></a>Bir DNS bölgesi oluşturma kullanılamaz

tooresolve sık karşılaşılan sorunları, bir veya daha fazla hello aşağıdaki adımları deneyin:

1.  Azure DNS denetim gözden geçirme hello toodetermine hello başarısızlık nedeniyle günlüğe kaydeder.
2.  Her DNS bölge adı, kaynak grubu içinde benzersiz olmalıdır. Diğer bir deyişle, iki DNS bölgeleri hello ile aynı adı, bir kaynak grubu paylaşamaz. Farklı bir bölge adı veya farklı bir kaynak grubu kullanmayı deneyin.
3.  "Ulaştınız veya bu abonelikte {abonelik kimliği} bölgelerinin hello en büyük sayıyı aştı." bir hata görebilirsiniz Ya da farklı bir Azure aboneliği kullanma, bazı bölgeleri silin veya abonelik sınırınızı Azure destek tooraise başvurun.
4.  Bir hata görebilirsiniz "Merhaba bölge '{bölge name}' kullanılamaz." Bu hata Azure DNS bu DNS bölgesi için ad sunucularını oluşturulamıyor tooallocate anlamına gelir. Farklı bir bölge adı kullanmayı deneyin. Alternatif olarak, hello etki alanı adı sahibi varsa, kimin ad sunucuları sizin için ayırabilirsiniz Azure desteğine başvurun.


### <a name="recommended-documents"></a>**Önerilen belgeler**

[DNS bölgeleri ve kayıtları](dns-zones-records.md)
<br>
[DNS bölgesi oluşturma](dns-getstarted-create-dnszone-portal.md)

## <a name="i-cant-create-a-dns-record"></a>DNS kaydı oluşturamıyorum

tooresolve sık karşılaşılan sorunları, bir veya daha fazla hello aşağıdaki adımları deneyin:

1.  Azure DNS denetim gözden geçirme hello toodetermine hello başarısızlık nedeniyle günlüğe kaydeder.
2.  Merhaba kayıt kümesi zaten var mı?  Azure DNS kaydı kullanarak kayıtları yönetir *ayarlar*, aynı ad ve aynı hello hello kayıtlarının hello koleksiyonu olan türü. Aynı ad ve zaten yazın hello içeren bir kayıt varsa, tooadd kaydı varolan hello düzenlemelisiniz gibi başka bir kayıtla ayarlayın.
3.  Merhaba DNS bölge tepesinde (Merhaba hello bölgenin ' kök') bir kaydı toocreate çalışıyorsunuz? Bu nedenle, hello DNS kuralı toouse hello ise ' @' karakteri hello kayıt adı. Ayrıca hello DNS standartlarında hello bölge tepesinde CNAME kayıtları vermez unutmayın.
4.  CNAME çakışmanız mı var?  Merhaba DNS standartlarında hello aynı kayıt diğer herhangi bir tür olarak ad ile bir CNAME kaydı izin vermez. Farklı bir tür aynı adı başarısız hello ile bir kayıt oluşturma, varolan bir CNAME varsa.  Varolan bir kaydı, farklı bir tür Hello adıyla eşleşen benzer şekilde, bir CNAME oluşturma başarısız olur. Başka bir kaydı veya farklı bir kayıt adını seçmek, Hello çakışma hello kaldırarak kaldırın.
5.  Hello hello DNS bölgesinde izin verilen kayıt kümesi sayısı sınırına? Merhaba geçerli kayıt kümesi sayısı ve hello en fazla kayıt kümesi sayısı hello hello 'Özellikler' hello bölgenin altında Azure portal'ın gösterilir. Bu sınıra ulaştınız, ardından bazı kaydı kümeleri silmek ya da Azure destek tooraise bu bölge için kayıt kümesi sınırınızı başvurun, sonra yeniden deneyin. 


### <a name="recommended-documents"></a>**Önerilen belgeler**

[DNS bölgeleri ve kayıtları](dns-zones-records.md)
<br>
[DNS bölgesi oluşturma](dns-getstarted-create-dnszone-portal.md)



## <a name="i-cant-resolve-my-dns-record"></a>DNS kaydımı çözümleyemiyorum

DNS ad çözümlemesi, çeşitli nedenlerle başarısız olabilecek çok adımlı bir işlemdir. Merhaba aşağıdaki adımlar neden Azure DNS'de barındırılan bir bölgedeki bir DNS kaydı için DNS çözümlemesi başarısız araştırmanıza yardımcı.

1.  Merhaba DNS kayıtlarını Azure DNS'de doğru şekilde yapılandırıldığını onaylayın. Merhaba hello bölge adı, kayıt adı ve kayıt türünün doğru olduğunu denetleme Azure portal Hello DNS kayıtlarını gözden geçirin.
2.  Merhaba DNS kayıtları doğru hello Azure DNS ad sunucuları üzerinde çözümleme onaylayın.
    - DNS sorguları yerel Bilgisayarınızdan yaparsanız hello ad sunucuları hello geçerli durumunu yansıtmaz önbelleğe alınan sonuçları görebilirsiniz.  Ayrıca, şirket ağlarına DNS proxy sunucuları, sık kullandığınız toospecific ad sunucuları, DNS sorgularını engellemek yönlendirilmiş.  tooavoid bu sorunları kullanan bir web tabanlı ad çözümleme hizmeti gibi [digwebinterface](http://digwebinterface.com).
    - Emin toospecify hello Azure portal gösterildiği gibi hello doğru ad sunucuları, DNS bölgesi için olabilir.
    - Merhaba DNS adı (Merhaba bölge adı dahil toospecify hello tam olarak nitelenmiş adını olması) doğru olduğundan ve hello kayıt türü doğru olduğundan emin olun
3.  Merhaba DNS etki alanı adının doğru bir şekilde açıldı onaylayın [toohello Azure DNS ad sunucuları temsilci](dns-domain-delegation.md). [DNS temsilci seçme doğrulaması hizmeti sunan birçok 3. taraf web sitesi](https://www.bing.com/search?q=dns+check+tool) vardır. Bu test bir *bölge* temsilci test hello DNS bölge adı ve hello tam kayıt adını değil yalnızca girmeniz gerekir.
4.  Yukarıdaki Hello tamamlandığını DNS kaydınız artık doğru çözümlenmelidir. tooverify, yeniden kullanabileceğiniz [digwebinterface](http://digwebinterface.com), hello varsayılan ad sunucusu ayarlarını kullanarak bu süre.


### <a name="recommended-documents"></a>**Önerilen belgeler**

[Bir etki alanı tooAzure DNS temsilci seçme](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a>Nasıl ı hello 'service' ve 'Protokolü' bir SRV kaydı için belirtin?

Azure DNS kayıt kümelerini olarak DNS kayıtlarını yönetir — kayıtları koleksiyonu ile aynı ad ve aynı hello hello hello türü. SRV kayıt kümesi için hello 'service' ve 'Protokolü' hello kayıt kümesi adı bir parçası olarak belirtilen toobe gerekir. Merhaba diğer SRV parametreler ('priority', 'weight', 'bağlantı noktası' ve 'target') ayrı olarak hello kayıt kümesindeki her kayıt için belirtildi.

Örnek SRV kayıt adları (hizmet adı 'sip', protokol 'tcp'):

- \_SIP. \_tcp (kayıt hello bölgenin tepesinde kümesi oluşturur)
- \_sip.\_tcp.sipservice ('sipservice' adlı bir kayıt kümesi oluşturur)

### <a name="recommended-documents"></a>**Önerilen belgeler**

[DNS bölgeleri ve kayıtları](dns-zones-records.md)
<br>
[Hello Azure portal kullanarak DNS kayıt kümelerini ve kayıtları oluşturma](dns-getstarted-create-recordset-portal.md)
<br>
[SRV kayıt türü (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)


## <a name="next-steps"></a>Sonraki adımlar

* Hakkında bilgi edinin [Azure DNS bölgeleri ve kayıtları](dns-zones-records.md)
* Azure DNS kullanarak toostart öğrenin nasıl çok[bir DNS bölgesi oluşturma](dns-getstarted-create-dnszone-portal.md) ve [DNS kayıtlarını oluşturun](dns-getstarted-create-recordset-portal.md).
* Varolan bir DNS bölgesi toomigrate öğrenin nasıl çok[içeri ve dışarı aktarma bir DNS bölge dosyasına](dns-import-export.md).

