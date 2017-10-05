---
title: "Market bir VM oluşturmak için PowerShell ayarlama | Microsoft Docs"
description: "Azure PowerShell ayarlama ve isteğe bağlı bir işlem olarak kullanmak için yönergeler dağıtmak için VM görüntüleri oluşturmak için akış ve Azure Market, satış"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: bbcce5093d2bbd5326523063db7d0e565fe4de6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-powershell-to-create-an-offer-for-the-azure-marketplace"></a><span data-ttu-id="43da5-103">Azure Market teklifi oluşturmak için Azure PowerShell ayarlayın</span><span class="sxs-lookup"><span data-stu-id="43da5-103">Set up Azure PowerShell to create an offer for the Azure Marketplace</span></span>
<span data-ttu-id="43da5-104">Azure PowerShell'de ayarlama konusunda ayrıntılı bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="43da5-104">For detailed information on how to set up PowerShell in Azure, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="43da5-105">Basit bir yaklaşım indirir ve kimlik doğrulaması için gerekli olan bir sertifika alır sertifika yöntemini kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="43da5-105">A simple approach is to use the certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="43da5-106">Gerekli sertifikayı almak için kullanın **Get-AzurePublishSettingsFile** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="43da5-106">To obtain the needed certificate, use the **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="43da5-107">İstendiğinde dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="43da5-107">Save the file when you're prompted.</span></span> <span data-ttu-id="43da5-108">Sertifika bir PowerShell oturumuna içeri aktarmak için kullanın **Import-AzurePublishSettingsFile** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="43da5-108">To import the certificate into a PowerShell session, use the **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="43da5-109">Yapılandırma ve PowerShell oturumu için genel Microsoft Azure abonelik ayarlarını depolamak için kullanmak **Set-AzureSubscription** ve **Select-AzureSubscription** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="43da5-109">To configure and store the common Microsoft Azure subscription settings for the PowerShell session, use the **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="43da5-110">İlk komut bir varsayılan depolama hesabı (bazı VM sağlama işlemleri için gereklidir) aboneliğiyle ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="43da5-110">The first command associates a default storage account with the subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="43da5-111">İkinci (diğer cmdlet'leri tarafından tanınan) geçerli bir abonelik yapar.</span><span class="sxs-lookup"><span data-stu-id="43da5-111">The second makes the subscription the current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="43da5-112">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="43da5-112">See also</span></span>
* [<span data-ttu-id="43da5-113">Başlarken: bir teklifi Azure Marketinde yayımlama</span><span class="sxs-lookup"><span data-stu-id="43da5-113">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="43da5-114">Market bir sanal makine görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="43da5-114">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

