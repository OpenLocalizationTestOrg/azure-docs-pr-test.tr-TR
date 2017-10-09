---
title: "Azure Automation farklı çalıştır hesabı PowerShell ile aaaCreate | Microsoft Docs"
description: "Bu makalede nasıl hello portalından ilk oluşturulurken bu adım gerçekleştirmediyseniz, tooupgrade Otomasyon hesabınızla PowerShell toocreate hello farklı çalıştır hesapları açıklanmaktadır."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1049601321d2bc1e5f9d982f622788f8e4e4d797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a>PowerShell kullanarak Otomasyon Farklı Çalıştır hesabını güncelleştirme
Varsa, PowerShell tooupdate var olan Otomasyon hesabınızı kullanabilirsiniz:

* Automation hesabı oluşturma ancak toocreate hello farklı çalıştır hesabı reddedin.
* Runbook kimlik doğrulaması için tooupdate hello tooinclude hello farklı çalıştır hesabı istediğiniz ve zaten bir Automation hesabı toomanage Resource Manager kaynakları kullanın.
* Zaten bir Automation hesabı toomanage Klasik kaynakları kullanır ve tooupdate isterseniz bunu toouse hello yeni bir hesap oluşturma ve runbook'ları ve varlıkları tooit geçirmek yerine Klasik farklı çalıştır hesabı.   
* Kuruluş sertifika yetkilisi (CA) tarafından verilen bir sertifikayı kullanarak toocreate bir farklı çalıştır ve klasik farklı çalıştır hesabı istiyor.

## <a name="prerequisites"></a>Ön koşullar

* Hello betik yalnızca Windows 10 ve Windows Server 2016 ile Azure Resource Manager modüllerini 2.01 ve daha sonra çalıştırılabilir. Windows'un önceki sürümleri desteklenmez.
* Azure PowerShell 1.0 ve üzeri. Hello PowerShell 1.0 sürümü hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
* Merhaba hello değeri olarak başvurulan bir Otomasyon hesabı *– AutomationAccountName* ve *- ApplicationDisplayName* hello PowerShell Betiği aşağıdaki parametreleri.

tooget hello değerleri *Subscriptionıd*, *ResourceGroup*, ve *AutomationAccountName*hello komut dosyaları için gerekli parametreler olan, aşağıdaki hello:
1. İçinde Azure portal Merhaba, Automation hesabınızı hello üzerinde seçin **Otomasyon hesabı** dikey ve ardından **tüm ayarları**. 
2. Merhaba üzerinde **tüm ayarları** dikey altında **hesap ayarlarını**seçin **özellikleri**. 
3. Not hello hello değerlerine **özellikleri** dikey.

![Merhaba Otomasyon hesabı "Özellikler" dikey](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a>Farklı Çalıştır Hesabı PowerShell komut dosyası oluşturma
Bu PowerShell Betiği yapılandırmaları aşağıdaki hello destekler:

* Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturun.
* Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.
* Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.
* Hello Azure Bulutu kendinden imzalı bir sertifika kullanarak bir farklı çalıştır hesabı ve klasik farklı çalıştır hesabı oluşturun.

Seçtiğiniz hello yapılandırma seçeneğine bağlı olarak aşağıdaki öğelerindeki hello hello komut dosyası oluşturur.

**Farklı Çalıştır hesapları için:**

* Bir Azure oluşturduğu AD uygulama toobe verilen kendinden imzalı ya da hello ile veya Kurumsal Sertifika genel anahtarı, Azure AD'de Merhaba uygulaması için bir hizmet sorumlusu hesabı oluşturur ve hello mevcut hello hesap için katılımcı rolü atar aboneliği. Bu ayar tooOwner veya başka bir rolle değiştirebilirsiniz. Daha fazla bilgi için bkz. [Azure Otomasyonu’nda rol tabanlı erişim denetimi](automation-role-based-access-control.md).
* Adlı bir Otomasyon sertifikası varlığı oluşturur *AzureRunAsCertificate* hello Otomasyon hesabı belirtilmedi. Merhaba sertifika varlığı hello Azure AD uygulama tarafından kullanılan hello sertifika özel anahtarı içerir.
* Adlı bir Otomasyon bağlantı varlığı oluşturur *AzureRunAsConnection* hello Otomasyon hesabı belirtilmedi. Merhaba bağlantı varlığı hello ApplicationId, Tenantıd, Subscriptionıd ve sertifika parmak izi tutar.

**Klasik Farklı Çalıştır hesapları için:**

* Adlı bir Otomasyon sertifikası varlığı oluşturur *AzureClassicRunAsCertificate* hello Otomasyon hesabı belirtilmedi. Merhaba sertifika varlığı hello yönetim sertifikası tarafından kullanılan hello sertifika özel anahtarı içerir.
* Adlı bir Otomasyon bağlantı varlığı oluşturur *AzureClassicRunAsConnection* hello Otomasyon hesabı belirtilmedi. Merhaba bağlantı varlığı hello abonelik adı, Subscriptionıd ve sertifika varlık adı tutar.

>[!NOTE]
> Merhaba betik yürütüldükten sonra Klasik farklı çalıştır hesabı oluşturmak için her iki seçeneği seçerseniz, karşıya yükleme hello ortak sertifika (.cer dosya adı uzantısı) toohello yönetim deposu hello abonelik için bu hello Otomasyon hesabı içinde oluşturuldu.
> 

1. Komut dosyası, bilgisayarınızda aşağıdaki hello kaydedin. İsteğe bağlı olarak bu örnekte, hello dosya adıyla kaydedin *yeni RunAsAccount.ps1*.

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. Bilgisayarınızda Başlat **Windows PowerShell** hello gelen **Başlat** yükseltilmiş kullanıcı haklarıyla ekran.
3. Hello komut satırı kabuğundan, 1. adımda oluşturduğunuz hello betik içeren gidin toohello klasörü yükseltilmiş.  
4. İçin gerek duyduğunuz hello yapılandırma hello parametre değerlerini kullanarak Hello betiğini yürütün.

    **Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturma**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Hello Azure Bulutu kendinden imzalı bir sertifika kullanarak bir farklı çalıştır hesabı ve klasik farklı çalıştır hesabı oluşturma**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Merhaba betiği yürüttükten sonra Azure ile istendiğinde tooauthenticate olacaktır. Merhaba abonelik Yöneticileri rolünün üyesi ve hello aboneliğinin ortak yöneticisi olan bir hesapla oturum açın.
    >
    >

Merhaba betiği başarıyla yürütüldü sonra hello aşağıdakileri göz önünde bulundurun:
* Otomatik olarak imzalanan bir PKI sertifikası (.cer dosyası) ile bir Klasik farklı çalıştır hesabını oluşturduysanız, hello komut dosyası oluşturur ve bilgisayarınızda hello kullanıcı profili altındaki toohello geçici dosyalar klasörüne kaydeder *%USERPROFILE%\AppData\Local\Temp*, tooexecute hello PowerShell oturumu kullanılan.
* Kurumsal ortak sertifika (.cer file) ile bir Klasik Farklı Çalıştır hesabı oluşturduysanız bu sertifikayı kullanın. Merhaba yönergeleri izleyin [yönetim API sertifikası toohello Klasik Azure portalı karşıya](../azure-api-management-certs.md)ve ardından hello kullanarak Klasik dağıtım kaynaklarla hello kimlik bilgisi yapılandırmasını doğrulamak [örnek kod Azure Klasik dağıtım kaynaklarla tooauthenticate](automation-verify-runas-authentication.md#classic-run-as-authentication). 
* Kaldırdıysanız *değil* Klasik farklı çalıştır hesabı oluşturma, Resource Manager kaynaklarıyla kimlik doğrulaması ve hello kullanarak hello kimlik bilgisi yapılandırmasını doğrulamak [örnek Hizmet Yönetimi ile kimlik doğrulaması için kod Kaynakları](automation-verify-runas-authentication.md#automation-run-as-authentication).

## <a name="next-steps"></a>Sonraki adımlar
* Hizmet sorumluları hakkında daha fazla bilgi için çok başvuran[uygulama ve hizmet sorumlusu nesneleri](../active-directory/active-directory-application-objects.md).
* Sertifikalar ve Azure hizmetleri hakkında daha fazla bilgi için çok başvuran[Azure Cloud Services sertifikalarına genel bakış](../cloud-services/cloud-services-certs-create.md).
