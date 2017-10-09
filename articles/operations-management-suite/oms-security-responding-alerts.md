---
title: "aaaMonitoring ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözüm | Microsoft Docs"
description: "Bu belge, toouse hello tehdit Intelligence seçeneği OMS güvenlik ve denetim toomonitor kullanılabilir yardımcı olur ve toosecurity uyarıları yanıt."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 3d92b6809b7bd934c889afc119e5e34ff2b85f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-responding-toosecurity-alerts-in-operations-management-suite-security-and-audit-solution"></a>İzleme ve yanıt toosecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü
Bu belge hello tehdit Intelligence seçeneği OMS güvenlik ve denetim toomonitor kullanılabilir kullanın ve toosecurity uyarıları yanıt yardımcı olur.

## <a name="what-is-oms"></a>OMS nedir?
Microsoft Operations Management Suite (OMS) Microsoft'un bulut yönetmek ve şirket içi korumak ve altyapı bulut yardımcı olan BT yönetim çözümü dayalıdır. OMS hakkında daha fazla bilgi için hello makaleyi okuyun [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="threat-intelligence"></a>Tehdit bilgileri
Kullanıcıların geniş kapsamlı erişime toohello ağına sahip ve çok çeşitli aygıtları tooconnect toocorporate verileri kullanan bir kuruluş ortamında, etkin olarak kaynaklarınızı izlemek ve toosecurity olayları hızla yanıt zorunludur. Belirli tehditlere değil yükseltmek bazı siber güvenlik uyarıları çünkü hello güvenlik yaşam döngüsü açısından önemli ya da teknik geleneksel güvenlik denetimleri tarafından tanımlanan kuşkulu etkinlikleri budur. 

Hello kullanarak **tehdit bilgileri** seçeneği kullanılabilir OMS güvenlik ve denetim, BT yöneticileri güvenlik tehditlerine karşı hello ortamında, örneğin tanımlamak, belirli bir bilgisayarın parçası olup olmadığını belirleyebilmek bir [ botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection). Saldırganlar bu bilgisayar toohello komut ve denetim gizlice bağlandığında kötü amaçlı yazılım yapacağıyla yüklediğinizde bilgisayarlar çoğunlukla düğümler olabilir. Yeraltı iletişim kanalları, gelen gibi olası tehditler tanımlayabilirsiniz [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents). 

Sipariş toobuild Microsoft içinde birden fazla kaynaktan gelen veri OMS güvenlik ve denetim bu tehdit bilgileri kullanın. OMS güvenlik ve denetim verileri bu tooidentify olası tehditlere karşı ortamınızın özelliğinden yararlanır.

Merhaba tehdit bilgileri bölmesinde üç ana seçenekleri ile oluşur:

* Giden kötü amaçlı trafiğe sahip sunucular
* Algılanan tehditler türleri
* Tehdit bilgileri haritası

> [!NOTE]
> Tüm bu seçenekler genel bakış için okuma [Operations Management Suite güvenlik ve denetim çözümü ile çalışmaya başlama](oms-security-getting-started.md).
> 
> 

### <a name="responding-toosecurity-alerts"></a>Yanıt veren toosecurity uyarıları
Merhaba adımlardan biri bir [güvenlik olay yanıtlama](https://technet.microsoft.com/library/cc512623.aspx) tooidentify hello önem derecesi hello güvenliğinin aşılmasına sistemleri bir işlemdir. Bu aşamada hello aşağıdaki görevleri gerçekleştirmeniz gerekir:

* Merhaba saldırı Hello yapısını belirleme
* Merhaba saldırı başlangıç noktasını belirler
* Merhaba saldırı Hello amacı belirler. Özellikle kuruluş tooacquire belirli bilgilerinizi yönlendirilmiş hello saldırı, veya rastgele bekliyordu?
* Aşılmış hello sistemleri belirle
* Erişilen ve bu dosyaların hello duyarlılık belirlemek hello dosyaları belirlemek

Yararlanabileceğiniz **tehdit bilgileri** bu görevleri ile OMS güvenlik ve denetim çözüm toohelp bilgileri. Merhaba tooaccess aşağıda bu adımları **tehdit bilgileri** seçenekleri:

1. Merhaba, **Microsoft Operations Management Suite** ana Pano tıklatın **güvenlik ve Denetim** döşeme.
   
    ![Güvenlik ve Denetim](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. Merhaba, **güvenlik ve Denetim** panoyu hello görürsünüz **tehdit bilgileri** aşağıda gösterildiği gibi hello sağ seçenekleri:
   
    ![Tehdit Intel](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

Bu üç kutucuklar hello geçerli tehditleri genel bir bakış sunar. Merhaba, **giden kötü amaçlı trafiği sunucusuyla** (içinde veya ağınızın dışında) izlemekte olduğunuz herhangi bir bilgisayarda ise mümkün tooidentify olur yani gönderen kötü amaçlı trafiği toohello Internet. 

Merhaba **algılanan tehdit türlerini** döşeme "hello joker" geçerli hello tehditleri özetini gösterir, bu kutucuğa tıkladığınızda bu tehditler hakkında daha fazla ayrıntı Göster aşağıdaki görürsünüz:

![Algılanan tehdit türleri](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

Tıklayarak her tehdit hakkında daha fazla bilgi ayıklayabilirsiniz. Aşağıdaki örnek Hello Botnet hakkında daha fazla ayrıntı gösterir:

![bir tehdit hakkında daha fazla ayrıntı](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

Merhaba'den itibaren bu bölümde açıklandığı gibi bu bilgileri bir olay yanıtlama çalışması sırasında çok kullanışlı olabilir. Bu aynı zamanda bir adli araştırma sırasında toofind hello kaynak hangi sistem aşılmış ve zaman çizelgesi hello hello saldırı, ihtiyaç duyacağınız önemli olabilir. Bu raporda, kolayca belirleyebilir hello saldırı hakkında bazı önemli ayrıntıları gibi: Merhaba kaynak hello saldırı, aşılmış yerel IP hello ve hello hello bağlantı geçerli oturum durumu. 

Merhaba **tehdit Intelligence harita** kötü amaçlı trafiği olan tooidentify hello geçerli konumlarına Merhaba Dünya çevresinde yardımcı olur. Turuncu (gelen) ve bu okları birini tıklatırsanız, hello trafiği yönünü tanımlayan kırmızı (giden) oklar bu haritadaki, aşağıda gösterildiği gibi tehdit ve hello trafiği yönünü hello türünü gösterir:

![Tehdit bilgisi haritası](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> Toouse bu özellik bir olay yanıtlama sırasında işleminin nasıl hello sunu izleyerek Tanıtımı görebilirsiniz [Operations Management Suite kullanarak destekli araştırma ile Veri Merkezi güvenlik tehditleri azaltmak](https://myignite.microsoft.com/videos/5000) Microsoft Ignite teslim.
> 

### <a name="responding-toodistinct-malicious-ip-accessed"></a>Erişilen kötü amaçlı IP toodistinct yanıt
Bazı senaryolarda, izlenen bir bilgisayardan erişilen olası bir kötü amaçlı IP ile karşılaşabilirsiniz:

![Tehdit bilgisi haritası](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Bu uyarı ve diğerleri içinde Merhaba aynı kategoride, OMS güvenlik yararlanarak oluşturulan [Microsoft tehdit bilgileri](https://youtu.be/O4WtxgUrDc8). Merhaba tehdit bilgileri veri Microsoft tarafından toplanan yanı sıra başında tehdit Intelligence sağlayıcılardan satın. Bu veriler, sık sık güncelleştirilir ve toofast taşıma tehditleri uyarlanan. Tooits yapısı, bu güvenlik bilgileri sırasında diğer kaynakları ile birleştirilmelidir [araştırma](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) bir güvenlik uyarısı. 

## <a name="customize-alerts-received-via-e-mail"></a>E-posta yoluyla alınan uyarıları özelleştirme

Güvenlik Uyarıları OMS güvenliği tarafından tetiklendiğinde, kuruluşunuzda hangi kullanıcıların bildirilecek özelleştirebilirsiniz. Bu seçenek altında genel bakış kullanılabilir / ayarları OMS Pano hello:

![E-posta](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, nasıl öğrenilen toouse hello **tehdit bilgileri** OMS güvenlik ve denetim çözüm toorespond toosecurity uyarıları seçeneği. toolearn OMS güvenlik hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:

* [Operations Management Suite'e (OMS) genel bakış](operations-management-suite-overview.md)
* [Operations Management Suite güvenlik ve denetim çözümü ile çalışmaya başlama](oms-security-getting-started.md)
* [Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme](oms-security-monitoring-resources.md)

