---
title: "aaaInstall Azure Windows VM üzerinde MongoDB | Microsoft Docs"
description: "Windows Server çalıştıran hello Klasik dağıtım modeliyle tooinstall Azure VM'de MongoDB nasıl oluşturulacağını öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a>Windows Azure VM MongoDB yükleyin.
> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).  Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. tooinstall ve hello Resource Manager dağıtım modelini kullanarak MongoDB yapılandırmak için bkz: [bu makalede](../install-mongodb.md).

[MongoDB] [ MongoDB] bir popüler açık kaynak, yüksek performanslı NoSQL veritabanıdır. Bu makalede, bir Windows Server hello kullanarak sanal makine (VM) oluşturmada size yol gösterir [Azure portal][AzurePortal]. Ardından oluşturun ve bir veri diski toohello yükleyip MongoDB yapılandırmadan önce VM ekleyin. Mevcut bir VM'yi toouse istediğiniz Azure'da varsa, doğrudan çok atlayabilirsiniz[yükleme ve yapılandırma MongoDB](#install-and-run-mongodb-on-the-virtual-machine).

## <a name="create-a-virtual-machine-running-windows-server"></a>Windows Server çalıştıran bir sanal makine oluşturma
Bu yönergeler toocreate bir sanal makine izleyin.

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> Merhaba sanal makine oluşturulurken MongoDB için bir uç nokta ekleyin ve aşağıdaki gibi yapılandırın: olarak adlandırın **Mongo**, kullanın **TCP** hello Protokolü hem de kümesi ortak ve özel bağlantı noktalarını çok hello gibi**27017**.
>
>

## <a name="attach-a-data-disk"></a>Veri diski ekleme
tooprovide depolama hello sanal makine için bir veri diskini ve Windows kullanabilmesi başlatılamıyor. Bir veri diski varsa, bu varolan bir diski ekleyebilirsiniz ya da boş bir disk ekleyin.

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

Merhaba disk başlatma ile ilgili yönergeler için bkz: "nasıl yapılır: Windows Server'da yeni bir veri diski başlatın" içinde [nasıl tooattach bir veri diski tooa Windows sanal makine](attach-disk.md).

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a>Yükleyin ve MongoDB hello sanal makinede çalıştırın
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a>Özet
Bu öğreticide, nasıl toocreate Windows Server çalıştıran bir sanal makine uzaktan tooit bağlanın ve bir veri diskini öğrendiniz.  Ayrıca nasıl öğrenilen tooinstall ve MongoDB hello Windows tabanlı sanal makinede yapılandırın. Artık MongoDB hello Windows tabanlı sanal makineye göre hello konularında Gelişmiş hello aşağıdaki erişebilirsiniz [MongoDB belgelerine][MongoDocs].

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

