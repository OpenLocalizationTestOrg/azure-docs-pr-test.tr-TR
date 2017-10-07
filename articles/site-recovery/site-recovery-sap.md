---
title: "aaaProtect Azure Site Recovery kullanarak çok katmanlı SAP NetWeaver uygulama dağıtımı | Microsoft Docs"
description: "Nasıl tooprotect SAP bu makalede Azure Site Recovery kullanarak NetWeaver uygulama dağıtımları"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 34651c7b14d23a44005372f4f923c401e0224231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a>Azure Site Recovery kullanarak çok katmanlı SAP NetWeaver uygulama dağıtımı koruma

En büyük ve orta ölçekli SAP dağıtımları bazı olağanüstü durum kurtarma çözümü sahiptir.  tooapplications SAP gibi işlemler daha fazla çekirdek iş taşındı sağlam ve sınanabilir olağanüstü durum kurtarma çözümleri hello önemini artar.  Azure Site Recovery test edilmiş ve tümleşik SAP uygulamaları olmuştur ve daha düşük maliyetle toplam sahip olma maliyetini (TCO) rakip çözümleri daha çoğu şirket içi olağanüstü durum kurtarma çözümleri hello yeteneklerini aşıyor.
Azure Site Recovery ile şunları yapabilirsiniz:
* Şirket içi bileşenleri tooAzure yineleyerek çalışan SAP NetWeaver ve NetWeaver üretim dışı uygulamalarının korumasını etkinleştirin.
* Bileşenleri tooanother Azure veri merkezi yineleyerek Azure, çalışan SAP NetWeaver ve NetWeaver üretim dışı uygulamalarının korumasını etkinleştirin.
* Buluta geçiş, Site Recovery toomigrate kullanarak SAP dağıtım tooAzure basitleştirin.
* SAP uygulamaları test etmek için talep üzerine üretim kopyası oluşturarak SAP proje yükseltmelerini, testlerini ve prototip oluşturma işlemlerini basitleştirin.

Nasıl tooprotect SAP bu makalede kullanarak NetWeaver uygulama dağıtımları [Azure Site Recovery](site-recovery-overview.md). Bu makalede Azure ile ilgili üç katmanlı SAP NetWeaver dağıtım tooanother Azure Site Recovery, desteklenen hello senaryoları ve yapılandırmaları kullanarak Azure veri merkezi yineleyerek korumak için en iyi yöntemler hello yer almaktadır ve nasıl tooperform test yük devretmeleri, her ikisi Yük devretme (olağanüstü durum kurtarma ayrıntılarını) ve gerçek yük devretmeleri.


## <a name="prerequisites"></a>Ön koşullar
Başlamadan önce hello aşağıdaki anladığınızdan emin olun:

1. [Bir sanal makine tooAzure çoğaltma](azure-to-azure-walkthrough-enable-replication.md)
2. Nasıl çok[kurtarma ağını tasarlama](site-recovery-azure-to-azure-networking-guidance.md)
3. [Bir test yük devretme tooAzure yapılması](azure-to-azure-walkthrough-test-failover.md)
4. [Bir yük devretme tooAzure yapılması](site-recovery-failover.md)
5. Nasıl çok[bir etki alanı denetleyicisi çoğaltma](site-recovery-active-directory.md)
6. Nasıl çok[SQL Server çoğaltma](site-recovery-sql.md)

## <a name="supported-scenarios"></a>Desteklenen senaryolar
Azure Site Recovery ile senaryoları aşağıdaki hello için bir olağanüstü durum kurtarma çözümü uygulayabilirsiniz:
* SAP sistemleri tasarlanmış olarak tooanother Azure veri merkezi (Azure Azure DR), çoğaltılması bir Azure veri merkezinde çalışan [burada](https://aka.ms/asr-a2a-architecture).
* SAP sistemleri VMWare (veya fiziksel) sunucuları üzerinde çalışan şirket içi çoğaltma tooa DR sitesi tasarlanmış gibi bazı ek bileşenleri gerektiren bir Azure veri merkezinde (VMware Azure DR) [burada](https://aka.ms/asr-v2a-architecture).
* SAP sistemleri üzerinde Hyper-V çalıştıran şirket içi çoğaltma tooa DR sitesi tasarlanmış gibi bazı ek bileşenleri gerektiren bir Azure veri merkezinde (Hyper-V-Azure'a DR) [burada](https://aka.ms/asr-h2a-architecture).

Bu belge hello ilk örneği - Azure Azure DR - toodemonstrate Azure Site Recovery'nin SAP olağanüstü durum kurtarma yeteneklerini kullanır. Azure Site Recovery çoğaltma uygulama belirsiz olduğundan açıklanan hello de diğer senaryolar için beklenen toohold işlemidir.

### <a name="required-foundation-services"></a>Gerekli foundation Hizmetleri
Tüm bu belgeleri senaryo edilmiş dağıtılan foundation Hizmetleri aşağıdaki hello ile dağıtılır:
* ExpressRoute veya siteden siteye sanal özel ağ (VPN)
* Azure'da çalışan en az bir Active Directory etki alanı denetleyicisi ve DNS sunucusu

Bu hello yukarıdaki kurulan önceki toodeploying Azure Site Recovery altyapısıdır önerilir.


## <a name="typical-sap-application-deployment"></a>Tipik SAP uygulama dağıtımı
Büyük SAP müşteriler genellikle 6 too20 tek tek SAP uygulamalar arasında dağıtın.  Bu uygulamaların çoğu hello SAP NetWeaver ABAP veya Java motorlarına dayanır.  Bu çekirdek NetWeaver uygulamaları destekleyen pek çok daha küçük belirli NetWeaver SAP olmayan tek başına motorları ve genellikle bazı SAP olmayan uygulamalar şunlardır.  

Çalışan bir yatay ve toodetermine hello dağıtım modunu (Katman 2 veya 3 katmanlı), sürüm, düzeltme ekleri tüm hello SAP uygulamaları boyutları, karmaşıklığı hızları ve disk Kalıcılık gereksinimleri kritik tooinventory olur.

![Dağıtım modeli](./media/site-recovery-sap/sap-typical-deployment.png)

SQL Server AlwaysOn, Oracle DataGuard veya HANA sistem çoğaltma gibi hello yerel DBMS araçları aracılığıyla Hello SAP veritabanı saklama katmanını korunmalıdır. Merhaba istemci katmanı da Azure Site Recovery tarafından korumalı olmayan, ancak bu katman DNS yayılma gecikmesi, güvenlik ve Uzaktan erişim toohello DR datacenter gibi etkileyen önemli tooconsider konuları değil.

Azure Site kurtarma çözümü hello uygulama katman (A) SCS dahil olmak üzere, önerilen hello ' dir. NetWeaver SAP uygulamaları ve SAP olmayan uygulamaları hello parçasını gibi diğer uygulamaları genel dağıtım ortamı SAP ve ayrıca Azure Site Recovery ile korunması.

## <a name="replicate-virtual-machines"></a>Çoğaltma sanal makineler
İzleyin [bu kılavuz](azure-to-azure-walkthrough-enable-replication.md) tüm çoğaltma toostart hello SAP uygulama sanal makineleri toohello Azure DR veri merkezi.

Bir statik IP kullanıyorsanız, sanal makine tootake hello ağ arabirimi kartları işlem ve ağ ayarları bölümünde hello istediğiniz hello IP belirtebilirsiniz.

![Hedef IP](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a>Bir kurtarma planı oluşturma
Bir kurtarma planı çeşitli katmanlarda çok katmanlı bir uygulama, bu nedenle, uygulama tutarlılığını sağlamak hello yük devretme sıralama sağlar. Açıklanan başlangıç adımları [burada](site-recovery-create-recovery-plans.md) çok katmanlı web uygulaması için bir kurtarma planı oluşturma sırasında.

### <a name="adding-scripts-toohello-recovery-plan"></a>Toohello kurtarma planı komutlar ekleme
Toodo hello Azure sanal makineleri post yük devretme ve test yük devretme üzerindeki bazı işlemler için uygulamaları toofunction doğru gerekebilir. DNS girişi güncelleştirme ve açıklandığı gibi hello kurtarma planında betikleri ekleyerek bağlamalar ve bağlantıları değiştirme gibi hello post yük devretme işlemi otomatikleştirebilirsiniz [bu makalede](site-recovery-create-recovery-plans.md#add-scripts).

### <a name="dns-update"></a>DNS güncelleştirme
Merhaba DNS genellikle dinamik DNS güncelleştirmeleri ve ardından sanal makineleri için yapılandırılmışsa, başladıktan sonra hello DNS hello yeni IP ile güncelleştirin. Tooadd hello ile açık adım tooupdate DNS yeni istiyorsanız hello sanal makinelerin IP sonra eklemek bu [tooupdate IP DNS'de komut dosyası](https://aka.ms/asr-dns-update) kurtarma planı grupları sonrası eylemi olarak.  

## <a name="example-azure-to-azure-deployment"></a>Örnek Azure Azure dağıtımı
Merhaba diyagramında hello Azure Site Recovery Azure Azure DR senaryo aşağıda belirtilmiştir:
* hello birincil veri merkezi Singapur (Azure Güney-Doğu Asya) olduğu ve hello DR datacenter, Hong Kong (Azure Doğu Asya) olur.  Bu senaryoda, SQL Server AlwaysOn Singapur zaman uyumlu modda çalışan iki VM sağlayarak yerel yüksek kullanılabilirlik sağlanır.
* Merhaba dosya paylaşımı ASCS hello SAP tekli hata noktaları için kullanılan tooprovide HA olabilir. Dosya Paylaşımı ASCS bir küme paylaşılan disk gerektirmez ve SIOS gibi uygulamalar gerekli değildir.
* Merhaba DBMS katmanı için DR koruma zaman uyumsuz çoğaltma kullanılarak gerçekleştirilir.
* Bu senaryoda kullanılan bir terim toodescribe üretim tam bir kopyasını bir DR Çözüm "simetrik DR" – gösterir, bu nedenle hello DR SQL Server çözümünü yerel yüksek kullanılabilirliğe sahip. simetrik DR Hello kullanımı hello veritabanı katmanı için zorunlu değildir ve birçok müşteri bulut dağıtımları toobuild bir yerel yüksek kullanılabilirlik düğümü hello esnekliğini DR olayından sonra hızlı bir şekilde yararlanın.
* Merhaba diyagramı hello SAP NetWeaver ASCS ve uygulama sunucusu katmanı Azure Site Recovery tarafından çoğaltılan gösterilmektedir.

![Çoğaltma senaryosu](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a>Yük devretme sınamasını yapmak
İzleyin [bu kılavuz](azure-to-azure-walkthrough-test-failover.md) toodo yük devretme sınaması.

1.  TooAzure portal gidin ve kurtarma Hizmetleri kasanız seçin.
2.  SAP uygulamaları (s) için oluşturulan hello kurtarma planı tıklayın.
3.  'Test yük devretme üzerinde' tıklayın.
4.  Kurtarma noktası ve Azure sanal ağı toostart hello test yük devretme işlemi seçin.
5.  Merhaba ikincil ortamı kurma olduğunda, doğrulama gerçekleştirebilirsiniz.
6.  Merhaba doğrulama tamamlandıktan sonra tıklayın 'Temizleme test yük devretme' ve tooclean hello yük devretme ortamı.

## <a name="doing-a-failover"></a>Bir yük devretme işleminden
İzleyin [bu kılavuz](site-recovery-failover.md) , yaparken bir yük devretme.

1.  TooAzure portal gidin ve kurtarma Hizmetleri kasanız seçin.
2.  SAP uygulamaları için oluşturulan hello kurtarma planı tıklayın.
3.  'Failover' üzerinde'ı tıklatın.
4.  Kurtarma noktası toostart hello yük devretme işlemini seçin.

## <a name="next-steps"></a>Sonraki adımlar
Azure Site RECOVERY'yi kullanarak SAP NetWeaver dağıtımları için bir olağanüstü durum kurtarma çözümü oluşturma hakkında daha fazla bilgi [Bu teknik](http://aka.ms/asr-sap). Merhaba Teknik İnceleme de farklı SAP mimari için öneriler açıklanır, Azure üzerinde SAP için desteklenen uygulamalar ve VM türlerini listeler ve olası test planları, olağanüstü durum kurtarma çözümünüzün anlatılır.

Daha fazla bilgi edinmek [diğer iş yüklerini çoğaltma](site-recovery-workload.md) Site RECOVERY'yi kullanarak.
