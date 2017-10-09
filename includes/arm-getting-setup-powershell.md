## <a name="setting-up-powershell-for-resource-manager-templates"></a>Resource Manager şablonları için PowerShell ayarlayan
Resource Manager ile Azure PowerShell kullanmadan önce toohave hello sağ Windows PowerShell ve Azure PowerShell sürümleri gerekir.

### <a name="verify-powershell-versions"></a>PowerShell sürümlerini doğrulama
Windows PowerShell sürüm 3.0 veya 4.0 doğrulayın. toofind hello sürümü Windows PowerShell, Windows PowerShell komut isteminde bu komutu yazın.

    $PSVersionTable

Tür bilgileri aşağıdaki hello alırsınız:

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


Bu hello değerini doğrulayın **PSVersion** 3.0 veya 4.0. Aksi takdirde bkz [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) veya [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

### <a name="set-your-azure-account-and-subscription"></a>Azure hesabınızı ve aboneliğinizi ayarlama
Bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) veya kaydolun bir [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).

Bir Azure PowerShell komut istemi açın ve bu komutla tooAzure oturum.

    Login-AzureRmAccount

Birden çok Azure aboneliğiniz varsa, bu komutla, Azure aboneliklerinize listeleyebilirsiniz.

    Get-AzureRmSubscription

Tür bilgileri aşağıdaki hello alırsınız:

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

Hello Azure PowerShell komut isteminde şu komutları çalıştırarak hello geçerli Azure aboneliği ayarlayabilirsiniz. Merhaba < ve > karakterleri dahil olmak üzere hello tırnak içindeki her şeyi hello doğru adıyla değiştirin.

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

Azure abonelikleri ve hesapları hakkında daha fazla bilgi için bkz: [nasıl yapılır: tooyour abonelik bağlanmak](/powershell/azureps-cmdlets-docs#step-3-connect).

