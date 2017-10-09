---
title: "Yönetim Paketi güvenlik ve denetim çözüm temel aaaOperations | Microsoft Docs"
description: "Bu belge açıklar nasıl toouse OMS güvenlik ve denetim çözüm tooperform tüm izlenen bilgisayarların uyumluluk ve güvenlik amaç için bir taban çizgisi değerlendirmesi."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: ea52408cb9d2598728fe3826a946067e1c99318f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Operations Management Suite Güvenlik ve Denetim Çözümünde Temel Değerlendirmesi
Bu belge toouse yardımcı olur [Operations Management Suite (OMS) güvenlik ve denetim çözümü](operations-management-suite-overview.md) yetenekleri tooaccess hello izlenen kaynaklarınızın güvenli durumunu temel değerlendirmesi.

## <a name="what-is-baseline-assessment"></a>Temel Değerlendirmesi nedir?
Dünya çapındaki sektör ve devlet kuruluşlarıyla birlikte Microsoft, yüksek güvenlikli sunucu dağıtımlarını temsil eden bir Windows yapılandırması tanımlar. Bu yapılandırma, kayıt defteri anahtarlarının, denetim ilkesi ayarlarının ve güvenlik ilkesi ayarlarının yanı sıra Microsoft'un bu ayarlar için önerilen değerlerinden oluşan bir kümedir. Bu kural kümesi, Güvenlik temeli olarak bilinir. OMS Güvenlik ve Denetim temeli değerlendirmesiyle tüm bilgisayarlarınız uyumluluk açısından sorunsuz bir biçimde taranır. 

Üç kural türü mevcuttur:

* **Kayıt defteri kuralları**: Kayıt defteri anahtarlarının doğru şekilde ayarlanıp ayarlanmadığını denetler.
* **Denetim ilkesi kuralları**: Denetim ilkenize ilişkin kurallardır.
* **Güvenlik İlkesi kuralları**: hello makine ilgili hello kullanıcının izinlerini kuralları.

> [!NOTE]
> Okuma [kullanım OMS güvenlik tooassess hello güvenlik yapılandırma temeli](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/) için bu özelliği kısa bir genel bakış.
> 
> 

## <a name="security-baseline-assessment"></a>Güvenlik Temeli Değerlendirmesi
OMS güvenlik ve denetim hello Panoyu kullanarak tarafından izlenen tüm bilgisayarlar için geçerli güvenlik temel değerlendirmeniz gözden geçirebilirsiniz.  Aşağıdaki adımları tooaccess hello güvenlik temeli değerlendirme Panosu hello yürütün:

1. Merhaba, **Microsoft Operations Management Suite** ana Pano tıklatın **güvenlik ve Denetim** döşeme.
2. Merhaba, **güvenlik ve Denetim** panoyu tıklatın **temeli değerlendirme** altında **güvenlik etki alanları**. Merhaba **güvenlik temeli değerlendirme** Pano hello görüntü aşağıdaki gösterildiği gibi görünür:
   
    ![OMS Güvenlik ve Denetim Temeli Değerlendirmesi](./media/oms-security-baseline/oms-security-baseline-fig1.png)

Bu pano üç ana bölüme ayrılır:

* **Bilgisayarlar karşılaştırıldığında toobaseline**: Bu bölümde hello erişilen ve hello hello değerlendirme geçirilen bilgisayar yüzdesini bilgisayarların sayısı bir özetini verir. Bu ayrıca hello üst 10 bilgisayarları ve hello yüzdesi sonuç hello değerlendirmesi için verir.
* **Kural durumu gerekli**: Bu bölümün önem derecesine göre hello hedefi toobring tanıma hello başarısız kuralları var ve türe göre kuralları başarısız oldu. Çoğu hello kuralları başarısız olursa, hızlı bir şekilde tanımlayabilirsiniz toohello ilk grafik bakarak veya değil, önemlidir. Ayrıca, hello üst 10 başarısız kuralları ve önem derecesine listesini verir. Merhaba ikinci grafik hello değerlendirme sırasında başarısız olan kuralı hello türünü gösterir. 
* **Taban çizgisi değerlendirme eksik olan bilgisayarlar**: Bu bölümde toooperating sistem uyumsuzluk veya hatalar erişilen değil hello bilgisayarları listeler. 

### <a name="accessing-computers-compared-toobaseline"></a>Karşılaştırılan toobaseline bilgisayarlara erişim
İdeal olarak tüm bilgisayarlarınızı hello güvenlik temel değerlendirmesi ile uyumlu olmalıdır. Ancak bazı durumlarda bunun olmaması olağandır. Merhaba güvenlik yönetimi işleminin bir parçası olarak, tüm güvenlik değerlendirmesi testleri toopass başarısız hello bilgisayarlar gözden geçirme önemli tooinclude olduğu. Merhaba seçeneğini belirleyerek olan bir hızlı yol toovisualize **erişilen bilgisayarlar** hello bulunan **bilgisayarlar karşılaştırıldığında toobaseline** bölümü. Merhaba ekranında aşağıdaki gösterildiği gibi hello günlük arama sonucu gösteren hello bilgisayarların listesini görmeniz gerekir:

![Erişilen bilgisayar sonuçları](./media/oms-security-baseline/oms-security-baseline-fig2.png)

Merhaba arama sonucu burada hello ilk sütun hello bilgisayar adı ve başarısız kuralları hello sayısı hello ikinci renk sahip bir tablo biçiminde gösterilir. başarısız oldu, kural hello türü ile ilgili tooretrieve hello bilgi tıklatın hello bilgisayar adının yanı sıra başarısız kuralları hello sayısı. Bir sonuç benzer toohello bir görüntü aşağıdaki hello gösterilen görmeniz gerekir:

![Erişilen bilgisayar sonuçlarına ilişkin ayrıntılar](./media/oms-security-baseline/oms-security-baseline-fig3.png)

Bu arama sonucunda, erişilen kuralları hello toplam sahip, başarısız olan kritik kurallar sayısı Merhaba, uyarı kuralları hello ve bilgi başarısız kuralları hello.

### <a name="accessing-required-rules-status"></a>Gerekli kurallar durumuna erişme
Hello yüzdesi hello değerlendirme geçirilen bilgisayar sayısı ile ilgili Hello bilgi aldıktan sonra hangi kuralları hakkında daha fazla bilgi according toohello kritiklik başarısız tooobtain isteyebilirsiniz. Hangi bilgisayarların olmalıdır tooprioritize ilk tooensure ele bu görselleştirme yardımcı bunlar hello sonraki değerlendirmesi uyumlu olur. Merhaba kritik hello bulunan hello grafiğin parçası üzerine gelerek **başarısız kuralları önem derecesine göre** altında döşeme **gerekli kuralları durum** ve tıklatın. Ekran izleyen bir sonuç benzer toohello görmeniz gerekir:

![Önem derecesine göre başarısız olan kurallara ilişkin ayrıntılar](./media/oms-security-baseline/oms-security-baseline-fig4.png) 

Bu günlük sonucunda başarısız oldu, bu kural, bu güvenlik kuralı hello Common Configuration Enumeration (CCE) kimliği hello açıklaması temel kuralı hello türü bakın. Bu öznitelikler yeterli tooperform düzeltme eylemi toofix hello hedef bilgisayarda bu sorun olması gerekir.

> [!NOTE]
> Merhaba CCE hakkında daha fazla bilgi için erişim [Ulusal Güvenlik Açığı veritabanı](https://nvd.nist.gov/cce/index.cfm).
> 
> 

### <a name="accessing-computers-missing-baseline-assessment"></a>Temel değerlendirmesi eksik bilgisayarlara erişim
OMS hello etki alanı üyesi ve etki alanı denetleyicisi temel profil tooWindows Server 2012 R2'in Windows Server 2008 R2'de destekler. Windows Server 2016 temeli, henüz tamamlanmamıştır ve yayımlandıktan hemen sonra eklenecektir. OMS güvenlik ve denetim temel değerlendirmesi taranan tüm diğer işletim sistemlerinin hello altında görünür **temeli değerlendirme eksik olan bilgisayarlar** bölümü.

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede OMS Güvenlik ve Denetim temeli değerlendirmesi hakkında bilgi edindiniz. toolearn OMS güvenlik hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:

* [Operations Management Suite'e (OMS) genel bakış](operations-management-suite-overview.md)
* [İzleme ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü](oms-security-responding-alerts.md)
* [Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme](oms-security-monitoring-resources.md)

