---
title: "PHP için Azure SDK'sını indirme"
description: "Azure SDK'sı için PHP yükleyip öğrenin."
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
ms.openlocfilehash: fd3d28b133ef8e646f5c2f1c1127f654daa61b95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="d9cb9-103">PHP için Azure SDK'sını indirme</span><span class="sxs-lookup"><span data-stu-id="d9cb9-103">Download the Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="d9cb9-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d9cb9-104">Overview</span></span>
<span data-ttu-id="d9cb9-105">PHP için Azure SDK'sı, geliştirme, dağıtma ve PHP uygulamaları için Azure yönetmenize olanak sağlayan bileşenleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-105">The Azure SDK for PHP includes components that allow you to develop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="d9cb9-106">Özellikle, PHP için Azure SDK aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="d9cb9-106">Specifically, the Azure SDK for PHP includes the following:</span></span>

* <span data-ttu-id="d9cb9-107">**Azure için PHP istemci kitaplıkları**.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-107">**The PHP client libraries for Azure**.</span></span> <span data-ttu-id="d9cb9-108">Bu sınıf kitaplıkları Veri Yönetimi Hizmetleri gibi Azure özelliklere erişmek için bir arabirim sağlar ve bulut Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="d9cb9-109">**Mac, Linux ve Windows (Azure CLI) için Azure komut satırı arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-109">**The Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="d9cb9-110">Bu, dağıtmak ve Azure Web siteleri ve Azure sanal makineler gibi Azure hizmetleri yönetmek için komutlar kümesidir.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="d9cb9-111">Mac, Linux ve Windows dahil olmak üzere herhangi bir platform üzerinde Azure CLI çalışma.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-111">The Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="d9cb9-112">**Azure PowerShell (yalnızca Windows)**.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="d9cb9-113">Bu, dağıtmak ve bulut Hizmetleri ve sanal makineler gibi Azure hizmetleri yönetmek için PowerShell cmdlet'leri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="d9cb9-114">**(Yalnızca Windows) Azure öykünücüsünü**.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-114">**The Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="d9cb9-115">İşlem ve depolama öykünücüsünü bulut Hizmetleri ve bir uygulamayı yerel olarak test etmenize izin veri yönetimi hizmetleri yerel Öykünücüler ' dir.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-115">The compute and storage emulators are local emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="d9cb9-116">Azure öykünücüsünü yalnızca Windows üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-116">The Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="d9cb9-117">Aşağıdaki bölümler, yukarıda açıklanan bileşenlerini yükleyip açıklar.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-117">The sections below describe how to download and install the components described above.</span></span>

<span data-ttu-id="d9cb9-118">Bu konudaki yönergeler sahip olduğunuzu varsaymaktadır [PHP] [ install-php] yüklü.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-118">The instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="d9cb9-119">Azure için PHP istemci kitaplıkları kullanmak için PHP 5.5 ya da daha yüksek olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-119">You must have PHP 5.5 or higher to use the PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="d9cb9-120">Azure için PHP istemci kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="d9cb9-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="d9cb9-121">Azure için PHP istemci kitaplıkları, Veri Yönetimi Hizmetleri gibi Azure özelliklere erişmek için bir arabirim sağlar ve bulut hizmetlerinden herhangi bir işletim sistemi.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-121">The PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="d9cb9-122">Bu kitaplıklar Oluşturucusu yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-122">These libraries can be installed via the Composer.</span></span>

<span data-ttu-id="d9cb9-123">Azure için PHP istemci kitaplıkları kullanma hakkında daha fazla bilgi için bkz: [Blob hizmeti kullanmak nasıl][blob-service], [tablo hizmetini kullanmayı] [ table-service]ve [kuyruk hizmetini kullanmayı][queue-service].</span><span class="sxs-lookup"><span data-stu-id="d9cb9-123">For information about how to use the PHP Client Libraries for Azure, see [How to Use the Blob Service][blob-service], [How to Use the Table Service][table-service] and [How to Use the Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="d9cb9-124">Oluşturucu yükleyin</span><span class="sxs-lookup"><span data-stu-id="d9cb9-124">Install via Composer</span></span>
1. <span data-ttu-id="d9cb9-125">[Git'i yükleyin][install-git].</span><span class="sxs-lookup"><span data-stu-id="d9cb9-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="d9cb9-126">Windows, PATH ortam değişkenine yürütülebilir Git eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-126">On Windows, you will also need to add the Git executable to your PATH environment variable.</span></span>

1. <span data-ttu-id="d9cb9-127">Adlı bir dosya oluşturun **composer.json** projenizi kök ve aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d9cb9-127">Create a file named **composer.json** in the root of your project and add the following code to it:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="d9cb9-128">Karşıdan  **[composer.phar] [ composer-phar]**  proje kök.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="d9cb9-129">Bir komut istemi açın ve bu proje kök dizininde yürütme</span><span class="sxs-lookup"><span data-stu-id="d9cb9-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="d9cb9-130">Azure PowerShell ve Azure öykünücüsünü</span><span class="sxs-lookup"><span data-stu-id="d9cb9-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="d9cb9-131">Azure PowerShell, dağıtma ve Azure Hizmetleri (örneğin, bulut Hizmetleri ve sanal makineler) yönetmek için PowerShell cmdlet'leri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="d9cb9-132">Azure öykünücüsünü Öykünücüler bulut Hizmetleri ve bir uygulamayı yerel olarak test etmenize izin Veri Yönetimi Hizmetleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-132">The Azure Emulators are emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="d9cb9-133">Bu bileşenlerin desteklenen yalnızca Windows.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-133">These components are supported Windows only.</span></span>

<span data-ttu-id="d9cb9-134">Azure PowerShell ve Azure öykünücüsünü yüklemek için önerilen yöntem kullanmaktır [Microsoft Web Platformu yükleyicisi][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="d9cb9-134">The recommended way to install Azure PowerShell and the Azure Emulators is to use the [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="d9cb9-135">Ayrıca, PHP, SQL Server, PHP ve WebMatrix için SQL Server için Microsoft Drivers gibi diğer geliştirme bileşenleri yüklemek seçebileceğiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-135">Note that you can also choose to install other development components, such as PHP, SQL Server, the Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="d9cb9-136">Azure PowerShell'in nasıl kullanılacağı hakkında daha fazla bilgi için bkz: [Azure PowerShell kullanmak için nasıl][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="d9cb9-136">For information about how to use Azure PowerShell, see [How to Use Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="d9cb9-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d9cb9-137">Azure CLI</span></span>
<span data-ttu-id="d9cb9-138">Azure CLI, dağıtma ve Azure Web siteleri ve Azure sanal makineler gibi Azure hizmetleri yönetmek için komutlar kümesidir.</span><span class="sxs-lookup"><span data-stu-id="d9cb9-138">The Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="d9cb9-139">Azure CLI yükleme hakkında daha fazla bilgi için bkz: [Azure CLI yükleme](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d9cb9-139">For information about installing Azure CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9cb9-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d9cb9-140">Next steps</span></span>
<span data-ttu-id="d9cb9-141">Daha fazla bilgi için bkz: [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="d9cb9-141">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

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
