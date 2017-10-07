---
title: "Azure Güvenlik Merkezi'nde doğrulama aaaAlerts | Microsoft Docs"
description: "Bu belge, Azure Güvenlik Merkezi'nde toovalidate hello güvenlik uyarılarını yardımcı olur."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde Uyarıları Doğrulama
Bu belge öğrenmenize yardımcı olur nasıl sisteminiz için Azure Güvenlik Merkezi uyarılarını düzgün şekilde yapılandırılmışsa tooverify.

## <a name="what-are-security-alerts"></a>Güvenlik uyarıları nedir?
Güvenlik Merkezi otomatik olarak toplar, analiz eder ve Azure kaynakları, hello ağ ve güvenlik duvarı ve endpoint protection çözümleri, toodetect ve uyarı, toothreats gibi bağlı iş ortağı çözümlerinden günlük verilerini tümleştirir. Okuma [yönetme ve yanıt toosecurity Azure Güvenlik Merkezi'nde uyarıları](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) güvenlik uyarıları ve okuma hakkında daha fazla bilgi için [Azure Güvenlik Merkezi'nde güvenlik uyarıları anlama](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn daha fazla Merhaba farklı türde bir uyarı hakkında.

## <a name="alert-validation"></a>Uyarı doğrulaması
Güvenlik Merkezi Aracısı, bilgisayarınızda yüklendikten sonra toobe saldırıya hello kaynak hello uyarının istediğiniz hello bilgisayardan hello adımları izleyin:

1. Bir yürütülebilir dosya (için örnek calc.exe) toohello bilgisayarın masaüstünde veya diğer kolaylık dizininin kopyalayın.
2. Bu dosyayı yeniden adlandırmak çok**ASC_AlertTest_662jfi039N.exe**.
3. Merhaba komut istemi açın ve bu dosyayı (yalnızca bir sahte bağımsız değişkeni adı), bağımsız değişkeni gibi yürütün: *ASC_AlertTest_662jfi039N.exe - foo*
4. 5 too10 dakika bekleyin ve Güvenlik Merkezi uyarılarını açın. Var. bir uyarı benzer toofollowing bir bulmanız gerekir:

    ![Uyarı Doğrulaması](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

Bu uyarıyı gözden geçirirken hello alan bağımsız değişkenleri denetiminin etkin olarak doğru göründüğünden emin olun. False gösteriyorsa, Denetim tooenable komut satırı bağımsız değişkenleri gerekir. Komut satırı aşağıdaki hello kullanarak bu seçeneği etkinleştirebilirsiniz:

*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*


## <a name="see-also"></a>Ayrıca bkz.
Bu makalede toohello uyarıları doğrulama işlemini kullanıma sunuldu. Bu doğrulama ile tanıdık, makaleler hello deneyin:

* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts). Bilgi nasıl toomanage uyarıları ve Güvenlik Merkezi'nde yanıt toosecurity olaylar.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md). Nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'ndeki güvenlik uyarılarını anlama](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). Merhaba farklı türlerde güvenlik uyarıları hakkında bilgi edinin.
* [Azure Güvenlik Merkezi Sorun Giderme Kılavuzu](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide). Güvenlik Merkezi'nde nasıl tootroubleshoot ortak sorunlar hakkında bilgi edinin. 
* [Azure Güvenlik Merkezi SSS](security-center-faq.md). Merhaba Hizmeti'ni kullanma hakkında sık sorulan soruları bulabilirsiniz.
* [Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/). Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulun.

