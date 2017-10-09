---
title: "Azure akış analizi için aaaTroubleshooting Kılavuzu | Microsoft Docs"
description: "Nasıl tootroubleshoot Stream Analytics işi"
keywords: "sorun giderme kılavuzu"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a>Azure akış analizi için sorun giderme kılavuzu

Azure Stream Analytics sorun giderme toobe karmaşık çaba ilk bakışta görülebilir. Birden çok kullanıcıya sahip çalışma sonra bu kılavuzu toohelp daha verimli hale hello işlem oluşturdunuz ve hello konusunda güvenilir girişleri, çıktıları, sorgular ve işlevleri hakkında bilgiler kaldırın.

## <a name="troubleshoot-your-stream-analytics-job"></a>Akış analizi işi sorunlarını giderme

Sorun giderme, Stream Analytics işi, en iyi sonuçlar için yönergeleri izleyerek hello kullan:

1.  Bağlantınızı test edin:
    - Bağlantı tooinputs çıkışları hello kullanarak doğrulayıp **Bağlantıyı Sına** her giriş ve çıkış düğmesi.

2.  Giriş verilerinizi inceleyin:
    - Giriş tooverify olay Hub'ına akan, kullanın [hizmet veri yolu Gezgini](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure olay hub'ı (olay hub'ı giriş kullanılıyorsa).  
    - Kullanım hello [ **örnek verileri** ](stream-analytics-sample-data-input.md) düğmesini her giriş için ve hello giriş örnek veri indirin.
    - Merhaba örnek veri toounderstand hello şekli hello veri inceleyin: Merhaba şema ve hello [veri türleri](https://msdn.microsoft.com/library/azure/dn835065.aspx).

3.  Sorgunuzu test edin:
    - Merhaba üzerinde **sorgu** sekmesinde, hello kullan **Test** düğmesini tootest hello sorgu ve indirilen hello örnek verileri çok kullanın[test hello sorgusu](stream-analytics-test-query.md). Hataları incelemek ve toocorrect denemek bunları.
    - Kullanırsanız [ **TIMESTAMP By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), hello olayları zaman damgaları hello büyük olduğunu doğrulayın [iş başlangıç zamanı](stream-analytics-out-of-order-and-late-events.md).

4.  Sorgunuz hata ayıklama:
    - Merhaba sorgudan aşamalı olarak basit select deyimi toomore karmaşık toplamalar adımları kullanarak yeniden oluşturun. Merhaba sorgu mantığı adım adım yukarı toobuild kullanmak [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) yan tümceleri.
    - Kullanım [SELECT INTO](stream-analytics-select-into.md) toodebug sorgu adımları.

5.  Ortak Tuzaklar gibi kaldırın:
    - A [ **nerede** ](https://msdn.microsoft.com/library/azure/dn835048.aspx) hello sorgusunda yan tümcesi, herhangi bir çıktı oluşturulmasını önler önleme, tüm olayları filtrelenmelidir.
    - Pencere işlevleri kullandığınızda, hello sorgudan bir çıktı hello tüm pencere süresi toosee için bekleyin.
    - olaylar için başlangıç zaman damgası hello iş başlangıç zamanı önündeki ve bu nedenle, olayları bırakılma.

6.  Olay sıralama kullanın:
    - Tüm ince çalışılan önceki adımları Merhaba, toohello gidin **ayarları** dikey penceresinde ve select [ **olay sıralama**](stream-analytics-out-of-order-and-late-events.md). Bu ilke ne senaryonuzda mantıklı yapılandırıldığından emin olun. Hello İlkesi *değil* hello kullandığınızda uygulanan **Test** düğmesini tootest hello sorgu. Üretim hello işi karşı tarayıcı içi test arasındaki tek fark sonucudur.

7.  Ölçümleri kullanarak hata ayıklama:
    - Merhaba (Merhaba sorguya dayalı) süresi beklenen sonra hiçbir çıktı edindiyseniz, hello aşağıdakileri deneyin:
        - Bakmak [ **izleme ölçümleri** ](stream-analytics-monitoring.md) hello üzerinde **İzleyici** sekmesi. Merhaba değerleri toplanır çünkü hello ölçümleri birkaç dakika gecikir.
            - Varsa giriş olaylarını > 0 hello iş ise mümkün tooread giriş verileri. Giriş olayları > 0 ise, ardından değilse:
                - toosee hello veri kaynağı geçerli veriler olup olmadığını denetleyin, kullanarak [hizmet veri yolu Gezgini](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a). Merhaba iş giriş olarak olay hub'ı kullanıyorsa, bu denetimi uygular.
                - Merhaba veri seri hale getirme biçimi ve veri kodlama beklendiği gibi olup toosee denetleyin.
                - Merhaba iş bir olay hub'ı kullanıyorsanız, toosee hello hello ileti gövdesi olup olmadığını denetleyin *Null*.
            - Veri dönüştürme hataları > 0 ve climbing, hello aşağıdaki olabilir doğru:
                - Merhaba iş mümkün toode olabilir-hello olayları seri.
                - Merhaba olay şema tanımlanan hello eşleşmeyebilir veya hello sorgusunda hello olayların beklenen şema.
                - Bazı hello olay hello alanların Hello veri türleri beklentilerini eşleşmeyebilir.
            - Çalışma zamanı hataları > 0 ise, bu anlamına gelir, hello iş hello veri alabilir ancak hello sorgu işlenirken hatalar üretme.
                - toofind hello hataları, Git toohello [denetim günlüklerini](../azure-resource-manager/resource-group-audit.md) ve filtre *başarısız* durumu.
            - Varsa InputEvents > 0 ve OutputEvents = 0, hello aşağıdakilerden birini doğru olduğu anlamına gelir:
                - Sorgu işleme sıfır çıkış olayıyla sonuçlandı.
                - Olayları veya kendi alanlar sorgu işlendikten sonra sıfır çıkış kaynaklanan hatalı olabilir.
                - Merhaba işi oluşturulamıyor toopush veri toohello oluştu [çıkış havuzunun](stream-analytics-select-into.md) bağlantı veya kimlik doğrulaması nedeniyle.
        - Tüm hello hata durumlarında, günlük iletilerini açıklayan ek ayrıntıları (olanlar dahil), işlemleri daha önce bahsedilen dışındaki hello sorgu mantığı tüm olayları da burada filtre uygulanmış durumda. Birden çok olay Hello işlenmesini hatalar oluşturursa, Stream Analytics aynı 10 dakika tooOperations içinde yazın hello ilk üç hata iletileri günlükleri hello günlüğe kaydeder. Ardından "Hataları çok hızlı bir şekilde bu gizlenen gerçekleştiği." iletisini ek aynı hatalarla gizler

8. Denetim ve tanılama günlüklerini kullanarak hata ayıklama:
    - Kullanım [denetim günlüklerini](../azure-resource-manager/resource-group-audit.md)ve filtre tooidentify ve hata ayıklama hataları.
    - Kullanım [iş tanılama günlüklerini](stream-analytics-job-diagnostic-logs.md) tooidentify ve hata ayıklama hataları.

9. Merhaba çıkışları inceleyin:
    - Merhaba iş durumu olduğunda *çalıştıran*hello çıktı hello havuz veri kaynağındaki görebilirsiniz hello sorguda belirlenen hello süre bağlı olarak.
    - Tooa belirli çıktı türü giderek çıkışları göremiyorsanız, bunları bir Azure Blob gibi daha az karmaşık tooan çıktı türü yönlendirin. Merhaba çıkış görünüp görünmeyeceğini Depolama Gezgini'ni kullanarak toosee denetleyin. Ayrıca, alınmasını azaltma sınırları hello çıkış adresindeki veri engelliyor olup olmadığını doğrulayın.

10. Veri akış analizi işi diyagramı Ölçümleriyle kullanın:
    - tooanalyze veri akış ve sorunları, kullanım hello belirlemek [ölçümleri ile iş diyagramı](stream-analytics-job-diagram-with-metrics.md).

11. Bir destek servis talebi açın:
    - Son olarak, tüm yöntemler başarısız olursa, Microsoft destek servis talebi hello işinizi içeren Subscriptionıd kullanarak açın.

## <a name="get-help"></a>Yardım alın

Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Sonraki adımlar

* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
