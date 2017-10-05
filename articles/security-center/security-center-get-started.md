---
title: "Azure Güvenlik Merkezi Hızlı Başlangıç Kılavuzu | Microsoft Docs"
description: "Bu makale, güvenlik izleme ve ilke yönetimi bileşenleri hakkında size rehberlik ederek ve sonraki adımlara yönlendirerek Azure Güvenlik Merkezi ile hızlıca çalışmaya başlamanıza yardımcı olur."
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
ms.openlocfilehash: 392c814b7d3ff6b4f0f7850a51960576775e0307
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-quick-start-guide"></a>Azure Güvenlik Merkezi hızlı başlangıç kılavuzu
Bu makale, Güvenlik Merkezi’nin güvenlik izleme ve ilke yönetimi bileşenleri hakkında size rehberlik ederek Azure Güvenlik Merkezi ile hızlıca çalışmaya başlamanıza yardımcı olur.

> [!NOTE]
> Haziran 2017'nin ilk günlerinden itibaren Güvenlik Merkezi, veri toplamak ve depolamak için Microsoft Monitoring Agent'ı kullanacak. Daha fazla bilgi edinmek için [Azure Güvenlik Merkezi Platform Geçişi](security-center-platform-migration.md) makalesine bakın. Bu makaledeki bilgiler, Microsoft Monitoring Agent'a geçiş sonrasındaki Güvenlik Merkezi işlevselliğine yöneliktir.
>
>

## <a name="prerequisites"></a>Ön koşullar
Güvenlik Merkezi ile çalışmaya başlamak için Microsoft Azure aboneliğinizin olması gerekir. Bir aboneliğiniz yoksa [ücretsiz hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.

Güvenlik Merkezi’nin Ücretsiz katmanı, aboneliğinizle birlikte otomatik olarak etkinleştirilir ve Azure kaynaklarınızın güvenlik durumunu gösterir. Bu katman temel güvenlik ilkesi yönetimi, güvenlik önerileri ve Azure iş ortaklarının güvenlik ürün ve hizmetleri ile tümleştirme sağlar.

Güvenlik Merkezi'ne [Azure portalından](https://azure.microsoft.com/features/azure-portal/) erişebilirsiniz. Azure portalı hakkında daha fazla bilgi için bkz. [portal belgeleri](https://azure.microsoft.com/documentation/services/azure-portal/).

## <a name="permissions"></a>İzinler
Güvenlik Merkezi'nde, yalnızca bir Azure kaynağı sahibi, katkıda bulunan veya okuyucu rolü abonelik veya kaynak ait olduğu kaynak grubu için atandığında ilgili bilgiler görürsünüz. Bkz: [izinleri Azure Güvenlik Merkezi'nde](security-center-permissions.md) rolleri ve Güvenlik Merkezi'nde izin verilen eylemleri hakkında daha fazla bilgi için.

## <a name="data-collection"></a>Veri toplama
Güvenlik Merkezi, verilerinizin güvenlik durumunu değerlendirmek, güvenlik önerileri sağlamak ve sizi tehditlere karşı uyarmak için sanal makinelerinizden (VM) veri toplar. Güvenlik Merkezi’ne ilk kez eriştiğinizde aboneliğinizdeki tüm sanal makinelerde veri toplama etkindir. Güvenlik Merkezi hükümleri tüm mevcut Microsoft İzleme Aracısı, Azure Vm'leri ve oluşturulan yeni bir tane desteklenir. Bkz: [veri koleksiyonunu etkinleştir](security-center-enable-data-collection.md) veri toplama nasıl çalıştığı hakkında daha fazla bilgi için.

Veri toplama önerilir. Güvenlik Merkezi, ücretsiz katmanı kullanıyorsanız, Güvenlik İlkesi'nde veri toplamayı devre dışı bırakarak VM'ler veri koleksiyonunu devre dışı bırakabilirsiniz. Veri koleksiyonu Güvenlik Merkezi'nin standart katmanında abonelikler için gereklidir. Bkz: [Güvenlik Merkezi fiyatlandırma](security-center-pricing.md) ücretsiz ve standart katmanları fiyatlandırma hakkında daha fazla bilgi edinmek için.

Aşağıdaki adımlar Güvenlik Merkezi’ne erişme ve bileşenlerini kullanma hakkında bilgi vermektedir. Bu adımlarda veri toplamayı kullanmak istememeniz halinde özeliği nasıl kapatacağınız gösterilmektedir.

> [!NOTE]
> Bu makale örnek bir dağıtım kullanarak hizmeti tanıtır. Bu makale adım adım ilerleyen bir kılavuz değildir.
>
>

## <a name="access-security-center"></a>Güvenlik Merkezi'ne erişme
Güvenlik Merkezi'ne erişmek için portalda şu adımları izleyin:

1. **Microsoft Azure** menüsünde **Güvenlik Merkezi**’ni seçin.

   ![Azure menüsü][1]
2. Güvenlik Merkezi’ne ilk kez erişiyorsanız **Hoş Geldiniz** dikey penceresi açılır. Seçin **başlatma Güvenlik Merkezi** açmak için **Güvenlik Merkezi** dikey ve veri toplamayı etkinleştirmek için.
   ![Hoş Geldiniz ekranı][10]
3. Hoş Geldiniz dikey penceresinden Güvenlik Merkezi’ni başlattıktan veya Microsoft Azure menüsünden Güvenlik Merkezi’ni seçtikten sonra **Güvenlik Merkezi** dikey penceresi açılır. Gelecekte **Güvenlik Merkezi** dikey penceresine kolay erişim için **Panoya dikey pencereyi sabitleme** seçeneğini (sağ üstte) seçin.
   ![Dikey pencereyi panoya sabitleme seçeneği][2]

## <a name="use-security-center"></a>Güvenlik Merkezi'ni Kullanma
Azure abonelikleriniz ve kaynak grupları için güvenlik ilkelerini yapılandırabilirsiniz. Aboneliğiniz için bir güvenlik ilkesi yapılandıralım:

1. **Güvenlik Merkezi** dikey penceresinde **İlke** kutucuğunu seçin.
2. Üzerinde **güvenlik ilkesi - abonelik başına ilkesi tanımlama** dikey penceresinde bir abonelik seçin.
3. Günlükleri otomatik olarak toplamak için **Güvenlik ilkesi** dikey penceresinde **Veri toplama** seçeneğini otomatik olarak etkinleştirilir. İzleme uzantısı, abonelikteki tüm mevcut ve yeni sanal makinelerde sağlanır. (Güvenlik Merkezi ücretsiz katmanında ayarlayarak veri toplama dışında seçebilirsiniz **veri toplama** için **devre dışı**. Ayarı **veri toplama** için **kapalı** Güvenlik Merkezi, güvenlik uyarısı ve öneri vermelerini önler.)
4. **Güvenlik İlkesi** dikey penceresinde **Önleme ilkesi**’ni seçin. Bu işlem **Önleme ilkesi** dikey penceresini açar.
5. **Önleme ilkesi** dikey penceresinde güvenlik ilkenizin bir parçası olarak görmek istediğiniz önerileri açın. Örnekler:

   * Ayarı **sistem güncelleştirmeleri** için **üzerinde** taramaları tüm işletim sistemi güncelleştirmeleri eksik VM'ler desteklenir.
   * Ayarı **işletim sistemi güvenlik açıkları** için **üzerinde** taramaları tüm desteklenen VM saldırı karşısında daha savunmasız hale işletim sistemi yapılandırmasını tanımlamak için VM'ler.

### <a name="view-recommendations"></a>Önerileri görüntüleme
1. **Güvenlik Merkezi** dikey penceresine geri dönüp **Öneriler** kutucuğunu seçin. Güvenlik Merkezi düzenli aralıklarla Azure kaynaklarınızın güvenlik durumunu çözümler. Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde **Öneriler** dikey penceresinde öneriler gösterir.
   ![Azure Güvenlik Merkezi'nde öneriler][5]
2. Daha fazla bilgi görüntülemek ve/veya sorunu çözmeye yönelik işlemler yapmak için **Öneriler** dikey penceresinde bir öneri seçin.

### <a name="view-the-security-state-of-your-resources"></a>Kaynaklarınızın güvenlik durumunu görüntüleyin
1. **Güvenlik Merkezi** dikey penceresine geri dönün. **Önleme** bölümü, ağ, veri ve uygulamaları VM'ler için güvenlik durumu göstergelerini içerir.
2. Seçin **işlem** daha fazla bilgi görüntülemek için. **İşlem** gösteren üç sekme dikey pencere açılır:

  - **Genel Bakış** -izleme içerir ve VM öneriler.
  - **Sanal makineler** -tüm sanal makineleri ve geçerli güvenlik listeler durumları.
  - **Bulut Hizmetleri** -Güvenlik Merkezi tarafından izlenen web ve çalışan rolleri listeler.

    ![Azure Güvenlik Merkezi'nde kaynak durumu kutucuğu][6]

3. Üzerinde **genel bakış** sekmesinde, bir önerinin altında seçin **sanal makine önerileri** daha fazla bilgi görüntülemek ve/veya gerekli denetimleri yapılandırmak amacıyla eyleme geçmek için.
4. Üzerinde **sanal makineleri** sekmesinde, ek ayrıntıları görüntülemek için bir VM seçin.

### <a name="view-security-alerts"></a>Güvenlik uyarılarını görüntüleme
1. **Güvenlik Merkezi** dikey penceresine geri dönüp **Güvenlik Uyarıları** kutucuğunu seçin. **Güvenlik uyarıları** dikey penceresi açılır ve uyarıların bir listesini gösterir. Güvenlik günlüklerinize ve ağ etkinliğinize ilişkin Güvenlik Merkezi çözümlemesi bu uyarıları oluşturur. Tümleşik iş ortağı çözümlerinden gelen uyarılar buna dahildir.
   ![Azure Güvenlik Merkezi'ndeki güvenlik uyarıları][7]

   > [!NOTE]
   > Güvenlik uyarıları yalnızca Güvenlik Merkezi Standart katmanı etkin olduğunda kullanılabilir. Standart katmanı, 60 günlük ücretsiz bir deneme kullanılabilir. Standart katmanı edinme hakkında bilgi için [Sonraki adımlara](#next-steps) bakın.
   >
   >
2. Ek bilgileri görüntülemek için bir uyarı seçin. Bu örnekte **Değiştirilen sistem ikili dosyası bulundu** seçeneğini kullanalım. Bunun yapılması uyarı hakkında ek bilgiler sağlayan dikey pencereler açar.
   ![Azure Güvenlik Merkezi'nde güvenlik uyarısı ayrıntıları][8]

### <a name="view-the-health-of-your-partner-solutions"></a>İş ortağı çözümlerinizin sistem durumunu görüntüleme
1. **Güvenlik Merkezi** dikey penceresine geri dönün. **İş ortağı çözümleri** kutucuğu, Azure aboneliğinizle tümleşik iş ortağı çözümlerinizin sistem durumunu bir bakışta izlemenizi sağlar.
2. **İş ortağı çözümleri** kutucuğunu seçin. Güvenlik Merkezi'ne bağlı iş ortağı çözümlerinizin listesini görüntüleyen dikey pencere açılır.
   ![İş ortağı çözümleri][9]
3. İş ortağı çözümü seçin. Bu örnekte, şimdi seçin **QualysVa1** çözümü.  İş ortağı çözümünün durumunu ve çözümle ilişkili kaynakları gösteren dikey pencere açılır. Bu çözüme ilişkin iş ortağı yönetimi deneyimini açmak için **Çözüm konsolunu** seçin.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede Güvenlik Merkezi'nin güvenlik izleme ve ilke yönetimi bileşenleri hakkında bilgi edindiniz. Güvenlik Merkezi hakkında bilgi sahibi olduğunuza göre aşağıdaki adımları deneyebilirsiniz:

* Azure aboneliğiniz için bir güvenlik ilkesi yapılandırın. Daha fazla bilgi için bkz. [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md).
* Azure kaynaklarınızı korumaya yardımcı olması için Güvenlik Merkezi’ndeki önerileri kullanın. Daha fazla bilgi için bkz. [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md).
* Geçerli güvenlik uyarılarınızı gözden geçirin ve yönetin. Daha fazla bilgi için bkz. [Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md).
- [Azure Güvenlik Merkezi veri güvenliği](security-center-data-security.md) -verilerin yönetilmesi ve diğer Güvenlik Merkezi'nde korunması nasıl öğrenin.
* Güvenlik Merkezi’nin [Standart katmanı](security-center-pricing.md) ile birlikte sunulan [gelişmiş tehdit algılama özellikleri](security-center-detection-capabilities.md) hakkında daha fazla bilgi edinin. Standart katman ilk 60 gün boyunca ücretsizdir.
* Güvenlik Merkezi’ni kullanma hakkında sorularınız varsa bkz. [Azure Güvenlik Merkezi SSS](security-center-faq.md).

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
