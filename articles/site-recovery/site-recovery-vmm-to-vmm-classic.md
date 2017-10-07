---
title: aaaReplicate Hyper-V sanal makineleri VMM tooa ikincil sitedeki (Azure Klasik) | Microsoft Docs
description: "Bu makalede, Azure Site Recovery ile ikincil VMM sitesi tooa tooreplicate vmm'de Hyper-V sanal makineleri nasıl Bulutlar açıklanmaktadır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a63acba3-8fb3-4926-aa29-b1e64a765681
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: fe551e1f741579044f540ea0e50a6e36d48133ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Hyper-V sanal makineleri VMM Bulutları tooa ikincil VMM sitesi Çoğalt
> [!div class="op_single_selector"]
> * [Azure portal](site-recovery-vmm-to-vmm.md)
> * [Klasik portal](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Hello Azure Site Recovery hizmeti tooyour iş devamlılığı ve olağanüstü durum kurtarma (BCDR) stratejinize yönetme çoğaltma, yük devretme ve kurtarma sanal makinelerin ve fiziksel sunucuları tarafından katkıda bulunur. Makineler çoğaltılmış tooAzure veya tooa ikincil şirket içi veri merkezi olabilir. Hızlı bir genel bakış için [Azure Site Recovery nedir?](site-recovery-overview.md) konusunu okuyun.

## <a name="overview"></a>Genel Bakış
Bu makalede, Azure Site RECOVERY'yi kullanarak VMM Bulutları toosecondary VMM sitede yönetilen sunucularda nasıl tooreplicate Hyper-V sanal makineleri Hyper-V konak açıklanmaktadır.

Hello makale önkoşulları içerir, nasıl bir Site Recovery kasasına yukarı tooset yüklemenize Azure Site Recovery sağlayıcısı kaynağında hello ve VMM sunucuları hedef gösterir, hello sunucuları hello kasaya kaydetmek, VMM Bulutları için koruma ayarlarını yapılandırın ve ardından etkinleştir Hyper-V sanal makineleri için koruma. Sınama hello yük devretme toomake tarafından her şeyin beklendiği gibi çalıştığından emin sonlandırın.

Tüm yorumlarınızı ve sorularınızı bu makalenin veya hello hello altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Mimari
Merhaba resimde hello farklı iletişim kanalları ve orchestration ve çoğaltma için Azure Site Recovery tarafından kullanılan bağlantı noktaları gösterilmektedir

![E2E topolojisi](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>Başlamadan önce
Bu Önkoşullar sağladığınızdan emin olun:

| **Önkoşullar** | **Ayrıntılar** |
| --- | --- |
| **Azure** |Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir. [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz. Site Recovery fiyatlandırması hakkında [daha fazla bilgi edinin](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **VMM** |En az bir VMM sunucusu gerekir.<br/><br/>Merhaba VMM sunucusu çalışıyor. en az hello en yeni birikmeli güncelleştirmeleri içeren System Center 2012 SP1.<br/><br/>Tek bir VMM sunucusu ile korumayı ayarlama tooset istiyorsanız hello sunucusunda yapılandırılan en az iki bulut gerekir.<br/><br/>İki VMM sunucusu ile toodeploy koruma istiyorsanız, her sunucunun yapılandırılmış en az bir bulut olmalıdır tooprotect ve hello ikincil VMM sunucusunda yapılandırılan bir bulut istediğiniz hello birincil VMM sunucusunda toouse koruma ve kurtarma için istediğiniz<br/><br/>Tüm VMM Bulutları hello Hyper-V işlev profili kümesine sahip olmalıdır.<br/><br/>Merhaba kaynak bulut tooprotect istediğiniz bir veya daha fazla VMM ana bilgisayar grubu içermesi gerekir. |
| **Hyper-V** |Bir veya daha fazla Hyper-V ana bilgisayar sunucuları hello birincil ve ikincil VMM konak gruplarında ve her Hyper-V ana bilgisayar sunucusunda bir veya daha fazla sanal makine gerekir.<br/><br/>Merhaba ana bilgisayarı ve hedef Hyper-V sunucuları en az çalıştırmalıdır hello Hyper-V rolü içeren Windows Server 2012 ve hello son güncelleştirmelerin yüklü olması.<br/><br/>Vm'leri içeren herhangi bir Hyper-V sunucusu tooprotect VMM bulutunda yer alması gerekir istiyor.<br/><br/>Bir kümede Hyper-V çalıştırıyorsanız, bir statik IP adresi tabanlı kümeniz varsa, küme aracısının otomatik olarak oluşturulamayacağını unutmayın. Tooconfigure hello küme Aracısı el ile yapmanız gerekir. Aidan Finn'in blog girdisi aracılığıyla [daha fazla bilgi edinin](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters). |
| **Ağ eşlemesi** |Ağ eşleme toomake yük devretme sonrasında ikincil Hyper-V ana bilgisayar sunucuları üzerinde çoğaltılmış sanal makinelere en iyi şekilde yerleştirilir ve tooappropriate VM ağları bağlanabilir yapılandırabilirsiniz. Ağ eşlemesini yapılandırmazsanız, çoğaltma sanal makineleri yük devretme sonrasında bağlı tooany ağ olmayacaktır.<br/><br/>dağıtım işlemi sırasında ağ eşlemesini tooset hello kaynak Hyper-V konak sunucusunda hello sanal makineleri bağlı tooa VMM VM ağ olduğundan emin olun. Bu ağ hello bulut. ile ilişkili mantıksal ağ bağlantılı tooa olmalıdır < br /<br/>Merhaba hedef bulut, kurtarma için kullandığınız hello ikincil VMM sunucusunda yapılandırılmış karşılık gelen VM ağı olmalıdır ve sırayla hello hedef Bulutu ile ilişkili olan mantıksal ağa karşılık gelen bağlı tooa olması gerekir. |
| **Depolama eşlemesi** |Bir kaynak Hyper-V konak sunucusu tooa hedef Hyper-V ana bilgisayarı sunucusunda, bir sanal makine çoğalttığınızda, varsayılan olarak Hyper-V Yöneticisi'nde hello hedef Hyper-V ana bilgisayarı için belirtilen hello varsayılan konumda çoğaltılan veriler depolanır. Çoğaltılan verilerin depolandığı üzerinde daha fazla denetim için depolama eşlemesi yapılandırabilirsiniz.<br/><br/> tooconfigure depolama eşlemesi, depolama sınıflandırmaları hello kaynağında yukarı tooset ve gerekir VMM sunucuları dağıtıma başlamadan önce hedef. |

## <a name="step-1-create-a-site-recovery-vault"></a>1. Adım: Site Recovery kasası oluşturma
1. İçinde toohello oturum [Yönetim Portalı](https://portal.azure.com) hello VMM sunucusundan tooregister istiyor.
2. Genişletme **Veri Hizmetleri** > **kurtarma Hizmetleri** tıklatıp **Site Recovery kasası**.
3. **Yeni Oluştur** > **Hızlı Oluştur**'a tıklayın.
4. İçinde **adı**, bir kolay ad tooidentify hello kasası girin.
5. İçinde **bölge** hello hello kasa için coğrafi bölgeyi seçin. desteklenen toocheck bölgeler coğrafi kullanılabilirlik kısmına bakın [Azure Site Recovery fiyatlandırma ayrıntıları](http://go.microsoft.com/fwlink/?LinkId=389880).
6. **Kasa Oluştur**'a tıklayın.

    ![Kasa oluşturma](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

Merhaba durum bu hello kasası çubuğu denetiminde oluşturuldu. Merhaba kasası listelenir **etkin** hello ana kurtarma Hizmetleri sayfasında.

## <a name="step-2-generate-a-vault-registration-key"></a>2. Adım: Kasa kayıt anahtarı oluşturma
Merhaba kasada bir kayıt anahtarı oluşturun. Hello Azure Site Recovery Sağlayıcısı'nı indirin ve hello VMM sunucusuna yükledikten sonra bu anahtar tooregister hello VMM sunucusu hello kasasına kullanacaksınız.

1. Merhaba, **kurtarma Hizmetleri** sayfasında, hello kasa tooopen hello hızlı başlangıç sayfasını tıklatın. Hızlı Başlangıç hello simgesini kullanarak herhangi bir zamanda açık olması.

    ![Hızlı Başlangıç Simgesi](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. Merhaba aşağı açılan listesinde seçin **iki şirket içi VMM siteler arasında**.
3. İçinde **VMM sunucularını hazırla**, tıklatın **kayıt defteri anahtar dosyası oluştur**. Merhaba anahtar dosyası otomatik olarak oluşturulur ve oluşturulduktan sonra 5 gün boyunca geçerlidir. Hello Azure portal hello VMM sunucusundan erişiyorsanız değil, bu dosya toohello sunucusu toocopy gerekir.

    ![Kayıt anahtarı](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>3. adım: hello Azure Site Recovery sağlayıcısı yükleme
1. Merhaba üzerinde **Hızlı Başlangıç** sayfasında **VMM sunucularını hazırla**, tıklatın **VMM sunucularında yükleme için Microsoft Azure Site kurtarma sağlayıcısı karşıdan** son tooobtain hello Merhaba Sağlayıcı yükleme dosyasının sürümü.
2. Bu dosya hello kaynak VMM sunucusunda çalıştırın.

   > [!NOTE]
   > VMM bir kümede dağıtılmışsa ve sağlayıcı Merhaba hello ilk kez yüklüyorsanız etkin bir düğümüne yükleyin ve hello yükleme tooregister hello VMM sunucusu hello kasasında tamamlayın. Daha sonra hello sağlayıcısı üzerinde hello diğer düğümlere yükleyin. Tüm gerekir çünkü tüm düğümlerde tooupgrade gereksinim sağlayıcısı olmak hello yükseltiyorsanız çalışan aynı sağlayıcı sürümlerinin hello unutmayın.
   >
   >
3. Merhaba yükleyici mu birkaç **ön koşulları denetlemek** ve izni toostop hello VMM toobegin sağlayıcısı kurulumu hizmet istekleri. Kurulum bittiğinde VMM hizmeti hello otomatik olarak yeniden başlatılır. Üzerinde yüklüyorsanız, olacak bir VMM küme toostop hello küme rolünü istenir.
4. **Microsoft Update** kısmında güncelleştirmeleri seçebilirsiniz. Bu ayar etkinleştirildiğinde sağlayıcı güncelleştirmeleri tooyour Microsoft Update ilkenize göre yüklenir.

    ![Microsoft Güncelleştirmeleri](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. Merhaba yükleme konumu olarak ayarlanmış çok**<SystemDrive>\Program System Center 2012 R2\Virtual Machine Manager\bin**. Merhaba üzerinde Yükle düğmesi toostart hello Sağlayıcı yükleme'yi tıklatın.

    ![InstallLocation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. Merhaba sağlayıcı yüklendikten sonra tıklatın **kaydetmek** tooregister hello sunucu hello kasasında.

    ![InstallComplete](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. İçinde **kasa adı**, hangi hello sunucunun kaydedileceği hello kasasının hello adını doğrulayın. *İleri*’ye tıklayın.

    ![Sunucu kaydı](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. İçinde **Internet bağlantısı** belirtin VMM hello üzerinde çalışan Sağlayıcı'nasıl hello sunucu toohello Internet bağlanır. Seçin **var olan ara sunucu ayarlarıyla Bağlan** hello sunucusunda yapılandırılan toouse hello varsayılan Internet bağlantısı ayarları.

    ![İnternet Ayarları](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

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
13. Tıklatın **sonraki** toocomplete hello işlemi. Kayıttan sonra Azure Site Recovery tarafından hello VMM sunucusundan meta veriler alınır. Merhaba sunucu görüntülenir **VMM sunucuları** > **sunucuları** hello kasasında.

    ![Sunucular](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>Komut satırı yüklemesi
Hello Azure Site Recovery sağlayıcısı hello komut satırından da yüklenebilir. Bu yöntem, bir sunucu çekirdek Windows Server 2012 R2 için kullanılan tooinstall hello sağlayıcısında olabilir.

1. Merhaba sağlayıcısı yükleme dosyasını ve kayıt anahtarı tooa klasörü indirin. Örneğin, C:\ASR.
2. Merhaba System Center Virtual Machine Manager hizmetini durdurun
3. İle bir komut isteminden aşağıdaki komutları çalıştırarak Hello sağlayıcı yükleyicisini ayıklamak **yönetici** ayrıcalıkları:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Merhaba sağlayıcısı çalıştırarak yükleyin:

        C:\ASR> setupdr.exe /i
5. Merhaba sağlayıcısı çalıştırarak kaydedin:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>     

Burada hello Parametreler şunlardır:

* **/ Credentials**: hangi hello kayıt anahtarı dosyasının bulunduğu hello konumu belirten zorunlu parametre  
* **/ FriendlyName**: hello Azure Site Recovery portalında görünen hello Hyper-V ana bilgisayar sunucusunun adını hello için zorunlu parametre.
* **/ EncryptionEnabled**: sanal makinelerinizin Azure bekleyen şifreleme gerekiyorsa toouse hello VMM tooAzure senaryo içinde yalnızca gereken isteğe bağlı bir parametre. Lütfen hello dosyasının bu hello adı olduğundan emin olun sağlayın sahip bir **.pfx** uzantısı.
* **/ proxyaddress**: hello proxy sunucusunun hello adresini belirten isteğe bağlı parametre.
* **/ proxyport**: hello proxy sunucusunun hello bağlantı noktasını belirten isteğe bağlı parametre.
* **/ proxyusername**: (proxy kimlik doğrulaması gerektiriyorsa) hello Ara sunucu kullanıcı adını belirten isteğe bağlı parametre.
* **/ proxypassword**: belirten isteğe bağlı parametre (Ara sunucu kimlik doğrulaması gerekirse) hello proxy sunucusu ile kimlik doğrulaması için parola hello.  

## <a name="step-4-configure-cloud-protection-settings"></a>4. adım: Bulut yapılandırma koruma ayarları
VMM sunucusu kayıtlı sonra bulut koruma ayarlarını yapılandırabilirsiniz. Merhaba seçeneği etkinleştirilirse **hello kasası ile Eşitle bulut verilerini** yüklediğinizde hello sağlayıcısı hello VMM sunucusundaki tüm Bulutlar hello görünür **korunan öğeler** hello kasasında sekmesi. Almadıysanız, belirli bir bulut Azure Site Recovery ile hello eşitleyebilirsiniz **genel** hello hello VMM konsolundaki bulut özellikleri sayfasında sekmesinde.

![Yayımlanan Bulut](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. Merhaba hızlı başlangıç sayfasında, tıklatın **VMM Bulutları için koruma ayarlama**.
2. Merhaba üzerinde **VMM Bulutları** sekmesinde, seçmek istediğiniz tooconfigure ve Git toohello hello bulut **yapılandırma** sekmesi.
3. İçinde **hedef**seçin **VMM**.
4. İçinde **hedef konum**, hello kurtarma için istediğiniz toouse hello bulut yöneten yerinde VMM sunucusu seçin.
5. İçinde **hedef bulut**, toouse hello kaynak buluttaki sanal makinelerin yük devretme için hello hedef Bulutu seçin. Şunlara dikkat edin:

   * Merhaba sanal makineleri korumaya kurtarma gereksinimlerini karşılayan bir hedef bulut seçmenizi öneririz.
   * Bir buluta yalnızca tooa tek bulut çifti ait olabilir — birincil veya bir hedef bulut olarak.
6. İçinde **kopyalama sıklığı**, ne sıklıkta belirtin verilerin 5he kaynak ve hedef konumlar arasında eşitlenmesi. Windows Server 2012 R2 Hello Hyper-V ana çalıştırırken bu ayar yalnızca ilgili olduğunu unutmayın. Diğer sunucular için beş dakika, varsayılan ayar kullanılır.
7. İçinde **ek kurtarma noktaları**, toocreate ek noktaları isteyip istemediğinizi belirtin. yalnızca hello son kurtarma noktası bir birincil sanal makine için bir çoğaltma ana bilgisayar sunucusunda depolanır Hello varsayılan sıfır değerini gösterir. Birden çok kurtarma noktasının etkinleştirilmesi ek depolama alanı her kurtarma noktasında depolanan hello anlık görüntüleri için gerektirdiğini unutmayın. Varsayılan olarak, her kurtarma noktasının bir saatlik verileri içeren her saat kurtarma noktaları oluşturulur. Merhaba sanal makine hello VMM Konsolu için atadığınız hello kurtarma noktası değeri hello Azure Site Recovery konsolunda atadığınız hello değerden daha küçük olmamalıdır.
8. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, ne sıklıkta belirtin toocreate uygulamayla tutarlı anlık görüntüler. Hyper-V iki çeşit anlık kullanır — bir artımlı hello tüm sanal makinenin anlık görüntüsünü sunan standart anlık görüntü ve zaman içinde nokta verilerin bir anlık görüntüsünü hello uygulama hello sanal makine içinde geçen uygulama tutarlı bir anlık görüntü. Uygulamayla tutarlı anlık görüntüleri hello anlık görüntü alınırken uygulamaların tutarlı bir durumda olan birim gölge kopyası hizmeti (VSS) tooensure kullanın. Uygulamayla tutarlı anlık görüntüleri etkinleştirirseniz, kaynak sanal makinelerde çalışan uygulamaların hello performansını etkiler unutmayın. Ayarladığınız hello değeri, yapılandırdığınız ilave kurtarma noktası hello sayısından daha az olduğundan emin olun.

    ![Koruma ayarlarını yapılandırın](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. İçinde **veri aktarımı sıkıştırma**, aktarılan çoğaltılmış verilerin sıkıştırılmasının gerekli olup olmadığını belirtin.
10. İçinde **kimlik doğrulaması**, hello birincil ve kurtarma Hyper-V ana bilgisayar sunucuları arasında trafik kimliğinin nasıl belirtin. Çalışan bir Kerberos ortamı yapılandırılmış olmadığı sürece, HTTPS seçin. Azure Site Recovery, HTTPS kimlik doğrulaması için sertifikaları otomatik olarak yapılandırır. El ile yapılandırma gereklidir. Kerberos seçerseniz, bir Kerberos anahtarı hello konak sunucularının karşılıklı kimlik doğrulaması için kullanılır. Varsayılan olarak, bağlantı noktası 8083 ve 8084 (Sertifikalar) hello Hyper-V ana bilgisayar sunucuları üzerinde Windows Güvenlik Duvarı hello açılacak. Bu ayar yalnızca Windows Server 2012 R2'de çalışan Hyper-V konak sunucuları için geçerli olduğunu unutmayın.
11. İçinde **bağlantı noktası**, hangi hello kaynağında hello bağlantı noktası numarasını değiştirin ve hedef ana bilgisayarların çoğaltma trafiğini dinler. Örneğin, tooapply hizmet kalitesi (QoS) ağ bant genişliği için çoğaltma trafiğini azaltma istiyorsanız hello ayarı değiştirebilirsiniz. Başlangıç bağlantı noktası başka bir uygulama tarafından kullanılmadığından ve hello Güvenlik Duvarı ayarlarında açık olup olmadığını denetleyin.
12. İçinde **çoğaltma yöntemini**, normal çoğaltma işlemi başlamadan önce nasıl hello ilk veri çoğaltma işlemi kaynak tootarget konumlardan, ele alınacağını belirtin:

    * **Ağ üzerinden**— hello ağ üzerinden veri kopyalamak olabilir zaman alabilir ve yoğun bir kaynak. Merhaba bulut görece küçük sanal sabit diskler sanal makinelerle içeriyorsa ve hello birincil site geniş bant genişliğine sahip bir bağlantı üzerinden bağlı toohello ikincil site ise bu seçeneği kullanmanızı öneririz. Merhaba kopyalama hemen başlatmak veya bir saat seçin gerektiğini belirtebilirsiniz. Ağ çoğaltmayı kullanırsanız, yoğun olmayan saatlerde zamanlamanızı öneririz.
    * **Çevrimdışı**— bu yöntemi dış medya kullanarak hello ilk çoğaltmanın gerçekleştirilecek belirtir. Tooavoid düşüşü ağ performansı veya coğrafi olarak Uzak konumlar için istiyorsanız kullanışlıdır. toouse hello kaynak bulutun ve hello içeri aktarma konumunu hello hedef bulut üzerinde hello dışarı aktarma konumunu belirttiğiniz bu yöntem. Bir sanal makine için korumayı etkinleştirdiğinizde, belirtilen kopyalanan toohello hello sanal sabit disk olduğundan verme konumu. Toohello hedef sitenin göndermek ve toohello içeri aktarma konumuna kopyalayın. Merhaba sistem kopyaları hello bilgi toohello çoğaltma sanal makineleri alındı.
13. Seçin **silmek çoğaltma sanal makinesi** hello seçerek hello sanal makine korumayı durdurursanız çoğaltma sanal makinesi hello toospecify'nin silinmesi **hello sanal makine için korumayı Sil ** hello bulut özellikleri hello sanal makineleri sekmesinde seçeneği. Bu ayar etkin olan, devre dışı bıraktığınızda koruma hello sanal makineyi Azure Site Recovery'den kaldırılır, hello sanal makine için hello Site Recovery ayarlarını hello VMM konsolundan kaldırılır ve hello çoğaltma silinir.

    ![Koruma ayarlarını yapılandırın](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

Hello ayarlarını kaydettikten sonra bir iş oluşturulur ve üzerinde hello izlenebilir **işleri** sekmesi. Merhaba VMM kaynak bulutundaki tüm Hyper-V ana bilgisayar sunucularının çoğaltma için yapılandırılır. Bulut ayarları üzerinde hello değiştirilebilir **yapılandırma** sekmesi. Toomodify hello hedef konumu veya hedef bulut istiyorsanız hello bulut yapılandırmasını kaldırın ve hello Bulutu yeniden yapılandırmanız gerekir.

### <a name="prepare-for-offline-initial-replication"></a>Çevrimdışı ilk çoğaltma için hazırlama
Çevrimdışı ilk çoğaltma için Eylemler tooprepare aşağıdaki toodo hello gerekir:

* Merhaba kaynak sunucuda hangi hello verileri dışarı aktarma devre dışı gerçekleşecek bir yolu konumuna belirtirsiniz. Tam Denetim toohello VMM hizmeti hello dışarı aktarma yolundaki NTFS ve paylaşım izinlerini atayın. Merhaba hedef sunucuda içinden hello verileri içeri bir yolu konumuna oluşacaktır belirtirsiniz. Merhaba, bu alma yolu aynı izinleri atayın.
* Merhaba içe veya dışa aktarma yolu paylaşılan, hello VMM hizmet hesabı hello uzak bilgisayarda yönetici, Power User, Print Operator veya sunucu işleci grup üyeliği atamak paylaşılan hangi hello bulunur.
* Tüm farklı çalıştır hesapları tooadd konaklar kullanıyorsanız, hello içeri aktarma ve dışarı aktarma yollarındaki, okuma atayın ve VMM'de toohello farklı çalıştır hesapları yazma izinleri.
* Merhaba içeri aktarma ve dışarı aktarma paylaşımları geri döngü yapılandırma Hyper-V tarafından desteklenmediği için Hyper-V konak sunucusu olarak kullanılan herhangi bir bilgisayarda bulunmalıdır değil.
* Her Hyper-V ana bilgisayar sunucusunda tooprotect, istediğiniz sanal makineleri içeren Active Directory'de etkinleştirme ve yapılandırma Kısıtlı temsilci tootrust hello uzak bilgisayarları hangi hello içeri ve dışarı aktarma yollarının bulunduğu, aşağıdaki gibidir:
  1. Merhaba etki alanı denetleyicisinde açın **Active Directory Kullanıcıları ve Bilgisayarları**.
  2. Merhaba konsol ağacında **DomainName** > **bilgisayarlar**.
  3. Sağ hello Hyper-V ana bilgisayarı sunucusu adı > **özellikleri**.
  4. Merhaba üzerinde **temsilci** sekmesini T**bu bilgisayar temsilci toospecified yalnızca Hizmetleri için paslanma**.
  5. Tıklatın **herhangi bir kimlik doğrulama protokolünü kullan**.
  6. Tıklatın **ekleme** > **kullanıcıları ve Bilgisayarları**.
  7. Merhaba verme yolu barındıran hello bilgisayarın türü hello adı > **Tamam**. Kullanılabilir hizmetler listeden Merhaba, hello CTRL tuşunu basılı tutun ve **CIFS** > **Tamam**. Merhaba hello bilgisayarın adını konakları hello alma yol yineleyin. Ek Hyper-V konak sunucuları için gerektiği kadar yineleyin.

## <a name="step-5-configure-network-mapping"></a>5. adım: ağ eşlemesini yapılandırma
1. Merhaba hızlı başlangıç sayfasında, tıklatın **ağları Eşle**.
2. İçinden toomap ağlar istediğiniz ve ardından ağların eşleneceği hedef VMM sunucusu toowhich hello hello hello kaynak VMM sunucusunu seçin. Hello kaynak ağların ve ilişkili hedef ağlarının listesi görüntülenir. Şu anda eşlenmemiş ağlar için boş bir değer gösterilir.
3. Bir ağ seçin **kaynak üzerinde ağ** > **harita**. Merhaba hizmet hello hedef sunucu üzerindeki hello VM ağlarını algılar ve görüntüler. Merhaba bilgi simgesi sonraki toohello kaynak ve hedef ağ adları tooview hello her ağın alt ağlarını'ı tıklatın.

    ![Ağ eşlemesini yapılandırma](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. Merhaba iletişim kutusunda hello VM ağları birini hello hedef VMM sunucusunu seçin.

    ![Hedef ağ Seç](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. Hedef ağ seçtiğinizde, hello hello kaynak ağı kullanan korumalı Bulutlar gösterilir. Koruma için kullanılan hello Bulutları ile ilişkili kullanılabilir hedef ağlar da görüntülenir. Kullanılabilir tooall hello Bulutlar için koruma kullanarak bir hedef ağ seçmeniz önerilir. Ya da toohello VMM sunucusuna gidin ve toochoose istediğiniz toohello vm ağına karşılık gelen hello bulut özellikleri tooadd hello mantıksal ağı değiştirmek.
6. Merhaba onay işareti toocomplete hello eşleme işlemini'ı tıklatın. Bir iş tootrack hello eşleme işlemini başlatır. Merhaba üzerinde görüntülemek **işleri** sekmesi.

## <a name="step-6-configure-storage-mapping"></a>6. adım: depolama eşlemesi yapılandırma
Bir kaynak Hyper-V konak sunucusu tooa hedef Hyper-V ana bilgisayarı sunucusunda, bir sanal makine çoğalttığınızda, varsayılan olarak Hyper-V Yöneticisi'nde hello hedef Hyper-V ana bilgisayarı için belirtilen hello varsayılan konumda çoğaltılan veriler depolanır. Çoğaltılan verilerin depolandığı üzerinde daha fazla denetim için depolama eşlemeleri aşağıdaki gibi yapılandırabilirsiniz:

1. Hedef VMM sunucuların ve depolama sınıflandırmaları hem hello kaynağında tanımlayın. [Daha fazla bilgi edinin](https://technet.microsoft.com/library/gg610685.aspx). Sınıflandırmaları kaynak ve hedef bulut, kullanılabilir toohello Hyper-V ana bilgisayar sunucuları olmalıdır. Sınıflandırmaları gerekmez toohave hello aynı türde depolama. Örneğin, csv içeren SMB paylaşımları tooa Hedef Sınıflandırma içeren bir kaynak sınıflandırma eşleyebilirsiniz.
2. Sınıflandırmaları hazır olduktan sonra eşlemeleri oluşturabilirsiniz. toodo hello üzerinde bu **Hızlı Başlangıç** sayfa > **eşleme depolama**.
3. Merhaba tıklatın **depolama** sekmesini > **eşleme depolama sınıflandırmaları**.
4. Merhaba üzerinde **eşleme depolama sınıflandırmaları** sekmesinde, sınıflandırmaları hello kaynağında seçip VMM sunucuyu hedefleyebilir. Ayarlarınızı kaydedin.

    ![Hedef ağ Seç](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>7. adım: sanal makine korumayı etkinleştirin
Sunucular, Bulutlar ve ağlar doğru şekilde yapılandırıldıktan sonra hello bulutta sanal makineler için korumayı etkinleştirebilirsiniz.

1. Merhaba üzerinde **sanal makineleri** hangi hello sanal makinenin bulunduğu hello bulutta sekmesini tıklatın, **korumayı etkinleştir** > **sanal makineleri ekleyin**.
2. Merhaba bulutta sanal makineler Hello listeden tooprotect istediğiniz hello birini seçin.

    ![Sanal makine korumasını etkinleştirme](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. Merhaba hello korumayı etkinleştir eylemi ilerleyişini izleyin **işleri** hello ilk çoğaltma dahil olmak üzere sekmesi. Sonra Hello korumayı Sonlandır işini çalıştırır hello sanal makine yük devretme için hazırdır. Koruma etkin ve sanal makineleri yinelenir sonra mümkün tooview olacak Azure bunları.

    ![Sanal makine koruma işi](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> Merhaba VMM konsolunda sanal makineler için korumayı etkinleştirebilirsiniz. Tıklatın **korumayı etkinleştir** hello hello araç çubuğundan **Azure Site Recovery** hello sanal makine özelliklerinde sekmesi.
>
>

### <a name="on-board-existing-virtual-machines"></a>Yerleşik mevcut sanal makineler
Hyper-V çoğaltma ile çoğaltma mevcut sanal makineler VMM varsa tooonboard gerekir şekilde Azure Site Recovery koruması için:

1. Birincil ve ikincil bulut doğrulayın. Merhaba varolan sanal makine barındıran hello Hyper-V server hello birincil bulutta bulunduğundan ve hello çoğaltma sanal makinesi barındıran bu hello Hyper-V server hello ikincil bulutta bulunduğundan emin olun. Emin olun, hello Bulutlar için koruma ayarlarını yapılandırdığınız. Hello ayarları şu anda Hyper-V çoğaltma için yapılandırılan eşleşmesi gerekir. Aksi durumda sanal makine çoğaltma beklendiği gibi çalışmayabilir.
2. Daha sonra hello birincil sanal makine için korumayı etkinleştirin. Azure Site Recovery ve VMM hello aynı çoğaltma konak ve sanal makine algılandığında, ve Azure Site Recovery yeniden kullanmak ve bulut yapılandırması sırasında yapılandırılan hello ayarları kullanarak çoğaltmayı yeniden oluşturmak sağlayacak.

## <a name="test-your-deployment"></a>Dağıtımınızı test edin
tootest bir yük devretme sınaması için tek bir sanal makine çalıştırmak veya birden çok sanal makine içeren ve bir yük devretme testi hello için bir kurtarma planı oluşturun, dağıtımınızı planlayın.  Yük devretme testi, yük devretme işleminizi ve kurtarma mekanizmanızı yalıtılmış bir ortamda benzetimli olarak gerçekleştirir.

### <a name="create-a-recovery-plan"></a>Kurtarma planı oluşturma
1. Merhaba üzerinde **kurtarma planları** sekmesini tıklatın, **kurtarma planı oluşturma**.
2. Merhaba kurtarma planı ve kaynak ve hedef VMM sunucuları için bir ad belirtin. Merhaba kaynak sunucu yük devretme ve kurtarma için etkinleştirilmiş sanal makineleri olması gerekir. Seçin **Hyper-V** Hyper-V çoğaltma için yapılandırılmış tooview tek bulut.

    ![Kurtarma planı oluşturma](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. İçinde **sanal makineyi Seç**, çoğaltma gruplarını seçin. Merhaba çoğaltma grubuyla ilişkili tüm sanal makineleri seçilir ve toohello kurtarma planı eklenir. Bu sanal makineleri toohello kurtarma planının varsayılan grubu eklenir: Grup 1. gerekli olursa, daha fazla grup ekleyebilirsiniz. Çoğaltma sanal makineler hello kurtarma planı grupları hello sırasını uygun olarak başlatılır sonra unutmayın.

    ![Sanal makineleri ekleyin](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

Bir kurtarma planı oluşturulduktan sonra hello hello listede görünür **kurtarma planları** sekmesi.

### <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma
1. Merhaba üzerinde **kurtarma planları** sekmesinde, seçin hello planı ve tıklatın **yük devretme testi**.
2. Merhaba üzerinde **onaylayın yük devretme testi** sayfasında, **hiçbiri**. Bu seçenek ile bağlı tooany ağ çoğaltma sanal makineleri başarısız etkin hello olmayacaktır unutmayın. Bu sanal makine başarısız üzerinde beklendiği gibi hello ancak çoğaltma ağ ortamınızı test değil sınayacak. Ne çok Ara[bir yük devretme testi](site-recovery-failover.md) nasıl hakkında daha fazla ayrıntı için toouse farklı ağ seçenekleri.
3. Merhaba test sanal makinesi aynı çoğaltma sanal makinesi üzerinde hangi hello var. hello konağına hello oluşturulur. Toohello eklenen hangi hello çoğaltma sanal makinesi bulunduğu aynı bulut.

### <a name="run-a-recovery-plan"></a>Bir kurtarma planı Çalıştır
Çoğaltma hello çoğaltma sanal makinesi hello bir IP adresi olmayabilir sonra hello IP adresini aynı birincil sanal makine hello. Sanal makineler, kullandıkları hello DNS sunucusu güncelleştirilecek başladıktan sonra. Bir komut dosyası tooupdate hello DNS sunucusu tooensure zamanında güncelleştirme de ekleyebilirsiniz.

#### <a name="script-tooretrieve-hello-ip-address"></a>Komut dosyası tooretrieve başlangıç IP adresi
Bu örnek komut dosyası tooretrieve başlangıç IP adresi çalıştırın.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-tooupdate-dns"></a>Komut dosyası tooupdate DNS
Bu örnek komut dosyası tooupdate başlangıç IP adresi belirterek DNS çalıştırmak hello önceki örnek komut dosyası kullanarak aldı.

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>Site Recovery için gizlilik bilgileri
Bu bölümde hello Microsoft Azure Site Recovery hizmeti ("hizmet") için ek gizlilik bilgileri sağlar. Microsoft Azure hizmetlerini tooview hello Gizlilik Bildirimi'ne bakın [Microsoft Azure gizlilik bildirimi](http://go.microsoft.com/fwlink/?LinkId=324899)

**Özellik: kayıt**

* **Ne yaptığını**: böylece sanal makineler korunabilir sunucu hizmeti ile kaydeder
* **Toplanan bilgiler**: hizmet toplar, işler ve yönetim sertifikası bilgileri hello VMM sunucusunun hello hizmet adı kullanarak tooprovide olağanüstü durum kurtarma atadığı hello VMM sunucusundan iletir hello kaydettikten sonra ve sanal makine Bulutları, VMM sunucusunda hello adı.
* **Bilgilerin kullanımı**:

  * Yönetim sertifikası — bu kullanılan toohelp tanımlamak ve kayıtlı hello VMM sunucusuna erişim toohello hizmeti için kimlik doğrulaması. Merhaba hizmeti kullanan ortak anahtar bölümü yalnızca hello bir belirteç kayıtlı hello sertifika toosecure hello VMM sunucusu erişebilir. Merhaba sunucu toouse Bu belirteci toogain erişim toohello hizmet özelliklerini gerekir.
  * Merhaba VMM sunucusunun adını — hello VMM Sunucu adı gerekli tooidentify ve üzerinde hangi hello Bulutlar konumlandırıldığını hello uygun VMM sunucusuyla iletişim kurar.
  * Bulut hello VMM sunucusundan adları — hello hizmet bulut eşleştirme/eşleştirmesini kaldırma özelliği aşağıda açıklanan kullanırken hello bulut adı gereklidir. Birincil veri merkezi bulut hello kurtarma veri merkezinde başka bir bulut ile toopair karar verdiğinizde, hello kurtarma veri merkezi tüm hello bulutlardan hello adlarını sunulur.
* **Seçim**: Bu bilgiler yardımcı olacağından hello hizmet kayıt işlemi önemli bir parçasıdır ve istediğiniz tooidentify hello yanı sıra tooprovide Azure Site Recovery koruması hizmeti tooidentify hello VMM sunucusu hello doğru kayıtlı VMM sunucusu. Bu bilgi toohello hizmet toosend istemiyorsanız, bu hizmet kullanmayın. Sunucunuza kaydetmek ve daha sonra toounregister istediğiniz, (hangi Azure portal hello) hello hizmet portalından hello VMM Sunucu bilgilerini silerek bunu yapabilirsiniz.

**Özellik: Azure Site Recovery korumasını etkinleştirin**

* **Ne yaptığını**: hello Azure Site Recovery sağlayıcısı hello VMM sunucusunda yüklü olan hello hizmeti ile iletişim kurmak için hello conduit. Merhaba sağlayıcısı hello VMM işlemde barındırılan bir dinamik bağlantı kitaplığı (DLL) olur. Hello sağlayıcı yüklendikten sonra hello VMM Yönetici konsolunda hello "Veri merkezi Kurtarma" özelliği etkin. Tüm yeni veya var olan sanal makine bir bulutta "Veri merkezi Kurtarma" adlı bir özellik etkinleştirebilirsiniz toohelp hello sanal makine koru. Bu özellik ayarlandıktan sonra hello sağlayıcısı hello adını ve Kimliğini hello sanal makine toohello hizmet gönderir. Windows Server 2012 veya Windows Server 2012 R2 Hyper-V çoğaltma teknolojisiyle Hello sanal koruması etkin. Merhaba sanal makine verilerini (genellikle bir farklı "Kurtarma" veri merkezinde bulunan) bir Hyper-V ana bilgisayar tooanother gelen çoğaltılan.
* **Toplanan bilgiler**: hello hizmet toplar, işler ve hello adı, kimliği, sanal ağ ve hello bulut hello adını içeren hello sanal makine için meta veri aktaran ait olduğu.
* **Bilgilerin kullanımı**: hello hizmet hizmet portalınızda bilgileri toopopulate hello sanal makine bilgileri yukarıda hello kullanır.
* **Seçim**: Bu hello hizmeti önemli bir parçasıdır ve devre dışı bırakılamaz. Toohello hizmet gönderilen bu bilgiler istemiyorsanız, herhangi bir sanal makine için Azure Site Recovery korumasını etkinleştirmeyin. Merhaba sağlayıcısı toohello hizmeti tarafından gönderilen tüm veriler HTTPS üzerinden gönderilen olduğunu unutmayın.

**Özellik: Kurtarma planı**

* **Ne yaptığını**: Bu özellik toobuild hello "Kurtarma" veri merkezi orchestration planlamanıza yardımcı olur. Hangi hello sanal makine ya da sanal makine grubu hello kurtarma sitesinde başlatılmalıdır hello düzenini tanımlayabilirsiniz. Çalıştırmak istediğiniz otomatik betikler toobe ya da kurtarma hello zaman her bir sanal makine için yapılan tüm el ile işlem toobe de belirtebilirsiniz. Yük devretme (Merhaba sonraki bölümde yer alan) genellikle hello Eşgüdümlü kurtarma için Kurtarma planlaması düzeyi en tetiklenir.
* **Toplanan bilgiler**: hello hizmet toplar, işler ve sanal makine meta veri ve meta veri Otomasyon betikleri ve el ile işlem notlar gibi hello kurtarma planı için meta veri aktarır.
* **Bilgilerin kullanımı**: yukarıda açıklanan hello meta veri olan hizmet Portalı'nda kullanılan toobuild hello kurtarma planı.
* **Seçim**: Bu hello hizmeti önemli bir parçasıdır ve devre dışı bırakılamaz. Toohello hizmet gönderilen bu bilgiler istemiyorsanız, Kurtarma planları bu hizmette yapı yok.

**Özellik: Ağ eşlemesi**

* **Ne yaptığını**: Bu özellik, hello birincil veri merkezi toohello kurtarma veri merkezi toomap ağ bilgileri sağlar. Hello sanal makineleri hello kurtarma sitesinde kurtarılan, bu eşleme için ağ bağlantısı oluşturmada yardımcı olur.
* **Toplanan bilgiler**: hello ağ eşleme özelliğini bir parçası olarak hello hizmet toplar, işler ve hello mantıksal ağların (birincil ve datacenter) her site için hello meta veri aktarır.
* **Bilgilerin kullanımı**: hello hizmet kullanır hello meta veri toopopulate servis portalınız hello ağ bilgileri nerede eşleyebilirsiniz.
* **Seçim**: Bu hello hizmeti önemli bir parçasıdır ve devre dışı bırakılamaz. Toohello hizmet gönderilen bu bilgiler istemiyorsanız hello ağ eşleme özelliğini kullanmayın.

**Özellik: Yük devretme - planlanmış, Planlanmayan, test**

* **Ne yaptığını**: Bu özellik, bir VMM tarafından yönetilen veri merkezi tooanother VMM tarafından yönetilen veri merkezinden bir sanal makinenin yük devretme sağlar. Merhaba yük devretme işlemi, kendi hizmet portalı hello kullanıcı tarafından tetiklenir. Bir yük devretme için olası nedenler şunlardır planlanmamış bir olay (doğal disaster0; biri hello durumda örneğin olay (örneğin veri merkezi yük dengeleme); test yük devretme (örneğin bir kurtarma planı prova).

Merhaba VMM sunucusunda sağlayıcı Hello hello hizmet hello olaydan haberdar ve VMM arabirimleri aracılığıyla hello Hyper-V konağı üzerinde bir yük devretme işlemi yürütür. Bir Hyper-V ana bilgisayar tooanother (genellikle farklı "Kurtarma" veri merkezinde çalışan) hello sanal makineden gerçek yük devretme hello Windows Server 2012 veya Windows Server 2012 R2 Hyper-V çoğaltma teknolojisiyle ele alınır. Merhaba yük devretme işlemi tamamlandıktan sonra hello hello VMM sunucusunda hello "Kurtarma" veri merkezinin yüklü sağlayıcı hello başarı bilgi toohello hizmet gönderir.

* **Toplanan bilgiler**: hello hizmet hizmet portalınızda bilgi toopopulate hello hello yük devretme eylem bilgileri durumunu yukarıda hello kullanır.
* **Bilgilerin kullanımı**: hello hizmet bilgileri yukarıda hello aşağıdaki gibi kullanır:

  * Yönetim sertifikası — bu kullanılan toohelp tanımlamak ve kayıtlı hello VMM sunucusuna erişim toohello hizmeti için kimlik doğrulaması. Merhaba hizmeti kullanan ortak anahtar bölümü yalnızca hello bir belirteç kayıtlı hello sertifika toosecure hello VMM sunucusu erişebilir. Merhaba sunucu toouse Bu belirteci toogain erişim toohello hizmet özelliklerini gerekir.
  * Merhaba VMM sunucusunun adını — hello VMM Sunucu adı gerekli tooidentify ve üzerinde hangi hello Bulutlar konumlandırıldığını hello uygun VMM sunucusuyla iletişim kurar.
  * Bulut hello VMM sunucusundan adları — hello hizmet bulut eşleştirme/eşleştirmesini kaldırma özelliği aşağıda açıklanan kullanırken hello bulut adı gereklidir. Birincil veri merkezi bulut hello kurtarma veri merkezinde başka bir bulut ile toopair karar verdiğinizde, hello kurtarma veri merkezi tüm hello bulutlardan hello adlarını sunulur.
* **Seçim**: Bu hello hizmeti önemli bir parçasıdır ve devre dışı bırakılamaz. Toohello hizmet gönderilen bu bilgiler istemiyorsanız, bu hizmet kullanmayın.

## <a name="next-steps"></a>Sonraki adımlar
Ortamınızı beklendiği gibi çalıştığını test yük devretme toocheck çalıştırdıktan sonra [hakkında bilgi edinin](site-recovery-failover.md) yerine farklı türde.
