---
title: "Linux sanal makinelerde aaaUse kök ayrıcalıkları | Microsoft Docs"
description: "Azure'da bir Linux sanal makinede nasıl toouse kök ayrıcalıkları öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a>Azure'daki Linux sanal makinelerinde kök ayrıcalıkları kullanma
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Varsayılan olarak, hello `root` kullanıcı azure'daki Linux sanal makinelerde devre dışıdır. Kullanıcılar çalışma komutları yükseltilmiş ayrıcalıklarla hello kullanarak `sudo` komutu. Ancak, hello deneyimi nasıl hello sistem sağlanan bağlı olarak değişebilir.

1. **SSH anahtarı ve parola veya parola yalnızca** -hello sanal makine ya da bir sertifika ile sağlanan (`.CER` dosyası) veya SSH anahtarı hem de bir parola veya yalnızca bir kullanıcı adı ve parola. Bu durumda `sudo` hello kullanıcının parolasını hello komutu yürütmeden önce sizden onay ister.
2. **SSH anahtarı yalnızca** -hello sanal makine bir sertifika ile sağlanan (`.cer`, `.pem`, veya `.pub` dosya) veya SSH anahtarı ancak parola yok.  Bu durumda `sudo` **almayacak** hello kullanıcının parolasını hello komutu yürütmeden önce sor.

## <a name="ssh-key-and-password-or-password-only"></a>SSH anahtarı ve parola veya parola yalnızca
Merhaba Linux SSH anahtarı veya parola kimlik doğrulaması kullanarak sanal makine oturum açın, sonra kullanarak komutları çalıştırmak `sudo`, örneğin:

    # sudo <command>
    [sudo] password for azureuser:

Bu durumda hello kullanıcı için bir parola istenir. Merhaba parola girdikten sonra `sudo` hello komutuyla çalışacak `root` ayrıcalıkları.

Merhaba düzenleyerek passwordless sudo etkinleştirebilirsiniz `/etc/sudoers.d/waagent` dosya, örneğin:

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

Bu değişiklik, "azureuser" Merhaba kullanıcı tarafından passwordless sudo için izin verir.

## <a name="ssh-key-only"></a>SSH yalnızca anahtar
Merhaba Linux SSH anahtar kimlik doğrulaması kullanarak sanal makine oturum açın, sonra kullanarak komutları çalıştırmak `sudo`, örneğin:

    # sudo <command>

Bu durumda hello kullanıcı olacak **değil** için bir parola istenir. Tuşlarına basarak sonra `<enter>`, `sudo` hello komutuyla çalışacak `root` ayrıcalıkları.

