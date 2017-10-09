---
title: "aaaCreate hello Azure portal'ın Windows VM için FQDN | Microsoft Docs"
description: "Nasıl toocreate bir tam etki alanı adı veya FQDN, bir kaynak yöneticisi için sanal makine hello Azure portal'ın temel bilgi edinin."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a>Bir tam etki alanı adı için bir Windows VM hello Azure portal oluşturma

Bir sanal makine (VM) hello oluşturduğunuzda [Azure portal](https://portal.azure.com), genel IP kaynağı hello sanal makine için otomatik olarak oluşturulur. Bu IP adresi tooremotely erişim hello VM kullanın. Merhaba portal oluşturmaz rağmen bir [tam etki alanı adı](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), veya FQDN, oluşturabilmeniz hello VM oluşturulduktan sonra. Bu makalede hello adımları toocreate bir DNS adı veya FQDN gösterilmektedir.

## <a name="create-a-fqdn"></a>Bir FQDN oluşturma
Bu makale, bir VM zaten oluşturduğunuzu varsayar. Gerekirse, [hello Portalı'nda bir VM oluşturma](quick-create-portal.md) veya [Azure PowerShell ile](quick-create-powershell.md). VM çalışır durumda sonra aşağıdaki adımları izleyin:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

Bu DNS adı gibi Uzak Masaüstü Protokolü (RDP) kullanarak VM toohello artık uzaktan bağlanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Bir ortak IP ve DNS adı, VM sahip, ortak uygulama çerçeveleri veya IIS, SQL ve SharePoint gibi hizmetleri dağıtabilirsiniz.

Ayrıca daha fazla hakkında bilgiyi [Kaynak Yöneticisi'ni kullanarak](../../azure-resource-manager/resource-group-overview.md) Azure dağıtımlarınızı oluşturma ipuçları için.

