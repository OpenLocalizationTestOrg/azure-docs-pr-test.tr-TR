---
title: "bir Linux VM hello Azure portal'ın FQDN'si aaaCreate | Microsoft Docs"
description: "Nasıl toocreate bir tam etki alanı adı veya FQDN, bir kaynak yöneticisi için sanal makine hello Azure portal'ın temel bilgi edinin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a>Bir tam etki alanı adı hello Azure portalı için bir Linux VM oluşturun.

Bir sanal makine (VM) hello oluşturduğunuzda [Azure portal](https://portal.azure.com), genel IP kaynağı hello sanal makine için otomatik olarak oluşturulur. Bu IP adresi tooremotely erişim hello VM kullanın. Merhaba portal oluşturmaz rağmen bir [tam etki alanı adı](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), veya FQDN, ekleyebileceğiniz bir hello VM oluşturulduktan sonra. Bu makalede hello adımları toocreate bir DNS adı veya FQDN gösterilmektedir.

## <a name="create-a-fqdn"></a>Bir FQDN oluşturma
Bu makale, bir VM zaten oluşturduğunuzu varsayar. Gerekirse, [hello Portalı'nda bir VM oluşturma](quick-create-portal.md) veya [hello Azure CLI ile](quick-create-cli.md). VM çalışır durumda sonra aşağıdaki adımları izleyin:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

Şimdi ile bu DNS kullanarak VM adı gibi toohello uzaktan bağlanabilirsiniz `ssh azureuser@mydns.westus.cloudapp.azure.com`.

## <a name="next-steps"></a>Sonraki adımlar
VM'yi bir ortak IP ve DNS adı olan, yaygın uygulama çerçeveleri veya nginx, MongoDB, Docker, gibi hizmetleri dağıtabilirsiniz vs.

Ayrıca daha fazla hakkında bilgiyi [Kaynak Yöneticisi'ni kullanarak](../../azure-resource-manager/resource-group-overview.md) Azure dağıtımlarınızı oluşturma ipuçları için.

