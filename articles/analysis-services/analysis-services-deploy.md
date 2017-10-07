---
title: SSDT kullanarak aaaDeploy tooAzure Analysis Services | Microsoft Docs
description: "Nasıl toodeploy tablolu model tooan Azure Analysis Services öğrenin SSDT kullanarak sunucu."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a>SSDT’den model dağıtma
Bir sunucu, Azure aboneliğinizde oluşturduktan sonra hazır toodeploy tablolu model veritabanı tooit demektir. SQL Server veri Araçları (SSDT) toobuild kullanabilir ve üzerinde çalıştığınız bir tablo modeli projesi dağıtabilirsiniz. 

## <a name="prerequisites"></a>Ön koşullar
başlatılan tooget, aşağıdakiler gerekir:

* Azure’da **Analysis Services sunucusu**. toolearn daha, fazla [Azure Analysis Services sunucusu oluşturmak](analysis-services-create-server.md).
* **Tablo modeli projesi** SSDT ya da var olan bir tablo modeli hello 1200 veya daha yüksek uyumluluk düzeyinde. Daha önce hiç oluşturmadınız mı? Merhaba deneyin [Adventure Works Internet satış tablo modelleme Öğreticisi](https://msdn.microsoft.com/library/hh231691.aspx).
* **Şirket içi ağ geçidi** -şirket içi kuruluşunuzun ağındaki bir veya daha fazla veri kaynağı varsa tooinstall gereken bir [şirket içi veri ağ geçidi](analysis-services-gateway.md). Merhaba bulutta sunucunuz bağlantısı için tooyour şirket içi veri kaynakları tooprocess ve yenileme veri hello modelinde hello ağ geçidi gereklidir.

> [!TIP]
> Dağıtmadan önce tabloları hello verileri işleyebildiğinden emin olun. SSDT’de **Model** > **İşlem** > **Tümünü İşle**’ye tıklayın. İşleme başarısız olursa dağıtımı başarıyla yapamazsınız.
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a>toodeploy SSDT tablolu bir modelden

1. Dağıtmadan önce tooget hello sunucu adı gerekiyor. İçinde **Azure portal** > server > **genel bakış** > **sunucu adı**, kopya hello sunucu adı.
   
    ![Azure'da sunucu adını alma](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. Ssdt'de > **Çözüm Gezgini**, sağ hello Proje > **özellikleri**. Ardından **dağıtım** > **Server** hello sunucu adı yapıştırın.   
   
    ![Sunucu adını dağıtım sunucusu özelliğine yapıştırma](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. **Çözüm Gezgini**’nde **Özellikler**’e sağ tıklayıp **Dağıt**’a tıklayın. İstendiğinde toosign tooAzure de olabilir.
   
    ![Tooserver dağıtma](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    Dağıtım durumu hem hello çıktı penceresinde ve Dağıt görünür.
   
    ![Dağıtım durumu](./media/analysis-services-deploy/aas-deploy-status.png)

Tüm olan tooit yok!


## <a name="troubleshooting"></a>Sorun giderme
Meta veri dağıtırken dağıtım başarısız olursa SSDT tooyour sunucu bağlanamadığımız için büyük olasılıkla olur. SSMS kullanarak tooyour sunucusuna bağlanabildiğinden emin olun. Ardından hello hello proje için dağıtım sunucusu özelliği doğru olduğundan emin olun.

Bir tablo üzerinde dağıtım başarısız olursa sunucunuz tooa veri kaynağı bağlanamadığımız için büyük olasılıkla olur. Veri kaynağınızı şirket içi kuruluşunuzun ağındaki emin tooinstall olması bir [şirket içi veri ağ geçidi](analysis-services-gateway.md).

## <a name="next-steps"></a>Sonraki adımlar
Tablo modeli dağıtılan tooyour sunucunuz sahip olduğunuza göre hazır tooconnect tooit demektir. Yapabilecekleriniz [tooit SSMS ile bağlanma](analysis-services-manage.md) toomanage onu. Ve yapabilecekleriniz [tooit bir istemci araç kullanarak bağlanmak](analysis-services-connect.md) Power BI, Power BI Desktop veya Excel ve raporları oluşturma başlangıç gibi.

