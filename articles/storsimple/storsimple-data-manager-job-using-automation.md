---
title: "aaaUse Azure Otomasyonu tootrigger bir işi | Microsoft Docs"
description: "Bilgi nasıl StorSimple Data Manager işleri (özel olarak incelenmektedir) tetiklemek toouse Azure Otomasyonu"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a>Azure Otomasyonu tootrigger işi (özel olarak incelenmektedir) kullanın

Bu makalede açıklanır nasıl toouse Azure Otomasyonu tootrigger bir StorSimple veri Yöneticisi işi.

## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce şunları yapın:

*   Azure Powershell yüklü. [Azure Powershell indirme](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Yapılandırma ayarları tooinitialize hello veri dönüştürme işi (yönergeleri tooobtain bu ayarları buraya dahil).
*   Bir kaynak grubu içinde karma veri kaynağındaki doğru şekilde yapılandırılmış bir iş tanımı.
*   Karşıdan `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) hello github deposunu dosyasından.
*   Karşıdan `Get-ConfigurationParams.ps1` [betik](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) hello github'da depodan.
*   Karşıdan `Trigger-DataTransformation-Job.ps1` [betik](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) hello github'da depodan.

## <a name="step-by-step"></a>Adım adım

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a>Azure Active Directory izinlerini hello Otomasyon iş toorun hello iş tanımı Al

1. Active Directory için tooretrieve hello yapılandırma parametreleri adımları izleyerek hello:

    1. Windows PowerShell'i yerel makinenizde açın. Emin [Azure PowerShell](https://azure.microsoft.com/downloads/) yüklenir.
    1. Merhaba çalıştırmak `Get-ConfigurationParams.ps1` komut dosyası (yukarıda indirdiğiniz hello klasörü). Merhaba komutu hello PowerShell penceresinde aşağıdaki komutu yazın:

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        Merhaba ActiveDirectoryKey daha sonra kullandığınız paroladır. Tercih ettiğiniz bir parola girin. AppName herhangi bir dize olabilir.

2. Bu komut dosyası hello Otomasyon runbook'u tetiklemek yüklenirken kullanılması gereken değerleri aşağıdaki hello çıkarır. Bu değerleri not edin.

    - İstemci kimliği
    - Kiracı Kimliği
    - Active Directory anahtar (bir Yukarıda girilen hello ile aynı)
    - Abonelik Kimliği

### <a name="set-up-hello-automation-account"></a>Otomasyon hesabı Hello ayarlayın

1. TooAzure üzerinde oturum ve Automation hesabınızı açın.
2. Tıklatın **varlıklar** döşeme tooopen hello varlıkların listesi.
3. Tıklatın **modülleri** döşeme tooopen hello modüller listesi.
4. Tıklatın **+ bir modül Ekle** düğmesi ve hello Ekle modülü dikey başlatıldığında.

    ![Otomasyon hesabı ayarları](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. Merhaba seçtikten sonra `DataTransformationApp.zip` dosya yerel bilgisayarınızdan, tıklatın **Tamam** tooimport hello modülü.

   Azure Otomasyonu modülü tooyour hesabı aldığında hello modülüyle ilgili meta verileri ayıklar. Bu işlem birkaç dakika sürebilir.

   ![Otomasyon hesabı ayarları](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. Bir bildirim bu hello modül dağıtılan ve hello işlemi tamamlandığında, başka bir bildirim.  Merhaba durum ayrıca kontrol edebilirsiniz **modülleri** döşeme.

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a>Merhaba iş tanımı tetikler tooimport hello runbook

1. Hello Azure portal, Automation hesabınızı açın.
2. Tıklatın **Runbook'lar** döşeme tooopen hello listesini.
3. Tıklatın **+ runbook Ekle** ve ardından **mevcut bir runbook'u içeri aktar**.

   ![Mevcut bir runbook'u İçeri Aktar](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. Tıklatın **Runbook dosyası** ve select hello dosya tooimport `Trigger-DataTransformation-Job.ps1`.
5. Tıklatın **oluşturma** tooimport hello runbook. Merhaba yeni runbook hello Otomasyon hesabı için runbook'ların hello listesinde görünür.
7. Tıklatın **tetikleyici DataTransformation iş** runbook ve ardından **Düzenle**.
8. Tıklatın **Yayımla** ve ardından **Evet** onaylamanız istendiğinde.


### <a name="toorun-hello-runbook"></a>toorun hello runbook:
1. Hello Azure portal, Automation hesabınızı açın.
2. Merhaba tıklatın **Runbook'lar** döşeme tooopen hello listesini.
3. Tıklatın **tetikleyici DataTransformation iş**.
4. Tıklatın **Başlat** toostart hello runbook.

   ![Runbook’u başlatma](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. Merhaba, **Başlat runbook** dikey penceresinde tüm hello parametreleri girin. Tıklatın **Tamam** toosubmit hello veri dönüştürme işi.

   ![Runbook’u başlatma](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a>Sonraki adımlar

[StorSimple veri Yöneticisi kullanıcı Arabirimi tootransform verilerinizi kullanma](storsimple-data-manager-ui.md).
