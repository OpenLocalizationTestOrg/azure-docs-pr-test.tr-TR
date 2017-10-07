---
title: "Azure otomasyonu kullanarak Azure anahtar kasası aaaManage | Microsoft Docs"
description: "Kullanılan toomanage Azure anahtar Kasası'hello Azure Otomasyon hizmetine nasıl olabilir hakkında bilgi edinin."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="49c4e-103">Azure anahtar Kasası'nın Azure otomasyonu kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="49c4e-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="49c4e-104">Bu kılavuz toohello Azure Otomasyon hizmetine ve anahtarları ve gizli anahtarları Azure anahtar Kasası'nda kullanılan toosimplify yönetimini nasıl çalıştırılabilir tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="49c4e-104">This guide will introduce you toohello Azure Automation service and how it can be used toosimplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="49c4e-105">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="49c4e-105">What is Azure Automation?</span></span>
<span data-ttu-id="49c4e-106">[Azure Otomasyonu](../automation/automation-intro.md) işlem Otomasyonu ve istenen durum yapılandırması aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="49c4e-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="49c4e-107">Azure otomasyonu kullanarak, el ile yinelenen, uzun süre çalışan ve hataya yatkın görevleri otomatik tooincrease güvenilirlik, verimliliği ve kuruluşunuz için zaman toovalue olabilir.</span><span class="sxs-lookup"><span data-stu-id="49c4e-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="49c4e-108">Azure Otomasyon gereksinimlerinizi toomeet ölçeklendirir bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="49c4e-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="49c4e-109">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="49c4e-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="49c4e-110">İşlem yükünü azaltmak ve boş BT ve DevOps personel toofocus iş değeri, bulut yönetim görevleri toobe taşıyarak ekler iş Azure Automation'ın otomatik olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="49c4e-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="49c4e-111">Azure Otomasyonu Azure anahtar kasası yönetmenize nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="49c4e-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="49c4e-112">Anahtar kasası yönetilebilir Azure Otomasyonu'nda hello kullanarak [AzureRM anahtar kasası cmdlet'leri](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) ve [Azure Klasik anahtar kasası cmdlet'leri](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="49c4e-112">Key Vault can be managed in Azure Automation by using hello [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="49c4e-113">otomatik olarak Azure Otomasyonu'nda Klasik anahtar kasası yönetme kullanılabilir için Azure modülü hello ve hello içeri aktarabilirsiniz [AzureRM KeyVault Modülü](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) içine Azure Otomasyonu, böylece anahtar kasası yönetimini çoğunu gerçekleştirebilirsiniz Görevler hello hizmet içinde.</span><span class="sxs-lookup"><span data-stu-id="49c4e-113">hello Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within hello service.</span></span> <span data-ttu-id="49c4e-114">Azure Automation bu cmdlet'leri diğer Azure Hizmetleri, tooautomate karmaşık görevleri için hello cmdlet'leri ile Azure hizmeti ve 3. taraf sistemi arasında eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="49c4e-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="49c4e-115">Hello Azure anahtar kasası cmdlet'leri ile diğerlerinin yanı sıra bu görevleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="49c4e-115">With hello Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="49c4e-116">Oluşturma ve bir anahtar kasası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="49c4e-116">Create and configure a key vault</span></span>
* <span data-ttu-id="49c4e-117">Oluşturun veya bir anahtarı içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="49c4e-117">Create or import a key</span></span>
* <span data-ttu-id="49c4e-118">Bir parolayı güncelle</span><span class="sxs-lookup"><span data-stu-id="49c4e-118">Create or update a secret</span></span>
* <span data-ttu-id="49c4e-119">Bir anahtarı güncelleştirme öznitelikleri</span><span class="sxs-lookup"><span data-stu-id="49c4e-119">Update attributes of a key</span></span>
* <span data-ttu-id="49c4e-120">Bir anahtar veya gizli Al</span><span class="sxs-lookup"><span data-stu-id="49c4e-120">Get a key or secret</span></span>
* <span data-ttu-id="49c4e-121">Bir anahtar veya gizli Sil</span><span class="sxs-lookup"><span data-stu-id="49c4e-121">Delete a key or secret</span></span>

<span data-ttu-id="49c4e-122">PowerShell toomanage anahtar kasası kullanmanın bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="49c4e-122">Here are some examples of using PowerShell toomanage Key Vault:</span></span>  

* [<span data-ttu-id="49c4e-123">Azure anahtar kasası - adım adım</span><span class="sxs-lookup"><span data-stu-id="49c4e-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="49c4e-124">Ayarlama ve Azure anahtar kasası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="49c4e-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="49c4e-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="49c4e-125">Next steps</span></span>
<span data-ttu-id="49c4e-126">Artık Azure Automation ve nasıl kullanılan toomanage Azure anahtar kasası olabilir hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn Azure Otomasyonu hakkında daha fazla izleyin.</span><span class="sxs-lookup"><span data-stu-id="49c4e-126">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Key Vault, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="49c4e-127">Hello Azure Otomasyonu bkz [başlangıç Öğreticisi](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="49c4e-127">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="49c4e-128">Merhaba bkz [Azure anahtar kasası PowerShell komut dosyalarını](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="49c4e-128">See hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

