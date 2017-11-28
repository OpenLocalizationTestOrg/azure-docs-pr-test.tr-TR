---
title: "Azure bulut Hizmetleri rolünde için Uzak Masaüstü Bağlantısı etkinleştirme | Microsoft Docs"
description: "Azure bulut hizmeti uygulamanız Uzak Masaüstü bağlantılarına izin verecek şekilde yapılandırma"
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
ms.openlocfilehash: 0ff7fde5f3753aa6a24fb0af54d68d0dc0bd96a4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="68e9b-103">Azure bulut Hizmetleri rolünde için Uzak Masaüstü Bağlantısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="68e9b-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68e9b-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="68e9b-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="68e9b-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="68e9b-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="68e9b-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68e9b-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="68e9b-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="68e9b-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="68e9b-108">Uzak Masaüstü, Azure'da çalışan rolü Masaüstü erişmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="68e9b-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="68e9b-109">Uzak Masaüstü Bağlantısı çalışırken, uygulamanızın sorunları tanılamak ve gidermek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68e9b-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="68e9b-110">Uzak Masaüstü Uzak Masaüstü uzantısı aracılığıyla etkinleştirmeyi seçebilirsiniz veya hizmet tanımında Uzak Masaüstü modüller ekleyerek geliştirme sırasında rolünüze Uzak Masaüstü Bağlantısı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68e9b-110">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="68e9b-111">Tercih edilen yaklaşım uygulamanızı yeniden dağıtmak zorunda kalmadan uygulama bile dağıtıldıktan sonra Uzak Masaüstü'nü etkinleştirme gibi Uzak Masaüstü uzantısı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="68e9b-111">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-portal"></a><span data-ttu-id="68e9b-112">Uzak Masaüstü Azure portalından yapılandırın</span><span class="sxs-lookup"><span data-stu-id="68e9b-112">Configure Remote Desktop from the Azure portal</span></span>
<span data-ttu-id="68e9b-113">Azure portalı Uzak Masaüstü uzantısı yaklaşımı kullanır, bu nedenle bile uygulama dağıtıldıktan sonra Uzak Masaüstü etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68e9b-113">The Azure portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="68e9b-114">**Uzak Masaüstü** dikey bulut hizmetiniz için Uzak Masaüstü'nü etkinleştirmek için sanal makinelere bağlanmak için kullanılan yerel yönetici hesabını değiştirirseniz olanak tanır, sertifika kimlik doğrulamasında kullanılan ve sona erme tarihini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="68e9b-114">The **Remote Desktop** blade for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="68e9b-115">Tıklatın **bulut Hizmetleri**, bulut hizmeti adına tıklayın ve ardından **Uzak Masaüstü**.</span><span class="sxs-lookup"><span data-stu-id="68e9b-115">Click **Cloud Services**, click the name of the cloud service, and then click **Remote Desktop**.</span></span>

    ![Bulut Hizmetleri Uzak Masaüstü](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="68e9b-117">Tek bir rol için veya tüm roller için Uzak Masaüstü'nü etkinleştirin, ardından değiştirici değerini değiştirmek isteyip istemediğinizi **etkin**.</span><span class="sxs-lookup"><span data-stu-id="68e9b-117">Choose whether you want to enable Remote Desktop for an individual role or for all roles, then change the value of the switcher to **Enabled**.</span></span>

3. <span data-ttu-id="68e9b-118">Kullanıcı adı, parola, süre sonu ve sertifika için gerekli alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="68e9b-118">Fill in the required fields for user name, password, expiry, and certificate.</span></span>

    ![Bulut Hizmetleri Uzak Masaüstü](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="68e9b-120">İlk olarak Uzak Masaüstü'nü etkinleştirin ve (onay işareti) Tamam'ı tıklatın, tüm rol örneklerini yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="68e9b-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="68e9b-121">Yeniden başlatma önlemek için parolayı şifrelemek için kullanılan sertifikanın rolünün yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-121">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="68e9b-122">Bir yeniden başlatmayı engellemek için [bulut hizmeti için bir sertifika karşıya](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) ve bu iletişim kutusuna dönün.</span><span class="sxs-lookup"><span data-stu-id="68e9b-122">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>
   >
   >
3. <span data-ttu-id="68e9b-123">İçinde **rolleri**, güncelleştirme veya seçmek istediğiniz rolü seçin **tüm** tüm rolleri için.</span><span class="sxs-lookup"><span data-stu-id="68e9b-123">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>

4. <span data-ttu-id="68e9b-124">Tamamladığınızda, yapılandırmayı güncelleştirmelerinizi tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="68e9b-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="68e9b-125">Rolü örneklerinizi bağlantıları almaya hazır önce birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-125">It will take a few moments before your role instances are ready to receive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="68e9b-126">Uzaktan rol örnekleri içine</span><span class="sxs-lookup"><span data-stu-id="68e9b-126">Remote into role instances</span></span>
<span data-ttu-id="68e9b-127">Uzak Masaüstü roller üzerinde etkinleştirildikten sonra Azure Portalı'ndan doğrudan bir bağlantı başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="68e9b-127">Once Remote Desktop is enabled on the roles, you can initiate a connection directly from the Azure Portal:</span></span>

1. <span data-ttu-id="68e9b-128">Tıklatın **örnekleri** açmak için **örnekleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="68e9b-128">Click **Instances** to open the **Instances** blade.</span></span>
2. <span data-ttu-id="68e9b-129">Yapılandırılmış Uzak Masaüstü sahip rol örneği seçin.</span><span class="sxs-lookup"><span data-stu-id="68e9b-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="68e9b-130">Tıklatın **Bağlan** rol örneği için bir RDP dosyası indirilemedi.</span><span class="sxs-lookup"><span data-stu-id="68e9b-130">Click **Connect** to download an RDP file for the role instance.</span></span>

    ![Bulut Hizmetleri Uzak Masaüstü](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="68e9b-132">Tıklatın **açık** ve ardından **Bağlan** Uzak Masaüstü bağlantısı başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="68e9b-132">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="68e9b-133">Bulut hizmetiniz bir NSG durduğunu değilse, bağlantı noktalarında trafiğine izin veren kuralları oluşturmanız gerekebilir **3389** ve **20000**.</span><span class="sxs-lookup"><span data-stu-id="68e9b-133">If your cloud service is sitting behind an NSG, you may need to create rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="68e9b-134">Uzak Masaüstü bağlantı noktasını kullanır **3389**.</span><span class="sxs-lookup"><span data-stu-id="68e9b-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="68e9b-135">Bulut hizmeti örnekleri yükü dengelenmiş, olduğundan, doğrudan bağlanmak için hangi örneğinin denetleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="68e9b-135">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="68e9b-136">*RemoteForwarder* ve *RemoteAccess* aracıları RDP trafiği yönetmek ve istemcisinin bir RDP tanımlama bilgisi göndermek ve bağlanmak için tek bir örnek belirtin.</span><span class="sxs-lookup"><span data-stu-id="68e9b-136">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="68e9b-137">*RemoteForwarder* ve *RemoteAccess* aracıları gerektiren bu bağlantı noktasını **20000*** açılıp, hangi engellenmiş olabilir bir NSG varsa.</span><span class="sxs-lookup"><span data-stu-id="68e9b-137">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="68e9b-138">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="68e9b-138">Additional resources</span></span>

<span data-ttu-id="68e9b-139">[Bulut hizmetleri yapılandırmak için nasıl](cloud-services-how-to-configure.md)
[bulut SSS - Uzak Masaüstü Hizmetleri](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="68e9b-139">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
