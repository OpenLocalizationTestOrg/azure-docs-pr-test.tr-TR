---
title: "Azure Active Directory etki alanı Hizmetleri: Başlarken | Microsoft Docs"
description: "Azure Active Directory etki alanı hello Azure portal (Önizleme) kullanarak Hizmetleri etkinleştir"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="0f600-103">Azure Active Directory etki alanı hello Azure portal (Önizleme) kullanarak Hizmetleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="0f600-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="0f600-104">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="0f600-104">Before you begin</span></span>
<span data-ttu-id="0f600-105">Çok başvuran[Azure Active Directory etki alanı Hizmetleri için ağ konuları](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="0f600-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="0f600-106">Görev 2: ağ ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0f600-106">Task 2: configure network settings</span></span>
<span data-ttu-id="0f600-107">Merhaba sonraki yapılandırma görevi bir Azure sanal ağı ve ayrılmış bir alt ağ içindeki toocreate değil.</span><span class="sxs-lookup"><span data-stu-id="0f600-107">hello next configuration task is toocreate an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="0f600-108">Sanal ağınızdaki bu alt ağda Azure Active Directory Domain Services’ı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0f600-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="0f600-109">Ayrıca varolan bir sanal ağı seçin ve ayrılmış hello alt ağ içindeki oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="0f600-109">You may also pick an existing virtual network and create hello dedicated subnet within it.</span></span>

1. <span data-ttu-id="0f600-110">Tıklatın **sanal ağ** tooselect bir sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="0f600-110">Click **Virtual network** tooselect a virtual network.</span></span>
2. <span data-ttu-id="0f600-111">Merhaba üzerinde **Seç sanal ağ** dikey penceresinde, var olan tüm sanal ağları bakın.</span><span class="sxs-lookup"><span data-stu-id="0f600-111">On hello **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="0f600-112">Merhaba üzerinde seçtiğiniz toohello kaynak grubu ve Azure konumuna ait yalnızca hello sanal ağlar bkz **Temelleri** sihirbaz sayfası.</span><span class="sxs-lookup"><span data-stu-id="0f600-112">You see only hello virtual networks that belong toohello resource group and Azure location you have selected on hello **Basics** wizard page.</span></span>

3. <span data-ttu-id="0f600-113">Azure AD etki alanı Hizmetleri etkinleştirilmelidir hello sanal ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="0f600-113">Choose hello virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="0f600-114">Tıklatın **Yeni Oluştur**, toocreate yeni bir sanal ağ tercih ederseniz.</span><span class="sxs-lookup"><span data-stu-id="0f600-114">Click **Create new**, if you prefer toocreate a new virtual network.</span></span> <span data-ttu-id="0f600-115">Ayrılmış bir alt ağ için Azure AD Etki Alanı Hizmetleri'ni kullanarak öneririz.</span><span class="sxs-lookup"><span data-stu-id="0f600-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="0f600-116">Mevcut bir sanal ağı seçerseniz [hello sanal ağlar uzantısını kullanarak ayrılmış bir alt ağ oluşturmak](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) ve bu alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="0f600-116">If you pick an existing virtual network, [create a dedicated subnet using hello virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Sanal ağ seçin](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="0f600-118">Tıklatın **alt** toopick hello içinde hangi tooenable yeni yönetilen etki alanı bu sanal ağ içinde ayrılmış bir alt ağ.</span><span class="sxs-lookup"><span data-stu-id="0f600-118">Click **Subnet** toopick hello dedicated subnet in this virtual network, within which tooenable your new managed domain.</span></span> <span data-ttu-id="0f600-119">Merhaba, **alt ağ oluşturmak** dikey penceresinde hello alt ağ için bir ad belirtin ve tıklatın **Tamam** tamamladığınızda.</span><span class="sxs-lookup"><span data-stu-id="0f600-119">In hello **Create subnet** blade, specify a name for hello subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="0f600-120">Örneğin, 'DomainServices' diğer yöneticiler toounderstand hello alt ağda dağıtılan kolaylaştırır, hello adında bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0f600-120">For example, create a subnet with hello name 'DomainServices', making it easy for other administrators toounderstand what is deployed within hello subnet.</span></span>

    ![Merhaba sanal ağ içindeki alt ağ seçin](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="0f600-122">**Bir alt seçme yönergeleri**</span><span class="sxs-lookup"><span data-stu-id="0f600-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="0f600-123">Ayrılmış bir alt ağ için Azure AD Etki Alanı Hizmetleri'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f600-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="0f600-124">Diğer bir sanal makine toothis alt dağıtmayın.</span><span class="sxs-lookup"><span data-stu-id="0f600-124">Do not deploy any other virtual machines toothis subnet.</span></span> <span data-ttu-id="0f600-125">Bu yapılandırma, yönetilen etki alanınız kesintiye uğratmadan iş yükleri/sanal makineleriniz için tooconfigure ağ güvenlik grupları (Nsg'ler) etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="0f600-125">This configuration enables you tooconfigure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="0f600-126">Ayrıntılar için bkz [konuları Azure Active Directory etki alanı Hizmetleri için ağ](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="0f600-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="0f600-127">Desteklenen bir yapılandırma olduğundan Azure AD etki alanı Hizmetleri dağıtmak için ağ geçidi alt ağı hello seçmeyin.</span><span class="sxs-lookup"><span data-stu-id="0f600-127">Do not select hello Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="0f600-128">Seçtiğiniz hello alt yeterli kullanılabilir adres alanı - en az 3-5 kullanılabilir IP adresleri olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0f600-128">Ensure that hello subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="0f600-129">İşiniz bittiğinde tıklatın **Tamam** toohello üzerinde toomove **yönetici grubuna** hello Sihirbazı sayfası.</span><span class="sxs-lookup"><span data-stu-id="0f600-129">When you are done, click **OK** toomove on toohello **Administrator group** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="0f600-130">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="0f600-130">Next step</span></span>
[<span data-ttu-id="0f600-131">Görev 3: yönetim grubunu yapılandırın ve Azure AD Etki Alanı Hizmetleri'ni etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0f600-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
