---
title: Azure Analysis Services aaaManage | Microsoft Docs
description: "Toomanage Analiz Hizmetleri nasıl öğrenin Azure sunucusu."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a>Çözümleme Hizmetleri yönetme
Azure'da bir Analysis Services sunucusuna oluşturduktan sonra bazı yönetim görevleri tooperform hemen gerekir ya da süre aşağı hello yol olabilir. Örneğin, toohello yenileme verileri, sunucunuzdaki hello modelleri erişebilir veya sunucunuzun sistem durumu izleme kimin işlemeyi çalıştırın. Bazı yönetim görevleri, Azure portalında, diğerleri de SQL Server Management Studio (SSMS), yalnızca gerçekleştirilebilir ve bazı görevler ya da gerçekleştirilebilir.

## <a name="azure-portal"></a>Azure portalına
[Azure portal](http://portal.azure.com/) , oluşturmak ve sunucuları silin, sunucu kaynaklarını izlemek, boyutunu değiştirmek ve erişim tooyour sunucuları olanların yönetmek yerdir.  Bazı sorunlar yaşıyorsanız, ayrıca bir destek isteği gönderebilirsiniz.

![Azure'da sunucu adını alma](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a>SQL Server Management Studio
Azure'da tooyour sunucusuyla bağlantı kuruluyor yalnızca tooa server örneği veya kendi kuruluşunuzdaki bağlanma gibi olur. SSMS aynı işlem verileri gibi görevleri veya bir işleme betiği oluşturmak, rolleri yönetmek ve PowerShell kullanmak hello çoğunu gerçekleştirebilirsiniz.
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a>SSMS yükleyip
tooget tüm son özellikleri ve hello en yumuşak deneyimi tooyour Azure Analysis Services sunucusuna bağlanırken Merhaba, hello SSMS en son sürümünü kullandığınızdan emin olun. 

[SQL Server Management Studio'yu indirme](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


### <a name="tooconnect-with-ssms"></a>SSMS ile tooconnect
 SSMS, bağlanan tooyour sunucu hello ilk kez önce kullanırken, kullanıcı adınızı hello Analysis Services Yöneticiler grubunda bulunduğundan emin olun. toolearn daha, fazla [sunucu yöneticileri](#server-administrators) bu makalenin ilerisinde yer.

1. Bağlanmadan önce tooget hello sunucu adı gerekiyor. İçinde **Azure portal** > server > **genel bakış** > **sunucu adı**, kopya hello sunucu adı.
   
    ![Azure'da sunucu adını alma](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. SSMS içinde > **Object Explorer**, tıklatın **Bağlan** > **Analysis Services**.
3. Merhaba, **tooServer bağlanmak** iletişim kutusu, Yapıştır hello sunucu adını, sonra da **kimlik doğrulaması**, şu kimlik doğrulama türlerini hello birini seçin:
   
    **Windows kimlik doğrulaması** toouse Windows etki alanı\kullanıcı adı ve parola bilgileriniz.

    **Active Directory parola kimlik doğrulaması** toouse bir kurumsal hesap. Örneğin, ne zaman bir etki bağlanma bilgisayar katıldı.

    **Active Directory Evrensel kimlik doğrulaması** toouse [etkileşimli olmayan veya çok faktörlü kimlik doğrulaması](../sql-database/sql-database-ssms-mfa-authentication.md). 
   
    ![SSMS bağlanma](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a>Sunucu yöneticileri ve veritabanı kullanıcısı
Azure Analysis Services içinde kullanıcılar, Yöneticiler ve veritabanı kullanıcılarını iki tür vardır. Her iki tür kullanıcı Azure Active Directory'yi olmalıdır ve kurumsal e-posta adresi veya UPN ile belirtilmelidir. toolearn daha, fazla [kimlik doğrulaması ve kullanıcı izinleri](analysis-services-manage-users.md).


## <a name="troubleshooting-connection-problems"></a>Bağlantı sorunlarını giderme
Sorunlarla karşılaşırsanız, SSMS, kullanarak bağlanırken, tooclear hello oturum açma önbellek gerekebilir. Önbelleğe alınan toodisc doğrudur. tooclear hello önbellek, kapatın ve yeniden başlatma hello işlem bağlayın. 

## <a name="next-steps"></a>Sonraki adımlar
Tablo modeli tooyour yeni bir sunucu zaten dağıttıysanız yapmadıysanız, iyi bir zamandır sunulmuştur. toolearn daha, fazla [tooAzure Analysis Services dağıtma](analysis-services-deploy.md).

Bir model tooyour sunucusu dağıttıktan sonra bir istemci veya tarayıcı kullanarak hazır tooconnect tooit demektir. toolearn daha, fazla [veri Azure Analysis Services sunucusundan alma](analysis-services-connect.md).

