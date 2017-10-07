---
title: "aaaSetting adlı kimlik doğrulama kimlik bilgilerini ayarlama | Microsoft Docs"
description: "Visual Studio tooauthenticate istekleri tooAzure toopublish Visual Studio veya toomonitor var olan bir uygulama tooAzure kullanabileceğiniz tootooprovide kimlik bilgileri bulut hizmeti nasıl bilgi edinin... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="8d93b-103">Adlandırılmış kimlik doğrulama kimlik bilgilerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="8d93b-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="8d93b-104">bir uygulama tooAzure Visual Studio veya toomonitor var olan bir bulut hizmetini toopublish, kimlik bilgilerini sağlamanız gerekir istekleri tooAzure Visual Studio tooauthenticate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d93b-104">toopublish an application tooAzure from Visual Studio or toomonitor an existing cloud service, you must provide credentials that Visual Studio can use tooauthenticate requests tooAzure.</span></span> <span data-ttu-id="8d93b-105">Visual Studio'da, bu kimlik bilgileri tooprovide içinde nerede imzalayabilirsiniz çeşitli yerlerde vardır.</span><span class="sxs-lookup"><span data-stu-id="8d93b-105">There are several places in Visual Studio where you can sign in tooprovide these credentials.</span></span> <span data-ttu-id="8d93b-106">Örneğin, Sunucu Gezgini hello hello hello kısayol menüsünü açabilirsiniz **Azure** düğümü seçin **tooMicrosoft Azure aboneliğine Bağlan...** . Oturum açtığınızda Visual Studio'da Azure hesabınızla ilişkili hello abonelik bilgilerini kullanılabilir ve daha fazla toodo sahip bir şey yok.</span><span class="sxs-lookup"><span data-stu-id="8d93b-106">For example, from hello Server Explorer, you can open hello shortcut menu for hello **Azure** node and choose **Connect tooMicrosoft Azure Subscription...**. When you sign in, hello subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have toodo.</span></span>

<span data-ttu-id="8d93b-107">Azure araçlarını da destekler kimlik bilgileri, sağlama daha eski bir şekilde hello abonelik dosyasını (.publishsettings) kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8d93b-107">Azure Tools also supports an older way of providing credentials, using hello subscription file (.publishsettings file).</span></span> <span data-ttu-id="8d93b-108">Bu konu Azure SDK 2.2 hala desteklenmektedir bu yöntem açıklar.</span><span class="sxs-lookup"><span data-stu-id="8d93b-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="8d93b-109">kimlik doğrulama tooAzure için öğeleri izleyen hello gereklidir:</span><span class="sxs-lookup"><span data-stu-id="8d93b-109">hello following items are required for authentication tooAzure:</span></span>

* <span data-ttu-id="8d93b-110">Abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="8d93b-110">Your subscription ID</span></span>
* <span data-ttu-id="8d93b-111">Geçerli bir X.509 v3 sertifikası</span><span class="sxs-lookup"><span data-stu-id="8d93b-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="8d93b-112">Hello hello X.509 v3 sertifikanın anahtar uzunluğu en az 2048 bit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8d93b-112">hello length of hello X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="8d93b-113">Azure, bu gereksinimi karşılamıyor veya geçerli olmayan herhangi bir sertifikayı reddeder.</span><span class="sxs-lookup"><span data-stu-id="8d93b-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="8d93b-114">Visual Studio abonelik Kimliğinizi hello sertifika verileri ile birlikte kimlik bilgileri olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="8d93b-114">Visual Studio uses your subscription ID together with hello certificate data as credentials.</span></span> <span data-ttu-id="8d93b-115">Merhaba uygun kimlik bilgilerini hello sertifika için bir ortak anahtar içeren hello abonelik dosyasında (.publishsettings dosyasını) başvurulur.</span><span class="sxs-lookup"><span data-stu-id="8d93b-115">hello appropriate credentials are referenced in hello subscription file (.publishsettings file), which contains a public key for hello certificate.</span></span> <span data-ttu-id="8d93b-116">Merhaba abonelik dosyası birden fazla aboneliğiniz için kimlik bilgileri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8d93b-116">hello subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="8d93b-117">Merhaba hello abonelik bilgilerini Düzenle **yeni/Düzenle abonelik** iletişim kutusunda, bu konunun ilerleyen bölümlerinde açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="8d93b-117">You can edit hello subscription information from hello **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="8d93b-118">Toocreate bir sertifika kendiniz istiyorsanız toohello yönergelerinde başvurabilir [oluşturun ve Azure için yönetim sertifikası karşıya](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) ve hello sertifika toohello el ile karşıya [Klasik Azure portalı ](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="8d93b-118">If you want toocreate a certificate yourself, you can refer toohello instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload hello certificate toohello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="8d93b-119">Visual Studio bulut hizmetlerinizi olmayan toomanage gerektirir bu kimlik bilgileri gerekli tooauthenticate aynı kimlik bilgileri isteği hello Azure storage hizmetlerine karşı hello.</span><span class="sxs-lookup"><span data-stu-id="8d93b-119">These credentials that Visual Studio requires toomanage your cloud services aren’t hello same credentials that are required tooauthenticate a request against hello Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="8d93b-120">İçeri aktarma, ayarlama veya Visual Studio'da kimlik doğrulama bilgilerini Düzenle</span><span class="sxs-lookup"><span data-stu-id="8d93b-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="8d93b-121">İçeri aktarma, ayarlama veya hello kimlik doğrulama kimlik bilgilerinizi değiştirmek **yeni abonelik** eylem aşağıdaki hello gerçekleştirirseniz görünür iletişim kutusu:</span><span class="sxs-lookup"><span data-stu-id="8d93b-121">You can import, set up, or modify your authentication credentials in hello **New Subscription** dialog box, which appears if you perform hello following action:</span></span>

* <span data-ttu-id="8d93b-122">İçinde **Sunucu Gezgini**açın hello hello kısayol menüsünü **Azure** düğümü seçin **yönetin ve filtre abonelikleri...** , hello seçin **sertifikaları** sekmesini tıklatın ve hello aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="8d93b-122">In **Server Explorer**, open hello shortcut menu for hello **Azure** node, choose **Manage and Filter Subscriptions...**, choose hello **Certificates** tab, and do one of hello following:</span></span>

    * <span data-ttu-id="8d93b-123">Seçin **alma** tooopen hello Microsoft Azure abonelikleri alma iletişim burada indirebilirsiniz hello için hello abonelikleri dosyası şu anda yüklenen abonelik, Gözat tooits konumu karşıdan yükleyip kullanmak için alma kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="8d93b-123">Choose **Import** tooopen hello Import Microsoft Azure Subscriptions dialog where you can download hello  subscriptions file for hello currently loaded subscription, browse tooits download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="8d93b-124">Seçin **yeni** tooopen hello Yeni Abonelik iletişim burada ayarlayabilirsiniz kimlik doğrulaması kullanmak için yeni bir abonelik.</span><span class="sxs-lookup"><span data-stu-id="8d93b-124">Choose **New** tooopen hello New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="8d93b-125">Seçin **Düzenle** (sonra etkin aboneliğinizi seçme) burada düzenleyebilirsiniz kimlik doğrulaması kullanmak için mevcut bir aboneliğe tooopen hello abonelik Düzenle iletişim.</span><span class="sxs-lookup"><span data-stu-id="8d93b-125">Choose **Edit** (after choosing your active subscription) tooopen hello Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="8d93b-126">Merhaba aşağıdaki yordamı varsayar bu hello **yeni abonelik** iletişim kutusunu açın.</span><span class="sxs-lookup"><span data-stu-id="8d93b-126">hello following procedure assumes that hello **New Subscription** dialog box is open.</span></span>

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="8d93b-127">Visual Studio'da kimlik doğrulama kimlik bilgileri tooset</span><span class="sxs-lookup"><span data-stu-id="8d93b-127">tooset up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="8d93b-128">Merhaba, **varolan bir sertifikayı seçin** kimlik doğrulama listesi için bir sertifika seçin.</span><span class="sxs-lookup"><span data-stu-id="8d93b-128">In hello **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="8d93b-129">Merhaba seçin **hello tam yol Kopyala** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="8d93b-129">Choose hello **Copy hello full path** link.</span></span> <span data-ttu-id="8d93b-130">Merhaba hello sertifika (.cer dosyası) kopyalanan toohello Pano yoludur.</span><span class="sxs-lookup"><span data-stu-id="8d93b-130">hello path for hello certificate (.cer file) is copied toohello Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="8d93b-131">toopublish Azure uygulamanızı Visual Studio'dan Bu sertifika toohello yüklemelisiniz [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8d93b-131">toopublish your Azure application from Visual Studio, you must upload this certificate toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="8d93b-132">tooupload hello sertifika toohello Azure portalı:</span><span class="sxs-lookup"><span data-stu-id="8d93b-132">tooupload hello certificate toohello Azure portal:</span></span>

   1. <span data-ttu-id="8d93b-133">Açık hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8d93b-133">Open hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="8d93b-134">İstenirse, toohello Portalı'nda oturum açın ve ardından çok gidin**ayarları**, **yönetim sertifikaları**.</span><span class="sxs-lookup"><span data-stu-id="8d93b-134">If prompted, sign in toohello portal and then navigate too**Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="8d93b-135">Merhaba yönetim sertifikaları bölmesinde seçin **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="8d93b-135">In hello Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="8d93b-136">Azure aboneliğinizi seçin, oluşturulan yeni hello .cer dosyasının tam yolunu hello yapıştırın ve **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="8d93b-136">Select your Azure subscription, paste hello full path of hello .cer file that you just created, and choose **Upload**.</span></span>
