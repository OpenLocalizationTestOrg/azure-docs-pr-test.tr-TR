---
title: aaaTemplates
description: "Bu konu, şablonları Azure bildirim hub'ları için açıklar."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a>Şablonlar
## <a name="overview"></a>Genel Bakış
Şablonlar, bir istemci uygulama toospecify hello tam biçim tooreceive istediği hello bildirimleri etkinleştirir. Şablonları kullanarak bir uygulama hello aşağıdakileri içeren birkaç farklı faydaları hayata geçirmek:

* Platform belirsiz arka uç
* Kişiselleştirilmiş bildirimler
* İstemci sürümü bağımsızlığı
* Kolay yerelleştirme

Bu bölümde nasıl bildirim tooeach cihaz platformları ve toopersonalize tüm aygıtlarınızın hedefleme toouse şablonları toosend platform belirsiz bildirimleri yayını iki ayrıntılı örnekler sağlar.

## <a name="using-templates-cross-platform"></a>Şablonları platformlar arası kullanma
Merhaba standart yol toosend anında iletme bildirimleri gönderilen toobe olan her bir bildirim için belirli yükü tooplatform Bildirim Hizmetleri (WNS, APNS) toosend olur. Örneğin, bir uyarı tooAPNS toosend hello form aşağıdaki Json nesnesinin hello yükü olduğu:

    {"aps": {"alert" : "Hello!" }}

bir Windows mağazası uygulaması üzerinde benzer bir bildirim iletisi toosend hello XML yükü aşağıdaki gibidir:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

MPNS (Windows Phone) ve GCM (Android) platformlar için benzer yükü oluşturabilirsiniz.

Bu gereksinim hello uygulama arka uç tooproduce farklı yüklerini her platform için zorlar ve etkili bir şekilde hello arka uç hello sunu katmanı hello uygulamanın parçası sorumlu hale getirir. Bazı sorunları yerelleştirme ve grafik düzenleri (döşeme çeşitli türleri için bildirimleri içeren özellikle Windows mağazası uygulamaları için) içerir.

Ayrıca etiketler, bir şablon toohello kümesi içerir şablon kayıtlar adlı bir istemci uygulama toocreate özel kayıtları Hello bildirim hub'ları şablon özelliği sağlar. (tercih edilen) yüklemeleri veya kayıtlar ile çalışıyorsanız olup olmadığını şablonları ile bir istemci uygulama tooassociate cihazları hello bildirim hub'ları şablon özelliği sağlar. Yükü örnekler önceki hello verildiğinde, hello yalnızca platformdan bağımsız hello gerçek uyarı iletisi (Merhaba!) bilgilerdir. Şablon yönergeleri için nasıl tooformat platformdan bağımsız ileti bu belirli istemci uygulama hello kaydı için bildirim hub'ı hello kümesidir. Örnek önceki hello hello platform bağımsız tek bir özellik iletisidir: **ileti Hello =!**.

Resim aşağıdaki hello işlem yukarıda hello gösterilmektedir:

![](./media/notification-hubs-templates/notification-hubs-hello.png)

Merhaba şablonu hello iOS istemci uygulamasını kaydı için aşağıdaki gibidir:

    {"aps": {"alert": "$(message)"}}

Merhaba Windows mağazası istemci uygulaması için karşılık gelen şablon Hello şöyledir:

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

Gerçek ileti hello bildirimi hello ifade $(ileti) konur. Bir ileti toothis belirli kayıt, toobuild ve hello ortak değeri anahtarları izleyen bir ileti gönderir olduğunda bu ifade hello bildirim hub'ı bildirir.

Yükleme modeliyle çalışıyorsanız, birden çok şablonlarının JSON hello yükleme "Şablon" anahtarı saklar. Kayıt modeliyle çalışıyorsanız, birden fazla şablon Merhaba istemci uygulaması birden çok kayıtlar sipariş toouse oluşturabilirsiniz; Örneğin, uyarı iletileri için bir şablon ve bölme için bir şablon güncelleştirir. İstemci uygulamaları, yerel kayıtları (kayıtlar herhangi bir şablon ile) ve şablon kayıtlar de karıştırabilirsiniz.

Merhaba bildirim hub'ı toohello ait düşünmeden her şablon için bir bildirim gönderir aynı istemci uygulaması. Bu davranış, daha fazla bildirimleri kullanılan tootranslate platformdan bağımsız bildirimlerini olabilir. Örneğin, aynı platform bağımsız ileti toohello bildirim hub'ı sorunsuz bir bildirim uyarı ve döşeme Güncelleştirmesi'nde hello arka uç toobe bu durumdan haberdar gerek kalmadan çevrilebilir hello. Bazı platformlar (örneğin, iOS) birden çok bildirimleri toohello Daralt Not kısa bir süre içinde gönderirse aynı aygıt.

## <a name="using-templates-for-personalization"></a>Kişiselleştirme için şablonları kullanma
Başka bir avantajı toousing şablonları hello özelliği toouse bildirim hub'ları tooperform kayıt başına kişiselleştirme bildirimler olur. Örneğin, belirli bir konumda hello hava koşulları içeren bir kutucuk görüntüleyen bir hava durumu uygulama göz önünde bulundurun. Bir kullanıcı derece veya Fahrenhayt derece ve tek veya beş günlük bir tahmini arasında seçim yapabilirsiniz. Şablonları kullanarak her bir istemci uygulama yükleme için gerekli hello biçimi kaydedebilirsiniz (1 gün Celsius, 1 gün Fahrenhayt, 5 gün derece, 5 gün Fahrenhayt), ve hello arka uç tüm hello bilgileri içeren tek bir ileti gereken toofill olanlar Gönder Şablonlar (örneğin, bir beş derece ve Fahrenhayt derece ile tahmin gün).

Merhaba şablonu ile derece tahmin hello bir gün için etme aşağıdaki gibidir:

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

Merhaba gönderilen ileti toohello bildirim hub'ı aşağıdaki özelliklere tüm hello içerir:

<table border="1">

<tr><td>day1_image</td><td>day2_image</td><td>day3_image</td><td>day4_image</td><td>day5_image</td></tr>

<tr><td>day1_tempC</td><td>day2_tempC</td><td>day3_tempC</td><td>day4_tempC</td><td>day5_tempC</td></tr>

<tr><td>day1_tempF</td><td>day2_tempF</td><td>day3_tempF</td><td>day4_tempF</td><td>day5_tempF</td></tr>
</table><br/>

Bu yöntemi kullanarak hello arka uç yalnızca tek bir ileti toostore belirli kişiselleştirme seçenekleri hello uygulama kullanıcılar için gerek kalmadan gönderir. Resim aşağıdaki hello bu senaryo gösterilmektedir:

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a>Nasıl tooregister şablonları
tooregister (tercih edilen) hello yükleme modeli kullanarak şablonları veya hello kayıt modelini bkz [kayıt yönetimi](notification-hubs-push-notification-registration-management.md).

## <a name="template-expression-language"></a>Şablon ifade dili
Sınırlı tooXML veya JSON Belge biçimleri şablonlarıdır. Ayrıca, belirli yerlerde ifadeleri yalnızca koyabilirsiniz; örnek, düğüm öznitelikleri veya XML değerleri için özellik değerleri için JSON dizesi.

Merhaba aşağıdaki tabloda şablonlarında izin hello dil gösterilmektedir:

| ifade | Açıklama |
| --- | --- |
| $(prop) |Başvuru tooan olay özelliği hello verilen ada sahip. Özellik adları büyük küçük harfe duyarlı değildir. Merhaba özellik mevcut değilse bu ifade hello özelliğin metin değeri veya boş bir dize çözümler. |
| $(prop, n) |Yukarıdaki, ancak hello metin açıkça olduğu gibi n karakter kırpılmış, örneğin $(başlık, 20) hello title özelliğini Merhaba içeriğine 20 karakter kırpar. |
| . (prop, n) |Kırpılmış olsun gibi metin yukarıdaki, ancak hello olarak üç nokta ile sonekine. dize hello Hello toplam boyutu kırpılmış ve hello soneki n karakteri aşmayan. . (başlık, 20) bir giriş özelliğiyle "Merhaba başlık satırı olduğu" sonuçlarında **hello başlık budur...** |
| %(prop) |Bu hello çıkışı dışında benzer too$(name) URI kodlanır. |
| #(prop) |JSON şablonları (örneğin, iOS ve Android şablonları için) kullanılır.<br><br>Bu işlev works tam olarak hello aynı daha önce JSON şablonları (örneğin, Apple Şablonları) kullanılması dışında belirtilen $(prop) olarak. Bu işlev tarafından çevrelenen değil, bu durumda, "{','}" (örneğin, 'myJsonProperty': '#(ad)'), ve Javascript biçimindeki, örneğin, regexp tooa sayı değerlendirir: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, JSON bir sayıdır hello çıktı sonra.<br><br>Örneğin, ' rozet: '#(ad)' hale 'göstergeye': 40 (ve değil '40'). |
| 'text' veya "metin" |Bir hazır değer. Değişmez değerler tek veya çift tırnak içine alınmış rastgele metin içerir. |
| Expr1 + expr2 |tek bir dize iki ifadelere birleştirme hello birleştirme işleci. |

Merhaba ifadeleri herhangi forms önceki hello olabilir.

Birleştirme kullanırken hello tüm ifade alınmalıdır {} ile. Örneğin, {$(prop) + '-' + $(prop2)}. |

Örneğin, hello aşağıdaki geçerli bir XML şablon değil:

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


Olarak yukarıda anlatıldığı, birleştirme, kullanırken ifadeleri süslü parantez içine alınmalıdır. Örneğin:

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

