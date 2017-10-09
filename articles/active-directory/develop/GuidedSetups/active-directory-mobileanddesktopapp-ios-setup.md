---
title: "aaaAzure AD v2 iOS Başlarken - Kurulumu | Microsoft Docs"
description: "İOS (Swift) uygulamaları, Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 62c4ee9a2d4ccaec780bee09fb4bc34cff2eb6df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="54886-103">İOS uygulamanızı kurma</span><span class="sxs-lookup"><span data-stu-id="54886-103">Setting up your iOS application</span></span>

<span data-ttu-id="54886-104">Bu bölümde hakkında adım adım yönergeler sağlar toocreate yeni bir proje toodemonstrate nasıl toointegrate bir iOS uygulaması (Swift) ile *Microsoft ile oturum açma* bir belirteci gerektiren Web API'leri sorgulayabilirsiniz şekilde.</span><span class="sxs-lookup"><span data-stu-id="54886-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="54886-105">Toodownload, bunun yerine bu örnek 's XCode projesi tercih ediyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="54886-105">Prefer toodownload this sample's XCode project instead?</span></span> <span data-ttu-id="54886-106">[Bir proje indirme](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) ve toohello atla [yapılandırma adımı](#create-an-application-express) yürütmeden önce tooconfigure hello kod örneği.</span><span class="sxs-lookup"><span data-stu-id="54886-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


## <a name="install-carthage-toodownload-and-build-msal"></a><span data-ttu-id="54886-107">Carthage toodownload yükle ve MSAL oluştur</span><span class="sxs-lookup"><span data-stu-id="54886-107">Install Carthage toodownload and build MSAL</span></span>
<span data-ttu-id="54886-108">Carthage Paket Yöneticisi MSAL, hello Önizleme dönemi boyunca kullanılan – Microsoft toomake değişiklikleri toohello kitaplığı hello yeteneği korurken XCode ile tümleşir.</span><span class="sxs-lookup"><span data-stu-id="54886-108">Carthage package manager is used during hello preview period of MSAL – it integrates with XCode while maintaining hello ability for Microsoft toomake changes toohello library.</span></span>

- <span data-ttu-id="54886-109">Merhaba Carthage en son sürümünü karşıdan yükleyip [burada](https://github.com/Carthage/Carthage/releases "Carthage indirme URL'si")</span><span class="sxs-lookup"><span data-stu-id="54886-109">Download and install hello latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="54886-110">Uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="54886-110">Creating your application</span></span>

1.  <span data-ttu-id="54886-111">Xcode açın ve seçin`Create a new Xcode project`</span><span class="sxs-lookup"><span data-stu-id="54886-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="54886-112">Seçin `iOS`  >  `Single view Application` tıklatıp *sonraki*</span><span class="sxs-lookup"><span data-stu-id="54886-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="54886-113">Bir ürün adı verin ve tıklatın *sonraki*</span><span class="sxs-lookup"><span data-stu-id="54886-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="54886-114">Bir klasör toocreate tıklayın seçin *oluştur*</span><span class="sxs-lookup"><span data-stu-id="54886-114">Select a folder toocreate your app and click *Create*</span></span>

## <a name="build-hello-msal-framework"></a><span data-ttu-id="54886-115">Merhaba MSAL Framework derleme</span><span class="sxs-lookup"><span data-stu-id="54886-115">Build hello MSAL Framework</span></span>

<span data-ttu-id="54886-116">Toopull aşağıdaki Hello yönergeleri izleyin ve Carthage kullanarak MSAL kitaplık en son sürümünü hello yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="54886-116">Follow hello instructions below toopull and then build hello latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="54886-117">Merhaba bash Terminali açın ve toohello uygulamanızın kök klasörüne gidin</span><span class="sxs-lookup"><span data-stu-id="54886-117">Open hello bash terminal and go toohello App’s root folder</span></span>
2.  <span data-ttu-id="54886-118">Merhaba aşağıdaki kopyalayın ve bir 'Cartfile' dosyası hello bash terminal toocreate yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="54886-118">Copy hello below and paste in hello bash terminal toocreate a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="54886-119">Merhaba aşağıdaki kopyalayıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="54886-119">Copy and paste hello below.</span></span> <span data-ttu-id="54886-120">Bu komut Carthage/kullanıma klasörüne bağımlılıkları getirir, ardından hello MSAL kitaplığı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="54886-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds hello MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="54886-121">Merhaba yukarıdaki kullanılan toodownload ve yapı hello Microsoft kimlik doğrulama kitaplığı (MSAL) işlemidir.</span><span class="sxs-lookup"><span data-stu-id="54886-121">hello process above is used toodownload and build hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="54886-122">MSAL alınırken, önbelleğe alma ve kullanıcı belirteçleri kullanılan tooaccess hello Azure Active Directory v2 tarafından korunan API'leri yenilemeyi işler.</span><span class="sxs-lookup"><span data-stu-id="54886-122">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by hello Azure Active Directory v2.</span></span>

## <a name="add-hello-msal-framework-tooyour-application"></a><span data-ttu-id="54886-123">Merhaba MSAL framework tooyour uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="54886-123">Add hello MSAL framework tooyour application</span></span>
1.  <span data-ttu-id="54886-124">Merhaba, Xcode'da Aç `General` sekmesi</span><span class="sxs-lookup"><span data-stu-id="54886-124">In Xcode, open hello `General` tab</span></span>
2.  <span data-ttu-id="54886-125">Toohello Git `Linked Frameworks and Libraries` ' ye tıklayın`+`</span><span class="sxs-lookup"><span data-stu-id="54886-125">Go toohello `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="54886-126">`Add other…` seçeneğini belirleyin</span><span class="sxs-lookup"><span data-stu-id="54886-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="54886-127">Seçim: `Carthage`  >  `Build`  >  `iOS`  >  `MSAL.framework` tıklatıp *açık*.</span><span class="sxs-lookup"><span data-stu-id="54886-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="54886-128">Görmeniz gerekir `MSAL.framework` toohello listesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="54886-128">You should see `MSAL.framework` added toohello list.</span></span>
5.  <span data-ttu-id="54886-129">Çok Git`Build Phases` sekmesine ve tıklayın `+` simgesini seçin`New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="54886-129">Go too`Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="54886-130">İçeriği toohello aşağıdaki hello eklemek *komut dosyası alanı*:</span><span class="sxs-lookup"><span data-stu-id="54886-130">Add hello following contents toohello *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="54886-131">Çok Hello ekleyin<code>Input Files</code> tıklayarak <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="54886-131">Add hello following too<code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="54886-132">Uygulamanızın kullanıcı Arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="54886-132">Creating your application’s UI</span></span>
<span data-ttu-id="54886-133">Main.storyboard dosya proje şablonu bir parçası olarak otomatik olarak oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="54886-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="54886-134">Toocreate hello uygulama kullanıcı Arabirimi aşağıdaki Hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="54886-134">Follow hello instructions below toocreate hello app UI:</span></span>

1.  <span data-ttu-id="54886-135">Control + tıklatın `Main.storyboard` toobring yukarı hello bağlamsal menü ve ardından:`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="54886-135">Control+click `Main.storyboard` toobring up hello contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="54886-136">Hello yerine `<scenes>` aşağıdaki hello kodu düğümle:</span><span class="sxs-lookup"><span data-stu-id="54886-136">Replace hello `<scenes>` node with hello code below:</span></span>

```xml
 <scenes>
    <scene sceneID="tne-QT-ifu">
        <objects>
            <viewController id="BYZ-38-t0r" customClass="ViewController" customModule="MSALiOS" customModuleProvider="target" sceneMemberID="viewController">
                <layoutGuides>
                    <viewControllerLayoutGuide type="top" id="y3c-jy-aDJ"/>
                    <viewControllerLayoutGuide type="bottom" id="wfy-db-euE"/>
                </layoutGuides>
                <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                    <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                    <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                    <subviews>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Microsoft Authentication Library" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="ifd-fu-zjm">
                            <rect key="frame" x="64" y="28" width="246" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Logging" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="98g-dc-BPL">
                            <rect key="frame" x="16" y="277" width="62" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="2rX-Vv-T1i">
                            <rect key="frame" x="87" y="100" width="200" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Call Microsoft Graph API"/>
                            <connections>
                                <action selector="callGraphButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="Kx0-JL-Bv9"/>
                            </connections>
                        </button>
                        <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" textAlignment="natural" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="qXW-2z-J7K">
                            <rect key="frame" x="16" y="324" width="343" height="291"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <color key="backgroundColor" white="1" alpha="1" colorSpace="calibratedWhite"/>
                            <accessibility key="accessibilityConfiguration">
                                <accessibilityTraits key="traits" updatesFrequently="YES"/>
                            </accessibility>
                            <fontDescription key="fontDescription" type="system" pointSize="14"/>
                            <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                        </textView>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="9u4-b8-vmX">
                            <rect key="frame" x="137" y="138" width="100" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Sign-Out"/>
                            <connections>
                                <action selector="signoutButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="kZT-P8-0Zy"/>
                            </connections>
                        </button>
                    </subviews>
                    <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="custom" customColorSpace="sRGB"/>
                </view>
                <connections>
                    <outlet property="loggingText" destination="qXW-2z-J7K" id="uqO-Yw-AsK"/>
                    <outlet property="signoutButton" destination="9u4-b8-vmX" id="OCh-qk-ldv"/>
                </connections>
            </viewController>
            <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
        </objects>
        <point key="canvasLocation" x="140" y="137.18140929535232"/>
    </scene>
</scenes>
```
