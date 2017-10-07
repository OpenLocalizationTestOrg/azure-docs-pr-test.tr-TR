---
title: "aaaAzure Mobile Engagement kullanıcı arabirimi - Reach kampanya"
description: "Laern nasıl toocreate ve Azure Mobile Engagement kullanarak anında iletme bildirimi kampanyaları yönetme"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a>Nasıl toocreate ve anında iletme bildirimi kampanyaları yönetme
Toosend bir anında iletme bildirimi gereksinim duyduğunuz tüm hello bilgileri sağlayarak karmaşık formül hello hello UI toocreate yeni bir itme kampanya ulaşma bölümünü kullanabilirsiniz. Merhaba seçenekler itme kampanyanın biraz hello dört kampanya türlerine bağlı olarak değişir: Duyurular, anketler, veri iter ve Kutucuklar (yalnızca Windows Phone).

### <a name="option-applies-to"></a>Seçenek için geçerlidir:
* Diller: Tüm (Duyurular, anketler, veri gönderimleri, kutucukları)
* Kampanya: Tüm (Duyurular, anketler, veri gönderimleri, kutucukları)
* Bildirim: Duyurular, anketler
* İçeriği: Her kampanya türü için benzersiz olmalıdır
* İzleyici: Tüm (Duyurular, anketler, veri gönderimleri, kutucukları)
* Zaman çerçevesi: Duyurular, anketler, döşeme
* Sınama: Tüm (Duyurular, anketler, veri gönderimleri, kutucukları)

![Reach Campaign1][20]

## <a name="languages"></a>Diller
Merhaba dilleri açılan menü toosend toouse farklı dillerde ayarlayın, anında iletme toodevices farklı bir sürümünü kullanabilirsiniz. Varsayılan olarak, tüm cihazlar aynı hangi dilde toouse ayarlandıktan bağımsız olarak Anında hello alır. Kendi cihaz kümesi tooa farklı dil kullanıcılarla hello itme hello varsayılan dil sürümünü alır. Merhaba itme kampanya seçeneklerinin birçoğu toospecify alternatif içerik her seçtiğiniz hello ek diller için sağlar. 

![Reach Campaign2][21]

### <a name="language-differences-apply-to"></a>Dil farklar geçerlidir:
* Diller: Benzersiz dilleri toplama toohello varsayılan dilde seçilebilir.
* Kampanya: Aynı tüm diller için
* Bildirim: Her dil için benzersiz ayrıca toohello varsayılan dil
* İçeriği: Her dil için benzersiz ayrıca toohello varsayılan dil
* İzleyici: ayrı dil ölçüte göre filtre uygulanabilir
* Zaman çerçevesi: tüm diller için aynı
* Sınama: tooeach dil aynı anda gönderilebilir.

### <a name="supported-languages"></a>Desteklenen diller:
* Arapça (ar) 
* Bulgarca (bg) 
* Katalanca (ca) 
* Çince (zh) 
* Hırvatça (hr) 
* Czech (cs) 
* Danca (da) 
* Felemenkçe (nl) 
* İngilizce (TR) 
* Fince (fi) 
* Fransızca (fr) 
* Almanca (de) 
* Yunanca (el) 
* İbranice (.) 
* Hintçe (yüksek) 
* Macarca (hu) 
* Endonezya dili (ID) 
* İtalyanca () 
* Japonca (ja) 
* Korece (ko) 
* Letonca (lv) 
* Litvanca (lt) 
* Malay (macrolanguage) (ms) 
* Norveççe Bokmål (nb) 
* Lehçe (pl) 
* Portekizce (pt) 
* Rumence (ro) 
* Rusça (ru) 
* Sırpça (sr) 
* Slovakça (sk) 
* Slovence (sl) 
* İspanyolca (es) 
* İsveç dili (sv) 
* Tagalog dili (tl) 
* Tay dili (th) 
* Türkçe (tr) 
* Ukrayna dili (TR) 
* Vietnam dili (VI) 

## <a name="campaign"></a>Kampanya
Tooignore hello İzleyici itme kampanya bölümünü planlamak ve bu kampanyayı hello Reach API'sini aracılığıyla (ve bazı öğeler hello düşük düzey itme API ile) yerine göndermek gibi hello kampanya bölüm tooset hello adı ve kategori kampanyanızın de kullanabilirsiniz. Kategoriler, önceden tanımlanmış ayarlarına dayanarak bir özel bildirim şablonu toocontrol uygulama bildirimleri ile kullanılabilir. Varolan "Kategoriler" Merhaba Reach API'sini aracılığıyla listesini elde edebilirsiniz.

> [!WARNING]
> Merhaba kampanya otomatik olarak göndermez, hello seçeneği "Yoksay İzleyici toousers hello API aracılığıyla bir gönderim" hello "Kampanya" bölümünde Reach kampanya kullanırsanız toosend gerekir, hello Reach API'sini kullanarak el ile.

![Reach Campaign3][22]

### <a name="option-applies-to"></a>Seçenek için geçerlidir:
* Ad: tüm
* Kategori: Duyurular, anketler
* Hedef kitleyi yok sayın itme toousers hello API üzerinden gönderilir: tüm

## <a name="notification"></a>Bildirim
Merhaba bildirim bölümü tooset temel ayarları, anında iletme dahil etmek için kullanabilirsiniz: Merhaba hello anında iletme, selamlama iletisine, bir uygulama görüntüsü başlığını veya atlanabilir tüm ise. Birçok bildirim belirli toohello platform aygıtınızın ayarlardır. "Uygulama" veya "uygulama dışında" bir gönderim seçebilirsiniz veya her ikisini de. (Kullanıcılar can "katılımı" veya "çevirin" dışında "uygulamasının" iter Merhaba işletim sistemi düzeyinde cihazlarına ve Azure Mobile Engagement almayacak unutmayın mümkün toooverride bu ayarı olabilir. Ayrıca "uygulama" Merhaba ulaşma API işler ve "uygulama dışı" iter unutmayın. "Hello itme API"uygulamasının out"çok iter kullanılan toohandle olabilir.) İter, resim veya HTML içeriğini, uygulama veya tooanother konumunuzda uygulamanız (Android SDK 2.1.0 veya gerekli sonraki hedefi kategorileri) dışında bağlama için ayrıntılı bağlantılar dahil olmak üzere özelleştirilebilir. Merhaba simgesini veya iOS rozet değiştirmek ve metin veya web içerik (html içerik, URL bağlantı tooanother konum içinde veya dışında hello uygulama popup) gönderin. Ayrıca, Android cihazları çaldır veya itme hello ile Titret. (, Android SDK izinler dosya tooring bildirim veya bir cihazı Titret doğru hello olduğunu unutmayın.) Var. şu anda hiçbir endüstri Android "büyük resimdeki" boyutları için standart ekran boyutlarına her cihazda farklı ancak neredeyse her ekran boyutuna 400 x 100 resimleri iş beri.

### <a name="delivery-types"></a>Teslim türleri:
* Yalnızca uygulama dışında: hello bildirim teslim edilemiyor hello kullanıcı Merhaba uygulaması kullanılmadığında.
* Uygulama yalnızca bildirim dışında Hello Apple veya Google (GCM ya da APNS sertifikası) bir sertifika gerektirir.
* Uygulama yalnızca: hello bildirim görüntülendiğinde yalnızca hello uygulama çalışırken.
* Merhaba bildirim hello Capptain teslim sistemi tooreach hello kullanıcı kullanır. Merhaba düzeni/görünümünü, anında tam olarak özelleştirebilirsiniz.
* Herhangi bir zaman: Veya değil ya da Merhaba uygulaması çalıştıran bildirim göndermek bu seçeneği sağlar.

![Reach Campaign4][23]

### <a name="option-applies-to"></a>Seçenek için geçerlidir:
* Bildirim: Duyurular, anketler

## <a name="content"></a>İçerik
Merhaba içerik bölümü toomodify hello içerik Duyurular, anketler, veri iter ve Kutucuklar (yalnızca Windows Phone) kullanabilirsiniz. Merhaba içerik anında iletme kampanyalarını kampanya belirli toohello türü ayarıdır. 

### <a name="see-also"></a>Ayrıca bkz.
* [UI belgeleri - ulaşmak - içerik gönderme][Link 29]

![Reach Campaign5][24]

## <a name="audience"></a>Hedef kitle
Kampanya veya kampanyanızı özelleştirilmiş ölçütlere göre sınırları hello İzleyici bölüm toodefine standart öğeleri toolimit listesini kullanabilirsiniz. Merhaba standart seçenekleri tooLimit kümesinin kitlenizi toopush tooeither yeni veya eski kullanıcılara veya yalnızca yerel gönderim kullanıcılar sağlar. Merhaba itme alma kullanıcıların kota toolimit hello sayısını da ayarlayabilirsiniz. El ile nasıl kampanyanızı filtrelenmiş tooinclude olduğu için hello ifade düzenleyebileceğiniz bir veya daha fazla ölçüt tootarget kullanıcı. Bir hedef kitle ifadesi el ile yazabilirsiniz. Bu tür bir ifade hello ölçütler arasındaki ilişkiyi açıkça tanımlamanız gerekir. Bir ölçüt büyük harfle başlamalı ve boşluk içeremez bir tanımlayıcı tarafından tanımlanır. Merhaba ölçütler arasındaki ilişkiyi Hello kullanarak tanımlanabilen 'and', 'or', 'not' işleçleri yanı sıra '(',')'. Örnek: "Criterion1 veya (Criterion1 ve değil Criterion2)".

> [!NOTE]
> Kampanyalarda bulunan büyük bir izleyici ile tarama hedefleme hello sunucu tarafı yavaş olabilir, özellikle toostart çalışırsanız, birden çok Kampanyalar aynı hello zaman.

* Mümkünse, yalnızca bir kampanya aynı anda başlatın.
* En çok yalnızca başlangıç dört kampanyaları birer birer hello.
* Yalnızca tooyour etkin kullanıcıları itme (onay kutusu "yalnızca yerel gönderim kullanılarak ulaşılabilen kullanıcıları devreye" ve "yalnızca etkin kullanıcıları göster") böylece hala hello uygulamasını yüklemediyseniz ve kullanmak, kullanıcılarınızın taranan toobe gerekir.
  Kitlenizi tanımlandığında hello kullanabilirsiniz kaç kullanıcının bu anında alacaksınız çıkışı düğmesi toofind benzetimini. Bu, büyük olasılıkla (Bu kullanıcıların rastgele bir örneği temel alarak bir tahmindir) Bu İzleyici tarafından hedeflenen bilinen kullanıcıların sayısını hello işlem. Merhaba uygulamayı kaldırmış kullanıcıların da bu hedef kitleye dahil olduğu, ancak ulaşılamıyor unutmayın.

### <a name="see-also"></a>Ayrıca bkz.
* [UI belgeleri - Reach - yeni itme ölçüt][Link 28]

![Reach Campaign6][25]

### <a name="edit-expression"></a>İfade Düzenle
![Reach Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a>Hedef kitle seçeneğinizi uygulandığı sınırı:
* Yalnızca bir kullanıcı alt kümesini göster: tüm (Duyurular, anketler, veri iter, kutucukları)
* Yalnızca eski kullanıcıları göster: tüm (Duyurular, anketler, veri iter, kutucukları)
* Yalnızca yeni kullanıcıları göster: tüm (Duyurular, anketler, veri iter, kutucukları)
* Yalnızca boştaki kullanıcıları göster: Duyurular, anketler, döşeme
* Yalnızca etkin kullanıcıları göster: tüm (Duyurular, anketler, veri iter, kutucukları)
* Yalnızca yerel gönderim kullanılarak ulaşılabilen kullanıcıları devreye sok: Duyurular, anketler

## <a name="time-frame"></a>Zaman çerçevesi
Merhaba gönderim veya başlangıç zamanını boş toostart hello kampanya hemen bırakabilirsiniz hello zaman çerçevesi bölüm tooset kullanabilirsiniz. Hello son saat dilimi kullanarak hello kampanya kullanıcılarınızın Asya'da bekler ve iter birer birer hello world eşleşme hello zaman çerçevesi içindeki tüm saat dilimleri için kampanyanızı ayarlanıncaya kadar küçük toplu Gönder'den önceki bir gün başlayabilir, unutmayın. Merhaba itme başlatmadan önce toorequest hello zaman hello telefondan olduğundan hello son kullanıcıların saat dilimi kullanarak da gecikmeler kampanyalarda neden olabilir.

> [!NOTE]
> Bitiş tarihi önbelleğe alabilir olmadan kampanyaları iter yerel olarak hala görünen ve bunları sonra el ile tam kampanyalar. tooavoid Bu davranış, özel kampanyalar için bitiş zamanı.

### <a name="see-also"></a>Ayrıca bkz.
* [Ulaşmaya - nasıl yapılır – planlama][Link 3] 

![Reach Campaign8][27]

### <a name="settings-apply-to"></a>Ayarlar için geçerlidir:
* Zaman çerçevesi: Duyurular, anketler, döşeme

## <a name="test"></a>Test etme
Merhaba kampanya kaydetmeden önce bu itme tooyour kendi test aygıt hello Test bölümü toosend kullanabilirsiniz. Bu kampanya için özel tüm diller yapılandırdıysanız, her dilde hello itme test edebilirsiniz. "Hesabım" test aygıttan ayarlayabilirsiniz.

> [!NOTE]
> Merhaba düğmesini kullandığınızda veriler günlüğe kaydedilir hiçbir sunucu tarafı çok "test" iter, veriler yalnızca gerçek anında iletme kampanyalarını için günlüğe kaydedilir.

### <a name="see-also"></a>Ayrıca bkz.
* [UI belgeleri - hesabım][Link 14]

![Reach Campaign9][28]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

