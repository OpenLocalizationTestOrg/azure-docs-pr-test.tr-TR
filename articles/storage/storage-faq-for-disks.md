---
title: "Azure Iaas sanal diskler hakkında sık sorulan sorular (SSS) | Microsoft Docs"
description: "Azure Iaas sanal diskler ve (yönetilen ve yönetilmeyen) premium diskler hakkında sık sorulan sorular"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 9e5eed35334f1b95441b8181c8e90645be78b389
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a>Azure Iaas sanal diskler ve yönetilen ve yönetilmeyen premium diskler hakkında sık sorulan sorular

Bu makalede Azure yönetilen diskleri ve Azure Premium Storage hakkında sık sorulan bazı sorular yanıtlanmaktadır.

## <a name="managed-disks"></a>Yönetilen Diskler

**Azure yönetilen diskleri nedir?**

Yönetilen diskleri depolama hesabı yönetimini işleyerek Azure Iaas VM'ler için disk yönetimi basitleştiren bir özelliktir. Daha fazla bilgi için bkz: [yönetilen diskleri genel bakış](storage-managed-disks-overview.md).

**Standart yönetilen disk 80 GB olan varolan bir VHD'yi oluşturursanız, ne kadar bana maliyeti ne olacak?**

80 GB VHD'den oluşturulan standart yönetilen disk S10 disk olan bir sonraki kullanılabilir standart disk boyutu olarak kabul edilir. S10 disk fiyatlandırma göre ücret ödersiniz. Daha fazla bilgi edinmek için bkz. [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).

**Standart yönetilen disk için herhangi bir işlem maliyetleri vardır?**

Evet. Her işlem için ücret ödersiniz. Daha fazla bilgi edinmek için bkz. [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).

**Standart yönetilen disk için sağlanan disk kapasitesini veya disk üzerindeki verileri gerçek boyutu için t ücretlendirilir?**

Sağlanan disk kapasitesine göre ücret ödersiniz. Daha fazla bilgi edinmek için bkz. [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).

**Nasıl yönetilen premium diskleri yönetilmeyen disklerden farklı fiyatlandırma olduğu?**

Yönetilen premium diskleri fiyatlandırma yönetilmeyen premium diskleri aynı değil.

**Depolama hesabı türünü (standart veya Premium) yönetilen disklerim değiştirebilir miyim?**

Evet. Azure portalı, PowerShell veya Azure CLI kullanarak yönetilen disklerinizi depolama hesabı türünü değiştirebilirsiniz.

**I kopyalayın veya böylelikle bir özel depolama hesabına yönetilen bir disk verme bir yolu var mı?**

Evet. Azure portalı, PowerShell veya Azure CLI kullanarak yönetilen disklerinizi dışarı aktarabilirsiniz.

**Farklı bir abonelik ile yönetilen bir disk oluşturmak için Azure storage hesabı VHD dosyasında kullanabilir miyim?**

Hayır.

**Farklı bir bölgede yönetilen bir disk oluşturmak için Azure storage hesabı VHD dosyasında kullanabilir miyim?**

Hayır.

**Yönetilen diskler kullanan müşteriler için ölçek sınırlamalar var mı?**

Yönetilen diskleri depolama hesaplarıyla ilişkili sınırları ortadan kaldırır. Ancak, yönetilen disk başına abonelik sayısı 2. 000'varsayılan olarak sınırlıdır. Bu sayıyı artırmak için destek çağırabilirsiniz.

**Yönetilen bir diskin artımlı bir anlık görüntüsünü alın?**

Hayır. Geçerli anlık görüntü özelliği yönetilen bir disk tam bir kopyasını oluşturur. Ancak, biz artımlı anlık görüntüleri gelecekte destekler planlıyorsanız.

**Sanal makineleri bir kullanılabilirlik kümesinde yönetilen ve yönetilmeyen diskleri birleşiminden oluşabilir?**

Hayır. Sanal makineleri bir kullanılabilirlik kümesinde, tüm yönetilen diskleri veya tüm yönetilmeyen diskler kullanmanız gerekir. Bir kullanılabilirlik kümesi oluşturduğunuzda, kullanmak istediğiniz disk türünü seçebilirsiniz.

**Yönetilen diskleri Azure portalında varsayılan seçenektir?**

Şu anda değil ancak varsayılan gelecekte olacaktır.

**Boş bir yönetilen diski oluşturabilir miyim?**

Evet. Boş bir disk oluşturabilirsiniz. Yönetilen bir disk için bir VM eklemeden VM bağımsız olarak, örneğin, oluşturulabilir.

**Bir kullanılabilirlik için desteklenen hata etki alanı sayısı yönetilen diskleri kullanan ne ayarlı?**

Yönetilen diskleri kullanan kullanılabilirlik kümesi bulunduğu bağlı olarak, desteklenen hata etki alanı sayısı 2 veya 3 bölgedir.

**Nasıl Tanılama ayarlamak için standart depolama hesabı mı?**

VM tanılama için özel depolama hesabı ayarlayın. Gelecekte, tanılama yönetilen disklere de geçiş planlıyoruz.

**Ne tür bir rol tabanlı erişim denetimi desteğini yönetilen disklerde var mı?**

Diskleri desteklediği üç anahtar varsayılan rol yönetilen:

* Sahibi: erişim dahil her şeyi yönetebilir
* Katkıda bulunan: erişim dışında her şeyi yönetebilir
* Okuyucu: her şeyi görüntüleyebilir ancak değişiklik yapamaz

**I kopyalayın veya böylelikle bir özel depolama hesabına yönetilen bir disk verme bir yolu var mı?**

Yönetilen disk için bir salt okunur paylaşılan erişim imzası URI alın ve içeriği özel depolama hesabı veya şirket içi depolama birimine kopyalamak için kullanın.

**Yönetilen my disk kopyasını oluşturabilir miyim?**

Müşteriler kendi yönetilen diskleri bir anlık görüntüsünü ve sonra yönetilen başka bir disk oluşturmak için anlık görüntüyü kullanın.

**Yönetilmeyen diskleri hala desteklenmektedir?**

Evet. Yönetilen ve yönetilmeyen diskleri destekliyoruz. Yönetilen diskleri yeni iş yükleri için kullanın ve geçerli iş yüklerinizi yönetilen disklere geçirmenizi öneririz.


**128 GB disk oluşturun ve ardından 130 GB boyutunu artırın, ı sonraki disk boyutu (512 GB) ücretlendirilir?**

Evet.

**Yerel olarak yedekli depolama, coğrafi olarak yedekli depolama, oluşturabiliyorum ve bölge olarak yedekli depolama yönetilen disklerde?**

Azure yönetilen diskleri şu anda yönetilen yalnızca yerel olarak yedekli depolama disklerini destekler.

**Daraltma veya miyim yönetilen disklerim downsize?**

Hayır. Bu özellik şu anda desteklenmiyor. 

**Bilgisayar adı özelliği değiştirmek bir özel (Sistem Hazırlama aracı kullanılarak oluşturulan veya genelleştirilmiş) işletim sistemi diski VM sağlamak için kullanılır?**

Hayır. Bilgisayar adı özelliği güncelleştirilemiyor. Yeni VM, işletim sistemi diski oluşturmak için kullanılan VM üstten devralmaz. 

**Yönetilen disklerle VM'ler oluşturmak için örnek Azure Resource Manager şablonları nereden bulabilirim?**
* [Yönetilen diskleri kullanarak şablonları](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* https://github.com/chagarw/MDPP

## <a name="managed-disks-and-storage-service-encryption"></a>Diskler ve depolama hizmeti şifrelemesi yönetilen 

**Azure depolama hizmeti şifrelemesi, yönetilen bir disk oluşturduğunuzda, varsayılan olarak etkindir?**

Evet.

**Şifreleme anahtarları yöneten?**

Microsoft şifreleme anahtarları yönetir.

**I depolama hizmeti şifrelemesi yönetilen disklerim için devre dışı bırakabilirim?**

Hayır.

**Depolama hizmeti şifrelemesi, yalnızca belirli bölgelerde kullanılabilir?**

Hayır. Tarafından yönetilen diskleri kullanılabilir olduğu tüm bölgelerde kullanılabilir. Yönetilen diskleri kullanılabilir tüm genel bölgeler ve Almanya.

**Nasıl ı yönetilen my disk şifrelenir öğrenebilirsiniz?**

Yönetilen bir disk Azure portalı, Azure CLI ve PowerShell oluşturulduğu zaman bulabilirsiniz. Saat 9 Haziran 2017 sonra ise, disk şifrelenir. 

**10 Haziran 2017 önce oluşturulan mevcut disklerim nasıl şifreleyebilir mi?**

10 Haziran 2017 sürümünden itibaren varolan yönetilen diske yazılan yeni veriler otomatik olarak şifrelenir. Biz de var olan verileri şifrelemek planladığınıza ve şifreleme zaman uyumsuz olarak arka planda gerçekleşir. Var olan verileri artık şifrelemeniz gerekir, diskinizin bir kopyasını oluşturun. Yeni disk şifrelenir.

* [Azure CLI kullanarak yönetilen diskleri kopyalama](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [PowerShell kullanarak yönetilen diskleri kopyalama](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

**Yönetilen anlık görüntüler ve şifrelenmiş görüntüleri misiniz?**

Evet. Yönetilen tüm anlık görüntüler ve 9 Haziran 2017 sonra oluşturulan görüntüleri otomatik olarak şifrelenir. 

**Sanal makineleri veya yönetilen diskleri daha önce şifrelenmiş depolama hesaplarında yer alan yönetilmeyen disklerle dönüştürebilirsiniz?**

Evet

**Yönetilen bir disk veya bir anlık görüntü dışarı aktarılan bir VHD'den de şifrelenir mi?**

Hayır. Ancak, bir VHD şifrelenmiş depolama hesabı için bir şifrelenmiş dışa varsa disk veya anlık görüntü yönetilen sonra şifrelenir. 

## <a name="premium-disks-managed-and-unmanaged"></a>Premium diskler: yönetilen ve yönetilmeyen

**VM bir DSv2 gibi Premium Storage destekleyen bir boyutu serisi kullanıyorsa ı premium ve standart veri diskleri ekleyebilir miyim?** 

Evet.

**I premium ve standart veri diskleri Premium depolama D, Dv2, G veya F serisi gibi desteklemiyor boyutu seriye ekleyebilir miyim?**

Hayır. Premium Storage destekleyen bir boyutu serisi kullanmayan sanal makineleri yalnızca standart veri diskleri ekleyebilirsiniz.

**80 GB varolan bir VHD'den premium veri diski oluşturursanız, ne kadar maliyeti ne olacak?**

80 GB VHD'den oluşturulan bir premium veri diski P10 disk sonraki kullanılabilir premium disk boyutu kabul edilir. P10 disk fiyatlandırma göre ücret ödersiniz.

**Premium depolama kullanmak için işlem maliyetleri vardır?**

IOPS ve üretilen iş ile belirli sınırları sağlanan gelen her disk boyutu için sabit bir maliyeti yoktur. Diğer maliyetlerin giden bant genişliği ve anlık görüntü kapasite varsa ' dir. Daha fazla bilgi edinmek için bkz. [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage).

**IOPS ve disk önbellekten elde edebilirsiniz işleme sınırları nelerdir?**

Önbellek için birleşik sınırları ve DS serisi için yerel SSD çekirdek başına 4.000 IOPS ve çekirdek saniyede 33 MB kümesidir. GS serisi çekirdek başına 5.000 IOPS'yi ve çekirdek saniyede 50 MB sunar.

**Yerel SSD yönetilen diskleri VM için destekleniyor mu?**

Yerel SSD yönetilen diskleri VM ile birlikte sağlanan geçici depolama ' dir. Var. ek bu geçici depolama için bir maliyeti yoktur. Azure Blob depolama alanına kalıcı değildir çünkü, uygulama verilerini depolamak için bu yerel SSD kullanmamanızı öneririz.

**Premium disklerde KIRPMA kullanılmak herhangi varsa var mı?**

KIRPMA kullanın ya da premium Azure disklerde veya standart diskler üzerinde hiçbir dezavantajı yoktur.

## <a name="new-disk-sizes-managed-and-unmanaged"></a>Yeni disk boyutları: yönetilen ve yönetilmeyen

**İşletim sistemi ve veri diskleri için desteklenen en büyük disk boyutu nedir?**

Bir işletim sistemi diski için Azure destekleyen bölüm ana önyükleme kaydı (MBR) türüdür. MBR biçimini destekleyen bir diski 2 TB boyut. Bir işletim sistemi diski için Azure desteklediği en büyük boyutu 2 TB'tır. Azure veri diskleri için en fazla 4 TB destekler. 

**Desteklenen en büyük sayfa blob boyutu nedir?**

Azure desteklediği en büyük sayfa blob boyutu 8 TB (8191 GB) ' dir. Sayfa bloblarını 4 TB veri veya işletim sistemi disklerinde olarak bir VM'ye bağlı (4.095 GB) büyük desteklemiyoruz.

**Azure Araçları'nın yeni bir sürüm oluşturma, ekleme, yeniden boyutlandırma ve 1 TB'den büyük olan diskler karşıya yükleme için kullanılacak gerekiyor mu?**

Oluşturma, ekleme veya 1 TB'den büyük diskleri yeniden boyutlandırmak için varolan Azure Araçları yükseltmeniz gerekmez. VHD dosyasına şirket içi doğrudan Azure sayfa blobu veya yönetilmeyen disk olarak karşıya yükleme için en son aracı kümeleri kullanmanız gerekir:

|Azure Araçları      | Desteklenen sürümler                                |
|-----------------|---------------------------------------------------|
|Azure PowerShell | Sürüm numarası 4.1.0'da: Haziran 2017 sürüm veya daha yenisi|
|Azure CLI v1     | Sürüm numarası 0.10.13: May 2017 sürüm veya daha yenisi|
|AzCopy           | Sürüm numarası 6.1.0: Haziran 2017 sürüm veya daha yenisi|

Azure CLI v2 ve Azure Storage Gezgini desteği yakında geliyor. 

**P4 ve P6 disk boyutları yönetilmeyen diskleri veya sayfa BLOB'ları için destekleniyor mu?**

Hayır. P4 (32 GB) ve P6 (64 GB) disk boyutları, yalnızca yönetilen diskler için desteklenir. Yönetilmeyen diskleri ve sayfa bloblarını desteği yakında geliyor.

**Nasıl yönetilen my varolan premium (15 Haziran 2017) küçük bir disk etkinleştirilmeden önce 64 GB oluşturulduğu daha az disk varsa, onu faturalandırılır?**

Var olan küçük premium göre P10 fiyatlandırma katmanı faturalandırılmaya devam 64 GB daha az diskler. 

**64 GB P10 ile P4 veya P6 değerinden küçük premium diskler, disk katmanı nasıl geçiş yapabilirim?**

Küçük disklerinizi bir anlık görüntüsünü ve fiyatlandırma katmanı P4 veya P6 sağlanan boyutuna göre otomatik olarak geçiş yapmak için bir diski oluşturun. 


## <a name="what-if-my-question-isnt-answered-here"></a>Ne sorumun cevabı burada cevaplanıp değil mi?

Sorunuzun yanıtını burada listelenmiyorsa, bize bildirin ve yanıt bulmanıza yardımcı olacağız. Bir soru bu makalenin sonunda yer alan yorumlara nakledebilirsiniz. Azure depolama ekibi ve diğer topluluk üyeleri bu makale hakkında ile etkileşim için MSDN kullanın [Azure depolama Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).

Özellik isteğinde, istekleri ve için fikirleri göndermek için [Azure Storage geri bildirim Forumunda](https://feedback.azure.com/forums/217298-storage).
