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
ms.date: 09/29/2017
ms.author: asgang
ms.openlocfilehash: 028aa0f23c3a7c98c4801d9e306c5dcfa35aab80
ms.sourcegitcommit: 2d1153d625a7318d7b12a6493f5a2122a16052e0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/20/2017
---
# <a name="replicate-applications-running-on-vmware-virtual-machines-to-azure"></a>Azure için VMware sanal makinelerde çalışan uygulamaların Çoğalt



Bu makalede, Azure'da VMware üzerinden çalışan sanal makineler (VM'ler) çoğaltmasını ayarlama açıklar.
## <a name="prerequisites"></a>Ön koşullar

Bu makalede, sahip olduğunuz varsayılmaktadır:

1.  [Şirket içi kaynak ortamını ayarlama](site-recovery-set-up-vmware-to-azure.md).
2.  [Azure hedef ortamda ayarlama](site-recovery-prepare-target-vmware-to-azure.md).


## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme
### <a name="before-you-start"></a>Başlamadan önce
VMware sanal makineleri çoğaltırken:

* Azure kullanıcı hesabınızın belirli sahip olması [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) yeni bir sanal makineye Azure çoğaltmayı etkinleştirmek için.
* VMware Vm'lerini her 15 dakikada bulunur. 15 dakika alabilir veya bunları bulmadan sonra Azure Portalı'nda görünmesi için daha uzun. Benzer şekilde, yeni bir vCenter sunucusu veya vSphere ana eklediğinizde bulma 15 dakika veya daha fazla sürebilir.
* Ortam değişiklikleri (örneğin, VMware araçları yükleme) sanal makinedeki 15 dakika veya portalda güncelleştirilmesi daha fazla sürebilir.
* VMware Vm'leri için son keşfedilen zamanı kontrol edebilirsiniz **en son kişi** vCenter sunucusu/vSphere sunucusu için alan **yapılandırma sunucularına** sayfası.
* Makineler için zamanlanmış bulma beklemeden çoğaltmayı eklemek için yapılandırma sunucusu vurgulayın (tıklatın yok), tıklatıp **yenileme** düğmesi.
* Makine hazır değilse çoğaltmayı etkinleştirdiğinizde, işlem sunucusu üzerinde Mobility hizmeti otomatik olarak yükler.


### <a name="enable-replication-as-follows"></a>Şekilde çoğaltmayı etkinleştirin

1. **2. Adım: Uygulama çoğaltma** > **Kaynak** seçeneklerine tıklayın. Çoğaltmayı ilk kez etkinleştirdikten sonra ek makineler için çoğaltma işlemini etkinleştirmek istiyorsanız kasada **+Çoğalt**'a tıklayın.
2. İçinde **kaynak** sayfa > **kaynak**, yapılandırma sunucusu seçin.
3. İçinde **makine türü**seçin **sanal makineleri** veya **fiziksel makineleri**.
4. İçinde **vCenter/vSphere hiper yönetici**vSphere ana yöneten vCenter sunucusu seçin veya konağı seçin. Bu ayar fiziksel makineleri çoğaltma yapıyorsanız geçerli değildir.
5. Yapılandırma sunucusunun adı herhangi bir ek işlem sunucusu oluşturmadıysanız olacağı işlem sunucusunu seçin. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltma kaynağı etkinleştir](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. İçinde **hedef**, abonelik ve başarısız üzerinden sanal makineler oluşturmak istediğiniz kaynak grubunu seçin. Azure (Klasik veya Azure Resource Manager) başarısız oldu üzerinden sanal makineler için kullanmak istediğiniz dağıtım modelini seçin.

7. Veri çoğaltmak için kullanmak istediğiniz Azure depolama hesabı seçin. 

    > [!NOTE]

    >   * Premium ya da standart depolama hesabı seçebilirsiniz. Premium hesabı seçerseniz, devam eden çoğaltma günlükleri için ek bir standart depolama hesabı belirtmeniz gerekir. Hesapları kurtarma Hizmetleri kasasıyla aynı bölgede olması gerekir.
    >   * Farklı bir depolama hesabı kullanmak istiyorsanız, şunları yapabilirsiniz [oluşturmak](../storage/common/storage-create-storage-account.md). Kaynak Yöneticisi'ni kullanarak bir depolama hesabı oluşturmak için tıklatın **Yeni Oluştur**. Klasik modeli kullanarak bir depolama hesabı oluşturmak istiyorsanız, Azure portalında yapın.

8. Yük devretme sonrasında çalışmaya başlayan Azure VM'lerinin bağlanacağı Azure ağını ve alt ağını seçin. Ağın, Kurtarma Hizmetleri kasasıyla aynı bölgede olması gerekir. Koruma için seçtiğiniz tüm makinelere ağ ayarını uygulamak için **Seçili makineler için şimdi yapılandır**’ı seçin. Makineler için Azure ağını ayrı ayrı seçmek için **Daha sonra yapılandır**'ı seçin. Bir ağ yoksa, gerek [oluşturmak](#set-up-an-azure-network). Kaynak Yöneticisi'ni kullanarak bir ağ oluşturmak için tıklatın **Yeni Oluştur**. Klasik modeli kullanarak bir ağ oluşturmak istiyorsanız, bunu [Azure portalında](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Varsa bir alt ağ seçin ve ardından **Tamam**.

    ![Çoğaltma hedefi ayarlarını etkinleştir](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. İçinde **sanal makineleri** > **sanal makine Seç**, çoğaltmak istediğiniz makineleri seçin. Yalnızca çoğaltmanın etkinleştirildiği makineleri seçebilirsiniz. Daha sonra, **Tamam**'a tıklayın.

    ![Çoğaltma select sanal makineleri etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. İçinde **özellikleri** > **özelliklerini yapılandırma**, otomatik olarak makinede mobilite hizmetinin yüklenmesi için işlem sunucusu tarafından kullanılan hesabı seçin.  
11. Varsayılan olarak, tüm diskler çoğaltılır. Diskleri çoğaltmanın dışında tutmak için tıklatın **tüm diskleri** ve çoğaltmak için istemediğiniz tüm diskleri temizleyin.  Daha sonra, **Tamam**'a tıklayın. Daha sonra ek özellikleri ayarlayabilirsiniz. [Daha fazla bilgi edinin](site-recovery-exclude-disk.md) diskleri hariç hakkında.

    ![Etkinleştirme çoğaltma özelliklerini yapılandırma](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. İçinde **çoğaltma ayarları** > **çoğaltma ayarlarını yapılandırın**, doğru Çoğaltma İlkesi'nin seçili olduğunu doğrulayın. Çoğaltma İlkesi ayarlarında değişiklik yapabilirsiniz **ayarları** > **çoğaltma ilkeleri** > (ilke adı) > **ayarlarını Düzenle**. Bir ilke uyguladığınız değişiklikleri de uygulamak için çoğaltma ve yeni makineler.
13. Etkinleştirme **çoklu VM tutarlılığını** makineler çoğaltma grubuna toplamak istiyorsanız. Grup için bir ad belirtin ve ardından **Tamam**. 

    > [!NOTE]

    >    * Çoğaltma grubunda makineleri birlikte çoğaltmak ve bunlar üzerinde başarısız olduğunda kilitlenme tutarlı ve uygulamayla tutarlı kurtarma noktaları paylaşılan.
    >    * Böylece, iş yüklerini yansıtma sanal makineleri ve fiziksel sunucuları birlikte toplayın. Çoklu VM tutarlılığını etkinleştirmek, iş yükü performansını etkileyebilir. Yalnızca makineler aynı iş yükünü çalıştırıyorsa ve tutarlılık ihtiyacınız varsa kullanın.

    ![Çoğaltmayı etkinleştirme](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. Tıklatın **çoğaltmasını etkinleştir**. İlerleme durumunu izleyebilirsiniz **korumayı etkinleştir** iş **ayarları** > **işleri** > **Site Recovery işleri**. **Korumayı Sonlandır** işi çalıştırıldıktan sonra makine yük devretme için hazırdır.

> [!NOTE]
> Makine gönderme yüklemesi için hazırlanmış, koruma etkinleştirildiğinde Mobility hizmeti bileşeninin yüklü. Bileşen makineye yüklendikten sonra bir koruma işi başlatır ve başarısız olur. Hatadan sonra el ile her makinenin yeniden başlatmanız gerekir. Yeniden başlatma işleminden sonra koruma işini yeniden başlar ve ilk çoğaltma gerçekleştirilir.
>
>

## <a name="view-and-manage-vm-properties"></a>VM özelliklerini görüntüleme ve yönetme

Ardından, kaynak makine özelliklerini doğrulayın. Azure VM adının uygun olması gerektiğini unutmayın [Azure sanal makine gereksinimlerini](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. Tıklatın **ayarları** > **öğeleri çoğaltılan** > ve ardından makine seçin. **Essentials** sayfa makine ayarlarını ve durumu hakkında bilgileri gösterir.
2. **Özellikler** kısmında VM'nin çoğaltma ve yük devretme bilgilerini inceleyebilirsiniz.
3. **İşlem ve Ağ** > **İşlem özellikleri** seçeneklerinden Azure VM adını ve hedef boyutu belirtebilirsiniz. Gerekirse, Azure gereksinimlerine uymak için adı değiştirin.

    ![İşlem ve ağ özellikleri](./media/site-recovery-vmware-to-azure/vmproperties.png)

4.  Seçebileceğiniz bir [kaynak grubu](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) gelen olduğu bir makineye post yük devretme parçası haline gelir. Bu yük devretme önce herhangi bir zamanda ayarı değiştirebilirsiniz. Farklı bir kaynak grubu, bu makine sonu için koruma ayarları için makineyi geçirirseniz, yük devretme sonrasında.
5. Seçebileceğiniz bir [kullanılabilirlik kümesi](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) makinenizde bir post yük devretme parçası olması gerekiyorsa. Bir kullanılabilirlik kümesi seçme sırada unutmayın:

    * Yalnızca belirtilen kaynak grubuna ait kullanılabilirlik kümeleri listelenir.  
    * Farklı sanal ağlar makinelerle aynı kullanılabilirlik kümesinin bir parçası olamaz.
    * Yalnızca sanal makineler aynı boyutta bir kullanılabilirlik kümesinin bir parçası olabilir.
5. Ayrıca, görüntülemek ve hedef ağ, alt ağ ve Azure VM'ye atanan IP adresi hakkında bilgi ekleyebilirsiniz.
6. İçinde **diskleri**, VM çoğaltılması için işletim sistemi ve veri disklerini görebilirsiniz.

### <a name="network-adapters-and-ip-addressing"></a>Ağ bağdaştırıcılarını ve IP adresleme

- Hedef IP adresini ayarlayabilirsiniz. Bir adresi sağlamazsanız, başarısız üzerinden makine DHCP kullanır. Yük devretmede kullanılamayan bir adres ayarlarsanız yük devretme işe yaramaz. Test Yük Devretme ağ adresi varsa, aynı hedef IP adresi yük devretme sınaması için kullanılabilir.
- Ağ bağdaştırıcılarının sayısı, hedef sanal makine için sizin belirlediğiniz boyuta göre aşağıdaki gibi belirlenmiştir:
    - Kaynak makinedeki ağ bağdaştırıcıları sayısı, hedef makine boyutu için izin verilen bağdaştırıcıları sayısına eşit veya daha az ise, hedef kaynak olarak aynı sayıda bağdaştırıcıya sahip.
    - Kaynak sanal makinenin bağdaştırıcı sayısı hedef boyut için izin verilen sayıyı aşarsa maksimum hedef boyutu kullanılır.
    Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa hedef makinenin iki bağdaştırıcısı vardır. Kaynak makinenin iki bağdaştırıcısı varken hedef boyut yalnızca bir destekler, hedef makine yalnızca bir bağdaştırıcı bulunur.
    - Sanal makinede birden fazla ağ bağdaştırıcısı varsa, bunların tümü aynı ağa bağlayın. Ayrıca, listedeki ilk gösterilene hale *varsayılan* Azure sanal makine ağ bağdaştırıcısı.

### <a name="azure-hybrid-use-benefit"></a>Azure karma kullanımı avantajı

Microsoft Yazılım Güvencesi müşteriler, Azure'a geçirilir Windows Server makine maliyetlerini lisans kaydetmek veya Azure olağanüstü durum kurtarma için kullanılacak Azure karma kullanma avantajını kullanabilirsiniz. Kullanmak yararlı Azure karma kullanmak uygun değilse, bir yük devretmeyi Azure Site Recovery oluşturur Bu avantajı atanan sanal makine olduğunu belirtebilirsiniz. Bunu yapmak için:
- Çoğaltılan sanal makinenin işlem ve ağ özellikleri bölümüne gidin.
- Azure karma kullanımı avantajı için uygun hale getirir bir Windows Server Lisans olup olmadığını soran soruyu yanıtlayın.
- Yük devretme oluşturulacak makinede karma kullanma avantajını uygulamak için kullanabileceğiniz Yazılım Güvencesi ile uygun bir Windows Server Lisans sahip olduğunuzu onaylamak için bu onay kutusunu seçin.
- Çoğaltılan makinelerin için ayarları kaydedin.

Daha fazla bilgi edinmek [Azure karma kullanımı avantajı](https://aka.ms/azure-hybrid-use-benefit-pricing).

## <a name="common-issues"></a>Genel sorunlar

* Her disk boyutu 1 TB değerinden küçük olmalıdır.
* İşletim sistemi diski temel disk ve dinamik disk olması gerekir.
* Nesil 2/UEFI etkin sanal makineler için Windows işletim sistemi ailesi olmalıdır ve önyükleme diski 300 GB daha az olmalıdır.

## <a name="next-steps"></a>Sonraki adımlar

Koruma tamamlandıktan sonra makineyi korumalı bir duruma ulaştı, deneyebilirsiniz bir [yük devretme](site-recovery-failover.md) uygulamanızı Azure'da veya gelir olup olmadığını denetlemek için.

Koruma devre dışı bırakmak istiyorsanız, bilgi nasıl [kayıt ve koruma ayarlarını Temizleme](site-recovery-manage-registration-and-protection.md).
