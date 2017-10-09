---
title: "Uzak Masaüstü bağlantısı için Azure bulut Hizmetleri rolünde aaaEnable | Microsoft Docs"
description: "Nasıl tooconfigure azure bulut hizmeti uygulama tooallow Uzak Masaüstü bağlantıları"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="a22ca-103">Azure bulut Hizmetleri rolünde için Uzak Masaüstü Bağlantısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a22ca-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a22ca-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="a22ca-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="a22ca-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="a22ca-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="a22ca-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a22ca-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="a22ca-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a22ca-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="a22ca-108">Uzak Masaüstü tooaccess hello Masaüstü Azure'da çalışan bir rolün sağlar.</span><span class="sxs-lookup"><span data-stu-id="a22ca-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="a22ca-109">Çalışırken uygulamanız ile sorunları tanılamak ve Uzak Masaüstü Bağlantısı tootroubleshoot kullanın.</span><span class="sxs-lookup"><span data-stu-id="a22ca-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="a22ca-110">Hizmet tanımında hello Uzak Masaüstü modüller ekleyerek geliştirme sırasında rolde bir Uzak Masaüstü Bağlantısı etkinleştirebilirsiniz veya tooenable Uzak Masaüstü hello Uzak Masaüstü uzantısı aracılığıyla seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a22ca-110">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="a22ca-111">Uygulamanızı tooredeploy gerek kalmadan Merhaba uygulaması bile dağıtıldıktan sonra Uzak Masaüstü etkinleştirebilirsiniz gibi hello tercih edilen yaklaşım toouse hello Uzak Masaüstü uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="a22ca-111">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-portal"></a><span data-ttu-id="a22ca-112">Azure portal hello Uzak Masaüstü'nü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a22ca-112">Configure Remote Desktop from hello Azure portal</span></span>
<span data-ttu-id="a22ca-113">hello Azure portal hello Uzak Masaüstü uzantısı yaklaşımı kullanır, bu nedenle bile hello uygulama dağıtıldıktan sonra Uzak Masaüstü etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a22ca-113">hello Azure portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="a22ca-114">Merhaba **Uzak Masaüstü** bulut hizmetinizin dikey tooenable Uzak Masaüstü sağlar, değişiklik hello yerel yönetici hesabı kullanılan tooconnect toohello sanal makineler, hello sertifika kimlik doğrulamasında kullanılan ve hello ayarlayın sona erme tarihi.</span><span class="sxs-lookup"><span data-stu-id="a22ca-114">hello **Remote Desktop** blade for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="a22ca-115">Tıklatın **bulut Hizmetleri**hello bulut hizmeti hello adına tıklayın ve ardından **Uzak Masaüstü**.</span><span class="sxs-lookup"><span data-stu-id="a22ca-115">Click **Cloud Services**, click hello name of hello cloud service, and then click **Remote Desktop**.</span></span>

    ![Bulut Hizmetleri Uzak Masaüstü](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="a22ca-117">Uzak Masaüstü tooenable tüm rolleri veya tek bir rol için istediğiniz sonra hello değiştirici hello değerini çok değiştirme olup olmadığını seçin**etkin**.</span><span class="sxs-lookup"><span data-stu-id="a22ca-117">Choose whether you want tooenable Remote Desktop for an individual role or for all roles, then change hello value of hello switcher too**Enabled**.</span></span>

3. <span data-ttu-id="a22ca-118">Kullanıcı adı, parola, süre sonu ve sertifika hello gerekli alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="a22ca-118">Fill in hello required fields for user name, password, expiry, and certificate.</span></span>

    ![Bulut Hizmetleri Uzak Masaüstü](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="a22ca-120">İlk olarak Uzak Masaüstü'nü etkinleştirin ve (onay işareti) Tamam'ı tıklatın, tüm rol örneklerini yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="a22ca-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="a22ca-121">tooprevent yeniden başlatma, hello sertifika kullanılan tooencrypt hello parolası hello rolünün yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a22ca-121">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="a22ca-122">tooprevent bir yeniden başlatma [hello bulut hizmeti için bir sertifika karşıya](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) ve toothis iletişim döndürür.</span><span class="sxs-lookup"><span data-stu-id="a22ca-122">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>
   >
   >
3. <span data-ttu-id="a22ca-123">İçinde **rolleri**seçin tooupdate istediğiniz ya da seçin hello rol **tüm** tüm rolleri için.</span><span class="sxs-lookup"><span data-stu-id="a22ca-123">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>

4. <span data-ttu-id="a22ca-124">Tamamladığınızda, yapılandırmayı güncelleştirmelerinizi tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="a22ca-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="a22ca-125">Rolü örneklerinizi hazır tooreceive bağlantıları önce birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="a22ca-125">It will take a few moments before your role instances are ready tooreceive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="a22ca-126">Uzaktan rol örnekleri içine</span><span class="sxs-lookup"><span data-stu-id="a22ca-126">Remote into role instances</span></span>
<span data-ttu-id="a22ca-127">Uzak Masaüstü hello rollerinde etkinleştirildikten sonra bir bağlantıdan doğrudan hello Azure Portal başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a22ca-127">Once Remote Desktop is enabled on hello roles, you can initiate a connection directly from hello Azure Portal:</span></span>

1. <span data-ttu-id="a22ca-128">Tıklatın **örnekleri** tooopen hello **örnekleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="a22ca-128">Click **Instances** tooopen hello **Instances** blade.</span></span>
2. <span data-ttu-id="a22ca-129">Yapılandırılmış Uzak Masaüstü sahip rol örneği seçin.</span><span class="sxs-lookup"><span data-stu-id="a22ca-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="a22ca-130">Tıklatın **Bağlan** toodownload bir RDP dosyası hello rol örneği için.</span><span class="sxs-lookup"><span data-stu-id="a22ca-130">Click **Connect** toodownload an RDP file for hello role instance.</span></span>

    ![Bulut Hizmetleri Uzak Masaüstü](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="a22ca-132">Tıklatın **açık** ve ardından **Bağlan** toostart hello Uzak Masaüstü Bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="a22ca-132">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="a22ca-133">Bulut hizmetiniz bir NSG durduğunu değilse, bağlantı noktalarında trafiğine izin veren toocreate kuralları gerekebilir **3389** ve **20000**.</span><span class="sxs-lookup"><span data-stu-id="a22ca-133">If your cloud service is sitting behind an NSG, you may need toocreate rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="a22ca-134">Uzak Masaüstü bağlantı noktasını kullanır **3389**.</span><span class="sxs-lookup"><span data-stu-id="a22ca-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="a22ca-135">Bulut hizmeti örnekleri yükü dengelenmiş, olduğundan, hangi örneğinin tooconnect doğrudan denetleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="a22ca-135">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="a22ca-136">Merhaba *RemoteForwarder* ve *RemoteAccess* aracıları RDP trafiği yönetmek ve hello istemci toosend bir RDP izin ver ve bir tek tek örnek tooconnect belirtin.</span><span class="sxs-lookup"><span data-stu-id="a22ca-136">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="a22ca-137">Merhaba *RemoteForwarder* ve *RemoteAccess* aracıları gerektiren bu bağlantı noktasını **20000*** açılıp, hangi engellenmiş olabilir bir NSG varsa.</span><span class="sxs-lookup"><span data-stu-id="a22ca-137">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a22ca-138">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a22ca-138">Additional resources</span></span>

<span data-ttu-id="a22ca-139">[Nasıl tooConfigure bulut Hizmetleri](cloud-services-how-to-configure.md)
[bulut SSS - Uzak Masaüstü Hizmetleri](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="a22ca-139">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
