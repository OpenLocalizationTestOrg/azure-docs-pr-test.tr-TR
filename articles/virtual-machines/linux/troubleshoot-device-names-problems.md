---
title: "aaaLinux VM aygıt adlarını Azure'da değiştiğinde | Microsoft Docs"
description: "Neden aygıt adlarının değiştirilir ve bu sorun için çözüm sağlamak hello açıklanmaktadır."
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
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>Sorunlarını giderme: Linux VM aygıt adlarının değişmesi

Linux sanal makine (VM) yeniden başlatın ya da hello diskleri yeniden iliştirmeye sonra aygıt adlarının neden değişmesi Hello makalede açıklanmaktadır. Ayrıca bu sorun için hello çözümü sağlar.

## <a name="symptom"></a>Belirti

Sorunları Linux VM'ler Microsoft Azure üzerinde çalışırken aşağıdaki hello karşılaşabilirsiniz.

- Merhaba VM yeniden başlatma sonrasında tooboot başarısız olur.

- Veri diskleri ayrılmış ve yeniden, diskleri için hello aygıtları adları değiştirilir.

- Bir uygulama veya aygıt adı kullanarak bir disk başvuruda bulunan komut dosyası başarısız olur. Bu hello bulur hello disk aygıt adı değiştirildi.

## <a name="cause"></a>Nedeni

Linux aygıt yollarında toobe tutarlı yeniden başlatmaları arasındaki garanti edilmez. Aygıt adlarının (harf) büyük ve küçük sayı oluşur.  Yeni bir cihaz Hello Linux depolama aygıtı sürücüsü algıladığında, birincil ve ikincil cihaz numaraları tooit hello kullanılabilir aralığından atar. Bir cihaz kaldırıldığında, hello aygıt daha sonra yeniden boşaltılmış toobe numaralarıdır.

Merhaba Linux hello SCSI alt sistemi tarafından zamanlanmış tarama aygıtı zaman uyumsuz olarak olur hello sorun nedeniyle oluşur. Merhaba son aygıt adlandırma yolu yeniden başlatmaları arasında farklılık gösterebilir. 

## <a name="solution"></a>Çözüm

tooresolve bu sorunu kalıcı adlandırma kullanın. Dört yöntemleri toopersistent vardır - filesystem etiketi, UUID, kimliğe göre ve tarafından yolu adlandırma. Merhaba filesystem etiket ve UUID yöntemleri Azure Linux VM'ler için önerilir. 

Çoğu dağıtımları da ya da hello sağlamak **nofail** veya **nobootwait** fstab seçenekleri. Merhaba disk toomount başlangıçta başarısız olsa bile bu seçenekler sistem tooboot sağlar. Bu parametreler hakkında daha fazla bilgi için Hello dağıtım'ın belgelerine bakın. Bir Linux VM toouse bir veri diski eklediğinizde UUID tooconfigure nasıl gördükleri hakkında daha fazla bilgi için [toohello Linux VM toomount hello yeni disk bağlanmak](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk). 

Hello Azure Linux Aracısı VM üzerinde yüklü olduğunda, sembolik bağlantılar altında bir dizi Udev kuralları tooconstruct kullanan **/dev/disk/azure**. Udev kurallar uygulamalar tarafından kullanılabilir ve komut dosyaları tooidentify diskleri ekli toohello VM, kendi türü ve LUN hello.

## <a name="more-information"></a>Daha fazla bilgi

### <a name="identify-disk-luns"></a>Diski LUN'ları tanımlayın

Bir uygulama LUN toofind tüm bağlı hello diskleri ve oluşturma sembolik bağlantılar kullanabilirsiniz. Hello Azure Linux Aracısı şimdi sembolik bağlantılar bir LUN toohello aygıtlardan aşağıdaki gibi ayarlayın udev kurallarını içerir:

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
                                 

LUN bilgileri de hello Linux konuktaki lsscsi veya benzer bir aracı gibi kullanılarak alınabilir.

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

Bu Konuk LUN bilgileri Azure aboneliği meta veri tooidentify hello konumunu hello hello bölüm verileri depolayan VHD ile Azure depolama alanında kullanılabilir. Örneğin, hello az CLI kullanın:

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

Bir komut dosyası veya uygulama blkid hello çıktısını ya da bilgi benzer kaynakları okuyabilir ve sembolik bağlantılar oluşturmak **/dev** kullanmak için. Merhaba çıkış ilişkili toohello VM ve hello aygıt dosya toowhich hello UUID tüm disklerin bağlı gösterir:

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

Merhaba waagent udev kuralları oluşturmak sembolik bağlantılar altında bir dizi **/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


Merhaba uygulaması, bu bilgiyi kullanabilir hello önyükleme disk aygıtı ve hello kaynak (kısa ömürlü) disk tanımlar. Azure'da, uygulamaları çok başvurmalıdır**/dev/disk/azure/root-part1** veya **/dev/disk/azure-resource-part1** toodiscover bu bölümler.

Merhaba blkid listeden ek bölümler varsa, bunlar bir veri diski bulunur. Uygulamalar bu bölümler için hello UUID korumak ve çalışma zamanında toodiscover hello aygıt adı altındaki hello gibi bir yol kullanın:

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a>Merhaba en son Azure depolama kuralları Al

Azure depolama kuralları son toohello, aşağıdaki komutları çalıştırın:

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


Daha fazla bilgi için aşağıdaki makaleler hello bakın:

- [Ubuntu: UUID kullanma](https://help.ubuntu.com/community/UsingUUID)

- [Red Hat: Kalıcı adlandırma](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [Linux: UUID'ler için yapabilecekleriniz](https://www.linux.com/news/what-uuids-can-do-you)

- [Udev: Giriş tooDevice yönetim içinde Modern Linux sistemi](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

