---
title: "PowerShell toocreate hello Market için bir VM yukarı aaaSet | Microsoft Docs"
description: "Azure PowerShell ayarlama ve isteğe bağlı bir işlem olarak kullanmak için yönergeler toocreate VM görüntüleri toodeploy için akış ve üzerinde satmak, Azure Marketi hello"
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
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a><span data-ttu-id="342e4-103">Azure PowerShell toocreate hello Azure Marketi teklifi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="342e4-103">Set up Azure PowerShell toocreate an offer for hello Azure Marketplace</span></span>
<span data-ttu-id="342e4-104">Hakkında ayrıntılı bilgi için Azure PowerShell'de yukarı tooset bkz [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="342e4-104">For detailed information on how tooset up PowerShell in Azure, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="342e4-105">Basit bir yaklaşım indirir ve kimlik doğrulaması için gerekli olan bir sertifika alır toouse hello sertifika yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="342e4-105">A simple approach is toouse hello certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="342e4-106">tooobtain hello, sertifika hello kullan **Get-AzurePublishSettingsFile** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="342e4-106">tooobtain hello needed certificate, use hello **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="342e4-107">İstendiğinde hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="342e4-107">Save hello file when you're prompted.</span></span> <span data-ttu-id="342e4-108">bir PowerShell oturumuna kullanım hello tooimport hello sertifika **Import-AzurePublishSettingsFile** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="342e4-108">tooimport hello certificate into a PowerShell session, use hello **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="342e4-109">tooconfigure ve deposu hello genel Microsoft Azure abonelik ayarlarını hello PowerShell oturumunda, kullanmak hello **Set-AzureSubscription** ve **Select-AzureSubscription** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="342e4-109">tooconfigure and store hello common Microsoft Azure subscription settings for hello PowerShell session, use hello **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="342e4-110">Merhaba ilk komut varsayılan depolama hesabı (bazı VM sağlama işlemleri için gereklidir) hello aboneliğiyle ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="342e4-110">hello first command associates a default storage account with hello subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="342e4-111">Merhaba, ikinci (diğer cmdlet'leri tarafından tanınan) geçerli bir hello hello abonelik yapar.</span><span class="sxs-lookup"><span data-stu-id="342e4-111">hello second makes hello subscription hello current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="342e4-112">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="342e4-112">See also</span></span>
* [<span data-ttu-id="342e4-113">Başlarken: nasıl toopublish bir teklif toohello Azure Market</span><span class="sxs-lookup"><span data-stu-id="342e4-113">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="342e4-114">Merhaba Market için bir sanal makine görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="342e4-114">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

