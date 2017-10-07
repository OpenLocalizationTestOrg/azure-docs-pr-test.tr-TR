---
title: "VMM Bulutları tooAzure aaaReplicate Hyper-V sanal makineleri | Microsoft Docs"
description: "Bu makalede, System Center VMM Bulutları tooAzure tooreplicate Hyper-V sanal makinelerini Hyper-V konaklarının nasıl bulunan açıklanmaktadır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 9d526a1f-0d8e-46ec-83eb-7ea762271db5
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 136f68585534c17b615ecc4e82c0133bf813503f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure"></a>Hyper-V sanal makineleri VMM Bulutları tooAzure Çoğalt
> [!div class="op_single_selector"]
> * [Azure portalı](site-recovery-vmm-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Klasik portal](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Klasik](site-recovery-deploy-with-powershell.md)
>
>

Hello Azure Site Recovery hizmeti tooyour iş devamlılığı ve olağanüstü durum kurtarma (BCDR) stratejinize yönetme çoğaltma, yük devretme ve kurtarma sanal makinelerin ve fiziksel sunucuları tarafından katkıda bulunur. Makineler çoğaltılmış tooAzure veya tooa ikincil şirket içi veri merkezi olabilir. Hızlı bir genel bakış için [Azure Site Recovery nedir?](site-recovery-overview.md) konusunu okuyun.

## <a name="overview"></a>Genel Bakış
Bu makalede, VMM özel Bulutlar tooAzure bulunan sunucular nasıl toodeploy Site Recovery tooreplicate Hyper-V sanal makineleri Hyper-V konağı açıklanmaktadır.

Merhaba makale hello senaryonun önkoşulları içerir ve size nasıl tooset bir Site Recovery kasasına yukarı hello hello kaynak VMM sunucusunda Azure Site Recovery sağlayıcısı hello sunucu hello kasaya kaydetmek, Azure depolama hesabı ekleme, hello yüklemek gösterir Azure kurtarma Hizmetleri aracısını Hyper-V ana bilgisayar sunucuları üzerinde uygulanan tooall korumalı sanal makineler olabilir ve bu sanal makineler için korumayı etkinleştir VMM Bulutları için koruma ayarlarını yapılandırın. Sınama hello yük devretme toomake tarafından her şeyin beklendiği gibi çalıştığından emin sonlandırın.

Tüm yorumlarınızı ve sorularınızı bu makalenin veya hello hello altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Mimari
![Mimari](./media/site-recovery-vmm-to-azure-classic/topology.png)

* Hello Azure Site kurtarma sağlayıcısı VMM hello üzerinde Site Recovery dağıtımı sırasında yüklenir ve hello VMM sunucusu hello Site Recovery kasasına kayıtlı. Merhaba sağlayıcı, Site Recovery toohandle çoğaltma orchestration ile iletişim kurar.
* Hello Azure kurtarma Hizmetleri aracısını Hyper-V ana bilgisayar sunucuları üzerinde Site Recovery dağıtımı sırasında yüklenir. Veri çoğaltma tooAzure depolama işler.

## <a name="azure-prerequisites"></a>Azure önkoşulları
İşte Azure'da ihtiyaç duyacaklarınız:

| **Önkoşul** | **Ayrıntılar** |
| --- | --- |
| **Azure hesabı** |Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir. [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz. Site Recovery fiyatlandırması hakkında [daha fazla bilgi edinin](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **Azure depolama alanı** |Bir Azure depolama hesabı toostore çoğaltılmış verileri gerekir. Çoğaltılan veriler Azure depolama alanında depolanır ve yük devretme durumunda Azure VM'leri çalışmaya başlar. <br/><br/>[Standart coğrafi olarak yedekli depolama hesabınızın](../storage/common/storage-redundancy.md#geo-redundant-storage) olması gerekir. Merhaba hesabı olmalıdır hello hello Site Recovery hizmeti ile aynı bölgeye ve ilişkilendirilmesi hello aynı abonelik. Çoğaltma toopremium depolama hesapları şu anda desteklenmiyor ve kullanılmaması unutmayın.<br/><br/>Azure depolama alanı [hakkında bilgi edinin](../storage/common/storage-introduction.md). |
| **Azure ağı** |Azure VM'ler bağlanacak bir Azure sanal ağı gerekir toowhen yük devretme oluşur. Hello Azure sanal ağı hello olmalıdır hello Site Recovery kasasıyla aynı bölgede. |

## <a name="on-premises-prerequisites"></a>Şirket içi önkoşullar
İşte şirket içinde ihtiyaç duyacaklarınız:

| **Önkoşul** | **Ayrıntılar** |
| --- | --- |
| **VMM** |Bir fiziksel veya sanal bağımsız sunucu olarak veya sanal küme olarak dağıtılmış en az bir VMM sunucusu gerekir. <br/><br/>Merhaba VMM sunucusu hello en yeni birikmeli güncelleştirmeleri içeren System Center 2012 R2 çalıştırması gerekir.<br/><br/>Merhaba VMM sunucusunda yapılandırılmış en az bir bulut gerekir.<br/><br/>Merhaba kaynak bulut tooprotect istediğiniz bir veya daha fazla VMM ana bilgisayar grubu içermesi gerekir.<br/><br/>VMM bulutlarını ayarlama hakkında daha fazla bilgi edinmek için Keith Mayer'ın blogundaki [Adım adım kılavuz: System Center 2012 SP1 VMM içeren özel bulut oluşturma](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx) |
| **Hyper-V** |Bir veya daha fazla Hyper-V ana bilgisayarı sunucuları veya hello VMM bulut kümelerde gerekir. Merhaba ana bilgisayar sunucusu olmalıdır ve bir veya daha fazla VM. <br/><br/>Merhaba Hyper-V server çalıştırmalıdır en az **Windows Server 2012 R2** hello Hyper-V rolüne sahip veya **Microsoft Hyper-V Server 2012 R2** ve hello son güncelleştirmelerin yüklü olması.<br/><br/>Vm'leri içeren herhangi bir Hyper-V sunucusu tooprotect VMM bulutunda yer alması gerekir istiyor.<br/><br/>Hyper-V'yi bir kümede çalıştırıyorsanız statik IP adresi temelli bir kümeye sahip olmanız durumunda küme aracısının otomatik olarak oluşturulamayacağını unutmayın. El ile tooconfigure hello küme Aracısı gerekir. Aidan Finn'in blog girdisi aracılığıyla [daha fazla bilgi edinin](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters). |
| **Korumalı makineler** | İstediğiniz tooprotect ile uyumlu olması gerekir VM'ler [Azure gereksinimleri](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). |

## <a name="network-mapping-prerequisites"></a>Ağ eşlemesi önkoşulları
Azure ağı eşlemesinde sanal makineleri korumaya zaman hello kaynak VMM sunucusunda VM ağları ve hedef Azure ağları tooenable hello aşağıdaki arasında eşler:

* Merhaba üzerinde aynı devreden tüm makineler ağ tooeach bulundukları hangi kurtarma planı yedeklemiş diğer bağlanabilir.
* Bir ağ geçidi hello hedef Azure ağında ayarlanıp ayarlanmadığını sanal makineleri tooother şirket içi sanal makinelere bağlanabilir.
* Hello aynı yük devri yalnızca sanal makineler eşleme, yapılandırmazsanız ağ kurtarma planı yük devretme tooAzure sonra diğer mümkün tooconnect tooeach olacaktır.

Toodeploy ağ eşlemesi istiyorsanız hello aşağıdakiler gerekir:

* Merhaba kaynak VMM sunucusunda tooprotect istediğiniz Hello sanal makineleri bağlı tooa VM ağı olmalıdır. Bu ağ hello Bulutu ile ilişkili mantıksal ağ bağlantılı tooa olmalıdır.
* Bir Azure ağı toowhich çoğaltılan sanal makineler, yük devretme sonrasında bağlanabilir. Bu ağ hello yük devretme sırasında seçersiniz. Merhaba ağ hello olmalıdır, Azure Site Recovery abonelik aynı bölgede.


VMM'de ağları hazırlayın:

   * [Mantıksal ağlar ayarlayın](https://technet.microsoft.com/library/jj721568.aspx).
   * [VM ağları ayarlayın](https://technet.microsoft.com/library/jj721575.aspx).


## <a name="step-1-create-a-site-recovery-vault"></a>1. Adım: Site Recovery kasası oluşturma
1. İçinde toohello oturum [Yönetim Portalı](https://portal.azure.com) hello VMM sunucusundan tooregister istiyor.
2. **Veri Hizmetleri** > **Kurtarma Hizmetleri** > **Site Recovery Kasası** seçeneklerine tıklayın.
3. **Yeni Oluştur** > **Hızlı Oluştur**'a tıklayın.
4. İçinde **adı**, bir kolay ad tooidentify hello kasası girin.
5. İçinde **bölge**, hello hello kasa için coğrafi bölgeyi seçin. desteklenen toocheck bölgeler coğrafi kullanılabilirlik kısmına bakın [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).
6. **Kasa Oluştur**'a tıklayın.

    ![Yeni Kasa](./media/site-recovery-vmm-to-azure-classic/create-vault.png)

Kasa hello onay hello durum çubuğu tooconfirm başarıyla oluşturuldu. Merhaba kasası listelenir **etkin** hello ana kurtarma Hizmetleri sayfasında.

## <a name="step-2-generate-a-vault-registration-key"></a>2. Adım: Kasa kayıt anahtarı oluşturma
Merhaba kasada bir kayıt anahtarı oluşturun. Hello Azure Site Recovery Sağlayıcısı'nı indirin ve hello VMM sunucusuna yükledikten sonra bu anahtar tooregister hello VMM sunucusu hello kasasına kullanacaksınız.

1. Merhaba, **kurtarma Hizmetleri** sayfasında, hello kasa tooopen hello hızlı başlangıç sayfasını tıklatın. Hızlı Başlangıç hello simgesini kullanarak herhangi bir zamanda açık olması.

    ![Hızlı Başlangıç Simgesi](./media/site-recovery-vmm-to-azure-classic/qs-icon.png)
2. Merhaba aşağı açılan listesinde seçin **bir şirket içi VMM sitesi ile Microsoft Azure arasında**.
3. **VMM Sunucularını Hazırla** alanında **Kayıt anahtarı oluştur** dosyasına tıklayın. Merhaba anahtar dosyası otomatik olarak oluşturulur ve oluşturulduktan sonra 5 gün boyunca geçerlidir. Hello Azure portal hello VMM sunucusundan erişiyorsanız değil, bu dosya toohello sunucusu toocopy gerekir.

    ![Kayıt anahtarı](./media/site-recovery-vmm-to-azure-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>3. adım: hello Azure Site Recovery sağlayıcısı yükleme
1. İçinde **Hızlı Başlangıç** > **VMM sunucularını hazırla**, tıklatın **VMM sunucularında yükleme için Microsoft Azure Site kurtarma sağlayıcısı karşıdan** tooobtain hello Merhaba Sağlayıcı yükleme dosyasının en son sürümü.
2. Bu dosya hello kaynak VMM sunucusunda çalıştırın.

   > [!NOTE]
   > VMM bir kümede dağıtılmışsa ve sağlayıcı Merhaba hello ilk kez yüklüyorsanız etkin bir düğümüne yükleyin ve hello yükleme tooregister hello VMM sunucusu hello kasasında tamamlayın. Daha sonra hello sağlayıcısı üzerinde hello diğer düğümlere yükleyin. Tüm gerekir çünkü tüm düğümlerde tooupgrade gerekir sağlayıcısı olmak hello yükseltiyorsanız çalışan aynı sağlayıcı sürümlerinin hello unutmayın.
   >
   >
3. Merhaba yükleyici ön gereksinimlere yönelik denetimi yapar ve izni toostop hello VMM hizmeti toobegin Sağlayıcısı Kurulumu ister. Kurulum bittiğinde VMM hizmeti hello otomatik olarak yeniden başlatılır. Üzerinde yüklüyorsanız, olacak bir VMM küme toostop hello küme rolünü istenir.
4. **Microsoft Update** kısmında güncelleştirmeleri seçebilirsiniz. Bu ayar etkinleştirildiğinde sağlayıcı güncelleştirmeleri tooyour Microsoft Update ilkenize göre yüklenir.

    ![Microsoft Güncelleştirmeleri](./media/site-recovery-vmm-to-azure-classic/updates.png)
5. Merhaba hello sağlayıcıyı çok ayarlamak için bir yükleme konumu**<SystemDrive>\Program System Center 2012 R2\Virtual Machine Manager\bin**. **Yükle**'ye tıklayın.

   ![InstallLocation](./media/site-recovery-vmm-to-azure-classic/install-location.png)
6. Merhaba sağlayıcı yüklendikten sonra tıklatın **kaydetmek** tooregister hello sunucu hello kasasında.

    ![InstallComplete](./media/site-recovery-vmm-to-azure-classic/install-complete.png)
7. İçinde **kasa adı**, hangi hello sunucunun kaydedileceği hello kasasının hello adını doğrulayın. *İleri*’ye tıklayın.

    ![Sunucu kaydı](./media/site-recovery-vmm-to-azure-classic/vaultcred.PNG)
8. İçinde **Internet bağlantısı** belirtin VMM hello üzerinde çalışan Sağlayıcı'nasıl hello sunucu toohello Internet bağlanır. Seçin **var olan ara sunucu ayarlarıyla Bağlan** hello sunucusunda yapılandırılan toouse hello varsayılan Internet bağlantısı ayarları.

    ![İnternet Ayarları](./media/site-recovery-vmm-to-azure-classic/proxydetails.PNG)

   * Toouse istiyorsanız hello sağlayıcı yüklemeden önce özel bir ara sunucu, onu ayarlamanız gerekir. Özel ara sunucu ayarlarını yapılandırırken bir test toocheck hello proxy bağlantı çalışır.
   * Özel bir ara sunucu kullanıyorsanız veya varsayılan ara sunucunuz kimlik doğrulaması gerektiren hello proxy adresi ve bağlantı noktası dahil olmak üzere, tooenter hello proxy ayrıntılarını gerekir.
   * Aşağıdaki URL'lere hello VMM sunucusu ve hello Hyper-v konakları erişilebilir olmalıdır
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Açıklanan hello IP adreslerinin izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653) ve HTTPS (443) protokolü. Merhaba toouse ve, Batı ABD planlama Azure bölgesi toowhite listesi IP aralıklarını gerekir.
   * Özel bir ara sunucu kullanırsanız, VMM RunAs hesabı (DRAProxyAccount) belirtilen hello kullanılarak otomatik olarak oluşturulacak proxy kimlik bilgileri. Bu hesap başarıyla doğrulanabilmesi hello proxy sunucusunu yapılandırın. Merhaba VMM RunAs hesabı ayarları hello VMM konsolundan değiştirilebilir. toodo Bu, açık hello **ayarları** çalışma alanında, genişletin **güvenlik**, tıklatın **farklı çalıştır hesapları**ve ardından hello DRAProxyAccount parolasını değiştirin. Bu ayar etkinleşir toorestart hello VMM hizmeti gerekmektedir.
9. İçinde **kayıt anahtarı**seçin hello anahtarı Azure Site Recovery'den indirdiğiniz ve toohello VMM sunucuya kopyalanır.
10. Merhaba şifreleme ayarı yalnızca VMM Bulutları tooAzure Hyper-V sanal makineleri çoğaltma yapıyorsanız kullanılır. İkincil site tooa çoğaltıyorsanız kullanılmaz.
11. İçinde **sunucu adı**, hello kasasında bir kolay ad tooidentify hello VMM sunucusu belirtin. Bir küme yapılandırmasında hello VMM kümesi rolü adını belirtin.
12. İçinde **Eşitle bulut meta verileri** hello kasası ile Merhaba VMM sunucusundaki tüm Bulutlar için toosynchronize meta verileri istediğinizi seçin. Bu eylem, yalnızca bir kez her sunucuda toohappen gerekir. Tüm bulutlar toosynchronize istemiyorsanız bu ayarı işaretsiz bırakın ve her Bulutu ayrı ayrı hello hello VMM konsolundaki bulut özellikleri eşitleyin.
13. Tıklatın **sonraki** toocomplete hello işlemi. Kayıttan sonra Azure Site Recovery tarafından hello VMM sunucusundan meta veriler alınır. Merhaba sunucu üzerinde hello görüntülenen **VMM sunucuları** hello sekmesinde **sunucuları** hello kasası sayfasında.

    ![Son sayfa](./media/site-recovery-vmm-to-azure-classic/provider13.PNG)

Kayıttan sonra Azure Site Recovery tarafından hello VMM sunucusundan meta veriler alınır. Merhaba sunucu üzerinde hello görüntülenen **VMM sunucuları** sekmesinde hello **sunucuları** hello kasası sayfasında.

### <a name="command-line-installation"></a>Komut satırı yüklemesi
Hello Azure Site Recovery sağlayıcısı komut satırından aşağıdaki hello kullanarak da yüklenebilir. Bu yöntem, bir sunucu çekirdek Windows Server 2012 R2 için kullanılan tooinstall hello sağlayıcısında olabilir.

1. Merhaba sağlayıcısı yükleme dosyasını ve kayıt anahtarı tooa klasörü indirin. Örnek: C:\ASR.
2. Merhaba System Center Virtual Machine Manager hizmetini durdurun
3. Yükseltilmiş bir komut isteminden hello sağlayıcı yükleyicisini şu komutları ayıklayın:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Merhaba sağlayıcısı gibi yükleyin:

        C:\ASR> setupdr.exe /i
5. Merhaba sağlayıcısı şu şekilde kaydedin:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

Parametre konumları aşağıdaki şekildedir:

* **/ Credentials** : hangi hello kayıt anahtarı dosyasının bulunduğu hello konumu belirten zorunlu parametre  
* **/ FriendlyName** : hello Azure Site Recovery portalında görünen hello Hyper-V ana bilgisayar sunucusunun adını hello için zorunlu parametre.
* **/ EncryptionEnabled** : tooencryption, sanal makineleri azure'da (Bekleyen şifreleme) istiyorsanız, isteğe bağlı bir parametre toospecify. Hello dosya adına sahip bir **.pfx** uzantısı.
* **/ proxyaddress** : hello proxy sunucusunun hello adresini belirten isteğe bağlı parametre.
* **/ proxyport** : hello proxy sunucusunun hello bağlantı noktasını belirten isteğe bağlı parametre.
* **/ proxyusername** : hello Ara sunucu kullanıcı adını belirten isteğe bağlı parametre.
* **/ proxypassword** : hello Ara sunucu parolasını belirten isteğe bağlı bir parametre.  

## <a name="step-4-create-an-azure-storage-account"></a>4. Adım: Azure depolama hesabı oluşturma
1. Tıklatın bir Azure depolama hesabınız yoksa **bir Azure depolama hesabı ekleme** toocreate bir hesap.
2. Coğrafi çoğaltmanın etkinleştirilmiş olduğu bir hesap oluşturun. Buna hello hello Azure Site Recovery hizmeti ile aynı bölgeye gerekir ve hello ile ilişkili aynı abonelik.

    ![Depolama hesabı](./media/site-recovery-vmm-to-azure-classic/storage.png)

> [!NOTE]
> [Geçiş depolama hesaplarının](../azure-resource-manager/resource-group-move-resources.md) kaynak arasında grupları içinde hello aynı abonelik veya abonelikler arasında Site Recovery dağıtmak için kullanılan depolama hesapları için desteklenmez.
>
>

## <a name="step-5-install-hello-azure-recovery-services-agent"></a>5. adım: hello Azure kurtarma Hizmetleri Aracısı yükleme
Merhaba VMM bulut her Hyper-V ana bilgisayar sunucusunda Hello Azure kurtarma Hizmetleri aracısını yükleyin.

1. Tıklatın **Hızlı Başlangıç** > **Azure Site kurtarma Hizmetleri Aracısı indir ve ana bilgisayarlara Yükle** tooobtain hello dosyasının en son sürümünü hello Aracısı yükleme.

    ![Kurtarma Hizmetleri Aracısı'nı Yükleme](./media/site-recovery-vmm-to-azure-classic/install-agent.png)
2. Merhaba her Hyper-V ana bilgisayar sunucusunda yükleme dosyasını çalıştırın.
3. Merhaba üzerinde **Önkoşul denetimi** sayfasında **sonraki**. Eksik önkoşullar otomatik olarak yüklenir.

    ![Kurtarma Hizmetleri Aracısı Önkoşulları](./media/site-recovery-vmm-to-azure-classic/agent-prereqs.png)
4. Merhaba üzerinde **yükleme ayarları** sayfasında, tooinstall hello aracısı ve select hello önbellek konumu, yedekleme meta verilerinin yükleneceği istediğiniz yeri belirtin. Ardından **Yükle**'ye tıklayın.
5. ' Ye tıklayın Yükleme bittikten sonra **Kapat** toocomplete hello Sihirbazı.

    ![MARS Aracısı'nı Kaydetme](./media/site-recovery-vmm-to-azure-classic/agent-register.png)

### <a name="command-line-installation"></a>Komut satırı yüklemesi
Microsoft Azure kurtarma Hizmetleri Aracısı hello hello bu komutu kullanarak komut satırından da yükleyebilirsiniz:

    marsagentinstaller.exe /q /nu

## <a name="step-6-configure-cloud-protection-settings"></a>6. Adım: Bulut koruma ayarlarını yapılandırma
Merhaba VMM sunucusunu kaydettikten sonra bulut koruma ayarlarını yapılandırabilirsiniz. Merhaba seçeneği etkin **hello kasası ile Eşitle bulut verilerini** yüklediğinizde hello sağlayıcısı hello VMM sunucusundaki tüm Bulutlar hello görünür <b>korunan öğeler</b> hello kasasında sekmesi.

![Yayımlanan Bulut](./media/site-recovery-vmm-to-azure-classic/clouds-list.png)

1. Merhaba hızlı başlangıç sayfasında, tıklatın **VMM Bulutları için koruma ayarlama**.
2. Merhaba üzerinde **korunan öğeler** sekmesini ve ardından hello bulutta tooconfigure istediğiniz ve Git toohello **yapılandırma** sekmesi.
3. **Hedef** alanı için **Azure**'ı seçin.
4. İçinde **depolama hesabı** çoğaltma için kullandığınız hello Azure depolama hesabını seçin.
5. Ayarlama **depolanan verileri şifrele** çok**devre dışı**. Bu ayar, veri hello şirket içi site ile Azure arasında çoğaltma sırasında şifrelenmesi gerektiğini belirtir.
6. İçinde **kopyalama sıklığı** hello varsayılan ayarı koruyun. Bu değer, verilerin kaynak ve hedef konumlar arasında hangi sıklıkla eşitlenmesi gerektiğini belirtir.
7. İçinde **için kurtarma noktalarını Beklet**, hello varsayılan ayarı koruyun. Varsayılan bir değerle sıfır, yalnızca hello son kurtarma noktası bir birincil sanal makine için bir çoğaltma ana bilgisayar sunucusunda depolanır.
8. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, hello varsayılan ayarı koruyun. Bu değer, ne sıklıkta belirtir toocreate anlık görüntüler. Anlık görüntüler hello anlık görüntü alınırken uygulamaların tutarlı bir durumda olan birim gölge kopyası hizmeti (VSS) tooensure kullanın.  Bir değer ayarlarsanız, yapılandırdığınız ilave kurtarma noktası hello sayısından daha az olduğundan emin olun.
9. İçinde **çoğaltma başlangıç zamanı**, veri tooAzure ilk çoğaltmasının ne zaman başlayacağını belirtin. Merhaba Hyper-V konak sunucusunda Hello saat dilimi kullanılır. Merhaba ilk çoğaltmayı yoğun olmayan saatlere zamanlama öneririz.

    ![Bulut çoğaltma ayarları](./media/site-recovery-vmm-to-azure-classic/cloud-settings.png)

Hello ayarlarını kaydettikten sonra bir iş oluşturulur ve üzerinde hello izlenebilir **işleri** sekmesi. Merhaba VMM kaynak bulutundaki tüm Hyper-V ana bilgisayar sunucularının çoğaltma için yapılandırılır.

Kaydettikten sonra bulut ayarları üzerinde hello değiştirilebilir **yapılandırma** tooremove hello bulut yapılandırması gerekir ve hello Bulutu yeniden yapılandırmanız sekmesini toomodify hello hedef konumu veya hedef depolama hesabı. Merhaba depolama hesabı hello değişikliği değiştirirseniz, yalnızca sanal makineler için hello depolama hesabı değiştirildikten sonra koruma için etkinleştirilmiş uygulanacağını unutmayın. Mevcut sanal makineler yükseltilmez toohello yeni depolama hesabı.

## <a name="step-7-configure-network-mapping"></a>7. Adım: Ağ eşlemesini yapılandırma
Başlamadan önce Ağ eşlemesi hello kaynak VMM sunucusundaki sanal makineleri bağlı tooa VM ağı olduğunu doğrulayın. Ayrıca, bir veya daha fazla Azure sanal ağı oluşturun. Birden fazla VM ağı eşlenen tooa tek Azure ağ olabileceğini unutmayın.

1. Merhaba hızlı başlangıç sayfasında, tıklatın **ağları Eşle**.
2. Merhaba üzerinde **ağlar** sekmesinde **kaynak konumu**seçin hello kaynak VMM sunucusu. **Hedef konumu** için Azure'ı seçin.
3. İçinde **kaynak** hello VMM sunucusuyla ilişkili VM ağlarının listesi görüntülenir. İçinde **hedef** ağlar hello Azure hello abonelikle ilişkili ağları görüntülenir.
4. Merhaba kaynak VM ağı seçin ve tıklatın **harita**.
5. Merhaba üzerinde **hedef ağ Seç** sayfası, select hello hedef Azure ağını toouse istiyor.
6. Merhaba onay işareti toocomplete hello eşleme işlemini'ı tıklatın.

    ![Bulut çoğaltma ayarları](./media/site-recovery-vmm-to-azure-classic/map-networks.png)

Hello ayarlarını kaydettikten sonra tootrack hello eşleme ilerleme bir iş başlatılır ve hello işler sekmesinde izlenebilir. Tüm mevcut çoğaltma toohello kaynak VM ağına karşılık gelen makineleri bağlı toohello olacaktır hedef Azure ağları. Kaynak VM ağına bağlı toohello olan yeni sanal makinelere bağlı toohello eşlenen Azure ağına çoğaltma işleminden sonra olacaktır. Yeni bir ağ ile varolan bir eşlemesini değiştirirseniz, çoğaltma sanal makineleri hello yeni ayarlar kullanılarak bağlanır.

Hello hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme sonrasında bağlı toothat hedef alt olacaktır unutmayın. Eşleşen ada sahip bir hedef alt ağ ise hello sanal makineye bağlı toohello hello ağdaki ilk alt ağ olacaktır.

> [!NOTE]
> [Geçiş ağların](../azure-resource-manager/resource-group-move-resources.md) kaynak arasında grupları içinde hello aynı abonelik veya abonelikler arasında Site Recovery dağıtmak için kullanılan ağlar için desteklenmez.
>
>

## <a name="step-8-enable-protection-for-virtual-machines"></a>8. Adım: Sanal makinelere yönelik korumayı etkinleştirme
Sunucular, Bulutlar ve ağlar doğru şekilde yapılandırıldıktan sonra hello bulutta sanal makineler için korumayı etkinleştirebilirsiniz. Merhaba aşağıdakileri göz önünde bulundurun:

* Sanal makinelerin [Azure gereksinimlerini](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) karşılaması gerekir.
* tooenable koruma hello işletim sistemi ve işletim sistemi disk özellikleri hello sanal makine için ayarlamanız gerekir. Bir sanal makine şablonu kullanarak VMM'de bir sanal makine oluşturduğunuzda hello özelliğini ayarlayabilirsiniz. Bu özellikleri mevcut sanal makineler üzerinde hello ayarlayabilirsiniz **genel** ve **donanım yapılandırması** sekmeleri hello sanal makine özellikleri. Bu özellikleri VMM'de ayarlamazsanız mümkün tooconfigure olacak hello Azure Site Recovery portalında bunları.

    ![Sanal makine oluşturma](./media/site-recovery-vmm-to-azure-classic/enable-new.png)

    ![Sanal makine özelliklerini değiştirme](./media/site-recovery-vmm-to-azure-classic/enable-existing.png)

1. Merhaba tooenable korumasını **sanal makineleri** hangi hello sanal makinenin bulunduğu hello bulutta sekmesini tıklatın, **korumayı etkinleştir** > **sanal makineleriekleyin**.
2. Merhaba bulutta sanal makineler Hello listeden tooprotect istediğiniz hello birini seçin.

    ![Sanal makine korumasını etkinleştirme](./media/site-recovery-vmm-to-azure-classic/select-vm.png)

    Merhaba ilerleyişini izleyin **korumayı etkinleştir** hello eylemde **işleri** hello ilk çoğaltma dahil olmak üzere sekmesinde. Merhaba sonra **korumayı Sonlandır** iş çalıştırmaları hello sanal makine yük devretme için hazır. Koruma etkin ve sanal makineleri yinelenir sonra mümkün tooview olacak Azure bunları.

    ![Sanal makine koruma işi](./media/site-recovery-vmm-to-azure-classic/vm-jobs.png)

1. Merhaba sanal makine özelliklerini doğrulayın ve gerektiği gibi değiştirin.

    ![Sanal makineleri doğrulama](./media/site-recovery-vmm-to-azure-classic/vm-properties.png)
2. Merhaba üzerinde **yapılandırma** hello sanal makine özellikleri aşağıdaki ağ özellikleri değiştirilebilir.

* **Merhaba hedef sanal makinedeki ağ bağdaştırıcısı sayısı** -hello hedef sanal makine için belirttiğiniz hello boyutuna göre ağ bağdaştırıcısı hello sayısını belirler. Denetleme [sanal makine boyutu özellikleri](../virtual-machines/linux/sizes.md) hello hello sanal makine boyutunun desteklediği bağdaştırıcı sayısı. Bir sanal makine için başlangıç boyutu değiştirmek ve hello ayarları kaydettiğinizde hello ağ bağdaştırıcıları sayısı, hello sonraki açışınızda hello değiştirme **yapılandırma** sayfası. Hedef sanal makinelerin ağ bağdaştırıcısı Hello sayısını hello sayısı alt sınırı kaynak sanal makine ve hello hello sanal makine seçildi, aşağıdaki gibi hello boyutu tarafından desteklenen ağ bağdaştırıcısı sayısı ağ bağdaştırıcılarında::

  * Merhaba hello kaynak makinedeki ağ bağdaştırıcısı sayısı küçük veya buna eşit ise toohello bağdaştırıcı sayısı hello hedef makine boyutu için izin verilen sonra hello hedef olacaktır hello aynı sayıda bağdaştırıcıya hello kaynağı olarak.
  * Merhaba hello kaynak sanal makinenin bağdaştırıcı sayısı hello hedef boyutu sonra hello maksimum hedef boyutu kullanılır için izin verilen hello sayıyı aşarsa.
  * Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hello hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa hello hedef makinenin iki bağdaştırıcısı gerekir. Merhaba kaynak makinenin iki bağdaştırıcısı varsa, ancak hello hedef boyut yalnızca bir destekler hello hedef makine yalnızca bir bağdaştırıcısı olur.     
* **Merhaba hedef sanal makine ağının** -hello ağ toowhich hello sanal makine hello ağ kaynak sanal makinenin Ağ eşlemesi tarafından belirlenen toois bağlanır. Merhaba kaynak sanal makine varsa hello hedef ağlardan birini toochoose gerekir sonra birden fazla ağ bağdaştırıcısı ve kaynak ağlar eşlenen toodifferent, hedefte ağlardır.
* **Her ağ bağdaştırıcısının alt ağı** - her ağ bağdaştırıcısı sanal makine başarısız hello alt toowhich hello seçebileceğiniz bağlanacağı için.
* **Hedef IP adresi** - kaynak sanal makinenin hello ağ bağdaştırıcısı statik bir IP adresi başlangıç IP adresi için hello hedef sanal makine sağlayın ve sonra yapılandırılmış toouse ise. Bu özelliği kullanmak hello IP adresi, bir kaynak sanal makinenin yük devretme sonrasında korur. IP adresi sağlanmazsa herhangi bir kullanılabilir IP adresi hello yük devretme sırasında toohello ağ bağdaştırıcısına verilir. Merhaba hedef IP adresi belirtildi, ancak Azure'da çalışan başka bir sanal makine tarafından zaten kullanılıyor yük devretme başarısız olur.  

    ![Ağ özelliklerini değiştirme](./media/site-recovery-vmm-to-azure-classic/multi-nic.png)

> [!NOTE]
> Statik IP adresi içeren Linux sanal makineleri desteklenmez.
>
>

## <a name="test-hello-deployment"></a>Merhaba dağıtımı test etme
tootest bir yük devretme sınaması için tek bir sanal makine çalıştırmak veya birden çok sanal makine içeren ve bir yük devretme testi hello için bir kurtarma planı oluşturun, dağıtımınızı planlayın.  

Yük devretme testi, yük devretme işleminizi ve kurtarma mekanizmanızı yalıtılmış bir ortamda benzetimli olarak gerçekleştirir. Şunlara dikkat edin:

* Hello yük devretme sonrasında Uzak Masaüstü'nü kullanarak azure'daki tooconnect toohello sanal makine istiyorsanız, Uzak Masaüstü Bağlantısı hello test yük devretmesi çalıştırmadan önce hello sanal makinesinde etkinleştirin.
* Yük devretme sonrasında ortak IP adresi tooconnect toohello Azure Uzak Masaüstü kullanarak VM kullanın. Bu toodo istiyorsanız, bağlanan tooa sanal genel bir adres kullanarak makineden engelleyecek etki alanı ilkelerine sahip olmadığınızdan emin olun.

> [!NOTE]
> tooAzure başarısız olduğunda tooget hello en iyi performansı elde etmek, yükledim Azure Aracısı'nı hello VM hello. Aracı daha hızlı önyükleme gerçekleştirilmesini sağlar ve sorun giderme konusunda yardımcı olur. Merhaba karşıdan [Linux Aracısı](https://github.com/Azure/WALinuxAgent), veya hello [Windows Aracısı](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="create-a-recovery-plan"></a>Kurtarma planı oluşturma
1. Merhaba üzerinde **kurtarma planları** sekmesinde, yeni bir plan ekleyin. Bir ad belirtin **VMM** içinde **kaynak türünü**ve hello kaynak VMM sunucusunda **kaynak**. Merhaba hedef Azure olur.

    ![Kurtarma planı oluşturma](./media/site-recovery-vmm-to-azure-classic/recovery-plan1.png)
2. Merhaba, **sanal makineleri seçin** sayfası, select sanal makineleri tooadd toohello kurtarma planı. Bu sanal makineleri toohello kurtarma planının varsayılan grubu eklenir: Grup 1. Tek bir kurtarma planında en fazla 100 sanal makine test edilebilir.

* Toohello planı eklemeden önce tooverify hello sanal makine özelliklerini istiyorsanız hello bulutun Özellikler sayfasında hello hello sanal makineye tıklayın makinenin bulunduğu. Merhaba VMM konsolunda hello sanal makine özelliklerini de yapılandırabilirsiniz.
* Tüm görüntülenen hello sanal makineler için koruma etkinleştirilmiş. Merhaba listesi ve ilk çoğaltması tamamlandı ve ile koruma için etkinleştirilmiş olan ilk bekleyen çoğaltma için etkinleştirilmiş hem sanal makineleri içerir. Yalnızca ilk çoğaltması tamamlanan sanal makineler kurtarma planının bir parçası olarak yük devredebilir.

    ![Kurtarma planı oluşturma](./media/site-recovery-vmm-to-azure-classic/select-rp.png)

Bir kurtarma planı oluşturulduktan sonra hello görünür **kurtarma planları** sekmesi. Ayrıca ekleyebileceğiniz [Azure Otomasyon çalışma kitabı](site-recovery-runbook-automation.md) toohello kurtarma planı tooautomate eylemleri yük devretme sırasında.

### <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma
Bir test yük devretme tooAzure iki yolu toorun vardır.

* **Azure ağı olmadan yük devretme sınamasını**— bu türdeki yük devretme testi hello sanal makinenin gelir doğru Azure'da denetler. Merhaba sanal makine yük devretme sonrasında bağlı tooany Azure ağ olmayacaktır.
* **Azure ağıyla yük devretme testi**— tüm çoğaltma ortamının hello yük devretme denetimleri bu tür istendiği şekilde alınıp ve bağlı toohello belirtilen hedef Azure ağını hello sanal makineler üzerinde başarısız olacaktır. Alt ağ işleme için yük devretme sınaması için hello alt hello sınama sanal makinesinin hello çoğaltma sanal makinesi hello alt ağa göre belirlenir. Bir çoğaltma sanal makinesi Hello alt hello kaynak sanal makine hello alt ağda alıyorsa, farklı tooregular çoğaltma budur.

Azure hedef ağı belirtmeden koruma tooAzure için etkinleştirilmiş bir sanal makine için yük devretme testi toorun istiyorsanız tooprepare herhangi bir şey gerekmez. toorun yük devretme testi ile hedef Azure ağını Azure üretim ağınızdan (Azure'da yeni bir ağ oluştururken, varsayılan davranıştır) toocreate yalıtılmış olan yeni bir Azure ağı gerekir. Ne çok Ara[bir yük devretme testi](site-recovery-failover.md) daha fazla ayrıntı için.

Merhaba çoğaltılan sanal makine toowork için beklendiği gibi hello altyapı yukarı tooset gerekir. Örneğin, etki alanı denetleyicisi ve DNS sahip bir sanal makineyi Azure Site RECOVERY'yi kullanarak çoğaltılmış tooAzure olabilir ve yük devretme testi kullanılarak hello test ağında oluşturulabilir. Daha fazla ayrıntı için [active directory için yük devretme testi ile ilgili dikkat edilmesi gerekenler](site-recovery-active-directory.md#test-failover-considerations) bölümüne bakın

Yük devretme testi toorun hello aşağıdaki:

1. Merhaba üzerinde **kurtarma planları** sekmesinde, seçin hello planı ve tıklatın **yük devretme testi**.
2. Merhaba üzerinde **onaylayın yük devretme testi** sayfasında **hiçbiri** veya özel Azure ağı.  Hiçbiri hello yük devretme testi olacak seçerseniz sanal makine hello onay tooAzure doğru şekilde çoğaltılan ancak çoğaltma ağı yapılandırmasını denetlemez unutmayın.

    ![Ağ yok](./media/site-recovery-vmm-to-azure-classic/test-no-network.png)
3. Veri şifreleme hello bulut için etkinleştirilmişse **şifreleme anahtarı** hello seçeneği tooenable veri şifrelemesi bir bulut için açık olduğunda hello VMM sunucusunda sağlayıcı hello yüklenmesi sırasında verilen select hello sertifika .
4. Merhaba üzerinde **işleri** sekmesini yük devretme işleminin ilerleyişini izleyebilirsiniz. Ayrıca, mümkün toosee hello sanal makinenin test çoğaltmasını hello Azure portal olmalıdır. Şirket içi ağınızdan tooaccess sanal makineleri ayarladıysanız, bir Uzak Masaüstü Bağlantısı toohello sanal makineyi başlatabilirsiniz.
5. Merhaba yük devretme hello ulaştığında **testi Tamamla** aşama, tıklatın **tam Test** toofinish onu. Toohello inebilir **iş** tootrack yük devretme işleminin ilerleyişini durumunu ve tooperform gerekli olan herhangi bir eylem sekmesi.
6. Yük devretme sonrasında hello sanal makinenin test çoğaltmasını hello Azure portal görebilirsiniz. Şirket içi ağınızdan tooaccess sanal makineleri ayarladıysanız, bir Uzak Masaüstü Bağlantısı toohello sanal makineyi başlatabilirsiniz. Aşağıdaki hello:

   1. Merhaba sanal makineler başarıyla başlatıldığını doğrulayın.
   2. Hello yük devretme sonrasında Uzak Masaüstü'nü kullanarak azure'daki tooconnect toohello sanal makine istiyorsanız, Uzak Masaüstü Bağlantısı hello test yük devretmesi çalıştırmadan önce hello sanal makinesinde etkinleştirin. Ayrıca tooadd hello sanal makinede bir RDP uç noktası gerekir. Yararlanabileceğiniz bir [Azure Automation Runbook](site-recovery-runbook-automation.md) toodo.
   3. Uzak Masaüstü kullanarak Azure'da bir ortak IP adresi tooconnect toohello sanal makine kullanırsanız, yük devretme sonrasında, genel bir adres kullanarak tooa sanal makineye bağlanmanızı engelleyecek etki alanı ilkelerine sahip olmadığınızdan emin olun.
7. Merhaba sınama tamamlandıktan sonra aşağıdaki hello:

   * Tıklatın **hello test yük devretme tamamlandığında**. Merhaba temizleme ortamı tooautomatically güç kapalı test edin ve hello test sanal makineleri silin.
   * Tıklatın **notları** toorecord ve hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek.


## <a name="next-steps"></a>Sonraki adımlar
[Kurtarma planlarını ayarlama](site-recovery-create-recovery-plans.md) ve [yük devretme](site-recovery-failover.md) hakkında daha fazla bilgi edinin.
