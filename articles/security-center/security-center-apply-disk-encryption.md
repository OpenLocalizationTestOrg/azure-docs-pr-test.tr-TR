---
title: "Azure Güvenlik Merkezi'nde disk şifrelemesi uygulamak | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi öneriyi uygulamayı gösterilmiştir ** disk şifreleme ** uygulayın."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 67cff664f3723b2194ecd1519729cca17069d07f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a><span data-ttu-id="042dc-103">Azure Güvenlik Merkezi'nde disk şifrelemesi Uygula</span><span class="sxs-lookup"><span data-stu-id="042dc-103">Apply disk encryption in Azure Security Center</span></span>
<span data-ttu-id="042dc-104">Azure Güvenlik Merkezi, Azure Disk şifrelemesi kullanılarak şifrelenmiş değil Windows veya Linux VM diskiniz varsa, disk şifrelemesi uygulamanızı önerir.</span><span class="sxs-lookup"><span data-stu-id="042dc-104">Azure Security Center recommends that you apply disk encryption if you have Windows or Linux VM disks that are not encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="042dc-105">Disk şifrelemesi, Windows ve Linux Iaas VM diskleri şifrelemek olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="042dc-105">Disk Encryption lets you encrypt your Windows and Linux IaaS VM disks.</span></span>  <span data-ttu-id="042dc-106">Şifreleme hem işletim sistemi hem de VM’nizin üzerindeki veri birimleri için önerilir.</span><span class="sxs-lookup"><span data-stu-id="042dc-106">Encryption is recommended for both the OS and data volumes on your VM.</span></span>

<span data-ttu-id="042dc-107">Disk şifrelemesi kullanılır endüstri standardı [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) Windows özelliğidir ve [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="042dc-107">Disk Encryption uses the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux.</span></span> <span data-ttu-id="042dc-108">Bu özellikleri korumak ve verilerinizi korumak ve Kuruluş güvenliği ve uyumluluğu taahhüt karşılamak için işletim sistemi ve veri şifreleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="042dc-108">These features provide OS and data encryption to help protect and safeguard your data and meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="042dc-109">Disk şifrelemesi ile tümleştirildiğinde [Azure anahtar kasası](https://azure.microsoft.com/documentation/services/key-vault/) denetlemek ve disk şifreleme anahtarları ve gizli anahtar kasası aboneliğinizde yönetmenize yardımcı olmak için while bekleyen VM disklerdeki tüm veriler şifrelenir sağlayarak, [Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="042dc-109">Disk Encryption is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk encryption keys and secrets in your Key Vault subscription, while ensuring that all data in the VM disks are encrypted at rest in your [Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span></span>

> [!NOTE]
> <span data-ttu-id="042dc-110">Azure Disk şifrelemesi aşağıdaki Windows server işletim sistemlerinde - Windows Server 2008 R2, Windows Server 2012 ve Windows Server 2012 R2 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="042dc-110">Azure Disk Encryption is supported on the following Windows server operating systems - Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span> <span data-ttu-id="042dc-111">Disk şifrelemesi aşağıdaki Linux sunucusu işletim sistemlerinde - Ubuntu ve CentOS, SUSE ve SUSE Linux Enterprise Server (SLES) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="042dc-111">Disk encryption is supported on the following Linux server operating systems - Ubuntu, CentOS, SUSE, and SUSE Linux Enterprise Server (SLES).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="042dc-112">Öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="042dc-112">Implement the recommendation</span></span>
1. <span data-ttu-id="042dc-113">İçinde **önerileri** dikey penceresinde, select **disk şifrelemesi uygulamak**.</span><span class="sxs-lookup"><span data-stu-id="042dc-113">In the **Recommendations** blade, select **Apply disk encryption**.</span></span>
2. <span data-ttu-id="042dc-114">İçinde **disk şifrelemesi uygulamak** dikey penceresinde, Disk şifrelemesi önerilir VM'ler listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="042dc-114">In the **Apply disk encryption** blade, you see a list of VMs for which Disk Encryption is recommended.</span></span>
3. <span data-ttu-id="042dc-115">Şifreleme için bu Vm'lere uygulamak için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="042dc-115">Follow the instructions to apply encryption to these VMs.</span></span>

![][1]

<span data-ttu-id="042dc-116">Güvenlik Merkezi tarafından şifreleme gerektiği belirlenen Azure Virtual Machines şifreleme için aşağıdaki adımları öneririz:</span><span class="sxs-lookup"><span data-stu-id="042dc-116">To encrypt Azure Virtual Machines that have been identified by Security Center as needing encryption, we recommend the following steps:</span></span>

* <span data-ttu-id="042dc-117">Azure PowerShell'i yükleyip yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="042dc-117">Install and configure Azure PowerShell.</span></span> <span data-ttu-id="042dc-118">Bu Azure Virtual Machines şifreleme için gereken önkoşulları ayarlama gerekli PowerShell komutlarını çalıştırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="042dc-118">This enables you to run the PowerShell commands required to set up the prerequisites required to encrypt Azure Virtual Machines.</span></span>
* <span data-ttu-id="042dc-119">Edinin ve Azure Disk şifrelemesi önkoşulları Azure PowerShell betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="042dc-119">Obtain and run the Azure Disk Encryption Prerequisites Azure PowerShell script.</span></span>
* <span data-ttu-id="042dc-120">Sanal makinelerinizi şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="042dc-120">Encrypt your virtual machines.</span></span>

<span data-ttu-id="042dc-121">[Bir Azure sanal Makine'yi şifreleme](security-center-disk-encryption.md) Bu adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="042dc-121">[Encrypt an Azure Virtual Machine](security-center-disk-encryption.md) walks you through these steps.</span></span>  <span data-ttu-id="042dc-122">Bu konu, disk şifrelemesi'ni yapılandırma istemci makine gibi Windows 10 kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="042dc-122">This topic assumes you are using Windows 10 as the client machine from which you configure disk encryption.</span></span>

<span data-ttu-id="042dc-123">Azure sanal makineler için kullanılabilir birçok yaklaşım vardır.</span><span class="sxs-lookup"><span data-stu-id="042dc-123">There are many approaches that can be used for Azure Virtual Machines.</span></span> <span data-ttu-id="042dc-124">Azure PowerShell veya Azure CLI konusunda zaten bilgiliyseniz alternatif yaklaşımlar kullanmayı tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="042dc-124">If you are already well-versed in Azure PowerShell or Azure CLI, then you may prefer to use alternate approaches.</span></span> <span data-ttu-id="042dc-125">Bu diğer yaklaşımlar hakkında bilgi edinmek için [Azure disk şifrelemesi](../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="042dc-125">To learn about these other approaches, see [Azure disk encryption](../security/azure-security-disk-encryption.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="042dc-126">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="042dc-126">See also</span></span>
<span data-ttu-id="042dc-127">Bu belgede Güvenlik Merkezi öneri "Uygula disk şifrelemesi." uygulamak nasıl oluşturulacağını gösterir</span><span class="sxs-lookup"><span data-stu-id="042dc-127">This document showed you how to implement the Security Center recommendation "Apply disk encryption."</span></span> <span data-ttu-id="042dc-128">Disk şifrelemesi hakkında daha fazla bilgi için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="042dc-128">To learn more about disk encryption, see the following:</span></span>

* <span data-ttu-id="042dc-129">[Azure anahtar kasası ile şifreleme ve anahtar yönetimi](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (video, 36 min 39 sn)--korumak ve verilerinizi korumaya yardımcı olmak için disk şifreleme Yönetimi Iaas Vm'leri ve Azure anahtar kasası için kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="042dc-129">[Encryption and key management with Azure Key Vault](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (video, 36 min 39 sec) -- Learn how to use disk encryption management for IaaS VMs and Azure Key Vault to help protect and safeguard your data.</span></span>
* <span data-ttu-id="042dc-130">[Bir Azure sanal Makine'yi şifreleme](security-center-disk-encryption.md) (belge)--Azure Virtual Machines şifreleme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="042dc-130">[Encrypt an Azure Virtual Machine](security-center-disk-encryption.md) (document) -- Learn how to encrypt Azure Virtual Machines.</span></span>
* <span data-ttu-id="042dc-131">[Azure disk şifrelemesi](../security/azure-security-disk-encryption.md) (belge)--disk şifrelemesi Windows ve Linux VM'ler için etkinleştirmeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="042dc-131">[Azure disk encryption](../security/azure-security-disk-encryption.md) (document) -- Learn how to enable disk encryption for Windows and Linux VMs.</span></span>

<span data-ttu-id="042dc-132">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="042dc-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="042dc-133">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --güvenlik ilkeleri yapılandırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="042dc-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="042dc-134">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --Azure kaynaklarınızı sağlığını izlemek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="042dc-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="042dc-135">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) -- Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="042dc-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="042dc-136">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="042dc-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="042dc-137">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -- Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="042dc-137">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="042dc-138">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="042dc-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
