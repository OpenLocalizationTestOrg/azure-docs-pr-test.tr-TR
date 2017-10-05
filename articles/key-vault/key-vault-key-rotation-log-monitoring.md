---
title: "Azure anahtar kasası uçtan uca anahtar döndürme ve denetim ayarlama | Microsoft Docs"
description: "Anahtar rotasyonu ve izleme anahtar kasası günlükleri ayarlanmasını yardımcı olması için bu nasıl yapılır konuları kullanın."
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
ms.openlocfilehash: 38c342802ed687985ac6f84f5a590a1a0dcc6c6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="26181-103">Azure Anahtar Kasası’nı uçtan uca döndürme ve denetleme ile ayarlama</span><span class="sxs-lookup"><span data-stu-id="26181-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="26181-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="26181-104">Introduction</span></span>
<span data-ttu-id="26181-105">Anahtar kasası oluşturduktan sonra anahtarları ve gizli anahtarları depolamak için bu kasası kullanmaya başlamak mümkün olur.</span><span class="sxs-lookup"><span data-stu-id="26181-105">After creating your key vault, you will be able to start using that vault to store your keys and secrets.</span></span> <span data-ttu-id="26181-106">Uygulamalarınızı artık anahtarları ve gizli anahtarları, ancak bunun yerine kalıcı hale getirmek için bunları anahtar Kasası'nı gerektiğinde ister.</span><span class="sxs-lookup"><span data-stu-id="26181-106">Your applications no longer need to persist your keys or secrets, but rather will request them from the key vault as needed.</span></span> <span data-ttu-id="26181-107">Bu, anahtarlar ve gizli anahtarı ve gizli yönetim olanakları derecesini açar uygulamanızın davranışını etkilemeden güncelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="26181-107">This allows you to update keys and secrets without affecting the behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="26181-108">Bu makalede bir gizlilik bu durumda, bir uygulama tarafından erişilebilen bir Azure depolama hesabı anahtarı depolamak için Azure anahtar kasası kullanmaya ilişkin bir örnek anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="26181-108">This article walks through an example of using Azure Key Vault to store a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="26181-109">Ayrıca, bu depolama hesabı anahtarı zamanlanmış dönüşünü uyarlamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="26181-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="26181-110">Son olarak, anahtar kasası denetim günlüklerini izlemek ve beklenmeyen istekler yapıldığında uyarıları yükseltmek nasıl Tanıtımı anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="26181-110">Finally, it walks through a demonstration of how to monitor the key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="26181-111">Bu öğretici anahtar kasanızı ilk kurulumu ayrıntılı olarak açıklamak için tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="26181-111">This tutorial is not intended to explain in detail the initial setup of your key vault.</span></span> <span data-ttu-id="26181-112">Bu bilgi için bkz. [Azure Anahtar Kasası ile çalışmaya başlama](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="26181-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="26181-113">Platformlar arası komut satırı arabirimi yönergeleri için bkz: [anahtar kasası CLI kullanarak yönetme](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="26181-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="26181-114">Anahtar Kasası ayarlama</span><span class="sxs-lookup"><span data-stu-id="26181-114">Set up Key Vault</span></span>
<span data-ttu-id="26181-115">Bir gizli anahtar Kasası'nı almak bir uygulama etkinleştirmek için öncelikle gizli anahtar oluşturma ve, kasaya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="26181-115">To enable an application to retrieve a secret from Key Vault, you must first create the secret and upload it to your vault.</span></span> <span data-ttu-id="26181-116">Bu, bir Azure PowerShell oturumu başlatarak ve aşağıdaki komut ile Azure hesabınızda oturum açma gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="26181-116">This can be accomplished by starting an Azure PowerShell session and signing in to your Azure account with the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="26181-117">Açılır tarayıcı penceresinde Azure hesabı kullanıcı adınızı ve parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="26181-117">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="26181-118">PowerShell Bu hesapla ilişkili tüm abonelikleri alır.</span><span class="sxs-lookup"><span data-stu-id="26181-118">PowerShell will get all the subscriptions that are associated with this account.</span></span> <span data-ttu-id="26181-119">PowerShell varsayılan olarak birinciyi kullanır.</span><span class="sxs-lookup"><span data-stu-id="26181-119">PowerShell uses the first one by default.</span></span>

<span data-ttu-id="26181-120">Birden çok aboneliğiniz varsa, anahtar kasanızı oluşturmak için kullanılan bir tane belirtmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="26181-120">If you have multiple subscriptions, you might have to specify the one that was used to create your key vault.</span></span> <span data-ttu-id="26181-121">Hesabınız için abonelikleri görmek için aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="26181-121">Enter the following to see the subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="26181-122">Günlüğünü tutacağınız anahtar kasasıyla ilişkili aboneliği belirtmek için şunu girin:</span><span class="sxs-lookup"><span data-stu-id="26181-122">To specify the subscription that's associated with the key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="26181-123">Bu makalede, bir depolama hesabı anahtarı gizli depolama gösterilmektedir olduğundan, bu depolama hesabı anahtarı edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="26181-124">Gizli (Bu durumda, depolama hesabı anahtarınızı) aldıktan sonra güvenli bir dizeye dönüştürmek ve anahtar kasanızı'da bu değerle bir gizli anahtar oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-124">After retrieving your secret (in this case, your storage account key), you must convert that to a secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="26181-125">Ardından, oluşturduğunuz için gizli anahtar URI'sini Al.</span><span class="sxs-lookup"><span data-stu-id="26181-125">Next, get the URI for the secret you created.</span></span> <span data-ttu-id="26181-126">Gizli anahtarı almak için anahtar kasası çağırdığınızda bu bir sonraki adımda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="26181-126">This is used in a later step when you call the key vault to retrieve your secret.</span></span> <span data-ttu-id="26181-127">Aşağıdaki PowerShell komutunu çalıştırın ve gizli URI kimliği değeri not edin:</span><span class="sxs-lookup"><span data-stu-id="26181-127">Run the following PowerShell command and make note of the ID value, which is the secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-the-application"></a><span data-ttu-id="26181-128">Uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="26181-128">Set up the application</span></span>
<span data-ttu-id="26181-129">Depolanan gizli sahip olduğunuza göre almak ve kullanmak için kodu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26181-129">Now that you have a secret stored, you can use code to retrieve and use it.</span></span> <span data-ttu-id="26181-130">Bunu başarmak için gereken birkaç adım vardır.</span><span class="sxs-lookup"><span data-stu-id="26181-130">There are a few steps required to achieve this.</span></span> <span data-ttu-id="26181-131">İlk ve en önemli adım Azure Active Directory ile uygulamanızı kaydetme ve böylece uygulamanız gelen istekleri izin verebilir anahtar kasası, uygulama bilgilerinizi belirtiyor.</span><span class="sxs-lookup"><span data-stu-id="26181-131">The first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="26181-132">Uygulamanız aynı Azure Active Directory Kiracı anahtar kasanızı olarak oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-132">Your application must be created on the same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="26181-133">Azure Active Directory uygulamalar sekmesini açın.</span><span class="sxs-lookup"><span data-stu-id="26181-133">Open the applications tab of Azure Active Directory.</span></span>

![Azure Active Directory'de açık uygulamalar](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="26181-135">Seçin **Ekle** Azure Active Directory'yi bir uygulama eklemek için.</span><span class="sxs-lookup"><span data-stu-id="26181-135">Choose **ADD** to add an application to your Azure Active Directory.</span></span>

![EKLE'yi seçin](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="26181-137">Uygulama türü olarak bırakın **WEB uygulaması ve/veya WEB API** ve uygulamanızı bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="26181-137">Leave the application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Uygulama adı](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="26181-139">Uygulamanızı vermek bir **oturum açma URL** ve bir **uygulama kimliği URI'si**.</span><span class="sxs-lookup"><span data-stu-id="26181-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="26181-140">Bunlar bu tanıtım için istediğiniz herhangi bir şey olabilir ve bunlar daha sonra gerekirse değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="26181-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Gerekli URI'ler sağlar](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="26181-142">Uygulama Azure Active Directory'ye eklendikten sonra uygulama sayfasına gidersiniz.</span><span class="sxs-lookup"><span data-stu-id="26181-142">After the application is added to Azure Active Directory, you will be brought into the application page.</span></span> <span data-ttu-id="26181-143">Tıklatın **yapılandırma** sekmesini ve ardından bulmak ve kopyalama **istemci kimliği** değeri.</span><span class="sxs-lookup"><span data-stu-id="26181-143">Click the **Configure** tab and then find and copy the **Client ID** value.</span></span> <span data-ttu-id="26181-144">Sonraki adımlar için istemci Kimliğini not edin.</span><span class="sxs-lookup"><span data-stu-id="26181-144">Make note of the client ID for later steps.</span></span>

<span data-ttu-id="26181-145">Ardından, Azure Active Directory ile etkileşim kurabilmesi uygulamanız için bir anahtar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26181-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="26181-146">Bu altında oluşturabilir **anahtarları** bölümüne **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="26181-146">You can create this under the **Keys** section in the **Configuration** tab.</span></span> <span data-ttu-id="26181-147">Bir sonraki adımda kullanmak için Azure Active Directory uygulamanızdan yeni oluşturulan anahtarı not edin.</span><span class="sxs-lookup"><span data-stu-id="26181-147">Make note of the newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Azure Active Directory uygulama anahtarları](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="26181-149">Anahtar kasası uygulamanıza gelen tüm çağrıları kurmadan önce anahtar kasası uygulamanız ve izinlerini hakkında bildirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-149">Before establishing any calls from your application into the key vault, you must tell the key vault about your application and its permissions.</span></span> <span data-ttu-id="26181-150">Kasa adı ve istemci kimliği verir ve Azure Active Directory Uygulama aşağıdaki komutu alır **almak** anahtar kasanızı erişim uygulama.</span><span class="sxs-lookup"><span data-stu-id="26181-150">The following command takes the vault name and the client ID from your Azure Active Directory app and grants **Get** access to your key vault for the application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="26181-151">Bu noktada, uygulama çağrılarınızı oluşturmaya başlamak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="26181-151">At this point, you are ready to start building your application calls.</span></span> <span data-ttu-id="26181-152">Uygulamanızda Azure anahtar kasası ve Azure Active Directory ile etkileşim kurmak için gerekli NuGet paketleri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-152">In your application, you must install the NuGet packages required to interact with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="26181-153">Visual Studio Paket Yöneticisi konsolundan aşağıdaki komutları yazın.</span><span class="sxs-lookup"><span data-stu-id="26181-153">From the Visual Studio Package Manager console, enter the following commands.</span></span> <span data-ttu-id="26181-154">Bu makalede yazıda geçerli paketinin sürümünü, Azure Active Directory 3.10.305231913, olduğundan en son sürümünü onaylamak ve buna uygun olarak güncelleştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26181-154">At the writing of this article, the current version of the Azure Active Directory package is 3.10.305231913, so you might want to confirm the latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="26181-155">Uygulama kodunuz, Azure Active Directory kimlik doğrulama yöntemi tutmak için bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26181-155">In your application code, create a class to hold the method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="26181-156">Bu örnekte, o sınıfın adlı **yardımcı programları**.</span><span class="sxs-lookup"><span data-stu-id="26181-156">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="26181-157">Şu deyimi kullanarak aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="26181-157">Add the following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="26181-158">Ardından, Azure Active Directory'den JWT belirtecini almak için aşağıdaki yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="26181-158">Next, add the following method to retrieve the JWT token from Azure Active Directory.</span></span> <span data-ttu-id="26181-159">Bakım için sabit kodlanmış dize değerleri, web veya uygulama yapılandırması taşımak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26181-159">For maintainability, you may want to move the hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="26181-160">Anahtar kasası çağırın ve gizli değer almak için gerekli kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="26181-160">Add the necessary code to call Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="26181-161">Aşağıdaki ilk eklemelisiniz deyimi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="26181-161">First you must add the following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="26181-162">Anahtar kasası çağırma ve gizli anahtarı almak için yöntem çağrıları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="26181-162">Add the method calls to invoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="26181-163">Bu yöntemde, gizli, bir önceki adımda kaydettiğiniz URI sağlayın.</span><span class="sxs-lookup"><span data-stu-id="26181-163">In this method, you provide the secret URI that you saved in a previous step.</span></span> <span data-ttu-id="26181-164">Kullanımına dikkat edin **GetToken** yönteminden **yardımcı programları** daha önce oluşturduğunuz sınıfı.</span><span class="sxs-lookup"><span data-stu-id="26181-164">Note the use of the **GetToken** method from the **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="26181-165">Uygulamanızı çalıştırdığınızda, şimdi olmalısınız Azure Active Directory kimlik doğrulaması ve ardından Azure anahtar Kasası'gizli değer alma.</span><span class="sxs-lookup"><span data-stu-id="26181-165">When you run your application, you should now be authenticating to Azure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="26181-166">Azure otomasyonu kullanarak anahtar döndürme</span><span class="sxs-lookup"><span data-stu-id="26181-166">Key rotation using Azure Automation</span></span>
<span data-ttu-id="26181-167">Değerleri Azure anahtar kasası gizlilikleri olarak depolamak için bir dönüş stratejisi uygulamaya yönelik çeşitli seçenekleriniz vardır.</span><span class="sxs-lookup"><span data-stu-id="26181-167">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="26181-168">El ile işleminin bir parçası gizli döndürülüp, bunlar program aracılığıyla API çağrılarını kullanarak döndürülüp ya da bir otomasyon komut dosyası aracılığıyla Döndürülmüş.</span><span class="sxs-lookup"><span data-stu-id="26181-168">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="26181-169">Bir Azure depolama hesabı erişim anahtarı değiştirmek için bu makalede amaçları doğrultusunda, Azure Automation ile birlikte Azure PowerShell kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="26181-169">For the purposes of this article, you will be using Azure PowerShell combined with Azure Automation to change an Azure Storage Account access key.</span></span> <span data-ttu-id="26181-170">Ardından bu yeni anahtarla bir anahtar kasası gizli anahtarı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="26181-170">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="26181-171">Anahtar kasasına gizli değerlerini ayarlamak Azure Otomasyonu izin vermek için Azure Automation örneğinizi kurulan oluşturulduğu AzureRunAsConnection adlı bağlantı için istemci kimliği edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-171">To allow Azure Automation to set secret values in your key vault, you must get the client ID for the connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="26181-172">Bu kimliği seçerek bulabileceğiniz **varlıklar** , Azure Automation örneğinden.</span><span class="sxs-lookup"><span data-stu-id="26181-172">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="26181-173">Buradan, seçtiğiniz **bağlantıları** ve ardından **AzureRunAsConnection** hizmet ilkesi.</span><span class="sxs-lookup"><span data-stu-id="26181-173">From there, you choose **Connections** and then select the **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="26181-174">Not edin **uygulama kimliği**.</span><span class="sxs-lookup"><span data-stu-id="26181-174">Take note of the **Application ID**.</span></span>

![Azure otomasyon istemci kimliği](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="26181-176">İçinde **varlıklar**, seçin **modülleri**.</span><span class="sxs-lookup"><span data-stu-id="26181-176">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="26181-177">Gelen **modülleri**seçin **galeri**, arayın ve sonra ve **alma** güncelleştirilmiş sürümlerini her biri aşağıdaki modüller:</span><span class="sxs-lookup"><span data-stu-id="26181-177">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of the following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="26181-178">Bu makalede yazma sırasında yalnızca daha önce not ettiğiniz modülleri için aşağıdaki komut güncelleştirilmesi gereken.</span><span class="sxs-lookup"><span data-stu-id="26181-178">At the writing of this article, only the previously noted modules needed to be updated for the following script.</span></span> <span data-ttu-id="26181-179">Otomasyon işinizi başarısız olduğunu fark ederseniz, gerekli olan tüm modülleri ve bağımlılıklarını içeri aktardığınız onaylayın.</span><span class="sxs-lookup"><span data-stu-id="26181-179">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="26181-180">Azure Otomasyonu bağlantınız için uygulama kimliği aldıktan sonra bu uygulamayı kasanızdaki gizli anahtarları güncelleştirmek için erişimi olduğunu, anahtar kasanızı bildirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-180">After you have retrieved the application ID for your Azure Automation connection, you must tell your key vault that this application has access to update secrets in your vault.</span></span> <span data-ttu-id="26181-181">Bu aşağıdaki PowerShell komutuyla gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="26181-181">This can be accomplished with the following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="26181-182">Ardından, **Runbook'lar** Azure Automation örneği ve ardından altında **Runbook Ekle**.</span><span class="sxs-lookup"><span data-stu-id="26181-182">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="26181-183">**Hızlı Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="26181-183">Select **Quick Create**.</span></span> <span data-ttu-id="26181-184">Runbook'unuzda adlandırın ve seçin **PowerShell** runbook türü.</span><span class="sxs-lookup"><span data-stu-id="26181-184">Name your runbook and select **PowerShell** as the runbook type.</span></span> <span data-ttu-id="26181-185">Bir açıklama ekleme seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="26181-185">You have the option to add a description.</span></span> <span data-ttu-id="26181-186">Son olarak, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="26181-186">Finally, click **Create**.</span></span>

![Runbook oluşturma](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="26181-188">Yeni runbook'unuz Düzenleyicisi bölmesinde aşağıdaki PowerShell betiğini yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="26181-188">Paste the following PowerShell script in the editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get the connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in to Azure..."
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

#Optionally you may set the following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for the storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="26181-189">Düzenleyici bölmesinden seçin **Test bölmesi** kodunuzu test etmek için.</span><span class="sxs-lookup"><span data-stu-id="26181-189">From the editor pane, choose **Test pane** to test your script.</span></span> <span data-ttu-id="26181-190">Komut hatasız çalışmaya başladıktan sonra seçebileceğiniz **Yayımla**, ve daha sonra geri runbook yapılandırma bölmesinde runbook için bir zamanlama uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26181-190">Once the script is running without error, you can select **Publish**, and then you can apply a schedule for the runbook back in the runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="26181-191">Anahtar kasası denetim ardışık düzen</span><span class="sxs-lookup"><span data-stu-id="26181-191">Key Vault auditing pipeline</span></span>
<span data-ttu-id="26181-192">Bir anahtar kasasını ayarladığınızda, anahtar Kasası'na erişim isteklerini günlükleri toplamak için denetimi kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26181-192">When you set up a key vault, you can turn on auditing to collect logs on access requests made to the key vault.</span></span> <span data-ttu-id="26181-193">Bu günlükler belirlenmiş bir Azure depolama hesabında depolanır ve çıkışı, izlenen ve analiz çekebilir.</span><span class="sxs-lookup"><span data-stu-id="26181-193">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="26181-194">Aşağıdaki senaryoda, web uygulamasının uygulama kimliği eşleşen bir uygulama parolaları kasadan aldığında bir e-posta göndermek için bir işlem hattı oluşturmak için Azure işlevleri, Azure mantıksal uygulamaları ve anahtar kasası denetim günlüklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="26181-194">The following scenario uses Azure functions, Azure logic apps, and key vault audit logs to create a pipeline to send an email when an app that does match the app ID of the web app retrieves secrets from the vault.</span></span>

<span data-ttu-id="26181-195">İlk olarak, anahtar kasanızı günlüğü etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-195">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="26181-196">Bu aşağıdaki PowerShell komutları yapılabilir (tam Ayrıntılar adresindeki görülme [anahtar kasası günlüğü](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="26181-196">This can be done via the following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="26181-197">Bu özellik etkinleştirildikten sonra belirlenen storage hesabınıza toplama başlangıç denetim günlüklerini.</span><span class="sxs-lookup"><span data-stu-id="26181-197">After this is enabled, audit logs start collecting into the designated storage account.</span></span> <span data-ttu-id="26181-198">Bu günlükler olayları anahtar kasalarınıza erişilen nasıl ve ne zaman ve kim tarafından içerir.</span><span class="sxs-lookup"><span data-stu-id="26181-198">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="26181-199">Günlük bilgilerinize anahtar kasası işleminden sonra 10 dakika erişebilir.</span><span class="sxs-lookup"><span data-stu-id="26181-199">You can access your logging information 10 minutes after the key vault operation.</span></span> <span data-ttu-id="26181-200">Genellikle bu değerden daha hızlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="26181-200">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="26181-201">Sonraki adım [bir Azure hizmet veri yolu kuyruğu oluşturma](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="26181-201">The next step is to [create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="26181-202">Anahtar kasası denetim günlüklerini burada gönderilen budur.</span><span class="sxs-lookup"><span data-stu-id="26181-202">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="26181-203">Denetim günlüğü iletileri sırada, mantıksal uygulama bunları alır ve bunlar üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="26181-203">When the audit log messages are in the queue, the logic app picks them up and acts on them.</span></span> <span data-ttu-id="26181-204">Hizmet veri yolu aşağıdaki adımlarla oluşturun:</span><span class="sxs-lookup"><span data-stu-id="26181-204">Create a service bus with the following steps:</span></span>

1. <span data-ttu-id="26181-205">(Bu, 2. adımı atla için kullanmak istediğiniz bir zaten varsa) bir hizmet veri yolu ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26181-205">Create a Service Bus namespace (if you already have one that you want to use for this, skip to Step 2).</span></span>
2. <span data-ttu-id="26181-206">Azure Portalı'nda hizmet veri yoluna göz atın ve sırada oluşturmak istediğiniz ad alanını seçin.</span><span class="sxs-lookup"><span data-stu-id="26181-206">Browse to the service bus in the Azure portal and select the namespace you want to create the queue in.</span></span>
3. <span data-ttu-id="26181-207">Seçin **yeni** ve **hizmet veri yolu > sıra** ve gerekli ayrıntıları girin.</span><span class="sxs-lookup"><span data-stu-id="26181-207">Select **New** and choose **Service Bus > Queue** and enter the required details.</span></span>
4. <span data-ttu-id="26181-208">Service Bus bağlantı bilgilerini ad alanını seçerek ve tıklatarak seçin **bağlantı bilgilerini**.</span><span class="sxs-lookup"><span data-stu-id="26181-208">Select the Service Bus connection information by choosing the namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="26181-209">Bu bilgiler için sonraki bölüme gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-209">You will need this information for the next section.</span></span>

<span data-ttu-id="26181-210">Ardından, [bir Azure işlevi oluşturma](../azure-functions/functions-create-first-azure-function.md) anahtar kasası günlükleri depolama hesabındaki yoklamak ve yeni olayları seçin.</span><span class="sxs-lookup"><span data-stu-id="26181-210">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) to poll key vault logs within the storage account and pick up new events.</span></span> <span data-ttu-id="26181-211">Bu bir zamanlamaya göre tetiklenen bir işlev olacaktır.</span><span class="sxs-lookup"><span data-stu-id="26181-211">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="26181-212">Bir Azure işlevi oluşturmak için seçtiğiniz **yeni > işlev uygulaması** Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="26181-212">To create an Azure function, choose **New > Function App** in the Azure portal.</span></span> <span data-ttu-id="26181-213">Oluşturma sırasında var olan bir barındırma planı kullanın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26181-213">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="26181-214">Ayrıca, dinamik barındırmak için tercih.</span><span class="sxs-lookup"><span data-stu-id="26181-214">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="26181-215">İşlevi barındırma seçenekleri hakkında daha fazla ayrıntı bulunabilir [Azure işlevlerini ölçeklendirme](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="26181-215">More details on Function hosting options can be found at [How to scale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="26181-216">Azure işlevi oluşturulduğunda, kendisine gidin ve bir süreölçer işlevi C seçip\#.</span><span class="sxs-lookup"><span data-stu-id="26181-216">When the Azure function is created, navigate to it and choose a timer function and C\#.</span></span> <span data-ttu-id="26181-217">Ardından **bu işlev oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="26181-217">Then click **Create this function**.</span></span>

![Azure işlevleri Başlat dikey penceresi](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="26181-219">Üzerinde **geliştirme** sekmesinde, run.csx kodu aşağıdakilerle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="26181-219">On the **Develop** tab, replace the run.csx code with the following:</span></span>

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
            log.Verbose($"Sync point file didnt have a date. Setting to now.");
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

            //required to order by time as they may not be in the file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending to ServiceBus, use the payloadStream and set keeporiginal to true
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

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="26181-220">Anahtar kasası günlükleri yazılacağı depolama hesabınıza işaret etmek için önceki kod değişkenlerde, daha önce oluşturduğunuz hizmet veri yolu ve anahtar kasası depolama günlükleri belirli yolu değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="26181-220">Make sure to replace the variables in the preceding code to point to your storage account where the key vault logs are written, the service bus you created earlier, and the specific path to the key vault storage logs.</span></span>
>
>

<span data-ttu-id="26181-221">İşlev anahtar kasası günlükleri yazılacağı en son günlük dosyasını depolama hesabından seçer, bu dosyanın en son olayların alan ve Service Bus kuyruğuna iter.</span><span class="sxs-lookup"><span data-stu-id="26181-221">The function picks up the latest log file from the storage account where the key vault logs are written, grabs the latest events from that file, and pushes them to a Service Bus queue.</span></span> <span data-ttu-id="26181-222">Tek bir dosyada birden çok olay olabilir beri işlevi de çekilmiş yukarı son olay zaman damgası belirlemek için bakan bir sync.txt dosyası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-222">Since a single file could have multiple events, you should create a sync.txt file that the function also looks at to determine the time stamp of the last event that was picked up.</span></span> <span data-ttu-id="26181-223">Bu, birden çok kez aynı olay gönderme yok sağlar.</span><span class="sxs-lookup"><span data-stu-id="26181-223">This ensures that you don't push the same event multiple times.</span></span> <span data-ttu-id="26181-224">Bu sync.txt dosya son karşılaşılan olayı için bir zaman damgası içeriyor.</span><span class="sxs-lookup"><span data-stu-id="26181-224">This sync.txt file contains a timestamp for the last encountered event.</span></span> <span data-ttu-id="26181-225">Yüklendiğinde, günlükleri, doğru sıralanmıştır emin olmak için zaman damgasını tabanlı sıralanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-225">The logs, when loaded, have to be sorted based on the timestamp to ensure they are ordered correctly.</span></span>

<span data-ttu-id="26181-226">Bu işlev için birkaç Azure işlevleri kutusuna dışında bulunmayan ek kitaplıklara başvuru.</span><span class="sxs-lookup"><span data-stu-id="26181-226">For this function, we reference a couple of additional libraries that are not available out of the box in Azure Functions.</span></span> <span data-ttu-id="26181-227">Azure işlevleri, bunları çıkarmak için ihtiyacımız bunlar için NuGet kullanma.</span><span class="sxs-lookup"><span data-stu-id="26181-227">To include these, we need Azure Functions to pull them using NuGet.</span></span> <span data-ttu-id="26181-228">Seçin **dosyaları görüntüle** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="26181-228">Choose the **View Files** option.</span></span>

![Görünüm dosyaları seçeneği](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="26181-230">Ve aşağıdaki içeriğe sahip project.json adlı bir dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="26181-230">And add a file called project.json with following content:</span></span>

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
<span data-ttu-id="26181-231">Bağlı **kaydetmek**, Azure işlevleri, gerekli ikili dosyaları indirir.</span><span class="sxs-lookup"><span data-stu-id="26181-231">Upon **Save**, Azure Functions will download the required binaries.</span></span>

<span data-ttu-id="26181-232">Geçiş **tümleştir** sekmesinde ve Zamanlayıcı parametre işlev içinde kullanmak için anlamlı bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="26181-232">Switch to the **Integrate** tab and give the timer parameter a meaningful name to use within the function.</span></span> <span data-ttu-id="26181-233">İsteğe bağlı olarak önceki kodda çağrılacak Zamanlayıcı bekliyor *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="26181-233">In the preceding code, it expects the timer to be called *myTimer*.</span></span> <span data-ttu-id="26181-234">Belirtin bir [CRON ifade](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) gibi: 0 \* \* \* \* \* bir dakika çalıştırılacak işlev neden olacak Zamanlayıcı için.</span><span class="sxs-lookup"><span data-stu-id="26181-234">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for the timer that will cause the function to run once a minute.</span></span>

<span data-ttu-id="26181-235">Aynı **tümleştir** sekmesinde, türündeki bir girdi ekleme **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="26181-235">On the same **Integrate** tab, add an input of the type **Azure Blob Storage**.</span></span> <span data-ttu-id="26181-236">Bu, işlev tarafından aranan son olay zaman damgası içeren sync.txt dosyasını işaret edecek.</span><span class="sxs-lookup"><span data-stu-id="26181-236">This will point to the sync.txt file that contains the timestamp of the last event looked at by the function.</span></span> <span data-ttu-id="26181-237">Bu işlev parametre adı tarafından içinde kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="26181-237">This will be available within the function by the parameter name.</span></span> <span data-ttu-id="26181-238">Önceki kodda, parametre adı olarak Azure Blob Storage girdi bekliyor *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="26181-238">In the preceding code, the Azure Blob Storage input expects the parameter name to be *inputBlob*.</span></span> <span data-ttu-id="26181-239">Sync.txt dosya nerede bulunacağı depolama hesabını seçin (aynı veya farklı bir depolama hesabı olabilir).</span><span class="sxs-lookup"><span data-stu-id="26181-239">Choose the storage account where the sync.txt file will reside (it could be the same or a different storage account).</span></span> <span data-ttu-id="26181-240">Yol alanı nerede dosya biçimi {container-name}/path/to/sync.txt. yaşıyor yolunu belirtin</span><span class="sxs-lookup"><span data-stu-id="26181-240">In the path field, provide the path where the file lives in the format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="26181-241">Bir çıkış türü ekleme *Azure Blob Storage* çıktı.</span><span class="sxs-lookup"><span data-stu-id="26181-241">Add an output of the type *Azure Blob Storage* output.</span></span> <span data-ttu-id="26181-242">Bu sync.txt dosyası girdide tanımlı işaret edecek.</span><span class="sxs-lookup"><span data-stu-id="26181-242">This will point to the sync.txt file you defined in the input.</span></span> <span data-ttu-id="26181-243">Zaman damgası'Aranan en son olay yazmak için bu işlev tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="26181-243">This is used by the function to write the timestamp of the last event looked at.</span></span> <span data-ttu-id="26181-244">Önceki kod çağrılacak Bu parametre bekliyor *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="26181-244">The preceding code expects this parameter to be called *outputBlob*.</span></span>

<span data-ttu-id="26181-245">Bu noktada, işlevi hazırdır.</span><span class="sxs-lookup"><span data-stu-id="26181-245">At this point, the function is ready.</span></span> <span data-ttu-id="26181-246">Dönmeyi emin olun **geliştirme** sekmesinde ve kod kaydedin.</span><span class="sxs-lookup"><span data-stu-id="26181-246">Make sure to switch back to the **Develop** tab and save the code.</span></span> <span data-ttu-id="26181-247">Derleme hataları için çıktı penceresini denetleyin ve uygun şekilde düzeltin.</span><span class="sxs-lookup"><span data-stu-id="26181-247">Check the output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="26181-248">Kodu derler, ardından kod şimdi anahtar kasası günlükleri dakikada denetleniyor ve tanımlanmış hizmet veri yolu kuyruğu üzerine yeni olaylar Ftp'den.</span><span class="sxs-lookup"><span data-stu-id="26181-248">If the code compiles, then the code should now be checking the key vault logs every minute and pushing any new events onto the defined Service Bus queue.</span></span> <span data-ttu-id="26181-249">Günlük kaydı bilgileri Günlük penceresine işlevi her başlatılışında yazamadı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-249">You should see logging information write out to the log window every time the function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="26181-250">Azure mantıksal uygulama</span><span class="sxs-lookup"><span data-stu-id="26181-250">Azure logic app</span></span>
<span data-ttu-id="26181-251">Sonraki işlev Service Bus kuyruğuna Ftp'den, içeriği ayrıştırır ve eşleşen bir koşula göre bir e-posta gönderir olayları seçer bir Azure mantıksal uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="26181-251">Next you must create an Azure logic app that picks up the events that the function is pushing to the Service Bus queue, parses the content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="26181-252">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md) giderek **yeni > mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="26181-252">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going to **New > Logic App**.</span></span>

<span data-ttu-id="26181-253">Mantıksal uygulama oluşturulduktan sonra dosyayı bulun ve seçin **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="26181-253">Once the logic app is created, navigate to it and choose **edit**.</span></span> <span data-ttu-id="26181-254">Mantıksal uygulama düzenleyicisinde seçin **hizmet veri yolu kuyruğu** ve Service Bus kuyruğuna bağlanmak için kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="26181-254">Within the logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials to connect it to the queue.</span></span>

![Azure Logic App Service Bus](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="26181-256">Sonraki seçin **bir koşul eklemek**.</span><span class="sxs-lookup"><span data-stu-id="26181-256">Next choose **Add a condition**.</span></span> <span data-ttu-id="26181-257">Koşul Gelişmiş düzenleyicisine geçin ve APP_ID web uygulamanızı gerçek APP_ID ile değiştirerek aşağıdaki kodu girin:</span><span class="sxs-lookup"><span data-stu-id="26181-257">In the condition, switch to the advanced editor and enter the following code, replacing APP_ID with the actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="26181-258">Bu ifade temelde döndürür **false** varsa *AppID* (Service Bus ileti gövdesi olan)'ndan gelen olayı değil *AppID* uygulamanın.</span><span class="sxs-lookup"><span data-stu-id="26181-258">This expression essentially returns **false** if the *appid* from the incoming event (which is the body of the Service Bus message) is not the *appid* of the app.</span></span>

<span data-ttu-id="26181-259">Şimdi, altında bir eylem oluşturun **Öyle değilse, hiçbir şey yapma**.</span><span class="sxs-lookup"><span data-stu-id="26181-259">Now, create an action under **If no, do nothing**.</span></span>

![Azure mantıksal uygulama eylemi seçin](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="26181-261">Eylem için **Office 365 - e-postası gönderme**.</span><span class="sxs-lookup"><span data-stu-id="26181-261">For the action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="26181-262">Tanımlanan koşulu döndürdüğünde göndermek için e-posta oluşturmak için alanları doldurun **false**.</span><span class="sxs-lookup"><span data-stu-id="26181-262">Fill out the fields to create an email to send when the defined condition returns **false**.</span></span> <span data-ttu-id="26181-263">Office 365 yoksa aynı sonucu elde etmek için alternatifleri görünebilir.</span><span class="sxs-lookup"><span data-stu-id="26181-263">If you do not have Office 365, you could look at alternatives to achieve the same results.</span></span>

<span data-ttu-id="26181-264">Bu noktada yeni anahtar kasası denetim günlükleri için bir dakika benzeyen bir uçtan uca ardışık vardır.</span><span class="sxs-lookup"><span data-stu-id="26181-264">At this point, you have an end to end pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="26181-265">Bu yeni günlükler bulduğu bir service bus kuyruğuna iter.</span><span class="sxs-lookup"><span data-stu-id="26181-265">It pushes new logs it finds to a service bus queue.</span></span> <span data-ttu-id="26181-266">Mantıksal uygulama yeni bir ileti sıraya adlandırıldığını geldiğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="26181-266">The logic app is triggered when a new message lands in the queue.</span></span> <span data-ttu-id="26181-267">Varsa *AppID* içinde olay çağrı yapan uygulamanın uygulama Kimliğini eşleşmiyor, bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="26181-267">If the *appid* within the event does not match the app ID of the calling application, it sends an email.</span></span>
