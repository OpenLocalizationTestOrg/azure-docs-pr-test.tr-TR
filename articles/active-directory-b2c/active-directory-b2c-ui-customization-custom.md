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
ms.openlocfilehash: d5a3c0a323b31696d39e3d2b36317dec3a2337d7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a><span data-ttu-id="5df4f-103">Azure Active Directory B2C: Kullanıcı Arabirimi özelleştirme özel bir ilke yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-103">Azure Active Directory B2C: Configure UI customization in a custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="5df4f-104">Bu makalede tamamladıktan sonra kaydolma ve oturum açma özel bir ilke ile marka ve görünümüne sahip olur.</span><span class="sxs-lookup"><span data-stu-id="5df4f-104">After you complete this article, you will have a sign-up and sign-in custom policy with your brand and appearance.</span></span> <span data-ttu-id="5df4f-105">Azure Active Directory B2C ile kullanıcılara sunulan HTML ve CSS içeriğin neredeyse tam denetim elde (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="5df4f-105">With Azure Active Directory B2C (Azure AD B2C), you get nearly full control of the HTML and CSS content that's presented to users.</span></span> <span data-ttu-id="5df4f-106">Özel bir ilke kullandığınızda, kullanıcı arabirimini özelleştirme XML'de Azure portalında denetimleri kullanmak yerine yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-106">When you use a custom policy, you configure UI customization in XML instead of using controls in the Azure portal.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5df4f-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5df4f-107">Prerequisites</span></span>

<span data-ttu-id="5df4f-108">Başlamadan önce tamamlamanız [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="5df4f-108">Before you begin, complete [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="5df4f-109">Çalışma özel bir ilke için kaydolma ve oturum açma yerel hesaplara sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5df4f-109">You should have a working custom policy for sign-up and sign-in with local accounts.</span></span>

## <a name="page-ui-customization"></a><span data-ttu-id="5df4f-110">Sayfanın UI Özelleştirme</span><span class="sxs-lookup"><span data-stu-id="5df4f-110">Page UI customization</span></span>

<span data-ttu-id="5df4f-111">Sayfanın UI Özelleştirme özelliğini kullanarak, herhangi bir özel ilke görünümünü özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5df4f-111">By using the page UI customization feature, you can customize the look and feel of any custom policy.</span></span> <span data-ttu-id="5df4f-112">Ayrıca, marka ve uygulama ve Azure AD B2C arasında visual tutarlılık koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5df4f-112">You can also maintain brand and visual consistency between your application and Azure AD B2C.</span></span>

<span data-ttu-id="5df4f-113">İşte nasıl çalışır?: Azure AD B2C, müşterinizin tarayıcıda kodu çalıştırır ve adlı modern bir yaklaşım kullanır [çıkış noktaları arası kaynak paylaşımı (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="5df4f-113">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span> <span data-ttu-id="5df4f-114">İlk olarak, özelleştirilmiş HTML içerikle özel ilkesindeki bir URL belirtin.</span><span class="sxs-lookup"><span data-stu-id="5df4f-114">First, you specify a URL in the custom policy with customized HTML content.</span></span> <span data-ttu-id="5df4f-115">Azure AD B2C, URL'den yüklenir ve ardından sayfanın müşteriye görüntüleyen HTML içeriğe sahip kullanıcı Arabirimi öğeleri birleştirir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-115">Azure AD B2C merges UI elements with the HTML content that's loaded from your URL and then displays the page to the customer.</span></span>

## <a name="create-your-html5-content"></a><span data-ttu-id="5df4f-116">HTML5 içerik oluşturma</span><span class="sxs-lookup"><span data-stu-id="5df4f-116">Create your HTML5 content</span></span>

<span data-ttu-id="5df4f-117">HTML başlığında ürününüzün marka adıyla içerik oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5df4f-117">Create HTML content with your product's brand name in the title.</span></span>

1. <span data-ttu-id="5df4f-118">Aşağıdaki HTML kod parçası kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-118">Copy the following HTML snippet.</span></span> <span data-ttu-id="5df4f-119">Doğru biçimlendirilmiş boş bir öğesiyle HTML5 adlı  *\<div ID "API" =\>\</div\>*  içinde bulunan  *\<gövde\>*  etiketler.</span><span class="sxs-lookup"><span data-stu-id="5df4f-119">It is well-formed HTML5 with an empty element called *\<div id="api"\>\</div\>* located within the *\<body\>* tags.</span></span> <span data-ttu-id="5df4f-120">Bu öğe, Azure AD B2C içerik eklenecek nerede gösterir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-120">This element indicates where Azure AD B2C content is to be inserted.</span></span>

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
   ><span data-ttu-id="5df4f-121">Güvenlik nedenleriyle, JavaScript kullanımı için özelleştirme şu anda engelleniyor.</span><span class="sxs-lookup"><span data-stu-id="5df4f-121">For security reasons, the use of JavaScript is currently blocked for customization.</span></span>

2. <span data-ttu-id="5df4f-122">Bir metin düzenleyicisinde kopyalanan parçacığını yapıştırın ve dosyayı farklı Kaydet *özelleştirme ui.html*.</span><span class="sxs-lookup"><span data-stu-id="5df4f-122">Paste the copied snippet in a text editor, and then save the file as *customize-ui.html*.</span></span>

## <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="5df4f-123">Bir Azure Blob storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5df4f-123">Create an Azure Blob storage account</span></span>

>[!NOTE]
> <span data-ttu-id="5df4f-124">Bu makalede, Azure Blob Depolama bizim içeriğini barındırmak için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="5df4f-124">In this article, we use Azure Blob storage to host our content.</span></span> <span data-ttu-id="5df4f-125">İçeriğinizi bir web sunucusunda barındırmak seçebilirsiniz, ancak gerekir [web sunucunuz üzerinde CORS'yi etkinleştirmeniz](https://enable-cors.org/server.html).</span><span class="sxs-lookup"><span data-stu-id="5df4f-125">You can choose to host your content on a web server, but you must [enable CORS on your web server](https://enable-cors.org/server.html).</span></span>

<span data-ttu-id="5df4f-126">Blob depolama alanındaki bu HTML içeriğini barındırmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="5df4f-126">To host this HTML content in Blob storage, do the following:</span></span>

1. <span data-ttu-id="5df4f-127">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5df4f-128">Üzerinde **Hub** menüsünde, select **yeni** > **depolama** > **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-128">On the **Hub** menu, select **New** > **Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="5df4f-129">Benzersiz bir girin **adı** depolama hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="5df4f-129">Enter a unique **Name** for your storage account.</span></span>
4. <span data-ttu-id="5df4f-130">**Dağıtım modeli** kalabileceği **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-130">**Deployment model** can remain **Resource Manager**.</span></span>
5. <span data-ttu-id="5df4f-131">Değişiklik **hesap türü** için **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-131">Change **Account Kind** to **Blob storage**.</span></span>
6. <span data-ttu-id="5df4f-132">**Performans** kalabileceği **standart**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-132">**Performance** can remain **Standard**.</span></span>
7. <span data-ttu-id="5df4f-133">**Çoğaltma** kalabileceği **RA-GRS**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-133">**Replication** can remain **RA-GRS**.</span></span>
8. <span data-ttu-id="5df4f-134">**Erişim katmanı** kalabileceği **etkin**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-134">**Access tier** can remain **Hot**.</span></span>
9. <span data-ttu-id="5df4f-135">**Depolama hizmeti şifrelemesi** kalabileceği **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-135">**Storage service encryption** can remain **Disabled**.</span></span>
10. <span data-ttu-id="5df4f-136">Seçin bir **abonelik** depolama hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="5df4f-136">Select a **Subscription** for your storage account.</span></span>
11. <span data-ttu-id="5df4f-137">Oluşturma bir **kaynak grubu** veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5df4f-137">Create a **Resource group** or select an existing one.</span></span>
12. <span data-ttu-id="5df4f-138">Seçin **coğrafi konum** depolama hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="5df4f-138">Select the **Geographic location** for your storage account.</span></span>
13. <span data-ttu-id="5df4f-139">Depolama hesabını oluşturmak için **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-139">Click **Create** to create the storage account.</span></span>  
    <span data-ttu-id="5df4f-140">Dağıtım tamamlandıktan sonra **depolama hesabı** dikey penceresinde otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="5df4f-140">After the deployment is completed, the **Storage account** blade opens automatically.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="5df4f-141">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5df4f-141">Create a container</span></span>

<span data-ttu-id="5df4f-142">Blob depolama alanına genel bir kapsayıcı oluşturmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="5df4f-142">To create a public container in Blob storage, do the following:</span></span>

1. <span data-ttu-id="5df4f-143">Tıklatın **genel bakış** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5df4f-143">Click the **Overview** tab.</span></span>
2. <span data-ttu-id="5df4f-144">Tıklatın **kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-144">Click **Container**.</span></span>
3. <span data-ttu-id="5df4f-145">İçin **adı**, türü **$root**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-145">For **Name**, type **$root**.</span></span>
4. <span data-ttu-id="5df4f-146">Ayarlama **erişim türüne** için **Blob**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-146">Set **Access type** to **Blob**.</span></span>
5. <span data-ttu-id="5df4f-147">Tıklatın **$root** yeni kapsayıcı açın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-147">Click **$root** to open the new container.</span></span>
6. <span data-ttu-id="5df4f-148">**Karşıya Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-148">Click **Upload**.</span></span>
7. <span data-ttu-id="5df4f-149">Klasör simgesine tıklayın **bir dosya seçin**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-149">Click the folder icon next to **Select a file**.</span></span>
8. <span data-ttu-id="5df4f-150">Git **özelleştirme ui.html**, daha önce içinde oluşturulan [sayfa UI özelleştirme](#the-page-ui-customization-feature) bölüm.</span><span class="sxs-lookup"><span data-stu-id="5df4f-150">Go to **customize-ui.html**, which you created earlier in the [Page UI customization](#the-page-ui-customization-feature) section.</span></span>
9. <span data-ttu-id="5df4f-151">**Karşıya Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-151">Click **Upload**.</span></span>
10. <span data-ttu-id="5df4f-152">Karşıya yüklediğiniz Özelleştir ui.html blob seçin.</span><span class="sxs-lookup"><span data-stu-id="5df4f-152">Select the customize-ui.html blob that you uploaded.</span></span>
11. <span data-ttu-id="5df4f-153">Yanına **URL**, tıklatın **kopya**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-153">Next to **URL**, click **Copy**.</span></span>
12. <span data-ttu-id="5df4f-154">Bir tarayıcıda, kopyalanan URL'sini yapıştırın ve sitesine gidin.</span><span class="sxs-lookup"><span data-stu-id="5df4f-154">In a browser, paste the copied URL, and go to the site.</span></span> <span data-ttu-id="5df4f-155">Site erişilemez, emin olun kapsayıcı erişim türü ayarlanırsa **blob**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-155">If the site is inaccessible, make sure the container access type is set to **blob**.</span></span>

## <a name="configure-cors"></a><span data-ttu-id="5df4f-156">CORS'yi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5df4f-156">Configure CORS</span></span>

<span data-ttu-id="5df4f-157">BLOB Depolama çıkış noktaları arası kaynak paylaşımı için aşağıdakileri yaparak yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="5df4f-157">Configure Blob storage for Cross-Origin Resource Sharing by doing the following:</span></span>

>[!NOTE]
><span data-ttu-id="5df4f-158">Bizim örnek HTML ve CSS içeriğini kullanarak kullanıcı Arabirimi özelleştirme özelliği denemek mi istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="5df4f-158">Want to try out the UI customization feature by using our sample HTML and CSS content?</span></span> <span data-ttu-id="5df4f-159">Sağladık [basit Yardımcısı aracı](active-directory-b2c-reference-ui-customization-helper-tool.md) karşıya yükleyen ve Blob Depolama hesabınıza bizim örnek içeriği yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5df4f-159">We've provided [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures our sample content on your Blob storage account.</span></span> <span data-ttu-id="5df4f-160">Aracı kullanırsanız, İleri için atlayabilirsiniz [oturum açma veya kaydolma özel ilkenizi değiştirmek](#modify-your-sign-up-or-sign-in-custom-policy).</span><span class="sxs-lookup"><span data-stu-id="5df4f-160">If you use the tool, skip ahead to [Modify your sign-up or sign-in custom policy](#modify-your-sign-up-or-sign-in-custom-policy).</span></span>

1. <span data-ttu-id="5df4f-161">Üzerinde **depolama** dikey altında **ayarları**, açık **CORS**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-161">On the **Storage** blade, under **Settings**, open **CORS**.</span></span>
2. <span data-ttu-id="5df4f-162">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-162">Click **Add**.</span></span>
3. <span data-ttu-id="5df4f-163">İçin **çıkış izin**, bir yıldız işareti girin (\*).</span><span class="sxs-lookup"><span data-stu-id="5df4f-163">For **Allowed origins**, type an asterisk (\*).</span></span>
4. <span data-ttu-id="5df4f-164">İçinde **fiillere izin** açılan listesinden, select **almak** ve **seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-164">In the **Allowed verbs** drop-down list, select both **GET** and **OPTIONS**.</span></span>
5. <span data-ttu-id="5df4f-165">İçin **üstbilgileri izin**, bir yıldız işareti girin (\*).</span><span class="sxs-lookup"><span data-stu-id="5df4f-165">For **Allowed headers**, type an asterisk (\*).</span></span>
6. <span data-ttu-id="5df4f-166">İçin **sunulan üstbilgileri**, bir yıldız işareti girin (\*).</span><span class="sxs-lookup"><span data-stu-id="5df4f-166">For **Exposed headers**, type an asterisk (\*).</span></span>
7. <span data-ttu-id="5df4f-167">İçin **en uzun geçerlilik süresi (saniye)**, türü **200**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-167">For **Maximum age (seconds)**, type **200**.</span></span>
8. <span data-ttu-id="5df4f-168">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-168">Click **Add**.</span></span>

## <a name="test-cors"></a><span data-ttu-id="5df4f-169">Test CORS</span><span class="sxs-lookup"><span data-stu-id="5df4f-169">Test CORS</span></span>

<span data-ttu-id="5df4f-170">Aşağıdakileri yaparak hazırsınız olduğunu doğrulama:</span><span class="sxs-lookup"><span data-stu-id="5df4f-170">Validate that you're ready by doing the following:</span></span>

1. <span data-ttu-id="5df4f-171">Git [test cors.org](http://test-cors.org/) Web sitesi, URL'de yapıştırın **uzak URL** kutusu.</span><span class="sxs-lookup"><span data-stu-id="5df4f-171">Go to the [test-cors.org](http://test-cors.org/) website, and then paste the URL in the **Remote URL** box.</span></span>
2. <span data-ttu-id="5df4f-172">Tıklatın **gönderme isteği**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-172">Click **Send Request**.</span></span>  
    <span data-ttu-id="5df4f-173">Bir hata alırsanız, emin olun, [CORS ayarları](#configure-cors) doğrudur.</span><span class="sxs-lookup"><span data-stu-id="5df4f-173">If you receive an error, make sure that your [CORS settings](#configure-cors) are correct.</span></span> <span data-ttu-id="5df4f-174">Tarayıcı önbelleğini temizlemek veya Ctrl + Shift + P tuşuna basarak özel gözatma oturumu açmak gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-174">You might also need to clear your browser cache or open an in-private browsing session by pressing Ctrl+Shift+P.</span></span>

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a><span data-ttu-id="5df4f-175">Oturum açma veya kaydolma özel ilkesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="5df4f-175">Modify your sign-up or sign-in custom policy</span></span>

<span data-ttu-id="5df4f-176">Üst düzey altında  *\<TrustFrameworkPolicy\>*  etiketi, bulmanız gerekir  *\<BuildingBlocks\>*  etiketi.</span><span class="sxs-lookup"><span data-stu-id="5df4f-176">Under the top-level *\<TrustFrameworkPolicy\>* tag, you should find *\<BuildingBlocks\>* tag.</span></span> <span data-ttu-id="5df4f-177">İçinde  *\<BuildingBlocks\>*  etiketler eklemek bir  *\<ContentDefinitions\>*  aşağıdaki örnekte kopyalayarak etiketi.</span><span class="sxs-lookup"><span data-stu-id="5df4f-177">Within the *\<BuildingBlocks\>* tags, add a *\<ContentDefinitions\>* tag by copying the following example.</span></span> <span data-ttu-id="5df4f-178">Değiştir *your_storage_account* depolama hesabınızın adı.</span><span class="sxs-lookup"><span data-stu-id="5df4f-178">Replace *your_storage_account* with the name of your storage account.</span></span>

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a><span data-ttu-id="5df4f-179">Güncelleştirilmiş özel ilkeniz karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="5df4f-179">Upload your updated custom policy</span></span>

1. <span data-ttu-id="5df4f-180">İçinde [Azure portal](https://portal.azure.com), [geçiş Azure AD B2C kiracınızın bağlamına](active-directory-b2c-navigate-to-b2c-context.md)ve ardından açın **Azure AD B2C** dikey.</span><span class="sxs-lookup"><span data-stu-id="5df4f-180">In the [Azure portal](https://portal.azure.com), [switch into the context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open the **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="5df4f-181">Tıklatın **tüm ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-181">Click **All Policies**.</span></span>
3. <span data-ttu-id="5df4f-182">Tıklatın **karşıya İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-182">Click **Upload Policy**.</span></span>
4. <span data-ttu-id="5df4f-183">Karşıya yükleme `SignUpOrSignin.xml` ile  *\<ContentDefinitions\>*  daha önce eklediğiniz etiketi.</span><span class="sxs-lookup"><span data-stu-id="5df4f-183">Upload `SignUpOrSignin.xml` with the *\<ContentDefinitions\>* tag that you added previously.</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="5df4f-184">Özel ilke kullanarak test **Şimdi Çalıştır**</span><span class="sxs-lookup"><span data-stu-id="5df4f-184">Test the custom policy by using **Run now**</span></span>

1. <span data-ttu-id="5df4f-185">Üzerinde **Azure AD B2C** dikey penceresinde, Git **tüm ilkeler**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-185">On the **Azure AD B2C** blade, go to **All polices**.</span></span>
2. <span data-ttu-id="5df4f-186">Karşıya yüklenen ve'ı tıklatın özel ilkeyi seçin **Şimdi Çalıştır** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5df4f-186">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="5df4f-187">Bir e-posta adresi kullanarak kaydolabilirsiniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-187">You should be able to sign up by using an email address.</span></span>

## <a name="reference"></a><span data-ttu-id="5df4f-188">Başvuru</span><span class="sxs-lookup"><span data-stu-id="5df4f-188">Reference</span></span>

<span data-ttu-id="5df4f-189">Buraya kullanıcı arabirimini özelleştirme örnek şablonları bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5df4f-189">You can find sample templates for UI customization here:</span></span>

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

<span data-ttu-id="5df4f-190">Aşağıdaki HTML dosyaları sample_templates/wingtip klasör içerir:</span><span class="sxs-lookup"><span data-stu-id="5df4f-190">The sample_templates/wingtip folder contains the following HTML files:</span></span>

| <span data-ttu-id="5df4f-191">HTML5 şablonu</span><span class="sxs-lookup"><span data-stu-id="5df4f-191">HTML5 template</span></span> | <span data-ttu-id="5df4f-192">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5df4f-192">Description</span></span> |
|----------------|-------------|
| <span data-ttu-id="5df4f-193">*phonefactor.HTML*</span><span class="sxs-lookup"><span data-stu-id="5df4f-193">*phonefactor.html*</span></span> | <span data-ttu-id="5df4f-194">Bu dosyayı bir çok faktörlü kimlik doğrulaması sayfası için bir şablon olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-194">Use this file as a template for a multi-factor authentication page.</span></span> |
| <span data-ttu-id="5df4f-195">*ResetPassword.HTML*</span><span class="sxs-lookup"><span data-stu-id="5df4f-195">*resetpassword.html*</span></span> | <span data-ttu-id="5df4f-196">Bu dosya için bir şablon olarak kullanmak bir parolanızı mı unuttunuz sayfasını.</span><span class="sxs-lookup"><span data-stu-id="5df4f-196">Use this file as a template for a forgot password page.</span></span> |
| <span data-ttu-id="5df4f-197">*selfasserted.HTML*</span><span class="sxs-lookup"><span data-stu-id="5df4f-197">*selfasserted.html*</span></span> | <span data-ttu-id="5df4f-198">Bu dosya, sosyal hesap kayıt sayfası, yerel hesap kaydolma sayfası veya bir yerel hesap oturum açma sayfası için bir şablon olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-198">Use this file as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span></span> |
| <span data-ttu-id="5df4f-199">*Unified.HTML*</span><span class="sxs-lookup"><span data-stu-id="5df4f-199">*unified.html*</span></span> | <span data-ttu-id="5df4f-200">Bu dosyayı bir birleşik kayıt veya oturum açma sayfası için bir şablon olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-200">Use this file as a template for a unified sign-up or sign-in page.</span></span> |
| <span data-ttu-id="5df4f-201">*updateprofile.HTML*</span><span class="sxs-lookup"><span data-stu-id="5df4f-201">*updateprofile.html*</span></span> | <span data-ttu-id="5df4f-202">Bu dosya için bir profil güncelleştirme sayfası şablon olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="5df4f-202">Use this file as a template for a profile update page.</span></span> |

<span data-ttu-id="5df4f-203">İçinde [, oturum açma veya kaydolma özel ilke bölümünü değiştirme](#modify-your-sign-up-or-sign-in-custom-policy), içerik tanımı yapılandırılmış `api.idpselections`.</span><span class="sxs-lookup"><span data-stu-id="5df4f-203">In the [Modify your sign-up or sign-in custom policy section](#modify-your-sign-up-or-sign-in-custom-policy), you configured the content definition for `api.idpselections`.</span></span> <span data-ttu-id="5df4f-204">Tam bir içerik kümesinin Azure AD B2C kimlik deneyimi framework ve açıklamalarının tarafından tanınan tanımı kimlikleri aşağıdaki tabloda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5df4f-204">The full set of content definition IDs that are recognized by the Azure AD B2C identity experience framework and their descriptions are in the following table:</span></span>

| <span data-ttu-id="5df4f-205">İçerik tanımı kimliği</span><span class="sxs-lookup"><span data-stu-id="5df4f-205">Content definition ID</span></span> | <span data-ttu-id="5df4f-206">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5df4f-206">Description</span></span> | 
|-----------------------|-------------|
| <span data-ttu-id="5df4f-207">*api.Error*</span><span class="sxs-lookup"><span data-stu-id="5df4f-207">*api.error*</span></span> | <span data-ttu-id="5df4f-208">**Hata sayfası**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-208">**Error page**.</span></span> <span data-ttu-id="5df4f-209">Bir özel durum ya da hatayla karşılaşıldığında bu sayfada görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-209">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="5df4f-210">*api.idpselections*</span><span class="sxs-lookup"><span data-stu-id="5df4f-210">*api.idpselections*</span></span> | <span data-ttu-id="5df4f-211">**Kimlik sağlayıcısı seçimi sayfası**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-211">**Identity provider selection page**.</span></span> <span data-ttu-id="5df4f-212">Bu sayfa, oturum açma sırasında seçebileceği kimlik sağlayıcıları listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-212">This page contains a list of identity providers that the user can choose from during sign-in.</span></span> <span data-ttu-id="5df4f-213">Bu, Kurumsal kimlik sağlayıcıları, Facebook ve Google + gibi sosyal kimlik sağlayıcıları ya da yerel hesaplar seçeneklerdir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-213">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="5df4f-214">*api.idpselections.Signup*</span><span class="sxs-lookup"><span data-stu-id="5df4f-214">*api.idpselections.signup*</span></span> | <span data-ttu-id="5df4f-215">**Kimlik sağlayıcısı seçimi için kaydolma**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-215">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="5df4f-216">Bu sayfa kullanıcı kayıt sırasında seçebileceği kimlik sağlayıcıları listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-216">This page contains a list of identity providers that the user can choose from during sign-up.</span></span> <span data-ttu-id="5df4f-217">Bu, Kurumsal kimlik sağlayıcıları, Facebook ve Google + gibi sosyal kimlik sağlayıcıları ya da yerel hesaplar seçeneklerdir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-217">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="5df4f-218">*api.localaccountpasswordreset*</span><span class="sxs-lookup"><span data-stu-id="5df4f-218">*api.localaccountpasswordreset*</span></span> | <span data-ttu-id="5df4f-219">**Parolanızı mı unuttunuz sayfasını**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-219">**Forgot password page**.</span></span> <span data-ttu-id="5df4f-220">Bu sayfa kullanıcı parola sıfırlama başlatmak için tamamlamanız gereken bir form içerir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-220">This page contains a form that the user must complete to initiate a password reset.</span></span>  |
| <span data-ttu-id="5df4f-221">*api.localaccountsignin*</span><span class="sxs-lookup"><span data-stu-id="5df4f-221">*api.localaccountsignin*</span></span> | <span data-ttu-id="5df4f-222">**Yerel hesap oturum açma sayfası**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-222">**Local account sign-in page**.</span></span> <span data-ttu-id="5df4f-223">Bu sayfa bir e-posta adresi veya bir kullanıcı adı göre yerel bir hesap ile oturum imzalamak için bir oturum açma formu içerir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-223">This page contains a sign-in form for signing in with a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="5df4f-224">Form, metin giriş kutusu ve parola giriş kutusu içerebilir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-224">The form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="5df4f-225">*api.localaccountsignup*</span><span class="sxs-lookup"><span data-stu-id="5df4f-225">*api.localaccountsignup*</span></span> | <span data-ttu-id="5df4f-226">**Yerel hesap kayıt sayfasına**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-226">**Local account sign-up page**.</span></span> <span data-ttu-id="5df4f-227">Bu sayfa bir e-posta adresi veya bir kullanıcı adı göre yerel bir hesap için kaydolduğunuz için bir kayıt formu içerir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-227">This page contains a sign-up form for signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="5df4f-228">Form, metin giriş kutusu, bir parola giriş kutusu, bir radyo düğmesi, tek seçimlik açılan kutuları ve çoklu seçim onay kutuları gibi çeşitli giriş denetimlerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-228">The form can contain various input controls, such as a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="5df4f-229">*api.phonefactor*</span><span class="sxs-lookup"><span data-stu-id="5df4f-229">*api.phonefactor*</span></span> | <span data-ttu-id="5df4f-230">**Çok faktörlü kimlik doğrulaması sayfası**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-230">**Multi-factor authentication page**.</span></span> <span data-ttu-id="5df4f-231">Bu sayfada, kullanıcıların telefon numaralarına (metin veya sesli kullanarak) kaydolma veya oturum açma sırasında doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5df4f-231">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="5df4f-232">*api.selfasserted*</span><span class="sxs-lookup"><span data-stu-id="5df4f-232">*api.selfasserted*</span></span> | <span data-ttu-id="5df4f-233">**Sosyal hesap kayıt sayfası**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-233">**Social account sign-up page**.</span></span> <span data-ttu-id="5df4f-234">Bu sayfa, bunlar Facebook veya Google + gibi sosyal kimlik sağlayıcısından var olan bir hesabı kullanarak kaydolduğunuzda, kullanıcılar tamamlamalısınız bir kayıt formu içerir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-234">This page contains a sign-up form that users must complete when they sign up by using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="5df4f-235">Bu sayfa, önceki sosyal hesap kayıt sayfası, parola girdi alanlarının dışında benzerdir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-235">This page is similar to the preceding social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="5df4f-236">*api.selfasserted.profileupdate*</span><span class="sxs-lookup"><span data-stu-id="5df4f-236">*api.selfasserted.profileupdate*</span></span> | <span data-ttu-id="5df4f-237">**Profil güncelleştirme sayfası**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-237">**Profile update page**.</span></span> <span data-ttu-id="5df4f-238">Bu sayfa, kullanıcıların kendi profilini güncelleştirmek için kullanabileceği bir form içerir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-238">This page contains a form that users can use to update their profile.</span></span> <span data-ttu-id="5df4f-239">Bu sayfa, sosyal hesap kaydolma sayfası, parola girdi alanlarının dışında benzerdir.</span><span class="sxs-lookup"><span data-stu-id="5df4f-239">This page is similar to the social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="5df4f-240">*api.signuporsignin*</span><span class="sxs-lookup"><span data-stu-id="5df4f-240">*api.signuporsignin*</span></span> | <span data-ttu-id="5df4f-241">**Birleşik kayıt veya oturum açma sayfası**.</span><span class="sxs-lookup"><span data-stu-id="5df4f-241">**Unified sign-up or sign-in page**.</span></span> <span data-ttu-id="5df4f-242">Bu sayfa, hem kaydolma ve oturum açma Kurumsal kimlik sağlayıcıları, Facebook veya Google + veya yerel hesaplar gibi sosyal kimlik sağlayıcıları kullanan kullanıcıların işler.</span><span class="sxs-lookup"><span data-stu-id="5df4f-242">This page handles both the sign-up and sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="5df4f-243">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5df4f-243">Next steps</span></span>

<span data-ttu-id="5df4f-244">Özelleştirilebilir kullanıcı Arabirimi öğeleri hakkında ek bilgi için bkz: [yerleşik ilkeleri için kullanıcı Arabirimi özelleştirme için başvuru kılavuzu](active-directory-b2c-reference-ui-customization.md).</span><span class="sxs-lookup"><span data-stu-id="5df4f-244">For additional information about UI elements that can be customized, see [reference guide for UI customization for built-in policies](active-directory-b2c-reference-ui-customization.md).</span></span>
