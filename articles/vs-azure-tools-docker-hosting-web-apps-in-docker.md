---
title: "bir ASP.NET Core Linux Docker kapsayıcısı tooa uzak Docker ana aaaDeploy | Microsoft Docs"
description: "Bir Azure Docker ana Linux VM üzerinde çalışan uygulama tooa Docker kapsayıcısı Docker toodeploy ASP.NET Core için Visual Studio Araçları toouse nasıl web öğrenin"
services: azure-container-service
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.service: azure-container-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 27b0c6420628c73220200bc071b47a4cd89fff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a><span data-ttu-id="c41f7-103">Bir ASP.NET kapsayıcı tooa uzak Docker ana dağıtma</span><span class="sxs-lookup"><span data-stu-id="c41f7-103">Deploy an ASP.NET container tooa remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="c41f7-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c41f7-104">Overview</span></span>
<span data-ttu-id="c41f7-105">Docker olan bazı yolları tooa sanal hangi yapabilecekleriniz makinede, benzer bir basit kapsayıcı altyapısı toohost uygulamaları ve Hizmetleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="c41f7-105">Docker is a lightweight container engine, similar in some ways tooa virtual machine, which you can use toohost applications and services.</span></span>
<span data-ttu-id="c41f7-106">Bu öğretici, hello kullanarak kılavuzluk [Docker için Visual Studio Araçları](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) uzantısı toodeploy Azure PowerShell kullanarak bir ASP.NET Core uygulama tooa Docker konağında.</span><span class="sxs-lookup"><span data-stu-id="c41f7-106">This tutorial walks you through using hello [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension toodeploy an ASP.NET Core app tooa Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c41f7-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c41f7-107">Prerequisites</span></span>
<span data-ttu-id="c41f7-108">Merhaba aşağıdaki gerekli toocomplete bu öğreticidir:</span><span class="sxs-lookup"><span data-stu-id="c41f7-108">hello following is required toocomplete this tutorial:</span></span>

* <span data-ttu-id="c41f7-109">Bir Azure Docker ana VM açıklandığı gibi oluşturmak [nasıl toouse docker-makine Azure ile](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c41f7-109">Create an Azure Docker Host VM as described in [How toouse docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="c41f7-110">Merhaba en son sürümünü yüklemek [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="c41f7-110">Install hello latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="c41f7-111">Merhaba karşıdan [Microsoft ASP.NET Core 1.0 SDK'sı](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="c41f7-111">Download hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="c41f7-112">Yükleme [Windows için Docker](https://docs.docker.com/docker-for-windows/install/)</span><span class="sxs-lookup"><span data-stu-id="c41f7-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="c41f7-113">1. Bir ASP.NET Core web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="c41f7-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="c41f7-114">Merhaba aşağıdaki adımlar, bu öğreticide kullanılan temel bir ASP.NET Core uygulama oluşturmada size yol.</span><span class="sxs-lookup"><span data-stu-id="c41f7-114">hello following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="c41f7-115">2. Docker desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="c41f7-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a><span data-ttu-id="c41f7-116">3. Merhaba DockerTask.ps1 PowerShell Betiği kullanın</span><span class="sxs-lookup"><span data-stu-id="c41f7-116">3. Use hello DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="c41f7-117">Bir PowerShell komut istemi toohello kök dizin projenizin açın.</span><span class="sxs-lookup"><span data-stu-id="c41f7-117">Open a PowerShell prompt toohello root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="c41f7-118">Doğrulama hello uzak ana bilgisayarda çalışır.</span><span class="sxs-lookup"><span data-stu-id="c41f7-118">Validate hello remote host is running.</span></span> <span data-ttu-id="c41f7-119">Durumunu görmelisiniz çalışan =</span><span class="sxs-lookup"><span data-stu-id="c41f7-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="c41f7-120">Yapı hello uygulamasını kullanarak hello - yapı parametresi</span><span class="sxs-lookup"><span data-stu-id="c41f7-120">Build hello app using hello -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="c41f7-121">Merhaba uygulama çalıştırma hello kullanarak - Çalıştır parametresi</span><span class="sxs-lookup"><span data-stu-id="c41f7-121">Run hello app, using hello -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="c41f7-122">Docker işlemi tamamlandıktan sonra benzer toohello aşağıdaki sonuçları görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="c41f7-122">Once docker completes, you should see results similar toohello following:</span></span>
   
   ![Uygulamanızı görüntülemek][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
