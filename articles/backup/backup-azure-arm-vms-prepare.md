---
title: "Azure yedekleme: sanal makineler yukarı tooback hazırlama | Microsoft Docs"
description: "Azure sanal makineleri yedeklemek için ortamınızı hazır olduğundan emin olun."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: yedeklemeleri; Yedekleme;
ms.assetid: e87e8db2-b4d9-40e1-a481-1aa560c03395
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 5c3a41b5d3bd56e62ca5f207442867913aa99816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-resource-manager-deployed-virtual-machines"></a>Resource Manager tarafından dağıtılan sanal makineleri yedeklemek, ortam tooback hazırlama
> [!div class="op_single_selector"]
> * [Resource Manager modeli](backup-azure-arm-vms-prepare.md)
> * [Klasik modeli](backup-azure-vms-prepare.md)
>
>

Bu makalede, Resource Manager tarafından dağıtılan bir bir sanal makineyi (VM), ortam tooback hazırlamak için hello adımları sağlar. Merhaba hello yordamda gösterildiği adımları hello Azure portalını kullanın.  

Hello Azure Backup hizmeti Vm'lerinizi koruma için kasa (Yedekleme kasaları ve kurtarma Hizmetleri kasaları) iki tür vardır. Bir yedekleme kasası hello Klasik dağıtım modeli kullanılarak dağıtılan VM'ler korur. Bir kurtarma Hizmetleri kasası korur **hem Klasik dağıtılan, hem de Resource Manager tarafından dağıtılan VM'ler**. Kurtarma Hizmetleri kasası tooprotect Resource Manager tarafından dağıtılan VM kullanmanız gerekir.

> [!NOTE]
> Azure'da kaynak oluşturmaya ve kaynaklarla çalışmaya yönelik iki dağıtım modeli mevcuttur: [Resource Manager ve Klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bkz: [Azure sanal makineleri yedeklemek, ortam tooback hazırlama](backup-azure-vms-prepare.md) Klasik dağıtımı ile çalışma hakkında ayrıntılar için model VM'ler.
>
>

Koruyabilir veya bir Resource Manager tarafından dağıtılan sanal makineyi (VM) geri önce şu önkoşulların mevcut olması emin olun:

* Bir kurtarma Hizmetleri kasası oluşturma (veya var olan bir kurtarma Hizmetleri kasası tanımlama) *hello içinde VM ile aynı konumda*.
* Bir senaryo seçmek, hello yedekleme ilkenizi tanımlayın ve öğeleri tooprotect tanımlayın.
* Sanal makine üzerinde VM Aracısı'nın Hello yüklemesini denetleyin.
* Ağ bağlantısını denetleyin
* Linux VM'ler için toocustomize istemeniz durumunda, yedekleme ortamınız uygulama tutarlı yedeklemeler için lütfen izleyin hello [adımları tooconfigure anlık görüntü öncesi ve sonrası betikleri anlık görüntüsünü alın](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)

Bu koşullar zaten ortamınızda mevcut sonra toohello devam biliyorsanız [VM'ler Makalenizi yedekleme](backup-azure-vms.md). Yukarı tooset gerekir ya da, bu Önkoşullar hiçbirini denetleyin Bu makalede, hello adımları tooprepare önkoşul yol açar.

##<a name="supported-operating-system-for-backup"></a>Yedekleme için desteklenen işletim sistemi
 * **Linux**: Azure Backup, [Azure tarafından onaylanan bir dağıtım listesini](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (CoreOS Linux hariç) destekler. _Diğer Getir-bilgisayarınızı-kendi-Linux dağıtımları da hello VM Aracısı hello sanal makinede kullanılabilir olduğu sürece çalışır ve Python var. desteği. Ancak, biz yedekleme için bu dağıtımları desteklemiyorsanız._
 * **Windows Server**:  Windows Server 2008 R2’den eski sürümler desteklenmez.

## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Yedekleme ve geri yükleme VM sınırlamaları
Ortamınızı hazırlama önce lütfen hello sınırlamaları anlayın.

* 16'dan fazla veri diskleri içeren sanal makineleri yedekleme desteklenmiyor.
* Sanal makineler verilerle disk boyutları 1023 GB'den büyük yedekleme desteklenmiyor.
* Ayrılmış bir IP adresi ve tanımlanmış hiçbir uç nokta ile sanal makineleri yedekleme desteklenmiyor.
* Yalnızca BEK kullanılarak şifrelenmiş VM'lerin yedeklenmesi desteklenmez. Linux VM'ler LUKS şifrelemesi kullanılarak şifrelenmiş yedeklemesi desteklenmiyor.
* Dosya sunucusu yapılandırması ölçekte VM'lerin yedekleme önerilmez.
* Yedekleme verilerini bağlı ağ bağlı sürücüler tooVM içermez.
* Geri yükleme sırasında mevcut bir sanal makinenin değiştirilmesi desteklenmez. Merhaba VM mevcut olduğunda toorestore hello VM çalışırsanız hello geri yükleme işlemi başarısız olur.
* Çapraz bölge yedekleme ve geri yükleme desteklenmez.
* Tüm ortak bölgelerde Azure sanal makineleri yedekleyebilirsiniz (Merhaba bkz [denetim listesi](https://azure.microsoft.com/regions/#services) desteklenen bölgeler). Aradığınız hello bölge bugün desteklenmiyorsa, kasa oluşturma sırasında hello açılır listede görünmez.
* Bir etki alanı denetleyicisini geri multi-DC yapılandırmasının bir parçası olan (DC) VM yalnızca PowerShell aracılığıyla desteklenir. Daha fazla bilgi edinin [multi-DC etki alanı denetleyicisini geri](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* Özel ağ yapılandırmaları aşağıdaki hello sahip sanal makineleri geri yüklenmesi yalnızca PowerShell aracılığıyla desteklenir. Merhaba geri yükleme işlemi tamamlandıktan sonra hello hello geri yükleme iş akışı kullanılarak oluşturulan sanal makineleri bu ağ yapılandırmaları UI sahip olmaz. toolearn daha, fazla [geri VM'ler özel ağ yapılandırmaları ile](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Sanal makineler yük dengeleyici yapılandırması (dahili ve harici)
  * Birden çok ayrılmış IP adreslerine sahip sanal makineler
  * Birden çok ağ bağdaştırıcısı ile sanal makineler

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Bir VM için kurtarma hizmetleri kasası oluşturma
Bir kurtarma Hizmetleri kasası hello yedeklemeleri ve zaman içinde oluşturulan kurtarma noktalarını depolayan bir varlıktır. Merhaba kurtarma Hizmetleri kasası ayrıca korumalı hello sanal makinelerle ilişkili hello yedekleme ilkelerini içerir.

Kasa toocreate bir kurtarma Hizmetleri:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba Hub menüsünde **Gözat** ve kaynakları hello listesinde yazın **kurtarma Hizmetleri**. Yazmaya başladığınızda, hello filtreleyecek girişinize bağlı. **Kurtarma Hizmetleri kasası** seçeneğine tıklayın.

    ![Merhaba Gözat düğmesini tıklatın ve kurtarma Hizmetleri yazın. Merhaba kurtarma seçeneği kasa, tooopen hello tıklatın Hizmetleri gördüğünüzde dikey kurtarma Hizmetleri kasası.](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

    Merhaba kurtarma Hizmetleri kasalarının listesi görüntülenir.
3. Merhaba üzerinde **kurtarma Hizmetleri kasaları** menüsünde tıklatın **Ekle**.

    ![Kurtarma Hizmetleri Kasası oluşturma 2. adım](./media/backup-azure-arm-vms-prepare/rs-vault-menu.png)

    Merhaba kurtarma Hizmetleri kasası dikey penceresi açılır tooprovide isteyen bir **adı**, **abonelik**, **kaynak grubu**, ve **konumu**.

    ![Kurtarma Hizmetleri kasası oluşturma 5. adım](./media/backup-azure-arm-vms-prepare/rs-vault-attributes.png)
4. İçin **adı**, bir kolay ad tooidentify hello kasası girin. Merhaba adı toobe hello Azure aboneliği için benzersiz olmalıdır. 2 ila 50 karakterden oluşan bir ad yazın. Ad bir harf ile başlamalıdır ve yalnızca harf, rakam ve kısa çizgi içerebilir.
5. Tıklatın **abonelik** toosee hello kullanılabilir abonelik listesini. Hangi abonelik toouse emin değilseniz, hello varsayılan kullanın (veya önerilen) aboneliği. Ancak kuruluş hesabınızın birden çok Azure aboneliği ile ilişkili olması durumunda birden çok seçenek olacaktır.
6. Tıklatın **kaynak grubu** toosee hello kullanılabilir kaynak gruplarının listesini ya da tıklatın **yeni** toocreate yeni bir kaynak grubu. Kaynak grupları hakkında eksiksiz bilgiler için bkz. [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md)
7. Tıklatın **konumu** tooselect hello hello kasa için coğrafi bölgeyi. Merhaba kasa **gerekir** hello olması tooprotect istediğiniz hello sanal makineleri aynı bölgede.

   > [!IMPORTANT]
   > VM bulunduğu hello konumunu emin değilseniz, hello kasa oluşturma iletişim kutusunu kapatmak ve sanal makinelerin listesini toohello hello portalında gidin. Birden çok bölgede sanal makineniz varsa her bölgede bir kurtarma Hizmetleri kasası toocreate gerekir. Merhaba kasası toohello sonraki konuma geçmeden önce hello ilk konumda oluşturun. Toostore hello yedekleme verilerini--hello kurtarma Hizmetleri kasası gerek toospecify depolama hesabı yoktur ve hello Azure Backup hizmeti bunu otomatik olarak gerçekleştirir.
   >
   >

8. **Oluştur**'a tıklayın. Oluşturulan toobe kurtarma Hizmetleri kasası hello için biraz zaman alabilir. Merhaba üst sağ alanında hello portal Hello durum bildirimlerini izleyin. Kasanız oluşturulduktan sonra hello kurtarma Hizmetleri kasaları listesinde görünür. Kasanızı görmüyorsanız tıklatın **yenileme** için

    ![Yedekleme kasalarının listesi](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Kasanızı oluşturduğunuza göre nasıl tooset hello depolama çoğaltma öğrenin.

## <a name="set-storage-replication"></a>Depolama Çoğaltmayı Ayarlama
Merhaba depolama çoğaltma seçeneği, coğrafi olarak yedekli depolama ve yerel olarak yedekli depolama arasında toochoose sağlar. Varsayılan olarak, kasanız coğrafi olarak yedekli depolamaya sahiptir. Bu, birincil yedeklemenizse hello seçenek kümesi toogeo yedekli depolama bırakın. Daha düşük dayanıklılık düzeyinde olan daha uygun maliyetli bir seçenek istiyorsanız yerel olarak yedekli depolamayı seçin.

tooedit hello depolama çoğaltma ayarı:

1. Merhaba üzerinde **kurtarma Hizmetleri kasaları** dikey penceresinde kasanızı seçin.
    Ayarlar dikey penceresinde kasanızı tıklattığınızda hello (*hello üstünde hello kasasının hello ada sahip*) ve hello kasası ayrıntıları dikey penceresi açılır.

    ![Merhaba yedekleme kasalarının listesinden kasanızı seçin](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. Merhaba üzerinde **ayarları** dikey penceresinde, kullanım hello Dikey kaydırıcı tooscroll toohello aşağı **Yönet** bölümü. Tıklatın **Yedekleme Altyapısı** tooopen kendi dikey. Merhaba, **genel** bölümünde **yedekleme yapılandırması** tooopen kendi dikey. Merhaba üzerinde **yedekleme yapılandırması** dikey penceresinde kasanızı hello depolama çoğaltma seçeneğini seçin. Varsayılan olarak, kasanız coğrafi olarak yedekli depolamaya sahiptir. Merhaba depolama çoğaltma türü değiştirirseniz, tıklatın **kaydetmek**.

    ![Yedekleme kasalarının listesi](./media/backup-azure-arm-vms-prepare/full-blade.png)

     Azure'ı birincil yedekleme alanı uç noktası olarak kullanıyorsanız coğrafi olarak yedekli depolamayı kullanmaya devam edin. Azure birincil olmayan yedekleme alanı uç noktası olarak kullanıyorsanız, yerel olarak yedekli depolamayı seçin. Daha fazla bilgi edinin [coğrafi olarak yedekli](../storage/common/storage-redundancy.md#geo-redundant-storage) ve [yerel olarak yedekli](../storage/common/storage-redundancy.md#locally-redundant-storage) hello Depolama Seçenekleri [Azure Storage Çoğaltmaya genel bakış](../storage/common/storage-redundancy.md).
    Merhaba kasanız için depolama seçeneğini belirledikten sonra hazır tooassociate hello VM hello kasası ile demektir. toobegin hello ilişkilendirme bulmak ve gerekir kaydetmek Azure sanal makineleri hello.

## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Yedekleme hedefi seçme, ilke ayarlamak ve öğeleri tooprotect tanımlayın
Bir VM'yi bir kasaya kaydetmeden önce toohello abonelik eklenen yeni sanal makineler tanımlanır hello bulma işlemi tooensure çalıştırın. Merhaba işlem sorgularında Azure hello ek bilgilerle birlikte hello Abonelikteki sanal makinelerin listesini hello bulut hizmeti adı ve hello bölge gibi. Hello Azure portal, senaryo tooput hello kurtarma Hizmetleri kasasına giden toowhat ifade eder. Kurtarma noktalarının ne sıklıkta ve ne zaman alınır hello zamanlamasını ilkesidir. İlke hello bekletme aralığı hello kurtarma noktaları için de içerir.

1. Açık bir kurtarma Hizmetleri kasası zaten varsa 2 toostep devam edin. Açık kurtarma Hizmetleri kasası yoksa hello açmak [Azure portal](https://portal.azure.com/) ve hello Hub menüsünde **daha fazla hizmet**.

   * Kaynakları Hello listesinde yazın **kurtarma Hizmetleri**.
   * Yazmaya başladığınızda, hello filtreleyecek girişinize bağlı. **Kurtarma Hizmetleri kasaları** seçeneğini gördüğünüzde buna tıklayın.

     ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

     Merhaba kurtarma Hizmetleri kasalarının listesi görüntülenir. Aboneliğinizde hiçbir kasalarını varsa, bu listenin boş olur.

    ![Liste Görünümü hello kurtarma Hizmetleri kasaları](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

   * Kurtarma Hizmetleri kasalarının Hello listesinden bir kasa tooopen kendi Pano seçin.

     Hello ayarları dikey penceresinde ve hello Pano seçilen hello kasası, açılır Kasa.

     ![Kasa dikey penceresini açma](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)
2. Merhaba kasa Panosu menüsünden tıklatın **yedekleme** tooopen hello yedekleme dikey penceresinde.

    ![Yedekleme dikey penceresini açma](./media/backup-azure-arm-vms-prepare/backup-button.png)

    Merhaba yedekleme ve yedekleme hedefi dikey pencere açılır.

    ![Senaryo dikey penceresini açma](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)

3. Merhaba yedekleme hedefi dikey penceresinde ayarlamak **, iş yükünü çalıştırdığı** tooAzure ve **ne toobackup istediğiniz** tooVirtual makine ve ardından **Tamam**.

    Bu hello VM uzantısı hello kasası ile kaydeder. Merhaba yedekleme hedefi dikey penceresi kapanır ve hello **yedekleme İlkesi** dikey pencere açılır.

    ![Senaryo dikey penceresini açma](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)
4. Merhaba yedekleme İlkesi dikey penceresinde, tooapply toohello kasası hello yedekleme ilkesini seçin.

    ![Yedekleme ilkesini seçme](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    Merhaba varsayılan ilke Hello ayrıntılarını hello açılan menüsünün altında listelenir. Yeni bir ilke toocreate istiyorsanız seçin **Yeni Oluştur** hello açılan menüsünden. Bir yedekleme ilkesi tanımlamaya yönelik yönergeler için bkz. [Yedekleme ilkesi tanımlama](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Tıklatın **Tamam** tooassociate hello yedekleme İlkesi hello kasası ile.

    Yedekleme İlkesi dikey penceresi kapanır ve hello hello **sanal makine Seç** dikey pencere açılır.
5. Merhaba, **sanal makine Seç** dikey penceresinde hello sanal makineleri tooassociate hello ile ilke belirtilen tıklatın seçip **Tamam**.

    ![İş yükünü seçme](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    Seçili hello sanal makine doğrulanır. Merhaba sanal makineleri toosee beklenen görmüyorsanız, başka bir kasaya kurtarma Hizmetleri kasası ve zaten olmayan hello aynı Azure konumuna korumalı hello içinde mevcut kontrol edin. Kurtarma Hizmetleri kasası hello Hello konumu hello kasa panosunda görüntülenir.

6. Merhaba kasa için tüm ayarların tanımladığınız, yedekleme dikey penceresinde hello tıklatın **yedeklemeyi etkinleştir**. Bu, hello İlkesi toohello kasası ve hello VM'ler dağıtır. Bu hello hello sanal makine için ilk kurtarma noktası oluşturmaz.

    ![Yedeklemeyi Etkinleştirme](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Başarılı bir şekilde hello yedekleme etkinleştirdikten sonra yedekleme ilkenizi zamanlamaya göre çalıştırır. Şimdi toogenerate bir talep üzerine yedekleme işi tooback hello sanal makineleri yedeklemek istiyorsanız, bkz: [Triggering hello yedekleme işi](./backup-azure-arm-vms.md#triggering-the-backup-job).

Merhaba sanal makine kaydetme sorunları varsa, aşağıdaki bilgilerle hello VM Aracısı yükleme ve ağ bağlantısını hello bakın. Azure üzerinde oluşturulan sanal makineleri koruyorsanız bilgisinden hello muhtemelen gerekmez. Azure'da sanal makinelerinizi geçirdiyseniz, ancak ardından hello VM aracısı ve sanal makineniz hello sanal ağ ile iletişim kurabildiğini düzgün yüklenmemiş emin olun.

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Merhaba VM Aracısı hello sanal makineye yükleme
Hello Azure VM Aracısı hello hello yedekleme uzantısını toowork Azure sanal makinesine yüklenmesi gerekir. VM hello Azure galerisinde oluşturduysanız, ardından hello VM Aracısı hello sanal makineye zaten. Bu bilgiler nerede olduğunuza hello durumlar için sağlanan *değil* VM kullanılarak oluşturulan Azure galerisinde hello - örneğin bir VM bir şirket içi veri merkezinden geçişi. Böyle bir durumda, sipariş tooprotect hello sanal makinede yüklü toobe hello VM Aracısı gerekiyor. Merhaba hakkında bilgi edinin [VM Aracısı](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux).

Azure VM hello konusunda sorun yaşarsanız Azure VM Aracısı hello onay doğru hello sanal makinede yüklü (Merhaba tabloya bakın). Aşağıdaki tablonun hello için hello VM Aracısı Windows ve Linux VM'ler hakkında ek bilgi sağlar.

| **İşlem** | **Windows** | **Linux** |
| --- | --- | --- |
| Merhaba VM Aracısı yükleme |Merhaba yükleyip [aracı MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir. |<li> Merhaba son yükleme [Linux Aracısı](../virtual-machines/linux/agent-user-guide.md). Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir. Aracı dağıtım depodan yüklemenizi öneririz. Biz **değil önerilir** doğrudan github'dan yükleme Linux VM Aracısı.  |
| Merhaba VM Aracısı güncelleştiriliyor |Güncelleştirme hello VM aracısı yeniden yüklemeyi hello kadar basit [VM Aracısı ikili dosyalarının](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Merhaba VM Aracısı güncelleştirilirken herhangi bir yedekleme işleminin çalıştığından emin olun. |Merhaba yönergelerini izleyin [güncelleştirme hello Linux VM Aracısı](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Aracı dağıtım havuzunuzdan güncelleştirme öneririz. Biz **değil önerilir** doğrudan github'dan güncelleştirme Linux VM Aracısı.<br>VM Aracısı güncelleştirilmiş hello sırasında herhangi bir yedekleme işleminin çalıştığından emin olun. |
| Merhaba VM Aracısı yüklemesini doğrulama |<li>Toohello gidin *C:\WindowsAzure\Packages* hello Azure VM klasöründe. <li>Mevcut hello WaAppAgent.exe dosyasını bulmanız gerekir.<li> Merhaba dosyaya sağ tıklayın, çok Git**özellikleri**seçip hello **ayrıntıları** sekmesini hello ürün sürümü alanı 2.6.1198.718 olmalıdır ya da daha yüksek. |Yok |

### <a name="backup-extension"></a>Backup uzantısı
VM Aracısı hello sanal makinede, hello Azure Backup hizmeti yüklü hello bir kez hello yedekleme uzantısını toohello VM aracısı yükler. Hello Azure Backup hizmeti sorunsuz bir şekilde yükseltir ve hello yedekleme uzantısını düzeltme ekleri.

Merhaba VM çalıştıran olup olmadığına bakılmaksızın hello yedekleme uzantısı hello Backup hizmeti tarafından yüklenir. Çalışan bir VM, uygulamayla tutarlı bir kurtarma noktası hello alınma olasılığını en yükseğe. Ancak, hello Azure Backup hizmeti kapalı ve hello uzantısı yüklenmemiş olsa bile hello VM yukarı tooback devam eder. Buna Çevrimdışı VM adı verilir. Bu durumda, hello kurtarma noktası olur *kilitlenmeyle tutarlı*.

## <a name="network-connectivity"></a>Ağ bağlantısı
Sipariş toomanage hello VM anlık görüntülerini, bağlantı toohello Azure hello backup uzantısı gereken genel IP adresleri. Merhaba sağ Internet bağlantısı hello sanal makinenin HTTP isteklerini zaman aşımına uğrar ve hello yedekleme işlemi başarısız olur. Dağıtımınızı (örneğin ağ güvenlik grubu (NSG)) aracılığıyla yerinde erişim sınırlamaları varsa, yedekleme trafiği için açık bir yol sağlamak için bu seçeneklerden birini seçin:

* [Beyaz liste hello Azure veri merkezi IP aralıkları](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -toowhitelist hello IP nasıl adresleri hello makaledeki yönergelere bakın.
* Yönlendirme trafiği için bir HTTP proxy sunucusu dağıtın.

Hangi seçeneği toouse karar verirken hello dengelemeler yönetilebilirlik, ayrıntılı bir denetim ve maliyet arasında ' dir.

| Seçenek | Avantajları | Olumsuz yönleri |
| --- | --- | --- |
| Beyaz liste IP aralıkları |Hiçbir ek maliyet.<br><br>Bir NSG erişim açmak için hello kullan <i>kümesi AzureNetworkSecurityRule</i> cmdlet'i. |Karmaşık toomanage etkilenen hello IP aralıkları değişikliği zamanla olarak.<br><br>Azure ve yalnızca depolama toohello tam erişim sağlar. |
| HTTP proxy |Merhaba depolama üzerinde ayrıntılı denetim hello proxy'de URL'lere izin.<br>Tek noktası Internet erişimi tooVMs.<br>TooAzure IP adresi değişiklikleri edilmez. |Bir VM hello Ara yazılımıyla çalıştırmak için ek ücrete. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Beyaz liste hello Azure veri merkezi IP aralıkları
toowhitelist hello Azure veri merkezi IP aralıkları, lütfen hello bakın [Azure Web sitesi](http://www.microsoft.com/en-us/download/details.aspx?id=41653) hello IP aralıkları ve yönergeleri hakkında ayrıntılı bilgi için.

### <a name="using-an-http-proxy-for-vm-backups"></a>VM yedeklemeler için bir HTTP proxy kullanma
VM yedeklemesi zaman hello VM yedekleme uzantısını hello hello anlık görüntü yönetimi komutları tooAzure bir HTTPS API kullanarak depolama gönderir. Merhaba tek bileşen erişim toohello için yapılandırılmış olduğundan hello yedekleme uzantısını trafiğini hello HTTP proxy üzerinden yönlendirmek genel Internet.

> [!NOTE]
> Kullanılması gereken hello ara yazılım için hiçbir öneri yok. Merhaba yapılandırma adımları ile uyumlu bir proxy çekme emin olun.
>
>

Aşağıdaki örnek görüntü Hello hello üç yapılandırma adımları gerekli toouse bir HTTP proxy gösterir:

* Uygulama VM yollar tüm HTTP trafiği için ilişkili ortak Internet Proxy VM üzerinden hello.
* Proxy VM hello sanal ağında Vm'lerden gelen trafiğine izin verir.
* Merhaba NSF kilitleme adlı ağ güvenlik grubu (NSG) bir güvenlik kuralı izin giden Internet trafiği Proxy VM gerekir.

![NSG ile HTTP proxy dağıtım diyagramı](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse bir HTTP proxy toocommunicating toohello genel Internet, şu adımları izleyin:

#### <a name="step-1-configure-outgoing-network-connections"></a>1. Adım Giden ağ bağlantılarını yapılandırma
###### <a name="for-windows-machines"></a>Windows makineler için
Bu, yerel sistem hesabı için proxy sunucusu yapılandırmasını Kurulum.

1. Karşıdan [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Yükseltilmiş isteminden şu komutu çalıştırın,

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Internet explorer penceresi açar.
3. Git tooTools Internet Seçenekleri -> -> bağlantıları LAN Ayarları ->.
4. Sistem hesabı için proxy ayarlarını doğrulayın. Proxy IP ve bağlantı noktası ayarlayın.
5. Internet Explorer'ı kapatın.

Bu bir makine genelinde proxy yapılandırmasını ayarlanır ve tüm giden HTTP/HTTPS trafiği için kullanılır.

Geçerli kullanıcı hesabında (yerel sistem hesabı değildir) bir proxy sunucu kurulum varsa, komut dosyası tooapply bunları tooSYSTEMACCOUNT hello:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Proxy sunucu oturum açma "(407) Proxy kimlik doğrulaması gerekli" gözlemlerseniz, kimlik doğrulama Kurulumu doğru ayarlandığından emin olun.
>
>

###### <a name="for-linux-machines"></a>Linux makineler için
Satır toohello aşağıdaki hello eklemek ```/etc/environment``` dosyası:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Aşağıdaki satırları toohello hello eklemek ```/etc/waagent.conf``` dosyası:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>2. Adım Gelen bağlantıları hello proxy sunucusuna izin ver:
1. Merhaba proxy sunucusunda, Windows Güvenlik Duvarı'nı açın. Merhaba en kolay yolu tooaccess hello Güvenlik Duvarı'nı Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı toosearch ' dir.

    ![Merhaba Güvenlik Duvarı'nı açın](./media/backup-azure-vms-prepare/firewall-01.png)
2. Merhaba Windows Güvenlik Duvarı iletişim kutusunda sağ **gelen kuralları** tıklatıp **yeni kural...** .

    ![Yeni bir kural oluşturun](./media/backup-azure-vms-prepare/firewall-02.png)
3. Merhaba, **yeni gelen kuralı Sihirbazı**, hello seçin **özel** hello seçeneği **kural türü** tıklatıp **sonraki**.
4. Başlangıç sayfası tooselect hello üzerinde **Program**, seçin **tüm programlar** tıklatıp **sonraki**.
5. Merhaba üzerinde **protokol ve bağlantı noktaları** sayfasında, aşağıdaki bilgilerle hello girin ve tıklatın **sonraki**:

    ![Yeni bir kural oluşturun](./media/backup-azure-vms-prepare/firewall-03.png)

   * için *protokol türü* seçin *TCP*
   * için *yerel bağlantı noktası* seçin *belirli bağlantı noktaları*, aşağıdaki hello alana hello belirtin ```<Proxy Port>``` yapılandırılmış.
   * için *uzak bağlantı noktası* seçin *tüm bağlantı noktaları*

     Merhaba rest hello Sihirbazı'nın tüm hello yolu toohello Sonlandır'ı tıklatın ve bu kural bir ad verin.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>3. Adım Bir özel durum kuralı toohello NSG ekleyin:
Bir Azure PowerShell komut isteminde, komutu aşağıdaki hello girin:

komutu aşağıdaki hello bir özel durum toohello NSG ekler. Bu özel durumun 10.0.0.5 üzerinde herhangi bir bağlantı gelen TCP trafiğine izin verir tooany bağlantı noktası 80 (HTTP) veya 443 (HTTPS) Internet adresi. Belirli bir bağlantı noktası gerekiyorsa ortak Internet olması toohello bağlantı noktası emin tooadd hello ```-DestinationPortRange``` de.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```


*Bu adımları, bu örnek için belirli adları ve değerleri kullanın. Lütfen girerken, dağıtımınıza veya kesme ve ayrıntıları kodunuza yapıştırma hello adları ve değerleri kullanın.*

Artık ağ bağlantısına sahip bildiğinize göre VM'yi yedekleme hazır tooback demektir. Bkz: [Resource Manager tarafından dağıtılan Vm'leri yedekleme](backup-azure-arm-vms.md).

## <a name="questions"></a>Sorularınız mı var?
Sorularınız varsa veya herhangi bir özellik varsa dahil, toosee istediğiniz [Geri bildirimlerinizi bize gönderin](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Sonraki adımlar
VM yedeklemesi için ortamınızı hazırlandığınıza göre sonraki mantıksal toocreate bir yedekleme adımdır. makale planlama hello Vm'leri yedekleme konusunda daha ayrıntılı bilgi sağlar.

* [Sanal makineleri yedekleme](backup-azure-vms.md)
* [VM yedekleme altyapınızı planlama](backup-azure-vms-introduction.md)
* [Sanal makine yedeklerini yönetme](backup-azure-manage-vms.md)
