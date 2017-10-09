---
title: aaaReplicate Hyper-V sanal makineleri tooa Azure Site Recovery ile ikincil site | Microsoft Docs
description: "VMM Bulutları tooa ikincil VMM sitesi kullanarak Hyper-V sanal makineleri tooreplicate hello Azure portalına nasıl açıklar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: b33a1922-aed6-4916-9209-0e257620fded
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: e79dbdeab74266e843e5146298dc5aadfe66b5df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-hello-azure-portal"></a>Hyper-V sanal makineleri hello Azure portal kullanarak VMM Bulutları tooa ikincil VMM sitesi Çoğalt
> [!div class="op_single_selector"]
> * [Azure portal](site-recovery-vmm-to-vmm.md)
> * [Klasik portal](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Bu makalede nasıl tooreplicate System Center Virtual Machine Manager (VMM) bulutlarında yönetilen Hyper-V sanal makineleri şirket içi ikincil site tooa kullanarak [Azure Site Recovery](site-recovery-overview.md) hello Azure Portalı'nda. Bu konu hakkında daha fazla bilgi edinin [senaryo mimarisinin](site-recovery-components.md).

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Ön koşullar

**Önkoşul** | **Ayrıntılar**
--- | ---
**Azure** | Bir [Microsoft Azure](http://azure.microsoft.com/) hesabınızın olması gerekir. [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz. Site Recovery fiyatlandırması hakkında [daha fazla bilgi edinin](https://azure.microsoft.com/pricing/details/site-recovery/).
**Şirket içi VMM** | İki VMM sunucusu, bir hello birincil sitedeki ve hello ikincil birinde olması önerilir.<br/><br/> Tek bir VMM sunucusundaki Bulutlar arasında çoğaltabilirsiniz.<br/><br/> VMM sunucuları çalışıyor. en az hello en son güncelleştirmeleri içeren System Center 2012 SP1.<br/><br/> VMM sunucuları Internet erişimine gerek vardır.
**VMM Bulutları** | Her bir VMM sunucusunun bir veya daha fazla bulut olmalıdır ve tüm Bulutlar hello Hyper-V Kapasite profili kümesine sahip olması gerekir. <br/><br/>Bulut bir veya daha fazla VMM ana bilgisayar grubu içermesi gerekir.<br/><br/> Yalnızca bir VMM sunucunuz varsa, en az iki bulut, tooact olarak birincil ve ikincil gerekir.
**Hyper-V** | Hyper-V sunucuları çalışıyor olmalıdır en az Windows Server 2012 hello Hyper-V rolüne sahip ve hello son güncelleştirmelerin yüklü olması.<br/><br/> Bir Hyper-V sunucusunun bir veya daha fazla VM içermesi gerekir.<br/><br/>  Hyper-V ana bilgisayar sunucuları konak grupları hello birincil ve ikincil VMM bulutlarında yer.<br/><br/> Windows Server 2012 R2'de bir kümede Hyper-V çalıştırırsanız, yükleme [2961977 güncelleştir](https://support.microsoft.com/kb/2961977)<br/><br/> Windows Server 2012'de bir kümede Hyper-V çalıştırırsanız, bir statik IP adresi tabanlı kümeniz varsa küme aracısının otomatik olarak oluşturulmaz. Merhaba küme aracısını el ile yapılandırın. [Daha fazla bilgi edinin](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Hyper-V sunucuları Internet erişimine gerek vardır.
**URL'leri** | VMM sunucuları ve Hyper-V konakları mümkün tooreach olmalıdır bu URL'leri:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]

## <a name="deployment-steps"></a>Dağıtım adımları

Neler aşağıda verilmiştir:

1. Ön koşulları doğrulayın.
2. Merhaba VMM sunucusu ve Hyper-V konakları hazırlayın.
3. Kurtarma Hizmetleri kasası oluşturun. Merhaba kasası yapılandırma ayarlarını içeren, çoğaltma ve yönetir.
4. Kaynak ve hedef çoğaltma ayarlarını belirtin.
5. Merhaba Mobility hizmeti sanal makineleri dağıtma tooreplicate istiyor.
6. Çoğaltma için hazırlanamadı ve Hyper-V sanal makineleri için çoğaltmayı etkinleştirin.
7. Her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırın.

## <a name="prepare-vmm-servers-and-hyper-v-hosts"></a>VMM sunucuları ve Hyper-V ana bilgisayarları hazırlama

tooprepare dağıtımı için:

1. Merhaba VMM sunucusu ve Hyper-V konakları yukarıda açıklanan hello Önkoşullar uyması ve gerekli hello URL'lere erişebildiğinden emin olun.
2. Böylece yapılandırabileceğiniz VMM ağları ayarlayın [ağ eşlemesi](#network-mapping-overview).

    - Merhaba kaynağı Hyper-V konak sunucusu üzerinde sanal makineleri bağlı tooa VMM VM ağ olduğundan emin olun. Bu ağ hello Bulutu ile ilişkili mantıksal ağ bağlantılı tooa olmalıdır.
    Kurtarma için kullanacağınız hello ikincil bulut yapılandırılmış karşılık gelen VM ağı olduğundan emin olun. Bir VM ağı hello ikincil bulutla ilişkilendirilen mantıksal ağ bağlantılı tooa olmalıdır.

3. Hazırlama bir [tek sunucu dağıtımı](#single-vmm-server-deployment)tooreplicate VM'ler hello bulutlarda arasında istiyorsanız aynı VMM sunucusu.

## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. **Yeni** > **Yönetim** > **Kurtarma Hizmetleri** seçeneklerine tıklayın.
3. İçinde **adı**, bir kolay ad tooidentify hello kasası belirtin. Birden fazla aboneliğiniz varsa bunlardan birini seçin.
4. [Kaynak grubu oluşturun](../azure-resource-manager/resource-group-template-deploy-portal.md) veya var olan bir grubu seçin. Bir Azure bölgesi belirtin. Makine çoğaltılmış toothis bölge yok. desteklenen toocheck bölgeler coğrafi kullanılabilirlik kısmına bakın [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Tooquickly erişim hello hello Pano kasadan istiyorsanız, **PIN toodashboard** > **kasa Oluştur**.

    ![Yeni kasa](./media/site-recovery-vmm-to-vmm/new-vault-settings.png)

Merhaba yeni kasa görünür hello üzerinde **Pano**, **tüm kaynakları**ve hello ana **kurtarma Hizmetleri kasaları** dikey.


## <a name="choose-a-protection-goal"></a>Koruma hedefi seçin

Ne seçin tooreplicate ve tooreplicate için istediğiniz istiyor.

2. Tıklatın **Site Recovery** > **1. adım: altyapıyı hazırlama** > **koruma hedefi**.
3. Seçin **toorecovery site**seçip **Evet, Hyper-V ile**.
4. Seçin **Evet** VMM toomanage hello Hyper-V konakları kullanmakta olduğunuz tooindicate.
5. Seçin **Evet** bir ikincil VMM sunucunuz varsa. Tek bir VMM sunucusundaki Bulutlar arasında çoğaltma dağıtıyorsanız tıklatın **Hayır**. Daha sonra, **Tamam**'a tıklayın.

    ![Hedefleri seçme](./media/site-recovery-vmm-to-vmm/choose-goals.png)

## <a name="set-up-hello-source-environment"></a>Merhaba kaynak ortamını ayarlama

Hello Azure Site kurtarma sağlayıcısı VMM sunucularında yükleme ve bulmak ve sunucuları hello kasaya kaydetmek.

1. Tıklatın **1. adım: altyapıyı hazırlama** > **kaynak**.

    ![Kaynağı ayarlama](./media/site-recovery-vmm-to-vmm/goals-source.png)
2. İçinde **kaynağı**, tıklatın **+ VMM** tooadd bir VMM sunucusu.

    ![Kaynağı ayarlama](./media/site-recovery-vmm-to-vmm/set-source1.png)
3. İçinde **Sunucu Ekle**, denetleyin **System Center VMM sunucusunun** görünür **sunucu türü** ve hello VMM sunucusunun hello karşılayan [Önkoşullar](#prerequisites).
4. Hello Azure Site Recovery sağlayıcısı yükleme dosyasını indirin.
5. Merhaba kayıt anahtarını indirin. Kurulumu çalıştırırken buna ihtiyacınız olur. Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.

    ![Kaynağı ayarlama](./media/site-recovery-vmm-to-vmm/set-source3.png)
6. Hello Azure Site Recovery sağlayıcısı hello VMM sunucusuna yükleyin. Gerekmeyen tooexplicitly herhangi bir şey Hyper-V ana bilgisayar sunucuları üzerinde yükleyin.


### <a name="install-hello-azure-site-recovery-provider"></a>Hello Azure Site Recovery sağlayıcısı yükleme

1. Her VMM sunucusunda Hello sağlayıcı kurulum dosyasını çalıştırın. VMM bir kümede dağıtılıyorsa, yüklediğiniz ilk kez hello aşağıdaki hello yapın:
    -  Hello sağlayıcısı etkin bir düğümüne yükleyin ve hello yükleme tooregister hello VMM sunucusu hello kasasında tamamlayın.
    - Ardından, hello sağlayıcısı üzerinde hello diğer düğümlere yükleyin. Küme düğümleri tüm çalışmalı hello hello sağlayıcısı aynı sürümü.
2. Kurulum, birkaç ön koşul denetimlerini çalıştırır ve izni toostop hello VMM hizmeti ister. Kurulum bittiğinde VMM hizmeti hello otomatik olarak yeniden başlatılır. Bir VMM kümesinde yüklerseniz, istendiğinde toostop hello küme rolünü demektir.
3. İçinde **Microsoft Update**, sağlayıcı güncelleştirmeleri Microsoft Update ilkenize uygun yüklendiğini toospecify seçebilirsiniz.
4. İçinde **yükleme**kabul edin veya hello varsayılan yükleme konumunu değiştirmek ve tıklatın **yükleme**.

    ![Yükleme konumu](./media/site-recovery-vmm-to-vmm/provider-location.png)
5. Yükleme tamamlandıktan sonra tıklayın **kaydetmek** hello kasadaki tooregister hello sunucu.

    ![Yükleme konumu](./media/site-recovery-vmm-to-vmm/provider-register.png)
6. İçinde **kasa adı**, hangi hello sunucunun kaydedileceği hello kasasının hello adını doğrulayın. *İleri*’ye tıklayın.

    ![Sunucu kaydı](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
7. İçinde **Internet bağlantısı**, hello VMM sunucusunda çalışan hello sağlayıcısı tooAzure nasıl bağlandığını belirtin.

    ![İnternet Ayarları](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   - Bu hello sağlayıcısına bağlanmak doğrudan toohello belirtebilirsiniz Internet veya bir proxy üzerinden.
   - Gerekiyorsa proxy ayarlarını belirtin.
   - Bir proxy kullanıyorsanız, VMM RunAs hesabı (DRAProxyAccount) belirtilen hello kullanılarak otomatik olarak oluşturulan proxy kimlik bilgileri. Bu hesap başarıyla doğrulanabilmesi hello proxy sunucusunu yapılandırın. Merhaba RunAs hesabı ayarları hello VMM konsolundan değiştirilebilir > **ayarları** > **güvenlik** > **farklı çalıştır hesapları**. Merhaba VMM hizmet tooupdate değişiklikleri yeniden başlatın.
8. İçinde **kayıt anahtarı**seçin hello anahtarı Azure Site Recovery'den indirdiğiniz ve toohello VMM sunucuya kopyalanır.
9. Merhaba şifreleme ayarı yalnızca VMM Bulutları tooAzure Hyper-V sanal makineleri çoğaltma yapıyorsanız kullanılır. İkincil site tooa çoğaltıyorsanız kullanılmaz.
10. İçinde **sunucu adı**, hello kasasında bir kolay ad tooidentify hello VMM sunucusu belirtin. Bir küme yapılandırmasında hello VMM kümesi rolü adını belirtin.
11. İçinde **Eşitle bulut meta verileri**hello kasası ile Merhaba VMM sunucusundaki tüm Bulutlar için toosynchronize meta verileri istediğinizi seçin. Bu eylem, yalnızca bir kez her sunucuda toohappen gerekir. Tüm bulutlar toosynchronize istemiyorsanız bu ayarı işaretsiz bırakın ve hello hello VMM konsolundaki bulut özellikleri ayrı ayrı her Bulutu eşitleyin.
12. Tıklatın **sonraki** toocomplete hello işlemi. Kayıttan sonra Azure Site Recovery tarafından hello VMM sunucusundan meta veriler alınır. Merhaba sunucu üzerinde hello görüntülenen **VMM sunucuları** hello sekmesinde **sunucuları** hello kasası sayfasında.

    ![Sunucu](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)
13. Merhaba sunucu hello Site Recovery konsolunda kullanılabilir duruma getirildikten sonra **kaynak** > **kaynağı** hello VMM sunucusu ve select hello bulut hello Hyper-V ana bilgisayar bulunduğu seçin. Daha sonra, **Tamam**'a tıklayın.

Merhaba sağlayıcısı hello komut satırından da yükleyebilirsiniz:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Merhaba hedef ortamını ayarlama

Merhaba hedef VMM sunucusunu ve Bulutu seçin.

1. Tıklatın **altyapıyı hazırlama** > **hedef**ve toouse istediğiniz select hello hedef VMM sunucusu.
2. Site Recovery ile eşitlenmiş Bulutlar hello sunucuda görüntülenir. Merhaba hedef bulut seçin.

   ![Hedef](./media/site-recovery-vmm-to-vmm/target-vmm.png)

## <a name="set-up-replication-settings"></a>Çoğaltma ayarlarını belirleme

- Bir çoğaltma ilkesi oluşturduğunuzda, tüm ana bilgisayar hello İlkesi'ni kullanarak gerekir sahip hello aynı işletim sistemi. Windows Server'ın farklı sürümlerini çalıştıran Hyper-V konakları Hello VMM bulut içerebilir ancak bu durumda, birden fazla çoğaltma ilkesi gerekir.
- Çevrimdışı ilk çoğaltma hello gerçekleştirebilirsiniz. [Daha fazla bilgi](#prepare-for-initial-offline-replication)

1. Yeni bir çoğaltma ilkesi toocreate tıklatın **altyapıyı hazırlama** > **çoğaltma ayarları** > **+ oluştur ve ilişkilendir**.

    ![Ağ](./media/site-recovery-vmm-to-vmm/gs-replication.png)
2. **İlke oluştur ve ilişkilendir** bölümünde bir ilke adı belirtin. Merhaba kaynak ve hedef türü olmalıdır. **Hyper-V**.
3. İçinde **Hyper-V konak sürümü**, hello konakta çalıştırdığı işletim sistemi seçin.
4. İçinde **kimlik doğrulama türü** ve **kimlik doğrulama bağlantı noktası**, hello birincil ve kurtarma Hyper-V ana bilgisayar sunucuları arasında trafik kimliğinin nasıl belirtin. Seçin **sertifika** çalışan bir Kerberos ortam yoksa. Azure Site Recovery, HTTPS kimlik doğrulaması için sertifikaları otomatik olarak yapılandırır. Toodo herhangi bir şey el ile gerek yoktur. Varsayılan olarak, bağlantı noktası 8083 ve 8084 (Sertifikalar) hello Hyper-V ana bilgisayar sunucuları üzerinde Windows Güvenlik Duvarı hello açılacak. Seçerseniz **Kerberos**, Kerberos bileti hello konak sunucularının karşılıklı kimlik doğrulaması için kullanılacak. Bu ayar yalnızca Windows Server 2012 R2'de çalışan Hyper-V konak sunucuları için geçerli olduğunu unutmayın.
5. İçinde **kopyalama sıklığı**, ne sıklıkta hello ilk çoğaltma (her 30 saniyede, 5 veya 15 dakika) sonra tooreplicate değişim verileri istediğinizi belirtin.
6. İçinde **kurtarma noktası bekletme**, saat cinsinden ne kadar süreyle hello bekletme penceresi belirtin her kurtarma noktası için olabilir. Korumalı makineler olabilir bir pencere içinde tooany noktası kurtarıldı.
7. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, ne sıklıkla (1-12 saat) içeren uygulamayla tutarlı anlık görüntüleri kurtarma noktalarını belirtin oluşturulur. Hyper-V iki çeşit anlık kullanır — bir artımlı hello tüm sanal makinenin anlık görüntüsünü sunan standart anlık görüntü ve zaman içinde nokta verilerin bir anlık görüntüsünü hello uygulama hello sanal makine içinde geçen uygulama tutarlı bir anlık görüntü. Uygulamayla tutarlı anlık görüntüleri hello anlık görüntü alınırken uygulamaların tutarlı bir durumda olan birim gölge kopyası hizmeti (VSS) tooensure kullanın. Uygulamayla tutarlı anlık görüntüleri etkinleştirirseniz kaynak sanal makinelerde çalışan uygulamaların hello performansını etkiler. Ayarladığınız hello değeri, yapılandırdığınız ilave kurtarma noktası hello sayısından daha az olduğundan emin olun.
8. İçinde **veri aktarımı sıkıştırma**, aktarılan çoğaltılmış verilerin sıkıştırılmasının gerekli olup olmadığını belirtin.
9. Seçin **çoğaltmayı Sil VM**, hello kaynak VM için korumayı devre dışı bırakırsanız çoğaltma sanal makinesi hello toospecify'nin silinmesi. Merhaba kaynak hello Site Recovery konsolundan kaldırılan VM için korumayı devre dışı bıraktığınızda bu ayarı etkinleştirirseniz, hello VMM için Site Recovery ayarları hello VMM konsolundan kaldırılır ve hello çoğaltma silinir.
10. İçinde **ilk çoğaltma yöntemini**, hello ağ üzerinden çoğaltıyorsanız toostart ilk çoğaltma hello veya zamanlamak belirtin. toosave ağ bant genişliği, tooschedule isteyebileceğiniz meşgul saatleriniz dışında. Daha sonra, **Tamam**'a tıklayın.

     ![Çoğaltma ilkesi](./media/site-recovery-vmm-to-vmm/gs-replication2.png)
11. Yeni bir ilke oluşturduğunuzda, otomatik olarak hello VMM Bulutu ile ilişkili. İçinde **Çoğaltma İlkesi**, tıklatın **Tamam**. Bu çoğaltma ilkesini ek VMM Bulutları (ve bunlara hello VM'ler) ilişkilendirebilirsiniz **çoğaltma** > ilke adı > **VMM Bulutu ile ilişkilendir**.

     ![Çoğaltma ilkesi](./media/site-recovery-vmm-to-vmm/policy-associate.png)


### <a name="configure-network-mapping"></a>Ağ eşlemesini yapılandırma

- Hakkında bilgi edinin [ağ eşlemesi](#prepare-for-network-mapping) başlamadan önce.
- Sanal makineler VMM sunucularında bağlı tooa VM ağı olduğundan emin olun.


1. İçinde **Site Recovery altyapısı** > **ağ eşlemesi** > **ağ eşlemeleri**, tıklatın **+ ağ eşlemesi**.

    ![Ağ eşlemesi](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. İçinde **ağ eşlemesi Ekle** sekmesinde hello kaynak seçin ve VMM sunucuyu hedefleyebilir. Merhaba VMM sunucular ile ilişkilendirilen hello VM ağları alınır.
3. İçinde **kaynak ağ**seçin toouse hello birincil VMM sunucusu ile ilişkili bir VM ağı hello listesinden istediğiniz hello ağ.
4. İçinde **hedef ağ**seçin hello ikincil VMM sunucusunda toouse istediğiniz hello ağ. Daha sonra, **Tamam**'a tıklayın.

    ![Ağ eşlemesi](./media/site-recovery-vmm-to-vmm/network-mapping2.png)

Ağ eşlemesi başladığında gerçekleşecekler şunlardır:

* Tüm mevcut çoğaltma toohello kaynak VM ağına karşılık gelen makineleri bağlı toohello hedef VM ağı olacaktır.
* Kaynak VM ağına bağlı toohello olan yeni sanal makinelere bağlı toohello hedef eşlenen ağ çoğaltma işleminden sonra olacaktır.
* Yeni bir ağ ile varolan bir eşlemesini değiştirirseniz, çoğaltma sanal makineleri hello yeni ayarlar kullanılarak bağlanır.
* Hello hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme sonrasında bağlı toothat hedef alt olacaktır. Eşleşen ada sahip bir hedef alt ağ ise hello sanal makineye bağlı toohello hello ağdaki ilk alt ağ olacaktır.

### <a name="configure-storage-mapping"></a>Depolama eşlemesi yapılandırın.

[Depolama eşlemesi](#prepare-for-storage-mapping) hello yeni Azure portalında desteklenmemektedir. Bununla birlikte, Powershell kullanarak etkinleştirilebilir. [Daha fazla bilgi edinin](site-recovery-vmm-to-vmm-powershell-resource-manager.md#step-7-configure-storage-mapping).

## <a name="step-5-capacity-planning"></a>5. Adım: Kapasite planlaması

Temel altyapınızı ayarladığınıza göre kapasite planlaması yapmayı ve ilave kaynaklara ihtiyacınız olup olmadığını düşünün.

- İndirme ve çalıştırma hello [Azure Site kurtarma kapasite Planlayıcısı](site-recovery-capacity-planner.md), VM dahil olmak üzere çoğaltma ortamınız hakkında toogather bilgi diskler VM ve disk başına depolama başına.
- Gerçek zamanlı çoğaltma bilgileri derledik sonra hello NetQos İlkesi toocontrol çoğaltma bant genişliği VM'ler için değiştirebilirsiniz. Daha fazla bilgi edinin [Hyper-V çoğaltma trafiğini azaltma](http://www.thomasmaurer.ch/2013/12/throttling-hyper-v-replica-traffic/), Thomas Maurer'ın blogunda. Merhaba hakkında daha fazla bilgi almak [New-NetQosPolicy cmdlet'i](https://technet.microsoft.com/library/hh967468.aspx.).

## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme

1. **2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın. Hello için çoğaltma ilk kez etkinleştirdikten sonra tıklayın **+ Çoğalt** hello kasa tooenable çoğaltma ilave makineler için.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmm-to-vmm/enable-replication1.png)
2. İçinde **kaynak**hello VMM sunucusunu seçin ve hello hangi hello tooreplicate istediğiniz Hyper-V konaklarının bulunduğu bulut. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmm-to-vmm/enable-replication2.png)
3. İçinde **hedef**, hello ikincil VMM sunucusu ve bulut doğrulayın.
4. İçinde **sanal makineleri**, tooprotect hello listeden istediğiniz hello VM'ler seçin.

    ![Sanal makine korumasını etkinleştirme](./media/site-recovery-vmm-to-vmm/enable-replication5.png)

Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** eylemde **işleri** > **Site Recovery işleri**. Merhaba sonra **korumayı Sonlandır** işi tamamlandığında, hello sanal makine yük devretme için hazır.

Şunlara dikkat edin:

- Merhaba VMM konsolunda sanal makineler için korumayı etkinleştirebilirsiniz. Tıklatın **korumayı etkinleştir** hello sanal makine Özellikleri'nde hello araç çubuğunda > **Azure Site Recovery** sekmesi.
- Çoğaltma etkinleştirdikten sonra hello VM özelliklerini görüntüleyebilir, **çoğaltılan öğeler**. Merhaba üzerinde **Essentials** panoyu hello çoğaltma ilkesi hello VM ve durumu hakkındaki bilgileri görebilirsiniz. Tıklatın **özellikleri** daha fazla ayrıntı için.

### <a name="onboard-existing-virtual-machines"></a>Yerleşik mevcut sanal makineler
Hyper-V çoğaltma ile çoğaltma mevcut sanal makineler VMM varsa, gerçekleştirebilir şekilde Azure Site Recovery çoğaltma için:

1. VM varolan hello barındıran hello Hyper-V server hello birincil bulutta bulunduğundan ve hello çoğaltma sanal makinesi barındıran bu hello Hyper-V server hello ikincil bulutta bulunduğundan emin olun.
2. Bir çoğaltma ilkesi hello birincil VMM bulutu için yapılandırılmış olduğundan emin olun.
3. Merhaba birincil sanal makine için çoğaltmayı etkinleştirin. Azure Site Recovery ve VMM hello aynı çoğaltma konak ve sanal makine algılandığında, Azure Site Recovery yeniden kullanılacak ve hello kullanarak yeniden çoğaltma ayarları belirtilen emin olun.

## <a name="test-your-deployment"></a>Dağıtımınızı test edin

tootest, dağıtımınızı çalıştırdığınız bir [yük devretme sınamasını](site-recovery-test-failover-vmm-to-vmm.md) tek bir sanal makine için veya [bir kurtarma planı oluşturma](site-recovery-create-recovery-plans.md) bir veya daha fazla sanal makine içeren.



## <a name="prepare-for-offline-initial-replication"></a>Çevrimdışı ilk çoğaltma için hazırlama

Merhaba ilk veri kopyalama için Çevrimdışı çoğaltma yapabilirsiniz. Bu şekilde hazırlayabilirsiniz:

* Hello kaynak sunucuda hangi hello verileri dışarı aktarma devre dışı gerçekleşecek bir yolu konumunu belirtin. Tam Denetim toohello VMM hizmeti hello dışarı aktarma yolundaki NTFS ve paylaşım izinlerini atayın. Merhaba hedef sunucuda içinden hello verileri içeri bir yolu konumuna oluşacaktır belirtin. Merhaba, bu alma yolu aynı izinleri atayın.
* Merhaba içe veya dışa aktarma yolu paylaşılan, hello VMM hizmet hesabı hello uzak bilgisayarda yönetici, Power User, Print Operator veya sunucu işleci grup üyeliği atamak paylaşılan hangi hello bulunur.
* Tüm farklı çalıştır hesapları tooadd konaklar kullanıyorsanız, hello içeri aktarma ve dışarı aktarma yollarındaki, okuma atayın ve VMM'de toohello farklı çalıştır hesapları yazma izinleri.
* Merhaba içeri aktarma ve dışarı aktarma paylaşımları geri döngü yapılandırma Hyper-V tarafından desteklenmediği için Hyper-V konak sunucusu olarak kullanılan herhangi bir bilgisayarda bulunmalıdır değil.
* Her Hyper-V ana bilgisayar sunucusunda tooprotect, istediğiniz sanal makineleri içeren Active Directory'de etkinleştirme ve yapılandırma Kısıtlı temsilci tootrust hello uzak bilgisayarları hangi hello içeri ve dışarı aktarma yollarının bulunduğu, aşağıdaki gibidir:
  1. Merhaba etki alanı denetleyicisinde açın **Active Directory Kullanıcıları ve Bilgisayarları**.
  2. Merhaba konsol ağacında **DomainName** > **bilgisayarlar**.
  3. Sağ hello Hyper-V ana bilgisayarı sunucusu adı > **özellikleri**.
  4. Merhaba üzerinde **temsilci** sekmesini tıklatın, **bu bilgisayara yalnızca temsilci toospecified Hizmetleri için güven**.
  5. Tıklatın **herhangi bir kimlik doğrulama protokolünü kullan**.
  6. Tıklatın **ekleme** > **kullanıcıları ve Bilgisayarları**.
  7. Merhaba verme yolu barındıran hello bilgisayarın türü hello adı > **Tamam**. Kullanılabilir hizmetler listeden Merhaba, hello CTRL tuşunu basılı tutun ve **CIFS** > **Tamam**. Merhaba hello bilgisayarın adını konakları hello alma yol yineleyin. Ek Hyper-V konak sunucuları için gerektiği kadar yineleyin.



## <a name="prepare-for-network-mapping"></a>Ağ eşlemesi için hazırlanma
Ağ eşlemesi eşlemeleri hello birincil ve ikincil VMM sunucuları için VMM VM ağlarında arasında:

* En iyi şekilde çoğaltılan VM'ler üzerinde ikincil Hyper-V konakları yük devretme sonrasında yerleştirin.
* Yük devretme sonrasında çoğaltma sanal makineleri tooappropriate VM ağları bağlayın.

Şunlara dikkat edin:
- Ağ eşlemesi iki VMM sunucusu üzerinde VM ağları arasındaki yapılandırılabilir veya iki site tarafından yönetilen, tek bir VMM sunucusunda aynı hello sunucu.
- Eşleme doğru bir şekilde yapılandırıldığından ve çoğaltma etkin olduğunda, bir VM hello birincil konumda bağlı tooa ağ olacaktır ve onun çoğaltması hello hedef konumda bağlı tooits ağ eşlenmiş.
- Bir hedef VM ağı sırasında ağ eşlemesini seçtiğinizde ağlar doğru VMM'de ayarlanan, hello kaynak VM ağı kullanan hello VMM kaynak Bulutları, hello kullanılabilir hedef VM ağları için kullanılan hello hedef Bulutları ile birlikte görüntülenir koruma.
- Merhaba hedef ağ birden çok alt ağı varsa ve bu alt ağlardan biri üzerinde hangi hello kaynak sanal makinenin bulunduğu alt ağ hello gibi aynı adı sonra hello hello çoğaltma sanal makinesi yük devretme sonrasında bağlı toothat hedef alt olacaktır. Eşleşen ada sahip bir hedef alt ağ ise hello sanal makineye bağlı toohello hello ağdaki ilk alt ağ olacaktır.


Bir örnek tooillustrate İşte bu mekanizması. New York ve Şikago iki konumda bulunduğu bir kuruluşta atalım.

| **Konum** | **VMM sunucusu** | **VM ağları** | **Eşlenen** |
| --- | --- | --- | --- |
| New York |VMM NewYork |VMNetwork1 NewYork |Eşlenen tooVMNetwork1 Chicago |
| VMNetwork2 NewYork |Eşlenmedi | | |
| Chicago |VMM Chicago |VMNetwork1 Chicago |Eşlenen tooVMNetwork1 NewYork |
| VMNetwork2 Chicago |Eşlenmedi | | |

Bu örnek ile:

* Bağlı tooVMNetwork1 NewYork olan tüm sanal makine için bir çoğaltma sanal makine oluşturulduğunda, bağlı tooVMNetwork1 Chicago olacaktır.
* Bir çoğaltma sanal makinesi VMNetwork2 NewYork veya VMNetwork2 Chicago oluşturulduğunda, bağlı tooany ağ olmaz.

İşte nasıl VMM Bulutları örnek kuruluş ve hello Mantıksal ağlar hello bulutlarıyla ilişkili ayarlanır.

### <a name="cloud-protection-settings"></a>Bulut koruma ayarlarını
| **Korumalı bulut** | **Bulut koruma** | **Mantıksal ağ (New York)** |
| --- | --- | --- |
| GoldCloud1 |GoldCloud2 | |
| SilverCloud1 |SilverCloud2 | |
| GoldCloud2 |<p>NA</p><p></p> |<p>LogicalNetwork1 NewYork</p><p>LogicalNetwork1 Chicago</p> |
| SilverCloud2 |<p>NA</p><p></p> |<p>LogicalNetwork1 NewYork</p><p>LogicalNetwork1 Chicago</p> |

### <a name="logical-and-vm-network-settings"></a>Mantıksal ve VM ağ ayarları
| **Konum** | **Mantıksal ağ** | **İlişkili bir VM ağı** |
| --- | --- | --- |
| New York |LogicalNetwork1 NewYork |VMNetwork1 NewYork |
| Chicago |LogicalNetwork1 Chicago |VMNetwork1 Chicago |
| LogicalNetwork2Chicago |VMNetwork2 Chicago | |

### <a name="target-networks"></a>Hedef ağ
Merhaba hedef VM ağ seçeneğini belirlediğinizde bu ayarları temel alarak, aşağıdaki tablonun hello kullanılabilecek hello seçimler gösterilmektedir.

| **Seç** | **Korumalı bulut** | **Bulut koruma** | **Hedef ağ yok** |
| --- | --- | --- | --- |
| VMNetwork1 Chicago |SilverCloud1 |SilverCloud2 |Kullanılabilir |
| GoldCloud1 |GoldCloud2 |Kullanılabilir | |
| VMNetwork2 Chicago |SilverCloud1 |SilverCloud2 |Kullanılamıyor |
| GoldCloud1 |GoldCloud2 |Kullanılabilir | |


### <a name="failback"></a>Yeniden çalışma
yeniden çalışma (geriye doğru çoğaltma), hello durumda neler toosee VMNetwork1 NewYork eşlenen tooVMNetwork1-Chicago, ayarlar aşağıdaki hello ile olduğunu varsayalım.

| **Sanal makine** | **Bağlı tooVM ağ** |
| --- | --- |
| VM1 |VMNetwork1 ağ |
| VM2 (VM1 çoğaltma) |VMNetwork1 Chicago |

Şimdi bu ayarlarla olası senaryolar birkaç içinde neler gözden geçirin.

| **Senaryo** | **Sonucu** |
| --- | --- |
| Yük devretme işleminden sonra VM-2 hello ağ özellikleri değişiklik. |VM 1 bağlı toohello kaynak ağ kalır. |
| VM-2 ağ özellikleri yük devretme işleminden sonra değiştirilir ve bağlantısı kesilir. |VM 1 kesilir. |
| VM-2 ağ özellikleri yük devretme işleminden sonra değiştirilir ve bağlı tooVMNetwork2 Chicago değil. |VMNetwork2 Chicago eşlenmediği olduysa, VM-1 kesilecektir. |
| Ağ eşlemesi VMNetwork1 Chicago değiştirilir. |VM 1 bağlı toohello şimdi eşlenen ağ tooVMNetwork1-Chicago olacaktır. |


## <a name="prepare-for-single-server-deployment"></a>Tek sunucu dağıtımı için hazırlama


Yalnızca tek bir VMM sunucusu varsa, sanal makineleri hello VMM bulut Hyper-V konakları olarak çok çoğaltabilirsiniz[Azure](site-recovery-vmm-to-azure.md) veya tooa ikincil VMM bulut. Bulutlar arasında çoğaltma sorunsuz olmadığından hello ilk seçenek öneririz. Bulutlar arasında tooreplicate istiyorsanız, tek tek başına VMM sunucusuyla veya esnetilen Windows kümesinde dağıtılan tek bir VMM sunucusuyla çoğaltabilirsiniz

### <a name="standalone-vmm-server"></a>Tek başına VMM sunucusu

Bu senaryoda, sanal makine hello birincil site olarak hello tek VMM sunucusu dağıtın ve Site kurtarma ve Hyper-V çoğaltma kullanarak bu VM tooa ikincil bir sitenin çoğaltma.

1. **Bir Hyper-V VM'de VMM ayarlama**. Merhaba SQL Server örneği üzerinde hello VMM tarafından kullanılan birlikte bulundurma önerdiğimiz aynı VM. Yalnızca bir VM oluşturulan toobe bulunduğundan bu zamandan tasarruf sağlar. VMM kurtarabilmek toouse uzak SQL Server örneğini istediğiniz ve bir kesinti oluşursa, bu örnek toorecover gerekir.
2. **Merhaba VMM sunucusunda yapılandırılmış en az iki bulut bulunduğundan emin olun**. Bir bulut tooreplicate istediğiniz ve diğer bulut hello VM'ler hello ikincil konumu olarak kullanılacak hello içerir. Merhaba istediğiniz tooprotect ile uyumlu olması gerekir hello VM'ler içeren bulut [Önkoşullar](#prerequisites).
3. Site Recovery, bu makalede açıklanan şekilde ayarlayın. Oluşturma ve hello VMM sunucusu bir kasaya kaydetmek bir çoğaltma ilkesini ayarlayın ve çoğaltmayı etkinleştirin. Merhaba kaynak ve hedef VMM adları olması hello aynı. Merhaba ağ üzerinden ilk çoğaltmanın gerçekleşir belirtin.
4. Ağ eşlemesi ayarlamanız hello VM ağı hello ikincil bulut için hello birincil bulut toohello VM ağı için eşleyin.
5. Merhaba Hyper-V Yöneticisi konsolunda, Hyper-V çoğaltma hello VMM VM içeren hello Hyper-V ana bilgisayarda ve hello VM çoğaltmayı etkinleştirebilirsiniz. Site Recovery, Hyper-V çoğaltma ayarlarını Site Recovery tarafından geçersiz kılınmış olmayan tooensure tarafından korunan hello VMM sanal makine tooclouds eklemeyin emin olun.
6. Kullandığınız yük devretme için kurtarma planları oluşturursanız, kaynak için aynı VMM sunucusu hello ve hedefleyebilirsiniz.
7. Tam bir kesinti yük devri ve aşağıdaki şekilde kurtarın:

   1. Planlanmamış bir yük devretme hello Hyper-V Yöneticisi konsolunda hello ikincil site, toofail hello birincil VMM VM toohello ikincil sitesi üzerinde çalıştırın.
   2. VMM VM çalışır durumda o hello doğrulayın ve çalıştırılması, hello kasadaki planlanmamış yük devretme toofail hello VM'ler üzerinde birincil toosecondary bulutlardan çalıştırın ve. Merhaba yük devretme kaydetmek ve gerekirse alternatif bir kurtarma noktası seçin.
   3. Tüm kaynaklar Hello planlanmamış yük devretme işlemi tamamlandıktan sonra hello birincil siteden yeniden erişilebilir.
   4. Merhaba birincil site yeniden hello Hyper-V Manager konsolunda hello ikincil sitedeki kullanılabilir olduğunda, çoğaltmayı tersine çevirme hello VMM VM için etkinleştirin. Bu, ikincil tooprimary hello VM için çoğaltma başlatır.
   5. Planlanmış bir yük devretme hello Hyper-V Yöneticisi konsolunda hello ikincil site, toofail hello VMM VM toohello birincil site üzerinden çalıştırın. Merhaba yük devretme uygulayın. Böylece Hello VMM VM yeniden birincil toosecondary çoğaltma çoğaltmayı tersine çevirme etkinleştirin.
   6. Merhaba kurtarma Hizmetleri kasasına hello iş yükü sanal makinelerinize, ikincil tooprimary çoğaltma toostart ters çoğaltmayı etkinleştirin.
   7. Bir planlı yük devretme toofail geri hello iş yükü VM'ler toohello birincil site çalıştırmak hello kurtarma Hizmetleri kasasına. Merhaba yük devretme toocomplete tamamlama. Daha sonra çoğaltmayı tersine çevirme toostart çoğaltma hello yükünden VM'ler birincil toosecondary etkinleştirin.

### <a name="stretched-vmm-cluster"></a>Esnetilen VMM kümesi

Tek başına VMM sunucusu tooa ikincil site çoğaltılan VM olarak dağıtmak yerine, VMM yüksek oranda kullanılabilir bir VM Windows Yük devretme kümesinde olarak dağıtarak yapabilirsiniz. Bu, iş yükü esnekliği ve donanım hatalarına karşı koruma sağlar. Site Recovery hello VMM VM ile toodeploy coğrafi olarak ayrı siteler arasında uzatma bir kümede dağıtılması gerekir. toodo bu:

1. Windows Yük devretme kümesindeki bir sanal makinede VMM yükleme ve başlangıç seçeneği toorun hello server kurulumu sırasında yüksek oranda kullanılabilir olarak seçin.
2. Merhaba ikincil sitedeki hello veritabanının çoğaltmasını olmasını sağlamak VMM tarafından kullanılan hello SQL Server örneği SQL Server AlwaysOn Kullanılabilirlik grupları ile çoğaltılması.
3. Bu makale toocreate bir kasa Hello yönergeleri izleyin, hello sunucuyu kaydetmek ve koruma ayarlama. Her VMM sunucusunda hello küme kurtarma Hizmetleri kasası hello tooregister gerekir. toodo Bu, etkin bir düğümde hello sağlayıcı yükleyin ve hello VMM sunucusunu kaydedin. Ardından hello sağlayıcısı diğer düğümlere yükleyin.
4. Kesinti oluştuğunda hello VMM sunucusu karşılık gelen SQL Server veritabanını devredilir ve hello ikincil siteden erişilebilir.



## <a name="prepare-for-storage-mapping"></a>Depolama eşlemeye hazırlama


Depolama alanı eşleme tarafından eşleme depolama sınıflandırmaları üzerinde bir kaynak kümesi ve VMM sunucuları toodo hello aşağıdaki hedef:

  * **Çoğaltma sanal makineler için hedef depolama tanımlamak**— bir kaynak VM sabit disk, belirttiğiniz toohello depolama çoğaltır (SMB paylaşımı veya Küme Paylaşılan birimleri (CSV)) hello hedef konumda.
  * **Çoğaltma sanal makine yerleştirme**— depolama eşlemesi kullanılan toooptimally yerine çoğaltma sanal makinelerini Hyper-V ana bilgisayar sunucuları üzerinde değil. Çoğaltma sanal makineleri hello eşlenen depolama sınıflandırması erişebilen Konaklara yerleştirilir.
  * **Depolama eşleme**— depolama eşlemesini yapılandırmazsanız, sanal makineler hello çoğaltma sanal makine ile ilişkili hello Hyper-V konak sunucusunda belirtilen çoğaltılmış toohello varsayılan depolama konumunu olacaktır.

Şunlara dikkat edin:
- Tek bir sunucuda iki VMM Bulutları arasında eşleme ayarlayabilirsiniz.
- Depolama sınıflandırmaları kullanılabilir toohello konak gruplarının kaynak ve hedef bulutlarında yer alan olması gerekir.
- Sınıflandırmaları gerekmez toohave hello aynı türde depolama. Örneğin, csv içeren SMB paylaşımları tooa Hedef Sınıflandırma içeren bir kaynak sınıflandırma eşleyebilirsiniz.

### <a name="example"></a>Örnek
Depolama eşlemesi sırasında hello kaynak ve hedef VMM sunucusu seçtiğinizde sınıflandırmaları doğru VMM'de yapılandırılmışsa, hello kaynak ve hedef sınıflandırmaları görüntülenir. Depolama dosya paylaşımlarını ve New York ve Şikago iki konumda olan bir kuruluş için sınıfların bir örneği burada verilmiştir.

| **Konum** | **VMM sunucusu** | **Dosya Paylaşımı (kaynak)** | **Sınıflandırma (kaynak)** | **Eşlenen** | **Dosya Paylaşımı (hedef)** |
| --- | --- | --- | --- | --- | --- |
| New York |VMM_Source |SourceShare1 |ALTIN |GOLD_TARGET |TargetShare1 |
| SourceShare2 |GÜMÜŞ |SILVER_TARGET |TargetShare2 | | |
| SourceShare3 |BRONZ |BRONZE_TARGET |TargetShare3 | | |
| Chicago |VMM_Target | |GOLD_TARGET |Eşlenmedi | |
|  |SILVER_TARGET |Eşlenmedi | | | |
|  |BRONZE_TARGET |Eşlenmedi | | | |

Bu örnek ile:

* Bir çoğaltma sanal makinesi, ALTIN depolama (SourceShare1) herhangi bir sanal makine için oluşturulduğunda, çoğaltılmış tooa GOLD_TARGET depolama (TargetShare1) olacaktır.
* GÜMÜŞ depolama (SourceShare2) herhangi bir sanal makine için bir çoğaltma sanal makinesi oluşturduğunuzda, onu çoğaltılmış tooa SILVER_TARGET (TargetShare2) depolama ve benzeri.

### <a name="multiple-storage-locations"></a>Birden çok depolama konumları
Merhaba Hedef Sınıflandırma toomultiple SMB paylaşımları veya csv atanmışsa hello sanal makine korunurken hello en iyi depolama konumu otomatik olarak seçilir. Uygun hedef depolama ile kullanılabilir durumdaysa hello Sınıflandırma, hello varsayılan belirtilen hello Hyper-V ana bilgisayarda belirtilen depolama konumudur kullanılan tooplace hello çoğaltma sanal sabit diskler.

Aşağıdaki tablonun hello nasıl depolama sınıflandırması ve Küme Paylaşılan Birimleri örneğimizde kurulduğunu gösterir.

| **Konum** | **Sınıflandırma** | **İlişkili depolama** |
| --- | --- | --- |
| New York |ALTIN |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> |
| GÜMÜŞ |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p> | |
| Chicago |GOLD_TARGET |<p>C:\ClusterStorage\TargetVolume1</p><p>\\FileServer\TargetShare1</p> |
| SILVER_TARGET |<p>C:\ClusterStorage\TargetVolume2</p><p>\\FileServer\TargetShare2</p> | |

Bu örnek ortamında (VM1 - VM5) sanal makineler için korumayı etkinleştirdiğinizde, bu tablo hello davranışı özetler.

| **Sanal makine** | **Kaynak depolama** | **Kaynak sınıflandırma** | **Eşlenen Hedef depolama** |
| --- | --- | --- | --- |
| VM1 |C:\ClusterStorage\SourceVolume1 |ALTIN |<p>C:\ClusterStorage\SourceVolume1</p><p>\\\FileServer\SourceShare1</p><p>Her iki GOLD_TARGET</p> |
| VM2 |\\FileServer\SourceShare1 |ALTIN |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> <p>Her iki GOLD_TARGET</p> |
| VM3 |C:\ClusterStorage\SourceVolume2 |GÜMÜŞ |<p>C:\ClusterStorage\SourceVolume2</p><p>\FileServer\SourceShare2</p> |
| VM4 |\FileServer\SourceShare2 |GÜMÜŞ |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p><p>Her iki SILVER_TARGET</p> |
| VM5 |C:\ClusterStorage\SourceVolume3 |Yok |Merhaba varsayılan depolama konumunu hello Hyper-V konağının kullanılmak üzere hiçbir eşleme |



### <a name="data-privacy-overview"></a>Veri gizliliği genel bakış

Bu tabloda, bu senaryoda, verilerin depolanma şeklini özetlenmektedir:

- - -
| Eylem | **Ayrıntılar** | **Toplanan veriler** | **Kullanma** | **Gerekli** |
| --- | --- | --- | --- | --- |
| **Kayıt** | Kurtarma Hizmetleri kasasına VMM sunucusunu kaydedin. Daha sonra bir sunucu toounregister istiyorsanız, Azure portal hello hello sunucu bilgilerini silerek bunu yapabilirsiniz. | VMM sunucusunu kaydettikten sonra Site Recovery, işlemler, toplar ve hello VMM sunucusu ve Site Recovery tarafından algılanan hello VMM Bulutları hello adlarını hakkındaki meta verileri aktarır. | Merhaba veriler kullanılan tooidentify ve hello uygun VMM sunucusuyla iletişim kurar ve uygun VMM Bulutları için ayarları yapılandırın. | Bu özellik gereklidir. Bu bilgi tooSite kurtarma toosend istemiyorsanız hello Site Recovery hizmeti kullanmamalısınız. |
| **Çoğaltmayı etkinleştirme** | Hello Azure Site Recovery sağlayıcısı hello VMM sunucusunda yüklü ve hello conduit hello Site Recovery hizmeti ile iletişim için. Merhaba sağlayıcısı hello VMM işlemde barındırılan bir dinamik bağlantı kitaplığı (DLL) olur. Hello sağlayıcı yüklendikten sonra hello VMM Yönetici konsolunda hello "Veri merkezi Kurtarma" özelliği etkin. Yeni ve mevcut sanal makineleri bir VM için bu özelliği tooenable korumayı etkinleştirebilirsiniz. |Bu özellik kümesiyle hello sağlayıcısı hello adını ve Kimliğini hello VM tooSite kurtarma gönderir.  Çoğaltma, Windows Server 2012 veya Windows Server 2012 R2 Hyper-V çoğaltma tarafından etkinleştirilir. Merhaba sanal makine verilerini (genellikle bir farklı "Kurtarma" veri merkezinde bulunan) bir Hyper-V ana bilgisayar tooanother gelen çoğaltılan. |Site Recovery hello Azure portal hello meta veri toopopulate hello VM bilgileri kullanır. | Bu özellik hello hizmeti önemli bir parçasıdır ve devre dışı bırakılamaz. Bu bilgiler toosend istemiyorsanız, VM'ler için Site Recovery korumasını etkinleştirmeyin. Merhaba sağlayıcısı tooSite kurtarma tarafından gönderilen tüm veriler HTTPS üzerinden gönderilen olduğunu unutmayın. |
| **Kurtarma planı** | Kurtarma planları hello kurtarma veri merkezi için bir düzenleme planı oluşturmanıza yardımcı olur. İçinde sanal makineler veya sanal makine grubu hello kurtarma sitesinde başlatılmalıdır hello düzenini tanımlayabilirsiniz. Çalıştırmak istediğiniz otomatik betikler toobe ya da her VM için kurtarma hello zamanında alınan tüm el ile işlem toobe de belirtebilirsiniz. Yük devretme düzeyinde hello kurtarma planı Eşgüdümlü kurtarma için genellikle tetiklenir. | Site Recovery toplar, işler ve sanal makine meta veri ve meta veri Otomasyon betikleri ve el ile işlem notlar gibi hello kurtarma planı için meta veri aktarır. |Merhaba meta verileri hello Azure portal kullanılan toobuild hello kurtarma planında değil. |Bu özellik hello hizmeti önemli bir parçasıdır ve devre dışı bırakılamaz. Bu bilgi tooSite kurtarma toosend istemiyorsanız, Kurtarma planları oluşturmayın. |
| **Ağ eşlemesi** | MAPS hello birincil veri merkezi toohello kurtarma veri merkezi bilgilerinden ağ. VM'ler hello kurtarma sitesinde kurtarılan, ağ bağlantısı oluşturmada ağ eşlemesi yardımcı olur. |Site Recovery toplar, işler ve hello mantıksal ağların (birincil ve datacenter) her site için hello meta veri aktarır. |Merhaba meta verileri kullanılan toopopulate ağ ayarlarını, böylelikle hello ağ bilgilerini eşleyebilirsiniz. | Bu özellik hello hizmeti önemli bir parçasıdır ve devre dışı bırakılamaz. Bu bilgi tooSite kurtarma toosend istemiyorsanız, ağ eşlemesi kullanmayın. |
| **Yük devretme (planlanmış ve planlanmamış/test)** | Yük devretme VM'ler VMM tarafından yönetilen bir veri merkezi tooanother başarısız olur. Merhaba yük devretme işlemi el ile hello Azure portal tetiklenir. |hello VMM sunucusunda sağlayıcı Hello hello yük devretme olayı Site Recovery tarafından bildirilir ve yük devretme işlemi VMM arabirimleri aracılığıyla hello Hyper-V ana bilgisayarda çalışır. Bir VM gerçek yük devretme bir Hyper-V ana bilgisayar tooanother olduğu ve Windows Server 2012 veya Windows Server 2012 R2 Hyper-V çoğaltma tarafından işlenir. Aft Site Recovery hello Azure portal toopopulate hello hello yük devretme eylem bilgileri durumunu gönderilen hello bilgileri kullanır. | Bu özellik hello hizmeti önemli bir parçasıdır ve devre dışı bırakılamaz. Bu bilgi tooSite kurtarma toosend istemiyorsanız, yük devretme kullanmayın. |

## <a name="next-steps"></a>Sonraki adımlar

Merhaba dağıtımı test ettikten sonra diğer türleri hakkında daha fazla bilgi [yük devretme](site-recovery-failover.md)
