---
title: "Merhaba kaynak ve hedef Azure Site Recovery ile Hyper-V çoğaltma tooAzure (System Center VMM ile) için yukarı aaaSet | Microsoft Docs"
description: "Hyper-V sanal makineleri çoğaltma VMM Bulutları tooAzure depolama Azure Site Recovery ile kaynak ve hedef ayarlar Hello adımları tooset özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a>8. adım: hello kaynak ve hedef Hyper-V (VMM ile) çoğaltma tooAzure için ayarlama

Sonra [bir kasa oluşturarak](vmm-to-azure-walkthrough-create-vault.md) ve neleri belirtme tooreplicate istediğiniz, bu makale tooconfigure kaynağı kullanmak ve şirket içi Hyper-V sanal makineleri System Center Virtual Machine Manager (VMM) çoğaltırken ayarları hedef Hello kullanarak bulut tooAzure [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Merhaba kaynak ortamını ayarlama

S1. **Altyapıyı Hazırlama** > **Kaynak** seçeneklerine tıklayın.

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. İçinde **kaynağı**, tıklatın **+ VMM** tooadd bir VMM sunucusu.

    ![Kaynağı ayarlama](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. İçinde **Sunucu Ekle**, denetleyin **System Center VMM sunucusunun** görünür **sunucu türü** ve hello VMM sunucusunun hello karşılayan [önkoşulları ve URL gereksinimleri](#prerequisites).
4. Hello Azure Site Recovery sağlayıcısı yükleme dosyasını indirin.
5. Merhaba kayıt anahtarını indirin. Kurulumu çalıştırırken buna ihtiyacınız olur. Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.

    ![Kaynağı ayarlama](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a>Merhaba sağlayıcısı hello VMM sunucusuna yükleyin

1. Merhaba sağlayıcı kurulum dosyasını hello VMM sunucusunda çalıştırın.
2. **Microsoft Update** kısmından güncelleştirmeleri seçebilirsiniz. Böylece, Sağlayıcı güncelleştirmeleri Microsoft Update ilkenize uygun şekilde yüklenir.
3. İçinde **yükleme**, kabul etmek veya hello varsayılan sağlayıcı yükleme konumunu değiştirmek ve tıklatın **yükleme**.

    ![Yükleme konumu](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. Yükleme bittiğinde, bilgisayarınızı **kaydetmek** hello kasadaki tooregister hello VMM sunucusu.
5. Merhaba, **kasa ayarlarını** sayfasında, **Gözat** tooselect hello kasa anahtarı dosyasını. Hello Azure Site Recovery aboneliğine ve hello kasa adını belirtin.

    ![Sunucu kaydı](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. İçinde **Internet bağlantısı**, nasıl hello VMM sunucusunda çalışan sağlayıcı üzerinden tooSite kurtarma bağlanacağı hello hello Internet belirtin.

   * Merhaba sağlayıcısı tooconnect doğrudan istiyorsanız seçin **tooAzure Site Recovery Ara sunucu olmadan doğrudan bağlan**.
   * Var olan ara sunucunuz kimlik doğrulaması gerektiren veya toouse özel bir ara sunucu isterseniz seçin **tooAzure Site kurtarma proxy sunucusu kullanarak bağlanmak**.
   * Özel bir ara sunucu kullanırsanız, başlangıç adresi, bağlantı noktası ve kimlik bilgilerini belirtin.
   * Bir proxy sunucu kullanıyorsanız, zaten açıklanan hello URL'lere izin [Önkoşullar](#on-premises-prerequisites).
   * Özel bir ara sunucu kullanırsanız, VMM RunAs hesabı (DRAProxyAccount) belirtilen hello kullanılarak otomatik olarak oluşturulacak proxy kimlik bilgileri. Bu hesap başarıyla doğrulanabilmesi hello proxy sunucusunu yapılandırın. Merhaba VMM RunAs hesabı ayarları hello VMM konsolundan değiştirilebilir. İçinde **ayarları**, genişletin **güvenlik** > **farklı çalıştır hesapları**ve ardından hello DRAProxyAccount parolasını değiştirin. Bu ayar etkinleşir toorestart hello VMM hizmeti gerekmektedir.

     ![internet](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. Kabul edin veya veri şifreleme için otomatik olarak oluşturulan bir SSL sertifikası hello konumunu değiştirin. Hello Azure Site Recovery portalında Azure tarafından korunan bir bulut için veri şifrelemeyi etkinleştirirseniz, bu sertifika kullanılır. Bu sertifikayı güvenli bir yerde saklayın. Bir yük devretme tooAzure çalıştırdığınızda, veri şifreleme etkinleştirilmişse, toodecrypt, gerekir.
8. İçinde **sunucu adı**, hello kasasında bir kolay ad tooidentify hello VMM sunucusu belirtin. Bir küme yapılandırmasında hello VMM kümesi rolü adını belirtin.
9. Etkinleştirme **bulut meta verilerini eşitle**hello kasası ile Merhaba VMM sunucusundaki tüm Bulutlar için toosynchronize meta verileri istiyorsanız. Bu eylem, yalnızca bir kez her sunucuda toohappen gerekir. Tüm bulutlar toosynchronize istemiyorsanız bu ayarı işaretsiz bırakın ve her Bulutu ayrı ayrı hello hello VMM konsolundaki bulut özellikleri eşitleyin. Tıklatın **kaydetmek** toocomplete hello işlemi.

    ![Sunucu kaydı](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. Kayıt başlar. Kayıt tamamlandıktan sonra hello sunucu görüntülenen **Site Recovery altyapısı** > **VMM sunucuları**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Hello Azure kurtarma Hizmetleri aracısını Hyper-V ana bilgisayarlarına yükleme

1. Sağlayıcı hello ayarladıktan sonra hello Azure kurtarma Hizmetleri Aracısı toodownload hello yükleme dosyası gerekir. Her Hyper-V sunucusu hello VMM bulutu için Kurulumu çalıştırın.

    ![Hyper-V siteleri](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. **Önkoşul Denetimi**’nde **İleri**'ye tıklayın. Eksik önkoşullar otomatik olarak yüklenir.

    ![Kurtarma Hizmetleri Aracısı Önkoşulları](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. İçinde **yükleme ayarları**kabul edin veya hello yükleme konumu ve hello önbellek konumunu değiştirin. Hello önbellek en az 5 GB depolama alanı kullanılabilir olan bir sürücüde yapılandırabilirsiniz, ancak 600 GB veya daha fazla boş alana sahip bir önbellek sürücüsü kullanmanızı öneririz. Ardından **Yükle**'ye tıklayın.
4. Yükleme tamamlandıktan sonra tıklayın **Kapat** toofinish.

    ![MARS Aracısı'nı Kaydetme](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a>Komut satırı yüklemesi
Microsoft Azure kurtarma Hizmetleri Aracısı hello komutu aşağıdaki hello kullanarak komut satırından yükleyebilirsiniz:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Internet proxy erişim tooSite kurtarma Hyper-V konakları ayarlama

Merhaba kurtarma Hizmetleri aracısını Hyper-V konakları üzerinde çalışan VM çoğaltması için Internet erişimi tooAzure gerekir. Erişiyorsanız Internet hello bir proxy üzerinden, aşağıdaki gibi ayarlayın:

1. Merhaba Hyper-V ana bilgisayarda Hello Microsoft Azure Backup MMC eklentisini açın. Varsayılan olarak, Microsoft Azure yedekleme için bir kısayol hello masaüstünde veya C:\Program Files\Microsoft Azure Recovery Services agent\bin\wabadmin yolunda kullanılabilir.
2. Merhaba ek bileşeninde, tıklatın **özelliklerini değiştirme**.
3. Merhaba üzerinde **Proxy Yapılandırması** sekmesinde, proxy sunucusu bilgilerini belirtin.

    ![MARS Aracısı'nı Kaydetme](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. Bu hello aracı hello açıklanan hello URL'leri ulaşmak denetleyin [Önkoşullar](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Merhaba hedef ortamını ayarlama
Çoğaltma için kullanılan hello Azure depolama hesabı toobe belirtin ve hello Azure ağ toowhich Azure Vm'lerinin yük devretme sonrasında bağlanır.

1. Tıklatın **altyapıyı hazırlama** > **hedef**hello aboneliği seçin ve hello devredilen sanal makinelerin toocreate hello istediğiniz kaynak grubu. Toouse (Klasik veya resource management) azure'da hello devredilen sanal makinelerin istediğiniz hello dağıtım modelini seçin.

    ![Depolama](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.

    ![Depolama](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. Bir depolama hesabı oluşturmadıysanız ve toocreate bir istiyorsanız Kaynak Yöneticisi'ni kullanarak tıklatın **+ depolama hesabı** toodo bu işlemi satır içinde.  Merhaba üzerinde **depolama hesabı oluşturma** dikey penceresinde bir hesap adı, türü, abonelik ve konum belirtin. Merhaba hesap hello olmalıdır hello aynı konuma kurtarma Hizmetleri kasası.

   ![Depolama](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * Merhaba Klasik modeli kullanarak bir depolama hesabı toocreate istiyorsanız, hello Azure portal yapın. [Daha fazla bilgi](../storage/common/storage-create-storage-account.md)
   * Çoğaltılan veriler için bir premium depolama hesabı kullanıyorsanız, bir ek bir standart depolama hesabı, devam eden değişiklikler tooon içi verilerini yakalama toostore çoğaltma günlükleri ayarlayın.
5. Bir Azure ağı oluşturmadıysanız ve toocreate bir istiyorsanız Kaynak Yöneticisi'ni kullanarak tıklatın **+ ağ** toodo bu işlemi satır içinde. Merhaba üzerinde **sanal ağ oluştur** dikey penceresinde, bir ağ adı, adres aralığı, alt ağ ayrıntıları, abonelik ve konum belirtin. Merhaba ağ hello olmalıdır hello aynı konuma kurtarma Hizmetleri kasası.

   ![Ağ](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   Merhaba Klasik modeli kullanarak bir ağ toocreate istiyorsanız, hello Azure portal yapın. [Daha fazla bilgi edinin](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).





## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 9: ağ eşlemesini yapılandırma](vmm-to-azure-walkthrough-network-mapping.md)
