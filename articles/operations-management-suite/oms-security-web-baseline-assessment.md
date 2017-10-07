---
title: "Operations Management Suite güvenlik ve denetim çözüm temel temeli değerlendirme aaaWeb | Microsoft Docs"
description: "Bu belgede nasıl toouse web OMS güvenlik ve denetim çözüm tooperform tüm izlenen web sunucuları uyumluluk ve güvenlik amaç için bir taban çizgisi değerlendirmesi temel değerlendirmesi açıklanmaktadır."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: dafa9d3d93fae31748306b60ee40b285dd59c802
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Operations Management Suite Güvenlik ve Denetim Çözümünde Web Temeli Değerlendirmesi
Bu belge, OMS güvenlik kullanmanıza yardımcı olur ve izlenen kaynaklarınızın güvenli durumunu denetleme web temeli değerlendirme yetenekleri tooaccess hello.

## <a name="what-is-web-baseline-assessment"></a>Web temeli değerlendirmesi nedir?
OMS Güvenliği şu anda işletim sistemleri için güvenlik temeli değerlendirmesi sağlamaktadır. Bunu hello işletim sistemi ayarlarını, sunucularınızın her 24 saatte tarar ve savunmasız olabilecek ayarları görünüme sağlar. Bu seçenek hakkında daha fazla bilgi için [Operations Management Suite Güvenlik ve Denetim Çözümünde Temel Değerlendirmesi](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline) makalesini okuyun.

Merhaba hello Web temeli değerlendirme toofind savunmasız olabilecek web sunucusu ayarları hedefidir. Merhaba web temel yapılandırmalar için üç birincil kaynağı hello: .NET, ASP.NET ve IIS yapılandırması.  Yalnızca işletim sistemi temel değerlendirme hello gibi OMS güvenlik tooscan geçiyor, her 24hrs web sunucuları ve bunları güvenlik durumunu görünüme sağlayın.  Internet Information Service (IIS), çeşitli site ve uygulama düzeyleri toobe ilgili geçersiz kılınmış sağlayan, yapılandırmaları büyük ölçüde özelleştirilebilir. Merhaba tarayıcı toplama toohello varsayılan kök düzeyinde her uygulama/site düzeyinde hello ayarlarını denetler. Bu tooidentify savunmasız olabilecek ayarları yardımcı olur ve hızlı bir şekilde, bu ayarlar için bizim önerileri birlikte düzeltin.

>[!NOTE] 
>Merhaba ortak yapılandırma tanımlayıcıları ve temel bu OMS güvenliği tarafından kullanılan kurallar indirebilirsiniz [sayfa](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0).


## <a name="web-security-baseline-assessment"></a>Web güvenlik temeli değerlendirmesi

Bu önizleme için hello özelliği hello OMS arama seçeneği ve hello OMS güvenlik ve denetim Pano aracılığıyla erişilebilir. Tooperform tahsis hello sorgu Hello adımları izleyin:

1. Merhaba, **Microsoft Operations Management Suite** ana Pano tıklatın **güvenlik ve Denetim** döşeme.
2. Merhaba, **güvenlik ve Denetim** panoyu hello Web temel perspektif sonraki toohello işletim sistemi temel perspektif görebilirsiniz.
   
    ![OMS Güvenlik ve Denetim Web Güvenliği Temeli Değerlendirmesi](./media/oms-security-web-baseline/oms-security-web-baseline-fig5.png)

3. Merhaba sol bölmesinde Web kıyasla sunucuları toohello temel hello yüzde olarak ortalamasını tüm hesaplanan hello sunucularında geçirilen kuralları ve hello değerlendirilen sunucularının listesini hello sayısını gösterir.
4. Hello bölmesini listeler hello benzersiz sağ tarafından başarısız kuralları *önem*, ve *RuleType*. Kurallardan herhangi birinin hello sağ bölmede üzerinde tıklatarak bu kuralın hello Ayrıntılar gösterilir. Bir örnek hello görüntüsü aşağıda gösterilmiştir. değerlendirilir hello kural altında listelenen *kuralı ayarı*. Merhaba *AzId* hello temel kurallar izlemek için Microsoft tarafından kullanılan her bir kuralı için benzersiz bir tanımlayıcı alanı. Merhaba toothat kullanıcılar ayrıca görebilir *beklenen sonuç* (Microsoft'un önerilen değeri) ve diğer ayrıntıları ilgili hello kural hello güvenlik etkisi.
    
    ![Sorgu](./media/oms-security-web-baseline/oms-security-web-baseline-fig6.png)

5. Tooreview hello sonuçları kendi sorgular oluşturabilirsiniz. 

kullanabileceğiniz hello ilk sorgudur hello **Web temeli değerlendirme özeti**. Merhaba, **burada başlangıç arama** alanına, bu sorgu yazın: *türü SecurityBaselineSummary BaselineType = Web =*. Merhaba, bir çıktı örneği aşağıdadır:

![Sorgu Sonucu](./media/oms-security-web-baseline/oms-security-web-baseline-fig7.png)

>[!NOTE] 
>Bu sorguda her kayıt, tek bir sunucu üzerindeki değerlendirme özetini gösterir.

Hello olduğunuzda **günlük arama**, farklı sorgular tooobtain hello web temeli değerlendirme hakkında daha fazla bilgi yazabilirsiniz. Ayrıca toohello önceki sorgu olanları bu Önizleme'de aşağıdaki hello de kullanabilirsiniz:

**Web Temeli Kural Değerlendirmesi**: Her kayıt, tek bir sunucudaki tek bir web temeli kural değerlendirmesini temsil eder. Başarısız bir kural için tüm veriler hello içerdiği *SitePath* üzerinde hangi hello kural, hello değerlendirildi *beklenen sonuç*ve hello *gerçek sonucu*.

Sorgu: *Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*

![Sorgu Sonucu 2](./media/oms-security-web-baseline/oms-security-web-baseline-fig8.png)

**Belirli bir sunucu için tüm sonuçları göster**: Bu sorgu nasıl toosee sonuçlarını gösterir belirli bir sunucunun: Sorgu: *türü SecurityBaseline BaselineType = Web bilgisayar = BaselineTestVM1 =*

![Sorgu Sonucu 3](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

Bu kayıtları/sorguları toocreate kendi panolar, raporlar ve uyarılar kullanabilirsiniz. Burada, tooyour Pano ekleyebileceğiniz örnek UI denetimi verilmiştir. Bilgi edinebilirsiniz nasıl toovisualize OMS Görünüm Tasarımcısı kullanarak verilerinizi [burada](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). Merhaba ekranında aşağıdaki bu özelleştirme yaptıktan sonra hello döşemenin nasıl örneği nasıl görüneceği gösterilmektedir.

![pano](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede OMS Güvenlik ve Denetim Web Temeli değerlendirmesi hakkında bilgi edindiniz. toolearn OMS güvenlik hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:

* [Operations Management Suite'e (OMS) genel bakış](operations-management-suite-overview.md)
* [İzleme ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü](oms-security-responding-alerts.md)
* [Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme](oms-security-monitoring-resources.md)

