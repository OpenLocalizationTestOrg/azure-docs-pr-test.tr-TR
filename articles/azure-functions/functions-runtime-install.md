---
title: "aaaAzure işlevleri çalışma zamanı yükleme | Microsoft Docs"
description: "Nasıl tooInstall hello Azure işlevleri çalışma zamanı"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a>Hello Azure işlevleri çalışma zamanı Önizleme yükleyin

Tooinstall hello Azure işlevleri çalışma zamanı Önizleme istiyorsanız şu adımları izlemelisiniz:

1. Merhaba en düşük gereksinimler makinenizi geçirir emin olun
1. Merhaba karşıdan [Azure işlevleri çalışma zamanı Önizleme yükleyici](https://aka.ms/azafr). 
1. Hello Azure işlevleri çalışma zamanı preview yükleyin
1. Hello Azure işlevleri çalışma zamanı Önizleme tam hello yapılandırması

## <a name="prerequisites"></a>Ön koşullar

Hello Azure işlevleri çalışma zamanı Önizleme yüklemeden önce hello şunlara sahip olmanız gerekir:

1. Microsoft Windows Server 2016 veya Microsoft Windows 10 oluşturucuları Update (Professional veya Enterprise Edition) çalıştıran bir makineye.
1. Ağınızın içinde çalışan bir SQL Server örneği.  En düşük sürümü SQL Server Express gereksinimdir.

## <a name="install-hello-azure-functions-runtime-preview"></a>Hello Azure işlevleri çalışma zamanı Önizleme yükleyin

Hello Azure işlevleri çalışma zamanı Önizleme yükleyici hello yüklemesi hello Azure işlevleri çalışma zamanı Önizleme yönetimi ve çalışan rolleri sırasında size kılavuzluk eder.  Olası tooinstall hello yönetimi ve hello üzerinde çalışan rolü olan aynı makine.  Ancak, daha fazla işlevler eklemek gibi ek makineleri toobe mümkün tooscale daha fazla çalışan rollerinde işlevlerinizi birden çok Worker üzerine dağıtmanız gerekir.

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a>Merhaba yönetimi ve çalışan rolü üzerinde hello yükleme aynı makine

1. Hello Azure işlevleri çalışma zamanı Önizleme yükleyici çalıştırın.

    ![Azure işlevleri çalışma zamanı Önizleme yükleyici][1]

1. **İleri'yi** öncelikli hello yükleyici ilk aşamasında hello geçmiş
1. Merhaba hello koşullarını okuduğunuzu sonra **EULA**, **hello kutuyu** tooaccept hello hüküm ve **İleri'yi tıklatın** tooadvance.
1. Rolleri seçin hello artık bu makinede tooinstall istediğiniz **işlevleri yönetim rolü** ve/veya **işlevleri çalışan rolü** ve **İleri'yi tıklatın**

    ![Azure işlevleri çalışma zamanı Önizleme yükleyici - rolü seçimi][3]

    > [!NOTE]
    > Merhaba yükleyebilirsiniz **işlevleri çalışan rolü** diğer birçok makineler toodo bu nedenle, bu yönergeleri izleyin ve yalnızca seçin **işlevleri çalışan rolü** hello yükleyicisinde.

1. **İleri'yi** toohave hello **Azure işlevleri çalışma zamanı yükleyicisi** makinenize yükleyin.
1. Tam hello yükleyici hello başlatacak sonra **Azure işlevleri çalışma zamanı yapılandırma aracı**.

    ![Azure işlevleri çalışma zamanı Önizleme yükleyici tamamlandı][5]

    > [!NOTE]
    > Üzerinde yüklüyorsanız **Windows 10** ve hello **kapsayıcı** özelliği daha önce etkinleştirilmemiş, hello **Azure işlevleri çalışma zamanı** yükleyici tooreboot ister Makine toocomplete hello yükleyin.

## <a name="configure-hello-azure-functions-runtime"></a>Hello Azure işlevleri çalışma zamanı yapılandırma

toocomplete hello Azure işlevleri çalışma zamanı yükleme hello yapılandırmasını tamamlamanız gerekir.

1. Merhaba **Azure işlevleri çalışma zamanı yapılandırma aracı** hangi rollerin makinenize yüklü olan gösterir.

    ![Azure işlevleri çalışma zamanı Önizleme yapılandırma aracı][6]

1. Hello tıklatın **veritabanı** sekmesinde, hello girin **bağlantı ayrıntıları, SQL Server örneği için** ve **Uygula'yı**.  Bu sipariş toohello Azure işlevleri çalışma zamanı toocreate veritabanı toosupport hello çalışma zamanı gereklidir.
    
    ![Azure işlevleri çalışma zamanı Önizleme veritabanı yapılandırması][7]

1. Merhaba tıklatın **kimlik bilgileri** sekmesi.  Bu ekranda tüm Azure işlevleri barındırmak için iki yeni kimlik bilgileri kullanmak için bir dosya paylaşımı ile oluşturmanız gerekir.  **Kullanıcı adı ve parola belirtin** hello için KOMBİNASYON **dosya paylaşımı sahibi** ve hello için **dosya paylaşımı kullanıcısı** tıklatıp **Uygula**.

    ![Azure işlevleri çalışma zamanı Önizleme kimlik bilgileri][8]

1. Merhaba tıklatın **dosya paylaşımı** sekmesi.  Bu ekranda hello hello ayrıntılarını belirtmelisiniz **dosya paylaşım konumunu**.  Bu sizin için oluşturulabilir veya var olan bir dosya paylaşımı kullanabilir ve tıklatın **Uygula**.  Yeni bir dosya paylaşımı konumu seçerseniz, hello Azure işlevleri çalışma zamanı tarafından kullanım için bir dizin belirtmeniz gerekir.
    
    ![Azure işlevleri çalışma zamanı Önizleme dosya paylaşımı][9]

1. Merhaba tıklatın **IIS** sekmesi.  Bu sekme, IIS Azure işlevleri çalışma zamanı yükleme oluşturacak bu hello hello Web siteleri hello ayrıntılarını gösterir.  **Uygula'yı** toocomplete.

    ![Azure işlevleri çalışma zamanı Önizleme IIS][10]

1. Merhaba tıklatın **Hizmetleri** sekmesi.  Bu sekme, Azure işlevleri çalışma zamanı yükleme hello hello hizmetlerinin durumunu gösterir.  Eğer ilk yapılandırma hello sonra **Azure işlevleri konak Etkinleştirme hizmeti** tıklatın çalışmıyor **Hizmeti'ni Başlat**

    ![Azure işlevleri çalışma zamanı Önizleme yapılandırma tamamlandı][11]

1. Son olarak toohello Gözat **Azure işlevleri çalışma zamanı Portal** olarak`https://<machinename>/`

    ![Azure işlevleri çalışma zamanı Önizleme portalı][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png