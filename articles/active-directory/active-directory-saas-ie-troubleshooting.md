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
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="f1aa3-103">Merhaba erişim paneli uzantısı Internet Explorer için sorun giderme</span><span class="sxs-lookup"><span data-stu-id="f1aa3-103">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="f1aa3-104">Bu makale hello aşağıdaki sorunları gidermenize yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="f1aa3-104">This article helps you troubleshoot hello following problems:</span></span>

* <span data-ttu-id="f1aa3-105">Internet Explorer kullanırken uygulamalarınızı hello My uygulamaları portal üzerinden oluşturulamıyor tooaccess demektir.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-105">You're unable tooaccess your apps through hello My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="f1aa3-106">Hello hello yazılımını zaten yüklemiş olsa bile "Yazılımı yükle" iletisini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-106">You see hello "Install Software" message even though you've already installed hello software.</span></span>

<span data-ttu-id="f1aa3-107">Bir yönetici, ayrıca bkz: [nasıl tooDeploy hello erişim paneli uzantısı Grup İlkesi'ni kullanarak Internet Explorer için](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="f1aa3-107">If you are an admin, see also: [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-hello-diagnostic-tool"></a><span data-ttu-id="f1aa3-108">Merhaba tanı aracı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="f1aa3-108">Run hello Diagnostic Tool</span></span>
<span data-ttu-id="f1aa3-109">Yükleme ve hello erişim paneli tanı aracı çalıştırma hello erişim paneli uzantısı ile yükleme sorunlarını tanılamanıza:</span><span class="sxs-lookup"><span data-stu-id="f1aa3-109">You can diagnose installation problems with hello Access Panel Extension by downloading and running hello Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="f1aa3-110">Burada toodownload hello tanı aracı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-110">Click here toodownload hello diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="f1aa3-111">Açık hello dosya ve tuşuna **tümünü Ayıkla** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-111">Open hello file, and press **Extract all** button.</span></span>
   
    ![Tuşuna tümünü Ayıkla](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="f1aa3-113">Merhaba tuşuna **ayıklamak** düğmesini toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-113">Then press hello **Extract** button toocontinue.</span></span>
   
    ![Extract tuşuna basın](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="f1aa3-115">toorun hello aracı adlı sağ hello dosya **AccessPanelExtensionDiagnosticTool**seçeneğini belirleyip **birlikte Aç > Microsoft Windows tabanlı komut dosyası ana bilgisayarı**.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-115">toorun hello tool, right-click hello file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Birlikte Aç > Microsoft Windows tabanlı komut dosyası ana bilgisayarı](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="f1aa3-117">Sonra ne yüklemenizle birlikte sorun olabilir açıklar tanılama penceresinde, aşağıdaki hello görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-117">You will then see hello following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Merhaba tanılama penceresi örneği](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="f1aa3-119">Tıklayın "**Evet**" bulundu toolet hello program düzeltme hello sorunları.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-119">Click "**YES**" toolet hello program fix hello issues that have been found.</span></span>
7. <span data-ttu-id="f1aa3-120">Bu değişiklikler, toosave her Internet Explorer penceresini kapatın ve Internet Explorer'ı yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-120">toosave these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="f1aa3-121">Uygulamalarınızı hala erişemiyorsanız hello adımları deneyin.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-121">If you still can't access your apps, try hello steps below.</span></span>

## <a name="check-that-hello-access-panel-extension-is-enabled"></a><span data-ttu-id="f1aa3-122">Erişim paneli uzantısı etkin bu hello denetleyin</span><span class="sxs-lookup"><span data-stu-id="f1aa3-122">Check that hello Access Panel Extension is enabled</span></span>
<span data-ttu-id="f1aa3-123">Erişim paneli uzantısı hello tooverify Internet Explorer'da etkinleştirilir:</span><span class="sxs-lookup"><span data-stu-id="f1aa3-123">tooverify that hello Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="f1aa3-124">Internet Explorer'da hello tıklatın **dişli simgesi** hello ekranın sağ üst köşesinde hello penceresi.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-124">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="f1aa3-125">Ardından **Internet Seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="f1aa3-126">(Internet Explorer'ın daha eski sürümlerinde bu altında bulabilirsiniz **Araçlar > Internet Seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![TooTools Git > Internet Seçenekleri](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="f1aa3-128">Merhaba tıklatın **programları** sekmesini ve ardından hello **eklentileri yönetme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-128">Click hello **Programs** tab, then click hello **Manage add-ons** button.</span></span>
   
    ![Eklentileri Yönet'e tıklayın](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="f1aa3-130">Bu iletişim kutusunda seçin **erişim paneli uzantısı** ve hello ardından **etkinleştirmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-130">In this dialog, select **Access Panel Extension** and then click hello **Enable** button.</span></span>
   
    ![Etkinleştir'i tıklatın](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="f1aa3-132">Bu değişiklikler, toosave her Internet Explorer penceresini kapatın ve Internet Explorer'ı yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-132">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="f1aa3-133">InPrivate Gözatma için uzantılarını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f1aa3-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="f1aa3-134">Merhaba InPrivate Gözatma modu kullanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="f1aa3-134">If you are using hello InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="f1aa3-135">Internet Explorer'da hello tıklatın **dişli simgesi** hello ekranın sağ üst köşesinde hello penceresi.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-135">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="f1aa3-136">Ardından **Internet Seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="f1aa3-137">(Internet Explorer'ın daha eski sürümlerinde bu altında bulabilirsiniz **Araçlar > Internet Seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Merhaba tanılama penceresi örneği](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="f1aa3-139">Toohello Git **gizlilik** sekmesinde, ardından **işaretini** etiketli onay kutusunu hello **devre dışı araç çubukları ve uzantıları InPrivate Gözatma başladığında**</span><span class="sxs-lookup"><span data-stu-id="f1aa3-139">Go toohello **Privacy** tab, then **uncheck** hello checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![InPrivate Gözatma başladığında devre dışı bırak araç çubukları ve uzantıları seçeneğinin işaretini kaldırın](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="f1aa3-141">Bu değişiklikler, toosave her Internet Explorer penceresini kapatın ve Internet Explorer'ı yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-141">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-hello-access-panel-extension"></a><span data-ttu-id="f1aa3-142">Merhaba erişim paneli uzantısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="f1aa3-142">Uninstall hello Access Panel Extension</span></span>
<span data-ttu-id="f1aa3-143">toouninstall hello bilgisayarınızdan erişim paneli uzantısı:</span><span class="sxs-lookup"><span data-stu-id="f1aa3-143">toouninstall hello Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="f1aa3-144">Merhaba, klavyede basın **Windows tuşu** tooopen hello Başlat menüsü.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-144">On your keyboard, press hello **Windows key** tooopen hello Start menu.</span></span> <span data-ttu-id="f1aa3-145">Merhaba menü açık olduğunda, herhangi bir şey yazabilirsiniz toodo arama.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-145">When hello menu is open, you can type anything toodo a search.</span></span> <span data-ttu-id="f1aa3-146">"Denetim Masası" yazın ve ardından hello açın **Denetim Masası** hello arama sonuçlarında görüntülendiğinde.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-146">Type "Control Panel" and then open hello **Control Panel** when it appears in hello search results.</span></span>
   
    ![Denetim Masası arayın](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="f1aa3-148">Merhaba sağ üst köşesinde hello Denetim Masası ', hello değiştirme **görüntülemek** çok seçenek**büyük simgeler**.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-148">In hello top right corner of hello Control Panel, change hello **View by** option too**Large icons**.</span></span> <span data-ttu-id="f1aa3-149">Ardından bulun ve hello tıklatın **programlar ve Özellikler** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-149">Then find and click hello **Programs and Features** button.</span></span>
   
    ![İzleme hello görünüm tooshow büyük simgeler](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="f1aa3-151">Hello listesinden **erişim paneli uzantısı**ve hello tıklatın hello **kaldırma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-151">From hello list, select **Access Panel Extension**, and hello click hello **Uninstall** button.</span></span>
   
    ![Kaldır'ı tıklatın](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="f1aa3-153">Ardından tooinstall hello uzantısı deneyebilirsiniz yeniden hello sorunu Çözümlendi, toosee.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-153">You can then try tooinstall hello extension again toosee if hello problem has been resolved.</span></span>

<span data-ttu-id="f1aa3-154">Merhaba uzantısını kaldırma sorunlarla karşılaşırsanız, ayrıca hello kullanarak kaldırabilirsiniz [Microsoft düzeltme IT](https://go.microsoft.com/?linkid=9779673) aracı.</span><span class="sxs-lookup"><span data-stu-id="f1aa3-154">If you encounter issues uninstalling hello extension, you can also remove it using hello [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="f1aa3-155">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="f1aa3-155">Related Articles</span></span>
* [<span data-ttu-id="f1aa3-156">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="f1aa3-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="f1aa3-157">Uygulama erişimi ve Azure Active Directory ile çoklu oturum açma</span><span class="sxs-lookup"><span data-stu-id="f1aa3-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="f1aa3-158">Nasıl tooDeploy hello erişim paneli uzantısı Grup İlkesi'ni kullanarak Internet Explorer için</span><span class="sxs-lookup"><span data-stu-id="f1aa3-158">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

