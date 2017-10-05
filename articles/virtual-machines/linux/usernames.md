---
title: "Linux kullanıcı adlarını seçme | Microsoft Docs"
description: "Azure'da bir Linux sanal makine için kullanıcı adları seçin öğrenin."
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
ms.openlocfilehash: 1874d72e5f88816036667932371ff28704d186c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a>Azure’da Linux için Kullanıcı Adları Seçme
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Azure üzerinde bir Linux sanal makine sağlarken, daha sonra VM'de oturum açmak için kullanabileceğiniz bir kök olmayan kullanıcının adını belirtmeniz gerekir. Yeni kullanıcı adını seçebilir veya Azure Klasik portalı üzerinden sağlama değişirse "azureuser" varsayılan adı kabul edebilir.

Çoğu durumda bu kullanıcı temel görüntü var olmaz ve sağlama işlemi sırasında oluşturulur. Ardından kullanıcı üzerinde temel VM görüntü varsa, Azure Linux Aracısı'nı parola ve/veya VM oluşturulurken belirtilen bilgilere göre bu kullanıcı için SSH anahtarı yalnızca yapılandırır.

**Ancak**, Linux kullanılmaması gereken kullanıcı adları kümesini tanımlar. Sağlama işlemi **başarısız** UID 0-99 olan bir kullanıcı olarak tanımlanan bir varolan bir sistem kullanıcı kullanarak bir Linux VM sağlayacak çalışırsanız. Tipik bir örnektir `root` UID 0 olan kullanıcı.

* Ayrıca bkz: [Linux standart Base - kullanıcı kimliği aralıkları](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)

Aşağıdakiler, CentOS ve Ubuntu Linux sanal makine azure'da sağlamada yapmaktan kaçınmalısınız ortak yerleşik sistem kullanıcıların bir listesidir. Bu liste yalnızca bir örnek, seçtiğiniz kullanıcı adı ile var olan bir sistem kullanıcı çakışmadığından emin olmak, dağıtım için belgelere başvurun.

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

