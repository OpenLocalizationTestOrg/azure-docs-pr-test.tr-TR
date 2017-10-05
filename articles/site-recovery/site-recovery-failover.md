---
title: "Yük devretme Site kurtarma | Microsoft Docs"
description: "Azure Site Recovery, çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma düzenler. Azure veya ikincil veri merkezine yük devretme hakkında bilgi edinin."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: ef586191f0b89dca89810644d45503fe42538635
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="failover-in-site-recovery"></a>Site Recovery'de yük devretme
Bu makalede, yük devretme sanal makinelere ve fiziksel sunucuları Site Recovery tarafından korunan nasıl açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar
1. Bir yük devretme uygulamadan önce yapmak bir [yük devretme sınamasını](site-recovery-test-failover-to-azure.md) her şeyin beklendiği gibi çalıştığından emin olmak için.
1. [Ağ hazırlama](site-recovery-network-design.md) bir yük devretme yapmadan önce hedef konumda.  


## <a name="run-a-failover"></a>Yük devretme gerçekleştirme
Bu yordamda, bir yük devretme için çalıştırmak açıklanmaktadır bir [kurtarma planı](site-recovery-create-recovery-plans.md). Alternatif olarak, yük devretme için tek bir sanal makine veya fiziksel sunucudan çalıştırabilirsiniz **öğeleri çoğaltılan** sayfası


![Yük devretme](./media/site-recovery-failover/Failover.png)

1. Seçin **kurtarma planları** > *recoveryplan_name*. Tıklatın **yük devretme**
2. Üzerinde **yük devretme** ekran, select bir **kurtarma noktası** yük. Aşağıdaki seçeneklerden birini kullanabilirsiniz:
    1.  **En son** (varsayılan): Bu seçenek ilk bunları üzerinden ona başarısız olmadan önce her bir sanal makine için bir kurtarma noktası oluşturmak için Site Recovery hizmetine gönderilen tüm verileri işler. Bu seçenek sanal yük devretme tüm verilere sahip sonra oluşturulan yük devretme tetiklendiğinde Site Recovery hizmetine çoğaltılan makinenin düşük RPO (kurtarma noktası hedefi) sağlar.
    1.  **En son işlenen**: Site Recovery hizmeti tarafından işlenmiş olan en son kurtarma noktasına kurtarma planının tüm sanal makineleri bu seçenek yöneltilir. Bir sanal makine yük devretme yapılırken, en son işlenen kurtarma noktası zaman damgası da gösterilir. Bir kurtarma planı yük devretme yapıyorsanız, tek tek sanal makineye gidin ve bakmak **en son kurtarma noktası** bu bilgileri almak için bölme. İşlenmemiş verileri işlemek için harcanan hiçbir zaman gibi bu seçenek bir düşük RTO (Kurtarma süresi hedefi) yük devretme seçeneği sağlar.
    1.  **Son uygulama tutarlı**: Site Recovery hizmeti tarafından işlenmiş olan son uygulama tutarlı kurtarma noktasına kurtarma planının tüm sanal makineleri bu seçenek yöneltilir. Bir sanal makine yük devretme yapılırken en son uygulamayla tutarlı kurtarma noktasının zaman damgası da gösterilir. Bir kurtarma planı yük devretme yapıyorsanız, tek tek sanal makineye gidin ve bakmak **en son kurtarma noktası** bu bilgileri almak için bölme.
    1.  **En son çoklu işlenen VM**: Bu seçenek yalnızca çoklu VM tutarlılığını en az bir sanal makineyle sahip kurtarma planları için kullanılabilir. En son ortak çoklu VM tutarlı Kurtarma bir çoğaltma grubu yük devretme parçası olan sanal makineleri gelin. Diğer sanal makineler yük devretme bunların en son işlenen kurtarma noktası.  
    1.  **En son çoklu VM uygulamayla tutarlı**: Bu seçenek yalnızca çoklu VM tutarlılığı ON ile en az bir sanal makinenin kurtarma planları için kullanılabilir. Çoğaltma grubu yük devretme son ortak çoklu VM uygulamaları tutarlı kurtarma için bir parçası olan sanal makineleri gelin. Diğer sanal makineler kendi son noktaya yük devretme uygulamaları tutarlı kurtarma.
    1.  **Özel**: bir sanal makinenin yük devretme testi yapmakta olduğunuz sonra belirli bir kurtarma noktası için yük devretme için bu seçeneği kullanabilirsiniz.

    > [!NOTE]
    > Bir kurtarma noktası seçin seçeneğine yalnızca için Azure üzerinden başarısız oluyor.
    >
    >


1. Bazı sanal makineler kurtarma planında üzerinden önceki çalışmada başarısız ve sanal makineleri hem kaynak hem de hedef konumunda etkin artık kullanabileceğiniz **değiştirme yönü** hangi yönde karar vermek için seçeneği Yük devretme gerçekleşmelidir.
1. Azure'a devretmek ve veri şifreleme (VMM sunucusundan Hyper-v sanal makineleri yalnızca korumalı olduğunda geçerlidir) bulut için etkinleştirildi, **şifreleme anahtarı** , etkinleştirildiğinde verilmiş sertifikayı seçin VMM sunucusundaki Kurulum sırasında veri şifreleme.
1. Seçin **yük devretme işlemine başlamadan önce makineyi kapatın** Site Kurtarma'nın bir kapanma kaynak sanal makinelerin yük devretme tetiklemeden yapmaya istiyorsanız. Kapatma başarısız olsa bile yük devretme devam eder.  

    > [!NOTE]
    > Hyper-v sanal makineleri durumunda henüz hizmete yük devretme tetiklemeden gönderilmedi şirket içi verileri eşitlemek bu seçeneği de çalışır.
    >
    >

1. Yük devretme işleminin ilerleyişini izleyin **işleri** sayfası. Planlanmamış bir yük devretme sırasında bir hata oluşmamasına olsa bile tamamlanıncaya kadar kurtarma planı çalıştırır.
1. Yük devretme işleminden sonra sanal makine için oturum açarak doğrulayın. Sanal makine için başka bir kurtarma noktası gitmek istiyorsanız sonra kullanabileceğiniz **değiştirmek kurtarma noktası** seçeneği.
1. Başarısız oldu memnun sonra sanal makine üzerinde yapabilecekleriniz **yürütme** yük devretme. Bu hizmetle birlikte kullanılabilir tüm kurtarma noktalarını siler ve **değiştirmek kurtarma noktası** seçeneği artık kullanılabilir.

## <a name="planned-failover"></a>Planlanan yük devretme
Dışında yük devretme, Site kurtarma desteği de kullanılarak korunan Hyper-V sanal makineler **planlanan yük devretme**. Bir sıfır veri kaybı yük devretme seçenek budur. Planlanmış bir yük devretme tetiklendiğinde, kaynak sanal makinelerden önce kapatmak, henüz eşitlenecek verileri eşitlenir ve ardından bir yük devretme tetiklenir.

> [!NOTE]
> Bir yük devretme Hyper-v sanal makineleri başka bir şirket içi siteye site içi içi birincil siteye geri dönün, öncelikle gerekir **ters çoğaltmak** sanal makine birincil siteye yedekleyin ve ardından bir yük devretmeyi tetikler. Birincil sanal makine için önce başlangıç kullanılabilir değilse, **ters çoğaltmak** sanal makine bir yedekten geri yüklemek zorunda.   
>
>

## <a name="failover-job"></a>Yük devretme işine

![Yük devretme](./media/site-recovery-failover/FailoverJob.png)

Bir yük devretme tetiklendiğinde, aşağıdaki adımları içerir:

1. Önkoşul denetimi: Bu adım, yük devretme için gerekli tüm koşulların karşılandığından sağlar
1. Yük devretme: Bu adım verileri işler ve böylece dışında bir Azure sanal makinesi oluşturulabilir hazır kolaylaştırır. Seçmiş olmanız durumunda **son** kurtarma noktası bu adımı oluşturur, bir kurtarma noktası hizmete gönderilen verileri.
1. Başlangıç: Bu adım önceki adımda işlenen veri kullanarak bir Azure sanal makine oluşturur.

> [!WARNING]
> **Etmekte iptal etme yük devretme**: yük devretme başlamadan önce sanal makine için çoğaltma durduruldu. Varsa, **iptal** bir ilerleme işinde yük devretme durdurur, ancak sanal makine başlatılmayacak çoğaltmak. Çoğaltma yeniden başlatılamıyor.
>
>

## <a name="time-taken-for-failover-to-azure"></a>Azure'a yük devretme için harcanan süre

Bazı durumlarda, sanal makinelerin yük devretme genellikle tamamlamak için yaklaşık 8-10 dakika sürer bir ek ara adım gerektirir. Bu durumların olarak olan aşağıdaki:

* Mobility hizmeti 9.8 eski sürümünün kullanarak VMware sanal makineleri
* Fiziksel sunucuları 
* VMware Linux sanal makineleri
* Fiziksel sunucuları olarak korunan Hyper-V sanal makineler
* Burada aşağıdaki sürücüleri önyükleme sürücüler olarak mevcut olmayan VMware sanal makineler 
    * storvsc 
    * VMBus 
    * storflt 
    * Intelide 
    * ATAPI
* VMware sanal makineleri'de, DHCP hizmeti, DHCP veya statik kullanarak yedeklemiş etkin olmayan IP adresleri

Tüm diğer durumlarda bu ara adım gerekli değildir ve yük devretme için harcanan süre önemli ölçüde düşebilir. 





## <a name="using-scripts-in-failover"></a>Yük devretme kümesinde komut dosyalarını kullanma
Bir yük devretme yaparken belirli eylemleri otomatik hale getirmek isteyebilirsiniz. Komut dosyalarını kullanabilirsiniz veya [Azure Otomasyon çalışma kitabı](site-recovery-runbook-automation.md) içinde [kurtarma planlarına](site-recovery-create-recovery-plans.md) Bunu yapmak için.

## <a name="other-considerations"></a>Diğer konular
* **Sürücü harfi** — sanal makinelerde sürücü harfi ayarlayabileceğiniz yük devretme sonrasında korumak için **SAN ilkesini** sanal makine için **OnlineAll**. [Daha fazla bilgi](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).



## <a name="next-steps"></a>Sonraki adımlar
Sanal makineler üzerinde başarısız oldu ve şirket içi veri merkezi kullanılabilir sonra yapmanız gerekenler [ **yeniden koruma** ](site-recovery-how-to-reprotect.md) VMware sanal makineleri şirket içi veri merkezine yedekleyin.

Kullanım [ **planlanan yük devretme** ](site-recovery-failback-from-azure-to-hyper-v.md) için seçenek **geri dönme** azure'dan şirket içi dön Hyper-v sanal makineleri.

Üzerinden bir Hyper-v sanal makine başka bir veri merkezi bir VMM sunucusu tarafından yönetilen şirket içi ve birincil veri merkezi kullanılabilir, başarısız olursa, ardından **ters çoğaltmak** geri birincil veri için çoğaltma başlatma seçeneği Merkezi.
