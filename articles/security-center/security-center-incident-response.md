---
title: "Azure Güvenlik Merkezi ile aaaRespond toosecurity olaylar | Microsoft Docs"
description: "Bu belgede nasıl toouse Azure Güvenlik Merkezi için bir olay yanıtlama senaryosu açıklanmaktadır."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 8af12f1c-4dce-4212-8ac4-170d4313492d
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: aaf50c0c7e774d03d517c3fd11686dbae48dd29b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-security-center-for-an-incident-response"></a>Olay yanıtı için Azure Güvenlik Merkezi’ni kullanma
Birçok kuruluş öğrenin nasıl yalnızca bir saldırı karşılaşan sonra toorespond toosecurity olaylar. tooreduce maliyetleri ve zarar, bir olay yanıtlama planlama yerinde bir saldırı gerçekleşmeden önce önemli toohave sağlanır. Bir olay yanıtının farklı aşamalarında Azure Güvenlik Merkezi’ni kullanabilirsiniz.

## <a name="incident-response-planning"></a>Olay yanıtı planlaması
Etkili bir plan üç çekirdek özelliklerine bağlıdır: mümkün tooprotect olmaya, algılamanıza ve yanıtlamanıza toothreats. Olaylar önleme hakkında koruma olması, tehditleri erken tanımlama hakkında algılama olması ve hello saldırgan çıkarma ve sistemler toomitigate hello etkileri bir ihlal geri yükleme hakkında cevaptır.

Bu makalede hello güvenlik olay yanıtlama aşamaları hello gelen kullanacağı [Microsoft Azure güvenlik hello bulut yanıtta](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678) hello Aşağıdaki diyagramda gösterildiği gibi makale:

![Olay yanıtı yaşam döngüsü](./media/security-center-incident-response/security-center-incident-response-fig1.png)

Merhaba algıla, değerlendirin ve Tanıla aşamaları sırasında Güvenlik Merkezi'ni kullanabilirsiniz. Güvenlik Merkezi hello üç ilk olay yanıtlama aşamaları sırasında nasıl yararlı olabilir örnekleri şunlardır:

* **Algılama**: hello ilk göstergesi bir olay araştırma gözden geçirin.
  * Örnek: yüksek öncelikli güvenlik uyarısı hello Güvenlik Merkezi panosunda gerçekleşmesine neden olan gözden geçirme hello ilk doğrulama.
* **Değerlendirme**: hello ilk değerlendirme tooobtain hello şüpheli etkinlik hakkında daha fazla bilgi gerçekleştirin.
  * Örnek: Merhaba güvenlik uyarısı hakkında daha fazla bilgi edinin.
* **Tanılama**: teknik bir inceleme gerçekleştirme, kapsamı tanımlama, giderme ve geçici çözüm stratejileri.
  * Örnek: Bu belirli güvenlik uyarısı Güvenlik Merkezi tarafından açıklanan hello düzeltme adımlarını izleyin.

izleyen hello senaryo nasıl tooleverage Güvenlik Merkezi sırasında hello bir güvenlik olayı algıla, değerlendirin ve Tanıla/yanıt aşamalarını gösterir. Güvenlik Merkezi'nde bir [güvenlik olayı](security-center-incident.md), bir kaynağın [sonlandırma zinciri](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) desenleri ile hizalanan tüm uyarılarının toplamıdır. Olaylar görünür hello [güvenlik uyarıları](security-center-managing-and-responding-alerts.md) döşeme ve dikey. Bir olay, tooobtain sağlayan hello ilgili uyarıların listesi, her oluşumu hakkında daha fazla bilgi gösterir. Güvenlik Merkezi, tek başına kullanılan tootrack kuşkulu bir etkinlik aşağı de olabilir güvenlik uyarıları da gösterir.

## <a name="scenario"></a>Senaryo
Contoso son bazı SQL veritabanları ve sanal makine tabanlı iş satır yükleri de dahil olmak üzere kendi şirket içi kaynakları tooAzure bazıları geçirildi. Contoso'nun Çekirdek Bilgisayar Güvenliği Olay Yanıtı Ekibi (CSIRT) şu anda geçerli olay yanıtı araçlarıyla tümleşik güvenlik bilgileri olmadığı için güvenlik sorunlarını araştırmayla ilgili bir sorun yaşamaktadır. Bu tümleştirme eksiği hello Algıla aşama (çok sayıda hatalı pozitif sonuç) sırasında yanı sıra hello değerlendirin ve Tanıla aşamaları sırasında bir sorun tanıtır. Bu geçişin bir parçası olarak, bunlar tooopt karar içinde Güvenlik Merkezi toohelp için bunları bu sorunu çözün.

Bu geçiş tamamlanmış ilk aşamasında, sonra edildi hello tüm kaynakları ve tüm Güvenlik Merkezi'nde güvenlik önerilerini hello ele. Contoso CSIRT hello odak bilgisayar güvenlik olaylarını postalarla noktasıdır. bir grubun tüm güvenlik olayı ilgilenmek için sorumluluklarını kişilerin Hello takım oluşur. Merhaba takım üyeleri açıkça sınamayla yanıtının alanı sol görevlerini tooensure tanımladınız.

Bu senaryo Hello amaçla Contoso CSIRT parçası olan kişiler aşağıdaki hello hello rollerinde toofocus oluşturacağız:

![Olay yanıtı yaşam döngüsü](./media/security-center-incident-response/security-center-incident-response-fig2.png)

Zehra güvenlik operasyonlarında görev almaktadır. Sorumlulukları şunlardır:

* İzleme ve başlangıç saati geçici toosecurity tehditleri yanıt.
* Toohello bulut iş yükü sahibi ya da gerektiği gibi güvenlik Analistin yükselen.

Vedat bir güvenlik analiz uzmanıdır ve aşağıdaki sorumluluklara sahiptir:

* Saldırıları araştırma.
* Uyarıları düzeltme.
* İş yükü sahipleri toodetermine ile çalışma ve bunları azaltmanın yollarını uygulayın.

Gördüğünüz gibi Gamze ve Sam farklı sorumlulukları vardır ve tooshare Güvenlik Merkezi bilgi birlikte çalışmalısınız.

## <a name="recommended-solution"></a>Önerilen çözüm
Gamze ve Sam farklı roller sahip olduğundan, bunlar Güvenlik Merkezi tooobtain ilgili bilgileri işleminin farklı alanları günlük etkinliklerini için kullanırsınız. Zehra günlük izleme görevinin bir parçası olarak **Güvenlik uyarılarını** kullanır.

![Güvenlik uyarıları](./media/security-center-incident-response/security-center-incident-response-fig3.png)

Gamze, güvenlik uyarıları hello Algıla ve değerlendirin aşamaları sırasında kullanır. Gamze hello ilk değerlendirme tamamlandıktan sonra ek araştırma gerekiyorsa aynen hello sorunu tooSam taşıyarak. Bu noktada, Sam Güvenlik Merkezi tarafından bazen diğer veri kaynakları ile birlikte toomove toohello Tanıla aşama sağlanan hello bilgileri kullanır.

## <a name="how-tooimplement-this-solution"></a>Nasıl tooimplement bu çözümü
toosee Azure Güvenlik Merkezi bir olay yanıtlama senaryoda kullanacağınız nasıl biz hello Algıla ve değerlendirme aşamasında Gamze'nın adımları izleyin ve sonra Sam yaptığı bakın toodiagnose hello sorun.

### <a name="detect-and-assess-incident-response-stages"></a>Olay yanıtının Algılama ve Değerlendirme aşamaları
Gamze toohello Azure portalında oturum ve hello Güvenlik Merkezi konsolunda çalışmaktadır. İzleme etkinlikleri kendi günlük bir parçası olarak kendisi aşağıdaki adımları gerçekleştirerek uyarıları hello yüksek öncelikli güvenlik gözden geçirme başlatıldı:

1. Merhaba tıklatın **güvenlik uyarıları** döşeme ve erişim hello **güvenlik uyarıları** dikey.
    ![Güvenlik uyarısı dikey penceresi](./media/security-center-incident-response/security-center-incident-response-fig4.png)

   > [!NOTE]
   > Bu senaryo Hello amaçla Gamze giderek tooperform hello kötü amaçlı SQL etkinlik uyarısı değerlendirmesine şekil önceki hello görülen aynıdır.
   >
   >
2. Hello tıklatın **kötü amaçlı SQL etkinliği** uyarı ve hello saldırıya hello kaynaklarında gözden **kötü amaçlı SQL etkinliği** dikey: ![Olay Ayrıntıları](./media/security-center-incident-response/security-center-incident-response-fig5.png)

    Bu dikey pencerede Gamze saldırıya hello kaynakları ile ilgili notlar nasıl yararlanabileceğinizi birçok kez Bu saldırının oldu ve bu zaman algılandı.
3. Merhaba tıklatın **kaynak saldırıya** tooobtain bu saldırı hakkında daha fazla bilgi.

Merhaba açıklamasını okuduktan sonra Gamze bu yanlış pozitif olmadığını ve aynen bu servis talebi tooSam İlerlet ikna.

### <a name="diagnose-incident-response-stage"></a>Tanılama olay yanıtı aşaması
SAM Gamze hello servis talebi alır ve Güvenlik Merkezi önerilen hello düzeltme adımları gözden geçirme başlatır.

![Olay yanıtı yaşam döngüsü](./media/security-center-incident-response/security-center-incident-response-fig6.png)

### <a name="additional-resources"></a>Ek kaynaklar
Merhaba olay yanıtlama takım ayrıca yararlanabilir hello [Güvenlik Merkezi Power BI](security-center-powerbi.md) yetenek toosee farklı türlerde raporlar. Bu raporlar daha fazla araştırma toovisualize sırasında Yardım çözümlemek ve önerileri ve güvenlik uyarılarını filtre. Ayrıca, güvenlik bilgileri ve Olay yönetimi (SIEM) çözümü hello araştırma işlemi sırasında kullandığı şirketler için yapabilir [Güvenlik Merkezi kendi çözümüyle tümleştirmek](security-center-integrating-alerts-with-log-integration.md). Hello kullanarak Azure denetim günlükleri ve sanal makine (VM) güvenlik olaylarını de tümleştirebilir [Azure günlük tümleştirme aracı](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/). tooinvestigate bir saldırı, Güvenlik Merkezi sağlar hello bilgi ile birlikte bu bilgiyi kullanabilirsiniz.

## <a name="conclusion"></a>Sonuç
Bir olay oluşmadan önce bir takım birleştirme çok önemli tooyour kuruluşunuzun ve olayların nasıl işleneceğini olumlu etkiler. Merhaba doğru Araçlar toomonitor kaynaklara sahip bu takım tootake doğru adımları tooremediate bir güvenlik olayı yardımcı olabilir. Güvenlik Merkezi [algılama özellikleri](security-center-detection-capabilities.md) BT tooquickly yanıt toosecurity olaylarını yardımcı olmak ve güvenlik sorunları düzeltin.
