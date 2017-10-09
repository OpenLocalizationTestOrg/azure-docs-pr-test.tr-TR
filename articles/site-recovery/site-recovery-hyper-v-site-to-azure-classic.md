---
title: "Merhaba Klasik Portalı'nda aaaReplicate Hyper-V sanal makineleri tooAzure | Microsoft Docs"
description: "Bu makalede, makineler VMM bulutlarında yönetilmeyen zaman tooAzure nasıl tooreplicate Hyper-V sanal makineleri açıklanmaktadır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 3f4c4483-e3dd-495a-bd02-c16e9e28c88d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/21/2017
ms.author: raynew
ms.openlocfilehash: 12d08d950a79e956436cb03ffc87ab40e86c589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-without-vmm-with-azure-site-recovery"></a>Şirket içi Hyper-V sanal makineleri (VMM olmadan) Azure Site Recovery ile Azure arasındaki çoğaltma
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Klasik Portal](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

Bu makalede nasıl tooreplicate Hyper-V sanal makineleri tooAzure hello kullanarak, şirket içi [Azure Site Recovery](site-recovery-overview.md) hello Azure portalına hizmet. Bu senaryoda, Hyper-V sunucuları VMM bulutlarında yönetilen değil.

Bu makaleyi okuduktan sonra hello altındaki tüm yorumlar post veya üzerinde hello teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="site-recovery-in-hello-azure-portal"></a>Site Kurtarma'hello Azure portalı

Azure, kaynak oluşturmak ve bu kaynaklarla çalışmak için iki [dağıtım modeli](../resource-manager-deployment-model.md) kullanır: Azure Resource Manager ve klasik model. Ayrıca Azure iki portala – hello Klasik Azure portalı ve Azure portal hello sahiptir.

Bu makalede nasıl toodeploy hello Klasik Portalı'nda. Merhaba Klasik portal kullanılan toomaintain varolan kasalarını olabilir. Yeni kasa hello Klasik portalı kullanarak oluşturulamıyor.

## <a name="site-recovery-in-your-business"></a>İşletmenizde Site Recovery

Kuruluşlar nasıl uygulamaları ve verileri planlanmış ve Planlanmamış kapalı kalma süresi sırasında çalışır ve kullanılabilir kalmasını belirleyen BCDR stratejisine gereksinim ve toonormal çalışma koşullarına mümkün olan en kısa sürede kurtarın. Site Recovery'nin sağladığı avantajlar şunlardır:

* Hyper-V VM’lerinde çalışan iş uygulamaları için şirket dışında koruma.
* Tek bir konum tooset, yönetin ve çoğaltma, yük devretme ve kurtarma izleyin.
* Basit yük devretme tooAzure ve şirket içi sitenizdeki Azure tooHyper-V ana bilgisayar sunuculardan geri dönme (geri yükleme).
* Katmanlı uygulama iş yüklerinin birlikte yük devredebilmesi için birden çok VM içeren kurtarma planları.

## <a name="azure-prerequisites"></a>Azure önkoşulları
* Bir [Microsoft Azure](https://azure.microsoft.com/) hesabınızın olması gerekir. [Ücretsiz deneme sürümüyle](https://azure.microsoft.com/pricing/free-trial/) başlayabilirsiniz.
* Bir Azure depolama hesabı toostore çoğaltılmış verileri gerekir. Merhaba hesabının coğrafi çoğaltmanın etkinleştirilmiş olması gerekir. Merhaba hello Azure Site kurtarma kasasıyla aynı bölgede ve ile ilişkili olmalıdır hello aynı abonelik. [Azure storage hakkında daha fazla bilgi](../storage/common/storage-introduction.md). Merhaba kullanılarak oluşturulan taşıma depolama hesapları desteklemiyoruz Not [yeni Azure portalına](../storage/common/storage-create-storage-account.md) kaynak grupları arasında.
* Birincil sitenizden üzerinden başarısız olduğunda Azure sanal makineleri bağlı tooa ağ böylece Azure sanal ağı gerekir.

## <a name="hyper-v-prerequisites"></a>Hyper-V önkoşulları
* Merhaba kaynak şirket içi sitede çalıştıran bir veya daha fazla sunucuya ihtiyacınız olacak **Windows Server 2012 R2** hello Hyper-V rolü yüklü olan veya **Microsoft Hyper-V Server 2012 R2**. Bu sunucu gerekir:
* Bir veya daha fazla sanal makine içeriyor.
* Bağlı toohello Internet, doğrudan veya bir proxy üzerinden olabilir.
* KB açıklanan hello düzeltmeler çalıştırması [2961977](https://support.microsoft.com/en-us/kb/2961977 "KB2961977").

## <a name="virtual-machine-prerequisites"></a>Sanal makine önkoşulları
Sanal makineleri tooprotect istediğiniz uygun ile [Azure sanal makine gereksinimlerini](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="provider-and-agent-prerequisites"></a>Sağlayıcı ve aracı önkoşulları
Azure Site Recovery dağıtımının bir parçası hello Azure Site Recovery sağlayıcısı yükleyin ve Azure kurtarma Hizmetleri Aracısı her Hyper-V sunucusunda hello. Şunlara dikkat edin:

* Her zaman hello en son sürümlerini hello sağlayıcı ve aracı çalıştırmanızı öneririz. Bunlar, hello Site Recovery portalında kullanılabilir.
* Bir kasadaki tüm Hyper-V sunucuları sahip hello aynı hello sağlayıcısı sürümleri ve aracı.
* Merhaba hello sunucuda çalışan sağlayıcı bağlayan tooSite kurtarma hello üzerinden internet. Bir ara sunucu olmadan hello Hyper-V sunucusunda yapılandırılmış hello proxy ayarlarıyla ya da sağlayıcı yüklemesi sırasında yapılandırırsınız özel proxy ayarlarıyla bunu yapabilirsiniz. Toomake tooAzure bağlanmak için bu hello URL'leri toouse istediğiniz bu hello proxy sunucusuna erişim sağlayabildiğinizden emin olmanız gerekir:

  * *.accesscontrol.windows.net
  * *.backup.windowsazure.com
  * *.hypervrecoverymanager.windowsazure.com
  * *.store.core.windows.net      
  * *.blob.core.windows.net
  - https://www.msftncsi.com/ncsi.txt
  - time.windows.com
  - time.nist.gov
* Ayrıca açıklanan hello IP adreslerinin izin [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653) ve HTTPS (443) protokolü. Merhaba toouse ve, Batı ABD planlama Azure bölgesi tooallow hello IP aralıklarını var.

Bu grafik hello farklı iletişim kanalları ve orchestration ve çoğaltma için Site Recovery tarafından kullanılan bağlantı noktaları gösterir

![B2A topolojisi](./media/site-recovery-hyper-v-site-to-azure-classic/b2a-topology.png)

## <a name="step-1-create-a-vault"></a>1. adım: bir kasa oluşturma
1. İçinde toohello oturum [Yönetim Portalı](https://portal.azure.com).
2. Genişletme **Veri Hizmetleri** > **kurtarma Hizmetleri** tıklatıp **Site Recovery kasası**.
3. **Yeni Oluştur** > **Hızlı Oluştur**'a tıklayın.
4. İçinde **adı**, bir kolay ad tooidentify hello kasası girin.
5. İçinde **bölge**, hello hello kasa için coğrafi bölgeyi seçin. desteklenen toocheck bölgeler coğrafi kullanılabilirlik kısmına bakın [Azure Site Recovery fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/site-recovery/).
6. **Kasa Oluştur**'a tıklayın.

    ![Yeni kasa](./media/site-recovery-hyper-v-site-to-azure-classic/vault.png)

Kasa hello onay hello durum çubuğu tooconfirm başarıyla oluşturuldu. Merhaba kasası listelenir **etkin** hello ana kurtarma Hizmetleri sayfasında.

## <a name="step-2-create-a-hyper-v-site"></a>2. adım: bir Hyper-V sitesi oluşturma
1. Merhaba kurtarma Hizmetleri sayfasında hello kasa tooopen hello hızlı başlangıç sayfasını tıklatın. Hızlı Başlangıç hello simgesini kullanarak herhangi bir zamanda açık olması.

    ![Hızlı Başlangıç](./media/site-recovery-hyper-v-site-to-azure-classic/quick-start-icon.png)
2. Merhaba aşağı açılan listesinde seçin **bir şirket içi Hyper-V sitesi ile Azure arasında**.

    ![Hyper-V sitesi senaryosu](./media/site-recovery-hyper-v-site-to-azure-classic/select-scenario.png)
3. İçinde **bir Hyper-V sitesi oluşturmak** tıklatın **oluşturma Hyper-V sitesi**. Bir site adı belirtin ve kaydedin.

    ![Hyper-V sitesi](./media/site-recovery-hyper-v-site-to-azure-classic/create-site.png)

## <a name="step-3-install-hello-provider-and-agent"></a>3. adım: hello sağlayıcı ve aracı yükleme
Merhaba sağlayıcı ve aracı tooprotect istediğiniz sanal makineleri olan her Hyper-V sunucusuna yükleyin.

Hyper-V kümesi üzerinde yüklüyorsanız, adım 5-11 hello yük devretme kümesindeki her düğümde gerçekleştirir. Bunlar hello kümedeki düğümler arasında geçiş olsa bile tüm düğümleri kaydedilir ve koruma etkinleştirildikten sonra sanal makineler korunur.

1. İçinde **hazırlama Hyper-V sunucuları**, tıklatın **bir kayıt anahtarı indirin** dosya.
2. Merhaba üzerinde **kayıt anahtarını indir** sayfasında, **karşıdan** sonraki toohello site. Merhaba Hyper-V sunucusu tarafından kolayca erişilebilen hello anahtar tooa güvenli konuma indirin. Merhaba anahtar oluşturulduktan sonra 5 gün boyunca geçerlidir.

    ![Kayıt anahtarı](./media/site-recovery-hyper-v-site-to-azure-classic/download-key.png)
3. Tıklatın **indirme hello sağlayıcısı** tooobtain hello en son sürümü.
4. İstediğiniz her Hyper-V sunucusu üzerinde Hello dosya tooregister hello kasasına çalıştırın. Merhaba dosyası iki bileşeni yükler:
   * **Azure Site Recovery sağlayıcısı**— iletişim ve orchestration hello Hyper-V sunucusu ve hello Azure Site Recovery portalında arasında işler.
   * **Azure kurtarma Hizmetleri Aracısı**— hello kaynak Hyper-V sunucusu ve Azure depolama üzerinde çalışan sanal makineler arasında veri aktarımı işler.
5. **Microsoft Update** kısmında güncelleştirmeleri seçebilirsiniz. Bu ayar etkinse, sağlayıcı ve aracı güncelleştirmeleri tooyour Microsoft Update ilkenize göre yüklenir.

    ![Microsoft Güncelleştirmeleri](./media/site-recovery-hyper-v-site-to-azure-classic/provider1.png)
6. İçinde **yükleme** burada tooinstall hello sağlayıcısı istediğiniz ve aracısında hello Hyper-V sunucusu belirtin.

    ![Yükleme konumu](./media/site-recovery-hyper-v-site-to-azure-classic/provider2.png)
7. Yükleme tamamlandıktan sonra Kurulum tooregister hello sunucu hello kasasına devam edin.
8. Merhaba üzerinde **kasa ayarlarını** sayfasında, **Gözat** tooselect hello anahtar dosyası. Hello Azure Site Recovery abonelik hello kasa adı belirtin ve hello Hyper-V site toowhich hello Hyper-V sunucusuna ait.

    ![Sunucu kaydı](./media/site-recovery-hyper-v-site-to-azure-classic/provider8.PNG)
9. Merhaba üzerinde **Internet bağlantısı** sayfası hello sağlayıcısı tooAzure Site Recovery nasıl bağlandığını belirtin. Seçin **varsayılan sistem Ara sunucu ayarlarını kullan** hello sunucusunda yapılandırılan toouse hello varsayılan Internet bağlantısı ayarları. Bir değer hello varsayılan ayarlar kullanılır belirtmezseniz.

   ![İnternet Ayarları](./media/site-recovery-hyper-v-site-to-azure-classic/provider7.PNG)
10. Kayıt tooregister hello sunucu hello kasasına başlar.

    ![Sunucu kaydı](./media/site-recovery-hyper-v-site-to-azure-classic/provider15.PNG)
11. Meta veri kayıt tamamlandıktan sonra hello ' Hyper-V server Azure Site Recovery tarafından alınır ve hello sunucu üzerinde hello görüntülenen **Hyper-V sitelerini** hello sekmesinde **sunucuları** hello kasası sayfasında.

### <a name="install-hello-provider-from-hello-command-line"></a>Merhaba sağlayıcısı hello komut isteminden yükleme
Alternatif olarak, hello Azure Site Recovery sağlayıcısı hello komut satırından yükleyebilirsiniz. Windows 2012 R2 Sunucu Çekirdeği çalıştıran bir bilgisayarda tooinstall hello sağlayıcısı istiyorsanız, bu yöntem kullanmanız gerekir. Merhaba komut satırından aşağıdaki gibi çalıştırın:

1. Merhaba sağlayıcısı yükleme dosyasını ve kayıt anahtarı tooa klasörü indirin. Örneğin, C:\ASR.
2. Bir komut istemi, bir yönetici ve türü olarak çalıştırın:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Ardından hello sağlayıcısı çalıştırarak yükleyin:

        C:\ASR> setupdr.exe /i
4. Toocomplete kayıt aşağıdaki hello çalıştırın:

        CD C:\Program Files\Microsoft Azure Site Recovery Provider
        C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Parametreler burada şunları içerir:

* **/ Credentials**: hello kayıt anahtarı indirdiğiniz hello konumunu belirtin.
* **/ FriendlyName**: bir ad tooidentify hello Hyper-V konak sunucusu belirtin. Bu ad hello Portalı'nda görünür
* **/ EncryptionEnabled**: isteğe bağlı. Tooencrypt çoğaltma sanal makineleri azure'da (Bekleyen şifreleme) isteyip istemediğinizi belirtin.
* **/ proxyaddress**; **/proxyport**; **/proxyusername**; **/proxypassword**: isteğe bağlı. Toouse özel bir ara sunucu istiyorsanız veya var olan ara sunucunuz kimlik doğrulaması gerektiren proxy parametrelerini belirtin.

## <a name="step-4-create-an-azure-storage-account"></a>4. Adım: Azure depolama hesabı oluşturma
* İçinde **kaynakları hazırla** seçin **depolama hesabı oluştur** toocreate, yoksa, Azure depolama hesabı. Merhaba hesabı coğrafi çoğaltmanın etkinleştirilmiş olması gerekir. Merhaba hello Azure Site kurtarma kasasıyla aynı bölgede ve ile ilişkili olmalıdır hello aynı abonelik.

    ![Depolama hesabı oluşturma](./media/site-recovery-hyper-v-site-to-azure-classic/create-resources.png)

> [!NOTE]
> 1. Merhaba taşıma hello kullanılarak oluşturulan depolama hesaplarının desteklemiyoruz [yeni Azure portalına](../storage/common/storage-create-storage-account.md) kaynak grupları arasında.
> 2. [Geçiş depolama hesaplarının](../azure-resource-manager/resource-group-move-resources.md) kaynak arasında grupları içinde hello aynı abonelik veya abonelikler arasında Site Recovery dağıtmak için kullanılan depolama hesapları için desteklenmez.
>

## <a name="step-5-create-and-configure-protection-groups"></a>Adım 5: Oluşturma ve koruma gruplarını yapılandırma
Koruma grupları mantıksal gruplandırmaları olan istediğiniz sanal makinelerin aynı koruma ayarlarını hello tooprotect kullanarak. Koruma ayarlarını tooa koruma grubu uygulanır ve bu ayarları uygulanan tooall sanal toohello grubu Ekle makinelerdir.

1. İçinde **oluşturma ve koruma gruplarını yapılandırma** tıklatın **koruma grubu oluşturma**. Tüm Önkoşullar yerinde yoksa bir ileti verilir ve tıklayabilirsiniz **ayrıntıları görüntüleyin** daha fazla bilgi için.
2. Merhaba, **koruma grupları** sekmesinde, bir koruma grubu ekleyin. Bir ad, hello kaynak Hyper-V sitesi, hello hedef belirtin **Azure**, Azure Site Recovery abonelik adı ve hello Azure depolama hesabı.

    ![Koruma grubu](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group.png)
3. İçinde **çoğaltma ayarları** kümesi hello **kopyalama sıklığı** toospecify hello veri değişim eşitlenmesi gerektiğini hello kaynak ve hedef arasında ne sıklıkta. Too30 saniye, 5 dakika veya 15 dakika ayarlayabilirsiniz.
4. İçinde **kurtarma noktalarını korumak** kurtarma geçmişini kaç saat saklanması gerektiğini belirtin.
5. İçinde **uygulamayla tutarlı anlık görüntü sıklığı** tootake anlık görüntüler, hello anlık görüntü alınırken uygulamaların tutarlı bir durumda olan birim gölge kopyası hizmeti (VSS) tooensure kullanıp kullanmayacağınızı belirtin. Varsayılan olarak bu gerçekleştirilecek değil. Bu değer, yapılandırdığınız ilave kurtarma noktası hello sayısından tooless ayarlandığından emin olun. Merhaba sanal makineyi bir Windows işletim sistemi çalıştırıyorsa, bu yalnızca desteklenir.
6. İçinde **ilk çoğaltma başlangıç zamanı** hello koruma grubundaki sanal makinelerin ilk çoğaltmasının tooAzure ne zaman gönderilmesi gerektiğini belirtin.

    ![Koruma grubu](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group2.png)

## <a name="step-6-enable-virtual-machine-protection"></a>6. adım: sanal makine korumayı etkinleştirin
Sanal makineler tooa koruma grubu tooenable koruma bunları ekleyin.

> [!NOTE]
> Statik bir IP adresiyle Linux çalıştıran VM'leri koruma işlemi desteklenmez.
>
>

1. Merhaba üzerinde **makineler** hello koruma grubunun tıklatın ** Ekle sanal makineleri tooprotection sekmesinde grupları tooenable koruma **.
2. Merhaba üzerinde **sanal makine korumayı etkinleştir** sayfasında tooprotect istediğiniz select hello sanal makineler.

    ![Sanal makine korumasını etkinleştirme](./media/site-recovery-hyper-v-site-to-azure-classic/add-vm.png)

    Merhaba korumayı etkinleştir işleri başlar. Merhaba üzerinde ilerleme durumunu izleyebilirsiniz **işleri** sekmesi. Sonra Hello korumayı Sonlandır işini çalıştırır hello sanal makine yük devretme için hazırdır.
3. Sonra koruma olduğundan, ayarlama yapabilirsiniz:

   * Sanal makinelerde görüntülemek **korunan öğeler** > **koruma grupları** > *protectiongroup_name*  >  **Sanal makineleri** hello toomachine ayrıntılarında ayrıntıya girebilirsiniz **özellikleri** sekmesini..
   * Sanal makinelerinizde Hello yük devretme özelliklerini yapılandırın **korunan öğeler** > **koruma grupları** > *protectiongroup_name*  >  **Sanal makineleri** *virtual_machine_name* > **yapılandırma**. Aşağıdakileri yapılandırabilirsiniz:

     * **Ad**: hello sanal makine azure'da hello adı.
     * **Boyutu**: Merhaba yöneltilir hello sanal makinenin hedef boyutu.

       ![Sanal makine özelliklerini yapılandırın](./media/site-recovery-hyper-v-site-to-azure-classic/vm-properties.png)
   * Ek sanal makine ayarlarında yapılandırdığınız *korunan öğeler** > **koruma grupları** > *protectiongroup_name* > **sanal makineleri** *virtual_machine_name* > **yapılandırma**dahil:

     * **Ağ bağdaştırıcıları**: hello hedef sanal makine için belirttiğiniz hello boyutuna göre ağ bağdaştırıcısı hello sayısını belirler. Denetleme [sanal makine boyutu özellikleri](../virtual-machines/linux/sizes.md) hello sanal makine boyutu tarafından desteklenen NIC'ler hello sayısı.

       Bir sanal makine için başlangıç boyutu değiştirmek ve hello ayarları kaydettiğinizde, açtığınızda hello ağ bağdaştırıcısı sayısı değişir **yapılandırma** sayfa hello sonraki saat. Merhaba, hedef sanal makinelerin ağ bağdaştırıcısı hello kaynak sanal makinedeki ağ bağdaştırıcısı sayısını ve seçilen hello sanal makine hello boyutu tarafından desteklenen ağ bağdaştırıcısı sayısı en düşük sayısıdır. Aşağıda açıklanan:

       * Merhaba hello kaynak makinedeki ağ bağdaştırıcısı sayısı küçük veya buna eşit ise toohello bağdaştırıcı sayısı hello hedef makine boyutu için izin verilen sonra hello hedef olacaktır hello aynı sayıda bağdaştırıcıya hello kaynağı olarak.
       * Merhaba hello kaynak sanal makinenin bağdaştırıcı sayısı hello hedef boyutu sonra hello maksimum hedef boyutu kullanılır için izin verilen hello sayıyı aşarsa.
       * Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hello hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa, hello hedef makinenin iki bağdaştırıcısı gerekir. Merhaba kaynak makinenin iki bağdaştırıcısı varsa, ancak hello hedef boyut yalnızca bir destekler hello hedef makine yalnızca bir bağdaştırıcısı olur.

     * **Azure ağı**: hello ağ toowhich hello sanal makine yük üzerinden belirtin. Tüm bağdaştırıcıları Hello sanal makinede birden çok ağ bağdaştırıcısı varsa bağlı toohello gereken aynı Azure ağı.
     * **Alt ağ** hello sanal makinedeki her ağ bağdaştırıcısı için select hello alt hello Azure ağ toowhich hello makinede yük devretme sonrasında bağlanmanız gerekir.
     * **Hedef IP adresi**: hello ağ bağdaştırıcısı kaynak sanal makinenin yapılandırılmış toouse statik ise bir IP adresi için makine hello hello hedef sanal makine tooensure hello hello IP adresini belirtebilirsiniz sonra Yük devretme sonrasında aynı IP adresi .  Bir IP adresi belirtmezseniz herhangi bir kullanılabilir adresi yük devretme hello aynı anda atanır. Kullanımda olan bir adresi belirtirseniz, yük devretme başarısız olur.

     > [!NOTE]
     > [Geçiş ağların](../azure-resource-manager/resource-group-move-resources.md) kaynak arasında grupları içinde hello aynı abonelik veya abonelikler arasında Site Recovery dağıtmak için kullanılan ağlar için desteklenmez.
     >

     ![Sanal makine özelliklerini yapılandırın](./media/site-recovery-hyper-v-site-to-azure-classic/multiple-nic.png)




## <a name="step-7-create-a-recovery-plan"></a>7. adım: bir kurtarma planı oluşturma
Sipariş tootest hello dağıtımında, bir yük devretme sınaması için tek bir sanal makine ya da bir veya daha fazla sanal makine içeren bir kurtarma planı çalıştırabilirsiniz. [Daha fazla bilgi edinin](site-recovery-create-recovery-plans.md) bir kurtarma planı oluşturma hakkında daha fazla.

## <a name="step-8-test-hello-deployment"></a>8. adım: Test hello dağıtımı
Bir test yük devretme tooAzure iki yolu toorun vardır.

* **Azure ağı olmadan yük devretme sınamasını**— bu türdeki yük devretme testi hello sanal makinenin gelir doğru Azure'da denetler. Merhaba sanal makine yük devretme sonrasında bağlı tooany Azure ağ olmayacaktır.
* **Azure ağıyla yük devretme testi**— tüm çoğaltma ortamının hello yük devretme denetimleri bu tür istendiği şekilde alınıp ve hello sanal makineler üzerinde başarısız toohello belirtilen hedef Azure ağını bağlanır. Yük devretme sınaması için hello alt hello sınama sanal makinesinin hello çoğaltma sanal makinesi hello alt ağa datalı belirlenir olduğunu unutmayın. Bir çoğaltma sanal makinesi Hello alt hello kaynak sanal makine hello alt ağda alıyorsa, farklı tooregular çoğaltma budur.

Bir Azure ağı belirtmeden toorun yük devretme testi istiyorsanız tooprepare herhangi bir şey gerekmez.

toorun yük devretme testi ile hedef Azure ağını Azure üretim ağınızdan (Azure'da yeni bir ağ oluştururken, varsayılan davranıştır) toocreate yalıtılmış olan yeni bir Azure ağı gerekir. Okuma [bir yük devretme testi](site-recovery-failover.md) daha fazla ayrıntı için.

toofully test, çoğaltma ve ağ dağıtımınızın beklendiği gibi sanal makine toowork bu hello çoğaltılan şekilde hello altyapı yukarı tooset gerekir. DNS etki alanı denetleyicisi olarak tek yönlü bir sanal makineyi bu tootooset yapılması ve Site Recovery toocreate hello test içindeki Ağ Yük devretme testi çalıştırarak kullanarak tooAzure çoğaltmak.  [Daha fazla bilgi](site-recovery-active-directory.md#test-failover-considerations) Active Directory için test yük devretme konusunda.

Yük devretme testi Hello aşağıdaki gibi çalıştırın:

> [!NOTE]
> bir yük devretme tooAzure yaptığınızda tooget hello en iyi performansı elde etmek korumalı hello makinede yüklü hello Azure Aracısı. Bu işlem, daha hızlı önyükleme yapılmasına ve sorunların meydana gelmesi durumunda tanılama işlemine yardımcı olur. Linux aracısına [buradan](https://github.com/Azure/WALinuxAgent) ve Windows aracısına da [buradan](http://go.microsoft.com/fwlink/?LinkID=394789) ulaşabilirsiniz.
>
>

1. Merhaba üzerinde **kurtarma planları** sekmesinde, seçin hello planı ve tıklatın **yük devretme testi**.
2. Merhaba üzerinde **onaylayın yük devretme testi** sayfasında **hiçbiri** veya özel Azure ağı.  Seçerseniz unutmayın **hiçbiri** hello yük devretme testi hello sanal makinenin doğru tooAzure çoğaltılan ancak çoğaltma ağı yapılandırmasını denetlemez denetler.

    ![Yük devretme sınaması](./media/site-recovery-hyper-v-site-to-azure-classic/test-nonetwork.png)
3. Merhaba üzerinde **işleri** sekmesini yük devretme işleminin ilerleyişini izleyebilirsiniz. Ayrıca, mümkün toosee hello sanal makinenin test çoğaltmasını hello Azure portal olmalıdır. Şirket içi ağınızdan tooaccess sanal makineleri ayarladıysanız, bir Uzak Masaüstü Bağlantısı toohello sanal makineyi başlatabilirsiniz.
4. Merhaba yük devretme hello ulaştığında **testi Tamamla** aşama, tıklatın **testi Tamamla** toofinish hello yük devretme testi ayarlama. Toohello inebilir **iş** tootrack yük devretme işleminin ilerleyişini durumunu ve tooperform gerekli olan herhangi bir eylem sekmesi.
5. Yük devretme sonrasında mümkün toosee hello sanal makinenin test çoğaltmasını hello Azure portal olması. Şirket içi ağınızdan tooaccess sanal makineleri ayarladıysanız, bir Uzak Masaüstü Bağlantısı toohello sanal makineyi başlatabilirsiniz.

   1. Merhaba sanal makineler başarıyla başlatıldığını doğrulayın.
   2. Hello yük devretme sonrasında Uzak Masaüstü'nü kullanarak azure'daki tooconnect toohello sanal makine istiyorsanız, Uzak Masaüstü Bağlantısı hello test yük devretmesi çalıştırmadan önce hello sanal makinesinde etkinleştirin. Tooadd hello sanal makinede bir RDP uç noktası de gerekir. Yararlanabileceğiniz bir [Azure Otomasyonu runbook'u](site-recovery-runbook-automation.md) toodo.
   3. Uzak Masaüstü'nü kullanarak Azure'da bir ortak IP adresi tooconnect toohello sanal makine kullanırsanız, yük devretme emin olduktan sonra genel bir adres kullanarak tooa sanal makineye bağlanmanızı engelleyecek etki alanı ilkelerine sahip değilsiniz.
6. Merhaba sınama tamamlandıktan sonra aşağıdaki hello:

   * Tıklatın **hello test yük devretme tamamlandığında**. Merhaba temizleme ortamı tooautomatically güç kapalı test edin ve hello test sanal makineleri silin.
   * Tıklatın **notları** toorecord ve hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek.
7. Merhaba yük devretme hello ulaştığında **testi Tamamla** aşaması son hello doğrulama gibi:
   1. Merhaba çoğaltma sanal makinesi hello Azure portalında görüntüleyin. Merhaba sanal makinenin başarıyla başlatır doğrulayın.
   2. Şirket içi ağınızdan tooaccess sanal makineleri ayarladıysanız, bir Uzak Masaüstü Bağlantısı toohello sanal makineyi başlatabilirsiniz.
   3. Tıklatın **tam hello test** toofinish onu.
   4. Tıklatın **notları** toorecord ve hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek.
   5. Tıklatın **hello test yük devretme tamamlandığında**. Merhaba temizleme ortamı tooautomatically güç kapalı test ve hello test sanal makinesi silin.

## <a name="next-steps"></a>Sonraki adımlar
Dağıtımınız ayarlandıktan ve çalışmaya başladıktan sonra yük devretme hakkında [daha fazla bilgi edinebilirsiniz](site-recovery-failover.md).
