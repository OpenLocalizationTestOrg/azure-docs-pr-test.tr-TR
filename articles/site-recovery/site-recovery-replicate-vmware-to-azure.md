---
title: "Uygulamaları (VMware tooAzure) çoğaltmak | Microsoft Docs"
description: "Çalışan nasıl tooset çoğaltma, sanal makineleri bu makalede Azure içine VMware üzerinde."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: asgang
ms.openlocfilehash: b07aabdacec521c7bd89e50f6a1427a774ff0287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-applications-running-on-vmware-vms-tooazure"></a>VMware Vm'leri tooAzure üzerinde çalışan uygulamalar Çoğalt



Çalışan nasıl tooset çoğaltma, sanal makineleri bu makalede Azure içine VMware üzerinde.
## <a name="prerequisites"></a>Ön koşullar

Merhaba makale zaten sahip olduğunuz varsayılmaktadır.

1.  [Şirket içi kaynak ortamı Kurulumu](site-recovery-set-up-vmware-to-azure.md)
2.  [Azure hedef ortamda Kurulumu](site-recovery-prepare-target-vmware-to-azure.md)


## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme
#### <a name="before-you-start"></a>Başlamadan önce
VMware sanal makineleri çoğaltırken dikkat edin:

* Azure kullanıcı hesabınızın toohave belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) yeni bir sanal makine tooAzure tooenable çoğaltması.
* VMware Vm'lerini her 15 dakikada bulunur. 15 dakika alabilir veya onlar için daha uzun bulma sonrasında hello portalında tooappear. Benzer şekilde, yeni bir vCenter sunucusu veya vSphere ana eklediğinizde, bulma 15 dakika veya daha fazla sürebilir.
* Ortam değişiklikleri (örneğin, VMware araçları yükleme) hello sanal makinede, 15 dakika veya daha fazla toobe hello Portalı'nda güncelleştirilmiş alabilir.
* Merhaba en son bulunan zaman VMware Vm'leri için hello denetleyebilirsiniz **en son kişi** hello üzerinde hello vCenter sunucusu/vSphere sunucusu için alan **yapılandırma sunucularına** dikey.
* tooadd makineleri hello zamanlanmış bulma beklemeden çoğaltma için vurgulayın hello yapılandırma sunucusu (tıklatın yok), hello tıklatıp **yenileme** düğmesi.
* Merhaba makine hazır değilse çoğaltmayı etkinleştirdiğinizde, hello işlem sunucusu üzerinde hello Mobility hizmeti otomatik olarak yükler.


**Şimdi şekilde çoğaltmayı etkinleştirin**:

1. **2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın. Hello için çoğaltma ilk kez etkinleştirdikten sonra tıklayın **+ Çoğalt** hello kasa tooenable çoğaltma ilave makineler için.
2. Merhaba, **kaynak** dikey > **kaynak**seçin hello yapılandırma sunucusu.
3. İçinde **makine türü**seçin **sanal makineleri** veya **fiziksel makineleri**.
4. İçinde **vCenter/vSphere hiper yönetici**hello vSphere ana yöneten hello vCenter sunucusu seçin veya hello konak seçin. Bu ayar fiziksel makineleri çoğaltma yapıyorsanız geçerli değildir.
5. Merhaba işlem sunucusunu seçin. Herhangi bir ek işlem sunucusu oluşturmadıysanız bu hello yapılandırma sunucusunun hello adı olacaktır. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. İçinde **hedef** hello abonelik ve devredilen sanal makinelerin toocreate hello istediğiniz hello kaynak grubu seçin. Toouse (Klasik veya resource management) azure'da hello devredilen sanal makinelerin istediğiniz hello dağıtım modelini seçin.
7. Veri çoğaltmak için toouse istediğiniz hello Azure depolama hesabı seçin. Şunlara dikkat edin:

   * Premium ya da standart depolama hesabı seçebilirsiniz. Premium hesabı seçerseniz, devam eden çoğaltma günlükleri için toospecify ek standart depolama hesabı gerekir. Hesapları hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası.
   * Toouse sahip farklı bir depolama hesabı olandan istiyorsanız bir oluşturabilirsiniz*yer tutucu kullanmaya başlama ele alınacak Yöneticisi kaynak kullanarak depolama hesabı oluşturmak için bağlantı*. toocreate Kaynak Yöneticisi'ni kullanarak bir depolama hesabını tıklatın **Yeni Oluştur**. Merhaba Klasik modeli kullanarak bir depolama hesabı toocreate istiyorsanız, bunu [hello Azure portal'ın](../storage/common/storage-create-storage-account.md).

8. Bunlar yukarı yük devretme sonrasında başlayan select hello Azure ağ ve alt ağ toowhich Azure VM'ler bağlanır. Merhaba ağ hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası. Seçin **seçili makineler için Şimdi Yapılandır**, seçtiğiniz tooapply hello ağ ayarı tooall makineler için koruma. Seçin **daha sonra yapılandırma** tooselect hello makine başına Azure ağı. Bir ağ yoksa, çok ihtiyacınız[oluşturmak](#set-up-an-azure-network). toocreate Kaynak Yöneticisi'ni kullanarak bir ağ tıklatın **Yeni Oluştur**. Merhaba Klasik modeli kullanarak bir ağ toocreate istiyorsanız, bunu [hello Azure portal'ın](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Bir alt ağ (varsa) seçin. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. İçinde **sanal makineleri** > **sanal makine Seç**, tıklatın ve tooreplicate istediğiniz her bir makine seçin. Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. İçinde **özellikleri** > **özelliklerini yapılandırmak**seçin hello işlem sunucusu tooautomatically tarafından kullanılacak hello hesap hello makinede hello Mobility hizmeti yükleyin.  
11. Varsayılan olarak tüm diskler çoğaltılır. Çoğaltma tooexclude diskleri tıklatın **tüm diskleri** ve tooreplicate istemediğiniz tüm diskleri temizleyin.  Daha sonra, **Tamam**'a tıklayın. Daha sonra ek özellikleri ayarlayabilirsiniz. [Daha fazla bilgi edinin](site-recovery-exclude-disk.md) diskleri hariç hakkında.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, o hello çoğaltma ilkesi seçili doğru doğrulayın. Çoğaltma İlkesi ayarlarında değişiklik yapabilirsiniz **ayarları** > **çoğaltma ilkeleri** > ilke adı > **ayarlarını Düzenle**. Değişiklikleri tooa İlkesi Uygula uygulanan tooreplicating ve yeni makineler olacaktır.
13. Etkinleştirme **çoklu VM tutarlılığını** toogather makineler çoğaltma grubuna isterseniz ve hello grubu için bir ad belirtin. Daha sonra, **Tamam**'a tıklayın. Şunlara dikkat edin:

    * Çoğaltma makinelerin çoğaltılacağı gruplamak ve üzerinden başarısız olduğunda kilitlenme tutarlı ve uygulamayla tutarlı kurtarma noktaları paylaşılan.
    * Böylece, iş yüklerini yansıtma sanal makineleri ve fiziksel sunucuları araya toplamak öneririz. Çoklu VM tutarlılığını etkinleştirmek iş yükü performansını etkileyebilir ve yalnızca makineler hello çalışıyorsa kullanılmalıdır aynı iş yükünü ve tutarlılık gerekir.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. Tıklatın **çoğaltmasını etkinleştir**. Merhaba ilerlemesini izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**. Merhaba sonra **korumayı Sonlandır** iş çalıştırmaları hello makine yük devretme için hazır.

> [!NOTE]
> Ne zaman Hello makine anında yükleme hello Mobility hizmeti bileşeninin yüklü hazırlanır koruma etkinleştirilir. Merhaba sonra bileşen yüklenir hello makine koruma işini başlatır ve başarısız olur. Merhaba hatasından sonra toomanually gereksinim duyduğunuz her makineyi yeniden başlatın. Merhaba yeniden hello koruma sonra işi yeniden başlar ve ilk çoğaltma gerçekleştirilir.
>
>

## <a name="view-and-manage-vm-properties"></a>VM özelliklerini görüntüleme ve yönetme

Merhaba hello kaynak makinenin özelliklerini doğrulamanızı öneririz. Bu hello Azure VM adı ile uygun olması unutmayın [Azure sanal makine gereksinimlerini](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. Tıklatın **ayarları** > **öğeleri çoğaltılan** > ve select hello makine. Merhaba **Essentials** dikey makineler ayarlarını ve durumu hakkında bilgileri gösterir.
2. İçinde **özellikleri**, çoğaltma görebilirsiniz ve Yük Devretme bilgilerini hello VM.
3. İçinde **işlem ve ağ** > **işlem özellikleri**, hello Azure VM adını ve hedef boyutu belirtebilirsiniz. Gerekirse hello adı toocomply Azure gereksinimleri ile değiştirin.
    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/VMProperties_AVSET.png)
 
4.  Seçebileceğiniz bir [kaynak grubu](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) devri hangi makineye post parçası olur. Üzerinden bu başarısız önce herhangi bir zamanda ayarı değiştirebilirsiniz. POST devredilir, makinenin koruma ayarlarını kesintiye uğrar sonra hello makine tooa farklı bir kaynak grubu geçirirseniz.
5. Seçebileceğiniz bir [kullanılabilirlik kümesi](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) makinenizi toobe bir post parçası olması gerekiyorsa devredin. Seçme kullanılabilirlik kümesi karşın, lütfen unutmayın:

    * Belirtilen ait toohello kullanılabilirlik kümeleri yalnızca kaynak grubu listelenir  
    * Farklı sanal ağlar makinelerle aynı kullanılabilirlik kümesinin bir parçası olamaz
    * Yalnızca sanal makineler aynı boyutta aynı kullanılabilirlik kümesinin bir parçası olabilir.
5. Ayrıca, görüntülemek ve hello hedef ağ, alt ağ ve toohello Azure VM atanacak IP adresi hakkında bilgi ekleyebilirsiniz.
6. İçinde **diskleri**, hello işletim sistemi görebilir ve veri disklerde hello çoğaltılır VM.

### <a name="network-adapters-and-ip-addressing"></a>Ağ bağdaştırıcılarını ve IP adresleme 

- Merhaba hedef IP adresini ayarlayabilirsiniz. Bir adresi sağlamazsanız, yükü devredilen makine üzerinde hello DHCP kullanır. Yük devretmede kullanılamayan bir adres ayarlarsanız hello yük devretme çalışmaz. Merhaba hello test yük devretme ağı testinde Hello adresi varsa, yük devretme sınaması için aynı hedef IP adresi kullanılabilir.
- ağ bağdaştırıcısı Hello sayısını hello hedef sanal makine için aşağıdaki gibi belirtin hello boyuta göre dikte edilir:
    - Merhaba hello kaynak makinedeki ağ bağdaştırıcısı sayısı küçük veya buna eşit ise toohello bağdaştırıcı sayısı hello hedef makine boyutu için izin verilen sonra hello hedef olacaktır hello aynı sayıda bağdaştırıcıya hello kaynağı olarak.
    - Merhaba hello kaynak sanal makinenin bağdaştırıcı sayısı hello hedef boyutu sonra hello maksimum hedef boyutu kullanılır için izin verilen hello sayıyı aşarsa.
    - Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hello hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa, hello hedef makinenin iki bağdaştırıcısı gerekir. Merhaba kaynak makinenin iki bağdaştırıcısı varsa, ancak hello hedef boyut yalnızca bir destekler hello hedef makine yalnızca bir bağdaştırıcısı olur.
    - Merhaba sanal makinede birden fazla ağ bağdaştırıcısı varsa bunların tümü toohello bağlanır aynı ağ.
    - Merhaba sanal makine birden çok ağ bağdaştırıcısı hello varsa, önce bir hello listede gösterilen hello haline gelir *varsayılan* hello Azure sanal makine ağ bağdaştırıcısı.
   



## <a name="common-issues"></a>Genel sorunlar

* Her disk boyutu 1 TB değerinden küçük olmalıdır.
* Merhaba işletim sistemi disk temel disk ve olmayan dinamik disk olması gerekir
* Sanal makineler oluşturma 2/UEFI etkin için Windows hello işletim sistemi ailesi olmalıdır ve önyükleme diski 300 GB daha az olmalıdır

## <a name="next-steps"></a>Sonraki adımlar

Merhaba koruma tamamlandıktan sonra deneyebilirsiniz [yük devri](site-recovery-failover.md) toocheck olup uygulamanızı Azure'da veya gelir.

Toodisable koruma olasılığına nasıl çok denetleyin[kayıt ve koruma ayarlarını temizleme](site-recovery-manage-registration-and-protection.md)
