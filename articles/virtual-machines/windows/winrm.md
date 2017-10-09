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
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a>Sanal makineler Azure Kaynak Yöneticisi'nde için WinRM erişimi ayarlama
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a>Azure Resource Manager Azure Hizmet Yönetimi vs'de WinRM

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* Hello Azure Resource Manager genel bakış için lütfen bu bakın [makale](../../azure-resource-manager/resource-group-overview.md)
* Azure Hizmet Yönetimi ve Azure Resource Manager arasındaki farklar için lütfen bu bakın [makale](../../resource-manager-deployment-model.md)

Merhaba hello iki yığınları arasında WinRM yapılandırması ayarlanması anahtar hello sertifika hello VM üzerinde nasıl yüklendiğini farktır. Merhaba sertifikalar, anahtar kasası kaynak sağlayıcısı hello tarafından yönetilen kaynaklar olarak Hello Azure Kaynak Yöneticisi yığınında modellenir. Bu nedenle, hello kullanıcı kendi sertifikanın tooprovide gerekir ve bir VM kullanmadan önce tooa anahtar kasası yükleyin.

Bir VM WinRM bağlantı kurma tootake tooset ihtiyacınız hello adımlar şunlardır

1. Anahtar kasası oluşturma
2. Otomatik olarak imzalanan sertifika oluşturma
3. Otomatik olarak imzalanan sertifika tooKey kasası karşıya yükle
4. Otomatik olarak imzalanan sertifikanızın hello anahtar kasası Hello URL'sini alma
5. Bir VM oluşturulurken otomatik olarak imzalanan sertifikalar URL'nizi başvurusu

## <a name="step-1-create-a-key-vault"></a>1. adım: bir anahtar kasası oluşturma
Komut toocreate hello anahtar kasası altındaki hello kullanabilirsiniz

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a>2. adım: otomatik olarak imzalanan sertifika oluşturma
Bu PowerShell Betiği kullanılarak otomatik olarak imzalanan bir sertifika oluşturabilir.

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a>3. adım: karşıya yükleme, otomatik olarak imzalanan sertifika toohello anahtar kasası
1. adımda oluşturduğunuz Hello sertifika toohello anahtar kasası karşıya önce biçiminde hello Microsoft.Compute kaynak sağlayıcısı anlayabileceği tooconverted gerekir. Bunu Hello PowerShell Betiği aşağıdaki izin verir

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

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a>4. adım: hello URL'sini otomatik olarak imzalanan sertifikanızın hello anahtar kasası alma
Merhaba Microsoft.Compute kaynak sağlayıcısındaki bir URL toohello gizlilik hello anahtar kasası içinde hello VM sağlarken gerekir. Bu hello Microsoft.Compute kaynak sağlayıcısı toodownload hello gizliliği sağlar ve hello VM üzerinde hello eşdeğer sertifika oluşturun.

> [!NOTE]
> Merhaba gizli Hello URL'sini de tooinclude hello sürüm olması gerekir. Bir örnek URL'si https://contosovault.vault.azure.net:443/gizli/contososecret/01h9db0df2cd4300a20ence585a6s7ve gibi görünüyor
> 
> 

#### <a name="templates"></a>Şablonlar
Kod aşağıda hello kullanarak hello şablonunda hello bağlantı toohello URL alabilirsiniz

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a>PowerShell
Merhaba aşağıdaki PowerShell komutunu kullanarak bu URL'yi elde edebilirsiniz

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a>5. adım: bir VM oluşturulurken otomatik olarak imzalanan sertifikalar URL'nizi başvuru
#### <a name="azure-resource-manager-templates"></a>Azure Resource Manager şablonları
VM şablonları aracılığıyla oluşturulurken hello sertifika hello gizli bölümü ve aşağıdaki şekilde hello winRM bölümünde başvurulan:

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

Yukarıdaki hello için bir örnek şablon burada bulunabilir [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)

Bu şablon için kaynak kodunu bulunabilir [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)

#### <a name="powershell"></a>PowerShell
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a>6. adım: toohello VM bağlanma
Toohello VM bağlanmadan önce makinenizde WinRM uzaktan yönetim için yapılandırıldığından emin toomake gerekir. Yönetici olarak PowerShell'i başlatın ve komutu toomake ayarladığınızdan emin aşağıda hello yürütün.

    Enable-PSRemoting -Force

> [!NOTE]
> Yukarıdaki hello çalışmazsa hello WinRM hizmetinin çalıştığından emin toomake gerekebilir. Bu kullanarak yapabilirsiniz`Get-Service WinRM`
> 
> 

Merhaba Kurulum tamamlandığında, toohello VM bağlanabilir komutu aşağıda hello kullanma

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
