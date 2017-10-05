---
title: "Azure bulut Kabuğu (Önizleme) hızlı başlangıç | Microsoft Docs"
description: "Azure bulut kabuğu için hızlı başlangıç"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 75676eb0ab784e2adbfd27b170c1dee5599b74ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-for-using-the-azure-cloud-shell"></a>Azure bulut Kabuğu'nu kullanarak için hızlı başlangıç

Bu belgede Azure bulut Kabuğu'nda kullanmak üzere nasıl ayrıntıları [Azure portal](https://ms.portal.azure.com/).

## <a name="start-cloud-shell"></a>Bulut Kabuğu'nu başlatın
1. Başlatma **bulut Kabuk** Azure portal'ın üst gezinti gelen <br>
![](media/shell-icon.png)
2. Bir depolama hesabı ve Azure dosya paylaşımı oluşturmak için bir abonelik seçin
3. "Depolama oluştur" seçeneğini belirleyin

> [!TIP]
> Azure CLI 2.0 için her oturumu otomatik olarak doğrulanır.

### <a name="set-your-subscription"></a>Aboneliğinizi
1. Liste abonelikler erişebilirsiniz: <br>
`az account list`
2. Tercih edilen aboneliğinizi ayarlayın: <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> Aboneliğinizi kullanarak sonraki oturumlar için hatırlanır `/home/<user>/.azure/azureProfile.json`.

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
İçinde WestUS "MyRG" adlı yeni bir kaynak grubu oluşturun: <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a>Linux VM oluşturma
Bir Ubuntu VM, yeni kaynak grubu oluşturun. Azure CLI 2.0 SSH anahtarları oluşturma ve bunlarla VM ayarlayın. <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> VM kimliğini doğrulamak için kullanılan ortak ve özel anahtarlar yerleştirilir `/User/.ssh/id_rsa` ve `/User/.ssh/id_rsa.pub` varsayılan olarak Azure CLI 2.0 tarafından. .Ssh klasörü, bağlı Azure dosya paylaşımının 5 GB görüntüde kalıcıdır.

Bulut Kabuğu'nda kullanılan kullanıcı adı, kullanıcı adı bu VM'de olacaktır ($User@Azure:).

### <a name="ssh-into-your-linux-vm"></a>SSH, Linux VM'NİZDE içine
1. Azure portal arama çubuğunda, VM adı arayın
2. "Bağlan"'ı tıklatın ve çalıştırın:`ssh username@ipaddress`

![](media/sshcmd-copy.png)

SSH bağlantı kurulduktan sonra Ubuntu Hoş Geldiniz istemi görmeniz gerekir.
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a>Temizleme 
Kaynak grubu ve içerdiği tüm kaynaklar Sil: <br>
`az group delete -n MyRG` öğesini çalıştırın

## <a name="next-steps"></a>Sonraki Adımlar
[Bulut Kabuk üzerinde kalıcı depolama hakkında bilgi edinin](persisting-shell-storage.md) <br>
[Azure CLI 2.0 hakkında bilgi edinin](https://docs.microsoft.com/cli/azure/) <br>
[Azure File storage hakkında bilgi edinin](../storage/files/storage-files-introduction.md) <br>