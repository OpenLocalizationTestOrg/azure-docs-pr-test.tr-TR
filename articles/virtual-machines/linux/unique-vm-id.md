---
title: "Bir Azure Linux VM'de kimliği alma | Microsoft Docs"
description: "Alma ve Azure Linux VM benzersiz bir kimliği nasıl kullanılacağını açıklar"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 258ce425d5692730011cf2f4468dc0ba77f4cb79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a>Erişme ve Azure VM benzersiz kimliği kullanma
Azure VM 128 bit tanımlayıcı kodlanmış ve tüm Azure Iaas sanal makinenin SMBIOS içinde depolanan ve şu anda platform BIOS komutları kullanarak okunabilir kimliktir.

Azure VM benzersiz kimliği salt okunur bir özelliktir. Azure VM kimliği olmaz yeniden başlatma kapatma sonrasında değiştirme (ya da planlanan planlanmamış), Başlat/Durdur ayırmayı, hizmet düzeltme veya geri yerinde. VM bir anlık görüntüdür ve yeni bir örneğini oluşturmak için kopyalanır, ancak yeni bir Azure VM kimliği yapılandırılır.

> [!NOTE]
> Eski varsa VM'ler oluşturulur ve bu yeni özellik (Eylül 18 2014), lütfen yeniden başlatma geri bu yana çalışan otomatik olarak Azure benzersiz almak için VM kimliği
> 
> 

Azure benzersiz VM Kimliğinden VM dahilinde erişmek için:

## <a name="create-a-vm"></a>VM oluşturma
Daha fazla bilgi için bkz: [bir sanal makine oluşturun](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="connect-to-the-vm"></a>VM’ye bağlanma
Daha fazla bilgi için bkz: [Linux SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="query-vm-unique-id"></a>Sorgu VM benzersiz kimliği
Komutu (örneğin kullanan **Ubuntu**):

```bash
sudo dmidecode | grep UUID
```

Örnek beklenen sonuçları:

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

Büyük bit sıralama Endian nedeniyle, gerçek benzersiz VM kimliği bu durumda olacaktır:

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

VM Azure üzerinde çalışan veya şirket içi ve Azure Iaas dağıtımlarınızı olabilir, lisans, raporlama veya genel izleme gereksinimlerinizi yardımcı olabilecek olup azure VM benzersiz kimliği farklı senaryolarda kullanılabilir. Bir Azure VM yaşam döngüsü tanımlamak için uygulamalar oluşturmak ve bunları Azure üzerinde onaylıyor birçok bağımsız yazılım satıcıları gerektirebilir ve VM Azure üzerinde çalışan olmadığını bildirmek için şirket içi veya diğer bulut sağlayıcıları. Bu bir platform tanımlayıcısı örneğin yazılım düzgün şekilde lisanslandığından algılamak veya sağ platform için doğru ölçümler ayarlama konusunda yardımcı olmak ve izlemek ve bu ölçümleri diğer kullanımlar arasında ilişkilendirmek için onun kaynağına gibi herhangi bir VM veri ilişkilendirmek için Yardım yardımcı olabilir.

