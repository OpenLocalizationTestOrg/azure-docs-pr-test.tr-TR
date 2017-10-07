---
title: "aaaAzure Güvenlik Merkezi Hızlı Başlangıç Kılavuzu | Microsoft Docs"
description: "Bu makalede Azure Güvenlik Merkezi ile Merhaba güvenlik izleme ve ilke yönetimi bileşenleri hakkında size rehberlik ederek ve toonext adımları bağlama hızla başlamanıza yardımcı olur."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 23b2444ba1ba30d0a1bd1a1afbc4fd0abfd0827c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-quick-start-guide"></a>Azure Güvenlik Merkezi hızlı başlangıç kılavuzu
Bu makalede hello güvenlik izleme ve ilke yönetimi bileşenleri hakkında Güvenlik Merkezi'nin size kılavuzluk ederek Azure Güvenlik Merkezi ile hızla başlamanıza yardımcı olur.

> [!NOTE]
> İçinde erken Haziran 2017'den itibaren Güvenlik Merkezi hello Microsoft İzleme Aracısı toocollect kullanmak ve verileri depolamak. Bkz: [Azure Güvenlik Merkezi platformu geçiş](security-center-platform-migration.md) toolearn daha fazla. Bu makaledeki Hello bilgiler geçiş toohello sonra Microsoft İzleme Aracısı Güvenlik Merkezi işlevlerini temsil eder.
>
>

## <a name="prerequisites"></a>Ön koşullar
Güvenlik Merkezi ile çalışmaya tooget abonelik tooMicrosoft Azure olması gerekir. Bir aboneliğiniz yoksa [ücretsiz hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.

Hello ücretsiz katmanı Güvenlik Merkezi, aboneliğiniz ile otomatik olarak etkinleştirilir ve Azure kaynaklarınızın güvenlik durumunu hello görünürlük sağlar. Bu katman temel güvenlik ilkesi yönetimi, güvenlik önerileri ve Azure iş ortaklarının güvenlik ürün ve hizmetleri ile tümleştirme sağlar.

Merhaba Güvenlik Merkezi erişim [Azure portal](https://azure.microsoft.com/features/azure-portal/). toolearn hello Azure portal hakkında daha fazla bilgi görmek hello [portal belgeleri](https://azure.microsoft.com/documentation/services/azure-portal/).

## <a name="permissions"></a>İzinler
Güvenlik Merkezi'nde, yalnızca ilgili bilgiler görürsünüz tooan sahibi, katkıda bulunan veya okuyucu bir kaynağa ait hello abonelik veya kaynak grubu için hello rolüne atandığında Azure kaynak. Bkz: [izinleri Azure Güvenlik Merkezi'nde](security-center-permissions.md) toolearn rolleri ve Güvenlik Merkezi'nde izin verilen eylemleri hakkında daha fazla.

## <a name="data-collection"></a>Veri toplama
Güvenlik Merkezi, sanal makineleri (VM'ler) tooassess güvenlik durumlarına toplar, güvenlik önerileri sağlamak ve toothreats sizi uyarır. Güvenlik Merkezi’ne ilk kez eriştiğinizde aboneliğinizdeki tüm sanal makinelerde veri toplama etkindir. Güvenlik Merkezi hükümleri hello Microsoft İzleme Aracısı tüm mevcut Azure Vm'leri ve oluşturulan yeni bir tane desteklenir. Bkz: [veri koleksiyonunu etkinleştir](security-center-enable-data-collection.md) toolearn veri toplama nasıl çalıştığı hakkında daha fazla.

Veri toplama önerilir. Güvenlik Merkezi'nin hello ücretsiz katmanı kullanıyorsanız, hello Güvenlik İlkesi'nde veri toplamayı devre dışı bırakarak VM'ler veri koleksiyonunu devre dışı bırakabilirsiniz. Veri koleksiyonu Güvenlik Merkezi'nin standart katmanda hello abonelikler için gereklidir. Bkz: [Güvenlik Merkezi fiyatlandırma](security-center-pricing.md) hakkında daha fazla bilgi toolearn hello ücretsiz ve standart fiyatlandırma katmanları.

Güvenlik Merkezi bileşenlerinin nasıl tooaccess ve kullanım hello hello aşağıdaki adımları açıklanmaktadır. Bu adımlarda, nasıl gösteriyoruz tooturn tooopt çıkışı seçerseniz veri toplamayı devre dışı.

> [!NOTE]
> Bu makalede, örnek bir dağıtım kullanarak hello hizmeti sunar. Bu makale adım adım ilerleyen bir kılavuz değildir.
>
>

## <a name="access-security-center"></a>Güvenlik Merkezi'ne erişme
Merhaba Portalı'nda bu adımları tooaccess Güvenlik Merkezi izleyin:

1. Merhaba üzerinde **Microsoft Azure** menüsünde, select **Güvenlik Merkezi**.

   ![Azure menüsü][1]
2. Güvenlik Merkezi hello için ilk kez erişiyorsanız hello **Hoş Geldiniz** dikey pencere açılır. Seçin **başlatma Güvenlik Merkezi** tooopen hello **Güvenlik Merkezi** dikey penceresinde ve tooenable veri koleksiyonu.
   ![Hoş Geldiniz ekranı][10]
3. Güvenlik Merkezi hello Hoş Geldiniz dikey penceresinden başlatın veya Güvenlik Merkezi hello Microsoft Azure menüsünü seçtikten sonra hello **Güvenlik Merkezi** dikey pencere açılır. Kolay erişim toohello için **Güvenlik Merkezi** dikey penceresinde hello gelecekteki, select hello **PIN dikey toodashboard** seçeneğini (sağ üstte).
   ![PIN dikey toodashboard seçeneği][2]

## <a name="use-security-center"></a>Güvenlik Merkezi'ni Kullanma
Azure abonelikleriniz ve kaynak grupları için güvenlik ilkelerini yapılandırabilirsiniz. Aboneliğiniz için bir güvenlik ilkesi yapılandıralım:

1. Merhaba üzerinde **Güvenlik Merkezi** dikey penceresinde, select hello **İlkesi** döşeme.
2. Merhaba üzerinde **güvenlik ilkesi - abonelik başına ilkesi tanımlama** dikey penceresinde bir abonelik seçin.
3. Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde **veri toplama** etkin tooautomatically toplama günlükleri değil. İzleme uzantısı hello hello Abonelikteki tüm geçerli ve yeni olan sanal makineleri üzerinde sağlanır. (Merhaba ücretsiz katmanında Güvenlik Merkezi, veri toplama dışında ayarlayarak seçebilirsiniz **veri toplama** çok**devre dışı**. Ayarı **veri toplama** çok**kapalı** Güvenlik Merkezi, güvenlik uyarısı ve öneri vermelerini önler.)
4. Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde, select **önleme İlkesi**. Merhaba açılır **önleme İlkesi** dikey.
5. Merhaba üzerinde **önleme İlkesi** dikey penceresinde hello öneriler güvenlik ilkenizin bir parçası olarak toosee istediğiniz açın. Örnekler:

   * Ayarı **sistem güncelleştirmeleri** çok**üzerinde** taramaları tüm işletim sistemi güncelleştirmeleri eksik VM'ler desteklenir.
   * Ayarı **işletim sistemi güvenlik açıkları** çok**üzerinde** duruma sokan bir işletim sistemi yapılandırmasını tüm desteklenen VM'ler tooidentify taramaları hello VM daha savunmasız tooattack.

### <a name="view-recommendations"></a>Önerileri görüntüleme
1. Toohello iade **Güvenlik Merkezi** dikey penceresinde ve select hello **önerileri** döşeme. Güvenlik Merkezi düzenli aralıklarla hello Azure kaynaklarınızın güvenlik durumunu çözümler. Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde hello hakkında öneriler gösterir **önerileri** dikey.
   ![Azure Güvenlik Merkezi'nde öneriler][5]
2. Merhaba bir öneriye seçin **önerileri** dikey tooview daha fazla bilgi ve/veya tootake eylem tooresolve hello sorun.

### <a name="view-hello-security-state-of-your-resources"></a>Merhaba kaynaklarınızın güvenlik durumunu görüntüleyin
1. Toohello iade **Güvenlik Merkezi** dikey. Merhaba **önleme** hello Pano bölümü, ağ, veri ve uygulamaları VM'ler için hello güvenlik durumu göstergelerini içerir.
2. Seçin **işlem** tooview daha fazla bilgi. Merhaba **işlem** gösteren üç sekme dikey pencere açılır:

  - **Genel Bakış** -izleme içerir ve VM öneriler.
  - **Sanal makineler** -tüm sanal makineleri ve geçerli güvenlik listeler durumları.
  - **Bulut Hizmetleri** -Güvenlik Merkezi tarafından izlenen web ve çalışan rolleri listeler.

    ![Azure Güvenlik Merkezi'nde Hello kaynak durumu kutucuğu][6]

3. Merhaba üzerinde **genel bakış** sekmesinde, bir önerinin altında seçin **sanal makine önerileri** tooview daha fazla bilgi ve/veya Al eylem tooconfigure gerekli denetimleri.
4. Merhaba üzerinde **sanal makineleri** sekmesinde, bir VM tooview ek Ayrıntılar'ı seçin.

### <a name="view-security-alerts"></a>Güvenlik uyarılarını görüntüleme
1. Toohello iade **Güvenlik Merkezi** dikey penceresinde ve select hello **güvenlik uyarıları** döşeme. Merhaba **güvenlik uyarıları** dikey penceresi açılır ve uyarı listesini görüntüler. Merhaba, güvenlik günlüklerinizin ve ağ etkinliğinin Güvenlik Merkezi çözümlemesi Bu uyarılar oluşturur. Tümleşik iş ortağı çözümlerinden gelen uyarılar buna dahildir.
   ![Azure Güvenlik Merkezi'ndeki güvenlik uyarıları][7]

   > [!NOTE]
   > Güvenlik Uyarıları, yalnızca Güvenlik Merkezi'nin standart katmanı hello etkinse kullanılabilir. 60 günlük ücretsiz bir deneme hello standart katman kullanılabilir. Bkz: [sonraki adımlar](#next-steps) nasıl tooget hello standart bilgi katmanı.
   >
   >
2. Bir uyarı tooview ek bilgileri seçin. Bu örnekte **Değiştirilen sistem ikili dosyası bulundu** seçeneğini kullanalım. Merhaba uyarı hakkında daha ayrıntılı bilgi sağlamayı dikey pencere açılır.
   ![Azure Güvenlik Merkezi'nde güvenlik uyarısı ayrıntıları][8]

### <a name="view-hello-health-of-your-partner-solutions"></a>İş ortağı çözümlerinizin hello durumunu görüntüle
1. Toohello iade **Güvenlik Merkezi** dikey. Merhaba **iş ortağı çözümleri** hello Azure aboneliğinizle tümleşik iş ortağı çözümlerinizin sistem durumunu izlemenizi, bir bakışta döşeme sağlar.
2. Select hello **iş ortağı çözümleri** döşeme. Bir dikey pencere açılır ve bağlanmış tooSecurity Center iş ortağı çözümlerinizin listesini görüntüler.
   ![İş ortağı çözümleri][9]
3. İş ortağı çözümü seçin. Bu örnekte, şimdi hello seçin **QualysVa1** çözümü.  Bir dikey pencere açılır ve ilişkili kaynakları hello iş ortağı çözümü ve hello çözümün hello durumunu gösterir. Seçin **çözüm konsolunu** tooopen hello iş ortağı Yönetimi deneyimini Bu çözüm için.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede toohello güvenlik izleme ve ilke yönetimi bileşenleri Güvenlik Merkezi kullanıma sunuldu. Güvenlik Merkezi ile tanıdık, hello aşağıdaki adımları deneyin:

* Azure aboneliğiniz için bir güvenlik ilkesi yapılandırın. toolearn daha, fazla [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md).
* Merhaba önerileri kullanın Azure kaynaklarınızı korumanıza Güvenlik Merkezi toohelp. toolearn daha, fazla [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md).
* Geçerli güvenlik uyarılarınızı gözden geçirin ve yönetin. toolearn daha, fazla [yönetme ve yanıt toosecurity Azure Güvenlik Merkezi'nde uyarıları](security-center-managing-and-responding-alerts.md).
- [Azure Güvenlik Merkezi veri güvenliği](security-center-data-security.md) -verilerin yönetilmesi ve diğer Güvenlik Merkezi'nde korunması nasıl öğrenin.
* Merhaba hakkında daha fazla bilgi [tehdit Gelişmiş algılama özelliklerini](security-center-detection-capabilities.md) hello ile gelen [standart katmanı](security-center-pricing.md) Güvenlik Merkezi'nin. Merhaba standart katmanı, ilk 60 gün Merhaba ücretsiz sunulur.
* Merhaba Güvenlik Merkezi'ni kullanma hakkında sorularınız varsa bkz [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md).

<!--Image references-->
[1]: ./media/security-center-get-started/azure-menu.png
[2]: ./media/security-center-get-started/security-center-pin.png
[3]: ./media/security-center-get-started/security-policy.png
[4]: ./media/security-center-get-started/prevention-policy.png
[5]: ./media/security-center-get-started/recommendations.png
[6]: ./media/security-center-get-started/resources-health.png
[7]: ./media/security-center-get-started/security-alert.png
[8]: ./media/security-center-get-started/security-alert-detail.png
[9]: ./media/security-center-get-started/partner-solutions.png
[10]: ./media/security-center-get-started/welcome.png
