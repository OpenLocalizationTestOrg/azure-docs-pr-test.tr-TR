---
title: "Bir Azure VM için WinRM erişimini Ayarla | Microsoft Docs"
description: "Resource Manager dağıtım modelinde oluşturulmuş bir Azure sanal makinesi ile kullanım için WinRM erişim ayarlayın."
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
ms.openlocfilehash: 2d6533462400bc1d93d0d3b0227769784e2658a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="e0960-103">Sanal makineler Azure Kaynak Yöneticisi'nde için WinRM erişimi ayarlama</span><span class="sxs-lookup"><span data-stu-id="e0960-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="e0960-104">Azure Resource Manager Azure Hizmet Yönetimi vs'de WinRM</span><span class="sxs-lookup"><span data-stu-id="e0960-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="e0960-105">Bir Azure Kaynak Yöneticisi'nin için lütfen bu bkz [makale](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e0960-105">For an overview of the Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="e0960-106">Azure Hizmet Yönetimi ve Azure Resource Manager arasındaki farklar için lütfen bu bakın [makale](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="e0960-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="e0960-107">İki yığınları arasında WinRM yapılandırması ayarlanması anahtar sertifika VM nasıl yüklendiğini farktır.</span><span class="sxs-lookup"><span data-stu-id="e0960-107">The key difference in setting up WinRM configuration between the two stacks is how the certificate gets installed on the VM.</span></span> <span data-ttu-id="e0960-108">Sertifikalar, anahtar kasası kaynak sağlayıcısı tarafından yönetilen kaynaklar olarak Azure Kaynak Yöneticisi yığınında modellenir.</span><span class="sxs-lookup"><span data-stu-id="e0960-108">In the Azure Resource Manager stack, the certificates are modeled as resources managed by the Key Vault Resource Provider.</span></span> <span data-ttu-id="e0960-109">Bu nedenle, kullanıcı kendi sertifikayı sağlayın ve bu bir anahtar Kasası'na VM ile kullanmadan önce karşıya yüklemesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="e0960-109">Therefore, the user needs to provide their own certificate and upload it to a Key Vault before using it in a VM.</span></span>

<span data-ttu-id="e0960-110">WinRM bağlantısına sahip bir VM'yi ayarlamak için atmanız gereken adımlar şunlardır</span><span class="sxs-lookup"><span data-stu-id="e0960-110">Here are the steps you need to take to set up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="e0960-111">Anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0960-111">Create a Key Vault</span></span>
2. <span data-ttu-id="e0960-112">Otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0960-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="e0960-113">Anahtar Kasası'na otomatik olarak imzalanan sertifikanızın karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="e0960-113">Upload your self-signed certificate to Key Vault</span></span>
4. <span data-ttu-id="e0960-114">Otomatik olarak imzalanan sertifikanızın anahtar kasasında URL'sini alma</span><span class="sxs-lookup"><span data-stu-id="e0960-114">Get the URL for your self-signed certificate in the Key Vault</span></span>
5. <span data-ttu-id="e0960-115">Bir VM oluşturulurken otomatik olarak imzalanan sertifikalar URL'nizi başvurusu</span><span class="sxs-lookup"><span data-stu-id="e0960-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="e0960-116">1. adım: bir anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0960-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="e0960-117">Kullanabileceğiniz anahtar kasası oluşturmak için komutu aşağıdaki</span><span class="sxs-lookup"><span data-stu-id="e0960-117">You can use the below command to create the Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="e0960-118">2. adım: otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0960-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="e0960-119">Bu PowerShell Betiği kullanılarak otomatik olarak imzalanan bir sertifika oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="e0960-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter the certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-to-the-key-vault"></a><span data-ttu-id="e0960-120">3. adım: anahtar Kasası'na otomatik olarak imzalanan sertifikanızın karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="e0960-120">Step 3: Upload your self-signed certificate to the Key Vault</span></span>
<span data-ttu-id="e0960-121">1. adımda oluşturduğunuz anahtar kasası için sertifika karşıya önce onu dönüştürülen Microsoft.Compute kaynak sağlayıcısındaki anlayabileceği bir biçime gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0960-121">Before uploading the certificate to the Key Vault created in step 1, it needs to converted into a format the Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="e0960-122">Aşağıdaki PowerShell komut dosyası, bunu izin verir</span><span class="sxs-lookup"><span data-stu-id="e0960-122">The below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path to the .pfx file>"
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

## <a name="step-4-get-the-url-for-your-self-signed-certificate-in-the-key-vault"></a><span data-ttu-id="e0960-123">4. adım: otomatik olarak imzalanan sertifikanızın anahtar kasasında URL'sini alma</span><span class="sxs-lookup"><span data-stu-id="e0960-123">Step 4: Get the URL for your self-signed certificate in the Key Vault</span></span>
<span data-ttu-id="e0960-124">Microsoft.Compute kaynak sağlayıcısındaki VM sağlarken gizli anahtar kasası içinde bir URL gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0960-124">The Microsoft.Compute resource provider needs a URL to the secret inside the Key Vault while provisioning the VM.</span></span> <span data-ttu-id="e0960-125">Bu, gizli anahtarı indirin ve eşdeğer sertifika VM oluşturmak Microsoft.Compute kaynak sağlayıcısındaki sağlar.</span><span class="sxs-lookup"><span data-stu-id="e0960-125">This enables the Microsoft.Compute resource provider to download the secret and create the equivalent certificate on the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="e0960-126">Gizli URL'sini sürümü de içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e0960-126">The URL of the secret needs to include the version as well.</span></span> <span data-ttu-id="e0960-127">Bir örnek URL'si https://contosovault.vault.azure.net:443/gizli/contososecret/01h9db0df2cd4300a20ence585a6s7ve gibi görünüyor</span><span class="sxs-lookup"><span data-stu-id="e0960-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="e0960-128">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="e0960-128">Templates</span></span>
<span data-ttu-id="e0960-129">Şablon kullanarak URL bağlantısını alma kodu aşağıda</span><span class="sxs-lookup"><span data-stu-id="e0960-129">You can get the link to the URL in the template using the below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="e0960-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0960-130">PowerShell</span></span>
<span data-ttu-id="e0960-131">Bu URL'yi kullanarak elde edebilirsiniz PowerShell komutunu aşağıda</span><span class="sxs-lookup"><span data-stu-id="e0960-131">You can get this URL using the below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="e0960-132">5. adım: bir VM oluşturulurken otomatik olarak imzalanan sertifikalar URL'nizi başvuru</span><span class="sxs-lookup"><span data-stu-id="e0960-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="e0960-133">Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="e0960-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="e0960-134">VM şablonları aracılığıyla oluşturulurken, sertifika gizli bölümü ve aşağıdaki şekilde winRM bölümünde başvurulan:</span><span class="sxs-lookup"><span data-stu-id="e0960-134">While creating a VM through templates, the certificate gets referenced in the secrets section and the winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of the Key Vault containing the secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for the certificate you got in Step 4>",
                  "certificateStore": "<Name of the certificate store on the VM>"
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
                  "certificateUrl": "<URL for the certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="e0960-135">Yukarıdaki için bir örnek şablon burada bulunabilir [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="e0960-135">A sample template for the above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="e0960-136">Bu şablon için kaynak kodunu bulunabilir [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="e0960-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="e0960-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0960-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-to-the-vm"></a><span data-ttu-id="e0960-138">6. adım: VM'ye bağlanma</span><span class="sxs-lookup"><span data-stu-id="e0960-138">Step 6: Connecting to the VM</span></span>
<span data-ttu-id="e0960-139">Emin olmak için gerekir VM bağlanmadan önce makinenizde WinRM uzaktan yönetim için yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="e0960-139">Before you can connect to the VM you'll need to make sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="e0960-140">Yönetici olarak PowerShell'i başlatın ve yürütme emin olmak için komut, ayarlamış.</span><span class="sxs-lookup"><span data-stu-id="e0960-140">Start PowerShell as an administrator and execute the below command to make sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="e0960-141">Yukarıdaki işe yaramazsa WinRM hizmetinin çalıştığından emin olmak gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e0960-141">You might need to make sure the WinRM service is running if the above does not work.</span></span> <span data-ttu-id="e0960-142">Bu kullanarak yapabilirsiniz`Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="e0960-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="e0960-143">Kurulum tamamlandığında, VM kullanmaya bağlanabilir komutu aşağıda</span><span class="sxs-lookup"><span data-stu-id="e0960-143">Once the setup is done, you can connect to the VM using the below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
