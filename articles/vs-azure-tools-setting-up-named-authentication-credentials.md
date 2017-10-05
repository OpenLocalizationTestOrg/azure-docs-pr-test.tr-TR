---
title: "Adlı kimlik doğrulama kimlik bilgilerini ayarlama | Microsoft Docs"
description: "İçin kimlik bilgilerini sağlamak için Visual Studio Azure uygulamaya Visual Studio'dan yayımlamak için veya var olan bir bulut hizmetini izlemek için istekleri Azure kimlik doğrulaması için nasıl kullanabileceğinizi öğrenin... "
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
ms.openlocfilehash: c486676a70e195ec85ad40540ea4b7caaa86bc48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="275b5-103">Adlandırılmış kimlik doğrulama kimlik bilgilerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="275b5-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="275b5-104">Azure uygulama Visual Studio'dan yayımlamak ya da var olan bir bulut hizmetini izlemek için Visual Studio Azure isteklerine kimliğini doğrulamak için kullanabileceğiniz kimlik bilgilerini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="275b5-104">To publish an application to Azure from Visual Studio or to monitor an existing cloud service, you must provide credentials that Visual Studio can use to authenticate requests to Azure.</span></span> <span data-ttu-id="275b5-105">Visual Studio'da burada bu kimlik bilgilerini sağlamak üzere oturum içinde çeşitli yerlerde vardır.</span><span class="sxs-lookup"><span data-stu-id="275b5-105">There are several places in Visual Studio where you can sign in to provide these credentials.</span></span> <span data-ttu-id="275b5-106">Örneğin, Sunucu Gezgini'nden için kısayol menüsünü açarak **Azure** düğümü seçin **Microsoft Azure aboneliğine Bağlan...** . Oturum açtığınızda Visual Studio'da Azure hesabınızla ilişkili abonelik bilgilerini kullanılabilir ve yapmanız gereken başka bir şey yok.</span><span class="sxs-lookup"><span data-stu-id="275b5-106">For example, from the Server Explorer, you can open the shortcut menu for the **Azure** node and choose **Connect to Microsoft Azure Subscription...**. When you sign in, the subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have to do.</span></span>

<span data-ttu-id="275b5-107">Azure araçlarını da destekler kimlik bilgileri, sağlama daha eski bir yol abonelik dosyasını (.publishsettings) kullanarak.</span><span class="sxs-lookup"><span data-stu-id="275b5-107">Azure Tools also supports an older way of providing credentials, using the subscription file (.publishsettings file).</span></span> <span data-ttu-id="275b5-108">Bu konu Azure SDK 2.2 hala desteklenmektedir bu yöntem açıklar.</span><span class="sxs-lookup"><span data-stu-id="275b5-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="275b5-109">Aşağıdaki öğeler, Azure için kimlik doğrulaması için gereklidir:</span><span class="sxs-lookup"><span data-stu-id="275b5-109">The following items are required for authentication to Azure:</span></span>

* <span data-ttu-id="275b5-110">Abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="275b5-110">Your subscription ID</span></span>
* <span data-ttu-id="275b5-111">Geçerli bir X.509 v3 sertifikası</span><span class="sxs-lookup"><span data-stu-id="275b5-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="275b5-112">X.509 v3 sertifikası'nın anahtar uzunluğu en az 2048 bit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="275b5-112">The length of the X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="275b5-113">Azure, bu gereksinimi karşılamıyor veya geçerli olmayan herhangi bir sertifikayı reddeder.</span><span class="sxs-lookup"><span data-stu-id="275b5-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="275b5-114">Visual Studio abonelik Kimliğinizi sertifika verileri ile birlikte kimlik bilgileri olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="275b5-114">Visual Studio uses your subscription ID together with the certificate data as credentials.</span></span> <span data-ttu-id="275b5-115">Uygun kimlik bilgilerini içeren bir ortak anahtar sertifikası için abonelik dosyasında (.publishsettings dosyasını) başvurulur.</span><span class="sxs-lookup"><span data-stu-id="275b5-115">The appropriate credentials are referenced in the subscription file (.publishsettings file), which contains a public key for the certificate.</span></span> <span data-ttu-id="275b5-116">Abonelik dosyası birden fazla aboneliğiniz için kimlik bilgileri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="275b5-116">The subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="275b5-117">Abonelik bilgileri düzenleyebilirsiniz **yeni/Düzenle abonelik** iletişim kutusunda, bu konunun ilerleyen bölümlerinde açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="275b5-117">You can edit the subscription information from the **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="275b5-118">Bir sertifika kendiniz oluşturmak istiyorsanız,'ndaki yönergeleri başvurabilirsiniz [oluşturun ve Azure için yönetim sertifikası karşıya](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) ve sertifikayı el ile karşıya [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="275b5-118">If you want to create a certificate yourself, you can refer to the instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload the certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="275b5-119">Bulut hizmetleri yönetmek için Visual Studio gerektirir bu kimlik bilgileri isteği Azure storage hizmetlerine karşı kimlik doğrulaması için gerekli kimlik bilgilerini değil.</span><span class="sxs-lookup"><span data-stu-id="275b5-119">These credentials that Visual Studio requires to manage your cloud services aren’t the same credentials that are required to authenticate a request against the Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="275b5-120">İçeri aktarma, ayarlama veya Visual Studio'da kimlik doğrulama bilgilerini Düzenle</span><span class="sxs-lookup"><span data-stu-id="275b5-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="275b5-121">İçeri aktarma, ayarlama veya kimlik doğrulama kimlik bilgilerinizi değiştirmek **yeni abonelik** iletişim kutusunda, şu işlemi gerçekleştirirseniz, görünür:</span><span class="sxs-lookup"><span data-stu-id="275b5-121">You can import, set up, or modify your authentication credentials in the **New Subscription** dialog box, which appears if you perform the following action:</span></span>

* <span data-ttu-id="275b5-122">İçinde **Sunucu Gezgini**, kısayol menüsünü açın **Azure** düğümü seçin **yönetin ve filtre abonelikleri...** , seçin **sertifikaları** sekmesini tıklatın ve aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="275b5-122">In **Server Explorer**, open the shortcut menu for the **Azure** node, choose **Manage and Filter Subscriptions...**, choose the **Certificates** tab, and do one of the following:</span></span>

    * <span data-ttu-id="275b5-123">Seçin **alma** burada indirebilirsiniz abonelikleri dosyanın şu anda yüklenen abonelik için Microsoft Azure abonelikleri alma iletişim kutusunu açmak için indirme konumuna göz atın ve kullanmak için alma kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="275b5-123">Choose **Import** to open the Import Microsoft Azure Subscriptions dialog where you can download the  subscriptions file for the currently loaded subscription, browse to its download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="275b5-124">Seçin **yeni** burada ayarlayabilirsiniz kimlik doğrulaması kullanmak için yeni bir abonelik Yeni Abonelik iletişim kutusunu açın.</span><span class="sxs-lookup"><span data-stu-id="275b5-124">Choose **New** to open the New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="275b5-125">Seçin **Düzenle** (sonra etkin aboneliğinizi seçme) burada düzenleyebilirsiniz kimlik doğrulaması kullanmak için mevcut bir aboneliğe abonelik Düzenle iletişim kutusunu açın.</span><span class="sxs-lookup"><span data-stu-id="275b5-125">Choose **Edit** (after choosing your active subscription) to open the Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="275b5-126">Aşağıdaki yordam varsayar **yeni abonelik** iletişim kutusunu açın.</span><span class="sxs-lookup"><span data-stu-id="275b5-126">The following procedure assumes that the **New Subscription** dialog box is open.</span></span>

### <a name="to-set-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="275b5-127">Visual Studio'da kimlik doğrulama kimlik bilgilerini ayarlamak için</span><span class="sxs-lookup"><span data-stu-id="275b5-127">To set up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="275b5-128">İçinde **varolan bir sertifikayı seçin** kimlik doğrulama listesi için bir sertifika seçin.</span><span class="sxs-lookup"><span data-stu-id="275b5-128">In the **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="275b5-129">Seçin **tam yolunu kopyalamak** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="275b5-129">Choose the **Copy the full path** link.</span></span> <span data-ttu-id="275b5-130">Sertifika (.cer dosyası) yolunu Panoya kopyalandı.</span><span class="sxs-lookup"><span data-stu-id="275b5-130">The path for the certificate (.cer file) is copied to the Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="275b5-131">Azure uygulamanızı Visual Studio'dan yayımlamak için bu sertifikayı karşıya [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="275b5-131">To publish your Azure application from Visual Studio, you must upload this certificate to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="275b5-132">Azure portalına sertifikayı karşıya yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="275b5-132">To upload the certificate to the Azure portal:</span></span>

   1. <span data-ttu-id="275b5-133">[Azure portalı](http://go.microsoft.com/fwlink/p/?LinkID=525040) açın.</span><span class="sxs-lookup"><span data-stu-id="275b5-133">Open the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="275b5-134">İstenirse, portalında oturum açın ve ardından gidin **ayarları**, **yönetim sertifikaları**.</span><span class="sxs-lookup"><span data-stu-id="275b5-134">If prompted, sign in to the portal and then navigate to **Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="275b5-135">Yönetim sertifikaları bölmesinde seçin **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="275b5-135">In the Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="275b5-136">Azure aboneliğinizi seçin, oluşturulan yeni .cer dosyasının tam yolunu yapıştırın ve **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="275b5-136">Select your Azure subscription, paste the full path of the .cer file that you just created, and choose **Upload**.</span></span>
