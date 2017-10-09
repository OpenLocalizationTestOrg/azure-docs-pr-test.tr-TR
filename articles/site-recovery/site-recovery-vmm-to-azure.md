---
title: aaaReplicate VMM Hyper-V VM Bulutu tooAzure | Microsoft Docs
description: "Çoğaltma, yük devretme ve kurtarma işlemlerini System Center VMM Bulutları tooAzure yönetilen Hyper-V Vm'lerini düzenlemek"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: 84182fe4b63862ac7643208a22f236a7515a25a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>VMM Bulutları tooAzure hello Azure portalında Site Recovery kullanarak Hyper-V sanal makineleri Çoğalt
> [!div class="op_single_selector"]
> * [Azure portal](site-recovery-vmm-to-azure.md)
> * [Azure klasik](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell klasik](site-recovery-deploy-with-powershell.md)


Bu makalede nasıl tooreplicate System Center VMM Bulutları tooAzure hello kullanarak yönetilen Hyper-V sanal makineleri şirket içi [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Toomigrate makineler tooAzure (olmadan yeniden çalışma) istiyorsanız, daha fazla bilgi edinin [bu makalede](site-recovery-migrate-to-azure.md).


## <a name="deployment-steps"></a>Dağıtım adımları

Merhaba makale toocomplete dağıtım adımları izleyin:


1. [Daha fazla bilgi edinin](site-recovery-components.md) bu dağıtım için hello mimarisi hakkında. Ayrıca Site Recovery'de Hyper-V çoğaltmanın nasıl çalıştığı [hakkında bilgi edinin](site-recovery-hyper-v-azure-architecture.md).
2. Önkoşulları ve sınırlamaları doğrulayın.
3. Azure ağ ve depolama hesaplarını kurun.
4. Merhaba şirket içi VMM sunucusu ve Hyper-V konakları hazırlayın.
5. Kurtarma Hizmetleri kasası oluşturun. Merhaba kasası yapılandırma ayarlarını içeren, çoğaltma ve yönetir.
6. Kaynak ayarlarını belirtin. Merhaba VMM sunucusunu hello kasaya kaydedin. Hello VMM sunucusu yükleme hello Microsoft Kurtarma Hizmetleri aracısını Hyper-V konaklarında'Hello Azure Site Recovery sağlayıcısı yükleyin.
7. Hedef ve çoğaltma ayarlarını yapın.
8. Merhaba VM'ler çoğaltmayı etkinleştirin.
9. Her şeyin beklendiği gibi çalıştığından emin bir test yük devretme toomake çalıştırın.



## <a name="prerequisites"></a>Ön koşullar


**Destek gereksinimi** | **Ayrıntılar**
--- | ---
**Azure** | [Azure gereksinimleri](site-recovery-prereq.md#azure-requirements) hakkında bilgi edinin.
**Şirket içi sunucular** | [Daha fazla bilgi edinin](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-in-vmm-clouds-to-azure) hello şirket içi VMM sunucusu ve Hyper-V konakları için gereksinimleri hakkında.
**Şirket içi Hyper-V VM'leri** | Tooreplicate çalışıyor istediğiniz sanal makineleri bir [işletim sistemi desteklenen](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)ve uygun olması [Azure önkoşulları](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Azure URL'leri** | Merhaba VMM sunucusu toothese URL'leri erişimi gerektirir:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> IP adresi tabanlı güvenlik duvarı kuralları varsa, iletişim tooAzure izin emin olun.<br/></br> Merhaba izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/confirmation.aspx?id=41653)ve hello HTTPS (443 numaralı) bağlantı noktası.<br/></br> IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.


## <a name="prepare-for-deployment"></a>Dağıtım için hazırlanma
tooprepare dağıtımı için şunları yapmanız gerekir:

1. Yük devretmeden sonra Azure VM’lerinin içinde bulunacağı [bir Azure ağı ayarlayın](#set-up-an-azure-network).
2. Çoğaltılan veriler için [Azure depolama hesabı ayarlama](#set-up-an-azure-storage-account).
3. [Merhaba VMM sunucusunu hazırlama](#prepare-the-vmm-server) Site Recovery dağıtımı için.
4. Ağ eşlemesi için hazırlanın. Site Recovery dağıtımı sırasında ağ eşlemesini yapılandırabilmeniz için ağları ayarlayın.

### <a name="set-up-an-azure-network"></a>Azure ağı ayarlama
Bir Azure ağı toowhich yük devretme bağlanacak sonra oluşturulan Azure VM'ler gerekir.

* Merhaba ağ hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası.
* Merhaba kaynak modeline bağlı olarak toouse Azure vm'lerinde istediğiniz, hello Azure ağı ayarlama [Resource Manager moduna](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) veya [Klasik modda](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* Başlamadan önce bir ağ ayarlamanızı öneririz. Bunu yapmazsanız, toodo gerekir, Site Recovery dağıtımı sırasında.
Site Recovery tarafından kullanılan azure ağları olamaz [taşınmış](../azure-resource-manager/resource-group-move-resources.md) hello aynı, ya da farklı Aboneliklerde içinde.

### <a name="set-up-an-azure-storage-account"></a>Azure depolama hesabı ayarlama
* Standart/premium toohold veri tooAzure çoğaltılan Azure depolama hesabı gerekir. [Premium depolama](../storage/common/storage-premium-storage.md) sanal makineler için bir tutarlı bir şekilde yüksek g/ç performans ve düşük gecikme süresi toohost g/ç yoğun iş yükleri gerek kullanılır. Toouse istiyorsanız premium hesap toostore veri çoğaltılan, yakalama devam eden tooon içi verileri değiştiren bir standart depolama hesabı toostore çoğaltma günlükleri de gerekir. Merhaba hesabı hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası.
* Merhaba kaynak modeline bağlı olarak toouse Azure vm'lerinde istediğiniz, hesap ayarlama [Resource Manager moduna](../storage/common/storage-create-storage-account.md) veya [Klasik modda](../storage/common/storage-create-storage-account.md).
* Başlamadan önce bir hesap ayarlamanızı öneririz. Bunu yapmazsanız, toodo gerekir, Site Recovery dağıtımı sırasında.
- Site Recovery tarafından kullanılan depolama hesapları olamayacağını unutmayın [taşınmış](../azure-resource-manager/resource-group-move-resources.md) hello aynı, ya da farklı Aboneliklerde içinde.

### <a name="prepare-hello-vmm-server"></a>Merhaba VMM sunucusunu hazırlama
* Merhaba VMM sunucusunun hello ile uyumlu olduğundan emin olun [Önkoşullar](#prerequisites).
* Site Recovery dağıtımı sırasında VMM sunucusundaki tüm Bulutlar hello Azure portalında kullanılabilir olması gerektiğini belirtebilirsiniz. Yalnızca özel Bulutlar tooappear hello portalında istiyorsanız, hello bulut hello VMM Yönetici konsolunda bu ayarı etkinleştirebilirsiniz.

### <a name="prepare-for-network-mapping"></a>Ağ eşlemesi için hazırlanma
Site Recovery dağıtımı sırasında ağ eşlemesini ayarlamanız gerekir. Ağ eşlemesi VMM VM ağları ve hedef Azure ağları kaynak aşağıdaki tooenable hello arasında eşler:

* Merhaba üzerinde aynı yük devri makineler ağ tooeach diğer bağlanma, bunlar üzerinde içinde gerçekleştirmiyor olsa bile yolu veya hello aynı hello aynı kurtarma planı.
* Bir ağ geçidi hello hedef Azure ağında ayarlanıp ayarlanmadığını Azure sanal makineleri tooon içi sanal makinelere bağlanabilir.
* tooset ağ eşlemesi, işte gerekenler:

  * Merhaba kaynağı Hyper-V konak sunucusu üzerinde sanal makineleri bağlı tooa VMM VM ağ olduğundan emin olun. Bu ağ hello Bulutu ile ilişkili mantıksal ağ bağlantılı tooa olmalıdır.
  * [Yukarıda](#set-up-an-azure-network) açıklandığı gibi bir Azure ağına sahip olmanız gerekir.

## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. **Yeni** > **İzleme + Yönetim** > **Backup and Site Recovery (OMS)** öğesine tıklayın.

    ![Yeni kasa](./media/site-recovery-vmm-to-azure/new-vault3.png)
3. İçinde **adı**, bir kolay ad tooidentify hello kasası belirtin. Birden fazla aboneliğiniz varsa bunlardan birini seçin.
4. [Kaynak grubu oluşturun](../azure-resource-manager/resource-group-template-deploy-portal.md) veya var olan bir grubu seçin. Bir Azure bölgesi belirtin. Makineler çoğaltılmış toothis bölge olacaktır. desteklenen toocheck bölgeler coğrafi kullanılabilirlik kısmına bakın [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Tooquickly erişim hello hello Pano kasadan istiyorsanız, **PIN toodashboard** > **kasa Oluştur**.

    ![Yeni kasa](./media/site-recovery-vmm-to-azure/new-vault.png)

Merhaba yeni kasa görünür hello üzerinde **Pano** > **tüm kaynakları**ve hello ana **kurtarma Hizmetleri kasaları** dikey.


## <a name="select-hello-protection-goal"></a>Merhaba koruma hedefi seçin

İstediğinizi seçin, tooreplicate ve tooreplicate için istediğiniz.

1. İçinde **kurtarma Hizmetleri kasaları**seçin hello kasası.
2. **Başlarken** bölümünde, **Site Recovery** > **Altyapıyı Hazırlama** > **Koruma hedefi** seçeneklerine tıklayın.

    ![Hedefleri seçme](./media/site-recovery-vmm-to-azure/choose-goals.png)
3. İçinde **koruma hedefi** seçin **tooAzure**seçip **Evet, Hyper-V ile**. Seçin **Evet** VMM toomanage Hyper-V konakları ve hello kurtarma sitesi kullanmakta olduğunuz tooconfirm. Daha sonra, **Tamam**'a tıklayın.

## <a name="set-up-hello-source-environment"></a>Merhaba kaynak ortamını ayarlama

Hello Azure Site Recovery sağlayıcısı hello VMM sunucusuna yükleyin ve hello sunucu hello kasaya kaydedin. Hello Azure kurtarma Hizmetleri aracısını Hyper-V ana bilgisayarlarına yükleyin.

1. **Altyapıyı Hazırlama** > **Kaynak** seçeneklerine tıklayın.

    ![Kaynağı ayarlama](./media/site-recovery-vmm-to-azure/set-source1.png)

2. İçinde **kaynağı**, tıklatın **+ VMM** tooadd bir VMM sunucusu.

    ![Kaynağı ayarlama](./media/site-recovery-vmm-to-azure/set-source2.png)

3. İçinde **Sunucu Ekle**, denetleyin **System Center VMM sunucusunun** görünür **sunucu türü** ve hello VMM sunucusunun hello karşılayan [önkoşulları ve URL gereksinimleri](#prerequisites).
4. Hello Azure Site Recovery sağlayıcısı yükleme dosyasını indirin.
5. Merhaba kayıt anahtarını indirin. Kurulumu çalıştırırken buna ihtiyacınız olur. Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.

    ![Kaynağı ayarlama](./media/site-recovery-vmm-to-azure/set-source3.png)


## <a name="install-hello-provider-on-hello-vmm-server"></a>Merhaba sağlayıcısı hello VMM sunucusuna yükleyin

1. Merhaba sağlayıcı kurulum dosyasını hello VMM sunucusunda çalıştırın.
2. **Microsoft Update** kısmından güncelleştirmeleri seçebilirsiniz. Böylece, Sağlayıcı güncelleştirmeleri Microsoft Update ilkenize uygun şekilde yüklenir.
3. İçinde **yükleme**, kabul etmek veya hello varsayılan sağlayıcı yükleme konumunu değiştirmek ve tıklatın **yükleme**.

    ![Yükleme konumu](./media/site-recovery-vmm-to-azure/provider2.png)
4. Yükleme bittiğinde, bilgisayarınızı **kaydetmek** hello kasadaki tooregister hello VMM sunucusu.
5. Merhaba, **kasa ayarlarını** sayfasında, **Gözat** tooselect hello kasa anahtarı dosyasını. Hello Azure Site Recovery aboneliğine ve hello kasa adını belirtin.

    ![Sunucu kaydı](./media/site-recovery-vmm-to-azure/provider10.PNG)
6. İçinde **Internet bağlantısı**, nasıl hello VMM sunucusunda çalışan sağlayıcı üzerinden tooSite kurtarma bağlanacağı hello hello Internet belirtin.

   * Merhaba sağlayıcısı tooconnect doğrudan istiyorsanız seçin **tooAzure Site Recovery Ara sunucu olmadan doğrudan bağlan**.
   * Var olan ara sunucunuz kimlik doğrulaması gerektiren veya toouse özel bir ara sunucu isterseniz seçin **tooAzure Site kurtarma proxy sunucusu kullanarak bağlanmak**.
   * Özel bir ara sunucu kullanırsanız, başlangıç adresi, bağlantı noktası ve kimlik bilgilerini belirtin.
   * Bir proxy sunucu kullanıyorsanız, zaten açıklanan hello URL'lere izin [Önkoşullar](#on-premises-prerequisites).
   * Özel bir ara sunucu kullanırsanız, VMM RunAs hesabı (DRAProxyAccount) belirtilen hello kullanılarak otomatik olarak oluşturulacak proxy kimlik bilgileri. Bu hesap başarıyla doğrulanabilmesi hello proxy sunucusunu yapılandırın. Merhaba VMM RunAs hesabı ayarları hello VMM konsolundan değiştirilebilir. İçinde **ayarları**, genişletin **güvenlik** > **farklı çalıştır hesapları**ve ardından hello DRAProxyAccount parolasını değiştirin. Bu ayar etkinleşir toorestart hello VMM hizmeti gerekmektedir.

     ![internet](./media/site-recovery-vmm-to-azure/provider13.PNG)
7. Kabul edin veya veri şifreleme için otomatik olarak oluşturulan bir SSL sertifikası hello konumunu değiştirin. Hello Azure Site Recovery portalında Azure tarafından korunan bir bulut için veri şifrelemeyi etkinleştirirseniz, bu sertifika kullanılır. Bu sertifikayı güvenli bir yerde saklayın. Bir yük devretme tooAzure çalıştırdığınızda, veri şifreleme etkinleştirilmişse, toodecrypt, gerekir.

    > [!NOTE]
    > Azure Site Recovery tarafından sağlanan hello veri şifreleme seçeneği kullanmak yerine, kalan verileri şifrelemek için Azure tarafından sağlanan toouse hello şifreleme özelliği önerilir. Azure tarafından sağlanan hello şifreleme özelliği için bir depolama açık > Hesap ve hello şifreleme/şifre çözme Azure Depolama tarafından işlenmiş olarak daha iyi performans elde yardımcı olur.
    > [Azure Depolama hizmeti şifrelemesi hakkında daha fazla bilgi edinin](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
8. İçinde **sunucu adı**, hello kasasında bir kolay ad tooidentify hello VMM sunucusu belirtin. Bir küme yapılandırmasında hello VMM kümesi rolü adını belirtin.
9. Etkinleştirme **bulut meta verilerini eşitle**hello kasası ile Merhaba VMM sunucusundaki tüm Bulutlar için toosynchronize meta verileri istiyorsanız. Bu eylem, yalnızca bir kez her sunucuda toohappen gerekir. Tüm bulutlar toosynchronize istemiyorsanız bu ayarı işaretsiz bırakın ve her Bulutu ayrı ayrı hello hello VMM konsolundaki bulut özellikleri eşitleyin. Tıklatın **kaydetmek** toocomplete hello işlemi.

    ![Sunucu kaydı](./media/site-recovery-vmm-to-azure/provider16.PNG)
10. Kayıt başlar. Kayıt tamamlandıktan sonra hello sunucu görüntülenen **Site Recovery altyapısı** > **VMM sunucuları**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Hello Azure kurtarma Hizmetleri aracısını Hyper-V ana bilgisayarlarına yükleme

1. Sağlayıcı hello ayarladıktan sonra hello Azure kurtarma Hizmetleri Aracısı toodownload hello yükleme dosyası gerekir. Her Hyper-V sunucusu hello VMM bulutu için Kurulumu çalıştırın.

    ![Hyper-V siteleri](./media/site-recovery-vmm-to-azure/hyperv-agent1.png)
2. **Önkoşul Denetimi**’nde **İleri**'ye tıklayın. Eksik önkoşullar otomatik olarak yüklenir.

    ![Kurtarma Hizmetleri Aracısı Önkoşulları](./media/site-recovery-vmm-to-azure/hyperv-agent2.png)
3. İçinde **yükleme ayarları**kabul edin veya hello yükleme konumu ve hello önbellek konumunu değiştirin. Hello önbellek en az 5 GB depolama alanı kullanılabilir olan bir sürücüde yapılandırabilirsiniz, ancak 600 GB veya daha fazla boş alana sahip bir önbellek sürücüsü kullanmanızı öneririz. Ardından **Yükle**'ye tıklayın.
4. Yükleme tamamlandıktan sonra tıklayın **Kapat** toofinish.

    ![MARS Aracısı'nı Kaydetme](./media/site-recovery-vmm-to-azure/hyperv-agent3.png)

### <a name="command-line-installation"></a>Komut satırı yüklemesi
Microsoft Azure kurtarma Hizmetleri Aracısı hello komutu aşağıdaki hello kullanarak komut satırından yükleyebilirsiniz:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Internet proxy erişim tooSite kurtarma Hyper-V konakları ayarlama

Merhaba kurtarma Hizmetleri aracısını Hyper-V konakları üzerinde çalışan VM çoğaltması için Internet erişimi tooAzure gerekir. Erişiyorsanız Internet hello bir proxy üzerinden, aşağıdaki gibi ayarlayın:

1. Merhaba Hyper-V ana bilgisayarda Hello Microsoft Azure Backup MMC eklentisini açın. Varsayılan olarak, Microsoft Azure yedekleme için bir kısayol hello masaüstünde veya C:\Program Files\Microsoft Azure Recovery Services agent\bin\wabadmin yolunda kullanılabilir.
2. Merhaba ek bileşeninde, tıklatın **özelliklerini değiştirme**.
3. Merhaba üzerinde **Proxy Yapılandırması** sekmesinde, proxy sunucusu bilgilerini belirtin.

    ![MARS Aracısı'nı Kaydetme](./media/site-recovery-vmm-to-azure/mars-proxy.png)
4. Bu hello aracı hello açıklanan hello URL'leri ulaşmak denetleyin [Önkoşullar](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Merhaba hedef ortamını ayarlama
Çoğaltma için kullanılan hello Azure depolama hesabı toobe belirtin ve hello Azure ağ toowhich Azure Vm'lerinin yük devretme sonrasında bağlanır.

1. Tıklatın **altyapıyı hazırlama** > **hedef**hello aboneliği seçin ve hello devredilen sanal makinelerin toocreate hello istediğiniz kaynak grubu. Toouse (Klasik veya resource management) azure'da hello devredilen sanal makinelerin istediğiniz hello dağıtım modelini seçin.

    ![Depolama](./media/site-recovery-vmm-to-azure/enablerep3.png)

2. Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.

    ![Depolama](./media/site-recovery-vmm-to-azure/compatible-storage.png)

3. Bir depolama hesabı oluşturmadıysanız ve toocreate bir istiyorsanız Kaynak Yöneticisi'ni kullanarak tıklatın **+ depolama hesabı** toodo bu işlemi satır içinde.  Merhaba üzerinde **depolama hesabı oluşturma** dikey penceresinde bir hesap adı, türü, abonelik ve konum belirtin. Merhaba hesap hello olmalıdır hello aynı konuma kurtarma Hizmetleri kasası.

   ![Depolama](./media/site-recovery-vmm-to-azure/gs-createstorage.png)


   * Merhaba Klasik modeli kullanarak bir depolama hesabı toocreate istiyorsanız, hello Azure portal yapın. [Daha fazla bilgi](../storage/common/storage-create-storage-account.md)
   * Çoğaltılan veriler için bir premium depolama hesabı kullanıyorsanız, bir ek bir standart depolama hesabı, devam eden değişiklikler tooon içi verilerini yakalama toostore çoğaltma günlükleri ayarlayın.
5. Bir Azure ağı oluşturmadıysanız ve toocreate bir istiyorsanız Kaynak Yöneticisi'ni kullanarak tıklatın **+ ağ** toodo bu işlemi satır içinde. Merhaba üzerinde **sanal ağ oluştur** dikey penceresinde, bir ağ adı, adres aralığı, alt ağ ayrıntıları, abonelik ve konum belirtin. Merhaba ağ hello olmalıdır hello aynı konuma kurtarma Hizmetleri kasası.

   ![Ağ](./media/site-recovery-vmm-to-azure/gs-createnetwork.png)

   Merhaba Klasik modeli kullanarak bir ağ toocreate istiyorsanız, hello Azure portal yapın. [Daha fazla bilgi edinin](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

### <a name="configure-network-mapping"></a>Ağ eşlemesini yapılandırma

* Ağ eşlemesi işlevinin genel hatlarını [okuyun](#prepare-for-network-mapping).
* Sanal makineler hello VMM sunucusunda bağlı tooa VM ağı olduğunu ve en az bir Azure sanal ağı oluşturduğunuzu doğrulayın. Birden fazla VM ağı eşlenen tooa tek Azure ağ olabilir.

Eşleme işlemini şu şekilde yapılandırın:

1. İçinde **Site Recovery altyapısı** > **ağ eşlemeleri** > **ağ eşlemesi**, hello tıklatın **+ ağ eşlemesi**  simgesi.

    ![Ağ eşlemesi](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. İçinde **ağ eşlemesi Ekle**seçin hello kaynak VMM sunucusunu ve **Azure** hello hedefi olarak.
3. Yük devretme sonrasında Hello abonelik ve hello dağıtım modeli doğrulayın.
4. İçinde **kaynak ağ**seçin hello kaynak şirket içi VM ağını hello VMM sunucusuyla ilişkili hello listeden toomap istiyor.
5. İçinde **hedef ağ**, hello hangi çoğaltma Azure VM'ler konumlandırılacağı oluşturuldukları zaman Azure ağı seçin. Daha sonra, **Tamam**'a tıklayın.

    ![Ağ eşlemesi](./media/site-recovery-vmm-to-azure/network-mapping2.png)

Ağ eşlemesi başladığında gerçekleşecekler şunlardır:

* Eşleme başladığında hello kaynak VM ağındaki VM'ler bağlı toohello hedef ağ tabanlıdır. Yeni sanal makineleri bağlı toohello kaynak VM ağına bağlı Çoğaltma gerçekleştiğinde eşlenen Azure ağ toohello.
* Varolan bir ağ eşlemesini değiştirirseniz, çoğaltma sanal makineleri hello yeni ayarları kullanarak bağlanır.
* Merhaba hedef ağ birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme sonrasında toothat hedef alt bağlanır.
* Eşleşen ada sahip bir hedef alt ağ varsa, hello sanal makine toohello hello ağdaki ilk alt ağa bağlanır.

## <a name="configure-replication-settings"></a>Çoğaltma ayarlarını yapılandırma
1. Yeni bir çoğaltma ilkesi toocreate tıklatın **altyapıyı hazırlama** > **çoğaltma ayarları** > **+ oluştur ve ilişkilendir**.

    ![Ağ](./media/site-recovery-vmm-to-azure/gs-replication.png)
2. **İlke oluştur ve ilişkilendir** bölümünde bir ilke adı belirtin.
3. İçinde **kopyalama sıklığı**, ne sıklıkta hello ilk çoğaltma (her 30 saniyede, 5 veya 15 dakika) sonra tooreplicate değişim verileri istediğinizi belirtin.

    > [!NOTE]
    >  30 ikinci sıklığı toopremium depolama çoğaltırken desteklenmiyor. Merhaba sınırlaması, premium depolama birimi tarafından desteklenen hello anlık görüntü sayısı blob (100) başına tarafından belirlenir. [Daha fazla bilgi](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. İçinde **kurtarma noktası bekletme**, saat cinsinden ne kadar süreyle hello bekletme penceresi belirtin her kurtarma noktası için olabilir. Korumalı makineler olabilir bir pencere içinde tooany noktası kurtarıldı.
5. **Uygulamayla tutarlı anlık görüntü sıklığı** kısmında, uygulamayla tutarlı anlık görüntüleri içeren kurtarma noktasının hangi sıklıkta oluşturulacağını (1-12 saat) belirtin. Hyper-V iki çeşit anlık kullanır — bir artımlı hello tüm sanal makinenin anlık görüntüsünü sunan standart anlık görüntü ve zaman içinde nokta verilerin bir anlık görüntüsünü hello uygulama hello sanal makine içinde geçen uygulama tutarlı bir anlık görüntü. Uygulamayla tutarlı anlık görüntüleri hello anlık görüntü alınırken uygulamaların tutarlı bir durumda olan birim gölge kopyası hizmeti (VSS) tooensure kullanın. Uygulamayla tutarlı anlık görüntüleri etkinleştirirseniz, kaynak sanal makinelerde çalışan uygulamaların hello performansını etkiler unutmayın. Ayarladığınız hello değeri, yapılandırdığınız ilave kurtarma noktası hello sayısından daha az olduğundan emin olun.
6. İçinde **ilk çoğaltma başlangıç zamanı**, ne zaman toostart hello ilk çoğaltma gösterir. Merhaba çoğaltmanın internet bant genişliğiniz tooschedule isteyebilirsiniz şekilde meşgul saatleriniz dışında.
7. İçinde **Azure'da depolanan verileri şifrele**, belirtin olup olmadığını tooencrypt Azure depolama alanında rest veri. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltma ilkesi](./media/site-recovery-vmm-to-azure/gs-replication2.png)
8. Yeni bir ilke oluşturduğunuzda, otomatik olarak hello VMM Bulutu ile ilişkili. **Tamam** düğmesine tıklayın. Bu çoğaltma ilkesini ek VMM Bulutları (ve bunlara hello VM'ler) ilişkilendirebilirsiniz **çoğaltma** > ilke adı > **VMM Bulutu ile ilişkilendir**.

    ![Çoğaltma ilkesi](./media/site-recovery-vmm-to-azure/policy-associate.png)

## <a name="capacity-planning"></a>Kapasite planlaması

Temel altyapınızı ayarladığınıza göre kapasite planlaması yapmayı ve ilave kaynaklara ihtiyacınız olup olmadığını düşünün.

Site Recovery, kapasite Planlayıcısı toohelp sağlar, kaynak ortamı, Site Recovery bileşenleri, ağ ve depolama için hello doğru kaynakları ayıramadı. Merhaba Planlayıcısı ortalama bir VM'ler, diskler ve depolama birimi sayısına göre tahmin oluşturmak için Hızlı modda ya da rakamları hello iş yükü düzeyinde giriş ayrıntılı modda çalıştırabilirsiniz. Başlamadan önce:

* VM'ler, VM başına disk ve disk başına depolama dahil olmak üzere çoğaltma ortamınız hakkında bilgi toplayın.
* Çoğaltılan veriler için sahip olacaksınız hello günlük değişim (dalgalanma) hızına yönelik tahminde bulunun. Merhaba kullanabilirsiniz [Hyper-V çoğaltma için kapasite Planlayıcı](https://www.microsoft.com/download/details.aspx?id=39057) bunu toohelp.

1. Tıklatın **karşıdan**, toodownload hello aracı ve ardından çalıştırın. [Merhaba makale okuma](site-recovery-capacity-planner.md) hello araçla birlikte.
2. İşiniz bittiğinde seçin **Evet** içinde **hello kapasite Planlayıcısı çalıştırmak**?

   ![Kapasite planlaması](./media/site-recovery-vmm-to-azure/gs-capacity-planning.png)

   [Ağ bant genişliğini denetleme](#network-bandwidth-considerations) hakkında daha fazla bilgi edinin




## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme

Başlamadan önce Azure kullanıcı hesabınızın gerekli hello sahip olduğundan emin olun [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) yeni bir sanal makine tooAzure tooenable çoğaltması.

Şimdi aşağıda belirtilen şekilde çoğaltmayı etkinleştirin:

1. **2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın. Hello için çoğaltma ilk kez etkinleştirdikten sonra tıklayın **+ Çoğalt** hello kasa tooenable çoğaltma ilave makineler için.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmm-to-azure/enable-replication1.png)
2. Merhaba, **kaynak** dikey penceresinde, select hello VMM sunucusu ve hello bulut hello Hyper-V konakları konumlandırıldığını. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmm-to-azure/enable-replication-source.png)
3. İçinde **hedef**hello aboneliği, yük devretme sonrası dağıtım modeli seçin ve hello çoğaltılan veriler için kullandığınız depolama hesabı.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmm-to-azure/enable-replication-target.png)
4. Toouse istediğiniz hello depolama hesabını seçin. Toouse sahip farklı bir depolama hesabı olandan isterseniz [oluşturmak](#set-up-an-azure-storage-account). Çoğaltılan veriler için bir premium depolama hesabı kullanıyorsanız, devam eden değişiklikler tooon içi data.toocreate yakalama hello Resource Manager modelini kullanarak bir depolama hesabı bir ek bir standart depolama hesabı toostore çoğaltma günlükleri tooselect gerekir tıklatın **Yeni Oluştur**. Merhaba Klasik modeli kullanarak bir depolama hesabı toocreate istiyorsanız, bunu [hello Azure portal'ın](../storage/common/storage-create-storage-account.md). Daha sonra, **Tamam**'a tıklayın.
5. Yük devretme sonrasında oluşturulduğunda select hello Azure ağ ve alt ağ toowhich Azure VM'ler bağlanır. Seçin **seçili makineler için Şimdi Yapılandır**, seçtiğiniz tooapply hello ağ ayarı tooall makineler için koruma. Seçin **daha sonra yapılandırma**, tooselect hello makine başına Azure ağı. Toouse elinizde kullanılanlardan farklı bir ağ isterseniz [oluşturmak](#set-up-an-azure-network). kullanarak bir ağ toocreate hello Resource Manager modeli tıklatın **Yeni Oluştur**. Merhaba Klasik modeli kullanarak bir ağ toocreate istiyorsanız, bunu [hello Azure portal'ın](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Bir alt ağ (varsa) seçin. Daha sonra, **Tamam**'a tıklayın.
6. İçinde **sanal makineleri** > **sanal makine Seç**, tıklatın ve tooreplicate istediğiniz her bir makine seçin. Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmm-to-azure/enable-replication5.png)

7. İçinde **özellikleri** > **özelliklerini yapılandırma**, seçili hello VM'ler için hello işletim sistemini seçin ve işletim sistemi diski hello.

    - Bu hello Azure VM adı (hedef) uyumlu ile doğrulayın [Azure sanal makine gereksinimlerini](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Varsayılan olarak tüm hello diskleri hello VM, çoğaltma için seçilir, ancak diskleri tooexclude temizleyebilirsiniz bunları.

        - Tooexclude diskleri tooreduce çoğaltma bant genişliği isteyebilirsiniz. Örneğin, geçici verileri tooreplicate disklerle istemeyebilirsiniz veya (pagefile.sys veya Microsoft SQL Server tempdb gibi) her zaman bir makine ya da uygulamaları yeniledi verileri yeniden başlatır. Merhaba disk unselecting hello disk tarafından çoğaltma dışında bırakabilirsiniz.
        - Yalnızca temel diskler dışarıda bırakılabilir. İşletim sistemi diskleri dışarıda bırakılamaz.
        - Dinamik diskleri dışarıda tutmamanızı öneririz. Site Recovery, konuk VM içerisindeki bir sanal sabit diskin temel mi yoksa dinamik mi olduğunu anlayamaz. Tüm bağımlı dinamik birimi disklerinin dışlanan olmayan varsa, hello korumalı dinamik disk hello VM yöneltilir ve bu disk üzerindeki hello verileri erişilebilir olmayacaktır başarısız disk olarak gösterir.
        - Çoğaltmayı etkinleştirdikten sonra çoğaltma için disk ekleme veya kaldırma gerçekleştiremezsiniz. Tooadd, veya bir disk dışlamak istiyorsanız Merhaba VM toodisable koruma gerektiren ve yeniden etkinleştirin.
        - Azure'da el ile oluşturduğunuz diskler yeniden çalışır duruma getirilmez. Örneğin, üzerinde üç disk başarısız ve iki doğrudan Azure VM'deki oluşturursanız, üzerinden başarısız olan yalnızca hello üç disk geri Azure tooHyper-V ile başarısız. Yeniden çalışma veya Hyper-V tooAzure ters çoğaltmayı el ile oluşturulan diskleri ekleyemezsiniz.
        - Bir uygulama toooperate için gerekli olan bir disk bıraksanız sonra Yük devretme tooAzure azure'da uygulama bu hello çoğaltılan şekilde el ile çalıştırabilirsiniz toocreate gerekir. Alternatif olarak, bir kurtarma planı toocreate hello disk hello makinenin yük devretme sırasında Azure Otomasyon tümleştirin.

    Tıklatın **Tamam** toosave değişiklikler. Daha sonra ek özellikleri ayarlayabilirsiniz.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

8. İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, istediğiniz tooapply hello VM'ler korumalı hello çoğaltma ilkesi seçin. Daha sonra, **Tamam**'a tıklayın. Merhaba Çoğaltma İlkesi'nde değiştirebilirsiniz **çoğaltma ilkeleri** > ilke adı > **ayarlarını Düzenle**. Uyguladığınız değişiklikler, zaten çoğaltılmakta olan makinelere ve yeni makinelere uygulanır.

   ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmm-to-azure/enable-replication7.png)

Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **işleri** > **Site Recovery işleri**. Merhaba sonra **korumayı Sonlandır** işi çalıştırır, hello makine yük devretme için hazır.

### <a name="view-and-manage-vm-properties"></a>VM özelliklerini görüntüleme ve yönetme

Merhaba hello kaynak makinenin özelliklerini doğrulamanızı öneririz. Bu hello Azure VM adı ile uygun olması unutmayın [Azure sanal makine gereksinimlerini](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. İçinde **korunan öğeler**, tıklatın **çoğaltılan öğeler**, ve ayrıntılarını Seç hello makine toosee.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmm-to-azure/vm-essentials.png)
2. İçinde **özellikleri**, çoğaltma görebilirsiniz ve Yük Devretme bilgilerini hello VM.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmm-to-azure/test-failover2.png)
3. İçinde **işlem ve ağ** > **işlem özellikleri**, hello Azure VM adını ve hedef boyutu belirtebilirsiniz. Merhaba adı toocomply ile değiştirmek [Azure gereksinimleri](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) gerekiyorsa. Ayrıca görüntülemek ve hello hedef ağ, alt ağ ve atanan başlangıç IP adresi hakkında bilgi değiştirme toohello Azure VM.
Şunlara dikkat edin:

   * Merhaba hedef IP adresini ayarlayabilirsiniz. Bir adresi sağlamazsanız, yükü devredilen makine üzerinde hello DHCP kullanır. Yük devretmede kullanılamayan bir adres ayarlarsanız hello yük devretme başarısız olur. Merhaba hello test yük devretme ağı testinde Hello adresi varsa, yük devretme sınaması için aynı hedef IP adresi kullanılabilir.
   * ağ bağdaştırıcısı Hello sayısını hello hedef sanal makine için aşağıdaki gibi belirtin hello boyuta göre dikte edilir:

     * Merhaba hello kaynak makinedeki ağ bağdaştırıcısı sayısı küçük veya buna eşit ise toohello bağdaştırıcı sayısı hello hedef makine boyutu için izin verilen sonra hello hedef olacaktır hello aynı sayıda bağdaştırıcıya hello kaynağı olarak.
     * Merhaba hello kaynak sanal makinenin bağdaştırıcı sayısı aşarsa hello hello hedef boyutu için izin verilen sonra hello maksimum hedef boyutu kullanılır.
     * Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hello hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa, hello hedef makinenin iki bağdaştırıcısı gerekir. Merhaba kaynak makinenin iki bağdaştırıcısı varsa, ancak hello hedef boyut yalnızca bir destekler, hello hedef makine yalnızca bir bağdaştırıcısı olur.     
     * Merhaba VM birden çok ağ bağdaştırıcısı varsa, bunların tümü toohello bağlanır aynı ağ.

     ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmm-to-azure/test-failover4.png)

4. İçinde **diskleri** hello çoğaltılır VM üzerinde hello işletim sistemi ve veri disklerini görebilirsiniz.

#### <a name="managed-disks"></a>Yönetilen diskler

İçinde **işlem ve ağ** > **işlem özellikleri**, tooattach yönetilen diskleri tooyour geçiş tooAzure makinede isterseniz "Yönetilen diskleri kullanımını" ayarı çok "Evet" Merhaba VM ayarlayabilirsiniz. Yönetilen diskleri hello VM disklerle ilişkilendirilmiş hello depolama hesaplarını yöneterek Azure Iaas VM'ler için disk yönetimi basitleştirir. [Yönetilen diskler hakkında daha fazla bilgi edinin](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Oluşturulan ve ekli toohello sanal makinede yalnızca bir yük devretme tooAzure yönetilen disklerdir. Korumayı etkinleştirmek için şirket içi makineler verilerden tooreplicate toostorage hesapları devam eder.
   Yönetilen diskler yalnızca hello Resource manager dağıtım modeli kullanılarak dağıtılan sanal makineleri için oluşturulabilir.  

  > [!NOTE]
  > Yeniden çalışma Azure tooon içi Hyper-V Ortamı'ndan yönetilen disklerle makineler için şu anda desteklenmiyor. Bu makineye Azure toomigrate düşünüyorsanız "Yönetilen diskleri kullanımını" çok "Evet" ayarlayın.

   - "Yönetilen diskleri kullanımını" çok "Evet" ayarladığınızda, yalnızca hello kaynak grubundaki kullanılabilirlik kümeleri "Kullanım diskleri yönetilen" olarak ayarlanmış çok "Evet" seçime uygun olacaktır. Bu durum, yönetilen bir diske sahip sanal makineler yalnızca parçası "Yönetilen kullanım diskleri" özelliği ayarlanmış kullanılabilirlik kümeleri çok "Evet" olabilir çünkü. Kullanılabilirlik kümeleri, yük devretme hedefi toouse yönetilen disklerde göre "Yönetilen kullanım diskleri" özellik kümesi ile oluşturduğunuzdan emin olun.  Benzer şekilde, "Yönetilen diskleri kullanımını" çok "Hayır" ayarladığınızda, hello kaynak grubunda "Yönetilen diskleri kullanımını" özelliği çok "Hayır" olarak ayarlanmış yalnızca kullanılabilirlik kümeleri seçime uygun olacaktır. [Yönetilen diskler ve kullanılabilirlik kümeleri hakkında daha fazla bilgi edinin](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Merhaba depolama hesabı çoğaltma için kullanılan herhangi bir noktada zamanında depolama hizmeti şifrelemesi ile şifrelenmişse, yük devretme sırasında yönetilen diskleri oluşturma başarısız olur. Seçebilir ya da "Yönetilen diskleri kullanımını" çok "Hayır" ayarlayın ve yük devretme yeniden deneyin veya hello sanal makine için korumayı devre dışı bırakmak ve herhangi bir noktada zamandaki etkin depolama hizmeti şifrelemesi sahip değilse, tooa depolama hesabı koruyun.
  > [Depolama Hizmeti Şifrelemesi ve yönetilen diskler hakkında daha fazla bilgi edinin](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Merhaba dağıtımı test etme

tootest hello dağıtımı, bir yük devretme sınaması için tek bir sanal makine ya da bir veya daha fazla sanal makine içeren bir kurtarma planı çalıştırabilirsiniz.

### <a name="before-you-start"></a>Başlamadan önce

 - Tooconnect tooAzure VM'ler istiyorsanız, yük devretme işleminden sonra RDP kullanarak bilgi hakkında [tooconnect hazırlama](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - Active Directory ve DNS toocopy test ortamınızda gereksinim duyduğunuz toofully sınayın. [Daha fazla bilgi edinin](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma

1. tek bir VM üzerinde toofail içinde **çoğaltılan öğeler**, hello VM tıklayın > **+ yük devretme testi**.
2. bir kurtarma üzerinden toofail planlama **kurtarma planları**, sağ hello planı > **yük devretme testi**. bir kurtarma planı toocreate [bu yönergeleri izleyin](site-recovery-create-recovery-plans.md).
3. İçinde **yük devretme testi**seçin hello Azure ağ toowhich Azure VM'ler, yük devretme gerçekleştikten sonra bağlanın.
4. Tıklatın **Tamam** toobegin hello yük devretme. Merhaba VM tooopen üzerinde özelliklerini tıklayarak ya da hello ilerleme durumunu izleyebilirsiniz **yük devretme testi** iş **Site Recovery işleri**.
5. Hello yük devretme işlemi tamamlandıktan sonra ayrıca olması toosee hello çoğaltma Azure makine görünür hello Azure portalı > **sanal makineleri**. Bu hello VM, toohello uygun ağ bağlandı ve çalışır durumda olduğundan hello uygun boyutta olduğundan emin olmanız gerekir.
6. Yük devretme sonrasında bağlantıları için hazır durumunda mümkün tooconnect toohello Azure VM olması gerekir.
7. İşiniz bittiğinde tıklayın **temizleme yük devretme testi** hello kurtarma planı üzerinde. İçinde **notları** kaydedin ve hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek. Bu yük devretme testi sırasında oluşturulan hello sanal makineleri siler.

Daha fazla ayrıntı için hello okuma [Test yük devretme tooAzure](site-recovery-test-failover-to-azure.md) makalesi.

## <a name="monitor-hello-deployment"></a>İzleyici hello dağıtım

İşte yapılandırma ayarları, durum ve hello Site Recovery dağıtımı için sistem durumu nasıl izleyebilirsiniz:

1. Tıklatın hello kasa adı tooaccess hello üzerinde **Essentials** Pano. Bu panoda Site Recovery işlerini, çoğaltma durumunu, kurtarma planlarını, sunucu sistem durumunu ve olayları izleyebilirsiniz.  Özelleştirebileceğiniz **Essentials** tooshow hello kutucukları ve diğer Site Recovery ve Backup kasalarını hello durumu da dahil olmak üzere en yararlı tooyou olan düzenler.

    ![Temel Bileşenler](./media/site-recovery-vmm-to-azure/essentials.png)
2. İçinde **sistem durumu**, şirket içi sunucuların (VMM veya yapılandırma sunucuları) sorunları izleyebilir ve hello son 24 saat hello Site Recovery tarafından başlatılan olayları.
3. Merhaba, **çoğaltılan öğeler**, **kurtarma planları**, ve **Site Recovery işleri** yönetmek ve izlemek çoğaltma döşeme. **İşler** > **Site Recovery İşleri** seçeneklerinden işlerin ayrıntılarına ulaşabilirsiniz.

## <a name="command-line-installation-for-hello-azure-site-recovery-provider"></a>Hello Azure Site Recovery sağlayıcısı için komut satırı yüklemesi

Hello Azure Site Recovery sağlayıcısı hello komut satırı yüklenebilir. Bu yöntem, kullanılan tooinstall hello çekirdek Windows Server 2012 R2 için sunucu sağlayıcısında olabilir.

1. Merhaba sağlayıcısı yükleme dosyasını ve kayıt anahtarı tooa klasörü indirin. Örneğin, C:\ASR.
2. Yükseltilmiş bir komut isteminden aşağıdaki komutları tooextract hello sağlayıcı yükleyicisini çalıştırın:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Bu komut tooinstall hello bileşenleri çalıştırın:

            C:\ASR> setupdr.exe /i
4. Ardından bu komutlar, tooregister hello sunucu hello kasasına çalıştırın:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

Konumlar:

* **/ Credentials**: hello kayıt anahtarı dosyasının bulunduğu belirten zorunlu parametre.  
* **/ FriendlyName**: hello Azure Site Recovery portalında görünen hello Hyper-V ana bilgisayar sunucusunun adını hello için zorunlu parametre.
* * **/ EncryptionEnabled**: vmm'de Hyper-V sanal makineleri çoğaltırken isteğe bağlı bir parametre Bulutlar tooAzure. Tooencrypt sanal makineleri azure'da (Bekleyen şifreleme) isteyip istemediğinizi belirtin. Bu hello olun hello dosyanın adı olan bir **.pfx** uzantısı. Varsayılan olarak şifreleme kapalıdır.

    > [!NOTE]
    > Azure Site Recovery tarafından sağlanan hello şifreleme seçeneği (EncryptionEnabled seçenek) kullanmak yerine, kalan verileri şifrelemek için Azure tarafından sağlanan toouse hello şifreleme özelliği önerilir. Azure tarafından sağlanan hello şifreleme özelliği için bir depolama hesabı açılabilir ve yardımcı hello şifreleme/şifre çözme Azure tarafından gerçekleştirilir gibi daha iyi performans elde etmek  
    > olur.
    > [Azure Depolama hizmeti şifrelemesi hakkında daha fazla bilgi edinin](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
* **/ proxyaddress**: hello proxy sunucusunun hello adresini belirten isteğe bağlı parametre.
* **/ proxyport**: hello proxy sunucusunun hello bağlantı noktasını belirten isteğe bağlı parametre.
* **/ proxyusername**: (proxy kimlik doğrulaması gerektiriyorsa) hello Ara sunucu kullanıcı adını belirten isteğe bağlı parametre.
* **/ proxypassword**: (Merhaba proxy kimlik doğrulaması gerektiriyorsa) proxy sunucusu ile Merhaba parola tooauthenticate belirten isteğe bağlı parametre.


### <a name="network-bandwidth-considerations"></a>Ağ bandı genişliği ile ilgili dikkat edilmesi gerekenler
(İlk çoğaltma ve ardından değişim) çoğaltma için gereksinim duyduğunuz hello kapasite planlayıcısı aracı toocalculate hello bant genişliği kullanabilir. Çoğaltma için bant genişliği kullanım toocontrol hello miktarı, birkaç seçeneğiniz vardır:

* **Bant genişliğini kısıtlama**: tooa ikincil siteye çoğaltılan Hyper-V trafiği belirli bir Hyper-V ana bilgisayar üzerinden gider. Merhaba ana bilgisayar sunucusunda bant genişliğini kısıtlayabilirsiniz.
* **Bant genişliği ince ayar**: birkaç kayıt defteri anahtarlarını kullanarak çoğaltma için kullanılan hello bant genişliği etkileyebilir.

#### <a name="throttle-bandwidth"></a>Bant genişliğini kısıtlama
1. Merhaba Hyper-V konak sunucusunda Hello Microsoft Azure Backup MMC eklentisini açın. Varsayılan olarak, Microsoft Azure yedekleme için bir kısayol hello masaüstünde veya C:\Program Files\Microsoft Azure Recovery Services agent\bin\wabadmin yolunda kullanılabilir.
2. Merhaba ek bileşeninde, tıklatın **özelliklerini değiştirme**.
3. Merhaba üzerinde **azaltma** sekmesine **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir**, iş için hello sınırını ayarlama ve saat İş dışı. Geçerli aralıklar saniye başına 512 Kbps too102 Mbps arasındadır.

    ![Bant genişliğini kısıtlama](./media/site-recovery-vmm-to-azure/throttle2.png)

Merhaba de kullanabilirsiniz [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) tooset cmdlet azaltma. Bu ayara ilişkin örneği aşağıda bulabilirsiniz:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting - NoThrottle** hiçbir azaltmanın gerekli olmadığını gösterir.

#### <a name="influence-network-bandwidth"></a>Ağ bant genişliği üzerinde etki oluşturma
Merhaba **UploadThreadsPerVM** kayıt defteri değeri denetimleri hello veri aktarımını bir disk için (başlangıç ve değişim çoğaltması) kullanılan iş parçacıklarının sayısı. Daha yüksek bir değer çoğaltma için kullanılan hello ağ bant genişliğini artırır. Merhaba **DownloadThreadsPerVM** kayıt defteri değeri hello yeniden çalışma sırasındaki veri aktarımı için kullanılan iş parçacığı sayısını belirtir.

1. Merhaba kayıt defterinde çok gidin**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.

   * Merhaba değerini değiştirin **UploadThreadsPerVM** (veya yoksa hello anahtar oluşturun) disk çoğaltması için kullanılan toocontrol iş parçacığı sayısı.
   * Merhaba değerini değiştirin **DownloadThreadsPerVM** (veya yoksa hello anahtar oluşturun) toocontrol iş parçacığı azure'dan yeniden çalışma trafiği için kullanılır.
2. Merhaba varsayılan değer 4'tür. "Fazla sağlanan" bir ağda, bu kayıt defteri anahtarları hello varsayılan değerlerinin değiştirilmesi. Merhaba en fazla 32'dir. Trafik toooptimize hello değeri izleyin.

## <a name="next-steps"></a>Sonraki adımlar

Merhaba ihtiyaç duydukça ilk çoğaltma tamamlandıktan ve hello dağıtımı test ettikten sonra Yük devretmeler çalıştırabilirsiniz. [Daha fazla bilgi edinin](site-recovery-failover.md) yerine farklı türleri hakkında ve nasıl toorun bunları.
