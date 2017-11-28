---
title: "Azure AD Connect eşitleme: işletimsel görevleri ve ilgili önemli noktalar | Microsoft Docs"
description: "Bu konu, Azure AD Connect eşitleme için işletimsel görevleri açıklar ve nasıl bu bileşen işletim tooprepare."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="8e723-103">Azure AD Connect eşitleme: işletimsel görevleri ve değerlendirme</span><span class="sxs-lookup"><span data-stu-id="8e723-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="8e723-104">Bu konuda Hello amacı toodescribe işletimsel görevler için Azure AD Connect Eşitleme ' dir.</span><span class="sxs-lookup"><span data-stu-id="8e723-104">hello objective of this topic is toodescribe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="8e723-105">Hazırlama modu</span><span class="sxs-lookup"><span data-stu-id="8e723-105">Staging mode</span></span>
<span data-ttu-id="8e723-106">Hazırlama modu dahil olmak üzere çeşitli senaryoları için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="8e723-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="8e723-107">Yüksek kullanılabilirlik.</span><span class="sxs-lookup"><span data-stu-id="8e723-107">High availability.</span></span>
* <span data-ttu-id="8e723-108">Test ve yeni yapılandırma değişikliği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8e723-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="8e723-109">Yeni bir sunucu getirir ve hello eski yetkisini alın.</span><span class="sxs-lookup"><span data-stu-id="8e723-109">Introduce a new server and decommission hello old.</span></span>

<span data-ttu-id="8e723-110">Merhaba sunucu etkin hale getirmeden önce hazırlama modunda bir sunucuyla değişiklikleri toohello yapılandırma ve önizleme hello değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e723-110">With a server in staging mode, you can make changes toohello configuration and preview hello changes before you make hello server active.</span></span> <span data-ttu-id="8e723-111">Ayrıca, toorun tam içeri aktarma ve tam eşitleme tooverify sağlar bu yapmadan önce tüm değişiklikleri beklenen üretim ortamınıza değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8e723-111">It also allows you toorun full import and full synchronization tooverify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="8e723-112">Yükleme sırasında hello sunucu toobe seçebilirsiniz **hazırlama modu**.</span><span class="sxs-lookup"><span data-stu-id="8e723-112">During installation, you can select hello server toobe in **staging mode**.</span></span> <span data-ttu-id="8e723-113">Bu eylemin hello sunucu içeri aktarma ve eşitleme için etkin hale getirir, ancak hiçbir dışarı aktarma çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="8e723-113">This action makes hello server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="8e723-114">Bu özellikler yüklemesi sırasında seçilen olsa bile sunucu hazırlama modunda bir parola eşitleme ya da parola geri yazma çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="8e723-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="8e723-115">Hazırlama modunu devre dışı bıraktığınızda, hello server dışarı aktarma başlatır, parola eşitleme sağlar ve parola geri yazma özelliğini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="8e723-115">When you disable staging mode, hello server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="8e723-116">Bir verme hello Eşitleme Hizmeti Yöneticisi'ni kullanarak hala zorlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e723-116">You can still force an export by using hello synchronization service manager.</span></span>

<span data-ttu-id="8e723-117">Sunucu hazırlama modunda bir Active Directory ve Azure AD tooreceive değişikliklerden devam eder.</span><span class="sxs-lookup"><span data-stu-id="8e723-117">A server in staging mode continues tooreceive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="8e723-118">Her zaman bir kopyasını hello en son değişiklikleri ve can çok hızlı gerçekleştirin başka bir sunucunun hello sorumlulukları vardır.</span><span class="sxs-lookup"><span data-stu-id="8e723-118">It always has a copy of hello latest changes and can very fast take over hello responsibilities of another server.</span></span> <span data-ttu-id="8e723-119">Yapılandırma değişiklikleri tooyour birincil sunucusu yapın, sorumluluk toomake hello hazırlama modunda aynı değişiklikleri toohello sunucusu olur.</span><span class="sxs-lookup"><span data-stu-id="8e723-119">If you make configuration changes tooyour primary server, it is your responsibility toomake hello same changes toohello server in staging mode.</span></span>

<span data-ttu-id="8e723-120">Merhaba sunucu kendi SQL veritabanı olduğundan bu, eski eşitleme teknolojilerinin bilgi ile hazırlama modunda hello farklıdır.</span><span class="sxs-lookup"><span data-stu-id="8e723-120">For those of you with knowledge of older sync technologies, hello staging mode is different since hello server has its own SQL database.</span></span> <span data-ttu-id="8e723-121">Bu mimarisi, farklı bir veri merkezinde bulunan modu sunucu toobe hazırlama hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e723-121">This architecture allows hello staging mode server toobe located in a different datacenter.</span></span>

### <a name="verify-hello-configuration-of-a-server"></a><span data-ttu-id="8e723-122">Bir sunucunun Hello yapılandırmasını doğrulama</span><span class="sxs-lookup"><span data-stu-id="8e723-122">Verify hello configuration of a server</span></span>
<span data-ttu-id="8e723-123">tooapply bu yöntem, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8e723-123">tooapply this method, follow these steps:</span></span>

1. [<span data-ttu-id="8e723-124">Hazırlama</span><span class="sxs-lookup"><span data-stu-id="8e723-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="8e723-125">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8e723-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="8e723-126">İçeri aktarma ve eşitleme</span><span class="sxs-lookup"><span data-stu-id="8e723-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="8e723-127">Doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8e723-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="8e723-128">Anahtar active server</span><span class="sxs-lookup"><span data-stu-id="8e723-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="8e723-129">Hazırlama</span><span class="sxs-lookup"><span data-stu-id="8e723-129">Prepare</span></span>
1. <span data-ttu-id="8e723-130">Azure AD Connect'i yüklemek, seçin **hazırlama modu**ve işaretini **Eşitlemeyi Başlat** hello son sayfasında hello Yükleme Sihirbazı'nda.</span><span class="sxs-lookup"><span data-stu-id="8e723-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on hello last page in hello installation wizard.</span></span> <span data-ttu-id="8e723-131">Bu mod toorun hello eşitleme altyapısı el ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e723-131">This mode allows you toorun hello sync engine manually.</span></span>
   <span data-ttu-id="8e723-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="8e723-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="8e723-133">Oturum Kapat/oturum açma ve hello Başlat menüsünü seçin **eşitleme hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="8e723-133">Sign off/sign in and from hello start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="8e723-134">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8e723-134">Configuration</span></span>
<span data-ttu-id="8e723-135">Sunucu hazırlama hello ile özel değişiklikler toohello birincil sunucu ve istediğiniz toocompare hello yapılandırma yaptıysanız, daha sonra kullanmak [Azure AD Connect yapılandırma Belgeleyici'yi](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="8e723-135">If you have made custom changes toohello primary server and want toocompare hello configuration with hello staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="8e723-136">İçeri aktarma ve eşitleme</span><span class="sxs-lookup"><span data-stu-id="8e723-136">Import and Synchronize</span></span>
1. <span data-ttu-id="8e723-137">Seçin **Bağlayıcılar**, ve seçin hello hello türüne sahip ilk bağlayıcı **Active Directory etki alanı Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="8e723-137">Select **Connectors**, and select hello first Connector with hello type **Active Directory Domain Services**.</span></span> <span data-ttu-id="8e723-138">Tıklatın **çalıştırmak**seçin **tam alma**, ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8e723-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="8e723-139">Bu türdeki tüm bağlayıcıları için bu adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="8e723-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="8e723-140">Select hello bağlayıcı türü olan **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="8e723-140">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="8e723-141">Tıklatın **çalıştırmak**seçin **tam alma**, ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8e723-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="8e723-142">Merhaba sekmesini bağlayıcılar hala seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8e723-142">Make sure hello tab Connectors is still selected.</span></span> <span data-ttu-id="8e723-143">Her bağlayıcı türü olan **Active Directory etki alanı Hizmetleri**, tıklatın **çalıştırmak**seçin **Delta eşitlemesi**, ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8e723-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="8e723-144">Select hello bağlayıcı türü olan **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="8e723-144">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="8e723-145">Tıklatın **çalıştırmak**seçin **Delta eşitlemesi**, ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8e723-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="8e723-146">Hazırlanan verme tooAzure AD değiştirir ve AD (Exchange karma dağıtımı kullanıyorsanız) şirket içi yazdınız.</span><span class="sxs-lookup"><span data-stu-id="8e723-146">You have now staged export changes tooAzure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="8e723-147">Merhaba sonraki adımlar gerçekte hello verme toohello dizinleri başlamadan önce toochange hakkında nedir tooinspect izin verin.</span><span class="sxs-lookup"><span data-stu-id="8e723-147">hello next steps allow you tooinspect what is about toochange before you actually start hello export toohello directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="8e723-148">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="8e723-148">Verify</span></span>
1. <span data-ttu-id="8e723-149">Bir komut istemi başlatın ve çok gidin`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="8e723-149">Start a cmd prompt and go too`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="8e723-150">Çalıştır: `csexport "Name of Connector" %temp%\export.xml /f:x` hello bağlayıcı hello adını eşitleme hizmetinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="8e723-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` hello name of hello Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="8e723-151">Bu ad benzer too"contoso.com – AAD için Azure AD var."</span><span class="sxs-lookup"><span data-stu-id="8e723-151">It has a name similar too"contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="8e723-152">Merhaba bölümünden Hello PowerShell Betiği kopyalayın [CSAnalyzer](#appendix-csanalyzer) adlı tooa dosya `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="8e723-152">Copy hello PowerShell script from hello section [CSAnalyzer](#appendix-csanalyzer) tooa file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="8e723-153">Bir PowerShell penceresi açın ve hello PowerShell komut dosyasını oluşturduğunuz toohello klasörü bulun.</span><span class="sxs-lookup"><span data-stu-id="8e723-153">Open a PowerShell window and browse toohello folder where you created hello PowerShell script.</span></span>
5. <span data-ttu-id="8e723-154">Çalıştır: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="8e723-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="8e723-155">Şimdi adlı bir dosyanız varsa **processedusers1.csv** , incelenmesi Microsoft Excel'de.</span><span class="sxs-lookup"><span data-stu-id="8e723-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="8e723-156">Tüm değişiklikleri hazırlanan dışarı toobe tooAzure AD bu dosyada bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8e723-156">All changes staged toobe exported tooAzure AD are found in this file.</span></span>
7. <span data-ttu-id="8e723-157">Gerekli değişiklikleri toohello veriler veya yapılandırma olun ve dışarı toobe hakkında değişikliklerini beklenen hello kadar bu adımları tekrar (içeri aktarma ve eşitleme ve doğrula) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8e723-157">Make necessary changes toohello data or configuration and run these steps again (Import and Synchronize and Verify) until hello changes that are about toobe exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="8e723-158">Anahtar active server</span><span class="sxs-lookup"><span data-stu-id="8e723-158">Switch active server</span></span>
1. <span data-ttu-id="8e723-159">Merhaba şu anda etkin sunucuda tooAzure AD verme olmayan şekilde hello sunucu (FIM/DirSync/Azure AD eşitleme) devre dışı etkinleştirmek ya da hazırlama modu (Azure AD Connect) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8e723-159">On hello currently active server, either turn off hello server (DirSync/FIM/Azure AD Sync) so it is not exporting tooAzure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="8e723-160">Merhaba sunucusunda Hello Yükleme Sihirbazı'nı çalıştırdığınız **hazırlama modu** ve devre dışı bırakma **hazırlama modu**.</span><span class="sxs-lookup"><span data-stu-id="8e723-160">Run hello installation wizard on hello server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="8e723-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="8e723-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="8e723-162">Olağanüstü durum kurtarma</span><span class="sxs-lookup"><span data-stu-id="8e723-162">Disaster recovery</span></span>
<span data-ttu-id="8e723-163">Durumunda bir olağanüstü durum hello eşitleme sunucusu kaybetmek burada hello uygulama tasarım hangi toodo tooplan parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="8e723-163">Part of hello implementation design is tooplan for what toodo in case there is a disaster where you lose hello sync server.</span></span> <span data-ttu-id="8e723-164">Farklı modelleri toouse ve hangi bir toouse dahil olmak üzere birkaç unsur vardır:</span><span class="sxs-lookup"><span data-stu-id="8e723-164">There are different models toouse and which one toouse depends on several factors including:</span></span>

* <span data-ttu-id="8e723-165">Mümkün yapma olmaması tooobjects hello kapalı kalma süresi sırasında Azure AD değişiklikleri için tolerans aralığınız nedir?</span><span class="sxs-lookup"><span data-stu-id="8e723-165">What is your tolerance for not being able make changes tooobjects in Azure AD during hello downtime?</span></span>
* <span data-ttu-id="8e723-166">Parola Eşitleme kullanırsanız, hello kullanıcılar durumda bunlar şirket içi değişiklik toouse hello eski parola Azure AD'de sahip oldukları kabul ediyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="8e723-166">If you use password synchronization, do hello users accept that they have toouse hello old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="8e723-167">Parola geri yazma gibi gerçek zamanlı işlemler üzerinde bir bağımlılık var mı?</span><span class="sxs-lookup"><span data-stu-id="8e723-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="8e723-168">Merhaba yanıtlar toothese sorular ve kuruluşunuzun ilkesini bağlı olarak, stratejileri aşağıdaki hello birini uygulanabilir:</span><span class="sxs-lookup"><span data-stu-id="8e723-168">Depending on hello answers toothese questions and your organization’s policy, one of hello following strategies can be implemented:</span></span>

* <span data-ttu-id="8e723-169">Gerektiğinde yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8e723-169">Rebuild when needed.</span></span>
* <span data-ttu-id="8e723-170">Bilinen bir yedek bir bekleme sunucusunun **hazırlama modu**.</span><span class="sxs-lookup"><span data-stu-id="8e723-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="8e723-171">Sanal makineler kullanır.</span><span class="sxs-lookup"><span data-stu-id="8e723-171">Use virtual machines.</span></span>

<span data-ttu-id="8e723-172">Merhaba yerleşik SQL Express veritabanı kullanmayın sonra hello da gözden geçirmelisiniz [SQL yüksek kullanılabilirlik](#sql-high-availability) bölümü.</span><span class="sxs-lookup"><span data-stu-id="8e723-172">If you do not use hello built-in SQL Express database, then you should also review hello [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="8e723-173">Gerektiğinde yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="8e723-173">Rebuild when needed</span></span>
<span data-ttu-id="8e723-174">Gerektiğinde bir sunucusu yeniden oluşturma için tooplan bir uygulanabilir stratejidir.</span><span class="sxs-lookup"><span data-stu-id="8e723-174">A viable strategy is tooplan for a server rebuild when needed.</span></span> <span data-ttu-id="8e723-175">Genellikle, yükleme ve eşitleme altyapısı hello ilk alma hello ve eşitleme birkaç saat içinde tamamlanabilir.</span><span class="sxs-lookup"><span data-stu-id="8e723-175">Usually, installing hello sync engine and do hello initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="8e723-176">Kullanılabilir bir yedek sunucu değilse, olası tootemporarily bir etki alanı denetleyicisi toohost hello eşitleme altyapısı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8e723-176">If there isn’t a spare server available, it is possible tootemporarily use a domain controller toohost hello sync engine.</span></span>

<span data-ttu-id="8e723-177">Active Directory ve Azure AD hello verilerden Hello veritabanı yeniden şekilde hello eşitleme altyapısı sunucusu hello nesneler hakkında herhangi bir durum depolamaz.</span><span class="sxs-lookup"><span data-stu-id="8e723-177">hello sync engine server does not store any state about hello objects so hello database can be rebuilt from hello data in Active Directory and Azure AD.</span></span> <span data-ttu-id="8e723-178">Merhaba **sourceAnchor** özniteliktir kullanılan toojoin hello nesneleri şirket içi ve bulut hello.</span><span class="sxs-lookup"><span data-stu-id="8e723-178">hello **sourceAnchor** attribute is used toojoin hello objects from on-premises and hello cloud.</span></span> <span data-ttu-id="8e723-179">Yeniden oluşturursanız şirket içi hello server varolan nesnelerle ve hello bulut sonra hello altyapısı eşleşmeleri bu nesneleri yeniden yeniden üzerinde birlikte eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="8e723-179">If you rebuild hello server with existing objects on-premises and hello cloud, then hello sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="8e723-180">Kaydet ve toodocument gerekir hello filtreleme ve eşitleme kuralları gibi toohello sunucusu hello yapılandırma değişikliklerini noktalardır.</span><span class="sxs-lookup"><span data-stu-id="8e723-180">hello things you need toodocument and save are hello configuration changes made toohello server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="8e723-181">Eşitlemeye başlamadan önce bu özel yapılandırmalar yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e723-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="8e723-182">Hazırlama modu yedek bir bekleme sunucusunun-</span><span class="sxs-lookup"><span data-stu-id="8e723-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="8e723-183">Daha karmaşık bir ortamınız varsa, bir veya daha fazla yedek sunucular olması önerilir.</span><span class="sxs-lookup"><span data-stu-id="8e723-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="8e723-184">Yükleme sırasında bir sunucu toobe etkinleştirebilirsiniz **hazırlama modu**.</span><span class="sxs-lookup"><span data-stu-id="8e723-184">During installation, you can enable a server toobe in **staging mode**.</span></span>

<span data-ttu-id="8e723-185">Daha fazla bilgi için bkz: [hazırlama modu](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="8e723-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="8e723-186">Sanal makineler kullanın</span><span class="sxs-lookup"><span data-stu-id="8e723-186">Use virtual machines</span></span>
<span data-ttu-id="8e723-187">Bir ortak ve desteklenen bir sanal makinede toorun hello eşitleme altyapısı yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="8e723-187">A common and supported method is toorun hello sync engine in a virtual machine.</span></span> <span data-ttu-id="8e723-188">Merhaba konak bir sorun var. durumda hello eşitleme altyapısı sunucusu hello görüntüsüyle geçirilen tooanother sunucusu olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e723-188">In case hello host has an issue, hello image with hello sync engine server can be migrated tooanother server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="8e723-189">SQL yüksek kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="8e723-189">SQL High Availability</span></span>
<span data-ttu-id="8e723-190">Hello Azure AD Connect ile birlikte gelen SQL Server Express'in kullanmıyorsanız, sonra SQL Server için yüksek kullanılabilirlik da dikkate alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8e723-190">If you are not using hello SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="8e723-191">desteklenen hello yüksek oranda kullanılabilirlik çözümleri SQL Kümeleme ve AOA (Always On kullanılabilirlik grupları) içerir.</span><span class="sxs-lookup"><span data-stu-id="8e723-191">hello high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="8e723-192">Yansıtma desteklenmeyen çözümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="8e723-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="8e723-193">SQL AOA için destek tooAzure AD eklendi sürümünde 1.1.524.0 Bağlan.</span><span class="sxs-lookup"><span data-stu-id="8e723-193">Support for SQL AOA was added tooAzure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="8e723-194">Azure AD Connect yüklemeden önce SQL AOA etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e723-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="8e723-195">Yükleme sırasında Azure AD Connect veya sağlanan hello SQL örneği için SQL AOA etkin olup olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="8e723-195">During installation, Azure AD Connect detects whether hello SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="8e723-196">SQL AOA etkinleştirilirse, daha fazla Azure AD Connect SQL AOA yapılandırılmış toouse zaman uyumlu veya zaman uyumsuz çoğaltma olup olmadığını rakamlar.</span><span class="sxs-lookup"><span data-stu-id="8e723-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured toouse synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="8e723-197">Kullanılabilirlik grubu dinleyicisi Hello ayarlarken hello RegisterAllProvidersIP özelliği too0 ayarlamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="8e723-197">When setting up hello Availability Group Listener, it is recommended that you set hello RegisterAllProvidersIP property too0.</span></span> <span data-ttu-id="8e723-198">Azure AD Connect SQL Native Client tooconnect tooSQL şu anda kullandığı ve SQL Native Client hello MultiSubNetFailover özelliğinin kullanımını desteklemez nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="8e723-198">This is because Azure AD Connect currently uses SQL Native Client tooconnect tooSQL and SQL Native Client does not support hello use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="8e723-199">Ek CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="8e723-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="8e723-200">Merhaba bölümüne bakın [doğrulayın](#verify) nasıl toouse bu komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="8e723-200">See hello section [verify](#verify) on how toouse this script.</span></span>

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="8e723-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8e723-201">Next steps</span></span>
<span data-ttu-id="8e723-202">**Genel bakış konuları**</span><span class="sxs-lookup"><span data-stu-id="8e723-202">**Overview topics**</span></span>  

* [<span data-ttu-id="8e723-203">Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="8e723-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="8e723-204">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="8e723-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
