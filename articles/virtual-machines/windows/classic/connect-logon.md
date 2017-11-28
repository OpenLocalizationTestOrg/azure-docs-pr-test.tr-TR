---
title: Klasik Azure VM oturumunu | Microsoft Docs
description: "Klasik dağıtım modeli kullanılarak oluşturulmuş bir Windows sanal makine oturum açmak için Azure portalını kullanın."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 43d54de7e875de9212c23c49ad0539bf2272a312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="log-on-to-a-windows-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="b2623-103">Azure Portal kullanarak bir Windows sanal makinesinde oturum açma</span><span class="sxs-lookup"><span data-stu-id="b2623-103">Log on to a Windows virtual machine using the Azure portal</span></span>
<span data-ttu-id="b2623-104">Azure portalında kullandığınız **Bağlan** bir Uzak Masaüstü oturumu ve bir Windows VM oturumunu Başlat düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b2623-104">In the Azure portal, you use the **Connect** button to start a Remote Desktop session and log on to a Windows VM.</span></span>

<span data-ttu-id="b2623-105">Bir Linux VM bağlanmak istiyor?</span><span class="sxs-lookup"><span data-stu-id="b2623-105">Do you want to connect to a Linux VM?</span></span> <span data-ttu-id="b2623-106">Bkz: [Linux çalıştıran bir sanal makine için oturum açma](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="b2623-106">See [How to log on to a virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how to [perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="b2623-107">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b2623-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b2623-108">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="b2623-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="b2623-109">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="b2623-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="b2623-110">Resource Manager modelini kullanarak bir VM'de oturum açma hakkında daha fazla bilgi için bkz: [burada](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2623-110">For information about how to log on to a VM using the Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="b2623-111">Sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="b2623-111">Connect to the virtual machine</span></span>
1. <span data-ttu-id="b2623-112">Azure Portal’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b2623-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="b2623-113">Erişmek istediğiniz sanal makineye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b2623-113">Click on the virtual machine that you want to access.</span></span> <span data-ttu-id="b2623-114">Ad içinde listelenen **tüm kaynakları** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="b2623-114">The name is listed in the **All resources** pane.</span></span>

    ![Sanal makine konumları](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="b2623-116">Tıklatın **Bağlan** sanal makine Pano üzerinde komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="b2623-116">Click **Connect** on the command bar atop the virtual machine dashboard.</span></span>

    ![Sanal makine için simge Bağlan](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If the **Connect** button isn't available, see the troubleshooting tips at the end of this article.
>
>
-->

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="b2623-118">Sanal makinede oturum açma</span><span class="sxs-lookup"><span data-stu-id="b2623-118">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="b2623-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2623-119">Next steps</span></span>
* <span data-ttu-id="b2623-120">Varsa **Bağlan** düğmesi etkin değil veya Uzak Masaüstü Bağlantısı ile ilgili başka sorununuz, yapılandırmayı sıfırlamayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="b2623-120">If the **Connect** button is inactive or you are having other problems with the Remote Desktop connection, try resetting the configuration.</span></span> <span data-ttu-id="b2623-121">tıklatın **sıfırlama uzaktan erişim** sanal makine panosundan.</span><span class="sxs-lookup"><span data-stu-id="b2623-121">click **Reset remote access** from the virtual machine dashboard.</span></span>

    ![Sıfırlama uzaktan erişim](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="b2623-123">Parolanızı sorunlar için onu sıfırlamayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="b2623-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="b2623-124">Tıklatın **parola sıfırlama** sol kenarına sanal makine panoyu altında **destek + sorun giderme**.</span><span class="sxs-lookup"><span data-stu-id="b2623-124">Click **Reset password** along the left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Parola sıfırlama](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="b2623-126">Bu ipuçları çalışmıyor veya ne bkz ihtiyacınız olmayan [sorun giderme Uzak Masaüstü bağlantıları için Windows tabanlı Azure sanal makine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2623-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b2623-127">Bu makale ortak sorunları tanılama ve çözme boyunca size yol gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="b2623-127">This article walks you through diagnosing and resolving common problems.</span></span>
