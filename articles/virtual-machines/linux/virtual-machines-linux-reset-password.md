---
title: aaaHow tooreset yerel Linux parola Azure vm'lerinde | Microsoft Docs
description: "Merhaba adımları tooreset hello yerel Linux parola Azure VM'de tanıtır"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: 3827e32186c5f034d9bb6fc502dc26708b52a00a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a>Nasıl tooreset yerel Linux parola Azure vm'lerinde

Bu makalede, çeşitli yöntemleri tooreset yerel Linux sanal makine (VM) parolaları tanıtılır. Merhaba kullanıcı hesabının süresinin dolduğunu veya yalnızca toocreate yeni bir hesap istiyorsanız, yöntemleri toocreate yeni bir yerel yönetici hesabı aşağıdaki hello ve erişim toohello VM yeniden elde kullanabilirsiniz.

## <a name="symptoms"></a>Belirtiler

Toohello VM oturum açamaz ve kullandığınız hello parola yanlış belirten bir ileti alırsınız. Ayrıca, parolanızı VMAgent tooreset hello Azure portalı üzerinde kullanamazsınız. 

## <a name="manual-password-reset-procedure"></a>El ile parola sıfırlama yordamı

1.  Merhaba VM silin ve hello bağlı diskler tutun.

2.  Merhaba işletim sistemi sürücü bir veri diski tooanother olarak ekleme hello zamana bağlı VM'de aynı konumu.

3.  SSH komutu hello zamana bağlı VM toobecome üzerinde aşağıdaki hello süper kullanıcı çalıştırın.


    ~~~~
    sudo su
    ~~~~

4.  Çalıştırma **fdisk -l** veya sistem günlükleri toofind hello bakma yeni disk bağlı. Merhaba sürücü adı toomount bulun. Ardından üzerinde hello zamana bağlı VM, ilgili hello Ara günlük dosyası.

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    Merhaba, örnek hello grep komutunun çıkışını aşağıdadır:

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  Adlı bir bağlama noktası oluşturma **tempmount**.

    ~~~~
    mkdir /tempmount
    ~~~~

6.  Merhaba işletim sistemi diski hello bağlama noktasında bağlayın. Genellikle toomount sdc1 veya sdc2 gerekir. Bu bölüm hello bozuk makine diskten/etc dizininde barındırma hello bağlıdır.

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  Herhangi bir değişiklik yapmadan önce bir yedekleme gerçekleştirin:

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  Gereksinim duyduğunuz hello kullanıcının parolasını sıfırlama:

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  Taşıma hello dosyaları toohello doğru konumda makinenin disk bozuk hello değiştirdi.

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    CD / umount /tempmount
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
