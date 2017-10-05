---
title: "BLOB depolama alanından Xamarin kullanma | Microsoft Docs"
description: "Xamarin için Azure Storage istemci kitaplığı, geliştiricilerin kendi yerel kullanıcı arabirimleri ile iOS, Android ve Windows mağazası uygulamaları oluşturmalarına olanak sağlar. Bu öğretici Xamarin Azure Blob Depolama kullanan bir uygulama oluşturmak için nasıl kullanılacağını gösterir."
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
ms.openlocfilehash: 0952c0e7189dd360098744a7e19b04cd330cb617
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-blob-storage-from-xamarin"></a><span data-ttu-id="47550-104">BLOB depolama alanından Xamarin kullanma</span><span class="sxs-lookup"><span data-stu-id="47550-104">How to use Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="47550-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="47550-105">Overview</span></span>
<span data-ttu-id="47550-106">Yerel kullanıcı arabirimlerini ile iOS, Android ve Windows mağazası uygulamaları oluşturmak için bir paylaşılan C# kullanmaya Xamarin etkinleştirir geliştiriciler codebase.</span><span class="sxs-lookup"><span data-stu-id="47550-106">Xamarin enables developers to use a shared C# codebase to create iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="47550-107">Bu öğretici Xamarin uygulamasıyla Azure Blob storage kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="47550-107">This tutorial shows you how to use Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="47550-108">Bilgi edinmek istiyorsanız, kodlara başlamadan önce Azure Storage hakkında daha fazla bakın [Microsoft Azure Storage'a giriş](storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47550-108">If you'd like to learn more about Azure Storage, before diving into the code, see [Introduction to Microsoft Azure Storage](storage-introduction.md).</span></span>

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="47550-109">Yeni bir Xamarin uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="47550-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="47550-110">Bu öğreticide, Android, iOS ve Windows hedefleyen bir uygulama oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="47550-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="47550-111">Bu uygulama yalnızca bir kapsayıcı oluşturun ve bu kapsayıcıya bir blob yükleyin.</span><span class="sxs-lookup"><span data-stu-id="47550-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="47550-112">Biz Visual Studio Windows kullanmaya, ancak aynı learnings üzerinde macOS Xamarin Studio kullanarak bir uygulama oluştururken uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="47550-112">We'll be using Visual Studio on Windows, but the same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="47550-113">Uygulamanızı oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="47550-113">Follow these steps to create your application:</span></span>

1. <span data-ttu-id="47550-114">Henüz yapmadıysanız yükleyip [Visual Studio için Xamarin](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="47550-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="47550-115">Visual Studio'yu açın ve (yerel taşınabilir) boş bir uygulaması oluşturun: **Dosya > Yeni > Proje > platformlar arası > boş App(Native Portable)**.</span><span class="sxs-lookup"><span data-stu-id="47550-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="47550-116">Çözüm Gezgini bölmesinde Çözümünüze sağ tıklayın ve seçin **çözüm için NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="47550-116">Right-click your solution in the Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="47550-117">Arama **WindowsAzure.Storage** ve çözümünüzdeki tüm projeleri için en son kararlı sürümü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="47550-117">Search for **WindowsAzure.Storage** and install the latest stable version to all projects in your solution.</span></span>
4. <span data-ttu-id="47550-118">Derleme ve projenizi çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="47550-118">Build and run your project.</span></span>

<span data-ttu-id="47550-119">Şimdi bir sayaç artırılır bir düğmeye tıklayın olanak sağlayan bir uygulama olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="47550-119">You should now have an application that allows you to click a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="47550-120">Kapsayıcı oluşturun ve blob karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="47550-120">Create container and upload blob</span></span>
<span data-ttu-id="47550-121">Ardından, altında `(Portable)` projesi için bazı kod ekleyeceğiz `MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="47550-121">Next, under your `(Portable)` project, you'll add some code to `MyClass.cs`.</span></span> <span data-ttu-id="47550-122">Bu kod, bir kapsayıcı oluşturur ve bu kapsayıcıya bir blob yükler.</span><span class="sxs-lookup"><span data-stu-id="47550-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="47550-123">`MyClass.cs`aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="47550-123">`MyClass.cs` should look like the following:</span></span>

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

            // Create the blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference to a previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create the container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference to a blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create the "myblob" blob with the text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

<span data-ttu-id="47550-124">"Your_account_name_here" ve "your_account_key_here" gerçek hesap adı ve hesap anahtarı ile değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="47550-124">Make sure to replace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="47550-125">İOS, Android ve Windows Phone projeleri tüm, tüm paylaşılan kodunuzu birinde yazabilirsiniz anlamına gelir, taşınabilir projenizi - başvuran yerleştirin ve tüm projeleriniz arasında kullanın.</span><span class="sxs-lookup"><span data-stu-id="47550-125">Your iOS, Android, and Windows Phone projects all have references to your Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="47550-126">Aşağıdaki kod satırını faydalanarak başlatmak için her proje için artık ekleyebilirsiniz:`MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="47550-126">You can now add the following line of code to each project to start taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="47550-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="47550-127">XamarinApp.Droid > MainActivity.cs</span></span>

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

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from the layout resource,
            // and attach an event to it
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

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="47550-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="47550-128">XamarinApp.iOS > ViewController.cs</span></span>

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
                // Perform any additional setup after loading the view, typically from a nib.
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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="47550-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="47550-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
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
        /// Invoked when this page is about to be displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used to configure the page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about to be displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used to configure the page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling the hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using the NavigationHelper provided by some templates,
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

## <a name="run-the-application"></a><span data-ttu-id="47550-130">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="47550-130">Run the application</span></span>
<span data-ttu-id="47550-131">Bu gibi durumlarda, bu uygulama artık bir Android veya Windows Phone öykünücüsü çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47550-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="47550-132">Bu uygulamayı bir iOS öykünücüsünde de çalıştırabilirsiniz, ancak bu bir Mac bilgisayar gerektirir</span><span class="sxs-lookup"><span data-stu-id="47550-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="47550-133">Bunu yapmak özel yönergeler Lütfen okumak için belgelerine [Visual Studio bir Mac bilgisayara bağlayarak](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="47550-133">For specific instructions on how to do this, please read the documentation for [connecting Visual Studio to a Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="47550-134">Uygulamanızı çalıştırdıktan sonra kapsayıcı oluşturacak `mycontainer` depolama hesabınızdaki.</span><span class="sxs-lookup"><span data-stu-id="47550-134">Once you run your app, it will create the container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="47550-135">Blob içermelidir `myblob`, metin olan `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="47550-135">It should contain the blob, `myblob`, which has the text, `Hello, world!`.</span></span> <span data-ttu-id="47550-136">Bunu kullanarak doğrulamak [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="47550-136">You can verify this by using the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="47550-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="47550-137">Next steps</span></span>
<span data-ttu-id="47550-138">Bu öğreticide, Azure Blob depolama alanındaki bir senaryo özel olarak odaklanan depolama alanını, Xamarin platformlar arası uygulama oluşturmak nasıl öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="47550-138">In this tutorial, you learned how to create a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="47550-139">Ancak, yalnızca Blob Storage ile aynı zamanda tablo, dosya ve kuyruk depolama ile çok daha fazla yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47550-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="47550-140">Daha fazla bilgi için aşağıdaki makalelere gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="47550-140">Please check out the following articles to learn more:</span></span>

* [<span data-ttu-id="47550-141">.NET kullanarak Azure Blob Depolama ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="47550-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="47550-142">.NET kullanarak Azure Tablo Depolama ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="47550-142">Get started with Azure Table storage using .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="47550-143">.NET kullanarak Azure Kuyruk Depolama ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="47550-143">Get started with Azure Queue storage using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="47550-144">Windows'da Azure Dosya Depolama ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="47550-144">Get started with Azure File storage on Windows</span></span>](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

