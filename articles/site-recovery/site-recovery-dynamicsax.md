---
title: "Azure Site Recovery kullanarak çok katmanlı Dynamics AX dağıtım çoğaltmak | Microsoft Docs"
description: "Bu makalede, çoğaltma ve Azure Site RECOVERY'yi kullanarak Dynamics AX korumak açıklar"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: 03127c8f4841b67436c4819628319705af0b2cd5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>Azure Site RECOVERY'yi kullanarak çok katmanlı Dynamics AX uygulamayı çoğaltma

## <a name="overview"></a>Genel Bakış


Microsoft Dynamics AX standartlaştırılmış işleme kuruluşlar arasında en popüler ERP çözüm konumlar arasında biri, kaynakları ve uyumluluk basitleştirme yönetebilirsiniz. Kuruluş için kritik iş uygulamasıdır considering emin olması durumunda olması çok önemlidir herhangi olağanüstü durum uygulama hazır ve çalışır en az sürede olmalıdır.

Bugün, Microsoft Dynamics AX tüm giden kutusu olağanüstü durum kurtarma özellikleri sağlamaz. Microsoft Dynamics AX Uygulama Nesne Sunucusu, Active Directory (AD), SQL veritabanı sunucusu, SharePoint Server, Raporlama sunucusu vb. gibi pek çok sunucu bileşenden oluşur. Olağanüstü durum kurtarma işlemi bu bileşenlerin her birini el ile yalnızca pahalı, ancak aynı zamanda hataya yönetmektir.

Bu makalede, nasıl bir olağanüstü durum kurtarma çözümü Dynamics AX kullanarak uygulamanızı için oluşturabileceğiniz hakkında ayrıntılı olarak açıklanmaktadır [Azure Site Recovery](site-recovery-overview.md). Ayrıca, tek tıklatmayla kurtarma planı, desteklenen yapılandırmalar ve önkoşullar kullanarak planlanan/planlanmamış/yük devretme sınaması işlemlerini kapsar.
Azure Site Recovery dayalı olağanüstü durum kurtarma çözümü tam olarak test sertifikalı ve Microsoft Dynamics AX tarafından önerilir.



## <a name="prerequisites"></a>Ön koşullar

Azure Site Recovery kullanarak Dynamics AX uygulamasının olağanüstü durum kurtarma uygulama tamamlandı aşağıdaki önkoşulları gerektirir.

• Şirket içi Dynamics AX dağıtım ayarlanmış

• Azure Site kurtarma Hizmetleri kasası Microsoft Azure aboneliğinin oluşturuldu

• Azure kurtarma siteniz olduğunda çalıştırmak Azure sanal makine hazırlık Değerlendirme Aracı vm'lerde Azure Vm'leri ve Azure Site kurtarma Hizmetleri ile uyumlu olduklarından emin olun


## <a name="site-recovery-support"></a>Site kurtarma desteği

Bu makalede oluşturmak amacıyla, Windows Server 2012 R2 Enterprise üzerinde Dynamics AX 2012R3 VMware sanal makineleri kullanılmıştır. Site recovery çoğaltma uygulama belirsiz olduğundan, burada sağlanan öneriler de aşağıdaki senaryoları tutun beklenir.

### <a name="source-and-target"></a>Kaynak ve hedef

**Senaryo** | **İkincil bir siteye** | **Azure'a**
--- | --- | ---
**Hyper-V** | Evet | Evet
**VMware** | Evet | Evet
**Fiziksel sunucu** | Evet | Evet

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>Azure Site RECOVERY'yi kullanarak Dynamics AX DR uygulamayı etkinleştir
### <a name="protect-your-dynamics-ax-application"></a>Dynamics AX uygulamanızı koruma
Dynamics AX her bileşenin tam uygulama çoğaltma ve kurtarma etkinleştirmek için korunması gerekir. Bu bölümde ele alınmaktadır:

**1. Active Directory koruma**

**2. SQL katmanının koruma**

**3. Uygulamanın ve Web katmanları koruma**

**4. Ağ yapılandırması**

**5. Kurtarma planı**

### <a name="1-setup-ad-and-dns-replication"></a>1. Kurulum AD ve DNS çoğaltması

Active Directory DR sitesi Dynamics AX uygulama işlevi için gereklidir. Bir müşterinin şirket içi ortamına karmaşıklığı önerilen iki seçeneğiniz vardır.

**Seçenek 1**

Müşterinin az sayıda uygulamaları ve tek etki alanı denetleyicisi varsa, tüm site içi ve ikincil siteye (için geçerli DC makine çoğaltmak için ASR çoğaltma kullanmanızı öneririz sonra birlikte, tüm site başarısız Siteden siteye hem Azure siteye).

**Seçenek 2**

Müşteri uygulamalar çok sayıda sahip bir Active Directory ormanı çalıştıran ve yük birkaç uygulamalar aynı anda devretme durumunda DR sitesi ek etki alanı denetleyicisinde ayarlama öneririz (ikincil site veya Azure).

Lütfen [bir etki alanı denetleyicisi DR sitede kullanılabilir hale getirme üzerinde yardımcı kılavuz](site-recovery-active-directory.md). Bu belgenin geri kalanında için DC DR sitesinden edinilebilir varsayacağız.

### <a name="2-setup-sql-server-replication"></a>2. SQL Server çoğaltması Kurulumu
Koruma için önerilen seçeneğinde yardımcı kılavuz ayrıntılı teknik kılavuzu için lütfen [SQL katmanı](site-recovery-sql.md).

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3. Dynamics AX İstemcisi ve AOS VM'ler için korumayı etkinleştirin
Olup VM'ler dağıtılan üzerinde temel ilgili Azure Site Recovery yapılandırmasını gerçekleştirmek [Hyper-V](site-recovery-hyper-v-site-to-azure.md) veya [VMware](site-recovery-vmware-to-azure.md).

> [!TIP]
> Kilitlenme tutarlı sıklığı önerilen yapılandırmak için 15 dakikadır.
>

Anlık Görüntü 'Azure sitesine VMware' koruma senaryoda Dynamics bileşen Vm'leri koruma durumunu gösterir.
![Korumalı öğeler](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4. Ağı yapılandırma
VM yapılandırma işlem ve ağ ayarları

Böylece VM ağları, yük devretme sonrasında doğru DR ağa bağlı AX İstemcisi ve AOS VM'ler için Azure Site Recovery ağ ayarlarını yapılandırın. Bu katmanlar için DR ağ SQL katmanına yönlendirilebilir olduğundan emin olun.

VM anlık görüntüde gösterildiği gibi ağ ayarlarını yapılandırmak için çoğaltılan öğe seçebilirsiniz.

* AOS sunucuları doğru kullanılabilirlik kümesi seçin.

* Bir statik IP kullanarak yeniden yapılacağını sanal makine istediğiniz IP belirtin **hedef IP** alan ![ağ ayarları](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)



### <a name="5-creating-a-recovery-plan"></a>5. Bir kurtarma planı oluşturma

Bir kurtarma planı yük devretme işlemini otomatikleştirmek için Azure Site Recovery oluşturabilirsiniz. Uygulama katmanı ve web katmanı kurtarma planındaki ekleyin. Böylece uygulama önce ön uç kapatma katmanı bunları farklı gruplarda sıralayın.

1)  Azure Site Recovery kasası aboneliğinizde seçin ve 'Kurtarma planları' kutucuğuna tıklayın.

2)  Tıklayın ' + kurtarma planı ve bir ad belirtin.

3)  'Target' ve 'Source' seçin. Hedef Azure veya ikincil site olabilir. Azure seçtiğiniz durumunda dağıtım modelini belirtin

![Kurtarma planı oluşturun](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  İstemci sanal makineleri kurtarma planına ve AOS seçin ve ✓'ı tıklatın.
![Kurtarma planı oluşturun](./media/site-recovery-dynamics-ax/selectvms.png)


![Kurtarma planı](./media/site-recovery-dynamics-ax/recoveryplan.png)

Aşağıda açıklandığı gibi çeşitli adımları ekleyerek kurtarma planı Dynamics AX uygulama için özelleştirebilirsiniz. Yukarıdaki anlık tüm adımları ekledikten sonra tam kurtarma planı gösterir.

*Adımlar:*

*1. SQL Server üzerinde adımları başarısız*

Başvurmak ['SQL Server DR çözüm'](site-recovery-sql.md) kurtarma adımlarını belirli SQL Server hakkındaki ayrıntılar için yardımcı kılavuz.

*2. Yük devretme Grup 1: Yük devretme AOS VM'ler*

Seçilen kurtarma noktası PIT veritabanına mümkün olduğunca yakın ancak değil şimdi olduğundan emin olun.

*3. Komut dosyası: Ekle yük dengeleyici (yalnızca E-A)* Ekle bir yük dengeleyici eklemek için bir komut dosyası (aracılığıyla Azure Otomasyonu) AOS VM gruptan sonra gelir. Bu görevi gerçekleştirmek için bir komut dosyası kullanabilirsiniz. Makale başvuran [çok katmanlı uygulama DR için yük dengeleyici ekleme](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)

*4. Yük devretme Grup 2: AX İstemcisi VM'ler başarısız.*
Kurtarma planının bir parçası olarak VM'ler web katmanı yük devri.


### <a name="doing-a-test-failover"></a>Yük devretme sınamasını yapmak

'AD DR çözüm' ve 'SQL Server DR çözüm' yardımcı kılavuzlar için konuları belirli AD için bakın ve SQL server yük devretme testi sırasında sırasıyla.

1.  Azure Portalı'na gidin ve Site Recovery kasanızı seçin.
2.  Dynamics AX için oluşturduğunuz kurtarma planı tıklayın.
3.  'Test yük devretme üzerinde' tıklayın.
4.  Test yük devretme işlemini başlatmak için sanal ağ seçin.
5.  İkincil ortamı kurma olduğunda, doğrulama gerçekleştirebilirsiniz.
6.  Doğrulama tamamlandıktan sonra 'Doğrulamaları tamamlamak' seçin ve yük devretme sınama ortamı temizlendi.

İzleyin [bu kılavuz](site-recovery-test-failover-to-azure.md) yük devretme sınamasını yapmak için.

### <a name="doing-a-failover"></a>Bir yük devretme işleminden

1.  Azure Portalı'na gidin ve Site Recovery kasanızı seçin.
2.  Dynamics AX için oluşturduğunuz kurtarma planı tıklayın.
3.  'Üzerinde yük devretme' tıklatın ve 'Failover' seçin.
4.  Hedef ağ seçin ve yük devretme işlemini başlatmak için ✓ tıklayın.

İzleyin [bu kılavuz](site-recovery-failover.md) , yaparken bir yük devretme.

### <a name="perform-a-failback"></a>Bir yeniden çalışma gerçekleştirme

'SQL Server DR çözüm' yardımcı Kılavuzu SQL Server'a özel konular için yeniden çalışma sırasında bakın.

1.  Azure Portalı'na gidin ve Site Recovery kasanızı seçin.
2.  Dynamics AX için oluşturduğunuz kurtarma planı tıklayın.
3.  'Üzerinde yük devretme' tıklayın ve yük devretme seçin.
4.  'Üzerinde değişiklik yön' seçeneğini tıklatın.
5.  -Veri eşitleme ve VM oluşturma seçenekleri uygun seçenekleri seçin
6.  ✓ 'Yeniden çalışma' işlemini başlatmak için tıklatın.


İzleyin [bu kılavuz](site-recovery-failback-azure-to-vmware.md) , yaparken bir yeniden çalışma.

##<a name="summary"></a>Özet
Azure Site Recovery kullanarak, Dynamics AX uygulamanız için bir tam otomatik olağanüstü durum kurtarma planı oluşturabilirsiniz. Her yerden saniye içinde yük devretmeyi başlatın durumunda kesintisi ve get uygulama dakika içinde çalışır.

## <a name="next-steps"></a>Sonraki adımlar
Okuma [hangi iş yüklerini koruyabilirim?](site-recovery-workload.md) Azure Site Recovery ile kurumsal iş yüklerini koruma hakkında daha fazla bilgi edinmek için.
