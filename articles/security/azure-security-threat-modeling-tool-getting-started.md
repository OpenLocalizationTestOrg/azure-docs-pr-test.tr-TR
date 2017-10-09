---
title: "aaaGetting başlatıldı - Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
description: "Bu eylemin hello tehdit modelleme aracı vurgulama daha derin bir genel bakıştır."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 75ef139071e8abd0e743aa17b443a6e353f29372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-threat-modeling-tool"></a>Merhaba tehdit modelleme aracı ile çalışmaya başlama

Bu yılın ücretsiz olarak Hello Bulut ve kurumsal güvenlik araçları takım yayımlanan hello tehdit modelleme aracı Önizleme  **[tıklatın indirme](https://aka.ms/tmtpreview)**. teslim mekanizması Hello değişikliği bize kolaylaştırarak toomaintain ve kullanım hello aracı her açışlarında toopush hello en son geliştirmeleri ve hata düzeltmeleri toocustomers sağlar.
Bu makalede hello süreci yaklaşım modelleme hello Microsoft SDL tehdidin Başlarken alır ve nasıl toouse hello aracı toodevelop harika tehdit güvenlik işleminin omurga olarak modeller gösterir.

Bu makale üzerinde mevcut yaklaşım modelleme hello SDL tehdit bilgilerini oluşturur. Hızlı bir gözden geçirme için çok başvuran**[tehdit modelleme Web uygulamaları](https://msdn.microsoft.com/library/ms978516.aspx)**  ve arşivlenen bir sürümünü  **[ortaya çıkarmaya güvenlik açıkları kullanarak hello STRIDE yaklaşım](https://docs.google.com/viewer?a=v&pid=sites&srcid=ZGVmYXVsdGRvbWFpbnxzZWN1cmVwcm9ncmFtbWluZ3xneDo0MTY1MmM0ZDI0ZjQ4ZDMy)**  MSDN makalesi, 2006'yayımlandı.

tooquickly Özetle, diyagram oluşturma, tehditleri tanımlamak, bunları Azaltıcı ve her azaltma doğrulama hello yaklaşım içerir. Bu işlem vurgular bir diyagram şöyledir:

![SDL işlemi](./media/azure-security-threat-modeling-tool/sdlapproach.png)

## <a name="starting-hello-threat-modeling-process"></a>Merhaba tehdit modelleme işlemi başlatılıyor

Merhaba tehdit modelleme aracı başlattığında, hello resimde görüldüğü gibi birkaç şeyi görürsünüz:

![Boş başlangıç sayfası](./media/azure-security-threat-modeling-tool/tmtstart.png)

### <a name="threat-model-section"></a>Tehdit modeli bölümü

| Bileşen                                   | Ayrıntılar                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Geri bildirim, öneriler ve sorunları düğmesi** | Alır, hello  **[MSDN Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sdlprocess)**  her şey SDL için. Diğer kullanıcıların, geçici çözümler ve öneriler birlikte gerçekleştirdiği aracılığıyla bir fırsat tooread sağlar. Aradığınızı hala bulamıyorsanız, e-posta tmtextsupport@microsoft.com bizim destek ekibi toohelp için                                                                                                                            |
| **Bir Model oluşturma**                          | Boş bir tuval, toodraw için diyagram açılır. Hangi şablonu emin tooselect yapmak için modelinizin toouse istiyorsunuz                                                                                                                                                                                                                                                                                                                                                                       |
| **Yeni modelleri için şablonu**                 | Bir modeli oluşturmadan önce hangi şablon toouse seçmeniz gerekir. Hello Azure özel şablonlar, tehditleri ve bunları azaltmanın yollarını içeren Azure tehdit modeli şablon bizim ana şablonudur. Genel modellerini hello SDL TM Bilgi Bankası hello açılır menüsünden seçin. Kendi şablonunuzu toocreate istediğiniz veya tüm kullanıcılar için yeni bir tane gönderme? Kullanıma bizim  **[şablonu deposu](https://github.com/Microsoft/threat-modeling-templates)**  GitHub sayfası toolearn daha fazla                              |
| **Bir Model açın**                            | <p>Açılır tehdit modelleri önceden kaydedilmiş. Merhaba son açılan modelleri en son dosyalarınızı tooopen gerekiyorsa harika özelliğidir. Merhaba seçimin üzerine geldiğinizde, 2 yolları tooopen modelleri bulabilirsiniz:</p><p><ul><li>Açık bu bilgisayardan – yerel depolama kullanarak bir dosyayı açma Klasik yolu</li><li>Açık OneDrive üzerinden – takımlar OneDrive toosave klasörlerde kullanın ve tüm tehdit modellerini bir tek bir konum toohelp artış üretkenliği ve işbirliği paylaşmak için kullanabileceğiniz</li></ul></p> |
| **Başlarken Kılavuzu**                   | Açılır hello  **[Microsoft tehdit modelleme aracı](./azure-security-threat-modeling-tool.md)**  ana sayfası                                                                                                                                                                                                                                                                                                                                                                                            |

### <a name="template-section"></a>Şablon bölümü

| Bileşen               | Ayrıntılar                                                                                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Yeni şablon oluşturun** | Üzerinde toobuild için boş bir şablon açar. Şablonları sıfırdan oluşturmanın kapsamlı bilgi yoksa var olanları gelen toobuild öneririz |
| **Şablonunu Aç**       | Şablonlar için toomake değişiklikleri çok mevcut açar                                                                                                             |

Merhaba tehdit modelleme aracı takım tooimprove aracı işlevselliği ve deneyimi sürekli çalışmaktadır. Birkaç küçük değişiklikler hello hello yıl boyunca gerçekleşmesi, ancak yeniden yazdırmaya Başlangıç Kılavuzu'ndaki tüm önemli değişiklikler gerektirir. Tooit başvurmak genellikle tooensure hello son Duyurular alın.

## <a name="building-a-model"></a>Bir model oluşturma

Bu bölümde, biz izleyin:

- Cristina (Geliştirici)
- Attila (program Yöneticisi) ve
- (Bir tester) olan Ashish

Bunlar ilk kendi tehdit modeli geliştirmek hello sürecinde adımıdır.

> Attila: Merhaba Cristina, hello tehdit modeli diyagram üzerinde çalışılan ve toomake emin istedik biz hello ayrıntıları sağ aldı. Beni Ara onu yardımcı olabilir?
> Cristina: kesinlikle. Bir göz atalım.
> Attila hello aracı açılır ve kendi ekran Cristina ile paylaşır.

![Temel tehdit modeli](./media/azure-security-threat-modeling-tool/basictmt.png)

> Cristina: Tamam, sonucunun görünüyor, ancak, bana üzerinden yol?
> Attila: emin! Merhaba dökümü şöyledir:
> - Bizim insan kullanıcı dışında bir varlık olarak çizilir — kare
> - Komutları tooour Web sunucusu gönderiyorsanız — hello daire
> - Merhaba Web sunucusu (iki paralel satırları) veritabanı danışmanlık

Ne Attila Cristina yalnızca gösterdi DFD, kısaltması olan  **[veri akış diyagramı](https://en.wikipedia.org/wiki/Data_flow_diagram)**. Merhaba tehdit modelleme aracı hello kırmızı noktalı çizgiler, farklı varlıklar denetiminde nerede tooshow belirttiği, kullanıcıların toospecify güven sınırları sağlar. Örneğin, BT yöneticileri Hello Active Directory kendi denetimi dışında olacak şekilde kimlik doğrulama amacıyla bir Active Directory sistemi gerektirir.

> Cristina: sağ toome arar. Merhaba tehditler hakkında neler?
> Attila: bana, Göster olanak tanır.

## <a name="analyzing-threats"></a>Tehditler analiz etme

Merhaba analiz görünümünü adlı hello SDL yaklaşım kullanan hello simgesi menü seçimi (ki tooa listesi hello varsayılan şablona göre oluşturulan tehditleri hello bulunan tehdit modelleme aracı alınır dosyayla Büyüteç) üzerinde tıklatır sonra  **[ STRIDE (, oynama, bilgi açıklama, hizmet reddi ve ayrıcalıkların kimlik sahtekarlığı)](https://en.wikipedia.org/wiki/STRIDE_(security))**. Merhaba yazılım bu 6 kategorileri kullanarak bulunabilir tehditleri tahmin edilebilir bir kümesi altında geldiğini olur.

Her kapı ve pencere sağlayarak evinizde güvenliğini sağlama kilitleme mekanizması bir alarm sistemi ekleme veya hello hırsız sonra birleştirme önce olduğu gibi bu yaklaşımdır.

![Temel tehditleri](./media/azure-security-threat-modeling-tool/basicthreats.png)

Attila hello hello listesindeki ilk öğeyi seçerek başlar. Şunlar olur:

Merhaba iki şablonlar arasındaki hello etkileşim ilk olarak, Gelişmiş

![Etkileşim](./media/azure-security-threat-modeling-tool/interaction.png)

İkinci, ek bilgiler hello tehdit hakkında hello tehdit Özellikleri penceresinde görüntülenir

![Etkileşim bilgisi](./media/azure-security-threat-modeling-tool/interactioninfo.png)

oluşturulan hello tehdit ona olası tasarım açıkları anlamanıza yardımcı olur. Merhaba STRIDE kategori ona olası saldırı vektörlerinin hakkında bir fikir verir, tam olarak ne sahip yanlış, olası yolları toomitigate yanı sıra, başlangıç sırasında ek açıklama ona söyler. Kendisine hello doğrulama ayrıntıları düzenlenebilir alanların toowrite notları kullanın veya öncelik derecelendirmeleri kuruluşunun hata çubuğu bağlı olarak değiştirin.

Azure şablonları sahip ek ayrıntılar toohelp kullanıcıların kalmayıp aynı zamanda nasıl sorun nedir anlamasına toofix, açıklamalar, örnekler ve köprüleri tooAzure özgü belgeleri ekleyerek.

Merhaba açıklama yapılan ona hello önem fark sahte gelen bir kimlik doğrulama mekanizması tooprevent kullanıcı ekleme, hello ilk tehdit toobe ortaya üzerinde çalışılan. Birkaç dakika hello tartışması Cristina ile içine bunlar erişim denetimi ve rolleri uygulama hello önemini anladım. Attila bazı hızlı notları toomake bu uygulanan emin doldurulur.

Bilgilerin açığa çıkmasına altında hello tehditleri içine Attila oluştu gibi kendisinin hello erişim denetimi planı bazı salt okunur hesapları denetleme ve rapor oluşturma için gerekli gerçekleşmiş. Ki bu yeni bir tehdit olmalıdır, ancak bunları azaltmanın yollarını olan hello Merhaba, aynı, kendisinin uygun şekilde hello tehdit belirtildiği şekilde olup olmadığını hiç merak ettiniz.
Kendisi ayrıca bilgilerin açığa çıkmasına biraz daha zorlayıcı ve hello yedekleme bantlarını tooneed şifreleme, hello işletim ekibi için bir işi giderek gerçekleşmiş.

Uygulanamaz toohello tasarım tooexisting Azaltıcı ya da güvenlik nedeniyle garanti değiştirilebilir çok tehditleri "Değil geçerli" Merhaba durumu açılır. Diğer üç seçenek vardır: – varsayılan seçim, gereken araştırma – başlatılmamış kullanılan toofollow öğeleri ve Mitigated – tam olarak üzerinde çalıştığı sonra.

## <a name="reports--sharing"></a>Raporlar ve paylaşma

Attila Cristina hello listesiyle geçer ve önemli notlar ekler sonra Azaltıcı Etkenler/justifications, öncelik ve durum değişikliği, raporlar tam raporu -> bir iyi hangi yazdırır bakması aracılığıyla toogo ile rapor, kaydetme Oluştur -> he seçer İş arkadaşlarınızı tooensure hello uygun güvenlik iş uygulanır.

![Etkileşim bilgisi](./media/azure-security-threat-modeling-tool/report.png)

Bunun yerine Attila tooshare hello dosya isterse, kendisinin kolayca kuruluşunun OneDrive hesabınıza kaydederek bunu yapabilirsiniz. Kendisine yapan sonra kendisinin hello belge bağlantıyı Kopyala ve kendi iş arkadaşlarınızla paylaşın. 

## <a name="threat-modeling-meetings"></a>Tehdit modelleme toplantılar

Attila OneDrive, Ashish, hello tester kullanarak kendi tehdit modeli toohis iş arkadaşı gönderildiğinde underwhelmed. Atlanan kolayca tehlikeye girebilir oldukça birkaç önemli köşe durumlarda Attila ve Cristina gibi seemed. Kendi skepticism tamamlama toothreat modelleri ' dir.

Merhaba tehdit modeli Ashish sürdü sonra bu senaryoda, kendisinin iki tehdit modelleme toplantılar için çağrılır: hello işlem ve ilerlemesi hello diyagramları ve tehdit gözden geçirme ve oturum kapatma için ikinci bir toplantı aracılığıyla bir toplantı toosynchronize.

Hello ilk toplantıya, 10 dakika işlem modelleme hello SDL tehdit aracılığıyla herkesin taramasını Ashish harcanan. Kendisi bu hello tehdit modeli diyagram çekilen ve ayrıntılı olarak açıklayan başlatıldı. Beş dakika içinde önemli bir bileşen eksik tanımlanmış.

Birkaç dakika daha sonra Ashish ve Attila hello Web sunucusuna nasıl oluşturulmuş bir genişletilmiş tartışma aldı. Toplantı tooproceed için ideal yöntem hello değil, ancak herkes sonunda hello tutarsızlık erken keşfetme hello gelecekte zaman toosave yüklemesiyle kabul ediyorum.

Hello ikinci toplantı, hello tehditleri gitti hello takım bazı yolları tooaddress bunları ve imzalanmış ele kapalı hello tehdit modeli üzerinde. Bunlar hello belge kaynak denetimine iade ve geliştirmeye devam etti.

## <a name="thinking-about-assets"></a>Varlıkları hakkında düşünmeye

Modellenen tehdit olan bazı okuyucular, biz varlıkları hakkında bilgileri hiç açıklandı henüz olduğunu fark edebilirsiniz. Biz, birçok yazılım mühendisleri yazılımlarını varlıklar hello kavramı anlamaları ve hangi varlıkları saldırgan ilginizi çekebilir çok daha iyi anlamak keşfettiniz.

Toothreat kullanacaksanız bir ev model, aile, yerine yenisi konulamayacak fotoğraf veya değerli resmi göz önünde bulundurulması tarafından başlayabilir. Belki de göz önünde bulundurulması kimin kesilebilir ve hello geçerli güvenlik sistemi tarafından başlayabilir. Veya hello hello havuzu veya hello ön porch gibi fiziksel özellikleri dikkate alarak başlayabilir. Varlıklar, saldırganlar veya yazılım tasarımı hakkında benzer toothinking bunlar. Bu üç yaklaşımlardan birini çalışır.

Biz Burada sunulan hello yaklaşım toothreat modelleme önemli ölçüde ne Microsoft hello geçmiş yapmıştır daha basittir. Merhaba yazılım tasarım yaklaşımı birçok ekipler için iyi çalışır bulduk. Sizinki içeren umuyoruz.

## <a name="next-steps"></a>Sonraki Adımlar

Sorularınızı, açıklamalar ve sorunları Gönder tootmtextsupport@microsoft.com. **[Karşıdan](https://aka.ms/tmtpreview)**  hello tehdit modelleme aracı tooget başlatıldı.
