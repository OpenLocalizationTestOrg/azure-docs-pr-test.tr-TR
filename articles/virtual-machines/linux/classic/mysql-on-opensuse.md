---
title: aaaInstall OpenSUSE VM'de MySQL | Microsoft Docs
description: "Tooinstall MySQL, azure'da OpenSUSE Linux VMirtual makinede öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1594e10e-c314-455a-9efb-a89441de364b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/19/2016
ms.author: cynthn
ms.openlocfilehash: 8f96d29f29cb9c466dd7fdaf92b378783fdaacd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a>Azure'da OpenSUSE Linux çalıştıran bir sanal makineye MySQL yükleme
[MySQL] [ MySQL] popüler, açık kaynaklı bir SQL veritabanı. Bu öğreticide gösterilmiştir nasıl toocreate OpenSUSE Linux çalıştıran bir sanal makine kurun MySQL.

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a>OpenSUSE Linux çalıştıran bir sanal makine oluşturma
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a>Yükleyin ve MySQL hello sanal makinede çalıştırın
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a>Sonraki adımlar
Merhaba MySQL hakkında daha fazla bilgi için bkz [MySQL belgeleri][MySQLDocs].

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

