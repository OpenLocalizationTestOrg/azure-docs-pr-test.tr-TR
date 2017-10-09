## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a><span data-ttu-id="9a59f-101">Azure Resource Manager istekleri tooauthenticate hazırlama</span><span class="sxs-lookup"><span data-stu-id="9a59f-101">Prepare tooauthenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="9a59f-102">Hello kullanarak kaynakları üzerinde gerçekleştirdiğiniz tüm hello işlemleri kimlik doğrulaması yapmalıdır [Azure Resource Manager] [ lnk-authenticate-arm] ile Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="9a59f-102">You must authenticate all hello operations that you perform on resources using hello [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="9a59f-103">en kolay yolu tooconfigure hello toouse PowerShell veya Azure CLI budur.</span><span class="sxs-lookup"><span data-stu-id="9a59f-103">hello easiest way tooconfigure this is toouse PowerShell or Azure CLI.</span></span>

<span data-ttu-id="9a59f-104">Merhaba yüklemek [Azure PowerShell cmdlet'lerini] [ lnk-powershell-install] devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="9a59f-104">Install hello [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="9a59f-105">adımları Göster nasıl aşağıdaki hello tooset parola kimlik doğrulaması için PowerShell kullanarak bir AD uygulamasını ayarlama.</span><span class="sxs-lookup"><span data-stu-id="9a59f-105">hello following steps show how tooset up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="9a59f-106">Standart bir PowerShell oturumunda aşağıdaki komutları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a59f-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="9a59f-107">Tooyour içinde Azure aboneliği komutu aşağıdaki hello kullanarak oturum:</span><span class="sxs-lookup"><span data-stu-id="9a59f-107">Log in tooyour Azure subscription using hello following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="9a59f-108">Birden çok Azure aboneliğiniz varsa tooAzure imzalama tooall erişim verir kimlik bilgilerinizle ilişkili Azure abonelik hello.</span><span class="sxs-lookup"><span data-stu-id="9a59f-108">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="9a59f-109">Toouse toolist hello Azure abonelikleri kullanılabilir sizin için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9a59f-109">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="9a59f-110">IOT hub'ınızı toomanage toouse toorun hello komutları istediğiniz komut tooselect abonelik aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="9a59f-110">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="9a59f-111">Merhaba hello önceki komutunun çıktısından hello abonelik adı veya kimliği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9a59f-111">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="9a59f-112">Not, **Tenantıd** ve **Subscriptionıd**.</span><span class="sxs-lookup"><span data-stu-id="9a59f-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="9a59f-113">Daha sonra gereksinim duyarsınız.</span><span class="sxs-lookup"><span data-stu-id="9a59f-113">You need them later.</span></span>
3. <span data-ttu-id="9a59f-114">Aşağıdaki komut, hello yer tutucu değiştirme hello kullanarak yeni bir Azure Active Directory uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="9a59f-114">Create a new Azure Active Directory application using hello following command, replacing hello place holders:</span></span>
   
   * <span data-ttu-id="9a59f-115">**{Görünen adı}:** gibi uygulamanız için bir görünen ad **MySampleApp**</span><span class="sxs-lookup"><span data-stu-id="9a59f-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="9a59f-116">**{Giriş sayfası URL'si}:** , uygulamanızın hello giriş sayfasının URL'sini gibi hello **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="9a59f-116">**{Home page URL}:** hello URL of hello home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="9a59f-117">Bu URL toopoint tooa gerçek uygulama gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9a59f-117">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="9a59f-118">**{Uygulama tanımlayıcısı}:** gibi benzersiz bir tanımlayıcı **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="9a59f-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="9a59f-119">Bu URL toopoint tooa gerçek uygulama gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9a59f-119">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="9a59f-120">**{Parola}:** tooauthenticate uygulamanızla kullandığınız parola.</span><span class="sxs-lookup"><span data-stu-id="9a59f-120">**{Password}:** A password that you use tooauthenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="9a59f-121">Merhaba Not **ApplicationId** oluşturduğunuz hello uygulamasının.</span><span class="sxs-lookup"><span data-stu-id="9a59f-121">Make a note of hello **ApplicationId** of hello application you created.</span></span> <span data-ttu-id="9a59f-122">Bu daha sonra ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="9a59f-122">You need this later.</span></span>
5. <span data-ttu-id="9a59f-123">Aşağıdaki komut, değiştirme hello kullanarak yeni bir hizmet sorumlusu oluşturma **{MyApplicationId}** hello ile **ApplicationId** hello önceki adımdaki:</span><span class="sxs-lookup"><span data-stu-id="9a59f-123">Create a new service principal using hello following command, replacing **{MyApplicationId}** with hello **ApplicationId** from hello previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="9a59f-124">Aşağıdaki komut, değiştirme hello kullanarak bir rol ataması ayarlamak **{MyApplicationId}** ile **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="9a59f-124">Set up a role assignment using hello following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="9a59f-125">Şimdi, özel C# uygulamanızdan tooauthenticate sağlar hello Azure AD uygulaması oluşturma tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="9a59f-125">You have now finished creating hello Azure AD application that enables you tooauthenticate from your custom C# application.</span></span> <span data-ttu-id="9a59f-126">Daha sonra Bu öğreticide değerleri aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="9a59f-126">You need hello following values later in this tutorial:</span></span>

* <span data-ttu-id="9a59f-127">Tenantıd</span><span class="sxs-lookup"><span data-stu-id="9a59f-127">TenantId</span></span>
* <span data-ttu-id="9a59f-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="9a59f-128">SubscriptionId</span></span>
* <span data-ttu-id="9a59f-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="9a59f-129">ApplicationId</span></span>
* <span data-ttu-id="9a59f-130">Parola</span><span class="sxs-lookup"><span data-stu-id="9a59f-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
