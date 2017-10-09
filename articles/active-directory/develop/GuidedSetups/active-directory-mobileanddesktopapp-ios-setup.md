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
## <a name="setting-up-your-ios-application"></a>İOS uygulamanızı kurma

Bu bölümde hakkında adım adım yönergeler sağlar toocreate yeni bir proje toodemonstrate nasıl toointegrate bir iOS uygulaması (Swift) ile *Microsoft ile oturum açma* bir belirteci gerektiren Web API'leri sorgulayabilirsiniz şekilde.

> Toodownload, bunun yerine bu örnek 's XCode projesi tercih ediyorsunuz? [Bir proje indirme](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) ve toohello atla [yapılandırma adımı](#create-an-application-express) yürütmeden önce tooconfigure hello kod örneği.


## <a name="install-carthage-toodownload-and-build-msal"></a>Carthage toodownload yükle ve MSAL oluştur
Carthage Paket Yöneticisi MSAL, hello Önizleme dönemi boyunca kullanılan – Microsoft toomake değişiklikleri toohello kitaplığı hello yeteneği korurken XCode ile tümleşir.

- Merhaba Carthage en son sürümünü karşıdan yükleyip [burada](https://github.com/Carthage/Carthage/releases "Carthage indirme URL'si")

## <a name="creating-your-application"></a>Uygulamanızı oluşturma

1.  Xcode açın ve seçin`Create a new Xcode project`
2.  Seçin `iOS`  >  `Single view Application` tıklatıp *sonraki*
3.  Bir ürün adı verin ve tıklatın *sonraki*
4.  Bir klasör toocreate tıklayın seçin *oluştur*

## <a name="build-hello-msal-framework"></a>Merhaba MSAL Framework derleme

Toopull aşağıdaki Hello yönergeleri izleyin ve Carthage kullanarak MSAL kitaplık en son sürümünü hello yapılandırın:

1.  Merhaba bash Terminali açın ve toohello uygulamanızın kök klasörüne gidin
2.  Merhaba aşağıdaki kopyalayın ve bir 'Cartfile' dosyası hello bash terminal toocreate yapıştırın:

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
Merhaba aşağıdaki kopyalayıp yeniden açın. Bu komut Carthage/kullanıma klasörüne bağımlılıkları getirir, ardından hello MSAL kitaplığı oluşturur:
</li>
</ol>

```bash
carthage update
```

> Merhaba yukarıdaki kullanılan toodownload ve yapı hello Microsoft kimlik doğrulama kitaplığı (MSAL) işlemidir. MSAL alınırken, önbelleğe alma ve kullanıcı belirteçleri kullanılan tooaccess hello Azure Active Directory v2 tarafından korunan API'leri yenilemeyi işler.

## <a name="add-hello-msal-framework-tooyour-application"></a>Merhaba MSAL framework tooyour uygulaması ekleyin
1.  Merhaba, Xcode'da Aç `General` sekmesi
2.  Toohello Git `Linked Frameworks and Libraries` ' ye tıklayın`+`
3.  `Add other…` seçeneğini belirleyin
4.  Seçim: `Carthage`  >  `Build`  >  `iOS`  >  `MSAL.framework` tıklatıp *açık*. Görmeniz gerekir `MSAL.framework` toohello listesine eklenir.
5.  Çok Git`Build Phases` sekmesine ve tıklayın `+` simgesini seçin`New Run Script Phase`
6.  İçeriği toohello aşağıdaki hello eklemek *komut dosyası alanı*:

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Çok Hello ekleyin<code>Input Files</code> tıklayarak <code>+</code>:
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a>Uygulamanızın kullanıcı Arabirimi oluşturma
Main.storyboard dosya proje şablonu bir parçası olarak otomatik olarak oluşturulması gerekir. Toocreate hello uygulama kullanıcı Arabirimi aşağıdaki Hello yönergeleri izleyin:

1.  Control + tıklatın `Main.storyboard` toobring yukarı hello bağlamsal menü ve ardından:`Open As` > `Source Code`
2.  Hello yerine `<scenes>` aşağıdaki hello kodu düğümle:

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
