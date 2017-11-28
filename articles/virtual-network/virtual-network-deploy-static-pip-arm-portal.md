---
title: "Bir statik genel IP adresi ile - Azure portalında bir VM oluşturma | Microsoft Docs"
description: "Azure Portalı'nı kullanarak bir statik genel IP adresi ile VM oluşturmayı öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 233e4eea8439320c1c7446e2c2b2e9d379351a3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-portal"></a><span data-ttu-id="bc405-103">Azure Portalı'nı kullanarak bir statik genel IP adresiyle bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc405-103">Create a VM with a static public IP address using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc405-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="bc405-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="bc405-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc405-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="bc405-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bc405-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="bc405-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="bc405-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="bc405-108">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="bc405-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="bc405-109">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bc405-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bc405-110">Bu makalede, Klasik dağıtım modeli yerine en yeni dağıtımlar için Microsoft önerir Resource Manager dağıtım modelini kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="bc405-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="bc405-111">Bir statik genel IP ile bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc405-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="bc405-112">Azure portalında bir statik genel IP adresine sahip bir VM oluşturmak için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="bc405-112">To create a VM with a static public IP address in the Azure portal, complete the following steps:</span></span>

1. <span data-ttu-id="bc405-113">Tarayıcıdan [Azure portalına](https://portal.azure.com) gidin ve gerekiyorsa Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="bc405-113">From a browser, navigate to the [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="bc405-114">Portalı'nı üst sol alt köşesindeki tıklatın **yeni**>>**işlem**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="bc405-114">On the top left hand corner of the portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="bc405-115">İçinde **dağıtım modeli seçin** listesinde, seçin **Resource Manager** tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="bc405-115">In the **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="bc405-116">İçinde **Temelleri** dikey penceresinde, aşağıda gösterildiği gibi VM bilgileri girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bc405-116">In the **Basics** blade, enter the VM information as shown below, and then click **OK**.</span></span>
   
    ![Azure portal - temelleri](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="bc405-118">İçinde **bir boyutu seçin** dikey penceresinde tıklatın **A1 standart** aşağıda gösterildiği gibi ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="bc405-118">In the **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Azure portal - bir boyutu seçin](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="bc405-120">İçinde **ayarları** dikey penceresinde tıklatın **genel IP adresi**, sonra **ortak IP adresi oluştur** dikey altında **atama**, 'ıtıklatın **Statik** aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="bc405-120">In the **Settings** blade, click **Public IP address**, then in the **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="bc405-121">Ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bc405-121">And then click **OK**.</span></span>
   
    ![Azure portal - ortak IP adresi oluştur](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="bc405-123">İçinde **ayarları** dikey penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bc405-123">In the **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="bc405-124">Gözden geçirme **Özet** dikey penceresini aşağıda gösterildiği gibi ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bc405-124">Review the **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Azure portal - ortak IP adresi oluştur](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="bc405-126">Yeni bir kutucuk Panonuzda dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bc405-126">Notice the new tile in your dashboard.</span></span>
   
    ![Azure portal - ortak IP adresi oluştur](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="bc405-128">VM oluşturulduktan sonra **ayarları** dikey penceresi aşağıda gösterildiği gibi görüntülenir</span><span class="sxs-lookup"><span data-stu-id="bc405-128">Once the VM is created, the **Settings** blade will be displayed as shown below</span></span>
    
    ![Azure portal - ortak IP adresi oluştur](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

