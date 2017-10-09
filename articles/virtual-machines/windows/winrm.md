---
title: "bir Azure VM için WinRM erişimi aaaSet | Microsoft Docs"
description: "Merhaba Resource Manager dağıtım modelinde oluşturulmuş bir Azure sanal makinesi ile kullanım için WinRM erişim ayarlayın."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="1057a-103">Sanal makineler Azure Kaynak Yöneticisi'nde için WinRM erişimi ayarlama</span><span class="sxs-lookup"><span data-stu-id="1057a-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="1057a-104">Azure Resource Manager Azure Hizmet Yönetimi vs'de WinRM</span><span class="sxs-lookup"><span data-stu-id="1057a-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="1057a-105">Hello Azure Resource Manager genel bakış için lütfen bu bakın [makale](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1057a-105">For an overview of hello Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="1057a-106">Azure Hizmet Yönetimi ve Azure Resource Manager arasındaki farklar için lütfen bu bakın [makale](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="1057a-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="1057a-107">Merhaba hello iki yığınları arasında WinRM yapılandırması ayarlanması anahtar hello sertifika hello VM üzerinde nasıl yüklendiğini farktır.</span><span class="sxs-lookup"><span data-stu-id="1057a-107">hello key difference in setting up WinRM configuration between hello two stacks is how hello certificate gets installed on hello VM.</span></span> <span data-ttu-id="1057a-108">Merhaba sertifikalar, anahtar kasası kaynak sağlayıcısı hello tarafından yönetilen kaynaklar olarak Hello Azure Kaynak Yöneticisi yığınında modellenir.</span><span class="sxs-lookup"><span data-stu-id="1057a-108">In hello Azure Resource Manager stack, hello certificates are modeled as resources managed by hello Key Vault Resource Provider.</span></span> <span data-ttu-id="1057a-109">Bu nedenle, hello kullanıcı kendi sertifikanın tooprovide gerekir ve bir VM kullanmadan önce tooa anahtar kasası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1057a-109">Therefore, hello user needs tooprovide their own certificate and upload it tooa Key Vault before using it in a VM.</span></span>

<span data-ttu-id="1057a-110">Bir VM WinRM bağlantı kurma tootake tooset ihtiyacınız hello adımlar şunlardır</span><span class="sxs-lookup"><span data-stu-id="1057a-110">Here are hello steps you need tootake tooset up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="1057a-111">Anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="1057a-111">Create a Key Vault</span></span>
2. <span data-ttu-id="1057a-112">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="1057a-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="1057a-113">Otomatik olarak imzalanan sertifika tooKey kasası karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="1057a-113">Upload your self-signed certificate tooKey Vault</span></span>
4. <span data-ttu-id="1057a-114">Otomatik olarak imzalanan sertifikanızın hello anahtar kasası Hello URL'sini alma</span><span class="sxs-lookup"><span data-stu-id="1057a-114">Get hello URL for your self-signed certificate in hello Key Vault</span></span>
5. <span data-ttu-id="1057a-115">Bir VM oluşturulurken otomatik olarak imzalanan sertifikalar URL'nizi başvurusu</span><span class="sxs-lookup"><span data-stu-id="1057a-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="1057a-116">1. adım: bir anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="1057a-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="1057a-117">Komut toocreate hello anahtar kasası altındaki hello kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1057a-117">You can use hello below command toocreate hello Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="1057a-118">2. adım: otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="1057a-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="1057a-119">Bu PowerShell Betiği kullanılarak otomatik olarak imzalanan bir sertifika oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="1057a-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a><span data-ttu-id="1057a-120">3. adım: karşıya yükleme, otomatik olarak imzalanan sertifika toohello anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="1057a-120">Step 3: Upload your self-signed certificate toohello Key Vault</span></span>
<span data-ttu-id="1057a-121">1. adımda oluşturduğunuz Hello sertifika toohello anahtar kasası karşıya önce biçiminde hello Microsoft.Compute kaynak sağlayıcısı anlayabileceği tooconverted gerekir.</span><span class="sxs-lookup"><span data-stu-id="1057a-121">Before uploading hello certificate toohello Key Vault created in step 1, it needs tooconverted into a format hello Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="1057a-122">Bunu Hello PowerShell Betiği aşağıdaki izin verir</span><span class="sxs-lookup"><span data-stu-id="1057a-122">hello below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path toohello .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a><span data-ttu-id="1057a-123">4. adım: hello URL'sini otomatik olarak imzalanan sertifikanızın hello anahtar kasası alma</span><span class="sxs-lookup"><span data-stu-id="1057a-123">Step 4: Get hello URL for your self-signed certificate in hello Key Vault</span></span>
<span data-ttu-id="1057a-124">Merhaba Microsoft.Compute kaynak sağlayıcısındaki bir URL toohello gizlilik hello anahtar kasası içinde hello VM sağlarken gerekir.</span><span class="sxs-lookup"><span data-stu-id="1057a-124">hello Microsoft.Compute resource provider needs a URL toohello secret inside hello Key Vault while provisioning hello VM.</span></span> <span data-ttu-id="1057a-125">Bu hello Microsoft.Compute kaynak sağlayıcısı toodownload hello gizliliği sağlar ve hello VM üzerinde hello eşdeğer sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1057a-125">This enables hello Microsoft.Compute resource provider toodownload hello secret and create hello equivalent certificate on hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="1057a-126">Merhaba gizli Hello URL'sini de tooinclude hello sürüm olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1057a-126">hello URL of hello secret needs tooinclude hello version as well.</span></span> <span data-ttu-id="1057a-127">Bir örnek URL'si https://contosovault.vault.azure.net:443/gizli/contososecret/01h9db0df2cd4300a20ence585a6s7ve gibi görünüyor</span><span class="sxs-lookup"><span data-stu-id="1057a-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="1057a-128">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="1057a-128">Templates</span></span>
<span data-ttu-id="1057a-129">Kod aşağıda hello kullanarak hello şablonunda hello bağlantı toohello URL alabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1057a-129">You can get hello link toohello URL in hello template using hello below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="1057a-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1057a-130">PowerShell</span></span>
<span data-ttu-id="1057a-131">Merhaba aşağıdaki PowerShell komutunu kullanarak bu URL'yi elde edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1057a-131">You can get this URL using hello below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="1057a-132">5. adım: bir VM oluşturulurken otomatik olarak imzalanan sertifikalar URL'nizi başvuru</span><span class="sxs-lookup"><span data-stu-id="1057a-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="1057a-133">Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="1057a-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="1057a-134">VM şablonları aracılığıyla oluşturulurken hello sertifika hello gizli bölümü ve aşağıdaki şekilde hello winRM bölümünde başvurulan:</span><span class="sxs-lookup"><span data-stu-id="1057a-134">While creating a VM through templates, hello certificate gets referenced in hello secrets section and hello winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="1057a-135">Yukarıdaki hello için bir örnek şablon burada bulunabilir [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="1057a-135">A sample template for hello above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="1057a-136">Bu şablon için kaynak kodunu bulunabilir [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="1057a-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="1057a-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1057a-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a><span data-ttu-id="1057a-138">6. adım: toohello VM bağlanma</span><span class="sxs-lookup"><span data-stu-id="1057a-138">Step 6: Connecting toohello VM</span></span>
<span data-ttu-id="1057a-139">Toohello VM bağlanmadan önce makinenizde WinRM uzaktan yönetim için yapılandırıldığından emin toomake gerekir.</span><span class="sxs-lookup"><span data-stu-id="1057a-139">Before you can connect toohello VM you'll need toomake sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="1057a-140">Yönetici olarak PowerShell'i başlatın ve komutu toomake ayarladığınızdan emin aşağıda hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="1057a-140">Start PowerShell as an administrator and execute hello below command toomake sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="1057a-141">Yukarıdaki hello çalışmazsa hello WinRM hizmetinin çalıştığından emin toomake gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1057a-141">You might need toomake sure hello WinRM service is running if hello above does not work.</span></span> <span data-ttu-id="1057a-142">Bu kullanarak yapabilirsiniz`Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="1057a-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="1057a-143">Merhaba Kurulum tamamlandığında, toohello VM bağlanabilir komutu aşağıda hello kullanma</span><span class="sxs-lookup"><span data-stu-id="1057a-143">Once hello setup is done, you can connect toohello VM using hello below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
