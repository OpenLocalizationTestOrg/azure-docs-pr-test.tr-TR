---
title: aaaReplicate Hyper-V sanal makineleri tooAzure | Microsoft Docs
description: "Açıklar nasıl tooorchestrate çoğaltma, yük devretme ve kurtarma işlemlerini şirket içi Hyper-V sanal makineleri tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: hyper-v-site-walkthrough-overview
ms.openlocfilehash: 6fba41e43823fc57511d51ea2e09691159693982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure-using-azure-site-recovery-with-hello-azure-portal"></a>Hello Azure portal ile Azure Site Recovery kullanarak Hyper-V sanal makineleri (VMM olmadan) tooAzure Çoğalt

> [!div class="op_single_selector"]
> * [Azure portal](site-recovery-hyper-v-site-to-azure.md)
> * [Azure klasik](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

Bu makalede nasıl tooreplicate Hyper-V sanal makineleri tooAzure, şirket içi kullanarak [Azure Site Recovery](site-recovery-overview.md) hello Azure Portalı'nda. Bu dağıtım Hyper-V VM System Center Virtual Machine Manager (VMM) tarafından yönetilmiyor.

Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Toomigrate makineler tooAzure (olmadan yeniden çalışma) istiyorsanız, daha fazla bilgi edinin [bu makalede](site-recovery-migrate-to-azure.md).



## <a name="deployment-steps"></a>Dağıtım adımları

Merhaba makale toocomplete dağıtım adımları izleyin:

1. [Daha fazla bilgi edinin](site-recovery-components.md#hyper-v-to-azure) bu dağıtım için hello mimarisi hakkında. Ayrıca Site Recovery'de Hyper-V çoğaltmanın nasıl çalıştığı [hakkında bilgi edinin](site-recovery-hyper-v-azure-architecture.md).
2. Önkoşulları ve sınırlamaları doğrulayın.
3. Azure ağ ve depolama hesaplarını kurun.
4. Hyper-V ana bilgisayarını hazırlayın.
5. Kurtarma Hizmetleri kasası oluşturun. Merhaba kasası yapılandırma ayarlarını içeren, çoğaltma ve yönetir.
6. Kaynak ayarlarını belirtin. Merhaba Hyper-V konakları içeren Hyper-V sitesi oluşturun ve hello site hello kasaya kaydedin. Hello Azure Site Recovery sağlayıcısı ve hello Microsoft Kurtarma Hizmetleri aracısını hello Hyper-V ana bilgisayarlarına yükleyin.
7. Hedef ve çoğaltma ayarlarını yapın.
8. Merhaba VM'ler çoğaltmayı etkinleştirin.
9. Her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırın.



## <a name="prerequisites"></a>Ön koşullar


**Gereksinim** | **Ayrıntılar** |
--- | --- |
**Azure** | [Azure gereksinimleri](site-recovery-prereq.md#azure-requirements) hakkında bilgi edinin.
**Şirket içi sunucular** | [Daha fazla bilgi edinin](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) hello şirket içi Hyper-V konakları için gereksinimleri hakkında.
**Şirket içi Hyper-V VM'leri** | Tooreplicate çalışıyor istediğiniz sanal makineleri bir [işletim sistemi desteklenen](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)ve uygun olması [Azure önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Azure URL'leri** | Hyper-V konakları toothese URL'leri erişim:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin emin olun.<br/></br> Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (443 numaralı) bağlantı noktası.<br/></br> IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.



## <a name="prepare-for-deployment"></a>Dağıtım için hazırlanma

tooprepare dağıtımı yapmanız için:

1. [Bir Azure ağı ayarlama](#set-up-an-azure-network) yük devretme sonrasında oluşturulduğunda, hangi Azure VM'ler bulunur.
2. Çoğaltılan veriler için [Azure depolama hesabı ayarlama](#set-up-an-azure-storage-account).
3. [Merhaba Hyper-V ana bilgisayarını hazırlayın](#prepare-the-hyper-v-hosts) bunlar hello erişebilir tooensure URL'leri gerekli.

### <a name="set-up-an-azure-network"></a>Azure ağı ayarlama

Azure ağı ayarlama ayarlayın. Böylece yük devretme sonra bağlı tooa ağ oluşturulan hello Azure Vm'lerinin gerekir.

* Merhaba ağ hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası.
* Merhaba kaynak modeline bağlı olarak toouse Azure vm'lerinde istediğiniz, hello Azure ağı ayarlama [Resource Manager moduna](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), veya [Klasik modda](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* Başlamadan önce bir ağ ayarlamanızı öneririz. Bunu yapmazsanız, toodo gerekir, Site Recovery dağıtımı sırasında.
- Site Recovery tarafından kullanılan depolama hesapları olamaz [taşınmış](../azure-resource-manager/resource-group-move-resources.md) hello aynı, ya da farklı Aboneliklerde içinde.


### <a name="set-up-an-azure-storage-account"></a>Azure depolama hesabı ayarlama

- Standart/premium toohold veri tooAzure çoğaltılan Azure depolama hesabı gerekir. [Premium depolama](../storage/storage-premium-storage.md) sanal makineler için bir tutarlı bir şekilde yüksek g/ç performans ve düşük gecikme süresi toohost g/ç yoğun iş yükleri gerek genellikle kullanılır.
- Toouse istiyorsanız premium hesap toostore veri çoğaltılan, yakalama devam eden tooon içi verileri değiştiren bir standart depolama hesabı toostore çoğaltma günlükleri de gerekir.
- Merhaba kaynak modeline bağlı olarak toouse Azure vm'lerinde istediğiniz, hesap ayarlama [Resource Manager moduna](../storage/storage-create-storage-account.md), veya [Klasik modda](../storage/storage-create-storage-account-classic-portal.md).
- Başlamadan önce bir depolama hesabı ayarlamanız önerilir. Bunu yapmazsanız toodo gerekir, Site Recovery dağıtımı sırasında. Merhaba hesapları hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası.
- Depolama hesapları kullanılan Site Recovery tarafından hello içindeki kaynak grupları arasında aynı taşıyamazsınız aboneliği ya da farklı Aboneliklerdeki.


### <a name="prepare-hello-hyper-v-hosts"></a>Merhaba Hyper-V ana bilgisayarları hazırlama

* Merhaba Hyper-V konakları hello karşıladığından emin olun [Önkoşullar](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).
- Merhaba konakları gerekli hello URL'leri erişebildiğinden emin olun.


## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. **Yeni** > **İzleme + Yönetim** > **Backup and Site Recovery (OMS)** öğesine tıklayın.  

    ![Yeni kasa](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. İçinde **adı**, bir kolay ad tooidentify hello kasası belirtin. Birden fazla aboneliğiniz varsa bunlardan birini seçin.

4. [Yeni bir kaynak grubu oluşturma](../azure-resource-manager/resource-group-template-deploy-portal.md) veya varolan bir tanesini seçin ve bir Azure bölgesi belirtin. Makineler çoğaltılmış toothis bölge olacaktır. desteklenen toocheck bölgeleri, coğrafi kullanılabilirlik kısmına bakın [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).

5. Tooquickly erişim hello hello Pano kasadan istiyorsanız, **PIN toodashboard**ve ardından **oluşturma**.

    ![Yeni kasa](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

Merhaba yeni kasa görünür hello **Pano** > **tüm kaynakları** listesinde ve üzerinde hello ana **kurtarma Hizmetleri kasaları** dikey.



## <a name="select-hello-protection-goal"></a>Merhaba koruma hedefi seçin

İstediğinizi seçin, tooreplicate ve tooreplicate için istediğiniz.

1. Merhaba, **kurtarma Hizmetleri kasaları**seçin hello kasası.
2. **Başlarken** bölümünde, **Site Recovery** > **Altyapıyı Hazırlama** > **Koruma hedefi** seçeneklerine tıklayın.

    ![Hedefleri seçme](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. İçinde **koruma hedefi**seçin **tooAzure**seçip **Evet, Hyper-V ile**. Seçin **Hayır** VMM kullanmadığınız tooconfirm. Daha sonra, **Tamam**'a tıklayın.

    ![Hedefleri seçme](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Merhaba kaynak ortamını ayarlama

Merhaba Hyper-V sitesini kurmak, hello Azure Site Recovery sağlayıcısı ve hello Azure kurtarma Hizmetleri aracısını Hyper-V ana bilgisayarlarına yükleyin ve hello site hello kasaya kaydetmek.

1. İçinde **altyapıyı hazırlama**, tıklatın **kaynak**. Hyper-V konakları veya kümeleri için kapsayıcı olarak yeni bir Hyper-V sitesi tooadd tıklatın **+ Hyper-V sitesi**.

    ![Kaynağı ayarlama](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. İçinde **oluşturma Hyper-V sitesi**, başlangıç sitesi için bir ad belirtin. Daha sonra, **Tamam**'a tıklayın. Şimdi, oluşturduğunuz ve tıklatın hello siteyi seçin **+ Hyper-V Server** tooadd server toohello sitesi.

    ![Kaynağı ayarlama](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. İçinde **Sunucu Ekle** > **sunucu türü**, denetleyin **Hyper-V server** görüntülenir.

    - İstediğiniz tooadd hello ile uyumlu hello Hyper-V sunucu emin olun [Önkoşullar](#on-premises-prerequisites), ve olduğu mümkün tooaccess hello belirtilen URL'leri.
    - Hello Azure Site Recovery sağlayıcısı yükleme dosyasını indirin. Bu dosya tooinstall hello sağlayıcısı çalıştırın ve her Hyper-V ana kurtarma Hizmetleri aracısını hello.

    ![Kaynağı ayarlama](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Merhaba sağlayıcı ve aracı yükleme

1. Her ana bilgisayarda Hello sağlayıcı kurulum dosyasını çalıştırın toohello Hyper-V sitesi eklendi. Hyper-V kümesi üzerinde yüklüyorsanız, her küme düğümünde Kurulumu çalıştırın. Düğümleri arasında geçirmek olsa bile yükleme ve her Hyper-V küme düğümü kaydetme VM'ler korunduğunu sağlar.
2. **Microsoft Update** kısmından güncelleştirmeleri seçebilirsiniz. Böylece, Sağlayıcı güncelleştirmeleri Microsoft Update ilkenize uygun şekilde yüklenir.
3. İçinde **yükleme**, kabul etmek veya hello varsayılan sağlayıcı yükleme konumunu değiştirmek ve tıklatın **yükleme**.
4. İçinde **kasa ayarlarını**, tıklatın **Gözat** indirdiğiniz tooselect hello kasa anahtarı dosyasını. Hello Azure Site Recovery abonelik hello kasa adı belirtin ve hello Hyper-V site toowhich hello Hyper-V sunucusuna ait.

    ![Sunucu kaydı](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. İçinde **Proxy ayarlarını**, Hyper-V konakları üzerinde çalışan sağlayıcı üzerinden Site Recovery tooAzure bağlanır hello hello Internet nasıl belirtin.

    * Merhaba sağlayıcısı tooconnect doğrudan select istiyorsanız **tooAzure Site Recovery Ara sunucu olmadan doğrudan bağlan**.
    * Var olan ara sunucunuz kimlik doğrulaması gerektiren veya hello sağlayıcı bağlantısı için özel bir ara sunucu toouse istiyorsanız, seçin **tooAzure Site kurtarma proxy sunucusu kullanarak bağlanmak**.
    * Bir proxy sunucu kullanıyorsanız:
        - Başlangıç adresi, bağlantı noktası ve kimlik bilgilerini belirtin
        - Hello açıklanan emin hello URL'leri olun [Önkoşullar](#prerequisites) hello proxy üzerinden izin verilir.

    ![internet](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. Yükleme tamamlandıktan sonra tıklatın **kaydetmek** hello kasadaki tooregister hello sunucu.

    ![Yükleme konumu](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. Kayıt tamamlandıktan sonra hello Hyper-V sunucusundan meta veriler, Azure Site Recovery tarafından alınır ve hello sunucu görüntülenir **Site Recovery altyapısı** > **Hyper-V konakları**.


## <a name="set-up-hello-target-environment"></a>Merhaba hedef ortamını ayarlama

Çoğaltma için Hello Azure depolama hesabı belirtin ve hello Azure ağ toowhich Azure Vm'lerinin yük devretme sonrasında bağlanır.

1. Tıklatın **altyapıyı hazırlama** > **hedef**.
2. Merhaba abonelik ve yük devretme sonrasında toocreate hello Azure VM'ler istediğiniz hello kaynak grubunu seçin. Merhaba dağıtımı seçin model toouse (Klasik veya resource management) azure'da hello VM'ler istiyor.

3. Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.

    - Bir depolama hesabınız yoksa tıklatın **+ depolama** toocreate bir Resource Manager tabanlı hesap satır içi. Hakkında bilgi edinin [depolama gereksinimleri](site-recovery-prereq.md#azure-requirements).
    - Bir Azure ağı yoksa tıklatın **+ ağ** toocreate bir Resource Manager tabanlı ağ satır içi.

    ![Depolama](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a>Çoğaltma ayarlarını yapılandırma

1. Yeni bir çoğaltma ilkesi toocreate tıklatın **altyapıyı hazırlama** > **çoğaltma ayarları** > **+ oluştur ve ilişkilendir**.

    ![Ağ](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. **İlke oluştur ve ilişkilendir** bölümünde bir ilke adı belirtin.
3. İçinde **kopyalama sıklığı**, ne sıklıkta hello ilk çoğaltma (her 30 saniyede, 5 veya 15 dakika) sonra tooreplicate değişim verileri istediğinizi belirtin.

    > [!NOTE]
    > 30 ikinci sıklığı toopremium depolama çoğaltırken desteklenmiyor. Merhaba sınırlaması, premium depolama birimi tarafından desteklenen hello anlık görüntü sayısı blob (100) başına tarafından belirlenir. [Daha fazla bilgi edinin](../storage/storage-premium-storage.md#snapshots-and-copy-blob).

4. İçinde **kurtarma noktası bekletme**, saat cinsinden süreyi belirtin hello bekletme penceresi olduğu için her kurtarma noktası. Sanal makineleri olabilir bir pencere içinde tooany noktası kurtarıldı.
5. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, ne sıklıkla (1-12 saat) içeren uygulamayla tutarlı anlık görüntüleri kurtarma noktalarını belirtin oluşturulur.

    - Hyper-V iki çeşit anlık kullanır — bir artımlı hello tüm sanal makinenin anlık görüntüsünü sunan standart anlık görüntü ve zaman içinde nokta verilerin bir anlık görüntüsünü hello uygulama hello sanal makine içinde geçen uygulama tutarlı bir anlık görüntü.
    - Uygulamayla tutarlı anlık görüntüleri hello anlık görüntü alınırken uygulamaların tutarlı bir durumda olan birim gölge kopyası hizmeti (VSS) tooensure kullanın.
    - Uygulamayla tutarlı anlık görüntüleri etkinleştirirseniz kaynak sanal makinelerde çalışan uygulamaların hello performansını etkiler. Ayarladığınız hello değeri, yapılandırdığınız ilave kurtarma noktası hello sayısından daha az olduğundan emin olun.

6. İçinde **ilk çoğaltma başlangıç zamanı**, ne zaman toostart hello ilk çoğaltma belirtin. Merhaba çoğaltmanın internet bant genişliğiniz tooschedule isteyebilirsiniz şekilde meşgul saatleriniz dışında. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltma ilkesi](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

Yeni bir ilke oluşturduğunuzda, otomatik olarak hello Hyper-V sitesi ile ilişkili. Birden fazla çoğaltma ilkesi ile bir Hyper-V sitesi (ve hello VM'ler da) ilişkilendirebilirsiniz **çoğaltma** > ilke adı > **ilişkilendirmek Hyper-V sitesi**.

## <a name="capacity-planning"></a>Kapasite planlaması

Temel altyapınızı sahip olduğunuza göre kapasite planlaması hakkında düşünün ve ek kaynaklar ihtiyacınız olup olmadığı şekil.

Site Recovery, kapasite Planlayıcısı toohelp sağlar işlem, ağ ve depolama için hello doğru kaynakları ayıramadı. Merhaba Planlayıcısı ortalama bir VM'ler, diskler ve depolama birimi sayısına göre tahmin oluşturmak için Hızlı modda ya da ayrıntılı modda özelleştirilmiş numaralarıyla hello iş yükü düzeyinde çalıştırabilirsiniz. Başlamadan önce şunları yapmanız gerekir:

* VM'ler, VM başına disk ve disk başına depolama dahil olmak üzere çoğaltma ortamınız hakkında bilgi toplayın.
* Çoğaltılan verilerin Hello günlük değişim (dalgalanma) hızına yönelik tahminde bulunun. Merhaba kullanabilirsiniz [Hyper-V çoğaltma için kapasite Planlayıcı](https://www.microsoft.com/download/details.aspx?id=39057) bunu toohelp.

1. Tıklatın **karşıdan** toodownload hello aracı ve ardından çalıştırın. [Merhaba makale okuma](site-recovery-capacity-planner.md) hello araçla birlikte.
2. İşiniz bittiğinde seçin **Evet** içinde **hello kapasite Planlayıcısı çalıştırmak**?

   ![Kapasite planlaması](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

[Ağ bant genişliğini denetleme](#network-bandwidth-considerations) hakkında daha fazla bilgi edinin



## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme

Başlamadan önce Azure kullanıcı hesabınızın gerekli hello sahip olduğundan emin olun [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) yeni bir sanal makine tooAzure tooenable çoğaltması.

VM'ler için çoğaltma gibi etkinleştirin:          

1. Tıklatın **uygulama çoğaltma** > **kaynak**. Çoğaltma hello için ilk kez ayarladıktan sonra tıklayabilirsiniz **+ Çoğalt** ilave makineler için tooenable çoğaltma.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. İçinde **kaynak**seçin hello Hyper-V sitesi. Daha sonra, **Tamam**'a tıklayın.
3. İçinde **hedef**hello kasa abonelik seçin ve hello yük devretme sonrasında Azure (Klasik veya resource management) toouse istediğiniz yük devretme modeli.
4. Toouse istediğiniz hello depolama hesabını seçin. Toouse istediğiniz bir hesabınız yoksa, şunları yapabilirsiniz [oluşturmak](#set-up-an-azure-storage-account). Daha sonra, **Tamam**'a tıklayın.
5. Yük devretme oluşturulduğunda select hello Azure ağ ve alt ağ toowhich Azure VM'ler bağlanır.

    - etkinleştirmeniz tooapply hello ağ ayarlarını tooall makineleri çoğaltma için seçin **seçili makineler için Şimdi Yapılandır**.
    - Seçin **daha sonra yapılandırma** tooselect hello makine başına Azure ağı.
    - Toouse istediğiniz ağ yoksa, şunları yapabilirsiniz [oluşturmak](#set-up-an-azure-network). Bir alt ağ (varsa) seçin. Daha sonra, **Tamam**'a tıklayın.

   ![Çoğaltmayı etkinleştirme](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. İçinde **sanal makineleri** > **sanal makine Seç**, tıklatın ve tooreplicate istediğiniz her bir makine seçin. Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. İçinde **özellikleri** > **özelliklerini yapılandırma**, seçili hello VM'ler için hello işletim sistemini seçin ve işletim sistemi diski hello.
8. Bu hello Azure VM adı (hedef) uyumlu ile doğrulayın [Azure sanal makine gereksinimlerini](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Varsayılan olarak tüm hello diskleri hello VM, çoğaltma için seçilir, ancak diskleri tooexclude temizleyebilirsiniz bunları.
    - Tooexclude diskleri tooreduce çoğaltma bant genişliği isteyebilirsiniz. Örneğin, geçici verileri tooreplicate disklerle istemeyebilirsiniz veya (pagefile.sys veya Microsoft SQL Server tempdb gibi) her zaman bir makine ya da uygulamaları yeniledi verileri yeniden başlatır. Merhaba disk unselecting hello disk tarafından çoğaltma dışında bırakabilirsiniz.
    - Yalnızca temel diskler dışarıda bırakılabilir. İşletim sistemi diskleri dışarıda bırakılamaz.
    - Dinamik diskleri dışarıda tutmamanızı öneririz. Site Recovery, konuk VM içerisindeki bir sanal sabit diskin temel mi yoksa dinamik mi olduğunu anlayamaz. Tüm bağımlı dinamik birimi disklerinin dışlanan olmayan varsa, hello korumalı dinamik disk hello VM yöneltilir ve bu disk üzerindeki hello verileri erişilebilir olmayacaktır başarısız disk olarak gösterir.
        - Çoğaltmayı etkinleştirdikten sonra çoğaltma için disk ekleme veya kaldırma gerçekleştiremezsiniz. Tooadd, veya bir disk dışlamak istiyorsanız Merhaba VM toodisable koruma gerektiren ve yeniden etkinleştirin.
        - Azure'da el ile oluşturduğunuz diskler yeniden çalışır duruma getirilmez. Örneğin, üzerinde üç disk başarısız ve iki doğrudan Azure VM'deki oluşturursanız, üzerinden başarısız olan yalnızca hello üç disk geri Azure tooHyper-V ile başarısız. Yeniden çalışma veya Hyper-V tooAzure ters çoğaltmayı el ile oluşturulan diskleri ekleyemezsiniz.
        - Bir uygulama toooperate için gerekli olan bir disk bıraksanız sonra Yük devretme tooAzure azure'da uygulama bu hello çoğaltılan şekilde el ile çalıştırabilirsiniz toocreate gerekir. Alternatif olarak, bir kurtarma planı toocreate hello disk hello makinenin yük devretme sırasında Azure Otomasyon tümleştirin.

10. Tıklatın **Tamam** toosave değişiklikler. Daha sonra ek özellikleri ayarlayabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, istediğiniz tooapply hello VM'ler korumalı hello çoğaltma ilkesi seçin. Daha sonra, **Tamam**'a tıklayın. Merhaba Çoğaltma İlkesi'nde değiştirebilirsiniz **çoğaltma ilkeleri** > ilke adı > **ayarlarını Düzenle**. Uyguladığınız değişiklikler, zaten çoğaltılmış olan makinelere ve yeni makinelere uygulanır.


   ![Çoğaltmayı etkinleştirme](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **işleri** > **Site Recovery işleri**. Merhaba sonra **korumayı Sonlandır** iş çalıştırmaları hello makine yük devretme için hazır.

### <a name="view-and-manage-vm-properties"></a>VM özelliklerini görüntüleme ve yönetme

Merhaba hello kaynak makinenin özelliklerini doğrulamanızı öneririz.

1. İçinde **korunan öğeler**, tıklatın **çoğaltılan öğeler**ve select hello makine.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. İçinde **özellikleri**, çoğaltma görebilirsiniz ve Yük Devretme bilgilerini hello VM.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. İçinde **işlem ve ağ** > **işlem özellikleri**, hello Azure VM adını ve hedef boyutu belirtebilirsiniz. Gerekirse hello adı toocomply Azure gereksinimleri ile değiştirin. Ayrıca, görüntüleyin ve hello hedef ağ, alt ağ ve toohello Azure VM atanacak IP adresi hakkında bilgi değiştirin. Merhaba aşağıdakileri göz önünde bulundurun:

   * Merhaba hedef IP adresini ayarlayabilirsiniz. Bir adresi sağlamazsanız, yükü devredilen makine üzerinde hello DHCP kullanır. Yük devretmede kullanılamayan bir adres ayarlarsanız hello yük devretme başarısız olur. Merhaba hello test yük devretme ağı testinde Hello adresi varsa, yük devretme sınaması için aynı hedef IP adresi kullanılabilir.
   * ağ bağdaştırıcısı Hello sayısını hello hedef sanal makine için aşağıdaki gibi belirtin hello boyuta göre dikte edilir:

     * Merhaba hello kaynak makinedeki ağ bağdaştırıcısı sayısı küçük veya buna eşit ise toohello bağdaştırıcı sayısı hello hedef makine boyutu için izin verilen sonra hello hedef olacaktır hello aynı sayıda bağdaştırıcıya hello kaynağı olarak.
     * Merhaba hello kaynak sanal makinenin bağdaştırıcı sayısı hello hedef boyutu sonra hello maksimum hedef boyutu kullanılır için izin verilen hello sayıyı aşarsa.
     * Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hello hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa, hello hedef makinenin iki bağdaştırıcısı gerekir. Merhaba kaynak makinenin iki bağdaştırıcısı varsa, ancak hello hedef boyut yalnızca bir destekler hello hedef makine yalnızca bir bağdaştırıcısı olur.     
     * Merhaba VM birden çok ağ bağdaştırıcısı varsa bunların tümü toohello bağlanır aynı ağ.
     * Merhaba sanal makine birden çok ağ bağdaştırıcısı hello varsa, önce bir hello listede gösterilen hello haline gelir *varsayılan* hello Azure sanal makine ağ bağdaştırıcısı.

     ![Çoğaltmayı etkinleştirme](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. İçinde **diskleri**, hello işletim sistemi görebilir ve veri disklerde hello çoğaltılır VM.

#### <a name="managed-disks"></a>Yönetilen diskler

İçinde **işlem ve ağ** > **işlem özellikleri**, tooattach yönetilen diskleri tooyour geçiş tooAzure makinede isterseniz "Yönetilen diskleri kullanımını" ayarı çok "Evet" Merhaba VM ayarlayabilirsiniz. Yönetilen diskleri hello VM disklerle ilişkilendirilmiş hello depolama hesaplarını yöneterek Azure Iaas VM'ler için disk yönetimi basitleştirir. [Yönetilen diskler hakkında daha fazla bilgi edinin](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Oluşturulan ve ekli toohello sanal makinede yalnızca bir yük devretme tooAzure yönetilen disklerdir. Korumayı etkinleştirmek için şirket içi makineler verilerden tooreplicate toostorage hesapları devam eder.
   Yönetilen diskler yalnızca hello Resource manager dağıtım modeli kullanılarak dağıtılan sanal makineleri için oluşturulabilir.

  > [!NOTE]
  > Yeniden çalışma Azure tooon içi Hyper-V Ortamı'ndan yönetilen disklerle makineler için şu anda desteklenmiyor. Bu makine tooAzure toomigrate düşünüyorsanız "Yönetilen diskleri kullanımını" çok "Evet" ayarlayın.

   - "Yönetilen diskleri kullanımını" çok "Evet" ayarladığınızda, yalnızca hello kaynak grubundaki kullanılabilirlik kümeleri "Kullanım diskleri yönetilen" olarak ayarlanmış çok "Evet" seçime uygun olacaktır. Bu durum, yönetilen bir diske sahip sanal makineler yalnızca parçası "Yönetilen kullanım diskleri" özelliği ayarlanmış kullanılabilirlik kümeleri çok "Evet" olabilir çünkü. Kullanılabilirlik kümeleri, yük devretme hedefi toouse yönetilen disklerde göre "Yönetilen kullanım diskleri" özellik kümesi ile oluşturduğunuzdan emin olun. Benzer şekilde, "Yönetilen diskleri kullanımını" çok "Hayır" ayarladığınızda, hello kaynak grubunda "Yönetilen diskleri kullanımını" özelliği çok "Hayır" olarak ayarlanmış yalnızca kullanılabilirlik kümeleri seçime uygun olacaktır. [Yönetilen diskler ve kullanılabilirlik kümeleri hakkında daha fazla bilgi edinin](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Merhaba depolama hesabı çoğaltma için kullanılan herhangi bir noktada zamanında depolama hizmeti şifrelemesi ile şifrelenmişse, yük devretme sırasında yönetilen diskleri oluşturma başarısız olur. Seçebilir ya da "Yönetilen diskleri kullanımını" çok "Hayır" ayarlayın ve yük devretme yeniden deneyin veya hello sanal makine için korumayı devre dışı bırakmak ve herhangi bir noktada zamandaki etkin depolama hizmeti şifrelemesi sahip değilse, tooa depolama hesabı koruyun.
  > [Depolama Hizmeti Şifrelemesi ve yönetilen diskler hakkında daha fazla bilgi edinin](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Merhaba dağıtımı test etme

tootest hello dağıtımı, bir yük devretme sınaması için tek bir sanal makine ya da bir veya daha fazla sanal makine içeren bir kurtarma planı çalıştırabilirsiniz.

### <a name="before-you-start"></a>Başlamadan önce

 - Tooconnect tooAzure VM'ler istiyorsanız, yük devretme işleminden sonra RDP kullanarak bilgi hakkında [tooconnect hazırlama](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - Active Directory ve DNS toocopy test ortamınızda gereksinim duyduğunuz toofully sınayın. [Daha fazla bilgi edinin](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma

1. tek bir makineye üzerinden toofail içinde **çoğaltılan öğeler**, hello VM tıklayın > **+ yük devretme testi** simgesi.
2. bir kurtarma üzerinden toofail planlama **kurtarma planları**, sağ hello planı > **yük devretme testi**. bir kurtarma planı toocreate [bu yönergeleri izleyin](site-recovery-create-recovery-plans.md).
3. İçinde **yük devretme testi**seçin hello Azure ağ toowhich Azure Vm'lerinin yük devretme gerçekleştikten sonra bağlanır.
4. Tıklatın **Tamam** toobegin hello yük devretme. Merhaba VM tooopen üzerinde özelliklerini tıklayarak ya da hello ilerleme durumunu izleyebilirsiniz **yük devretme testi** kasa adı işinde > **işleri** > **Site Recovery işleri**.
5. Hello yük devretme işlemi tamamlandıktan sonra ayrıca olması toosee hello çoğaltma Azure makine görünür hello Azure portalı > **sanal makineleri**. Bu hello VM toohello uygun ağ ve çalıştığını bağlı hello uygun boyutta olduğundan emin olmanız gerekir.
6. Yük devretme sonrasında bağlantıları için hazır durumunda mümkün tooconnect toohello Azure VM olması gerekir.
7. İşiniz bittiğinde tıklayın **temizleme yük devretme testi** hello kurtarma planı üzerinde. İçinde **notları** kaydedin ve hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek. Bu yük devretme testi sırasında oluşturulan hello sanal makineleri siler.

Daha fazla ayrıntı için hello okuma [Test yük devretme tooAzure](site-recovery-test-failover-to-azure.md) makalesi.



## <a name="monitor-hello-deployment"></a>İzleyici hello dağıtım

Merhaba yapılandırma ayarları, durum ve Site kurtarma dağıtımınız için sistem durumu izleme:

1. Tıklatın hello kasa adı tooaccess hello üzerinde **Essentials** Pano. Bu Panoda Site Recovery işleri, çoğaltma durumunu, Kurtarma planlarını, sunucu sistem durumu ve olayları izleyebilirsiniz.  

    ![Temel Bileşenler](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. Merhaba, **sistem durumu** döşeme sorunu yaşıyor ve Site Recovery tarafından son 24 saat hello başlatılan olayları hello site sunucularını izleyebilirsiniz. Essentials tooshow hello kutucukları ve diğer Site Recovery ve Backup kasalarını hello durumu da dahil olmak üzere en yararlı tooyou olan düzenleri özelleştirebilirsiniz.
3. Yönetmek ve izlemek hello çoğaltmasında **çoğaltılan öğeler**, **kurtarma planları**, ve **Site Recovery işleri** döşeme. Daha ayrıntılı bilgi için iş ayrıntılarına geçebilir **işleri** > **Site Recovery işleri**.

## <a name="command-line-provider-and-agent-installation"></a>Komut satırı sağlayıcı ve aracı yükleme

Hello Azure Site Recovery sağlayıcısı ve aracı ayrıca hello aşağıdaki komut satırı kullanılarak yüklenebilir. Bu yöntem, bir sunucu çekirdek Windows Server 2012 R2 için kullanılan tooinstall hello sağlayıcısında olabilir.

1. Merhaba sağlayıcısı yükleme dosyasını ve kayıt anahtarı tooa klasörü indirin. Örneğin, C:\ASR.
2. Yükseltilmiş bir komut isteminden aşağıdaki komutları tooextract hello sağlayıcı yükleyicisini çalıştırın:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Bu komut tooinstall hello bileşenleri çalıştırın:

            C:\ASR> setupdr.exe /i
4. Ardından bu komutları tooregister hello sunucu hello kasasına çalıştırın:

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file>

<br/>
Konumlar:

* **/ Credentials**: hangi hello kayıt anahtarı dosyasının bulunduğu hello konumu belirten zorunlu parametre  
* **/ FriendlyName**: hello Azure Site Recovery portalında görünen hello Hyper-V ana bilgisayar sunucusunun adını hello için zorunlu parametre.
* **/ proxyaddress**: hello proxy sunucusunun hello adresini belirten isteğe bağlı parametre.
* **/ proxyport** : hello proxy sunucusunun hello bağlantı noktasını belirten isteğe bağlı parametre.
* **/ proxyusername**: (proxy kimlik doğrulaması gerektiriyorsa) hello Ara sunucu kullanıcı adını belirten isteğe bağlı parametre.
* **/ proxypassword**: belirten isteğe bağlı parametre (Ara sunucu kimlik doğrulaması gerekirse) hello proxy sunucusu ile kimlik doğrulaması için parola hello.


## <a name="network-bandwidth-considerations"></a>Ağ bandı genişliği ile ilgili dikkat edilmesi gerekenler
Merhaba kullanabilirsiniz [Hyper-V kapasite planlayıcısı aracı](site-recovery-capacity-planner.md) toocalculate hello bant genişliği (ilk çoğaltma ve ardından değişim) için çoğaltma gerekir. toocontrol hello tutar çoğaltma için bant genişliği kullanımı, birkaç seçeneğiniz vardır:

* **Bant genişliğini kısıtlama**: tooAzure çoğaltır Hyper-V trafiği belirli bir Hyper-V ana bilgisayar üzerinden gider. Merhaba ana bilgisayar sunucusunda bant genişliğini kısıtlayabilirsiniz.
* **Bant genişliği ince ayar**: birkaç kayıt defteri anahtarlarını kullanarak çoğaltma için kullanılan hello bant genişliği etkileyebilir.

### <a name="throttle-bandwidth"></a>Bant genişliğini kısıtlama
1. Merhaba Hyper-V konak sunucusunda Hello Microsoft Azure Backup MMC eklentisini açın. Varsayılan olarak Microsoft Azure yedekleme için bir kısayol hello masaüstünde veya C:\Program Files\Microsoft Azure Recovery Services agent\bin\wabadmin yolunda kullanılabilir durumdadır.
2. Merhaba ek bileşeninde tıklatın **özelliklerini değiştirme**.
3. Merhaba üzerinde **azaltma** sekmesini seçin **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir**, iş için hello sınırını ayarlama ve saat İş dışı. Geçerli aralıklar saniye başına 512 Kbps too102 Mbps arasındadır.

    ![Bant genişliğini kısıtlama](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

Merhaba de kullanabilirsiniz [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) tooset cmdlet azaltma. Bu ayara ilişkin örneği aşağıda bulabilirsiniz:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting - NoThrottle** hiçbir azaltmanın gerekli olmadığını gösterir.

### <a name="influence-network-bandwidth"></a>Ağ bant genişliği üzerinde etki oluşturma
1. Merhaba kayıt defterinde çok gidin**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * bir çoğaltma diskte tooinfluence hello bant genişliği trafiği değiştirebilir hello değeri hello **UploadThreadsPerVM**, veya yoksa hello anahtar oluşturun.
   * Azure, yeniden çalışma trafiği için tooinfluence hello bant genişliği değiştirme hello değeri **DownloadThreadsPerVM**.
2. Merhaba varsayılan değer 4'tür. "Fazla sağlanan" bir ağda, bu kayıt defteri anahtarları hello varsayılan değerlerinin değiştirilmesi. Merhaba en fazla 32'dir. Trafik toooptimize hello değeri izleyin.

## <a name="next-steps"></a>Sonraki adımlar

Merhaba ihtiyaç duydukça ilk çoğaltma tamamlandıktan ve hello dağıtımı test ettikten sonra Yük devretmeler çalıştırabilirsiniz. [Daha fazla bilgi edinin](site-recovery-failover.md) yerine farklı türleri hakkında ve nasıl toorun bunları.
