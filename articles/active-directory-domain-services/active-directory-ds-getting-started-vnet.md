---
title: "Azure Active Directory Domain Services: Sanal ağ oluşturma veya seçme | Microsoft Docs"
description: "Azure Active Directory etki alanı hello Klasik Azure portalı kullanarak Hizmetleri etkinleştir"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="52aad-103">Azure Active Directory Domain Services için sanal ağ oluşturma veya seçme</span><span class="sxs-lookup"><span data-stu-id="52aad-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="52aad-104">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="52aad-104">Before you begin</span></span>
<span data-ttu-id="52aad-105">Çok başvuran[Azure Active Directory etki alanı Hizmetleri için ağ konuları](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="52aad-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="52aad-106">Görev 2: Azure sanal ağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="52aad-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="52aad-107">Merhaba sonraki yapılandırma görevi Azure sanal ağı ve bir alt ağ içindeki toocreate değil.</span><span class="sxs-lookup"><span data-stu-id="52aad-107">hello next configuration task is toocreate an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="52aad-108">Sanal ağınızdaki bu alt ağda Azure Active Directory Domain Services’ı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="52aad-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="52aad-109">Toouse tercih var olan bir sanal ağınız varsa, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52aad-109">If you have an existing virtual network that you’d prefer toouse, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="52aad-110">Bu hello oluşturun veya Azure Active Directory etki alanı Hizmetleri ile toouse tooan Azure Active Directory etki alanı Hizmetleri tarafından desteklenen Azure bölgesine ait seçin Azure sanal ağı emin olun.</span><span class="sxs-lookup"><span data-stu-id="52aad-110">Make sure that hello Azure virtual network you create or choose toouse with Azure Active Directory Domain Services belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="52aad-111">tooascertain Azure Active Directory etki alanı Hizmetleri olduğu kullanılabilir Azure bölgeleri Merhaba, bkz: [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="52aad-111">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="52aad-112">Bir sonraki yapılandırma adımında Azure Active Directory etki alanı Hizmetleri'ni etkinleştirdiğinizde hello doğru sanal ağı seçin hello sanal ağ tooensure Hello adını not edin.</span><span class="sxs-lookup"><span data-stu-id="52aad-112">Note hello name of hello virtual network tooensure that you select hello right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="52aad-113">toocreate tooenable Azure Active Directory etki alanı Hizmetleri, istediğiniz bir Azure sanal ağı bu yapılandırma yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="52aad-113">toocreate an Azure virtual network in which you want tooenable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="52aad-114">Toohello Git [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="52aad-114">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="52aad-115">Merhaba sol bölmesinde seçin **ağlar**.</span><span class="sxs-lookup"><span data-stu-id="52aad-115">In hello left pane, select **Networks**.</span></span>

    <span data-ttu-id="52aad-116">![Ağlar düğümü](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="52aad-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="52aad-117">Merhaba **sanal ağlar** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="52aad-117">hello **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="52aad-118">Merhaba görev hello pencerenin hello altındaki bölmesinde **yeni**.</span><span class="sxs-lookup"><span data-stu-id="52aad-118">In hello task pane at hello bottom of hello window, click **New**.</span></span>

    ![Sanal ağlar penceresi](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="52aad-120">**Ağ Hizmetleri** düğümüne tıklayıp **Sanal Ağ** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="52aad-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Sanal ağ - hızlı oluştur](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="52aad-122">bir sanal ağ toocreate tıklatın **hızlı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="52aad-122">toocreate a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="52aad-123">Belirtin bir **adı** , sanal ağ ve hello aşağıdakileri yaparak göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="52aad-123">Specify a **Name** for your virtual network, and consider doing hello following:</span></span>
    * <span data-ttu-id="52aad-124">Tooconfigure seçebilirsiniz **adres alanı** veya **maksimum VM sayısını** bu ağ için.</span><span class="sxs-lookup"><span data-stu-id="52aad-124">You can choose tooconfigure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="52aad-125">Merhaba bırakabilirsiniz **DNS sunucusu** olarak ayarlama **hiçbiri** şimdilik.</span><span class="sxs-lookup"><span data-stu-id="52aad-125">You can leave hello **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="52aad-126">Azure Active Directory etki alanı Hizmetleri'ni etkinleştirdikten sonra hello ayarı güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52aad-126">You can update hello setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="52aad-127">Merhaba, **konumu** aşağı açılan listesinde, desteklenen bir Azure bölgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="52aad-127">In hello **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="52aad-128">tooascertain Azure Active Directory etki alanı Hizmetleri olduğu kullanılabilir Azure bölgeleri Merhaba, bkz: [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="52aad-128">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="52aad-129">toocreate sanal ağınızı tıklatın **bir sanal ağ oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="52aad-129">toocreate your virtual network, click **Create a Virtual Network**.</span></span>

    ![Azure Active Directory Domain Services için sanal ağ oluşturma](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="52aad-131">Bir sanal ağ oluşturduktan sonra hello hello sanal ağın adını seçin ve hello ardından **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="52aad-131">After you've created a virtual network, select hello name of hello virtual network, and then click hello **Configure** tab.</span></span>

    ![Alt ağ oluşturma](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="52aad-133">Altında **sanal ağ adres alanları**, tıklatın **alt ağ Ekle**ve ardından hello ada sahip bir alt ağ belirtip **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="52aad-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with hello name **AaddsSubnet**.</span></span>

    ![Azure Active Directory Domain Services için alt ağ oluşturma](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="52aad-135">toocreate alt Merhaba, tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="52aad-135">toocreate hello subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="52aad-136">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="52aad-136">Next step</span></span>
[<span data-ttu-id="52aad-137">Görev 3: Azure Active Directory Domain Services'i etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="52aad-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
