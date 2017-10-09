---
title: aaaManaging rolleri Azure bulut Hizmetleri'ni Visual Studio ile | Microsoft Docs
description: "Nasıl tooadd ekleme ve kaldırma rolleri Azure bulut hizmetlerine Visual Studio ile bilgi edinin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="8ccc2-103">Azure bulut Hizmetleri'ni Visual Studio ile rollerini yönetme</span><span class="sxs-lookup"><span data-stu-id="8ccc2-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="8ccc2-104">Azure bulut hizmetinizi oluşturduktan sonra yeni rol tooit ekleyebilir veya var olan rollerini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-104">After you have created your Azure cloud service, you can add new roles tooit or remove existing roles from it.</span></span> <span data-ttu-id="8ccc2-105">Ayrıca, mevcut bir projeyi alın ve tooa rol dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-105">You can also import an existing project and convert it tooa role.</span></span> <span data-ttu-id="8ccc2-106">Örneğin, bir ASP.NET web uygulamasını almak ve bir web rolü olarak belirleyin.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-tooan-azure-cloud-service"></a><span data-ttu-id="8ccc2-107">Bir rol tooan Azure bulut hizmeti ekleme</span><span class="sxs-lookup"><span data-stu-id="8ccc2-107">Adding a role tooan Azure cloud service</span></span>
<span data-ttu-id="8ccc2-108">Aşağıdaki adımları hello Visual Studio'da bir web veya çalışan rolü tooan Azure bulut hizmeti projesini eklerken size kılavuzluk.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-108">hello following steps guide you through adding a web or worker role tooan Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="8ccc2-109">Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="8ccc2-110">İçinde **Çözüm Gezgini**, başlangıç projesi düğümünü genişletin</span><span class="sxs-lookup"><span data-stu-id="8ccc2-110">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="8ccc2-111">Sağ hello **rolleri** düğümü toodisplay hello bağlam menüsü.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-111">Right-click hello **Roles** node toodisplay hello context menu.</span></span> <span data-ttu-id="8ccc2-112">Merhaba bağlam menüsünden seçin **Ekle**, bir var olan web rolü veya çalışan rolü hello geçerli çözümden seçin veya bir web veya çalışan rolü projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-112">From hello context menu, select **Add**, then select an existing web role or worker role from hello current solution, or create a web or worker role project.</span></span> <span data-ttu-id="8ccc2-113">Ayrıca, bir ASP.NET web uygulaması projesini gibi uygun bir projeyi seçin ve rol projesi ile ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Menü seçeneklerini tooadd bir rol tooan Azure bulut hizmeti projesi](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="8ccc2-115">Bir Azure bulut hizmetinden bir rolünü kaldırma</span><span class="sxs-lookup"><span data-stu-id="8ccc2-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="8ccc2-116">Hello aşağıdaki adımlarda size bir Azure bulut hizmeti projesini Visual Studio'da web veya çalışan rolü kaldırma aracılığıyla yol.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-116">hello following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="8ccc2-117">Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="8ccc2-118">İçinde **Çözüm Gezgini**, başlangıç projesi düğümünü genişletin</span><span class="sxs-lookup"><span data-stu-id="8ccc2-118">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="8ccc2-119">Merhaba genişletin **rolleri** düğümü.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-119">Expand hello **Roles** node.</span></span>

1. <span data-ttu-id="8ccc2-120">Tooremove isterseniz ve, hello bağlam menüsünden seçin sağ hello düğümü **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-120">Right-click hello node you want tooremove, and, from hello context menu, select **Remove**.</span></span> 

    ![Menü seçeneklerini tooadd rol tooan Azure bulut hizmeti](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a><span data-ttu-id="8ccc2-122">Bir rol tooan Azure bulut hizmeti projesini yeniden ekleniyor</span><span class="sxs-lookup"><span data-stu-id="8ccc2-122">Readding a role tooan Azure cloud service project</span></span>
<span data-ttu-id="8ccc2-123">Bulut hizmeti projenizden rolü kaldırmak, ancak daha sonra geri tooadd hello rol karar toohello proje, yalnızca hello rol bildirim ve uç noktaları ve tanılama bilgileri gibi temel öznitelikler eklenir.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-123">If you remove a role from your cloud service project but later decide tooadd hello role back toohello project, only hello role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="8ccc2-124">Ek kaynaklar veya başvuruları toohello eklenen `ServiceDefinition.csdef` dosya ya da toohello `ServiceConfiguration.cscfg` dosya.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-124">No additional resources or references are added toohello `ServiceDefinition.csdef` file or toohello `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="8ccc2-125">Bu bilgiler tooadd istiyorsanız, toomanually gerekir bu dosyaları geri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-125">If you want tooadd this information, you need toomanually add it back into these files.</span></span>

<span data-ttu-id="8ccc2-126">Örneğin, bir web hizmeti rolü kaldırabilir ve daha sonra bu rolü geri tooadd çözümünüze karar.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-126">For example, you might remove a web service role and later you decide tooadd this role back into your solution.</span></span> <span data-ttu-id="8ccc2-127">Bunu yaparsanız, bir hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-127">If you do this, an error occurs.</span></span> <span data-ttu-id="8ccc2-128">tooprevent bu hatayı tooadd hello sahip `<LocalResources>` XML geri hello aşağıdaki hello gösterilen öğesinin `ServiceDefinition.csdef` dosya.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-128">tooprevent this error, you have tooadd hello `<LocalResources>` element shown in hello following XML back into hello `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="8ccc2-129">Kullanım hello hello hello name özniteliği bir parçası olarak geri hello projeye eklenen hello web hizmeti rolü adını  **<LocalStorage>**  öğesi.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-129">Use hello name of hello web service role that you added back into hello project as part of hello name attribute for hello **<LocalStorage>** element.</span></span> <span data-ttu-id="8ccc2-130">Bu örnekte, hello hello web hizmeti rolü adıdır **WCFServiceWebRole1**.</span><span class="sxs-lookup"><span data-stu-id="8ccc2-130">In this example, hello name of hello web service role is **WCFServiceWebRole1**.</span></span>

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a><span data-ttu-id="8ccc2-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ccc2-131">Next steps</span></span>
- [<span data-ttu-id="8ccc2-132">Visual Studio ile Merhaba rolleri bir Azure bulut hizmeti için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8ccc2-132">Configure hello Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
