---
title: "aaaCreate hello Azure Portal işlevi uygulamadan | Microsoft Docs"
description: "Yeni bir işlev uygulaması Azure App Service'te hello portalından oluşturun."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a>Azure portal hello bir işlev uygulaması oluşturma

Azure işlev uygulamalarının hello Azure App Service altyapısı kullanır. Bu konu, nasıl gösterir toocreate hello Azure portal'ın bir işlev uygulaması. Bir işlev uygulaması tekil işlevler hello yürütülmesi barındıran hello kapsayıcıdır. Bir işlev uygulaması hello App Service barındırma planı oluşturduğunuzda, işlevi uygulamanızı App Service tüm hello özelliklerini kullanabilirsiniz.

## <a name="create-a-function-app"></a>İşlev uygulaması oluşturma

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

Bir işlev uygulaması oluşturduğunuzda, geçerli bir tedarik **uygulama adı**, hangi içerebilir yalnızca harf, rakam ve kısa çizgi. Alt çizgi (**_**) izin verilen bir karakter değildir.

Depolama hesabı adları 3 ile 24 karakter arasında olmalı ve yalnızca sayıyla küçük harf içermelidir. Depolama hesabınızın adının Azure içinde benzersiz olması gerekir. 

Merhaba işlevi uygulama oluşturulduktan sonra bir veya daha fazla farklı dillerde tekil işlevler oluşturabilirsiniz. İşlevler Oluştur [hello portalını kullanarak](functions-create-first-azure-function.md#create-function), [sürekli dağıtım](functions-continuous-deployment.md), ya da [FTP ile karşıya](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).

## <a name="service-plans"></a>Hizmet planları

Azure işlevleri sahip iki farklı hizmet planları: Tüketim planlama ve uygulama hizmeti planı. kod çalışmadığı zaman, kodunuzu, Ölçek genişletme gerekli toohandle yükü olarak ve ardından ölçekler bileşenini çalışırken hello tüketim planı otomatik olarak işlem gücü ayırır. Uygulama hizmeti planı Hello işlevinizi uygulama erişim tooall hello tesis App Service'in sağlar. İşlev uygulamanızı oluşturulur ve şu anda değiştirilemez, hizmeti planınızı seçmeniz gerekir. Daha fazla bilgi için bkz: [barındırma planı bir Azure işlevleri arasından seçim](functions-scale.md).

Bir uygulama hizmeti planı toorun JavaScript işlevleri planlıyorsanız, daha az çekirdek planla seçmeniz gerekir. Daha fazla bilgi için bkz: Merhaba [işlevleri için JavaScript başvurusu](functions-reference-node.md#choose-single-core-app-service-plans).

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a>Depolama hesabı gereksinimleri

Bir işlev uygulaması App Service'te oluştururken oluşturmanız veya Blob, kuyruk ve tablo depolama destekleyen tooa genel amaçlı Azure depolama hesabı bağlantı gerekir. Dahili olarak, işlevlerini kullanan depolama Tetikleyicileri yönetme ve işlev yürütmeleri günlüğü gibi işlemler için. Bazı depolama hesapları, kuyruklar ve tablolar, yalnızca blob storage hesapları, Azure Premium Storage ve ZRS çoğaltma genel amaçlı depolama hesaplarıyla gibi desteklemez. Bu hesapları dışı hello depolama hesabı dikey penceresinden bir işlev uygulaması oluştururken filtrelenir.

>[!NOTE]
>Hello tüketim barındırma planı kullanırken, işlevi kod ve bağlama yapılandırma dosyaları Azure File storage hello ana depolama hesabında depolanır. Merhaba ana depolama hesabını sildiğinizde, bu içeriği silinir ve kurtarılamaz.

Depolama hesabı türleri hakkında daha fazla toolearn bkz [hello Azure Storage hizmetlerine giriş](../storage/common/storage-introduction.md#introducing-the-azure-storage-services). 

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



