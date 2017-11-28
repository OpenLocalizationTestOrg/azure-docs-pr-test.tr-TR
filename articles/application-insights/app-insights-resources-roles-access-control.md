---
title: "Azure Application Insights aaaResources, rolleri ve erişim denetimi | Microsoft Docs"
description: "Sahipleri, Katkıda Bulunanlar ve okuyucular, kuruluşunuzun Öngörüler."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="d7b95-103">Kaynaklar, rolleri ve erişim denetimi Application Insights</span><span class="sxs-lookup"><span data-stu-id="d7b95-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="d7b95-104">Kim okuma ve güncelleştirme erişim tooyour verilerini azure'da denetleyebilirsiniz [Application Insights][start], kullanarak [Microsoft Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d7b95-104">You can control who has read and update access tooyour data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7b95-105">Merhaba, erişim toousers atamak **kaynak grubuna veya aboneliğe** uygulama kaynağınızı ait - değil hello kaynağında kendisini toowhich.</span><span class="sxs-lookup"><span data-stu-id="d7b95-105">Assign access toousers in hello **resource group or subscription** toowhich your application resource belongs - not in hello resource itself.</span></span> <span data-ttu-id="d7b95-106">Merhaba atamak **Application Insights bileşen katkıda bulunan** rol.</span><span class="sxs-lookup"><span data-stu-id="d7b95-106">Assign hello **Application Insights component contributor** role.</span></span> <span data-ttu-id="d7b95-107">Bu erişim tooweb testleri ve uygulama kaynağınızı birlikte uyarıları Tekdüzen denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7b95-107">This ensures uniform control of access tooweb tests and alerts along with your application resource.</span></span> <span data-ttu-id="d7b95-108">[Daha fazla bilgi edinin](#access).</span><span class="sxs-lookup"><span data-stu-id="d7b95-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="d7b95-109">Kaynaklar, gruplar ve abonelikleri</span><span class="sxs-lookup"><span data-stu-id="d7b95-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="d7b95-110">İlk olarak, bazı tanımları:</span><span class="sxs-lookup"><span data-stu-id="d7b95-110">First, some definitions:</span></span>

* <span data-ttu-id="d7b95-111">**Kaynak** - Microsoft Azure hizmet örneğini bir.</span><span class="sxs-lookup"><span data-stu-id="d7b95-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="d7b95-112">Application Insights kaynağınıza toplar, çözümler ve uygulamanızdan gönderilen hello telemetri verilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d7b95-112">Your Application Insights resource collects, analyzes and displays hello telemetry data sent from your application.</span></span>  <span data-ttu-id="d7b95-113">Web uygulamaları, veritabanları ve VM'ler Azure kaynaklarını diğer türleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d7b95-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="d7b95-114">Kaynaklarınızın toosee açmak hello [Azure Portal][portal], oturum açın ve tüm kaynaklar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d7b95-114">toosee your resources, open hello [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="d7b95-115">toofind bir kaynak türü adını hello filtre alanına parçası.</span><span class="sxs-lookup"><span data-stu-id="d7b95-115">toofind a resource, type part of its name in hello filter field.</span></span>
  
    ![Azure kaynak listesi](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="d7b95-117">[**Kaynak grubu** ] [ group] -tooone grubun her kaynağa ait.</span><span class="sxs-lookup"><span data-stu-id="d7b95-117">[**Resource group**][group] - Every resource belongs tooone group.</span></span> <span data-ttu-id="d7b95-118">Bir grup kullanışlı olduğu şekilde toomanage ilgili erişim denetimi için özellikle kaynakları.</span><span class="sxs-lookup"><span data-stu-id="d7b95-118">A group is a convenient way toomanage related resources, particularly for access control.</span></span> <span data-ttu-id="d7b95-119">Örneğin, tek bir kaynak grubu bir Web uygulaması, bir Application Insights kaynağı toomonitor hello uygulama ve depolama kaynak tookeep koyabilirsiniz verileri dışarı.</span><span class="sxs-lookup"><span data-stu-id="d7b95-119">For example, into one resource group you could put a Web App, an Application Insights resource toomonitor hello app, and a Storage resource tookeep exported data.</span></span>

    ![Gözat, kaynak grupları belirtin, sonra bir grup seçin](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="d7b95-121">[**Abonelik** ](https://manage.windowsazure.com) -toouse Application Insights veya diğer Azure kaynaklarına, oturum tooan Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="d7b95-121">[**Subscription**](https://manage.windowsazure.com) - toouse Application Insights or other Azure resources, you sign in tooan Azure subscription.</span></span> <span data-ttu-id="d7b95-122">Her kaynak grubu tooone fiyat paketinizi seçin ve burada, bir kuruluşun abonelik ise hello üyeleri ve bunların erişim izinlerini seçmeniz Azure aboneliği aittir.</span><span class="sxs-lookup"><span data-stu-id="d7b95-122">Every resource group belongs tooone Azure subscription, where you choose your price package and, if it's an organization subscription, choose hello members and their access permissions.</span></span>
* <span data-ttu-id="d7b95-123">[**Microsoft hesabı** ] [ account] -hello kullanıcı adı ve parola tooMicrosoft Azure toosign kullanmak abonelikler, XBox Live, Outlook.com ve diğer Microsoft Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="d7b95-123">[**Microsoft account**][account] - hello username and password that you use toosign in tooMicrosoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="d7b95-124"><a name="access"></a>Merhaba kaynak grubunda erişimi denetleme</span><span class="sxs-lookup"><span data-stu-id="d7b95-124"><a name="access"></a> Control access in hello resource group</span></span>
<span data-ttu-id="d7b95-125">Toplama toohello kaynak uygulamanız için oluşturduğunuz olduğunu da uyarıları ve web testleri için gizli kaynaklar ayrı önemli toounderstand olur.</span><span class="sxs-lookup"><span data-stu-id="d7b95-125">It's important toounderstand that in addition toohello resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="d7b95-126">Ekli toohello oldukları aynı [kaynak grubu](#resource-group) uygulamanız.</span><span class="sxs-lookup"><span data-stu-id="d7b95-126">They are attached toohello same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="d7b95-127">Ayrıca diğer Azure hizmetleriyle gibi Web sitesi ya da depolama burada konumuna.</span><span class="sxs-lookup"><span data-stu-id="d7b95-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Application Insights kaynakları](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="d7b95-129">toocontrol erişim toothese kaynaklar için önerilir:</span><span class="sxs-lookup"><span data-stu-id="d7b95-129">toocontrol access toothese resources it's therefore recommended to:</span></span>

* <span data-ttu-id="d7b95-130">Denetim hello erişim **kaynak grubuna veya aboneliğe** düzeyi.</span><span class="sxs-lookup"><span data-stu-id="d7b95-130">Control access at hello **resource group or subscription** level.</span></span>
* <span data-ttu-id="d7b95-131">Merhaba atamak **uygulama Öngörüler bileşeni katkıda bulunan** rol toousers.</span><span class="sxs-lookup"><span data-stu-id="d7b95-131">Assign hello **Application Insights Component contributor** role toousers.</span></span> <span data-ttu-id="d7b95-132">Bu tooedit web testleri, uyarılar ve Application Insights kaynaklara erişim tooany hello grubundaki diğer hizmetler sağlamadan sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7b95-132">This allows them tooedit web tests, alerts, and Application Insights resources, without providing access tooany other services in hello group.</span></span>

## <a name="tooprovide-access-tooanother-user"></a><span data-ttu-id="d7b95-133">tooprovide tooanother kullanıcıya erişim</span><span class="sxs-lookup"><span data-stu-id="d7b95-133">tooprovide access tooanother user</span></span>
<span data-ttu-id="d7b95-134">Sahibi hakları toohello abonelik veya hello kaynak grubu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7b95-134">You must have Owner rights toohello subscription or hello resource group.</span></span>

<span data-ttu-id="d7b95-135">Merhaba kullanıcı olmalıdır bir [Microsoft Account][account], veya tootheir erişim [kuruluş Microsoft Account](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="d7b95-135">hello user must have a [Microsoft Account][account], or access tootheir [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="d7b95-136">Erişim tooindividuals ve toouser grupları Azure Active Directory'de tanımlı sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="d7b95-136">You can provide access tooindividuals, and also toouser groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-toohello-resource-group"></a><span data-ttu-id="d7b95-137">Toohello kaynak grubuna gidin</span><span class="sxs-lookup"><span data-stu-id="d7b95-137">Navigate toohello resource group</span></span>
<span data-ttu-id="d7b95-138">Merhaba kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d7b95-138">Add hello user there.</span></span>

![Uygulamanızın kaynak dikey penceresinde, Essentials'ı açın, hello kaynak grubu açın ve var. ayarları/kullanıcılar'ı seçin.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="d7b95-141">Veya başka düzeyi gidin ve hello kullanıcı toohello abonelik ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d7b95-141">Or you could go up another level and add hello user toohello Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="d7b95-142">Rol seçin</span><span class="sxs-lookup"><span data-stu-id="d7b95-142">Select a role</span></span>
![Merhaba yeni kullanıcı için bir rol seçin](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="d7b95-144">Rol</span><span class="sxs-lookup"><span data-stu-id="d7b95-144">Role</span></span> | <span data-ttu-id="d7b95-145">Merhaba kaynak grubunda</span><span class="sxs-lookup"><span data-stu-id="d7b95-145">In hello resource group</span></span> |
| --- | --- |
| <span data-ttu-id="d7b95-146">Sahip</span><span class="sxs-lookup"><span data-stu-id="d7b95-146">Owner</span></span> |<span data-ttu-id="d7b95-147">Kullanıcı erişim dahil her şeyi değiştirebilir</span><span class="sxs-lookup"><span data-stu-id="d7b95-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="d7b95-148">Katılımcı</span><span class="sxs-lookup"><span data-stu-id="d7b95-148">Contributor</span></span> |<span data-ttu-id="d7b95-149">Tüm kaynaklar da dahil olmak üzere her şeyi düzenleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d7b95-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="d7b95-150">Uygulama Öngörüler bileşen katkıda bulunan</span><span class="sxs-lookup"><span data-stu-id="d7b95-150">Application Insights Component contributor</span></span> |<span data-ttu-id="d7b95-151">Application Insights kaynaklara, web testleri ve Uyarıları düzenleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d7b95-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="d7b95-152">Okuyucu</span><span class="sxs-lookup"><span data-stu-id="d7b95-152">Reader</span></span> |<span data-ttu-id="d7b95-153">Görüntüleyebilir, ancak değişikliği değil</span><span class="sxs-lookup"><span data-stu-id="d7b95-153">Can view but not change anything</span></span> |

<span data-ttu-id="d7b95-154">'Düzenleme' oluşturma, silme ve güncelleştirme içerir:</span><span class="sxs-lookup"><span data-stu-id="d7b95-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="d7b95-155">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d7b95-155">Resources</span></span>
* <span data-ttu-id="d7b95-156">Web testleri</span><span class="sxs-lookup"><span data-stu-id="d7b95-156">Web tests</span></span>
* <span data-ttu-id="d7b95-157">Uyarılar</span><span class="sxs-lookup"><span data-stu-id="d7b95-157">Alerts</span></span>
* <span data-ttu-id="d7b95-158">Sürekli dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="d7b95-158">Continuous export</span></span>

#### <a name="select-hello-user"></a><span data-ttu-id="d7b95-159">Merhaba kullanıcıyı seçin</span><span class="sxs-lookup"><span data-stu-id="d7b95-159">Select hello user</span></span>

<span data-ttu-id="d7b95-160">İstediğiniz hello kullanıcı hello dizininde değilse, bir Microsoft hesabı olan herkes davet edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7b95-160">If hello user you want isn't in hello directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="d7b95-161">(Bunlar Outlook.com, OneDrive, Windows Phone veya XBox LIVE gibi hizmetleri kullanıyorsanız, bunlar bir Microsoft hesabınız vardır.)</span><span class="sxs-lookup"><span data-stu-id="d7b95-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="d7b95-162">İlgili içerik</span><span class="sxs-lookup"><span data-stu-id="d7b95-162">Related content</span></span>

* [<span data-ttu-id="d7b95-163">Rol tabanlı erişim denetimi Azure</span><span class="sxs-lookup"><span data-stu-id="d7b95-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
