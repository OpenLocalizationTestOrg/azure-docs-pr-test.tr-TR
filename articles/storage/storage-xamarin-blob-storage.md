---
title: "Blob depolama alanından Xamarin aaaHow toouse | Microsoft Docs"
description: "Hello Xamarin için Azure Storage istemci kitaplığı, geliştiricilerin toocreate iOS, Android ve Windows mağazası uygulamaları ile yerel kullanıcı arabirimlerini sağlar. Bu öğreticide gösterilmiştir nasıl toouse Xamarin toocreate Azure Blob Depolama kullanan bir uygulama."
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 751f66d1d2392c8bcf6e5f8d1b185af73582fab3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a><span data-ttu-id="2fe13-104">Nasıl toouse Blob depolama alanından Xamarin</span><span class="sxs-lookup"><span data-stu-id="2fe13-104">How toouse Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="2fe13-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2fe13-105">Overview</span></span>
<span data-ttu-id="2fe13-106">Xamarin etkinleştirir geliştiriciler toouse paylaşılan C# toocreate iOS, Android ve Windows mağazası uygulamaları kendi yerel kullanıcı arabirimleri ile codebase.</span><span class="sxs-lookup"><span data-stu-id="2fe13-106">Xamarin enables developers toouse a shared C# codebase toocreate iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="2fe13-107">Bu öğretici şunların nasıl yapıldığını gösterir toouse Xamarin uygulamasıyla Azure Blob Depolama.</span><span class="sxs-lookup"><span data-stu-id="2fe13-107">This tutorial shows you how toouse Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="2fe13-108">Merhaba kodlara başlamadan önce toolearn Azure Storage hakkında daha fazla bilgi isterseniz bkz [giriş tooMicrosoft Azure Storage](storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2fe13-108">If you'd like toolearn more about Azure Storage, before diving into hello code, see [Introduction tooMicrosoft Azure Storage](storage-introduction.md).</span></span>

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="2fe13-109">Yeni bir Xamarin uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="2fe13-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="2fe13-110">Bu öğreticide, Android, iOS ve Windows hedefleyen bir uygulama oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="2fe13-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="2fe13-111">Bu uygulama yalnızca bir kapsayıcı oluşturun ve bu kapsayıcıya bir blob yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2fe13-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="2fe13-112">Windows, ancak aynı learnings üzerinde macOS Xamarin Studio kullanarak bir uygulama oluştururken uygulanabilir hello Biz Visual Studio kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2fe13-112">We'll be using Visual Studio on Windows, but hello same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="2fe13-113">Bu adımları toocreate uygulamanızı izleyin:</span><span class="sxs-lookup"><span data-stu-id="2fe13-113">Follow these steps toocreate your application:</span></span>

1. <span data-ttu-id="2fe13-114">Henüz yapmadıysanız yükleyip [Visual Studio için Xamarin](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="2fe13-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="2fe13-115">Visual Studio'yu açın ve (yerel taşınabilir) boş bir uygulaması oluşturun: **Dosya > Yeni > Proje > platformlar arası > boş App(Native Portable)**.</span><span class="sxs-lookup"><span data-stu-id="2fe13-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="2fe13-116">Çözümünüzü hello Çözüm Gezgini bölmesinde sağ tıklatıp **çözüm için NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="2fe13-116">Right-click your solution in hello Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="2fe13-117">Arama **WindowsAzure.Storage** ve hello en son kararlı sürümü tooall projeleri çözümünüzde yükler.</span><span class="sxs-lookup"><span data-stu-id="2fe13-117">Search for **WindowsAzure.Storage** and install hello latest stable version tooall projects in your solution.</span></span>
4. <span data-ttu-id="2fe13-118">Derleme ve projenizi çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="2fe13-118">Build and run your project.</span></span>

<span data-ttu-id="2fe13-119">Şimdi tooclick bir sayaç artırılır düğmesinin sağlayan bir uygulama olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2fe13-119">You should now have an application that allows you tooclick a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="2fe13-120">Kapsayıcı oluşturun ve blob karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="2fe13-120">Create container and upload blob</span></span>
<span data-ttu-id="2fe13-121">Sonraki altında `(Portable)` proje, biraz kod çok ekleyeceksiniz`MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="2fe13-121">Next, under your `(Portable)` project, you'll add some code too`MyClass.cs`.</span></span> <span data-ttu-id="2fe13-122">Bu kod, bir kapsayıcı oluşturur ve bu kapsayıcıya bir blob yükler.</span><span class="sxs-lookup"><span data-stu-id="2fe13-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="2fe13-123">`MyClass.cs`Merhaba aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="2fe13-123">`MyClass.cs` should look like hello following:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create hello blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference tooa previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create hello container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference tooa blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create hello "myblob" blob with hello text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

<span data-ttu-id="2fe13-124">Emin tooreplace "your_account_name_here" ve "your_account_key_here" gerçek hesap adı ve hesap anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2fe13-124">Make sure tooreplace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="2fe13-125">İOS, Android ve Windows Phone projeleri tüm, tüm paylaşılan kodunuzu birinde yazabilirsiniz anlamı başvuruları tooyour taşınabilir proje - yerleştirin ve tüm projeleriniz arasında kullanın.</span><span class="sxs-lookup"><span data-stu-id="2fe13-125">Your iOS, Android, and Windows Phone projects all have references tooyour Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="2fe13-126">Kod tooeach proje toostart alma avantajı satırının aşağıdaki hello artık ekleyebilirsiniz:`MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="2fe13-126">You can now add hello following line of code tooeach project toostart taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="2fe13-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="2fe13-127">XamarinApp.Droid > MainActivity.cs</span></span>

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="2fe13-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="2fe13-128">XamarinApp.iOS > ViewController.cs</span></span>

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading hello view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="2fe13-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="2fe13-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// hello Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated toowithin a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about toobe displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used tooconfigure hello page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about toobe displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used tooconfigure hello page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling hello hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using hello NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="2fe13-130">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2fe13-130">Run hello application</span></span>
<span data-ttu-id="2fe13-131">Bu gibi durumlarda, bu uygulama artık bir Android veya Windows Phone öykünücüsü çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fe13-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="2fe13-132">Bu uygulamayı bir iOS öykünücüsünde de çalıştırabilirsiniz, ancak bu bir Mac bilgisayar gerektirir</span><span class="sxs-lookup"><span data-stu-id="2fe13-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="2fe13-133">Nasıl toodo bunu okuyun hello belgelerine ilgili ayrıntılı yönergeler için [Visual Studio tooa Mac bağlanma](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="2fe13-133">For specific instructions on how toodo this, please read hello documentation for [connecting Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="2fe13-134">Uygulamanızı çalıştırdıktan sonra hello kapsayıcı oluşturacak `mycontainer` depolama hesabınızdaki.</span><span class="sxs-lookup"><span data-stu-id="2fe13-134">Once you run your app, it will create hello container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="2fe13-135">Merhaba blob içermelidir `myblob`, hello metin olan `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="2fe13-135">It should contain hello blob, `myblob`, which has hello text, `Hello, world!`.</span></span> <span data-ttu-id="2fe13-136">Bu hello kullanarak doğrulayın [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="2fe13-136">You can verify this by using hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fe13-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2fe13-137">Next steps</span></span>
<span data-ttu-id="2fe13-138">Bu öğreticide, öğrenilen nasıl toocreate Xamarin platformlar arası uygulamada kullanan Azure Storage, Blob depolama alanındaki bir senaryo özel olarak odaklanan.</span><span class="sxs-lookup"><span data-stu-id="2fe13-138">In this tutorial, you learned how toocreate a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="2fe13-139">Ancak, yalnızca Blob Storage ile aynı zamanda tablo, dosya ve kuyruk depolama ile çok daha fazla yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fe13-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="2fe13-140">Daha fazla makaleleri toolearn aşağıdaki hello gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="2fe13-140">Please check out hello following articles toolearn more:</span></span>

* [<span data-ttu-id="2fe13-141">.NET kullanarak Azure Blob Depolama ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2fe13-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="2fe13-142">.NET kullanarak Azure Tablo Depolama ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2fe13-142">Get started with Azure Table storage using .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="2fe13-143">.NET kullanarak Azure Kuyruk Depolama ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2fe13-143">Get started with Azure Queue storage using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="2fe13-144">Windows'da Azure Dosya Depolama ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2fe13-144">Get started with Azure File storage on Windows</span></span>](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

