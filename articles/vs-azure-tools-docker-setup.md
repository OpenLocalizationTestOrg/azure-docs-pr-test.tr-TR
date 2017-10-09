---
title: aaaConfigure Docker ana VirtualBox ile | Microsoft Docs
description: "Adım adım yönergeler tooconfigure Docker varsayılan örnek Docker makine ve VirtualBox kullanma"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a>Docker ana bilgisayar ile VirtualBox yapılandırma
## <a name="overview"></a>Genel Bakış
Bu makalede, Docker makine ve VirtualBox kullanarak varsayılan Docker örneği yapılandırırken size rehberlik eder. Merhaba kullanıyorsanız [Windows için Docker beta](http://beta.docker.com/), bu yapılandırma gerekli değildir.

## <a name="prerequisites"></a>Ön koşullar
Merhaba aşağıdaki araçları yüklü toobe gerekir.

* [Docker araç kutusu](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a>Windows PowerShell ile Merhaba Docker istemci yapılandırma
tooconfigure Docker istemci yalnızca Windows PowerShell'i açın ve hello aşağıdaki adımları gerçekleştirin:

1. Bir varsayılan docker ana bilgisayar örneği oluşturun.
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. Merhaba varsayılan örnek yapılandırılmış ve çalışıyor olduğunu doğrulayın. (Çalışan'default ' adlı bir örneği görmeniz gerekir.
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker makine ls çıktı][0]
3. Varsayılan hello geçerli ana bilgisayar olarak ayarlayın ve kabuğunuzu yapılandırın.
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. Merhaba active Docker kapsayıcıları görüntüleyin. Merhaba listesi boş olmalıdır.
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps çıktı][1]

> [!NOTE]
> Geliştirme makinenizi yeniden başlatmanız her zaman yerel docker ana bilgisayarınız toorestart gerekir.
> toodo komutu bir komut isteminde aşağıdaki Bu, sorun hello: `docker-machine start default`.
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
