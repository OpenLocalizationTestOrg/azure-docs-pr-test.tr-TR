---
title: "Azure AD v2 Android alma başlatıldı - Kurulumu | Microsoft Docs"
description: "Nasıl bir Android ap erişim belirteci almak ve Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren API'larını çağırma"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: a43d7e30a6f4176afba27f0de2c2c116df741080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="4f07c-103">Projenizin kurulumunu</span><span class="sxs-lookup"><span data-stu-id="4f07c-103">Set up your project</span></span>

> <span data-ttu-id="4f07c-104">Bunun yerine bu örneği ait Android Studio projesi indirmeyi tercih ediyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="4f07c-104">Prefer to download this sample's Android Studio project instead?</span></span> <span data-ttu-id="4f07c-105">[Bir proje indirme](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) ve geçin [yapılandırma adımı](#create-an-application-express) kod örneği çalıştırmadan önce yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="4f07c-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="4f07c-106">Yeni bir proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f07c-106">Create a new project</span></span> 
1.  <span data-ttu-id="4f07c-107">Android Studio'yu açın, gidin:`File` > `New` > `New Project`</span><span class="sxs-lookup"><span data-stu-id="4f07c-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="4f07c-108">Uygulamanızı adlandırın ve'ı tıklatın`Next`</span><span class="sxs-lookup"><span data-stu-id="4f07c-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="4f07c-109">Seçtiğinizden emin olun *API 21 ya da daha yeni (Android 5.0)* ve'ı tıklatın`Next`</span><span class="sxs-lookup"><span data-stu-id="4f07c-109">Make sure to select *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="4f07c-110">Bırakın `Empty Activity`, tıklatın `Next`, ardından`Finish`</span><span class="sxs-lookup"><span data-stu-id="4f07c-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a><span data-ttu-id="4f07c-111">Microsoft kimlik doğrulama kitaplığı (MSAL) projenize ekleyin</span><span class="sxs-lookup"><span data-stu-id="4f07c-111">Add the Microsoft Authentication Library (MSAL) to your project</span></span>
1.  <span data-ttu-id="4f07c-112">Android Studio'da gidin:`Gradle Scripts` > `build.gradle (Module: app)`</span><span class="sxs-lookup"><span data-stu-id="4f07c-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="4f07c-113">Altında aşağıdaki kodu kopyalayıp yapıştırın `Dependencies`:</span><span class="sxs-lookup"><span data-stu-id="4f07c-113">Copy and paste the following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="4f07c-114">Bu paketi hakkında</span><span class="sxs-lookup"><span data-stu-id="4f07c-114">About this package</span></span>

<span data-ttu-id="4f07c-115">Yukarıdaki paket Microsoft kimlik doğrulama kitaplığı (MSAL) yükler.</span><span class="sxs-lookup"><span data-stu-id="4f07c-115">The package above installs the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="4f07c-116">MSAL alınırken, önbelleğe alma ve Azure Active Directory v2 bitiş noktası tarafından korunan API'leri erişmek için kullanılan kullanıcı belirteçleri yenilemeyi işler.</span><span class="sxs-lookup"><span data-stu-id="4f07c-116">MSAL handles acquiring, caching and refreshing user tokens used to access APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="4f07c-117">Uygulamanızın kullanıcı Arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f07c-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="4f07c-118">Açık: `activity_main.xml` altında`res` > `layout`</span><span class="sxs-lookup"><span data-stu-id="4f07c-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="4f07c-119">Etkinlik düzeninden değiştirmek `android.support.constraint.ConstraintLayout` veya için diğer`LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="4f07c-119">Change the activity layout from `android.support.constraint.ConstraintLayout` or other to `LinearLayout`</span></span>
3.  <span data-ttu-id="4f07c-120">Ekleme `android:orientation="vertical"` özelliğine `LinearLayout` düğümü</span><span class="sxs-lookup"><span data-stu-id="4f07c-120">Add `android:orientation="vertical"` property to `LinearLayout` node</span></span>
4.  <span data-ttu-id="4f07c-121">Aşağıdaki kodu kopyalayıp `LinearLayout` düğüm, geçerli içerik değiştirme:</span><span class="sxs-lookup"><span data-stu-id="4f07c-121">Copy and paste the following code into the `LinearLayout` node, replacing the current content:</span></span>

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

