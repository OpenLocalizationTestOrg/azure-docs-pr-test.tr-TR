---
title: "Visual Studio'da bağlı hizmetler kullanarak Azure Storage aaaAdd | Microsoft Docs"
description: "Merhaba Visual Studio bağlı Hizmetleri Ekle iletişim kutusunu kullanarak Azure Storage tooyour uygulama Ekle"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Visual Studio bağlantılı hizmetler kullanarak Azure depolama ekleme
Visual Studio ile tooAzure depolama hello kullanarak aşağıdaki hello hiçbirini bağlayabilirsiniz **bağlı Hizmetleri Ekle** iletişim:

- C# bulut hizmeti
- .NET arka uç mobil hizmeti
- ASP.NET Web sitesi veya hizmeti
- ASP.NET Core hizmeti
- Azure Web işi hizmeti 

Merhaba bağlı hizmeti işlevselliği tüm gerekli hello başvuruları ve bağlantı kod tooyour projesi ekler ve yapılandırma dosyalarına uygun şekilde değiştirir. 

Tamamlandıktan sonra hello **bağlı Hizmetleri Ekle** iletişim hello adımları gerekli toostart blob storage'ı, kuyruklar ve tablolar çalışma ayrıntılı belgeler otomatik olarak görüntüler.

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a>TooAzure hello bağlantılı hizmetler kullanarak depolama Bağlan iletişim kutusu
1. Projenizi Visual Studio'da açın

1. İçinde **Çözüm Gezgini**, sağ hello **bağlantılı Hizmetler** düğümü ve hello bağlam menüsünden ve select **bağlı hizmet Ekle**.
   
    ![Azure eklemek bağlı hizmet](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. Merhaba, **bağlantılı Hizmetler** sayfasında, **Azure Storage ile bulut depolama**.
   
    ![Azure depolama ekleme](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. Merhaba, **Azure Storage** iletişim kutusu, varolan bir depolama hesabı seçin ve Seç **Ekle**.
   
    Bir depolama hesabı toocreate gerekiyorsa, toohello sonraki adıma gidin. Aksi halde toostep 6 geçin.
    
    ![Var olan depolama hesabı tooproject Ekle](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. toocreate bir depolama hesabı: 
   
   1. Seçin **yeni depolama hesabı oluşturma** hello iletişim hello sonundaki.

   1. Merhaba doldurun **depolama hesabı oluştur** iletişim ve select **oluşturma**.
      
       ![Yeni Azure depolama hesabı](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. Ne zaman hello **Azure Storage** iletişim kutusu gösterilir, hello yeni depolama hesabı hello listesinde görünür. Merhaba listede Hello yeni depolama hesabı seçin ve Seç **Ekle**.

1. Merhaba depolama bağlı hizmeti hello altında görünür **hizmeti başvuruları** projenizin düğümü.
   
## <a name="how-your-project-is-modified"></a>Projenizi nasıl değiştirilir
Merhaba iletişim bitirdikten sonra Visual Studio başvuruları ekler ve belirli yapılandırma dosyalarını değiştirir. Merhaba belirli değişiklikleri hello proje türüne bağlıdır: 

- ASP.NET proje - [ne – ASP.NET projeleri](http://go.microsoft.com/fwlink/p/?LinkId=513126)
- ASP.NET Core proje - [ne – ASP.NET 5 projeleri](http://go.microsoft.com/fwlink/p/?LinkId=513124) 
- Bulut hizmeti projesi (web rolleri ve çalışan rolleri) - [ne – bulut hizmeti projeleri](http://go.microsoft.com/fwlink/p/?LinkId=516965)
- Web işi projesinin - [ne oldu - WebJob projeleri](visual-studio/vs-storage-webjobs-what-happened.md)

## <a name="next-steps"></a>Sonraki adımlar
- [MSDN forumu: Azure depolama](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Microsoft Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/)
- [Azure Storage belgeleri](https://docs.microsoft.com/azure/storage/)
