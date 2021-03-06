---
title: Hello, Android：快速入門
description: 在這份含有兩部分的指南中，您將會建置您的第一個 Xamarin.Android 應用程式 (使用 Visual Studio 或 Visual Studio for Mac)，以及了解使用 Xamarin 進行 Android 應用程式開發的基本知識。 在過程中，將會為您介紹建置和部署 Xamarin.Android 應用程式所需的工具、概念和步驟。
ms.topic: quickstart
ms.prod: xamarin
ms.assetid: 44007FA1-3ABC-4935-BF52-4613AF0553A6
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 07/20/2018
ms.openlocfilehash: beb90587e0d720de7770056c8b51264099edecdc
ms.sourcegitcommit: fb55eba393e43bcc9e9d1fef9ef1f1310e99f620
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2018
ms.locfileid: "39189017"
---
# <a name="hello-android-quickstart"></a>Hello, Android：快速入門

_在這份含有兩部分的指南中，您將會建置您的第一個 Xamarin.Android 應用程式 (使用 Visual Studio 或 Visual Studio for Mac)，以及了解使用 Xamarin 進行 Android 應用程式開發的基本知識。在此過程中，將會為您介紹建置和部署 Xamarin.Android 應用程式所需的工具、概念和步驟。_

## <a name="hello-android-quickstart"></a>Hello, Android 快速入門

在本逐步解說中，您將建立可將使用者輸入的英數字元電話號碼翻譯成數字電話號碼，然後將數字電話號碼顯示給使用者的應用程式。 最終的應用程式看起來如下：

[![完成時的應用程式螢幕擷取畫面](hello-android-quickstart-images/intro-app-examples-sml.png)](hello-android-quickstart-images/intro-app-examples.png#lightbox)


## <a name="requirements"></a>需求

若要遵循這個逐步解說，您需要下列項目：

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

-   Windows 7 (含) 以後版本。

-   Visual Studio 2015 Professional (含) 以後版本。

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio for Mac](#tab/vsmac)

-   最新版本的 Visual Studio for Mac。

-   OS X Yosemite (含) 以後版本。

-----

本逐步解說假設您所選擇的平台上已安裝並執行 Xamarin.Android 的最新版本。 如需安裝 Xamarin.Android 的指南，請參閱 [Xamarin.Android 安裝](~/android/get-started/installation/index.md)指南。
在您開始之前，請下載並解壓縮 [Xamarin 應用程式圖示和啟動螢幕](https://github.com/xamarin/monodroid-samples/blob/master/Phoneword/Resources/XamarinAndroidIcons.zip?raw=true)集。

## <a name="configuring-emulators"></a>設定模擬器

如果您使用 Android 模擬器，我們建議您設定模擬器以使用硬體加速。 設定硬體加速的指示請參閱[硬體加速以提升模擬器效能](~/android/get-started/installation/android-emulator/hardware-acceleration.md)。


## <a name="walkthrough"></a>逐步解說

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

啟動 Visual Studio。  按一下 [檔案] > [新增] > [專案]，建立新的專案。

在 [新增專案] 對話方塊中，按一下 [Android 應用程式] 範本。
將新專案命名為 `Phoneword`。 按一下 [確定]：

[![新的專案是 Phoneword](hello-android-quickstart-images/vs/01-new-project-name-w157-sml.png)](hello-android-quickstart-images/vs/01-new-project-name-w157.png#lightbox)

在 [新增 Android 應用程式] 對話方塊中，按一下 [空白應用程式]，然後按一下 [確定] 以建立新應用程式：

[![選取空白應用程式範本](hello-android-quickstart-images/vs/02-blank-app-w157-sml.png)](hello-android-quickstart-images/vs/02-blank-app-w157.png#lightbox)

### <a name="creating-the-layout"></a>建立版面配置

建立新專案之後，請展開 [資源] 資料夾，然後在方案總管中展開 [配置] 資料夾。
按兩下 [activity_main.axml] 以在 Android Designer 中開啟它。 這是應用程式螢幕的配置檔案：

[![開啟 activity main.axml](hello-android-quickstart-images/vs/04-open-layout-sml.png)](hello-android-quickstart-images/vs/04-open-layout.png#lightbox)

從 [工具箱] (左側區域)，在搜尋欄位中輸入 `text`，然後將 [Text (Large)] (文字 (大型)) 小工具拖曳至設計介面 (中央區域)：

[![新增大型文字小工具](hello-android-quickstart-images/vs/04-large-text-sml.png)](hello-android-quickstart-images/vs/04-large-text.png#lightbox)

在設計介面上選取 [Text (Large)] (文字 (大型)) 控制項之後，使用 [屬性] 窗格將 [Text (Large)] (文字 (大型)) 小工具的 `text` 屬性變更為 `Enter a Phoneword:`，如下所示：

[![設定大型文字屬性](hello-android-quickstart-images/vs/05-enter-a-phoneword-sml.png)](hello-android-quickstart-images/vs/05-enter-a-phoneword.png#lightbox)

從 [工具箱] 將 [純文字] 小工具拖曳到設計介面，並將其放置於 [Text (Large)] (文字 (大型)) 小工具下：

[![新增純文字小工具](hello-android-quickstart-images/vs/06-plain-text-sml.png)](hello-android-quickstart-images/vs/06-plain-text.png#lightbox)

在設計介面上選取 [純文字] 小工具之後，使用 [屬性] 窗格將 [純文字] 小工具的 `id` 屬性變更為 `@+id/PhoneNumberText`，並將 `text` 屬性變更為 `1-855-XAMARIN`：

[![設定純文字屬性](hello-android-quickstart-images/vs/07-add-properties-sml.png)](hello-android-quickstart-images/vs/07-add-properties.png#lightbox)

從 [工具箱] 將 [按鈕] 拖曳到設計介面，並將其放置於 [純文字] 小工具下：

[![將翻譯按鈕拖曳到設計](hello-android-quickstart-images/vs/08-drag-button-sml.png)](hello-android-quickstart-images/vs/08-drag-button.png#lightbox)

在設計介面上選取 [按鈕] 之後，使用 [屬性] 窗格將 [按鈕] 的 `id` 屬性變更為 `@+id/TranslateButton`，並將 `text` 屬性變更為 `Translate`：

[![設定翻譯按鈕屬性](hello-android-quickstart-images/vs/09-translate-button-sml.png)](hello-android-quickstart-images/vs/09-translate-button.png#lightbox)

從 [工具箱] 將 [文字檢視] 拖曳到設計介面，並將其放置於 [按鈕] 小工具下。 將 **TextView** 的 `id` 屬性設定為 `@+id/TranslatedPhoneWord`，並將 `text` 變更為空字串：

[![在文字檢視上設定屬性。](hello-android-quickstart-images/vs/10-textview-properties-sml.png)](hello-android-quickstart-images/vs/10-textview-properties.png#lightbox)    

藉由按下 **CTRL + S** 儲存您的工作。

### <a name="writing-translation-code"></a>撰寫翻譯程式碼

下一步是新增一些將電話號碼從英數字元翻譯為數字的程式碼。 先以滑鼠右鍵按一下方案總管窗格中的 **Phoneword** 專案，然後選擇 [新增] > [新增項目...]，如下所示：

[![新增項目](hello-android-quickstart-images/vs/12-add-new-item-sml.png)](hello-android-quickstart-images/vs/12-add-new-item.png#lightbox)

在 [新增項目] 對話方塊中選取 [Visual C#] > [程式碼] > [程式碼檔案] 並將新的程式碼檔案命名為 **PhoneTranslator.cs**：

[![新增 PhoneTranslator.cs](hello-android-quickstart-images/vs/14-add-class-sml-w157.png)](hello-android-quickstart-images/vs/14-add-class-w157.png#lightbox)

這會建立新的空白 C# 類別。 將下列程式碼插入這個檔案中：

```csharp
using System.Text;
using System;
namespace Core
{
    public static class PhonewordTranslator
    {
        public static string ToNumber(string raw)
        {
            if (string.IsNullOrWhiteSpace(raw))
                return "";
            else
                raw = raw.ToUpperInvariant();

            var newNumber = new StringBuilder();
            foreach (var c in raw)
            {
                if (" -0123456789".Contains(c))
                {
                    newNumber.Append(c);
                }
                else
                {
                    var result = TranslateToNumber(c);
                    if (result != null)
                        newNumber.Append(result);
                }
                // otherwise we've skipped a non-numeric char
            }
            return newNumber.ToString();
        }
        static bool Contains (this string keyString, char c)
        {
            return keyString.IndexOf(c) >= 0;
        }
        static int? TranslateToNumber(char c)
        {
            if ("ABC".Contains(c))
                return 2;
            else if ("DEF".Contains(c))
                return 3;
            else if ("GHI".Contains(c))
                return 4;
            else if ("JKL".Contains(c))
                return 5;
            else if ("MNO".Contains(c))
                return 6;
            else if ("PQRS".Contains(c))
                return 7;
            else if ("TUV".Contains(c))
                return 8;
            else if ("WXYZ".Contains(c))
                return 9;
            return null;
        }
    }
}
```

儲存對 **PhoneTranslator.cs** 檔案的變更，方法是按一下 [檔案] > [儲存] (或按 **CTRL + S**)，然後關閉檔案。

### <a name="wiring-up-the-interface"></a>連接介面

下一個步驟是將支援程式碼插入到 `MainActivity` 類別，以便新增程式碼來連接使用者介面。 首先連接 [翻譯] 按鈕。 在 `MainActivity` 類別中找到 `OnCreate` 方法。 下一個步驟是將按鈕程式碼新增在 `OnCreate` 內，`base.OnCreate(bundle)` 和 `SetContentView
(Resource.Layout.Main)` 呼叫底下。 首先，修改範本程式碼，讓 `OnCreate` 方法如下所示：

```csharp
using System;
using Android.App;
using Android.Content;
using Android.Widget;
using Android.OS;

namespace Phoneword
{
    [Activity (Label = "Phone Word", MainLauncher = true)]
    public class MainActivity : Activity
    {
        protected override void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // New code will go here
        }
    }
}
```

針對透過 Android Designer 在配置檔案中建立的控制項取得參考。 在 `OnCreate` 方法內的 `SetContentView` 呼叫後方新增下列程式碼：

```csharp
// Get our UI controls from the loaded layout
EditText phoneNumberText = FindViewById<EditText>(Resource.Id.PhoneNumberText);
TextView translatedPhoneWord = FindViewById<TextView>(Resource.Id.TranslatedPhoneWord);
Button translateButton = FindViewById<Button>(Resource.Id.TranslateButton);
```

新增回應使用者按下 [翻譯] 按鈕的程式碼。
將下列程式碼新增到 `OnCreate` 方法 (在上一個步驟中所新增的行之後)：

```csharp
// Add code to translate number
translateButton.Click += (sender, e) =>
{
    // Translate user's alphanumeric phone number to numeric
    string translatedNumber = Core.PhonewordTranslator.ToNumber(phoneNumberText.Text);
    if (string.IsNullOrWhiteSpace(translatedNumber))
    {
        translatedPhoneWord.Text = string.Empty;
    }
    else
    {
        translatedPhoneWord.Text = translatedNumber;
    }
};
```

選取 [檔案] > [全部儲存] (或按 **CTRL-SHIFT-S**) 來儲存您的工作，然後選取 [建置] > [重建方案] (或按 **CTRL-SHIFT-B**) 來建置應用程式。 

如果發生錯誤，請完成上述步驟，並更正任何錯誤，直到應用程式建置成功為止。 如果您收到建置錯誤，例如「資源不存在於目前的內容」，請確認 **MainActivity.cs** 中的命名空間名稱符合專案名稱 (`Phoneword`)，然後完全重建解決方案。 如果您仍然得到建置錯誤，請確認您已安裝最新的 Xamarin.Android 更新。

### <a name="setting-the-label-and-app-icon"></a>設定標籤和應用程式圖示

您現在應該有可用的應用程式 &ndash; 該新增最後修飾了！ 在 **MainActivity.cs** 中，編輯 `MainActivity` 的 `Label`。 `Label` 是 Android 顯示在螢幕頂端，讓使用者知道他們在應用程式何處的內容。
在 `MainActivity` 類別頂端，將 `Label` 變更為 `Phone Word`，如下所示：

```csharp
namespace Phoneword
{
    [Activity (Label = "Phone Word", MainLauncher = true)]
    public class MainActivity : Activity
    {
        ...
    }
}
```

現在是時候來設定應用程式圖示了。 根據預設，Visual Studio 會為專案提供預設圖示。 讓我們從解決方案刪除這些檔案，並將它們取代成不同的圖示。 在 **Solution Pad** 中展開 [Resources] 資料夾。 請注意，有五個資料夾前面會加上 **mipmap-**，且這些每個資料夾都包含一個 **Icon.png** 檔案：

[![mipmap- 資料夾和 Icon.png 檔案](hello-android-quickstart-images/vs/21-mipmap-folders-sml.png)](hello-android-quickstart-images/vs/21-mipmap-folders.png#lightbox)

必須從專案刪除這些圖示檔的每一個。 以滑鼠右鍵按一下每個 **Icon.png** 檔案，然後從捷徑功能表選取 [刪除]：
   
[![刪除預設 Icon.png](hello-android-quickstart-images/vs/21-delete-icon-sml.png)](hello-android-quickstart-images/vs/21-delete-icon.png#lightbox)
   
在對話方塊中按一下 [刪除] 按鈕。

接下來，下載並解壓縮 [Xamarin 應用程式圖示集](https://github.com/xamarin/monodroid-samples/blob/master/Phoneword/Resources/XamarinAndroidIcons.zip?raw=true)。 這個 ZIP 檔案中有應用程式的圖示。 每個圖示看起來相同，但會以不同的解析度正確地翻譯在不同螢幕密度的不同裝置上。  檔案集必須複製到 Xamarin.Android 專案。 在 Visual Studio 的方案總管中，以滑鼠右鍵按一下 **mipmap-hdpi** 資料夾，然後選取 [新增] > [現有的項目]：

[![新增檔案](hello-android-quickstart-images/vs/22-add-files-sml.png)](hello-android-quickstart-images/vs/22-add-files.png#lightbox)

從選取項目對話方塊中，巡覽至解壓縮的 Xamarin AdApp Icons 目錄，並開啟 **mipmap-hdpi** 資料夾。 選取 **Icon.png** 然後按一下 [新增]。

針對每個 **mipmap-** 資料夾重複這些步驟，直到 **mipmap-** Xamarin App Icons 資料夾的內容複製到 **Phoneword** 專案中的對應 **mipmap-** 資料夾。

所有的圖示複製到 Xamarin.Android 專案之後，請開啟 [專案選項] 對話方塊，方法是在 **Solution Pad** 中以滑鼠右鍵按一下專案。 選取 [建置] > [Android 應用程式]，然後從 **應用程式圖示**下拉式方塊選取 **@mipmap/icon**：

[![設定專案圖示](hello-android-quickstart-images/vs/25-set-project-icon-sml.png)](hello-android-quickstart-images/vs/25-set-project-icon.png#lightbox)

### <a name="running-the-app"></a>執行應用程式

最後，在 Android 裝置或模擬器上執行應用程式，然後翻譯 Phoneword 以測試應用程式：

[![完成時的應用程式螢幕擷取畫面](hello-android-quickstart-images/intro-app-examples-sml.png)](hello-android-quickstart-images/intro-app-examples.png#lightbox)



# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio for Mac](#tab/vsmac)

從 [Applications] 資料夾，或從 [Spotlight]，啟動 Visual Studio for Mac。 

按一下 [新增方案...] 以建立新專案。

在 [Choose a template for your new project] (選擇新專案的範本) 對話方塊中，按一下 [Android] > [應用程式]，然後選取 [Android 應用程式] 範本。 按 [ **下一步**]。

[![選擇 Android 應用程式範本](hello-android-quickstart-images/xs/03-choose-template-sml.png)](hello-android-quickstart-images/xs/03-choose-template.png#lightbox)

在 [Configure your Android app] (設定您的 Android 應用程式) 對話方塊中，將新的應用程式命名為 `Phoneword`，然後按一下 [下一步]。

[![設定 Android 應用程式](hello-android-quickstart-images/xs/04-configure-android-app-sml.png)](hello-android-quickstart-images/xs/04-configure-android-app.png#lightbox)

在 [Configure your new Android App] (設定新的 Android 應用程式) 對話方塊中，將解決方案和專案名稱設定保留為 `Phoneword`，然後按一下 [建立] 建立專案。

### <a name="creating-the-layout"></a>建立版面配置

建立新專案之後，請展開 [資源] 資料夾，然後在 **Solution** Pad 中展開 [配置] 資料夾。
按兩下 **Main.axml** 以在 Android Designer 中開啟它。 這是在 Android Designer 中檢視時，螢幕的配置檔案：

[![開啟 Main.axml](hello-android-quickstart-images/xs/05-open-layout-sml.png)](hello-android-quickstart-images/xs/05-open-layout.png#lightbox)

在設計介面上選取 [Hello World, Click Me!] 按鈕，然後按 **Delete** 鍵來移除它。 

從 [工具箱] (右側區域)，在搜尋欄位中輸入 `text`，然後將 [Text (Large)] (文字 (大型)) 小工具拖曳至設計介面 (中央區域)：

[![新增大型文字小工具](hello-android-quickstart-images/xs/06-large-text-sml.png)](hello-android-quickstart-images/xs/06-large-text.png#lightbox)

在設計介面上選取 [Text (Large)] (文字 (大型)) 小工具之後，您可以使用 **Properties** Pad 將 [Text (Large)] (文字 (大型)) 小工具的 `Text` 屬性變更為 `Enter a Phoneword:`，如下所示：

[![設定大型文字小工具屬性](hello-android-quickstart-images/xs/07-enter-a-phoneword-sml.png)](hello-android-quickstart-images/xs/07-enter-a-phoneword.png#lightbox)

接下來，從 [工具箱] 將 [純文字] 小工具拖曳到設計介面，並將其放置於 [Text (Large)] (文字 (大型)) 小工具下。 請注意，您可以使用搜尋欄位來協助依名稱尋找小工具：

[![新增純文字小工具](hello-android-quickstart-images/xs/08-plain-text-sml.png)](hello-android-quickstart-images/xs/08-plain-text.png#lightbox)

在設計介面上選取 [純文字] 小工具之後，您可以使用 **Properties** Pad 將 [純文字] 小工具的 `Id` 屬性變更為 `@+id/PhoneNumberText`，並將 `Text` 屬性變更為 `1-855-XAMARIN`：

[![設定純文字小工具屬性](hello-android-quickstart-images/xs/09-add-properties-sml.png)](hello-android-quickstart-images/xs/09-add-properties.png#lightbox)

從 [工具箱] 將 [按鈕] 拖曳到設計介面，並將其放置於 [純文字] 小工具下：

[![新增按鈕](hello-android-quickstart-images/xs/10-drag-button-sml.png)](hello-android-quickstart-images/xs/10-drag-button.png#lightbox)

在設計介面上選取 [按鈕] 之後，您可以使用 **Properties** Pad 將 [按鈕] 小工具的 `Id` 屬性變更為 `@+id/TranslateButton`，並將 `Text` 屬性變更為 `Translate`：

[![設定為翻譯按鈕](hello-android-quickstart-images/xs/11-translate-button-sml.png)](hello-android-quickstart-images/xs/11-translate-button.png#lightbox)

從 [工具箱] 將 **TextView** 拖曳到設計介面，並將其放置於 [按鈕] 小工具下。 選取 **TextView** 之後，請將 **TextView** 的 `id` 屬性設定為 `@+id/TranslatedPhoneWord`，並將 `text` 變更為空字串：

[![在文字檢視上設定屬性。](hello-android-quickstart-images/xs/12-textview-properties-sml.png)](hello-android-quickstart-images/xs/12-textview-properties.png#lightbox)    

藉由按下 **&#8984; + S** 儲存您的工作。

### <a name="writing-translation-code"></a>撰寫翻譯程式碼

現在，新增一些將電話號碼從英數字元翻譯為數字的程式碼。 按一下 **Solution** Pad 中的 **Phoneword** 專案旁的齒輪圖示，然後選擇 [新增] > [新增檔案...]，將新檔案新增至專案：

[![將新檔案新增至專案](hello-android-quickstart-images/xs/14-add-new-file-sml.png)](hello-android-quickstart-images/xs/14-add-new-file.png#lightbox)

在 [新增檔案] 對話方塊中，選取 [一般] > [空的類別]、將新檔案命名為 **PhoneTranslator**，然後按一下 [新增]。 這會建立新的空白 C# 類別。

在新類別中移除所有範本程式碼，並取代為下列程式碼：

```csharp
using System.Text;
using System;
namespace Core
{
    public static class PhonewordTranslator
    {
        public static string ToNumber(string raw)
        {
            if (string.IsNullOrWhiteSpace(raw))
                return "";
            else
                raw = raw.ToUpperInvariant();

            var newNumber = new StringBuilder();
            foreach (var c in raw)
            {
                if (" -0123456789".Contains(c))
                {
                    newNumber.Append(c);
                }
                else
                {
                    var result = TranslateToNumber(c);
                    if (result != null)
                        newNumber.Append(result);
                }
                // otherwise we've skipped a non-numeric char
            }
            return newNumber.ToString();
        }
        static bool Contains (this string keyString, char c)
        {
            return keyString.IndexOf(c) >= 0;
        }
        static int? TranslateToNumber(char c)
        {
            if ("ABC".Contains(c))
                return 2;
            else if ("DEF".Contains(c))
                return 3;
            else if ("GHI".Contains(c))
                return 4;
            else if ("JKL".Contains(c))
                return 5;
            else if ("MNO".Contains(c))
                return 6;
            else if ("PQRS".Contains(c))
                return 7;
            else if ("TUV".Contains(c))
                return 8;
            else if ("WXYZ".Contains(c))
                return 9;
            return null;
        }
    }
}
```

儲存對 **PhoneTranslator.cs** 檔案的變更，方法是選擇 [檔案] > [儲存] (或按 **&#8984; + S**)，然後關閉檔案。 重建解決方案以確定沒有任何編譯時間錯誤。

### <a name="wiring-up-the-interface"></a>連接介面

下一個步驟是將支援程式碼新增到 `MainActivity` 類別，以便新增程式碼來連接使用者介面。
在 **Solution Pad** 中，按兩下 **MainActivity.cs**，將其開啟。

開始新增事件處理常式至 [翻譯] 按鈕。 在 `MainActivity` 類別中找到 `OnCreate` 方法。 將按鈕程式碼新增在 `OnCreate` 內，`base.OnCreate(bundle)` 和 `SetContentView (Resource.Layout.Main)` 呼叫底下。 移除任何現有的按鈕處理程式碼 (亦即參考 `Resource.Id.myButton` 並為它建立點擊處理常式的程式碼) 以便 `OnCreate` 方法看起來像下面這樣：

```csharp
using System;
using Android.App;
using Android.Content;
using Android.Runtime;
using Android.Views;
using Android.Widget;
using Android.OS;

namespace Phoneword
{
    [Activity (Label = "Phone Word", MainLauncher = true)]
    public class MainActivity : Activity
    {
        protected override void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Our code will go here
        }
    }
}
```

接下來，需要針對透過 Android Designer 在配置檔案中建立的控制項參考。 在 `OnCreate` 方法內 (在 `SetContentView` 呼叫後方) 新增下列程式碼：

```csharp
// Get our UI controls from the loaded layout
EditText phoneNumberText = FindViewById<EditText>(Resource.Id.PhoneNumberText);
TextView translatedPhoneWord = FindViewById<TextView>(Resource.Id.TranslatedPhoneWord);
Button translateButton = FindViewById<Button>(Resource.Id.TranslateButton);
```

新增回應使用者按下 [翻譯] 的程式碼，方法是新增下列程式碼到 `OnCreate` 方法 (在上個步驟中新增的行後方)：

```csharp
// Add code to translate number
string translatedNumber = string.Empty;

translateButton.Click += (sender, e) =>
{
    // Translate user's alphanumeric phone number to numeric
    translatedNumber = PhonewordTranslator.ToNumber(phoneNumberText.Text);
    if (string.IsNullOrWhiteSpace(translatedNumber))
    {
        translatedPhoneWord.Text = string.Empty;
    }
    else
    {
        translatedPhoneWord.Text = translatedNumber;
    }
};
```

選取 [建置] > [Build All] (全部建置) (或按 **& #8984; + B**) 儲存工作並建置應用程式。 如果應用程式會編譯，您會在 Visual Studio for Mac 的頂端看到成功訊息：

如果發生錯誤，請完成上述步驟，並更正任何錯誤，直到應用程式建置成功為止。 如果您收到建置錯誤，例如「資源不存在於目前的內容」，請確認 **MainActivity.cs** 中的命名空間名稱符合專案名稱 (`Phoneword`)，然後完全重建解決方案。 如果您仍然得到建置錯誤，請確認您已安裝最新的 Xamarin.Android 和 Visual Studio for Mac 更新。

### <a name="setting-the-label-and-app-icon"></a>設定標籤和應用程式圖示

既然您已有可用的應用程式，該新增最後修飾了！ 請開始編輯 `MainActivity` 的 `Label`。
`Label` 是 Android 顯示在螢幕頂端，讓使用者知道他們在應用程式何處的內容。 在 `MainActivity` 類別頂端，將 `Label` 變更為 `Phone Word`，如下所示：

```csharp
namespace Phoneword
{
    [Activity (Label = "Phone Word", MainLauncher = true)]
    public class MainActivity : Activity
    {
        ...
    }
}
```

現在是時候來設定應用程式圖示了。 根據預設，Visual Studio for Mac 會為專案提供預設圖示。 讓我們從解決方案刪除這些檔案，並將它們取代成不同的圖示。 在 **Solution Pad** 中展開 [Resources] 資料夾。 請注意，有五個資料夾前面會加上 **mipmap-**，且這些每個資料夾都包含一個 **Icon.png** 檔案：

[![mipmap- 資料夾和 Icon.png 檔案](hello-android-quickstart-images/xs/23-mipmap-folders-sml.png)](hello-android-quickstart-images/xs/23-mipmap-folders.png#lightbox)

必須從專案刪除這些圖示檔的每一個。 以滑鼠右鍵按一下每個 **Icon.png** 檔案，然後從捷徑功能表選取 [移除]：

[![刪除預設的 Icon.png](hello-android-quickstart-images/xs/23-delete-icon-sml.png)](hello-android-quickstart-images/xs/23-delete-icon.png#lightbox)

在對話方塊中按一下 [刪除] 按鈕。

接下來，下載並解壓縮 [Xamarin 應用程式圖示集](https://github.com/xamarin/monodroid-samples/blob/master/Phoneword/Resources/XamarinAndroidIcons.zip?raw=true)。 這個 ZIP 檔案中有應用程式的圖示。 每個圖示看起來相同，但會以不同的解析度正確地翻譯在不同螢幕密度的不同裝置上。  檔案集必須複製到 Xamarin.Android 專案。 在 Visual Studio for Mac 的 Solution Pad 中，以滑鼠右鍵按一下 **mipmap-hdpi** 資料夾，然後選取 [新增] > [新增檔案]：

[![新增檔案](hello-android-quickstart-images/xs/24-add-files-sml.png)](hello-android-quickstart-images/xs/24-add-files.png#lightbox)

從選取項目對話方塊中，巡覽至解壓縮的 Xamarin AdApp Icons 目錄，並開啟 **mipmap-hdpi** 資料夾。 選取 **Icon.png**然後按一下 [開啟]。

在 [Add File to Folder] (將檔案新增至資料夾) 對話方塊中，選取 [Copy the file into the directory] (將檔案複製到目錄)，然後按一下 [確定]：

[![將檔案複製到目錄對話方塊](hello-android-quickstart-images/xs/26-copy-to-directory-sml.png)](hello-android-quickstart-images/xs/26-copy-to-directory.png#lightbox)

針對每個 **mipmap-** 資料夾重複這些步驟，直到 **mipmap-** Xamarin App Icons 資料夾的內容複製到 **Phoneword** 專案中的對應 **mipmap-** 資料夾。

所有的圖示複製到 Xamarin.Android 專案之後，請開啟 [專案選項] 對話方塊，方法是在 **Solution Pad** 中以滑鼠右鍵按一下專案。 選取 [建置] > [Android 應用程式]，然後從 **應用程式圖示**下拉式方塊選取 **@mipmap/icon**：

[![設定專案圖示](hello-android-quickstart-images/xs/28-set-project-icon-sml.png)](hello-android-quickstart-images/xs/28-set-project-icon.png#lightbox)

### <a name="running-the-app"></a>執行應用程式

最後，在 Android 裝置或模擬器上執行應用程式，然後翻譯 Phoneword 以測試應用程式：

[![完成時的應用程式螢幕擷取畫面](hello-android-quickstart-images/intro-app-examples-sml.png)](hello-android-quickstart-images/intro-app-examples.png#lightbox)

-----

恭喜您完成第一個 Xamarin.Android 應用程式！
現在就可以仔細分析您剛學會的工具和技巧。 接下來是 [Hello, Android 深度剖析](~/android/get-started/hello-android/hello-android-deepdive.md)。


## <a name="related-links"></a>相關連結

- [Xamarin Android 應用程式圖示 (ZIP)](https://github.com/xamarin/monodroid-samples/blob/master/Phoneword/Resources/XamarinAndroidIcons.zip?raw=true)
- [Phoneword (範例)](https://developer.xamarin.com/samples/monodroid/Phoneword)
