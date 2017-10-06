---
title: "aaaAzure Danışmanı yüksek kullanılabilirlik önerileri | Microsoft Docs"
description: "Azure Danışmanı tooimprove yüksek kullanılabilirliğini Azure dağıtımlarınızı kullanın."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 3ac75ce401271f0212d198d7a7dc75ab702b6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-high-availability-recommendations"></a>Advisor yüksek kullanılabilirlik önerileri

Azure Danışmanı emin olun ve iş açısından kritik uygulamalar hello sürekliliği artırmanıza yardımcı olur. Hello Danışmanı göre yüksek kullanılabilirlik öneriler alabilirsiniz **yüksek kullanılabilirlik** hello Danışmanı Pano sekmesi.

![Merhaba Danışmanı Panoda yüksek kullanılabilirlik düğmesi](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a>Sanal makine hataya dayanıklılık sağlamak

Advisor bir kullanılabilirlik kümesi ve bir kullanılabilirlik kümesine taşıma önerir parçası olmayan sanal makineleri tanımlar. Artıklık tooyour uygulama sağlamak için bir kullanılabilirlik kümesinde iki veya daha fazla sanal makineyi gruplandırmanız önerilir. Bu yapılandırma ya da bir planlı veya plansız bir bakım olayı sırasında en az bir sanal makine kullanılabilir ve Azure sanal makinesi SLA karşılıyor hello sağlar. Merhaba sanal makine ya da tooadd hello sanal makine tooan varolan kullanılabilirlik kümesi için bir kullanılabilirlik ya da toocreate seçebilirsiniz.

> [!NOTE]
> Bir kullanılabilirlik toocreate seçerseniz ayarla, en az bir daha fazla sanal makine içine eklemeniz gerekir. İki grup veya tooensure daha fazla sanal makine bir kullanılabilirlik kümesi öneririz en az bir makine kesinti sırasında kullanılabilir.

![Advisor öneri: sanal makine artıklık için kullanılabilirlik kümelerini kullanın](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a>Hataya dayanıklılık kullanılabilirlik kümesi emin olun 

Advisor tek bir sanal makine içeren kullanılabilirlik kümeleri tanımlar ve bir veya daha fazla sanal makine tooit ekleme önerir. Artıklık tooyour uygulama sağlamak için bir kullanılabilirlik kümesinde iki veya daha fazla sanal makineyi gruplandırmanız önerilir. Bu yapılandırma ya da bir planlı veya plansız bir bakım olayı sırasında en az bir sanal makine kullanılabilir ve Azure sanal makinesi SLA karşılıyor hello sağlar. Bir sanal makine veya toouse var olan bir sanal makine ve tooadd ya da toocreate seçebilirsiniz, toohello kullanılabilirlik kümesi.  

![Advisor öneri: bir veya daha fazla sanal makineleri toothis kullanılabilirlik kümesi Ekle](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a>Uygulama ağ geçidi hataya dayanıklılık sağlamak
Uygulama ağ geçidi tarafından desteklenen kritik uygulamaların tooensure hello iş sürekliliği, Advisor hataya dayanıklılık için yapılandırılmamış uygulama ağ geçidi örnekleri tanımlar ve yapabileceğiniz düzeltme eylemleri önerir . Orta veya büyük tek örnekli uygulama ağ geçitleri Danışmanı tanımlar ve en az bir daha fazla örneğini eklemede önerir. Ayrıca, tek veya birden çok instance küçük uygulama ağ geçitleri tanımlar ve geçirme toomedium veya büyük SKU'ları önerir. Advisor, uygulama ağ geçidi örnekleri yapılandırılmış toosatisfy hello bu kaynaklar için geçerli SLA gereksinimleri olan bu eylemleri tooensure önerir.

![Advisor öneri: iki veya daha fazla Orta veya büyük boyutlu uygulama ağ geçidi örnekleri dağıtma](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-hello-performance-and-reliability-of-virtual-machine-disks"></a>Merhaba performans ve sanal makine disklerini güvenilirliğini artırmak

Advisor standart diskler ile sanal makineleri tanımlar ve toopremium diskleri yükseltme önerir.
 
Azure Premium depolama g/Ç kullanımı yoğun iş yükleri çalıştıran sanal makineler için yüksek performanslı, düşük gecikmeli disk desteği sunar. Premium depolama hesapları kullanan sanal makine diskler katı hal sürücüleri (SSD) verileri depolar. Merhaba en iyi performans için uygulamanız için yüksek IOPS toopremium depolama gerektiren herhangi bir sanal makine disklerini geçirmek öneririz. 

Disklerinizi yüksek IOPS ihtiyacınız yoksa, standart depolama tutarak maliyetleri sınırlayabilirsiniz. Standart depolama SSD yerine sabit disk sürücülerinin (HDD'ler) üzerinde sanal makine disk verilerini depolar. Sanal makine disklerini toopremium disklerinizi toomigrate seçebilirsiniz. Premium diskleri çoğu sanal makine SKU'ları üzerinde desteklenir. Toouse premium diskler, isterseniz, ancak bazı durumlarda, tooupgrade, sanal makinenize SKU'ları da gerekebilir.

![Advisor öneri: toopremium diskleri yükselterek, sanal makine diskleriniz hello güvenilirliğini geliştirmeye](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a>Sanal makine verilerinizi yanlışlıkla silinmeye karşı koru
Advisor burada yedekleme etkin değil ve yedekleme etkinleştirme önerir sanal makineleri tanımlar. Sanal makine yedekleme ayarı Merhaba, iş açısından kritik verilerin kullanılabilirliğini sağlar ve yanlışlıkla silme veya bozulmasına karşı koruma sağlar.

![Advisor öneri: sanal makine yedekleme tooprotect kritik verilerinizi yapılandırın](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a>Advisor erişim yüksek kullanılabilirlik önerileri

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. Merhaba sol bölmede **daha fazla hizmet**.

3. Hello menü bölmesi altında hizmet **izleme ve Yönetim**, tıklatın **Azure Danışmanı**.  
 Merhaba Danışmanı Panosu görüntülenir.

4. Hello Danışmanı Panoda hello tıklatın **yüksek kullanılabilirlik** sekmesini tıklatın ve ardından tooreceive önerileri istediğiniz hello aboneliği seçin.

> [!NOTE]
> tooaccess Advisor önerileri, şunları yapmalısınız ilk *aboneliğinizi kaydetmek* Danışmanı ile. Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* başlatır hello Danışmanı Pano ve tıklama hello **alma önerileri** düğmesi. Bu bir *tek seferlik işlem*. Merhaba abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* abonelik, bir kaynak grubu için veya bir belirli kaynak.

## <a name="next-steps"></a>Sonraki adımlar

Advisor önerileri hakkında daha fazla bilgi için bkz:
* [Giriş tooAzure Danışmanı](advisor-overview.md)
* [Danışman’ı kullanmaya başlama](advisor-get-started.md)
* [Advisor maliyet önerileri](advisor-performance-recommendations.md)
* [Advisor performans önerileri](advisor-performance-recommendations.md)
* [Advisor güvenlik önerileri](advisor-security-recommendations.md)

