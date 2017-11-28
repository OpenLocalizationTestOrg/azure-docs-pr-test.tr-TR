---
title: "PowerShell ile Azure Otomasyonu Farklı Çalıştır hesabı oluşturma | Microsoft Docs"
description: "Bu makalede, portaldaki ilk oluşturma sırasında bu adımı uygulamadıysanız Farklı Çalıştır hesapları oluşturmak üzere PowerShell ile Otomasyon hesabınızı yükseltme işlemi açıklanmaktadır."
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
ms.openlocfilehash: a41a57ee3815a815c23e9bbe2dd0309e6c61c8f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="0e194-103">PowerShell kullanarak Otomasyon Farklı Çalıştır hesabını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0e194-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="0e194-104">Aşağıdaki durumlarda var olan Otomasyon hesabınızı güncelleştirmek için PowerShell kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0e194-104">You can use PowerShell to update your existing Automation account if:</span></span>

* <span data-ttu-id="0e194-105">Bir Otomasyon hesabı oluşturdunuz, ancak Farklı Çalıştır hesabı oluşturmayı reddettiniz.</span><span class="sxs-lookup"><span data-stu-id="0e194-105">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="0e194-106">Resource Manager kaynaklarını yönetmek için bir Otomasyon hesabı zaten kullanıyorsunuz ve runbook kimlik doğrulaması için Farklı Çalıştır hesabını içerecek şekilde güncelleştirmek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="0e194-106">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="0e194-107">Klasik kaynakları yönetmek için bir Otomasyon hesabı zaten kullanıyorsunuz ve yeni bir hesap oluşturup runbook’larınızı ve varlıklarınızı ona geçirmek yerine Klasik Farklı Çalıştır hesabını kullanacak şekilde güncelleştirmek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="0e194-107">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="0e194-108">Kuruluş sertifika yetkiliniz (CA) tarafından verilen bir sertifika kullanarak bir Farklı Çalıştır ve Klasik Farklı Çalıştır hesabı oluşturmak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="0e194-108">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e194-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0e194-109">Prerequisites</span></span>

* <span data-ttu-id="0e194-110">Betik yalnızca Azure Resource Manager 2.01 veya sonrasındaki modülleri içeren Windows 10 ve Windows Server 2016 işletim sistemlerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="0e194-110">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="0e194-111">Windows'un önceki sürümleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="0e194-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="0e194-112">Azure PowerShell 1.0 ve üzeri.</span><span class="sxs-lookup"><span data-stu-id="0e194-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="0e194-113">PowerShell 1.0 sürümü hakkında bilgi için bkz. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0e194-113">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="0e194-114">Aşağıdaki PowerShell betiğinde *–AutomationAccountName* ve *-ApplicationDisplayName* parametrelerinin değeri olarak başvurulan bir Otomasyon hesabı.</span><span class="sxs-lookup"><span data-stu-id="0e194-114">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="0e194-115">Betiklerin parametreleri için gerekli olan *SubscriptionID*, *ResourceGroup* ve *AutomationAccountName* değerlerini almak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="0e194-115">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span></span>
1. <span data-ttu-id="0e194-116">Azure portalında, **Otomasyon hesabı** dikey penceresinden Otomasyon hesabınızı ve ardından **Tüm ayarlar** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="0e194-116">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="0e194-117">**Tüm ayarlar** dikey penceresindeki **Hesap Ayarları** altında **Özellikler**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="0e194-117">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="0e194-118">**Özellikler** dikey penceresindeki değerleri not alın.</span><span class="sxs-lookup"><span data-stu-id="0e194-118">Note the values on the **Properties** blade.</span></span>

![Otomasyon hesabı "Özellikler" dikey penceresi](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="0e194-120">Farklı Çalıştır Hesabı PowerShell komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e194-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="0e194-121">Bu PowerShell betiği aşağıdaki yapılandırmalar için destek içerir:</span><span class="sxs-lookup"><span data-stu-id="0e194-121">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="0e194-122">Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e194-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="0e194-123">Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e194-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="0e194-124">Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e194-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="0e194-125">Azure Kamu bulutunda otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e194-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="0e194-126">Seçtiğiniz yapılandırma seçeneğine bağlı olarak, betik aşağıdaki öğeleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0e194-126">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="0e194-127">**Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="0e194-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="0e194-128">Otomatik olarak imzalanan sertifika veya kurumsal sertifika ortak anahtarıyla dışarı aktarılacak bir Azure AD uygulaması oluşturur, Azure AD’de bu uygulama için bir hizmet sorumlusu hesabı oluşturur ve geçerli aboneliğinizde hesap için Katkıda Bulunan rolünü atar.</span><span class="sxs-lookup"><span data-stu-id="0e194-128">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="0e194-129">Bu ayarı Sahip veya başka bir rolle değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e194-129">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="0e194-130">Daha fazla bilgi için bkz. [Azure Otomasyonu’nda rol tabanlı erişim denetimi](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="0e194-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="0e194-131">Belirtilen Otomasyon hesabında *AzureRunAsCertificate* adlı bir Otomasyon sertifikası varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0e194-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="0e194-132">Sertifika varlıkları, Azure AD uygulaması tarafından kullanılan sertifika özel anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0e194-132">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="0e194-133">Belirtilen Otomasyon hesabında *AzureRunAsConnection* adlı bir Otomasyon bağlantı varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0e194-133">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="0e194-134">Bağlantı varlığı applicationId, tenantId, subscriptionId ve sertifika parmak izini içerir.</span><span class="sxs-lookup"><span data-stu-id="0e194-134">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="0e194-135">**Klasik Farklı Çalıştır hesapları için:**</span><span class="sxs-lookup"><span data-stu-id="0e194-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="0e194-136">Belirtilen Otomasyon hesabında *AzureClassicRunAsCertificate* adlı bir Otomasyon sertifikası varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0e194-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="0e194-137">Sertifika varlığı, yönetim sertifikası tarafından kullanılan sertifika özel anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0e194-137">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="0e194-138">Belirtilen Otomasyon hesabında *AzureClassicRunAsConnection* adlı bir Otomasyon bağlantı varlığı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0e194-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="0e194-139">Bağlantı varlığı; abonelik adı, subscriptionId ve sertifika varlık adını içerir.</span><span class="sxs-lookup"><span data-stu-id="0e194-139">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="0e194-140">Klasik Farklı Çalıştır hesabı oluşturma seçeneğini belirlerseniz, betik yürütüldükten sonra Otomasyon hesabının oluşturulduğu abonelik için yönetim deposuna ortak sertifikayı (.cer dosya adı uzantısı) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0e194-140">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

1. <span data-ttu-id="0e194-141">Aşağıdaki betiği bilgisayarınıza kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0e194-141">Save the following script on your computer.</span></span> <span data-ttu-id="0e194-142">Bu örnekte *New-RunAsAccount.ps1* dosya adıyla kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0e194-142">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
           Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                    "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload the .cer format of #CERT#"

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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="0e194-143">Bilgisayarınızda **Windows PowerShell**’i yükseltilmiş kullanıcı haklarına sahip **Başlat** ekranından başlatın.</span><span class="sxs-lookup"><span data-stu-id="0e194-143">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="0e194-144">Yükseltilmiş komut satırı kabuğundan, 1. adımda oluşturduğunuz komut dosyasını içeren klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="0e194-144">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span></span>  
4. <span data-ttu-id="0e194-145">İstediğiniz yapılandırmanın parametre değerlerini kullanarak betiği yürütün.</span><span class="sxs-lookup"><span data-stu-id="0e194-145">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="0e194-146">**Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="0e194-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="0e194-147">**Otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="0e194-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="0e194-148">**Kurumsal sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="0e194-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="0e194-149">**Azure Kamu bulutunda otomatik olarak imzalanan sertifika kullanarak Farklı Çalıştır hesabı ve Klasik Farklı Çalıştır hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="0e194-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="0e194-150">Betik yürütüldükten sonra Azure kimlik doğrulamasını yapmanız istenecektir.</span><span class="sxs-lookup"><span data-stu-id="0e194-150">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="0e194-151">Aboneliğin yöneticiler rolünün üyesi ve aboneliğin ortak yöneticisi olan bir hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0e194-151">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="0e194-152">Betik başarıyla yürütüldükten sonra aşağıdakilere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="0e194-152">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="0e194-153">Otomatik olarak imzalanan bir ortak sertifika (.cer dosyası) ile Klasik Farklı Çalıştır hesabı oluşturduysanız, betik bu hesabı oluşturup bilgisayarınızdaki geçici dosya klasörüne, PowerShell oturumunu yürütmek için kullandığınız *%USERPROFILE%\AppData\Local\Temp* kullanıcı profili altında kaydeder.</span><span class="sxs-lookup"><span data-stu-id="0e194-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="0e194-154">Kurumsal ortak sertifika (.cer file) ile bir Klasik Farklı Çalıştır hesabı oluşturduysanız bu sertifikayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e194-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="0e194-155">[Klasik Azure portalında yönetim API sertifikasını yükleme](../azure-api-management-certs.md) yönergelerini izleyin ve ardından [Azure Klasik Dağıtım Kaynakları ile kimlik doğrulamaya yönelik örnek kodunu](automation-verify-runas-authentication.md#classic-run-as-authentication) kullanarak klasik dağıtım kaynakları ile kimlik bilgisi yapılandırmasını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0e194-155">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with classic deployment resources by using the [sample code to authenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="0e194-156">Klasik Farklı Çalıştır hesabı *oluşturmadıysanız*, Resource Manager kaynakları kimlik doğrulaması yapmak ve kimlik bilgisi yapılandırmasını doğrulamak için [Service Management kaynakları ile kimlik doğrulamaya yönelik örnek kodu](automation-verify-runas-authentication.md#automation-run-as-authentication) kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e194-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e194-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e194-157">Next steps</span></span>
* <span data-ttu-id="0e194-158">Hizmet Sorumluları hakkında daha fazla bilgi için bkz. [Uygulama Nesneleri ve Hizmet Sorumlusu Nesneleri](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="0e194-158">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="0e194-159">Sertifikalar ve Azure hizmetleri hakkında daha fazla bilgi için bkz. [Azure Cloud Services sertifikalarına genel bakış](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="0e194-159">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
