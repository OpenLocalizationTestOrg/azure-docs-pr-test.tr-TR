---
title: "aaaConfiguring ve Visual Studio ile depolama öykünücüsü hello kullanarak | Microsoft Docs"
description: "Yapılandırma ve Visual Studio ile Merhaba depolama öykünücüsünü kullanma"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: c8e7996f-6027-4762-806e-614b93131867
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/17/2017
ms.author: kraigb
ms.openlocfilehash: d590f21146c86bcb7bfa6b6164b92c6df5938d5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-hello-storage-emulator-with-visual-studio"></a>Yapılandırma ve Visual Studio ile Merhaba depolama öykünücüsünü kullanma
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Genel Bakış
Hello Azure SDK geliştirme ortamı hello depolama öykünücüsü, hello Blob, kuyruk ve tablo depolama hizmetleri, yerel geliştirme makinenizde Azure'da kullanılabilir benzetim yapan bir yardımcı program içerir. Kullanıyorsanız hello Azure storage hizmetleri kullanan bir bulut hizmeti oluşturma veya herhangi bir dış uygulama çağrıları depolama hizmetleri hello yazma, kodunuzu hello storage öykünücüsüne karşı yerel olarak test edebilirsiniz. Microsoft Visual Studio için Hello Azure Araçları Visual Studio'ya hello depolama öykünücüsünü yönetim tümleştirin. Merhaba depolama öykünücüsü veritabanı ilk kullanımda Hello Azure Araçları başlatmak, çalıştırdığınızda veya Visual Studio kodunuzdan hata ayıklama ve salt okunur erişim toohello depolama öykünücüsü veri hello Azure Storage Gezgini aracılığıyla sağlayan depolama öykünücüsü hizmeti başlatır hello.

Merhaba depolama öykünücüsü sistem gereksinimleri ve özel yapılandırma yönergeleri de dahil olmak üzere hakkında ayrıntılı bilgi için bkz: [kullanım hello geliştirme ve sınama için Azure Storage öykünücüsü](storage/common/storage-use-emulator.md).

> [!NOTE]
> Bazı hello depolama öykünücüsü benzetimi ve hello Azure storage Hizmetleri arasındaki işlevsel farklılıklar vardır. Bkz: [arasındaki farklar depolama öykünücüsü hello ve Azure depolama hizmetleri](storage/common/storage-use-emulator.md) hello hello belirli farklılıklar hakkında bilgi için Azure SDK belgeleri içinde.
> 
> 

## <a name="configuring-a-connection-string-for-hello-storage-emulator"></a>Merhaba depolama öykünücüsü için bağlantı dizesini yapılandırma
bir rolü içindeki kodundan tooaccess hello depolama öykünücüsü, tooconfigure bir bağlantı dizesi bu noktaları toohello depolama öykünücüsü ve daha sonra değiştirilen toopoint tooan Azure depolama hesabı olabilir isteyeceksiniz. Bir bağlantı dizesi çalışma zamanı tooconnect tooa depolama hesabı rolünüze okuyabilen bir yapılandırma ayardır. Hakkında daha fazla bilgi için bkz toocreate bağlantı dizeleri, [yapılandırma hello Azure uygulama](https://msdn.microsoft.com/library/azure/2da5d6ce-f74d-45a9-bf6b-b3a60c5ef74e#BK_SettingsPage).

> [!NOTE]
> Hello kullanarak bir başvuru toohello depolama öykünücüsü hesabı kodunuzdan döndürebilir **DevelopmentStorageAccount** özelliği. Tooaccess hello kodunuzdan depolama öykünücüsü, ancak uygulama tooAzure toopublish planlıyorsanız, Azure depolama hesabınızın toocreate bir bağlantı dizesi tooaccess ihtiyacınız ve kod toouse değiştirmek isterseniz, bu yaklaşım düzgün çalışır, yayımlamadan önce bağlantı dizesi. Bir bağlantı dizesi, bir Azure depolama hesabı hello depolama öykünücüsü hesabı arasında sıklıkla geçiş yapıyorsanız, bu işlemi basitleştirir.
> 
> 

## <a name="initializing-and-running-hello-storage-emulator"></a>Başlatma ve hello depolama öykünücüsünün çalışır durumda
Çalıştırın ya da hizmetiniz Visual Studio'da hata ayıklama Visual Studio hello depolama öykünücüsü otomatik olarak başlatır belirtebilirsiniz. Çözüm Gezgini'nde hello kısayol menüsünü açın, **Azure** proje ve seçin **özellikleri**. Merhaba üzerinde **geliştirme** sekmede hello **Başlat Azure Storage öykünücüsü** listesinde, seçin **True** (Bu zaten toothat değer ayarlanmamışsa).

Merhaba çalıştırın ya da hizmetiniz Visual Studio'dan hello depolama öykünücüsü hata ayıklama ilk kez bir başlatma işlemi başlatır. Bu işlem yerel bağlantı noktaları için hello depolama öykünücüsü ayırır ve hello depolama öykünücüsü veritabanı oluşturur. Merhaba depolama öykünücüsü veritabanı silinmedikçe tamamlandıktan sonra bu işlem toorun yeniden gerekmez.

> [!NOTE]
> Hello Azure Araçları, Hello Haziran 2012 sürüm ile başlayarak, hello depolama öykünücüsü, varsayılan olarak, SQL Express LocalDB çalışır. SQL Express 2005 veya 2008, varsayılan örneği karşı hello depolama öykünücüsü hello Azure Araçları önceki sürümlerde çalışır önce yüklemeniz gereken hello Azure SDK'sı yükleyebilirsiniz. Merhaba storage öykünücüsüne karşı SQL Express veya bir adlandırılmış'ın adlandırılmış örneği veya Microsoft SQL Server varsayılan örneğini de çalıştırabilirsiniz. Tooconfigure hello depolama öykünücüsü toorun hello varsayılan örnek dışında bir örneğiyle gerekirse bkz [kullanım hello geliştirme ve sınama için Azure Storage öykünücüsü](storage/common/storage-use-emulator.md).
> 
> 

toostart, durdurmak ve bunları sıfırlamak ve Hello depolama öykünücüsü hello yerel depolama Hizmetleri kullanıcı arabirimi tooview hello durumunu sağlar. Merhaba depolama öykünücüsü Hizmet başladıktan sonra hello kullanıcı arabirimi görüntüler veya Başlat veya hello bildirim alanı simgesini sağ tıklanarak hello Hizmeti Durdur hello Microsoft Azure öykünücüsünü hello Windows görev çubuğunda.

## <a name="viewing-storage-emulator-data-in-server-explorer"></a>Server Explorer'da depolama öykünücüsü verileri görüntüleme
Depolama öykünücüsü de dahil olmak üzere depolama hesaplarınızı tablo verileri hello ve Sunucu Gezgininde Hello Azure Depolama düğümü blob tooview veri ve değişiklik ayarlarını sağlar. Bkz: [Depolama Gezgini (Önizleme) ile Azure Blob Storage'ı yönetme kaynaklarını](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs) daha fazla bilgi için.

