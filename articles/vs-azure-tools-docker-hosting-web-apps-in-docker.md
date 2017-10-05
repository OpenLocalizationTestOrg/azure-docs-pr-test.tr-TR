---
title: "Bir ASP.NET Core Linux Docker kapsayıcısı uzak bir Docker konağına dağıtın | Microsoft Docs"
description: "Bir Azure Docker ana Linux VM'de çalışan bir Docker kapsayıcısı ASP.NET Core web uygulama dağıtmak için Docker için Visual Studio Araçları kullanmayı öğrenin"
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
ms.openlocfilehash: 4a87ee69f23779bf4f6f5db40bc05edbcfc7668d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-aspnet-container-to-a-remote-docker-host"></a><span data-ttu-id="88a1d-103">Bir ASP.NET kapsayıcısı uzak bir Docker konağına dağıtın</span><span class="sxs-lookup"><span data-stu-id="88a1d-103">Deploy an ASP.NET container to a remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="88a1d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="88a1d-104">Overview</span></span>
<span data-ttu-id="88a1d-105">Docker ana uygulamalar ve hizmetler için kullanabileceğiniz bir sanal makineye, bazı şekillerde benzer bir basit kapsayıcı alt yapısıdır.</span><span class="sxs-lookup"><span data-stu-id="88a1d-105">Docker is a lightweight container engine, similar in some ways to a virtual machine, which you can use to host applications and services.</span></span>
<span data-ttu-id="88a1d-106">Bu öğretici, kullanarak kılavuzluk [Docker için Visual Studio Araçları](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) Docker konağına PowerShell kullanarak Azure üzerinde ASP.NET Core uygulama dağıtmak için uzantı.</span><span class="sxs-lookup"><span data-stu-id="88a1d-106">This tutorial walks you through using the [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension to deploy an ASP.NET Core app to a Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88a1d-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="88a1d-107">Prerequisites</span></span>
<span data-ttu-id="88a1d-108">Aşağıdakiler bu öğreticiyi tamamlamak için gereklidir:</span><span class="sxs-lookup"><span data-stu-id="88a1d-108">The following is required to complete this tutorial:</span></span>

* <span data-ttu-id="88a1d-109">Bir Azure Docker ana VM açıklandığı gibi oluşturmak [docker makine Azure ile kullanma](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="88a1d-109">Create an Azure Docker Host VM as described in [How to use docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="88a1d-110">En son sürümünü yüklemek [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="88a1d-110">Install the latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="88a1d-111">Karşıdan [Microsoft ASP.NET Core 1.0 SDK'sı](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="88a1d-111">Download the [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="88a1d-112">Yükleme [Windows için Docker](https://docs.docker.com/docker-for-windows/install/)</span><span class="sxs-lookup"><span data-stu-id="88a1d-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="88a1d-113">1. Bir ASP.NET Core web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="88a1d-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="88a1d-114">Aşağıdaki adımlar Bu öğreticide kullanılan temel bir ASP.NET Core uygulama oluşturmada size yol.</span><span class="sxs-lookup"><span data-stu-id="88a1d-114">The following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="88a1d-115">2. Docker desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="88a1d-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-the-dockertaskps1-powershell-script"></a><span data-ttu-id="88a1d-116">3. DockerTask.ps1 PowerShell komut dosyası kullan</span><span class="sxs-lookup"><span data-stu-id="88a1d-116">3. Use the DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="88a1d-117">Projenizi kök dizininin bir PowerShell komut istemini açın.</span><span class="sxs-lookup"><span data-stu-id="88a1d-117">Open a PowerShell prompt to the root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="88a1d-118">Uzak doğrulama konak çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="88a1d-118">Validate the remote host is running.</span></span> <span data-ttu-id="88a1d-119">Durumunu görmelisiniz çalışan =</span><span class="sxs-lookup"><span data-stu-id="88a1d-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="88a1d-120">Uygulamasını kullanarak yapı yapı parametresi</span><span class="sxs-lookup"><span data-stu-id="88a1d-120">Build the app using the -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="88a1d-121">Uygulama Çalıştırma kullanarak Çalıştır parametresi</span><span class="sxs-lookup"><span data-stu-id="88a1d-121">Run the app, using the -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="88a1d-122">Docker işlemi tamamlandıktan sonra aşağıdakine benzer sonuçlar görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="88a1d-122">Once docker completes, you should see results similar to the following:</span></span>
   
   ![Uygulamanızı görüntülemek][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
