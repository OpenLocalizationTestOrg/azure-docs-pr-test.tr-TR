---
title: "Azure Güvenlik Merkezi'nde veri koleksiyonunu etkinleştirme | Microsoft Docs"
description: " Azure Güvenlik Merkezi'nde veri koleksiyonunu etkinleştirme hakkında bilgi edinin. "
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
ms.openlocfilehash: 7e9ad8cd8c77c57c37dc208b86b3727a4e1dc7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde veri toplamayı etkinleştir

> [!NOTE]
> Haziran 2017'nin ilk günlerinden itibaren Güvenlik Merkezi, veri toplamak ve depolamak için Microsoft Monitoring Agent'ı kullanacak. Daha fazla bilgi için bkz: [Azure Güvenlik Merkezi platformu geçiş](security-center-platform-migration.md). Bu makaledeki bilgiler, Microsoft Monitoring Agent'a geçiş sonrasındaki Güvenlik Merkezi işlevselliğine yöneliktir.
>
>

Güvenlik Merkezi, verilerinizin güvenlik durumunu değerlendirmek, güvenlik önerileri sağlamak ve sizi tehditlere karşı uyarmak için sanal makinelerinizden (VM) veri toplar. Güvenlik Merkezi ilk eriştiğinizde, aboneliğinizdeki tüm VM'ler için veri toplamayı etkinleştirmek için seçeneğiniz vardır. Veri toplama etkin değilse, Güvenlik Merkezi Bu abonelik için Güvenlik İlkesi'nde veri toplamayı Aç önerir.

Veri toplama etkinleştirilmişse, Güvenlik Merkezi hükümleri tüm mevcut Microsoft İzleme Aracısı Azure sanal makineleri ve oluşturulan yeni bir tane desteklenmiyor. Microsoft Monitoring Agent için güvenlikle ilgili çeşitli yapılandırmaları tarar. Ayrıca, işletim sistemi olay günlüğü olaylarını başlatır. Bu tür verilerin örnekleri şunlardır: işletim sistemi türü ve sürümü, işletim sistemi günlükleri (Windows olay günlükleri), çalışan işlemler, makine adı, IP adresleri, oturum açmış kullanıcı ve kiracı kimliği. Microsoft Monitoring Agent olay günlüğü girişleri ve yapılandırmaları okur ve verileri analiz için çalışma alanınızda kopyalar. Microsoft Monitoring Agent ayrıca alanınıza kilitlenme bilgi döküm dosyaları kopyalar.

Güvenlik Merkezi, ücretsiz katmanı kullanıyorsanız, Güvenlik İlkesi'nde veri toplamayı devre dışı bırakarak sanal makinelerden veri toplamayı devre dışı bırakabilirsiniz. Veri toplamayı devre dışı bırakma, VM'ler için güvenlik değerlendirmeleri sınırlar. Daha fazla bilgi için bkz: [veri toplamayı devre dışı bırakma](#disabling-data-collection). Veri toplamayı devre dışı bırakılmış olsa bile VM disk anlık görüntüler ve yapı toplama etkinleştirilir. Veri koleksiyonu Güvenlik Merkezi'nin standart katmanında abonelikler için gereklidir.

> [!NOTE]
> Güvenlik Merkezi'nin ücretsiz ve standart hakkında daha fazla bilgi [fiyatlandırma katmanlarına](security-center-pricing.md).
>
>

## <a name="implement-the-recommendation"></a>Öneriyi uygulamayı

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır. Bu belge hakkında adım adım kılavuz değildir.
>
>

1. İçinde **önerileri** dikey penceresinde, select **abonelikler için veri koleksiyonunu etkinleştir**.  Bu açılır **veri koleksiyonunu Aç** dikey.
   ![Öneriler dikey][2]
2. Üzerinde **veri koleksiyonunu Aç** dikey penceresinde, aboneliğinizi seçin. **Güvenlik İlkesi** Bu abonelik için bir dikey pencere açılır.
3. Üzerinde **Güvenlik İlkesi** dikey penceresinde, select **üzerinde** altında **veri toplama** günlükleri otomatik olarak toplamak için. Tüm geçerli ve yeni izleme uzantısı verileri koleksiyonu hükümleri üzerinde açma VM'ler abonelikte desteklenmiyor.
4. **Kaydet**’i seçin.
5. **Tamam**’ı seçin.

## <a name="disabling-data-collection"></a>Veri toplamayı devre dışı bırakma
Güvenlik Merkezi, ücretsiz katmanı kullanıyorsanız, Güvenlik İlkesi'nde veri toplamayı devre dışı bırakarak sanal makinelerden veri toplamayı dilediğiniz zaman devre dışı bırakabilirsiniz. Veri koleksiyonu Güvenlik Merkezi'nin standart katmanında abonelikler için gereklidir.

1. Geri dönüp **Güvenlik Merkezi** dikey penceresinde ve select **İlkesi** döşeme. Bu açılır **abonelik başına ilke güvenlik ilkesi-tanımlama** dikey.
   ![İlke kutucuk seçin][5]
2. Üzerinde **abonelik başına ilke güvenlik ilkesi-tanımlama** dikey penceresinde, veri toplamayı devre dışı bırakmak istediğiniz aboneliği seçin.
3. **Güvenlik İlkesi** Bu abonelik için bir dikey pencere açılır.  Seçin **kapalı** veri toplama altında.
4. Seçin **kaydetmek** üst Şeritte.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede "veri toplamayı etkinleştirmek" Güvenlik Merkezi öneriyi uygulamayı nasıl oluşturulacağını gösterir Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -- Azure abonelikleriniz ve kaynak gruplarınız için güvenlik ilkelerini yapılandırma hakkında bilgi edinin.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) - Azure kaynaklarınızın sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.
* [Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) - Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.
- [Azure Güvenlik Merkezi veri güvenliği](security-center-data-security.md) -verilerin yönetilmesi ve diğer Güvenlik Merkezi'nde korunması nasıl öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) - Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - En son Azure güvenlik haberlerini ve bilgilerini edinin.

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
