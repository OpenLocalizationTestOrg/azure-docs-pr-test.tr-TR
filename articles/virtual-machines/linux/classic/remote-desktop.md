---
title: "aaaRemote Masaüstü tooa Linux VM | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve Uzak Masaüstü tooconnect tooa Microsoft Azure Linux VM'de hello Klasik dağıtım modeli için yapılandırma"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a><span data-ttu-id="9d011-103">Uzak Masaüstü tooconnect tooa Microsoft Azure Linux VM'de kullanma</span><span class="sxs-lookup"><span data-stu-id="9d011-103">Using Remote Desktop tooconnect tooa Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="9d011-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9d011-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9d011-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="9d011-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="9d011-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="9d011-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="9d011-107">Bu makalede Resource Manager sürümü Hello almak için bkz: [burada](../use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="9d011-107">For hello updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="9d011-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9d011-108">Overview</span></span>
<span data-ttu-id="9d011-109">RDP (Uzak Masaüstü Protokolü), Windows için kullanılan özel bir protokoldür.</span><span class="sxs-lookup"><span data-stu-id="9d011-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="9d011-110">Nasıl RDP tooconnect tooa Linux VM (sanal makine) uzaktan kullanabilir?</span><span class="sxs-lookup"><span data-stu-id="9d011-110">How can we use RDP tooconnect tooa Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="9d011-111">Bu kılavuz size verecektir hello yanıt!</span><span class="sxs-lookup"><span data-stu-id="9d011-111">This guidance will give you hello answer!</span></span> <span data-ttu-id="9d011-112">Bu, Microsoft Azure Linux tooit Uzak Masaüstü ile bir Windows makineden erişmenize olanak sağlayan bir VM'nin üzerinde tooinstall ve config xrdp yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9d011-112">It will help you tooinstall and config xrdp on your Microsoft Azure Linux VM, which lets you connect tooit with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="9d011-113">Bu kılavuzu hello örnek olarak Ubuntu veya OpenSUSE çalışan Linux VM kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="9d011-113">We will use Linux VM running Ubuntu or OpenSUSE as hello example in this guidance.</span></span>

<span data-ttu-id="9d011-114">Merhaba xrdp açık kaynak tooconnect sağlayan RDP sunucu Linux sunucunuza Uzak Masaüstü kullanarak bir Windows makineden aracıdır.</span><span class="sxs-lookup"><span data-stu-id="9d011-114">hello xrdp tool is an open source RDP server that allows you tooconnect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="9d011-115">RDP VNC (sanal ağ bilgisayar) daha iyi performans sahiptir.</span><span class="sxs-lookup"><span data-stu-id="9d011-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="9d011-116">VNC JPEG kaliteli grafikler kullanarak işler ve RDP hızlı ve Billur iken yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="9d011-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="9d011-117">Zaten bir Microsoft Azure Linux çalıştıran VM olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d011-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="9d011-118">toocreate ve bir Linux VM ayarlama Bkz hello [Azure Linux VM'de Öğreticisi](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="9d011-118">toocreate and set up a Linux VM, see hello [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="9d011-119">Uzak Masaüstü için bir uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d011-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="9d011-120">Bu belge hello varsayılan uç noktası 3389 Uzak Masaüstü için kullanacağız. 3389 uç noktası olarak ayarlamanız `Remote Desktop` tooyour Linux VM ister altında:</span><span class="sxs-lookup"><span data-stu-id="9d011-120">We will use hello default endpoint 3389 for Remote Desktop in this doc. Set up 3389 endpoint as `Remote Desktop` tooyour Linux VM like below:</span></span>

![Görüntü](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="9d011-122">Bilmiyorsanız, VM için bir uç nokta yukarı tooset nasıl görürüm [bu kılavuz](setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="9d011-122">If you don't know how tooset up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="9d011-123">Gnome Masaüstü yükleme</span><span class="sxs-lookup"><span data-stu-id="9d011-123">Install Gnome Desktop</span></span>
<span data-ttu-id="9d011-124">Linux VM tooyour bağlantı üzerinden `putty`, yükleyip `Gnome Desktop`.</span><span class="sxs-lookup"><span data-stu-id="9d011-124">Connect tooyour Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="9d011-125">Ubuntu için kullanın:</span><span class="sxs-lookup"><span data-stu-id="9d011-125">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="9d011-126">OpenSUSE için kullanın:</span><span class="sxs-lookup"><span data-stu-id="9d011-126">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="9d011-127">Xrdp yükleyin</span><span class="sxs-lookup"><span data-stu-id="9d011-127">Install xrdp</span></span>
<span data-ttu-id="9d011-128">Ubuntu için kullanın:</span><span class="sxs-lookup"><span data-stu-id="9d011-128">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="9d011-129">OpenSUSE için kullanın:</span><span class="sxs-lookup"><span data-stu-id="9d011-129">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="9d011-130">Komutu aşağıdaki hello kullanarak hello sürümüyle Hello OpenSUSE sürüme güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9d011-130">Update hello OpenSUSE version with hello version you are using in hello following command.</span></span> <span data-ttu-id="9d011-131">Aşağıdaki örnek Hello içindir `OpenSUSE 13.2`.</span><span class="sxs-lookup"><span data-stu-id="9d011-131">hello example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="9d011-132">Xrdp başlatın ve önyükleme yukarı xdrp hizmeti ayarlayın</span><span class="sxs-lookup"><span data-stu-id="9d011-132">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="9d011-133">OpenSUSE için kullanın:</span><span class="sxs-lookup"><span data-stu-id="9d011-133">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="9d011-134">Ubuntu için xrdp başlatılır ve yüklemeden sonra otomatik olarak önyükleme yukarı adresindeki eanbled.</span><span class="sxs-lookup"><span data-stu-id="9d011-134">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="9d011-135">Ubuntu 12.04LTS'den sonraki bir Ubuntu sürümü kullanıyorsanız xfce kullanma</span><span class="sxs-lookup"><span data-stu-id="9d011-135">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="9d011-136">Merhaba xrdp geçerli sürümü Gnome Masaüstü Ubuntu sürümleri için daha sonraki Ubuntu 12.04LTS desteklemediğinden, kullanacağız `xfce` Masaüstü yerine.</span><span class="sxs-lookup"><span data-stu-id="9d011-136">Because hello current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="9d011-137">tooinstall `xfce`, bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="9d011-137">tooinstall `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="9d011-138">Daha sonra etkinleştirin `xfce` bu komutu kullanma:</span><span class="sxs-lookup"><span data-stu-id="9d011-138">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="9d011-139">Merhaba yapılandırma dosyasını düzenleyin `/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="9d011-139">Edit hello config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="9d011-140">Merhaba satırı ekleyin `xfce4-session` hello satırından önce `/etc/X11/Xsession`.</span><span class="sxs-lookup"><span data-stu-id="9d011-140">Add hello line `xfce4-session` before hello line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="9d011-141">toorestart Merhaba xrdp hizmeti, bunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="9d011-141">toorestart hello xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="9d011-142">Bir Windows makineden Linux VM Bağlan</span><span class="sxs-lookup"><span data-stu-id="9d011-142">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="9d011-143">Bir Windows makinesinde hello uzak masaüstü istemcisini başlatın ve Linux VM DNS adı girin.</span><span class="sxs-lookup"><span data-stu-id="9d011-143">In a Windows machine, start hello Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="9d011-144">Veya toohello hello Azure portal, VM'yi Pano gidip tıklayın `Connect` tooconnect Linux VM.</span><span class="sxs-lookup"><span data-stu-id="9d011-144">Or go toohello Dashboard of your VM in hello Azure portal and click `Connect` tooconnect your Linux VM.</span></span> <span data-ttu-id="9d011-145">Bu durumda, hello oturum açma penceresi görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="9d011-145">In that case, you see hello login window:</span></span>

![Görüntü](./media/remote-desktop/no2.png)

<span data-ttu-id="9d011-147">Merhaba kullanıcı adı ve parola, Linux VM oturum.</span><span class="sxs-lookup"><span data-stu-id="9d011-147">Log in with hello user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d011-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9d011-148">Next steps</span></span>
<span data-ttu-id="9d011-149">Xrdp kullanma hakkında daha fazla bilgi için bkz: [http://www.xrdp.org/](http://www.xrdp.org/).</span><span class="sxs-lookup"><span data-stu-id="9d011-149">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
