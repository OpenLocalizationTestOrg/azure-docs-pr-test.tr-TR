---
title: "aaaLog tooa üzerinde Klasik Azure VM | Microsoft Docs"
description: "Merhaba Klasik dağıtım modeli kullanılarak oluşturulmuş tooa Windows sanal makinesinde Hello Azure portal toolog kullanın."
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
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="8b72f-103">Hello Azure portal kullanarak Windows sanal makine üzerinde tooa oturum</span><span class="sxs-lookup"><span data-stu-id="8b72f-103">Log on tooa Windows virtual machine using hello Azure portal</span></span>
<span data-ttu-id="8b72f-104">Hello Azure portal, kullandığınız hello **Bağlan** düğmesini toostart bir Uzak Masaüstü oturumu ve tooa Windows VM üzerinde oturum.</span><span class="sxs-lookup"><span data-stu-id="8b72f-104">In hello Azure portal, you use hello **Connect** button toostart a Remote Desktop session and log on tooa Windows VM.</span></span>

<span data-ttu-id="8b72f-105">Tooconnect tooa Linux VM istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="8b72f-105">Do you want tooconnect tooa Linux VM?</span></span> <span data-ttu-id="8b72f-106">Bkz: [nasıl toolog Linux çalıştıran tooa sanal makine üzerinde](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="8b72f-106">See [How toolog on tooa virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="8b72f-107">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8b72f-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8b72f-108">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="8b72f-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="8b72f-109">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="8b72f-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="8b72f-110">Model nasıl tooa VM kullanma toolog hello Resource Manager hakkında bilgi için bkz: [burada](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b72f-110">For information about how toolog on tooa VM using hello Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="8b72f-111">Toohello sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="8b72f-111">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="8b72f-112">Toohello Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8b72f-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="8b72f-113">Tooaccess istediğiniz Hello sanal makineye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b72f-113">Click on hello virtual machine that you want tooaccess.</span></span> <span data-ttu-id="8b72f-114">Merhaba adı hello listelenen **tüm kaynakları** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="8b72f-114">hello name is listed in hello **All resources** pane.</span></span>

    ![Sanal makine konumları](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="8b72f-116">Tıklatın **Bağlan** hello komut çubuğunda hello sanal makine Pano üzerinde.</span><span class="sxs-lookup"><span data-stu-id="8b72f-116">Click **Connect** on hello command bar atop hello virtual machine dashboard.</span></span>

    ![Bağlan hello sanal makine için simgesi](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="8b72f-118">Toohello sanal makinede oturum açın</span><span class="sxs-lookup"><span data-stu-id="8b72f-118">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="8b72f-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8b72f-119">Next steps</span></span>
* <span data-ttu-id="8b72f-120">Merhaba, **Bağlan** düğmesi etkin değil veya hello Uzak Masaüstü Bağlantısı ile ilgili başka sorununuz, hello yapılandırma sıfırlamayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="8b72f-120">If hello **Connect** button is inactive or you are having other problems with hello Remote Desktop connection, try resetting hello configuration.</span></span> <span data-ttu-id="8b72f-121">tıklatın **sıfırlama uzaktan erişim** hello sanal makine panosundan.</span><span class="sxs-lookup"><span data-stu-id="8b72f-121">click **Reset remote access** from hello virtual machine dashboard.</span></span>

    ![Sıfırlama uzaktan erişim](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="8b72f-123">Parolanızı sorunlar için onu sıfırlamayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="8b72f-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="8b72f-124">Tıklatın **parola sıfırlama** hello altında sanal makine Pano kenarı sol **destek + sorun giderme**.</span><span class="sxs-lookup"><span data-stu-id="8b72f-124">Click **Reset password** along hello left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Parola sıfırlama](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="8b72f-126">Bu ipuçları çalışmıyor veya ne bkz ihtiyacınız olmayan [sorun giderme Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b72f-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="8b72f-127">Bu makale ortak sorunları tanılama ve çözme boyunca size yol gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="8b72f-127">This article walks you through diagnosing and resolving common problems.</span></span>
