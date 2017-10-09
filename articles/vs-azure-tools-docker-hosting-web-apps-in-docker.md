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
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a>Bir ASP.NET kapsayıcı tooa uzak Docker ana dağıtma
## <a name="overview"></a>Genel Bakış
Docker olan bazı yolları tooa sanal hangi yapabilecekleriniz makinede, benzer bir basit kapsayıcı altyapısı toohost uygulamaları ve Hizmetleri kullanın.
Bu öğretici, hello kullanarak kılavuzluk [Docker için Visual Studio Araçları](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) uzantısı toodeploy Azure PowerShell kullanarak bir ASP.NET Core uygulama tooa Docker konağında.

## <a name="prerequisites"></a>Ön koşullar
Merhaba aşağıdaki gerekli toocomplete bu öğreticidir:

* Bir Azure Docker ana VM açıklandığı gibi oluşturmak [nasıl toouse docker-makine Azure ile](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Merhaba en son sürümünü yüklemek [Visual Studio](https://www.visualstudio.com/downloads/)
* Merhaba karşıdan [Microsoft ASP.NET Core 1.0 SDK'sı](https://go.microsoft.com/fwlink/?LinkID=809122)
* Yükleme [Windows için Docker](https://docs.docker.com/docker-for-windows/install/)

## <a name="1-create-an-aspnet-core-web-app"></a>1. Bir ASP.NET Core web uygulaması oluşturma
Merhaba aşağıdaki adımlar, bu öğreticide kullanılan temel bir ASP.NET Core uygulama oluşturmada size yol.

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Docker desteği ekleme
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a>3. Merhaba DockerTask.ps1 PowerShell Betiği kullanın
1. Bir PowerShell komut istemi toohello kök dizin projenizin açın. 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. Doğrulama hello uzak ana bilgisayarda çalışır. Durumunu görmelisiniz çalışan = 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. Yapı hello uygulamasını kullanarak hello - yapı parametresi
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. Merhaba uygulama çalıştırma hello kullanarak - Çalıştır parametresi
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   Docker işlemi tamamlandıktan sonra benzer toohello aşağıdaki sonuçları görmeniz gerekir:
   
   ![Uygulamanızı görüntülemek][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
