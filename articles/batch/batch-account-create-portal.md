---
title: "aaaCreate hello Azure portalında bir Batch hesabında | Microsoft Docs"
description: "Nasıl toocreate bir Azure Batch hesabı hello Azure portal toorun hello bulutta büyük ölçekli paralel iş yüklerini öğrenin"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a><span data-ttu-id="62edb-103">Hello Azure portal ile bir toplu işlem hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="62edb-103">Create a Batch account with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="62edb-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="62edb-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="62edb-105">Batch Yönetimi .NET</span><span class="sxs-lookup"><span data-stu-id="62edb-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="62edb-106">Nasıl toocreate bir Azure Batch hesabı hello öğrenin [Azure portal][azure_portal]ve işlem senaryonuzun sığacak hello hesap Özellikler'i seçin.</span><span class="sxs-lookup"><span data-stu-id="62edb-106">Learn how toocreate an Azure Batch account in hello [Azure portal][azure_portal], and choose hello account properties that fit your compute scenario.</span></span> <span data-ttu-id="62edb-107">Burada gibi erişim anahtarlarını ve hesap URL'leri toofind önemli hesap özelliklerini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="62edb-107">Learn where toofind important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="62edb-108">Toplu işlem hesaplarını ve senaryoları hakkında arka plan için hello bkz [genel bakış özellik](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="62edb-108">For background about Batch accounts and scenarios, see hello [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="62edb-109">Batch hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="62edb-109">Create a Batch account</span></span>

<span data-ttu-id="62edb-110">Merhaba portal toocreate toplu işlem hesabı hello iki birini kullanın *havuzu ayırma modları*: **Batch hizmeti** modu ya da daha yeni hello **kullanıcı aboneliği** daha fazlasını gerektiriyor modu yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="62edb-110">Use hello portal toocreate a Batch account in one of hello two *pool allocation modes*: **Batch service** mode or hello newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="62edb-111">Bu iki modları hakkında daha fazla bilgi için bkz: Merhaba [genel bakış özellik](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="62edb-111">For information about these two modes, see hello [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="62edb-112">Ayrıca bkz: hello hello kullanıcı abonelik modunun özellikleri [blog gönderisi](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span><span class="sxs-lookup"><span data-stu-id="62edb-112">For features of hello user subscription mode, see also hello [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="62edb-113">Batch hizmeti modu</span><span class="sxs-lookup"><span data-stu-id="62edb-113">Batch service mode</span></span>



1. <span data-ttu-id="62edb-114">İçinde toohello oturum [Azure portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="62edb-114">Sign in toohello [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="62edb-115">**Yeni** > **İşlem** > **Batch Hizmeti**'ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62edb-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Toplu işlemde hello Market][marketplace_portal]
3. <span data-ttu-id="62edb-117">Merhaba **yeni toplu işlem hesabı** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="62edb-117">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="62edb-118">Her bir dikey pencere öğesinin Hello açıklamaları aşağıda konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="62edb-118">See hello descriptions below of each blade element.</span></span>

    ![Batch hesabı oluşturma][account_portal]

    <span data-ttu-id="62edb-120">a.</span><span class="sxs-lookup"><span data-stu-id="62edb-120">a.</span></span> <span data-ttu-id="62edb-121">**Hesap adı**: hello toplu işlem hesabı adı seçtiğiniz hello hesabın oluşturulduğu Azure bölgesinde hello içinde benzersiz olmalıdır (bkz **konumu** aşağıda).</span><span class="sxs-lookup"><span data-stu-id="62edb-121">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="62edb-122">Merhaba hesap adı yalnızca küçük harf karakterler ya da sayı içerebilir ve 3-24 karakter uzunluğunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="62edb-122">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="62edb-123">b.</span><span class="sxs-lookup"><span data-stu-id="62edb-123">b.</span></span> <span data-ttu-id="62edb-124">**Abonelik**: Merhaba hangi toocreate hello toplu işlem hesabı abonelikte.</span><span class="sxs-lookup"><span data-stu-id="62edb-124">**Subscription**: hello subscription in which toocreate hello Batch account.</span></span> <span data-ttu-id="62edb-125">Yalnızca bir aboneliğiniz varsa, varsayılan olarak seçilidir.</span><span class="sxs-lookup"><span data-stu-id="62edb-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="62edb-126">c.</span><span class="sxs-lookup"><span data-stu-id="62edb-126">c.</span></span> <span data-ttu-id="62edb-127">**Havuz ayırma modu**: **Batch hizmeti**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="62edb-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="62edb-128">c.</span><span class="sxs-lookup"><span data-stu-id="62edb-128">c.</span></span> <span data-ttu-id="62edb-129">**Kaynak grubu**: Yeni Batch hesabınız için mevcut bir kaynak grubu seçebilir ya da isterseniz yeni bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62edb-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="62edb-130">d.</span><span class="sxs-lookup"><span data-stu-id="62edb-130">d.</span></span> <span data-ttu-id="62edb-131">**Konum**: hangi toocreate hello toplu işlem hesabı Azure bölgesinde hello.</span><span class="sxs-lookup"><span data-stu-id="62edb-131">**Location**: hello Azure region in which toocreate hello Batch account.</span></span> <span data-ttu-id="62edb-132">Yalnızca abonelik ve kaynak grubu tarafından desteklenen hello bölgeler seçenek olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="62edb-132">Only hello regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="62edb-133">e.</span><span class="sxs-lookup"><span data-stu-id="62edb-133">e.</span></span> <span data-ttu-id="62edb-134">**Depolama hesabı** (isteğe bağlı): Batch hesabınızla ilişkilendireceğiniz genel amaçlı depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="62edb-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="62edb-135">Çoğu Batch hesabı için önerilen seçenek budur.</span><span class="sxs-lookup"><span data-stu-id="62edb-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="62edb-136">Daha fazla bilgi için bu makalenin sonraki bölümlerinde [Bağlı Azure Depolama hesabı](#linked-azure-storage-account) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="62edb-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="62edb-137">Tıklatın **oluşturma** toocreate hello hesabı.</span><span class="sxs-lookup"><span data-stu-id="62edb-137">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="62edb-138">Merhaba portal dağıtımı devam ediyor gösterir.</span><span class="sxs-lookup"><span data-stu-id="62edb-138">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="62edb-139">İşlem tamamlandıktan sonra **Bildirimler** bölümünde **Dağıtım başarılı** bildirimi görünür.</span><span class="sxs-lookup"><span data-stu-id="62edb-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="62edb-140">Kullanıcı aboneliği modu</span><span class="sxs-lookup"><span data-stu-id="62edb-140">User subscription mode</span></span>

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a><span data-ttu-id="62edb-141">Azure Batch tooaccess hello abonelik (bir defalık işlem) izin ver</span><span class="sxs-lookup"><span data-stu-id="62edb-141">Allow Azure Batch tooaccess hello subscription (one-time operation)</span></span>
<span data-ttu-id="62edb-142">İlk Batch hesabınıza kullanıcı abonelik modunda oluştururken, aşağıdaki adımları tooregister hello toplu aboneliğinizle gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="62edb-142">When creating your first Batch account in user subscription mode, perform hello following steps tooregister your subscription with Batch.</span></span> <span data-ttu-id="62edb-143">(Daha önce bu kaldırdıysanız, toohello sonraki bölüme atlayın.)</span><span class="sxs-lookup"><span data-stu-id="62edb-143">(If you previously did this, skip toohello next section.)</span></span>

1. <span data-ttu-id="62edb-144">İçinde toohello oturum [Azure portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="62edb-144">Sign in toohello [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="62edb-145">Tıklatın **daha Hizmetleri** > **abonelikleri**, hello abonelik istediğiniz toouse hello toplu işlem hesabı için'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62edb-145">Click **More Services** > **Subscriptions**, and click hello subscription you want toouse for hello Batch account.</span></span>

3. <span data-ttu-id="62edb-146">Merhaba, **abonelik** dikey penceresinde tıklatın **erişim denetimi (IAM)** > **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="62edb-146">In hello **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Abonelik erişim denetimi][subscription_access]

4. <span data-ttu-id="62edb-148">Merhaba üzerinde **izinleri eklemek** dikey penceresinde, select hello **katkıda bulunan** rolü, toplu işlem API hello arayın.</span><span class="sxs-lookup"><span data-stu-id="62edb-148">On hello **Add permissions** blade, select hello **Contributor** role, search for hello Batch API.</span></span> <span data-ttu-id="62edb-149">Arama hello API bulana kadar bu dizelerin her biri için:</span><span class="sxs-lookup"><span data-stu-id="62edb-149">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="62edb-150">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="62edb-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="62edb-151">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="62edb-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="62edb-152">Daha yeni Azure AD kiracıları bu adı kullanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="62edb-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="62edb-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** hello toplu API hello kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="62edb-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 

5. <span data-ttu-id="62edb-154">Hello toplu API bulduktan sonra onu seçin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="62edb-154">Once you find hello Batch API, select it and click **Save**.</span></span>

    ![Batch izinleri ekleme][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="62edb-156">Bir anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="62edb-156">Create a key vault</span></span>
<span data-ttu-id="62edb-157">Azure anahtar kasası kullanıcı abonelik modunda gerekli olan toothe ait aynı kaynak grubunda oluşturulan hello toplu işlem hesabı toobe.</span><span class="sxs-lookup"><span data-stu-id="62edb-157">In user subscription mode, an Azure key vault is required that belongs toothe same resource group as hello Batch account toobe created.</span></span> <span data-ttu-id="62edb-158">Merhaba kaynak grubu toplu olduğu bir bölgede olduğundan emin olun [kullanılabilir](https://azure.microsoft.com/regions/services/) ve aboneliğinizi destekleyen.</span><span class="sxs-lookup"><span data-stu-id="62edb-158">Make sure hello resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="62edb-159">Merhaba, [Azure portal][azure_portal], tıklatın **yeni** > **güvenlik + kimlik** > **anahtar kasası** .</span><span class="sxs-lookup"><span data-stu-id="62edb-159">In hello [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="62edb-160">Merhaba, **anahtar kasası oluşturma** dikey penceresinde hello anahtar kasası için bir ad girin ve toplu işlem hesabı için istediğiniz hello bölgede bulunan bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62edb-160">In hello **Create Key Vault** blade, enter a name for hello key vault, and create a resource group in hello region you want for your Batch account.</span></span> <span data-ttu-id="62edb-161">Varsayılan değerleri ayarları kalan hello bırakın ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="62edb-161">Leave hello remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="62edb-162">Batch hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="62edb-162">Create a Batch account</span></span>

1. <span data-ttu-id="62edb-163">Merhaba, [Azure portal][azure_portal], tıklatın **yeni** > **işlem** > **Batch hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="62edb-163">In hello [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Toplu işlemde hello Market][marketplace_portal]
3. <span data-ttu-id="62edb-165">Merhaba **yeni toplu işlem hesabı** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="62edb-165">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="62edb-166">Her bir dikey pencere öğesinin Hello açıklamaları aşağıda konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="62edb-166">See hello descriptions below of each blade element.</span></span>

    ![Batch hesabı oluşturma][account_portal_byos]

    <span data-ttu-id="62edb-168">a.</span><span class="sxs-lookup"><span data-stu-id="62edb-168">a.</span></span> <span data-ttu-id="62edb-169">**Hesap adı**: hello toplu işlem hesabı adı seçtiğiniz hello hesabın oluşturulduğu Azure bölgesinde hello içinde benzersiz olmalıdır (bkz **konumu** aşağıda).</span><span class="sxs-lookup"><span data-stu-id="62edb-169">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="62edb-170">Merhaba hesap adı yalnızca küçük harf karakterler ya da sayı içerebilir ve 3-24 karakter uzunluğunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="62edb-170">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="62edb-171">b.</span><span class="sxs-lookup"><span data-stu-id="62edb-171">b.</span></span> <span data-ttu-id="62edb-172">**Abonelik**: birden fazla aboneliğiniz varsa, Batch hizmeti hello ile kayıtlı hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="62edb-172">**Subscription**: If you have more than one subscription, select hello subscription that you registered with hello Batch service.</span></span>

    <span data-ttu-id="62edb-173">c.</span><span class="sxs-lookup"><span data-stu-id="62edb-173">c.</span></span> <span data-ttu-id="62edb-174">**Havuzu ayırma modu**: **Kullanıcı aboneliği**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="62edb-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="62edb-175">d.</span><span class="sxs-lookup"><span data-stu-id="62edb-175">d.</span></span> <span data-ttu-id="62edb-176">**Anahtar kasası**: Batch hesabınızın hello önceki bölümde oluşturduğunuz Select hello anahtar kasası.</span><span class="sxs-lookup"><span data-stu-id="62edb-176">**Key vault**: Select hello key vault you created for your Batch account in hello previous section.</span></span> <span data-ttu-id="62edb-177">İsteğe bağlı olarak, yeni bir anahtar kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62edb-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="62edb-178">Merhaba kasası seçtikten sonra hello onay kutusunu toogrant Azure Batch erişim toohello anahtar kasası seçin.</span><span class="sxs-lookup"><span data-stu-id="62edb-178">After selecting hello vault, select hello checkbox toogrant Azure Batch access toohello key vault.</span></span>

    <span data-ttu-id="62edb-179">c.</span><span class="sxs-lookup"><span data-stu-id="62edb-179">c.</span></span> <span data-ttu-id="62edb-180">**Kaynak grubu**: hello anahtar kasası oluşturulan Select hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="62edb-180">**Resource group**: Select hello resource group in which you  created hello key vault.</span></span>

    <span data-ttu-id="62edb-181">d.</span><span class="sxs-lookup"><span data-stu-id="62edb-181">d.</span></span> <span data-ttu-id="62edb-182">**Konum**: hello anahtar kasası hello toplu işlem hesabı için oluşturulan Azure bölgesi hello.</span><span class="sxs-lookup"><span data-stu-id="62edb-182">**Location**: hello Azure region in which you created hello key vault for hello Batch account.</span></span>

    <span data-ttu-id="62edb-183">e.</span><span class="sxs-lookup"><span data-stu-id="62edb-183">e.</span></span> <span data-ttu-id="62edb-184">**Depolama hesabı** (isteğe bağlı): Batch hesabınızla ilişkilendireceğiniz genel amaçlı depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="62edb-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="62edb-185">Çoğu Batch hesabı için önerilen seçenek budur.</span><span class="sxs-lookup"><span data-stu-id="62edb-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="62edb-186">Daha fazla bilgi için aşağıdaki [Bağlı Azure Storage hesabı](#linked-azure-storage-account) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="62edb-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="62edb-187">Tıklatın **oluşturma** toocreate hello hesabı.</span><span class="sxs-lookup"><span data-stu-id="62edb-187">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="62edb-188">Merhaba portal dağıtımı devam ediyor gösterir.</span><span class="sxs-lookup"><span data-stu-id="62edb-188">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="62edb-189">İşlem tamamlandıktan sonra **Bildirimler** bölümünde **Dağıtım başarılı** bildirimi görünür.</span><span class="sxs-lookup"><span data-stu-id="62edb-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="62edb-190">Batch hesabı özelliklerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="62edb-190">View Batch account properties</span></span>
<span data-ttu-id="62edb-191">Merhaba hesabı oluşturulduktan sonra hello açabilirsiniz **Batch hesabı dikey** tooaccess kendi ayarları ve özellikleri.</span><span class="sxs-lookup"><span data-stu-id="62edb-191">Once hello account has been created, you can open hello **Batch account blade** tooaccess its settings and properties.</span></span> <span data-ttu-id="62edb-192">Tüm hesap ayarları ve özellikleri hello Batch hesabı dikey penceresinde, soldaki menüden hello kullanarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62edb-192">You can access all account settings and properties by using hello left menu of hello Batch account blade.</span></span>

![Azure portalında Batch hesabı dikey penceresi][account_blade]

* <span data-ttu-id="62edb-194">**Batch hesabı URL'si**: hello sahip bir uygulama geliştirirken [Batch API'lerini](batch-apis-tools.md#azure-accounts-for-batch-development), bir hesap URL tooaccess Batch kaynaklarınız ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="62edb-194">**Batch account URL**: When you develop an application with hello [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL tooaccess your Batch resources.</span></span> <span data-ttu-id="62edb-195">Bir Batch hesabı URL'si biçimi aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="62edb-195">A Batch account URL has hello following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![Portalda Batch hesabı URL’si][account_url]

* <span data-ttu-id="62edb-197">**Erişim tuşları** (toplu işlem hizmeti mod): tooauthenticate erişim tooyour toplu işlem hesabı uygulamanızdan, hesap erişim anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="62edb-197">**Access keys** (Batch service mode): tooauthenticate access tooyour Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="62edb-198">(Bu ayar, Azure Active Directory kimlik doğrulamasını kullandığınız kullanıcı aboneliği modunda mevcut değildir.)</span><span class="sxs-lookup"><span data-stu-id="62edb-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="62edb-199">Batch hesabınızın erişim anahtarlarını tooview veya yeniden girin `keys` hello soldaki menüde **arama** kutusunda hello Batch hesabı dikey penceresinde, ardından seçin **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="62edb-199">tooview or regenerate your Batch account's access keys, enter `keys` in hello left menu **Search** box on hello Batch account blade, then select **Keys**.</span></span>

    ![Azure portalında Batch hesabı anahtarları][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="62edb-201">Bağlı Azure Storage hesabı</span><span class="sxs-lookup"><span data-stu-id="62edb-201">Linked Azure Storage account</span></span>

<span data-ttu-id="62edb-202">Genel amaçlı bir Azure depolama hesabı tooyour toplu işlem hesabı isteğe bağlı olarak bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62edb-202">You can optionally link a general-purpose Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="62edb-203">Merhaba [uygulama paketleri](batch-application-packages.md) toplu özelliği hello yaptığı gibi Azure Blob Depolama kullanır [toplu iş dosyası kuralları .NET](batch-task-output.md) kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="62edb-203">hello [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does hello [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="62edb-204">Bu isteğe bağlı özellikler, toplu görevlerinizin çalıştığı hello uygulamaları dağıtma ve oluşturdukları kalıcı hello veri yardımcı.</span><span class="sxs-lookup"><span data-stu-id="62edb-204">These optional features assist you in deploying hello applications that your Batch tasks run, and persisting hello data they produce.</span></span>

<span data-ttu-id="62edb-205">Yalnızca Batch hesabınız tarafından kullanılacak yeni bir Depolama hesabı oluşturmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="62edb-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Genel amaçlı depolama hesabı oluşturma][storage_account]

> [!NOTE]
> <span data-ttu-id="62edb-207">Azure toplu işlem şu anda yalnızca hello genel amaçlı depolama hesabı türünü destekler.</span><span class="sxs-lookup"><span data-stu-id="62edb-207">Azure Batch currently supports only hello general-purpose Storage account type.</span></span> <span data-ttu-id="62edb-208">Bu hesap türü [Azure depolama hesapları hakkında](../storage/common/storage-create-storage-account.md) belgesinin 5. adımında [Depolama hesabı oluşturma] (../storage/common/storage-create-storage-account.md#create-a-storage-account) açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="62edb-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="62edb-209">Merhaba, bağlantılı bir depolama hesabının erişim anahtarlarını yeniden oluştururken dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="62edb-209">Be careful when regenerating hello access keys of a linked Storage account.</span></span> <span data-ttu-id="62edb-210">Yalnızca bir depolama hesabı anahtarı yeniden oluşturmak ve tıklayın **anahtarları Eşitle** depolama hesabı dikey penceresinde hello üzerinde bağlı.</span><span class="sxs-lookup"><span data-stu-id="62edb-210">Regenerate only one Storage account key and click **Sync Keys** on hello linked Storage account blade.</span></span> <span data-ttu-id="62edb-211">Gerekirse diğer anahtarı hello tooallow hello anahtarları toopropagate toohello işlem düğümleri, havuzlar, ardından yeniden ve eşitleme beş dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="62edb-211">Wait five minutes tooallow hello keys toopropagate toohello compute nodes in your pools, then regenerate and synchronize hello other key if necessary.</span></span> <span data-ttu-id="62edb-212">Her ikisini de yeniden oluşturursanız hello aynı anahtarları süresi, işlem düğümleriniz mümkün toosynchronize ya da anahtar olmayacak ve erişim toohello depolama hesabı kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="62edb-212">If you regenerate both keys at hello same time, your compute nodes will not be able toosynchronize either key, and they will lose access toohello Storage account.</span></span>
>
>

<span data-ttu-id="62edb-213">![Depolama hesabı anahtarlarını yeniden oluşturma][4]</span><span class="sxs-lookup"><span data-stu-id="62edb-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="62edb-214">Batch hizmet kotaları ve limitleri</span><span class="sxs-lookup"><span data-stu-id="62edb-214">Batch service quotas and limits</span></span>
<span data-ttu-id="62edb-215">Lütfen olması olarak Azure aboneliğinize ve diğer Azure hizmetlerini kullanan, belirli [kotalar ve sınırlar](batch-quota-limit.md) tooBatch hesapları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="62edb-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply tooBatch accounts.</span></span> <span data-ttu-id="62edb-216">Bir toplu işlem hesabı için geçerli kotalar görünür hello hesabındaki hello portalında **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="62edb-216">Current quotas for a Batch account appear in hello portal in hello account **Properties**.</span></span>

![Azure portalında Batch hesabı kotaları][quotas]



<span data-ttu-id="62edb-218">Ayrıca, bu kotalar çoğunu hello Azure portal yalnızca bir ücretsiz ürün destek isteği gönderildi ile artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="62edb-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in hello Azure portal.</span></span> <span data-ttu-id="62edb-219">Bkz: [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md) kota artar isteme ile ilgili ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="62edb-219">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="62edb-220">Diğer Batch hesabı yönetim seçenekleri</span><span class="sxs-lookup"><span data-stu-id="62edb-220">Other Batch account management options</span></span>
<span data-ttu-id="62edb-221">Ayrıca toousing Merhaba Azure portal, da oluşturabilir ve hello aşağıdaki Batch hesaplarıyla yönetebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="62edb-221">In addition toousing hello Azure portal, you can also create and manage Batch accounts with hello following:</span></span>

* [<span data-ttu-id="62edb-222">Batch PowerShell cmdlet’leri</span><span class="sxs-lookup"><span data-stu-id="62edb-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="62edb-223">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="62edb-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="62edb-224">Batch Yönetimi .NET</span><span class="sxs-lookup"><span data-stu-id="62edb-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="62edb-225">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="62edb-225">Next steps</span></span>
* <span data-ttu-id="62edb-226">Merhaba bkz [Batch özelliklerine genel bakış](batch-api-basics.md) toolearn Batch hizmeti kavramları ve özellikler hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="62edb-226">See hello [Batch feature overview](batch-api-basics.md) toolearn more about Batch service concepts and features.</span></span> <span data-ttu-id="62edb-227">Merhaba makale havuzlar, işlem düğümleri, işler ve görevler gibi birincil Batch kaynaklarını hello açıklanır ve büyük ölçekli işlem iş yükü yürütmeye hizmetin özellikleri hello genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="62edb-227">hello article discusses hello primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of hello service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="62edb-228">Hello kullanarak Batch özellikli bir uygulama geliştirme hello temellerini öğrenin [Batch .NET istemci kitaplığını](batch-dotnet-get-started.md) veya [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="62edb-228">Learn hello basics of developing a Batch-enabled application using hello [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="62edb-229">Bu Tanıtım makaleler hello Batch hizmeti tooexecute bir iş yükü birden çok işlem düğümlerinde kullanır ve iş yükü dosyası hazırlama ve alma için Azure Storage kullanmayı da içeren çalışan bir uygulama size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="62edb-229">These introductory articles guide you through a working application that uses hello Batch service tooexecute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Depolama hesabı anahtarlarını yeniden oluşturma"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
