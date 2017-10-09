---
title: "aaaAzure şifrelemeli REST kişisel verileri koruma | Microsoft Docs"
description: "Bu makalede, Azure tooprotect kişisel verileri kullanmanıza yardımcı olacak bir dizi bir parçasıdır"
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
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="96fe8-103">Azure şifreleme teknolojilerini: rest şifrelemeli kişisel verileri korumak</span><span class="sxs-lookup"><span data-stu-id="96fe8-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="96fe8-104">Bu makalede anlamak ve Azure şifreleme teknolojileri toosecure veri bekleyen kullanmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="96fe8-104">This article helps you understand and use Azure encryption technologies toosecure data at rest.</span></span>

<span data-ttu-id="96fe8-105">En iyi yöntem tooprotect hassas veya kişisel veri ve toomeet uyumluluk ve veri gizlilik gereksinimleri kalan verileri şifrelemesini gereklidir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-105">Encryption of data at rest is essential as a best practice tooprotect sensitive or personal data and toomeet compliance and data privacy requirements.</span></span>
<span data-ttu-id="96fe8-106">Bekleyen şifreleme zaman diskteki veri şifrelenir hello sağlayarak şifrelenmemiş hello veri erişimini tasarlanmış tooprevent hello saldırgan ' dir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-106">Encryption at rest is designed tooprevent hello attacker from accessing hello unencrypted data by ensuring hello data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="96fe8-107">Senaryo</span><span class="sxs-lookup"><span data-stu-id="96fe8-107">Scenario</span></span> 

<span data-ttu-id="96fe8-108">Merhaba Amerika Birleşik Devletleri, yönetim büyük seyahat şirket, kendi işlemleri toooffer programlarıyla hello İngiliz Adaları arasında yanı sıra hello Akdeniz ve Baltık seas genişletmektedir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="96fe8-109">toosupport bu çaba İtalya, Almanya, Danimarka ve hello İngiltere dayanarak birkaç küçük seyahat satırları aldı</span><span class="sxs-lookup"><span data-stu-id="96fe8-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="96fe8-110">Merhaba şirket hello bulutta Microsoft Azure toostore şirket verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="96fe8-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="96fe8-111">Bu çalışan ve/veya müşteri bilgileri gibi içerebilir:</span><span class="sxs-lookup"><span data-stu-id="96fe8-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="96fe8-112">adresleri</span><span class="sxs-lookup"><span data-stu-id="96fe8-112">addresses</span></span>
- <span data-ttu-id="96fe8-113">Telefon numaraları</span><span class="sxs-lookup"><span data-stu-id="96fe8-113">phone numbers</span></span>
- <span data-ttu-id="96fe8-114">Vergi kimlik numaraları</span><span class="sxs-lookup"><span data-stu-id="96fe8-114">tax identification numbers</span></span>
- <span data-ttu-id="96fe8-115">Sağlık bilgileri</span><span class="sxs-lookup"><span data-stu-id="96fe8-115">medical information</span></span>
- <span data-ttu-id="96fe8-116">Kredi kartı bilgileri</span><span class="sxs-lookup"><span data-stu-id="96fe8-116">credit card information</span></span>

<span data-ttu-id="96fe8-117">Merhaba şirket ihtiyaç veri erişilebilir toothose Departmanlar yaparken hello gizlilik çalışan ve Müşteri verilerinin korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="96fe8-118">(bordro ve ayırmaları Departmanlar gibi)</span><span class="sxs-lookup"><span data-stu-id="96fe8-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="96fe8-119">Merhaba seyahat satır Ayrıca, kişisel bilgi tootrack ilişkileri geçerli ve geçmiş müşterilerle içeren büyük bir veritabanını ödül ve bağlılık programı üyeleri korur.</span><span class="sxs-lookup"><span data-stu-id="96fe8-119">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="96fe8-120">Sorun bildirimi</span><span class="sxs-lookup"><span data-stu-id="96fe8-120">Problem statement</span></span>

<span data-ttu-id="96fe8-121">Merhaba şirket, çalışanların ve müşterilerin kişisel verilerin hello gizliliği (bordro ve ayırmaları Departmanlar gibi) gereken veri erişilebilir toothose Departmanlar yaparken korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-121">hello company must protect hello privacy of employees’ and customers’ personal data while making data accessible toothose departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="96fe8-122">Bu kişisel verileri hello denetlenen kurumsal veri merkezi dışında depolanır ve hello şirketin fiziksel denetiminde değildir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-122">This personal data is stored outside of hello corporate-controlled data center and is not under hello company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="96fe8-123">Şirket hedefi</span><span class="sxs-lookup"><span data-stu-id="96fe8-123">Company goal</span></span>

<span data-ttu-id="96fe8-124">Çok katmanlı savunma güvenlik stratejisinin bir parçası, kişisel verileri içeren tüm veri kaynakları, bulut depolama alanında bulunan dahil olmak üzere şifrelenmesini şirket hedef tooensure değil.</span><span class="sxs-lookup"><span data-stu-id="96fe8-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal tooensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="96fe8-125">Kişi kazanç erişim toohello kişisel verileri yetkisiz okunamaz kılacak bir formda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-125">If unauthorized persons gain access toohello personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="96fe8-126">Şifreleme uygulama kolay veya – kullanıcılar ve Yöneticiler için saydam olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="96fe8-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="96fe8-127">Çözümler</span><span class="sxs-lookup"><span data-stu-id="96fe8-127">Solutions</span></span>

<span data-ttu-id="96fe8-128">Azure hizmetleri sağlayan birden çok Araçlar ve teknolojiler toohelp şifreleyerek rest kişisel verileri koruyun.</span><span class="sxs-lookup"><span data-stu-id="96fe8-128">Azure services provide multiple tools and technologies toohelp you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="96fe8-129">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="96fe8-129">Azure Key Vault</span></span>

<span data-ttu-id="96fe8-130">[Azure anahtar kasası](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) hello anahtarları kullanılan tooencrypt veri Azure Hizmetleri bekleyen ve hello anahtar depolama ve yönetim çözümü önerilir güvenli depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="96fe8-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for hello keys used tooencrypt data at rest in Azure services and is hello recommended key storage and management solution.</span></span> <span data-ttu-id="96fe8-131">Şifreleme anahtar yönetimi depolanan önemli toosecuring verilerdir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-131">Encryption key management is essential toosecuring stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a><span data-ttu-id="96fe8-132">Kişisel verileri şifrelemek Azure anahtar kasası tooprotect anahtarları nasıl kullanabilirim?</span><span class="sxs-lookup"><span data-stu-id="96fe8-132">How do I use Azure Key Vault tooprotect keys that encrypt personal data?</span></span>

<span data-ttu-id="96fe8-133">Azure anahtar kasası toouse, abonelik tooan Azure hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-133">toouse Azure Key Vault, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="96fe8-134">Ayrıca Azure PowerShell yüklü gerekir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="96fe8-135">PowerShell cmdlet'leri toodo hello aşağıdakileri kullanarak adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="96fe8-135">Steps include using PowerShell cmdlets toodo hello following:</span></span>

1. <span data-ttu-id="96fe8-136">Tooyour abonelikleri Bağlan</span><span class="sxs-lookup"><span data-stu-id="96fe8-136">Connect tooyour subscriptions</span></span>

2. <span data-ttu-id="96fe8-137">Bir anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="96fe8-137">Create a key vault</span></span>

3. <span data-ttu-id="96fe8-138">Bir anahtar veya gizli toohello anahtar kasası ekleme</span><span class="sxs-lookup"><span data-stu-id="96fe8-138">Add a key or secret toohello key vault</span></span>

4. <span data-ttu-id="96fe8-139">Azure Active Directory ile Merhaba anahtar kasası kullanacak uygulamaları kaydetme</span><span class="sxs-lookup"><span data-stu-id="96fe8-139">Register applications that will use hello key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="96fe8-140">Merhaba uygulamaları toouse hello anahtar veya gizli yetkilendirmek</span><span class="sxs-lookup"><span data-stu-id="96fe8-140">Authorize hello applications toouse hello key or secret</span></span>

<span data-ttu-id="96fe8-141">toocreate bir anahtar kasası hello New-AzureRmKeyVault PowerShell cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="96fe8-141">toocreate a key vault, use hello New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="96fe8-142">Kasa adı, kaynak grubu adı ve coğrafi konum atar.</span><span class="sxs-lookup"><span data-stu-id="96fe8-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="96fe8-143">Diğer cmdlet'ler anahtarlarında yönetirken hello kasa adını kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="96fe8-143">You’ll use hello vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="96fe8-144">Merhaba REST API aracılığıyla hello kasası kullanan uygulamaların hello kasa URI'si kullanır.</span><span class="sxs-lookup"><span data-stu-id="96fe8-144">Applications that use hello vault through hello REST API will use hello vault URI.</span></span>

<span data-ttu-id="96fe8-145">Azure anahtar kasası yazılımla korunan anahtardan sizin için sağlayabilir veya mevcut bir anahtarı içeri aktarabilirsiniz bir. PFX dosyası.</span><span class="sxs-lookup"><span data-stu-id="96fe8-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="96fe8-146">Merhaba kasasına gizli anahtarları (Parolalar) de depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-146">You can also store secrets (passwords) in hello vault.</span></span>

<span data-ttu-id="96fe8-147">Ayrıca, yerel HSM'NİZDE bir anahtar oluşturmak ve hello HSM sınırını terk hello anahtar olmadan hello anahtar kasası hizmetindeki tooHSMs aktarım.</span><span class="sxs-lookup"><span data-stu-id="96fe8-147">You can also generate a key in your local HSM and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary.</span></span>

<span data-ttu-id="96fe8-148">Azure anahtar kasası kullanma hakkında ayrıntılı yönergeler izleyin hello adımları [Azure anahtar kasası ile çalışmaya başlama.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span><span class="sxs-lookup"><span data-stu-id="96fe8-148">For detailed instructions on using Azure Key Vault, follow hello steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="96fe8-149">Azure anahtar kasası ile kullanılan PowerShell cmdlet'leri listesi için bkz: [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="96fe8-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="96fe8-150">Windows için Azure Disk şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="96fe8-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="96fe8-151">[Azure Disk şifrelemesi for Windows ve Linux Iaas VM'ler](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) Azure sanal makinelerde rest kişisel verilerinizi korur ve Azure anahtar kasası ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="96fe8-152">Azure Disk şifrelemesi kullanan [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) Windows ve [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux tooencrypt hem işletim sistemi ve hello veri diskleri hello.</span><span class="sxs-lookup"><span data-stu-id="96fe8-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt both hello OS and hello data disks.</span></span> <span data-ttu-id="96fe8-153">Azure Disk şifrelemesi, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 ve Windows 8 ve Windows 10 istemcileri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a><span data-ttu-id="96fe8-154">Azure Disk şifrelemesi tooprotect kişisel verileri nasıl kullanabilirim?</span><span class="sxs-lookup"><span data-stu-id="96fe8-154">How do I use Azure Disk Encryption tooprotect personal data?</span></span>

<span data-ttu-id="96fe8-155">Azure Disk şifrelemesi toouse, abonelik tooan Azure hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-155">toouse Azure Disk Encryption, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="96fe8-156">için tooenable Azure Disk şifrelemesi Windows ve Linux VM'ler hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="96fe8-156">tooenable Azure Disk Encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="96fe8-157">Hello Azure Disk şifrelemesi Resource Manager şablonu, PowerShell veya hello komut satırı arabirimi (CLI) tooenable disk şifrelemesi kullanın ve şifreleme yapılandırması belirtin.</span><span class="sxs-lookup"><span data-stu-id="96fe8-157">Use hello Azure Disk Encryption Resource Manager template, PowerShell, or hello command line interface (CLI) tooenable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="96fe8-158">GRANT erişim toohello Azure platformu tooread hello şifreleme anahtar kasanızı malzemesini.</span><span class="sxs-lookup"><span data-stu-id="96fe8-158">Grant access toohello Azure platform tooread hello encryption material from your key vault.</span></span>

3. <span data-ttu-id="96fe8-159">Bir Azure Active Directory (AAD) uygulama kimliği toowrite hello şifreleme anahtar malzeme tooyour anahtar kasası sağlar.</span><span class="sxs-lookup"><span data-stu-id="96fe8-159">Provide an Azure Active Directory (AAD) application identity toowrite hello encryption key material tooyour key vault.</span></span>

<span data-ttu-id="96fe8-160">Azure VM hello ve hello anahtar kasası yapılandırma güncelleyin ve şifrelenmiş VM'nizi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="96fe8-160">Azure will update hello VM and hello key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="96fe8-161">Anahtar kasası toosupport Azure Disk şifrelemesi ayarladığınızda, ek güvenlik ve şifrelenmiş sanal makinelerin toosupport yedekleme için bir anahtar şifreleme anahtarı (KEK) ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96fe8-161">When you set up your key vault toosupport Azure Disk Encryption, you can add a key encryption key (KEK) for added security and toosupport backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="96fe8-162">Ayrıntılı yönergeler belirli dağıtım senaryoları ve kullanıcı deneyimleri için dahil edilmiştir [için Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span><span class="sxs-lookup"><span data-stu-id="96fe8-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="96fe8-163">Azure Depolama Hizmeti Şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="96fe8-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="96fe8-164">[Azure Storage hizmeti şifreleme (SSE) bekleyen veri için](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) korumak ve veri toomeet, kuruluş güvenlik ve uyumluluk taahhüt korumaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="96fe8-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="96fe8-165">Azure depolama otomatik olarak 256 bit AES şifreleme önceki toopersisting toostorage kullanarak verilerinizi şifreler ve önceki tooretrieval şifresini çözer.</span><span class="sxs-lookup"><span data-stu-id="96fe8-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior toopersisting toostorage, and decrypts it prior tooretrieval.</span></span> <span data-ttu-id="96fe8-166">Bu hizmet, Azure BLOB'ları ve dosyaları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a><span data-ttu-id="96fe8-167">Depolama hizmeti şifrelemesi tooprotect kişisel verileri nasıl kullanabilirim?</span><span class="sxs-lookup"><span data-stu-id="96fe8-167">How do I use Storage Service Encryption tooprotect personal data?</span></span>

<span data-ttu-id="96fe8-168">tooenable depolama hizmeti şifrelemesi, hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="96fe8-168">tooenable Storage Service Encryption, do hello following:</span></span>

1. <span data-ttu-id="96fe8-169">Hello Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="96fe8-169">Log into hello Azure portal.</span></span>

2. <span data-ttu-id="96fe8-170">Bir depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="96fe8-170">Select a storage account.</span></span>

3. <span data-ttu-id="96fe8-171">Ayarları'nda, hello Blob hizmeti bölümü altında şifreleme seçin.</span><span class="sxs-lookup"><span data-stu-id="96fe8-171">In Settings, under hello Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="96fe8-172">Hello dosya hizmeti bölümü altında şifreleme seçin.</span><span class="sxs-lookup"><span data-stu-id="96fe8-172">Under hello File Service section, select Encryption.</span></span>

<span data-ttu-id="96fe8-173">Hello şifreleme ayarı tıkladıktan sonra etkinleştirme veya depolama hizmeti şifrelemesi devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96fe8-173">After you click hello Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="96fe8-174">Yeni veri şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-174">New data will be encrypted.</span></span> <span data-ttu-id="96fe8-175">Bu depolama hesabı var olan dosyalardaki veriler şifrelenmemiş kalır.</span><span class="sxs-lookup"><span data-stu-id="96fe8-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="96fe8-176">Şifreleme etkinleştirdikten sonra yöntemler aşağıdaki hello birini kullanarak veri toohello depolama hesabı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="96fe8-176">After enabling encryption, copy data toohello storage account using one of hello following methods:</span></span>

1. <span data-ttu-id="96fe8-177">Kopyalama BLOB veya hello dosyalarıyla [AzCopy komut satırı yardımcı programı](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span><span class="sxs-lookup"><span data-stu-id="96fe8-177">Copy blobs or files with hello [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="96fe8-178">[SMB kullanan bir dosya paylaşımını bağlama](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) Robocopy toocopy dosyaları gibi bir yardımcı programını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96fe8-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy toocopy files.</span></span>

3. <span data-ttu-id="96fe8-179">Depolama hesaplarını kullanarak blob veya dosya veri tooand blob depolama biriminden veya arasında kopyalama [depolama istemcisi kitaplıklarını .NET gibi](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="96fe8-179">Copy blob or file data tooand from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="96fe8-180">Kullanım bir [Depolama Gezgini](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload BLOB tooyour depolama hesabı'şifreleme etkin.</span><span class="sxs-lookup"><span data-stu-id="96fe8-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload blobs tooyour storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="96fe8-181">Saydam Veri Şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="96fe8-181">Transparent Data Encryption</span></span>

<span data-ttu-id="96fe8-182">Saydam veri şifreleme (TDE), SQL Azure hem hello veritabanı ve sunucu düzeyi verileri şifrelemek bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both hello database and server levels.</span></span> <span data-ttu-id="96fe8-183">TDE, şimdi tüm yeni oluşturulan veritabanı üzerinde varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="96fe8-184">TDE, gerçek zamanlı I/O şifreleme ve şifre çözme hello veri ve günlük dosyalarının gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-184">TDE performs real-time I/O encryption and decryption of hello data and log files.</span></span>

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a><span data-ttu-id="96fe8-185">TDE tooprotect kişisel verileri nasıl kullanabilirim?</span><span class="sxs-lookup"><span data-stu-id="96fe8-185">How do I use TDE tooprotect personal data?</span></span>

<span data-ttu-id="96fe8-186">TDE hello Azure portal hello REST API veya PowerShell kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96fe8-186">You can configure TDE through hello Azure portal, by using hello REST API, or by using PowerShell.</span></span> <span data-ttu-id="96fe8-187">tooenable TDE hello Azure Portal kullanarak var olan bir veritabanı üzerinde hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="96fe8-187">tooenable TDE on an existing database using hello Azure Portal, do hello following:</span></span>

1. <span data-ttu-id="96fe8-188">Hello Azure'ı ziyaret edin, portal <https://portal.azure.com> ve Azure yönetici veya katkıda hesabınız ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="96fe8-188">Visit hello Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="96fe8-189">Merhaba sol başlık tooBROWSE'ı tıklatın ve ardından SQL veritabanları tıklayın.</span><span class="sxs-lookup"><span data-stu-id="96fe8-189">On hello left banner, click tooBROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="96fe8-190">Merhaba sol bölmede seçili SQL veritabanları ile kullanıcı veritabanınız'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="96fe8-190">With SQL databases selected in hello left pane, click your user database.</span></span>

4. <span data-ttu-id="96fe8-191">Merhaba veritabanı dikey penceresinde tüm ayarlar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="96fe8-191">In hello database blade, click All settings.</span></span>

5. <span data-ttu-id="96fe8-192">Hello ayarları dikey penceresinde, saydam veri şifreleme bölümü tooopen hello saydam veri şifreleme dikey tıklayın.</span><span class="sxs-lookup"><span data-stu-id="96fe8-192">In hello Settings blade, click Transparent data encryption part tooopen hello Transparent data encryption blade.</span></span>

6. <span data-ttu-id="96fe8-193">Merhaba veri şifreleme dikey penceresinde hello veri şifreleme düğmesi tooOn taşıyın ve (Merhaba sayfanın en üstündeki hello) Kaydet'i tıklatın tooapply hello ayarı.</span><span class="sxs-lookup"><span data-stu-id="96fe8-193">In hello Data encryption blade, move hello Data encryption button tooOn, and then click Save (at hello top of hello page) tooapply hello setting.</span></span> <span data-ttu-id="96fe8-194">Merhaba şifreleme durumu hello saydam veri şifreleme hello ilerlemesini yaklaşık.</span><span class="sxs-lookup"><span data-stu-id="96fe8-194">hello Encryption status will approximate hello progress of hello transparent data encryption.</span></span>

![Veri şifrelemeyi etkinleştirme](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="96fe8-196">Tooenable TDE ve TDE korumalı veritabanları ve daha fazlasını çözme hakkında bilgi hello makalesinde nasıl bulunabilir yönergeleri [saydam veri şifrelemesi ile Azure SQL veritabanı.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span><span class="sxs-lookup"><span data-stu-id="96fe8-196">Instructions on how tooenable TDE and information on decrypting TDE-protected databases and more can be found in hello article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="96fe8-197">Özet</span><span class="sxs-lookup"><span data-stu-id="96fe8-197">Summary</span></span>

<span data-ttu-id="96fe8-198">Merhaba şirket hello Azure bulut depolanan kişisel verileri şifreleme kendi amacı gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96fe8-198">hello company can accomplish its goal of encrypting personal data stored in hello Azure cloud.</span></span> <span data-ttu-id="96fe8-199">Azure Disk şifrelemesi kullanarak bunu yapabilmeleri çok tüm birimlerini koruyun.</span><span class="sxs-lookup"><span data-stu-id="96fe8-199">They can do this by using Azure Disk Encryption too protect entire volumes.</span></span> <span data-ttu-id="96fe8-200">Bu, hem hello işletim sistemi dosyalarını hem de kişisel olarak tanımlanabilir bilgileri ve diğer hassas verileri tutmak veri dosyaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-200">This may include both hello operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="96fe8-201">Azure depolama hizmeti şifrelemesi, BLOB'lar ve dosyaları depolanan kullanılan tooprotect kişisel veriler olabilir.</span><span class="sxs-lookup"><span data-stu-id="96fe8-201">Azure Storage Service encryption can be used tooprotect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="96fe8-202">Azure SQL veritabanlarında depolanan veriler için saydam veri şifreleme yetkisiz Etkilenme kişisel bilgilerin kullanımına karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="96fe8-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="96fe8-203">azure'da kullanılan tooencrypt veri tooprotect hello anahtarları, Azure anahtar kasası hello şirket kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96fe8-203">tooprotect hello keys that are used tooencrypt data in Azure, hello company can use Azure Key Vault.</span></span> <span data-ttu-id="96fe8-204">Bu hello anahtar yönetimi işlemini kolaylaştırır ve erişmek ve kişisel veri şifreleme anahtarları şirket toomaintain denetimini etkinleştirir hello.</span><span class="sxs-lookup"><span data-stu-id="96fe8-204">This streamlines hello key management process and enables hello company toomaintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96fe8-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96fe8-205">Next steps</span></span>

- [<span data-ttu-id="96fe8-206">Azure Disk şifrelemesi sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="96fe8-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="96fe8-207">Azure sanal Makine'yi şifreleme</span><span class="sxs-lookup"><span data-stu-id="96fe8-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="96fe8-208">Azure Data Lake Store'da verilerin şifrelenmesi</span><span class="sxs-lookup"><span data-stu-id="96fe8-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="96fe8-209">Bekleyen Azure Cosmos DB veritabanı şifreleme</span><span class="sxs-lookup"><span data-stu-id="96fe8-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
