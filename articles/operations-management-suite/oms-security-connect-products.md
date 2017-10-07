---
title: "aaaConnecting güvenlik ürünleri toohello Operations Management Suite (OMS) güvenlik ve denetim çözümü | Microsoft Docs"
description: "Bu belge, tooconnect Yönetim Paketi güvenlik ve denetim ortak olay biçimini kullanarak çözüm güvenlik ürünleri tooOperations yardımcı olur."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a>Güvenlik ürünleri toohello Operations Management Suite (OMS) güvenlik ve denetim çözümü bağlanma 
Bu belgede güvenlik ürünlerinizi hello OMS güvenlik ve denetim çözümü bağlanmanıza yardımcı olur. Aşağıdaki kaynaklar hello desteklenir:

- Common Event Format (CEF) olayları
- Cisco ASA olayları


## <a name="what-is-cef"></a>CEF nedir?
Ortak olay biçimi (CEF) endüstri standardı bir biçime Syslog iletileri, çok sayıda güvenlik satıcılar tooallow olay birlikte çalışabilirliğini farklı platformlar tarafından kullanılan en üstünde ' dir. OMS güvenlik ve denetim çözüm veri alımı tooconnect etkinleştirir olduğunda CEF güvenlik ürünlerinizi OMS güvenliği ile kullanma desteği. 

Veri kaynağı tooOMS bağlanarak bu platform parçası olan özellikler aşağıdaki hello mümkün tootake avantajı şunlardır:

- Arama ve Bağıntı
- Denetim
- Uyarı
- Tehdit Bilgisi
- Önemli sorunlar

## <a name="collection-of-security-solution-logs"></a>Güvenlik çözümü günlüklerinin toplanması

OMS Security, CEF kullanarak Syslog’lar ve [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) günlükleri üzerinden günlüklerin toplanmasını destekler. Bu örnekte, hello (Merhaba günlükleri oluşturur bilgisayar) ng syslog arka plan programı çalıştıran bir Linux bilgisayar kaynaktır ve OMS güvenlik hello hedefidir. Aşağıdaki tooperform hello gerekir tooprepare hello Linux bilgisayarı görevler:

- Merhaba OMS aracısı veya üzeri Linux, sürüm 1.2.0-25 için indirin.
- Merhaba bölümü izleyin **Hızlı Yükleme Kılavuzu** gelen [bu makalede](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall ve yerleşik hello Aracısı tooyour çalışma.

Genellikle, hello Aracısı hangi hello günlükleri birinde üretilen hello bilgisayardan farklı bir bilgisayara yüklenir. İletme hello günlükleri toohello aracı makine genellikle aşağıdaki adımları hello gerektirir:

- Ürün/makine tooforward hello gerekli olayları toohello syslog arka plan programı (rsyslog veya syslog ng) günlüğü hello hello aracı makinede yapılandırın.
- Uzaktaki sistemden Merhaba aracı makine tooreceive iletileri Hello syslog arka plan etkinleştirin.

Merhaba aracı makinede hello olayları hello syslog arka plan programı toolocal UDP bağlantı noktasından 25226 gönderilen toobe gerekir. Merhaba Aracısı, bu bağlantı noktasına gelen olaylar için dinliyor. Merhaba, (yerel ayarlarınızı hello yapılandırma toofit değiştirebilirsiniz) hello yerel sistem toohello Aracısı'ndan tüm olayları göndermek için örnek bir yapılandırma aşağıdadır:

1. Açık hello terminal penceresi ve Git toohello directory */etc/syslog-ng /* 
2. Yeni bir dosya oluşturun *güvenlik config omsagent.conf* ve içeriği aşağıdaki hello ekleyin: OMS_facility local4 =
    
    filter f_local4_oms { facility(local4); };

    destination security_oms { tcp("127.0.0.1" port(25226)); };

    log { source(src); filter(f_local4_oms); destination(security_oms); };
    
3. Merhaba dosya indirme *security_events.conf* ve yerleştirin */etc/opt/microsoft/omsagent/conf/omsagent.d/* hello OMS Aracısı bilgisayar.
4. Merhaba toorestart hello syslog arka plan programı aşağıdaki komutu yazın: *syslog ng çalıştırmak için:*
    
    ```
    sudo service rsyslog restart
    ```

    *For rsyslog run:*
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. Toorestart hello OMS aracısı aşağıdaki Hello komutunu yazın:

    *For syslog-ng run:*
    
    ```
    sudo service omsagent restart
    ```

    *For rsyslog run:*
    
    ```
    systemctl restart omsagent
    ```
6. Merhaba aşağıdaki komutu yazın ve hello OMS Aracısı günlüğünde hatalar yoktur hello sonuç tooconfirm gözden geçirin:

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a>Toplanan güvenlik olaylarını gözden geçirme

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

Merhaba yapılandırma bittikten sonra hello güvenlik olayı OMS güvenliği tarafından alınan toobe başlar. toovisualize bu olayları, açık hello günlük arama hello komutunu yazın *türü CommonSecurityLog =* hello arama alanı ve ENTER tuşuna basın. Merhaba aşağıdaki örnek hello sonucunu bu komut gösterir, bu durumda OMS güvenlik zaten güvenlik günlüklerini birden çok satıcılardan alınan olduğunu dikkat edin:
   
![OMS Güvenlik ve Denetim Temeli Değerlendirmesi](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

Tek tek bir satıcı için örneğin, çevrimiçi Cisco günlüklerini toovisualize, türü bu arama iyileştirebilirsiniz: *türü CommonSecurityLog DeviceVendor = Cisco =*. Merhaba "CommonSecurityLog", "Özel uzantısının" olsun veya olmasın, başka bir uzantı sırasında hello temel extensios de dahil olmak üzere herhangi bir olduğunda CEF başlığını eklenecek için "Ekuzantılar" alanına alanları önceden tanımlanmış. Merhaba özel alanlar özellik ayrılmış tooget alanlardan bunu kullanabilirsiniz. 

### <a name="accessing-computers-missing-baseline-assessment"></a>Temel değerlendirmesi eksik bilgisayarlara erişim
OMS hello etki alanı üyesi temel profil tooWindows Server 2012 R2'in Windows Server 2008 R2'de destekler. Windows Server 2016 temeli, henüz tamamlanmamıştır ve yayımlandıktan hemen sonra eklenecektir. OMS güvenlik ve denetim temel değerlendirmesi taranan tüm diğer işletim sistemlerinin hello altında görünür **temeli değerlendirme eksik olan bilgisayarlar** bölümü.

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, nasıl öğrenilen tooconnect olduğunda CEF çözüm tooOMS. toolearn OMS güvenlik hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:

* [Operations Management Suite'e (OMS) genel bakış](operations-management-suite-overview.md)
* [İzleme ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü](oms-security-responding-alerts.md)
* [Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme](oms-security-monitoring-resources.md)

