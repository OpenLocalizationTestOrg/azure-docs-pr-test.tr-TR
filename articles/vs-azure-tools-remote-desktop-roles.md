---
title: "aaaUsing Azure rolleriyle, Uzak Masaüstü'nü | Microsoft Docs"
description: "Azure rolleri ile Uzak Masaüstü'nü kullanma"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="ab6e9-103">Azure rolleri ile Uzak Masaüstü'nü kullanma</span><span class="sxs-lookup"><span data-stu-id="ab6e9-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="ab6e9-104">Uzak Masaüstü Hizmetleri ve Hello Azure SDK kullanarak Azure rolleri ve Azure tarafından barındırılan sanal makinelerin erişebilir.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-104">By using hello Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="ab6e9-105">Visual Studio'da bir Azure bulut hizmeti projesi Uzak Masaüstü Hizmetleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="ab6e9-106">tooenable Uzak Masaüstü Hizmetleri, bir veya daha fazla rolü içeren bir çalışma projesi oluşturun ve sonra tooAzure yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-106">tooenable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it tooAzure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab6e9-107">Sorun giderme veya yalnızca geliştirme için Azure bir rolü erişim.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="ab6e9-108">Merhaba amacı, her bir sanal makinenin diğer istemci uygulamaları toorun Azure uygulamanız, değil toorun belirli bir rolde değil.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-108">hello purpose of each virtual machine is toorun a specific role in your Azure application, not toorun other client applications.</span></span> <span data-ttu-id="ab6e9-109">Toouse Azure toohost herhangi bir amaçla kullanabileceğiniz bir sanal makine istiyorsanız, Azure sanal makineleri Sunucu Gezgini'nden erişme bakın.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-109">If you want toouse Azure toohost a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="ab6e9-110">tooenable ve bir Azure rol için Uzak Masaüstü'nü kullanma</span><span class="sxs-lookup"><span data-stu-id="ab6e9-110">tooenable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="ab6e9-111">Çözüm Gezgini'nde, bulut hizmeti projenizi başlangıç kısayol menüsünü açın ve ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-111">In Solution Explorer, open hello shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="ab6e9-112">Merhaba **Azure uygulamasını Yayımla** Sihirbazı görünür.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-112">hello **Publish Azure Application** wizard appears.</span></span>
   
    ![Komutu için bir bulut hizmeti projesini Yayımla](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="ab6e9-114">Merhaba altındaki **Microsoft Azure yayımlama ayarları** hello sihirbazının select hello **Uzak Masaüstü'nü etkinleştirme** tüm rolleri onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-114">At hello bottom of **Microsoft Azure Publish Settings** page of hello wizard, select hello **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="ab6e9-115">Merhaba **uzak masaüstü yapılandırması** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-115">hello **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="ab6e9-116">Merhaba hello sonundaki **uzak masaüstü yapılandırması** iletişim kutusunda, hello seçin **diğer seçenekler** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-116">At hello bottom of hello **Remote Desktop Configuration** dialog box, choose hello **More Options** button.</span></span> 
   
    <span data-ttu-id="ab6e9-117">Bu oluşturmak veya Uzak Masaüstü aracılığıyla bağlanırken kimlik bilgilerini şifrelemek için bir sertifika seçin imkan tanıyan bir açılır liste kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="ab6e9-118">Merhaba aşağı açılan listesinde seçin  **&lt;Oluştur >**, veya mevcut bir hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-118">In hello dropdown list, choose **&lt;Create>**, or choose an existing one from hello list.</span></span> 
   
    <span data-ttu-id="ab6e9-119">Varolan bir sertifikayı seçerseniz, aşağıdaki adımları hello atlayın.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-119">If you choose an existing certificate, skip hello following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ab6e9-120">bir Uzak Masaüstü bağlantısı için gereksinim duyduğunuz hello sertifikalar, diğer Azure işlemleri için kullandığınız hello sertifikaları farklıdır.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-120">hello certificates that you need for a remote desktop connection are different from hello certificates that you use for other Azure operations.</span></span> <span data-ttu-id="ab6e9-121">Merhaba uzaktan erişim sertifikasının özel anahtarı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-121">hello remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="ab6e9-122">Merhaba **oluşturduğunuz sertifika** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-122">hello **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="ab6e9-123">Merhaba yeni sertifika için kolay bir ad sağlayın ve ardından hello **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-123">Provide a friendly name for hello new certificate, and then choose hello **OK** button.</span></span> <span data-ttu-id="ab6e9-124">Merhaba yeni sertifika hello açılır liste kutusunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-124">hello new certificate appears in hello dropdown list box.</span></span>
   2. <span data-ttu-id="ab6e9-125">Merhaba, **uzak masaüstü yapılandırması** iletişim kutusunda, bir kullanıcı adı ve parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-125">In hello **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="ab6e9-126">Var olan bir hesap kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-126">You can’t use an existing account.</span></span> <span data-ttu-id="ab6e9-127">Yönetici hello hello yeni hesap için kullanıcı adı olarak belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-127">Don’t specify Administrator as hello user name for hello new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="ab6e9-128">Merhaba parola hello karmaşıklık gereksinimlerini karşılamıyorsa, kırmızı bir simge sonraki toohello parola metin kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-128">If hello password doesn’t meet hello complexity requirements, a red icon appears next toohello password text box.</span></span> <span data-ttu-id="ab6e9-129">Merhaba parola büyük harf, küçük harfler ve sayılar veya simgeler içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-129">hello password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="ab6e9-130">Hangi hello hesabın süresi dolacak ve hangi Uzak Masaüstü bağlantıları engellenir sonra bir tarihi seçin.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-130">Choose a date on which hello account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="ab6e9-131">Tüm gerekli bilgileri hello sağlanan seçtiğiniz sonra hello seçin **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-131">After you've provided all hello required information, choose hello **OK** button.</span></span>
      
       <span data-ttu-id="ab6e9-132">Uzaktan erişim hizmetleri sağlayan birkaç ayarları toohello .cscfg ve .csdef dosyaları eklenir.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-132">Several settings that enable Remote Access Services are added toohello .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="ab6e9-133">Merhaba, **Microsoft Azure yayımlama ayarları** Sihirbazı'nı hello seçin **Tamam** düğmesini gönderirken, bulut hizmetinizin toopublish hazır.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-133">In hello **Microsoft Azure Publish Settings** wizard, choose hello **OK** button when you’re ready toopublish your cloud service.</span></span>
   
    <span data-ttu-id="ab6e9-134">Hazır toopublish değilseniz hello seçin **iptal** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-134">If you're not ready toopublish, choose hello **Cancel** button.</span></span> <span data-ttu-id="ab6e9-135">Merhaba yapılandırma ayarları kaydedilir ve daha sonra bulut hizmetinizi yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-135">hello configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a><span data-ttu-id="ab6e9-136">Uzak Masaüstü'nü kullanarak tooan Azure rol Bağlan</span><span class="sxs-lookup"><span data-stu-id="ab6e9-136">Connect tooan Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="ab6e9-137">Bulut hizmetinizde Azure yayımladıktan sonra Azure barındıran hello sanal makinelerine Sunucu Gezgini toolog kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-137">After you publish your cloud service on Azure, you can use Server Explorer toolog into hello virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="ab6e9-138">Sunucu Gezgini'nde hello genişletin **Azure** düğümü, bir bulut hizmeti ve kendi rolleri toodisplay örneklerinin bir listesini biri için hello düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-138">In Server Explorer, expand hello **Azure** node, and then expand hello node for a cloud service and one of its roles toodisplay a list of instances.</span></span>
2. <span data-ttu-id="ab6e9-139">Bir örnek düğümü için hello kısayol menüsünü açın ve ardından **Uzak Masaüstü kullanarak bağlanmak**.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-139">Open hello shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Uzak Masaüstü aracılığıyla bağlanma](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="ab6e9-141">Merhaba kullanıcı adı ve daha önce oluşturduğunuz parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-141">Enter hello user name and password that you created previously.</span></span> <span data-ttu-id="ab6e9-142">Şimdi uzak oturumunuza günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="ab6e9-142">You are now logged into your remote session.</span></span>

