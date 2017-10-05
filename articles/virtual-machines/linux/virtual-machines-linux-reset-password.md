---
title: "Azure vm'lerinde yerel Linux parola sıfırlama | Microsoft Docs"
description: "Azure VM'de yerel Linux parola sıfırlama adım tanıtır"
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
ms.openlocfilehash: 084cdb26c7dfd8f46fb6ec7f8c48f7b4a327e2ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-local-linux-password-on-azure-vms"></a><span data-ttu-id="d0edf-103">Azure vm'lerinde yerel Linux parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="d0edf-103">How to reset local Linux password on Azure VMs</span></span>

<span data-ttu-id="d0edf-104">Bu makalede, yerel Linux sanal makine (VM) parola sıfırlama için çeşitli yöntemler sunar.</span><span class="sxs-lookup"><span data-stu-id="d0edf-104">This article introduces several methods to reset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="d0edf-105">Kullanıcı hesabının süresinin dolduğunu veya yalnızca yeni bir hesap oluşturmak istiyorsanız, yeni bir yerel yönetici hesabı oluşturun ve VM erişimi yeniden kazanmak için aşağıdaki yöntemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0edf-105">If the user account is expired or you just want to create a new account, you can use the following methods to create a new local admin account and re-gain access to the VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="d0edf-106">Belirtiler</span><span class="sxs-lookup"><span data-stu-id="d0edf-106">Symptoms</span></span>

<span data-ttu-id="d0edf-107">VM oturum açamıyor ve kullandığınız parola yanlış olduğunu belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d0edf-107">You can't log in to the VM, and you receive a message that indicates that the password that you used is incorrect.</span></span> <span data-ttu-id="d0edf-108">Ayrıca, Azure Portal'da, parolanızı sıfırlamak için VMAgent kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="d0edf-108">Additionally, you can't use VMAgent to reset your password on the Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="d0edf-109">El ile parola sıfırlama yordamı</span><span class="sxs-lookup"><span data-stu-id="d0edf-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="d0edf-110">VM silme ve kullanıma açılan diskler tutun.</span><span class="sxs-lookup"><span data-stu-id="d0edf-110">Delete the VM and keep the attached disks.</span></span>

2.  <span data-ttu-id="d0edf-111">İşletim sistemi sürücüsü zamana bağlı başka bir VM ile aynı konumda bir veri diski iliştirin.</span><span class="sxs-lookup"><span data-stu-id="d0edf-111">Attach the OS Drive as a data disk to another temporal VM in the same location.</span></span>

3.  <span data-ttu-id="d0edf-112">Aşağıdaki SSH komutu süper kullanıcı olmasını zamana bağlı VM üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d0edf-112">Run the following SSH command on the temporal VM to become a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="d0edf-113">Çalıştırma **fdisk -l** ya da yeni eklenen disk bulmak için sistem günlüklerine bakın.</span><span class="sxs-lookup"><span data-stu-id="d0edf-113">Run **fdisk -l** or look at system logs to find the newly attached disk.</span></span> <span data-ttu-id="d0edf-114">Bağlama için sürücü adını bulun.</span><span class="sxs-lookup"><span data-stu-id="d0edf-114">Locate the drive name to mount.</span></span> <span data-ttu-id="d0edf-115">Ardından zamana bağlı VM ilgili günlük dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="d0edf-115">Then on the temporal VM, look in the relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="d0edf-116">Örnek çıktı grep komut verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d0edf-116">The following is example output of the grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="d0edf-117">Adlı bir bağlama noktası oluşturma **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="d0edf-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="d0edf-118">İşletim sistemi diski bağlama noktasında bağlayın.</span><span class="sxs-lookup"><span data-stu-id="d0edf-118">Mount the OS disk on the mount point.</span></span> <span data-ttu-id="d0edf-119">Bağlama sdc1 veya sdc2 için genellikle olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0edf-119">You usually need to mount sdc1 or sdc2.</span></span> <span data-ttu-id="d0edf-120">Bu barındırma/etc dizin bozuk makine diskten bölümünde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d0edf-120">This will depend on the hosting partition in /etc directory from the broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="d0edf-121">Herhangi bir değişiklik yapmadan önce bir yedekleme gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d0edf-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="d0edf-122">Gereksinim duyduğunuz kullanıcının parolasını sıfırlama:</span><span class="sxs-lookup"><span data-stu-id="d0edf-122">Reset the user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="d0edf-123">Değiştirilen Dosyalar bozuk makinenin diskte doğru konuma taşıyın.</span><span class="sxs-lookup"><span data-stu-id="d0edf-123">Move the modified files to the correct location on the broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back to the root and unmount the disk.

    ~~~~
    <span data-ttu-id="d0edf-124">CD / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="d0edf-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach the disk from the management portal.

12. Recreate the VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk to another Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How to delete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)