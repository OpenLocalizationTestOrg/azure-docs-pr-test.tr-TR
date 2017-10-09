---
title: "aaaAzure Analysis Services veritabanını yedekleme ve geri yükleme | Microsoft Docs"
description: "Toobackup ve geri yükleme Azure Analiz Hizmetleri nasıl açıklar veritabanı."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a>Yedekleme ve geri yükleme

Azure Analysis Services tablolu model veritabanlarını yedeklemek için çok hello aynı olduğu gibi şirket içi Analysis Services olur. Merhaba birincil yedekleme dosyalarını depoladığınız farktır. Tooa kapsayıcısında yedekleme dosyalarını kaydedilmiş bir [Azure depolama hesabı](../storage/common/storage-create-storage-account.md). Sunucunuz için depolama ayarlarını yapılandırırken oluşturulabilir veya zaten bir depolama hesabı ve kapsayıcı kullanabilirsiniz.

> [!NOTE]
> Bir depolama hesabı oluştururken bir ek hizmet ücretlerin alınmasına neden olabilir. toolearn daha, fazla [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/blobs/).
> 
> 

Yedeklemeler bir abf uzantısıyla kaydedilir. Bellek içi tablolu modeller için model verileri ve meta veriler depolanır. DirectQuery tablolu modeller için yalnızca model meta verilerini depolanır. Yedeklemeleri sıkıştırılmış ve, size hello seçeneklere bağlı olarak şifrelenir. 



## <a name="configure-storage-settings"></a>Depolama ayarlarını yapılandırın
Yedekleme önce tooconfigure depolama ayarlarını sunucunuz için gerekir.


### <a name="tooconfigure-storage-settings"></a>tooconfigure depolama ayarları
1.  Azure portalında > **ayarları**, tıklatın **yedekleme**.

    ![Yedekleme ayarları](./media/analysis-services-backup/aas-backup-backups.png)

2.  Tıklatın **etkin**, ardından **depolama ayarlarını**.

    ![Etkinleştirme](./media/analysis-services-backup/aas-backup-enable.png)

3. Depolama hesabınızı seçin veya yeni bir tane oluşturun.

4. Bir kapsayıcı seçin veya yeni bir tane oluşturun.

    ![Kapsayıcı seçin](./media/analysis-services-backup/aas-backup-container.png)

5. Yedekleme ayarlarınızı kaydedin.

    ![Yedekleme ayarlarını Kaydet](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a>Backup

### <a name="toobackup-by-using-ssms"></a>SSMS kullanarak toobackup

1. SSMS, bir veritabanına sağ tıklayın > **yedekleme**.

2. İçinde **Backup Database** > **yedekleme dosyası**, tıklatın **Gözat**.

3. Merhaba, **Kaydet dosyası olarak** iletişim kutusunda, hello klasör yolunu doğrulayın ve sonra hello yedekleme dosyası için bir ad yazın. 

4. Merhaba, **Backup Database** iletişim, seçenekleri belirleyin.

    **Dosya izin üzerine** -bu seçenek toooverwrite yedekleme dosyaları hello seçin aynı adı. Bu seçenek seçilmezse kaydetmekte olduğunuz hello dosya hello aynı zaten bir dosya olarak aynı ad hello olamaz konumu.

    **Sıkıştırma uygulamak** -bu seçenek toocompress hello yedekleme dosyasını seçin. Sıkıştırılmış yedek dosyaları disk alanından tasarruf, ancak biraz daha yüksek CPU kullanımı gerektirir. 

    **Yedek dosyayı şifrelemek** -bu seçenek tooencrypt hello yedekleme dosyasını seçin. Bu seçenek, bir kullanıcı tarafından sağlanan parola toosecure hello yedekleme dosyası gerektirir. Merhaba parola hello yedekleme verilerini başka bir yöntemle bir geri yükleme işlemi daha okuma önler. Tooencrypt yedeklemeler seçerseniz, hello parola güvenli bir yerde saklayın.

5. Tıklatın **Tamam** toocreate ve hello yedekleme dosyasını kaydedin.


### <a name="powershell"></a>PowerShell
Kullanım [yedekleme ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet'i.

## <a name="restore"></a>Geri Yükleme
Geri yüklerken, yedekleme dosyası, sunucunuz için yapılandırdığınız hello depolama hesabı olması gerekir. Bir şirket içi konumu tooyour depolama hesabından bir yedekleme dosyası toomove gerekiyorsa kullanın [Microsoft Azure Storage Gezgini](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) veya hello [AzCopy](../storage/common/storage-use-azcopy.md) komut satırı yardımcı programı. 



> [!NOTE]
> Bir şirket içi sunucusundan geri yükleme, tüm hello etki alanı kullanıcıları hello modelinin rollerini kaldırın ve bunları eklemeniz gerekir toohello rolleri Azure Active Directory Kullanıcıları olarak yedekleyin.
> 
> 

### <a name="toorestore-by-using-ssms"></a>SSMS kullanarak toorestore

1. SSMS, bir veritabanına sağ tıklayın > **geri**.

2. Merhaba, **Backup Database** iletişim, **yedekleme dosyası**, tıklatın **Gözat**.

3. Merhaba, **veritabanı dosyalarını bulmak** iletişim, select hello dosyasını toorestore.

4. İçinde **veritabanı geri yükleme**seçin hello veritabanı.

5. Seçeneklerini belirtin. Güvenlik seçenekleri yedekleme yapılırken kullanılan hello yedekleme seçenekleri eşleşmesi gerekir.


### <a name="powershell"></a>PowerShell

Kullanım [geri yükleme ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet'i.


## <a name="related-information"></a>İlgili bilgiler

[Azure depolama hesapları](../storage/common/storage-create-storage-account.md)  
[Yüksek düzey kullanılabilirlik](analysis-services-bcdr.md)     
[Azure Analysis Services yönetme](analysis-services-manage.md)
