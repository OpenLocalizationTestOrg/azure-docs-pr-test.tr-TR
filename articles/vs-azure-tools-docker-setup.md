---
title: "Docker ana bilgisayar ile VirtualBox yapılandırma | Microsoft Docs"
description: "Docker makine ve VirtualBox kullanarak varsayılan Docker örneği yapılandırmak için adım adım yönergeler"
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
ms.openlocfilehash: e9465afb560a73d74f853c19094b3ee75b8c470c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="06fa9-103">Docker ana bilgisayar ile VirtualBox yapılandırma</span><span class="sxs-lookup"><span data-stu-id="06fa9-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="06fa9-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="06fa9-104">Overview</span></span>
<span data-ttu-id="06fa9-105">Bu makalede, Docker makine ve VirtualBox kullanarak varsayılan Docker örneği yapılandırırken size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="06fa9-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="06fa9-106">Kullanıyorsanız, [Windows için Docker beta](http://beta.docker.com/), bu yapılandırma gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="06fa9-106">If you’re using the [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06fa9-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="06fa9-107">Prerequisites</span></span>
<span data-ttu-id="06fa9-108">Aşağıdaki araçları yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="06fa9-108">The following tools need to be installed.</span></span>

* [<span data-ttu-id="06fa9-109">Docker araç kutusu</span><span class="sxs-lookup"><span data-stu-id="06fa9-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-the-docker-client-with-windows-powershell"></a><span data-ttu-id="06fa9-110">Windows PowerShell ile Docker istemci yapılandırma</span><span class="sxs-lookup"><span data-stu-id="06fa9-110">Configuring the Docker client with Windows PowerShell</span></span>
<span data-ttu-id="06fa9-111">Docker istemciyi yapılandırmak için yalnızca Windows PowerShell'i açın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="06fa9-111">To configure a Docker client, simply open Windows PowerShell, and perform the following steps:</span></span>

1. <span data-ttu-id="06fa9-112">Bir varsayılan docker ana bilgisayar örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06fa9-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="06fa9-113">Varsayılan örnek yapılandırılmış ve çalışıyor olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="06fa9-113">Verify the default instance is configured and running.</span></span> <span data-ttu-id="06fa9-114">(Çalışan'default ' adlı bir örneği görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="06fa9-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker makine ls çıktı][0]
3. <span data-ttu-id="06fa9-116">Varsayılan geçerli konağı ayarlayın ve kabuğunuzu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="06fa9-116">Set default as the current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="06fa9-117">Etkin Docker kapsayıcıları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="06fa9-117">Display the active Docker containers.</span></span> <span data-ttu-id="06fa9-118">Liste boş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="06fa9-118">The list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps çıktı][1]

> [!NOTE]
> <span data-ttu-id="06fa9-120">Geliştirme makinenizi yeniden başlatmanız her zaman yerel docker ana bilgisayarınız yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="06fa9-120">Each time you reboot your development machine, you’ll need to restart your local docker host.</span></span>
> <span data-ttu-id="06fa9-121">Bunu yapmak için bir komut isteminde aşağıdaki komutu sorun: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="06fa9-121">To do this, issue the following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
