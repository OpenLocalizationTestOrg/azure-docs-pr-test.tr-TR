---
title: aaaReplicate VMware Vm'lerini tooAzure | Microsoft Docs
description: "VMware Vm'leri tooAzure depolama üzerinde çalışan iş yüklerini çoğaltmak için gereken hello adımları özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-overview
ms.openlocfilehash: f800e7d8a3b59a86809a995748eacf87630a1713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-tooazure-with-site-recovery"></a>Site Recovery ile VMware sanal makineleri tooAzure Çoğalt

> [!div class="op_single_selector"]
> * [Azure portal](site-recovery-vmware-to-azure.md)
> * [Azure klasik](site-recovery-vmware-to-azure-classic.md)


Bu makalede nasıl tooreplicate VMware sanal makineleri tooAzure hello kullanarak, şirket içi [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

Toomigrate VMware Vm'lerini tooAzure (yalnızca yük devretme), okuma istiyorsanız [bu makalede](site-recovery-migrate-to-azure.md) toolearn daha fazla.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="deployment-steps"></a>Dağıtım adımları

İşte gerekenler toodo:

1. Önkoşulları ve sınırlamaları doğrulayın.
2. Azure ağ ve depolama hesaplarını kurun.
3. Merhaba şirket içi makineyi hazırlama hello yapılandırma sunucusu olarak toodeploy istiyor.
4. Toobe sanal makineleri otomatik olarak bulmayı ve isteğe bağlı olarak hello mobilite hizmetinin göndermeli yüklemesi için kullanılan VMware hesapları hazırlayın.
4. Kurtarma Hizmetleri kasası oluşturun. Merhaba kasası yapılandırma ayarlarını içeren, çoğaltma ve yönetir.
5. Kaynak ve hedef çoğaltma ayarlarını belirtin.
6. Merhaba Mobility hizmetini dağıtma Vm'lerinde tooreplicate istiyor.
7. Merhaba VM'ler çoğaltmayı etkinleştirin.
7. Her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırın.

## <a name="prerequisites"></a>Ön koşullar

**Destek gereksinimi** | **Ayrıntılar**
--- | ---
**Azure** | Hakkında bilgi edinin [Azure gereksinimleri](site-recovery-prereq.md#azure-requirements)
**Şirket içi yapılandırma sunucusu** | Windows Server 2012 R2 çalıştıran bir VMware VM gerekir ya da daha sonra. Site Recovery dağıtımı sırasında bu sunucusu ayarlayın.<br/><br/> Varsayılan hello işlem tarafından sunucu ve ana hedef sunucusu Ayrıca bu VM yüklenir. Ölçeği artırma, ayrı bir işlem sunucusu gerekebilir ve hello sahip olduğunda hello yapılandırma sunucusuyla aynı gereksinimleri.<br/><br/> Bu bileşenler hakkında daha fazla bilgi [burada](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**Şirket içi VMware sunucuları** | 6.0, 5.5, 5.1 ile en son güncelleştirmeleri çalıştıran bir veya daha fazla VMware vSphere sunucuları. Sunucular, aynı ağ hello yapılandırma sunucusu (veya ayrı işlem sunucusu) hello alanında bulunmalıdır.<br/><br/> Bir vCenter 6.0 veya 5.5 hello son güncelleştirmeleriyle çalıştıran sunucu toomanage ana öneririz. Sürüm 6.0 dağıttığınızda 5.5 içinde kullanılabilir olan özellikler desteklenir.
**Şirket içi sanal makineleri** | Tooreplicate çalışıyor istediğiniz sanal makineleri bir [işletim sistemi desteklenen](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)ve uygun olması [Azure önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). VM VMware araçları çalışıyor olması gerekir.
**URL'leri** | Merhaba yapılandırma sunucusu toothese URL'leri erişmesi gereken:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin emin olun.<br/></br> Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (443 numaralı) bağlantı noktası.<br/></br> IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.<br/><br/> Merhaba MySQL yüklemek için bu URL'ye izin ver: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Mobility hizmeti** | Her çoğaltılmış VM'de yüklü.




## <a name="limitations"></a>Sınırlamalar

**Sınırlama** | **Ayrıntılar**
--- | ---
**Azure** | Depolama ve ağ hesapları hello olmalıdır hello kasasıyla aynı bölgede<br/><br/> Premium depolama hesabı kullanırsanız, standart bir etmeniz hesap toostore çoğaltma günlüklerini depolamak<br/><br/> Orta ve Güney Hindistan toopremium hesapları çoğaltma yapamaz.
**Şirket içi yapılandırma sunucusu** | VMware VM bağdaştırıcı türü VMXNET3 olmalıdır. Öyle değilse, [bu güncelleştirmeyi yükleyin](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> vSphere Powerclı 6.0 yüklenmesi gerekir.<br/><br> Merhaba makine bir etki alanı denetleyicisi olmaması gerekir. Merhaba makine statik bir IP adresi olmalıdır.<br/><br/> Merhaba ana bilgisayar adı 15 karakter uzunluğunda olmalıdır veya daha az ve işletim sistemi İngilizce olmalıdır.
**VMware** | Yalnızca 5.5 özellikler vCenter 6.0 desteklenir. Site Recovery yeni vCenter desteklemez ve vSphere 6.0 özellikleri gibi vCenter VMotion'ı, sanal birimler ve depolama DRS arası.
**VM’ler** | Doğrulama [Azure VM sınırlamaları](site-recovery-prereq.md#azure-requirements)<br/><br/> Şifrelenmiş disklerle VM'ler veya UEFI/EFI Önyükleme olan VM'ler çoğaltma yapamaz.<br/><br> Paylaşılan disk kümelerini desteklenmez. NIC ekibi oluşturma Hello kaynak VM varsa, dönüştürülür tooa tek NIC yük devretme sonrasında.<br/><br/> Sanal makineleri bir iSCSI diski varsa, Site Recovery bu tooa VHD dosyasını yük devretme sonrasında dönüştürür. Merhaba iSCSI hedef hello Azure VM tarafından ulaşılabiliyorsa tooit bağlanır ve onu ve hello VHD görür. Bu durumda, hello iSCSI hedef bağlantısını kesin.<br/><br/> Aynı iş yükünü toobe kurtarılan hello çalıştıran VM'ler sağlayan tooenable çoklu VM tutarlılığını istiyorsanız birlikte tooa tutarlı veri noktası, bağlantı noktası 20004 hello VM açın.<br/><br/> Windows hello C sürücüsünde yüklenmesi gerekir. Merhaba işletim sistemi diski, temel ve dinamik olmayan olması gerekir. Merhaba veri diski dinamik olabilir.<br/><br/> Linux/Etc/Hosts dosyaları vm'lerde tüm ağ bağdaştırıcıları ile ilişkili hello yerel ana bilgisayar adı tooIP adresleri eşleyin giriş içermelidir. Merhaba ana bilgisayar adı, bağlama noktaları, aygıt adı, sistem yolu ve dosya adları (/ etc; / usr) İngilizce yalnızca olmalıdır.<br/><br/> Belirli türlerdeki [Linux depolama](site-recovery-support-matrix-to-azure.md#support-for-storage) desteklenir.<br/><br/>Oluşturma veya ayarlama **disk.enableUUID=true** hello VM Ayarları'nda. Bu tutarlı bir UUID toohello VMDK, sunar, böylece doğru bağlar ve yalnızca delta değişiklikler tam çoğaltma olmadan yeniden çalışma sırasında aktarılan geri tooon içi olmasını sağlar.

## <a name="set-up-azure"></a>Azure ayarlayın

1. [Bir Azure ağı ayarlama](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    - Yük devretme sonrasında oluşturulduğunda azure sanal makineleri bu ağda yer alır.
    - Bir ağda ayarlayabilirsiniz [Resource Manager](../resource-manager-deployment-model.md), ya da Klasik modda.

2. Ayarlanmış bir [Azure depolama hesabı](../storage/storage-create-storage-account.md#create-a-storage-account) çoğaltılan veriler için.
    - Merhaba hesap standart olabilir veya [premium](../storage/storage-premium-storage.md).
    - Kaynak Yöneticisi'nde veya Klasik modda bir hesap ayarlayabilirsiniz.

3. [Bir hesap hazırlama](#prepare-for-automatic-discovery-and-push-installation) hello vCenter sunucusu veya vSphere ana bilgisayarları, böylece bu Site Recovery otomatik olarak algılayabilir VMware Vm'lerini.

## <a name="prepare-hello-configuration-server"></a>Merhaba yapılandırma sunucusunu hazırlama

1. Windows Server 2012 R2 yükleme ya da daha sonra bir VMware VM.
2. Merhaba VM listelenen erişim toohello URL'leri sahip olduğundan emin olun [Önkoşullar](#prerequisites).
3. Yükleme [VMware vSphere Powerclı 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1).


## <a name="prepare-for-automatic-discovery-and-push-installation"></a>Otomatik bulma ve anında iletme yükleme için hazırlama

- **Otomatik bulma için bir hesap hazırlama**: hello Site Recovery işlem sunucusu sanal makineleri otomatik olarak bulur. toodo vCenter sunucuları ve vSphere ESXi konakları erişebilir. Bu, Site kurtarma gereksinimlerini kimlik bilgileri.

    1. bir rolü toouse adanmış bir hesap oluşturun (Bu hello vCenter düzeyinde [izinleri](#vmware-account-permissions). Gibi bir ad verin **Azure_Site_Recovery**.
    2. Ardından, hello vSphere ana bilgisayar/vCenter sunucusu üzerinde bir kullanıcı oluşturun ve hello rol toohello kullanıcı atayın. Site Recovery dağıtımı sırasında bu kullanıcı hesabı belirtin.

- **Bir hesap toopush hello Mobility hizmeti hazırlama**: toopush hello Mobility hizmeti tooVMs istiyorsanız, hello işlem sunucusu tooaccess hello VM tarafından kullanılan bir hesabınızın olması gerekir. Merhaba hesabı yalnızca hello gönderme yüklemesi için kullanılır. Bir etki alanı veya yerel bir hesap kullanabilirsiniz:

    - Windows, bir etki alanı hesabı kullanmıyorsanız toodisable hello yerel makine üzerinde uzak kullanıcı erişim denetimi gerekir. Bu, hello kaydetmek altında toodo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, hello DWORD girdisi eklemek **LocalAccountTokenFilterPolicy**, 1 değerine sahip.
    - CLI Windows'dan tooadd hello kayıt defteri girdisini isterseniz, yazın:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
    - Linux için kök hello kaynak Linux sunucuda hello hesabı olmalıdır.

## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-hello-protection-goal"></a>Merhaba koruma hedefi seçin

İstediğinizi seçin, tooreplicate ve tooreplicate için istediğiniz.

1. Tıklatın **kurtarma Hizmetleri kasaları** > kasası.
2. Hello kaynak menüsü, tıklatın **Site Recovery** > **1. adım: altyapıyı hazırlama** > **koruma hedefi**.

    ![Hedefleri seçme](./media/site-recovery-vmware-to-azure/choose-goals.png)
3. İçinde **koruma hedefi**seçin **tooAzure** > **Evet, VMware vSphere hiper yönetici ile**.

    ![Hedefleri seçme](./media/site-recovery-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Merhaba kaynak ortamını ayarlama

Merhaba yapılandırma sunucusunu ayarlamayı, hello kasaya kaydetmek ve Vm'leri bulma.

1. Tıklatın **Site kurtarma** > **1. adım: altyapıyı hazırlama** > **kaynak**.
2. Yapılandırma sunucusu yoksa, tıklatın **+ yapılandırma sunucusu**.

    ![Kaynağı ayarlama](./media/site-recovery-vmware-to-azure/set-source1.png)
3. İçinde **Sunucu Ekle**, denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.
4. Merhaba Site Recovery birleşik Kurulumu yükleme dosyasını indirin.
5. Merhaba kasa kayıt anahtarını indirin. Birleşik Kurulum'u çalıştırdığınızda bu gerekir. Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.

   ![Kaynağı ayarlama](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Kurulumu çalıştırma Site Recovery birleşik

, Önce hello aşağıdaki başlayın, ardından birleşik Kurulum tooinstall hello yapılandırma sunucusu, hello işlem sunucusu ve hello ana hedef sunucusunda çalıştırın.
    - Hızlı bir video özeti

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - Merhaba yapılandırma sunucusunda VM, o hello sistem saati ile eşitlenir emin olun bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Eşleşmelidir. Önde 15 dakika ise veya arkasında kurulum başarısız olabilir.
    - Kurulum bir yerel yönetici hello yapılandırma sunucusundaki VM olarak çalıştırın.
    - TLS 1.0 hello VM etkin olduğundan emin olun.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Merhaba yapılandırma sunucusu da yüklenebilir [hello komut satırından](http://aka.ms/installconfigsrv).



### <a name="add-hello-account-for-automatic-discovery"></a>Otomatik bulma için Hello hesabı ekleyin

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="connect-toovmware-servers"></a>TooVMware sunucularına bağlanmak

ToovSphere ESXi konakları veya vCenter sunucuları, toodiscover VMware Vm'lerini bağlayın.

- Merhaba sunucuda hello vCenter sunucusu veya yönetici ayrıcalıkları olmayan bir hesapla vSphere ana bilgisayarları eklerseniz, hello hesabının etkin Bu ayrıcalıkları gerekir:
    - Datacenter, veri deposu, klasör, ana bilgisayar, ağ, kaynak, sanal makine, vSphere dağıtılmış anahtar.
    - Merhaba vCenter sunucusu depolama görünümleri izinleri olması gerekir.
- VMware sunucular eklediğinizde, 15 dakika alabilir veya onlar için daha uzun tooappear hello Portalı'nda.
tooallow Azure Site Recovery toodiscover şirket içi ortamınızda çalışan sanal makineler, VMware vCenter sunucusu veya Site Recovery ile vSphere ESXi konakları tooconnect gerekir.

Seçin **+ vCenter** toostart bir VMware vCenter sunucusu veya bir VMware vSphere ESXi konağı bağlanma.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

Site Recovery bağlayan tooVMware sunucuları hello kullanarak belirtilen ayarlarını ve sanal makineleri bulur.

## <a name="set-up-hello-target"></a>Merhaba hedefi ayarlama

Merhaba hedef ortamını ayarlama önce sahip olduğunuz denetleyin bir [Azure depolama hesabı ve ağ](#set-up-azure)

1. Tıklatın **altyapıyı hazırlama** > **hedef**, ve hello toouse istediğiniz Azure aboneliğini seçin.
2. Belirtin, hedef dağıtım modeli Resource Manager tabanlı veya Klasik olup.
3. Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.

   ![Hedef](./media/site-recovery-vmware-to-azure/gs-target.png)
4. Bir depolama hesabı veya ağı oluşturmadıysanız, tıklatın **+ depolama hesabı** veya **+ ağ**, toocreate bir Resource Manager hesabı ya da ağ satır içi.

## <a name="set-up-replication-settings"></a>Çoğaltma ayarlarını belirleme

Başlamadan önce hızlı bir video genel bakış alın:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. Yeni bir çoğaltma ilkesi toocreate tıklatın **Site Recovery altyapısı** > **çoğaltma ilkeleri** > **+ Çoğaltma İlkesi**.
2. İçinde **çoğaltma ilkesi oluşturun**, bir ilke adı belirtin.
3. İçinde **RPO eşik**, hello RPO sınırını belirtin. Bu değer, ne sıklıkta belirtir veri kurtarma noktaları oluşturulur. Sürekli çoğaltma bu sınırı aşarsa bir uyarı üretilir.
4. İçinde **kurtarma noktası bekletme**, ne kadar süre (saat olarak) belirtin hello bekletme penceresi olduğu için her kurtarma noktası. Çoğaltılan VM'ler olabilir bir pencerede tooany noktası kurtarıldı. Saat bekletme makineler için desteklenen too24 yukarı toopremium depolama ile standart depolama için 72 saat çoğaltılan.
5. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, belirtin ne sıklıkta (dakika cinsinden) uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktaları oluşturulur. Tıklatın **Tamam** toocreate hello ilkesi.

    ![Çoğaltma ilkesi](./media/site-recovery-vmware-to-azure/gs-replication2.png)
8. Yeni bir ilke oluşturduğunuzda, otomatik olarak hello yapılandırma sunucusu ile ilişkili. Varsayılan olarak, eşleşen bir ilkesi yeniden çalışma için otomatik olarak oluşturulur. Örneğin, hello çoğaltma ilkesi ise **rep İlkesi** hello geri dönme ilkesini sonra **rep İlkesi yeniden**. Bir azure'dan başlatana kadar bu ilkeyi kullanılmaz.  



## <a name="plan-capacity"></a>Kapasite planlama

1. Göre temel altyapınızı ayarladığınıza kapasite planlaması hakkında düşünün ve ek kaynaklar ihtiyacınız olup olmadığı şekil. [Daha fazla bilgi edinin](site-recovery-plan-capacity-vmware.md).
2. Kapasite planlaması bittiğinde, seçin **Evet** içinde **kapasite planlamasını tamamladınız?**

   ![Kapasite planlaması](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Sanal makineleri çoğaltma için hazırlama

Merhaba Mobility hizmeti tooreplicate istediğiniz tüm VMware VM'ler üzerinde yüklü olmalıdır. Çeşitli yollarla hello Mobility hizmeti yükleyebilirsiniz:

1. Merhaba işlem sunucusu anında yüklemesinden ile yükleyin. Bu yöntem tooprepare VM'ler toouse gerekir.
2. System Center Configuration Manager veya Azure automation DSC gibi dağıtım araçları kullanarak yükleyin.
3.  El ile yükleyin.

[Daha fazla bilgi](site-recovery-vmware-to-azure-install-mob-svc.md)


## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme

Başlamadan önce:

- Azure kullanıcı hesabınızın toohave belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) yeni bir sanal makine tooAzure tooenable çoğaltması.
- Ekleyin veya VM'ler değiştirdiğinizde, too15 dakika veya daha uzun değişiklikler tootake etkisi ve bunları alabilir tooappear hello Portalı'nda.
- VM için en son bulunan hello zaman denetimi **yapılandırma sunucularına** > **en son kişi**.
- Merhaba zamanlanmış bulma Vurgu hello yapılandırma sunucusu bekleyen olmadan VM'ler tooadd (tıklatın yok), tıklatıp **yenileme**.
- Bir VM gönderme yüklemesi için hazırlanmış, çoğaltma etkinleştirdiğinizde hello işlem sunucusu otomatik olarak hello Mobility hizmetini yükler.


### <a name="exclude-disks-from-replication"></a>Diskleri çoğaltmanın dışında tutma

Varsayılan olarak, bir makine üzerindeki tüm diskleri çoğaltılır. Diskleri çoğaltmanın dışında bırakabilirsiniz. Örneğin, geçici verileri ya da her zaman bir makine yeniledi veri tooreplicate disklerle istemeyebilirsiniz veya (örneğin pagefile.sys ya da SQL Server tempdb) uygulamasını yeniden başlatır.

### <a name="replicate-vms"></a>Vm'lerini çoğaltma

Başlamadan önce hızlı bir video genel bakış izleyin

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. **2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın.
2. İçinde **kaynak**seçin hello yapılandırma sunucusu.
3. İçinde **makine türü**seçin **sanal makineleri**.
4. İçinde **vCenter/vSphere hiper yönetici**hello vSphere ana yöneten hello vCenter sunucusu seçin veya hello konak seçin.
5. Merhaba işlem sunucusunu seçin. Herhangi bir ek işlem sunucusu oluşturmadıysanız bu hello yapılandırma sunucusu olacaktır. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. İçinde **hedef**hello aboneliği seçin ve hello vm'lerinde toocreate hello istediğiniz kaynak grubunu. Toouse (Yönetim), Klasik veya resource azure'da hello vm'lerinde için istediğiniz hello dağıtım modelini seçin.


7. Veri çoğaltmak için toouse istediğiniz hello Azure depolama hesabı seçin. Toouse ayarlamış bir hesap istemiyorsanız, yeni bir tane oluşturabilirsiniz.

8. Yük devretme sonrasında oluşturulduğunda select hello Azure ağ ve alt ağ toowhich Azure VM'ler bağlanır. Seçin **seçili makineler için Şimdi Yapılandır**, seçtiğiniz tooapply hello ağ ayarı tooall makineler için koruma. Seçin **daha sonra yapılandırma** tooselect hello makine başına Azure ağı. Varolan bir ağ toouse istemiyorsanız, bir tane oluşturabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. İçinde **sanal makineleri** > **sanal makine Seç**, tıklatın ve tooreplicate istediğiniz her bir makine seçin. Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. İçinde **özellikleri** > **özelliklerini yapılandırmak**seçin hello işlem sunucusu tooautomatically tarafından kullanılacak hello hesap hello makinede hello Mobility hizmeti yükleyin.
11. Varsayılan olarak tüm diskler çoğaltılır. Tıklatın **tüm diskleri** ve tooreplicate istemediğiniz tüm diskleri temizleyin. Daha sonra, **Tamam**'a tıklayın. Ek VM özellikleri daha sonra ayarlayabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication6.png)
11. İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, o hello çoğaltma ilkesi seçili doğru doğrulayın. Bir ilkeyi değiştirirseniz, değişiklikler uygulanan tooreplicating makine ve toonew makineleri olacaktır.
12. Etkinleştirme **çoklu VM tutarlılığını** toogather makineler çoğaltma grubuna isterseniz ve hello grubu için bir ad belirtin. Daha sonra, **Tamam**'a tıklayın. Şunlara dikkat edin:

    * Çoğaltma gruplarındaki makineler birlikte çoğaltılır ve kilitlenme tutarlı ve uygulamayla tutarlı kurtarma noktaları üzerinden başarısız olduğunda paylaşılan.
    * Böylece, iş yüklerini yansıtma sanal makineleri ve fiziksel sunucuları araya toplamak öneririz. Çoklu VM tutarlılığını etkinleştirmek iş yükü performansını etkileyebilir ve yalnızca makineler hello çalışıyorsa kullanılmalıdır aynı iş yükünü ve tutarlılık gerekir.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication7.png)
13. Tıklatın **çoğaltmasını etkinleştir**. Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**. Merhaba sonra **korumayı Sonlandır** iş çalıştırmaları hello makine yük devretme için hazır.

### <a name="view-and-manage-vm-properties"></a>VM özelliklerini görüntüleme ve yönetme

Hello VM özelliklerini doğrulayın ve istediğiniz değişiklikleri yapın öneririz.

1. Tıklatın **öğeleri çoğaltılan** > ve select hello makine. Merhaba **Essentials** dikey makineler ayarlarını ve durumu hakkında bilgileri gösterir.
2. İçinde **özellikleri**, çoğaltma görebilirsiniz ve Yük Devretme bilgilerini hello VM.
3. İçinde **işlem ve ağ** > **işlem özellikleri**, hello Azure VM adını ve hedef boyutu belirtebilirsiniz. Merhaba adı toocomply ile değiştirmek [Azure gereksinimleri](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) gerekiyorsa.
4. Merhaba hedef ağ, alt ağ ve toohello Azure VM atanacak IP adresi ayarlarını değiştirin:

   - Merhaba hedef IP adresini ayarlayabilirsiniz.

    - Bir adresi sağlamazsanız, yükü devredilen makine üzerinde hello DHCP kullanır.
    - Yük devretmede kullanılamayan bir adres ayarlarsanız yük devretme çalışmaz.
    - Merhaba hello test yük devretme ağı testinde Hello adresi varsa, yük devretme sınaması için aynı hedef IP adresi kullanılabilir.

   - ağ bağdaştırıcısı Hello sayısını hello hedef sanal makine için belirttiğiniz hello boyuta göre dikte edilir:

     - Merhaba hello kaynak makinedeki ağ bağdaştırıcısı sayısıdır hello ile aynı veya sayısından küçük, hello hello hedef makine boyutu için izin verilen bağdaştırıcıları sonra hello hedef olacaktır hello aynı sayıda bağdaştırıcıya hello kaynağı olarak.
     - Merhaba maksimum hedef boyutu kullanılır hello hello kaynak sanal makinenin bağdaştırıcı sayısı hello hedef boyutu için izin verilen hello sayıyı aşarsa.
     - Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hello hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa hello hedef makinenin iki bağdaştırıcısı gerekir. Merhaba kaynak makinenin iki bağdaştırıcısı varsa, ancak hello hedef boyut yalnızca bir destekler hello hedef makine yalnızca bir bağdaştırıcısı olur.     
   - Merhaba sanal makinede birden fazla ağ bağdaştırıcısı varsa bunların tümü toohello bağlanır aynı ağ.
   - Merhaba sanal makine birden çok ağ bağdaştırıcısı hello varsa, önce bir hello listede gösterilen hello haline gelir *varsayılan* hello Azure sanal makine ağ bağdaştırıcısı.
4. İçinde **diskleri**hello VM işletim sistemi görebilir ve hello veri diskler çoğaltılır.

#### <a name="managed-disks"></a>Yönetilen diskler

İçinde **işlem ve ağ** > **işlem özellikleri**, yük devretme tooAzure tooattach yönetilen diskleri tooyour makinede isterseniz "Yönetilen diskleri kullanımını" ayarı çok "Evet" Merhaba VM ayarlayabilirsiniz. Yönetilen diskleri hello VM disklerle ilişkilendirilmiş hello depolama hesaplarını yöneterek Azure Iaas VM'ler için disk yönetimi basitleştirir. [Yönetilen diskler hakkında daha fazla bilgi edinin.](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)

   - Oluşturulan ve ekli toohello sanal makinede yalnızca bir yük devretme tooAzure yönetilen disklerdir. Korumayı etkinleştirmek için şirket içi makineler verilerden tooreplicate toostorage hesapları devam eder.  Yönetilen diskler yalnızca hello Resource manager dağıtım modeli kullanılarak dağıtılan sanal makineleri için oluşturulabilir.  

   - "Yönetilen diskleri kullanımını" çok "Evet" ayarladığınızda, yalnızca hello kaynak grubundaki kullanılabilirlik kümeleri "Kullanım diskleri yönetilen" olarak ayarlanmış çok "Evet" seçime uygun olacaktır. Bu durum, yönetilen bir diske sahip sanal makineler yalnızca parçası "Yönetilen kullanım diskleri" özelliği ayarlanmış kullanılabilirlik kümeleri çok "Evet" olabilir çünkü. Kullanılabilirlik kümeleri, yük devretme hedefi toouse yönetilen disklerde göre "Yönetilen kullanım diskleri" özellik kümesi ile oluşturduğunuzdan emin olun.  Benzer şekilde, "Yönetilen diskleri kullanımını" çok "Hayır" ayarladığınızda, hello kaynak grubunda "Yönetilen diskleri kullanımını" özelliği çok "Hayır" olarak ayarlanmış yalnızca kullanılabilirlik kümeleri seçime uygun olacaktır. [Yönetilen diskler ve kullanılabilirlik kümeleri hakkında daha fazla bilgi edinin](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Merhaba depolama hesabı çoğaltma için kullanılan herhangi bir noktada zamanında depolama hizmeti şifrelemesi ile şifrelenmişse, yük devretme sırasında yönetilen diskleri oluşturma başarısız olur. Seçebilir ya da "Yönetilen diskleri kullanımını" çok "Hayır" ayarlayın ve yük devretme yeniden deneyin veya hello sanal makine için korumayı devre dışı bırakmak ve herhangi bir noktada zamandaki etkin depolama hizmeti şifrelemesi sahip değilse, tooa depolama hesabı koruyun.
  > [Depolama Hizmeti Şifrelemesi ve yönetilen diskler hakkında daha fazla bilgi edinin](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma


Her şeyi kurduktan sonra bir test yük devretme toomake her şeyin beklendiği gibi çalıştığından emin çalıştırın. Başlamadan önce hızlı bir video genel bakış Al
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. tek bir makineye üzerinden toofail içinde **ayarları** > **çoğaltılan öğeler**, hello VM tıklayın > **+ yük devretme testi** simgesi.

    ![Yük devretme sınaması](./media/site-recovery-vmware-to-azure/TestFailover.png)

1. bir kurtarma üzerinden toofail planlama **ayarları** > **kurtarma planları**, sağ hello planı > **yük devretme testi**. bir kurtarma planı toocreate [bu yönergeleri izleyin](site-recovery-create-recovery-plans.md).  

1. İçinde **yük devretme testi**seçin hello Azure ağ toowhich Azure Vm'lerinin yük devretme gerçekleştikten sonra bağlanır.

1. Tıklatın **Tamam** toobegin hello yük devretme. Merhaba VM tooopen üzerinde özelliklerini tıklayarak ya da hello ilerleme durumunu izleyebilirsiniz **yük devretme testi** kasa adı işinde > **ayarları** > **işleri**  >  **Site Recovery işleri**.

1. Hello yük devretme işlemi tamamlandıktan sonra ayrıca olması toosee hello çoğaltma Azure makine görünür hello Azure portalı > **sanal makineleri**. Bu hello VM toohello uygun ağ ve çalıştığını bağlı hello uygun boyutta olduğundan emin olmanız gerekir.

1. Varsa, [yük devretme sonrasında bağlantıları için hazır](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), mümkün tooconnect toohello Azure VM olmalıdır.

1. İşiniz bittiğinde tıklayın **temizleme yük devretme testi** hello kurtarma planı üzerinde. İçinde **notları**hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek ve kaydedin. Bu yük devretme testi sırasında oluşturulan hello VM'ler siler.

[Daha fazla bilgi edinin](site-recovery-test-failover-to-azure.md) yük devretme sınaması işlemlerini hakkında.


## <a name="vmware-account-permissions"></a>VMware hesabı izinleri

Site kurtarma erişim tooVMware hello işlem sunucusu tooautomatically bulmak için sanal makineleri ve yük devretme ve sanal makineleri geri dönmesi gerekir.

- **Geçiş**: herhangi bir zamanda bunları geri başarısız olmadan toomigrate VMware Vm'lerini tooAzure'ni yalnızca isterseniz, salt okunur rolüyle VMware hesabı kullanabilirsiniz. Bu tür bir rol, yük devretme çalıştırabilirsiniz ancak korumalı kaynak makineleri kapatmayı olamaz. Bu geçiş için gerekli değildir.
- **Replicate/Recover**: toodeploy (çoğaltılır, yük devretme, yeniden çalışma) tam çoğaltma hello hesabı oluşturma ve diskleri kaldırma gibi işlemleri yapabilir toorun olmalıdır isterseniz, üzerinde sanal makineleri vb. destekleyen.
- **Otomatik bulma**: en az bir salt okunur hesabı gereklidir.


**Görev** | **Gerekli hesap/rol** | **İzinler** | **Ayrıntılar**
--- | --- | --- | ---
**İşlem sunucusu VMware sanal makineleri otomatik olarak bulur.** | En az bir salt okunur kullanıcının gerekiyor | Veri Merkezi Nesne –> Propagate tooChild nesnesi, rol = salt okunur | Kullanıcı veri merkezi düzeyde atanan ve hello veri merkezinde erişim tooall hello nesnelere sahip.<br/><br/> toorestrict erişim, Ata hello **erişim yok** hello rolüyle **toochild yayılması** nesnesi, toohello alt nesneler (vSphere ana bilgisayarları, datastores, sanal makineleri ve ağları).
**Yük devretme** | En az bir salt okunur kullanıcının gerekiyor | Veri Merkezi Nesne –> Propagate tooChild nesnesi, rol = salt okunur | Kullanıcı veri merkezi düzeyde atanan ve hello veri merkezinde erişim tooall hello nesnelere sahip.<br/><br/> toorestrict erişim, Ata hello **erişim yok** hello rolüyle **toochild yayılması** toohello alt nesneleri (vSphere ana bilgisayarları, datastores, sanal makineleri ve ağları).<br/><br/> Geçiş amacıyla, ancak değil tam çoğaltma, yük devretme, yeniden çalışma için kullanışlıdır.
**Yük devretme ve yeniden çalışma** | Merhaba gerekli izinlere sahip bir rol (Azure_Site_Recovery) oluşturun ve hello rol tooa VMware kullanıcı veya grup atayın öneririz | Veri Merkezi Nesne –> Propagate tooChild nesnesi, rol Azure_Site_Recovery =<br/><br/> Veri deposu alanı Ayır ->, veri deposu, alt düzey dosya işlemleri göz atın, dosyayı kaldırmak, sanal makine dosyalarını güncelleştir<br/><br/> Ağ -> Ağ atama<br/><br/> Kaynak VM atamak tooresource havuzu ->, VM güç beslemeli geçirmek, VM güç beslemeli geçirme<br/><br/> Görevler oluşturma görevi, güncelleştirme görevi -><br/><br/> Sanal Makine Yapılandırma -><br/><br/> Sanal makine -> etkileşimde bulunma yanıt soru, cihaz bağlantısı ->, CD ortamı yapılandırmak, disket ortamı, kapatma, açma, VMware araçları yükleme yapılandırın<br/><br/> Sanal makine -> Stok Oluştur ->, kaydetme, kaydı<br/><br/> Sanal makine sağlama -> izin sanal makine indirme ->, sanal makine dosyalarını karşıya yükleme izin ver<br/><br/> Sanal makine anlık görüntüleri -> Kaldır anlık görüntüleri -> | Kullanıcı veri merkezi düzeyde atanan ve hello veri merkezinde erişim tooall hello nesnelere sahip.<br/><br/> toorestrict erişim, Ata hello **erişim yok** hello rolüyle **toochild yayılması** nesnesi, toohello alt nesneler (vSphere ana bilgisayarları, datastores, sanal makineleri ve ağları).


## <a name="next-steps"></a>Sonraki adımlar

Sonra çoğaltma hale getirmek ve çalışan, kesinti oluştuğunda tooAzure başarısız ve çoğaltılan hello verilerinden oluşturulan Azure Vm'lerinin. Toonormal işlemleri geri döndüğünde geri tooyour birincil konumu başarısız kadar iş yüklerini ve uygulamaları Azure, daha sonra erişebilirsiniz.

- [Daha fazla bilgi edinin](site-recovery-failover.md) yerine, farklı türlerde hakkında ve nasıl toorun bunları.
- Makineleri çoğaltmak yerine ve geri, başarısız olan geçiş [daha fazla bilgi](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [Yeniden çalışma hakkında okuyun](site-recovery-failback-azure-to-vmware.md), toofail arka ve çoğaltma Azure Vm'leri yedekleme toohello içi birincil site.

## <a name="third-party-software-notices-and-information"></a>Üçüncü taraf yazılım uyarılar ve bilgiler
Sağlamadığı Çevir veya yerelleştirme

Merhaba yazılımını ve bellenimini çalışır durumda hello Microsoft Ürün veya hizmet dayanır veya hello malzemesini içerir projeleri listelenen (topluca "üçüncü taraf kodu").  Microsoft, hello hello üçüncü taraf kodu değil özgün yazarı.  Hello özgün telif hakkı bildirimi ve lisansı altında Microsoft gibi üçüncü taraf kodu alındı, aşağıda belirtilen ayarlanır.

Bir bölümdeki Hello bilgiler üçüncü taraf bileşenleri hello projelerden aşağıda listelenen kod ilgili olduğu. Bu tür lisansları ve bilgi yalnızca bilgilendirme amacıyla sağlanır.  Bu üçüncü taraf kodu Microsoft yazılım lisans hello Microsoft Ürün veya hizmet koşulları altında Microsoft tarafından relicensed tooyou yapılıyor.  

Bölüm B Hello bilgilerinde kullanılabilir tooyou hello özgün lisans şartları altında Microsoft tarafından kurulan üçüncü taraf kodu bileşenleri ilgili olduğu.

Merhaba tam dosya hello üzerinde bulunan [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft tarafından uygulanır olup olmadığını, belirtilmeyen tüm hakları ayırır rıza ya da aksi takdirde.
