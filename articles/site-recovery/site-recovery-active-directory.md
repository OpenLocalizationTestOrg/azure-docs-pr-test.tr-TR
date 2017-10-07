---
title: aaaProtect Active Directory ve DNS Azure Site Recovery ile | Microsoft Docs
description: "Bu makalede nasıl tooimplement Azure Site Recovery kullanarak Active Directory için bir olağanüstü durum kurtarma çözümü."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a>Active Directory ve DNS Azure Site Recovery ile koruma
SharePoint, Dynamics AX ve SAP gibi kurumsal uygulamalar Active Directory ve DNS altyapısı toofunction doğru bağlıdır. Uygulamalar için bir olağanüstü durum kurtarma çözümü oluşturduğunuzda, tooprotect gerekir ve Active Directory ve DNS hello önce kurtarma önemli tooremember olan diğer uygulama bileşenleri, olağanüstü durum oluştuğunda şeyler düzgün tooensure.

Site kurtarma, çoğaltma, yük devretme ve kurtarma sanal makinelerin düzenleyerek olağanüstü durum kurtarma sağlayan bir Azure hizmetidir. Site Recovery, bir dizi çoğaltma senaryolarını tooconsistently korumak ve sorunsuz bir şekilde yük devretme sanal makineler ve uygulamaları tooprivate, public veya barındırma sağlayıcısı bulut destekler.

Site Kurtarma'yı kullanarak, Active Directory için bir tam otomatik olağanüstü durum kurtarma planı oluşturabilirsiniz. Kesinti oluştuğunda yerden saniye içinde bir yük devretme başlatın ve Active Directory birkaç dakika içinde hazır ve çalışır alın. SharePoint ve SAP gibi birden çok uygulama için birincil sitenizde Active Directory dağıttığınıza ve hello eksiksiz site toofail istiyorsanız Active Directory ilk kullanarak üzerinden edilemeyebilir Site Recovery ve sonra Yük devretme hello diğer uygulamalar uygulamaya özgü kurtarma planları kullanma.

Bu makalede, desteklenen yapılandırmalar ve önkoşullar nasıl toocreate Active Directory için bir olağanüstü durum kurtarma çözümü, nasıl tooperform planlanmış, Planlanmayan ve test yük devretmeleri tek tıklatmayla kurtarma planı kullanarak hello açıklanmaktadır.  Başlamadan önce Active Directory ve Azure Site Recovery konusunda bilgi sahibi olmanız gerekir.

## <a name="replicating-domain-controller"></a>Çoğaltma etki alanı denetleyicisi

Toosetup gerek [Site Recovery çoğaltma](#enable-protection-using-site-recovery) en az bir sanal makine etki alanı denetleyicisi ve DNS barındırma üzerinde. Varsa [birden çok etki alanı denetleyicileri](#environment-with-multiple-domain-controllers) ortamınızda, ayrıca tooreplicating hello de tooset çalışır duruma getirdikten Site Recovery ile etki alanı denetleyicisi sanal makine bir [ek etki alanı denetleyicisi](#protect-active-directory-with-active-directory-replication) hello hedef sitede (Azure veya bir ikincil şirket içi veri merkezine). 

### <a name="single-domain-controller-environment"></a>Tek bir etki alanı denetleyici ortamı
Bazı uygulamalar ve yalnızca bir tek etki alanı denetleyicisi olması ve toofail hello tüm site birlikte istediğiniz durumunda Site Recovery tooreplicate hello etki alanı denetleyicisini kullanarak toohello ikincil site öneririz (tooAzure çalıştırma işlemini gerçekleştiriyorsanız veya tooa ikincil site). Merhaba aynı etki alanı denetleyicisinin/DNS sanal makine için kullanılabilir çoğaltılan [yük devretme sınamasını](#test-failover-considerations) de.

### <a name="environment-with-multiple-domain-controllers"></a>Birden çok etki alanı denetleyicileriyle ortamı
Birçok uygulama varsa ve hello ortamında birden fazla etki alanı denetleyicisi yoktur veya aynı anda birkaç uygulamaları toofail planlıyorsanız, ayrıca bu tooreplicating hello etki alanı denetleyicisi sanal öneririz Site Recovery ile ayrıca makine ayarlanmış bir [ek etki alanı denetleyicisi](#protect-active-directory-with-active-directory-replication) hello hedef sitede (Azure veya bir ikincil şirket içi veri merkezine). İçin [yük devretme sınamasını](#test-failover-considerations), Site Recovery tarafından ve yük devretme, hello hedef sitesinde hello ek etki alanı denetleyicisi için etki alanı denetleyicisi kullanın. 


Merhaba aşağıdaki bölümlerde açıklanmıştır nasıl Site Recovery, bir etki alanı denetleyicisine tooenable korumasına ve nasıl tooset Azure etki alanı denetleyicisi.

## <a name="prerequisites"></a>Ön koşullar
* Active Directory ve DNS sunucusu bir şirket içi dağıtımı.
* Bir Microsoft Azure aboneliği Azure Site kurtarma Hizmetleri kasasına.
* Hello Azure sanal makine hazırlık Değerlendirme Aracı VM'ler tooensure üzerinde çalıştırmak tooAzure çoğaltıyorsanız Azure Vm'leri ve Azure Site kurtarma Hizmetleri ile uyumlu.

## <a name="enable-protection-using-site-recovery"></a>Site RECOVERY'yi kullanarak korumayı etkinleştir
### <a name="protect-hello-virtual-machine"></a>Merhaba sanal makine koru
Merhaba etki alanı denetleyicisinin/DNS sanal makine Site Recovery korumasını etkinleştirin. Site Recovery ayarlarını Hello sanal makine türüne (Hyper-V veya VMware) göre yapılandırın. Site Recovery kullanılarak çoğaltılmış hello etki alanı denetleyicisi için kullanıldığından [yük devretme sınamasını](#test-failover-considerations). Merhaba aşağıdaki gereksinimleri karşıladığından emin olun:

1. Merhaba etki alanı denetleyicisi genel katalog sunucusudur
2. Merhaba etki alanı denetleyicisi, yük devretme testi sırasında gerekli rolleri için hello FSMO rol sahibi olmalıdır (Bu rolleri toobe else gerekir [ele](http://aka.ms/ad_seize_fsmo) hello yük devretme sonrasında)

### <a name="configure-virtual-machine-network-settings"></a>Sanal makine ağ ayarlarını yapılandırma
Merhaba sanal makine yük devretme sonrasında ekli toohello doğru ağ olmayacaktır hello etki alanı denetleyicisinin/DNS sanal makine için Site Recovery ağ ayarlarını yapılandırın. 

![VM ağ ayarları](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a>Active Directory Active Directory çoğaltma ile koruma
### <a name="site-to-site-protection"></a>Siteden siteye koruma
Bir etki alanı denetleyicisi hello ikincil sitede oluşturun. Merhaba sunucu tooa etki alanı denetleyicisi rolünü yükselttiğinizde hello hello adını belirtin hello birincil sitede kullanılan aynı etki alanı. Merhaba kullanabilirsiniz **Active Directory Siteleri ve Hizmetleri** hello site bağlantısı ayarlarını tooconfigure nesne toowhich hello siteleri eklenir eklentisi. Bir site bağlantısı ayarlarını yapılandırarak, iki veya daha fazla siteler arasında çoğaltma oluştuğunda denetleyebilir ve ne sıklıkta. Daha fazla bilgi için bkz: [siteler arasında çoğaltma zamanlama](https://technet.microsoft.com/library/cc731862.aspx).

### <a name="site-to-azure-protection"></a>Site Azure koruma
Çok olarak Hello yönergeleri[bir Azure sanal ağındaki bir etki alanı denetleyicisi oluşturmak](../active-directory/active-directory-install-replica-active-directory-domain-controller.md). Merhaba sunucu tooa etki alanı denetleyicisi rolünü yükselttiğinizde hello belirtin hello birincil sitede kullanılan aynı etki alanı adı.

Ardından [hello DNS sunucusu hello sanal ağ için yeniden](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), azure'da toouse hello DNS sunucusu.

![Azure Ağı](./media/site-recovery-active-directory/azure-network.png)

**Azure üretim ağındaki DNS**

## <a name="test-failover-considerations"></a>Test yük devretme konuları
Üretim iş yükleri üzerinde hiçbir etkisi yani üretim ağınızdan yalıtılmış olan bir ağda yük devretme testi oluşur.

Çoğu uygulama aynı zamanda bir etki alanı denetleyicisi ve DNS sunucusu toofunction hello bulunması gerekir. Bu nedenle, bir etki alanı denetleyicisi Merhaba uygulaması devredilen önce yük devretme sınaması için kullanılan hello yalıtılmış ağ toobe oluşturulan toobe gerekir. en kolay yolu toodo hello tooreplicate Site Recovery ile etki alanı denetleyicisinin/DNS sanal makine budur. Ardından hello etki alanı denetleyicisi sanal makineye bir sınama yük devretmesi hello kurtarma planı Merhaba uygulaması için bir sınama yük devretmesi çalıştırmadan önce çalıştırın. Bunu nasıl aşağıda verilmiştir:

1. [Çoğaltma](site-recovery-replicate-vmware-to-azure.md) Site Recovery kullanarak etki alanı denetleyicisinin/DNS sanal makine hello.
1. Yalıtılmış bir ağ oluşturun. Varsayılan olarak Azure içinde oluşturulan herhangi bir sanal ağ diğer ağlardan yalıtılır. Bu ağ için başlangıç IP adresi aralığı, üretim ağınıza aynı olduğunu öneririz. Bu ağ üzerinde siteden siteye bağlantı etkinleştirmeyin.
1. Oluşturulan, başlangıç IP adresi olarak hello DNS sanal makine tooget beklediğiniz hello ağdaki bir DNS IP adresi sağlayın. TooAzure çoğaltıyorsanız sonra başlangıç IP adresi hello yük devretme kümesinde kullanılan VM sağlamak **hedef IP** ayarı **işlem ve ağ** ayarlar. 

    ![Hedef IP](./media/site-recovery-active-directory/DNS-Target-IP.png) **hedef IP**

    ![Azure Test ağı](./media/site-recovery-active-directory/azure-test-network.png)

    **Azure Test ağındaki DNS**

> [!TIP]
> Site Recovery toocreate test sanal makineleri aynı adlı bir alt ağda çalışır ve kullanarak hello olarak sağlanan aynı IP **işlem ve ağ** hello sanal makinenin ayarlarını. Test sanal makinesi hello ilk alt ağda alfabetik olarak oluşturulduktan sonra aynı adlı alt ağ hello yük devretme sınaması için sağlanan Azure sanal ağı kullanılabilir değilse. Merhaba hedef IP alt ağı seçilen hello parçası ise, Site Recovery hello hedef IP kullanarak toocreate hello test yük devretme sanal makine çalışır. Merhaba hedef IP alt ağı seçilen hello parçası değilse, test yük devretme sanal makine kullanılabilir bir IP alt ağı seçilen hello kullanarak oluşturulur. 
>
>


1. Tooanother şirket içi siteye çoğaltma yapıyorsanız ve DHCP kullanıyorsanız, hello çok yönergeleri[DNS ve DHCP yük devretme sınaması için Kur](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)
1. Yük devretme testi hello etki alanı denetleyicisi sanal makinenin hello yalıtılmış ağda çalıştırmak yapın. Kullanım en son kullanılabilir **uygulama tutarlı** hello etki alanı denetleyicisi sanal makine toodo hello yük devretme sınamasının kurtarma noktası. 
1. Yük devretme sınaması hello uygulamanın sanal makineleri içeren hello kurtarma planı için çalıştırın. 
1. Test tamamlandıktan sonra **temizleme yük devretme testi** hello etki alanı denetleyicisi sanal makine üzerinde. Bu adım, yük devretme sınaması için oluşturulan hello etki alanı denetleyicisi siler.


### <a name="removing-reference-tooother-domain-controllers"></a>Başvuru tooother etki alanı denetleyicilerini kaldırma
Bir test yük devretme yapılırken hello test ağında tüm hello etki alanı denetleyicileri Getir yok. tooremove hello başvurusu, üretim ortamınızda mevcut diğer etki alanı denetleyicilerinin ihtiyacınız olabilecek çok[Active Directory FSMO rolleri](http://aka.ms/ad_seize_fsmo) ve [meta veri temizleme](https://technet.microsoft.com/library/cc816907.aspx) eksik etki alanı için denetleyicileri. 



> [!IMPORTANT]
> Bölümden hello açıklanan hello yapılandırmaların bazıları hello standart/varsayılan etki alanı denetleyicisi yapılandırması değildir. Toomake istemiyorsanız, bu değişiklikleri tooa üretim etki alanı denetleyicisi olduktan sonra Site Recovery yük devretme sınaması için kullanılan bir etki alanı denetleyicisi ayrılmış toobe oluşturabilir ve bu değişiklikleri toothat olun.  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a>Sorunları nedeniyle sanallaştırma korumaları 

Windows Server 2012 ile başlayan [ek güvenlik önlemleri, Active Directory etki alanı hizmetlerine inşa](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100). Merhaba temel hiper yönetici platformunun VM-Generationıd'yi destekleyen sürece bu korumalar USN geri alma, sanallaştırılmış etki alanı denetleyicilerinde koruyun. Azure, Windows Server 2012 ya da daha sonra Azure sanal makineleri çalıştıran etki alanı denetleyicileri hello ek güvenlik önlemleri sahip VM-Generationıd'yi destekleyen. 


Merhaba VM-Generationıd sıfırladığınızda hello Invocationıd hello AD DS veritabanının da sıfırlanır, hello RID havuzu atılır ve SYSVOL'ü yetkisiz olarak işaretlenmiş. Daha fazla bilgi için bkz: [giriş tooActive Directory etki alanı Hizmetleri sanallaştırma](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) ve [DFSR'yi sanallaştırılması](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)

TooAzure yapabilmesini VM-Generationıd sıfırlama neden olabilir ve Azure'da hello etki alanı denetleyicisi sanal makine başlatıldığında, hello içinde ek güvenlik önlemleri başlatır. Bu neden bir **önemli gecikme** mümkün toologin toohello etki alanı denetleyicisi sanal makine olan kullanıcı. Bu etki alanı denetleyicisi yalnızca bir test yük devretme kümesinde kullanılacak olduğundan, sanallaştırma korumalarını gerekli değildir. Merhaba şirket içi etki alanı denetleyicisinde aşağıdaki DWORD too4 hello değerini değiştirebilir sonra VM-Generationıd hello etki alanı denetleyicisi sanal makine için değişmez tooensure.

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a>Sanallaştırma korumaları belirtileri
 
Sanallaştırma korumaları test yük devretme sonrasında koparılan değilse, bir veya daha fazla aşağıdaki belirtilerden birini görebilirsiniz:  

Oluşturma kimliği değişikliği

![Oluşturma kimliği değişikliği](./media/site-recovery-active-directory/Event2170.png)

Çağırma kimliği değişikliği

![Çağırma kimliği değişikliği](./media/site-recovery-active-directory/Event1109.png)

SYSVOL ve Netlogon paylaşımları kullanılabilir değil

![Sysvol paylaşımı](./media/site-recovery-active-directory/sysvolshare.png)

![Ntfrs Sysvol](./media/site-recovery-active-directory/Event13565.png)

Tüm DFSR veritabanlarını sildi

![DFSR DB Sil](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> Bölümden hello açıklanan hello yapılandırmaların bazıları hello standart/varsayılan etki alanı denetleyicisi yapılandırması değildir. Toomake istemiyorsanız, bu değişiklikleri tooa üretim etki alanı denetleyicisi olduktan sonra Site Recovery yük devretme sınaması için kullanılan bir etki alanı denetleyicisi ayrılmış toobe oluşturabilir ve bu değişiklikleri toothat olun.  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a>Yük devretme testi sırasında etki alanı denetleyicisi sorunlarını giderme


Bir komut isteminde, SYSVOL ve NETLOGON klasörleri paylaşılıp paylaşılmayacağını komutu toocheck aşağıdaki hello çalıştırın:

    NET SHARE

Merhaba komut isteminde, etki alanı denetleyicisi hello tooensure düzgün komutu aşağıdaki hello çalıştırın.

    dcdiag /v > dcdiag.txt

Merhaba çıktı günlüğünde etki alanı denetleyicisi hello aşağıdaki metin tooconfirm arayın iyi çalışır. 

* "geçen test bağlantısı"
* "geçen test reklam"
* "geçen test MakineHesabı"

Merhaba Yukarıdaki koşullar sağlanırsa, hello etki alanı denetleyicisi düzgün olasıdır. Aksi durumda, aşağıdaki adımları deneyin.


* Merhaba etki alanı denetleyicisinin yetkili geri yükleme yapın.
    * Bu olmasına rağmen [toouse FRS çoğaltma önerilmez](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), ancak hala kullanıyorsanız sonra sağlanan hello adımları [burada](https://support.microsoft.com/kb/290762) toodo yetkili geri yükleme. Burflags hakkında daha fazla açıklandı hakkında hello önceki bağlantıyı okuyabilirsiniz [burada](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/).
    * DFSR çoğaltma kullanıyorsanız, ardından hello kullanılabilir adımları [burada](https://support.microsoft.com/kb/2218556) toodo yetkili geri yükleme. Ayrıca Powershell işlevleri bu kullanabilirsiniz [bağlantı](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/) bu amaç için. 
    
* İlk eşitleme gereksinimi, kayıt defteri anahtarı too0 hello şirket içi etki alanı denetleyicisinde aşağıdaki ayarlayarak atlama. Bu DWORD yoksa, daha sonra onu düğümünde 'Parameters' oluşturabilirsiniz. Daha fazla bilgiyi ilgili [burada](https://support.microsoft.com/kb/2001093)

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* Kayıt defteri anahtarı too1 hello şirket içi etki alanı denetleyicisinde aşağıdaki ayarlayarak bir genel katalog sunucusu kullanılabilir toovalidate kullanıcı oturum açma olduğunu hello gereksinimini devre dışı bırakın. Ardından bu DWORD yoksa, bunu 'Lsa' düğümünde oluşturabilirsiniz. Daha fazla bilgiyi ilgili [burada](http://support.microsoft.com/kb/241789)

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a>Farklı makinelerde DNS ve etki alanı denetleyicisi
DNS üzerinde hello değilse aynı sanal makine hello etki alanı denetleyicisi olarak hello yük devretme sınaması için DNS VM toocreate gerekir. Üzerinde iseniz aynı VM Merhaba, bu bölümü atlayabilirsiniz.

Yeni bir DNS sunucusu kullanın ve tüm gerekli hello bölgeler oluşturun. Örneğin, Active Directory etki alanı contoso.com ise, hello adı contoso.com bir DNS bölgesi oluşturabilirsiniz. tooActive dizin karşılık gelen hello girişlerinden DNS'de şu şekilde güncelleştirilmesi gerekir:

1. Herhangi bir sanal makine hello kurtarma planında gelir önce bu ayarları yerine getirildiğinden emin olun:
   
   * Merhaba bölge hello orman kök adından sonra adlandırılmalıdır.
   * Dosya yedekli Hello bölge olmalıdır.
   * Merhaba bölge için güvenli ve güvenli olmayan güncelleştirmeleri etkinleştirilmesi gerekir.
   * Merhaba çözümleyici hello etki alanı denetleyicisi sanal makinenin hello DNS sanal makinenin toohello IP adresini işaret etmelidir.
2. Etki alanı denetleyicisi sanal makinede komutu aşağıdaki hello çalıştırın:
   
    `nltest /dsregdns`
3. Merhaba DNS sunucusuna bir bölge ekleyin, güvenli olmayan güncelleştirmelere izin vermek ve bir girdi için tooDNS ekleyin:
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a>Sonraki adımlar
Okuma [hangi iş yüklerini koruyabilirim?](site-recovery-workload.md) toolearn Azure Site Recovery ile kurumsal iş yüklerini koruma hakkında daha fazla.

