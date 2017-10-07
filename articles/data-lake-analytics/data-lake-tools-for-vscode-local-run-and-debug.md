---
title: "Azure Data Lake araçları: U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama | Microsoft Docs"
description: "Nasıl toouse Azure Data Lake araçları Visual Studio Code toolocal çalıştırma ve yerel için hata ayıklama öğrenin."
Keywords: "VScode, Azure Data Lake araçları, yerel çalıştırma, yerel hata ayıklama, yerel hata ayıklama, Önizleme depolama dosyası toostorage yolu karşıya yükle"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a>U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama

## <a name="prerequisites"></a>Ön koşullar
Merhaba bu yordamlara başlamadan önce aşağıdaki önkoşulların yerinde olduğundan emin olun:
- Visual Studio Code için Azure Data Lake aracı. Yönergeler için bkz: [kullanım Azure Data Lake araçları Visual Studio Code için](data-lake-analytics-data-lake-tools-for-vscode.md).
- C# Visual Studio (tooperform U-SQL yerel hata ayıklama istiyorsanız) kodu.

   ![C# Data Lake araçları Visual Studio için yükleme kodu](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > U-SQL yerel çalıştırma hello ve hata ayıklama özelliklerini şu anda yalnızca Windows kullanıcıları destekler. 


## <a name="set-up-hello-u-sql-local-run-environment"></a>Merhaba U-SQL yerel çalıştırma ortamını ayarlama

1. Ctrl + Shift + P tooopen hello komutu palet seçin ve ardından girin **ADL: LocalRun bağımlılık indirme** toodownload hello paketler.  

   ![Merhaba ADL LocalRun bağımlılık paketlerini yükleyin](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. Merhaba bağımlılık paketlerini hello gösterilen hello yolundan bulun **çıkış** bölmesinde ve sonra BuildTools ve Win10SDK 10240 yükleyin. Bir örnek yolu şöyledir:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  ![Merhaba bağımlılık paketlerini bulun](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)

   a. tooinstall BuildTools, hello sihirbazdaki yönergeleri izleyin.   

  ![BuildTools yükleyin](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   b. tooinstall Win10SDK 10240 hello sihirbazdaki yönergeleri izleyin.  

  ![Win10SDK yükleme 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. Merhaba ortam değişkeni ayarlayın. Set hello **SCOPE_CPP_SDK** ortam değişkenine:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. Merhaba OS toomake hello ortam değişkeni ayarlarının etkili emin yeniden başlatın.  

   ![Merhaba SCOPE_CPP_SDK ortam değişkeni yüklendiğinden emin olun](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a>Merhaba yerel çalıştırma hizmetini başlatın ve hello U-SQL iş tooa yerel hesap gönderme 
Merhaba ilk kez kullanıcı için olduğunuz istendiğinde toodownload hello ADL: LocalRun bağımlılık indirme paketler zaten yüklü değilse.
1. Ctrl + Shift + P tooopen hello komutu palet seçin ve ardından girin **ADL: yerel çalıştırma Hizmeti'ni Başlat**.
2. Seçin **kabul** tooaccept hello hello ilk kez için Microsoft Yazılımı Lisans koşulları. 

   ![Merhaba Microsoft Yazılımı Lisans koşulları kabul edin](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. Başlangıç cmd konsolu açılır. İlk kez kullanıcılar için ihtiyacınız tooenter **3**ve verilerinizi giriş ve çıkış hello yerel klasör yolunu bulun. Diğer seçenekler için hello varsayılan değerleri kullanabilirsiniz. 

   ![Visual Studio Code yerel çalıştırma cmd için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. Ctrl + Shift + P tooopen hello komutu palet seçip girin **ADL: işi Gönder**ve ardından **yerel** toosubmit hello iş tooyour yerel hesap.

   ![Visual Studio Code için Data Lake araçları yerel seçin](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. Merhaba işi gönderdikten sonra hello gönderme ayrıntıları görüntüleyebilirsiniz. tooview hello gönderimi Seç ayrıntıları **jobUrl** hello içinde **çıkış** penceresi. Başlangıç cmd konsolundan hello iş gönderme durumunu da görüntüleyebilirsiniz. Girin **7** tooknow istiyorsanız başlangıç cmd konsolunda daha fazla proje ayrıntıları.

   ![Data Lake araçları için Visual Studio Code yerel çıkış çalıştırma](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake araçları Visual Studio Code yerel cmd durumunu çalıştırmak için](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png) 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a>Yerel bir hata ayıklama hello U-SQL işi Başlat  
Merhaba ilk kez kullanıcı için olduğunuz istendiğinde toodownload hello ADL: LocalRun bağımlılık indirme paketler zaten yüklü değilse.
  
1. Ctrl + Shift + P tooopen hello komutu palet seçin ve ardından girin **ADL: yerel çalıştırma Hizmeti'ni Başlat**. Başlangıç cmd konsolu açılır. Bu hello emin olun **DataRoot** ayarlanır.
3. Bir kesme noktası, C# kod arkasında ayarlayın.
4. Merhaba komut dosyası Düzenleyicisi'nde geri Ctrl + Shift + P tooopen hello komut konsolundan seçin ve ardından girin **yerel hata ayıklama** toostart yerel hata ayıklama hizmetinizi.

![Visual Studio Code yerel hata ayıklama sonuç için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a>Sonraki adımlar
- Azure Data Lake araçları için Visual Studio Code kullanmak için bkz: [kullanım Azure Data Lake araçları Visual Studio Code için](data-lake-analytics-data-lake-tools-for-vscode.md).
- Data Lake Analytics başlatılan bilgi almak için bkz: [Öğreticisi: Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md).
- Visual Studio için Data Lake araçları hakkında bilgi için bkz: [öğretici: Visual Studio için Data Lake araçları kullanarak geliştirme U-SQL betikleri](data-lake-analytics-data-lake-tools-get-started.md).
- Derlemeler geliştirme hello hakkında bilgi için bkz [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md).
