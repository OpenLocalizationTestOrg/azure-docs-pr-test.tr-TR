---
title: "aaaUse artımlı anlık görüntüleri yedekleme ve kurtarma yönetilmeyen Azure VM disklerinin | Microsoft Docs"
description: "Yedekleme ve kurtarma artımlı anlık görüntülerini kullanarak Azure sanal makine disklerinizi için özel bir çözüm oluşturun."
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: 3524b987-bd65-4e35-83e7-fbc2136643e5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: aungoo
ms.openlocfilehash: 6d3e6d78e953f77a1028ac35dcde1ef046dbc3bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-unmanaged-vm-disks-with-incremental-snapshots"></a>Artımlı anlık görüntüleri ile Azure yönetilmeyen VM diskleri yedekleyin
## <a name="overview"></a>Genel Bakış
Azure Storage blobları tootake anlık görüntülerini hello yeteneği sağlar. Anlık görüntüler zamandaki o noktada hello blob durumu yakalayın. Bu makalede, biz anlık görüntülerini kullanarak sanal makine disklerinin yedeklerini nasıl koruyabilirsiniz bir senaryoyu açıklar. Değil toouse seçtiğinizde, bu yöntemi kullanabilirsiniz Azure yedekleme ve kurtarma hizmeti ve istek toocreate, sanal makine diskleriniz için özel bir yedekleme stratejisi.

Azure virtual machine diskleri sayfa blobları Azure storage'da olarak depolanır. Bu makalede sanal makine disklerini yedekleme stratejisi hakkında varsayılır olduğundan, biz toosnapshots sayfa bloblarını hello bağlamında başvuran. Anlık görüntüler hakkında daha fazla toolearn başvurmak çok[Blob anlık görüntüsünün oluşturulmasına](https://msdn.microsoft.com/library/azure/hh488361.aspx).

## <a name="what-is-a-snapshot"></a>Bir anlık görüntü nedir?
Bir blob anlık bir noktada zamanında yakalanan bir blob, salt okunur bir sürümüdür. Bir anlık görüntü oluşturulduktan sonra okumak, kopyalanan, veya silinmiş, ancak değişiklik. Bir anda göründüğü gibi anlık bir blob yukarı şekilde tooback sağlar. Sürüm 2015-04-05 REST kadar hello özelliği toocopy tam anlık görüntüleri içeriyor. Ayrıca hello REST sürüm 2015-07-08 ve üstü ile, artımlı anlık görüntüleri kopyalayabilirsiniz.

## <a name="full-snapshot-copy"></a>Tam anlık görüntü kopyalama
Anlık görüntü olabilir tooanother depolama hesabı hello temel blobu blob tookeep yedeklerini kopyalanır. Merhaba blob tooan geri yüklemeyi gibi kendi temel blob üzerinden bir anlık görüntü kopyalayabilirsiniz önceki sürümü. Bir anlık görüntü bir depolama hesabı tooanother kopyalandığında, aynı hello temel sayfa blob'u olarak boşluk hello dolduracaktır. Bu nedenle, bir depolama hesabı tooanother tüm anlık görüntüleri kopyalama yavaş olacaktır ve ayrıca çok fazla alan hello hedef depolama hesabındaki tüketir.

> [!NOTE]
> Merhaba temel blob tooanother hedef kopyalarsanız, hello blob hello anlık görüntüleri onunla birlikte kopyalanmaz. Benzer şekilde, bir kopya ile temel bir blob üzerine hello temel blob ile ilişkili anlık görüntüleri etkilenmez ve temel blob adı altında olduğu gibi kalır.
> 
> 

### <a name="back-up-disks-using-snapshots"></a>Diskleri anlık görüntülerini kullanarak yedekleme
Sanal makine diskleriniz için bir yedekleme stratejisi da hello disk ya da sayfa blob düzenli anlık görüntülerini almak ve bunları gibi araçları kullanarak tooanother depolama hesabı kopyalayın [kopyalama Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) işlemi veya [AzCopy](storage-use-azcopy.md). Bir anlık görüntü tooa hedef sayfa blob'u farklı bir adla kopyalayabilirsiniz. Merhaba elde edilen hedef sayfa blobu yazılabilir sayfa blobu ve anlık görüntü olmayan ' dir. Bu makalenin sonraki bölümlerinde biz adımları tootake anlık görüntülerini kullanarak sanal makine disklerinin yedeklerini anlatmaktadır.

### <a name="restore-disks-using-snapshots"></a>Anlık görüntülerini kullanarak disklerini geri yükle
Disk tooa önceki kararlı sürümünü hello yedekleme anlık görüntülerinin birinde yakalanan zaman toorestore olduğunda, bir anlık görüntü hello temel sayfa blobu kopyalayabilirsiniz. Yükseltilen toohello temel sayfa blobu Hello anlık görüntü olduktan sonra anlık görüntü kalır hello ancak kaynağı, hem okuma ve yazılabilir bir kopya ile üzerine yazılır. Bu makalenin sonraki bölümlerinde biz adımları toorestore kendi anlık görüntüsünü diskinizden önceki bir sürümünü anlatmaktadır.

### <a name="implementing-full-snapshot-copy"></a>Tam anlık görüntü kopyalama uygulama
Merhaba aşağıdakileri yaparak tam anlık görüntü kopyalama uygulayabilir,

* İlk olarak, hello temel blob hello kullanarak bir anlık görüntüsünü [anlık görüntü Blob](https://msdn.microsoft.com/library/azure/ee691971.aspx) işlemi.
* Ardından, kopyalama hello anlık görüntü tooa hedef depolama hesabı kullanılarak [kopyalama Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx).
* Bu işlem toomaintain yedek kopyalarını temel blob yineleyin.

## <a name="incremental-snapshot-copy"></a>Artımlı anlık görüntü kopyalama
Merhaba yeni özellik [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx) API'si, bir çok daha iyi şekilde tooback sayfa BLOB'ları veya diskleri hello anlık görüntüleri yedekleme sağlar. Merhaba API hello temel blob ve hello anlık görüntüleri değişiklikleri hello listesini döndürür. Bu hello hello yedekleme hesabında kullanılan depolama alanı miktarını azaltır. Merhaba API standart depolama yanı sıra Premium depolama üzerinde sayfa bloblarını destekler. Bu API kullanarak Azure VM'ler için daha hızlı ve verimli yedekleme çözümleri şimdi oluşturabilirsiniz. Bu hello REST sürüm 2015-07-08 ile kullanılabilir ve daha yüksek olur.

Artımlı anlık görüntü kopyalama toocopy gelen bir depolama hesabı tooanother hello arasındaki farkı verir,

* Temel blob ve onun anlık görüntü veya
* Merhaba temel BLOB iki tüm anlık görüntüleri

Aşağıdaki koşullar hello karşılandığından sağlanan

* Merhaba blob Oca 1 2016 veya sonraki bir sürümünde oluşturulmuş.
* Merhaba blob ile üzerine [PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) veya [kopyalama Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) arasında iki anlık görüntüler.

**Not**: Bu özellik Premium ve standart Azure sayfa BLOB'ları için kullanılabilir.

Bir depolama hesabı tooanother hello anlık görüntü kopyalama anlık görüntüleri kullanan özel bir yedekleme stratejisi olduğunda çok yavaş olabilir ve çok miktarda depolama alanı kullanır. Merhaba tüm anlık görüntü tooa yedekleme depolama hesabı kopyalamak yerine art arda gelen anlık görüntüleri tooa yedekleme sayfa blobu hello birbirinden yazabilirsiniz. Bu şekilde hello zaman toocopy ve alan toostore yedeklemelerini önemli ölçüde azaltılır.

### <a name="implementing-incremental-snapshot-copy"></a>Uygulama artımlı anlık görüntü kopyalama
Merhaba aşağıdakileri yaparak artımlı anlık görüntü kopyalama uygulayabilir,

* Temel blob hello kullanmanın bir anlık görüntüsünü [anlık görüntü Blob](https://msdn.microsoft.com/library/azure/ee691971.aspx).
* Kopya hello anlık görüntü toohello hedef yedekleme depolama hesabı kullanılarak [kopyalama Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx). Bu hello yedekleme sayfa blobu olacaktır. Bu yedekleme sayfa blobu bir anlık görüntüsünü ve yedekleme hesabında depolayın.
* Merhaba temel BLOB anlık görüntü Blob kullanarak başka bir anlık görüntü alın.
* Temel blob kullanmanın ilk ve ikinci anlık görüntüleri Hello birbirinden alma [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx). Merhaba yeni parametresini kullanın **prevsnapshot** toospecify hello tooget hello farkı hello anlık görüntüsünü DateTime değeri. Bu parametre mevcut olduğunda hello REST yanıt hedef anlık görüntüsü ile Temizle sayfalar dahil olmak üzere önceki anlık arasında değiştirilen hello sayfalar içerir.
* Kullanım [PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) tooapply bu değişiklikleri toohello yedekleme sayfa blobu.
* Son olarak, hello yedekleme sayfa blobu bir anlık görüntüsünü ve hello yedekleme depolama hesabında saklayın.

Merhaba sonraki bölümde, biz daha ayrıntılı olarak artımlı anlık görüntü kopyalama kullanarak diskleri yedeklerini nasıl koruyabilirsiniz anlatmaktadır

## <a name="scenario"></a>Senaryo
Bu bölümde biz anlık görüntülerini kullanarak sanal makine disklerini için özel bir yedekleme stratejisi içeren bir senaryo açıklanmaktadır.

DS serisi Azure VM'ye bağlı premium depolama P30 diskle göz önünde bulundurun. adlı hello P30 diske *mypremiumdisk* adlı bir premium depolama hesabında depolanan *mypremiumaccount*. Standart depolama hesabı olarak adlandırılan *mybackupstdaccount* hello yedeğini depolamak için kullanılacak *mypremiumdisk*. Tookeep bir anlık görüntü isteriz, *mypremiumdisk* 12 saatte bir.

Depolama hesabı ve diskleri oluşturma hakkında daha fazla toolearn başvurmak çok[Azure storage hesapları hakkında](storage-create-storage-account.md).

Azure VM'lerin yedeklenmesi hakkında toolearn başvurmak çok[planlama Azure VM yedeklemeleri](../backup/backup-azure-vms-introduction.md).

## <a name="steps-toomaintain-backups-of-a-disk-using-incremental-snapshots"></a>Artımlı anlık görüntülerini kullanarak bir disk adımları toomaintain yedekleri
Merhaba aşağıda açıklanan adımları anlık görüntülerini uygulayacaktır *mypremiumdisk* ve hello yedeklemelerin sürdürmek *mybackupstdaccount*. Merhaba yedekleme adlı bir standart sayfa blob'u olacaktır *mybackupstdpageblob*. Merhaba yedekleme sayfa blobu her zaman aynı durum hello son anlık görüntüsü olarak hello yansıtılacaktır *mypremiumdisk*.

1. İlk olarak hello yedekleme sayfa blobu, premium depolama diski oluşturun. toodo Bu, Al anlık görüntüsü *mypremiumdisk* adlı *mypremiumdisk_ss1*.
2. Bu anlık görüntü toomybackupstdaccount adlı bir sayfa blob'u olarak kopyalamak *mybackupstdpageblob*.
3. Bir anlık görüntüsünü *mybackupstdpageblob* adlı *mybackupstdpageblob_ss1*kullanarak [anlık görüntü Blob](https://msdn.microsoft.com/library/azure/ee691971.aspx) içinde depolamak ve *mybackupstdaccount*.
4. Merhaba Yedekleme penceresi sırasında başka bir anlık görüntüsünü oluşturmak *mypremiumdisk*, deyin *mypremiumdisk_ss2*, içinde depolamak ve *mypremiumaccount*.
5. Merhaba artımlı değişiklikler hello iki anlık görüntüler arasında almak *mypremiumdisk_ss2* ve *mypremiumdisk_ss1*kullanarak [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx) üzerinde  *mypremiumdisk_ss2* ile **prevsnapshot** parametre toohello zaman damgasını *mypremiumdisk_ss1*. Bu artımlı değişiklikler toohello yedekleme sayfa blobu yazma *mybackupstdpageblob* içinde *mybackupstdaccount*. Merhaba artımlı değişiklikler silinen aralık varsa hello yedekleme sayfa blobundan temizlenmelidir. Kullanım [PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) toowrite artımlı değişiklikler toohello yedekleme sayfa blobu.
6. Merhaba yedekleme sayfa blobu bir anlık görüntüsünü *mybackupstdpageblob*adlı *mybackupstdpageblob_ss2*. Merhaba önceki anlık görüntüyü silmek *mypremiumdisk_ss1* premium depolama hesabından.
7. Her yedekleme penceresi 4-6 adımlarını yineleyin. Bu şekilde, yedeklerini bulundurabilirsiniz *mypremiumdisk* bir standart depolama hesabı.

![Artımlı anlık görüntülerini kullanarak diski yedeklemeniz](./media/storage-incremental-snapshots/storage-incremental-snapshots-1.png)

## <a name="steps-toorestore-a-disk-from-snapshots"></a>Adımları toorestore bir diskten anlık görüntüler
Merhaba aşağıda açıklanan adımları premium disk geri *mypremiumdisk* önceki hello yedekleme depolama hesabından anlık görüntü tooan *mybackupstdaccount*.

1. Toorestore hello premium disk için istediğiniz zaman Hello noktası belirleyin. Anlık görüntü düşünelim *mybackupstdpageblob_ss2*, hello yedekleme depolama hesabında depolanan *mybackupstdaccount*.
2. Merhaba anlık görüntü mybackupstdaccount içinde Yükselt *mybackupstdpageblob_ss2* hello yeni yedekleme temel sayfa blobu olarak *mybackupstdpageblobrestored*.
3. Adlı bu geri yüklenen yedekleme sayfa blobu bir anlık görüntüsünü *mybackupstdpageblobrestored_ss1*.
4. Kopya geri hello sayfa blobu *mybackupstdpageblobrestored* gelen *mybackupstdaccount* çok*mypremiumaccount* hello yeni premium disk olarak  *mypremiumdiskrestored*.
5. Bir anlık görüntüsünü *mypremiumdiskrestored*adlı *mypremiumdiskrestored_ss1* gelecekteki artımlı yedekleme yapmak için.
6. Noktası hello DS serisi VM geri toohello disk *mypremiumdiskrestored* ve hello eski ayırma *mypremiumdisk* hello VM gelen.
7. Geri hello disk için önceki bölümde açıklanan hello yedekleme işlemine başlamak *mypremiumdiskrestored*, hello kullanarak *mybackupstdpageblobrestored* hello yedekleme sayfa blobu olarak.

![Disk anlık görüntülerden geri yükleme](./media/storage-incremental-snapshots/storage-incremental-snapshots-2.png)

## <a name="next-steps"></a>Sonraki Adımlar
Bir blob anlık görüntülerini oluşturma ve aşağıdaki hello bağlantıları kullanarak VM yedekleme altyapınızı planlama hakkında daha fazla bilgi edinin.

* [Bir BLOB bir anlık görüntü oluşturma](https://msdn.microsoft.com/library/azure/hh488361.aspx)
* [VM yedekleme altyapınızı planlama](../backup/backup-azure-vms-introduction.md)

