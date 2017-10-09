---
title: "aaaWindows sanal makinelere genel bakış | Microsoft Docs"
description: "Azure’da Windows sanal makineler oluşturma ve yönetme hakkında bilgi edinin."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: fbae9c8e-2341-4ed0-bb20-fd4debb2f9ca
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 8015b1aa4bcdaac2e721f25d85a5bc995a22f0f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-windows-virtual-machines-in-azure"></a>Azure’da Windows sanal makinelere genel bakış

Azure Virtual Machines (VM) Azure’un sunduğu [isteğe bağlı ve ölçeklenebilir işlem kaynağı türlerinden](../../app-service-web/choose-web-site-cloud-service-vm.md) biridir. Genellikle, hello bilgi işlem ortamı üzerinden hello diğer seçimlere daha fazla denetime ihtiyacınız olduğunda bir VM seçin. Bu makalede VM oluşturmadan önce dikkat etmeniz gereken bilgilere, oluşturma yöntemine ve yönetim seçeneklerine yer verilmiştir.

Sanallaştırma esnekliği toobuy gerek kalmadan hello ve hello fiziksel donanım korumak bir Azure VM sağlar, bu çalıştırır. Ancak, yine toomaintain hello VM yapılandırma, düzeltme eki uygulama ve bunun üzerinde çalıştırılır hello yazılım yükleme gibi görevleri gerçekleştirerek gerekir.

Azure sanal makineleri farklı amaçlarla kullanılabilir. Bazı örnekler şunlardır:

* **Geliştirme ve test** – Azure VM'ler sunan bir hızlı ve kolay bir yolu toocreate belirli yapılandırmalarla bir bilgisayarı gerekli toocode ve bir uygulamayı test etme.
* **Merhaba bulut uygulamalarında** – uygulamanız için isteğe bağlı dalgalanma çünkü mantıklı toorun yapabileceğiniz azure'da VM üzerinde. İhtiyaç duyduğunuzda oluşturulan ek VM’ler için ödeme yapar, ihtiyaç kalmadığında bunları kapatırsınız.
* **Veri Merkezi Genişletilmiş** – Azure sanal ağı sanal makinelere bağlı tooyour kuruluşun ağına kolayca olabilir.

ölçeği artırabilirsiniz ve toowhatever gerekli toomeet gereksinimlerinizi olduğundan, uygulamanızın kullandığı VM'ler Hello sayısıdır.

## <a name="what-do-i-need-toothink-about-before-creating-a-vm"></a>Ne hakkında toothink VM oluşturmadan önce ihtiyacım var mı?
Azure’da uygulama altyapısı oluştururken [dikkate almanız gereken tasarım ölçütleri](/architecture/reference-architectures/virtual-machines-linux?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) vardır. Başlamadan önce bu VM yönlerini hakkında önemli toothink şunlardır:

* Uygulama kaynaklarınızın Hello adları
* Merhaba kaynakları depolandığı hello konumu
* Merhaba VM Hello boyutu
* oluşturulabilir VM'ler Hello sayısı
* VM hello bir Hello işletim sistemi
* Merhaba başladıktan sonra VM Hello yapılandırması
* Merhaba VM gereken bu hello ilgili başka kaynaklar

### <a name="naming"></a>Adlandırma
Bir sanal makinenin bir [adı](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) atanan tooit ve hello işletim sisteminin bir parçası olarak yapılandırılan bir bilgisayar adı vardır. bir VM Hello adını too15 karakter olabilir.

Merhaba sanal makine adı Azure toocreate hello işletim sistemi diski, hello bilgisayar adı kullanın ve aynı hello. Varsa, [karşıya yükleme ve kendi görüntünüzü kullanma](upload-generalized-managed.md) önceden yapılandırılmış bir işletim sistemini içeren ve toocreate bir sanal makine kullanın, hello adları farklı olabilir. Kendi görüntü dosyasını karşıya yüklediğinde, hello hello işletim sisteminde bilgisayar adını ve aynı hello hello sanal makine adı yapmanızı öneririz.

### <a name="locations"></a>Konumlar
Azure içinde oluşturulan tüm kaynakları çok sayıda sunucuya dağıtılmış [coğrafi bölgeler](https://azure.microsoft.com/regions/) Merhaba Dünya. Genellikle, hello Bölge adlı **konumu** bir VM oluştururken. Bir VM için sanal sabit diskleri hello depolandığı hello konumunu belirtir.

Bu tablo kullanılabilir konumların bir listesini alabilirsiniz hello yollardan bazılarını gösterir.

| Yöntem | Açıklama |
| --- | --- |
| Azure portalına |Bir VM oluştururken hello listeden bir konum seçin. |
| Azure PowerShell |Kullanım hello [Get-AzureRmLocation](/powershell/module/azurerm.resources/get-azurermlocation) komutu. |
| REST API |Kullanım hello [listesinde konumları](https://docs.microsoft.com/rest/api/resources/subscriptions#Subscriptions_ListLocations) işlemi. |

### <a name="vm-size"></a>VM boyutu
Merhaba [boyutu](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Merhaba kullandığınız VM hello iş yükü tarafından toorun istediğiniz belirlenir. Seçtiğiniz hello boyutu sonra güç, bellek ve depolama kapasitesi işleme gibi Etkenler belirler. Azure çok çeşitli boyutlarda toosupport sayıda kullanım türünü sunar.

Azure ücretleri bir [saatlik fiyat](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) hello VM'nin boyutu ve işletim sistemi temelinde. Kısmi saatler için yalnızca kullanılan hello dakika için Azure ücretlidir. Depolama ayrı olarak fiyatlandırılır ve ücretlendirilir.

### <a name="vm-limits"></a>VM Sınırları
Aboneliğiniz varsayılan sahip [kota sınırları](../../azure-subscription-service-limits.md) yerinde projeniz için birçok VM hello dağıtımını etkileyebilir. Hello geçerli bir abonelik başına temelinde bölge başına 20 VM sınırıdır. Sınırların yükseltilmesini talep etmek için destek bileti oluşturabilirsiniz.

### <a name="operating-system-disks-and-images"></a>İşletim sistemi diskleri ve görüntüleri
Sanal makineler kullanın [sanal sabit diskleri (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toostore veri ve işletim sistemi (OS). VHD bir işletim sistemi tooinstall seçebilirsiniz hello görüntüleri için de kullanılır. 

Azure sağlayan birçok [Market görüntülerini](https://azure.microsoft.com/marketplace/virtual-machines/) toouse çeşitli sürümleri ve Windows Server işletim sistemleri türleri. Market görüntüleri; görüntü yayımcısı, teklif, sku ve sürüm (genelde sürüm en son belirtilir) bilgileriyle tanımlanır. 

Bu tablo bir resmi için hello bilgileri bulabilirsiniz bazı yollarını gösterir.

| Yöntem | Açıklama |
| --- | --- |
| Azure portalına |bir görüntü toouse seçtiğinizde hello değerleri sizin için otomatik olarak belirtilir. |
| Azure PowerShell |[Get-AzureRMVMImagePublisher](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimagepublisher) -Location "konum"<BR>[Get-AzureRMVMImageOffer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimageoffer) -Location "konum" -Publisher "yayımcıAdı"<BR>[Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) -Location "konum" -Publisher "yayımcıAdı" -Offer "teklifAdı" |
| REST API'leri |[Görüntü yayımcılarını listeleme](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publishers)<BR>[Görüntü tekliflerini listeleme](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offers)<BR>[Görüntü sku’larını listeleme](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offer-skus) |

Çok seçebilirsiniz[karşıya yükleme ve kendi görüntünüzü kullanma](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account) ve bunu yaptığınızda hello Yayımcı adı, teklif ve sku kullanılmaz.

### <a name="extensions"></a>Uzantılar
VM [uzantıları](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), dağıtım sonrası yapılandırma ve otomatik görevlerle VM’nize yeni özellikler ekler.

Uzantıları kullanarak şu genel görevleri gerçekleştirebilirsiniz:

* **Özel komut dosyalarını Çalıştır** – hello [özel betik uzantısı](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello VM sağlandığında, komut dosyasını çalıştırarak hello VM üzerinde iş yükleri yapılandırmanıza yardımcı olur.
* **Dağıtma ve yapılandırmalarını yönetme** – hello [PowerShell istenen durum yapılandırması (DSC) uzantısı](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) yardımcı olan bir VM toomanage DSC ayarlamak yapılandırmalarını ve ortamları.
* **Tanılama verilerini toplamak** – hello [Azure tanılama uzantısını](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) kullanılan toomonitor olabilir hello VM toocollect tanılama verilerini yapılandırdığınız yardımcı olur, uygulamanızın durumunu hello.

### <a name="related-resources"></a>İlgili kaynaklar
Bu tabloda Hello kaynakları hello VM tarafından kullanılır ve tooexist gerekir veya hello VM oluşturulduğunda.

| Kaynak | Gerekli | Açıklama |
| --- | --- | --- |
| [Kaynak grubu](../../azure-resource-manager/resource-group-overview.md) |Evet |Merhaba VM bir kaynak grubunda yer alması gerekir. |
| [Depolama hesabı](../../storage/common/storage-create-storage-account.md) |Evet |Merhaba VM sanal sabit diskleri hello depolama hesabı toostore gerekir. |
| [Sanal ağ](../../virtual-network/virtual-networks-overview.md) |Evet |Merhaba VM sanal ağ bir üyesi olması gerekir. |
| [Genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) |Hayır |Merhaba VM erişim bir ortak IP adresi atanmış tooit tooremotely olabilir. |
| [Ağ arabirimi](../../virtual-network/virtual-network-network-interface.md) |Evet |Merhaba VM hello ağ arabirimi toocommunicate hello ağındaki gerekir. |
| [Veri diskleri](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |Hayır |Merhaba VM veri diskleri tooexpand depolama özellikleri ekleyebilirsiniz. |

## <a name="how-do-i-create-my-first-vm"></a>İlk VM’mi nasıl oluşturabilirim?
İlk VM’nizi oluşturmak için kullanabileceğiniz birden fazla yöntem vardır. içinde bulunduğunuz hello ortamda yaptığınız hello seçim bağlıdır. 

Bu tablo bilgileri tooget VM oluşturmaya başlamanızı sağlar.

| Yöntem | Makale |
| --- | --- |
| Azure portalına |[Hello portal kullanarak Windows çalıştıran bir sanal makine oluşturma](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Şablonlar |[Resource Manager şablonu kullanarak Windows sanal makine oluşturma](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure PowerShell |[PowerShell kullanarak Windows VM oluşturma](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| İstemci SDK'ları |[C# kullanarak Azure Kaynaklarını dağıtma](csharp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| REST API'leri |[VM oluşturma veya güncelleştirme](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-create-or-update) |

Hiç istemeyiz ama bazen ters giden bir şeyler olabilir. Bu durum tooyou olursa, hello bilgilerinde bakın [Azure'da Windows sanal makine oluşturma ile ilgili sorunları giderme Resource Manager dağıtım sorunları](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="how-do-i-manage-hello-vm-that-i-created"></a>Merhaba oluşturduğum VM nasıl yönetebilirim?
VM’ler tarayıcı tabanlı bir portal, betik oluşturma desteğine sahip komut satırı araçları kullanılarak veya doğrudan API’ler aracılığıyla yönetilebilir. Gerçekleştirebileceğiniz bazı tipik yönetim görevleri tooa kullanılabilirlik yönetme ve yedekleme yapmak VM üzerinde oturum bir VM hakkında bilgi alma.

### <a name="get-information-about-a-vm"></a>VM hakkında bilgi alma
Bu tablo bir VM hakkında bilgi edinebilirsiniz hello yollardan bazılarını gösterir.

| Yöntem | Açıklama |
| --- | --- |
| Azure portalına |Merhaba hub menüsünde **sanal makineleri** ve ardından hello VM hello listeden seçin. Merhaba dikey penceresinde hello VM, erişim toooverview bilgileri, değerleri ayarlama ve izleme ölçümleri sahip. |
| Azure PowerShell |PowerShell toomanage sanal makineleri kullanma hakkında daha fazla bilgi için bkz: [oluşturma ve hello Azure PowerShell modülü ile Windows sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| REST API |Kullanım hello [VM Al bilgi](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) VM hakkında işlemi tooget bilgi. |
| İstemci SDK'ları |C# toomanage sanal makineleri kullanma hakkında daha fazla bilgi için bkz: [yönetmek Azure Azure Resource Manager ve C# kullanarak sanal makineleri](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |

### <a name="log-on-toohello-vm"></a>VM toohello üzerinde oturum
Merhaba Bağlan düğmesi hello Azure portal çok kullandığınız[bir Uzak Masaüstü (RDP) oturumu başlatmak](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Şeyler bazen toouse uzak bağlantı çalışırken yanlış gidebilirsiniz. Bu durum tooyou olursa, hello Yardım bilgileri kullanıma [sorun giderme Uzak Masaüstü bağlantıları tooan Azure Windows çalıştıran sanal makine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="manage-availability"></a>Kullanılabilirliği yönetme
Nasıl çok, toounderstand daha önemlidir[yüksek kullanılabilirlik sağlamak](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) uygulamanız için. Bu yapılandırma, en az bir çalışan birden çok sanal makineleri tooensure oluşturursunuz.

Bizim 99.95 VM hizmet düzeyi sözleşmesi için dağıtım tooqualify için sırayla yükünüzü içinde çalışan iki veya daha fazla VM toodeploy gereken bir [kullanılabilirlik kümesi](tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Bu yapılandırma, VM’lerinizin birden fazla hata etki alanına dağıtılmasını ve dağıtımlarının farklı bakım aralıklarına sahip ana bilgisayarlara yapılmasını sağlar. Merhaba tam [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) açıklayan bir bütün olarak Azure kullanılabilirliğini garanti hello.

### <a name="back-up-hello-vm"></a>VM Hello yedekleyin
A [kurtarma Hizmetleri kasası](../../backup/backup-introduction-to-azure-backup.md) kullanılan tooprotect veri ve Azure Backup ve Azure Site Recovery Services varlıklar. Kurtarma Hizmetleri kasası kullanabileceğine[dağıtma ve PowerShell kullanarak Resource Manager tarafından dağıtılan VM'ler için yedeklemeleri yönetme](../../backup/backup-azure-vms-automation.md). 

## <a name="next-steps"></a>Sonraki adımlar
* Maksadınızı Linux VM'ler ile toowork ise, bakmak [Azure ve Linux](../linux/overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Merhaba altyapınızda ayarlama geçici hello yönergeleri hakkında daha fazla bilgi [örnek Azure altyapı izlenecek](infrastructure-example.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
