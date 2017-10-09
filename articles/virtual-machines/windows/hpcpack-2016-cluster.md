---
title: "aaaHPC paketi 2016 küme Azure'da | Microsoft Docs"
description: "Nasıl toodeploy bir HPC Pack 2016 küme Azure'da öğrenin"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="58262-103">Azure'da bir HPC Pack 2016 kümeyi dağıtma</span><span class="sxs-lookup"><span data-stu-id="58262-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="58262-104">Bu makale toodeploy Hello adımları bir [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) Azure sanal makinelerde küme.</span><span class="sxs-lookup"><span data-stu-id="58262-104">Follow hello steps in this article toodeploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="58262-105">HPC Pack, Microsoft'un Microsoft Azure ve Windows Server teknolojileri kurulu ücretsiz HPC çözüm ve geniş HPC iş yüklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="58262-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="58262-106">Merhaba birini kullanın [Azure Resource Manager şablonları](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 küme.</span><span class="sxs-lookup"><span data-stu-id="58262-106">Use one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="58262-107">Küme topolojisi farklı sayıda küme baş düğümler ve ya da Linux, birkaç seçeneğiniz vardır veya Windows işlem düğümleri.</span><span class="sxs-lookup"><span data-stu-id="58262-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58262-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="58262-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="58262-109">PFX sertifikası</span><span class="sxs-lookup"><span data-stu-id="58262-109">PFX certificate</span></span>

<span data-ttu-id="58262-110">Microsoft HPC Pack 2016 kümesi hello HPC düğümler arasında bir kişisel bilgi değişimi (PFX) sertifika toosecure hello iletişim gerektirir.</span><span class="sxs-lookup"><span data-stu-id="58262-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate toosecure hello communication between hello HPC nodes.</span></span> <span data-ttu-id="58262-111">Merhaba sertifika hello aşağıdaki gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="58262-111">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="58262-112">Anahtar değişimi yeteneğine sahip bir özel anahtara sahip olmalıdır</span><span class="sxs-lookup"><span data-stu-id="58262-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="58262-113">Dijital imza ve anahtar şifreleme anahtar kullanımı içerir</span><span class="sxs-lookup"><span data-stu-id="58262-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="58262-114">İstemci kimlik doğrulaması ve sunucu kimlik doğrulaması Gelişmiş anahtar kullanımı içerir</span><span class="sxs-lookup"><span data-stu-id="58262-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="58262-115">Bu gereksinimleri karşılayan bir sertifika yoksa, bir sertifika yetkilisinden hello sertifika isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="58262-115">If you don’t already have a certificate that meets these requirements, you can request hello certificate from a certification authority.</span></span> <span data-ttu-id="58262-116">Alternatif olarak, aşağıdaki komutları toogenerate hello otomatik olarak imzalanan sertifika üretileceği hello komutunu çalıştırın ve hello PFX biçimi sertifikayı özel anahtarla dışarı hello işletim sistemi temel hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58262-116">Alternatively, you can use hello following commands toogenerate hello self-signed certificate based on hello operating system on which you run hello command, and export hello PFX format certificate with private key.</span></span>

* <span data-ttu-id="58262-117">**Windows 10 veya Windows Server 2016 için**, yerleşik hello çalıştırmak **yeni SelfSignedCertificate** PowerShell cmdlet'ini şekilde:</span><span class="sxs-lookup"><span data-stu-id="58262-117">**For Windows 10 or Windows Server 2016**, run hello built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="58262-118">**Windows 10 veya Windows Server 2016'den önceki işletim sistemleri için**, hello karşıdan [otomatik olarak imzalanan sertifika Oluşturucu](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) hello Microsoft Script Center gelen.</span><span class="sxs-lookup"><span data-stu-id="58262-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download hello [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from hello Microsoft Script Center.</span></span> <span data-ttu-id="58262-119">İçeriğini ayıklayın ve komutları bir PowerShell komut isteminde aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="58262-119">Extract its contents and run hello following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a><span data-ttu-id="58262-120">Sertifika tooan Azure anahtar kasası karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="58262-120">Upload certificate tooan Azure key vault</span></span>

<span data-ttu-id="58262-121">Merhaba sertifika tooan Hello HPC küme dağıtmadan önce karşıya yükleme [Azure anahtar kasası](../../key-vault/index.md) hello dağıtımı sırasında kullanmak için bilgi aşağıdaki gizli ve kayıt hello olarak: **kasa adı**,  **Kasa kaynak grubu**, **sertifika URL'si**, ve **sertifika parmak izi**.</span><span class="sxs-lookup"><span data-stu-id="58262-121">Before deploying hello HPC cluster, upload hello certificate tooan [Azure key vault](../../key-vault/index.md) as a secret, and record hello following information for use during hello deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="58262-122">Bir örnek PowerShell komut dosyası tooupload hello sertifika izler.</span><span class="sxs-lookup"><span data-stu-id="58262-122">A sample PowerShell script tooupload hello certificate follows.</span></span> <span data-ttu-id="58262-123">Sertifika tooan Azure anahtar kasası karşıya yükleme hakkında daha fazla bilgi için bkz: [Azure anahtar kasası ile çalışmaya başlama](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="58262-123">For more information about uploading a certificate tooan Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="58262-124">Desteklenen topolojiler</span><span class="sxs-lookup"><span data-stu-id="58262-124">Supported topologies</span></span>

<span data-ttu-id="58262-125">Merhaba birini [Azure Resource Manager şablonları](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 küme.</span><span class="sxs-lookup"><span data-stu-id="58262-125">Choose one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="58262-126">Üç desteklenen küme topolojileri üst düzey mimarilerini aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="58262-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="58262-127">Yüksek kullanılabilirlik topolojileri birden çok küme baş düğümüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="58262-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="58262-128">Active Directory etki alanı ile yüksek oranda kullanılabilirlik kümesi</span><span class="sxs-lookup"><span data-stu-id="58262-128">High-availability cluster with Active Directory domain</span></span>

    ![AD etki alanındaki HA küme](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="58262-130">Active Directory etki alanı olmadan yüksek oranda kullanılabilirlik kümesi</span><span class="sxs-lookup"><span data-stu-id="58262-130">High-availability cluster without Active Directory domain</span></span>

    ![AD etki alanı olmadan HA küme](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="58262-132">Tek bir baş düğüm Küme</span><span class="sxs-lookup"><span data-stu-id="58262-132">Cluster with a single head node</span></span>

   ![Baş düğümü ile küme](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="58262-134">Bir kümeyi dağıtma</span><span class="sxs-lookup"><span data-stu-id="58262-134">Deploy a cluster</span></span>

<span data-ttu-id="58262-135">toocreate hello kümesi, bir şablon seçin ve tıklatın **tooAzure dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="58262-135">toocreate hello cluster, choose a template and click **Deploy tooAzure**.</span></span> <span data-ttu-id="58262-136">Merhaba, [Azure portal](https://portal.azure.com), aşağıdaki adımları hello açıklandığı gibi hello şablon parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="58262-136">In hello [Azure portal](https://portal.azure.com), specify parameters for hello template as described in hello following steps.</span></span> <span data-ttu-id="58262-137">Her şablon hello HPC küme altyapısı için gereken tüm Azure kaynakları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="58262-137">Each template creates all Azure resources required for hello HPC cluster infrastructure.</span></span> <span data-ttu-id="58262-138">Bir Azure sanal ağı, ortak IP adresi, yük dengeleyici (yalnızca için yüksek oranda kullanılabilirlik kümesi), ağ arabirimleri, kullanılabilirlik kümeleri, depolama hesapları ve sanal makineler kaynaklar içerir.</span><span class="sxs-lookup"><span data-stu-id="58262-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a><span data-ttu-id="58262-139">1. adım: hello abonelik, konumunu ve kaynak grubu seçin</span><span class="sxs-lookup"><span data-stu-id="58262-139">Step 1: Select hello subscription, location, and resource group</span></span>

<span data-ttu-id="58262-140">Merhaba **abonelik** ve hello **konumu** PFX sertifikanızı karşıya belirtilen aynı olmalıdır (önkoşullara bakın).</span><span class="sxs-lookup"><span data-stu-id="58262-140">hello **Subscription** and hello **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="58262-141">Oluşturduğunuz öneririz bir **kaynak grubu** hello dağıtımı için.</span><span class="sxs-lookup"><span data-stu-id="58262-141">We recommend that you create a **Resource group** for hello deployment.</span></span>

### <a name="step-2-specify-hello-parameter-settings"></a><span data-ttu-id="58262-142">2. adım: hello parametre ayarlarını belirtin</span><span class="sxs-lookup"><span data-stu-id="58262-142">Step 2: Specify hello parameter settings</span></span>

<span data-ttu-id="58262-143">Girin veya hello şablon parametreleri için değerleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="58262-143">Enter or modify values for hello template parameters.</span></span> <span data-ttu-id="58262-144">Merhaba simgesi Yardım bilgileri için sonraki tooeach parametresi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="58262-144">Click hello icon next tooeach parameter for help information.</span></span> <span data-ttu-id="58262-145">Ayrıca hello yönergeler için bkz. [kullanılabilir VM boyutları](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="58262-145">Also see hello guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="58262-146">Şu parametreler hello hello önkoşulları içinde kaydettiğiniz hello değerleri belirtin: **kasa adı**, **kasası kaynak grubu**, **sertifika URL'si**ve **Sertifika parmak izi**.</span><span class="sxs-lookup"><span data-stu-id="58262-146">Specify hello values you recorded in hello Prerequisites for hello following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="58262-147">3. Adım</span><span class="sxs-lookup"><span data-stu-id="58262-147">Step 3.</span></span> <span data-ttu-id="58262-148">Yasal koşulları gözden geçirin ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="58262-148">Review legal terms and create</span></span>
<span data-ttu-id="58262-149">Tıklatın **yasal koşulları gözden geçir** tooreview hello koşulları.</span><span class="sxs-lookup"><span data-stu-id="58262-149">Click **Review legal terms** tooreview hello terms.</span></span> <span data-ttu-id="58262-150">Kabul ediyorsa **satın alma**ve ardından **oluşturma** toostart hello dağıtım.</span><span class="sxs-lookup"><span data-stu-id="58262-150">If you agree, click **Purchase**, and then click **Create** toostart hello deployment.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="58262-151">Toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="58262-151">Connect toohello cluster</span></span>
1. <span data-ttu-id="58262-152">Merhaba HPC paketi küme dağıtıldıktan sonra toohello Git [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="58262-152">After hello HPC Pack cluster is deployed, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="58262-153">Tıklatın **kaynak grupları**ve hangi hello küme dağıtılan Bul hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="58262-153">Click **Resource groups**, and find hello resource group in which hello cluster was deployed.</span></span> <span data-ttu-id="58262-154">Baş düğüm sanal makineleri hello bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58262-154">You can find hello head node virtual machines.</span></span>

    ![Küme baş düğümler hello portalında](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="58262-156">Bir baş düğümüne tıklayın (yüksek oranda kullanılabilirlik kümesi içinde herhangi bir hello baş düğüme tıklayın).</span><span class="sxs-lookup"><span data-stu-id="58262-156">Click one head node (in a high-availability cluster, click any of hello head nodes).</span></span> <span data-ttu-id="58262-157">İçinde **Essentials**, hello genel IP adresi veya tam DNS adı hello kümesinin bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58262-157">In **Essentials**, you can find hello public IP address or full DNS name of hello cluster.</span></span>

    ![Küme bağlantısı ayarları](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="58262-159">Tıklatın **Bağlan** toolog tooany belirtilen yönetici kullanıcı adınız ile Uzak Masaüstü kullanarak hello baş düğüm üzerinde.</span><span class="sxs-lookup"><span data-stu-id="58262-159">Click **Connect** toolog on tooany of hello head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="58262-160">Dağıttığınız hello küme bir Active Directory etki alanında hello kullanıcı adı hello biçiminde ise, <privateDomainName> \<adminUsername > (örneğin, hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="58262-160">If hello cluster you deployed is in an Active Directory Domain, hello user name is of hello form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="58262-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="58262-161">Next steps</span></span>
* <span data-ttu-id="58262-162">İşlerini tooyour küme gönderin.</span><span class="sxs-lookup"><span data-stu-id="58262-162">Submit jobs tooyour cluster.</span></span> <span data-ttu-id="58262-163">Bkz: [işleri tooHPC Azure HPC Pack kümede gönderme](hpcpack-cluster-submit-jobs.md) ve [Azure Active Directory'yi kullanarak azure'da bir HPC Pack 2016 kümeyi yönetmek](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="58262-163">See [Submit jobs tooHPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

