---
title: "Medya uygulaması için aaaAzure Mobile Engagement uygulaması"
description: "Medya uygulaması senaryosu tooimplement Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a495eb790993a30d5c03802aa9e6404fea983d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a>Medya uygulaması ile Mobile Engagement uygulama
## <a name="overview"></a>Genel Bakış
John, büyük media şirket için bir mobil proje yöneticisidir. Daha kısa bir süre önce bir çok yüksek indirme sayısı sahip yeni bir uygulama başlattı. Kendisine indirme için kendi hedefleri erişti ancak hala kendi dönüş üzerinde Investment(ROI) kullanıcı başına kendi gereksinimlerini karşılamıyor. 

John, kendi ROI çok düşük olmasının zaten belirledi. Yalnızca 2 hafta sonra uygulamayı kullanarak kullanıcıların sık durdurun ve bunların çoğu asla geri dönün. Kendi uygulama tooincrease hello bekletme istediği.

Bazı ilk test sonra kendisinin zaman kendisinin kullanıcıları prosese öğrenilen ile anında iletme bildirimleri, bunlar kendi uygulamasını kullanarak toocontinue eğilimi gösterir. Etkin olmayan kullanıcılar ayrıca genellikle toohello uygulamaya kendisinin gönderir bildirimleri bağlı olarak döndürür. John Gelişmiş hedefleme ile anında iletme bildirimleri kullanan kendi uygulama için bir tür, katılım programının tooinvest karar verir.

John hello okuyun son [Azure Mobile Engagement - en iyi yöntemlerle Başlangıç Kılavuzu](mobile-engagement-getting-started-best-practices.md) ve tooimplement hello önerileri hello Guide'daki karar vermiştir.

## <a name="objectives-and-kpis"></a>Hedefleri ve KPI'leri
Önemli katılımcılara Can'ın uygulama için karşılar. Kullanıcılar kendi medya kullanma gibi iş reklamları'ndan oluşturulur. Kullanıcı başına tüketilen içerik artırarak John kendi gelirleri artırır. Tüm bir ana hedefte kabul ediyorum: tooincrease satış ads % 25. Bu amaç iş anahtar performans göstergelerini (KPI'lar) toomeasure ve sürücü oluşturun

* Kullanıcı başına tıklanan reklam sayısı
* Kaç tane makale ziyaret edilen sayfalar (kullanıcı başına / oturumu başına / haftada / aylık...)
* Sık kullanılan kategorileri nelerdir

Önemli katılımcılara Can'ın Toplantı göre kendisine kendi iş KPI'leri tanımlamıştır. Kendisine hello 1. Bölüm izleyen [Azure Mobile Engagement - en iyi yöntemlerle Başlangıç Kılavuzu](mobile-engagement-getting-started-best-practices.md). 

Ardından, hedefleri ulaşıldığında katılım KPI'leri tooensure aşağıdaki hello oluşturur:

* Bekletme aralıkları aşağıdaki hello izleme: günlük, haftalık, iki haftalık ve aylık.
* Etkin kullanıcı sayısı
* Merhaba uygulama derecelendirme hello uygulamasında depolar

Merhaba BT Ekibi önerilerine dayalı olarak, hello teknik KPI'ları aşağıdaki soruları aşağıdaki tooanswer hello eklendi:

* My kullanıcı yolu nedir (hangi sayfasını ziyaret, kaç kullanıcının harcamanız üzerinde)
* Kilitlenmelerine veya oturum başına karşılaşılan hataların sayısı?
* İşletim sistemi sürümleri çalıştıran Kullanıcılarım nelerdir?
* Kullanıcılarım için ekranın hello ortalama boyutu nedir?
* Ne tür bir internet bağlantıları Kullanıcılarım var mı?

Her KPI için kendisine gerekli hello verileri sınıflandırır ve kendisine hello uygun kendi playbook konumda kaydeder.

## <a name="engagement-program-and-integration"></a>Katılım programı ve tümleştirme
Bu John kendi KPI'leri tanımlamaya bitirdi artık, kendisinin kendi katılım stratejisi Aşama 4 katılım programları ve bunların hedefler tanımlayarak başlar:![][1]

Sonra John anında iletme bildirimleri her program için ayrıntılı tarafından daha derin gider. Anında iletme bildirimi beş öğeleri tarafından tanımlanır:

1. Hedef: hello bildirim hello amacı nedir
2. Merhaba hedefi ulaşıldı nasıl
3. Hedef: kimin hello bildirim alırsınız?
4. İçeriği: Hello ifadesi ve hello biçimini hello bildirim (içinde App/Out, uygulama) nedir
5. When: ne olduğunu hello en iyi şu anda toosend bu anında iletme bildirimi
   
    ![][2]

Daha fazla bilgi için toohello başvurun [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).

John hedef bölüm toodefine sahip hangi verileri kullanır hello incelemeyi 2 parçası toohello toocollect ve kendi etiket planı ortaklaşa BT Ekibi tooimplement hello çözümüyle yazma göre. Uygulama ve kullanıcı kabul testi 1 hafta sonra John son olarak, programlar başlatabilirsiniz.

## <a name="program-results"></a>Program sonuçları
4 ay sonra John programlar performansını inceler. Merhaba Karşılama programı ve hello haftalık Program kendi hedefleri ulaşmanızı. Kullanıcı yalnızca bir oturum ile Merhaba sayısını azaltır, haftada bağlantı hello sayısı iki katına ve hello uygulamanın daha fazla özellik kullanılır.

Merhaba **etkin olmayan Program** John kullanıcı tendencies anlamanıza yardımcı olur. % 15'hello etkin olmayan kullanıcı toohello uygulama geri dönün görünür. Ancak bunların çoğu birden fazla 1 ay etkin kalmaz. John bu sırası ek bildirimler ve kendi içerik seçimleri genişletme ile olası iyileştirmesi foresees.

Merhaba **Bul Program** düzgün çalışmıyor. Satış ancak yeterli tooreach kendi hedefleri artırır. John, kendisinin değil yeterli veri toomake ilgili hedefleme olması ve uygun içeriğin önermek olduğunu tanımlar. Kendisi bu programı durdurur ve Azure Mobile Engagement ile "düzenleme anında iletme bildirimleri" gönderme odaklanır. Kendi gazeteciler bir CMS çözüm toosend anında iletme bildirimleri zaten var ve toochange istemezsiniz.

John toouse hello Reach toouse AZME Web arabirimi gerek kalmadan Reach kampanyaları yönetme izin veren bir HTTP REST API'si olan API'sini karar verir. Bu yaklaşımda John kendisinin gerekir ve kendi yazıcılarının izin hello veri toplayabilir hello CMS çözümünü kullanarak tookeep.

works doğru özellik tooensure, John BT Ekibi toobe temkinli noktaları aşağıdaki hello üzerinde ister:

1. **İşletim sistemi** : hello API'leri gerçekleştiriliyorsa John toolist tüm örnekleri ve denetimleri karar verir tüm kendi kuralları tooadministrate anında iletme bildirimleri sahiptirler.
   Örneğin: İOS hello durumuyla olmayan büyük resmi Android anında iletme sistem izin verir.
2. **Zaman dilimi**: John istediği başlangıç zamanını ve son toocampaigns ayarlanmış bir API. Herhangi bir kesintiye uğratan bildirim bombing toopreserve kullanıcıların istediği.
3. **Kategoriler**: Pazarlama Takım şablon her uyarı türü için hazırlar. John, BT Ekibi tooset kategorileri hello API içinde sorar.

Bazı testleri sonra John memnun kalır. Teşekkür ederiz toothis API gazeteciler kendi CMS ile anında iletme Bildirimleri göndermeye devam edebilir ve Azure Mobile Engagement tüm davranış bunları toplar

Bu 4 sonra ilk ay, sonuçları iyi bir genel performans ve verir güvenirlik John ve kendi Panosu, kullanıcı artar % 15 başına Başına ROI yansıtacak ve Mobil Satış %7.5 artışı yalnızca dört ay içinde % 17,5 toplam satış temsil eder.

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
