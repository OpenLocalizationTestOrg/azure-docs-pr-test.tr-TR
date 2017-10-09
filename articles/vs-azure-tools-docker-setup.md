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
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="cbb93-103">Docker ana bilgisayar ile VirtualBox yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cbb93-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="cbb93-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cbb93-104">Overview</span></span>
<span data-ttu-id="cbb93-105">Bu makalede, Docker makine ve VirtualBox kullanarak varsayılan Docker örneği yapılandırırken size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="cbb93-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="cbb93-106">Merhaba kullanıyorsanız [Windows için Docker beta](http://beta.docker.com/), bu yapılandırma gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="cbb93-106">If you’re using hello [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbb93-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cbb93-107">Prerequisites</span></span>
<span data-ttu-id="cbb93-108">Merhaba aşağıdaki araçları yüklü toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbb93-108">hello following tools need toobe installed.</span></span>

* [<span data-ttu-id="cbb93-109">Docker araç kutusu</span><span class="sxs-lookup"><span data-stu-id="cbb93-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a><span data-ttu-id="cbb93-110">Windows PowerShell ile Merhaba Docker istemci yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cbb93-110">Configuring hello Docker client with Windows PowerShell</span></span>
<span data-ttu-id="cbb93-111">tooconfigure Docker istemci yalnızca Windows PowerShell'i açın ve hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cbb93-111">tooconfigure a Docker client, simply open Windows PowerShell, and perform hello following steps:</span></span>

1. <span data-ttu-id="cbb93-112">Bir varsayılan docker ana bilgisayar örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbb93-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="cbb93-113">Merhaba varsayılan örnek yapılandırılmış ve çalışıyor olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cbb93-113">Verify hello default instance is configured and running.</span></span> <span data-ttu-id="cbb93-114">(Çalışan'default ' adlı bir örneği görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbb93-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker makine ls çıktı][0]
3. <span data-ttu-id="cbb93-116">Varsayılan hello geçerli ana bilgisayar olarak ayarlayın ve kabuğunuzu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cbb93-116">Set default as hello current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="cbb93-117">Merhaba active Docker kapsayıcıları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="cbb93-117">Display hello active Docker containers.</span></span> <span data-ttu-id="cbb93-118">Merhaba listesi boş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cbb93-118">hello list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps çıktı][1]

> [!NOTE]
> <span data-ttu-id="cbb93-120">Geliştirme makinenizi yeniden başlatmanız her zaman yerel docker ana bilgisayarınız toorestart gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbb93-120">Each time you reboot your development machine, you’ll need toorestart your local docker host.</span></span>
> <span data-ttu-id="cbb93-121">toodo komutu bir komut isteminde aşağıdaki Bu, sorun hello: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="cbb93-121">toodo this, issue hello following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
