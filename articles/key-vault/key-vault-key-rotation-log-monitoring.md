---
title: "Azure anahtar kasası yukarı aaaSet uçtan uca anahtar döndürme ve Denetim ile | Microsoft Docs"
description: "Anahtar rotasyonu ve izleme anahtar kasası günlükleri ayarlamak bu nasıl tootoohelp kullanın."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="9a363-103">Azure Anahtar Kasası’nı uçtan uca döndürme ve denetleme ile ayarlama</span><span class="sxs-lookup"><span data-stu-id="9a363-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="9a363-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="9a363-104">Introduction</span></span>
<span data-ttu-id="9a363-105">Anahtar kasası oluşturduktan sonra o kasa toostore anahtarları ve gizli anahtarları kullanarak mümkün toostart olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9a363-105">After creating your key vault, you will be able toostart using that vault toostore your keys and secrets.</span></span> <span data-ttu-id="9a363-106">Uygulamalarınızı artık toopersist anahtar veya gizli gerekir, ancak bunun yerine bunları hello anahtar Kasası'nı gerektiğinde isteyecek.</span><span class="sxs-lookup"><span data-stu-id="9a363-106">Your applications no longer need toopersist your keys or secrets, but rather will request them from hello key vault as needed.</span></span> <span data-ttu-id="9a363-107">Bu, tooupdate anahtarlar ve gizli anahtarı ve gizli yönetim olanakları derecesini açar uygulamanızın hello davranışını etkilemeden sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a363-107">This allows you tooupdate keys and secrets without affecting hello behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="9a363-108">Bu makalede Azure anahtar kasası toostore kullanma örneği bu durumda, bir uygulama tarafından erişilebilen bir Azure depolama hesabı anahtarı bir gizlilik anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9a363-108">This article walks through an example of using Azure Key Vault toostore a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="9a363-109">Ayrıca, bu depolama hesabı anahtarı zamanlanmış dönüşünü uyarlamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9a363-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="9a363-110">Son olarak, nasıl toomonitor anahtar kasası denetim günlüklerini hello ve beklenmeyen istekler yapıldığında uyarı verileceğini Tanıtımı anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9a363-110">Finally, it walks through a demonstration of how toomonitor hello key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="9a363-111">Bu öğretici hedeflenen tooexplain ayrıntı hello ilk kurulumunda anahtar kasanızı değil.</span><span class="sxs-lookup"><span data-stu-id="9a363-111">This tutorial is not intended tooexplain in detail hello initial setup of your key vault.</span></span> <span data-ttu-id="9a363-112">Bu bilgi için bkz. [Azure Anahtar Kasası ile çalışmaya başlama](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9a363-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="9a363-113">Platformlar arası komut satırı arabirimi yönergeleri için bkz: [anahtar kasası CLI kullanarak yönetme](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="9a363-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="9a363-114">Anahtar Kasası ayarlama</span><span class="sxs-lookup"><span data-stu-id="9a363-114">Set up Key Vault</span></span>
<span data-ttu-id="9a363-115">tooenable uygulama tooretrieve bir gizli anahtar Kasası'nı öncelikle hello gizli anahtar oluşturma ve tooyour kasası karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9a363-115">tooenable an application tooretrieve a secret from Key Vault, you must first create hello secret and upload it tooyour vault.</span></span> <span data-ttu-id="9a363-116">Bu, bir Azure PowerShell oturumu başlatarak ve tooyour içinde Azure hesabı komutu aşağıdaki hello ile imzalama gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="9a363-116">This can be accomplished by starting an Azure PowerShell session and signing in tooyour Azure account with hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="9a363-117">Merhaba açılır tarayıcı penceresinde Azure hesabı kullanıcı adınızı ve parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="9a363-117">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="9a363-118">PowerShell Bu hesapla ilişkili tüm hello abonelikleri alır.</span><span class="sxs-lookup"><span data-stu-id="9a363-118">PowerShell will get all hello subscriptions that are associated with this account.</span></span> <span data-ttu-id="9a363-119">PowerShell kullanan varsayılan olarak birinci hello.</span><span class="sxs-lookup"><span data-stu-id="9a363-119">PowerShell uses hello first one by default.</span></span>

<span data-ttu-id="9a363-120">Birden çok aboneliğiniz varsa, kullanılan toocreate olan bir anahtar kasanızı hello toospecify olabilir.</span><span class="sxs-lookup"><span data-stu-id="9a363-120">If you have multiple subscriptions, you might have toospecify hello one that was used toocreate your key vault.</span></span> <span data-ttu-id="9a363-121">Hesabınız için toosee hello abonelikleri aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="9a363-121">Enter hello following toosee hello subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="9a363-122">günlüğünü tutacağınız, hello anahtar kasasıyla ilişkili toospecify hello abonelik girin:</span><span class="sxs-lookup"><span data-stu-id="9a363-122">toospecify hello subscription that's associated with hello key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="9a363-123">Bu makalede, bir depolama hesabı anahtarı gizli depolama gösterilmektedir olduğundan, bu depolama hesabı anahtarı edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a363-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="9a363-124">Gizli (Bu durumda, depolama hesabı anahtarınızı) aldıktan sonra o tooa güvenli dize dönüştürme ve anahtar kasanızı'da bu değerle bir gizli anahtar oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a363-124">After retrieving your secret (in this case, your storage account key), you must convert that tooa secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="9a363-125">Ardından, oluşturduğunuz hello gizliliğini hello URI alın.</span><span class="sxs-lookup"><span data-stu-id="9a363-125">Next, get hello URI for hello secret you created.</span></span> <span data-ttu-id="9a363-126">Gizli hello anahtar kasası tooretrieve çağırdığınızda bu bir sonraki adımda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9a363-126">This is used in a later step when you call hello key vault tooretrieve your secret.</span></span> <span data-ttu-id="9a363-127">Merhaba aşağıdaki PowerShell komutunu çalıştırın ve hello parolası URI hello kimliği değeri not edin:</span><span class="sxs-lookup"><span data-stu-id="9a363-127">Run hello following PowerShell command and make note of hello ID value, which is hello secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a><span data-ttu-id="9a363-128">Merhaba uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="9a363-128">Set up hello application</span></span>
<span data-ttu-id="9a363-129">Depolanan gizli sahip olduğunuza göre kod tooretrieve kullanın ve bunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9a363-129">Now that you have a secret stored, you can use code tooretrieve and use it.</span></span> <span data-ttu-id="9a363-130">Vardır birkaç adımları gerekli tooachieve bu.</span><span class="sxs-lookup"><span data-stu-id="9a363-130">There are a few steps required tooachieve this.</span></span> <span data-ttu-id="9a363-131">Hello ilk ve en önemli adım Azure Active Directory ile uygulamanızı kaydetme ve böylece uygulamanız gelen istekleri izin verebilir anahtar kasası, uygulama bilgilerinizi belirtiyor.</span><span class="sxs-lookup"><span data-stu-id="9a363-131">hello first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="9a363-132">Uygulamanızın üzerinde hello aynı oluşturulmalıdır anahtar kasanızı olarak Azure Active Directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="9a363-132">Your application must be created on hello same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="9a363-133">Azure Active Directory Hello uygulamalar sekmesini açın.</span><span class="sxs-lookup"><span data-stu-id="9a363-133">Open hello applications tab of Azure Active Directory.</span></span>

![Azure Active Directory'de açık uygulamalar](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="9a363-135">Seçin **ekleme** tooadd uygulama tooyour Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9a363-135">Choose **ADD** tooadd an application tooyour Azure Active Directory.</span></span>

![EKLE'yi seçin](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="9a363-137">Merhaba uygulama türü olarak bırakın **WEB uygulaması ve/veya WEB API** ve uygulamanızı bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="9a363-137">Leave hello application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Ad Merhaba uygulaması](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="9a363-139">Uygulamanızı vermek bir **oturum açma URL** ve bir **uygulama kimliği URI'si**.</span><span class="sxs-lookup"><span data-stu-id="9a363-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="9a363-140">Bunlar bu tanıtım için istediğiniz herhangi bir şey olabilir ve bunlar daha sonra gerekirse değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9a363-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Gerekli URI'ler sağlar](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="9a363-142">Merhaba uygulaması tooAzure Active Directory eklendikten sonra hello uygulama sayfasına gidersiniz.</span><span class="sxs-lookup"><span data-stu-id="9a363-142">After hello application is added tooAzure Active Directory, you will be brought into hello application page.</span></span> <span data-ttu-id="9a363-143">Merhaba tıklatın **yapılandırma** sekmesini ve ardından bulmak ve kopyalama hello **istemci kimliği** değeri.</span><span class="sxs-lookup"><span data-stu-id="9a363-143">Click hello **Configure** tab and then find and copy hello **Client ID** value.</span></span> <span data-ttu-id="9a363-144">Sonraki adımlar için hello istemci Kimliğini not edin.</span><span class="sxs-lookup"><span data-stu-id="9a363-144">Make note of hello client ID for later steps.</span></span>

<span data-ttu-id="9a363-145">Ardından, Azure Active Directory ile etkileşim kurabilmesi uygulamanız için bir anahtar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9a363-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="9a363-146">Bu altında hello oluşturabilir **anahtarları** hello bölümünde **yapılandırma** sekmesi. Bir sonraki adımda kullanmak için Azure Active Directory uygulamanızdan hello yeni oluşturulan anahtarı not edin.</span><span class="sxs-lookup"><span data-stu-id="9a363-146">You can create this under hello **Keys** section in hello **Configuration** tab. Make note of hello newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Azure Active Directory uygulama anahtarları](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="9a363-148">Merhaba anahtar kasası uygulamanıza gelen tüm çağrıları oluşturmadan önce uygulamanızı ve izinlerini hakkında hello anahtar kasası söylemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="9a363-148">Before establishing any calls from your application into hello key vault, you must tell hello key vault about your application and its permissions.</span></span> <span data-ttu-id="9a363-149">Merhaba aşağıdaki komutu hello kasa adı ve hello istemci kimliği verir ve Azure Active Directory Uygulama alır **almak** hello uygulama için erişim tooyour anahtar kasası.</span><span class="sxs-lookup"><span data-stu-id="9a363-149">hello following command takes hello vault name and hello client ID from your Azure Active Directory app and grants **Get** access tooyour key vault for hello application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="9a363-150">Bu noktada, uygulama çağrılarınızı oluşturmaya hazır toostart var.</span><span class="sxs-lookup"><span data-stu-id="9a363-150">At this point, you are ready toostart building your application calls.</span></span> <span data-ttu-id="9a363-151">Uygulamanızda Azure anahtar kasası ve Azure Active Directory ile Merhaba NuGet paketleri gerekli toointeract yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a363-151">In your application, you must install hello NuGet packages required toointeract with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="9a363-152">Merhaba Visual Studio Paket Yöneticisi Konsolu'ndan komutları aşağıdaki hello girin.</span><span class="sxs-lookup"><span data-stu-id="9a363-152">From hello Visual Studio Package Manager console, enter hello following commands.</span></span> <span data-ttu-id="9a363-153">Tooconfirm hello en son sürümünü istediğiniz ve uygun şekilde güncelleştirmek için bu makalenin hello yazıda hello geçerli hello Azure Active Directory paket 3.10.305231913, sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="9a363-153">At hello writing of this article, hello current version of hello Azure Active Directory package is 3.10.305231913, so you might want tooconfirm hello latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="9a363-154">Uygulama kodunuz, Azure Active Directory kimlik doğrulaması için bir sınıf toohold hello yöntemi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9a363-154">In your application code, create a class toohold hello method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="9a363-155">Bu örnekte, o sınıfın adlı **yardımcı programları**.</span><span class="sxs-lookup"><span data-stu-id="9a363-155">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="9a363-156">Merhaba aşağıdaki ekleme deyimini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="9a363-156">Add hello following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="9a363-157">Ardından, Azure Active Directory'den yöntemi tooretrieve hello JWT belirteci aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9a363-157">Next, add hello following method tooretrieve hello JWT token from Azure Active Directory.</span></span> <span data-ttu-id="9a363-158">Bakım için web ya da uygulama yapılandırmanızı toomove hello sabit kodlanmış dize değerlerini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a363-158">For maintainability, you may want toomove hello hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="9a363-159">Merhaba gerekli kodu toocall anahtar kasası ekleme ve gizli değer alma.</span><span class="sxs-lookup"><span data-stu-id="9a363-159">Add hello necessary code toocall Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="9a363-160">İlk hello aşağıdakileri ekleyin deyimi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="9a363-160">First you must add hello following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="9a363-161">Merhaba yöntemi çağrıları tooinvoke anahtar kasası ekleme ve gizli anahtarı alma.</span><span class="sxs-lookup"><span data-stu-id="9a363-161">Add hello method calls tooinvoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="9a363-162">Bu yöntemde hello gizli bir önceki adımda kaydettiğiniz URI sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9a363-162">In this method, you provide hello secret URI that you saved in a previous step.</span></span> <span data-ttu-id="9a363-163">Not hello hello **GetToken** hello yönteminden **yardımcı programları** daha önce oluşturduğunuz sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9a363-163">Note hello use of hello **GetToken** method from hello **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="9a363-164">Uygulamanızı çalıştırdığınızda, şimdi tooAzure Active Directory ve sonra gizli değer Azure anahtar Kasası'alma kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="9a363-164">When you run your application, you should now be authenticating tooAzure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="9a363-165">Azure otomasyonu kullanarak anahtar döndürme</span><span class="sxs-lookup"><span data-stu-id="9a363-165">Key rotation using Azure Automation</span></span>
<span data-ttu-id="9a363-166">Değerleri Azure anahtar kasası gizlilikleri olarak depolamak için bir dönüş stratejisi uygulamaya yönelik çeşitli seçenekleriniz vardır.</span><span class="sxs-lookup"><span data-stu-id="9a363-166">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="9a363-167">El ile işleminin bir parçası gizli döndürülüp, bunlar program aracılığıyla API çağrılarını kullanarak döndürülüp ya da bir otomasyon komut dosyası aracılığıyla Döndürülmüş.</span><span class="sxs-lookup"><span data-stu-id="9a363-167">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="9a363-168">Bu makalede Hello amaçları doğrultusunda, siz olacaksınız bir Azure depolama hesabı erişim tuşu birleştirilmiş Azure Otomasyonu toochange ile Azure PowerShell'i kullanma.</span><span class="sxs-lookup"><span data-stu-id="9a363-168">For hello purposes of this article, you will be using Azure PowerShell combined with Azure Automation toochange an Azure Storage Account access key.</span></span> <span data-ttu-id="9a363-169">Ardından bu yeni anahtarla bir anahtar kasası gizli anahtarı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="9a363-169">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="9a363-170">tooallow Azure Otomasyonu tooset gizli değer anahtar kasanızı hello istemci kimliği, Azure Automation örneğiyle oluşturulduğu AzureRunAsConnection adlı hello bağlantısı için almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a363-170">tooallow Azure Automation tooset secret values in your key vault, you must get hello client ID for hello connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="9a363-171">Bu kimliği seçerek bulabileceğiniz **varlıklar** , Azure Automation örneğinden.</span><span class="sxs-lookup"><span data-stu-id="9a363-171">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="9a363-172">Buradan, seçtiğiniz **bağlantıları** seçip hello **AzureRunAsConnection** hizmet ilkesi.</span><span class="sxs-lookup"><span data-stu-id="9a363-172">From there, you choose **Connections** and then select hello **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="9a363-173">Merhaba not edin **uygulama kimliği**.</span><span class="sxs-lookup"><span data-stu-id="9a363-173">Take note of hello **Application ID**.</span></span>

![Azure otomasyon istemci kimliği](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="9a363-175">İçinde **varlıklar**, seçin **modülleri**.</span><span class="sxs-lookup"><span data-stu-id="9a363-175">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="9a363-176">Gelen **modülleri**seçin **galeri**, arayın ve sonra ve **alma** güncelleştirilmiş sürümlerini her bir modül aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="9a363-176">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of hello following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="9a363-177">Bu makalenin Hello yazıda yalnızca hello gerekli daha önce not ettiğiniz modülleri toobe komut dosyası izleyen hello için güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="9a363-177">At hello writing of this article, only hello previously noted modules needed toobe updated for hello following script.</span></span> <span data-ttu-id="9a363-178">Otomasyon işinizi başarısız olduğunu fark ederseniz, gerekli olan tüm modülleri ve bağımlılıklarını içeri aktardığınız onaylayın.</span><span class="sxs-lookup"><span data-stu-id="9a363-178">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="9a363-179">Azure Otomasyonu bağlantınız için hello uygulama kimliği aldıktan sonra bu uygulama, kasaya erişim tooupdate gizli olduğunu, anahtar kasanızı bildirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a363-179">After you have retrieved hello application ID for your Azure Automation connection, you must tell your key vault that this application has access tooupdate secrets in your vault.</span></span> <span data-ttu-id="9a363-180">Bu PowerShell komutunu aşağıdaki hello ile gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="9a363-180">This can be accomplished with hello following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="9a363-181">Ardından, **Runbook'lar** Azure Automation örneği ve ardından altında **Runbook Ekle**.</span><span class="sxs-lookup"><span data-stu-id="9a363-181">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="9a363-182">**Hızlı Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="9a363-182">Select **Quick Create**.</span></span> <span data-ttu-id="9a363-183">Runbook'unuzda adlandırın ve seçin **PowerShell** hello runbook türü.</span><span class="sxs-lookup"><span data-stu-id="9a363-183">Name your runbook and select **PowerShell** as hello runbook type.</span></span> <span data-ttu-id="9a363-184">Merhaba seçeneği tooadd bir tanıma sahip.</span><span class="sxs-lookup"><span data-stu-id="9a363-184">You have hello option tooadd a description.</span></span> <span data-ttu-id="9a363-185">Son olarak, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="9a363-185">Finally, click **Create**.</span></span>

![Runbook oluşturma](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="9a363-187">Yeni runbook'unuz için hello Düzenleyicisi bölmesinde PowerShell Betiği aşağıdaki hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="9a363-187">Paste hello following PowerShell script in hello editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="9a363-188">Merhaba Düzenleyicisi bölmesinden seçin **Test bölmesi** tootest komut.</span><span class="sxs-lookup"><span data-stu-id="9a363-188">From hello editor pane, choose **Test pane** tootest your script.</span></span> <span data-ttu-id="9a363-189">Merhaba komut hatasız çalışmaya başladıktan sonra seçebileceğiniz **Yayımla**, ve daha sonra geri hello runbook yapılandırma Bölmesi'nde hello runbook için bir zamanlama uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a363-189">Once hello script is running without error, you can select **Publish**, and then you can apply a schedule for hello runbook back in hello runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="9a363-190">Anahtar kasası denetim ardışık düzen</span><span class="sxs-lookup"><span data-stu-id="9a363-190">Key Vault auditing pipeline</span></span>
<span data-ttu-id="9a363-191">Bir anahtar kasasını ayarladığınızda, toohello anahtar kasası erişim isteklerini toocollect açtığında denetim kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a363-191">When you set up a key vault, you can turn on auditing toocollect logs on access requests made toohello key vault.</span></span> <span data-ttu-id="9a363-192">Bu günlükler belirlenmiş bir Azure depolama hesabında depolanır ve çıkışı, izlenen ve analiz çekebilir.</span><span class="sxs-lookup"><span data-stu-id="9a363-192">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="9a363-193">hello uygulama kimliği hello web uygulamasının eşleşen bir uygulama parolaları hello kasadan aldığında hello aşağıdaki senaryoyu Azure işlevleri, Azure mantıksal uygulamaları ve anahtar kasası denetim günlüklerini toocreate ardışık düzen toosend bir e-posta kullanır.</span><span class="sxs-lookup"><span data-stu-id="9a363-193">hello following scenario uses Azure functions, Azure logic apps, and key vault audit logs toocreate a pipeline toosend an email when an app that does match hello app ID of hello web app retrieves secrets from hello vault.</span></span>

<span data-ttu-id="9a363-194">İlk olarak, anahtar kasanızı günlüğü etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a363-194">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="9a363-195">Bu PowerShell komutlarını aşağıdaki hello yapılabilir (tam Ayrıntılar adresindeki görülme [anahtar kasası günlüğü](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="9a363-195">This can be done via hello following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="9a363-196">Bu özellik etkinleştirildikten sonra Denetim depolama hesabını belirlenmiş hello toplama başlangıç günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9a363-196">After this is enabled, audit logs start collecting into hello designated storage account.</span></span> <span data-ttu-id="9a363-197">Bu günlükler olayları anahtar kasalarınıza erişilen nasıl ve ne zaman ve kim tarafından içerir.</span><span class="sxs-lookup"><span data-stu-id="9a363-197">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="9a363-198">Merhaba anahtar kasası işleminden sonra 10 dakika günlük bilgilerinize erişebilir.</span><span class="sxs-lookup"><span data-stu-id="9a363-198">You can access your logging information 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="9a363-199">Genellikle bu değerden daha hızlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9a363-199">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="9a363-200">Merhaba sonraki adımdır çok[bir Azure hizmet veri yolu kuyruğu oluşturma](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="9a363-200">hello next step is too[create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="9a363-201">Anahtar kasası denetim günlüklerini burada gönderilen budur.</span><span class="sxs-lookup"><span data-stu-id="9a363-201">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="9a363-202">Merhaba denetim günlüğü iletileri hello sırada olduğunda hello mantıksal uygulama bunları alır ve bunlar üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="9a363-202">When hello audit log messages are in hello queue, hello logic app picks them up and acts on them.</span></span> <span data-ttu-id="9a363-203">Hizmet veri yolu ile şu adımları hello oluşturun:</span><span class="sxs-lookup"><span data-stu-id="9a363-203">Create a service bus with hello following steps:</span></span>

1. <span data-ttu-id="9a363-204">Hizmet veri yolu ad alanı oluşturma (istediğiniz zaten varsa, bunun için toouse tooStep 2 atlayın).</span><span class="sxs-lookup"><span data-stu-id="9a363-204">Create a Service Bus namespace (if you already have one that you want toouse for this, skip tooStep 2).</span></span>
2. <span data-ttu-id="9a363-205">Toohello service bus hello Azure portal ve select hello ad toocreate hello sıra istediğiniz göz atın.</span><span class="sxs-lookup"><span data-stu-id="9a363-205">Browse toohello service bus in hello Azure portal and select hello namespace you want toocreate hello queue in.</span></span>
3. <span data-ttu-id="9a363-206">Seçin **yeni** ve **hizmet veri yolu > sıra** ve gerekli hello ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="9a363-206">Select **New** and choose **Service Bus > Queue** and enter hello required details.</span></span>
4. <span data-ttu-id="9a363-207">Merhaba Service Bus bağlantı bilgilerini hello ad seçme ve tıklatarak seçin **bağlantı bilgilerini**.</span><span class="sxs-lookup"><span data-stu-id="9a363-207">Select hello Service Bus connection information by choosing hello namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="9a363-208">Merhaba sonraki bölüm için bu bilgilere ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9a363-208">You will need this information for hello next section.</span></span>

<span data-ttu-id="9a363-209">Ardından, [bir Azure işlevi oluşturma](../azure-functions/functions-create-first-azure-function.md) toopoll anahtar kasası günlükleri içinde hello depolama hesabı ve yeni olayları seçin.</span><span class="sxs-lookup"><span data-stu-id="9a363-209">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) toopoll key vault logs within hello storage account and pick up new events.</span></span> <span data-ttu-id="9a363-210">Bu bir zamanlamaya göre tetiklenen bir işlev olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9a363-210">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="9a363-211">toocreate bir Azure işlevi seçin **yeni > işlev uygulaması** hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="9a363-211">toocreate an Azure function, choose **New > Function App** in hello Azure portal.</span></span> <span data-ttu-id="9a363-212">Oluşturma sırasında var olan bir barındırma planı kullanın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9a363-212">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="9a363-213">Ayrıca, dinamik barındırmak için tercih.</span><span class="sxs-lookup"><span data-stu-id="9a363-213">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="9a363-214">İşlevi barındırma seçenekleri hakkında daha fazla ayrıntı bulunabilir [nasıl tooscale Azure işlevleri](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="9a363-214">More details on Function hosting options can be found at [How tooscale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="9a363-215">Hello Azure işlevi oluşturulduğunda tooit gidin ve bir süreölçer işlevi C seçip\#.</span><span class="sxs-lookup"><span data-stu-id="9a363-215">When hello Azure function is created, navigate tooit and choose a timer function and C\#.</span></span> <span data-ttu-id="9a363-216">Ardından **bu işlev oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="9a363-216">Then click **Create this function**.</span></span>

![Azure işlevleri Başlat dikey penceresi](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="9a363-218">Merhaba üzerinde **geliştirme** sekmesinde, hello run.csx kod hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9a363-218">On hello **Develop** tab, replace hello run.csx code with hello following:</span></span>

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="9a363-219">Kod toopoint tooyour depolama hesabı hello anahtar kasası günlükleri yazılacağı önceki hello hello hizmet veri yolu daha önce oluşturduğunuz emin tooreplace hello değişkenleri yapın ve belirli bir yola toohello anahtar kasası depolama günlükleri hello.</span><span class="sxs-lookup"><span data-stu-id="9a363-219">Make sure tooreplace hello variables in hello preceding code toopoint tooyour storage account where hello key vault logs are written, hello service bus you created earlier, and hello specific path toohello key vault storage logs.</span></span>
>
>

<span data-ttu-id="9a363-220">Merhaba işlevi hello anahtar kasası günlükleri, hello son olayları alan bu dosyadan yazılacağı hello en son günlük dosyası hello depolama hesabından seçer ve tooa Service Bus kuyruğuna iter.</span><span class="sxs-lookup"><span data-stu-id="9a363-220">hello function picks up hello latest log file from hello storage account where hello key vault logs are written, grabs hello latest events from that file, and pushes them tooa Service Bus queue.</span></span> <span data-ttu-id="9a363-221">Tek bir dosyada birden çok olay olabilir beri hello işlevi toodetermine hello çekilmiş yukarı hello son olay zaman damgası da bakan bir sync.txt dosyası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a363-221">Since a single file could have multiple events, you should create a sync.txt file that hello function also looks at toodetermine hello time stamp of hello last event that was picked up.</span></span> <span data-ttu-id="9a363-222">Bu, anında yok sağlar birden çok kez aynı olay hello.</span><span class="sxs-lookup"><span data-stu-id="9a363-222">This ensures that you don't push hello same event multiple times.</span></span> <span data-ttu-id="9a363-223">Bu sync.txt dosya hello son karşılaşılan olayı için bir zaman damgası içeriyor.</span><span class="sxs-lookup"><span data-stu-id="9a363-223">This sync.txt file contains a timestamp for hello last encountered event.</span></span> <span data-ttu-id="9a363-224">Merhaba yüklendiğinde, günlükleri, sahip sıralanmış toobe bunlar doğru sıralı hello zaman damgası tooensure üzerinde temel.</span><span class="sxs-lookup"><span data-stu-id="9a363-224">hello logs, when loaded, have toobe sorted based on hello timestamp tooensure they are ordered correctly.</span></span>

<span data-ttu-id="9a363-225">Bu işlev için birkaç Azure işlevleri hello kutusunda dışında bulunmayan ek kitaplıklara başvuru.</span><span class="sxs-lookup"><span data-stu-id="9a363-225">For this function, we reference a couple of additional libraries that are not available out of hello box in Azure Functions.</span></span> <span data-ttu-id="9a363-226">tooinclude bunlar, Azure işlevleri toopull ihtiyacımız bunları NuGet kullanma.</span><span class="sxs-lookup"><span data-stu-id="9a363-226">tooinclude these, we need Azure Functions toopull them using NuGet.</span></span> <span data-ttu-id="9a363-227">Merhaba seçin **dosyaları görüntüle** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="9a363-227">Choose hello **View Files** option.</span></span>

![Görünüm dosyaları seçeneği](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="9a363-229">Ve aşağıdaki içeriğe sahip project.json adlı bir dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9a363-229">And add a file called project.json with following content:</span></span>

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
<span data-ttu-id="9a363-230">Bağlı **kaydetmek**, Azure işlevleri, gerekli hello ikili dosyaları indirir.</span><span class="sxs-lookup"><span data-stu-id="9a363-230">Upon **Save**, Azure Functions will download hello required binaries.</span></span>

<span data-ttu-id="9a363-231">Geçiş toohello **tümleştir** sekmesinde ve hello Zamanlayıcı parametre anlamlı bir ad toouse hello işlevi içinde verin.</span><span class="sxs-lookup"><span data-stu-id="9a363-231">Switch toohello **Integrate** tab and give hello timer parameter a meaningful name toouse within hello function.</span></span> <span data-ttu-id="9a363-232">İsteğe bağlı olarak kod önceki hello adlı hello Zamanlayıcı toobe bekliyor *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="9a363-232">In hello preceding code, it expects hello timer toobe called *myTimer*.</span></span> <span data-ttu-id="9a363-233">Belirtin bir [CRON ifade](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) gibi: 0 \* \* \* \* \* hello işlevi toorun bir dakika neden olacak hello Zamanlayıcı için.</span><span class="sxs-lookup"><span data-stu-id="9a363-233">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for hello timer that will cause hello function toorun once a minute.</span></span>

<span data-ttu-id="9a363-234">Üzerinde hello aynı **tümleştir** sekmesinde, hello türündeki bir girdi ekleme **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="9a363-234">On hello same **Integrate** tab, add an input of hello type **Azure Blob Storage**.</span></span> <span data-ttu-id="9a363-235">Bu en hello işlevi tarafından aranan hello son olay hello zaman damgası içeren toohello sync.txt dosyasını işaret edecek.</span><span class="sxs-lookup"><span data-stu-id="9a363-235">This will point toohello sync.txt file that contains hello timestamp of hello last event looked at by hello function.</span></span> <span data-ttu-id="9a363-236">Bu, hello parametre adı tarafından hello işlevi içinde kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9a363-236">This will be available within hello function by hello parameter name.</span></span> <span data-ttu-id="9a363-237">Kod önceki hello hello parametre adı toobe hello Azure Blob Storage giriş bekliyor *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="9a363-237">In hello preceding code, hello Azure Blob Storage input expects hello parameter name toobe *inputBlob*.</span></span> <span data-ttu-id="9a363-238">Merhaba sync.txt dosya nerede bulunacağı hello depolama hesabını seçin (aynı veya farklı bir depolama hesabı hello olabilir).</span><span class="sxs-lookup"><span data-stu-id="9a363-238">Choose hello storage account where hello sync.txt file will reside (it could be hello same or a different storage account).</span></span> <span data-ttu-id="9a363-239">Merhaba yol alanına nerede {container-name}/path/to/sync.txt. hello biçiminde hello dosya yaşıyor hello yolunu belirtin</span><span class="sxs-lookup"><span data-stu-id="9a363-239">In hello path field, provide hello path where hello file lives in hello format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="9a363-240">Bir çıkış hello türü ekleme *Azure Blob Storage* çıktı.</span><span class="sxs-lookup"><span data-stu-id="9a363-240">Add an output of hello type *Azure Blob Storage* output.</span></span> <span data-ttu-id="9a363-241">Bu toohello sync.txt dosyası hello girişinde tanımlı noktası.</span><span class="sxs-lookup"><span data-stu-id="9a363-241">This will point toohello sync.txt file you defined in hello input.</span></span> <span data-ttu-id="9a363-242">Bu, aranan hello son olay hello işlevi toowrite hello zaman damgası tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9a363-242">This is used by hello function toowrite hello timestamp of hello last event looked at.</span></span> <span data-ttu-id="9a363-243">Merhaba önceki kod bekliyor olarak adlandırılan bu parametre toobe *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="9a363-243">hello preceding code expects this parameter toobe called *outputBlob*.</span></span>

<span data-ttu-id="9a363-244">Bu noktada, hello işlevi hazırdır.</span><span class="sxs-lookup"><span data-stu-id="9a363-244">At this point, hello function is ready.</span></span> <span data-ttu-id="9a363-245">Emin tooswitch geri toohello olun **geliştirme** sekmesinde ve hello kodu kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9a363-245">Make sure tooswitch back toohello **Develop** tab and save hello code.</span></span> <span data-ttu-id="9a363-246">Derleme hataları için Hello çıktı penceresini denetleyin ve uygun şekilde düzeltin.</span><span class="sxs-lookup"><span data-stu-id="9a363-246">Check hello output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="9a363-247">Hello kodu derler, hello kod artık hello anahtar kasası günlükleri dakikada kontrol edilmesi ve Service Bus kuyruğuna hello üzerine yeni olaylar Ftp'den tanımlı.</span><span class="sxs-lookup"><span data-stu-id="9a363-247">If hello code compiles, then hello code should now be checking hello key vault logs every minute and pushing any new events onto hello defined Service Bus queue.</span></span> <span data-ttu-id="9a363-248">Günlük kaydı bilgileri hello işlevi her başlatılışında toohello günlük penceresindeki yazma görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a363-248">You should see logging information write out toohello log window every time hello function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="9a363-249">Azure mantıksal uygulama</span><span class="sxs-lookup"><span data-stu-id="9a363-249">Azure logic app</span></span>
<span data-ttu-id="9a363-250">Sonraki hello işlevi toohello Service Bus kuyruğuna Ftp'den, hello içerik ayrıştırır ve eşleşen bir koşula göre bir e-posta gönderir hello olayları seçer bir Azure mantıksal uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a363-250">Next you must create an Azure logic app that picks up hello events that hello function is pushing toohello Service Bus queue, parses hello content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="9a363-251">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md) çok giderek**yeni > mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="9a363-251">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going too**New > Logic App**.</span></span>

<span data-ttu-id="9a363-252">Merhaba mantıksal uygulama oluşturulduktan sonra tooit gidin ve seçin **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="9a363-252">Once hello logic app is created, navigate tooit and choose **edit**.</span></span> <span data-ttu-id="9a363-253">Merhaba mantığı uygulama düzenleyicisinde seçin **hizmet veri yolu kuyruğu** ve Service Bus kimlik bilgilerini tooconnect girin, toohello sırası.</span><span class="sxs-lookup"><span data-stu-id="9a363-253">Within hello logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials tooconnect it toohello queue.</span></span>

![Azure Logic App Service Bus](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="9a363-255">Sonraki seçin **bir koşul eklemek**.</span><span class="sxs-lookup"><span data-stu-id="9a363-255">Next choose **Add a condition**.</span></span> <span data-ttu-id="9a363-256">Merhaba koşulunda Düzenleyicisi Gelişmiş toohello geçin ve aşağıdaki kod, APP_ID hello ile değiştiriliyor hello girin, web uygulamanızın gerçek APP_ID:</span><span class="sxs-lookup"><span data-stu-id="9a363-256">In hello condition, switch toohello advanced editor and enter hello following code, replacing APP_ID with hello actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="9a363-257">Bu ifade temelde döndürür **false** hello varsa *AppID* olduğundan (Bu hello hello Service Bus ileti gövdesi) gelen olay hello değil hello *AppID* Merhaba, uygulama.</span><span class="sxs-lookup"><span data-stu-id="9a363-257">This expression essentially returns **false** if hello *appid* from hello incoming event (which is hello body of hello Service Bus message) is not hello *appid* of hello app.</span></span>

<span data-ttu-id="9a363-258">Şimdi, altında bir eylem oluşturun **Öyle değilse, hiçbir şey yapma**.</span><span class="sxs-lookup"><span data-stu-id="9a363-258">Now, create an action under **If no, do nothing**.</span></span>

![Azure mantıksal uygulama eylemi seçin](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="9a363-260">Merhaba eylem için **Office 365 - e-postası gönderme**.</span><span class="sxs-lookup"><span data-stu-id="9a363-260">For hello action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="9a363-261">Merhaba koşul döndürür tanımlandığında hello alanları toocreate bir e-posta toosend doldurun **false**.</span><span class="sxs-lookup"><span data-stu-id="9a363-261">Fill out hello fields toocreate an email toosend when hello defined condition returns **false**.</span></span> <span data-ttu-id="9a363-262">Office 365 yoksa alternatifleri görünebilir tooachieve hello aynı sonuçları.</span><span class="sxs-lookup"><span data-stu-id="9a363-262">If you do not have Office 365, you could look at alternatives tooachieve hello same results.</span></span>

<span data-ttu-id="9a363-263">Bu noktada yeni anahtar kasası denetim günlükleri için bir dakika benzeyen bir bitiş tooend ardışık vardır.</span><span class="sxs-lookup"><span data-stu-id="9a363-263">At this point, you have an end tooend pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="9a363-264">Yeni günlükler tooa hizmet veri yolu kuyruğu bulduğu iter.</span><span class="sxs-lookup"><span data-stu-id="9a363-264">It pushes new logs it finds tooa service bus queue.</span></span> <span data-ttu-id="9a363-265">Yeni bir ileti hello sırada adlandırıldığını zaman hello mantıksal uygulama tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="9a363-265">hello logic app is triggered when a new message lands in hello queue.</span></span> <span data-ttu-id="9a363-266">Merhaba, *AppID* içinde hello uygulamasını çağıran hello hello uygulama Kimliğini olay eşleşmiyor, bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="9a363-266">If hello *appid* within hello event does not match hello app ID of hello calling application, it sends an email.</span></span>
