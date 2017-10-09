---
title: "aaaDownload hello PHP için Azure SDK'sı"
description: "Nasıl toodownload ve yükleme PHP için Azure SDK'sı hello öğrenin."
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a>PHP için Hello Azure SDK'sını indirme
## <a name="overview"></a>Genel Bakış
Merhaba PHP için Azure SDK toodevelop izin, dağıtmak ve PHP uygulamaları için Azure yöneten bileşenleri içerir. Özellikle, hello PHP için Azure SDK hello aşağıdakileri içerir:

* **Azure için PHP istemci kitaplıkları hello**. Bu sınıf kitaplıkları Veri Yönetimi Hizmetleri gibi Azure özelliklere erişmek için bir arabirim sağlar ve bulut Hizmetleri.  
* **Merhaba Mac, Linux ve Windows (Azure CLI) için Azure komut satırı arabirimi**. Bu, dağıtmak ve Azure Web siteleri ve Azure sanal makineler gibi Azure hizmetleri yönetmek için komutlar kümesidir. Merhaba Mac, Linux ve Windows dahil olmak üzere herhangi bir platform üzerinde Azure CLI çalışma.
* **Azure PowerShell (yalnızca Windows)**. Bu, dağıtmak ve bulut Hizmetleri ve sanal makineler gibi Azure hizmetleri yönetmek için PowerShell cmdlet'leri kümesidir.
* **Merhaba (yalnızca Windows) Azure öykünücüsünü**. Merhaba işlem ve depolama öykünücüsünü bulut Hizmetleri ve tootest uygulama yerel olarak izin veri yönetimi hizmetleri yerel Öykünücüler ' dir. Hello Azure öykünücüsünü yalnızca Windows üzerinde çalıştırın.

Aşağıdaki Hello bölümler, yukarıda açıklanan bileşenleri toodownload ve yükleme nasıl hello anlatmaktadır.

Merhaba bu konudaki yönergeler sahip olduğunuz varsayılmıştır [PHP] [ install-php] yüklü.

> [!NOTE]
> Azure için PHP 5.5 veya daha yüksek toouse hello PHP istemci kitaplıkları olması gerekir.
> 
> 

## <a name="php-client-libraries-for-azure"></a>Azure için PHP istemci kitaplıkları
Azure için Hello PHP istemci kitaplıkları, Veri Yönetimi Hizmetleri gibi Azure özelliklere erişmek için bir arabirim sağlar ve bulut hizmetlerinden herhangi bir işletim sistemi. Bu kitaplıklar Oluşturucu hello yüklenebilir.

Nasıl toouse hello Azure için PHP istemci kitaplıkları hakkında daha fazla bilgi için bkz: [nasıl tooUse hello Blob hizmeti][blob-service], [nasıl tooUse hello tablo hizmeti] [ table-service] ve [nasıl tooUse hello sıra hizmeti][queue-service].

### <a name="install-via-composer"></a>Oluşturucu yükleyin
1. [Git'i yükleyin][install-git].

    > [AZURE.NOTE] Windows üzerinde tooadd hello Git yürütülebilir tooyour PATH ortam değişkeni de gerekir.

1. Adlı bir dosya oluşturun **composer.json** hello projenizin kök ve kod tooit aşağıdaki hello ekleyin:
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. Karşıdan  **[composer.phar] [ composer-phar]**  proje kök.
3. Bir komut istemi açın ve bu proje kök dizininde yürütme
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a>Azure PowerShell ve Azure öykünücüsünü
Azure PowerShell, dağıtma ve Azure Hizmetleri (örneğin, bulut Hizmetleri ve sanal makineler) yönetmek için PowerShell cmdlet'leri kümesidir. Hello Azure öykünücüsünü Öykünücüler bulut Hizmetleri ve tootest uygulama yerel olarak izin Veri Yönetimi Hizmetleri ' dir. Bu bileşenlerin desteklenen yalnızca Windows.

önerilen yöntem tooinstall Azure PowerShell hello ve hello Azure öykünücüsünü ise toouse hello [Microsoft Web Platformu yükleyicisi][download-wpi]. PHP, SQL Server, SQL Server için PHP ve WebMatrix için hello Microsoft Drivers gibi diğer geliştirme bileşenleri tooinstall de seçebilirsiniz unutmayın.

Hakkında bilgi için bkz toouse Azure PowerShell [nasıl tooUse Azure PowerShell][powershell-tools].

## <a name="azure-cli"></a>Azure CLI
Hello Azure CLI, dağıtma ve Azure Web siteleri ve Azure sanal makineler gibi Azure hizmetleri yönetmek için komutlar kümesidir. Azure CLI yükleme hakkında daha fazla bilgi için bkz: [yükleme hello Azure CLI](cli-install-nodejs.md).

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
