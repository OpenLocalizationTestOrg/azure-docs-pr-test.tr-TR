---
title: "Operations Management Suite güvenlik ve denetim çözümü kaynaklarında aaaMonitoring | Microsoft Docs"
description: "Bu belge, OMS güvenlik toouse ve denetim özellikleri toomonitor kaynaklarınızı yardımcı olur ve güvenlik sorunlarını tanımlamak."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 932b946ae1ffa3b979c02f419702d42d46abf7ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a>Operations Management Suite güvenlik ve denetim çözümü kaynaklarında izleme
Bu belge OMS güvenlik ve denetim özellikleri toomonitor kaynaklarınızı kullanın ve güvenlik sorunları belirlemenize yardımcı olur.

## <a name="what-is-oms"></a>OMS nedir?
Microsoft Operations Management Suite (OMS) Microsoft'un bulut yönetmek ve şirket içi korumak ve altyapı bulut yardımcı olan BT yönetim çözümü dayalıdır. OMS hakkında daha fazla bilgi için hello makaleyi okuyun [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="monitoring-resources"></a>İzleme kaynakları
Her hello ilk yerinde oluşmasını kaynaklı tooprevent güvenlik olayların istediğiniz, mümkündür. Ancak, mümkün olmayan tooprevent olan tüm güvenlik olayları. Bir güvenlik olayı gerçekleştiğinde, bu etkisini en aza indirilir tooensure gerekir.  Kullanılan toominimize olabilir üç önemli öneriler sayı hello ve hello güvenlik olaylarına etkisi vardır:

* Güvenlik açıkları, ortamınızda düzenli olarak değerlendirin.
* Tüm bilgisayar sistemleri ve yüklü hello en son düzeltme eklerinin tümüne sahip ağ aygıtları tooensure düzenli olarak denetleyin.
* Tüm günlükleri ve işletim sistemi olay günlüklerini, uygulama belirli günlüklerini ve izinsiz giriş algılama sistem günlükleri gibi günlük mekanizmaları düzenli olarak denetleyin.

BT tooactively izlemenize yardımcı olabilecek tüm kaynakları OMS güvenlik ve denetim çözümü sağlar, güvenlik olaylarına hello etkisini en aza. OMS güvenlik ve denetim kaynakları izlemek için kullanılan güvenlik etki alanları bulunur. Merhaba güvenlik etki alanları tooa seçenekleri hızlı erişim sağlar, güvenlik izleme hello için şu etki alanlarına daha ayrıntılı olarak ele alınacaktır:

* kötü amaçlı yazılım değerlendirmesi
* Güncelleştirme değerlendirmesi
* Kimlik ve Erişim

> [!NOTE]
> Tüm bu seçenekler genel bakış için okuma [Operations Management Suite güvenlik ve denetim çözümü ile çalışmaya başlama](oms-security-getting-started.md).
> 
> 

### <a name="monitoring-system-protection"></a>Sistem Koruması izleme
İçinde savunma derinliği yaklaşımda koruma her katman için hello önemlidir, varlık genel güvenlik durumu. Tehditler ve yetersiz korumalı bilgisayarlar hello kötü amaçlı yazılım değerlendirmesi döşeme güvenlik etki alanları altında gösterilen bilgisayarlarla algıladı. Kötü amaçlı yazılım değerlendirmesi hello üzerinde Hello bilgileri kullanarak, gerek bir plan tooapply koruma toohello sunucuları tanımlayabilirsiniz. Aşağıda bu seçeneği izleyin hello adımları tooaccess:

1. Merhaba, **Microsoft Operations Management Suite** ana Pano tıklatın **güvenlik ve Denetim** döşeme.
   
    ![Güvenlik ve Denetim](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. Merhaba, **güvenlik ve Denetim** panoyu tıklatın **kötü amaçlı yazılımdan koruma değerlendirme** altında **güvenlik etki alanları**. Merhaba **kötü amaçlı yazılımdan koruma değerlendirme** Pano, aşağıda gösterildiği gibi görünür:

![kötü amaçlı yazılım değerlendirmesi](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

Merhaba kullanabilirsiniz **kötü amaçlı yazılım değerlendirmesi** güvenlik sorunları aşağıdaki Pano tooidentify hello:

* **Etkin tehditleri**: güvenliği ve etkin tehditleri hello sistemi sahip bilgisayarlar.
* **Düzeltilen tehditleri**: hello tehditler güvenliği bilgisayarlar düzeltilebilir.
* **İmza güncel**: kötü amaçlı yazılımdan koruma hello imza etkinleştirilmiş bilgisayarları güncel değil.
* **Gerçek zamanlı koruma yok**: kötü amaçlı yazılımdan koruma yüklü olmayan bilgisayarlar.

### <a name="monitoring-updates"></a>güncelleştirmeleri izleme
Merhaba en son güvenlik güncelleştirmelerini uygulamak bir güvenlik en iyi uygulamadır ve güncelleştirme yönetimi stratejinizde birleştirilmesi. Microsoft İzleme Aracısı hizmeti (HealthService.exe) izlenen bilgisayarlardan güncelleştirme bilgilerini okur ve işleme hello bulutta bu güncelleştirilmiş bilgileri toohello OMS hizmetine gönderir. Merhaba Microsoft İzleme Aracısı hizmeti otomatik bir hizmet olarak yapılandırılır ve bu her zaman hello hedef bilgisayarda çalışıyor olması gerekir.

![güncelleştirmeleri izleme](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

Mantığı uygulanan toohello güncelleştirme veri ve hello bulut hizmeti hello verilerini kaydeder. Eksik güncelleştirmeleri bulunursa, bunlar üzerinde hello gösterilir **güncelleştirmeleri** Pano. Merhaba kullanabilirsiniz **güncelleştirmeleri** eksik olan Pano toowork güncelleştirir ve planı tooapply geliştirmek bunları ihtiyaç toohello sunucuları. Tooaccess hello Hello adımları izleyin **güncelleştirmeleri** Pano:

1. Merhaba, **Microsoft Operations Management Suite** ana Pano tıklatın **güvenlik ve Denetim** döşeme.
2. Merhaba, **güvenlik ve Denetim** panoyu tıklatın **güncelleştirme değerlendirme** altında **güvenlik etki alanları**. Merhaba güncelleştirme Pano, aşağıda gösterildiği gibi görünür:

![Güncelleştirme değerlendirme](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

Bu Panoda bir güncelleştirme değerlendirme toounderstand hello geçerli durumu bilgisayarların ve adresi hello en kritik tehditleri gerçekleştirebilirsiniz. Hello kullanarak **kritik güncelleştirmeler veya güvenlik güncelleştirmeleri** kutucuğu, BT yöneticilerinin olacaktır mümkün tooaccess hakkında ayrıntılı bilgi aşağıda gösterildiği gibi eksik hello güncelleştirmeleri:

![arama sonucu](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

Bu rapora dahil olabilir önemli bilgiler kullanılan hello güvenlik güncelleştirmesi ve hello hello hakkında daha fazla ayrıntı sahip MS Bulletin ilişkili hello Microsoft KB makalelerini içeren bu sistemde saldırılara karşı tehdit tooidentify hello türü güvenlik açığı.

### <a name="monitoring-identity-and-access"></a>Kimlik ve erişim izleme
Farklı cihaz kullanarak ve Bulut ve şirket içi uygulamalar çok büyük miktarda erişme yerden çalışmaları kullanıcılarla kimlik bilgilerini korunduğunu zorunludur. Kimlik bilgisi hırsızlığı saldırıları, saldırganın başlangıçta erişim tooa normal kullanıcının kimlik bilgilerini tooaccess hello ağ içindeki bir sistem kazanır izinlerdir. Çoğu zaman, bu ilk saldırının yalnızca bir şekilde tooget erişim toohello ağ, hello nihai amacıyla toodiscover ayrıcalıklı hesaplar. 

Saldırganlar, diğer oturum açan hesaplar hello oturumları tooextract kimlik bilgilerini tooling ücretsiz kullanarak hello ağında kalır. Merhaba sistem yapılandırmasına bağlı olarak, bu kimlik bilgileri karmaları, raporları veya bile düz metin parola hello formunda ayıklanabilir.  

> [!NOTE]
> doğrudan makinelerde kullanıma sunulan toohello Internet birçok başarısız denemeleri tüm tür iyi bilinen kullanıcı adları (örneğin, yönetici) kullanarak bu try toologin görürsünüz. Çoğu durumda bu hello iyi bilinen kullanıcı adları kullanılmıyorsa ve hello parola yeterince güçlü ise Tamam olur.
> 
> 

Bu ayrıcalıklı bir hesap tehlikeye önce olası tooidentify saldırganlar vardır. Yararlanabileceğiniz **OMS güvenlik ve denetim çözümü** toomonitor kimlik ve erişim. Tooaccess hello Hello adımları izleyin **kimlik ve erişim** Pano:

1. Merhaba, **Microsoft Operations Management Suite** ana Pano tıklatın güvenlik ve denetim döşeme.
2. Merhaba, **güvenlik ve Denetim** panoyu tıklatın **kimlik ve erişim** altında **güvenlik etki alanları**. Merhaba **kimlik ve erişim** Pano, aşağıda gösterildiği gibi görünür:

![kimlik ve erişim](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

Normal izleme stratejinizin bir parçası olarak, kimlik izleme eklemeniz gerekir. BT yöneticisi, birçok denemeleri olan belirli geçerli bir kullanıcı adı ise görünmelidir. Bu edinilen hello gerçek kullanıcı adı ya da bir saldırganı işaret ve toobrute zorla veya süresi dolmuş sabit kodlanmış parola kullanan bir otomatik araç deneyin.

Bu Pano etkinleştir BT tooquickly olası tehditler ilgili tooidentity ve erişim toocompany ait kaynakları belirleyin. Belirli önemli tooalso olası eğilimleri belirlemek, örneğin hello zaman içinde oturum açmalar parçasında, süre başarısız oturum açma girişimi gerçekleştirilir kaç kez görebilirsiniz. Bu durumda, bilgisayar hello **DosyaSunucusu** 35 oturum açma girişimlerinin aldı. Bu bilgisayar hakkında daha fazla ayrıntı tıklayarak keşfedebilirsiniz. 

![Daha fazla ayrıntı](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

Bu bilgisayar için oluşturulan hello rapor bu deseni değerli ayrıntılarını getirir. Bu hello fark **hesap** kullanılan tootry tooaccess olan kullanıcı hesabı hello sütun verir hello sistemi hello **TIMEGENERATED** zaman aralığı içinde hangi hello girişim yapıldı hello sütun verir ve Merhaba **LOGONTYPENAME** burada bu girişim yapıldı konumu hello sütun sağlar. Bu deneme, yerel olarak hello sistemde bir program tarafından gerçekleştirilen, hello **işlem** sütun hello işlemin adını gösteren. Bir programdan hello oturum açma denemesi geldiği yere senaryolarda hello işlem adı zaten var ve artık size daha fazla araştırma hello hedef sistemde gerçekleştirebilirsiniz.

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, nasıl öğrenilen toouse OMS güvenlik ve denetim çözüm toomonitor kaynaklarınızı. toolearn OMS güvenlik hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:

* [Operations Management Suite'e (OMS) genel bakış](operations-management-suite-overview.md)
* [Operations Management Suite güvenlik ve denetim çözümü ile çalışmaya başlama](oms-security-getting-started.md)
* [İzleme ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü](oms-security-responding-alerts.md)

