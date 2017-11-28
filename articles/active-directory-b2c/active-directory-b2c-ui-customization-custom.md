---
title: "Özel ilkeler - Azure AD B2C kullanarak bir UI Özelleştirme | Microsoft Docs"
description: "Azure AD B2C'de özel ilkeler kullanırken bir kullanıcı arabirimi (UI) özelleştirme hakkında bilgi edinin."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a><span data-ttu-id="b3d9a-103">Azure Active Directory B2C: Kullanıcı Arabirimi özelleştirme özel bir ilke yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-103">Azure Active Directory B2C: Configure UI customization in a custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="b3d9a-104">Bu makalede tamamladıktan sonra kaydolma ve oturum açma özel bir ilke ile marka ve görünümüne sahip olur.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-104">After you complete this article, you will have a sign-up and sign-in custom policy with your brand and appearance.</span></span> <span data-ttu-id="b3d9a-105">Azure Active Directory B2C ile (Azure AD B2C) elde hello HTML ve CSS içeriğin neredeyse tam denetim, toousers sunulan.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-105">With Azure Active Directory B2C (Azure AD B2C), you get nearly full control of hello HTML and CSS content that's presented toousers.</span></span> <span data-ttu-id="b3d9a-106">Özel bir ilke kullandığınızda, kullanıcı arabirimini özelleştirme XML biçiminde hello Azure portal denetimleri kullanmak yerine yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-106">When you use a custom policy, you configure UI customization in XML instead of using controls in hello Azure portal.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b3d9a-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b3d9a-107">Prerequisites</span></span>

<span data-ttu-id="b3d9a-108">Başlamadan önce tamamlamanız [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b3d9a-108">Before you begin, complete [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="b3d9a-109">Çalışma özel bir ilke için kaydolma ve oturum açma yerel hesaplara sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-109">You should have a working custom policy for sign-up and sign-in with local accounts.</span></span>

## <a name="page-ui-customization"></a><span data-ttu-id="b3d9a-110">Sayfanın UI Özelleştirme</span><span class="sxs-lookup"><span data-stu-id="b3d9a-110">Page UI customization</span></span>

<span data-ttu-id="b3d9a-111">Başlangıç sayfası kullanıcı Arabirimi özelleştirme özelliğini kullanarak, herhangi bir özel ilke hello Görünüm ve yapısını özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-111">By using hello page UI customization feature, you can customize hello look and feel of any custom policy.</span></span> <span data-ttu-id="b3d9a-112">Ayrıca, marka ve uygulama ve Azure AD B2C arasında visual tutarlılık koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-112">You can also maintain brand and visual consistency between your application and Azure AD B2C.</span></span>

<span data-ttu-id="b3d9a-113">İşte nasıl çalışır?: Azure AD B2C, müşterinizin tarayıcıda kodu çalıştırır ve adlı modern bir yaklaşım kullanır [çıkış noktaları arası kaynak paylaşımı (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="b3d9a-113">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span> <span data-ttu-id="b3d9a-114">İlk olarak, özelleştirilmiş HTML içeriğe sahip hello özel ilkesindeki bir URL belirtin.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-114">First, you specify a URL in hello custom policy with customized HTML content.</span></span> <span data-ttu-id="b3d9a-115">Azure AD B2C kullanıcı Arabirimi öğeleri Merhaba, URL'den yüklenir ve hello sayfa toohello müşteri görüntüleyen HTML içeriği ile birleştirir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-115">Azure AD B2C merges UI elements with hello HTML content that's loaded from your URL and then displays hello page toohello customer.</span></span>

## <a name="create-your-html5-content"></a><span data-ttu-id="b3d9a-116">HTML5 içerik oluşturma</span><span class="sxs-lookup"><span data-stu-id="b3d9a-116">Create your HTML5 content</span></span>

<span data-ttu-id="b3d9a-117">HTML hello başlığında ürününüzün marka adıyla içerik oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-117">Create HTML content with your product's brand name in hello title.</span></span>

1. <span data-ttu-id="b3d9a-118">HTML kod parçası aşağıdaki hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-118">Copy hello following HTML snippet.</span></span> <span data-ttu-id="b3d9a-119">Doğru biçimlendirilmiş boş bir öğesiyle HTML5 adlı  *\<div ID "API" =\>\</div\>*  hello içinde bulunan  *\<gövde\>*  etiketler.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-119">It is well-formed HTML5 with an empty element called *\<div id="api"\>\</div\>* located within hello *\<body\>* tags.</span></span> <span data-ttu-id="b3d9a-120">Bu öğe, Azure AD B2C içerik eklenen toobe nerede gösterir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-120">This element indicates where Azure AD B2C content is toobe inserted.</span></span>

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   ><span data-ttu-id="b3d9a-121">Güvenlik nedenleriyle, JavaScript hello kullanımını özelleştirme için şu anda engelleniyor.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-121">For security reasons, hello use of JavaScript is currently blocked for customization.</span></span>

2. <span data-ttu-id="b3d9a-122">Bir metin düzenleyicisinde kopyalanan hello parçacığını yapıştırın ve sonra hello dosyası olarak kaydedin *özelleştirme ui.html*.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-122">Paste hello copied snippet in a text editor, and then save hello file as *customize-ui.html*.</span></span>

## <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="b3d9a-123">Bir Azure Blob storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b3d9a-123">Create an Azure Blob storage account</span></span>

>[!NOTE]
> <span data-ttu-id="b3d9a-124">Bu makalede, bazı içeriklerin Azure Blob Depolama toohost kullanırız.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-124">In this article, we use Azure Blob storage toohost our content.</span></span> <span data-ttu-id="b3d9a-125">İçeriğinizi bir web sunucusunda toohost seçebilirsiniz, ancak gerekir [web sunucunuz üzerinde CORS'yi etkinleştirmeniz](https://enable-cors.org/server.html).</span><span class="sxs-lookup"><span data-stu-id="b3d9a-125">You can choose toohost your content on a web server, but you must [enable CORS on your web server](https://enable-cors.org/server.html).</span></span>

<span data-ttu-id="b3d9a-126">toohost bu HTML içeriğine Blob depolama alanındaki hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="b3d9a-126">toohost this HTML content in Blob storage, do hello following:</span></span>

1. <span data-ttu-id="b3d9a-127">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b3d9a-127">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b3d9a-128">Merhaba üzerinde **Hub** menüsünde, select **yeni** > **depolama** > **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-128">On hello **Hub** menu, select **New** > **Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="b3d9a-129">Benzersiz bir girin **adı** depolama hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-129">Enter a unique **Name** for your storage account.</span></span>
4. <span data-ttu-id="b3d9a-130">**Dağıtım modeli** kalabileceği **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-130">**Deployment model** can remain **Resource Manager**.</span></span>
5. <span data-ttu-id="b3d9a-131">Değişiklik **hesap türü** çok**Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-131">Change **Account Kind** too**Blob storage**.</span></span>
6. <span data-ttu-id="b3d9a-132">**Performans** kalabileceği **standart**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-132">**Performance** can remain **Standard**.</span></span>
7. <span data-ttu-id="b3d9a-133">**Çoğaltma** kalabileceği **RA-GRS**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-133">**Replication** can remain **RA-GRS**.</span></span>
8. <span data-ttu-id="b3d9a-134">**Erişim katmanı** kalabileceği **etkin**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-134">**Access tier** can remain **Hot**.</span></span>
9. <span data-ttu-id="b3d9a-135">**Depolama hizmeti şifrelemesi** kalabileceği **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-135">**Storage service encryption** can remain **Disabled**.</span></span>
10. <span data-ttu-id="b3d9a-136">Seçin bir **abonelik** depolama hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-136">Select a **Subscription** for your storage account.</span></span>
11. <span data-ttu-id="b3d9a-137">Oluşturma bir **kaynak grubu** veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-137">Create a **Resource group** or select an existing one.</span></span>
12. <span data-ttu-id="b3d9a-138">Select hello **coğrafi konum** depolama hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-138">Select hello **Geographic location** for your storage account.</span></span>
13. <span data-ttu-id="b3d9a-139">Tıklatın **oluşturma** toocreate hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-139">Click **Create** toocreate hello storage account.</span></span>  
    <span data-ttu-id="b3d9a-140">Merhaba dağıtım tamamlandıktan sonra hello **depolama hesabı** dikey penceresinde otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-140">After hello deployment is completed, hello **Storage account** blade opens automatically.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="b3d9a-141">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b3d9a-141">Create a container</span></span>

<span data-ttu-id="b3d9a-142">Blob storage, ortak bir kapsayıcıda toocreate hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="b3d9a-142">toocreate a public container in Blob storage, do hello following:</span></span>

1. <span data-ttu-id="b3d9a-143">Merhaba tıklatın **genel bakış** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-143">Click hello **Overview** tab.</span></span>
2. <span data-ttu-id="b3d9a-144">Tıklatın **kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-144">Click **Container**.</span></span>
3. <span data-ttu-id="b3d9a-145">İçin **adı**, türü **$root**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-145">For **Name**, type **$root**.</span></span>
4. <span data-ttu-id="b3d9a-146">Ayarlama **erişim türüne** çok**Blob**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-146">Set **Access type** too**Blob**.</span></span>
5. <span data-ttu-id="b3d9a-147">Tıklatın **$root** tooopen hello yeni kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-147">Click **$root** tooopen hello new container.</span></span>
6. <span data-ttu-id="b3d9a-148">**Karşıya Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-148">Click **Upload**.</span></span>
7. <span data-ttu-id="b3d9a-149">Merhaba klasör simgesine tıklayın sonraki çok**bir dosya seçin**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-149">Click hello folder icon next too**Select a file**.</span></span>
8. <span data-ttu-id="b3d9a-150">Çok Git**özelleştirme ui.html**, hello daha önce oluşturmuş olduğunuz [sayfa UI özelleştirme](#the-page-ui-customization-feature) bölümü.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-150">Go too**customize-ui.html**, which you created earlier in hello [Page UI customization](#the-page-ui-customization-feature) section.</span></span>
9. <span data-ttu-id="b3d9a-151">**Karşıya Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-151">Click **Upload**.</span></span>
10. <span data-ttu-id="b3d9a-152">Karşıya yüklediğiniz hello özelleştirme ui.html blob seçin.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-152">Select hello customize-ui.html blob that you uploaded.</span></span>
11. <span data-ttu-id="b3d9a-153">Sonraki çok**URL**, tıklatın **kopya**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-153">Next too**URL**, click **Copy**.</span></span>
12. <span data-ttu-id="b3d9a-154">Bir tarayıcıda, kopyalanan hello URL'sini yapıştırın ve toohello sitesine gidin.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-154">In a browser, paste hello copied URL, and go toohello site.</span></span> <span data-ttu-id="b3d9a-155">Merhaba site erişilemiyorsa hello kapsayıcı erişim türü çok ayarlandığından emin olun**blob**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-155">If hello site is inaccessible, make sure hello container access type is set too**blob**.</span></span>

## <a name="configure-cors"></a><span data-ttu-id="b3d9a-156">CORS'yi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b3d9a-156">Configure CORS</span></span>

<span data-ttu-id="b3d9a-157">BLOB Depolama çıkış noktaları arası kaynak paylaşımı için hello aşağıdakileri yaparak yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="b3d9a-157">Configure Blob storage for Cross-Origin Resource Sharing by doing hello following:</span></span>

>[!NOTE]
><span data-ttu-id="b3d9a-158">Bizim örnek HTML ve CSS içerik kullanarak hello UI Özelleştirme özelliği çıkışı tootry istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="b3d9a-158">Want tootry out hello UI customization feature by using our sample HTML and CSS content?</span></span> <span data-ttu-id="b3d9a-159">Sağladık [basit Yardımcısı aracı](active-directory-b2c-reference-ui-customization-helper-tool.md) karşıya yükleyen ve Blob Depolama hesabınıza bizim örnek içeriği yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-159">We've provided [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures our sample content on your Blob storage account.</span></span> <span data-ttu-id="b3d9a-160">İleri hello aracı kullanırsanız, çok atlayabilirsiniz[oturum açma veya kaydolma özel ilkenizi değiştirmek](#modify-your-sign-up-or-sign-in-custom-policy).</span><span class="sxs-lookup"><span data-stu-id="b3d9a-160">If you use hello tool, skip ahead too[Modify your sign-up or sign-in custom policy](#modify-your-sign-up-or-sign-in-custom-policy).</span></span>

1. <span data-ttu-id="b3d9a-161">Merhaba üzerinde **depolama** dikey altında **ayarları**, açık **CORS**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-161">On hello **Storage** blade, under **Settings**, open **CORS**.</span></span>
2. <span data-ttu-id="b3d9a-162">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-162">Click **Add**.</span></span>
3. <span data-ttu-id="b3d9a-163">İçin **çıkış izin**, bir yıldız işareti girin (\*).</span><span class="sxs-lookup"><span data-stu-id="b3d9a-163">For **Allowed origins**, type an asterisk (\*).</span></span>
4. <span data-ttu-id="b3d9a-164">Merhaba, **fiillere izin** açılan listesinden, select **almak** ve **seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-164">In hello **Allowed verbs** drop-down list, select both **GET** and **OPTIONS**.</span></span>
5. <span data-ttu-id="b3d9a-165">İçin **üstbilgileri izin**, bir yıldız işareti girin (\*).</span><span class="sxs-lookup"><span data-stu-id="b3d9a-165">For **Allowed headers**, type an asterisk (\*).</span></span>
6. <span data-ttu-id="b3d9a-166">İçin **sunulan üstbilgileri**, bir yıldız işareti girin (\*).</span><span class="sxs-lookup"><span data-stu-id="b3d9a-166">For **Exposed headers**, type an asterisk (\*).</span></span>
7. <span data-ttu-id="b3d9a-167">İçin **en uzun geçerlilik süresi (saniye)**, türü **200**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-167">For **Maximum age (seconds)**, type **200**.</span></span>
8. <span data-ttu-id="b3d9a-168">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-168">Click **Add**.</span></span>

## <a name="test-cors"></a><span data-ttu-id="b3d9a-169">Test CORS</span><span class="sxs-lookup"><span data-stu-id="b3d9a-169">Test CORS</span></span>

<span data-ttu-id="b3d9a-170">Merhaba aşağıdakileri yaparak hazırsınız olduğunu doğrulama:</span><span class="sxs-lookup"><span data-stu-id="b3d9a-170">Validate that you're ready by doing hello following:</span></span>

1. <span data-ttu-id="b3d9a-171">Toohello Git [test cors.org](http://test-cors.org/) Web sitesi ve Yapıştır hello hello URL'de **uzak URL** kutusu.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-171">Go toohello [test-cors.org](http://test-cors.org/) website, and then paste hello URL in hello **Remote URL** box.</span></span>
2. <span data-ttu-id="b3d9a-172">Tıklatın **gönderme isteği**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-172">Click **Send Request**.</span></span>  
    <span data-ttu-id="b3d9a-173">Bir hata alırsanız, emin olun, [CORS ayarları](#configure-cors) doğrudur.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-173">If you receive an error, make sure that your [CORS settings](#configure-cors) are correct.</span></span> <span data-ttu-id="b3d9a-174">Ayrıca tarayıcı önbelleğiniz tooclear ihtiyacınız veya Ctrl + Shift + P tuşuna basarak bir özel tarayıcı oturumu açın.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-174">You might also need tooclear your browser cache or open an in-private browsing session by pressing Ctrl+Shift+P.</span></span>

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a><span data-ttu-id="b3d9a-175">Oturum açma veya kaydolma özel ilkesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="b3d9a-175">Modify your sign-up or sign-in custom policy</span></span>

<span data-ttu-id="b3d9a-176">Üst düzey hello altında  *\<TrustFrameworkPolicy\>*  etiketi, bulmanız gerekir  *\<BuildingBlocks\>*  etiketi.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-176">Under hello top-level *\<TrustFrameworkPolicy\>* tag, you should find *\<BuildingBlocks\>* tag.</span></span> <span data-ttu-id="b3d9a-177">Merhaba içinde  *\<BuildingBlocks\>*  etiketler eklemek bir  *\<ContentDefinitions\>*  aşağıdaki örneğine hello kopyalayarak etiketi.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-177">Within hello *\<BuildingBlocks\>* tags, add a *\<ContentDefinitions\>* tag by copying hello following example.</span></span> <span data-ttu-id="b3d9a-178">Değiştir *your_storage_account* depolama hesabınızın hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-178">Replace *your_storage_account* with hello name of your storage account.</span></span>

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a><span data-ttu-id="b3d9a-179">Güncelleştirilmiş özel ilkeniz karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="b3d9a-179">Upload your updated custom policy</span></span>

1. <span data-ttu-id="b3d9a-180">Merhaba, [Azure portal](https://portal.azure.com), [geçiş hello Azure AD B2C kiracınızın bağlamına](active-directory-b2c-navigate-to-b2c-context.md)ve ardından hello açın **Azure AD B2C** dikey.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-180">In hello [Azure portal](https://portal.azure.com), [switch into hello context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open hello **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="b3d9a-181">Tıklatın **tüm ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-181">Click **All Policies**.</span></span>
3. <span data-ttu-id="b3d9a-182">Tıklatın **karşıya İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-182">Click **Upload Policy**.</span></span>
4. <span data-ttu-id="b3d9a-183">Karşıya yükleme `SignUpOrSignin.xml` hello ile  *\<ContentDefinitions\>*  daha önce eklediğiniz etiketi.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-183">Upload `SignUpOrSignin.xml` with hello *\<ContentDefinitions\>* tag that you added previously.</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="b3d9a-184">Test hello özel ilke kullanarak **Şimdi Çalıştır**</span><span class="sxs-lookup"><span data-stu-id="b3d9a-184">Test hello custom policy by using **Run now**</span></span>

1. <span data-ttu-id="b3d9a-185">Merhaba üzerinde **Azure AD B2C** dikey penceresinde çok Git**tüm ilkeler**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-185">On hello **Azure AD B2C** blade, go too**All polices**.</span></span>
2. <span data-ttu-id="b3d9a-186">Karşıya yüklediğiniz hello özel ilkesini seçin ve hello tıklayın **Şimdi Çalıştır** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-186">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="b3d9a-187">Bir e-posta adresi kullanarak yukarı mümkün toosign olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-187">You should be able toosign up by using an email address.</span></span>

## <a name="reference"></a><span data-ttu-id="b3d9a-188">Başvuru</span><span class="sxs-lookup"><span data-stu-id="b3d9a-188">Reference</span></span>

<span data-ttu-id="b3d9a-189">Buraya kullanıcı arabirimini özelleştirme örnek şablonları bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b3d9a-189">You can find sample templates for UI customization here:</span></span>

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

<span data-ttu-id="b3d9a-190">Aşağıdaki HTML dosyaları hello Hello sample_templates/wingtip klasör içerir:</span><span class="sxs-lookup"><span data-stu-id="b3d9a-190">hello sample_templates/wingtip folder contains hello following HTML files:</span></span>

| <span data-ttu-id="b3d9a-191">HTML5 şablonu</span><span class="sxs-lookup"><span data-stu-id="b3d9a-191">HTML5 template</span></span> | <span data-ttu-id="b3d9a-192">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b3d9a-192">Description</span></span> |
|----------------|-------------|
| <span data-ttu-id="b3d9a-193">*phonefactor.HTML*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-193">*phonefactor.html*</span></span> | <span data-ttu-id="b3d9a-194">Bu dosyayı bir çok faktörlü kimlik doğrulaması sayfası için bir şablon olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-194">Use this file as a template for a multi-factor authentication page.</span></span> |
| <span data-ttu-id="b3d9a-195">*ResetPassword.HTML*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-195">*resetpassword.html*</span></span> | <span data-ttu-id="b3d9a-196">Bu dosya için bir şablon olarak kullanmak bir parolanızı mı unuttunuz sayfasını.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-196">Use this file as a template for a forgot password page.</span></span> |
| <span data-ttu-id="b3d9a-197">*selfasserted.HTML*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-197">*selfasserted.html*</span></span> | <span data-ttu-id="b3d9a-198">Bu dosya, sosyal hesap kayıt sayfası, yerel hesap kaydolma sayfası veya bir yerel hesap oturum açma sayfası için bir şablon olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-198">Use this file as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span></span> |
| <span data-ttu-id="b3d9a-199">*Unified.HTML*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-199">*unified.html*</span></span> | <span data-ttu-id="b3d9a-200">Bu dosyayı bir birleşik kayıt veya oturum açma sayfası için bir şablon olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-200">Use this file as a template for a unified sign-up or sign-in page.</span></span> |
| <span data-ttu-id="b3d9a-201">*updateprofile.HTML*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-201">*updateprofile.html*</span></span> | <span data-ttu-id="b3d9a-202">Bu dosya için bir profil güncelleştirme sayfası şablon olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-202">Use this file as a template for a profile update page.</span></span> |

<span data-ttu-id="b3d9a-203">Merhaba, [, oturum açma veya kaydolma özel ilke bölümünü değiştirme](#modify-your-sign-up-or-sign-in-custom-policy), hello içerik tanımı için yapılandırılmış `api.idpselections`.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-203">In hello [Modify your sign-up or sign-in custom policy section](#modify-your-sign-up-or-sign-in-custom-policy), you configured hello content definition for `api.idpselections`.</span></span> <span data-ttu-id="b3d9a-204">İçerik tanımı hello Azure AD B2C kimlik deneyimi framework ve açıklamalarının tarafından tanınan kimlikleri Hello kümesini aşağıdaki tablonun hello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b3d9a-204">hello full set of content definition IDs that are recognized by hello Azure AD B2C identity experience framework and their descriptions are in hello following table:</span></span>

| <span data-ttu-id="b3d9a-205">İçerik tanımı kimliği</span><span class="sxs-lookup"><span data-stu-id="b3d9a-205">Content definition ID</span></span> | <span data-ttu-id="b3d9a-206">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b3d9a-206">Description</span></span> | 
|-----------------------|-------------|
| <span data-ttu-id="b3d9a-207">*api.Error*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-207">*api.error*</span></span> | <span data-ttu-id="b3d9a-208">**Hata sayfası**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-208">**Error page**.</span></span> <span data-ttu-id="b3d9a-209">Bir özel durum ya da hatayla karşılaşıldığında bu sayfada görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-209">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="b3d9a-210">*api.idpselections*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-210">*api.idpselections*</span></span> | <span data-ttu-id="b3d9a-211">**Kimlik sağlayıcısı seçimi sayfası**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-211">**Identity provider selection page**.</span></span> <span data-ttu-id="b3d9a-212">Bu sayfa, oturum açma sırasında kullanıcı hello sağlayıcıları seçebileceği kimlik listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-212">This page contains a list of identity providers that hello user can choose from during sign-in.</span></span> <span data-ttu-id="b3d9a-213">Bu, Kurumsal kimlik sağlayıcıları, Facebook ve Google + gibi sosyal kimlik sağlayıcıları ya da yerel hesaplar seçeneklerdir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-213">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="b3d9a-214">*api.idpselections.Signup*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-214">*api.idpselections.signup*</span></span> | <span data-ttu-id="b3d9a-215">**Kimlik sağlayıcısı seçimi için kaydolma**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-215">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="b3d9a-216">Bu sayfa kullanıcı hello sağlayıcıları kayıt sırasında seçebileceği kimlik listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-216">This page contains a list of identity providers that hello user can choose from during sign-up.</span></span> <span data-ttu-id="b3d9a-217">Bu, Kurumsal kimlik sağlayıcıları, Facebook ve Google + gibi sosyal kimlik sağlayıcıları ya da yerel hesaplar seçeneklerdir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-217">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="b3d9a-218">*api.localaccountpasswordreset*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-218">*api.localaccountpasswordreset*</span></span> | <span data-ttu-id="b3d9a-219">**Parolanızı mı unuttunuz sayfasını**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-219">**Forgot password page**.</span></span> <span data-ttu-id="b3d9a-220">Bu sayfa bir formu içeren hello kullanıcı parola sıfırlama tooinitiate tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-220">This page contains a form that hello user must complete tooinitiate a password reset.</span></span>  |
| <span data-ttu-id="b3d9a-221">*api.localaccountsignin*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-221">*api.localaccountsignin*</span></span> | <span data-ttu-id="b3d9a-222">**Yerel hesap oturum açma sayfası**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-222">**Local account sign-in page**.</span></span> <span data-ttu-id="b3d9a-223">Bu sayfa bir e-posta adresi veya bir kullanıcı adı göre yerel bir hesap ile oturum imzalamak için bir oturum açma formu içerir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-223">This page contains a sign-in form for signing in with a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="b3d9a-224">Merhaba form, metin giriş kutusu ve parola giriş kutusu içerebilir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-224">hello form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="b3d9a-225">*api.localaccountsignup*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-225">*api.localaccountsignup*</span></span> | <span data-ttu-id="b3d9a-226">**Yerel hesap kayıt sayfasına**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-226">**Local account sign-up page**.</span></span> <span data-ttu-id="b3d9a-227">Bu sayfa bir e-posta adresi veya bir kullanıcı adı göre yerel bir hesap için kaydolduğunuz için bir kayıt formu içerir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-227">This page contains a sign-up form for signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="b3d9a-228">Merhaba form metin giriş kutusu, bir parola giriş kutusu, bir radyo düğmesi, tek seçimlik açılan kutuları ve çoklu seçim onay kutuları gibi çeşitli giriş denetimlerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-228">hello form can contain various input controls, such as a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="b3d9a-229">*api.phonefactor*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-229">*api.phonefactor*</span></span> | <span data-ttu-id="b3d9a-230">**Çok faktörlü kimlik doğrulaması sayfası**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-230">**Multi-factor authentication page**.</span></span> <span data-ttu-id="b3d9a-231">Bu sayfada, kullanıcıların telefon numaralarına (metin veya sesli kullanarak) kaydolma veya oturum açma sırasında doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-231">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="b3d9a-232">*api.selfasserted*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-232">*api.selfasserted*</span></span> | <span data-ttu-id="b3d9a-233">**Sosyal hesap kayıt sayfası**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-233">**Social account sign-up page**.</span></span> <span data-ttu-id="b3d9a-234">Bu sayfa, bunlar Facebook veya Google + gibi sosyal kimlik sağlayıcısından var olan bir hesabı kullanarak kaydolduğunuzda, kullanıcılar tamamlamalısınız bir kayıt formu içerir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-234">This page contains a sign-up form that users must complete when they sign up by using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="b3d9a-235">Bu sayfa hello parola giriş alanları dışında sosyal hesap kayıt sayfası, önceki benzer toohello içindir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-235">This page is similar toohello preceding social account sign-up page, except for hello password entry fields.</span></span> |
| <span data-ttu-id="b3d9a-236">*api.selfasserted.profileupdate*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-236">*api.selfasserted.profileupdate*</span></span> | <span data-ttu-id="b3d9a-237">**Profil güncelleştirme sayfası**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-237">**Profile update page**.</span></span> <span data-ttu-id="b3d9a-238">Bu sayfa kullanıcı profillerini tooupdate kullanabileceğiniz bir form içerir.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-238">This page contains a form that users can use tooupdate their profile.</span></span> <span data-ttu-id="b3d9a-239">Bu sayfa benzer toohello sosyal hesap kaydolma, hello parola giriş alanları dışında sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-239">This page is similar toohello social account sign-up page, except for hello password entry fields.</span></span> |
| <span data-ttu-id="b3d9a-240">*api.signuporsignin*</span><span class="sxs-lookup"><span data-stu-id="b3d9a-240">*api.signuporsignin*</span></span> | <span data-ttu-id="b3d9a-241">**Birleşik kayıt veya oturum açma sayfası**.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-241">**Unified sign-up or sign-in page**.</span></span> <span data-ttu-id="b3d9a-242">Bu sayfa, kaydolma ve oturum açma Kurumsal kimlik sağlayıcıları, Facebook veya Google + veya yerel hesaplar gibi sosyal kimlik sağlayıcıları kullanan kullanıcılar, her iki hello işler.</span><span class="sxs-lookup"><span data-stu-id="b3d9a-242">This page handles both hello sign-up and sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="b3d9a-243">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b3d9a-243">Next steps</span></span>

<span data-ttu-id="b3d9a-244">Özelleştirilebilir kullanıcı Arabirimi öğeleri hakkında ek bilgi için bkz: [yerleşik ilkeleri için kullanıcı Arabirimi özelleştirme için başvuru kılavuzu](active-directory-b2c-reference-ui-customization.md).</span><span class="sxs-lookup"><span data-stu-id="b3d9a-244">For additional information about UI elements that can be customized, see [reference guide for UI customization for built-in policies](active-directory-b2c-reference-ui-customization.md).</span></span>
