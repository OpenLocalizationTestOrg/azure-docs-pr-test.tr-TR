
1. <span data-ttu-id="b0d15-101">Başlangıç projesi Android Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="b0d15-101">Open hello project in Android Studio.</span></span>

2. <span data-ttu-id="b0d15-102">İçinde **Proje Gezgini** Android Studio'da hello ToDoActivity.java dosyasını açın ve içeri aktarma deyimlerini aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0d15-102">In **Project Explorer** in Android Studio, open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="b0d15-103">Yöntem toohello aşağıdaki hello eklemek **ToDoActivity** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="b0d15-103">Add hello following method toohello **ToDoActivity** class:</span></span>

        // You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using hello Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check hello request code matches hello one we send in hello login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check hello error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    <span data-ttu-id="b0d15-104">Bu kod bir yöntem toohandle hello Google kimlik doğrulama işlemi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b0d15-104">This code creates a method toohandle hello Google authentication process.</span></span> <span data-ttu-id="b0d15-105">Bir iletişim kutusu hello hello kimliği doğrulanmış kullanıcının Kimliğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b0d15-105">A dialog displays hello ID of hello authenticated user.</span></span> <span data-ttu-id="b0d15-106">Yalnızca başarılı bir kimlik doğrulaması devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0d15-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b0d15-107">Google dışında bir kimlik sağlayıcısı kullanıyorsanız, toohello geçirilen hello değeri değiştirmek **oturum açma** değerleri aşağıdaki Merhaba, yöntemi tooone: _MicrosoftAccount_, _Facebook_, _Twitter_, veya _windowsazureactivedirectory_.</span><span class="sxs-lookup"><span data-stu-id="b0d15-107">If you are using an identity provider other than Google, change hello value passed toohello **login** method tooone of hello following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="b0d15-108">Merhaba, **onCreate** yöntemi, hello başlatır hello koddan sonra aşağıdaki kod hello eklemek `MobileServiceClient` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="b0d15-108">In hello **onCreate** method, add hello following line of code after hello code that instantiates hello `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="b0d15-109">Bu çağrı hello kimlik doğrulama işlemi başlatır.</span><span class="sxs-lookup"><span data-stu-id="b0d15-109">This call starts hello authentication process.</span></span>

5. <span data-ttu-id="b0d15-110">Koddan sonra kalan hello taşıma `authenticate();` hello içinde **onCreate** yöntemi tooa yeni **createTable** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b0d15-110">Move hello remaining code after `authenticate();` in hello **onCreate** method tooa new **createTable** method:</span></span>

        private void createTable() {

            // Get hello table instance toouse.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter toobind hello items with hello view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load hello items from Azure.
            refreshItemsFromTable();
        }

6. <span data-ttu-id="b0d15-111">tooensure yeniden yönlendirme works beklendiği gibi parçacığını aşağıdaki hello eklemek _RedirectUrlActivity_ too_AndroidManifest.xml_:</span><span class="sxs-lookup"><span data-stu-id="b0d15-111">tooensure redirection works as expected, add hello following snippet of _RedirectUrlActivity_ too_AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="b0d15-112">Android uygulamanızın redirectUriScheme too_build.gradle_ ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b0d15-112">Add redirectUriScheme too_build.gradle_ of your Android application.</span></span>

        android {
            buildTypes {
                release {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
                debug {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
            }
        }

8. <span data-ttu-id="b0d15-113">Com.Android.support:customtabs:23.0.1 toohello bağımlılıkları, build.gradle ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0d15-113">Add com.android.support:customtabs:23.0.1 toohello dependencies in your build.gradle:</span></span>

      <span data-ttu-id="b0d15-114">bağımlılıklar {/ /... 'com.android.support:customtabs:23.0.1' derleme}</span><span class="sxs-lookup"><span data-stu-id="b0d15-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="b0d15-115">Merhaba gelen **çalıştırmak** menüsünde tıklatın **uygulamayı çalıştırın** toostart hello uygulama ve seçilen kimlik sağlayıcınızı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b0d15-115">From hello **Run** menu, click **Run app** toostart hello app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="b0d15-116">Merhaba URL belirtilen düzeni büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="b0d15-116">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="b0d15-117">Emin tüm oluşumlarını `{url_scheme_of_you_app}` kullanım hello aynı durumda.</span><span class="sxs-lookup"><span data-stu-id="b0d15-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use hello same case.</span></span>

<span data-ttu-id="b0d15-118">Başarılı bir şekilde imzalanmış, hello uygulama hatasız çalışması gerektiğini ve mümkün tooquery hello arka uç hizmeti olması ve güncelleştirmeleri toodata yapın.</span><span class="sxs-lookup"><span data-stu-id="b0d15-118">When you are successfully signed in, hello app should run without errors, and you should be able tooquery hello back-end service and make updates toodata.</span></span>
