---
title: "Linux için kullanıcı adları aaaSelecting | Microsoft Docs"
description: "Azure'da bir Linux sanal makine için nasıl tooselect kullanıcı adları öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a>Azure’da Linux için Kullanıcı Adları Seçme
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Azure üzerinde bir Linux sanal makine sağlarken hello VM hello toolog daha sonra kullanabileceğiniz bir kök olmayan kullanıcı adını belirtmeniz gerekir. Merhaba hello yeni kullanıcı adını seçebilir veya Klasik Azure Portalı aracılığıyla sağlama hello değişirse adı "azureuser" Merhaba varsayılan kabul edebilir.

Çoğu durumda bu kullanıcı hello temel görüntü üzerinde var olmaz ve hello sağlama işlemi sırasında oluşturulur. Ardından Hello kullanıcı hello temel VM görüntü varsa, hello Azure Linux Aracısı hello parola ve/veya SSH anahtarı hello VM oluşturulurken belirtilen hello bilgilere göre bu kullanıcı için yalnızca yapılandırır.

**Ancak**, Linux kullanılmaması gereken kullanıcı adları kümesini tanımlar. işlem sağlama hello **başarısız** tooprovision UID 0-99 olan bir kullanıcı olarak tanımlanan bir varolan bir sistem kullanıcı kullanarak bir Linux VM çalışırsanız. Merhaba tipik örneğidir `root` UID 0 olan kullanıcı.

* Ayrıca bkz: [Linux standart Base - kullanıcı kimliği aralıkları](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)

Merhaba, CentOS ve Ubuntu Linux sanal makine azure'da sağlamada yapmaktan kaçınmalısınız için ortak yerleşik sistem kullanıcıları listesi aşağıdadır. Bu liste yalnızca bir örnek, Lütfen, dağıtım tooensure için mevcut bir sistem kullanıcıyla çakışıp çakışmadığını'ı seçin, hello kullanıcıadı toohello belgelerine bakın.

## <a name="centos"></a>CentOS
* abrt
* adm
* Ses
* Depo
* CDROM
* cgred
* arka plan programı
* dbus
* araması
* DIP
* disk
* Disket
* FTP
* FTP
* Oyunlar
* Gopher
* haldaemon
* durdurma
* kmem
* kilitleme
* LP
* Posta
* ADAM
* mem
* nfsnobody
* hiç kimse
* NTP
* işleci
* oprofile
* postdrop
* sonek
* qpidd
* kök
* RPC
* rpcuser
* saslauth
* kapatma
* slocate
* sshd
* stapdev
* stapusr
* Eşitleme
* sys
* bant
* test etme
* tcpdump
* TTY
* kullanıcılar
* utempter
* utmp
* UUCP
* vcsa
* video
* Tekerlek

## <a name="ubuntu"></a>Ubuntu
* adm
* Yönetici
* Ses
* yedekleme
* Depo
* CDROM
* crontab
* arka plan programı
* araması
* DIP
* disk
* Faks
* Disket
* Sigortası
* Oyunlar
* gnats
* IRC
* kmem
* Yatay
* libuuid
* Liste
* LP
* Posta
* ADAM
* MessageBus
* mlocate
* netdev
* Haber
* hiç kimse
* hiçbir Grup
* işleci
* plugdev
* Proxy
* kök
* SASL
* Gölge
* src
* SSH
* sshd
* Personel
* sudo
* Eşitleme
* sys
* syslog
* bant
* TTY
* kullanıcılar
* utmp
* UUCP
* video
* Ses
* whoopsie
* www-data

