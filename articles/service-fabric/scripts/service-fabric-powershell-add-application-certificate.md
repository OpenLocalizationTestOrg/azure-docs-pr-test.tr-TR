---
title: "PowerShell komut dosyası örneği - aaaAzure uygulama cert tooa küme ekleme | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir uygulama sertifika tooa Service Fabric kümesi ekleyin."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a><span data-ttu-id="3977c-103">Bir uygulama sertifika tooa Service Fabric kümesi Ekle</span><span class="sxs-lookup"><span data-stu-id="3977c-103">Add an application certificate tooa Service Fabric cluster</span></span>

<span data-ttu-id="3977c-104">Bu örnek betik hello belirtilen Azure anahtar kasası içinde otomatik olarak imzalanan bir sertifika oluşturur ve hello Service Fabric kümesi tooall düğümlerinin yükler.</span><span class="sxs-lookup"><span data-stu-id="3977c-104">This sample script creates a self-signed certificate in hello specified Azure key vault and installs it tooall nodes of hello Service Fabric cluster.</span></span> <span data-ttu-id="3977c-105">Merhaba sertifika ayrıca tooa yerel klasöre indirir.</span><span class="sxs-lookup"><span data-stu-id="3977c-105">hello certificate also downloads tooa local folder.</span></span> <span data-ttu-id="3977c-106">indirilen hello sertifikanın Hello adı olduğu hello hello sertifikanın hello anahtar kasasında hello adı ile aynı.</span><span class="sxs-lookup"><span data-stu-id="3977c-106">hello name of hello downloaded certificate is hello same as hello name of hello certificate in hello key vault.</span></span> <span data-ttu-id="3977c-107">Merhaba parametrelerini gerektiği gibi özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3977c-107">Customize hello parameters as needed.</span></span>

<span data-ttu-id="3977c-108">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview) ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="3977c-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3977c-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="3977c-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a><span data-ttu-id="3977c-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="3977c-110">Script explanation</span></span>

<span data-ttu-id="3977c-111">Bu komut dosyası komutları aşağıdaki hello kullanır: hello tablosundaki her komut toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="3977c-111">This script uses hello following commands: Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3977c-112">Komut</span><span class="sxs-lookup"><span data-stu-id="3977c-112">Command</span></span> | <span data-ttu-id="3977c-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="3977c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3977c-114">Ekleme AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="3977c-114">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="3977c-115">Merhaba küme oluşturan bir yeni uygulama sertifika toohello sanal makine ölçek kümesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3977c-115">Add a new application certificate toohello virtual machine scale set that make up hello cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="3977c-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3977c-116">Next steps</span></span>

<span data-ttu-id="3977c-117">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3977c-117">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3977c-118">Azure Service Fabric ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3977c-118">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
