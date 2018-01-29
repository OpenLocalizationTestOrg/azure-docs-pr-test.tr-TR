---
title: "Azure Site Recovery ile şirket içi siteleriniz arasında Hyper-V VM'ler için olağanüstü durum kurtarma ayarlama | Microsoft Docs"
description: "Olağanüstü durum kurtarma Hyper-V VM'ler için Azure Site Recovery ile şirket içi siteleriniz arasında öğrenin."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 65eda71c-3ca3-41bc-b02d-00fecc1557d7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/17/2017
ms.author: raynew
ms.openlocfilehash: 1647e9d69da3e991bec4e00b3a1083a254fa9550
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/01/2017
---
# <a name="set-up-disaster-recovery-for-hyper-v-vms-to-your-secondary-on-premises-site"></a>Olağanüstü durum kurtarma için Hyper-V Vm'lerini ikincil şirket içi sitenize ayarlayın.

[Azure Site Recovery](site-recovery-overview.md) hizmeti yönetme ve çoğaltma, yük devretme ve yeniden çalışma şirket içi makineler ve Azure sanal makineleri (VM'ler) yönetme olağanüstü durum kurtarma stratejiniz katkıda bulunur.

System Center Virtual Machine Manager (VMM) bulutlarında yönetilen şirket içi Hyper-V Vm'lerini için Bu öğretici, ikincil bir siteye olağanüstü durum kurtarma ayarlama gösterilmektedir. Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Şirket içi VMM sunucuları ve Hyper-V ana bilgisayarları hazırlama
> * Site kurtarma için bir kurtarma Hizmetleri kasası oluşturma 
> * Kaynağı ayarlama ve çoğaltma ortamları hedefleyebilirsiniz. 
> * (Hyper-V System Center VMM tarafından yönetiliyorsa) ağ eşlemesi ayarlamak
> * Çoğaltma ilkesi oluşturma
> * Bir sanal makine için çoğaltmayı etkinleştirme

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticiyi tamamlamak için:

- Gözden geçirme [senaryo mimarisi ve bileşenleri](concepts-hyper-v-to-secondary-architecture.md).
- Gözden geçirme [destek gereksinimleri](site-recovery-support-matrix-to-sec-site.md) tüm bileşenler için.
- VMM sunucuları ve Hyper-V konakları ile uyumlu olduğundan emin olun [destek gereksinimleri](site-recovery-support-matrix-to-sec-site.md).
- Çoğaltmak istediğiniz sanal makineleri uyması onay [makine desteği çoğaltılan](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions).
- VMM sunucuları ağ eşlemesi için hazırlayın.

### <a name="prepare-for-network-mapping"></a>Ağ eşlemesi için hazırlanma

[Ağ eşlemesi](site-recovery-network-mapping.md) arasındaki eşlemeleri şirket içi VMM VM ağları kaynak ve hedef bulutlarındaki. Eşleme şunları yapar:

- Sanal makineleri yük devretme sonrasında uygun hedef VM ağına bağlanır. 
- En iyi şekilde çoğaltılan VM'ler hedef Hyper-V ana bilgisayar sunucuları üzerinde yerleştirir. 
- Ağ eşlemesini yapılandırmazsanız, çoğaltma sanal makineleri yük devretme sonrasında bir VM ağa bağlanmayacaktır.

VMM aşağıdaki gibi hazırlayın:

1. Olduğundan emin olun [VMM mantıksal ağlarına](https://docs.microsoft.com/system-center/vmm/network-logical) kaynak ve hedef VMM sunucularında.
    - Mantıksal ağ kaynak sunucu üzerindeki Hyper-V konaklarının bulunduğu kaynak Bulutu ile ilişkili olmalıdır.
    - Hedef sunucudaki mantıksal ağ hedef Bulutu ile ilişkili olmalıdır.
1. Olduğundan emin olun [VM ağları](https://docs.microsoft.com/system-center/vmm/network-virtual) kaynak ve hedef VMM sunucularında. VM ağları her konumdaki mantıksal ağ bağlantılı olması gerekir.
2. Vm'leri kaynak Hyper-V konaklarının kaynak VM ağına bağlayın. 


## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a>Koruma hedefi seçin

Neleri çoğaltmak istediğinizi ve bunları nereye çoğaltacağınızı seçin.

1. Tıklatın **Site Recovery** > **1. adım: altyapıyı hazırlama** > **koruma hedefi**.
2. Seçin **kurtarma sitesine**seçip **Evet, Hyper-V ile**.
3. Seçin **Evet** Hyper-V ana bilgisayarları yönetmek için VMM kullandığınızı belirtmek için.
4. Seçin **Evet** bir ikincil VMM sunucunuz varsa. Tek bir VMM sunucusundaki Bulutlar arasında çoğaltma dağıtıyorsanız tıklatın **Hayır**. Daha sonra, **Tamam**'a tıklayın.


## <a name="set-up-the-source-environment"></a>Kaynak ortamı ayarlama

Azure Site kurtarma sağlayıcısı VMM sunucularında yükleme ve bulmak ve sunucuları kasaya kaydetmek.

1. **Altyapıyı Hazırlama** > **Kaynak** seçeneklerine tıklayın.
2. **Kaynağı ayarla** kısmında, bir VMM sunucusu eklemek için **+ VMM**'ye tıklayın.
3. İçinde **Sunucu Ekle**, denetleyin **System Center VMM sunucusunun** görünür **sunucu türü**.
4. Azure Site Recovery Sağlayıcısı yükleme dosyasını indirin.
5. Kayıt anahtarını indirin. Sağlayıcı yüklediğinizde bu gerekir. Anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.

    ![Kaynağı ayarlama](./media/tutorial-vmm-to-vmm/source-settings.png)

6. Sağlayıcı her VMM sunucusuna yükleyin. Açıkça şey Hyper-V ana bilgisayarlarına yüklemeniz gerekmez.

### <a name="install-the-azure-site-recovery-provider"></a>Azure Site kurtarma Sağlayıcısı'nı yüklemek

1. Sağlayıcı kurulum dosyasını her VMM sunucusunda çalıştırın. VMM bir kümede dağıtılıyorsa, ilk olarak aşağıdaki gibi yükleyin:
    -  Etkin bir düğümde bir sağlayıcı yükleyin ve VMM sunucusunu kasaya kaydetmek için yüklemeyi sonlandırın.
    - Ardından, sağlayıcı diğer düğümlere yükleyin. Küme düğümlerini tüm sağlayıcının aynı sürümüne çalıştırmanız gerekir.
2. Kurulum, birkaç ön koşul denetimlerini çalıştırır ve VMM hizmetini durdurmak için izin ister. Kurulum bittiğinde VMM hizmeti otomatik olarak yeniden başlatılır. Bir VMM kümesinde yüklerseniz, küme rolünü durdurmanız istenir.
3. İçinde **Microsoft Update**, sağlayıcı güncelleştirmeleri Microsoft Update ilkenize uygun yüklü olduğunu belirtmek için de seçebilirsiniz.
4. İçinde **yükleme**kabul edin veya varsayılan yükleme konumunu değiştirmek ve tıklatın **yükleme**.
5. Yükleme tamamlandıktan sonra tıklayın **kaydetmek** sunucuyu kasaya kaydetmek için.

    ![Yükleme konumu](./media/tutorial-vmm-to-vmm/provider-register.png)
6. **Kasa adı** alanında, sunucunun kayıtlı olduğu kasanın adını doğrulayın. **İleri**’ye tıklayın.
7. İçinde **Proxy bağlantı**, Azure'a VMM sunucusunda çalışan sağlayıcı nasıl bağlandığını belirtin.
   - Sağlayıcı İnternete doğrudan ya da bir proxy üzerinden bağlanmalısınız belirtebilirsiniz. Proxy ayarları gerektiği gibi belirtin.
   - Bir proxy kullanıyorsanız, VMM RunAs hesabı (DRAProxyAccount) otomatik olarak, belirtilen proxy kimlik bilgileri kullanılarak oluşturulur. Bu hesabın kimlik doğrulamasını başarıyla gerçekleştirebilmesi için ara sunucuyu yapılandırın. RunAs hesabı ayarları VMM konsolundan değiştirilebilir > **ayarları** > **güvenlik** > **farklı çalıştır hesapları**.
   - Değişiklikleri güncelleştirme için VMM hizmetini yeniden başlatın.
8. İçinde **kayıt anahtarı**, indirdiğiniz ve VMM sunucusuna kopyaladığınız anahtar seçin.
9. Şifreleme ayarı bu senaryoyla ilgili değildir. 
10. **Sunucu adı** alanında, kasadaki VMM sunucusunu tanımlamak için bir kolay ad belirtin. Bir kümede VMM kümesi rolü adını belirtin.
11. İçinde **Eşitle bulut meta verileri**VMM sunucusundaki tüm Bulutlar için meta verilerini eşitlemek istediğinizi seçin. Bu eylemin her sunucuda yalnızca bir kez gerçekleştirilmesi gerekir. Tüm Bulutları eşitlemek istemiyorsanız bu ayarı işaretsiz bırakın. Her Bulutu VMM konsolundaki bulut özellikleri ayrı ayrı eşitleyebilirsiniz.
12. İşlemi tamamlamak için **İleri**'ye tıklayın. Kayıttan sonra Site Recovery VMM sunucusundan meta verilerini alır. Sunucu görüntülenen **sunucuları** > **VMM sunucuları** kasadaki.
13. Kasada sunucu göründükten sonra **kaynak** > **kaynağı** VMM sunucusunu seçin ve Hyper-V konağı bulunduğu Bulutu seçin. Daha sonra, **Tamam**'a tıklayın.


## <a name="set-up-the-target-environment"></a>Hedef ortamı ayarlama

Hedef VMM sunucusunu ve Bulutu seçin:

1. Tıklatın **altyapıyı hazırlama** > **hedef**ve hedef VMM sunucusunu seçin.
2. Site Recovery ile eşitlenmiş VMM Bulutları görüntülenir. Hedef bulut seçin.

   ![Hedef](./media/tutorial-vmm-to-vmm/target-vmm.png)


## <a name="set-up-a-replication-policy"></a>Bir çoğaltma ilkesini ayarlayın

Başlamadan önce ilkeyi kullanarak tüm konakları aynı işletim sistemi olduğundan emin olun. Ana bilgisayar Windows Server'ın farklı sürümleri çalıştırıyorsanız, birden fazla çoğaltma ilkesi gerekir.

1. Yeni bir çoğaltma ilkesi oluşturmak için **Altyapıyı hazırlama** > **Çoğaltma Ayarları** > **+Oluştur ve ilişkilendir** seçeneklerine tıklayın.
2. **İlke oluştur ve ilişkilendir** bölümünde bir ilke adı belirtin. Kaynak ve hedef türü olmalıdır. **Hyper-V**.
3. İçinde **Hyper-V konak sürümü**, ana bilgisayarda çalıştırdığı işletim sistemi seçin.
4. İçinde **kimlik doğrulama türü** ve **kimlik doğrulama bağlantı noktası**, birincil ve kurtarma Hyper-V ana bilgisayar sunucuları arasında trafik kimliğinin nasıl belirtin.
    - Seçin **sertifika** çalışan bir Kerberos ortam yoksa. Azure Site Recovery, HTTPS kimlik doğrulaması için sertifikaları otomatik olarak yapılandırır. El ile bir şey yapmanız gerekmez.
    - Varsayılan olarak, Hyper-V ana bilgisayar sunucuları üzerinde Windows Güvenlik Duvarı'nda bağlantı noktası 8083 ve 8084 (Sertifikalar) yeniden açılır.
    - Seçerseniz **Kerberos**, bir Kerberos anahtarı konak sunucularının karşılıklı kimlik doğrulaması için kullanılacak. Kerberos yalnızca Windows Server 2012 R2 veya üstü çalıştıran Hyper-V konak sunucuları için geçerlidir.
1. **Kopyalama sıklığı** kısmında, ilk çoğaltmadan sonra değişim verilerini ne sıklıkta çoğaltacağınızı belirleyin (30 saniyede, 5 veya 15 dakikada bir).
2. İçinde **kurtarma noktası bekletme**, \how belirtin (saat olarak) uzun her kurtarma noktası için bekletme penceresi olacaktır. Çoğaltılan makineler bir pencere içinde herhangi bir noktaya kurtarılabilir.
3. İçinde **uygulamayla tutarlı anlık görüntü sıklığı**, ne sıklıkla (1-12 saat) içeren uygulamayla tutarlı anlık görüntüleri kurtarma noktalarını belirtin oluşturulur. Hyper-V iki çeşit anlık kullanır:
    - **Standart anlık görüntü**: tüm sanal makinenin artımlı bir anlık görüntü sağlar.
    - **Uygulamayla tutarlı anlık görüntü**: VM içindeki uygulama verilerinin bir zaman içinde nokta anlık görüntüsünü alır. Birim Gölge Kopyası Hizmeti (VSS) anlık görüntü alınırken uygulamaların tutarlı bir durumda olmasını sağlar. Uygulamayla tutarlı anlık görüntüleri etkinleştirilmesi, kaynak VM'ler uygulama performansını etkiler. Yapılandırdığınız ilave kurtarma noktası sayısından küçük bir değere ayarlayın.
4. İçinde **veri aktarımı sıkıştırma**, aktarılan çoğaltma verilerin sıkıştırılmasının gerekli olup olmadığını belirtin.
5. Seçin **çoğaltmayı Sil VM**VM kaynak için korumayı devre dışı bırakırsanız, çoğaltma sanal makinesinin silinmesi gerektiğini belirtmek için. Site Recovery konsolundan kaldırılan VM kaynak için korumayı devre dışı bıraktığınızda bu ayarı etkinleştirirseniz, VMM için Site Recovery ayarları VMM konsolundan kaldırılır ve çoğaltma silinir.
6. İçinde **ilk çoğaltma yöntemini**, ağ üzerinden çoğaltıyorsanız ilk çoğaltmayı başlatmadan veya zamanlamak belirtin. Ağ bant genişliğini korumak amacıyla meşgul saatleriniz dışında zamanlamak isteyebilirsiniz. Daha sonra, **Tamam**'a tıklayın.

     ![Çoğaltma ilkesi](./media/tutorial-vmm-to-vmm/replication-policy.png)
     
7. Yeni ilke, otomatik olarak VMM bulutuyla ilişkilendirilir. İçinde **Çoğaltma İlkesi**, tıklatın **Tamam**. 


## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme

1. Tıklatın **uygulama çoğaltma** > **kaynak**. 
2. İçinde **kaynak**, VMM sunucusu ve çoğaltmak istediğiniz Hyper-V konakları olduğu bulunduğu Bulutu seçin. Daha sonra, **Tamam**'a tıklayın.
3. İçinde **hedef**, ikincil VMM sunucusu ve bulut doğrulayın.
4. İçinde **sanal makineleri**, listeden korumak istediğiniz sanal makineleri seçin.


İlerleme durumunu izleyebilirsiniz **korumayı etkinleştir** eylemde **işleri** > **Site Recovery işleri**. Sonra **korumayı Sonlandır** işi tamamlandığında, ilk çoğaltma tamamlandıktan ve VM yük devretme için hazırdır.

## <a name="next-steps"></a>Sonraki adımlar

[Olağanüstü durum kurtarma tatbikatı çalıştırma](tutorial-dr-drill-secondary.md)
