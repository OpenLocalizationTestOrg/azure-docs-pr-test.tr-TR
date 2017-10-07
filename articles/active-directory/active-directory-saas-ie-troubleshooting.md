---
title: "aaaTroubleshooting hello Azure erişim paneli uzantısı IE için | Microsoft Docs"
description: "Toouse Grup nasıl hello My uygulamaları portal için ilke toodeploy hello Internet Explorer eklentisi."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23cbb6117f34759330206de3a26f1397486acedb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a>Merhaba erişim paneli uzantısı Internet Explorer için sorun giderme
Bu makale hello aşağıdaki sorunları gidermenize yardımcı olur:

* Internet Explorer kullanırken uygulamalarınızı hello My uygulamaları portal üzerinden oluşturulamıyor tooaccess demektir.
* Hello hello yazılımını zaten yüklemiş olsa bile "Yazılımı yükle" iletisini görürsünüz.

Bir yönetici, ayrıca bkz: [nasıl tooDeploy hello erişim paneli uzantısı Grup İlkesi'ni kullanarak Internet Explorer için](active-directory-saas-ie-group-policy.md)

## <a name="run-hello-diagnostic-tool"></a>Merhaba tanı aracı çalıştırın
Yükleme ve hello erişim paneli tanı aracı çalıştırma hello erişim paneli uzantısı ile yükleme sorunlarını tanılamanıza:

1. [Burada toodownload hello tanı aracı tıklatın.](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. Açık hello dosya ve tuşuna **tümünü Ayıkla** düğmesi.
   
    ![Tuşuna tümünü Ayıkla](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. Merhaba tuşuna **ayıklamak** düğmesini toocontinue.
   
    ![Extract tuşuna basın](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. toorun hello aracı adlı sağ hello dosya **AccessPanelExtensionDiagnosticTool**seçeneğini belirleyip **birlikte Aç > Microsoft Windows tabanlı komut dosyası ana bilgisayarı**.
   
    ![Birlikte Aç > Microsoft Windows tabanlı komut dosyası ana bilgisayarı](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. Sonra ne yüklemenizle birlikte sorun olabilir açıklar tanılama penceresinde, aşağıdaki hello görürsünüz.
   
    ![Merhaba tanılama penceresi örneği](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. Tıklayın "**Evet**" bulundu toolet hello program düzeltme hello sorunları.
7. Bu değişiklikler, toosave her Internet Explorer penceresini kapatın ve Internet Explorer'ı yeniden açın.<br />Uygulamalarınızı hala erişemiyorsanız hello adımları deneyin.

## <a name="check-that-hello-access-panel-extension-is-enabled"></a>Erişim paneli uzantısı etkin bu hello denetleyin
Erişim paneli uzantısı hello tooverify Internet Explorer'da etkinleştirilir:

1. Internet Explorer'da hello tıklatın **dişli simgesi** hello ekranın sağ üst köşesinde hello penceresi. Ardından **Internet Seçenekleri**.<br />(Internet Explorer'ın daha eski sürümlerinde bu altında bulabilirsiniz **Araçlar > Internet Seçenekleri**.
   
    ![TooTools Git > Internet Seçenekleri](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. Merhaba tıklatın **programları** sekmesini ve ardından hello **eklentileri yönetme** düğmesi.
   
    ![Eklentileri Yönet'e tıklayın](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. Bu iletişim kutusunda seçin **erişim paneli uzantısı** ve hello ardından **etkinleştirmek** düğmesi.
   
    ![Etkinleştir'i tıklatın](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. Bu değişiklikler, toosave her Internet Explorer penceresini kapatın ve Internet Explorer'ı yeniden açın.

## <a name="enable-extensions-for-inprivate-browsing"></a>InPrivate Gözatma için uzantılarını etkinleştirme
Merhaba InPrivate Gözatma modu kullanıyorsanız:

1. Internet Explorer'da hello tıklatın **dişli simgesi** hello ekranın sağ üst köşesinde hello penceresi. Ardından **Internet Seçenekleri**.<br />(Internet Explorer'ın daha eski sürümlerinde bu altında bulabilirsiniz **Araçlar > Internet Seçenekleri**.
   
    ![Merhaba tanılama penceresi örneği](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. Toohello Git **gizlilik** sekmesinde, ardından **işaretini** etiketli onay kutusunu hello **devre dışı araç çubukları ve uzantıları InPrivate Gözatma başladığında**</p>
   
    ![InPrivate Gözatma başladığında devre dışı bırak araç çubukları ve uzantıları seçeneğinin işaretini kaldırın](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. Bu değişiklikler, toosave her Internet Explorer penceresini kapatın ve Internet Explorer'ı yeniden açın.

## <a name="uninstall-hello-access-panel-extension"></a>Merhaba erişim paneli uzantısını kaldırma
toouninstall hello bilgisayarınızdan erişim paneli uzantısı:

1. Merhaba, klavyede basın **Windows tuşu** tooopen hello Başlat menüsü. Merhaba menü açık olduğunda, herhangi bir şey yazabilirsiniz toodo arama. "Denetim Masası" yazın ve ardından hello açın **Denetim Masası** hello arama sonuçlarında görüntülendiğinde.
   
    ![Denetim Masası arayın](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. Merhaba sağ üst köşesinde hello Denetim Masası ', hello değiştirme **görüntülemek** çok seçenek**büyük simgeler**. Ardından bulun ve hello tıklatın **programlar ve Özellikler** düğmesi.
   
    ![İzleme hello görünüm tooshow büyük simgeler](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. Hello listesinden **erişim paneli uzantısı**ve hello tıklatın hello **kaldırma** düğmesi.
   
    ![Kaldır'ı tıklatın](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. Ardından tooinstall hello uzantısı deneyebilirsiniz yeniden hello sorunu Çözümlendi, toosee.

Merhaba uzantısını kaldırma sorunlarla karşılaşırsanız, ayrıca hello kullanarak kaldırabilirsiniz [Microsoft düzeltme IT](https://go.microsoft.com/?linkid=9779673) aracı.

## <a name="related-articles"></a>İlgili makaleler
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Uygulama erişimi ve Azure Active Directory ile çoklu oturum açma](active-directory-appssoaccess-whatis.md)
* [Nasıl tooDeploy hello erişim paneli uzantısı Grup İlkesi'ni kullanarak Internet Explorer için](active-directory-saas-ie-group-policy.md)

