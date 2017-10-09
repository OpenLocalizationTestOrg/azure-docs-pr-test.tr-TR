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
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="7bcda-103">Azure’da Linux için Kullanıcı Adları Seçme</span><span class="sxs-lookup"><span data-stu-id="7bcda-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="7bcda-104">Azure üzerinde bir Linux sanal makine sağlarken hello VM hello toolog daha sonra kullanabileceğiniz bir kök olmayan kullanıcı adını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7bcda-104">When you provision a Linux virtual machine on Azure you must specify hello name of a non-root user that you can later use toolog into hello VM.</span></span> <span data-ttu-id="7bcda-105">Merhaba hello yeni kullanıcı adını seçebilir veya Klasik Azure Portalı aracılığıyla sağlama hello değişirse adı "azureuser" Merhaba varsayılan kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="7bcda-105">You may choose hello name of hello new user, or if provisioning via hello Azure classic portal you can accept hello default name "azureuser".</span></span>

<span data-ttu-id="7bcda-106">Çoğu durumda bu kullanıcı hello temel görüntü üzerinde var olmaz ve hello sağlama işlemi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7bcda-106">In most cases this user won't exist on hello base image and will be created during hello provisioning process.</span></span> <span data-ttu-id="7bcda-107">Ardından Hello kullanıcı hello temel VM görüntü varsa, hello Azure Linux Aracısı hello parola ve/veya SSH anahtarı hello VM oluşturulurken belirtilen hello bilgilere göre bu kullanıcı için yalnızca yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7bcda-107">If hello user exists on hello base VM image, then hello Azure Linux agent simply configures hello password and/or SSH key for that user based on hello information you specified when creating hello VM.</span></span>

<span data-ttu-id="7bcda-108">**Ancak**, Linux kullanılmaması gereken kullanıcı adları kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7bcda-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="7bcda-109">işlem sağlama hello **başarısız** tooprovision UID 0-99 olan bir kullanıcı olarak tanımlanan bir varolan bir sistem kullanıcı kullanarak bir Linux VM çalışırsanız.</span><span class="sxs-lookup"><span data-stu-id="7bcda-109">hello provisioning process will **fail** if you try tooprovision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="7bcda-110">Merhaba tipik örneğidir `root` UID 0 olan kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="7bcda-110">A typical example is hello `root` user, which has UID 0.</span></span>

* <span data-ttu-id="7bcda-111">Ayrıca bkz: [Linux standart Base - kullanıcı kimliği aralıkları](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="7bcda-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="7bcda-112">Merhaba, CentOS ve Ubuntu Linux sanal makine azure'da sağlamada yapmaktan kaçınmalısınız için ortak yerleşik sistem kullanıcıları listesi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="7bcda-112">hello following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="7bcda-113">Bu liste yalnızca bir örnek, Lütfen, dağıtım tooensure için mevcut bir sistem kullanıcıyla çakışıp çakışmadığını'ı seçin, hello kullanıcıadı toohello belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="7bcda-113">This list is just an example, please refer toohello documentation for your distribution tooensure that hello username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="7bcda-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="7bcda-114">CentOS</span></span>
* <span data-ttu-id="7bcda-115">abrt</span><span class="sxs-lookup"><span data-stu-id="7bcda-115">abrt</span></span>
* <span data-ttu-id="7bcda-116">adm</span><span class="sxs-lookup"><span data-stu-id="7bcda-116">adm</span></span>
* <span data-ttu-id="7bcda-117">Ses</span><span class="sxs-lookup"><span data-stu-id="7bcda-117">audio</span></span>
* <span data-ttu-id="7bcda-118">Depo</span><span class="sxs-lookup"><span data-stu-id="7bcda-118">bin</span></span>
* <span data-ttu-id="7bcda-119">CDROM</span><span class="sxs-lookup"><span data-stu-id="7bcda-119">cdrom</span></span>
* <span data-ttu-id="7bcda-120">cgred</span><span class="sxs-lookup"><span data-stu-id="7bcda-120">cgred</span></span>
* <span data-ttu-id="7bcda-121">arka plan programı</span><span class="sxs-lookup"><span data-stu-id="7bcda-121">daemon</span></span>
* <span data-ttu-id="7bcda-122">dbus</span><span class="sxs-lookup"><span data-stu-id="7bcda-122">dbus</span></span>
* <span data-ttu-id="7bcda-123">araması</span><span class="sxs-lookup"><span data-stu-id="7bcda-123">dialout</span></span>
* <span data-ttu-id="7bcda-124">DIP</span><span class="sxs-lookup"><span data-stu-id="7bcda-124">dip</span></span>
* <span data-ttu-id="7bcda-125">disk</span><span class="sxs-lookup"><span data-stu-id="7bcda-125">disk</span></span>
* <span data-ttu-id="7bcda-126">Disket</span><span class="sxs-lookup"><span data-stu-id="7bcda-126">floppy</span></span>
* <span data-ttu-id="7bcda-127">FTP</span><span class="sxs-lookup"><span data-stu-id="7bcda-127">ftp</span></span>
* <span data-ttu-id="7bcda-128">FTP</span><span class="sxs-lookup"><span data-stu-id="7bcda-128">ftp</span></span>
* <span data-ttu-id="7bcda-129">Oyunlar</span><span class="sxs-lookup"><span data-stu-id="7bcda-129">games</span></span>
* <span data-ttu-id="7bcda-130">Gopher</span><span class="sxs-lookup"><span data-stu-id="7bcda-130">gopher</span></span>
* <span data-ttu-id="7bcda-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="7bcda-131">haldaemon</span></span>
* <span data-ttu-id="7bcda-132">durdurma</span><span class="sxs-lookup"><span data-stu-id="7bcda-132">halt</span></span>
* <span data-ttu-id="7bcda-133">kmem</span><span class="sxs-lookup"><span data-stu-id="7bcda-133">kmem</span></span>
* <span data-ttu-id="7bcda-134">kilitleme</span><span class="sxs-lookup"><span data-stu-id="7bcda-134">lock</span></span>
* <span data-ttu-id="7bcda-135">LP</span><span class="sxs-lookup"><span data-stu-id="7bcda-135">lp</span></span>
* <span data-ttu-id="7bcda-136">Posta</span><span class="sxs-lookup"><span data-stu-id="7bcda-136">mail</span></span>
* <span data-ttu-id="7bcda-137">ADAM</span><span class="sxs-lookup"><span data-stu-id="7bcda-137">man</span></span>
* <span data-ttu-id="7bcda-138">mem</span><span class="sxs-lookup"><span data-stu-id="7bcda-138">mem</span></span>
* <span data-ttu-id="7bcda-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="7bcda-139">nfsnobody</span></span>
* <span data-ttu-id="7bcda-140">hiç kimse</span><span class="sxs-lookup"><span data-stu-id="7bcda-140">nobody</span></span>
* <span data-ttu-id="7bcda-141">NTP</span><span class="sxs-lookup"><span data-stu-id="7bcda-141">ntp</span></span>
* <span data-ttu-id="7bcda-142">işleci</span><span class="sxs-lookup"><span data-stu-id="7bcda-142">operator</span></span>
* <span data-ttu-id="7bcda-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="7bcda-143">oprofile</span></span>
* <span data-ttu-id="7bcda-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="7bcda-144">postdrop</span></span>
* <span data-ttu-id="7bcda-145">sonek</span><span class="sxs-lookup"><span data-stu-id="7bcda-145">postfix</span></span>
* <span data-ttu-id="7bcda-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="7bcda-146">qpidd</span></span>
* <span data-ttu-id="7bcda-147">kök</span><span class="sxs-lookup"><span data-stu-id="7bcda-147">root</span></span>
* <span data-ttu-id="7bcda-148">RPC</span><span class="sxs-lookup"><span data-stu-id="7bcda-148">rpc</span></span>
* <span data-ttu-id="7bcda-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="7bcda-149">rpcuser</span></span>
* <span data-ttu-id="7bcda-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="7bcda-150">saslauth</span></span>
* <span data-ttu-id="7bcda-151">kapatma</span><span class="sxs-lookup"><span data-stu-id="7bcda-151">shutdown</span></span>
* <span data-ttu-id="7bcda-152">slocate</span><span class="sxs-lookup"><span data-stu-id="7bcda-152">slocate</span></span>
* <span data-ttu-id="7bcda-153">sshd</span><span class="sxs-lookup"><span data-stu-id="7bcda-153">sshd</span></span>
* <span data-ttu-id="7bcda-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="7bcda-154">stapdev</span></span>
* <span data-ttu-id="7bcda-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="7bcda-155">stapusr</span></span>
* <span data-ttu-id="7bcda-156">Eşitleme</span><span class="sxs-lookup"><span data-stu-id="7bcda-156">sync</span></span>
* <span data-ttu-id="7bcda-157">sys</span><span class="sxs-lookup"><span data-stu-id="7bcda-157">sys</span></span>
* <span data-ttu-id="7bcda-158">bant</span><span class="sxs-lookup"><span data-stu-id="7bcda-158">tape</span></span>
* <span data-ttu-id="7bcda-159">test etme</span><span class="sxs-lookup"><span data-stu-id="7bcda-159">test</span></span>
* <span data-ttu-id="7bcda-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="7bcda-160">tcpdump</span></span>
* <span data-ttu-id="7bcda-161">TTY</span><span class="sxs-lookup"><span data-stu-id="7bcda-161">tty</span></span>
* <span data-ttu-id="7bcda-162">kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="7bcda-162">users</span></span>
* <span data-ttu-id="7bcda-163">utempter</span><span class="sxs-lookup"><span data-stu-id="7bcda-163">utempter</span></span>
* <span data-ttu-id="7bcda-164">utmp</span><span class="sxs-lookup"><span data-stu-id="7bcda-164">utmp</span></span>
* <span data-ttu-id="7bcda-165">UUCP</span><span class="sxs-lookup"><span data-stu-id="7bcda-165">uucp</span></span>
* <span data-ttu-id="7bcda-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="7bcda-166">vcsa</span></span>
* <span data-ttu-id="7bcda-167">video</span><span class="sxs-lookup"><span data-stu-id="7bcda-167">video</span></span>
* <span data-ttu-id="7bcda-168">Tekerlek</span><span class="sxs-lookup"><span data-stu-id="7bcda-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="7bcda-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7bcda-169">Ubuntu</span></span>
* <span data-ttu-id="7bcda-170">adm</span><span class="sxs-lookup"><span data-stu-id="7bcda-170">adm</span></span>
* <span data-ttu-id="7bcda-171">Yönetici</span><span class="sxs-lookup"><span data-stu-id="7bcda-171">admin</span></span>
* <span data-ttu-id="7bcda-172">Ses</span><span class="sxs-lookup"><span data-stu-id="7bcda-172">audio</span></span>
* <span data-ttu-id="7bcda-173">yedekleme</span><span class="sxs-lookup"><span data-stu-id="7bcda-173">backup</span></span>
* <span data-ttu-id="7bcda-174">Depo</span><span class="sxs-lookup"><span data-stu-id="7bcda-174">bin</span></span>
* <span data-ttu-id="7bcda-175">CDROM</span><span class="sxs-lookup"><span data-stu-id="7bcda-175">cdrom</span></span>
* <span data-ttu-id="7bcda-176">crontab</span><span class="sxs-lookup"><span data-stu-id="7bcda-176">crontab</span></span>
* <span data-ttu-id="7bcda-177">arka plan programı</span><span class="sxs-lookup"><span data-stu-id="7bcda-177">daemon</span></span>
* <span data-ttu-id="7bcda-178">araması</span><span class="sxs-lookup"><span data-stu-id="7bcda-178">dialout</span></span>
* <span data-ttu-id="7bcda-179">DIP</span><span class="sxs-lookup"><span data-stu-id="7bcda-179">dip</span></span>
* <span data-ttu-id="7bcda-180">disk</span><span class="sxs-lookup"><span data-stu-id="7bcda-180">disk</span></span>
* <span data-ttu-id="7bcda-181">Faks</span><span class="sxs-lookup"><span data-stu-id="7bcda-181">fax</span></span>
* <span data-ttu-id="7bcda-182">Disket</span><span class="sxs-lookup"><span data-stu-id="7bcda-182">floppy</span></span>
* <span data-ttu-id="7bcda-183">Sigortası</span><span class="sxs-lookup"><span data-stu-id="7bcda-183">fuse</span></span>
* <span data-ttu-id="7bcda-184">Oyunlar</span><span class="sxs-lookup"><span data-stu-id="7bcda-184">games</span></span>
* <span data-ttu-id="7bcda-185">gnats</span><span class="sxs-lookup"><span data-stu-id="7bcda-185">gnats</span></span>
* <span data-ttu-id="7bcda-186">IRC</span><span class="sxs-lookup"><span data-stu-id="7bcda-186">irc</span></span>
* <span data-ttu-id="7bcda-187">kmem</span><span class="sxs-lookup"><span data-stu-id="7bcda-187">kmem</span></span>
* <span data-ttu-id="7bcda-188">Yatay</span><span class="sxs-lookup"><span data-stu-id="7bcda-188">landscape</span></span>
* <span data-ttu-id="7bcda-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="7bcda-189">libuuid</span></span>
* <span data-ttu-id="7bcda-190">Liste</span><span class="sxs-lookup"><span data-stu-id="7bcda-190">list</span></span>
* <span data-ttu-id="7bcda-191">LP</span><span class="sxs-lookup"><span data-stu-id="7bcda-191">lp</span></span>
* <span data-ttu-id="7bcda-192">Posta</span><span class="sxs-lookup"><span data-stu-id="7bcda-192">mail</span></span>
* <span data-ttu-id="7bcda-193">ADAM</span><span class="sxs-lookup"><span data-stu-id="7bcda-193">man</span></span>
* <span data-ttu-id="7bcda-194">MessageBus</span><span class="sxs-lookup"><span data-stu-id="7bcda-194">messagebus</span></span>
* <span data-ttu-id="7bcda-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="7bcda-195">mlocate</span></span>
* <span data-ttu-id="7bcda-196">netdev</span><span class="sxs-lookup"><span data-stu-id="7bcda-196">netdev</span></span>
* <span data-ttu-id="7bcda-197">Haber</span><span class="sxs-lookup"><span data-stu-id="7bcda-197">news</span></span>
* <span data-ttu-id="7bcda-198">hiç kimse</span><span class="sxs-lookup"><span data-stu-id="7bcda-198">nobody</span></span>
* <span data-ttu-id="7bcda-199">hiçbir Grup</span><span class="sxs-lookup"><span data-stu-id="7bcda-199">nogroup</span></span>
* <span data-ttu-id="7bcda-200">işleci</span><span class="sxs-lookup"><span data-stu-id="7bcda-200">operator</span></span>
* <span data-ttu-id="7bcda-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="7bcda-201">plugdev</span></span>
* <span data-ttu-id="7bcda-202">Proxy</span><span class="sxs-lookup"><span data-stu-id="7bcda-202">proxy</span></span>
* <span data-ttu-id="7bcda-203">kök</span><span class="sxs-lookup"><span data-stu-id="7bcda-203">root</span></span>
* <span data-ttu-id="7bcda-204">SASL</span><span class="sxs-lookup"><span data-stu-id="7bcda-204">sasl</span></span>
* <span data-ttu-id="7bcda-205">Gölge</span><span class="sxs-lookup"><span data-stu-id="7bcda-205">shadow</span></span>
* <span data-ttu-id="7bcda-206">src</span><span class="sxs-lookup"><span data-stu-id="7bcda-206">src</span></span>
* <span data-ttu-id="7bcda-207">SSH</span><span class="sxs-lookup"><span data-stu-id="7bcda-207">ssh</span></span>
* <span data-ttu-id="7bcda-208">sshd</span><span class="sxs-lookup"><span data-stu-id="7bcda-208">sshd</span></span>
* <span data-ttu-id="7bcda-209">Personel</span><span class="sxs-lookup"><span data-stu-id="7bcda-209">staff</span></span>
* <span data-ttu-id="7bcda-210">sudo</span><span class="sxs-lookup"><span data-stu-id="7bcda-210">sudo</span></span>
* <span data-ttu-id="7bcda-211">Eşitleme</span><span class="sxs-lookup"><span data-stu-id="7bcda-211">sync</span></span>
* <span data-ttu-id="7bcda-212">sys</span><span class="sxs-lookup"><span data-stu-id="7bcda-212">sys</span></span>
* <span data-ttu-id="7bcda-213">syslog</span><span class="sxs-lookup"><span data-stu-id="7bcda-213">syslog</span></span>
* <span data-ttu-id="7bcda-214">bant</span><span class="sxs-lookup"><span data-stu-id="7bcda-214">tape</span></span>
* <span data-ttu-id="7bcda-215">TTY</span><span class="sxs-lookup"><span data-stu-id="7bcda-215">tty</span></span>
* <span data-ttu-id="7bcda-216">kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="7bcda-216">users</span></span>
* <span data-ttu-id="7bcda-217">utmp</span><span class="sxs-lookup"><span data-stu-id="7bcda-217">utmp</span></span>
* <span data-ttu-id="7bcda-218">UUCP</span><span class="sxs-lookup"><span data-stu-id="7bcda-218">uucp</span></span>
* <span data-ttu-id="7bcda-219">video</span><span class="sxs-lookup"><span data-stu-id="7bcda-219">video</span></span>
* <span data-ttu-id="7bcda-220">Ses</span><span class="sxs-lookup"><span data-stu-id="7bcda-220">voice</span></span>
* <span data-ttu-id="7bcda-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="7bcda-221">whoopsie</span></span>
* <span data-ttu-id="7bcda-222">www-data</span><span class="sxs-lookup"><span data-stu-id="7bcda-222">www-data</span></span>

