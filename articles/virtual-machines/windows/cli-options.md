---
title: Windows Azure CLI aaaUsing hello | Microsoft Docs
description: Windows Hello Azure CLI kullanma
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a><span data-ttu-id="b93d0-103">Windows Hello Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="b93d0-103">Using hello Azure CLI on Windows</span></span>

<span data-ttu-id="b93d0-104">Hello Azure komut satırı arabirimi (CLI), bir komut satırı ve oluşturmak ve Azure kaynaklarınızı yönetmek için komut dosyası ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b93d0-104">hello Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="b93d0-105">Hello Azure CLI macOS, Linux ve Windows işletim sistemleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b93d0-105">hello Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="b93d0-106">İşletim sistemi belirli sözdiziminin farklı olabilir ancak bu işletim sistemleri arasında hello CLI komutları, aynıdır.</span><span class="sxs-lookup"><span data-stu-id="b93d0-106">Across these operating systems, hello CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="b93d0-107">Azure CLI hello bu belge ayrıntıları hello yolları yüklü ve Windows ve ayrıntıları söz dizimi konuları her çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b93d0-107">This document details hello ways that hello Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="b93d0-108">Ayrıntılı Azure CLI belgelere bakın, [Azure CLI belgelerine]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b93d0-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="b93d0-109">Linux için Windows alt sistem</span><span class="sxs-lookup"><span data-stu-id="b93d0-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="b93d0-110">Merhaba Windows alt sistemi için Linux (WSL), Windows 10 Anniversary ve sonraki sürümleri bir Ubuntu Linux ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="b93d0-110">hello Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="b93d0-111">Etkinleştirildiğinde, WSL oluşturmak ve Azure CLI komut dosyaları çalıştırmak için kullanılan bir yerel Bash deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b93d0-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="b93d0-112">WSL yerel bir Bash deneyimi sağladığından, Azure CLI betikleri macOS, Linux ve Windows arasında değişiklik yapmadan paylaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="b93d0-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="b93d0-113">toouse hello WSL, Azure CLI hello aşağıdaki tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="b93d0-113">toouse hello Azure CLI in WSL, complete hello following.</span></span>

|<span data-ttu-id="b93d0-114">Görev</span><span class="sxs-lookup"><span data-stu-id="b93d0-114">Task</span></span> | <span data-ttu-id="b93d0-115">Yönergeleri</span><span class="sxs-lookup"><span data-stu-id="b93d0-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="b93d0-116">WSL etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b93d0-116">Enable WSL</span></span> | [<span data-ttu-id="b93d0-117">WSL belge yükleme</span><span class="sxs-lookup"><span data-stu-id="b93d0-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="b93d0-118">Hello Azure CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="b93d0-118">Install hello Azure CLI</span></span> |[<span data-ttu-id="b93d0-119">Merhaba CLI WSL/Ubuntu 14.04 yükleyin</span><span class="sxs-lookup"><span data-stu-id="b93d0-119">Install hello CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="b93d0-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b93d0-120">PowerShell</span></span>

<span data-ttu-id="b93d0-121">Windows Hello Azure CLI yerel olarak çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b93d0-121">hello Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="b93d0-122">Bu yapılandırmada, hello Azure CLI paketinin hello Windows işletim sisteminde yüklü olduğu ve Powershell'den komutları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b93d0-122">In this configuration, hello Azure CLI package is installed on hello Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="b93d0-123">Platform özel komut dosyası sözdizimi gerekli değildir ancak bu yapılandırmada, Azure CLI komutları ve komut dosyaları Windows, desteklenen tüm sürümlerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b93d0-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="b93d0-124">Bu nedenle, komut dosyaları mutlaka macOS, Linux ve Windows arasında değişiklik yapmadan paylaşılamaz.</span><span class="sxs-lookup"><span data-stu-id="b93d0-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="b93d0-125">toouse hello Windows, Azure CLI yükleme bu yönergeleri kullanarak hello paketini [yükleme hello Windows CLI](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="b93d0-125">toouse hello Azure CLI on Windows, install hello package using these instructions, [Install hello CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="b93d0-126">Docker görüntüsü</span><span class="sxs-lookup"><span data-stu-id="b93d0-126">Docker Image</span></span>

<span data-ttu-id="b93d0-127">Windows için Docker kullanırken, Docker görüntü hello Azure CLI içeren başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="b93d0-127">When using Docker for Windows, a Docker image can be started that includes hello Azure CLI.</span></span> <span data-ttu-id="b93d0-128">Bu görüntü dışına Linux tabanlı ve yerel bir Bash deneyimi içerir.</span><span class="sxs-lookup"><span data-stu-id="b93d0-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="b93d0-129">Kullanırken Windows için Docker ve hello Azure CLI görüntü, komut dosyaları toobe macOS, Linux ve Windows arasında paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="b93d0-129">When using Docker for Windows and hello Azure CLI image, scripts toobe shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="b93d0-130">toouse hello Docker için Windows Azure CLI için Docker Windows çalıştıran ve hello aşağıdaki komutu çalıştırın emin olun.</span><span class="sxs-lookup"><span data-stu-id="b93d0-130">toouse hello Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run hello following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="b93d0-131">Tamamlandığında, oturumu diğer bir deyişle başlatmak Bash hello Azure CLI araçlarını ile önceden yüklü.</span><span class="sxs-lookup"><span data-stu-id="b93d0-131">Once completed, a Bash session will start that is preloaded with hello Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b93d0-132">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b93d0-132">Next Steps</span></span>

[<span data-ttu-id="b93d0-133">Azure sanal makineleri için CLI örnek</span><span class="sxs-lookup"><span data-stu-id="b93d0-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="b93d0-134">Azure Web uygulamaları için CLI örnekleri</span><span class="sxs-lookup"><span data-stu-id="b93d0-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="b93d0-135">Azure SQL CLI örnekleri</span><span class="sxs-lookup"><span data-stu-id="b93d0-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
