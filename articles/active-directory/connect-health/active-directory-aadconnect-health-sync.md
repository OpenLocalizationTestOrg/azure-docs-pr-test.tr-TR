---
title: "Azure AD Connect Health eşitleme ile aaaUsing | Microsoft Docs"
description: "Bu, nasıl toomonitor Azure AD Connect eşitleme ele alınacaktır hello Azure AD Connect Health sayfasıdır."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>Azure AD Connect eşitlemesini Azure AD Connect Health ile izleme
Belge aşağıdaki hello belirli toomonitoring Azure AD Connect (eşitleme) Azure AD Connect Health ile olur.  Azure Connect Health ile AD FS'yi izleme hakkında bilgi almak için bkz. [Azure AD Connect Health'i AD FS ile kullanma](active-directory-aadconnect-health-adfs.md). Ek olarak, Active Directory Etki Alanı Hizmetleri’ni Azure AD Connect Health ile izleme hakkında bilgi için bkz. [AD DS ile Azure AD Connect Health Kullanma](active-directory-aadconnect-health-adds.md).

![Eşitleme için Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>Eşitleme için Azure AD Connect Health uyarıları
Hello Azure AD Connect Health uyarıları eşitleme bölümü için etkin uyarıların listesi hello sağlar. Her uyarı ilgili bilgileri, çözüm adımları ve bağlantıları toorelated belgeleri içerir. Etkin veya çözümlenmiş bir uyarıyı seçtiğinizde tooresolve hello uyarı ve bağlantıları tooadditional belgelerine atabileceğiniz adımlar yanı sıra ek bilgiler içeren yeni bir dikey pencere görürsünüz. Ayrıca, geçmiş verileri hello geçmişte çözümlenen uyarıları görüntüleyebilirsiniz.

Adımları yanı sıra ek bilgiler sağlanacak bir uyarıyı seçtiğinizde tooadditional belgelerine tooresolve hello uyarı ve bağlantıları alabilir.

![Azure AD Connect eşitleme hatası](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>Sınırlı Uyarı Değerlendirmesi
Azure AD Connect (örneğin, öznitelik filtrelemesi hello varsayılan yapılandırma tooa özel yapılandırma değiştirildiyse) hello varsayılan yapılandırmayı kullanmıyorsa, ardından hello Azure AD Connect Health Aracısı hello hata olayları ilgili tooAzure karşıya yüklemez AD bağlanın.

Bu uyarı hello değerlendirmesi hello hizmeti tarafından sınırlar. Hello Azure Portal'da hizmetinizin altında bu koşulu belirten bir başlık görürsünüz.

![Eşitleme için Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner.png)

Bu, "Ayarlar" a tıklayarak ve Azure AD Connect Health Aracısı tooupload tüm hata günlüklerini vererek değiştirebilirsiniz.

![Eşitleme için Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>Eşitleme Öngörüsü
Sık yöneticileri, tooknow toosync değişiklikleri tooAzure AD ve gerçekleşmesini değişiklikleri hello miktarını hello süresini hakkında istiyor. Bu özellik bir kolay bir yolu toovisualize bu grafikleri aşağıda hello kullanarak aşağıdakileri sağlar:   

* Eşitleme işlemlerinin gecikme süresi
* Nesne Değişikliği eğilimi

### <a name="sync-latency"></a>Eşitleme Gecikme Süresi
Bu özellik, gecikme hello eşitleme işlemlerinin (içeri aktarma, dışarı aktarma, vb.) bağlayıcıların grafik eğilimini sağlar.  Bu hızlı sağlar ve kolay bir yolu toounderstand daha fazla incelenmesi gerekebilecek hello gecikme süresi içinde değil yalnızca işlemlerinizin (çok sayıda değişikliğinizin varsa, daha büyük) de bir şekilde toodetect anormallikleri gecikme hello.

![Eşitleme Gecikme Süresi](./media/active-directory-aadconnect-health-sync/synclatency02.png)

Varsayılan olarak, yalnızca hello 'Verme' işlemi'hello Azure AD Bağlayıcısı için hello gecikme gösterilir.  toosee hello bağlayıcı üzerinde daha fazla işlem veya diğer bağlayıcılara tooview işlemleri hello grafikte sağ grafiği Düzenle öğesini seçmeniz veya hello "Gecikmesi grafiği Düzenle" düğmesine tıklayın ve hello belirli işlemi ve bağlayıcıları seçin.

### <a name="sync-object-changes"></a>Eşitleme Nesnesi Değişiklikleri
Bu özellik, değerlendirilen ve tooAzure AD dışarı değişiklikleri hello sayısının grafik eğilimini sağlar.  Bugün, çalışırken toogather bu bilgileri hello eşitleme günlüklerinden zordur.  Merhaba grafik, ortamınızda oluşan değişiklik hello sayısı, aynı zamanda yaşanan hello hataları görsel görünümünü İzleme yalnızca daha basit bir yol sağlar.

![Eşitleme Gecikme Süresi](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>Nesne Düzeyinde Eşitleme Hata Raporu (Önizleme)
Bu özellik, kimlik verileri Azure AD Connect kullanılarak Windows Server AD ile Azure AD arasında eşitlenirken oluşabilecek eşitleme hataları hakkında bir rapor sağlar.

* Merhaba raporun kapsadığı hello eşitleme istemcisi tarafından kaydedilen hataları (Azure AD Connect sürüm 1.1.281.0 veya üzeri)
* Merhaba eşitleme altyapısı hello son eşitleme işlemi oluştu hello hataları içerir. ("Merhaba Azure AD Bağlayıcısı üzerinde ver.")
* Eşitleme için Azure AD Connect Health aracısını hello rapor tooinclude hello en son veriler için giden bağlantı gerekli toohello bitiş noktası olması gerekir.
* Merhaba rapor **her 30 dakika sonra güncelleştirilmiş** hello verileri kullanarak eşitleme için Azure AD Connect Health aracısı tarafından yüklendi. Aşağıdaki temel işlevler hello sağlar

  * Hataların kategorilere ayrılması
  * Kategoriye göre hatalı nesnelerin listesi
  * Tek bir yerde hello hatalarını ilgili tüm hello verileri
  * Yan yana tooa çakışması nedeniyle hatasıyla nesnelerin yan karşılaştırma
  * Merhaba hata raporu (yakında) CVS karşıdan yükle

### <a name="categorization-of-errors"></a>Hataların Kategorilere Ayrılması
Merhaba rapor kategorileri aşağıdaki hello hello mevcut eşitleme hatalarının gruplandırır:

| Kategori | Açıklama |
| --- | --- |
| Yinelenen Öznitelik |Azure AD Connect, bir Kiracıda benzersiz olması gereken ve Azure AD Connect’te bulunan bir veya daha fazla özniteliğin (proxyAddresses ve UserPrincipalName gibi) yinelenen değerleri ile nesneler oluşturmaya veya güncelleştirmeye çalıştığında oluşan hatalar. |
| Veri Uyuşmazlığı |Eşitleme hatalarına neden toomatch nesneleri Hello soft-match başarısız olduğunda hataları. |
| Veri Doğrulama Hatası |Hataları UserPrincipalName gibi kritik öznitelikleri desteklenmeyen karakterler gibi tooinvalid verileri nedeniyle başarısız Azure AD'de yazılmakta önce doğrulama hatalarını biçimlendirin. |
| Büyük Öznitelik |Bir veya daha fazla öznitelik hello büyük olduğunda hataları izin verilen boyutu, uzunluk veya sayısı. |
| Diğer |Kategoriler yukarıda hello uymayan tüm diğer hatalar. Bu kategori, geri bildirimleriniz temel alınarak alt kategorilere ayrılacaktır. |

![Eşitleme Hata Raporu Özeti](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Eşitleme Hata Raporu Kategorileri](./media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>Kategoriye göre hatalı nesnelerin listesi
Her kategoride ayrıntılara hello hata kategoriye sahip nesneleri hello listesini sağlar.
![Eşitleme Hata Raporu Listesi](./media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>Hata Ayrıntıları
Veri aşağıdaki kullanılabilir hello ayrıntılı görünümü her hata için

* Merhaba tanımlayıcıları *AD nesne* söz konusu
* Merhaba tanımlayıcıları *Azure AD nesne* (uygun şekilde) dahil
* Hata açıklaması ve nasıl toofix
* İlgili makaleler

![Eşitleme Hata Raporu Ayrıntıları](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a>Merhaba hata raporu CSV olarak indir
Merhaba seçerek "tüm hello hataları ile ilgili tüm hello ayrıntıları içeren CSV dosyası indirebilirsiniz dışa aktarma düğmesi".

## <a name="related-links"></a>İlgili bağlantılar
* [Eşitleme sırasında karşılaşılan Hataları giderme](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [Yinelenen Öznitelik Dayanıklılığı](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health Aracısı Yüklemesi](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health İşlemleri](active-directory-aadconnect-health-operations.md)
* [Azure AD Connect Health'i AD FS ile Kullanma](active-directory-aadconnect-health-adfs.md)
* [Azure AD Connect Health'i AD DS ile Kullanma](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health ile ilgili SSS](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health Sürüm Geçmişi](active-directory-aadconnect-health-version-history.md)