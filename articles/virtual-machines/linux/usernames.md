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
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="0425a-103">Azure’da Linux için Kullanıcı Adları Seçme</span><span class="sxs-lookup"><span data-stu-id="0425a-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="0425a-104">Azure üzerinde bir Linux sanal makine sağlarken, daha sonra VM'de oturum açmak için kullanabileceğiniz bir kök olmayan kullanıcının adını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0425a-104">When you provision a Linux virtual machine on Azure you must specify the name of a non-root user that you can later use to log into the VM.</span></span> <span data-ttu-id="0425a-105">Yeni kullanıcı adını seçebilir veya Azure Klasik portalı üzerinden sağlama değişirse "azureuser" varsayılan adı kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="0425a-105">You may choose the name of the new user, or if provisioning via the Azure classic portal you can accept the default name "azureuser".</span></span>

<span data-ttu-id="0425a-106">Çoğu durumda bu kullanıcı temel görüntü var olmaz ve sağlama işlemi sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0425a-106">In most cases this user won't exist on the base image and will be created during the provisioning process.</span></span> <span data-ttu-id="0425a-107">Ardından kullanıcı üzerinde temel VM görüntü varsa, Azure Linux Aracısı'nı parola ve/veya VM oluşturulurken belirtilen bilgilere göre bu kullanıcı için SSH anahtarı yalnızca yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="0425a-107">If the user exists on the base VM image, then the Azure Linux agent simply configures the password and/or SSH key for that user based on the information you specified when creating the VM.</span></span>

<span data-ttu-id="0425a-108">**Ancak**, Linux kullanılmaması gereken kullanıcı adları kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0425a-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="0425a-109">Sağlama işlemi **başarısız** UID 0-99 olan bir kullanıcı olarak tanımlanan bir varolan bir sistem kullanıcı kullanarak bir Linux VM sağlayacak çalışırsanız.</span><span class="sxs-lookup"><span data-stu-id="0425a-109">The provisioning process will **fail** if you try to provision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="0425a-110">Tipik bir örnektir `root` UID 0 olan kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="0425a-110">A typical example is the `root` user, which has UID 0.</span></span>

* <span data-ttu-id="0425a-111">Ayrıca bkz: [Linux standart Base - kullanıcı kimliği aralıkları](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="0425a-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="0425a-112">Aşağıdakiler, CentOS ve Ubuntu Linux sanal makine azure'da sağlamada yapmaktan kaçınmalısınız ortak yerleşik sistem kullanıcıların bir listesidir.</span><span class="sxs-lookup"><span data-stu-id="0425a-112">The following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="0425a-113">Bu liste yalnızca bir örnek, seçtiğiniz kullanıcı adı ile var olan bir sistem kullanıcı çakışmadığından emin olmak, dağıtım için belgelere başvurun.</span><span class="sxs-lookup"><span data-stu-id="0425a-113">This list is just an example, please refer to the documentation for your distribution to ensure that the username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="0425a-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="0425a-114">CentOS</span></span>
* <span data-ttu-id="0425a-115">abrt</span><span class="sxs-lookup"><span data-stu-id="0425a-115">abrt</span></span>
* <span data-ttu-id="0425a-116">adm</span><span class="sxs-lookup"><span data-stu-id="0425a-116">adm</span></span>
* <span data-ttu-id="0425a-117">Ses</span><span class="sxs-lookup"><span data-stu-id="0425a-117">audio</span></span>
* <span data-ttu-id="0425a-118">Depo</span><span class="sxs-lookup"><span data-stu-id="0425a-118">bin</span></span>
* <span data-ttu-id="0425a-119">CDROM</span><span class="sxs-lookup"><span data-stu-id="0425a-119">cdrom</span></span>
* <span data-ttu-id="0425a-120">cgred</span><span class="sxs-lookup"><span data-stu-id="0425a-120">cgred</span></span>
* <span data-ttu-id="0425a-121">arka plan programı</span><span class="sxs-lookup"><span data-stu-id="0425a-121">daemon</span></span>
* <span data-ttu-id="0425a-122">dbus</span><span class="sxs-lookup"><span data-stu-id="0425a-122">dbus</span></span>
* <span data-ttu-id="0425a-123">araması</span><span class="sxs-lookup"><span data-stu-id="0425a-123">dialout</span></span>
* <span data-ttu-id="0425a-124">DIP</span><span class="sxs-lookup"><span data-stu-id="0425a-124">dip</span></span>
* <span data-ttu-id="0425a-125">disk</span><span class="sxs-lookup"><span data-stu-id="0425a-125">disk</span></span>
* <span data-ttu-id="0425a-126">Disket</span><span class="sxs-lookup"><span data-stu-id="0425a-126">floppy</span></span>
* <span data-ttu-id="0425a-127">FTP</span><span class="sxs-lookup"><span data-stu-id="0425a-127">ftp</span></span>
* <span data-ttu-id="0425a-128">FTP</span><span class="sxs-lookup"><span data-stu-id="0425a-128">ftp</span></span>
* <span data-ttu-id="0425a-129">Oyunlar</span><span class="sxs-lookup"><span data-stu-id="0425a-129">games</span></span>
* <span data-ttu-id="0425a-130">Gopher</span><span class="sxs-lookup"><span data-stu-id="0425a-130">gopher</span></span>
* <span data-ttu-id="0425a-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="0425a-131">haldaemon</span></span>
* <span data-ttu-id="0425a-132">durdurma</span><span class="sxs-lookup"><span data-stu-id="0425a-132">halt</span></span>
* <span data-ttu-id="0425a-133">kmem</span><span class="sxs-lookup"><span data-stu-id="0425a-133">kmem</span></span>
* <span data-ttu-id="0425a-134">kilitleme</span><span class="sxs-lookup"><span data-stu-id="0425a-134">lock</span></span>
* <span data-ttu-id="0425a-135">LP</span><span class="sxs-lookup"><span data-stu-id="0425a-135">lp</span></span>
* <span data-ttu-id="0425a-136">Posta</span><span class="sxs-lookup"><span data-stu-id="0425a-136">mail</span></span>
* <span data-ttu-id="0425a-137">ADAM</span><span class="sxs-lookup"><span data-stu-id="0425a-137">man</span></span>
* <span data-ttu-id="0425a-138">mem</span><span class="sxs-lookup"><span data-stu-id="0425a-138">mem</span></span>
* <span data-ttu-id="0425a-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="0425a-139">nfsnobody</span></span>
* <span data-ttu-id="0425a-140">hiç kimse</span><span class="sxs-lookup"><span data-stu-id="0425a-140">nobody</span></span>
* <span data-ttu-id="0425a-141">NTP</span><span class="sxs-lookup"><span data-stu-id="0425a-141">ntp</span></span>
* <span data-ttu-id="0425a-142">işleci</span><span class="sxs-lookup"><span data-stu-id="0425a-142">operator</span></span>
* <span data-ttu-id="0425a-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="0425a-143">oprofile</span></span>
* <span data-ttu-id="0425a-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="0425a-144">postdrop</span></span>
* <span data-ttu-id="0425a-145">sonek</span><span class="sxs-lookup"><span data-stu-id="0425a-145">postfix</span></span>
* <span data-ttu-id="0425a-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="0425a-146">qpidd</span></span>
* <span data-ttu-id="0425a-147">kök</span><span class="sxs-lookup"><span data-stu-id="0425a-147">root</span></span>
* <span data-ttu-id="0425a-148">RPC</span><span class="sxs-lookup"><span data-stu-id="0425a-148">rpc</span></span>
* <span data-ttu-id="0425a-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="0425a-149">rpcuser</span></span>
* <span data-ttu-id="0425a-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="0425a-150">saslauth</span></span>
* <span data-ttu-id="0425a-151">kapatma</span><span class="sxs-lookup"><span data-stu-id="0425a-151">shutdown</span></span>
* <span data-ttu-id="0425a-152">slocate</span><span class="sxs-lookup"><span data-stu-id="0425a-152">slocate</span></span>
* <span data-ttu-id="0425a-153">sshd</span><span class="sxs-lookup"><span data-stu-id="0425a-153">sshd</span></span>
* <span data-ttu-id="0425a-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="0425a-154">stapdev</span></span>
* <span data-ttu-id="0425a-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="0425a-155">stapusr</span></span>
* <span data-ttu-id="0425a-156">Eşitleme</span><span class="sxs-lookup"><span data-stu-id="0425a-156">sync</span></span>
* <span data-ttu-id="0425a-157">sys</span><span class="sxs-lookup"><span data-stu-id="0425a-157">sys</span></span>
* <span data-ttu-id="0425a-158">bant</span><span class="sxs-lookup"><span data-stu-id="0425a-158">tape</span></span>
* <span data-ttu-id="0425a-159">test etme</span><span class="sxs-lookup"><span data-stu-id="0425a-159">test</span></span>
* <span data-ttu-id="0425a-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="0425a-160">tcpdump</span></span>
* <span data-ttu-id="0425a-161">TTY</span><span class="sxs-lookup"><span data-stu-id="0425a-161">tty</span></span>
* <span data-ttu-id="0425a-162">kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="0425a-162">users</span></span>
* <span data-ttu-id="0425a-163">utempter</span><span class="sxs-lookup"><span data-stu-id="0425a-163">utempter</span></span>
* <span data-ttu-id="0425a-164">utmp</span><span class="sxs-lookup"><span data-stu-id="0425a-164">utmp</span></span>
* <span data-ttu-id="0425a-165">UUCP</span><span class="sxs-lookup"><span data-stu-id="0425a-165">uucp</span></span>
* <span data-ttu-id="0425a-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="0425a-166">vcsa</span></span>
* <span data-ttu-id="0425a-167">video</span><span class="sxs-lookup"><span data-stu-id="0425a-167">video</span></span>
* <span data-ttu-id="0425a-168">Tekerlek</span><span class="sxs-lookup"><span data-stu-id="0425a-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="0425a-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0425a-169">Ubuntu</span></span>
* <span data-ttu-id="0425a-170">adm</span><span class="sxs-lookup"><span data-stu-id="0425a-170">adm</span></span>
* <span data-ttu-id="0425a-171">Yönetici</span><span class="sxs-lookup"><span data-stu-id="0425a-171">admin</span></span>
* <span data-ttu-id="0425a-172">Ses</span><span class="sxs-lookup"><span data-stu-id="0425a-172">audio</span></span>
* <span data-ttu-id="0425a-173">yedekleme</span><span class="sxs-lookup"><span data-stu-id="0425a-173">backup</span></span>
* <span data-ttu-id="0425a-174">Depo</span><span class="sxs-lookup"><span data-stu-id="0425a-174">bin</span></span>
* <span data-ttu-id="0425a-175">CDROM</span><span class="sxs-lookup"><span data-stu-id="0425a-175">cdrom</span></span>
* <span data-ttu-id="0425a-176">crontab</span><span class="sxs-lookup"><span data-stu-id="0425a-176">crontab</span></span>
* <span data-ttu-id="0425a-177">arka plan programı</span><span class="sxs-lookup"><span data-stu-id="0425a-177">daemon</span></span>
* <span data-ttu-id="0425a-178">araması</span><span class="sxs-lookup"><span data-stu-id="0425a-178">dialout</span></span>
* <span data-ttu-id="0425a-179">DIP</span><span class="sxs-lookup"><span data-stu-id="0425a-179">dip</span></span>
* <span data-ttu-id="0425a-180">disk</span><span class="sxs-lookup"><span data-stu-id="0425a-180">disk</span></span>
* <span data-ttu-id="0425a-181">Faks</span><span class="sxs-lookup"><span data-stu-id="0425a-181">fax</span></span>
* <span data-ttu-id="0425a-182">Disket</span><span class="sxs-lookup"><span data-stu-id="0425a-182">floppy</span></span>
* <span data-ttu-id="0425a-183">Sigortası</span><span class="sxs-lookup"><span data-stu-id="0425a-183">fuse</span></span>
* <span data-ttu-id="0425a-184">Oyunlar</span><span class="sxs-lookup"><span data-stu-id="0425a-184">games</span></span>
* <span data-ttu-id="0425a-185">gnats</span><span class="sxs-lookup"><span data-stu-id="0425a-185">gnats</span></span>
* <span data-ttu-id="0425a-186">IRC</span><span class="sxs-lookup"><span data-stu-id="0425a-186">irc</span></span>
* <span data-ttu-id="0425a-187">kmem</span><span class="sxs-lookup"><span data-stu-id="0425a-187">kmem</span></span>
* <span data-ttu-id="0425a-188">Yatay</span><span class="sxs-lookup"><span data-stu-id="0425a-188">landscape</span></span>
* <span data-ttu-id="0425a-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="0425a-189">libuuid</span></span>
* <span data-ttu-id="0425a-190">Liste</span><span class="sxs-lookup"><span data-stu-id="0425a-190">list</span></span>
* <span data-ttu-id="0425a-191">LP</span><span class="sxs-lookup"><span data-stu-id="0425a-191">lp</span></span>
* <span data-ttu-id="0425a-192">Posta</span><span class="sxs-lookup"><span data-stu-id="0425a-192">mail</span></span>
* <span data-ttu-id="0425a-193">ADAM</span><span class="sxs-lookup"><span data-stu-id="0425a-193">man</span></span>
* <span data-ttu-id="0425a-194">MessageBus</span><span class="sxs-lookup"><span data-stu-id="0425a-194">messagebus</span></span>
* <span data-ttu-id="0425a-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="0425a-195">mlocate</span></span>
* <span data-ttu-id="0425a-196">netdev</span><span class="sxs-lookup"><span data-stu-id="0425a-196">netdev</span></span>
* <span data-ttu-id="0425a-197">Haber</span><span class="sxs-lookup"><span data-stu-id="0425a-197">news</span></span>
* <span data-ttu-id="0425a-198">hiç kimse</span><span class="sxs-lookup"><span data-stu-id="0425a-198">nobody</span></span>
* <span data-ttu-id="0425a-199">hiçbir Grup</span><span class="sxs-lookup"><span data-stu-id="0425a-199">nogroup</span></span>
* <span data-ttu-id="0425a-200">işleci</span><span class="sxs-lookup"><span data-stu-id="0425a-200">operator</span></span>
* <span data-ttu-id="0425a-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="0425a-201">plugdev</span></span>
* <span data-ttu-id="0425a-202">Proxy</span><span class="sxs-lookup"><span data-stu-id="0425a-202">proxy</span></span>
* <span data-ttu-id="0425a-203">kök</span><span class="sxs-lookup"><span data-stu-id="0425a-203">root</span></span>
* <span data-ttu-id="0425a-204">SASL</span><span class="sxs-lookup"><span data-stu-id="0425a-204">sasl</span></span>
* <span data-ttu-id="0425a-205">Gölge</span><span class="sxs-lookup"><span data-stu-id="0425a-205">shadow</span></span>
* <span data-ttu-id="0425a-206">src</span><span class="sxs-lookup"><span data-stu-id="0425a-206">src</span></span>
* <span data-ttu-id="0425a-207">SSH</span><span class="sxs-lookup"><span data-stu-id="0425a-207">ssh</span></span>
* <span data-ttu-id="0425a-208">sshd</span><span class="sxs-lookup"><span data-stu-id="0425a-208">sshd</span></span>
* <span data-ttu-id="0425a-209">Personel</span><span class="sxs-lookup"><span data-stu-id="0425a-209">staff</span></span>
* <span data-ttu-id="0425a-210">sudo</span><span class="sxs-lookup"><span data-stu-id="0425a-210">sudo</span></span>
* <span data-ttu-id="0425a-211">Eşitleme</span><span class="sxs-lookup"><span data-stu-id="0425a-211">sync</span></span>
* <span data-ttu-id="0425a-212">sys</span><span class="sxs-lookup"><span data-stu-id="0425a-212">sys</span></span>
* <span data-ttu-id="0425a-213">syslog</span><span class="sxs-lookup"><span data-stu-id="0425a-213">syslog</span></span>
* <span data-ttu-id="0425a-214">bant</span><span class="sxs-lookup"><span data-stu-id="0425a-214">tape</span></span>
* <span data-ttu-id="0425a-215">TTY</span><span class="sxs-lookup"><span data-stu-id="0425a-215">tty</span></span>
* <span data-ttu-id="0425a-216">kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="0425a-216">users</span></span>
* <span data-ttu-id="0425a-217">utmp</span><span class="sxs-lookup"><span data-stu-id="0425a-217">utmp</span></span>
* <span data-ttu-id="0425a-218">UUCP</span><span class="sxs-lookup"><span data-stu-id="0425a-218">uucp</span></span>
* <span data-ttu-id="0425a-219">video</span><span class="sxs-lookup"><span data-stu-id="0425a-219">video</span></span>
* <span data-ttu-id="0425a-220">Ses</span><span class="sxs-lookup"><span data-stu-id="0425a-220">voice</span></span>
* <span data-ttu-id="0425a-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="0425a-221">whoopsie</span></span>
* <span data-ttu-id="0425a-222">www-data</span><span class="sxs-lookup"><span data-stu-id="0425a-222">www-data</span></span>

