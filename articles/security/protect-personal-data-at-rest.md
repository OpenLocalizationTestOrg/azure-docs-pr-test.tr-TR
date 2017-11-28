---
title: "Azure kişisel verileri koruma şifrelemeli REST | Microsoft Docs"
description: "Bu makalede, kişisel verileri korumak için Azure kullanmanıza yardımcı olacak bir dizi bir parçasıdır"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: d0ef3ca8d48f5ba11a89c787ff59df39eeaf673b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="22f3b-103">Azure şifreleme teknolojilerini: rest şifrelemeli kişisel verileri korumak</span><span class="sxs-lookup"><span data-stu-id="22f3b-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="22f3b-104">Bu makalede anlamak ve durağan verilerin güvenliğini sağlamak için Azure şifreleme teknolojilerini kullanmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="22f3b-104">This article helps you understand and use Azure encryption technologies to secure data at rest.</span></span>

<span data-ttu-id="22f3b-105">Kalan verileri şifrelemesini bir en iyi uygulama olarak hassas veya kişisel verileri korumak ve uyumluluk ve veri gizlilik gereksinimlerini karşılamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-105">Encryption of data at rest is essential as a best practice to protect sensitive or personal data and to meet compliance and data privacy requirements.</span></span>
<span data-ttu-id="22f3b-106">Bekleyen şifreleme saldırgan şifrelenmemiş erişimini engellemek için tasarlanmıştır, diskteki verileri sağlayarak veriler şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-106">Encryption at rest is designed to prevent the attacker from accessing the unencrypted data by ensuring the data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="22f3b-107">Senaryo</span><span class="sxs-lookup"><span data-stu-id="22f3b-107">Scenario</span></span> 

<span data-ttu-id="22f3b-108">Amerika Birleşik Devletleri'nde yönetim büyük seyahat şirket, İngiliz Adaları arasında yanı sıra Akdeniz ve Baltık seas masraflarını sunmaya işlemlerini genişletmektedir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="22f3b-109">Bu çalışmalarını desteklemek için daha küçük birkaç seyahat satırlarını İtalya, Almanya, Danimarka ve İngiltere göre aldı</span><span class="sxs-lookup"><span data-stu-id="22f3b-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and the U.K.</span></span>

<span data-ttu-id="22f3b-110">Şirket Microsoft Azure bulutta şirket verilerini depolamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="22f3b-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="22f3b-111">Bu çalışan ve/veya müşteri bilgileri gibi içerebilir:</span><span class="sxs-lookup"><span data-stu-id="22f3b-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="22f3b-112">adresleri</span><span class="sxs-lookup"><span data-stu-id="22f3b-112">addresses</span></span>
- <span data-ttu-id="22f3b-113">Telefon numaraları</span><span class="sxs-lookup"><span data-stu-id="22f3b-113">phone numbers</span></span>
- <span data-ttu-id="22f3b-114">Vergi kimlik numaraları</span><span class="sxs-lookup"><span data-stu-id="22f3b-114">tax identification numbers</span></span>
- <span data-ttu-id="22f3b-115">Sağlık bilgileri</span><span class="sxs-lookup"><span data-stu-id="22f3b-115">medical information</span></span>
- <span data-ttu-id="22f3b-116">Kredi kartı bilgileri</span><span class="sxs-lookup"><span data-stu-id="22f3b-116">credit card information</span></span>

<span data-ttu-id="22f3b-117">Şirket verileri ihtiyaç bu Departmanlar için erişilebilir hale getirme sırasında çalışan ve müşteri verilerin gizliliği korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-117">The company must protect the privacy of employee and customer data while making data accessible to those departments that need it.</span></span> <span data-ttu-id="22f3b-118">(bordro ve ayırmaları Departmanlar gibi)</span><span class="sxs-lookup"><span data-stu-id="22f3b-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="22f3b-119">Seyahat satır de geçerli ve geçmiş müşterilerle ilişkilerini izlemek için kişisel bilgi içeren büyük bir veritabanı ödül ve bağlılık programı üyelerinin tutar.</span><span class="sxs-lookup"><span data-stu-id="22f3b-119">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="22f3b-120">Sorun bildirimi</span><span class="sxs-lookup"><span data-stu-id="22f3b-120">Problem statement</span></span>

<span data-ttu-id="22f3b-121">Şirket verileri (bordro ve ayırmaları Departmanlar gibi) ihtiyaç bu Departmanlar için erişilebilir olmasını sağlarken çalışanlarınızın ve müşterilerin kişisel verilerin gizliliği konusunda korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-121">The company must protect the privacy of employees’ and customers’ personal data while making data accessible to those departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="22f3b-122">Bu kişisel verileri şirket denetimli veri merkezi dışında depolanır ve şirketin fiziksel denetimi altında değil.</span><span class="sxs-lookup"><span data-stu-id="22f3b-122">This personal data is stored outside of the corporate-controlled data center and is not under the company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="22f3b-123">Şirket hedefi</span><span class="sxs-lookup"><span data-stu-id="22f3b-123">Company goal</span></span>

<span data-ttu-id="22f3b-124">Çok katmanlı savunma güvenlik stratejisinin bir parçası, kişisel verileri içeren tüm veri kaynakları, bulut depolama alanında bulunan dahil olmak üzere şifrelendiğinden emin olmak için bir şirket hedeftir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal to ensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="22f3b-125">Yetkisiz kişilerin kişisel verilere erişirse, okunamaz kılacak bir biçiminde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="22f3b-125">If unauthorized persons gain access to the personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="22f3b-126">Şifreleme uygulama kolay veya – kullanıcılar ve Yöneticiler için saydam olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="22f3b-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="22f3b-127">Çözümler</span><span class="sxs-lookup"><span data-stu-id="22f3b-127">Solutions</span></span>

<span data-ttu-id="22f3b-128">Birden çok Araçlar ve teknolojiler kalan kişisel verileri şifreleyerek korumanıza yardımcı olmak için Azure hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="22f3b-128">Azure services provide multiple tools and technologies to help you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="22f3b-129">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="22f3b-129">Azure Key Vault</span></span>

<span data-ttu-id="22f3b-130">[Azure anahtar kasası](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) Azure Hizmetleri, kalan verileri şifrelemek için kullanılan anahtarları için güvenli depolama sağlar ve önerilen anahtar depolama ve yönetimi çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="22f3b-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for the keys used to encrypt data at rest in Azure services and is the recommended key storage and management solution.</span></span> <span data-ttu-id="22f3b-131">Şifreleme anahtar yönetimi, depolanan verilerin güvenliğini sağlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-131">Encryption key management is essential to securing stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-to-protect-keys-that-encrypt-personal-data"></a><span data-ttu-id="22f3b-132">Kişisel veri şifreleme anahtarlarınızı korumak için Azure anahtar kasası nasıl kullanırım?</span><span class="sxs-lookup"><span data-stu-id="22f3b-132">How do I use Azure Key Vault to protect keys that encrypt personal data?</span></span>

<span data-ttu-id="22f3b-133">Azure anahtar kasası kullanmak için bir Azure hesabı için bir abonelik gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="22f3b-133">To use Azure Key Vault, you need a subscription to an Azure account.</span></span> <span data-ttu-id="22f3b-134">Ayrıca Azure PowerShell yüklü gerekir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="22f3b-135">Aşağıdakileri yapmak için PowerShell cmdlet'leri kullanılarak adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="22f3b-135">Steps include using PowerShell cmdlets to do the following:</span></span>

1. <span data-ttu-id="22f3b-136">Aboneliklerinize bağlanma</span><span class="sxs-lookup"><span data-stu-id="22f3b-136">Connect to your subscriptions</span></span>

2. <span data-ttu-id="22f3b-137">Bir anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="22f3b-137">Create a key vault</span></span>

3. <span data-ttu-id="22f3b-138">Anahtar kasasına bir anahtar veya gizli anahtar ekleme</span><span class="sxs-lookup"><span data-stu-id="22f3b-138">Add a key or secret to the key vault</span></span>

4. <span data-ttu-id="22f3b-139">Anahtar kasası Azure Active Directory ile kullanacağınız uygulamaları kaydetme</span><span class="sxs-lookup"><span data-stu-id="22f3b-139">Register applications that will use the key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="22f3b-140">Anahtar veya gizli kullanmak için uygulamalar yetkilendirmek</span><span class="sxs-lookup"><span data-stu-id="22f3b-140">Authorize the applications to use the key or secret</span></span>

<span data-ttu-id="22f3b-141">Bir anahtar kasası oluşturmak için New-AzureRmKeyVault PowerShell cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="22f3b-141">To create a key vault, use the New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="22f3b-142">Kasa adı, kaynak grubu adı ve coğrafi konum atar.</span><span class="sxs-lookup"><span data-stu-id="22f3b-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="22f3b-143">Diğer cmdlet'ler anahtarlarında yönetirken kasa adını kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="22f3b-143">You’ll use the vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="22f3b-144">REST API'si aracılığıyla kasası kullanan uygulamaların URI kasası kullanır.</span><span class="sxs-lookup"><span data-stu-id="22f3b-144">Applications that use the vault through the REST API will use the vault URI.</span></span>

<span data-ttu-id="22f3b-145">Azure anahtar kasası yazılımla korunan anahtardan sizin için sağlayabilir veya mevcut bir anahtarı içeri aktarabilirsiniz bir. PFX dosyası.</span><span class="sxs-lookup"><span data-stu-id="22f3b-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="22f3b-146">Ayrıca, kasaya parolaları (Parolalar) depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22f3b-146">You can also store secrets (passwords) in the vault.</span></span>

<span data-ttu-id="22f3b-147">Ayrıca, yerel HSM'NİZDE bir anahtar oluşturmak ve bunu Hsm'lerine anahtar kasası hizmetindeki HSM sınırını terk anahtar olmadan aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22f3b-147">You can also generate a key in your local HSM and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary.</span></span>

<span data-ttu-id="22f3b-148">Azure anahtar kasası kullanma hakkında ayrıntılı yönergeleri için adımlarda [Azure anahtar kasası ile çalışmaya başlama.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span><span class="sxs-lookup"><span data-stu-id="22f3b-148">For detailed instructions on using Azure Key Vault, follow the steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="22f3b-149">Azure anahtar kasası ile kullanılan PowerShell cmdlet'leri listesi için bkz: [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="22f3b-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="22f3b-150">Windows için Azure Disk şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="22f3b-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="22f3b-151">[Azure Disk şifrelemesi for Windows ve Linux Iaas VM'ler](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) Azure sanal makinelerde rest kişisel verilerinizi korur ve Azure anahtar kasası ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="22f3b-152">Azure Disk şifrelemesi kullanan [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) Windows ve [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux işletim sistemi ve veri diskleri şifrelemek için de.</span><span class="sxs-lookup"><span data-stu-id="22f3b-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux to encrypt both the OS and the data disks.</span></span> <span data-ttu-id="22f3b-153">Azure Disk şifrelemesi, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 ve Windows 8 ve Windows 10 istemcileri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-to-protect-personal-data"></a><span data-ttu-id="22f3b-154">Azure Disk şifrelemesi kişisel verilerinizi korumak için nasıl kullanırım?</span><span class="sxs-lookup"><span data-stu-id="22f3b-154">How do I use Azure Disk Encryption to protect personal data?</span></span>

<span data-ttu-id="22f3b-155">Azure Disk Şifrelemesi'ni kullanmak için bir Azure hesabı için bir aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-155">To use Azure Disk Encryption, you need a subscription to an Azure account.</span></span> <span data-ttu-id="22f3b-156">İçin Azure Disk şifrelemesi Windows ve Linux VM'ler etkinleştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="22f3b-156">To enable Azure Disk Encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="22f3b-157">Azure Disk şifrelemesi Resource Manager şablonu, PowerShell veya komut satırı arabirimi (CLI) disk şifrelemesi etkinleştirmek ve şifreleme yapılandırmasını belirtmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="22f3b-157">Use the Azure Disk Encryption Resource Manager template, PowerShell, or the command line interface (CLI) to enable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="22f3b-158">Anahtar Kasası'nı şifreleme malzeme okumak için Azure platformu izni verin.</span><span class="sxs-lookup"><span data-stu-id="22f3b-158">Grant access to the Azure platform to read the encryption material from your key vault.</span></span>

3. <span data-ttu-id="22f3b-159">Şifreleme anahtar malzemesini anahtar kasanızı yazmak için bir Azure Active Directory (AAD) uygulama kimliği sağlayın.</span><span class="sxs-lookup"><span data-stu-id="22f3b-159">Provide an Azure Active Directory (AAD) application identity to write the encryption key material to your key vault.</span></span>

<span data-ttu-id="22f3b-160">Azure VM ve anahtar kasası yapılandırmasını güncelleştirin ve şifrelenmiş VM'nizi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="22f3b-160">Azure will update the VM and the key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="22f3b-161">Azure Disk şifrelemesi desteklemek için anahtar kasanızı ayarladığınızda, ek güvenlik için ve şifrelenmiş sanal makinelerinin desteklemek için bir anahtar şifreleme anahtarı (KEK) ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22f3b-161">When you set up your key vault to support Azure Disk Encryption, you can add a key encryption key (KEK) for added security and to support backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="22f3b-162">Ayrıntılı yönergeler belirli dağıtım senaryoları ve kullanıcı deneyimleri için dahil edilmiştir [için Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span><span class="sxs-lookup"><span data-stu-id="22f3b-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="22f3b-163">Azure Depolama Hizmeti Şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="22f3b-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="22f3b-164">[Azure Storage hizmeti şifreleme (SSE) bekleyen veri için](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) korumak ve Kuruluş güvenliği ve uyumluluğu taahhüt karşılamak için verilerinizi korumaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="22f3b-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="22f3b-165">Azure depolama otomatik olarak depolama birimine devam ettirmeden önce 256 bit AES şifreleme kullanarak, verilerinizi şifreler ve alma önce şifresini çözer.</span><span class="sxs-lookup"><span data-stu-id="22f3b-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior to persisting to storage, and decrypts it prior to retrieval.</span></span> <span data-ttu-id="22f3b-166">Bu hizmet, Azure BLOB'ları ve dosyaları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-to-protect-personal-data"></a><span data-ttu-id="22f3b-167">Depolama hizmeti şifrelemesi kişisel verilerinizi korumak için nasıl kullanırım?</span><span class="sxs-lookup"><span data-stu-id="22f3b-167">How do I use Storage Service Encryption to protect personal data?</span></span>

<span data-ttu-id="22f3b-168">Depolama hizmeti şifrelemesi etkinleştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="22f3b-168">To enable Storage Service Encryption, do the following:</span></span>

1. <span data-ttu-id="22f3b-169">Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="22f3b-169">Log into the Azure portal.</span></span>

2. <span data-ttu-id="22f3b-170">Bir depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="22f3b-170">Select a storage account.</span></span>

3. <span data-ttu-id="22f3b-171">Ayarları'nda, Blob hizmeti bölümü altında şifreleme seçin.</span><span class="sxs-lookup"><span data-stu-id="22f3b-171">In Settings, under the Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="22f3b-172">Dosya hizmeti bölümü altında şifreleme seçin.</span><span class="sxs-lookup"><span data-stu-id="22f3b-172">Under the File Service section, select Encryption.</span></span>

<span data-ttu-id="22f3b-173">Şifreleme ayarı tıkladıktan sonra etkinleştirme veya depolama hizmeti şifrelemesi devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22f3b-173">After you click the Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="22f3b-174">Yeni veri şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-174">New data will be encrypted.</span></span> <span data-ttu-id="22f3b-175">Bu depolama hesabı var olan dosyalardaki veriler şifrelenmemiş kalır.</span><span class="sxs-lookup"><span data-stu-id="22f3b-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="22f3b-176">Veri şifreleme etkinleştirdikten sonra aşağıdaki yöntemlerden birini kullanarak depolama hesabına kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="22f3b-176">After enabling encryption, copy data to the storage account using one of the following methods:</span></span>

1. <span data-ttu-id="22f3b-177">BLOB'ları veya dosyaları kopyalama [AzCopy komut satırı yardımcı programı](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span><span class="sxs-lookup"><span data-stu-id="22f3b-177">Copy blobs or files with the [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="22f3b-178">[SMB kullanan bir dosya paylaşımını bağlama](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) dosyaları kopyalamak için Robocopy gibi bir yardımcı programını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22f3b-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy to copy files.</span></span>

3. <span data-ttu-id="22f3b-179">Depolama hesaplarını kullanarak blob veya dosya verileri için ve blob depolamadan veya arasında kopyalamak [depolama istemcisi kitaplıklarını .NET gibi](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="22f3b-179">Copy blob or file data to and from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="22f3b-180">Kullanım bir [Depolama Gezgini](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) BLOB Depolama hesabınıza şifreleme ile karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="22f3b-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) to upload blobs to your storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="22f3b-181">Saydam Veri Şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="22f3b-181">Transparent Data Encryption</span></span>

<span data-ttu-id="22f3b-182">Saydam veri şifreleme (TDE), SQL Azure veritabanı ve sunucu düzeyi verileri şifrelemek bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both the database and server levels.</span></span> <span data-ttu-id="22f3b-183">TDE, şimdi tüm yeni oluşturulan veritabanı üzerinde varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="22f3b-184">TDE, gerçek zamanlı I/O şifreleme ve şifre çözme veri ve günlük dosyalarının gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-184">TDE performs real-time I/O encryption and decryption of the data and log files.</span></span>

#### <a name="how-do-i-use-tde-to-protect-personal-data"></a><span data-ttu-id="22f3b-185">TDE kişisel verilerinizi korumak için nasıl kullanırım?</span><span class="sxs-lookup"><span data-stu-id="22f3b-185">How do I use TDE to protect personal data?</span></span>

<span data-ttu-id="22f3b-186">REST API kullanarak veya PowerShell kullanarak Azure portalı üzerinden TDE yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22f3b-186">You can configure TDE through the Azure portal, by using the REST API, or by using PowerShell.</span></span> <span data-ttu-id="22f3b-187">Azure Portalı'nı kullanarak var olan bir veritabanı üzerinde TDE etkinleştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="22f3b-187">To enable TDE on an existing database using the Azure Portal, do the following:</span></span>

1. <span data-ttu-id="22f3b-188">Azure portalında ziyaret <https://portal.azure.com> ve Azure yönetici veya katkıda hesabınız ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="22f3b-188">Visit the Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="22f3b-189">Sol başlıktaki Gözat'ı tıklatın ve SQL veritabanları'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22f3b-189">On the left banner, click to BROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="22f3b-190">Sol bölmede seçili SQL veritabanları ile kullanıcı veritabanınız'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="22f3b-190">With SQL databases selected in the left pane, click your user database.</span></span>

4. <span data-ttu-id="22f3b-191">Veritabanı dikey penceresinde tüm ayarlar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="22f3b-191">In the database blade, click All settings.</span></span>

5. <span data-ttu-id="22f3b-192">Ayarlar dikey penceresinde Saydam veri şifreleme bölümü saydam veri şifreleme dikey penceresini açmak için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="22f3b-192">In the Settings blade, click Transparent data encryption part to open the Transparent data encryption blade.</span></span>

6. <span data-ttu-id="22f3b-193">Veri şifreleme dikey için veri şifreleme düğmesi taşıyın ve sonra (sayfanın en üstünde) ayarı uygulamak için Kaydet'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="22f3b-193">In the Data encryption blade, move the Data encryption button to On, and then click Save (at the top of the page) to apply the setting.</span></span> <span data-ttu-id="22f3b-194">Şifreleme durumu saydam veri şifreleme ilerlemesini yaklaşık.</span><span class="sxs-lookup"><span data-stu-id="22f3b-194">The Encryption status will approximate the progress of the transparent data encryption.</span></span>

![Veri şifrelemeyi etkinleştirme](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="22f3b-196">TDE etkinleştirmek yönergeler ve TDE korumalı veritabanları ve daha fazlasını çözme hakkında bilgi makalesinde bulunan [saydam veri şifrelemesi ile Azure SQL veritabanı.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span><span class="sxs-lookup"><span data-stu-id="22f3b-196">Instructions on how to enable TDE and information on decrypting TDE-protected databases and more can be found in the article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="22f3b-197">Özet</span><span class="sxs-lookup"><span data-stu-id="22f3b-197">Summary</span></span>

<span data-ttu-id="22f3b-198">Şirket Azure bulutta depolanan kişisel verileri şifreleme kendi amacı gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22f3b-198">The company can accomplish its goal of encrypting personal data stored in the Azure cloud.</span></span> <span data-ttu-id="22f3b-199">Tüm birimleri korumak için Azure Disk şifrelemesi kullanarak bunu.</span><span class="sxs-lookup"><span data-stu-id="22f3b-199">They can do this by using Azure Disk Encryption to  protect entire volumes.</span></span> <span data-ttu-id="22f3b-200">Bu hem işletim sistemi dosyalarını hem de kişisel olarak tanımlanabilir bilgileri ve diğer hassas verileri tutmak veri dosyaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-200">This may include both the operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="22f3b-201">Azure depolama hizmeti şifrelemesi, BLOB'lar ve dosyaları depolanan kişisel verilerinizi korumak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="22f3b-201">Azure Storage Service encryption can be used to protect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="22f3b-202">Azure SQL veritabanlarında depolanan veriler için saydam veri şifreleme yetkisiz Etkilenme kişisel bilgilerin kullanımına karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="22f3b-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="22f3b-203">Azure verileri şifrelemek için kullanılan anahtarları korumak için şirket Azure anahtar kasası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22f3b-203">To protect the keys that are used to encrypt data in Azure, the company can use Azure Key Vault.</span></span> <span data-ttu-id="22f3b-204">Bu anahtar yönetimi işlemini kolaylaştırır ve şirket erişmek ve kişisel veri şifreleme anahtarları denetim kurmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="22f3b-204">This streamlines the key management process and enables the company to maintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22f3b-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="22f3b-205">Next steps</span></span>

- [<span data-ttu-id="22f3b-206">Azure Disk şifrelemesi sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="22f3b-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="22f3b-207">Azure sanal Makine'yi şifreleme</span><span class="sxs-lookup"><span data-stu-id="22f3b-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="22f3b-208">Azure Data Lake Store'da verilerin şifrelenmesi</span><span class="sxs-lookup"><span data-stu-id="22f3b-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="22f3b-209">Bekleyen Azure Cosmos DB veritabanı şifreleme</span><span class="sxs-lookup"><span data-stu-id="22f3b-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
