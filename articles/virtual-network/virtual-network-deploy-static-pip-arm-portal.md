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
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir statik genel IP adresiyle bir VM oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [Şablon](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Klasik)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md). Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a>Bir statik genel IP ile bir VM oluşturma

toocreate hello Azure portalı, aşağıdaki adımları tam hello VM bir statik genel IP adresi:

1. Tarayıcıdan toohello gidin [Azure portal](https://portal.azure.com) ve gerekiyorsa Azure hesabınızla oturum açın.
2. Merhaba üst sol alt köşesindeki hello portalı üzerinde tıklatın **yeni**>>**işlem**>**Windows Server 2012 R2 Datacenter**.
3. Merhaba, **dağıtım modeli seçin** listesinde, seçin **Resource Manager** tıklatıp **oluşturma**.
4. Merhaba, **Temelleri** dikey penceresinde, aşağıda gösterildiği gibi hello VM bilgileri girin ve ardından **Tamam**.
   
    ![Azure portal - temelleri](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. Merhaba, **bir boyutu seçin** dikey penceresinde tıklatın **A1 standart** aşağıda gösterildiği gibi ve ardından **seçin**.
   
    ![Azure portal - bir boyutu seçin](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. Merhaba, **ayarları** dikey penceresinde tıklatın **genel IP adresi**, hello sonra **ortak IP adresi oluştur** dikey altında **atama**,'ı tıklatın **Statik** aşağıda gösterildiği gibi. Ve ardından **Tamam**.
   
    ![Azure portal - ortak IP adresi oluştur](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. Merhaba, **ayarları** dikey penceresinde tıklatın **Tamam**.
8. Gözden geçirme hello **Özet** dikey penceresini aşağıda gösterildiği gibi ve ardından **Tamam**.
   
    ![Azure portal - ortak IP adresi oluştur](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. Yeni bir kutucuk Hello Panonuzda dikkat edin.
   
    ![Azure portal - ortak IP adresi oluştur](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. Merhaba VM oluşturulduktan sonra hello **ayarları** dikey penceresi aşağıda gösterildiği gibi görüntülenir
    
    ![Azure portal - ortak IP adresi oluştur](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

