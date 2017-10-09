---
title: bir statik genel IP adresi - Azure portal'yle bir VM'yi aaaCreate | Microsoft Docs
description: "Nasıl toocreate ile bir statik genel IP adresini kullanarak bir VM hello Azure portal hakkında bilgi edinin."
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
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a><span data-ttu-id="7de96-103">Hello Azure portal kullanarak bir statik genel IP adresiyle bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="7de96-103">Create a VM with a static public IP address using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7de96-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="7de96-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="7de96-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7de96-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="7de96-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7de96-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="7de96-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="7de96-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="7de96-108">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="7de96-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="7de96-109">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7de96-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7de96-110">Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.</span><span class="sxs-lookup"><span data-stu-id="7de96-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="7de96-111">Bir statik genel IP ile bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="7de96-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="7de96-112">toocreate hello Azure portalı, aşağıdaki adımları tam hello VM bir statik genel IP adresi:</span><span class="sxs-lookup"><span data-stu-id="7de96-112">toocreate a VM with a static public IP address in hello Azure portal, complete hello following steps:</span></span>

1. <span data-ttu-id="7de96-113">Tarayıcıdan toohello gidin [Azure portal](https://portal.azure.com) ve gerekiyorsa Azure hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7de96-113">From a browser, navigate toohello [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="7de96-114">Merhaba üst sol alt köşesindeki hello portalı üzerinde tıklatın **yeni**>>**işlem**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="7de96-114">On hello top left hand corner of hello portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="7de96-115">Merhaba, **dağıtım modeli seçin** listesinde, seçin **Resource Manager** tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="7de96-115">In hello **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="7de96-116">Merhaba, **Temelleri** dikey penceresinde, aşağıda gösterildiği gibi hello VM bilgileri girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7de96-116">In hello **Basics** blade, enter hello VM information as shown below, and then click **OK**.</span></span>
   
    ![Azure portal - temelleri](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="7de96-118">Merhaba, **bir boyutu seçin** dikey penceresinde tıklatın **A1 standart** aşağıda gösterildiği gibi ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="7de96-118">In hello **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Azure portal - bir boyutu seçin](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="7de96-120">Merhaba, **ayarları** dikey penceresinde tıklatın **genel IP adresi**, hello sonra **ortak IP adresi oluştur** dikey altında **atama**,'ı tıklatın **Statik** aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="7de96-120">In hello **Settings** blade, click **Public IP address**, then in hello **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="7de96-121">Ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7de96-121">And then click **OK**.</span></span>
   
    ![Azure portal - ortak IP adresi oluştur](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="7de96-123">Merhaba, **ayarları** dikey penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7de96-123">In hello **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="7de96-124">Gözden geçirme hello **Özet** dikey penceresini aşağıda gösterildiği gibi ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7de96-124">Review hello **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Azure portal - ortak IP adresi oluştur](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="7de96-126">Yeni bir kutucuk Hello Panonuzda dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7de96-126">Notice hello new tile in your dashboard.</span></span>
   
    ![Azure portal - ortak IP adresi oluştur](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="7de96-128">Merhaba VM oluşturulduktan sonra hello **ayarları** dikey penceresi aşağıda gösterildiği gibi görüntülenir</span><span class="sxs-lookup"><span data-stu-id="7de96-128">Once hello VM is created, hello **Settings** blade will be displayed as shown below</span></span>
    
    ![Azure portal - ortak IP adresi oluştur](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

