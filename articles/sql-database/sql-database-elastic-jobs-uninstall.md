---
title: "Esnek veritabanı işleri Aracı kaldırma"
description: "Esnek veritabanı işleri Aracı kaldırma"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: ae7f0bce452a0a86f6f1e4d9b0c93a0fa1727f21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="23e1f-103">Esnek veritabanı işleri bileşenlerini Kaldır</span><span class="sxs-lookup"><span data-stu-id="23e1f-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="23e1f-104">**Esnek veritabanı iş** bileşenleri Portal veya PowerShell kullanarak kaldırılması.</span><span class="sxs-lookup"><span data-stu-id="23e1f-104">**Elastic Database jobs** components can be uninstalled using either the Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-the-azure-portal"></a><span data-ttu-id="23e1f-105">Azure portalını kullanarak esnek veritabanı işleri bileşenlerini Kaldır</span><span class="sxs-lookup"><span data-stu-id="23e1f-105">Uninstall Elastic Database jobs components using the Azure portal</span></span>
1. <span data-ttu-id="23e1f-106">[Azure portalı](https://portal.azure.com/) açın.</span><span class="sxs-lookup"><span data-stu-id="23e1f-106">Open the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="23e1f-107">İçeren abonelik gidin **esnek veritabanı işleri** bileşenleri, yani hangi esnek veritabanı işleri bileşeni yüklenmedi abonelik.</span><span class="sxs-lookup"><span data-stu-id="23e1f-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="23e1f-108">Tıklatın **Gözat** tıklatıp **kaynak grupları**.</span><span class="sxs-lookup"><span data-stu-id="23e1f-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="23e1f-109">"__ElasticDatabaseJob" adlı kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="23e1f-109">Select the resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="23e1f-110">Kaynak grubunu silin.</span><span class="sxs-lookup"><span data-stu-id="23e1f-110">Delete the resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="23e1f-111">PowerShell kullanarak esnek veritabanı işleri bileşenlerini Kaldır</span><span class="sxs-lookup"><span data-stu-id="23e1f-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="23e1f-112">Microsoft Azure PowerShell komut penceresini başlatın ve Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x klasörü altındaki Araçlar alt dizinine gidin: türü **cd Araçları**.</span><span class="sxs-lookup"><span data-stu-id="23e1f-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="23e1f-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > cd araçları</span><span class="sxs-lookup"><span data-stu-id="23e1f-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="23e1f-114">.\UninstallElasticDatabaseJobs.ps1 PowerShell betiğini yürütün.</span><span class="sxs-lookup"><span data-stu-id="23e1f-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="23e1f-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > engellemesini dosya.\UninstallElasticDatabaseJobs.ps1 PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="23e1f-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="23e1f-116">Veya yalnızca varsayılan varsayılarak aşağıdaki komut dosyası yürütme bileşenleri yüklemesinde kullanılan burada değerler:</span><span class="sxs-lookup"><span data-stu-id="23e1f-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "The Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing the Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing the Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="23e1f-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="23e1f-117">Next steps</span></span>
<span data-ttu-id="23e1f-118">Esnek veritabanı işleri yeniden yüklemek için bkz: [esnek veritabanı iş hizmetini yükleme](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="23e1f-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="23e1f-119">Esnek veritabanı işleri genel bakış için bkz: [esnek veritabanı işleri genel bakış](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="23e1f-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


