---
title: "aaaAzure bulut Kabuğu (Önizleme) hızlı başlangıç | Microsoft Docs"
description: "Hello Azure bulut kabuğu için hızlı başlangıç"
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
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a>Hello Azure bulut Kabuğu'nu kullanmak için hızlı başlangıç

Bu belge nasıl toouse hello Azure bulut Kabuk hello ayrıntıları [Azure portal](https://ms.portal.azure.com/).

## <a name="start-cloud-shell"></a>Bulut Kabuğu'nu başlatın
1. Başlatma **bulut Kabuk** hello üst gezinti hello Azure portal, gelen <br>
![](media/shell-icon.png)
2. Bir abonelik toocreate bir depolama hesabı ve Azure dosya paylaşımı seçin
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
Bir Ubuntu VM, yeni kaynak grubu oluşturun. Hello Azure CLI 2.0 SSH anahtarları ve Kurulum hello VM bunlarla oluşturur. <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> VM yerleştirilir kullanılan ortak ve özel anahtarlar tooauthenticate hello `/User/.ssh/id_rsa` ve `/User/.ssh/id_rsa.pub` varsayılan olarak Azure CLI 2.0 tarafından. .Ssh klasörü, bağlı Azure dosya paylaşımının 5 GB görüntüde kalıcıdır.

Bulut Kabuğu'nda kullanılan kullanıcı adı, kullanıcı adı bu VM'de olacaktır ($User@Azure:).

### <a name="ssh-into-your-linux-vm"></a>SSH, Linux VM'NİZDE içine
1. VM adınızı hello Azure portal arama çubuğunda arayın
2. "Bağlan"'ı tıklatın ve çalıştırın:`ssh username@ipaddress`

![](media/sshcmd-copy.png)

Hello SSH bağlantı kurulduktan sonra hello Ubuntu Hoş Geldiniz istemi görmeniz gerekir.
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a>Temizleme 
Kaynak grubu ve içerdiği tüm kaynaklar Sil: <br>
`az group delete -n MyRG` öğesini çalıştırın

## <a name="next-steps"></a>Sonraki Adımlar
[Bulut Kabuk üzerinde kalıcı depolama hakkında bilgi edinin](persisting-shell-storage.md) <br>
[Azure CLI 2.0 hakkında bilgi edinin](https://docs.microsoft.com/cli/azure/) <br>
[Azure File storage hakkında bilgi edinin](../storage/files/storage-files-introduction.md) <br>