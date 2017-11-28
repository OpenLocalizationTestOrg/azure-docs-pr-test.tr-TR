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
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a><span data-ttu-id="f2291-103">Nasıl tooreset yerel Linux parola Azure vm'lerinde</span><span class="sxs-lookup"><span data-stu-id="f2291-103">How tooreset local Linux password on Azure VMs</span></span>

<span data-ttu-id="f2291-104">Bu makalede, çeşitli yöntemleri tooreset yerel Linux sanal makine (VM) parolaları tanıtılır.</span><span class="sxs-lookup"><span data-stu-id="f2291-104">This article introduces several methods tooreset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="f2291-105">Merhaba kullanıcı hesabının süresinin dolduğunu veya yalnızca toocreate yeni bir hesap istiyorsanız, yöntemleri toocreate yeni bir yerel yönetici hesabı aşağıdaki hello ve erişim toohello VM yeniden elde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2291-105">If hello user account is expired or you just want toocreate a new account, you can use hello following methods toocreate a new local admin account and re-gain access toohello VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="f2291-106">Belirtiler</span><span class="sxs-lookup"><span data-stu-id="f2291-106">Symptoms</span></span>

<span data-ttu-id="f2291-107">Toohello VM oturum açamaz ve kullandığınız hello parola yanlış belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f2291-107">You can't log in toohello VM, and you receive a message that indicates that hello password that you used is incorrect.</span></span> <span data-ttu-id="f2291-108">Ayrıca, parolanızı VMAgent tooreset hello Azure portalı üzerinde kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="f2291-108">Additionally, you can't use VMAgent tooreset your password on hello Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="f2291-109">El ile parola sıfırlama yordamı</span><span class="sxs-lookup"><span data-stu-id="f2291-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="f2291-110">Merhaba VM silin ve hello bağlı diskler tutun.</span><span class="sxs-lookup"><span data-stu-id="f2291-110">Delete hello VM and keep hello attached disks.</span></span>

2.  <span data-ttu-id="f2291-111">Merhaba işletim sistemi sürücü bir veri diski tooanother olarak ekleme hello zamana bağlı VM'de aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="f2291-111">Attach hello OS Drive as a data disk tooanother temporal VM in hello same location.</span></span>

3.  <span data-ttu-id="f2291-112">SSH komutu hello zamana bağlı VM toobecome üzerinde aşağıdaki hello süper kullanıcı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f2291-112">Run hello following SSH command on hello temporal VM toobecome a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="f2291-113">Çalıştırma **fdisk -l** veya sistem günlükleri toofind hello bakma yeni disk bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2291-113">Run **fdisk -l** or look at system logs toofind hello newly attached disk.</span></span> <span data-ttu-id="f2291-114">Merhaba sürücü adı toomount bulun.</span><span class="sxs-lookup"><span data-stu-id="f2291-114">Locate hello drive name toomount.</span></span> <span data-ttu-id="f2291-115">Ardından üzerinde hello zamana bağlı VM, ilgili hello Ara günlük dosyası.</span><span class="sxs-lookup"><span data-stu-id="f2291-115">Then on hello temporal VM, look in hello relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="f2291-116">Merhaba, örnek hello grep komutunun çıkışını aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="f2291-116">hello following is example output of hello grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="f2291-117">Adlı bir bağlama noktası oluşturma **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="f2291-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="f2291-118">Merhaba işletim sistemi diski hello bağlama noktasında bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f2291-118">Mount hello OS disk on hello mount point.</span></span> <span data-ttu-id="f2291-119">Genellikle toomount sdc1 veya sdc2 gerekir.</span><span class="sxs-lookup"><span data-stu-id="f2291-119">You usually need toomount sdc1 or sdc2.</span></span> <span data-ttu-id="f2291-120">Bu bölüm hello bozuk makine diskten/etc dizininde barındırma hello bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f2291-120">This will depend on hello hosting partition in /etc directory from hello broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="f2291-121">Herhangi bir değişiklik yapmadan önce bir yedekleme gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f2291-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="f2291-122">Gereksinim duyduğunuz hello kullanıcının parolasını sıfırlama:</span><span class="sxs-lookup"><span data-stu-id="f2291-122">Reset hello user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="f2291-123">Taşıma hello dosyaları toohello doğru konumda makinenin disk bozuk hello değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="f2291-123">Move hello modified files toohello correct location on hello broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    <span data-ttu-id="f2291-124">CD / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="f2291-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
