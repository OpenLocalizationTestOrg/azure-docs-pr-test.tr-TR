---
title: "bir Azure Linux VM kimliği aaaGet | Microsoft Docs"
description: "Tooget ve kullanım nasıl bir Azure Linux VM benzersiz kimliği açıklar"
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
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a>Erişme ve Azure VM benzersiz kimliği kullanma
Azure VM 128 bit tanımlayıcı kodlanmış ve tüm Azure Iaas sanal makinenin SMBIOS içinde depolanan ve şu anda platform BIOS komutları kullanarak okunabilir kimliktir.

Azure VM benzersiz kimliği salt okunur bir özelliktir. Azure VM kimliği olmaz yeniden başlatma kapatma sonrasında değiştirme (ya da planlanan planlanmamış), Başlat/Durdur ayırmayı, hizmet düzeltme veya geri yerinde. Ancak, Hello VM bir anlık görüntü ve kopyalanan toocreate yeni bir örnek ise, yeni bir Azure VM kimliği yapılandırılır.

> [!NOTE]
> Oluşturulan eski VM'ler varsa ve bu yeni özellik (18 Eylül 2014) geri bu yana çalışan Lütfen yeniden başlatın, VM tooautomatically alma Azure benzersiz kimliği
> 
> 

Azure benzersiz VM Kimliğinden tooaccess hello VM içinde:

## <a name="create-a-vm"></a>VM oluşturma
Daha fazla bilgi için bkz: [bir sanal makine oluşturun](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="connect-toohello-vm"></a>Toohello VM Bağlan
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

Sıralama tooBig Endian bit hello gerçek benzersiz VM kimliği bu durumda olacaktır:

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

Merhaba VM Azure üzerinde çalışan veya şirket içi ve Azure Iaas dağıtımlarınızı olabilir, lisans, raporlama veya genel izleme gereksinimlerinizi yardımcı olabilecek olup azure VM benzersiz kimliği farklı senaryolarda kullanılabilir. Azure, şirket içi ya da diğer bulut sağlayıcıları Hello VM çalışıyorsa, uygulamaları geliştirmek ve bunları Azure üzerinde onaylıyor birçok bağımsız yazılım satıcıları tooidentify tootell ve yaşam döngüsü boyunca bir Azure VM gerektirebilir. Bu platform tanımlayıcı örneğin hello yazılım düzgün şekilde lisanslandığından algılamak ya da herhangi bir VM veri tooits kaynağı hello sağ ölçümleri hello sağ platform ve tootrack ayarlama tooassist gibi toocorrelate Yardım ve Bu ölçümler arasında ilişkilendirmenize yardımcı olabilir diğer kullanır.

