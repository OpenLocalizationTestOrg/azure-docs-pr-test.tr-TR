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
# <a name="how-toouse-blob-storage-from-xamarin"></a>Nasıl toouse Blob depolama alanından Xamarin
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a>Genel Bakış
Xamarin etkinleştirir geliştiriciler toouse paylaşılan C# toocreate iOS, Android ve Windows mağazası uygulamaları kendi yerel kullanıcı arabirimleri ile codebase. Bu öğretici şunların nasıl yapıldığını gösterir toouse Xamarin uygulamasıyla Azure Blob Depolama. Merhaba kodlara başlamadan önce toolearn Azure Storage hakkında daha fazla bilgi isterseniz bkz [giriş tooMicrosoft Azure Storage](storage-introduction.md).

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a>Yeni bir Xamarin uygulaması oluşturma
Bu öğreticide, Android, iOS ve Windows hedefleyen bir uygulama oluşturuluyor. Bu uygulama yalnızca bir kapsayıcı oluşturun ve bu kapsayıcıya bir blob yükleyin. Windows, ancak aynı learnings üzerinde macOS Xamarin Studio kullanarak bir uygulama oluştururken uygulanabilir hello Biz Visual Studio kullanarak.

Bu adımları toocreate uygulamanızı izleyin:

1. Henüz yapmadıysanız yükleyip [Visual Studio için Xamarin](https://www.xamarin.com/download).
2. Visual Studio'yu açın ve (yerel taşınabilir) boş bir uygulaması oluşturun: **Dosya > Yeni > Proje > platformlar arası > boş App(Native Portable)**.
3. Çözümünüzü hello Çözüm Gezgini bölmesinde sağ tıklatıp **çözüm için NuGet paketlerini Yönet**. Arama **WindowsAzure.Storage** ve hello en son kararlı sürümü tooall projeleri çözümünüzde yükler.
4. Derleme ve projenizi çalıştırma.

Şimdi tooclick bir sayaç artırılır düğmesinin sağlayan bir uygulama olmalıdır.

## <a name="create-container-and-upload-blob"></a>Kapsayıcı oluşturun ve blob karşıya yükleme
Sonraki altında `(Portable)` proje, biraz kod çok ekleyeceksiniz`MyClass.cs`. Bu kod, bir kapsayıcı oluşturur ve bu kapsayıcıya bir blob yükler. `MyClass.cs`Merhaba aşağıdaki gibi görünmelidir:

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

Emin tooreplace "your_account_name_here" ve "your_account_key_here" gerçek hesap adı ve hesap anahtarı oluşturur. 

İOS, Android ve Windows Phone projeleri tüm, tüm paylaşılan kodunuzu birinde yazabilirsiniz anlamı başvuruları tooyour taşınabilir proje - yerleştirin ve tüm projeleriniz arasında kullanın. Kod tooeach proje toostart alma avantajı satırının aşağıdaki hello artık ekleyebilirsiniz:`MyClass.performBlobOperation()`

### <a name="xamarinappdroid--mainactivitycs"></a>XamarinApp.Droid > MainActivity.cs

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

### <a name="xamarinappios--viewcontrollercs"></a>XamarinApp.iOS > ViewController.cs

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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a>XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs

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

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın
Bu gibi durumlarda, bu uygulama artık bir Android veya Windows Phone öykünücüsü çalıştırabilirsiniz. Bu uygulamayı bir iOS öykünücüsünde de çalıştırabilirsiniz, ancak bu bir Mac bilgisayar gerektirir Nasıl toodo bunu okuyun hello belgelerine ilgili ayrıntılı yönergeler için [Visual Studio tooa Mac bağlanma](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)

Uygulamanızı çalıştırdıktan sonra hello kapsayıcı oluşturacak `mycontainer` depolama hesabınızdaki. Merhaba blob içermelidir `myblob`, hello metin olan `Hello, world!`. Bu hello kullanarak doğrulayın [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, öğrenilen nasıl toocreate Xamarin platformlar arası uygulamada kullanan Azure Storage, Blob depolama alanındaki bir senaryo özel olarak odaklanan. Ancak, yalnızca Blob Storage ile aynı zamanda tablo, dosya ve kuyruk depolama ile çok daha fazla yapabilirsiniz. Daha fazla makaleleri toolearn aşağıdaki hello gözden geçirin:

* [.NET kullanarak Azure Blob Depolama ile çalışmaya başlama](storage-dotnet-how-to-use-blobs.md)
* [.NET kullanarak Azure Tablo Depolama ile çalışmaya başlama](storage-dotnet-how-to-use-tables.md)
* [.NET kullanarak Azure Kuyruk Depolama ile çalışmaya başlama](storage-dotnet-how-to-use-queues.md)
* [Windows'da Azure Dosya Depolama ile çalışmaya başlama](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

