---
title: "Uygulamaları (VMware azure'a) çoğaltma | Microsoft Docs"
description: "Bu makalede, Azure'da VMware üzerinden çalışan sanal makinelerin çoğaltmasını ayarlama açıklar."
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
ms.openlocfilehash: e0047a996c9bfd7d950b32f0871ddd7608924b42
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-applications-running-on-vmware-vms-to-azure"></a>Azure'da VMware Vm'lerinde çalışan uygulamalar Çoğalt



Bu makalede, Azure'da VMware üzerinden çalışan sanal makinelerin çoğaltmasını ayarlama açıklar.
## <a name="prerequisites"></a>Ön koşullar

Makaleyi zaten sahip olduğunuz varsayılmaktadır.

1.  [Şirket içi kaynak ortamı Kurulumu](site-recovery-set-up-vmware-to-azure.md)
2.  [Azure hedef ortamda Kurulumu](site-recovery-prepare-target-vmware-to-azure.md)


## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme
#### <a name="before-you-start"></a>Başlamadan önce
VMware sanal makineleri çoğaltırken dikkat edin:

* Azure kullanıcı hesabınızın belirli sahip olması [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) yeni bir sanal makineye Azure çoğaltmayı etkinleştirmek için.
* VMware Vm'lerini her 15 dakikada bulunur. 15 dakika alabilir veya bunları sonra bulma Portalı'nda görünmesi için daha uzun. Benzer şekilde, yeni bir vCenter sunucusu veya vSphere ana eklediğinizde, bulma 15 dakika veya daha fazla sürebilir.
* Ortam değişiklikleri (örneğin, VMware araçları yükleme) sanal makinedeki 15 dakika veya portalda güncelleştirilmesi daha fazla sürebilir.
* VMware Vm'leri için son keşfedilen zamanı denetleyebilirsiniz **en son kişi** vCenter sunucusu/vSphere sunucusu için alan **yapılandırma sunucularına** dikey.
* Makineler için zamanlanmış bulma beklemeden çoğaltmayı eklemek için yapılandırma sunucusu vurgulayın (tıklatın yok), tıklatıp **yenileme** düğmesi.
* Makine hazır değilse çoğaltmayı etkinleştirdiğinizde, işlem sunucusu üzerinde Mobility hizmeti otomatik olarak yükler.


**Şimdi şekilde çoğaltmayı etkinleştirin**:

1. **2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın. Çoğaltmayı ilk kez etkinleştirdikten sonra ek makineler için çoğaltma işlemini etkinleştirmek istiyorsanız kasada **+Çoğalt**'a tıklayın.
2. İçinde **kaynak** dikey > **kaynak**, yapılandırma sunucusu seçin.
3. İçinde **makine türü**seçin **sanal makineleri** veya **fiziksel makineleri**.
4. İçinde **vCenter/vSphere hiper yönetici**vSphere ana yöneten vCenter sunucusu seçin veya konağı seçin. Bu ayar fiziksel makineleri çoğaltma yapıyorsanız geçerli değildir.
5. İşlem sunucusu seçin. Herhangi bir ek işlem sunucusu oluşturmadıysanız bu yapılandırma sunucusunun adı olacaktır. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. İçinde **hedef** abonelik ve başarısız sanal makineler üzerinde oluşturmak istediğiniz kaynak grubunu seçin. Yükü devredilen sanal makineler için Azure’da kullanmak istediğiniz dağıtım modelini (klasik veya kaynak yönetimi) seçin.
7. Veri çoğaltmak için kullanmak istediğiniz Azure depolama hesabı seçin. Şunlara dikkat edin:

   * Premium ya da standart depolama hesabı seçebilirsiniz. Premium hesabı seçerseniz, devam eden çoğaltma günlükleri için ek bir standart depolama hesabı belirtmeniz gerekir. Hesapları kurtarma Hizmetleri kasasıyla aynı bölgede olması gerekir.
   * Sahip olduğunuz farklı bir depolama hesabı olandan kullanmak istiyorsanız, bir oluşturabilirsiniz*yer tutucu kullanmaya başlama ele alınacak Yöneticisi kaynak kullanarak depolama hesabı oluşturmak için bağlantı*. Kaynak Yöneticisi'ni kullanarak bir depolama hesabı oluşturmak için tıklatın **Yeni Oluştur**. Klasik modeli kullanarak bir depolama hesabı oluşturmak istiyorsanız bu işlemi [Azure portalda](../storage/common/storage-create-storage-account.md) gerçekleştirirsiniz.

8. Azure ağı ve bunların yukarı yük devretme sonrasında başlayan Azure Vm'lerinin, bağlanacağı alt ağı seçin. Ağın, Kurtarma Hizmetleri kasasıyla aynı bölgede olması gerekir. Koruma için seçtiğiniz tüm makinelere ağ ayarını uygulamak için **Seçili makineler için şimdi yapılandır**’ı seçin. Makineler için Azure ağını ayrı ayrı seçmek için **Daha sonra yapılandır**'ı seçin. Bir ağ yoksa, gerek [oluşturmak](#set-up-an-azure-network). Kaynak Yöneticisi'ni kullanarak bir ağ oluşturmak için tıklatın **Yeni Oluştur**. Klasik modeli kullanarak bir ağ oluşturmak isterseniz bu işlemi [Azure portalından](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) gerçekleştirin. Bir alt ağ (varsa) seçin. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. **Sanal Makineler** > **Sanal makine seçin** seçeneklerine tıklayın ve çoğaltmak istediğiniz makineleri seçin. Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. İçinde **özellikleri** > **özelliklerini yapılandırma**, işlem sunucusu tarafından otomatik olarak makinede Mobility hizmeti yüklemek için kullanılacak hesabı seçin.  
11. Varsayılan olarak tüm diskler çoğaltılır. Diskleri çoğaltmanın dışında tutmak için tıklatın **tüm diskleri** ve çoğaltmak için istemediğiniz tüm diskleri temizleyin.  Daha sonra, **Tamam**'a tıklayın. Daha sonra ek özellikleri ayarlayabilirsiniz. [Daha fazla bilgi edinin](site-recovery-exclude-disk.md) diskleri hariç hakkında.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, doğru Çoğaltma İlkesi'nin seçili olduğunu doğrulayın. Çoğaltma İlkesi ayarlarında değişiklik yapabilirsiniz **ayarları** > **çoğaltma ilkeleri** > ilke adı > **ayarlarını Düzenle**. Bir ilke uyguladığınız değişiklikler uygulanabilir çoğaltma ve yeni makineler.
13. Etkinleştirme **çoklu VM tutarlılığını** makineler çoğaltma grubuna toplayın ve grup için bir ad belirtmek istiyorsanız. Daha sonra, **Tamam**'a tıklayın. Şunlara dikkat edin:

    * Çoğaltma makinelerin çoğaltılacağı gruplamak ve üzerinden başarısız olduğunda kilitlenme tutarlı ve uygulamayla tutarlı kurtarma noktaları paylaşılan.
    * Böylece, iş yüklerini yansıtma sanal makineleri ve fiziksel sunucuları araya toplamak öneririz. Çoklu VM tutarlılığını etkinleştirmek, iş yükü performansını etkileyebilir ve yalnızca makineler aynı iş yükünü çalıştırıyorsa ve tutarlılık ihtiyacınız varsa kullanılmalıdır.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. Tıklatın **çoğaltmasını etkinleştir**. İlerleme durumunu izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**. **Korumayı Sonlandır** işi çalıştırıldıktan sonra makine yük devretme için hazırdır.

> [!NOTE]
> Makine koruması etkinleştirildiğinde Mobility hizmeti bileşeninin yüklü gönderme yüklemesi için hazırlanmış durumunda. Bileşen sonra koruma işini başlatır makine ve başarısız yüklenir. Hatadan sonra el ile her makinenin yeniden başlatmanız gerekir. Yeniden başladıktan sonra koruma işini yeniden başlar ve ilk çoğaltma gerçekleştirilir.
>
>

## <a name="view-and-manage-vm-properties"></a>VM özelliklerini görüntüleme ve yönetme

Kaynak makinenin özelliklerini doğrulamanızı öneririz. Azure VM adının [Azure sanal makine gereksinimlerini](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) karşılaması gerektiğini unutmayın.

1. Tıklatın **ayarları** > **öğeleri çoğaltılan** > ve makineyi seçin. **Essentials** dikey makineler ayarlarını ve durumu hakkında bilgileri gösterir.
2. **Özellikler** kısmında VM'nin çoğaltma ve yük devretme bilgilerini inceleyebilirsiniz.
3. **İşlem ve Ağ** > **İşlem özellikleri** seçeneklerinden Azure VM adını ve hedef boyutu belirtebilirsiniz. Gerekirse Azure gereksinimlerine uymak için adı değiştirin.
    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/VMProperties_AVSET.png)
 
4.  Seçebileceğiniz bir [kaynak grubu](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) devri hangi makineye post parçası olur. Üzerinden bu başarısız önce herhangi bir zamanda ayarı değiştirebilirsiniz. POST devredilir, makinenin koruma ayarlarını kesintiye uğrar sonra farklı bir kaynak grubu için makineyi geçirirseniz.
5. Seçebileceğiniz bir [kullanılabilirlik kümesi](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) makinenizin olması gereken bir post bir parçası olarak üzerinden başarısız. Seçme kullanılabilirlik kümesi karşın, lütfen unutmayın:

    * Yalnızca belirtilen kaynak grubuna ait kullanılabilirlik kümeleri listelenmez.  
    * Farklı sanal ağlar makinelerle aynı kullanılabilirlik kümesinin bir parçası olamaz
    * Yalnızca sanal makineler aynı boyutta aynı kullanılabilirlik kümesinin bir parçası olabilir.
5. Ayrıca, görüntülemek ve hedef ağ, alt ağ ve Azure VM'ye atanacak IP adresi hakkında bilgi ekleyebilirsiniz.
6. İçinde **diskleri**, çoğaltılacak VM işletim sistemi ve veri disklerini görebilirsiniz.

### <a name="network-adapters-and-ip-addressing"></a>Ağ bağdaştırıcılarını ve IP adresleme 

- Hedef IP adresini ayarlayabilirsiniz. Bir IP adresi sağlamazsanız yük devredilen makine DHCP kullanır. Yük devretmede kullanılamayan bir adres ayarlarsanız yük devretme çalışmaz. Hedef IP adresi, yük devretme ağı testinde kullanılabilirse aynı IP adresi yük devretme sınamasında da kullanılabilir.
- Ağ bağdaştırıcılarının sayısı, hedef sanal makine için sizin belirlediğiniz boyuta göre aşağıdaki gibi belirlenmiştir:
    - Kaynak makinedeki ağ bağdaştırıcılarının sayısı, hedef makine boyutu için verilen ağ bağdaştırıcısı sayısına eşitse veya daha azsa hedef makine kaynakla aynı sayıda bağdaştırıcıya sahip olur.
    - Kaynak sanal makinenin bağdaştırıcı sayısı, hedef boyut için izin verilen sayıyı aşarsa maksimum hedef boyutu kullanılır.
    - Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa hedef makinenin iki bağdaştırıcısı olur. Kaynak makinenin iki bağdaştırıcısı varken hedef boyut yalnızca bir bağdaştırıcıyı destekliyorsa hedef makinenin bir bağdaştırıcısı olur.
    - Sanal makinede birden fazla ağ bağdaştırıcısı varsa bunların tümü aynı ağa bağlanır.
    - Sanal makine birden çok ağ bağdaştırıcısına sahip sonra listede gösterilen birinci hale *varsayılan* Azure sanal makine ağ bağdaştırıcısı.
   



## <a name="common-issues"></a>Genel sorunlar

* Her disk boyutu 1 TB değerinden küçük olmalıdır.
* İşletim sistemi diski, dinamik disk değil temel disk olmalıdır
* 2. nesil/UEFI özellikli sanal makinelerin işletim sistemi Windows olmalıdır ve önyükleme diskinin boyutu 300 GB’tan fazla olmamalıdır

## <a name="next-steps"></a>Sonraki adımlar

Koruma tamamlandıktan sonra deneyebilirsiniz [yük devri](site-recovery-failover.md) uygulamanızı Azure'da veya gelir olup olmadığını denetlemek için.

Koruma devre dışı bırakmak istediğiniz durumda denetleyin nasıl [kayıt ve koruma ayarlarını temizleme](site-recovery-manage-registration-and-protection.md)
