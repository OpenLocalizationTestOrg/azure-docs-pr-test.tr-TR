---
title: "Güvenlik Merkezi tehdit Intelligence rapor aaaAzure | Microsoft Docs"
description: "Bu belge, toouse Azure Güvenlik Merkezi tehdit akıllı raporları bir araştırma toofind sırasında bir güvenlik uyarısı ilgili daha fazla bilgi yardımcı olur."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: c888cfac1dd8b057616a6b8e6c6f6b67b552f2e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a>Azure Güvenlik Merkezi Tehdit Zekası Raporu
Bu belge, Azure Güvenlik Merkezi Tehdit Zekası Raporlarının, güvenlik uyarılarını oluşturan tehditler hakkında daha fazla bilgi edinmenize nasıl yardımcı olabileceğini açıklamaktadır.

## <a name="what-is-a-threat-intelligence-report"></a>Tehdit zekası rapor nedir?
Güvenlik Merkezi tehdit algılaması Azure kaynaklarını, hello ağ ve bağlı iş ortağı çözümlerinden güvenlik bilgileri izleme ile çalışır. Genellikle birden fazla kaynaktan tooidentify tehditleri bilgileri ilişkilendirerek, bu bilgileri çözümler. Bu işlem hello Güvenlik Merkezi bir parçasıdır [algılama özellikleri](security-center-detection-capabilities.md).

Güvenlik Merkezi tarafından bir tehdit algılandığında, belirli bir olay için düzeltme önerileri de dahil olmak üzere ayrıntılı bilgiler içeren bir [güvenlik uyarısı](security-center-managing-and-responding-alerts.md) tetikler. tooassist olay yanıtlama ekipleri araştırmak ve tehditleri düzeltme, Güvenlik Merkezi, gibi bilgiler dahil olmak üzere algılandı hello tehdit hakkında bilgi içeren bir tehdit Intelligence rapor içerir:

* Saldırganların kimliği veya bağlantıları (bu konuda bilgi varsa)
* Saldırganların hedefleri
* Güncel ve geçmiş saldırı kampanyaları (bu konuda bilgi varsa)
* Saldırganların taktikleri, araçları ve yordamları
* URL’ler ve dosya karmaları gibi ilgili tehlike göstergeleri (IoC)
* Merhaba endüstri ve coğrafi yaygınlığını tooassist victimology size Azure kaynaklarınızı risk altında olup olmadığını belirleme
* Azaltma ve düzeltme bilgileri

> [!NOTE]
> Merhaba miktarda bilgi herhangi bir rapordaki değişir; ayrıntı düzeyini Hello hello kötü amaçlı yazılımın etkinliği ve yaygınlığını dayanır.
>
>

Güvenlik Merkezi according toohello saldırı değişebilir tehdit raporları üç tür vardır. kullanılabilir Hello raporlar şunlardır:

* **Etkinlik Grubu Raporu**: Saldırganlar, amaçları ve taktikleri hakkında ayrıntılı bilgi sunar.
* **Kampanya Raporu**: Belirli saldırı kampanyaların ayrıntılarına odaklanır.
* **İş parçacığı özet raporu**: hello önceki iki raporlarında hello öğelerin tümünü kapsar.

Bu tür bilgiler hello sırasında faydalıdır [olay yanıtlama](security-center-incident-response.md) işlem, bir sürekli araştırma toounderstand hello kaynak hello saldırı, saldırganın hello sözleri ve ne olduğu toodo toomitigate bu ilerleyen sorun.

## <a name="how-tooaccess-hello-threat-intelligence-report"></a>Nasıl tooaccess tehdit Intelligence rapor hello?
Merhaba bakarak mevcut uyarılarınızı gözden geçirebilirsiniz **güvenlik uyarıları** döşeme. Hello Azure Portal'ı açın ve her uyarı hakkında daha fazla ayrıntı toosee hello adımları izleyin:

1. Merhaba Güvenlik Merkezi panosunda hello görürsünüz **güvenlik uyarıları** döşeme.
2. Merhaba döşeme tooopen hello tıklatın **güvenlik uyarıları** hello uyarılar hakkında daha fazla ayrıntı içeren ve daha fazla bilgi tooobtain istediğiniz hello güvenlik uyarısı tıklatın dikey hakkında.

    ![Güvenlik uyarıları](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. Bu durumda hello **yürütülen şüpheli işlem** dikey penceresinde hello hello aşağıdaki çizimde gösterildiği gibi hello uyarı ayrıntılarını gösterir:

    ![Güvenlik uyarısı ayrıntıları](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. Merhaba miktarda bilgi her güvenlik uyarı için kullanılabilir uyarı according toohello türü değişir. Merhaba, **RAPORLARI** alan bir bağlantı toohello tehdit yönetim bilgileri raporu vardır. Bağlantıya tıkladığınızda PDF dosyası yeni bir tarayıcı penceresinde açılacaktır.

   ![Storage seçimi](./media/security-center-threat-report/security-center-threat-report-fig3.png)

Buradan PDF için bu raporu ve okuma hello güvenlik hakkında daha fazla sorunu algılandı hello indirin ve sağlanan hello bilgilere göre eylemleri gerçekleştirin.

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede Azure Güvenlik Merkezi Tehdit Zekası Raporlarının güvenlik uyarısı araştırmaları sırasında nasıl yardımcı olabileceğini öğrendiniz. Azure Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi SSS](security-center-faq.md). Merhaba Hizmeti'ni kullanma hakkında sık sorulan soruları bulabilirsiniz.
* [Olay Yanıtı için Azure Güvenlik Merkezi’nden Yararlanma](security-center-incident-response.md)
* [Azure Güvenlik Merkezi algılama özellikleri](security-center-detection-capabilities.md)
* [Azure Güvenlik Merkezi planlama ve işlemler kılavuzu](security-center-planning-and-operations-guide.md). Bilgi nasıl tooplan ve hello tasarım konuları tooadopt Azure Güvenlik Merkezi anladığınızdan emin olun.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md). Bilgi nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi'nde Güvenlik Olayını İşleme](security-center-incident.md)
* [Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/). Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulun.
