---
title: "Azure yedekleme: Azure portalını kullanarak sanal makineleri geri yükleme | Microsoft Docs"
description: "Bir Azure sanal makinesini Azure portalını kullanarak bir kurtarma noktasından geri yükleme"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "yedeklemeyi geri; geri yükleme; kurtarma noktası;"
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: e1fe2b94d462a30f09cb23ab905542aa121ba46b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-portal-to-restore-virtual-machines"></a>Azure portalı kullanarak sanal makineleri geri yükleme
> [!div class="op_single_selector"]
> * [Sanal makineleri Klasik portalda geri yükleme](backup-azure-restore-vms.md)
> * [Azure portalında sanal makineleri geri yükleme](backup-azure-arm-restore-vms.md)
>
>

Verilerinizin anlık görüntüleri tanımlanan aralıklarla gerçekleştirerek verilerinizi koruyun. Bu anlık görüntüleri kurtarma noktaları olarak bilinir ve kurtarma Hizmetleri kasaları içinde depolanır. İse veya onarmak veya VM yeniden oluşturmak gerekli olduğunda, kaydedilen kurtarma noktaları hiçbirini VM geri yükleyebilirsiniz. Bir kurtarma noktası geri yüklediğinizde, yedeklenen VM zaman içinde nokta gösterimi olan yeni bir VM oluşturmak veya diskleri geri yüklemek ve onunla birlikte geri yüklenen VM özelleştirebilir veya tek tek dosya kurtarma yapmak için gelen şablonu kullanabilirsiniz. Bu makalede, bir VM için yeni bir VM geri yükleyin veya tüm yedeklenen diskleri geri açıklanmaktadır. Tek tek dosya kurtarma için başvurmak [dosyaları Azure VM yedekten kurtarma](backup-azure-restore-files-from-vm.md)

![3-ways-Restore-from-VM-Backup](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki dağıtım modeline sahiptir: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, Resource Manager modelini kullanarak dağıtılan VM'ler geri yüklemek için bilgi ve yordamlar sağlar.
>
>

Sanal makineden bir VM veya tüm diskleri geri yedekleme iki adımdan oluşur:

1. Geri yükleme için bir geri yükleme noktası seçin
2. Geri yükleme seçerek yazın - yeni bir VM oluşturmak veya diskleri geri ve gerekli parametreleri belirtin. 

## <a name="select-restore-point-for-restore"></a>Geri yükleme için geri yükleme noktası seçin
1. Oturum [Azure portalı](http://portal.azure.com/)
2. Azure menüsünde **Gözat** ve Hizmetler listesinde yazın **kurtarma Hizmetleri**. Hizmetler listesi, yazdığınız için ayarlar. Gördüğünüzde **kurtarma Hizmetleri kasaları**, onu seçin.

    ![Açık kurtarma Hizmetleri kasası](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    Abonelikteki kasalarının listesi görüntülenir.

    ![Liste kurtarma Hizmetleri kasaları](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. Listeden, geri yüklemek istediğiniz VM ile ilişkili kasayı seçin. Kasa tıkladığınızda, kendi panosu açılır.

    ![Liste kurtarma Hizmetleri kasaları](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. Kasa panosunda olduğunuz göre. Üzerinde **yedekleme öğeleri** döşeme, tıklatın **Azure sanal makineleri** kasayla ilişkili VM'ler görüntülemek için.

    ![Kasa Panosu](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    **Yedekleme öğeleri** dikey penceresi açılır ve Azure sanal makinelerin listesini görüntüler.

    ![Kasa VM'ler listesinde](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. Listeden panoyu açmak için bir VM seçin. VM Pano geri yükleme noktaları döşeme içeren izleme alanı açılır.

    ![Kasa VM'ler listesinde](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. VM Pano menüsünde **geri yükleme**

    ![Kasa VM'ler listesinde](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    Geri yükleme dikey pencere açılır.

    ![geri yükleme dikey penceresi](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. Üzerinde **geri** dikey penceresinde tıklatın **geri yükleme noktası** açmak için **seçin geri yükleme noktası** dikey.

    ![geri yükleme dikey penceresi](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    Varsayılan olarak, son 30 günün tüm geri yükleme noktaları iletişim kutusu görüntüler. Kullanım **filtre** geri yükleme noktaları zaman aralığını değiştirmek için görüntülenir. Varsayılan olarak, tüm tutarlı geri yükleme noktaları görüntülenir. Değiştirme **tüm geri yükleme noktaları** belirli bir geri yükleme noktaları tutarlılığını seçmek için filtre. Geri yükleme noktası türleri hakkında daha fazla bilgi için bkz: Açıklama [veri tutarlılığını](backup-azure-vms-introduction.md#data-consistency).  

   * **Geri yükleme noktası tutarlılık** bu listeden seçin:
     * Kilitlenme tutarlı geri yükleme noktaları,
     * Uygulama tutarlı geri yükleme noktaları
     * Dosya sistemiyle tutarlı geri yükleme noktaları
     * Tüm geri yükleme noktaları.  
8. Bir geri yükleme noktası seçin ve tıklatın **Tamam**.

    ![geri yükleme noktası seçin](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    **Geri** dikey gösterir geri yükleme noktası ayarlanır.

    ![geri yükleme noktası ayarlayın](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. Üzerinde **geri** dikey penceresinde **geri yükleme yapılandırmasını** geri yükleme noktası ayarlandıktan sonra otomatik olarak açılır.

## <a name="choosing-a-vm-restore-configuration"></a>Bir VM geri yükleme yapılandırmasını seçme
Seçili geri yükleme noktası, geri yüklemenizi VM için bir yapılandırma seçin. Kullanılacak geri yüklenen VM yapılandırma Seçenekleriniz şunlardır: Azure portal veya PowerShell.

1. Olan değil zaten vardır, giderseniz için **geri** dikey. Olun bir [geri yükleme noktası seçili](#select-restore-point-for-restore), tıklatıp **geri yükleme yapılandırmasını** açmak için **kurtarma Yapılandırması** dikey.

    ![Kurtarma Yapılandırma Sihirbazı'nı ayarlama](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. Üzerinde **geri yükleme yapılandırmasını** dikey penceresinde, iki seçeneğiniz vardır:
   * Sanal makineyi tam geri yükleme
   * Diskleri yedeği geri yükleme

Portal, geri yüklenen VM için bir hızlı oluştur seçeneği sağlar. VM yapılandırması özelleştirmek istediğiniz veya yeni bir VM seçenek parçası olarak oluşturulan kaynakların adları oluşturun, yedeklenen diskleri geri yükleyin ve istediğiniz bir VM yapılandırmasına ekleyin veya birlikte şablonu kullanmak için PowerShell komutlarını kullanın için PowerShell veya portal kullanın re geri yüklenen VM özelleştirmek için diskleri depolar. Bkz: [özel ağ yapılandırmaları olan bir VM geri](#restoring-vms-with-special-network-configurations) birden çok NIC içeren VM geri yükleme veya yük dengeleyici altındaki ayrıntılar için. Windows VM kullanıyorsa [HUB lisans](../virtual-machines/windows/hybrid-use-benefit-licensing.md), diskleri geri yüklemek ve VM oluşturma ve LicenseType değeri HUB avantajları üzerinde kullanılabilir kredi VM oluşturulurken "Windows_Server" belirttiğinizden emin olun PowerShell/şablon olarak belirtilen aşağıdaki kullanması gereken geri yüklenen VM. 
 
## <a name="create-a-new-vm-from-restore-point"></a>Geri yükleme noktasından yeni bir VM oluşturun
Zaten orada değilseniz [bir geri yükleme noktası seçin](#restoring-vms-with-special-network-configurations) etmeden önce geri yükleme noktasından yeni bir VM oluşturmak için. Geri yükleme noktası, üzerinde seçildikten sonra **geri yükleme yapılandırmasını** dikey penceresinde girin veya seçin değerleri aşağıdaki alanların her biri için:

* **Türü geri** -sanal makine oluşturun.
* **Sanal makine adı** -VM için bir ad sağlayın. Adı kaynak grubu (Resource Manager tarafından dağıtılan VM) veya (için Klasik VM) bulut hizmeti için benzersiz olmalıdır. Abonelikte zaten varsa, sanal makineyi değiştiremiyor.
* **Kaynak grubu** - varolan bir kaynak grubunu kullanın veya yeni bir tane oluşturun. Klasik VM geri yüklüyorsanız, yeni bir bulut hizmeti adını belirtmek için bu alanı kullanın. Yeni bir kaynak grubu/bulut hizmeti oluşturuyorsanız, adı genel olarak benzersiz olması gerekir. Genellikle, bulut hizmet adı örneğin genel kullanıma yönelik URL ile - ilişkilendirilen: [buluthizmeti]. cloudapp.net. Zaten kullanılan bulut kaynak grubu/bulut hizmeti için bir ad kullanmayı denerseniz, Azure kaynak grubu/bulut hizmeti VM adıyla aynı atar. Azure kaynak gruplarını/bulut Hizmetleri ve herhangi bir benzeşim grupları ile ilişkili olmayan VM'ler görüntüler. Daha fazla bilgi için bkz: [benzeşim grupları bölgesel bir sanal ağa (VNet) geçirmek nasıl](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
* **Sanal ağ** -VM oluştururken sanal ağı (VNET) seçin. Alan abonelikle ilişkili tüm sanal ağlar sağlar. Kaynak grubu VM parantez içinde görüntülenir.
* **Alt ağ** -sanal ağ alt ağlar varsa, ilk alt ağ varsayılan olarak seçilidir. Ek alt ağlar varsa, istenen alt ağ seçin.
* **Depolama hesabı** -bu menü kurtarma Hizmetleri kasasıyla aynı konumda depolama hesaplarını listeler. Bölge olarak yedekli depolama hesapları desteklenmez. Kurtarma Hizmetleri kasasıyla aynı konumda ile depolama hesabı yoksa, geri yükleme işlemini başlatmadan önce oluşturmanız gerekir. Depolama hesabının çoğaltma türü parantez içinde belirtiliyor.

![geri yükleme Yapılandırma Sihirbazı'nı ayarlama](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. Resource Manager tarafından dağıtılan VM geri yüklüyorsanız, bir sanal ağ (VNET) tanımlamanız gerekir. Bir sanal ağ (VNET) klasik bir VM için isteğe bağlıdır.
> 2. Yönetilen disklerle VM'ler geri yüklüyorsanız, seçilen depolama hesabı için depolama hizmet Encryption(SSE) ömrü etkinleştirilmemiş olduğundan emin olun.
> 3. Seçilen depolama hesabı (premium veya standart) depolama türüne bağlı olarak, tüm diskleri geri premium veya standart diskler olacaktır. Şu anda disklerin karma mod geri yüklerken desteklemiyoruz.  
>
>

Üzerinde **geri yükleme yapılandırmasını** dikey penceresinde tıklatın **Tamam** geri yükleme yapılandırmasını son haline getirmek için. Üzerinde **geri** dikey penceresinde tıklatın **geri** geri yükleme işlemi tetiklemek için.

## <a name="restore-backed-up-disks"></a>Diskleri yedeği geri yükleme
Sanal makineyi özelleştirmek istiyorsanız oluşturmak geri yükleme yapılandırma dikey penceresinde, select varsa daha diskleri yedeklenen istediğiniz **geri diskleri** olarak değer **geri türü**. Bu seçenek yedeklemeleri disklerden burada kopyalanır bir depolama hesabı ister. Bir depolama hesabı seçerken, Kurtarma Hizmetleri kasasıyla aynı konumda paylaşan bir hesap seçin. Bölge olarak yedekli depolama hesapları desteklenmez. Kurtarma Hizmetleri kasasıyla aynı konumda ile depolama hesabı yoksa, geri yükleme işlemini başlatmadan önce oluşturmanız gerekir. Depolama hesabının çoğaltma türü parantez içinde belirtiliyor.

Geri yükleme işlemi tamamlandıktan sonra şunları yapabilirsiniz:
* [Geri yüklenen VM özelleştirmek için şablon kullanın](#use-templates-to-customize-restore-vm)
* [Varolan bir sanal makineye eklemek için geri yüklenen diskleri kullanın](../virtual-machines/windows/attach-managed-disk-portal.md)
* [Geri yüklenen disklerden PowerShell kullanarak yeni bir sanal makine oluşturun.](./backup-azure-vms-automation.md#restore-an-azure-vm)

Üzerinde **geri yükleme yapılandırmasını** dikey penceresinde tıklatın **Tamam** geri yükleme yapılandırmasını son haline getirmek için. Üzerinde **geri** dikey penceresinde tıklatın **geri** geri yükleme işlemi tetiklemek için.

![Kurtarma yapılandırması tamamlandı](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-the-restore-operation"></a>Geri yükleme işlemini izlemek
Geri yükleme işlemi tetiklemek sonra Backup hizmeti geri yükleme işlemini izlemek için bir proje oluşturur. Yedekleme hizmeti da oluşturur ve bildirim portal bildirimleri alanında geçici olarak görüntüler. Bildirim görmüyorsanız, her zaman bildirimlerinizi görüntülemek için bildirimler simgesine tıklayabilirsiniz.

![Tetiklenen geri yükleme](./media/backup-azure-arm-restore-vms/restore-notification.png)

Bunu işlerken işlemi görüntülemek veya onu tamamlandığında görüntülemek için yedekleme işleri listesini açın.

1. Azure menüsünde **Gözat** ve Hizmetler listesinde yazın **kurtarma Hizmetleri**. Hizmetler listesi, yazdığınız için ayarlar. Gördüğünüzde **kurtarma Hizmetleri kasaları**, onu seçin.

    ![Açık kurtarma Hizmetleri kasası](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    Abonelikteki kasalarının listesi görüntülenir.

    ![Liste kurtarma Hizmetleri kasaları](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. Listeden, geri VM ile ilişkili kasayı seçin. Kasa tıkladığınızda, kendi panosu açılır.
3. Kasa panosunda **yedekleme işlerini** döşeme, tıklatın **Azure sanal makineleri** kasayla ilişkili işleri görüntülemek için.

    ![Kasa Panosu](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    **Yedekleme işlerini** dikey penceresi açılır ve işlerin listesini görüntüler.

    ![Kasa VM'ler listesinde](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-to-customize-restore-vm"></a>Geri yükleme vm özelleştirmek için şablonlar kullanın
Bir kez [geri yükleme diskleri işlemi tamamlandığında](#Track-the-restore-operation), bir yapılandırma ile yeni bir VM yedekleme yapılandırması farklı oluşturmayı veya oluşturulan kaynakların adları özelleştirmek için geri yükleme işleminin bir parçası olarak oluşturulan şablon kullanabilirsiniz olarak geri yükleme noktasından yeni bir vm oluşturun. 

> [!NOTE]
> Şablonlar, 1 Mart 2017 sonra gerçekleştirilecek kurtarma noktaları için geri diskleri parçası olarak eklenir. Bunlar, şifrelenmemiş ve yönetilmeyen disk VM'ler için geçerlidir. Şifrelenmiş VM'ler ve yönetilen Disk VM'ler için destek gelecek sürümlerde kullanıma sunulacaktır. 
>
>

Geri yükleme diskler seçeneği bir parçası olarak oluşturulan şablonunu almak için

1. İşin iş ayrıntılarını geri gidin. 
2. Geri yükleme işi ayrıntıları ekranda tıklayın *dağıtma şablonu* şablon dağıtımını başlatmak için düğmesi. 

     ![İş ayrıntıya geri yükleme](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
Dağıtım şablonu dikey penceresinde özel dağıtım, şablon dağıtımı kullanmak [düzenleyin ve şablonu dağıtmak](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) veya daha fazla özelleştirme tarafından ilave [şablon yazma](../azure-resource-manager/resource-group-authoring-templates.md) dağıtmadan önce. 

   ![Şablon dağıtımı yükleme](./media/backup-azure-arm-restore-vms/loading-template.png)
   
Gereken değerleri girdikten sonra kabul *hüküm ve koşullar* ve tıklayın **satın alma**.

   ![Şablon dağıtımı gönderiliyor](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>Geri yükleme sonrası adımlar
* Güvenlik nedenleriyle Ubuntu gibi bir bulut init göre Linux dağıtım kullanıyorsanız, parola engellendi geri yükleme sonrası. Lütfen geri yüklenen VM üzerinde VMAccess uzantısını kullanmak [parola sıfırlama](../virtual-machines/linux/classic/reset-access.md). Parola post geri yükleme sıfırlama önlemek için bu dağıtım üzerinde SSH anahtarları kullanmanızı öneririz.
* Bunlar etkin olmaz ancak yedekleme yapılandırma sırasında mevcut uzantıları yüklenir. Herhangi bir sorun görürseniz uzantılarını yeniden yükleyin. 
* Statik IP, post geri yükleme, yedeklenen VM varsa, geri yüklenen VM oluşturma VM geri zaman çakışmayı önlemek için dinamik IP sahip olur. Ne yapabileceğiniz hakkında daha fazla bilgi edinin [geri yüklenen VM için bir statik IP Ekle](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* Geri yüklenen VM kullanılabilirlik değeri ayarlanmış sahip olmaz. Geri yükleme diskler seçeneği kullanmanız önerilir ve [kullanılabilirlik kümesi ekleme](../virtual-machines/windows/tutorial-availability-sets.md) zaman PowerShell kullanarak şablonları VM oluşturuluyor izin ver geri diskler. 


## <a name="backup-for-restored-vms"></a>Geri yüklenen VM'ler için yedekleme
İlk olarak VM yedeklemesi yedeklenen aynı adla aynı kaynak grubuna VM geri yükledikten, yedekleme VM post geri yükleme devam eder. VM için farklı bir kaynak grubuna geri veya geri yüklenen VM için farklı bir ad belirtilen varsa, bu yeni VM olarak değerlendirilir ve geri yüklenen VM için Kurulum yedekleme gerekiyor.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Bir VM Azure veri merkezi olağanüstü durum sırasında geri yükleme
Azure yedekleme geri yükleme durumunda burada VM'ler deneyimleri olağanüstü durum çalıştırıyorsanız ve yedekleme Kasası'coğrafi olarak yedekli olacak şekilde yapılandırılmış birincil veri merkezi Vm'leri eşleştirilmiş veri merkezine yedeklenen sağlar. Bu tür senaryoları sırasında eşlenmiş veri merkezinde mevcut bir depolama hesabı seçmeniz gerekir ve geri yükleme işleminin geri kalanında aynı kalır. Azure yedekleme, geri yüklenen sanal makine oluşturmak için işlem hizmetinden eşleştirilmiş coğrafi kullanır. Daha fazla bilgi edinmek [Azure veri merkezi dayanıklılık](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Etki alanı denetleyicisi sanal makineleri geri yükleme
Etki alanı denetleyicisi (DC) sanal makinelerinin Azure yedekleme ile desteklenen bir senaryodur. Ancak, geri yükleme işlemi sırasında dikkatli olunması gerekir. Doğru geri yükleme işlemi, etki alanı yapısına bağlıdır. En basit durumda tek bir etki alanında tek bir DC sahip. Daha sık üretim yükleri, tek bir etki alanı birden çok DC'ler, belki de DC'lere ile şirket içinde gerekir. Son olarak, birden çok etki alanı içeren bir ormanda olabilir. 

Bir Active Directory açısından herhangi bir VM modern desteklenen hiper yönetici üzerinde Azure VM gibidir. Şirket içi hiper ile en önemli fark, hiçbir VM konsolu ile Azure kullanılabilir olduğunu ' dir. Bir konsol tam kurtarma (BMR) türü yedekleme kullanarak kurtarma gibi belirli senaryolar için gereklidir. Ancak, VM geri yükleme yedekleme kasasından tam bir BMR yerini alır. Active Directory Geri Yükleme Modu'nda (DSRM), ayrıca tüm Active Directory Kurtarma senaryolarına uygun şekilde kullanılabilir. Daha fazla bilgi için lütfen denetleyin [yedekleme ve geri yükleme hakkında önemli noktalar sanallaştırılmış etki alanı denetleyicileri için](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) ve [için Active Directory orman Kurtarma planlaması](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Tek bir etki alanındaki tek DC
VM (tüm diğer VM gibi) Azure'dan geri yüklenebilir portal veya PowerShell kullanarak.

### <a name="multiple-dcs-in-a-single-domain"></a>Tek bir etki alanındaki birden çok DC'leri
Aynı etki alanının diğer DC'ler ağ üzerinden erişilebilir olduğunda, etki alanı denetleyicisi gibi herhangi bir VM geri yüklenebilir. Etki alanındaki son kalan DC olduğu veya kurtarma yalıtılmış bir ağda gerçekleştirilir, orman kurtarma yordamı gelmelidir.

### <a name="multiple-domains-in-one-forest"></a>Bir ormandaki birden çok etki alanları
Aynı etki alanının diğer DC'ler ağ üzerinden erişilebilir olduğunda, etki alanı denetleyicisi gibi herhangi bir VM geri yüklenebilir. Ancak, diğer tüm durumlarda bir orman kurtarma önerilir.

## <a name="restoring-vms-with-special-network-configurations"></a>Özel ağ yapılandırmaları ile sanal makineleri geri yükleme
Ve aşağıdaki özel ağ yapılandırmaları ile sanal makineleri geri mümkündür. Ancak, bu yapılandırmalar geri yükleme sürecinden sırasında bazı ayrıcalık gerektirir.

* Yük Dengeleyici (iç ve dış) altında yer alan VM'ler
* Birden çok ayrılmış IP ile sanal makineleri
* Birden çok NIC içeren VM'ler

> [!IMPORTANT]
> VM'ler için özel ağ yapılandırması oluştururken, sanal makineleri geri disklerden oluşturmak için PowerShell kullanmanız gerekir.
>
>

Tam olarak diske geri yükledikten sonra sanal makineleri yeniden için şu adımları izleyin:

1. Kurtarma Hizmetleri kasası kullanarak bir diskleri geri [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. Yük Dengeleyici için gereken VM yapılandırması oluştur / VM oluşturmak için istenen PowerShell cmdlet'lerini kullanarak, birden çok NIC/birden çok ayrılmış IP yapılandırması.

   * VM bulut hizmetiyle oluşturmak [iç yük dengeleyici](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Bağlanmak için VM oluşturma [Internet'e yönelik Yük Dengeleyici](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * VM oluşturma [birden çok NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * VM oluşturma [birden çok ayrılmış IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Sonraki adımlar
Vm'leriniz geri yükleyebilir, sanal makineler ile sık karşılaşılan hatalar hakkında bilgi için sorun giderme makalesine bakın. Ayrıca Vm'lerinizi görevlerle yönetme makaleyi göz atın.

* [Sorun giderme](backup-azure-vms-troubleshoot.md#restore)
* [Sanal makineleri yönetme](backup-azure-manage-vms.md)
