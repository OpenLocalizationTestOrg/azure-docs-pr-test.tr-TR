---
title: "Azure yedekleme: Hello Azure portal kullanarak sanal makineleri geri yükleme | Microsoft Docs"
description: "Bir Azure sanal makinesini Azure portalını kullanarak bir kurtarma noktasından geri yükleme"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "yedeklemeyi geri; nasıl toorestore; kurtarma noktası;"
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: f4f75d1da73c7760d2952afe80ff94918a08351c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toorestore-virtual-machines"></a>Azure portal toorestore sanal makineler kullanın
> [!div class="op_single_selector"]
> * [Sanal makineleri Klasik portalda geri yükleme](backup-azure-restore-vms.md)
> * [Azure portalında sanal makineleri geri yükleme](backup-azure-arm-restore-vms.md)
>
>

Verilerinizin anlık görüntüleri tanımlanan aralıklarla gerçekleştirerek verilerinizi koruyun. Bu anlık görüntüleri kurtarma noktaları olarak bilinir ve kurtarma Hizmetleri kasaları içinde depolanır. Varsa ya da gerekli toorepair olduğunda veya bir VM'yi yeniden kurtarma noktaları kaydedilmiş hello hiçbirini hello VM geri yükleyebilirsiniz. Bir kurtarma noktası geri yüklediğinizde, yedeklenen VM zaman içinde nokta gösterimi olan yeni bir VM oluşturmak veya diskleri geri yükleyebilir ve onunla birlikte gelir Başlangıç şablonu kullanmak toocustomize hello VM geri ya da bir bireysel dosya kurtarma yapın. Bu makalede açıklanır nasıl toorestore VM tooa yeni VM veya yedeklenen geri yükleme tüm diskler. Tek tek dosya kurtarma için çok başvuran[dosyaları Azure VM yedekten kurtarma](backup-azure-restore-files-from-vm.md)

![3-ways-Restore-from-VM-Backup](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki dağıtım modeline sahiptir: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Resource Manager modelini kullanarak dağıtılan VM'ler geri yüklemek için hello bilgi ve yordamlar sağlar.
>
>

Sanal makineden bir VM veya tüm diskleri geri yedekleme iki adımdan oluşur:

1. Geri yükleme için bir geri yükleme noktası seçin
2. Merhaba türü geri yükleme - yeni bir VM oluşturmak veya diskleri geri seçip gerekli parametreleri belirtin. 

## <a name="select-restore-point-for-restore"></a>Geri yükleme için geri yükleme noktası seçin
1. İçinde toohello oturum [Azure portalı](http://portal.azure.com/)
2. Hello Azure menüsü, tıklatın **Gözat** ve hizmetler hello listesinde yazın **kurtarma Hizmetleri**. hizmetlerin Hello listesi yazdığınız toowhat ayarlar. Gördüğünüzde **kurtarma Hizmetleri kasaları**, onu seçin.

    ![Açık kurtarma Hizmetleri kasası](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    Merhaba hello Abonelikteki kasalarının listesi görüntülenir.

    ![Liste kurtarma Hizmetleri kasaları](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. Merhaba listeden seçin hello kasası hello toorestore istediğiniz VM ile ilişkili. Merhaba kasası tıkladığınızda, kendi panosu açılır.

    ![Liste kurtarma Hizmetleri kasaları](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. Merhaba kasa panosunda olduğunuz göre. Merhaba üzerinde **yedekleme öğeleri** döşeme, tıklatın **Azure sanal makineleri** toodisplay hello VM'ler hello kasayla ilişkili.

    ![Kasa Panosu](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    Merhaba **yedekleme öğeleri** dikey penceresi açılır ve Azure sanal makineleri hello listesini görüntüler.

    ![Kasa VM'ler listesinde](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. Merhaba listeden bir VM tooopen hello Pano seçin. Merhaba VM Pano toohello hello geri yükleme noktaları kutucuğu içerir İzleme alanı açılır.

    ![Kasa VM'ler listesinde](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. Merhaba VM Pano menüsünde **geri yükleme**

    ![Kasa VM'ler listesinde](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    Merhaba geri yükleme dikey pencere açılır.

    ![geri yükleme dikey penceresi](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. Merhaba üzerinde **geri** dikey penceresinde tıklatın **geri yükleme noktası** tooopen hello **seçin geri yükleme noktası** dikey.

    ![geri yükleme dikey penceresi](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    Varsayılan olarak, son 30 gün hello tüm geri yükleme noktalarından hello iletişim kutusu görüntüler. Kullanım hello **filtre** hello tooalter hello zaman aralığını geri yükleme noktaları görüntülenir. Varsayılan olarak, tüm tutarlı geri yükleme noktaları görüntülenir. Değiştirme **tüm geri yükleme noktaları** tooselect belirli bir geri yükleme noktaları tutarlılığını filtre. Geri yükleme noktası türleri hakkında daha fazla bilgi için bkz: hello açıklaması [veri tutarlılığını](backup-azure-vms-introduction.md#data-consistency).  

   * **Geri yükleme noktası tutarlılık** bu listeden seçin:
     * Kilitlenme tutarlı geri yükleme noktaları,
     * Uygulama tutarlı geri yükleme noktaları
     * Dosya sistemiyle tutarlı geri yükleme noktaları
     * Tüm geri yükleme noktaları.  
8. Bir geri yükleme noktası seçin ve tıklatın **Tamam**.

    ![geri yükleme noktası seçin](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    Merhaba **geri** dikey gösterir hello geri yükleme noktası ayarlanır.

    ![geri yükleme noktası ayarlayın](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. Merhaba üzerinde **geri** dikey penceresinde **geri yükleme yapılandırmasını** geri yükleme noktası ayarlandıktan sonra otomatik olarak açılır.

## <a name="choosing-a-vm-restore-configuration"></a>Bir VM geri yükleme yapılandırmasını seçme
Seçili hello geri yükleme noktası, geri yüklemenizi VM için bir yapılandırma seçin. VM hello Yapılandırma seçimlerinizi geri toouse şunlardır: Azure portal veya PowerShell.

1. Toohello, zaten orada değilseniz, Git **geri** dikey. Olun bir [geri yükleme noktası seçili](#select-restore-point-for-restore), tıklatıp **geri yükleme yapılandırmasını** tooopen hello **kurtarma Yapılandırması** dikey.

    ![Kurtarma Yapılandırma Sihirbazı'nı ayarlama](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. Merhaba üzerinde **geri yükleme yapılandırmasını** dikey penceresinde, iki seçeneğiniz vardır:
   * Sanal makineyi tam geri yükleme
   * Diskleri yedeği geri yükleme

Portal, geri yüklenen VM için bir hızlı oluştur seçeneği sağlar. Toocustomize hello VM yapılandırması istediğiniz veya yeni bir VM seçenek parçası olarak oluşturulan hello kaynakların adları oluşturun, PowerShell kullanın veya portal toorestore yedeklenen diskleri ve kullanım PowerShell komutları tooattach bunları toochoice VM yapılandırması veya kullanımı şablonunun, gelen geri yükleme ile VM diskleri toocustomize hello geri. Bkz: [özel ağ yapılandırmaları olan bir VM geri](#restoring-vms-with-special-network-configurations) hakkında ayrıntılar için toorestore birden çok NIC veya yük dengeleyici altındaki VM. Windows VM kullanıyorsa [HUB lisans](../virtual-machines/windows/hybrid-use-benefit-licensing.md), toorestore diskiniz olması gerekir ve toocreate hello VM aşağıda belirtildiği gibi PowerShell/şablonu kullanın ve LicenseType değeri VM tooavail HUB oluşturulurken "Windows_Server" belirttiğinizden emin olun geri yüklenen VM üzerinde avantajları. 
 
## <a name="create-a-new-vm-from-restore-point"></a>Geri yükleme noktasından yeni bir VM oluşturun
Zaten orada değilseniz [bir geri yükleme noktası seçin](#restoring-vms-with-special-network-configurations) devam etmeden toocreating yeni bir VM geri yüklemeden önce gelin. Geri yükleme noktası seçildiğinde hello üzerinde **geri yükleme yapılandırmasını** dikey penceresinde girin veya seçin değerleri her alanları izleyen hello için:

* **Türü geri** -sanal makine oluşturun.
* **Sanal makine adı** -hello VM için bir ad sağlayın. Merhaba adı benzersiz toohello kaynak grubunun (bir Resource Manager tarafından dağıtılan VM) veya (için Klasik VM) bulut hizmeti olması gerekir. Merhaba abonelikte zaten mevcut değilse hello sanal makineyi değiştiremiyor.
* **Kaynak grubu** - varolan bir kaynak grubunu kullanın veya yeni bir tane oluşturun. Klasik VM geri yüklüyorsanız, yeni bir bulut hizmeti bu alan toospecify hello adını kullanın. Yeni bir kaynak grubu/bulut hizmeti oluşturuyorsanız hello adı genel olarak benzersiz olmalıdır. Genellikle, hello bulut hizmeti adı örneğin genel kullanıma yönelik URL ile - ilişkilendirilen: [buluthizmeti]. cloudapp.net. Toouse zaten kullanılmış hello bulut kaynak grubu/bulut hizmeti için bir ad çalışırsanız, Azure atar hello kaynak grubu/bulut hizmeti hello aynı adı VM hello gibi. Azure kaynak gruplarını/bulut Hizmetleri ve herhangi bir benzeşim grupları ile ilişkili olmayan VM'ler görüntüler. Daha fazla bilgi için bkz: [nasıl toomigrate benzeşim grupları tooa bölgesel sanal ağ (VNet) gelen](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
* **Sanal ağ** - seçin hello sanal ağ (VNET) oluştururken hello VM. Merhaba alan hello abonelikle ilişkili tüm sanal ağlar sağlar. Kaynak grubu hello VM parantez içinde görüntülenir.
* **Alt ağ** -hello sanal alt ağlar varsa, hello ilk alt ağ varsayılan olarak seçilidir. Ek alt ağlar varsa desired hello alt ağ seçin.
* **Depolama hesabı** -bu menü hello hello depolama hesaplarında listeler hello aynı konuma kurtarma Hizmetleri kasası. Bölge olarak yedekli depolama hesapları desteklenmez. Depolama hesabı ile yoksa hello hello aynı konuma kurtarma Hizmetleri kasası, bir hello geri yükleme işlemini başlatmadan önce oluşturmanız gerekir. Merhaba depolama hesabının çoğaltma türü parantez içinde belirtiliyor.

![geri yükleme Yapılandırma Sihirbazı'nı ayarlama](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. Resource Manager tarafından dağıtılan VM geri yüklüyorsanız, bir sanal ağ (VNET) tanımlamanız gerekir. Bir sanal ağ (VNET) klasik bir VM için isteğe bağlıdır.
> 2. Yönetilen disklerle VM'ler geri yüklüyorsanız, seçilen depolama hesabı için depolama hizmet Encryption(SSE) ömrü etkinleştirilmemiş olduğundan emin olun.
> 3. Merhaba depolama seçili depolama hesabının türüne (premium veya standart) bağlı olarak, tüm diskleri geri premium veya standart diskler olacaktır. Şu anda disklerin karma mod geri yüklerken desteklemiyoruz.  
>
>

Merhaba üzerinde **geri yükleme yapılandırmasını** dikey penceresinde tıklatın **Tamam** toofinalize hello geri yükleme yapılandırma. Merhaba üzerinde **geri** dikey penceresinde tıklatın **geri** tootrigger hello geri yükleme işlemi.

## <a name="restore-backed-up-disks"></a>Diskleri yedeği geri yükleme
Toocustomize hello sanal makine isterseniz geri yükleme yapılandırma dikey penceresinde, select varsa daha diskleri toocreate gelen yedeklenen istediğinizi **geri diskleri** olarak değer **geri türü**. Bu seçenek yedeklemeleri disklerden burada kopyalanır bir depolama hesabı ister. Bir depolama hesabı seçerken, hello kurtarma Hizmetleri kasası olarak paylaşımları aynı konuma hello bir hesap seçin. Bölge olarak yedekli depolama hesapları desteklenmez. Depolama hesabı ile yoksa hello hello aynı konuma kurtarma Hizmetleri kasası, bir hello geri yükleme işlemini başlatmadan önce oluşturmanız gerekir. Merhaba depolama hesabının çoğaltma türü parantez içinde belirtiliyor.

Geri yükleme işlemi tamamlandıktan sonra şunları yapabilirsiniz:
* [VM kullanım şablonu toocustomize hello geri](#use-templates-to-customize-restore-vm)
* [Diskleri tooattach tooan varolan sanal makine kullanım hello geri](../virtual-machines/windows/attach-managed-disk-portal.md)
* [Geri yüklenen disklerden PowerShell kullanarak yeni bir sanal makine oluşturun.](./backup-azure-vms-automation.md#restore-an-azure-vm)

Merhaba üzerinde **geri yükleme yapılandırmasını** dikey penceresinde tıklatın **Tamam** toofinalize hello geri yükleme yapılandırma. Merhaba üzerinde **geri** dikey penceresinde tıklatın **geri** tootrigger hello geri yükleme işlemi.

![Kurtarma yapılandırması tamamlandı](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-hello-restore-operation"></a>İzleme hello geri yükleme işlemi
Merhaba geri yükleme işlemi tetiklemek sonra hello Backup hizmeti izleme hello geri yükleme işlemi için bir iş oluşturur. Merhaba Backup hizmeti da oluşturur ve hello bildirim portal bildirimleri alanında geçici olarak görüntüler. Merhaba bildirim görmüyorsanız, her zaman bildirimlerinizi hello bildirimler simgesine tooview tıklayabilirsiniz.

![Tetiklenen geri yükleme](./media/backup-azure-arm-restore-vms/restore-notification.png)

Bunu işlerken tooview hello işlem ya da tamamlandığında, tooview hello yedekleme işleri listesini açın.

1. Hello Azure menüsü, tıklatın **Gözat** ve hizmetler hello listesinde yazın **kurtarma Hizmetleri**. hizmetlerin Hello listesi yazdığınız toowhat ayarlar. Gördüğünüzde **kurtarma Hizmetleri kasaları**, onu seçin.

    ![Açık kurtarma Hizmetleri kasası](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    Merhaba hello Abonelikteki kasalarının listesi görüntülenir.

    ![Liste kurtarma Hizmetleri kasaları](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. Merhaba listeden seçin hello kasası hello geri VM ile ilişkili. Merhaba kasası tıkladığınızda, kendi panosu açılır.
3. Hello kasa panosunda hello üzerinde **yedekleme işlerini** döşeme, tıklatın **Azure sanal makineleri** toodisplay hello işleri hello kasayla ilişkili.

    ![Kasa Panosu](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    Merhaba **yedekleme işlerini** dikey penceresi açılır ve işleri hello listesini görüntüler.

    ![Kasa VM'ler listesinde](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-toocustomize-restore-vm"></a>Şablonları toocustomize geri yükleme vm kullanın
Bir kez [geri yükleme diskleri işlemi tamamlandığında](#Track-the-restore-operation), geri yükleme işlemi toocreate kaynakların yedekleme yapılandırması veya toocustomize adlarından farklı bir yapılandırma ile yeni bir VM bir parçası olarak oluşturulan hello şablonu kullanın geri yükleme noktasından yeni bir vm oluşturmak gibi oluşturulur. 

> [!NOTE]
> Şablonlar, 1 Mart 2017 sonra gerçekleştirilecek kurtarma noktaları için geri diskleri parçası olarak eklenir. Bunlar, şifrelenmemiş ve yönetilmeyen disk VM'ler için geçerlidir. Şifrelenmiş VM'ler ve yönetilen Disk VM'ler için destek gelecek sürümlerde kullanıma sunulacaktır. 
>
>

geri yükleme diskler seçeneği bir parçası olarak oluşturulan tooget hello şablonunu

1. Toohello iş karşılık gelen toorestore iş ayrıntılarına gidin. 
2. Merhaba geri yükleme işi ayrıntıları ekranda tıklayın *dağıtma şablonu* düğmesini tooinitiate şablon dağıtımı. 

     ![İş ayrıntıya geri yükleme](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
Merhaba dağıtma şablonu dikey penceresinde özel dağıtım, şablon dağıtımı çok kullanmak[düzenleyin ve hello şablonu dağıtmak](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) veya daha fazla özelleştirme tarafından ilave [şablon yazma](../azure-resource-manager/resource-group-authoring-templates.md) dağıtmadan önce. 

   ![Şablon dağıtımı yükleme](./media/backup-azure-arm-restore-vms/loading-template.png)
   
Gerekli hello değerleri girdikten sonra hello kabul *hüküm ve koşullar* ve tıklayın **satın alma**.

   ![Şablon dağıtımı gönderiliyor](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>Geri yükleme sonrası adımlar
* Güvenlik nedenleriyle Ubuntu gibi bir bulut init göre Linux dağıtım kullanıyorsanız, parola engellendi geri yükleme sonrası. Lütfen kullanım hello VMAccess uzantısını VM çok geri[hello parola sıfırlama](../virtual-machines/linux/classic/reset-access.md). Parola post geri yükleme sıfırlama bu dağıtımları tooavoid üzerinde SSH anahtarları kullanmanızı öneririz.
* Bunlar etkin olmaz ancak uzantıları hello yedekleme yapılandırma sırasında mevcut yüklenir. Herhangi bir sorun görürseniz uzantılarını yeniden yükleyin. 
* Merhaba yedeklenen VM statik IP, post geri yükleme sahip, VM oluşturma geri geri yüklenen VM dinamik IP tooavoid çakışma olur. Ne yapabileceğiniz hakkında daha fazla bilgi edinin [statik bir IP toorestored VM ekleme](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* Geri yüklenen VM kullanılabilirlik değeri ayarlanmış sahip olmaz. Geri yükleme diskler seçeneği kullanmanız önerilir ve [kullanılabilirlik kümesi ekleme](../virtual-machines/windows/tutorial-availability-sets.md) zaman PowerShell kullanarak şablonları VM oluşturuluyor izin ver geri diskler. 


## <a name="backup-for-restored-vms"></a>Geri yüklenen VM'ler için yedekleme
Aynı adı olarak ilk olarak VM yedeklemesi yedeklenen hello ile VM toosame kaynak grubu geri yüklediyseniz, yedekleme hello üzerinde VM post geri yükleme devam eder. VM tooa farklı kaynak grubuna geri veya geri yüklenen VM için farklı bir ad belirtilen varsa, bu yeni VM olarak değerlendirilir ve geri yüklenen VM için toosetup yedekleme gerekiyor.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Bir VM Azure veri merkezi olağanüstü durum sırasında geri yükleme
Azure yedekleme, burada VM'ler deneyimleri olağanüstü durum çalıştırıyorsanız ve yedekleme kasası toobe coğrafi olarak yedekli yapılandırılmış hello birincil veri merkezi durumda VM'ler toohello eşleştirilmiş veri merkezi yedeklenen sağlar. Bu tür senaryoları sırasında hello geri yükleme işleminin geri kalanında aynı kalır ve tooselect eşleştirilmiş veri merkezinde mevcut bir depolama hesabı gerekir. Azure yedekleme eşleştirilmiş coğrafi toocreate geri hello sanal makine işlem hizmetinden kullanır. Daha fazla bilgi edinmek [Azure veri merkezi dayanıklılık](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Etki alanı denetleyicisi sanal makineleri geri yükleme
Etki alanı denetleyicisi (DC) sanal makinelerinin Azure yedekleme ile desteklenen bir senaryodur. Ancak, hello geri yükleme işlemi sırasında dikkatli olunması gerekir. Merhaba doğru geri yükleme işlemi hello hello etki alanı yapısına bağlıdır. Merhaba en basit durumda tek bir etki alanında tek bir DC sahip. Daha sık üretim yükleri, tek bir etki alanı birden çok DC'ler, belki de DC'lere ile şirket içinde gerekir. Son olarak, birden çok etki alanı içeren bir ormanda olabilir. 

Bir Active Directory perspektif hello başka bir VM modern desteklenen bir hiper yöneticide Azure VM gibidir. Merhaba ana ile şirket içi hiper yöneticilerin VM konsolu ile Azure kullanılabilir olduğunu farktır. Bir konsol tam kurtarma (BMR) türü yedekleme kullanarak kurtarma gibi belirli senaryolar için gereklidir. Ancak, VM geri yükleme hello yedekleme Kasası'ndan tam bir BMR yerini alır. Active Directory Geri Yükleme Modu'nda (DSRM), ayrıca tüm Active Directory Kurtarma senaryolarına uygun şekilde kullanılabilir. Daha fazla bilgi için lütfen denetleyin [yedekleme ve geri yükleme hakkında önemli noktalar sanallaştırılmış etki alanı denetleyicileri için](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) ve [için Active Directory orman Kurtarma planlaması](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Tek bir etki alanındaki tek DC
Merhaba VM (tüm diğer VM gibi) hello Azure ' geri yüklenebilir portal veya PowerShell kullanarak.

### <a name="multiple-dcs-in-a-single-domain"></a>Tek bir etki alanındaki birden çok DC'leri
Ağ üzerinden aynı etki alanında ulaşılabilen Merhaba, diğer DC'ler Merhaba, hello DC gibi herhangi bir VM geri yüklenebilir. Merhaba etki alanındaki son kalan DC hello veya yalıtılmış bir ağda kurtarma gerçekleştirilen ise, orman kurtarma yordamı gelmelidir.

### <a name="multiple-domains-in-one-forest"></a>Bir ormandaki birden çok etki alanları
Ağ üzerinden aynı etki alanında ulaşılabilen Merhaba, diğer DC'ler Merhaba, hello DC gibi herhangi bir VM geri yüklenebilir. Ancak, diğer tüm durumlarda bir orman kurtarma önerilir.

## <a name="restoring-vms-with-special-network-configurations"></a>Özel ağ yapılandırmaları ile sanal makineleri geri yükleme
Bu olası tooback yedeklemek ve geri yükleme VM'ler ile özel ağ yapılandırmaları aşağıdaki hello olur. Ancak, bu yapılandırmalar hello geri yükleme sürecinden sırasında bazı ayrıcalık gerektirir.

* Yük Dengeleyici (iç ve dış) altında yer alan VM'ler
* Birden çok ayrılmış IP ile sanal makineleri
* Birden çok NIC içeren VM'ler

> [!IMPORTANT]
> Merhaba özel ağ yapılandırması VM'ler için oluştururken, PowerShell toocreate VM'ler geri hello disklerden kullanmanız gerekir.
>
>

toodisk, geri yükledikten sonra toofully yeniden oluşturun hello sanal makineleri şu adımları izleyin:

1. Kurtarma Hizmetleri kasası kullanarak bir Hello diskleri geri [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. Yük Dengeleyici için gerekli hello VM yapılandırması oluştur / birden çok NIC/birden çok ayrılmış IP kullanarak ve PowerShell cmdlet'leri hello toocreate hello istenen yapılandırma VM kullanın.

   * VM bulut hizmetiyle oluşturmak [iç yük dengeleyici](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * VM tooconnect çok oluşturmak[Internet'e yönelik Yük Dengeleyici](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * VM oluşturma [birden çok NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * VM oluşturma [birden çok ayrılmış IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Sonraki adımlar
Vm'leriniz geri yükleyebilir, makale VMs sık karşılaşılan hatalar hakkında bilgi için sorun giderme hello bakın. Ayrıca Vm'lerinizi görevlerle yönetme hello makalede göz atın.

* [Sorun giderme](backup-azure-vms-troubleshoot.md#restore)
* [Sanal makineleri yönetme](backup-azure-manage-vms.md)
