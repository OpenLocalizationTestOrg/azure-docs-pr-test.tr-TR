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
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a>Uzak Masaüstü tooconnect tooa Microsoft Azure Linux VM'de kullanma
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Bu makalede Resource Manager sürümü Hello almak için bkz: [burada](../use-remote-desktop.md).

## <a name="overview"></a>Genel Bakış
RDP (Uzak Masaüstü Protokolü), Windows için kullanılan özel bir protokoldür. Nasıl RDP tooconnect tooa Linux VM (sanal makine) uzaktan kullanabilir?

Bu kılavuz size verecektir hello yanıt! Bu, Microsoft Azure Linux tooit Uzak Masaüstü ile bir Windows makineden erişmenize olanak sağlayan bir VM'nin üzerinde tooinstall ve config xrdp yardımcı olur. Bu kılavuzu hello örnek olarak Ubuntu veya OpenSUSE çalışan Linux VM kullanacağız.

Merhaba xrdp açık kaynak tooconnect sağlayan RDP sunucu Linux sunucunuza Uzak Masaüstü kullanarak bir Windows makineden aracıdır. RDP VNC (sanal ağ bilgisayar) daha iyi performans sahiptir. VNC JPEG kaliteli grafikler kullanarak işler ve RDP hızlı ve Billur iken yavaş olabilir.

> [!NOTE]
> Zaten bir Microsoft Azure Linux çalıştıran VM olması gerekir. toocreate ve bir Linux VM ayarlama Bkz hello [Azure Linux VM'de Öğreticisi](createportal.md).
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a>Uzak Masaüstü için bir uç noktası oluşturma
Bu belge hello varsayılan uç noktası 3389 Uzak Masaüstü için kullanacağız. 3389 uç noktası olarak ayarlamanız `Remote Desktop` tooyour Linux VM ister altında:

![Görüntü](./media/remote-desktop/endpoint-for-linux-server.png)

Bilmiyorsanız, VM için bir uç nokta yukarı tooset nasıl görürüm [bu kılavuz](setup-endpoints.md).

## <a name="install-gnome-desktop"></a>Gnome Masaüstü yükleme
Linux VM tooyour bağlantı üzerinden `putty`, yükleyip `Gnome Desktop`.

Ubuntu için kullanın:

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


OpenSUSE için kullanın:

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a>Xrdp yükleyin
Ubuntu için kullanın:

    #sudo apt-get install xrdp

OpenSUSE için kullanın:

> [!NOTE]
> Komutu aşağıdaki hello kullanarak hello sürümüyle Hello OpenSUSE sürüme güncelleştirin. Aşağıdaki örnek Hello içindir `OpenSUSE 13.2`.
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a>Xrdp başlatın ve önyükleme yukarı xdrp hizmeti ayarlayın
OpenSUSE için kullanın:

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

Ubuntu için xrdp başlatılır ve yüklemeden sonra otomatik olarak önyükleme yukarı adresindeki eanbled.

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a>Ubuntu 12.04LTS'den sonraki bir Ubuntu sürümü kullanıyorsanız xfce kullanma
Merhaba xrdp geçerli sürümü Gnome Masaüstü Ubuntu sürümleri için daha sonraki Ubuntu 12.04LTS desteklemediğinden, kullanacağız `xfce` Masaüstü yerine.

tooinstall `xfce`, bu komutu kullanın:

    #sudo apt-get install xubuntu-desktop

Daha sonra etkinleştirin `xfce` bu komutu kullanma:

    #echo xfce4-session >~/.xsession

Merhaba yapılandırma dosyasını düzenleyin `/etc/xrdp/startwm.sh`:

    #sudo vi /etc/xrdp/startwm.sh   

Merhaba satırı ekleyin `xfce4-session` hello satırından önce `/etc/X11/Xsession`.

toorestart Merhaba xrdp hizmeti, bunu kullanın:

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a>Bir Windows makineden Linux VM Bağlan
Bir Windows makinesinde hello uzak masaüstü istemcisini başlatın ve Linux VM DNS adı girin. Veya toohello hello Azure portal, VM'yi Pano gidip tıklayın `Connect` tooconnect Linux VM. Bu durumda, hello oturum açma penceresi görürsünüz:

![Görüntü](./media/remote-desktop/no2.png)

Merhaba kullanıcı adı ve parola, Linux VM oturum.

## <a name="next-steps"></a>Sonraki adımlar
Xrdp kullanma hakkında daha fazla bilgi için bkz: [http://www.xrdp.org/](http://www.xrdp.org/).
