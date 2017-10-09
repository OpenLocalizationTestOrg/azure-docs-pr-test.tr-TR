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
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a>Hello Azure portal kullanarak Windows sanal makine üzerinde tooa oturum
Hello Azure portal, kullandığınız hello **Bağlan** düğmesini toostart bir Uzak Masaüstü oturumu ve tooa Windows VM üzerinde oturum.

Tooconnect tooa Linux VM istiyor musunuz? Bkz: [nasıl toolog Linux çalıştıran tooa sanal makine üzerinde](../../linux/mac-create-ssh-keys.md).

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Model nasıl tooa VM kullanma toolog hello Resource Manager hakkında bilgi için bkz: [burada](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="connect-toohello-virtual-machine"></a>Toohello sanal makineye bağlanma
1. Toohello Azure portalında oturum açın.
2. Tooaccess istediğiniz Hello sanal makineye tıklayın. Merhaba adı hello listelenen **tüm kaynakları** bölmesi.

    ![Sanal makine konumları](./media/connect-logon/azureportaldashboard.png)

3. Tıklatın **Bağlan** hello komut çubuğunda hello sanal makine Pano üzerinde.

    ![Bağlan hello sanal makine için simgesi](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a>Toohello sanal makinede oturum açın
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba, **Bağlan** düğmesi etkin değil veya hello Uzak Masaüstü Bağlantısı ile ilgili başka sorununuz, hello yapılandırma sıfırlamayı deneyin. tıklatın **sıfırlama uzaktan erişim** hello sanal makine panosundan.

    ![Sıfırlama uzaktan erişim](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* Parolanızı sorunlar için onu sıfırlamayı deneyin. Tıklatın **parola sıfırlama** hello altında sanal makine Pano kenarı sol **destek + sorun giderme**.

    ![Parola sıfırlama](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

Bu ipuçları çalışmıyor veya ne bkz ihtiyacınız olmayan [sorun giderme Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Bu makale ortak sorunları tanılama ve çözme boyunca size yol gösterecektir.
