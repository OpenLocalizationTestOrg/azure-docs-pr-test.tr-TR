---
title: Windows Azure CLI kullanarak | Microsoft Docs
description: Windows Azure CLI kullanma
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
ms.openlocfilehash: be02ad0d7752cb08f092deeb5a86dcd126403237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-on-windows"></a><span data-ttu-id="bc932-103">Windows Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="bc932-103">Using the Azure CLI on Windows</span></span>

<span data-ttu-id="bc932-104">Azure komut satırı arabirimi (CLI), bir komut satırı ve oluşturmak ve Azure kaynaklarınızı yönetmek için komut dosyası ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc932-104">The Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="bc932-105">Azure CLI macOS, Linux ve Windows işletim sistemleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bc932-105">The Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="bc932-106">İşletim sistemi belirli sözdiziminin farklı olabilir ancak bu işletim sistemleri arasında CLI komutları, aynıdır.</span><span class="sxs-lookup"><span data-stu-id="bc932-106">Across these operating systems, the CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="bc932-107">Bu belgede Azure CLI yüklenebilir ve Windows ve ayrıntıları söz dizimi konuları her çalıştırın, yolları ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="bc932-107">This document details the ways that the Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="bc932-108">Ayrıntılı Azure CLI belgelere bakın, [Azure CLI belgelerine]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bc932-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="bc932-109">Linux için Windows alt sistem</span><span class="sxs-lookup"><span data-stu-id="bc932-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="bc932-110">Windows alt sistemi için Linux (WSL), Windows 10 Anniversary ve sonraki sürümleri bir Ubuntu Linux ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc932-110">The Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="bc932-111">Etkinleştirildiğinde, WSL oluşturmak ve Azure CLI komut dosyaları çalıştırmak için kullanılan bir yerel Bash deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc932-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="bc932-112">WSL yerel bir Bash deneyimi sağladığından, Azure CLI betikleri macOS, Linux ve Windows arasında değişiklik yapmadan paylaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="bc932-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="bc932-113">Azure CLI WSL içinde kullanmak için aşağıdaki adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="bc932-113">To use the Azure CLI in WSL, complete the following.</span></span>

|<span data-ttu-id="bc932-114">Görev</span><span class="sxs-lookup"><span data-stu-id="bc932-114">Task</span></span> | <span data-ttu-id="bc932-115">Yönergeleri</span><span class="sxs-lookup"><span data-stu-id="bc932-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="bc932-116">WSL etkinleştir</span><span class="sxs-lookup"><span data-stu-id="bc932-116">Enable WSL</span></span> | [<span data-ttu-id="bc932-117">WSL belge yükleme</span><span class="sxs-lookup"><span data-stu-id="bc932-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="bc932-118">Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="bc932-118">Install the Azure CLI</span></span> |[<span data-ttu-id="bc932-119">WSL/Ubuntu 14.04 üzerinde CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="bc932-119">Install the CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="bc932-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc932-120">PowerShell</span></span>

<span data-ttu-id="bc932-121">Windows Azure CLI yerel olarak çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="bc932-121">The Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="bc932-122">Bu yapılandırmada, Azure CLI paketi Windows işletim sisteminde yüklü ve Powershell'den komutları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc932-122">In this configuration, the Azure CLI package is installed on the Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="bc932-123">Platform özel komut dosyası sözdizimi gerekli değildir ancak bu yapılandırmada, Azure CLI komutları ve komut dosyaları Windows, desteklenen tüm sürümlerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="bc932-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="bc932-124">Bu nedenle, komut dosyaları mutlaka macOS, Linux ve Windows arasında değişiklik yapmadan paylaşılamaz.</span><span class="sxs-lookup"><span data-stu-id="bc932-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="bc932-125">Windows Azure CLI kullanmak için bu yönergeleri kullanarak paketi yükleyin [Windows CLI'yı yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="bc932-125">To use the Azure CLI on Windows, install the package using these instructions, [Install the CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="bc932-126">Docker görüntüsü</span><span class="sxs-lookup"><span data-stu-id="bc932-126">Docker Image</span></span>

<span data-ttu-id="bc932-127">Windows için Docker kullanırken, Azure CLI içeren bir Docker görüntüsü başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="bc932-127">When using Docker for Windows, a Docker image can be started that includes the Azure CLI.</span></span> <span data-ttu-id="bc932-128">Bu görüntü dışına Linux tabanlı ve yerel bir Bash deneyimi içerir.</span><span class="sxs-lookup"><span data-stu-id="bc932-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="bc932-129">Windows için Docker ve Azure CLI görüntü macOS, Linux ve Windows arasında paylaşılmak üzere komut dosyaları kullanırken.</span><span class="sxs-lookup"><span data-stu-id="bc932-129">When using Docker for Windows and the Azure CLI image, scripts to be shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="bc932-130">Docker Windows için Azure CLI kullanmak için Windows için Docker çalıştığından emin olun ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bc932-130">To use the Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run the following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="bc932-131">Tamamlandığında, oturumu diğer bir deyişle başlatmak Bash ile Azure CLI araçlarını önceden yüklü.</span><span class="sxs-lookup"><span data-stu-id="bc932-131">Once completed, a Bash session will start that is preloaded with the Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc932-132">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="bc932-132">Next Steps</span></span>

[<span data-ttu-id="bc932-133">Azure sanal makineleri için CLI örnek</span><span class="sxs-lookup"><span data-stu-id="bc932-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="bc932-134">Azure Web uygulamaları için CLI örnekleri</span><span class="sxs-lookup"><span data-stu-id="bc932-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="bc932-135">Azure SQL CLI örnekleri</span><span class="sxs-lookup"><span data-stu-id="bc932-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
