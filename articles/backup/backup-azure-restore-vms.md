---
title: sanal makineler yedekten bir aaaRestore | Microsoft Docs
description: "Nasıl toorestore bir Azure sanal makinesi bir kurtarma noktası öğrenin"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "yedeklemeyi geri; nasıl toorestore; kurtarma noktası;"
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: 44c25f3248784accd1c2beaabb2c9a4dca3232d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-virtual-machines-in-azure"></a>Azure’da sanal makineleri geri yükleme
> [!div class="op_single_selector"]
> * [Azure portalında sanal makineleri geri yükleme](backup-azure-arm-restore-vms.md)
> * [Sanal makineleri Klasik portalda geri yükleme](backup-azure-restore-vms.md)
>
>

Yeni VM aşağıdaki hello ile bir Azure yedekleme kasasında depolanan hello yedeklerden adımlar bir sanal makine tooa geri yükleyin.

> [!IMPORTANT]
> Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> **15 Ekim 2017**, artık mümkün toouse PowerShell toocreate yedekleme kasaları olacaktır. <br/> **1 Kasım 2017'den itibaren**:
>- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
>- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.
>

## <a name="restore-workflow"></a>İş akışını geri yükle
### <a name="step-1-choose-an-item-toorestore"></a>1. adım: bir öğe toorestore seçin
1. Toohello gidin **korunan öğeler** sekmesi ve select hello toorestore tooa istediğiniz sanal makinenin yeni VM.

    ![Korumalı öğeler](./media/backup-azure-restore-vms/protected-items.png)

    Merhaba **kurtarma noktası** hello sütununda **korunan öğeler** sayfası, bir sanal makine için kurtarma noktası sayısı hello olmadığını bildirir. Merhaba **en yeni kurtarma noktası** sütun söyler, hello hello en son yedekleme, bir sanal makine geri yükleyebilirsiniz.
2. Tıklatın **geri** tooopen hello **öğeyi geri** Sihirbazı.

    ![Bir öğeyi geri yükle](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a>2. adım: bir kurtarma noktası seçin
1. Merhaba, **bir kurtarma noktası seçin** ekran, geri yükleyebilir, hello en yeni kurtarma noktasından veya önceki bir noktaya süre. Merhaba Sihirbazı açıldığında seçilen varsayılan seçenektir *en yeni kurtarma noktası*.

    ![Bir kurtarma noktası seçin](./media/backup-azure-restore-vms/select-recovery-point.png)
2. toopick, zaman içinde önceki bir nokta seçin hello **tarihi seçin** seçeneğini hello açılır ve bir tarih hello Takvim denetimi üzerinde hello tıklayarak **takvim simgesini**. Merhaba denetiminde kurtarma noktalarına sahip tüm tarihleri açık bir gri gölge ile doldurulur ve hello kullanıcı tarafından seçilebilen.

    ![Bir tarih seçin](./media/backup-azure-restore-vms/select-date.png)

    Bir tarih hello Takvim denetimi tıkladığınızda hello kurtarma kullanılabilir tarih kurtarma noktaları tabloda gösterilen işaret eder. Merhaba **zaman** sütun hangi Merhaba anlık görüntü alındığı hello saati belirtir. Merhaba **türü** sütunu görüntüler hello [tutarlılık](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) hello kurtarma noktası. Merhaba tablo üstbilgisi o gün parantez içinde kullanılabilir kurtarma noktaları hello sayısını gösterir.

    ![Kurtarma noktaları](./media/backup-azure-restore-vms/recovery-points.png)
3. Hello Hello kurtarma noktası seçin **kurtarma noktaları** tablo ve hello İleri okuna toogo toohello sonraki ekran'ı tıklatın.

### <a name="step-3-specify-a-destination-location"></a>3. adım: bir hedef konum belirtin
1. Merhaba, **seçin geri örneği** ekran nerede toorestore hello sanal makine ayrıntılarını belirtin.

   * Merhaba sanal makine adı belirtin: verilen bulut hizmetinde hello sanal makine adı benzersiz olmalıdır. Var olan VM aşırı yazma desteklemiyoruz.
   * Merhaba VM için bir bulut hizmeti seçin: Bu bir VM oluşturmak için zorunludur. Var olan bir bulut hizmetini tooeither Kullan'ı seçin veya yeni bir bulut hizmeti oluşturun.

        Herhangi bir bulut hizmeti adının çekilir küresel olarak benzersiz olmalıdır. Genellikle, hello bulut hizmeti adı [buluthizmeti] hello biçiminde bir genel kullanıma yönelik URL ile ilişkili alır. cloudapp.net. Merhaba adı zaten kullanıldı varsa azure toocreate yeni bir bulut hizmeti izin vermez. Yeni bir bulut hizmeti toocreate seçerseniz, olacaktır hello hello sanal makine olarak – hangi servis talebi hello VM ile aynı adı verilen ad çekilen uygulanan yeterince benzersiz toobe ilişkili toohello bulut hizmeti olması gerekir.

        Biz yalnızca bulut hizmetleri görüntülemek ve tüm hello benzeşim gruplarında ilişkili olmayan sanal ağları örnek ayrıntıları geri yükleyin. [Daha fazla bilgi edinin](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
2. Merhaba VM için bir depolama hesabı seçin: Bu hello VM oluşturmak için zorunludur. Var olan depolama hesaplarından hello aynı seçebileceğiniz bölge hello Azure yedekleme kasası olarak. Bölge olarak yedekli veya Premium depolama türü olan depolama hesapları desteklemiyoruz.

    Desteklenen yapılandırmaya sahip depolama hesabı varsa, Lütfen desteklenen yapılandırma önceki toostarting geri yükleme işlemi, bir depolama hesabı oluşturun.

    ![Sanal ağ seçin](./media/backup-azure-restore-vms/restore-sa.png)
3. Bir sanal ağı seçin: hello sanal ağ (VNET) hello sanal makine oluşturma hello zaman seçilebilir VM hello. Merhaba UI gösterir kullanılabilmesi için bu abonelik içindeki tüm hello sanal ağlar geri yükleyin. Bu zorunlu değildir tooselect VNET hello geri VM – üzerinden mümkün tooconnect geri toohello sanal makine olacaktır için hello Internet dahi hello VNET uygulanmaz.

    Merhaba bulut hello sanal ağ değiştirilemez sonra seçili hizmeti bir sanal ağ ile ilişkili ise.

    ![Sanal ağ seçin](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. Bir alt ağ seçin: hello ilk alt ağ hello VNET alt ağa sahip olmaması durumunda, varsayılan olarak seçilir. Tercih ettiğiniz Hello alt hello açılır seçeneklerden birini seçin. Alt ağ ayrıntılarını hello tooNetworks uzantısına gidin [portal giriş sayfasının](https://manage.windowsazure.com/), çok Git**sanal ağlar** ve select hello sanal ağ ve yapılandırma toosee alt ağ ayrıntıları aşağı ayrıntıya.

    ![Alt ağ seçin](./media/backup-azure-restore-vms/select-subnet.png)
5. Merhaba tıklatın **gönderme** hello Sihirbazı toosubmit simgesine hello ayrıntıları ve geri yükleme işi oluşturun.

## <a name="track-hello-restore-operation"></a>İzleme hello geri yükleme işlemi
Merhaba Geri Yükleme Sihirbazı'nı tüm hello bilgilerini girin ve gönderdikten sonra Azure Backup toocreate bir iş tootrack hello geri yükleme işlemi deneyin.

![Bir geri yükleme işi oluşturma](./media/backup-azure-restore-vms/create-restore-job.png)

Merhaba iş oluşturma başarılı olursa, o hello iş oluşturulur belirten bir bildirim bildirim görürsünüz. Merhaba tıklayarak daha fazla bilgi alabilirsiniz **işi görüntüle** çok sürer düğmesi**işleri** sekmesi.

![Geri yükleme işi oluşturuldu](./media/backup-azure-restore-vms/restore-job-created.png)

Merhaba geri yükleme işlemi tamamlandıktan sonra tamamlandı olarak işaretlenecek **işleri** sekmesi.

![Geri yükleme işi tamamlandı](./media/backup-azure-restore-vms/restore-job-complete.png)

Geri yükleme hello sonra sanal makine ihtiyacınız olabilecek mevcut toore yükleme hello uzantıları özgün VM hello ve [hello uç noktaları değiştirme](../virtual-machines/windows/classic/setup-endpoints.md) hello Azure portal hello sanal makine için.

## <a name="post-restore-steps"></a>Geri yükleme sonrası adımlar
Güvenlik nedenleriyle Ubuntu gibi bir bulut init göre Linux dağıtım kullanıyorsanız, parola engellenir geri yükleme sonrası. Lütfen kullanım hello VMAccess uzantısını VM çok geri[hello parola sıfırlama](../virtual-machines/linux/classic/reset-access.md). Parola post geri yükleme sıfırlama bu dağıtımları tooavoid üzerinde SSH anahtarları kullanmanızı öneririz.

## <a name="backup-for-restored-vms"></a>Geri yüklenen VM'ler için yedekleme
VM toosame bulut hizmetiyle aynı adı olarak ilk olarak VM yedeklemesi yedeklenen hello geri yüklediyseniz, yedekleme hello üzerinde VM post geri yükleme devam eder. VM tooa farklı bir bulut hizmeti geri veya geri yüklenen VM için farklı bir ad belirtilen varsa, bu yeni VM olarak kabul edilir ve geri yüklenen VM için toosetup yedekleme gerekiyor.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Bir VM sırasında Azure veri merkezi olağanüstü durum geri yükleme
Azure yedekleme, burada VM'ler deneyimleri olağanüstü durum çalıştırıyorsanız ve yedekleme kasası toobe coğrafi olarak yedekli yapılandırılmış hello birincil veri merkezi durumda VM'ler toohello eşleştirilmiş veri merkezi yedeklenen sağlar. Bu tür senaryoları sırasında hello geri yükleme işleminin geri kalanında aynı kalır ve tooselect eşleştirilmiş veri merkezinde mevcut olan bir depolama hesabı gerekir. Azure yedekleme eşleştirilmiş coğrafi toocreate geri hello sanal makine işlem hizmetinden kullanır. Daha fazla bilgi edinmek [Azure veri merkezi dayanıklılık](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Etki alanı denetleyicisi sanal makineleri geri yükleme
Etki alanı denetleyicisi (DC) sanal makinelerinin Azure yedekleme ile desteklenen bir senaryodur. Ancak, hello geri yükleme işlemi sırasında dikkatli olunması gerekir. Merhaba doğru geri yükleme işlemi hello hello etki alanı yapısına bağlıdır. Merhaba en basit durumda tek bir etki alanında tek bir DC sahip. Daha sık üretim yükleri, tek bir etki alanı birden çok DC'ler, belki de DC'lere ile şirket içinde gerekir. Son olarak, birden çok etki alanı içeren bir ormanda olabilir.

Bir Active Directory perspektif hello başka bir VM modern desteklenen bir hiper yöneticide Azure VM gibidir. Merhaba ana ile şirket içi hiper yöneticilerin VM konsolu ile Azure kullanılabilir olduğunu farktır. Bir konsol tam kurtarma (BMR) türü yedekleme kullanarak kurtarma gibi belirli senaryolar için gereklidir. Ancak, VM geri yükleme hello yedekleme Kasası'ndan tam bir BMR yerini alır. Active Directory Geri Yükleme Modu'nda (DSRM), ayrıca tüm Active Directory Kurtarma senaryolarına uygun şekilde kullanılabilir. Daha fazla bilgi için lütfen denetleyin [yedekleme ve geri yükleme hakkında önemli noktalar sanallaştırılmış etki alanı denetleyicileri için](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) ve [için Active Directory orman Kurtarma planlaması](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Tek bir etki alanındaki tek DC
Merhaba VM (tüm diğer VM gibi) hello Azure ' geri yüklenebilir portal veya PowerShell kullanarak.

### <a name="multiple-dcs-in-a-single-domain"></a>Tek bir etki alanındaki birden çok DC'leri
Ağ üzerinden aynı etki alanında ulaşılabilen Merhaba, diğer DC'ler Merhaba, hello DC gibi herhangi bir VM geri yüklenebilir. Merhaba etki alanındaki son kalan DC hello veya yalıtılmış bir ağda kurtarma gerçekleştirilen ise, orman kurtarma yordamı gelmelidir.

### <a name="multiple-domains-in-one-forest"></a>Bir ormandaki birden çok etki alanları
Ağ üzerinden aynı etki alanında ulaşılabilen Merhaba, diğer DC'ler Merhaba, hello DC gibi herhangi bir VM geri yüklenebilir. Ancak, diğer tüm durumlarda bir orman kurtarma önerilir.

<!--- WK: this following original supportability statement is incorrect, taking it out.
hello challenge arises because DSRM mode is not present in Azure. So toorestore such a VM, you cannot use hello Azure portal. hello only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use hello Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about hello [USN rollback problem](https://technet.microsoft.com/library/dd363553) and hello strategies suggested toofix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a>Özel ağ yapılandırmaları ile sanal makineleri geri yükleme
Azure yedekleme, sanal makinelerin özel ağ yapılandırmaları izlemek için yedeklemeyi destekler.

* Yük Dengeleyici (iç ve dış) altında yer alan VM'ler
* Birden çok ayrılmış IP ile sanal makineleri
* Birden çok NIC içeren VM'ler

Bu yapılandırmalar, bunları geri yükleme sırasında ilgili önemli noktalar aşağıdaki zorunlu kılabilir.

> [!TIP]
> Lütfen PowerShell tabanlı geri yükleme akış toorecreate hello özel ağ yapılandırması VM'ler post geri yükleme kullanın.
>
>

### <a name="restoring-from-hello-ui"></a>Merhaba UI ' geri yükleme:
Kullanıcı Arabiriminde, geri yükleme sırasında **her zaman yeni bir bulut hizmeti seçin**. Lütfen geri yükleme akışı sırasında yalnızca kullandığı zorunlu parametreler portal olduğundan VM'ler kullanıcı arabirimini kullanarak geri Not bunlar sahip hello özel ağ yapılandırması kaybedersiniz. Diğer bir deyişle, geri yükleme VM'ler yük dengeleyici veya çoklu yapılandırması olmadan normal VM'ler olacaktır NIC veya birden çok ayrılmış IP.

### <a name="restoring-from-powershell"></a>Powershell'den geri yükleme:
PowerShell hello VM diskleri yedekten geri yükleyin ve hello sanal makine oluşturma hello özelliği toojust sahiptir. Yukarıda belirtilen özel ağ yapılandırmaları gerektiren sanal makineler geri yüklerken yardımcı olur.

Sırayla toofully diskleri geri hello sanal makine post oluşturun, şu adımları izleyin:

1. Yedekleme kasası kullanarak Hello diskleri geri [Azure yedekleme PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)
2. Yük Dengeleyici için gerekli hello yapılandırması oluşturma / birden çok NIC/birden çok ayrılmış IP kullanarak ve PowerShell cmdlet'leri hello toocreate hello istenen yapılandırma VM kullanın.

   * VM bulut hizmetiyle oluşturmak [iç yük dengeleyici](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * VM tooconnect çok oluşturmak[Internet'e yönelik Yük Dengeleyici](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * VM oluşturma [birden çok NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * VM oluşturma [birden çok ayrılmış IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Sonraki adımlar
* [Sorun giderme](backup-azure-vms-troubleshoot.md#restore)
* [Sanal makineleri yönetme](backup-azure-manage-vms.md)
