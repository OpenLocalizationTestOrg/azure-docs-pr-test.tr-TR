---
title: "Azure Site Recovery kullanarak çok katmanlı Dynamics AX dağıtım aaaReplicate | Microsoft Docs"
description: "Bu makalede nasıl tooreplicate ve Azure Site RECOVERY'yi kullanarak Dynamics AX koruyun"
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
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>Azure Site RECOVERY'yi kullanarak çok katmanlı Dynamics AX uygulamayı çoğaltma

## <a name="overview"></a>Genel Bakış


Microsoft Dynamics AX hello en popüler ERP çözüm kuruluşların toostandardized işlem arasında konumlar arasında biri, kaynakları ve uyumluluk basitleştirme yönetebilirsiniz. İş kritik tooan kuruluş Hello uygulamasıdır considering çok önemli toobe emin olup, bir olağanüstü durum uygulama hazır ve çalışır en az sürede olup olmayacağını.

Bugün, Microsoft Dynamics AX tüm giden kutusu olağanüstü durum kurtarma özellikleri sağlamaz. Microsoft Dynamics AX oluşur uygulama nesne sunucusu, Active Directory (AD), SQL veritabanı sunucusu, SharePoint Server gibi birçok sunucu bileşenlerinin, Raporlama sunucusu vb. toomanage hello olağanüstü durum kurtarma, bu bileşenlerin her birini el ile yalnızca Ayrıca hataya ancak pahalı.

Bu makalede, nasıl bir olağanüstü durum kurtarma çözümü Dynamics AX kullanarak uygulamanızı için oluşturabileceğiniz hakkında ayrıntılı olarak açıklanmaktadır [Azure Site Recovery](site-recovery-overview.md). Ayrıca, tek tıklatmayla kurtarma planı, desteklenen yapılandırmalar ve önkoşullar kullanarak planlanan/planlanmamış/yük devretme sınaması işlemlerini kapsar.
Azure Site Recovery dayalı olağanüstü durum kurtarma çözümü tam olarak test sertifikalı ve Microsoft Dynamics AX tarafından önerilir.



## <a name="prerequisites"></a>Ön koşullar

Azure Site Recovery kullanarak Dynamics AX uygulamasının olağanüstü durum kurtarma uygulama tamamlandı ön koşullar aşağıdaki hello gerektirir.

• Şirket içi Dynamics AX dağıtım ayarlanmış

• Azure Site kurtarma Hizmetleri kasası Microsoft Azure aboneliğinin oluşturuldu

• Azure kurtarma siteniz olduğunda çalıştırmak hello Azure sanal makine hazırlık değerlendirme aracı üzerinde sanal makineleri tooensure Azure Vm'leri ve Azure Site kurtarma Hizmetleri ile uyumlu olan


## <a name="site-recovery-support"></a>Site kurtarma desteği

Bu makalede oluşturma hello amaç için VMware sanal makineleri üzerinde Windows Server 2012 R2 Enterprise Dynamics AX 2012R3 kullanılmıştır. Site recovery çoğaltma uygulama belirsiz olduğu gibi hello önerileri burada beklenen toohold de aşağıdaki senaryoları sağlanır.

### <a name="source-and-target"></a>Kaynak ve hedef

**Senaryo** | **tooa ikincil site** | **tooAzure**
--- | --- | ---
**Hyper-V** | Evet | Evet
**VMware** | Evet | Evet
**Fiziksel sunucu** | Evet | Evet

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>Azure Site RECOVERY'yi kullanarak Dynamics AX DR uygulamayı etkinleştir
### <a name="protect-your-dynamics-ax-application"></a>Dynamics AX uygulamanızı koruma
Her bir bileşeninin hello Dynamics AX gereksinimlerini toobe tooenable hello tam uygulama çoğaltma ve kurtarma korumalı. Bu bölümde ele alınmaktadır:

**1. Active Directory koruma**

**2. SQL katmanının koruma**

**3. Uygulamanın ve Web katmanları koruma**

**4. Ağ yapılandırması**

**5. Kurtarma planı**

### <a name="1-setup-ad-and-dns-replication"></a>1. Kurulum AD ve DNS çoğaltması

Active Directory hello DR sitesi Dynamics AX uygulama toofunction için gereklidir. Merhaba müşterinin şirket içi ortamına hello kapsamına bağlı iki önerilen seçenek vardır.

**Seçenek 1**

Hello müşteri varsa, az sayıda uygulamayı ve onun tüm tek etki alanı denetleyicisi şirket içi site ve ASR çoğaltma tooreplicate hello DC makine toosecondary site (kullanmanızı öneririz sonra hello tüm site birlikte başarısız olması Geçerli Site tooSite ve Site tooAzure için).

**Seçenek 2**

Merhaba müşteri uygulamalar çok sayıda sahip bir Active Directory ormanı çalıştıran ve yük birkaç uygulamalar aynı anda devretme durumunda hello DR sitesi ek etki alanı denetleyicisinde ayarlama öneririz (ikincil site veya Azure).

Lütfen çok başvurun[bir etki alanı denetleyicisi DR sitede kullanılabilir hale getirme üzerinde yardımcı kılavuz](site-recovery-active-directory.md). Bu belgenin geri kalanında için DC DR sitesinden edinilebilir varsayacağız.

### <a name="2-setup-sql-server-replication"></a>2. SQL Server çoğaltması Kurulumu
Lütfen koruma seçeneği önerilen hello ayrıntılı teknik kılavuzluk etmesi için toocompanion Kılavuzu başvurun [SQL katmanı](site-recovery-sql.md).

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3. Dynamics AX İstemcisi ve AOS VM'ler için korumayı etkinleştirin
Olup hello VM'ler dağıtılan üzerinde temel ilgili Azure Site Recovery yapılandırmasını gerçekleştirmek [Hyper-V](site-recovery-hyper-v-site-to-azure.md) veya [VMware](site-recovery-vmware-to-azure.md).

> [!TIP]
> Önerilen kilitlenme tutarlı sıklığı tooconfigure 15 dakikadır.
>

Anlık görüntü aşağıda Hello 'VMware sitesi tooAzure' koruma senaryoda Dynamics bileşen VM'ler hello koruma durumunu gösterir.
![Korumalı öğeler](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4. Ağı yapılandırma
VM yapılandırma işlem ve ağ ayarları

Merhaba VM ağları, yük devretme sonrasında ekli toohello doğru DR ağ elde etmeniz hello AX İstemcisi ve AOS VM'ler için Azure Site Recovery ağ ayarlarını yapılandırın. Bu katmanlar için Hello DR ağ yönlendirilebilir toohello SQL katmanı olduğundan emin olun.

Seçebileceğiniz hello hello VM çoğaltılan öğeler tooconfigure hello ağ ayarlarını aşağıdaki hello anlık görüntüde gösterildiği gibi.

* AOS sunucuları hello doğru kullanılabilirlik kümesi seçin.

* Bir statik IP kullanarak yeniden hello içinde sanal makine tootake hello istediğiniz hello IP belirtin **hedef IP** alan ![ağ ayarları](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)



### <a name="5-creating-a-recovery-plan"></a>5. Bir kurtarma planı oluşturma

Azure Site Recovery tooautomate hello yük devretme işleminde bir kurtarma planı oluşturabilirsiniz. Uygulama katmanı ve web katmanı hello Kurtarma planlaması ekleyin. Uygulama katmanı önce ön uç kapatma hello için bunları farklı gruplarda sıralayın.

1)  Aboneliğinizde Hello Azure Site Recovery kasası seçin ve 'Kurtarma planları' kutucuğuna tıklayın.

2)  Tıklayın ' + kurtarma planı ve bir ad belirtin.

3)  Merhaba 'Source' ve 'Target' seçin. Merhaba hedef Azure veya ikincil site olabilir. Azure seçtiğiniz durumda hello dağıtım modelini belirtin

![Kurtarma planı oluşturun](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  Merhaba AOS ve istemci VM'ler toohello kurtarma planı seçin ve ✓'ı tıklatın.
![Kurtarma planı oluşturun](./media/site-recovery-dynamics-ax/selectvms.png)


![Kurtarma planı](./media/site-recovery-dynamics-ax/recoveryplan.png)

Aşağıda açıklandığı gibi çeşitli adımları ekleyerek hello kurtarma planı Dynamics AX uygulama için özelleştirebilirsiniz. Anlık görüntü yukarıda Hello hello adımların tümünü ekledikten sonra hello tam kurtarma planı gösterir.

*Adımlar:*

*1. SQL Server üzerinde adımları başarısız*

Çok başvuran['SQL Server DR çözüm'](site-recovery-sql.md) kurtarma adımları belirli tooSQL sunucu hakkındaki ayrıntılar için yardımcı kılavuz.

*2. Yük devretme Grup 1: hello AOS VM'ler başarısız*

Seçili hello kurtarma noktası olası toohello veritabanı PIT olarak Kapat ancak değil şimdi olduğundan emin olun.

*3. Komut dosyası: Ekle yük dengeleyici (yalnızca E-A)* tooadd bir yük dengeleyici tooit gelen AOS VM gruptan sonra bir komut dosyası (aracılığıyla Azure Otomasyonu) ekleyin. Bu görev bir betiği toodo kullanabilirsiniz. Makale başvuran [nasıl tooadd yük dengeleyici çok katmanlı uygulama DR için](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)

*4. Yük devretme Grup 2: hello AX İstemcisi VM'ler başarısız.*
Merhaba web katmanı VM'ler hello kurtarma planının bir parçası olarak yük devri.


### <a name="doing-a-test-failover"></a>Yük devretme sınamasını yapmak

Too'AD DR çözüm başvuran ' ve 'SQL Server DR çözüm' yardımcı Kılavuzlar konuları belirli tooAD ve SQL server yük devretme testi sırasında sırasıyla için.

1.  TooAzure portal gidin ve Site Recovery kasanızı seçin.
2.  Dynamics AX için oluşturduğunuz hello kurtarma planı tıklayın.
3.  'Test yük devretme üzerinde' tıklayın.
4.  Merhaba sanal ağ toostart hello test yük devretme işlemini seçin.
5.  Merhaba ikincil ortamı kurma olduğunda, doğrulama gerçekleştirebilirsiniz.
6.  Hello doğrulama tamamlandıktan sonra 'Doğrulamaları tamamlamak' seçin ve yük devretme sınama ortamı hello temizlenecek.

İzleyin [bu kılavuz](site-recovery-test-failover-to-azure.md) toodo yük devretme sınaması.

### <a name="doing-a-failover"></a>Bir yük devretme işleminden

1.  TooAzure portal gidin ve Site Recovery kasanızı seçin.
2.  Dynamics AX için oluşturduğunuz hello kurtarma planı tıklayın.
3.  'Üzerinde yük devretme' tıklatın ve 'Failover' seçin.
4.  Merhaba hedef ağ seçin ve ✓ toostart hello yük devretme işlemi'ı tıklatın.

İzleyin [bu kılavuz](site-recovery-failover.md) , yaparken bir yük devretme.

### <a name="perform-a-failback"></a>Bir yeniden çalışma gerçekleştirme

Too'SQL sunucu DR çözüm başvuran ' yeniden çalışma sırasında dikkat edilecek noktalar belirli tooSQL sunucusu için yardımcı kılavuz.

1.  TooAzure portal gidin ve Site Recovery kasanızı seçin.
2.  Dynamics AX için oluşturduğunuz hello kurtarma planı tıklayın.
3.  'Üzerinde yük devretme' tıklayın ve yük devretme seçin.
4.  'Üzerinde değişiklik yön' seçeneğini tıklatın.
5.  Merhaba uygun seçenekleri - veri eşitleme ve VM oluşturma seçeneklerini belirtin
6.  ✓ toostart hello 'Yeniden çalışma' işlemi'ı tıklatın.


İzleyin [bu kılavuz](site-recovery-failback-azure-to-vmware.md) , yaparken bir yeniden çalışma.

##<a name="summary"></a>Özet
Azure Site Recovery kullanarak, Dynamics AX uygulamanız için bir tam otomatik olağanüstü durum kurtarma planı oluşturabilirsiniz. Her yerden saniye içinde hello yük devretme başlatabilirsiniz hello kesilme olayı ve dakika içinde çalışır durumda hello uygulama alın.

## <a name="next-steps"></a>Sonraki adımlar
Okuma [hangi iş yüklerini koruyabilirim?](site-recovery-workload.md) toolearn Azure Site Recovery ile kurumsal iş yüklerini koruma hakkında daha fazla.
