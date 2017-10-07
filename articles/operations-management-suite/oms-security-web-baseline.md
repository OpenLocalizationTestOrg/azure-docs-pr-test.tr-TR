---
title: "Yönetim Paketi güvenlik ve denetim çözüm Web temel aaaOperations | Microsoft Docs"
description: "Bu belge açıklar nasıl toouse OMS güvenlik ve denetim çözüm tooperform web temeli değerlendirme uyumluluk ve güvenlik amaçla tüm izlenen web sunucuları."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Operations Management Suite Güvenlik ve Denetim Çözümünde Web Temeli Değerlendirmesi
Bu belge toouse yardımcı olur [Operations Management Suite (OMS) güvenlik ve denetim çözümü](operations-management-suite-overview.md) web özellikleri tooaccess hello izlenen kaynaklarınızın güvenli durumunu temel değerlendirmesi.

## <a name="what-is-web-baseline-assessment"></a>Web Temeli Değerlendirmesi nedir?
OMS Güvenliği şu anda işletim sistemleri için güvenlik temeli değerlendirmesi sağlamaktadır. Hello işletim sistemi ayarlarını, sunucularınızın her 24 saatte tarar ve savunmasız olabilecek ayarları içine bir görünümünü sağlar. Bu seçenek hakkında daha fazla bilgi için [Operations Management Suite Güvenlik ve Denetim Çözümünde Temel Değerlendirmesi](oms-security-baseline.md) makalesini okuyun.

Merhaba hello web temeli değerlendirme toofind savunmasız olabilecek web sunucusu ayarları hedefidir. Merhaba web temel yapılandırmalar için üç birincil kaynağı hello: .NET, ASP.NET ve IIS yapılandırması.  Yalnızca işletim sistemi temel değerlendirme hello gibi OMS güvenlik tooscan geçiyor, her 24hrs web sunucuları ve bunları güvenlik durumunu görünüme sağlayın.  Internet Information Service (IIS), çeşitli site ve uygulama düzeyleri toobe ilgili geçersiz kılınmış sağlayan, yapılandırmaları büyük ölçüde özelleştirilebilir. Merhaba tarayıcı toplama toohello varsayılan kök düzeyinde her uygulama/site düzeyinde hello ayarlarını denetler. Bu tooidentify olası güvenlik açığı ayarları konumları yardımcı olur ve hızlı bir şekilde düzeltin.


## <a name="web-security-baseline-assessment"></a>Web Güvenlik Temeli Değerlendirmesi
Bu önizleme için bu özelliği hello OMS arama seçeneği kullanılarak erişilir toobe geçiyor. Tooperform tahsis hello sorgu Hello adımları izleyin:

1. Merhaba, **Microsoft Operations Management Suite** ana Pano tıklatın **güvenlik ve Denetim** döşeme.
2. Merhaba, **güvenlik ve Denetim** panoyu tıklatın **günlük arama** düğmesi.
3. kullanabileceğiniz hello ilk sorgudur hello **Web temeli değerlendirme özeti**. Merhaba, **burada başlangıç arama** alanına, bu sorgu yazın: türü*SecurityBaselineSummary BaselineType = web =*. Merhaba ekranında aşağıdaki çıktı örneği vardır:

![Web temeli değerlendirme özeti](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> Bu sorguda her kayıt, tek bir sunucu üzerindeki değerlendirme özetini gösterir.

Hello olduğunuzda **günlük arama**, farklı sorgular tooobtain hello web temeli değerlendirme hakkında daha fazla bilgi yazabilirsiniz. Ayrıca toohello önceki sorgu olanları bu Önizleme'de aşağıdaki hello de kullanabilirsiniz.

**Web Temeli Kural Değerlendirmesi**: Her kayıt, tek bir sunucudaki tek bir web temeli kural değerlendirmesini temsil eder. Merhaba kuralı, konumu, beklenen hello sonuç ve hello gerçek sonucu için tüm verileri içerir.

**Sorgu**: Type*=SecurityBaseline BaselineType=web*

![Web temeli kural değerlendirmesi](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

**Belirli bir sunucu için tüm sonuçları göster**: Bu sorgu nasıl toosee sonuçlarını gösterir belirli bir sunucunun.

**Sorgu**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*

![Tüm sonuçlar](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

Bu kayıtları/sorguları toocreate kendi panolar, raporlar ve uyarılar de kullanabilirsiniz. Merhaba ekranında aşağıdaki tooyour Pano ekleyebileceğiniz örnek UI denetimi vardır. Bilgi edinebilirsiniz nasıl toovisualize OMS Görünüm Tasarımcısı kullanarak verilerinizi [burada](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). Merhaba ekranında aşağıdaki bu özelleştirme yaptıktan sonra hello döşemenin nasıl örneği nasıl görüneceği gösterilmektedir.

![Örnek Kullanıcı Arabirimi](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> Merhaba temel değerlendirmesi için işaretlenmiş olan tooknow hello ayarlar isterseniz indirebilirsiniz [bu Excel elektronik tablosu](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) bu ayarları içerir.

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede OMS Güvenlik ve Denetim web temeli değerlendirmesi hakkında bilgi edindiniz. toolearn OMS güvenlik hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:

* [Operations Management Suite'e (OMS) genel bakış](operations-management-suite-overview.md)
* [İzleme ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü](oms-security-responding-alerts.md)
* [Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme](oms-security-monitoring-resources.md)

