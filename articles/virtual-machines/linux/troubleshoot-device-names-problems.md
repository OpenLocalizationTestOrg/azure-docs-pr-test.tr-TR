---
title: "Linux VM aygıt adlarını Azure'da değiştiğinde | Microsoft Docs"
description: "Nedenini açıklayan aygıtı adları değiştirilir ve bu sorun için çözüm sağlar."
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 789f4580901a22dc3aaae9599c7205c76f268403
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>Sorunlarını giderme: Linux VM aygıt adlarının değişmesi

Bu makalede, Linux sanal makine (VM) yeniden başlatın veya diskleri yeniden iliştirmeye sonra aygıt adlarının neden değişmesi açıklanmaktadır. Ayrıca bu sorun için çözüm sağlar.

## <a name="symptom"></a>Belirti

Microsoft Azure Linux VM'ler çalıştırırken aşağıdaki sorunlarla karşılaşabilirsiniz.

- VM yeniden başlatma sonrasında önyükleme başarısız olur.

- Veri diskleri ayrılmış ve yeniden, diskler için cihazları adları değiştirilir.

- Bir uygulama veya aygıt adı kullanarak bir disk başvuruda bulunan komut dosyası başarısız olur. Disk aygıt adına değiştiğini bulun.

## <a name="cause"></a>Nedeni

Linux yollarında cihaz yeniden başlatmaları arasındaki tutarlı olması garanti edilmez. Aygıt adlarının (harf) büyük ve küçük sayı oluşur.  Linux depolama aygıtı sürücüsü yeni bir cihaz algıladığında, birincil ve ikincil cihaz numaraları kullanılabilir aralıktan atar. Bir cihaz kaldırıldığında, aygıtı sayıları daha sonra yeniden kurtulurlar.

Sorun, Linux SCSI alt sistemi tarafından zamanlanmış tarama aygıt zaman uyumsuz olarak olur nedeniyle oluşur. Son aygıt adlandırma yolu yeniden başlatmaları arasında farklılık gösterebilir. 

## <a name="solution"></a>Çözüm

Bu sorunu gidermek için kalıcı adlandırma kullanın. Dört yöntem kalıcı adlandırma için - filesystem etiketi, UUID, kimliğe göre ve tarafından yolu vardır. Dosya sistemi etiket ve UUID yöntemleri Azure Linux VM'ler için önerilir. 

Çoğu dağıtımları da ya da sağlamak **nofail** veya **nobootwait** fstab seçenekleri. Bu seçenekler, başlangıçta bağlamak disk başarısız olsa bile önyükleme sistemi sağlar. Bu parametreler hakkında daha fazla bilgi için dağıtım ait belgelere bakın. Bir veri diski eklediğinizde bir UUID kullanmak için bir Linux VM yapılandırma hakkında daha fazla bilgi için bkz: [yeni diski Linux VM Bağlan](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk). 

Azure Linux Aracısı VM üzerinde yüklü olduğunda Udev kuralları altında sembolik bağlantılar kümesi oluşturmak için kullandığı **/dev/disk/azure**. Udev kurallar uygulamalar tarafından kullanılabilir ve diskleri tanımlamak için komut dosyaları VM, kendi türü ve LUN'a bağlı.

## <a name="more-information"></a>Daha fazla bilgi

### <a name="identify-disk-luns"></a>Diski LUN'ları tanımlayın

Bir uygulama, tüm dünyada sembolik bağlantılar ve bağlı disklerde bulmak için LUN'ları kullanabilirsiniz. Azure Linux Aracısı'nı şimdi sembolik bağlantılar bir LUN cihazlara aşağıdaki gibi ayarlayın udev kurallarını içerir:

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

LUN bilgileri de lsscsi veya benzer bir aracı gibi kullanarak Linux konuktaki alınabilir.

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

Bu Konuk LUN bilgileri Azure aboneliği meta verileriyle bölüm verileri depolayan VHD Azure depolama alanında konumunu tanımlamak için kullanılabilir. Örneğin, az CLI kullanın:

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a>Dosya sistemi UUID'ler blkid kullanarak Bul

Bir komut dosyası veya uygulama blkid çıktısını ya da bilgi benzer kaynakları okuyabilir ve sembolik bağlantılar oluşturmak **/dev** kullanmak için. Çıktı VM ve için ilişkili oldukları aygıt dosyası bağlı tüm diskleri UUID'ler gösterir:

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

Sembolik bağlantılar altında bir dizi waagent udev kuralları oluşturmak **/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


Uygulama bu bilgileri kullanabilir önyükleme diski cihaz ve kaynak (kısa ömürlü) disk tanımlar. Azure'da, uygulamalar için başvurmalıdır **/dev/disk/azure/root-part1** veya **/dev/disk/azure-resource-part1** bu bölümler bulmak için.

Ek bölümlere blkid listede yoksa, bir veri diski bulundukları. Uygulamalar bu bölümler UUID'si korumak ve gibi bir yol kullanmak aşağıdaki çalışma zamanında cihaz adını bulmak için:

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-the-latest-azure-storage-rules"></a>En son Azure depolama kuralları Al

En son Azure depolama kuralları aşağıdaki komutları çalıştırın:

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


Daha fazla bilgi için aşağıdaki makalelere bakın:

- [Ubuntu: UUID kullanma](https://help.ubuntu.com/community/UsingUUID)

- [Red Hat: Kalıcı adlandırma](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [Linux: UUID'ler için yapabilecekleriniz](https://www.linux.com/news/what-uuids-can-do-you)

- [Udev: Aygıt Yönetimi Modern Linux sistemindeki giriş](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

