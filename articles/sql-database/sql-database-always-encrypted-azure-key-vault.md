---
title: "Her zaman şifreli: SQL veritabanı - Azure anahtar kasası | Microsoft Docs"
description: "Bu makalede, veri şifreleme kullanarak bir SQL veritabanında toosecure hassas verileri her zaman şifreli Sihirbazı SQL Server Management Studio'da nasıl hello gösterir. Bunu nasıl yapacağınızı gösterir yönergeleri de içerir toostore Azure anahtar Kasası'nda her şifreleme anahtarı."
keywords: "veri şifreleme, şifreleme anahtarı, bulut şifreleme"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="56cd1-105">Her zaman şifreli: SQL veritabanındaki hassas verileri korumak ve Azure anahtar kasası, şifreleme anahtarlarını saklamak</span><span class="sxs-lookup"><span data-stu-id="56cd1-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="56cd1-106">Bu makalede nasıl hello kullanarak veri şifrelemesi ile toosecure hassas verileri bir SQL veritabanı gösterilmektedir [her zaman şifreli Sihirbazı](https://msdn.microsoft.com/library/mt459280.aspx) içinde [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="56cd1-106">This article shows you how toosecure sensitive data in a SQL database with data encryption using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="56cd1-107">Bunu nasıl yapacağınızı gösterir yönergeleri de içerir toostore Azure anahtar Kasası'nda her şifreleme anahtarı.</span><span class="sxs-lookup"><span data-stu-id="56cd1-107">It also includes instructions that will show you how toostore each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="56cd1-108">Her zaman şifreli bir yeni veri şifreleme Azure SQL veritabanındaki bir teknolojidir ve yardımcı olan bir SQL Server ve istemci ve sunucu arasında hello veri kullanımdayken taşıma sırasında rest hello sunucusunda hassas verileri koruyun.</span><span class="sxs-lookup"><span data-stu-id="56cd1-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use.</span></span> <span data-ttu-id="56cd1-109">Her zaman şifreli hassas verileri asla hello veritabanı sistem içinde düz metin olarak görünmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="56cd1-109">Always Encrypted ensures that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="56cd1-110">Veri şifreleme yapılandırdıktan sonra yalnızca istemci uygulamaları ya da erişim toohello anahtarlara sahip uygulama sunucuları düz metin verilere erişebilir.</span><span class="sxs-lookup"><span data-stu-id="56cd1-110">After you configure data encryption, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="56cd1-111">Ayrıntılı bilgi için bkz: [(veritabanı altyapısı)'her zaman şifreli](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="56cd1-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="56cd1-112">Merhaba veritabanı toouse her zaman şifreli yapılandırdıktan sonra C# Visual Studio toowork hello şifrelenmiş verilerle birlikte bir istemci uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="56cd1-112">After you configure hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="56cd1-113">Bu makalede Hello adımları izleyin ve öğrenin nasıl bir Azure SQL veritabanı için her zaman şifreli yukarı tooset.</span><span class="sxs-lookup"><span data-stu-id="56cd1-113">Follow hello steps in this article and learn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="56cd1-114">Bu makalede nasıl tooperform hello aşağıdaki görevleri öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="56cd1-114">In this article you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="56cd1-115">Kullanım hello her zaman şifreli sihirbazında SSMS toocreate [her zaman şifreli anahtarları](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="56cd1-115">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="56cd1-116">Oluşturma bir [sütun ana anahtar (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="56cd1-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="56cd1-117">Oluşturma bir [sütun şifreleme anahtarı (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="56cd1-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="56cd1-118">Bir veritabanı tablosu oluşturmak ve sütunları şifreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56cd1-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="56cd1-119">Ekler, seçer ve şifrelenmiş hello sütunları verileri görüntüleyen bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="56cd1-119">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56cd1-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="56cd1-120">Prerequisites</span></span>
<span data-ttu-id="56cd1-121">Bu öğretici için ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="56cd1-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="56cd1-122">Bir Azure hesabı ve aboneliği</span><span class="sxs-lookup"><span data-stu-id="56cd1-122">An Azure account and subscription.</span></span> <span data-ttu-id="56cd1-123">Yoksa, kaydolun bir [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56cd1-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="56cd1-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) sürüm 13.0.700.242 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="56cd1-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="56cd1-125">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) veya üstünü (Merhaba istemci bilgisayarda).</span><span class="sxs-lookup"><span data-stu-id="56cd1-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="56cd1-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="56cd1-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="56cd1-127">[Azure PowerShell](/powershell/azure/overview), sürüm 1.0 veya üstü.</span><span class="sxs-lookup"><span data-stu-id="56cd1-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="56cd1-128">Tür **(Get-Module azure - listavailable birlikte). Sürüm** toosee PowerShell sürümünü çalıştırıyor.</span><span class="sxs-lookup"><span data-stu-id="56cd1-128">Type **(Get-Module azure -ListAvailable).Version** toosee what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a><span data-ttu-id="56cd1-129">İstemci uygulama tooaccess hello SQL veritabanı hizmetini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="56cd1-129">Enable your client application tooaccess hello SQL Database service</span></span>
<span data-ttu-id="56cd1-130">İstemci uygulaması tooaccess hello SQL veritabanı hizmetinin hello gerekli kimlik doğrulama ve alınırken hello ayarlayarak etkinleştirmelisiniz *ClientID* ve *gizli* tooauthenticate gerekir koddan hello uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="56cd1-130">You must enable your client application tooaccess hello SQL Database service by setting up hello required authentication and acquiring hello *ClientId* and *Secret* that you will need tooauthenticate your application in hello following code.</span></span>

1. <span data-ttu-id="56cd1-131">Açık hello [Klasik Azure portalı](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="56cd1-131">Open hello [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="56cd1-132">Seçin **Active Directory** ve uygulamanız kullanacak hello Active Directory örneğine'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-132">Select **Active Directory** and click hello Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="56cd1-133">Tıklatın **uygulamaları**ve ardından **eklemek**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="56cd1-134">Uygulamanız için bir ad yazın (örneğin: *myClientApp*), select **WEB uygulaması**ve hello ok toocontinue'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click hello arrow toocontinue.</span></span>
5. <span data-ttu-id="56cd1-135">Hello için **oturum açma URL** ve **uygulama kimliği URI'si** geçerli bir URL yazın (örneğin, *http://myClientApp*) ve devam edin.</span><span class="sxs-lookup"><span data-stu-id="56cd1-135">For hello **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="56cd1-136">Tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="56cd1-137">Kopyalama, **istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="56cd1-138">(Bu değer, kodunuzda daha sonra gerekecektir.)</span><span class="sxs-lookup"><span data-stu-id="56cd1-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="56cd1-139">Merhaba, **anahtarları** bölümünde, select **1 yıl** hello gelen **seçin süresi** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="56cd1-139">In hello **keys** section, select **1 year** from hello  **Select duration** drop-down list.</span></span> <span data-ttu-id="56cd1-140">(Adım 13 kaydettikten sonra hello anahtar kopyalayacak.)</span><span class="sxs-lookup"><span data-stu-id="56cd1-140">(You will copy hello key after you save in step 13.)</span></span>
9. <span data-ttu-id="56cd1-141">Aşağı kaydırın ve tıklatın **uygulama eklemek**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="56cd1-142">Bırakın **Göster** çok ayarlamak**Microsoft Apps** seçip **Microsoft Azure Hizmet Yönetimi API'si**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-142">Leave **SHOW** set too**Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="56cd1-143">Merhaba onay işareti toocontinue'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-143">Click hello checkmark toocontinue.</span></span>
11. <span data-ttu-id="56cd1-144">Seçin **erişim Azure hizmet yönetimi...**  hello gelen **izinlere temsilci** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="56cd1-144">Select **Access Azure Service Management...** from hello **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="56cd1-145">**KAYDET**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="56cd1-146">Sonlandığında kaydetme Hello sonra hello anahtar değeri hello kopyalama **anahtarları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="56cd1-146">After hello save finishes, copy hello key value in hello **keys** section.</span></span> <span data-ttu-id="56cd1-147">(Bu değer, kodunuzda daha sonra gerekecektir.)</span><span class="sxs-lookup"><span data-stu-id="56cd1-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-toostore-your-keys"></a><span data-ttu-id="56cd1-148">Bir anahtar kasası toostore anahtarlarınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="56cd1-148">Create a key vault toostore your keys</span></span>
<span data-ttu-id="56cd1-149">İstemci uygulamanızı yapılandırılmış ve istemci Kimliğiniz sahip olduğunuza zaman toocreate bir anahtar kasası olan ve hello Kasası'nın gizli anahtarları (Merhaba her zaman şifreli anahtarlar) ve uygulamanızı erişebilmesi için erişim ilkesi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-149">Now that your client app is configured and you have your client ID, it's time toocreate a key vault and configure its access policy so you and your application can access hello vault's secrets (hello Always Encrypted keys).</span></span> <span data-ttu-id="56cd1-150">Merhaba *oluşturma*, *almak*, *listesi*, *oturum*, *doğrulayın*, *wrapKey*, ve *unwrapKey* yeni bir sütun ana anahtar oluşturma ve şifreleme SQL Server Management Studio ile ayarlamak için gerekli izinleri.</span><span class="sxs-lookup"><span data-stu-id="56cd1-150">hello *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="56cd1-151">Komut dosyası izleyen hello çalıştırarak, bir anahtar kasası hızlı bir şekilde oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56cd1-151">You can quickly create a key vault by running hello following script.</span></span> <span data-ttu-id="56cd1-152">Ayrıntılı bir açıklaması ve bu cmdlet'leri ve oluşturma ve bir anahtar kasası yapılandırma hakkında daha fazla bilgi için bkz: [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="56cd1-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="56cd1-153">Boş bir SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="56cd1-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="56cd1-154">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="56cd1-154">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="56cd1-155">Çok Git**yeni** > **veri + depolama** > **SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-155">Go too**New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="56cd1-156">Oluşturma bir **boş** adlı veritabanı **Clinic** yeni veya var olan bir sunucuda.</span><span class="sxs-lookup"><span data-stu-id="56cd1-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="56cd1-157">Toocreate hello Azure portal, bir veritabanına nasıl görürüm hakkında ayrıntılı yönergeler için [ilk Azure SQL veritabanınızı](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="56cd1-157">For detailed directions about how toocreate a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Boş veritabanı oluşturma](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="56cd1-159">Bağlantı dizesi hello hello veritabanı oluşturduktan sonra daha sonra hello öğreticide toohello yeni Clinic veritabanı ve kopyalama hello bağlantı dizesi bu nedenle göz atın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-159">You will need hello connection string later in hello tutorial, so after you create hello database, browse toohello new  Clinic database and copy hello connection string.</span></span> <span data-ttu-id="56cd1-160">Herhangi bir zamanda hello bağlantı dizesi elde edebilirsiniz, ancak bunu kolay toocopy hello Azure portalı içinde.</span><span class="sxs-lookup"><span data-stu-id="56cd1-160">You can get hello connection string at any time, but it's easy toocopy it in hello Azure portal.</span></span>

1. <span data-ttu-id="56cd1-161">Çok Git**SQL veritabanları** > **Clinic** > **veritabanı bağlantı dizelerini Göster**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-161">Go too**SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="56cd1-162">Merhaba bağlantı dizesini kopyalayın **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-162">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Merhaba bağlantı dizesini kopyalayın](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="56cd1-164">SSMS ile toohello veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="56cd1-164">Connect toohello database with SSMS</span></span>
<span data-ttu-id="56cd1-165">SSMS açın ve toohello sunucu hello Clinic veritabanıyla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="56cd1-165">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="56cd1-166">SSMS açın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-166">Open SSMS.</span></span> <span data-ttu-id="56cd1-167">(Çok Git**Bağlan** > **veritabanı altyapısı** tooopen hello **tooServer bağlanmak** açık değilse, pencere.)</span><span class="sxs-lookup"><span data-stu-id="56cd1-167">(Go too**Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it isn't open.)</span></span>
2. <span data-ttu-id="56cd1-168">Sunucu adı ve kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="56cd1-168">Enter your server name and credentials.</span></span> <span data-ttu-id="56cd1-169">Merhaba sunucu adı hello SQL veritabanı dikey bulunabilir ve daha önce kopyaladığınız hello bağlantı dizesinde.</span><span class="sxs-lookup"><span data-stu-id="56cd1-169">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="56cd1-170">Tür hello tam sunucu adını dahil olmak üzere *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="56cd1-170">Type hello complete server name, including *database.windows.net*.</span></span>
   
    ![Merhaba bağlantı dizesini kopyalayın](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="56cd1-172">Merhaba, **yeni güvenlik duvarı kuralı** penceresi açılır oturum içinde tooAzure ve let SSMS sizin için yeni bir güvenlik duvarı kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="56cd1-172">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="56cd1-173">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="56cd1-173">Create a table</span></span>
<span data-ttu-id="56cd1-174">Bu bölümde, bir tablo toohold Hasta verileri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="56cd1-174">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="56cd1-175">Başlangıçta değil şifrelenmiş--hello sonraki bölümde şifreleme yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="56cd1-175">It's not initially encrypted--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="56cd1-176">Genişletme **veritabanları**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="56cd1-177">Sağ hello **Clinic** veritabanı ve tıklatın **yeni sorgu**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-177">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="56cd1-178">Transact-SQL (T-SQL) hello yeni sorgu penceresine aşağıdaki Yapıştır hello ve **yürütme** onu.</span><span class="sxs-lookup"><span data-stu-id="56cd1-178">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="56cd1-179">(Her zaman şifreli yapılandırma) sütunları şifrele</span><span class="sxs-lookup"><span data-stu-id="56cd1-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="56cd1-180">SSMS kolayca ayarlayarak hello sütun ana anahtar, sütun şifreleme anahtarı ve şifrelenmiş sütunlar, her zaman şifreli yapılandırmanıza yardımcı olacak bir sihirbaz sağlar.</span><span class="sxs-lookup"><span data-stu-id="56cd1-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up hello column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="56cd1-181">Genişletme **veritabanları** > **Clinic** > **tabloları**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="56cd1-182">Sağ hello **hastalar** tablo ve seçin **şifrelemek sütunları** tooopen hello her zaman şifreli Sihirbazı:</span><span class="sxs-lookup"><span data-stu-id="56cd1-182">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Sütunları şifrele](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="56cd1-184">Merhaba her zaman şifreli Sihirbazı'nı içerir bölümleri aşağıdaki hello: **sütun seçimi**, **ana anahtar yapılandırma**, **doğrulama**, ve **özeti** .</span><span class="sxs-lookup"><span data-stu-id="56cd1-184">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="56cd1-185">Sütun Seçimi</span><span class="sxs-lookup"><span data-stu-id="56cd1-185">Column Selection</span></span>
<span data-ttu-id="56cd1-186">Tıklatın **sonraki** hello üzerinde **giriş** sayfa tooopen hello **sütun seçimi** sayfası.</span><span class="sxs-lookup"><span data-stu-id="56cd1-186">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="56cd1-187">Bu sayfada, hangi sütunların seçecektir tooencrypt, istediğiniz [hello şifreleme türünü ve hangi sütun şifreleme anahtarı (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="56cd1-187">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="56cd1-188">Şifreleme **SSN** ve **doğum tarihi** bilgi için her bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="56cd1-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="56cd1-189">Merhaba SSN sütun eşitlik aramaları, birleştirmeler ve Grupla destekleyen belirleyici şifreleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="56cd1-189">hello SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="56cd1-190">Merhaba doğum tarihi sütun işlemlerini desteklemeyen rastgele şifreleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="56cd1-190">hello BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="56cd1-191">Set hello **şifreleme türü** hello SSN sütun için çok**Deterministic** ve doğum tarihi sütun çok hello**Randomized**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-191">Set hello **Encryption Type** for hello SSN column too**Deterministic** and hello BirthDate column too**Randomized**.</span></span> <span data-ttu-id="56cd1-192">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-192">Click **Next**.</span></span>

![Sütunları şifrele](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="56cd1-194">Ana anahtar yapılandırma</span><span class="sxs-lookup"><span data-stu-id="56cd1-194">Master Key Configuration</span></span>
<span data-ttu-id="56cd1-195">Merhaba **ana anahtar yapılandırma** sayfasıdır CMK ve select hello anahtar depolama sağlayıcısı hello CMK depolanacağı ayarladığınız.</span><span class="sxs-lookup"><span data-stu-id="56cd1-195">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="56cd1-196">Şu anda bir CMK hello Windows sertifika deposu, Azure anahtar kasası veya bir donanım güvenlik modülü (HSM) depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56cd1-196">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="56cd1-197">Bu öğreticide gösterilmiştir nasıl toostore anahtarlarınızı Azure anahtar Kasası'nda.</span><span class="sxs-lookup"><span data-stu-id="56cd1-197">This tutorial shows how toostore your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="56cd1-198">Seçin **Azure anahtar kasası**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="56cd1-199">Merhaba İstenen anahtar kasası hello aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="56cd1-199">Select hello desired key vault from hello drop-down list.</span></span>
3. <span data-ttu-id="56cd1-200">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-200">Click **Next**.</span></span>

![Ana anahtar yapılandırma](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="56cd1-202">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="56cd1-202">Validation</span></span>
<span data-ttu-id="56cd1-203">Merhaba sütunları şifrelemek veya bir PowerShell komut dosyası toorun daha sonra kaydedin.</span><span class="sxs-lookup"><span data-stu-id="56cd1-203">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="56cd1-204">Bu öğretici için seçin **toofinish şimdi devam** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-204">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="56cd1-205">Özet</span><span class="sxs-lookup"><span data-stu-id="56cd1-205">Summary</span></span>
<span data-ttu-id="56cd1-206">Hello ayarlarının doğru olduğunu tıklatın emin olun ve **son** toocomplete hello kurulumu için her zaman şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="56cd1-206">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Özet](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="56cd1-208">Merhaba sihirbazın Eylemler doğrulayın</span><span class="sxs-lookup"><span data-stu-id="56cd1-208">Verify hello wizard's actions</span></span>
<span data-ttu-id="56cd1-209">Merhaba Sihirbaz tamamlandıktan sonra veritabanı her zaman şifreli için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="56cd1-209">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="56cd1-210">Merhaba gerçekleştirilen Sihirbazı hello aşağıdaki eylemler:</span><span class="sxs-lookup"><span data-stu-id="56cd1-210">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="56cd1-211">Bir sütun ana anahtar oluşturulur ve Azure anahtar Kasası ' depolanır.</span><span class="sxs-lookup"><span data-stu-id="56cd1-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="56cd1-212">Bir sütun şifreleme anahtarı oluşturulur ve Azure anahtar Kasası ' depolanır.</span><span class="sxs-lookup"><span data-stu-id="56cd1-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="56cd1-213">Seçili sütunları şifreleme için yapılandırılmış hello.</span><span class="sxs-lookup"><span data-stu-id="56cd1-213">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="56cd1-214">Merhaba hastalar tablosu şu anda hiç veri içermiyor, ancak mevcut verileri hello seçili sütunlardaki şimdi şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="56cd1-214">hello Patients table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="56cd1-215">SSMS hello anahtarlarında hello oluşturulmasını genişleterek doğrulayabilirsiniz **Clinic** > **güvenlik** > **her zaman şifreli anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-215">You can verify hello creation of hello keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="56cd1-216">Şifrelenmiş hello verilerle çalışan istemci uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="56cd1-216">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="56cd1-217">Her zaman şifreli ayarlamak, gerçekleştiren bir uygulama oluşturabilirsiniz *ekler* ve *seçer* sütunlar üzerinde hello şifrelenmiş.</span><span class="sxs-lookup"><span data-stu-id="56cd1-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="56cd1-218">Uygulamanızı kullanmalısınız [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) nesneleri düz metin veri toohello sunucusu her zaman şifreli sütunlarla geçirilirken.</span><span class="sxs-lookup"><span data-stu-id="56cd1-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="56cd1-219">Değişmez değerler SqlParameter nesnelerini kullanmadan geçirme bir özel durum neden olur.</span><span class="sxs-lookup"><span data-stu-id="56cd1-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="56cd1-220">Visual Studio'yu açın ve yeni C# oluşturma **konsol uygulaması** (2015 ve daha önceki Visual Studio) veya **konsol uygulaması (.NET Framework)** (2017 ve daha sonra Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="56cd1-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="56cd1-221">Projenizi çok ayarlandığından emin olun**.NET Framework 4.6** veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="56cd1-221">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="56cd1-222">Ad hello proje **AlwaysEncryptedConsoleAKVApp** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-222">Name hello project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="56cd1-223">NuGet paketlerini çok giderek aşağıdaki hello yüklemek**Araçları** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-223">Install hello following NuGet packages by going too**Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="56cd1-224">Bu iki kod satırı hello Paket Yöneticisi konsolu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-224">Run these two lines of code in hello Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="56cd1-225">Bağlantı dizesi tooenable her zaman şifreli değiştirme</span><span class="sxs-lookup"><span data-stu-id="56cd1-225">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="56cd1-226">Bu bölümde nasıl tooenable veritabanı bağlantı dizenizi her zaman şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="56cd1-226">This section  explains how tooenable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="56cd1-227">tooenable her zaman şifreli, gereksinim duyduğunuz tooadd hello **sütun şifreleme ayarı** anahtar sözcüğü tooyour bağlantı dizesi ve çok ayarlayın**etkin**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-227">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="56cd1-228">Bu doğrudan hello bağlantı dizesinde ayarlayabilirsiniz veya kullanarak ayarlayabilirsiniz [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="56cd1-228">You can set this directly in hello connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="56cd1-229">Merhaba Hello örnek uygulama sonraki bölüm gösterir nasıl toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-229">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="56cd1-230">Her zaman şifreli hello bağlantı dizesinde etkinleştir</span><span class="sxs-lookup"><span data-stu-id="56cd1-230">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="56cd1-231">Anahtar sözcüğü tooyour bağlantı dizesi aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="56cd1-231">Add hello following keyword tooyour connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="56cd1-232">Her zaman SqlConnectionStringBuilder ile şifrelenmiş etkinleştir</span><span class="sxs-lookup"><span data-stu-id="56cd1-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="56cd1-233">kodun gösterdiği nasıl aşağıdaki hello ayarlayarak tooenable her zaman şifreli [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) çok[etkin](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="56cd1-233">hello following code shows how tooenable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a><span data-ttu-id="56cd1-234">Hello Azure anahtar kasası sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="56cd1-234">Register hello Azure Key Vault provider</span></span>
<span data-ttu-id="56cd1-235">Merhaba aşağıdaki kodu nasıl tooregister hello Azure anahtar kasası sağlayıcı hello ADO.NET sürücüsü ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="56cd1-235">hello following code shows how tooregister hello Azure Key Vault provider with hello ADO.NET driver.</span></span>

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="56cd1-236">Her zaman şifreli örnek konsol uygulaması</span><span class="sxs-lookup"><span data-stu-id="56cd1-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="56cd1-237">Bu örnek gösterilmektedir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="56cd1-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="56cd1-238">Bağlantı dizesi tooenable her zaman şifreli değiştirin.</span><span class="sxs-lookup"><span data-stu-id="56cd1-238">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="56cd1-239">Azure anahtar kasası, uygulamanın anahtar depolama sağlayıcısı hello olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="56cd1-239">Register Azure Key Vault as hello application's key store provider.</span></span>  
* <span data-ttu-id="56cd1-240">Veriler şifrelenmiş hello sütunlara ekleyin.</span><span class="sxs-lookup"><span data-stu-id="56cd1-240">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="56cd1-241">Bir kayıt şifrelenmiş sütununda belirli bir değeri filtreleyerek seçin.</span><span class="sxs-lookup"><span data-stu-id="56cd1-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="56cd1-242">Merhaba Değiştir **Program.cs** koddan hello ile.</span><span class="sxs-lookup"><span data-stu-id="56cd1-242">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="56cd1-243">Merhaba genel connectionString değişkeni doğrudan hello Main yönteminin hello Azure portal, geçerli bağlantı dizesi ile önündeki hello satırında Hello bağlantı dizesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="56cd1-243">Replace hello connection string for hello global connectionString variable in hello line that directly precedes hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="56cd1-244">Bu toomake toothis kodu gerekli hello yalnızca değişikliktir.</span><span class="sxs-lookup"><span data-stu-id="56cd1-244">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="56cd1-245">Merhaba uygulama toosee her zaman şifreli eylemini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-245">Run hello app toosee Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
        }

        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
     VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }



## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="56cd1-246">Merhaba verilerin şifrelendiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="56cd1-246">Verify that hello data is encrypted</span></span>
<span data-ttu-id="56cd1-247">SSMS ile Merhaba hastalar veri sorgulayarak hello sunucuda hello gerçek veri şifrelenir hızlı bir şekilde kontrol edebilirsiniz (geçerli bağlantınızı kullanarak nerede **sütun şifreleme ayarı** henüz etkin değil).</span><span class="sxs-lookup"><span data-stu-id="56cd1-247">You can quickly check that hello actual data on hello server is encrypted by querying hello Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="56cd1-248">Sorgu hello Clinic veritabanında aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-248">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="56cd1-249">Herhangi bir düz metin veri içermemesi hello şifrelenmiş sütunlar görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56cd1-249">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Yeni konsol uygulaması](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="56cd1-251">toouse SSMS tooaccess düz metin veri Merhaba, hello ekleyebilirsiniz *sütun şifreleme ayarı = etkin* parametresi toohello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="56cd1-251">toouse SSMS tooaccess hello plaintext data, you can add hello *Column Encryption Setting=enabled* parameter toohello connection.</span></span>

1. <span data-ttu-id="56cd1-252">SSMS, sunucunuzun sağ **Nesne Gezgini** ve **Bağlantıyı Kes**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="56cd1-253">Tıklatın **Bağlan** > **veritabanı altyapısı** tooopen hello **tooServer bağlanmak** penceresini açın ve **seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-253">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window and click **Options**.</span></span>
3. <span data-ttu-id="56cd1-254">Tıklatın **ek bağlantı parametrelerini** ve türü **sütun şifreleme ayarı = etkin**.</span><span class="sxs-lookup"><span data-stu-id="56cd1-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Yeni konsol uygulaması](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="56cd1-256">Sorgu hello Clinic veritabanında aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="56cd1-256">Run hello following query on hello Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="56cd1-257">Şimdi şifrelenmiş hello sütunlardaki hello düz metin verileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56cd1-257">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Yeni konsol uygulaması](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="56cd1-259">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="56cd1-259">Next steps</span></span>
<span data-ttu-id="56cd1-260">Her zaman şifreli kullanan bir veritabanı oluşturduktan sonra toodo hello aşağıdaki isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="56cd1-260">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="56cd1-261">[Döndürün ve anahtarlarınızı Temizleme](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="56cd1-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="56cd1-262">[Zaten her zaman şifreli ile şifrelenmiş veri geçişi](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="56cd1-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="56cd1-263">İlgili bilgiler</span><span class="sxs-lookup"><span data-stu-id="56cd1-263">Related information</span></span>
* [<span data-ttu-id="56cd1-264">Her zaman şifreli (istemci geliştirme)</span><span class="sxs-lookup"><span data-stu-id="56cd1-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="56cd1-265">Saydam veri şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="56cd1-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="56cd1-266">SQL Server şifrelemesi</span><span class="sxs-lookup"><span data-stu-id="56cd1-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="56cd1-267">Her zaman şifreli Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="56cd1-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="56cd1-268">Her zaman şifreli blogu</span><span class="sxs-lookup"><span data-stu-id="56cd1-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

