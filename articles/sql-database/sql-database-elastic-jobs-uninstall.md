---
title: "aaaHow toouninstall esnek veritabanı işleri aracı"
description: "Nasıl toouninstall hello esnek veritabanı işleri aracı"
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
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="6973c-103">Esnek veritabanı işleri bileşenlerini Kaldır</span><span class="sxs-lookup"><span data-stu-id="6973c-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="6973c-104">**Esnek veritabanı iş** bileşenleri hello Portal veya PowerShell kullanarak kaldırılması.</span><span class="sxs-lookup"><span data-stu-id="6973c-104">**Elastic Database jobs** components can be uninstalled using either hello Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a><span data-ttu-id="6973c-105">Esnek veritabanı işleri bileşenlerini Hello Azure portal kullanarak Kaldır</span><span class="sxs-lookup"><span data-stu-id="6973c-105">Uninstall Elastic Database jobs components using hello Azure portal</span></span>
1. <span data-ttu-id="6973c-106">Açık hello [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6973c-106">Open hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6973c-107">İçeren toohello abonelik gidin **esnek veritabanı işleri** bileşenleri, yani hello abonelik hangi esnek veritabanı işleri bileşeni yüklenmedi.</span><span class="sxs-lookup"><span data-stu-id="6973c-107">Navigate toohello subscription that contains **Elastic Database jobs** components, namely hello subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="6973c-108">Tıklatın **Gözat** tıklatıp **kaynak grupları**.</span><span class="sxs-lookup"><span data-stu-id="6973c-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="6973c-109">"__ElasticDatabaseJob" adlı select hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="6973c-109">Select hello resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="6973c-110">Merhaba kaynak grubunu silin.</span><span class="sxs-lookup"><span data-stu-id="6973c-110">Delete hello resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="6973c-111">PowerShell kullanarak esnek veritabanı işleri bileşenlerini Kaldır</span><span class="sxs-lookup"><span data-stu-id="6973c-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="6973c-112">Microsoft Azure PowerShell komut penceresini başlatın ve hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x klasörü altında toohello Araçlar alt dizinine gidin: türü **cd Araçları**.</span><span class="sxs-lookup"><span data-stu-id="6973c-112">Launch a Microsoft Azure PowerShell command window and navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="6973c-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > cd araçları</span><span class="sxs-lookup"><span data-stu-id="6973c-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="6973c-114">Merhaba.\UninstallElasticDatabaseJobs.ps1 PowerShell betiğini yürütün.</span><span class="sxs-lookup"><span data-stu-id="6973c-114">Execute hello .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="6973c-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > engellemesini dosya.\UninstallElasticDatabaseJobs.ps1 PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="6973c-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="6973c-116">Veya yalnızca, aşağıdaki komut, varsayılanı kabul hello yürütme hello bileşenleri yüklemesinde kullanılan burada değerler:</span><span class="sxs-lookup"><span data-stu-id="6973c-116">Or simply, execute hello following script, assuming default values where used on installation of hello components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="6973c-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6973c-117">Next steps</span></span>
<span data-ttu-id="6973c-118">toore yükleme esnek veritabanı işleri görmek [hello esnek veritabanı iş hizmetini yükleme](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="6973c-118">toore-install Elastic Database jobs, see [Installing hello Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="6973c-119">Esnek veritabanı işleri genel bakış için bkz: [esnek veritabanı işleri genel bakış](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6973c-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


