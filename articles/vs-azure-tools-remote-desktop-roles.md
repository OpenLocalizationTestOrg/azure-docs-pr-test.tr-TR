---
title: "Uzak Masaüstü kullanarak Azure rolleriyle | Microsoft Docs"
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
ms.openlocfilehash: eab135d10c0d6df8ca72ac47d6804017a998a3d2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="ee414-103">Azure rolleri ile Uzak Masaüstü'nü kullanma</span><span class="sxs-lookup"><span data-stu-id="ee414-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="ee414-104">Uzak Masaüstü Hizmetleri ve Azure SDK kullanarak Azure rolleri ve Azure tarafından barındırılan sanal makinelerin erişebilir.</span><span class="sxs-lookup"><span data-stu-id="ee414-104">By using the Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="ee414-105">Visual Studio'da bir Azure bulut hizmeti projesi Uzak Masaüstü Hizmetleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee414-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="ee414-106">Uzak Masaüstü Hizmetleri etkinleştirmek için bir veya daha fazla rolü içeren bir çalışma projesi oluşturun ve Azure'a yayımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ee414-106">To enable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it to Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee414-107">Sorun giderme veya yalnızca geliştirme için Azure bir rolü erişim.</span><span class="sxs-lookup"><span data-stu-id="ee414-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="ee414-108">Her bir sanal makine amacı, diğer istemci uygulamaları çalıştırmayı Azure uygulamanızı, belirli bir rol çalıştırmaktır.</span><span class="sxs-lookup"><span data-stu-id="ee414-108">The purpose of each virtual machine is to run a specific role in your Azure application, not to run other client applications.</span></span> <span data-ttu-id="ee414-109">Herhangi bir amaçla kullanabileceğiniz bir sanal makineyi barındırmak için Azure kullanmak istiyorsanız, Azure sanal makineleri Sunucu Gezgini'nden erişme bakın.</span><span class="sxs-lookup"><span data-stu-id="ee414-109">If you want to use Azure to host a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="to-enable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="ee414-110">Etkinleştirmek ve bir Azure rol için Uzak Masaüstü'nü kullanmak için</span><span class="sxs-lookup"><span data-stu-id="ee414-110">To enable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="ee414-111">Çözüm Gezgini'nde, bulut hizmeti projenizi için kısayol menüsünü açın ve ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="ee414-111">In Solution Explorer, open the shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="ee414-112">**Azure uygulamasını Yayımla** Sihirbazı görünür.</span><span class="sxs-lookup"><span data-stu-id="ee414-112">The **Publish Azure Application** wizard appears.</span></span>
   
    ![Komutu için bir bulut hizmeti projesini Yayımla](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="ee414-114">Ekranın alt kısmındaki **Microsoft Azure yayımlama ayarları** seçin sayfasında **Uzak Masaüstü'nü etkinleştirme** tüm rolleri onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="ee414-114">At the bottom of **Microsoft Azure Publish Settings** page of the wizard, select the **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="ee414-115">**Uzak masaüstü yapılandırması** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ee414-115">The **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="ee414-116">Ekranın alt kısmındaki **uzak masaüstü yapılandırması** iletişim kutusunda, seçin **diğer seçenekler** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ee414-116">At the bottom of the **Remote Desktop Configuration** dialog box, choose the **More Options** button.</span></span> 
   
    <span data-ttu-id="ee414-117">Bu oluşturmak veya Uzak Masaüstü aracılığıyla bağlanırken kimlik bilgilerini şifrelemek için bir sertifika seçin imkan tanıyan bir açılır liste kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ee414-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="ee414-118">Aşağı açılan listesinde seçin  **&lt;Oluştur >**, veya mevcut bir listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="ee414-118">In the dropdown list, choose **&lt;Create>**, or choose an existing one from the list.</span></span> 
   
    <span data-ttu-id="ee414-119">Varolan bir sertifikayı seçerseniz, aşağıdaki adımları atlayın.</span><span class="sxs-lookup"><span data-stu-id="ee414-119">If you choose an existing certificate, skip the following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ee414-120">Bir Uzak Masaüstü bağlantısı için gereken sertifikalar, diğer Azure işlemleri için kullandığı sertifikalar farklıdır.</span><span class="sxs-lookup"><span data-stu-id="ee414-120">The certificates that you need for a remote desktop connection are different from the certificates that you use for other Azure operations.</span></span> <span data-ttu-id="ee414-121">Uzaktan erişim sertifikasının özel anahtarı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee414-121">The remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="ee414-122">**Oluşturduğunuz sertifika** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ee414-122">The **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="ee414-123">Yeni sertifika için kolay bir ad sağlayın ve ardından **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ee414-123">Provide a friendly name for the new certificate, and then choose the **OK** button.</span></span> <span data-ttu-id="ee414-124">Yeni sertifika açılır liste kutusunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ee414-124">The new certificate appears in the dropdown list box.</span></span>
   2. <span data-ttu-id="ee414-125">İçinde **uzak masaüstü yapılandırması** iletişim kutusunda, bir kullanıcı adı ve parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ee414-125">In the **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="ee414-126">Var olan bir hesap kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="ee414-126">You can’t use an existing account.</span></span> <span data-ttu-id="ee414-127">Yönetici yeni hesap için kullanıcı adı olarak belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="ee414-127">Don’t specify Administrator as the user name for the new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="ee414-128">Parola karmaşıklık gereksinimlerini karşılamıyorsa, kırmızı bir simge yanındaki parola metin kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="ee414-128">If the password doesn’t meet the complexity requirements, a red icon appears next to the password text box.</span></span> <span data-ttu-id="ee414-129">Parola büyük harf, küçük harfler ve sayılar veya simgeler içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ee414-129">The password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="ee414-130">Hesap sona erecek ve hangi Uzak Masaüstü bağlantıları engellenir sonra bir tarihi seçin.</span><span class="sxs-lookup"><span data-stu-id="ee414-130">Choose a date on which the account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="ee414-131">Gerekli tüm bilgileri sağladığınız sonra tercih **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ee414-131">After you've provided all the required information, choose the **OK** button.</span></span>
      
       <span data-ttu-id="ee414-132">Uzaktan erişim hizmetleri sağlayan birkaç ayarları .cscfg ve .csdef dosyasına eklenir.</span><span class="sxs-lookup"><span data-stu-id="ee414-132">Several settings that enable Remote Access Services are added to the .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="ee414-133">İçinde **Microsoft Azure yayımlama ayarları** Sihirbazı'nı seçin **Tamam** bulut hizmetiniz yayımlamaya hazır olduğunuzda düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ee414-133">In the **Microsoft Azure Publish Settings** wizard, choose the **OK** button when you’re ready to publish your cloud service.</span></span>
   
    <span data-ttu-id="ee414-134">Yayımlamaya hazır değilseniz seçin **iptal** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ee414-134">If you're not ready to publish, choose the **Cancel** button.</span></span> <span data-ttu-id="ee414-135">Yapılandırma ayarları kaydedilir ve daha sonra bulut hizmetinizi yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="ee414-135">The configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-to-an-azure-role-by-using-remote-desktop"></a><span data-ttu-id="ee414-136">Uzak Masaüstü'nü kullanarak bir Azure rolüne bağlayın</span><span class="sxs-lookup"><span data-stu-id="ee414-136">Connect to an Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="ee414-137">Bulut hizmetinizde Azure yayımladıktan sonra Azure barındıran sanal makinelerine oturum için Sunucu Gezgini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee414-137">After you publish your cloud service on Azure, you can use Server Explorer to log into the virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="ee414-138">Server Explorer'da genişletin **Azure** düğümünü ve bir bulut hizmeti ve örneklerinin bir listesini görüntülemek için kendi rollerinden birini düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="ee414-138">In Server Explorer, expand the **Azure** node, and then expand the node for a cloud service and one of its roles to display a list of instances.</span></span>
2. <span data-ttu-id="ee414-139">Bir örnek düğümü için kısayol menüsünü açın ve ardından **Uzak Masaüstü kullanarak bağlanmak**.</span><span class="sxs-lookup"><span data-stu-id="ee414-139">Open the shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Uzak Masaüstü aracılığıyla bağlanma](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="ee414-141">Kullanıcı adı ve daha önce oluşturduğunuz parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="ee414-141">Enter the user name and password that you created previously.</span></span> <span data-ttu-id="ee414-142">Şimdi uzak oturumunuza günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="ee414-142">You are now logged into your remote session.</span></span>

