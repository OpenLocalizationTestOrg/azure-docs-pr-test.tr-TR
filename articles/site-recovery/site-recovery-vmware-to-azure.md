---
title: "VMware Vm'lerini Azure'a çoğaltma | Microsoft Docs"
description: "Azure depolama alanına VMware Vm'lerinde çalışan iş yükleri çoğaltmak için gereken adımları özetler"
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
ms.openlocfilehash: 8a312f3c1a65b2a9bb91abbfd8b18fb0ec0279b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-virtual-machines-to-azure-with-site-recovery"></a>VMware sanal makinelerini Site Recovery ile azure'a çoğaltma

> [!div class="op_single_selector"]
> * [Azure portal](site-recovery-vmware-to-azure.md)
> * [Azure klasik](site-recovery-vmware-to-azure-classic.md)


Bu makale, şirket içi VMware sanal makinelerini Azure'a çoğaltma açıklamaktadır kullanarak [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.

VMware Vm'lerini Azure'a (yalnızca yük devretme) geçirmek istiyorsanız, okuma [bu makalede](site-recovery-migrate-to-azure.md) daha fazla bilgi için.

POST açıklamaları ve soruları alt bu makalenin veya üzerinde [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="deployment-steps"></a>Dağıtım adımları

İşte yapmanız gerekenler:

1. Önkoşulları ve sınırlamaları doğrulayın.
2. Azure ağ ve depolama hesaplarını kurun.
3. Yapılandırma sunucusu olarak dağıtmak istediğiniz şirket içi makineyi hazırlayın.
4. Sanal makineleri otomatik bulma için kullanılacak VMware hesapları hazırlayın ve isteğe bağlı olarak için mobilite hizmetinin göndermeli.
4. Kurtarma Hizmetleri kasası oluşturun. Kasa yapılandırma ayarlarını içerir ve çoğaltmayı yönetir.
5. Kaynak ve hedef çoğaltma ayarlarını belirtin.
6. Çoğaltmak istediğiniz Vm'leri Mobility hizmeti dağıtın.
7. VM'ler için çoğaltmayı etkinleştirin.
7. Her şeyin beklendiği gibi çalıştığından emin olmak için bir yük devretme testi çalıştırın.

## <a name="prerequisites"></a>Ön koşullar

**Destek gereksinimi** | **Ayrıntılar**
--- | ---
**Azure** | Hakkında bilgi edinin [Azure gereksinimleri](site-recovery-prereq.md#azure-requirements)
**Şirket içi yapılandırma sunucusu** | Windows Server 2012 R2 çalıştıran bir VMware VM gerekir ya da daha sonra. Site Recovery dağıtımı sırasında bu sunucusu ayarlayın.<br/><br/> Varsayılan olarak işlem sunucusu ve ana hedef sunucusu Ayrıca bu VM yüklenir. Ölçeği artırma, ayrı bir işlem sunucusu gerekebilir ve yapılandırma sunucusu aynı gereksinimlerine sahiptir.<br/><br/> Bu bileşenler hakkında daha fazla bilgi [burada](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**Şirket içi VMware sunucuları** | 6.0, 5.5, 5.1 ile en son güncelleştirmeleri çalıştıran bir veya daha fazla VMware vSphere sunucuları. Sunucuları yapılandırma sunucusu (veya ayrı işlem sunucusu) aynı ağda yer.<br/><br/> En son güncelleştirmeleri 6.0 veya 5.5 çalıştıran konak yönetmek için bir vCenter sunucusu öneririz. Sürüm 6.0 dağıttığınızda 5.5 içinde kullanılabilir olan özellikler desteklenir.
**Şirket içi sanal makineleri** | Çoğaltmak istediğiniz VM'lerin [desteklenen işletim sistemi](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) çalıştırıyor olması ve [Azure önkoşullarına](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) uygun olması gerekir. VM VMware araçları çalışıyor olması gerekir.
**URL'leri** | Yapılandırma sunucusunun bu URL'leri erişimi olmalıdır:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> IP adresi tabanlı güvenlik duvarı kurallarına sahipseniz bu kuralların Azure ile iletişim kurmaya izin verdiğinden emin olun.<br/></br> [Azure Veri Merkezi IP Aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)'na ve HTTPS (443) bağlantı noktasına izin verin.<br/></br> Aboneliğinizin Azure bölgesi ve Batı ABD (Access Control ve Identity Management için kullanılır) için IP adresi aralıklarına izin verin.<br/><br/> MySQL yüklemek için bu URL'ye izin ver: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Mobility hizmeti** | Her çoğaltılmış VM'de yüklü.




## <a name="limitations"></a>Sınırlamalar

**Sınırlama** | **Ayrıntılar**
--- | ---
**Azure** | Depolama ve ağ hesapları, kasa ile aynı bölgede olmalıdır<br/><br/> Premium depolama hesabı kullanırsanız, çoğaltma günlüklerini depolamak için bir standart depolama hesabı da gerekir<br/><br/> Orta ve Güney Hindistan premium hesaplarına çoğaltma yapamaz.
**Şirket içi yapılandırma sunucusu** | VMware VM bağdaştırıcı türü VMXNET3 olmalıdır. Öyle değilse, [bu güncelleştirmeyi yükleyin](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> vSphere Powerclı 6.0 yüklenmesi gerekir.<br/><br> Makine bir etki alanı denetleyicisi olmamalıdır. Makinenin bir statik IP adresi olmalıdır.<br/><br/> Ana bilgisayar adı 15 karakter uzunluğunda olmalıdır veya daha az ve işletim sistemi İngilizce olmalıdır.
**VMware** | Yalnızca 5.5 özellikler vCenter 6.0 desteklenir. Site Recovery yeni vCenter desteklemez ve vSphere 6.0 özellikleri gibi vCenter VMotion'ı, sanal birimler ve depolama DRS arası.
**VM’ler** | Doğrulama [Azure VM sınırlamaları](site-recovery-prereq.md#azure-requirements)<br/><br/> Şifrelenmiş disklerle VM'ler veya UEFI/EFI Önyükleme olan VM'ler çoğaltma yapamaz.<br/><br> Paylaşılan disk kümelerini desteklenmez. Kaynak VM NIC ekibi oluşturma varsa, yük devretme sonrasında tek bir NIC'ye dönüştürülür.<br/><br/> Sanal makineleri bir iSCSI diski varsa, Site Recovery, VHD dosyasına yönelik Yük devretme sonrasında dönüştürür. İSCSI hedef Azure VM tarafından ulaşılabiliyorsa ona bağlanan ve onu ve VHD görür. Bu durumda, iSCSI hedefi bağlantısını kesin.<br/><br/> Aynı iş yükünü çalıştıran VM'ler birlikte bir tutarlı veri noktasına kurtarılır sağlar, çoklu VM tutarlılığını etkinleştirmek istiyorsanız, VM bağlantı noktası 20004 açın.<br/><br/> Windows C sürücüsünde yüklenmesi gerekir. İşletim sistemi diski, temel ve dinamik olmayan olması gerekir. Veri diski dinamik olabilir.<br/><br/> Linux/Etc/Hosts dosyaları vm'lerde yerel ana bilgisayar adı tüm ağ bağdaştırıcıları ile ilişkili IP adreslerini eşlemek giriş içermelidir. Ana bilgisayar adı, bağlama noktaları, aygıt adı, sistem yolu ve dosya adları (/ etc; / usr) İngilizce yalnızca olmalıdır.<br/><br/> Belirli türlerdeki [Linux depolama](site-recovery-support-matrix-to-azure.md#support-for-storage) desteklenir.<br/><br/>Oluşturma veya ayarlama **disk.enableUUID=true** VM Ayarları'nda. Böylece doğru bağlar ve tam çoğaltma olmadan yeniden çalışma sırasında yalnızca delta değişiklikler geri şirket içi aktarılır sağlar bu VMDK'ye, tutarlı bir UUID sağlar.

## <a name="set-up-azure"></a>Azure ayarlayın

1. [Bir Azure ağı ayarlama](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    - Yük devretme sonrasında oluşturulduğunda azure sanal makineleri bu ağda yer alır.
    - Bir ağda ayarlayabilirsiniz [Resource Manager](../resource-manager-deployment-model.md), ya da Klasik modda.

2. Ayarlanmış bir [Azure depolama hesabı](../storage/storage-create-storage-account.md#create-a-storage-account) çoğaltılan veriler için.
    - Hesap standart olabilir veya [premium](../storage/storage-premium-storage.md).
    - Kaynak Yöneticisi'nde veya Klasik modda bir hesap ayarlayabilirsiniz.

3. [Bir hesap hazırlama](#prepare-for-automatic-discovery-and-push-installation) vCenter sunucusu veya vSphere ana bilgisayarları, böylece bu Site Recovery otomatik olarak algılayabilir VMware Vm'lerini.

## <a name="prepare-the-configuration-server"></a>Yapılandırma sunucusu hazırlayın

1. Windows Server 2012 R2 yükleme ya da daha sonra bir VMware VM.
2. VM listelenmiş URL'lere erişimi olduğundan emin olun [Önkoşullar](#prerequisites).
3. Yükleme [VMware vSphere Powerclı 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1).


## <a name="prepare-for-automatic-discovery-and-push-installation"></a>Otomatik bulma ve anında iletme yükleme için hazırlama

- **Otomatik bulma için bir hesap hazırlama**: Site Recovery işlem sunucusu sanal makineleri otomatik olarak bulur. Bunu yapmak için Site Recovery vCenter sunucuları ve vSphere ESXi konakları erişebilmeniz için kimlik bilgileri gerekir.

    1. Adanmış bir hesap kullanmak için bir rol oluşturmak (Bu vCenter düzeyinde [izinleri](#vmware-account-permissions). Gibi bir ad verin **Azure_Site_Recovery**.
    2. Ardından, vSphere ana bilgisayar/vCenter sunucusu üzerinde bir kullanıcı oluşturun ve kullanıcıya rol atayın. Site Recovery dağıtımı sırasında bu kullanıcı hesabı belirtin.

- **Mobility hizmetinin gönderim için bir hesap hazırlama**: Mobility hizmeti sanal makineleri için itmek istiyorsanız, VM erişmek için işlem sunucusu tarafından kullanılan bir hesabınızın olması gerekir. Hesabı yalnızca gönderme yüklemesi için kullanılır. Bir etki alanı veya yerel bir hesap kullanabilirsiniz:

    - Windows, bir etki alanı hesabı kullanmıyorsanız yerel makine üzerinde uzak kullanıcı erişimi denetimini devre dışı bırakmak gerekir. Bu, altında kayıttaki yapmak için **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, DWORD girdisi ekleyin **LocalAccountTokenFilterPolicy**, 1 değerine sahip.
    - CLI üzerinden için Windows kayıt defteri girdisini eklemek istiyorsanız, yazın:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
    - Linux için hesabın kaynak Linux sunucusu kökünde olması gerekir.

## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-the-protection-goal"></a>Koruma hedefi seçme

Neleri çoğaltmak istediğinizi ve bunları nereye çoğaltacağınızı seçin.

1. Tıklatın **kurtarma Hizmetleri kasaları** > kasası.
2. Kaynak menüye tıklayın **Site Recovery** > **1. adım: altyapıyı hazırlama** > **koruma hedefi**.

    ![Hedefleri seçme](./media/site-recovery-vmware-to-azure/choose-goals.png)
3. İçinde **koruma hedefi**seçin **için Azure** > **Evet, VMware vSphere hiper yönetici ile**.

    ![Hedefleri seçme](./media/site-recovery-vmware-to-azure/choose-goals2.png)

## <a name="set-up-the-source-environment"></a>Kaynak ortamı ayarlama

Yapılandırma sunucusunu ayarlamayı, kasaya kaydetmek ve Vm'leri bulma.

1. Tıklatın **Site kurtarma** > **1. adım: altyapıyı hazırlama** > **kaynak**.
2. Yapılandırma sunucusu yoksa, tıklatın **+ yapılandırma sunucusu**.

    ![Kaynağı ayarlama](./media/site-recovery-vmware-to-azure/set-source1.png)
3. İçinde **Sunucu Ekle**, denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.
4. Site Recovery birleşik Kurulumu yükleme dosyasını indirin.
5. Kasa kayıt anahtarını indir Birleşik Kurulum'u çalıştırdığınızda bu gerekir. Anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.

   ![Kaynağı ayarlama](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Kurulumu çalıştırma Site Recovery birleşik

Başlayın, ardından birleştirilmiş yapılandırma sunucusuna işlem sunucusu ve ana hedef sunucusu yüklemek üzere kurulumu çalıştırmadan önce aşağıdakileri yapın.
    - Hızlı bir video özeti

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - VM yapılandırma sunucusundaki sistem saatinin eşitlendiğinden emin olun bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Eşleşmelidir. Önde 15 dakika ise veya arkasında kurulum başarısız olabilir.
    - Kurulum, VM yapılandırma sunucusunda yerel yönetici olarak çalıştırın.
    - TLS 1.0 VM etkin olduğundan emin olun.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Yapılandırma sunucusu da yüklenebilir [komut satırından](http://aka.ms/installconfigsrv).



### <a name="add-the-account-for-automatic-discovery"></a>Otomatik bulma hesabı Ekle

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="connect-to-vmware-servers"></a>VMware sunucularına bağlanmak

VMware sanal makinelerini bulmanız vSphere ESXi konakları veya vCenter sunucuları bağlanın.

- Sunucu üzerinde yönetici ayrıcalıklarına sahip olmayan bir hesapla vSphere ana bilgisayarları ve vCenter sunucusu eklerseniz, hesap etkin Bu ayrıcalıkları gerekir:
    - Datacenter, veri deposu, klasör, ana bilgisayar, ağ, kaynak, sanal makine, vSphere dağıtılmış anahtar.
    - VCenter sunucusu depolama görünümleri izinleri olması gerekir.
- VMware sunucular eklediğinizde, 15 dakika alabilir ya da sunumların portalda görünebilmesi daha uzun.
Azure Site Recovery, şirket içi ortamınızda çalışan sanal makineleri bulmak izin vermek için VMware vCenter Server veya vSphere ESXi konakları Site Recovery ile bağlanmanız gerekir.

Seçin **+ vCenter** bir VMware vCenter sunucusu veya bir VMware vSphere ESXi konağı bağlanma başlatmak için.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

Site Recovery belirtilen ayarları kullanarak VMware sunucularına bağlanır ve sanal makineleri bulur.

## <a name="set-up-the-target"></a>Hedefi ayarlama

Hedef ortamını ayarlama önce sahip olduğunuz denetleyin bir [Azure depolama hesabı ve ağ](#set-up-azure)

1. **Altyapıyı hazırlama** > **Hedef** seçeneklerine tıklayıp kullanmak istediğiniz Azure aboneliğini seçin.
2. Belirtin, hedef dağıtım modeli Resource Manager tabanlı veya Klasik olup.
3. Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.

   ![Hedef](./media/site-recovery-vmware-to-azure/gs-target.png)
4. Bir depolama hesabı veya ağı oluşturmadıysanız, tıklatın **+ depolama hesabı** veya **+ ağ**, bir kaynak yöneticisi hesabı oluşturun veya satır içi ağ.

## <a name="set-up-replication-settings"></a>Çoğaltma ayarlarını belirleme

Başlamadan önce hızlı bir video genel bakış alın:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. Yeni bir çoğaltma ilkesi oluşturmak için tıklatın **Site Recovery altyapısı** > **çoğaltma ilkeleri** > **+ Çoğaltma İlkesi**.
2. İçinde **çoğaltma ilkesi oluşturun**, bir ilke adı belirtin.
3. **RPO eşiği** bölümünde RPO limitini belirtin. Bu değer, ne sıklıkta belirtir veri kurtarma noktaları oluşturulur. Sürekli çoğaltma bu sınırı aşarsa bir uyarı üretilir.
4. İçinde **kurtarma noktası bekletme**, (saat olarak) ne kadar süreyle bekletme penceresi için her kurtarma noktası belirtin. Çoğaltılan VM'ler penceresinde herhangi bir noktaya kurtarılabilir. 24 saat bekletme için premium depolama ve standart depolama için 72 saat çoğaltılan makineler için desteklenir.
5. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, belirtin ne sıklıkta (dakika cinsinden) uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktaları oluşturulur. Tıklatın **Tamam** bir ilke oluşturmak için.

    ![Çoğaltma ilkesi](./media/site-recovery-vmware-to-azure/gs-replication2.png)
8. Yeni bir ilke oluşturduğunuzda, otomatik olarak yapılandırma sunucusu ile ilişkili. Varsayılan olarak, eşleşen bir ilkesi yeniden çalışma için otomatik olarak oluşturulur. Örneğin, çoğaltma ilkesi ise **rep İlkesi** geri dönme ilkesini sonra **rep İlkesi yeniden**. Bir azure'dan başlatana kadar bu ilkeyi kullanılmaz.  



## <a name="plan-capacity"></a>Kapasite planlama

1. Göre temel altyapınızı ayarladığınıza kapasite planlaması hakkında düşünün ve ek kaynaklar ihtiyacınız olup olmadığı şekil. [Daha fazla bilgi edinin](site-recovery-plan-capacity-vmware.md).
2. Kapasite planlaması bittiğinde, seçin **Evet** içinde **kapasite planlamasını tamamladınız?**

   ![Kapasite planlaması](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Sanal makineleri çoğaltma için hazırlama

Mobility hizmetinin çoğaltmak istediğiniz tüm VMware VM'ler üzerinde yüklü olmalıdır. Mobility hizmeti çeşitli yollarla yükleyebilirsiniz:

1. İşlem sunucusundan bir anında yükleme ile yükleyin. Bu yöntemi kullanmak için sanal makineleri hazırlamanız gerekir.
2. System Center Configuration Manager veya Azure automation DSC gibi dağıtım araçları kullanarak yükleyin.
3.  El ile yükleyin.

[Daha fazla bilgi](site-recovery-vmware-to-azure-install-mob-svc.md)


## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme

Başlamadan önce:

- Azure kullanıcı hesabınızın belirli sahip olması [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) yeni bir sanal makineye Azure çoğaltmayı etkinleştirmek için.
- Ekleyin veya VM'ler değiştirdiğinizde, 15 dakika veya daha uzun değişikliklerin etkili olması ve sunumların portalda görünebilmesi kadar sürebilir.
- Vm'lerde bulunan en son ne zaman denetleyebilir **yapılandırma sunucularına** > **en son kişi**.
- VM'ler için zamanlanmış bulma beklemeden eklemek için yapılandırma sunucusu vurgulayın (tıklatın yok), tıklatıp **yenileme**.
- Bir VM gönderme yüklemesi için hazırlanmış, çoğaltma etkinleştirdiğinizde işlem sunucusu Mobility hizmeti otomatik olarak yükler.


### <a name="exclude-disks-from-replication"></a>Diskleri çoğaltmanın dışında tutma

Varsayılan olarak, bir makine üzerindeki tüm diskleri çoğaltılır. Diskleri çoğaltmanın dışında bırakabilirsiniz. Örneğin, geçici veriler veya her zaman bir makine yeniledi veri disklerini çoğaltmak istemeyebilirsiniz veya (örneğin pagefile.sys ya da SQL Server tempdb) uygulamasını yeniden başlatır.

### <a name="replicate-vms"></a>Vm'lerini çoğaltma

Başlamadan önce hızlı bir video genel bakış izleyin

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. **2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın.
2. İçinde **kaynak**, yapılandırma sunucusu seçin.
3. İçinde **makine türü**seçin **sanal makineleri**.
4. İçinde **vCenter/vSphere hiper yönetici**vSphere ana yöneten vCenter sunucusu seçin veya konağı seçin.
5. İşlem sunucusu seçin. Herhangi bir ek işlem sunucusu oluşturmadıysanız bu yapılandırma sunucusu olacaktır. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. İçinde **hedef**, abonelik ve başarısız VM'ler üzerinde oluşturmak istediğiniz kaynak grubunu seçin. Devredilen sanal makineleri için Azure (Yönetim), Klasik veya resource kullanmak istediğiniz dağıtım modelini seçin.


7. Veri çoğaltmak için kullanmak istediğiniz Azure depolama hesabı seçin. Ayarlamış bir hesap kullanmak istemiyorsanız, yeni bir tane oluşturabilirsiniz.

8. Yük devretme sonrasında oluşturulan Azure VM'lerinin bağlanacağı Azure ağını ve alt ağını seçin. Koruma için seçtiğiniz tüm makinelere ağ ayarını uygulamak için **Seçili makineler için şimdi yapılandır**’ı seçin. Makineler için Azure ağını ayrı ayrı seçmek için **Daha sonra yapılandır**'ı seçin. Varolan bir ağı kullanmak istemiyorsanız, bir tane oluşturabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. **Sanal Makineler** > **Sanal makine seçin** seçeneklerine tıklayın ve çoğaltmak istediğiniz makineleri seçin. Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. İçinde **özellikleri** > **özelliklerini yapılandırma**, işlem sunucusu tarafından otomatik olarak makinede Mobility hizmeti yüklemek için kullanılacak hesabı seçin.
11. Varsayılan olarak tüm diskler çoğaltılır. Tıklatın **tüm diskleri** ve çoğaltmak için istemediğiniz tüm diskleri temizleyin. Daha sonra, **Tamam**'a tıklayın. Ek VM özellikleri daha sonra ayarlayabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication6.png)
11. İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, doğru Çoğaltma İlkesi'nin seçili olduğunu doğrulayın. Bir ilkeyi değiştirirseniz, değişiklikler makinenin çoğaltıldığını ve yeni makinelere uygulanır.
12. Etkinleştirme **çoklu VM tutarlılığını** makineler çoğaltma grubuna toplayın ve grup için bir ad belirtmek istiyorsanız. Daha sonra, **Tamam**'a tıklayın. Şunlara dikkat edin:

    * Çoğaltma gruplarındaki makineler birlikte çoğaltılır ve kilitlenme tutarlı ve uygulamayla tutarlı kurtarma noktaları üzerinden başarısız olduğunda paylaşılan.
    * Böylece, iş yüklerini yansıtma sanal makineleri ve fiziksel sunucuları araya toplamak öneririz. Çoklu VM tutarlılığını etkinleştirmek, iş yükü performansını etkileyebilir ve yalnızca makineler aynı iş yükünü çalıştırıyorsa ve tutarlılık ihtiyacınız varsa kullanılmalıdır.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication7.png)
13. Tıklatın **çoğaltmasını etkinleştir**. İlerleme durumunu izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**. **Korumayı Sonlandır** işi çalıştırıldıktan sonra makine yük devretme için hazırdır.

### <a name="view-and-manage-vm-properties"></a>VM özelliklerini görüntüleme ve yönetme

VM özelliklerini doğrulayın ve istediğiniz değişiklikleri yapın öneririz.

1. Tıklatın **öğeleri çoğaltılan** > ve makineyi seçin. **Essentials** dikey makineler ayarlarını ve durumu hakkında bilgileri gösterir.
2. **Özellikler** kısmında VM'nin çoğaltma ve yük devretme bilgilerini inceleyebilirsiniz.
3. **İşlem ve Ağ** > **İşlem özellikleri** seçeneklerinden Azure VM adını ve hedef boyutu belirtebilirsiniz. Gerekirse [Azure gereksinimleri](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) ile uyum sağlamak için adı değiştirin.
4. Hedef ağ, alt ağ ve Azure VM'ye atanacak IP adresi ayarlarını değiştirin:

   - Hedef IP adresini ayarlayabilirsiniz.

    - Bir IP adresi sağlamazsanız yük devredilen makine DHCP kullanır.
    - Yük devretmede kullanılamayan bir adres ayarlarsanız yük devretme çalışmaz.
    - Test Yük Devretme ağ adresi varsa, aynı hedef IP adresi yük devretme sınaması için kullanılabilir.

   - Ağ bağdaştırıcısı sayısı, hedef sanal makine için belirlediğiniz boyuta göre dikte edilir:

     - Hedef makine boyutu, daha sonra hedef izin bağdaştırıcı sayısı kaynak olarak aynı sayıda bağdaştırıcıya sahip olur daha kaynak makinedeki ağ bağdaştırıcısı sayısı aynı olarak ya da daha az ise.
     - Kaynak sanal makinenin bağdaştırıcı sayısı maksimum hedef boyutu kullanılır hedef boyutu için izin verilen sayıyı aşarsa.
     - Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa hedef makinenin iki bağdaştırıcısı olur. Kaynak makinenin iki bağdaştırıcısı varken hedef boyut yalnızca bir bağdaştırıcıyı destekliyorsa hedef makinenin bir bağdaştırıcısı olur.     
   - Sanal makinede birden fazla ağ bağdaştırıcısı varsa bunların tümü aynı ağa bağlanır.
   - Sanal makine birden çok ağ bağdaştırıcısına sahip sonra listede gösterilen birinci hale *varsayılan* Azure sanal makine ağ bağdaştırıcısı.
4. İçinde **diskleri**VM işletim sistemi görebilir ve veri diskleri çoğaltılır.

#### <a name="managed-disks"></a>Yönetilen diskler

İçinde **işlem ve ağ** > **işlem özellikleri**, azure'a yük devretme makinenizde yönetilen diskleri eklemek istiyorsanız, VM için "Evet" ayarı "Yönetilen diskleri kullanımını" ayarlayabilirsiniz. Yönetilen diskler, VM diskleriyle ilişkilendirilmiş depolama hesaplarını yöneterek Azure IaaS VM'leri için disk yönetimini kolaylaştırır. [Yönetilen diskler hakkında daha fazla bilgi edinin.](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)

   - Yönetilen diskler yalnızca Azure'a yük devretme sonrasında oluşturulur ve sanal makineye eklenir. Koruma etkinleştirildikten sonra şirket içi makinelerdeki veriler depolama hesaplarında çoğaltılmaya devam eder.  Yönetilen diskler yalnızca Resource Manager dağıtım modeli kullanılarak dağıtılan sanal makineler için oluşturulabilir.  

   - "Yönetilen diskleri kullan" ayarını "Evet" olarak belirlediğinizde yalnızca kaynak grubundaki "Yönetilen diskleri kullan" ayarı "Evet" olarak belirlenmiş kullanılabilirlik kümeleri seçilebilir. Bunu nedeni yönetilen disklere sahip sanal makinelerin yalnızca "Yönetilen diskleri kullan" özelliği "Evet" olarak belirlenmiş kullanılabilirlik kümelerinin parçası olmasıdır. "Yönetilen diskleri kullan" özelliğiyle kullanılabilirlik kümelerini, yük devretme sırasında yönetilen diskleri kullanma isteğinize göre belirlendiğinden emin olun.  Benzer şekilde "Yönetilen diskleri kullan" ayarını "Hayır" olarak belirlediğinizde yalnızca kaynak grubundaki "Yönetilen diskleri kullan" özelliği "Hayır" olarak belirlenmiş kullanılabilirlik kümeleri seçilebilir. [Yönetilen diskler ve kullanılabilirlik kümeleri hakkında daha fazla bilgi edinin](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Çoğaltma için kullanılan depolama hesabı herhangi bir zamanda Depolama Hizmeti Şifrelemesiyle şifrelendiyse yük devretme sırasında yönetilen disk oluşturma işlemi başarısız olacaktır. "Yönetilen diskleri kullan" özelliğini "Hayır" olarak belirleyip yük devretmeyi tekrar deneyebilir veya sanal makine için korumayı devre dışı bırakıp Depolama Hizmeti Şifrelemesi etkinleştirilmemiş bir depolama hesabında korumaya alabilirsiniz.
  > [Depolama Hizmeti Şifrelemesi ve yönetilen diskler hakkında daha fazla bilgi edinin](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma


Her şeyi kurduktan sonra emin olmak için bir yük devretme testi her şeyin beklendiği gibi çalışmaktadır. Başlamadan önce hızlı bir video genel bakış Al
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. İçinde tek bir makineye vermesine **ayarları** > **çoğaltılan öğeler**, VM tıklayın > **+ yük devretme testi** simgesi.

    ![Yük devretme sınaması](./media/site-recovery-vmware-to-azure/TestFailover.png)

1. Kurtarma planında yük devretme için **Ayarlar** > **Kurtarma Planları** seçeneklerinde plana sağ tıklayıp **Yük Devretme Testi**'ne tıklayın. Kurtarma planı oluşturmak için [aşağıdaki yönergeleri uygulayın](site-recovery-create-recovery-plans.md).  

1. İçinde **yük devretme testi**, Azure Vm'lerinin Azure ağa bağlı olacak yük devretme gerçekleştikten sonra seçin.

1. Yük devretmeyi başlatmak için **Tamam**'a tıklayın. Özelliklerini açmak için VM'ye veya üzerinde tıklayarak ilerleme durumunu izleyebilirsiniz **yük devretme testi** kasa adı işinde > **ayarları** > **işleri** > **Site Recovery işleri**.

1. Yük devretme tamamlandıktan sonra çoğaltılan makineyi Azure portalı > **Sanal Makineler** kısmında da görmeniz gerekir. VM'nin uygun boyutta olduğundan, uygun bir ağa bağlandığından ve çalıştığından emin olmanız gerekir.

1. [Yük devretme sonrasındaki bağlantılar için hazırlık yaptıysanız](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) Azure VM'ye bağlanabilmeniz gerekir.

1. İşiniz bittiğinde kurtarma planındaki **Temizleme testi yük devretme** öğesine tıklayın. İçinde **notları**, kaydetme ve yük devretme testiyle ilişkili gözlemlerinizi kaydetmek. Bu yük devretme testi sırasında oluşturulan sanal makineleri siler.

[Daha fazla bilgi edinin](site-recovery-test-failover-to-azure.md) yük devretme sınaması işlemlerini hakkında.


## <a name="vmware-account-permissions"></a>VMware hesabı izinleri

Site Recovery, sanal makineleri otomatik olarak bulmak üzere işlem sunucusu için ve yük devretme ve sanal makineleri geri dönmesi için VMware erişimi olmalıdır.

- **Geçiş**: yalnızca herhangi bir zamanda bunları geri başarısız olmadan VMware Vm'lerini Azure'a geçirmek istiyorsanız, bir salt okunur rolüyle VMware hesabı kullanabilirsiniz. Bu tür bir rol, yük devretme çalıştırabilirsiniz ancak korumalı kaynak makineleri kapatmayı olamaz. Bu geçiş için gerekli değildir.
- **Replicate/Recover**: tam çoğaltma (çoğaltılır, yük devretme, yeniden çalışma) dağıtmak istiyorsanız hesap oluşturma ve diskler, sanal makineleri vb. üzerinde başlatırken kaldırma gibi işlemleri çalıştırabilir ve olmalıdır.
- **Otomatik bulma**: en az bir salt okunur hesabı gereklidir.


**Görev** | **Gerekli hesap/rol** | **İzinler** | **Ayrıntılar**
--- | --- | --- | ---
**İşlem sunucusu VMware sanal makineleri otomatik olarak bulur.** | En az bir salt okunur kullanıcının gerekiyor | Veri Merkezi Nesne –> Propagate alt nesne için rol = salt okunur | Kullanıcı veri merkezi düzeyde atanan ve veri merkezinde tüm nesnelere erişimi vardır.<br/><br/> Erişimi kısıtlamak için Ata **erişim yok** rolüyle **alt Propagate** (vSphere ana bilgisayarları, datastores, sanal makineleri ve ağları) alt nesneleri için nesne.
**Yük devretme** | En az bir salt okunur kullanıcının gerekiyor | Veri Merkezi Nesne –> Propagate alt nesne için rol = salt okunur | Kullanıcı veri merkezi düzeyde atanan ve veri merkezinde tüm nesnelere erişimi vardır.<br/><br/> Erişimi kısıtlamak için Ata **erişim yok** rolüyle **alt Propagate** (vSphere ana bilgisayarları, datastores, sanal makineleri ve ağları) alt nesneleri için nesne.<br/><br/> Geçiş amacıyla, ancak değil tam çoğaltma, yük devretme, yeniden çalışma için kullanışlıdır.
**Yük devretme ve yeniden çalışma** | Gerekli izinlere sahip bir rol (Azure_Site_Recovery) oluşturun ve bir VMware kullanıcı veya grup rol atamak öneririz | Veri Merkezi Nesne –> Propagate alt nesne için rol Azure_Site_Recovery =<br/><br/> Veri deposu alanı Ayır ->, veri deposu, alt düzey dosya işlemleri göz atın, dosyayı kaldırmak, sanal makine dosyalarını güncelleştir<br/><br/> Ağ -> Ağ atama<br/><br/> Kaynak VM atamak için kaynak havuzu ->, VM güç beslemeli geçirmek, VM güç beslemeli geçirme<br/><br/> Görevler oluşturma görevi, güncelleştirme görevi -><br/><br/> Sanal Makine Yapılandırma -><br/><br/> Sanal makine -> etkileşimde bulunma yanıt soru, cihaz bağlantısı ->, CD ortamı yapılandırmak, disket ortamı, kapatma, açma, VMware araçları yükleme yapılandırın<br/><br/> Sanal makine -> Stok Oluştur ->, kaydetme, kaydı<br/><br/> Sanal makine sağlama -> izin sanal makine indirme ->, sanal makine dosyalarını karşıya yükleme izin ver<br/><br/> Sanal makine anlık görüntüleri -> Kaldır anlık görüntüleri -> | Kullanıcı veri merkezi düzeyde atanan ve veri merkezinde tüm nesnelere erişimi vardır.<br/><br/> Erişimi kısıtlamak için Ata **erişim yok** rolüyle **alt Propagate** (vSphere ana bilgisayarları, datastores, sanal makineleri ve ağları) alt nesneleri için nesne.


## <a name="next-steps"></a>Sonraki adımlar

Azure'a yük devretme ve çoğaltılmış verilerinden oluşturulan Azure Vm'lerinin kesinti oluştuğunda çoğaltmayı ayarlama ve çalıştırma, aldıktan sonra. Normal çalışma dönüldüğünde birincil konumunuz başarısız kadar iş yüklerini ve uygulamaları Azure, daha sonra erişebilirsiniz.

- [Daha fazla bilgi edinin](site-recovery-failover.md) farklı türdeki yük devretmeler ve bunları çalıştırma hakkında.
- Makineleri çoğaltmak yerine ve geri, başarısız olan geçiş [daha fazla bilgi](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [Yeniden çalışma hakkında okuyun](site-recovery-failback-azure-to-vmware.md), geri dönecek ve Azure Vm'lerini geri içi birincil siteye çoğaltma.

## <a name="third-party-software-notices-and-information"></a>Üçüncü taraf yazılım uyarılar ve bilgiler
Sağlamadığı Çevir veya yerelleştirme

Microsoft ürünü veya hizmetinde çalışan bellenim ve yazılım dayanır veya malzeme aşağıda listelenen projelerden birleştirir (topluca "üçüncü taraf kodu").  Microsoft, üçüncü taraf kodu değil özgün yazarı almıştır.  Özgün telif hakkı bildirimi ve lisans altında Microsoft gibi üçüncü taraf kodu alındı, aşağıda belirtilen ayarlanır.

Bir bölümdeki bilgiler, aşağıda listelenen projelerden üçüncü taraf kodu bileşenleri ile ilgili. Bu tür lisansları ve bilgi yalnızca bilgilendirme amacıyla sağlanır.  Bu üçüncü taraf kodu size Microsoft tarafından Microsoft Ürün veya hizmet için Microsoft Yazılımı Lisans koşulları altında relicensed.  

Bölüm B bilgileri size Microsoft tarafından özgün lisans koşullarına sunulmaktadır üçüncü taraf kodu bileşenleri ilgili olduğu.

Tam dosya üzerinde bulunabilir [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft tarafından uygulanır olup olmadığını, belirtilmeyen tüm hakları ayırır rıza ya da aksi takdirde.
