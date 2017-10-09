---
title: "Azure Güvenlik Merkezi'nde aaaDetection özellikleri | Microsoft Docs"
description: "Bu belge, Azure Güvenlik Merkezi algılama özelliklerinin nasıl çalıştığını toounderstand yardımcı olur."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 4c5599cc-99a1-430f-895f-601615ef12a0
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: d8001cc2acdd0026bd9b3596bbdfec56f8874513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-detection-capabilities"></a>Azure Güvenlik Merkezi algılama özellikleri
Bu belgede, Microsoft Azure kaynaklarınızı hedefleyen etkin tehditleri belirlemenize yardımcı olur ve hello Öngörüler sizinle toorespond hızla gerekli sağlayan Azure Güvenlik Merkezi'nin Gelişmiş algılama özelliklerini ele alınmaktadır.

> [!NOTE]
> Gelişmiş algılamalar hello standart katmanı, Azure Güvenlik Merkezi kullanılabilir. 60 günlük ücretsiz deneme sürümü mevcuttur. Merhaba hello fiyatlandırma katmanı seçimi yükseltme yapabilirsiniz [Güvenlik İlkesi](security-center-policies.md). Ziyaret [Güvenlik Merkezi sayfasını](https://azure.microsoft.com/pricing/details/security-center/) toolearn fiyatlandırma hakkında daha fazla bilgi. 
> 
> 

## <a name="responding-tootodays-threats"></a>Tootoday'nın tehditlerine yanıt verme
Olmuştur önemli değişiklikler hello tehdit ortamında hello son 20 yılda. Hello geçmiş, şirketler genellikle yalnızca çoğunlukla görme "yapabileceklerini" ilgilenen bireysel saldırganların web sitesi tahrifatından hakkında tooworry vardı. Bugün ise saldırganlar çok daha karmaşık ve organize hareket etmektedir. Saldırganlar genellikle belirli finansal ve stratejik hedeflere sahiptir. Bunlar ulus Devletler veya organize suç örgütleri tarafından finanse edilebildiklerinden aynı zamanda daha fazla kaynak kullanılabilir toothem, sahiptirler.

Bu yaklaşım tooan profesyonellik hello saldırganlar tarafında eşi görülmemiş düzeyine yol açmıştır. Saldırganlar artık web tahrifatı ile ilgilenmemektedir. Bunlar bilgileri, mali hesapları ve bunların tümü kullanabilecekleri gizli verileri çalmayla ilgilenmektedir artık toogenerate nakit hello açık Pazar veya tooleverage belirli bir ticari, siyasi veya Askeri konumdan. Mali hedefleri olan bu saldırganlardan ağları toodo zarar tooinfrastructure ve kişiler ihlal hello saldırganlar çok daha da fazla ile ilgili.

Yanıt olarak, kuruluşlar çoğunlukla hello Kurumsal çevrelerini veya uç noktaların bilinen saldırı imzalarını arayarak savunmaya odaklanan çeşitli noktası çözümleri dağıtın. Bu çözümlerin toogenerate güvenlik analist tootriage gerektirir ve araştırın düşük güvenilirlik uyarıları yüksek hacimli eğilimlidir. Çoğu kuruluş hello zaman olmaması ve uzmanlığa toorespond toothese uyarılar – pek çok olmayan gidin.  Bu sırada, saldırganlar kendi yöntemleri toosubvert çok sayıda imza tabanlı savunmayı gelişim göstermiştir ve [toocloud ortamları uyum](https://azure.microsoft.com/blog/detecting-threats-with-azure-security-center/). Yeni yaklaşımlar olan gerekli toomore hızlı bir şekilde ortaya çıkan tehditleri belirlemek ve algılama ile yanıtı hızlandırmak. 

## <a name="how-azure-security-center-detects-and-responds-toothreats"></a>Azure Güvenlik Merkezi nasıl algılar ve toothreats yanıt verir
Microsoft Güvenlik Araştırmacıları sürekli olarak tehditleri hello lookout bulunur. Bunlar Microsoft'un hello Bulut ve şirket içindeki genel varlığından alanından elde edilen telemetri erişim tooan korunmalarını kümesine sahip. Geniş kapsamlı ve çeşitlilik barındıran bu veri kümeleri koleksiyonunu Microsoft toodiscover yeni saldırı desenleri ve eğilimleri şirket içi müşteri ve kuruluş ürünlerinin yanı sıra arasında çevrimiçi hizmetleri sağlar. Sonuç olarak, saldırganlar yeni ve giderek karmaşık hale gelen sömürülerini ortaya çıkardıkça Güvenlik Merkezi algılama algoritmalarını hızlı bir şekilde güncelleştirebilmektedir. Bu yaklaşık hızlı hareket eden bir ortama ayak uydurmanıza yardımcı olmaktadır. 

Güvenlik Merkezi tehdit algılaması Azure kaynaklarını, hello ağ ve bağlı iş ortağı çözümlerinden güvenlik bilgileri otomatik olarak toplayarak çalışır. Genellikle birden fazla kaynaktan tooidentify tehditleri bilgileri ilişkilendirerek, bu bilgileri çözümler. Güvenlik uyarıları nasıl tooremediate hello tehdit ilişkin öneriler birlikte Güvenlik Merkezi'nde önceliklendirilir.

![Güvenlik Merkezi Veri toplama ve sunumu](./media/security-center-detection-capabilities/security-center-detection-capabilities-fig1.png)

Güvenlik Merkezi, imza tabanlı yaklaşımların ötesine geçen gelişmiş güvenlik analizleri kullanır. Büyük veri sıçramalar ve [makine öğrenme](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) teknolojilerdir çevrelerini tooevaluate olayları elle yaklaşımlar kullanılarak ve hello tahmin etmeye imkansız tooidentify olacak tehditler hello tüm bulut yapısındaki – saldırıları evrimi. Bu güvenlik analizleri şunlardır: 

* **Tümleşik tehdit bilgileri**: görünüyor Microsoft ürünleri ve Hizmetleri, küresel tehdit bilgilerinden yararlanarak bilinen kötü aktörleri hello için Microsoft dijital Suçlar birimi (DCU), hello Microsoft Güvenlik Yanıt Merkezi (MSRC) ve dış akışları.
* **Davranış analizi**: bilinen desenleri toodiscover kötü amaçlı davranış uygulanır. 
* **Anomali algılama**: geçmiş taban çizgisi toobuild profil istatistiksel kullanır. Tooa olası saldırı vektörüne uygun olan yerleşik taban çizgilerinden sapmalar konusunda uyarır.

### <a name="threat-intelligence"></a>Tehdit bilgileri
Microsoft yoğun miktarda genel tehdit bilgisine sahiptir. Telemetri, Azure gibi birden fazla kaynaktan Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, hello Microsoft dijital Suçlar birimi (DCU) ve Microsoft Güvenlik Yanıt Merkezi (MSRC) akar. Araştırmacılar ayrıca büyük bulut hizmeti sağlayıcıları arasında paylaşılan ve Üçüncü taraflardan toothreat akışlarına abone tehdit Bilgileri'ni alırsınız. Azure Güvenlik Merkezi, bu bilgileri tooalert kullanabilir, bilinen kötü aktörlerden gelen toothreats. Bazı örnekler:

* **Giden iletişim tooa kötü amaçlı IP adresi**: botnet veya darknet bilinen giden trafiği tooa, kaynağınızın tehlikeye ve bir saldırgan tooexecute çalıştığından, sistem ya da verileri üzerinde komutları gösterir. Azure Güvenlik Merkezi, ağ trafiğini tooMicrosoft'ın genel tehdit veritabanıyla karşılaştırır ve iletişim tooa kötü amaçlı IP adresi algılarsa sizi uyarır.

## <a name="behavioral-analytics"></a>Davranış analizi
Davranış analizi, analiz eden ve bilinen modeller veri tooa koleksiyonuyla karşılaştıran bir tekniktir. Ancak, bu modeller basit imzalar değildir. Bunlar uygulanan toomassive veri kümeleri olan karmaşık machine learning algoritmaları belirlenen var. Bunlar, kötü amaçlı davranışların uzman analistler tarafından dikkatlice çözümlenmesiyle de belirlenir. Azure Güvenlik Merkezi sanal makine günlükleri, sanal ağ cihaz günlükleri, yapı günlükleri, kilitlenme bilgi dökümleri ve diğer kaynakları analize dayalı davranış analizi tehlikeye tooidentify kaynakları kullanabilir. 

Ayrıca, yaygın bir kampanyanın kanıt desteklemek için diğer sinyaller toocheck ile bağıntı yoktur. Bu bağıntı yerleşik tehlike göstergeleriyle tutarlı tooidentify olayları yardımcı olur. Bazı örnekler:

* **Şüpheli işlem yürütme**: saldırganlar tespit birkaç teknikleri tooexecute kötü amaçlı yazılım algılama olmadan. Örneğin, bir saldırganın kötü amaçlı yazılım hello yasal sistem dosyalarıyla aynı adlar verin ancak bu dosyaları alternatif bir konuma yerleştirmek için çok benzer tooa zararsız dosya veya maskesi hello dosyanın gerçek uzantısını bir ad kullanın. Güvenlik Merkezi modelleri, davranışları işler ve izleyiciler gibi bu yürütmeleri toodetect aykırı değerlerini işler.  
* **Gizli kötü amaçlı yazılım ve istismarı denemeleri**: karmaşık kötü amaçlı yazılımlar hiçbir zaman toodisk yazma veya diske depolanmış yazılım bileşenlerini şifreleyerek mümkün tooevade geleneksel kötü amaçlı yazılımdan koruma ürünleri değil.  Merhaba kötü amaçlı yazılım sipariş toofunction bellekte izlemeleri bırakmalıdır gibi ancak, bu tür kötü amaçlı yazılım bellek analizi kullanılarak algılanabilir. Yazılım kilitlendiğinde bir kilitlenme dökümü hello kilitlenme hello aynı anda belleğin bir kısmını yakalar.  Merhaba kilitlenme döküm Hello bellekte analiz ederek Azure Güvenlik Merkezi teknikleri kullanılan tooexploit güvenlik açıkları yazılımda algılayabilir, gizli verilere erişebilir ve gizlice sızmak hello performansını etkileyen olmadan tehlikeye giren bir makineye makinenizde.
* **Yanal hareket ve iç keşif**: toopersist güvenliği aşılmış bir ağ ve bulmak/toplamak değerli veri saldırganlar genellikle toomove yanal tehlikeye hello gelen deneyin içinde makine tooothers hello aynı ağ. Güvenlik Merkezi işlem izler ve oturum açma etkinlikleri sipariş toodiscover tooexpand bir saldırganın uzaktan komut yürütme, ağ araştırma gibi hello ağ ve hesap numaralandırma içinde çalışır.
* **Kötü amaçlı PowerShell komut dosyalarını**: PowerShell kullanılan hedef sanal makinelerde tooexecute kötü amaçlı kod saldırganlar tarafından çeşitli amaçlarla için. Güvenlik Merkezi şüpheli etkinliklerin kanıtı için PowerShell etkinliğini inceler. 
* **Giden saldırılar**: saldırganlar genellikle bulut kaynaklarını bu kaynakları toomount ek saldırılarını kullanmasını hello amacı hedef. Riskli sanal makineler, örneğin, diğer sanal makinelere karşı deneme yanılma saldırıları kullanılan toolaunch olması, istenmeyen posta göndermek veya açık bağlantı noktalarını Tara ve Internet üzerindeki diğer cihazlar hello. Makine uygulayarak giden ağ iletişimlerinin hello normu aştığını toonetwork trafiği öğrenme, Güvenlik Merkezi algılayabilir. Merhaba posta büyük olasılıkla olup istenmeyen posta hello durumda Güvenlik Merkezi de olağandışı e-posta trafiğini Office 365 toodetermine'ten ile karşılık gelen alınan ya da bir meşru e-posta kampanya hello sonucu.  

### <a name="anomaly-detection"></a>Anormallik algılama
Azure Güvenlik Merkezi, ayrıca anomali algılama tooidentify tehditleri kullanır. (Bu, büyük veri kümelerinden türetilmiş bilinen modellere bağlıdır) Karşıtlık toobehavioral analytics'te anomali algılama daha fazla "kişiselleştirilmiştir" ve belirli tooyour dağıtımları temelleri odaklanır. Machine learning dağıtımlarınızın normal etkinliğini uygulanan toodetermine, ve bir güvenlik olayını gösterebilecek aykırı değer koşullarını oluşturulan toodefine kurallardır. Bir örneği aşağıda verilmiştir:

* **Gelen RDP/SSH deneme yanılma saldırıları**: Dağıtımlarınız her gün çok sayıda oturumun açıldığı yoğun sanal makineler ve çok az oturumun açıldığı ya da hiç oturum açılmayan sanal makineler içerebilir. Azure Güvenlik Merkezi bu sanal makineler için taban çizgisi oturum açma etkinliğini belirler ve machine learning toodefine normal oturum açma etkinliğinin dışındaki nedir kullanın. Oturum açma Hello sayısı veya hello oturumlar veya hangi hello açmanın istendiği hello konumu hello saati veya diğer oturum açma ile ilgili özellikleri hello taban çizgisinden önemli ölçüde farklı ise, bir uyarı oluşturulabilir. Yine machine learning neyin önemli olduğunu belirler.

## <a name="continuous-threat-intelligence-monitoring"></a>Sürekli tehdit bilgisi izleme
Azure Güvenlik Merkezi hello tehdit kapsamındaki değişiklikleri sürekli olarak izleyen güvenlik araştırması ve veri bilimi ekipleri çalıştırır. Bu girişimleri aşağıdaki hello içerir:

* **Tehdit bilgisi izleme**: Tedit bilgileri, var olan veya yeni ortaya çıkan tehditlere ilişkin mekanizma, gösterge, etkiler ve uygulanabilir öneriler içerir. Bu bilgiler hello güvenlik topluluğu içinde paylaşılır ve Microsoft iç ve dış kaynaklardan gelen tehdit bilgisi akışlarını sürekli olarak izler.
* **Sinyal paylaşımı**: Microsoft'un bulut ve şirket içi hizmetler, sunucular ve istemci uç noktası cihazları içeren geniş portföyünde güvenlik ekiplerinden alınan bilgiler paylaşılır ve analiz edilir. 
* **Microsoft güvenlik uzmanları**: Microsoft’ta hukuk ve web saldırıcı algılama gibi uzman güvenlik alanlarında çalışan ekiplerle sürekli iletişim.
* **Algılama ayarı**: Gerçek müşteri veri kümelerine göre algoritmalar çalıştırılır ve güvenlik Araştırmacıları müşteriler toovalidate hello sonuçları. TRUE ve false kullanılan toorefine machine learning algoritmaları durumlarıdır.

Hangi konumdan anında yararlanabilirsiniz yeni ve geliştirilmiş algılama içinde bu birleşik çabalar culminate –, tootake için bir eylem yok.

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, tooAzure Güvenlik Merkezi algılama özelliklerinin nasıl çalıştığı hakkında bilgi edindiniz. Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi Planlama ve İşlemler Kılavuzu](security-center-planning-and-operations-guide.md)
* [Yönetme ve Azure Güvenlik Merkezi'nde toosecurity uyarılarını yanıt](security-center-managing-and-responding-alerts.md)
* [Azure Güvenlik Merkezi’nde Türe Göre Güvenlik Uyarıları](security-center-alerts-type.md)
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) — nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) — nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.

