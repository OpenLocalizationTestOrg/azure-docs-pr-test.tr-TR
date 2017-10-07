---
title: "aaaAzure PowerShell komut dosyası örneği - web uygulama tooa SQL veritabanına bağlanma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - web uygulama tooa SQL veritabanına bağlan"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 055440a9-fff1-49b2-b964-9c95b364e533
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8f80b940378d020cbcaec2c1bbc28bae1a3ef35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="1ef5e-103">Web uygulaması tooa SQL veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="1ef5e-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="1ef5e-104">Bu senaryoda, nasıl toocreate bir Azure SQL veritabanı ve bir Azure web uygulaması öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="1ef5e-105">Uygulama ayarları kullanarak hello SQL veritabanı toohello web uygulaması bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-105">Then you will link hello SQL database toohello web app using app settings.</span></span>

<span data-ttu-id="1ef5e-106">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="1ef5e-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="1ef5e-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app tooa SQL database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1ef5e-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="1ef5e-108">Clean up deployment</span></span> 

<span data-ttu-id="1ef5e-109">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="1ef5e-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="1ef5e-110">Script explanation</span></span>

<span data-ttu-id="1ef5e-111">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-111">This script uses hello following commands.</span></span> <span data-ttu-id="1ef5e-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1ef5e-113">Komut</span><span class="sxs-lookup"><span data-stu-id="1ef5e-113">Command</span></span> | <span data-ttu-id="1ef5e-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="1ef5e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1ef5e-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1ef5e-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1ef5e-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1ef5e-117">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="1ef5e-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="1ef5e-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="1ef5e-119">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="1ef5e-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="1ef5e-120">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-120">Creates a web app.</span></span> |
| [<span data-ttu-id="1ef5e-121">AzureRMSQLServer yeni</span><span class="sxs-lookup"><span data-stu-id="1ef5e-121">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="1ef5e-122">Bir SQL veritabanı sunucusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-122">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="1ef5e-123">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="1ef5e-123">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="1ef5e-124">Bir SQL veritabanı sunucusu için bir güvenlik duvarı kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-124">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="1ef5e-125">AzureRMSQLDatabase yeni</span><span class="sxs-lookup"><span data-stu-id="1ef5e-125">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="1ef5e-126">Bir veritabanı veya esnek bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-126">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="1ef5e-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="1ef5e-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="1ef5e-128">Web uygulamanızın yapılandırmasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1ef5e-128">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1ef5e-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ef5e-129">Next steps</span></span>

<span data-ttu-id="1ef5e-130">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1ef5e-130">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1ef5e-131">Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1ef5e-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
