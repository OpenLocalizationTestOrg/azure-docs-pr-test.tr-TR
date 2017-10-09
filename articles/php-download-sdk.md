---
title: "aaaDownload hello PHP için Azure SDK'sı"
description: "Nasıl toodownload ve yükleme PHP için Azure SDK'sı hello öğrenin."
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="a3506-103">PHP için Hello Azure SDK'sını indirme</span><span class="sxs-lookup"><span data-stu-id="a3506-103">Download hello Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="a3506-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a3506-104">Overview</span></span>
<span data-ttu-id="a3506-105">Merhaba PHP için Azure SDK toodevelop izin, dağıtmak ve PHP uygulamaları için Azure yöneten bileşenleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a3506-105">hello Azure SDK for PHP includes components that allow you toodevelop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="a3506-106">Özellikle, hello PHP için Azure SDK hello aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="a3506-106">Specifically, hello Azure SDK for PHP includes hello following:</span></span>

* <span data-ttu-id="a3506-107">**Azure için PHP istemci kitaplıkları hello**.</span><span class="sxs-lookup"><span data-stu-id="a3506-107">**hello PHP client libraries for Azure**.</span></span> <span data-ttu-id="a3506-108">Bu sınıf kitaplıkları Veri Yönetimi Hizmetleri gibi Azure özelliklere erişmek için bir arabirim sağlar ve bulut Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="a3506-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="a3506-109">**Merhaba Mac, Linux ve Windows (Azure CLI) için Azure komut satırı arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="a3506-109">**hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="a3506-110">Bu, dağıtmak ve Azure Web siteleri ve Azure sanal makineler gibi Azure hizmetleri yönetmek için komutlar kümesidir.</span><span class="sxs-lookup"><span data-stu-id="a3506-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="a3506-111">Merhaba Mac, Linux ve Windows dahil olmak üzere herhangi bir platform üzerinde Azure CLI çalışma.</span><span class="sxs-lookup"><span data-stu-id="a3506-111">hello Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="a3506-112">**Azure PowerShell (yalnızca Windows)**.</span><span class="sxs-lookup"><span data-stu-id="a3506-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="a3506-113">Bu, dağıtmak ve bulut Hizmetleri ve sanal makineler gibi Azure hizmetleri yönetmek için PowerShell cmdlet'leri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="a3506-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="a3506-114">**Merhaba (yalnızca Windows) Azure öykünücüsünü**.</span><span class="sxs-lookup"><span data-stu-id="a3506-114">**hello Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="a3506-115">Merhaba işlem ve depolama öykünücüsünü bulut Hizmetleri ve tootest uygulama yerel olarak izin veri yönetimi hizmetleri yerel Öykünücüler ' dir.</span><span class="sxs-lookup"><span data-stu-id="a3506-115">hello compute and storage emulators are local emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="a3506-116">Hello Azure öykünücüsünü yalnızca Windows üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a3506-116">hello Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="a3506-117">Aşağıdaki Hello bölümler, yukarıda açıklanan bileşenleri toodownload ve yükleme nasıl hello anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a3506-117">hello sections below describe how toodownload and install hello components described above.</span></span>

<span data-ttu-id="a3506-118">Merhaba bu konudaki yönergeler sahip olduğunuz varsayılmıştır [PHP] [ install-php] yüklü.</span><span class="sxs-lookup"><span data-stu-id="a3506-118">hello instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="a3506-119">Azure için PHP 5.5 veya daha yüksek toouse hello PHP istemci kitaplıkları olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a3506-119">You must have PHP 5.5 or higher toouse hello PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="a3506-120">Azure için PHP istemci kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="a3506-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="a3506-121">Azure için Hello PHP istemci kitaplıkları, Veri Yönetimi Hizmetleri gibi Azure özelliklere erişmek için bir arabirim sağlar ve bulut hizmetlerinden herhangi bir işletim sistemi.</span><span class="sxs-lookup"><span data-stu-id="a3506-121">hello PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="a3506-122">Bu kitaplıklar Oluşturucu hello yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a3506-122">These libraries can be installed via hello Composer.</span></span>

<span data-ttu-id="a3506-123">Nasıl toouse hello Azure için PHP istemci kitaplıkları hakkında daha fazla bilgi için bkz: [nasıl tooUse hello Blob hizmeti][blob-service], [nasıl tooUse hello tablo hizmeti] [ table-service] ve [nasıl tooUse hello sıra hizmeti][queue-service].</span><span class="sxs-lookup"><span data-stu-id="a3506-123">For information about how toouse hello PHP Client Libraries for Azure, see [How tooUse hello Blob Service][blob-service], [How tooUse hello Table Service][table-service] and [How tooUse hello Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="a3506-124">Oluşturucu yükleyin</span><span class="sxs-lookup"><span data-stu-id="a3506-124">Install via Composer</span></span>
1. <span data-ttu-id="a3506-125">[Git'i yükleyin][install-git].</span><span class="sxs-lookup"><span data-stu-id="a3506-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="a3506-126">Windows üzerinde tooadd hello Git yürütülebilir tooyour PATH ortam değişkeni de gerekir.</span><span class="sxs-lookup"><span data-stu-id="a3506-126">On Windows, you will also need tooadd hello Git executable tooyour PATH environment variable.</span></span>

1. <span data-ttu-id="a3506-127">Adlı bir dosya oluşturun **composer.json** hello projenizin kök ve kod tooit aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a3506-127">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="a3506-128">Karşıdan  **[composer.phar] [ composer-phar]**  proje kök.</span><span class="sxs-lookup"><span data-stu-id="a3506-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="a3506-129">Bir komut istemi açın ve bu proje kök dizininde yürütme</span><span class="sxs-lookup"><span data-stu-id="a3506-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="a3506-130">Azure PowerShell ve Azure öykünücüsünü</span><span class="sxs-lookup"><span data-stu-id="a3506-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="a3506-131">Azure PowerShell, dağıtma ve Azure Hizmetleri (örneğin, bulut Hizmetleri ve sanal makineler) yönetmek için PowerShell cmdlet'leri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="a3506-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="a3506-132">Hello Azure öykünücüsünü Öykünücüler bulut Hizmetleri ve tootest uygulama yerel olarak izin Veri Yönetimi Hizmetleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="a3506-132">hello Azure Emulators are emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="a3506-133">Bu bileşenlerin desteklenen yalnızca Windows.</span><span class="sxs-lookup"><span data-stu-id="a3506-133">These components are supported Windows only.</span></span>

<span data-ttu-id="a3506-134">önerilen yöntem tooinstall Azure PowerShell hello ve hello Azure öykünücüsünü ise toouse hello [Microsoft Web Platformu yükleyicisi][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="a3506-134">hello recommended way tooinstall Azure PowerShell and hello Azure Emulators is toouse hello [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="a3506-135">PHP, SQL Server, SQL Server için PHP ve WebMatrix için hello Microsoft Drivers gibi diğer geliştirme bileşenleri tooinstall de seçebilirsiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a3506-135">Note that you can also choose tooinstall other development components, such as PHP, SQL Server, hello Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="a3506-136">Hakkında bilgi için bkz toouse Azure PowerShell [nasıl tooUse Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="a3506-136">For information about how toouse Azure PowerShell, see [How tooUse Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="a3506-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a3506-137">Azure CLI</span></span>
<span data-ttu-id="a3506-138">Hello Azure CLI, dağıtma ve Azure Web siteleri ve Azure sanal makineler gibi Azure hizmetleri yönetmek için komutlar kümesidir.</span><span class="sxs-lookup"><span data-stu-id="a3506-138">hello Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="a3506-139">Azure CLI yükleme hakkında daha fazla bilgi için bkz: [yükleme hello Azure CLI](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a3506-139">For information about installing Azure CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3506-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a3506-140">Next steps</span></span>
<span data-ttu-id="a3506-141">Daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="a3506-141">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
