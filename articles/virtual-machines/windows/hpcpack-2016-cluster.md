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
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a>Azure'da bir HPC Pack 2016 kümeyi dağıtma

Bu makale toodeploy Hello adımları bir [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) Azure sanal makinelerde küme. HPC Pack, Microsoft'un Microsoft Azure ve Windows Server teknolojileri kurulu ücretsiz HPC çözüm ve geniş HPC iş yüklerini destekler.

Merhaba birini kullanın [Azure Resource Manager şablonları](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 küme. Küme topolojisi farklı sayıda küme baş düğümler ve ya da Linux, birkaç seçeneğiniz vardır veya Windows işlem düğümleri.

## <a name="prerequisites"></a>Ön koşullar

### <a name="pfx-certificate"></a>PFX sertifikası

Microsoft HPC Pack 2016 kümesi hello HPC düğümler arasında bir kişisel bilgi değişimi (PFX) sertifika toosecure hello iletişim gerektirir. Merhaba sertifika hello aşağıdaki gereksinimleri karşılamalıdır:

* Anahtar değişimi yeteneğine sahip bir özel anahtara sahip olmalıdır
* Dijital imza ve anahtar şifreleme anahtar kullanımı içerir
* İstemci kimlik doğrulaması ve sunucu kimlik doğrulaması Gelişmiş anahtar kullanımı içerir

Bu gereksinimleri karşılayan bir sertifika yoksa, bir sertifika yetkilisinden hello sertifika isteyebilir. Alternatif olarak, aşağıdaki komutları toogenerate hello otomatik olarak imzalanan sertifika üretileceği hello komutunu çalıştırın ve hello PFX biçimi sertifikayı özel anahtarla dışarı hello işletim sistemi temel hello kullanabilirsiniz.

* **Windows 10 veya Windows Server 2016 için**, yerleşik hello çalıştırmak **yeni SelfSignedCertificate** PowerShell cmdlet'ini şekilde:

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* **Windows 10 veya Windows Server 2016'den önceki işletim sistemleri için**, hello karşıdan [otomatik olarak imzalanan sertifika Oluşturucu](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) hello Microsoft Script Center gelen. İçeriğini ayıklayın ve komutları bir PowerShell komut isteminde aşağıdaki hello çalıştırın:

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a>Sertifika tooan Azure anahtar kasası karşıya yükle

Merhaba sertifika tooan Hello HPC küme dağıtmadan önce karşıya yükleme [Azure anahtar kasası](../../key-vault/index.md) hello dağıtımı sırasında kullanmak için bilgi aşağıdaki gizli ve kayıt hello olarak: **kasa adı**,  **Kasa kaynak grubu**, **sertifika URL'si**, ve **sertifika parmak izi**.

Bir örnek PowerShell komut dosyası tooupload hello sertifika izler. Sertifika tooan Azure anahtar kasası karşıya yükleme hakkında daha fazla bilgi için bkz: [Azure anahtar kasası ile çalışmaya başlama](../../key-vault/key-vault-get-started.md).

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


## <a name="supported-topologies"></a>Desteklenen topolojiler

Merhaba birini [Azure Resource Manager şablonları](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 küme. Üç desteklenen küme topolojileri üst düzey mimarilerini aşağıda verilmiştir. Yüksek kullanılabilirlik topolojileri birden çok küme baş düğümüne ekleyin.

1. Active Directory etki alanı ile yüksek oranda kullanılabilirlik kümesi

    ![AD etki alanındaki HA küme](./media/hpcpack-2016-cluster/haad.png)



2. Active Directory etki alanı olmadan yüksek oranda kullanılabilirlik kümesi

    ![AD etki alanı olmadan HA küme](./media/hpcpack-2016-cluster/hanoad.png)

3. Tek bir baş düğüm Küme

   ![Baş düğümü ile küme](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a>Bir kümeyi dağıtma

toocreate hello kümesi, bir şablon seçin ve tıklatın **tooAzure dağıtmak**. Merhaba, [Azure portal](https://portal.azure.com), aşağıdaki adımları hello açıklandığı gibi hello şablon parametreleri belirtin. Her şablon hello HPC küme altyapısı için gereken tüm Azure kaynakları oluşturur. Bir Azure sanal ağı, ortak IP adresi, yük dengeleyici (yalnızca için yüksek oranda kullanılabilirlik kümesi), ağ arabirimleri, kullanılabilirlik kümeleri, depolama hesapları ve sanal makineler kaynaklar içerir.

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a>1. adım: hello abonelik, konumunu ve kaynak grubu seçin

Merhaba **abonelik** ve hello **konumu** PFX sertifikanızı karşıya belirtilen aynı olmalıdır (önkoşullara bakın). Oluşturduğunuz öneririz bir **kaynak grubu** hello dağıtımı için.

### <a name="step-2-specify-hello-parameter-settings"></a>2. adım: hello parametre ayarlarını belirtin

Girin veya hello şablon parametreleri için değerleri değiştirin. Merhaba simgesi Yardım bilgileri için sonraki tooeach parametresi'ı tıklatın. Ayrıca hello yönergeler için bkz. [kullanılabilir VM boyutları](sizes.md).

Şu parametreler hello hello önkoşulları içinde kaydettiğiniz hello değerleri belirtin: **kasa adı**, **kasası kaynak grubu**, **sertifika URL'si**ve **Sertifika parmak izi**.

### <a name="step-3-review-legal-terms-and-create"></a>3. Adım Yasal koşulları gözden geçirin ve oluşturma
Tıklatın **yasal koşulları gözden geçir** tooreview hello koşulları. Kabul ediyorsa **satın alma**ve ardından **oluşturma** toostart hello dağıtım.

## <a name="connect-toohello-cluster"></a>Toohello kümesine bağlanın
1. Merhaba HPC paketi küme dağıtıldıktan sonra toohello Git [Azure portal](https://portal.azure.com). Tıklatın **kaynak grupları**ve hangi hello küme dağıtılan Bul hello kaynak grubu. Baş düğüm sanal makineleri hello bulabilirsiniz.

    ![Küme baş düğümler hello portalında](./media/hpcpack-2016-cluster/clusterhns.png)

2. Bir baş düğümüne tıklayın (yüksek oranda kullanılabilirlik kümesi içinde herhangi bir hello baş düğüme tıklayın). İçinde **Essentials**, hello genel IP adresi veya tam DNS adı hello kümesinin bulabilirsiniz.

    ![Küme bağlantısı ayarları](./media/hpcpack-2016-cluster/clusterconnect.png)

3. Tıklatın **Bağlan** toolog tooany belirtilen yönetici kullanıcı adınız ile Uzak Masaüstü kullanarak hello baş düğüm üzerinde. Dağıttığınız hello küme bir Active Directory etki alanında hello kullanıcı adı hello biçiminde ise, <privateDomainName> \<adminUsername > (örneğin, hpc.local\hpcadmin).

## <a name="next-steps"></a>Sonraki adımlar
* İşlerini tooyour küme gönderin. Bkz: [işleri tooHPC Azure HPC Pack kümede gönderme](hpcpack-cluster-submit-jobs.md) ve [Azure Active Directory'yi kullanarak azure'da bir HPC Pack 2016 kümeyi yönetmek](hpcpack-cluster-active-directory.md).

