---
title: "Vmm'de Hyper-V Vm'lerini ikincil bir siteye (Azure Klasik) çoğaltma | Microsoft Docs"
description: "Bu makalede, Azure Site Recovery ile ikincil VMM sitesi VMM bulutlarındaki Hyper-V Vm'lerini çoğaltma açıklar."
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
ms.openlocfilehash: 6814f62f73bad272229205f4768dcce5947117d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site"></a>VMM bulutlarındaki Hyper-V sanal makineleri bir ikincil VMM siteye çoğaltma
> [!div class="op_single_selector"]
> * [Azure portal](site-recovery-vmm-to-vmm.md)
> * [Klasik portal](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Azure Site Recovery hizmeti; çoğaltma, yük devretme ve sanal makineler ile fiziksel sunucuları kurtarma işlemlerini düzenleyerek iş sürekliliği ve olağanüstü durum kurtarma (BCDR) stratejinize katkı sağlar. Makineler, Azure'a veya bir ikincil şirket içi veri merkezine çoğaltılabilir. Hızlı bir genel bakış için [Azure Site Recovery nedir?](site-recovery-overview.md) konusunu okuyun.

## <a name="overview"></a>Genel Bakış
Bu makale, Hyper-V sanal makinelerini ikincil VMM sitesi Azure Site RECOVERY'yi kullanarak VMM bulutlarında yönetilen Hyper-V ana bilgisayar sunucuları üzerinde çoğaltma açıklar.

Makaleyi önkoşulları içerir, Site Recovery kasasını oluşturup, Azure Site Recovery sağlayıcısı yükleme kaynağı üzerinde ve hedef VMM sunucularda, sunucuları kasaya kaydetmek, VMM Bulutları için koruma ayarlarını yapılandırın ve Hyper-V VM'ler için korumayı etkinleştirmek gösterilmektedir. Her şeyin istendiği gibi çalıştığından emin olmak için yük devretmeyi test ederek işlemi sonlandırın.

Tüm yorumlarınızı ve sorularınızı bu makalenin alt kısmında veya [Azure Kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)'nda paylaşabilirsiniz.

## <a name="architecture"></a>Mimari
Aşağıdaki resimde farklı iletişim kanalları ve orchestration ve çoğaltma için Azure Site Recovery tarafından kullanılan bağlantı noktaları gösterilmektedir

![E2E topolojisi](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>Başlamadan önce
Bu Önkoşullar sağladığınızdan emin olun:

| **Önkoşullar** | **Ayrıntılar** |
| --- | --- |
| **Azure** |Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir. [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz. Site Recovery fiyatlandırması hakkında [daha fazla bilgi edinin](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **VMM** |En az bir VMM sunucusu gerekir.<br/><br/>VMM sunucusu en az çalıştırması en yeni birikmeli güncelleştirmeleri içeren System Center 2012 SP1.<br/><br/>Tek bir VMM sunucusu ile korumayı ayarlama istiyorsanız, sunucu üzerinde yapılandırılmış en az iki bulut gerekir.<br/><br/>İki VMM sunucusu ile koruma dağıtmak istiyorsanız, her sunucusunun korumak istediğiniz birincil VMM sunucusunda yapılandırılmış en az bir bulut ve bir bulut koruma ve kurtarma için kullanmak istediğiniz ikincil VMM sunucusunda yapılandırılmış olması gerekir<br/><br/>Tüm VMM Bulutları Hyper-V işlev profili kümesine sahip olmalıdır.<br/><br/>Korumak istediğiniz kaynak bulutun, bir veya birden fazla VMM ana bilgisayar grubu içermesi gerekir. |
| **Hyper-V** |Bir veya daha fazla Hyper-V ana bilgisayar sunucularının birincil ve ikincil VMM konak gruplarında ve her Hyper-V ana bilgisayar sunucusunda bir veya daha fazla sanal makine gerekir.<br/><br/>En az ana bilgisayarı ve hedef Hyper-V sunucularında çalışan Windows Server 2012 Hyper-V rolüne sahip ve en son güncelleştirmelerin yüklü olması.<br/><br/>Korumak istediğiniz ve VM'leri içeren herhangi bir Hyper-V sunucusunun, VMM bulutunda yer alması gerekir.<br/><br/>Bir kümede Hyper-V çalıştırıyorsanız, bir statik IP adresi tabanlı kümeniz varsa, küme aracısının otomatik olarak oluşturulamayacağını unutmayın. Küme Aracısı el ile yapılandırmanız gerekir. Aidan Finn'in blog girdisi aracılığıyla [daha fazla bilgi edinin](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters). |
| **Ağ eşlemesi** |Yük devretme sonrasında ikincil Hyper-V ana bilgisayar sunucuları üzerinde çoğaltılmış sanal makinelere en iyi şekilde yerleştirilir ve uygun VM ağlarına bağlanmasını sağlayabilirsiniz emin olmak için Ağ eşlemesi yapılandırabilirsiniz. Ağ eşlemesini yapılandırmazsanız, yük devretme sonrasında çoğaltma sanal makineleri, herhangi bir ağa bağlanmayacaktır.<br/><br/>Dağıtımı sırasında ağ eşlemesini ayarlamak için sanal makineleri kaynak Hyper-V konak sunucusunda bir VMM VM ağına bağlı olduğundan emin olun. Bu ağ bulut ilişkilendirilmiş bir mantıksal ağ bağlantılı olması gerekir < br /<br/>Hedef bulut, kurtarma için kullandığınız ikincil VMM sunucusunda yapılandırılmış karşılık gelen VM ağı olmalıdır ve bu sırayla hedef Bulutu ile ilişkili değil karşılık gelen bir mantıksal ağ bağlantılı olması gerekir. |
| **Depolama eşlemesi** |Hedef Hyper-V konak sunucusu için bir kaynak Hyper-V konak sunucusunda bir sanal makine çoğalttığınızda, varsayılan olarak Hyper-V Yöneticisi'nde hedef Hyper-V ana bilgisayarı için belirtilen varsayılan konuma çoğaltılan veriler depolanır. Çoğaltılan verilerin depolandığı üzerinde daha fazla denetim için depolama eşlemesi yapılandırabilirsiniz.<br/><br/> Depolama eşlemesi yapılandırmak için depolama sınıflandırmaları kaynağı ayarlayabilir ve VMM sunucuları dağıtıma başlamadan önce hedef gerekir. |

## <a name="step-1-create-a-site-recovery-vault"></a>1. Adım: Site Recovery kasası oluşturma
1. Kaydolmak istediğiniz VMM sunucusundan [Yönetim Portalı](https://portal.azure.com)'nda oturum açın.
2. Genişletme **Veri Hizmetleri** > **kurtarma Hizmetleri** tıklatıp **Site Recovery kasası**.
3. **Yeni Oluştur** > **Hızlı Oluştur**'a tıklayın.
4. **Ad** alanına kasayı tanımlamak için kolay bir ad girin.
5. İçinde **bölge** kasa için coğrafi bölgeyi seçin. Desteklenen bölgeleri kontrol etmek için [Azure Site Recovery Fiyatlandırma Ayrıntıları](http://go.microsoft.com/fwlink/?LinkId=389880) bölümünde Coğrafi Kullanılabilirlik kısmına bakın.
6. **Kasa Oluştur**'a tıklayın.

    ![Kasa oluşturma](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

Durum çubuğunda kasa oluşturulduğunu denetleyin. Kasa, ana Kurtarma Hizmetleri sayfasında **Etkin** olarak listelenir.

## <a name="step-2-generate-a-vault-registration-key"></a>2. Adım: Kasa kayıt anahtarı oluşturma
Kasada bir kayıt anahtarı oluşturun. Azure Site Recovery Sağlayıcısı'nı indirdikten sonra VMM sunucusuna yükleyin, oluşturduğunuz anahtarı kasadaki VMM sunucusuna kaydolmak için kullanacaksınız.

1. **Kurtarma Hizmetleri** sayfasında, Hızlı Başlangıç sayfasını açmak için kasaya tıklayın. Ayrıca, Hızlı Başlangıç sayfasını istediğiniz zaman simgesini kullanarak da açabilirsiniz.

    ![Hızlı Başlangıç Simgesi](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. Aşağı açılan listesinde seçin **iki şirket içi VMM siteler arasında**.
3. İçinde **VMM sunucularını hazırla**, tıklatın **kayıt defteri anahtar dosyası oluştur**. Anahtar dosyası otomatik olarak oluşturulur ve oluşturulduktan sonra 5 gün boyunca geçerlidir. VMM sunucusundan Azure portalına erişmek değil, bu dosyayı sunucuya kopyalamanız gerekir.

    ![Kayıt anahtarı](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-the-azure-site-recovery-provider"></a>3. Adım: Azure Site Recovery Sağlayıcısı'nı yükleme
1. Üzerinde **Hızlı Başlangıç** sayfasında **VMM sunucularını hazırla**, tıklatın **VMM sunucularında yükleme için Microsoft Azure Site kurtarma sağlayıcısı karşıdan** Sağlayıcı yükleme dosyasının en son sürümünü elde etmek için.
2. Bu dosyayı kaynak VMM sunucusunda çalıştırın.

   > [!NOTE]
   > VMM bir kümede dağıtılmışsa ve Sağlayıcı'yı ilk kez yüklüyorsanız yükleme işlemini etkin bir düğümde gerçekleştirin ve VMM sunucusunu kasaya kaydetmek için yüklemeyi sonlandırın. Ardından, Sağlayıcı'yı diğer düğümlere yükleyin. Sağlayıcı yükseltiyorsanız bunların tümü aynı sağlayıcı sürümlerinin çalışması gerektiği için tüm düğümlerde yükseltmeniz gerektiğini unutmayın.
   >
   >
3. Birkaç yükleyici mu **ön koşulları denetlemek** ve sağlayıcının kurulumunu başlatmak için VMM hizmetini durdurmak için izin ister. Kurulum bittiğinde VMM Hizmeti otomatik olarak yeniden başlatılır. Yükleme işlemini bir VMM kümesinde gerçekleştiriyorsanız Küme rolünü durdurmanız istenir.
4. **Microsoft Update** kısmında güncelleştirmeleri seçebilirsiniz. Bu ayar etkinleştirildiğinde Sağlayıcı güncelleştirmeleri, Microsoft Update ilkenize uygun olarak yüklenir.

    ![Microsoft Güncelleştirmeleri](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. Yükleme konumu kümesine  **<SystemDrive>\Program System Center 2012 R2\Virtual Machine Manager\bin**. Sağlayıcı yüklemeye başlamak için yükle düğmesine tıklayın.

    ![InstallLocation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. Sağlayıcı yüklendikten sonra sunucuyu kasaya kaydetmek için **Kaydet**'e tıklayın.

    ![InstallComplete](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. **Kasa adı** alanında, sunucunun kayıtlı olduğu kasanın adını doğrulayın. *İleri*’ye tıklayın.

    ![Sunucu kaydı](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. **İnternet Bağlantısı** kısmında VMM sunucusunda çalışan Sağlayıcı'nın İnternet'e nasıl bağlanacağını belirleyin. Sunucuda yapılandırılan varsayılan İnternet bağlantısı ayarlarını kullanmak için **Var olan proxy ayarları ile bağlan**'a tıklayın.

    ![İnternet Ayarları](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   * Özel bir ara sunucu kullanmak isterseniz bu ara sunucuyu Sağlayıcı'yı yüklemeden önce ayarlamanız gerekir. Özel ara sunucu ayarlarını yapılandırırken ara sunucu bağlantısını denetlemek için bir test çalıştırılır.
   * Özel bir ara sunucu kullanmak, veya varsayılan ara sunucunuz kimlik doğrulaması Ara sunucu adresi ve bağlantı noktası dahil olmak üzere ara sunucu bilgilerini girmeniz gereken gerekiyorsa.
   * VMM Sunucusu'ndan ve Hyper-V ana bilgisayarlarından aşağıdaki URL'lere erişim sağlanması gerekir:
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * [Azure Veri Merkezi IP Aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)'nda tanımlanan IP adreslerine ve HTTPS (443) protokolüne izin verin. Batı ABD ve kullanmayı düşündüğünüz Azure bölgesinin IP aralıklarını güvenilir listeye almanız gerekir.
   * Özel bir ara sunucu kullanırsanız otomatik olarak belirtilen ara sunucu kimlik bilgilerini kullanan VMM RunAs hesabı (DRAProxyAccount) oluşturulacaktır. Bu hesabın kimlik doğrulamasını başarıyla gerçekleştirebilmesi için ara sunucuyu yapılandırın. VMM RunAs hesabı ayarları VMM konsolundan değiştirilebilir. Bu işlemi gerçekleştirmek için **Ayarlar** çalışma alanını açın, **Güvenlik** bölümünü genişletin, **Farklı Çalıştır Hesapları**’na tıklayın ve ardından DRAProxyAccount parolasını değiştirin. Bu ayarın etkili olabilmesi için VMM hizmetinin yeniden başlatılması gerekir.
9. **Kayıt Anahtarı** kısmında, Azure Site Recovery'den indirdiğiniz anahtarı seçin ve VMM sunucusuna kopyalayın.
10. Şifreleme ayarı yalnızca Hyper-V sanal makinelerini Azure'daki VMM bulutlarına çoğaltırken kullanılır. İkincil bir siteye çoğaltma yapıyorsanız kullanılmaz.
11. **Sunucu adı** alanında, kasadaki VMM sunucusunu tanımlamak için bir kolay ad belirtin. Küme yapılandırmasında VMM kümesi rolü adını belirtin.
12. **Bulut meta verilerini eşitle** bölümünde VMM sunucusundaki tüm bulutlar için meta verileri kasa ile eşitlemek isteyip istemediğinizi seçin. Bu eylemin her sunucuda yalnızca bir kez gerçekleştirilmesi gerekir. Tüm bulutları eşitlemek istemezseniz bu ayarı işaretlemeden bırakıp her bulutu VMM konsolundaki bulut özelliklerinde bağımsız olarak eşitleyebilirsiniz.
13. İşlemi tamamlamak için **İleri**'ye tıklayın. Kayıttan sonra Azure Site Recovery tarafından VMM sunucusundan meta veriler alınır. Sunucu görüntülenen **VMM sunucuları** > **sunucuları** kasadaki.

    ![Sunucular](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>Komut satırı yüklemesi
Azure Site Recovery sağlayıcısı komut satırından da yüklenebilir. Bu yöntem, bir çekirdek Windows Server 2012 R2 için sunucu üzerinde sağlayıcı yüklemek için kullanılabilir.

1. Sağlayıcı yükleme dosyasını ve kayıt anahtarını bir klasöre indirin. Örneğin, C:\ASR.
2. System Center Virtual Machine Manager hizmetini durdurun
3. İle bir komut isteminden aşağıdaki komutları çalıştırarak sağlayıcı yükleyicisini ayıklamak **yönetici** ayrıcalıkları:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Sağlayıcı çalıştırarak yükleyin:

        C:\ASR> setupdr.exe /i
5. Sağlayıcıyı çalıştırarak kaydedin:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of the server> /Credentials <path of the credentials file> /EncryptionEnabled <full file name to save the encryption certificate>     

Burada Parametreler şunlardır:

* **/ Credentials**: kayıt anahtarı dosyasının bulunduğu konumu belirten zorunlu parametre  
* **/FriendlyName**: Azure Site Recovery portalında görünen Hyper-V konak sunucusunun adı için zorunlu parametre.
* **/ EncryptionEnabled**: yalnızca Azure senaryosuna vmm'de sanal makinelerinizin Azure bekleyen şifreleme gerekiyorsa kullanması gereken isteğe bağlı parametre. Sağladığınız dosya adı olduğundan lütfen emin bir **.pfx** uzantısı.
* **/proxyAddress**: Ara sunucunun adresini belirten isteğe bağlı parametre.
* **/proxyport**: Ara sunucunun bağlantı noktasını belirten isteğe bağlı parametre.
* **/ proxyusername**: (proxy kimlik doğrulaması gerektiriyorsa) Ara sunucu kullanıcı adını belirten isteğe bağlı parametre.
* **/ proxypassword**: (proxy kimlik doğrulaması gerektiriyorsa), proxy sunucusu ile kimlik doğrulaması için parolayı belirten isteğe bağlı parametre.  

## <a name="step-4-configure-cloud-protection-settings"></a>4. adım: Bulut yapılandırma koruma ayarları
VMM sunucusu kayıtlı sonra bulut koruma ayarlarını yapılandırabilirsiniz. Seçeneği etkinleştirilirse **Eşitle bulut verilerini kasayla** yüklediğinizde sağlayıcı VMM sunucusundaki tüm Bulutlar görünür **korunan öğeler** kasadaki sekmesi. Almadıysanız, belirli bir bulut Azure Site Recovery ile eşitleyebilirsiniz **genel** VMM konsolundaki bulut özellikleri sayfasında sekmesinde.

![Yayımlanan Bulut](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. Hızlı Başlangıç sayfasında **VMM Bulutları için koruma ayarla**'ya tıklayın.
2. Üzerinde **VMM Bulutları** sekmesinde, yapılandırmak ve Git istediğiniz Bulutu seçin **yapılandırma** sekmesi.
3. İçinde **hedef**seçin **VMM**.
4. İçinde **hedef konum**, kurtarma için kullanmak istediğiniz bulut yönetir yerinde VMM sunucusunu seçin.
5. İçinde **hedef bulut**, kaynak buluttaki sanal makinelerin yük devretme için kullanmak istediğiniz hedef Bulutu seçin. Şunlara dikkat edin:

   * Koruma sanal makineleri kurtarma gereksinimlerini karşılayan bir hedef bulut seçmenizi öneririz.
   * Bir buluta yalnızca bir tek bulut çifti ait olabilir — birincil veya bir hedef bulut olarak.
6. İçinde **kopyalama sıklığı**, ne sıklıkta belirtin verilerin 5he kaynak ve hedef konumlar arasında eşitlenmesi. Windows Server 2012 R2 Hyper-V ana çalıştırırken bu ayar yalnızca geçerli olduğunu unutmayın. Diğer sunucular için beş dakika, varsayılan ayar kullanılır.
7. İçinde **ek kurtarma noktaları**, ek noktaları oluşturmak isteyip istemediğinizi belirtin. Yalnızca en son kurtarma noktası bir birincil sanal makine için bir çoğaltma ana bilgisayar sunucusunda depolanır varsayılan sıfır değerini gösterir. Birden çok kurtarma noktasının etkinleştirilmesi ek depolama alanı her kurtarma noktasında depolanan anlık görüntüler için gerektirdiğini unutmayın. Varsayılan olarak, her kurtarma noktasının bir saatlik verileri içeren her saat kurtarma noktaları oluşturulur. VMM konsolunda sanal makine için atadığınız kurtarma noktası değeri Azure Site Recovery konsolunda atadığınız değerden daha küçük olmamalıdır.
8. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, uygulamayla tutarlı anlık görüntüleri ne sıklıkla oluşturulacağını belirtin. Hyper-V iki çeşit anlık görüntü kullanır: tüm sanal makinenin artımlı anlık görüntüsünü sunan standart anlık görüntü ve sanal makine içinde uygulama verilerinin belirli bir noktadaki anlık görüntüsünü alan uygulamayla tutarlı anlık görüntü. Uygulamayla tutarlı anlık görüntüler, anlık görüntü alınırken uygulamaların tutarlı bir durumda olmasını sağlamak için Birim Gölge Kopyası Hizmeti'ni (VSS) kullanır. Uygulamayla tutarlı anlık görüntüleri etkinleştirirseniz kaynak sanal makinelerde çalışan uygulamaların performansının etkileneceğini unutmayın. Ayarladığınız değerin, yapılandırdığınız ilave kurtarma noktası sayısından daha az olduğundan emin olun.

    ![Koruma ayarlarını yapılandırın](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. İçinde **veri aktarımı sıkıştırma**, aktarılan çoğaltılmış verilerin sıkıştırılmasının gerekli olup olmadığını belirtin.
10. İçinde **kimlik doğrulaması**, birincil ve kurtarma Hyper-V ana bilgisayar sunucuları arasında trafik kimliğinin nasıl belirtin. Çalışan bir Kerberos ortamı yapılandırılmış olmadığı sürece, HTTPS seçin. Azure Site Recovery, HTTPS kimlik doğrulaması için sertifikaları otomatik olarak yapılandırır. El ile yapılandırma gereklidir. Kerberos seçerseniz, konak sunucularının karşılıklı kimlik doğrulaması için Kerberos bileti kullanılır. Varsayılan olarak, Hyper-V ana bilgisayar sunucuları üzerinde Windows Güvenlik Duvarı'nda bağlantı noktası 8083 ve 8084 (Sertifikalar) yeniden açılır. Bu ayar yalnızca Windows Server 2012 R2'de çalışan Hyper-V konak sunucuları için geçerli olduğunu unutmayın.
11. İçinde **bağlantı noktası**, kaynak ve hedef ana bilgisayarlar üzerinde çoğaltma trafiği için dinleme bağlantı noktası numarasını değiştirin. Örneğin, hizmet kalitesi (QoS) ağ bant genişliği için çoğaltma trafiğini azaltma uygulamak isterseniz ayarı değiştirebilirsiniz. Bağlantı noktası başka bir uygulama tarafından kullanılmadığından ve Güvenlik Duvarı ayarlarında açık olup olmadığını denetleyin.
12. İçinde **çoğaltma yöntemini**, normal çoğaltma işlemi başlamadan önce ne ilk veri çoğaltma işlemi kaynaktan hedef konumlara, yapılacağını belirtin:

    * **Ağ üzerinden**— ağ üzerinden veri kopyalamak olabilir zaman alabilir ve yoğun bir kaynak. Bulut görece küçük sanal sabit diskler sanal makinelerle içeriyorsa ve birincil site ikincil siteye geniş bant genişliğine sahip bir bağlantı üzerinden bağlıysa, bu seçeneği kullanmanızı öneririz. Kopyalama hemen başlatmak veya bir süre seçin olduğunu belirtebilirsiniz. Ağ çoğaltmayı kullanırsanız, yoğun olmayan saatlerde zamanlamanızı öneririz.
    * **Çevrimdışı**— bu yöntemi dış medya kullanarak ilk çoğaltma gerçekleştirilir belirtir. Ağ performansı veya coğrafi olarak Uzak konumlar için azalmasını önlemeyi istiyorsanız kullanışlıdır. Bu yöntemi kullanmak için kaynak bulutun ve hedef bulut üzerinde içeri aktarma konumunu dışarı aktarma konumunu belirtin. Bir sanal makine için korumayı etkinleştirdiğinizde sanal sabit disk belirtilen dışa aktarma konumuna kopyalanır. Hedef siteye gönderin ve içeri aktarma konumuna kopyalayın. Sistem içeri aktarılan bilgileri çoğaltma sanal makinelerine kopyalar.
13. Seçin **silmek çoğaltma sanal makinesi** seçerek sanal makine korumayı durdurursanız, çoğaltma sanal makinesinin silinmesi gerektiğini belirtmek için **silmek sanal makine için korumayı** bulut özellikleri sanal makineleri sekmesinde seçeneği. Bu ayar etkinken, korumayı devre dışı bıraktığınızda sanal makineyi Azure Site Recovery'den kaldırılır, sanal makine için Site Recovery ayarları VMM konsolundan kaldırılır ve çoğaltma silinir.

    ![Koruma ayarlarını yapılandırın](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

Ayarlar kaydedildikten sonra bir iş oluşturulur ve bu iş **İşler** sekmesinden izlenebilir. VMM kaynak bulutundaki tüm Hyper-V sunucular çoğaltma için yapılandırılır. Bulut ayarları değiştirilebilir **yapılandırma** sekmesi. Hedef konumu veya hedef bulut değiştirmek istiyorsanız bulut yapılandırmasını kaldırın ve Bulutu yeniden yapılandırmanız gerekir.

### <a name="prepare-for-offline-initial-replication"></a>Çevrimdışı ilk çoğaltma için hazırlama
Çevrimdışı ilk çoğaltma için hazırlamak için aşağıdaki eylemleri yapmanız gerekir:

* Kaynak sunucuda veri dışarı aktarma yerini alacak bir yolu konumuna belirtirsiniz. Dışarı aktarma yolundaki VMM hizmeti için NTFS ve Paylaşım izinleri için tam denetim atayın. Hedef sunucuda veri içe aktarma ortaya çıkar bir yolu konumuna belirtirsiniz. Bu alma yolu aynı izinleri atayın.
* İçe veya dışa aktarma yol paylaşılıyorsa, VMM hizmet hesabının paylaşılan bulunduğu uzak bilgisayarda yönetici, Power User, Print Operator veya sunucu işleci grup üyelikleri atayın.
* Eklemek için herhangi bir farklı çalıştır hesabı kullanıyorsanız, içeri ve dışarı aktarma yollarındaki konakları okuma atayın ve vmm'de farklı çalıştır hesapları için yazma izinleri.
* Geri döngü yapılandırma Hyper-V tarafından desteklenmediği için içeri ve dışarı aktarma paylaşımları bir Hyper-V konak sunucusu olarak kullanılan herhangi bir bilgisayarda bulunmuyor.
* Active Directory'de, her Hyper-V ana bilgisayar sunucusunda korumak, etkinleştirmek ve yapılandırmak istediğiniz sanal makine içeren kısıtlı temsilcisi içeri ve dışarı aktarma yollarındaki gibi bulunduğu olduğu uzak bilgisayarların güvenmesi için:
  1. Etki alanı denetleyicisinde açın **Active Directory Kullanıcıları ve Bilgisayarları**.
  2. Konsol ağacında **DomainName** > **bilgisayarlar**.
  3. Hyper-V ana bilgisayar sunucu adına sağ tıklayın > **özellikleri**.
  4. Üzerinde **temsilci** sekmesini T**bu bilgisayara yalnızca belirtilen hizmetlere temsilci seçmek için paslanma**.
  5. Tıklatın **herhangi bir kimlik doğrulama protokolünü kullan**.
  6. Tıklatın **ekleme** > **kullanıcıları ve Bilgisayarları**.
  7. Dışarı aktarma yoluna barındıran bilgisayarın adını yazın > **Tamam**. Kullanılabilir hizmetler listeden CTRL tuşunu basılı tutun ve **CIFS** > **Tamam**. Alma yolu barındıran bilgisayarın adı için yineleyin. Ek Hyper-V konak sunucuları için gerektiği kadar yineleyin.

## <a name="step-5-configure-network-mapping"></a>5. adım: ağ eşlemesini yapılandırma
1. Hızlı Başlangıç sayfasında **Ağları eşle**'ye tıklayın.
2. Ağlarını eşlemek istediğiniz kaynak VMM sunucusunu ve ağlar eşleştirilecek hedef VMM sunucusunu seçin. Kaynak ağların ve ilişkili hedef ağlarının listesi görüntülenir. Şu anda eşlenmemiş ağlar için boş bir değer gösterilir.
3. Bir ağ seçin **kaynak üzerinde ağ** > **harita**. Hizmet, hedef sunucu üzerindeki VM ağlarını algılar ve bunları görüntüler. Her ağın alt ağlarını görüntülemek için kaynak ve hedef ağ adlarının yanındaki bilgi simgesine tıklayın.

    ![Ağ eşlemesini yapılandırma](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. İletişim kutusunda hedef VMM sunucusunda VM ağları birini seçin.

    ![Hedef ağ Seç](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. Hedef ağ seçtiğinizde, kaynak ağı kullanan korumalı Bulutlar gösterilir. Koruma için kullanılan Bulutlar ile ilişkili kullanılabilir hedef ağlar da görüntülenir. Koruma için kullandığınız tüm bulutların kullanabildiği bir hedef ağ seçmeniz önerilir. Ya da aynı zamanda VMM sunucusuna gidin ve seçmek için istediğiniz vm ağına karşılık gelen mantıksal ağ eklemek için bulut özelliklerini değiştirin.
6. Eşleme işlemini tamamlamak için onay işaretine tıklayın. Eşleme ilerleme durumunu izlemek bir iş başlatılır. Üzerinde görüntülemek **işleri** sekmesi.

## <a name="step-6-configure-storage-mapping"></a>6. adım: depolama eşlemesi yapılandırma
Hedef Hyper-V konak sunucusu için bir kaynak Hyper-V konak sunucusunda bir sanal makine çoğalttığınızda, varsayılan olarak Hyper-V Yöneticisi'nde hedef Hyper-V ana bilgisayarı için belirtilen varsayılan konuma çoğaltılan veriler depolanır. Çoğaltılan verilerin depolandığı üzerinde daha fazla denetim için depolama eşlemeleri aşağıdaki gibi yapılandırabilirsiniz:

1. Depolama sınıflandırmaları hem kaynak hem de hedef VMM sunucularında tanımlayın. [Daha fazla bilgi edinin](https://technet.microsoft.com/library/gg610685.aspx). Sınıflandırmaları kaynak ve hedef bulutlarındaki Hyper-V ana bilgisayar sunucularına kullanılabilir olması gerekir. Sınıflandırmaları depolama aynı türde olması gerekmez. Örneğin, SMB paylaşımları csv içeren bir hedef sınıflandırmasına içeren bir kaynak sınıflandırma eşleyebilirsiniz.
2. Sınıflandırmaları hazır olduktan sonra eşlemeleri oluşturabilirsiniz. Bunu yapmak için **Hızlı Başlangıç** sayfa > **eşleme depolama**.
3. Tıklatın **depolama** sekmesini > **eşleme depolama sınıflandırmaları**.
4. Üzerinde **eşleme depolama sınıflandırmaları** sekmesinde sınıflandırmaları kaynağı seçin ve VMM sunucuyu hedefleyebilir. Ayarlarınızı kaydedin.

    ![Hedef ağ Seç](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>7. adım: sanal makine korumayı etkinleştirin
Sunucular, bulutlar ve ağlar doğru şekilde yapılandırıldıktan sonra buluttaki sanal makineler için korumayı etkinleştirebilirsiniz.

1. Üzerinde **sanal makineleri** sanal makinenin bulunduğu bulutun sekmesini tıklatın, **korumayı etkinleştir** > **sanal makineleri ekleyin**.
2. Buluttaki sanal makineler listesinden korumak istediğinizi seçin.

    ![Sanal makine korumasını etkinleştirme](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. Korumayı etkinleştirme eyleminin ilerleyişini izleyin **işleri** sekmesi, ilk çoğaltma dahil olmak üzere. Korumayı Sonlandır işini çalıştıktan sonra sanal makine yük devretme için hazır olur. Koruma etkinleştirilip sanal makineler çoğaltıldıktan sonra bunları Azure'da görüntüleyebilirsiniz.

    ![Sanal makine koruma işi](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> VMM konsolunda sanal makineler için korumayı etkinleştirebilirsiniz. Tıklatın **korumayı etkinleştir** araç çubuğunda **Azure Site Recovery** sanal makine özellikleri sekmesindedir.
>
>

### <a name="on-board-existing-virtual-machines"></a>Yerleşik mevcut sanal makineler
Hyper-V çoğaltma ile çoğaltma mevcut sanal makineler VMM varsa yerleşik için bunları Azure Site Recovery koruması için aşağıdaki gibi ihtiyacınız vardır:

1. Birincil ve ikincil bulut doğrulayın. Varolan sanal makine barındıran Hyper-V server birincil buluta bulunur ve çoğaltma sanal makine barındıran Hyper-V sunucusu ikincil bulutta bulunduğundan emin olun. Emin olun, Bulutlar için koruma ayarlarını yapılandırdığınız. Ayarları şu anda Hyper-V çoğaltma için yapılandırılan eşleşmesi gerekir. Aksi durumda sanal makine çoğaltma beklendiği gibi çalışmayabilir.
2. Ardından birincil sanal makine için korumayı etkinleştirin. Azure Site Recovery ile VMM aynı çoğaltma konak ve sanal makine algılandığında, ve Azure Site Recovery yeniden kullanmak ve bulut yapılandırması sırasında yapılandırılan ayarları kullanarak çoğaltmayı yeniden oluşturmak sağlayacak.

## <a name="test-your-deployment"></a>Dağıtımınızı test edin
Dağıtımınızı test etmek için bir yük devretme sınaması için tek bir sanal makine çalıştırmak veya birden çok sanal makine içeren bir kurtarma planı oluşturmak ve bir yük devretme sınaması için plan çalıştırın.  Yük devretme testi, yük devretme işleminizi ve kurtarma mekanizmanızı yalıtılmış bir ortamda benzetimli olarak gerçekleştirir.

### <a name="create-a-recovery-plan"></a>Kurtarma planı oluşturma
1. Üzerinde **kurtarma planları** sekmesini tıklatın, **kurtarma planı oluşturma**.
2. Kurtarma planı ve kaynak ve hedef VMM sunucuları için bir ad belirtin. Kaynak sunucu yük devretme ve kurtarma için etkinleştirilmiş sanal makineleri olması gerekir. Seçin **Hyper-V** Hyper-V çoğaltma için yapılandırılan Bulutlar görüntülemek için.

    ![Kurtarma planı oluşturma](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. İçinde **sanal makineyi Seç**, çoğaltma gruplarını seçin. Çoğaltma grubuyla ilişkili tüm sanal makineleri seçili ve kurtarma planına eklenir. Bu sanal makineler, kurtarma planının varsayılan grubu olan Grup 1'e eklenir. gerekli olursa, daha fazla grup ekleyebilirsiniz. Çoğaltma sanal makineler kurtarma planı grupların sırasını uygun olarak başlatılır sonra unutmayın.

    ![Sanal makineleri ekleyin](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

Bir kurtarma planı oluşturulduktan sonra listede göründüğü **kurtarma planları** sekmesi.

### <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma
1. **Kurtarma Planları** sekmesinde planı seçin ve **Yük devretme Testi**'ne tıklayın.
2. Üzerinde **onaylayın yük devretme testi** sayfasında, **hiçbiri**. Bu seçenek başarısız çoğaltma sanal makineleri üzerinde etkin unutmayın herhangi bir ağa bağlanmayacaktır. Bu sanal makine beklendiği gibi yöneltilir ancak çoğaltma ağ ortamınızı test değil sınayın. Nasıl yapılır bakabilir [bir yük devretme testi](site-recovery-failover.md) farklı ağ seçeneklerini kullanma hakkında daha fazla ayrıntı için.
3. Test sanal makinesi, çoğaltma sanal makinesi bulunduğu konak aynı bilgisayarda oluşturulur. Çoğaltma sanal makinesi bulunduğu aynı bulut eklenir.

### <a name="run-a-recovery-plan"></a>Bir kurtarma planı Çalıştır
Çoğaltma sonrasında çoğaltma sanal makinesi, birincil sanal makinenin IP adresi ile aynı olan bir IP adresine sahip olmayabilir. Sanal makineler, kullanmakta olduğunuz DNS sunucusu güncelleştirilecek başladıktan sonra. Güncelleştirme zamanında güncelleştirme emin olmak için DNS sunucusu için bir komut dosyası da ekleyebilirsiniz.

#### <a name="script-to-retrieve-the-ip-address"></a>IP adresi almak için komut dosyası
IP adresi almak için bu örnek komut dosyasını çalıştırın.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-to-update-dns"></a>DNS'yi güncelleştirmek için komut dosyası
DNS, önceki örnek komut dosyası kullanarak alınan IP adresi belirtme güncelleştirmek için bu örnek komut dosyasını çalıştırın.

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>Site Recovery için gizlilik bilgileri
Bu bölümde, Microsoft Azure Site Recovery hizmeti ("hizmet") için ek gizlilik bilgileri sağlar. Microsoft Azure Hizmetleri için gizlilik bildirimini görüntülemek için bkz: [Microsoft Azure gizlilik bildirimi](http://go.microsoft.com/fwlink/?LinkId=324899)

**Özellik: kayıt**

* **Ne yaptığını**: böylece sanal makineler korunabilir sunucu hizmeti ile kaydeder
* **Toplanan bilgiler**: hizmeti kaydetme topladıktan sonra işler ve olağanüstü durum kurtarma VMM sunucusunda VMM sunucusu hizmet adını ve sanal makine Bulutları adını kullanarak sağlamak üzere atadığı VMM sunucusundan yönetim sertifika bilgileri iletir.
* **Bilgilerin kullanımı**:

  * Yönetim sertifikası — bu tanımlamak ve hizmete erişmek için kayıtlı VMM sunucusuna kimlik doğrulaması için kullanılır. Hizmet sertifikasının ortak anahtar bölümünü yalnızca kayıtlı VMM sunucusuna erişmesini bir belirteç güvenliğini sağlamak için kullanır. Sunucunun hizmet özelliklerini erişmek için bu belirteci kullanması gerekir.
  * VMM sunucusunun adını — tanımlamak ve Bulutlar olduğu bulunduğu uygun VMM sunucusu ile iletişim kurmak için VMM Sunucu adı gereklidir.
  * Bulut VMM sunucusundan adları — eşleştirme/eşleştirmesini kaldırma özelliği aşağıda açıklanan Hizmet bulut kullanırken bulut adı gereklidir. Birincil veri merkezi bulut kurtarma veri merkezinde başka bir bulut ile eşleştirmeye karar verdiğinizde, Kurtarma veri merkezi tüm Bulutlar adlarını sunulur.
* **Seçim**: Bu bilgiler ve hizmetin doğru kayıtlı VMM sunucusunu tanımlamak için de Azure Site Recovery koruması sağlamak istediğiniz VMM sunucusunu tanımlamak için yardımcı hizmeti kayıt işleminin önemli bir parçası olduğundan. Bu bilgilerin hizmete gönderilmesini istemiyorsanız, bu hizmet kullanmayın. Sunucunuza kaydetmek ve onu kaydı, daha sonra istiyorsanız (Azure portalı olan) hizmet portalından VMM Sunucu bilgilerini silerek bunu yapabilirsiniz.

**Özellik: Azure Site Recovery korumasını etkinleştirin**

* **Ne yaptığını**: Azure Site Recovery VMM sunucusunda yüklü sağlayıcısı olan hizmet ile iletişim için conduit. VMM işlemde barındırılan bir dinamik bağlantı kitaplığı (DLL) sağlayıcıdır. Sağlayıcı yüklendikten sonra "Veri merkezi Kurtarma" özelliği VMM Yönetici konsolunda etkin. Tüm yeni veya var olan sanal makine bir bulutta sanal makine korunmasına yardımcı olmak için "veri merkezi Kurtarma" adlı bir özellik etkinleştirebilirsiniz. Bu özellik ayarlandıktan sonra sağlayıcı adı ve sanal makinenin kimliği hizmetine gönderir. Windows Server 2012 veya Windows Server 2012 R2 Hyper-V çoğaltma teknolojisiyle sanal koruması etkin. Sanal makine verilerini (genellikle bir farklı "Kurtarma" veri merkezinde bulunan) başka bir Hyper-V ana bilgisayardan çoğaltılan.
* **Toplanan bilgiler**: hizmet toplar, işler ve adı, kimliği, sanal ağ ve bulut adını içeren sanal makine için meta veri aktaran ait olduğu.
* **Bilgilerin kullanımı**: Hizmet, hizmet portalınızda sanal makine bilgilerini doldurmak için yukarıdaki bilgileri kullanır.
* **Seçim**: Bu hizmet, önemli bir parçasıdır ve devre dışı bırakılamaz. Hizmete gönderilen bu bilgileri istemiyorsanız, herhangi bir sanal makine için Azure Site Recovery korumasını etkinleştirmeyin. İçin hizmet sağlayıcı tarafından gönderilen tüm veriler HTTPS üzerinden gönderilen olduğunu unutmayın.

**Özellik: Kurtarma planı**

* **Ne yaptığını**: Bu özellik "Kurtarma" veri merkezi için bir düzenleme planı oluşturmanıza yardımcı olur. İçinde sanal makine ya da sanal makineler grubunun kurtarma sitesinde başlatılmalıdır düzenini tanımlayabilirsiniz. Ayrıca, her bir sanal makine için kurtarma zamanında çalıştırma ya da her el ile eylemin gerçekleştirilmesine olacak şekilde otomatik herhangi bir komut dosyası belirtebilirsiniz. Yük devretme (sonraki bölümde yer alan) genellikle Eşgüdümlü kurtarma Kurtarma planlaması düzeyinde tetiklenir.
* **Toplanan bilgiler**: hizmet toplar, işler ve sanal makine meta veri ve meta veri Otomasyon betikleri ve el ile işlem Notları dahil olmak üzere kurtarma planı için meta veri aktarır.
* **Bilgilerin kullanımı**: yukarıda açıklanan meta veri hizmeti portalınızın kurtarma planı oluşturmak için kullanılır.
* **Seçim**: Bu hizmet, önemli bir parçasıdır ve devre dışı bırakılamaz. Hizmete gönderilen bu bilgileri istemiyorsanız, Kurtarma planları bu hizmette yapı yok.

**Özellik: Ağ eşlemesi**

* **Ne yaptığını**: Bu özellik, ağ birincil veri merkezi kurtarma veri merkezine eşlemek sağlar. Sanal makineleri kurtarma sitesinde kurtarılan olduğunda, bu eşleme için ağ bağlantısı oluşturmada yardımcı olur.
* **Toplanan bilgiler**: parçası olarak ağ eşleme özelliğini, hizmet toplar, işler ve mantıksal ağları (birincil ve datacenter) her site için meta verileri iletir.
* **Bilgilerin kullanımı**: hizmet kullanır meta verileri servis portalınız doldurmak için ağ bilgilerinin nerede eşleyebilirsiniz.
* **Seçim**: Bu hizmet, önemli bir parçasıdır ve devre dışı bırakılamaz. Hizmete gönderilen bu bilgileri istemiyorsanız, ağ eşleme özelliğini kullanmayın.

**Özellik: Yük devretme - planlanmış, Planlanmayan, test**

* **Ne yaptığını**: Bu özellik, bir sanal makinenin yük devretme bir VMM tarafından yönetilen veri merkezinden başka bir VMM tarafından yönetilen veri merkezine yardımcı olur. Yük devretme işlemi, kendi hizmet portalı kullanıcı tarafından tetiklenir. Bir yük devretme için olası nedenler şunlardır planlanmamış bir olay (örneğin doğal disaster0; olması durumunda (örneğin veri merkezi yük dengeleme) olay; test yük devretme (örneğin bir kurtarma planı prova).

VMM sunucusundaki sağlayıcı hizmetinden olay bildirimi ve VMM arabirimleri aracılığıyla Hyper-V konağı üzerinde bir yük devretme işlemi yürütür. Sanal makinenin bir Hyper-V ana (genellikle farklı "Kurtarma" veri merkezinde çalışan) başka bir bilgisayardan gerçek yük devretme, Windows Server 2012 veya Windows Server 2012 R2 Hyper-V çoğaltma teknolojisiyle ele alınır. Yük devretme işlemi tamamlandıktan sonra "Kurtarma" veri merkezi VMM sunucusunda yüklü sağlayıcı başarı bilgi hizmetine gönderir.

* **Toplanan bilgiler**: Hizmet, hizmet portalınızda yük devretme eylem bilgileri durumunu doldurmak için yukarıdaki bilgileri kullanır.
* **Bilgilerin kullanımı**: hizmet Yukarıdaki bilgilerin aşağıdaki gibi kullanır:

  * Yönetim sertifikası — bu tanımlamak ve hizmete erişmek için kayıtlı VMM sunucusuna kimlik doğrulaması için kullanılır. Hizmet sertifikasının ortak anahtar bölümünü yalnızca kayıtlı VMM sunucusuna erişmesini bir belirteç güvenliğini sağlamak için kullanır. Sunucunun hizmet özelliklerini erişmek için bu belirteci kullanması gerekir.
  * VMM sunucusunun adını — tanımlamak ve Bulutlar olduğu bulunduğu uygun VMM sunucusu ile iletişim kurmak için VMM Sunucu adı gereklidir.
  * Bulut VMM sunucusundan adları — eşleştirme/eşleştirmesini kaldırma özelliği aşağıda açıklanan Hizmet bulut kullanırken bulut adı gereklidir. Birincil veri merkezi bulut kurtarma veri merkezinde başka bir bulut ile eşleştirmeye karar verdiğinizde, Kurtarma veri merkezi tüm Bulutlar adlarını sunulur.
* **Seçim**: Bu hizmet, önemli bir parçasıdır ve devre dışı bırakılamaz. Hizmete gönderilen bu bilgileri istemiyorsanız, bu hizmet kullanmayın.

## <a name="next-steps"></a>Sonraki adımlar
Ortamınızı beklendiği gibi çalıştığını denetlemek için bir yük devretme testi çalıştırdıktan sonra [hakkında bilgi edinin](site-recovery-failover.md) yerine farklı türde.
