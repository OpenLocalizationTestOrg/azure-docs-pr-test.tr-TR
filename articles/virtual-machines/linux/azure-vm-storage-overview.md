---
title: aaaAzure Linux VM'ler ve Azure Storage | Microsoft Docs
description: "Azure standart ve Premium depolama ile yönetilen ve yönetilmeyen diskler ile Linux sanal makineleri açıklar."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: d364c69e-0bd1-4f80-9838-bbc0a95af48c
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 2/7/2017
ms.author: rasquill
ms.openlocfilehash: d34441698a4e59721847685099e5fb3aa378c597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-storage"></a>Azure ve Linux VM depolama
Azure Storage hello bulut depolama dayanıklılık, kullanılabilirlik ve ölçeklenebilirlik toomeet hello müşterilerin ihtiyaçlarını kullanan modern uygulamalar için çözümüdür.  Toplama toomaking içinde olası geliştiriciler toobuild büyük ölçekli uygulamalar toosupport yeni senaryolar için Azure Storage ayrıca hello depolama foundation Azure sanal makineler için sağlar.

## <a name="managed-disks"></a>Yönetilen Diskler

Kullanılabilir kullanarak Azure VM'ler şimdi olan [Azure yönetilen diskleri](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), sağlayan, toocreate Vm'leriniz oluşturma veya herhangi bir yönetme [Azure depolama hesapları](../../storage/common/storage-introduction.md) kendiniz. Premium istediğiniz veya standart depolama ve ne kadar büyük hello disk olmalıdır ve hello Azure VM diskleri sizin için oluşturduğu olup olmadığını belirtin. Yönetilen disklerle VM'ler dahil olmak üzere birçok önemli özelliklere sahiptir:

- Otomatik ölçeklenebilirlik desteği. Azure hello diskleri oluşturur ve abonelik başına 000 diskleri hello temel alınan depolama toosupport too10, Yukarı yönetir.
- Daha fazla güvenilirlik kullanılabilirlik kümeleri ile. Azure VM diskleri otomatik olarak birbirinden kullanılabilirlik kümeleri içinde yalıtılmış olduğundan emin olunmasını sağlar.
- Daha fazla erişim denetimi. Yönetilen disk işlemleri tarafından denetlenen çeşitli kullanıma [Azure rol tabanlı erişim denetimi (RBAC)](../../active-directory/role-based-access-control-what-is.md).

Yönetilen diskler için fiyatlandırma, yönetilmeyen diskleri için farklıdır. Bu bilgi için bkz: [fiyatlandırma ve faturalama yönetilen disklerde](../windows/managed-disks-overview.md#pricing-and-billing).

Yönetilmeyen diskleri yönetilen toouse disklerle kullanan VM'ler dönüştürebilirsiniz [az vm dönüştürme](/cli/azure/vm#convert). Daha fazla bilgi için bkz: [nasıl tooconvert bir Linux VM yönetilmeyenden tooAzure yönetilen diskleri](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Merhaba yönetilmeyen disk veya herhangi bir zamanda bırakıldı, kullanılarak şifrelenmiş bir depolama hesabında ise, bir yönetilmeyen disk yönetilen bir diske dönüştüremezsiniz [Azure depolama hizmeti şifreleme (SSE)](../../storage/common/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Merhaba aşağıdaki nasıl tootooconvert veya şifrelenmiş depolama hesabı olan diskleri yönetilmeyen ayrıntılı adımlar:

- Kopyalama hello sanal sabit disk (VHD) ile [az depolama blob kopyalama başlangıç](/cli/azure/storage/blob/copy#start) Azure depolama hizmeti şifrelemesi için hiçbir zaman etkinleştirilmiş tooa depolama hesabı.
- Yönetilen diskleri kullanan ve ile oluşturma sırasında bu VHD dosyasını belirtmek bir VM oluşturma [az vm oluşturma](/cli/azure/vm#create), veya
- Attach hello kopyalanan VHD ile [az vm diskini](/cli/azure/vm/disk#attach) tooa VM ile çalışan yönetilen diskleri.


## <a name="azure-storage-standard-and-premium"></a>Azure Storage: Standart ve Premium
Azure VM'ler--Yönetilen diskleri kullanarak olup olmadığını veya yönetilmeyen--standart depolama disklerini veya premium depolama diskleri yerleştirilmiş olabilir. Merhaba portal toochoose VM kullanırken bir açılan hello geçiş **Temelleri** ekran tooview standart ve premium diskler. Ne zaman basılı tooSSD, yalnızca etkin VM'ler gösterilir, premium storage SSD tarafından desteklenen tüm sürücüleri.  Ne zaman basılı tooHDD, disk sürücüleri dönmesini tarafından desteklenen standart depolama etkin VM'ler gösterilir, premium depolama Vm'leri SSD tarafından yedeklenen yanı sıra.

Bir VM hello oluşturulurken `azure-cli` hello aracılığıyla hello VM boyutu seçerken, standart ve premium arasında seçebilirsiniz `-z` veya `--vm-size` CLI bayrağı.

## <a name="creating-a-vm-with-a-managed-disk"></a>Bir VM ile yönetilen bir Disk oluşturma

Merhaba aşağıdaki örnek gerektirir hello yapabilecekleriniz Azure CLI 2.0 [burada yüklemek](/cli/azure/install-azure-cli).

İlk olarak, bir kaynak grubu toomanage hello kaynaklarla oluşturun [az grubu oluşturma](/cli/azure/group#create):

```azurecli
az group create --location westus --name myResourceGroup
```

Şimdi oluşturmak VM ile Merhaba [az vm oluşturma](/cli/azure/vm#create). Benzersiz bir belirtin `--public-ip-address-dns-name` bağımsız değişken olarak `mypublicdns` olasılıkla alınır.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns
```

Merhaba önceki örnek bir VM ile standart depolama hesabı yönetilen bir disk oluşturur. toouse bir Premium depolama hesabı ekleme hello `--storage-sku Premium_LRS` aşağıdaki örneğine hello gibi bağımsız değişkeni:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns \
    --storage-sku Premium_LRS
```

## <a name="standard-storage"></a>Standart depolama
Azure Standard Storage hello varsayılan depolama türüdür.  Standart depolama, kullanıcı hala devam ederken uygun maliyetli olması.  

## <a name="premium-storage"></a>Premium depolama
Azure Premium depolama g/Ç kullanımı yoğun iş yükleri çalıştıran sanal makineler için yüksek performanslı, düşük gecikmeli disk desteği sunar. Premium depolama kullanan sanal makine (VM) diskler katı hal sürücüleri (SSD) verileri depolar. Uygulamanızın VM diskleri tooAzure Premium depolama tootake avantajı hello hızına ve bu disklerin performansını geçirebilirsiniz.

Premium depolama özellikleri:

* Premium depolama diskleri: Azure Premium Storage ekli tooDS, DSv2 veya GS serisi Azure Vm'lerde VM diskleri destekler.
* Premium sayfa blobu: Premium Storage kullanılan toohold kalıcı diskler için Azure sanal makineler (VM'ler) Azure sayfa Bloblarını destekler.
* Premium yerel olarak yedekli depolama: Premium Storage hesabı yalnızca yerel olarak yedekli depolama (LRS) hello çoğaltma seçeneği olarak destekler ve tek bir bölge içinde hello veri üç kopyasını tutar.
* [Premium depolama](../../storage/common/storage-premium-storage.md)

## <a name="premium-storage-supported-vms"></a>Premium depolama Vm'leri desteklenen
Premium depolama destekleyen DS serisi, DSv2 serisi, GS serisi ve Fs-serisi Azure sanal makineleri (VM'ler). Premium depolama Vm'leri desteklenen standart ve Premium depolama diskleri kullanabilirsiniz. Ancak Premium Storage uyumlu olmayan VM serisiyle Premium depolama diskleri kullanamazsınız.

Merhaba Linux dağıtımları Premium Storage ile biz doğrulanan aşağıda verilmiştir.

| Dağıtım | Sürüm | Desteklenen çekirdek |
| --- | --- | --- |
| Ubuntu |12.04 |3.2.0-75.110+ |
| Ubuntu |14.04 |3.13.0-44.73+ |
| Debian |7.x, 8.x |3.16.7-ckt4-1+ |
| SLES |SLES 12 |3.12.36-38.1+ |
| SLES |SLES 11 SP4 |3.0.101-0.63.1+ |
| CoreOS |584.0.0+ |3.18.4+ |
| Centos |6.5, 6.6, 6.7, 7.0, 7.1 |3.10.0-229.1.2.el7+ |
| RHEL |6.8+, 7.2+ | |

## <a name="azure-file-storage"></a>Azure dosya depolama
Azure File storage hello bulutta hello standart SMB protokolünü kullanan dosya paylaşımları sağlar. Azure dosyaları ile dosya sunucuları tooAzure üzerinde kullanan kurumsal uygulamalar geçirebilirsiniz. Azure'da çalışan uygulamalar, Linux çalıştıran Azure sanal makinelerden dosya paylaşımları kolayca bağlayabilirsiniz. Ve hello en son sürümü File storage ile Ayrıca, SMB 3.0 destekleyen bir şirket içi uygulamasından bir dosya paylaşımı bağlayabilir.  Dosya paylaşımları SMB paylaşımları olduğundan bunlara standart dosya sistemi API'leriyle erişebilirsiniz.

Dosya depolama Blob, tablo ve kuyruk depolama dosya depolama hello kullanılabilirlik, dayanıklılık, ölçeklenebilirlik ve coğrafi yedeklilik, sağlamadığından aynı teknolojiye hello Azure depolama platformuna yerleşik hello yerleşik olarak bulunur. Azure Storage ölçeklenebilirlik ve performans hedefleri dosya depolama performans hedefleri ve sınırları hakkında daha fazla ayrıntı için bkz.

* [Nasıl toouse Linux Azure File storage](../../storage/files/storage-how-to-use-files-linux.md)

## <a name="hot-storage"></a>Sık erişimli depolama
Hello Azure sık erişimli depolama katmanı, sık erişilen verileri depolamak için en iyi duruma getirilmiştir.  Sık erişimli depolama hello varsayılan depolama blob depolarının türüdür.

## <a name="cool-storage"></a>Seyrek erişimli depolama
Hello Azure seyrek erişimli depolama katmanı, seyrek erişilen ve uzun süreli verileri depolamak için en iyi duruma getirilmiştir. Örnek kullanım durumları seyrek erişimli depolama için yedeklemeleri, medya içeriği, bilimsel verilerin, uyumluluk ve Arşiv verileri içerir. Genel olarak, nadiren erişilir herhangi bir veri seyrek erişimli depolama için mükemmel bir adaydır.

|  | Sık erişimli depolama katmanı | Seyrek erişimli depolama katmanı |
|:--- |:---:|:---:|
| Kullanılabilirlik |%99,9 |%99 |
| Kullanılabilirlik (RA-GRS okumaları) |%99,99 |%99,9 |
| Kullanım ücretleri |Daha yüksek depolama maliyetleri |Daha düşük depolama maliyetleri |
| Daha düşük erişim |Daha yüksek erişim | |
| ve işlem maliyetleri |ve işlem maliyetleri | |

## <a name="redundancy"></a>Yedeklilik
Microsoft Azure depolama hesabı her zaman olduğu Hello verilerde tooensure dayanıklılık ve yüksek kullanılabilirlik, hello Azure depolama SLA bile geçici donanım arızalarında hello yüzünü toplantı çoğaltılan.

Bir depolama hesabı oluşturduğunuzda, çoğaltma seçenekleri aşağıdaki hello birini seçmeniz gerekir:

* Yerel olarak yedekli depolama (LRS)
* Bölge olarak yedekli depolama (ZRS)
* Coğrafi olarak yedekli depolama (GRS)
* Okuma erişimli coğrafi olarak yedekli depolama (RA-GRS)

### <a name="locally-redundant-storage"></a>Yerel olarak yedekli depolama
Yerel olarak yedekli depolama (LRS) verilerinizi depolama hesabınız oluşturuldu hello bölgedeki çoğaltır. toomaximize dayanıklılık, depolama hesabınızdaki verilere karşı yapılan her isteği üç kez çoğaltılır. Bu üç çoğaltmaların her ayrı hata etki alanları ve yükseltme etki alanları bulunur.  Yalnızca yazılı tooall üç çoğaltmaları silindikten sonra isteği başarıyla döndürür.

### <a name="zone-redundant-storage"></a>Bölge olarak yedekli depolama
Bölge olarak yedekli depolama (ZRS) verilerinizi LRS daha fazla dayanıklılık sağlayan iki toothree olanakları, tek bir bölge içinde veya iki bölgede arasında çoğaltılır. Etkin ZRS depolama hesabınız varsa, verilerinizi hello tesis birinde hata hello durumda bile dayanıklı.

### <a name="geo-redundant-storage"></a>Coğrafi Olarak Yedekli Depolama
Coğrafi olarak yedekli depolama (GRS) hello birincil bölge çıktığınızda mil yüzlerce olduğundan, veri tooa ikincil bölge çoğaltır. Etkin GRS depolama hesabınız varsa, verilerinizi bile hello durumda tam bölgesel bir kesintinin veya hangi hello birincil bölge kurtarılamaz olağanüstü durum dayanıklı.

### <a name="read-access-geo-redundant-storage"></a>Coğrafi olarak yedekli depolamaya okuma erişimi
Okuma erişimli coğrafi olarak yedekli depolama (RA-GRS) salt okunur erişim toohello veri hello ikincil konumdaki Ayrıca iki bölgede toohello çoğaltma GRS tarafından sağlanan sağlayarak depolama hesabınız için kullanılabilirliği en üst düzeye çıkarır. Veri hello birincil bölgede kullanılamaz hale hello olayda uygulamanızı hello ikincil bölge ' verileri okuyabilir.

Azure Depolama artıklık bakın içine derinlemesine bir bakış için:

* [Azure Depolama çoğaltması](../../storage/common/storage-redundancy.md)

## <a name="scalability"></a>Ölçeklenebilirlik
Azure depolama depolamak ve yüzlerce terabaytlık veri toosupport hello büyük veri senaryolarını Bilimsel, finansal analiz ve medya uygulamalar tarafından gerekli işlem yüksek düzeyde ölçeklenebilir olduğundan. Veya hello küçük miktarda bir küçük işletmenin Web sitesi için gerekli veri depolayabilirsiniz. İhtiyaçlarınız ne olursa yalnızca, depoladığınız hello veri için ücret ödersiniz. Şu anda Azure Storage onlarca trilyon benzersiz müşteri nesnesi depolamaktadır ve saniyede ortalama olarak milyonlarca talebi ele alır.

Standart depolama hesapları için: bir standart depolama hesabı 20.000 IOPS en büyük toplam istek oranı vardır. Hello tüm standart depolama hesabındaki bir sanal makine disklerinizi toplam IOPS bu sınırını aşmamalıdır.

Premium depolama hesapları için: 50 GB/sn maksimum toplam üretilen iş oranını premium depolama hesabı vardır. Hello toplam verimlilik tüm VM disklerinizi bu sınırını aşmamalıdır.

## <a name="availability"></a>Kullanılabilirlik
En az % 99,99 (seyrek erişimli erişim katmanı için % 99,9) hello süre, biz başarıyla işlem istekleri tooread verileri okuma erişimi coğrafi olarak yedekli depolama (RA-GRS) hesaplarından olur, koşuluyla hello birincil bölge tooread verilerden denemeleri başarısız olduğundan, garanti ediyoruz Merhaba ikincil bölge üzerinde denenecek.

En az % 99,9 oranda (seyrek erişimli erişim katmanı için % 99) başlangıç saati, biz başarıyla olacağı garanti işlem istekleri tooread verileri yerel olarak yedekli depolama (LRS), bölge olarak yedekli depolama (ZRS) ve coğrafi olarak yedekli depolama (GRS) hesaplar.

En az % 99,9 oranda (seyrek erişimli erişim katmanı için % 99) başlangıç saati, biz başarıyla olacağı garanti işlem istekleri toowrite veri tooLocally yedekli depolama (LRS), bölge olarak yedekli depolama (ZRS) ve coğrafi olarak yedekli depolama (GRS) hesapları ve okuma erişimi coğrafi olarak yedekli Depolama (RA-GRS) hesabı.

* [Depolama için Azure SLA](https://azure.microsoft.com/support/legal/sla/storage/v1_1/)

## <a name="regions"></a>Bölgeler
Azure Merhaba Dünya 30 bölgelerdeki genel olarak kullanılabilir ve planları 4 ek bölgeler için bildirme. Coğrafi genişleme Azure için bir öncelik bizim müşteriler tooachieve daha yüksek performans sağlar ve Destek kendi gereksinimleri ve veri konumu ilgili tercihlerini nedeni.  Azures son bölge toolaunch içinde Almanya ' dir.

Merhaba Microsoft Cloud Almanya farklı seçeneği toohello Microsoft Cloud services zaten kullanılabilir Avrupa arasında yenilik artan olanaklarını ve ekonomik büyüme için yüksek oranda düzenlenen iş ortakları ve müşterileri Almanya oluşturma sağlar, Merhaba Avrupa Birliği (AB) ve hello Avrupa Serbest Ticaret ilişkilendirme (EFTA).

Bu yeni veri merkezlerinde, Magdeburg ve Frankfurt, müşteri verileri hello denetimi bir veri güvenliği, T-sistemleri uluslararası, bir bağımsız Almanca şirket ve Alman Telekom'ın altında yönetilir. Microsoft'un ticari bulut hizmetlerini bu veri merkezlerinde düzenlemelerini işleme tooGerman veri kalmayı ve müşteriler nasıl ve nerede veriler işlenir, ek seçenekler sağlar.

* [Harita Azure bölgeleri](https://azure.microsoft.com/regions/)

## <a name="security"></a>Güvenlik
Azure depolama toobuild güvenli uygulamalar birlikte, geliştiricilerin güvenlik özellikleri kapsamlı bir kümesini sağlar. Merhaba depolama hesabının kendisi rol tabanlı erişim denetimi ve Azure Active Directory kullanılarak güvenli hale getirilebilir. Verileri bir uygulama ile Azure arasında aktarımda istemci tarafı şifreleme, HTTPS veya SMB 3.0 kullanarak güvenli hale getirilebilir. Verileri otomatik olarak şifrelenir toobe ayarlanabilir zaman tooAzure depolama hizmeti şifreleme (SSE) kullanarak depolama yazılır. Sanal makineler tarafından kullanılan işletim sistemi ve veri diskleri Azure Disk şifrelemesi kullanılarak şifrelenmiş toobe ayarlayabilirsiniz. Azure depolama atanmış erişim toohello veri nesneleri, paylaşılan erişim imzaları kullanılarak verilebilir.

### <a name="management-plane-security"></a>Yönetim düzlemi güvenliği
Merhaba Yönetim düzeyi hello kullanılan kaynakları toomanage depolama hesabınız oluşur. Bu bölümde, biz hello Azure Resource Manager dağıtım modeli ve nasıl toouse rol tabanlı erişim denetimi (RBAC) toocontrol erişim tooyour depolama hesapları hakkında konuşun. Biz, depolama hesabı anahtarlarını yönetme hakkında konuşur ve nasıl tooregenerate bunları.

### <a name="data-plane-security"></a>Veri düzlemi güvenliği
Bu bölümde, biz erişim toohello gerçek veri nesneleri depolama hesabınızdaki BLOB'lar, dosyalar, kuyruklar ve tablolar gibi izin vermeyi paylaşılan erişim imzaları ve depolanan erişim ilkeleri kullanarak göreceğiz. Hizmet düzeyi SAS ve hesap düzeyinde SAS ele alınacaktır. Ayrıca nasıl toolimit erişim tooa belirli bir IP adresi (veya IP adresi aralığı) tooHTTPS toolimit hello protokolü kullanılan nasıl ve ne göreceğiz için bekleyen olmadan bir paylaşılan erişim imzası toorevoke tooexpire.

## <a name="encryption-in-transit"></a>Aktarımdaki şifreleme
Bu bölümde ele alınmaktadır nasıl içine veya dışına Azure Storage aktardığınızda toosecure veri. Azure dosya paylaşımları için SMB 3.0 tarafından kullanılan şifreleme HTTPS ve hello kullanımını önerilen hello hakkında konuşun. Biz de dışında depolama aktarıldıktan sonra bir istemci uygulamasında depolama alanına aktarılır önce tooencrypt hello verileri ve toodecrypt hello verileri sağlayan istemci tarafı şifreleme göz atın.

## <a name="encryption-at-rest"></a>Bekleyen şifreleme
Biz depolama hizmeti şifreleme (SSE) ve nasıl, blok blobları, sayfa bloblarını kaynaklanan bir depolama hesabı için etkinleştirmek ve ne zaman tooAzure depolama yazılmış ekleme blobları otomatik olarak Şifrelenmekte hakkında konuşur. Ayrıca Azure Disk şifrelemesi kullanın ve hello temel farklar ve istemci tarafı şifreleme karşı SSE karşı Disk şifrelemesi örneklerini keşfedin nasıl ele alacağız. Kısaca ABD için FIPS uyumluluk ele alacağız Kamu bilgisayarlar.

* [Azure depolama Güvenlik Kılavuzu](../../storage/common/storage-security-guide.md)

## <a name="temporary-disk"></a>Geçici disk
Her VM geçici disk içerir. Merhaba geçici disk uygulamalar ve işlemler için kısa vadeli depolama sağlar ve sayfa veya takas dosyaları gibi hedeflenen tooonly deposu veriler. Merhaba geçici disk üzerindeki verileri kaybolabilir sırasında bir [bakım olayı](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) veya ne zaman, [VM yeniden](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Merhaba VM standart yeniden sırasında hello geçici sürücüdeki hello verilerin kalıcı.

Linux sanal makinelerde hello genellikle disktir **/dev/sdb** ve biçimlendirilmiş ve çok takılı**/mnt** hello Azure Linux aracısı tarafından. Merhaba hello geçici diskin boyutunu, hello hello sanal makine boyutuna göre değişir. Daha fazla bilgi için bkz: [Linux sanal makineler için Boyutlar](sizes.md).

Azure hello geçici disk nasıl kullandığı hakkında daha fazla bilgi için bkz: [hello geçici sürücü Microsoft Azure sanal makineler üzerinde anlama](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="cost-savings"></a>Maliyet tasarrufları
* [Depolama maliyeti](https://azure.microsoft.com/pricing/details/storage/)
* [Depolama maliyeti hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/?service=storage)

## <a name="storage-limits"></a>Depolama sınırları
* [Depolama hizmet sınırları](../../azure-subscription-service-limits.md#storage-limits)
