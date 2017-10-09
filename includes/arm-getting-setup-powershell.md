## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="acf48-101">Resource Manager şablonları için PowerShell ayarlayan</span><span class="sxs-lookup"><span data-stu-id="acf48-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="acf48-102">Resource Manager ile Azure PowerShell kullanmadan önce toohave hello sağ Windows PowerShell ve Azure PowerShell sürümleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="acf48-102">Before you can use Azure PowerShell with Resource Manager, you will need toohave hello right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="acf48-103">PowerShell sürümlerini doğrulama</span><span class="sxs-lookup"><span data-stu-id="acf48-103">Verify PowerShell versions</span></span>
<span data-ttu-id="acf48-104">Windows PowerShell sürüm 3.0 veya 4.0 doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="acf48-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="acf48-105">toofind hello sürümü Windows PowerShell, Windows PowerShell komut isteminde bu komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="acf48-105">toofind hello version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="acf48-106">Tür bilgileri aşağıdaki hello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="acf48-106">You will receive hello following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="acf48-107">Bu hello değerini doğrulayın **PSVersion** 3.0 veya 4.0.</span><span class="sxs-lookup"><span data-stu-id="acf48-107">Verify that hello value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="acf48-108">Aksi takdirde bkz [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) veya [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="acf48-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="acf48-109">Azure hesabınızı ve aboneliğinizi ayarlama</span><span class="sxs-lookup"><span data-stu-id="acf48-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="acf48-110">Bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) veya kaydolun bir [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="acf48-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="acf48-111">Bir Azure PowerShell komut istemi açın ve bu komutla tooAzure oturum.</span><span class="sxs-lookup"><span data-stu-id="acf48-111">Open an Azure PowerShell command prompt and log on tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="acf48-112">Birden çok Azure aboneliğiniz varsa, bu komutla, Azure aboneliklerinize listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acf48-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="acf48-113">Tür bilgileri aşağıdaki hello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="acf48-113">You will receive hello following type of information:</span></span>

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

<span data-ttu-id="acf48-114">Hello Azure PowerShell komut isteminde şu komutları çalıştırarak hello geçerli Azure aboneliği ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acf48-114">You can set hello current Azure subscription by running these commands at hello Azure PowerShell command prompt.</span></span> <span data-ttu-id="acf48-115">Merhaba < ve > karakterleri dahil olmak üzere hello tırnak içindeki her şeyi hello doğru adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="acf48-115">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="acf48-116">Azure abonelikleri ve hesapları hakkında daha fazla bilgi için bkz: [nasıl yapılır: tooyour abonelik bağlanmak](/powershell/azureps-cmdlets-docs#step-3-connect).</span><span class="sxs-lookup"><span data-stu-id="acf48-116">For more information about Azure subscriptions and accounts, see [How to: Connect tooyour subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

