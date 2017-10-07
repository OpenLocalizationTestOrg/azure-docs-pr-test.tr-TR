---
title: "aaaCreate Azure Service Fabric kümesi bir şablondan | Microsoft Docs"
description: "Bu makalede nasıl güvenli bir Service Fabric yukarı tooset küme Azure'da Azure Resource Manager, Azure anahtar kasası ve Azure Active Directory (Azure AD) istemci kimlik doğrulaması için kullanarak açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a>Azure Kaynak Yöneticisi'ni kullanarak bir Service Fabric kümesi oluştur
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Azure portal](service-fabric-cluster-creation-via-portal.md)
>
>

Bu adım adım kılavuz, Azure Kaynak Yöneticisi'ni kullanarak azure'da güvenli bir Azure Service Fabric kümesi ayarlama aracılığıyla açıklanmaktadır. Merhaba makaleyi uzun bildiremedi. Bununla birlikte, hello içerikle baştan sona bilginiz sürece her adım dikkatle emin toofollow olması.

Merhaba kılavuz yordamları izleyerek hello kapsar:

* Küme ve uygulama güvenliği için bir Azure anahtar kasası tooupload sertifikalar ayarlama
* Azure Resource Manager kullanarak Azure'da güvenli küme oluşturma
* Kullanıcıların Azure Active Directory (Azure AD) kullanarak küme yönetimi için kimlik doğrulaması

Güvenli bir küme yetkisiz erişim toomanagement işlemleri engelleyen bir kümedir. Bu, dağıtma, yükseltme ve silme uygulamaları, hizmetleri ve içerdikleri hello verilerini içerir. Güvenli olmayan bir küme herkes tooat dilediğiniz zaman bağlanmak ve böylelikle yönetim işlemlerini gerçekleştirmek bir kümedir. Olası toocreate güvenli olmayan bir küme olmasına rağmen hello outset güvenli bir küme oluşturmak önerilir. Güvenli olmayan bir küme daha sonra korunamıyor olduğundan, yeni bir küme oluşturulması gerekir.

oluşturulurken güvenli küme Hello kavramı olan hello aynı, Linux veya Windows kümesi olup. Güvenli Linux kümeleri oluşturmak için daha fazla bilgi ve yardımcı komut dosyası için bkz: [Linux'ta güvenli küme oluşturma](#secure-linux-clusters).

## <a name="sign-in-tooyour-azure-account"></a>Azure hesabı tooyour içinde oturum
Bu kılavuzu kullanır [Azure PowerShell][azure-powershell]. Yeni bir PowerShell oturumu başlattığınızda tooyour Azure hesabı oturum ve Azure komutları çalıştırmadan önce aboneliğinizi seçin.

Azure hesabı tooyour oturum:

```powershell
Login-AzureRmAccount
```

Aboneliğinizi seçin:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a>Bir anahtar kasasını oluşturup
Bu bölümde, Service Fabric uygulamaları ve Azure Service Fabric kümesi için bir anahtar kasası oluşturma açıklanmaktadır. Tam Kılavuzu tooAzure anahtar kasası, toohello başvuran [anahtar kasası kullanmaya başlama Kılavuzu][key-vault-get-started].

Service Fabric X.509 sertifikaları toosecure bir küme kullanır ve uygulama güvenlik özellikleri sağlar. Azure Service Fabric kümeleri için anahtar kasası toomanage sertifikaları kullanın. Bir küme Azure'da dağıtıldığında, Service Fabric kümeleri oluşturmaktan sorumlu hello Azure kaynak sağlayıcısı sertifikaları anahtar Kasası'nı çeker ve VM'ler hello kümede yükler.

Merhaba Aşağıdaki diyagramda hello Azure anahtar kasası, Service Fabric kümesi ve küme oluşturduğunda, bir anahtar kasasında depolanan sertifika kullanan hello Azure kaynak sağlayıcısı arasındaki ilişki gösterilmektedir:

![Sertifika Yükleme diyagramı][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
Merhaba ilk adımı toocreate özellikle anahtar kasanız için bir kaynak grubu oluşturur. Kendi kaynak grubuna hello anahtar kasası koymak öneririz. Bu eylem, Service Fabric kümesi anahtarları ve gizli anahtarları kaybetmeden içeren hello kaynak grubunu da dahil olmak üzere hello işlem ve depolama kaynak grupları, kaldırmanıza olanak sağlar. anahtar kasanızı içeren hello kaynak grubunu _hello olmalıdır aynı bölgede_ tarafından kullanıldığı hello kümesi olarak.

Birden çok bölgeye toodeploy kümelerde planlıyorsanız, hello kaynak grubu ve ait hangi bölgede gösterir şekilde hello anahtar kasası adı öneririz.  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
Merhaba çıktı aşağıdaki gibi görünmelidir:

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a>Merhaba yeni kaynak grubunda bir anahtar kasası oluşturma
Merhaba anahtar kasası _dağıtımı için etkinleştirilmelidir_ tooallow işlem kaynak sağlayıcısı tooget sertifikaları dışarı hello ve sanal makine örnekleri yükleyin:

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

Merhaba çıktı aşağıdaki gibi görünmelidir:

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a>Var olan bir anahtar kasası kullanın

toouse var olan bir anahtar kasası, _dağıtımı için etkinleştirmeniz gerekir_ tooallow işlem kaynak sağlayıcısı tooget sertifikaları dışarı hello ve küme düğümlerine yükleyin:

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a>Sertifikaları tooyour anahtar kasası ekleme

Sertifikaları Service Fabric tooprovide kimlik doğrulama ve şifreleme toosecure içinde kullanılan bir küme ve kendi uygulamalarına çeşitli yönlerini. Service Fabric sertifikaların nasıl kullanıldığını daha fazla bilgi için bkz: [Service Fabric kümesi güvenlik senaryoları][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Küme ve sunucu sertifikası (gerekli)
Bu sertifika, gerekli toosecure bir kümedir ve yetkisiz erişim tooit engelleyebilirsiniz. İki yolla küme güvenlik sağlar:

* Küme kimlik doğrulaması: düğümü düğümü iletişimin küme Federasyon kimlik doğrulamasını yapar. Yalnızca bu sertifikayla kimliğini kanıtlamak düğümleri hello kümeye katılabilir.
* Sunucu kimlik doğrulaması: hello management istemcisi, toohello gerçek küme Konuşmayı bilir böylece hello küme yönetim uç noktaları tooa yönetim istemci kimliğini doğrular. Bu sertifika aynı zamanda bir SSL hello HTTPS yönetim API'si ve Service Fabric Explorer için HTTPS üzerinden sağlar.

tooserve bu amacıyla, hello sertifika hello aşağıdaki gereksinimleri karşılamalıdır:

* Merhaba sertifika özel anahtar içermelidir.
* Merhaba sertifika verilebilir tooa kişisel bilgi değişimi (.pfx) dosyası olan anahtar değişimi için oluşturulmuş olması gerekir.
* Merhaba sertifikanın konu adı tooaccess hello Service Fabric kümesi kullanın hello etki alanı eşleşmesi gerekir. Bu eşleştirme, gerekli tooprovide hello kümenin HTTPS yönetim uç noktaları için bir SSL ve Service Fabric Explorer değildir. Hello için bir sertifika yetkilisinden (CA) bir SSL sertifikası alınamıyor. cloudapp.azure.com etki alanı. Özel etki alanı adı, kümeniz için edinmeniz gerekir. Bir CA'dan bir sertifika isteme, hello sertifikanın konu adı, kümeniz için kullandığınız hello özel etki alanı adı eşleşmelidir.

### <a name="application-certificates-optional"></a>Uygulama sertifikaları (isteğe bağlı)
Ek sertifikaların herhangi bir sayıda uygulama güvenlik amacıyla bir kümede yüklenebilir. Kümenizi oluşturmadan önce hello düğümlerinde gibi yüklü bir sertifika toobe gerektiren hello güvenlik senaryolarını göz önünde bulundurun:

* Şifreleme ve şifre çözme uygulama yapılandırma değerlerini.
* Çoğaltma sırasında şifreleme düğümler arasında veri.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Azure kaynak sağlayıcısı kullanmak için sertifikaları biçimlendirme
Ekleme ve özel anahtar dosyaları (.pfx) doğrudan aracılığıyla anahtar kasanızı kullanın. Ancak, özel bir JavaScript nesne gösterimi (JSON) biçiminde depolanan anahtarları toobe hello Azure işlem kaynak sağlayıcısı gerektirir. Merhaba biçiminde hello .pfx dosyası olarak bir base 64 kodlu bir dize ve hello özel anahtar parolası içerir. Bu gereksinimler, anahtarları bir JSON dizesinde yerleştirilir ve başlangıç anahtarı "gizli" olarak depolanan hello tooaccommodate Kasa.

Bu işlem daha kolay toomake bir [PowerShell modülüdür Github'da bulunan][service-fabric-rp-helpers]. toouse hello Modülü aşağıdaki hello:

1. Merhaba depodaki tüm içeriğini Hello bir yerel dizine indirin.
2. Toohello yerel dizinine gidin.
2. PowerShell penceresinde Hello ServiceFabricRPHelpers modülünü içeri aktarın:

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

Merhaba `Invoke-AddCertToKeyVault` bu PowerShell modülünü komutu otomatik olarak bir sertifika özel anahtarı bir JSON dizeye biçimlendirir ve toohello anahtar kasası yükler. Merhaba komutu tooadd hello küme sertifika ve tüm ek uygulama sertifikaları toohello anahtar kasası kullanın. Kümenizdeki tooinstall istediğiniz ek sertifika için bu adımı yineleyin.

#### <a name="uploading-an-existing-certificate"></a>Varolan bir sertifikayı karşıya yükleme

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

Merhaba bir burada gösterildiği gibi bir hata alırsanız, genellikle kaynak URL çakışması olduğu anlamına gelir. tooresolve hello çakışması, değişiklik hello anahtar kasasının adı.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Merhaba çakışması çözümlendikten sonra hello çıktı aşağıdaki gibi görünmelidir:

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
>Uygulama güvenliği için kullanıyor olabilecek herhangi bir uygulama sertifika hello üç önceki dizeleri CertificateThumbprint, SourceVault ve CertificateURL, güvenli Service Fabric kümesi ve tooobtain tooset gerekir. Merhaba dizeleri kaydetmezseniz, daha sonra bunları hello anahtar sorgulamak kasa zor tooretrieve olabilir.

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a>Otomatik olarak imzalanan sertifika oluşturma ve toohello anahtar kasası karşıya yükleme

Sertifikaları toohello anahtar kasanız zaten karşıya yüklediyseniz, bu adımı atlayın. Bu adım, yeni bir otomatik olarak imzalanan sertifika oluşturma ve tooyour anahtar kasası karşıya içindir. Komut dosyası izleyen hello hello parametreleri değiştirin ve ardından çalıştırdıktan sonra sertifika parola sorulur.  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

Merhaba bir burada gösterildiği gibi bir hata alırsanız, genellikle kaynak URL çakışması olduğu anlamına gelir. tooresolve hello çakışma, değişiklik hello anahtar kasası adı, RG adı ve benzeri.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Merhaba çakışması çözümlendikten sonra hello çıktı aşağıdaki gibi görünmelidir:

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
>Uygulama güvenliği için kullanıyor olabilecek herhangi bir uygulama sertifika hello üç önceki dizeleri CertificateThumbprint, SourceVault ve CertificateURL, güvenli Service Fabric kümesi ve tooobtain tooset gerekir. Merhaba dizeleri kaydetmezseniz, daha sonra bunları hello anahtar sorgulamak kasa zor tooretrieve olabilir.

 Bu noktada, yerinde öğeleri aşağıdaki hello olmalıdır:

* Merhaba anahtar kasası kaynak grubu.
* anahtar kasası ve URL'sini (PowerShell çıkış önceki hello SourceVault olarak adlandırılır) hello.
* Merhaba küme sunucu kimlik doğrulama sertifikası ve URL'sini hello anahtar Kasası'nda.
* Merhaba uygulama sertifikaları ve bunların URL'lerini hello anahtar Kasası'nda.


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a>İstemci kimlik doğrulaması için Azure Active Directory'yi ayarlama ayarlayın

Azure AD kuruluş (kiracılar olarak bilinir) toomanage kullanıcı erişimi tooapplications sağlar. Uygulamaları web tabanlı olanlar oturum açma kullanıcı Arabirimi ve yerel istemci deneyimini olanlar ayrılır. Bu makalede, bir kiracı zaten oluşturduğunuzu varsayalım. Yüklemediyseniz, okuyarak başlamanız [nasıl tooget bir Azure Active Directory Kiracı][active-directory-howto-tenant].

Service Fabric kümesi birkaç giriş noktaları tooits hello web tabanlı dahil olmak üzere Yönetim işlevselliği sunar [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] ve [Visual Studio] [service-fabric-manage-application-in-visual-studio]. Sonuç olarak, iki Azure AD uygulamaları toocontrol erişim toohello kümesi, bir web uygulaması ve bir yerel uygulama oluşturun.

Azure AD ile bir Service Fabric kümesi yapılandırılırken bazı hello adımlarını söz konusu toosimplify, Windows PowerShell komut kümesini oluşturduk.

> [!NOTE]
> Merhaba hello küme oluşturmadan önce aşağıdaki adımları tamamlamanız gerekir. Küme adları ve uç noktaları Hello betikleri beklediğiniz çünkü hello değerler planlanması gerekir ve, önceden oluşturduğunuz değerleri değil.

1. [Merhaba komut dosyalarını indirme] [ sf-aad-ps-script-download] tooyour bilgisayar.
2. Sağ hello zip dosyası, select **özellikleri**seçin hello **Engellemeyi Kaldır** onay kutusunu işaretleyin ve ardından **Uygula**.
3. Merhaba zip dosyasını ayıklayın.
4. Çalıştırma `SetupApplications.ps1`ve hello Tenantıd, ClusterName ve WebApplicationReplyUrl parametre olarak sağlayın. Örneğin:

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    Merhaba PowerShell komutunu yürüterek, Tenantıd bulabilirsiniz `Get-AzureSubscription`. Bu komutu yürütmek hello Tenantıd her abonelik için görüntüler.

    ClusterName hello komut dosyası tarafından oluşturulan kullanılan tooprefix hello Azure AD uygulamaları ' dir. Bunun toomatch hello gerçek küme adı tam olarak gerekli değildir. Hedeflenen yalnızca toomake olduğundan, bunlar ile kullanılan daha kolay toomap Azure AD yapıları toohello Service Fabric kümesi.

    WebApplicationReplyUrl oturum açma işlemini tamamladıktan sonra tooyour kullanıcıları Azure AD döndüren hello varsayılan uç noktadır. Bu uç nokta olan varsayılan olarak, kümeniz için hello Service Fabric Explorer bitiş noktası olarak ayarlayın:

    https://&lt;cluster_domain&gt;: 19080/Explorer

    İstendiğinde toosign tooan hesabındaki hello Azure AD kiracısı için yönetici ayrıcalıklarına sahip olduğunuz. Oturum açtıktan sonra hello betiği hello web ve yerel uygulamalar toorepresent Service Fabric kümesi oluşturur. Merhaba hello kiracının uygulamaları gözden geçirmeniz [Klasik Azure portalı][azure-classic-portal], iki yeni giriş görmeniz gerekir:

   * *ClusterName*\_küme
   * *ClusterName*\_istemci

   Merhaba betik bir fikir tookeep hello PowerShell penceresi olacak şekilde hello sonraki bölümde hello Küme oluşturduğunuzda hello Azure Resource Manager şablonu için gerekli JSON açmak hello yazdırır.

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a>Service Fabric kümesi Resource Manager şablonu oluşturma
Bu bölümde, hello Merhaba önceki bir Service Fabric kümesi Resource Manager şablonunda kullanılan PowerShell komutları çıkarır.

Örnek Resource Manager şablonları hello kullanılabilir [github'da Azure hızlı başlangıç Şablon Galerisi][azure-quickstart-templates]. Bu şablonlar, küme şablonunuz için bir başlangıç noktası olarak kullanılabilir.

### <a name="create-hello-resource-manager-template"></a>Merhaba Resource Manager şablonu oluşturma
Bu kılavuzu hello kullanır [5-node güvenli küme] [ service-fabric-secure-cluster-5-node-1-nodetype] örnek şablonu ve şablon parametreleri. Karşıdan `azuredeploy.json` ve `azuredeploy.parameters.json` tooyour bilgisayar ve her iki dosyalarını sık kullandığınız metin düzenleyicisinde açın.

### <a name="add-certificates"></a>Sertifikaları Ekle
Merhaba sertifika anahtarları içeren anahtar kasası hello başvurarak sertifikaları tooa küme Resource Manager şablonu ekleyin. Bir Resource Manager şablonu parametreleri dosyasında hello anahtar kasası değerleri koyun öneririz. Bunun yapılması hello Resource Manager şablon dosyası yeniden kullanılabilir ve boş değerler belirli tooa dağıtımının tutar.

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a>OsProfile tüm sertifikaları toohello sanal makine ölçek kümesi ekleme
Merhaba kümede yüklü her sertifikanın hello osProfile bölümünde hello ölçek kümesi kaynağı (Microsoft.Compute/virtualMachineScaleSets) yapılandırılması gerekir. Bu eylemin hello kaynak sağlayıcısı tooinstall hello sertifika hello VM'ler bildirir. Bu yükleme hello küme sertifika ve herhangi bir uygulama güvenlik sertifika toouse uygulamalarınız için planlama içerir:

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a>Merhaba Service Fabric kümesi sertifika yapılandırma
Merhaba küme kimlik doğrulama sertifikası her iki hello Service Fabric küme kaynağı (Microsoft.ServiceFabric/clusters) olarak yapılandırılmalıdır ve hello sanal makine ölçek için Service Fabric uzantısı hello sanal makine ölçek kümesi kaynağı ayarlar. Bu düzenlemenin hello Service Fabric kaynak sağlayıcısı tooconfigure sağlar, küme kimlik doğrulaması ve yönetim uç noktaları için sunucu kimlik doğrulaması için kullanılacak.

##### <a name="virtual-machine-scale-set-resource"></a>Kaynak sanal makine ölçek kümesi:
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a>Service Fabric kaynak:
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a>Azure AD Yapılandırması Ekle
daha önce oluşturduğunuz hello Azure AD yapılandırma doğrudan Resource Manager şablonuna eklenebilir. Ancak, önce bir parametre dosyası tookeep hello Resource Manager şablonu yeniden kullanılabilir hello değerleri ayıklamak ve değerleri belirli tooa dağıtımını boş önerilir.

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### < bir "yapılandırma-arm" ></a>yapılandırma Resource Manager şablonu parametreleri
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
Son olarak, hello çıkış değerler hello anahtar kasası ve Azure AD PowerShell komutları toopopulate hello parametreler dosyası kullanın:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
Bu noktada, yerinde öğeleri aşağıdaki hello olmalıdır:

* Anahtar kasası kaynak grubu
  * Key Vault
  * Küme sunucu kimlik doğrulama sertifikası
  * Veri şifreleme sertifikası
* Azure Active Directory kiracısı
  * Web tabanlı yönetim ve Service Fabric Explorer için Azure AD uygulaması
  * Yerel istemci yönetimi için Azure AD uygulaması
  * Kullanıcılar ve onların atanan roller
* Service Fabric kümesi Resource Manager şablonu
  * Anahtar kasası ile yapılandırılan sertifikaları
  * Yapılandırılmış Azure Active Directory

Aşağıdaki diyagramda hello anahtar kasası ve Azure AD yapılandırma Resource Manager şablonunuza nerelerde gösterilmektedir.

![Resource Manager bağımlılık Haritası][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a>Merhaba kümesi oluşturma
Şimdi kullanarak hazır toocreate hello küme olan [Azure kaynak şablon dağıtımı][resource-group-template-deploy].

#### <a name="test-it"></a>test
PowerShell komut tootest aşağıdaki hello Resource Manager şablonu ile bir parametre dosyası kullanın:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a>dağıtın
Hello Resource Manager şablonu testi başarılı olursa, aşağıdaki PowerShell komut toodeploy hello Resource Manager şablonu ile bir parametre dosyası kullanın:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a>Kullanıcıların tooroles atayın
Merhaba uygulamaları toorepresent kümenizi oluşturduktan sonra kullanıcılarınızın Service Fabric tarafından desteklenen toohello rolleri ata: salt okunur ve yönetici Hello kullanarak hello roller atayabilirsiniz [Klasik Azure portalı][azure-classic-portal].

1. Hello Azure portal, tooyour Kiracı gidin ve ardından **uygulamaları**.
2. Bir ada sahip hello web uygulaması seçin gibi `myTestCluster_Cluster`.
3. Merhaba tıklatın **kullanıcılar** sekmesi.
4. Bir kullanıcı tooassign seçin ve hello ardından **atamak** hello ekranın hello düğmesini.

    ![Kullanıcıların tooroles düğmesi atama][assign-users-to-roles-button]
5. Merhaba rol tooassign toohello kullanıcıyı seçin.

    !["Kullanıcılar atama" iletişim kutusu][assign-users-to-roles-dialog]

> [!NOTE]
> Service Fabric rolleri hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi](service-fabric-cluster-security-roles.md).
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a>Linux'ta güvenli küme oluşturma
toomake hello işlemini daha kolay, biz olması koşuluyla bir [yardımcı betik](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux). Bu yardımcı betik kullanmadan önce Azure komut satırı yüklü arabirimi (CLI) zaten var ve yolunuzda olduğundan emin olun. Merhaba komut dosyası çalıştırarak izinleri tooexecute olduğundan emin olun `chmod +x cert_helper.py` karşıdan sonra. Merhaba ilk adımdır tooyour Azure hesabı toosign ile Merhaba CLI kullanarak `azure login` komutu. Tooyour Azure hesabı oturum sonra hello yardımcı komut dosyası kullan CA'nız ile komut gösterir aşağıdaki hello sertifika, oturum:

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

Merhaba - ifile parametresi hello sertifika türü (pfx veya pem ya da kendinden imzalı bir sertifika varsa ss) ile giriş olarak bir .pfx dosyasına ya da .pem dosyasını alabilir.
Merhaba parametre -h hello Yardım metni yazdırır.


Bu komut, üç dizeleri hello çıkış olarak aşağıdaki hello döndürür:

* Merhaba hello kimliği SourceVaultID yeni KeyVault sizin için oluşturulan kaynak grubu
* Merhaba sertifika erişmek için CertificateUrl
* Kimlik doğrulaması için kullanılan CertificateThumbprint

Aşağıdaki örnek hello nasıl toouse hello komutu gösterir:

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
Üç dizeler gibi hello komut verir önceki hello yürütülüyor:

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

Merhaba sertifikanın konu adı tooaccess hello Service Fabric kümesi kullanın hello etki alanı eşleşmesi gerekir. Gerekli tooprovide hello kümenin HTTPS yönetim uç noktaları için bir SSL ve Service Fabric Explorer eşleşmedir. Hello için bir CA'dan bir SSL sertifikası elde edemiyor `.cloudapp.azure.com` etki alanı. Özel etki alanı adı, kümeniz için edinmeniz gerekir. Bir CA'dan bir sertifika isteme, hello sertifikanın konu adı, kümeniz için kullandığınız hello özel etki alanı adı eşleşmelidir.

Bu konu adları toocreate (olmadan Azure AD), güvenli bir Service Fabric kümesi ihtiyacınız hello konusunda açıklandığı gibi girişler [yapılandırma Resource Manager şablonu parametreleri](#configure-arm). Merhaba yönergeleri izleyerek toohello güvenli küme bağlanabilir [istemci erişim tooa küme kimlik doğrulaması](service-fabric-connect-to-secure-cluster.md). Linux Önizleme kümeleri, Azure AD kimlik doğrulamasını desteklemez. Hello açıklandığı gibi yönetici ve istemci roller atayabilirsiniz [atamak rolleri toousers](#assign-roles) bölümü. Linux Önizleme küme için yönetici ve istemci rolleri belirlemek için kimlik doğrulaması için tooprovide sertifika parmak izleri vardır. (Hiçbir zincir doğrulama veya iptal Bu önizleme sürümünde gerçekleştirilmekte olduğundan, hello konu adı, sağlamaz.)

Test etmek için toouse otomatik olarak imzalanan bir sertifika istiyorsanız kullanabileceğiniz hello aynı komut dosyasını toogenerate biri. Merhaba bayrağı sağlayarak hello sertifika tooyour anahtar kasası sonra yükleyebilirsiniz `ss` sağlayan hello sertifika yolu ve sertifika adı yerine. Örneğin, oluşturma ve otomatik olarak imzalanan bir sertifika karşıya yükleme için komutu aşağıdaki hello bakın:

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
Bu komut döndürür hello aynı üç dizeleri: SourceVault, CertificateUrl ve CertificateThumbprint. Merhaba dizeleri toocreate daha sonra güvenli bir Linux kümesi ve hello otomatik olarak imzalanan sertifika yerleştirildiği konum da kullanabilirsiniz. Merhaba otomatik olarak imzalanan sertifika tooconnect toohello küme gerekir. Merhaba yönergeleri izleyerek toohello güvenli küme bağlanabilir [istemci erişim tooa küme kimlik doğrulaması](service-fabric-connect-to-secure-cluster.md).

Merhaba sertifikanın konu adı tooaccess hello Service Fabric kümesi kullanın hello etki alanı eşleşmesi gerekir. Gerekli tooprovide hello kümenin HTTPS yönetim uç noktaları için bir SSL ve Service Fabric Explorer eşleşmedir. Hello için bir CA'dan bir SSL sertifikası elde edemiyor `.cloudapp.azure.com` etki alanı. Özel etki alanı adı, kümeniz için edinmeniz gerekir. Bir CA'dan bir sertifika isteme, hello sertifikanın konu adı, kümeniz için kullandığınız hello özel etki alanı adı eşleşmelidir.

Hello açıklandığı gibi hello Yardımcısı hello Azure portal, kodda hello parametrelerinden doldurabilir [hello Azure portal bir küme oluşturmak](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) bölümü.

## <a name="next-steps"></a>Sonraki adımlar
Bu noktada, Azure Active Directory sağlayan yönetim kimlik doğrulama ile güvenli bir küme var. Ardından, [tooyour kümesine bağlanın](service-fabric-connect-to-secure-cluster.md) ve nasıl çok öğrenin[uygulama parolaları yönetme](service-fabric-application-secret-management.md).

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a>İstemci kimlik doğrulaması için Azure Active Directory ayarlayan sorun giderme
İstemci kimlik doğrulaması için Azure AD ayarlarken bir sorunu yaşayıp çalıştırırsanız, bu bölümdeki hello olası çözümleri gözden geçirin.

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a>Service Fabric Explorer sertifika tooselect ister
#### <a name="problem"></a>Sorun
Oturum açma başarılı bir şekilde tooAzure AD Service Fabric Explorer'da sonra hello tarayıcı toohello giriş sayfasını döndürür ancak bir sertifika tooselect isteyen bir ileti alırsınız.

![SFX select sertifika iletişim kutusu][sfx-select-certificate-dialog]

#### <a name="reason"></a>Neden
Merhaba kullanıcı hello Azure AD küme uygulaması bir rolü atanmamış. Bu nedenle, Service Fabric kümesi üzerinde Azure AD kimlik doğrulaması başarısız olur. Service Fabric Explorer toocertificate kimlik doğrulama geri döner.

#### <a name="solution"></a>Çözüm
Azure AD ayarlamak için hello yönergeleri izleyin ve kullanıcı rolleri atayın. Ayrıca, "Kullanıcı atama gerekli tooaccess uygulamayı üzerinde" Aç olarak öneririz `SetupApplications.ps1` yapar.

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a>PowerShell ile bağlantı bir hata ile başarısız olur: "Merhaba belirtilen kimlik bilgileri geçersiz"
#### <a name="problem"></a>Sorun
PowerShell tooconnect toohello küme başarıyla tooAzure AD ' oturumu sonra "AzureActiveDirectory" güvenlik modunu kullanarak kullandığınızda, hello bağlantı bir hata ile başarısız olur: "Merhaba belirtilen kimlik bilgileri geçersiz."

#### <a name="solution"></a>Çözüm
Aynı şekilde bir önceki hello hello çözümüdür.

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a>Service Fabric Explorer oturum açarken bir hata döndürür: "AADSTS50011"
#### <a name="problem"></a>Sorun
Service Fabric Explorer'da tooAzure AD toosign çalıştığınızda hata hello sayfasını döndürür: "AADSTS50011: Merhaba yanıt adresi &lt;url&gt; hello uygulama için yapılandırılan hello yanıt adresleri eşleşmiyor: &lt;GUID&gt;."

![SFX yanıt adresi eşleşmiyor][sfx-reply-address-not-match]

#### <a name="reason"></a>Neden
Azure ad tooauthenticate hello küme (web) Service Fabric Explorer temsil eden bir uygulama çalışır ve isteğe bağlı olarak hello isteğin bir parçası hello yeniden yönlendirme dönüş URL'SİYLE sağlar. Ancak hello URL hello Azure AD uygulama listelenmemiş **yanıt URL'si** listesi.

#### <a name="solution"></a>Çözüm
Merhaba üzerinde **yapılandırma** hello sekmesinde küme (web) uygulaması, hello Service Fabric Explorer URL toohello ekleme **yanıt URL'si** listelemek veya hello listesinde hello öğelerden birini değiştirin. İşiniz bittiğinde, değişikliğinizi kaydedin.

![Web uygulaması yanıtı URL'si][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a>PowerShell aracılığıyla Azure AD kimlik doğrulaması kullanarak Hello kümesine bağlanın
tooconnect hello Service Fabric kümesi, aşağıdaki PowerShell komut örneğine hello kullan:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

toolearn hello Connect-ServiceFabricCluster cmdlet'i hakkında bkz [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a>Birden çok küme hello aynı Azure AD kiracısında yeniden kullanabilir?
Evet. Ancak tooadd Merhaba Service Fabric Explorer URL tooyour küme (web) uygulaması unutmayın. Aksi takdirde, Service Fabric Explorer işe yaramaz.

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a>Azure AD etkinken neden hala bir sunucu sertifikası ihtiyacım var mı?
FabricClient ve FabricGateway karşılıklı kimlik doğrulaması gerçekleştirir. Azure AD kimlik doğrulaması sırasında bir istemci kimlik toohello sunucusunu Azure AD tümleştirme sağlar ve hello sunucu sertifikasıdır kullanılan tooverify hello sunucu kimliği. Service Fabric sertifikalar hakkında daha fazla bilgi için bkz: [X.509 sertifikalarını ve Service Fabric][x509-certificates-and-service-fabric].

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

