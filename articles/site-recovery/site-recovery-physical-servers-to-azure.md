---
title: "aaaReplicate fiziksel sunucuları tooAzure | Microsoft Docs"
description: "Nasıl toodeploy Azure Site Recovery tooorchestrate çoğaltma, yük devretme ve kurtarma işlemlerini şirket içi Windows/Linux fiziksel sunucuları tooAzure hello Azure portal kullanarak açıklar"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: physical-walkthrough-overview
ms.openlocfilehash: cf5928fb631f6858d57b27f6f21babc312714e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
---
# <a name="replicate-physical-machines-tooazure-by-using-site-recovery"></a>Site RECOVERY'yi kullanarak fiziksel makineleri tooAzure Çoğalt


Bu makalede nasıl tooreplicate fiziksel makineleri tooAzure hello Azure Site Recovery hizmeti hello Azure portal kullanarak şirket içi açıklanmaktadır.

Toomigrate fiziksel makineleri tooAzure (yalnızca yük devretme), okuma istiyorsanız [tooAzure Site Recovery ile geçirmek](site-recovery-migrate-to-azure.md) toolearn daha fazla.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Ön koşullar

**Destek gereksinimi** | **Ayrıntılar**
--- | ---
**Azure** | [Azure gereksinimleri](site-recovery-prereq.md#azure-requirements) hakkında bilgi edinin.
**Şirket içi yapılandırma sunucusu** | Şirket içi makineyi (fiziksel veya VMware VM) çalıştıran Windows Server 2012 R2 veya üstü. Site Recovery dağıtımı sırasında hello yapılandırma sunucusu ayarlayın.<br/><br/> Varsayılan olarak, hello işlem sunucusu ve ana hedef sunucusu bu makinede de yüklenir. Ölçeği artırma, ayrı bir işlem sunucusu gerekebilir ve hello sahip olduğunda hello yapılandırma sunucusuyla aynı gereksinimleri.<br/><br/> Bu bileşenler hakkında daha fazla bilgi [hello kaynak ortamını ayarlama](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**Şirket içi sanal makineleri** | İstediğiniz tooreplicate çalışıyor makineler bir [işletim sistemi desteklenen](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) ve uygun olması [Azure önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL'leri** | Merhaba yapılandırma sunucusu toothese URL'leri erişmesi gereken:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin verdiğinden emin olun.<br/></br> Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653) ve hello HTTPS (443 numaralı) bağlantı noktası.<br/></br> IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.<br/><br/> Merhaba MySQL yüklemek için bu URL'ye izin ver: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Mobility hizmeti** | Bu hizmeti yükleyen tooreplicate istediğiniz her makinede.

## <a name="limitations"></a>Sınırlamalar

**Sınırlama** | **Ayrıntılar**
--- | ---
**Azure** | Depolama ve ağ hesapları hello olmalıdır hello kasasıyla aynı bölgede.<br/><br/> Premium depolama hesabı kullanırsanız, standart bir etmeniz hesap toostore çoğaltma günlüklerini depolamak.<br/><br/> Orta ve Güney Hindistan toopremium hesapları çoğaltma yapamaz.
**Şirket içi yapılandırma sunucusu** | VMware VM üzerinden hello yapılandırma sunucusu yüklerseniz, hello VM bağdaştırıcı türü VMXNET3 olmalıdır. Öyle değilse, [bu güncelleştirmeyi yükleyin](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> VMware VM kullanıyorsanız, üzerinde vSphere Powerclı 6.0 yüklü olmalıdır.<br/><br> Merhaba makine bir etki alanı denetleyicisi olmaması gerekir.<br/><br/> Merhaba makine statik bir IP adresi olmalıdır.<br/><br/> Merhaba ana bilgisayar adı 15 karakter uzunluğunda olmalıdır veya daha az hello işletim sistemi İngilizce olmalıdır.
**Çoğaltılan makineler** | Doğrulama [Azure VM sınırlamaları](site-recovery-prereq.md#azure-requirements).<br/><br/> Aynı iş yükünü toobe kurtarılan hello çalışan sanal makinelerin sağlar tooenable çoklu VM tutarlılığını istiyorsanız birlikte tooa tutarlı veri noktası, bağlantı noktası 20004 hello makinede açın.<br/><br/> Belirli türlerdeki [Linux depolama](site-recovery-support-matrix-to-azure.md#support-for-storage) desteklenir.
**İlk duruma döndürme** | Azure tooa fiziksel makineden kapatamazsınız. Yük devretme sonrasında toobe mümkün toofail geri tooon içi istiyorsanız, böylece geri tooa VMware VM başarısız olabilir bir VMware ortamı gerekir.


## <a name="set-up-azure"></a>Azure ayarlayın

1. [Bir Azure ağı ayarlama](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

      a. Yük devretme sonrasında oluşturulduğunda azure sanal makineleri bu ağda yerleştirilir.

      b. Azure ağında ayarlayabilirsiniz [Resource Manager](../resource-manager-deployment-model.md) veya Klasik modda.

2. Ayarlanmış bir [Azure depolama hesabı](../storage/storage-create-storage-account.md#create-a-storage-account) çoğaltılan veriler için.

    a. Merhaba hesap standart olabilir veya [premium](../storage/storage-premium-storage.md).

    b. Kaynak Yöneticisi'nde veya Klasik modda bir hesap ayarlayabilirsiniz.

## <a name="prepare-hello-configuration-server"></a>Merhaba yapılandırma sunucusunu hazırlama

1. Windows Server 2012 R2 veya sonraki bir şirket içi fiziksel sunucu veya bir VMware VM yükleyin.

2. Merhaba makine listelenen erişim toohello URL'leri sahip olduğundan emin olun [Önkoşullar](#prerequisites).

## <a name="prepare-for-mobility-service-installation"></a>Mobility hizmeti yüklemesi için hazırlama

Toopush hello Mobility hizmeti tooa fiziksel makine istiyorsanız hello işlem sunucusu tooaccess hello makineler tarafından kullanılan bir hesabınızın olması gerekir. Merhaba hesabı yalnızca hello gönderme yüklemesi için kullanılır. Bir etki alanı veya yerel bir hesap kullanabilirsiniz:

  - Windows, bir etki alanı hesabı kullanmıyorsanız toodisable hello yerel makine üzerinde uzak kullanıcı erişim denetimi gerekir. toodo hello defterinde altında bu **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, hello DWORD girdisi eklemek **LocalAccountTokenFilterPolicy**, 1 değerine sahip. Windows için bir komut satırı arabiriminden tooadd hello kayıt defteri girdisini istiyorsanız yazın:

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - Linux için kök kullanıcının hello kaynak Linux sunucuda hello hesabı olmalıdır.


## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-hello-protection-goal"></a>Merhaba koruma hedefi seçin

Ne seçin tooreplicate ve tooreplicate için istediğiniz istiyor.

1. Tıklatın **kurtarma Hizmetleri kasaları** > **kasa**.
2. Merhaba üzerinde **kaynak** menüsünde tıklatın **Site Recovery** > **altyapıyı hazırlama** > **koruma hedefi**.

    ![Hedefleri seçme](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. İçinde **koruma hedefi**seçin **tooAzure** > **değil sanallaştırılmış / diğer**.


## <a name="set-up-hello-source-environment"></a>Merhaba kaynak ortamını ayarlama

Merhaba yapılandırma sunucusunu ayarlamayı, hello kasaya kaydetmek ve Vm'leri bulma.

1. Tıklatın **Site kurtarma** > **altyapıyı hazırlama** > **kaynak**.
2. Yapılandırma sunucusu yoksa, tıklatın **+ yapılandırma sunucusu**.

    ![Kaynağı ayarlama](./media/site-recovery-vmware-to-azure/set-source1.png)

3. İçinde **Sunucu Ekle**, denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.
4. Merhaba karşıdan **Site Recovery birleşik Kurulumu** yükleme dosyası.
5. Merhaba karşıdan **kasa kayıt anahtarını**. Birleşik Kurulum'u çalıştırdığınızda, bu anahtar gerekir. Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.

   ![Kaynağı ayarlama](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Kurulumu çalıştırma Site Recovery birleşik

Başlamadan önce aşağıdaki hello:

- Hızlı bir video genel bakış alın. (Merhaba video açıklar tooreplicate VMware Vm'lerini ancak hello işleminin nasıl fiziksel makine çoğaltma için benzer.)

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- Merhaba configuration server makinesinde bu hello sistem saati ile eşitlenir emin olun bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Önde 15 dakika ise veya arkasında kurulum başarısız olabilir.
- Kurulum hello configuration server makinesinde yerel yönetici olarak çalıştırın.
- TLS 1.0 hello makinede etkin olduğundan emin olun.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Merhaba yapılandırma sunucusu da yüklenebilir [hello komut satırından](http://aka.ms/installconfigsrv).


## <a name="set-up-hello-target-environment"></a>Merhaba hedef ortamını ayarlama

Merhaba hedef ortamını ayarlama önce toomake emin denetleyin bir [Azure depolama hesabı ve ağ](#set-up-azure).

1. Tıklatın **altyapıyı hazırlama** > **hedef**, ve hello toouse istediğiniz Azure aboneliğini seçin.
2. Hedef dağıtım modeli Resource Manager veya Klasik olup olmadığını belirtin.
3. Site Recovery, bir veya birden çok uyumlu Azure depolama hesapları ve ağlar sahip olduğunuzdan emin toomake denetler.

   ![Hedef](./media/site-recovery-vmware-to-azure/gs-target.png)

4. Bir depolama hesabı veya ağı oluşturmadıysanız, tıklatın **+ depolama hesabı** veya **+ ağ** toocreate bir Resource Manager hesabı ya da ağ satır içi.

## <a name="set-up-replication-settings"></a>Çoğaltma ayarlarını belirleme

Başlamadan önce hızlı bir video genel bakış alın. (Merhaba video açıklar tooreplicate VMware Vm'lerini ancak hello işleminin nasıl fiziksel makine çoğaltma için benzer.)

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. Yeni bir çoğaltma ilkesi toocreate tıklatın **Site Recovery altyapısı** > **çoğaltma ilkeleri** > **+ Çoğaltma İlkesi**.
2. İçinde **çoğaltma ilkesi oluşturun**, bir ilke adı belirtin.
3. İçinde **RPO eşik**, hello RPO sınırını belirtin. Bu değer, ne sıklıkta belirtir veri kurtarma noktaları oluşturulur. Sürekli çoğaltma bu sınırı aşarsa bir uyarı üretilir.
4. İçinde **kurtarma noktası bekletme**, ne kadar süre (saat olarak) belirtin hello bekletme penceresi olduğu için her kurtarma noktası. Çoğaltılan VM'ler olabilir bir pencerede tooany noktası kurtarıldı. Too24 saat bekletme makineler çoğaltılmış toopremium depolama için desteklenir. Too72 saat bekletme makineler çoğaltılmış toostandard depolama için desteklenir.
5. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, belirtin ne sıklıkta (dakika cinsinden) uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktaları oluşturulur. Tıklatın **Tamam** toocreate hello ilkesi.

    ![Çoğaltma ilkesi](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. Yeni bir ilke oluşturduğunuzda, otomatik olarak hello yapılandırma sunucusu ile ilişkili. Varsayılan olarak, eşleşen bir ilkesi yeniden çalışma için otomatik olarak oluşturulur. Örneğin, hello çoğaltma ilkesi ise **rep İlkesi**, hello geri dönme ilkesini ise **rep İlkesi yeniden**. Bir azure'dan başlatana kadar bu ilkeyi kullanılmaz.  


## <a name="plan-capacity"></a>Kapasite planlama

1. Temel altyapınızı sahip olduğunuza göre kapasite planlaması hakkında düşünün ve ek kaynaklar ihtiyacınız olup olmadığı şekil. [Daha fazla bilgi edinin](site-recovery-plan-capacity-vmware.md).
2. Kapasite planlaması bittiğinde, seçin **Evet** içinde **kapasite planlamasını tamamladınız?**

   ![Kapasite planlaması](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>Sanal makineleri çoğaltma için hazırlama

Tooreplicate istediğiniz tüm makineler hello Mobility hizmetinin yüklü olması gerekir. Çeşitli yollarla hello Mobility hizmeti yükleyebilirsiniz:

- Merhaba işlem sunucusu anında yüklemesinden ile Merhaba hizmetini yükleyin. Bu yöntem öncelikli toouse tooprepare makineniz olması gerekir.
- System Center Configuration Manager veya Azure Otomasyonu istenen durum yapılandırması gibi dağıtım araçlarını kullanarak Hello hizmetini yükleyin.
- Merhaba hizmetini el ile yükleyin.

[Daha fazla bilgi edinin](site-recovery-vmware-to-azure-install-mob-svc.md).


## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme

Başlamadan önce:

- Azure kullanıcı hesabınızın toohave belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) yeni bir sanal makine tooAzure tooenable çoğaltması.
- Ekleyin veya VM'ler değiştirdiğinizde, too15 dakika veya daha uzun değişiklikler tootake etkisi ve bunları alabilir tooappear hello Portalı'nda.
- VM için en son bulunan hello zaman denetimi **yapılandırma sunucularına** > **en son kişi**.
- Merhaba zamanlanmış bulma Vurgu hello yapılandırma sunucusu bekleyen olmadan VM'ler tooadd (tıklatın yok), tıklatıp **yenileme**.
- Bir VM gönderme yüklemesi için hazırlanmış, çoğaltma etkinleştirdiğinizde hello işlem sunucusu otomatik olarak hello Mobility hizmetini yükler.
- Hızlı bir video genel bakış alın. (Merhaba video açıklar tooreplicate VMware Vm'lerini ancak hello işleminin nasıl fiziksel makine çoğaltma için benzer.)

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a>Diskleri çoğaltmanın dışında tutma

Varsayılan olarak, bir makinedeki tüm diskler çoğaltılır. Diskleri çoğaltmanın dışında bırakabilirsiniz. Örneğin, geçici verileri tooreplicate disklerle istemeyebilirsiniz veya her yeniledi verileri (örneğin, pagefile.sys ya da SQL Server tempdb) bir makineye veya uygulama başlatılma süresi.

### <a name="replicate-vms"></a>Vm'lerini çoğaltma

1. Tıklatın **uygulama çoğaltma** > **kaynak**.
2. İçinde **kaynak**seçin **şirket içi**.
3. İçinde **kaynak konumu**seçin hello yapılandırma sunucusunun adı.
4. İçinde **makine türü**seçin **fiziksel makineleri**.
5. İçinde **işlem sunucusu**, hello işlem sunucusunu seçin. Herhangi bir ek işlem sunucusu oluşturmadıysanız, bu sunucu hello yapılandırma sunucusudur. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-physical-to-azure/chooseVM.png)

6. İçinde **hedef**seçin hello **abonelik** ve hello **kaynak grubu** istediğiniz toocreate hello Azure Vm'lerinin yük devretme sonrasında. Merhaba dağıtımı seçin model Azure toouse istediğiniz (Klasik veya Resource Manager) hello başarısız oldu-VMs üzerinden için.

7. Veri çoğaltmak için toouse istediğiniz hello Azure depolama hesabı seçin. Toouse ayarlamış bir hesap istemiyorsanız, yeni bir tane oluşturabilirsiniz.

8. Select hello **Azure ağ** ve **alt** toowhich Azure Vm'lerinin yük devretme sonrasında bağlanın. Seçin **seçili makineler için Şimdi Yapılandır** seçtiğiniz tooapply hello ağ ayarı tooall makineler için koruma. Seçin **daha sonra yapılandırma** tooselect hello makine başına Azure ağı. Varolan bir ağ toouse istemiyorsanız, bir tane oluşturabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-physical-to-azure/targetsettings.png)

9. İçinde **fiziksel makineleri**, tıklatın **+ fiziksel makine** ve hello girin **adı** ve **IP adresi**. Merhaba işletim sistemi seçin hello makinenin tooreplicate istiyor. Makineler bulunan ve hello listede gösterilen kadar birkaç dakika sürer.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-physical-to-azure/machineselect.png)

10. İçinde **özellikleri** > **özelliklerini yapılandırmak**seçin hello hesap hello işlem sunucusu tooautomatically tarafından kullanılan toobe hello makinede hello Mobility hizmeti yükleyin.
11. Varsayılan olarak, tüm diskler çoğaltılır. Tıklatın **tüm diskleri**ve tooreplicate istemediğiniz tüm diskleri temizleyin. Daha sonra, **Tamam**'a tıklayın. Ek VM özellikleri daha sonra ayarlayabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-physical-to-azure/configprop.png)

12. İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, o hello çoğaltma ilkesi seçili doğru doğrulayın. Bir ilkeyi değiştirirseniz, makine ve toonew makineleri çoğaltma uygulanan toohello değişir.
13. Etkinleştirme **çoklu VM tutarlılığını** toogather makineler çoğaltma grubuna isterseniz ve hello grubu için bir ad belirtin. Daha sonra, **Tamam**'a tıklayın. Şunlara dikkat edin:

    a. Çoğaltma gruplarındaki makineler birlikte çoğaltılır ve kilitlenme tutarlı ve uygulamayla tutarlı kurtarma noktaları üzerinden başarısız olduğunda paylaşılan.

    b. Böylece, iş yüklerini yansıtma sanal makineleri ve fiziksel sunucuları araya toplamak öneririz. Çoklu VM tutarlılığını etkinleştirmek, iş yükü performansını etkileyebilir. Yalnızca makineleri çalışan hello aynı iş yükünü ve tutarlılık ihtiyacınız kullanılmalıdır.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-physical-to-azure/policy.png)

14. Tıklatın **çoğaltmasını etkinleştir**. Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**. Merhaba sonra **korumayı Sonlandır** işi çalıştırır, hello makine yük devretme için hazır.

Çoğaltma etkinleştirdikten sonra itme yüklemesini ayarlarsanız hello Mobility hizmeti yüklenir. Merhaba Mobility hizmeti bir makinede yüklü itme olduktan sonra koruma işini başlatır ve başarısız olur. Merhaba hatasından sonra toomanually gereksinim duyduğunuz her makineyi yeniden başlatın. Merhaba koruma işini yeniden başlar ve ilk çoğaltma gerçekleştirilir.


### <a name="view-and-manage-azure-vm-properties"></a>Görüntüleme ve Azure VM özelliklerini yönetme

Merhaba VM özelliklerini doğrulayın ve ihtiyacınız değişiklik öneririz.

1. Tıklatın **öğeleri çoğaltılan**ve select hello makine. Merhaba **Essentials** dikey makineler ayarlarını ve durumu hakkında bilgileri gösterir.
2. İçinde **özellikleri**, çoğaltma görebilirsiniz ve Yük Devretme bilgilerini hello VM.
3. İçinde **işlem ve ağ** > **işlem özellikleri**, hello Azure VM adını ve hedef boyutu belirtebilirsiniz. Merhaba adı toocomply ile değiştirmek [Azure gereksinimleri](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) gerekiyorsa.
4. Azure VM toohello atanan hello hedef ağ, alt ağ ve IP adresi ayarlarını değiştirin:

    a. Merhaba hedef IP adresini ayarlayabilirsiniz.

    b.  Bir adresi sağlamazsanız, hello başarısız üzerinden makine DHCP kullanır.

    c. Yük devretmede kullanılamayan bir adres ayarlarsanız yük devretme işe yaramaz.

    d. Merhaba hello test yük devretme ağı testinde Hello adresi varsa, yük devretme sınaması için aynı hedef IP adresi kullanılabilir.

    e. ağ bağdaştırıcısı Hello sayısını hello hedef sanal makine için belirttiğiniz hello boyuta göre dikte edilir:

     - Merhaba hello kaynak makinedeki ağ bağdaştırıcısı sayısıdır hello ile aynı veya sayısından küçük, hello hello hedef makine boyutu için izin verilen bağdaştırıcıları sonra hello hedef hello sahip aynı sayıda bağdaştırıcıya hello kaynağı olarak.
     - Merhaba hello kaynak sanal makinenin bağdaştırıcı sayısı aşarsa hello hello hedef boyutu için izin verilen sonra hello maksimum hedef boyutu kullanılır.
     - Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hello hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa, hello hedef makinenin iki bağdaştırıcısı vardır. Merhaba kaynak makinenin iki bağdaştırıcısı varsa ancak tek desteklenen hello hedef boyutu destekliyorsa, hello hedef makine yalnızca bir bağdaştırıcı vardır.     
   - Merhaba sanal makinede birden fazla ağ bağdaştırıcısı varsa, tüm toohello bağlandıklarında aynı ağ.
   - Merhaba sanal makine birden çok ağ bağdaştırıcısına sahip sonra hello önce bir hello listede gösterilen hello hale *varsayılan* hello Azure VM ağ bağdaştırıcısı.
5. İçinde **diskleri**, hello VM işletim sistemi ve çoğaltılır hello veri disklerini görebilirsiniz.

## <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma

Her şeyi oluşturduktan sonra her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırın. Başlamadan önce hızlı bir video genel bakış izleyin.

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. tek bir makineye üzerinden toofail içinde **ayarları** > **çoğaltılan öğeler**, tıklatın **yük devretme testi**.

    ![Yük devretme sınaması](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. bir kurtarma üzerinden toofail planlama **ayarları** > **kurtarma planları**, sağ hello planı > **yük devretme testi**. bir kurtarma planı toocreate [bu yönergeleri izleyin](site-recovery-create-recovery-plans.md).  
3. İçinde **yük devretme testi**seçin hello Azure ağ toowhich Azure Vm'lerinin yük devretme gerçekleştikten sonra bağlanır.
4. Tıklatın **Tamam** toobegin hello yük devretme. Merhaba VM tooopen özelliklerini tıklatarak veya hello tıklayarak ilerleme durumunu izleyebilirsiniz **yük devretme testi** kasa adı işinde > **ayarları** > **işleri**  >  **Site Recovery işleri**.
5. Hello yük devretme tamamlandıktan sonra ayrıca olması toosee hello çoğaltma Azure makine görünür hello Azure portalı > **sanal makineleri**. Bu hello VM toohello uygun ağ ve çalıştığını bağlı hello uygun boyutta olduğundan emin olun.
6. Varsa, [yük devretme sonrasında bağlantıları için hazır](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), mümkün tooconnect toohello Azure VM olmalıdır.
7. Bitirdikten sonra tıklatın **temizleme yük devretme testi** hello kurtarma planı üzerinde. İçinde **notları**hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek ve kaydedin. Bu adım, yük devretme testi sırasında oluşturulan hello sanal makineleri siler.

Daha fazla bilgi için bkz: Merhaba [Test yük devretme tooAzure](site-recovery-test-failover-to-azure.md) belge.

## <a name="next-steps"></a>Sonraki adımlar

Sonra çoğaltma hale getirmek ve çalışan, kesinti oluştuğunda tooAzure başarısız ve çoğaltılan hello verilerinden oluşturulan Azure Vm'lerinin. Toonormal işlemleri geri döndüğünde geri tooyour birincil konumu başarısız kadar iş yüklerini ve uygulamaları Azure, daha sonra erişebilirsiniz.

- [Daha fazla bilgi edinin](site-recovery-failover.md) yerine farklı türleri hakkında ve nasıl toorun bunları.
- Makineleri çoğaltmak yerine ve geri, başarısız olan geçiş [daha fazla bilgi](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- Fiziksel makineleri çoğaltırken, yalnızca yeniden çalışma tooa VMware Ortamı'nı kullanabilirsiniz. [Yeniden çalışma hakkında okuyun](site-recovery-failback-azure-to-vmware.md).

## <a name="third-party-software-notices-and-information"></a>Üçüncü taraf yazılım uyarılar ve bilgiler
Sağlamadığı Çevir veya yerelleştirme

Merhaba yazılımını ve bellenimini çalışır durumda hello Microsoft Ürün veya hizmet dayanır veya hello malzemesini içerir projeleri listelenen (topluca "üçüncü taraf kodu"). Microsoft hello özgün yazarı hello üçüncü taraf kodu değil. Hello özgün telif hakkı bildirimi ve lisansı altında Microsoft gibi üçüncü taraf kodu alındı, aşağıda belirtilen ayarlanır.

Bir bölümdeki Hello bilgiler üçüncü taraf bileşenleri hello projelerden aşağıda listelenen kod ilgili olduğu. Bu tür lisansları ve bilgi yalnızca bilgilendirme amacıyla sağlanır. Bu üçüncü taraf kodu Microsoft yazılım lisans hello Microsoft Ürün veya hizmet koşulları altında Microsoft tarafından relicensed tooyou yapılıyor.  

Bölüm B Hello bilgilerinde kullanılabilir tooyou hello özgün lisans şartları altında Microsoft tarafından kurulan üçüncü taraf kodu bileşenleri ilgili olduğu.

Merhaba tam dosya hello üzerinde bulunabilir [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft tarafından uygulanır olup olmadığını, belirtilmeyen tüm hakları ayırır başkaca, ya da aksi takdirde.
