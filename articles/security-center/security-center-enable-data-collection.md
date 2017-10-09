---
title: "Azure Güvenlik Merkezi'nde aaaEnable veri toplama | Microsoft Docs"
description: " Bilgi nasıl Azure Güvenlik Merkezi'nde tooenable veri koleksiyonu. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 78bbf9a3d852095e2a1387c1606ff4bbb778a0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde veri toplamayı etkinleştir

> [!NOTE]
> İçinde erken Haziran 2017'den itibaren Güvenlik Merkezi hello Microsoft İzleme Aracısı toocollect kullanmak ve verileri depolamak. toolearn daha, fazla [Azure Güvenlik Merkezi platformu geçiş](security-center-platform-migration.md). Bu makaledeki Hello bilgiler geçiş toohello sonra Microsoft İzleme Aracısı Güvenlik Merkezi işlevlerini temsil eder.
>
>

Güvenlik Merkezi, sanal makineleri (VM'ler) tooassess güvenlik durumlarına toplar, güvenlik önerileri sağlamak ve toothreats sizi uyarır. İlk Güvenlik Merkezi erişim aboneliğinizdeki tüm VM'ler için hello seçeneği tooenable veri koleksiyonu vardır. Veri toplama etkin değilse, Güvenlik Merkezi Bu abonelik için hello Güvenlik İlkesi'nde veri toplamayı Aç önerir.

Veri toplama etkinleştirilmişse, Güvenlik Merkezi hükümleri hello Microsoft İzleme Aracısı tüm mevcut Azure sanal makineleri ve oluşturulan yeni bir tane desteklenmiyor. Merhaba Microsoft Monitoring Agent için güvenlikle ilgili çeşitli yapılandırmaları tarar. Ayrıca, olay günlüğü olaylarını hello işletim sistemini başlatır. Bu tür verilerin örnekleri şunlardır: işletim sistemi türü ve sürümü, işletim sistemi günlükleri (Windows olay günlükleri), çalışan işlemler, makine adı, IP adresleri, oturum açmış kullanıcı ve kiracı kimliği. Merhaba Microsoft Monitoring Agent olay günlüğü girişleri ve yapılandırmaları okur ve analiz için hello veri tooyour çalışma kopyalar. Merhaba Microsoft Monitoring Agent ayrıca kilitlenme döküm dosyaları tooyour çalışma kopyalar.

Güvenlik Merkezi'nin hello ücretsiz katmanı kullanıyorsanız, hello Güvenlik İlkesi'nde veri toplamayı devre dışı bırakarak sanal makinelerden veri toplamayı devre dışı bırakabilirsiniz. Veri toplamayı devre dışı bırakma, VM'ler için güvenlik değerlendirmeleri sınırlar. toolearn daha, fazla [veri toplamayı devre dışı bırakma](#disabling-data-collection). Veri toplamayı devre dışı bırakılmış olsa bile VM disk anlık görüntüler ve yapı toplama etkinleştirilir. Veri koleksiyonu Güvenlik Merkezi'nin standart katmanda hello abonelikler için gereklidir.

> [!NOTE]
> Güvenlik Merkezi'nin ücretsiz ve standart hakkında daha fazla bilgi [fiyatlandırma katmanlarına](security-center-pricing.md).
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar. Bu belge hakkında adım adım kılavuz değildir.
>
>

1. Merhaba, **önerileri** dikey penceresinde, select **abonelikler için veri koleksiyonunu etkinleştir**.  Merhaba açılır **veri koleksiyonunu Aç** dikey.
   ![Öneriler dikey][2]
2. Merhaba üzerinde **veri koleksiyonunu Aç** dikey penceresinde, aboneliğinizi seçin. Merhaba **Güvenlik İlkesi** Bu abonelik için bir dikey pencere açılır.
3. Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde, select **üzerinde** altında **veri toplama** tooautomatically günlüklerini toplayın. Tüm geçerli ve yeni veri toplama hükümleri hello üzerinde izleme uzantısı etkinleştirdikten VM'ler hello abonelikte desteklenmiyor.
4. **Kaydet**’i seçin.
5. **Tamam**’ı seçin.

## <a name="disabling-data-collection"></a>Veri toplamayı devre dışı bırakma
Güvenlik Merkezi'nin hello ücretsiz katmanı kullanıyorsanız, hello Güvenlik İlkesi'nde veri toplamayı devre dışı bırakarak sanal makinelerden veri toplamayı dilediğiniz zaman devre dışı bırakabilirsiniz. Veri koleksiyonu Güvenlik Merkezi'nin standart katmanda hello abonelikler için gereklidir.

1. Toohello iade **Güvenlik Merkezi** dikey penceresinde ve select hello **İlkesi** döşeme. Merhaba açılır **abonelik başına ilke güvenlik ilkesi-tanımlama** dikey.
   ![Hello İlkesi kutucuk seçin][5]
2. Merhaba üzerinde **abonelik başına ilke güvenlik ilkesi-tanımlama** dikey penceresinde, select hello abonelik toodisable veri toplama istiyor.
3. Merhaba **Güvenlik İlkesi** Bu abonelik için bir dikey pencere açılır.  Seçin **kapalı** veri toplama altında.
4. Seçin **kaydetmek** hello üst Şeritte.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl tooimplement hello Güvenlik Merkezi öneri "etkin veri toplama." gösterdi. Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md)--nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md)--öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
- [Azure Güvenlik Merkezi veri güvenliği](security-center-data-security.md) -verilerin yönetilmesi ve diğer Güvenlik Merkezi'nde korunması nasıl öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md)--hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/)--hello en son Azure güvenlik haberlerini ve bilgilerini alın.

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
