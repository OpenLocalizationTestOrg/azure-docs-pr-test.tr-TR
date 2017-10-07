---
title: Site kurtarma aaaFailover | Microsoft Docs
description: "Azure Site Recovery hello çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma düzenler. Yük devretme tooAzure veya ikincil veri merkezine hakkında bilgi edinin."
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
ms.openlocfilehash: 7cacea829d78bb7de2b2d67402291b472b10f023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="failover-in-site-recovery"></a>Site Recovery'de yük devretme
Bu makalede nasıl toofailover sanal makineleri ve fiziksel sunucuları Site Recovery tarafından korunan açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar
1. Bir yük devretme uygulamadan önce yapmak bir [yük devretme sınamasını](site-recovery-test-failover-to-azure.md) her şeyin beklendiği gibi çalıştığını tooensure.
1. [Merhaba ağ hazırlama](site-recovery-network-design.md) bir yük devretme yapmadan önce hedef konumda.  


## <a name="run-a-failover"></a>Yük devretme gerçekleştirme
Bu yordam açıklar nasıl toorun bir yük devretme için bir [kurtarma planı](site-recovery-create-recovery-plans.md). Alternatif olarak hello yük devretme tek sanal makine ya da fiziksel sunucu için hello çalıştırabilirsiniz **öğeleri çoğaltılan** sayfası


![Yük devretme](./media/site-recovery-failover/Failover.png)

1. Seçin **kurtarma planları** > *recoveryplan_name*. Tıklatın **yük devretme**
2. Merhaba üzerinde **yük devretme** ekran, select bir **kurtarma noktası** toofailover için. Seçenekler aşağıdaki hello birini kullanabilirsiniz:
    1.  **En son** (varsayılan): Bu seçenek ilk gönderilen tooSite kurtarma hizmeti toocreate her bir sanal makine için bir kurtarma noktası tooit başarısız olmadan önce yapılmış tüm hello verileri işler. Bu seçenek hello sağlar hello yük devretme tetiklendiğinde düşük RPO (kurtarma noktası hedefi) hello yük devretme tüm hello veri sahip olduktan sonra oluşturulan sanal boyunca makinenin olarak çoğaltılmış tooSite kurtarma hizmeti.
    1.  **En son işlenen**: Site Recovery hizmeti tarafından işlenmiş olan hello kurtarma planı toohello en son kurtarma noktası tüm sanal makinelerin bu seçenek yöneltilir. Bir sanal makine yük devretme yapılırken hello son işlenen kurtarma noktasının zaman damgası da gösterilir. Bir kurtarma planı yük devretme yapıyorsanız, tooindividual sanal makineye gidin ve bakmak **en son kurtarma noktası** bu bilgileri tooget döşeme. Hiçbir zaman harcanan şekilde işlenmemiş verileri tooprocess Merhaba, bu seçenek, bir düşük RTO (Kurtarma süresi hedefi) yük devretme seçeneği sağlar.
    1.  **Son uygulama tutarlı**: Bu seçenek, Site Recovery hizmeti tarafından işlenmiş olan hello kurtarma planı toohello en son uygulama tutarlı bir kurtarma noktası tüm sanal makinelerin yöneltilir. Bir sanal makine yük devretme yapılırken hello son uygulamayla tutarlı kurtarma noktasının zaman damgası da gösterilir. Bir kurtarma planı yük devretme yapıyorsanız, tooindividual sanal makineye gidin ve bakmak **en son kurtarma noktası** bu bilgileri tooget döşeme.
    1.  **En son çoklu işlenen VM**: Bu seçenek yalnızca çoklu VM tutarlılığını en az bir sanal makineyle sahip kurtarma planları için kullanılabilir. Bir çoğaltma grubu yük devretme toohello son ortak çoklu VM tutarlı kurtarma parçası olan sanal makineleri gelin. Diğer sanal makineler yük devretme tootheir son işlenen kurtarma noktası.  
    1.  **En son çoklu VM uygulamayla tutarlı**: Bu seçenek yalnızca çoklu VM tutarlılığı ON ile en az bir sanal makinenin kurtarma planları için kullanılabilir. Bir çoğaltma parçası olan sanal makinelere yük devretme toohello son ortak çoklu VM uygulamaları tutarlı kurtarma noktası gruplandırın. Diğer sanal makineler yük devretme tootheir en son uygulama tutarlı kurtarma noktası.
    1.  **Özel**: bir sanal makinenin yük devretme testi yapmakta olduğunuz sonra bu seçeneği toofailover tooa belirli kurtarma noktası kullanabilirsiniz.

    > [!NOTE]
    > Merhaba seçeneği toochoose bir kurtarma noktası, yalnızca tooAzure başarısız olduğunda kullanılabilir.
    >
    >


1. Bazı hello kurtarma planında hello sanal makinelerin üzerinden önceki çalışmada başarısız ve hello sanal makineleri hem kaynak hem de hedef konumunda etkin artık kullanabileceğiniz **değiştirme yönü** seçeneği toodecide hello yönde hangi hello yük devretme gerçekleşmelidir.
1. TooAzure çalıştırma işlemini gerçekleştiriyorsanız ve veri şifreleme (VMM sunucusundan Hyper-v sanal makineleri yalnızca korumalı olduğunda geçerlidir) hello bulut için etkinleştirildi, **şifreleme anahtarı** ne zaman verilmiş select hello sertifika, Merhaba VMM sunucusunda kurulumu sırasında veri şifrelemesi etkin.
1. Seçin **yük devretme işlemine başlamadan önce makineyi kapatın** Site Recovery tooattempt toodo istiyorsanız, bir kapanma tetiklemeden önce kaynak sanal makinelerin hello yük devretme. Kapatma başarısız olsa bile yük devretme devam eder.  

    > [!NOTE]
    > Bu seçenek, Hyper-v sanal makineleri durumunda henüz toohello hizmet hello yük devretme tetiklemeden gönderilmedi toosynchronize hello şirket içi veri de çalışır.
    >
    >

1. Merhaba üzerinde hello yük devretme işleminin ilerleyişini izleyebilirsiniz **işleri** sayfası. Planlanmamış bir yük devretme sırasında bir hata oluşmamasına olsa bile tamamlanıncaya kadar hello kurtarma planı çalıştırır.
1. Merhaba yük devretme sonrasında hello sanal makine içinde tooit oturum açarak doğrulayın. Merhaba sanal makine için başka bir kurtarma noktası toogo istediğiniz sonra kullanabileceğiniz **değiştirmek kurtarma noktası** seçeneği.
1. Yükü devredilen sanal makine üzerinde hello ile memnun sonra **yürütme** yük devretme hello. Bu hello hizmetiyle kullanılabilir tüm hello kurtarma noktalarını siler ve **değiştirmek kurtarma noktası** seçeneği artık kullanılabilir.

## <a name="planned-failover"></a>Planlanan yük devretme
Dışında yük devretme, Site kurtarma desteği de kullanılarak korunan Hyper-V sanal makineler **planlanan yük devretme**. Bir sıfır veri kaybı yük devretme seçenek budur. Planlanmış bir yük devretme tetiklendiğinde ilk sanal makineleri hello veri aşağı, eşitlenen toobe eşitlenir ve ardından bir yük devretme tetiklenir henüz kapatılır kaynak hello.

> [!NOTE]
> Yük devretme Hyper-v sanal makinelerden biri site tooanother şirket, şirket içi sitesi, toofirst sahip toocome geri toohello içi birincil site **ters çoğaltmak** hello sanal makine geri tooprimary site ve ardından bir yük devretmeyi tetikler. Merhaba birincil sanal makine ardından önce çok başlayarak kullanılabilir değilse,**ters çoğaltmak** toorestore hello sanal makine bir yedekten sahip.   
>
>

## <a name="failover-job"></a>Yük devretme işine

![Yük devretme](./media/site-recovery-failover/FailoverJob.png)

Bir yük devretme tetiklendiğinde, aşağıdaki adımları içerir:

1. Önkoşul denetimi: Bu adım, yük devretme için gerekli tüm koşulların karşılandığından sağlar
1. Yük devretme: Bu adım hello verilerini işler ve böylece dışında bir Azure sanal makinesi oluşturulabilir hazır yapar. Seçmiş olmanız durumunda **son** kurtarma noktası, bu adımı oluşturur bir kurtarma noktası toohello hizmeti gönderilen hello verileri.
1. Başlangıç: Bu adım hello önceki adımda işlenen hello verileri kullanarak bir Azure sanal makinesi oluşturur.

> [!WARNING]
> **Etmekte iptal etme yük devretme**: yük devretme başlatılmadan önce hello sanal makinesi için çoğaltma durduruldu. Varsa, **iptal** bir ilerleme işinde tooreplicate yük devretme durdurur ancak hello sanal makine başlatılmaz. Çoğaltma yeniden başlatılamıyor.
>
>

## <a name="time-taken-for-failover-tooazure"></a>Yük devretme tooAzure için harcanan süre

Bazı durumlarda, sanal makinelerin yük devretme genellikle, yaklaşık 8 too10 dakika toocomplete alır bir ek ara adım gerektirir. Bu durumların olarak olan aşağıdaki:

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

Tüm hello diğer durumlarda bu ara adım gerekli değildir ve hello yük devretme için harcanan hello süre önemli ölçüde düşebilir. 





## <a name="using-scripts-in-failover"></a>Yük devretme kümesinde komut dosyalarını kullanma
Bir yük devretme yaparken belirli eylemleri tooautomate isteyebilirsiniz. Komut dosyalarını kullanabilirsiniz veya [Azure Otomasyon çalışma kitabı](site-recovery-runbook-automation.md) içinde [kurtarma planlarına](site-recovery-create-recovery-plans.md) toodo.

## <a name="other-considerations"></a>Diğer konular
* **Sürücü harfi** — tooretain hello sürücü harfi yük devretme sonrasında sanal makinelerde hello ayarlayabilirsiniz **SAN ilkesini** çok hello sanal makine**OnlineAll**. [Daha fazla bilgi](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).



## <a name="next-steps"></a>Sonraki adımlar
Sanal makineler üzerinde başarısız oldu ve hello şirket içi veri merkezi kullanılabilir sonra yapmanız gerekenler [ **yeniden koruma** ](site-recovery-how-to-reprotect.md) toohello şirket içi veri merkezi VMware sanal makineleri yedekleyin.

Kullanım [ **planlanan yük devretme** ](site-recovery-failback-from-azure-to-hyper-v.md) çok seçenek**geri dönme** Hyper-v sanal makineleri Azure'dan tooon içi yedekleyin.

Başarısız olan merkezi bir VMM sunucusu ve hello birincil veri merkezi tarafından yönetilen bir Hyper-v sanal makine tooanother şirket içi veri kullanılabilir, ardından **ters çoğaltmak** seçeneği toostart hello çoğaltma geri toohello birincil veri merkezi.
