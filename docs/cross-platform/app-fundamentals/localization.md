---
title: 應用程式使用者介面當地語系化
description: 本文件說明國際化和當地語系化的跨平台概念，並且檢查它們如何影響應用程式的設計。
ms.prod: xamarin
ms.assetid: CC6847B2-23FB-4EDE-9F7E-EF29DD46A5C5
author: asb3993
ms.author: amburns
ms.date: 03/22/2017
ms.openlocfilehash: 299fe28a896c2bf2e5c420b330b8e8bde7d9dc22
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34781952"
---
# <a name="localization"></a>當地語系化

這個指南介紹的概念*國際化*和*當地語系化*以及如何產生 Xamarin 行動應用程式使用這些概念的指示的連結。

如果您想要直接跳過的當地語系化的 Xamarin 應用程式的技術詳細資料，以其中一個這些平台專屬的使用說明文章的開頭：

- [**Xamarin.Forms** ](~/xamarin-forms/app-fundamentals/localization/index.md)使用 RESX 檔案的跨平台當地語系化。
- [**Xamarin.iOS** ](~/ios/app-fundamentals/localization/index.md)原生平台當地語系化。
- [**Xamarin.Android** ](~/android/app-fundamentals/localization.md)原生平台當地語系化。

## <a name="i18n-and-l10n"></a>i18n 和 L10n

*國際化*是程序可確保您的程式碼可以顯示不同的語言與調整它的顯示畫面，針對不同的地區設定 （例如數字和日期格式）。 這也稱為*全球化*。

*當地語系化*是遵循 – 每一種語言建立 （例如字串和影像） 的資源及配套它們與 internationalize 應用程式的步驟。

國際化它通常會縮短成 i18n –"i"和"n"之間的 18 字母的縮寫。 以 L10n – 代表"L"和"n"之間的 10 個字母，同樣地會縮短當地語系化。

## <a name="overview"></a>總覽

本文件介紹使用國際化和當地語系化，以及如何將它們套用行動應用程式開發一般相關聯的概念。
設計和建置應用程式中，項目時，您可能先前有硬式編碼，但其必須包含當地語系化的參數化：

-   畫面配置和文字，
-   圖示、 圖形和色彩
-   視訊和音訊檔案，
-   動態的文字和文字格式 （例如數字、 貨幣和日期），
 - 對於由右至左 (RTL) 語言，版面配置變更，
-   資料排序。

無論哪個行動平台應用程式為目標的這些提示可協助您建置高品質的當地語系化應用程式。


## <a name="design-considerations"></a>設計考量

架構應用程式，使其可以當地語系化其內容會呼叫國際化。 正確進行國際化是多個要在執行階段載入只允許對不同的語言字串 – 設計良好的應用程式應該允許進行變更的所有資源的基礎語言和地區設定 （包括影像、 音效和影片） 上，而且可以調整格式和配置，以處理增加的不同大小的字串。

本章節討論某些設計考量，以建置國際化的應用程式時加以考量。

### <a name="layouts-and-string-length"></a>版面配置和字串長度

中文和日文字串可能會很短，有時一個或兩個的字元可以是有足夠的意義，輸入的欄位標籤。

德文字串 （例如） 可能會很長。有時候以英文相當短一段文字會變成以其他語言 – 裁剪或其他非預期地重新配置可能變得很長。

比較的字串長度在英文、 德文與日文的 iOS 主畫面的一些項目：

[![](localization-images/language-compare-sml.png "德文 vs 日文的字串長度")](localization-images/language-compare.png#lightbox)

請注意，**設定**英文 （8 個字元） 為德文的轉譯，但在日文中只有 2 個字元需要 13 個字元。

顯示標籤和輸入的欄位會由並行的配置是不能使用當標籤長度很大的差異。 通常會顯示標籤欄位上方的版面配置是螢幕的您更輕鬆地當地語系化，因為完整寬度是螢幕的適用於標籤和輸入。

一般而言，如果您要建立固定的配置 （尤其是由並行項目） 可以讓需要的標籤和文字的英文字串比寬度至少 50%。 這不會解決所有問題，但會提供在許多情況下運作的緩衝區。

### <a name="input-validation"></a>輸入的驗證

寫入驗證規則時，要注意的假設。 可能不按照有效要求輸入至 「 需要 」 在英文中，至少三個字元，因為單一字母很少會有任何意義的文字欄位。 中文和日文中單一字元可能是有效的輸入，並驗證訊息 「 至少 3 個字元是必要的 」，但不具意義這些語言。

其他看似簡單的工作，例如驗證電子郵件地址或變得更複雜字元的網站 URL 並不僅限於 ASCII 的子集。

撰寫您的驗證規則與國際化記住 – 選擇最不嚴格的規則，或使其以不同的方式可為每種語言撰寫的邏輯。

### <a name="images-and-color"></a>影像和色彩

並非每個映像必須變更根據使用者的語言選擇。 許多圖示或相片將適用於所有使用者，不論說話何種語言。
某些資源合理的當地語系化，例如：

 - 映像用來描述人員或特定位置 – 您的應用程式可能會覺得與使用者更有相關性如果它會顯示本機的人位置。
 - 圖示 – 某些遙控器可以是特定文化特性，您可以讓您的應用程式容易使用當地語系化的圖像以反映本機的了解。
 - 色彩 – 某些文化特性中了解色彩不同 – 紅色可能表示有一個區域，但在另一個祝您好運警告。 設計您的應用程式，以判斷是否您應該會建置一個機制，當地語系化色彩時，請洽詢原生喇叭。


### <a name="videos-and-sound"></a>視訊與音效

視訊及聲音存在的特殊挑戰時當地語系化應用程式，因為儘管它是相對較容易取得翻譯的字串，錄製旁白的多個追蹤或視訊剪輯，可以是昂貴且困難。

視訊和音訊檔案的多個複本 （特別是如果您將當地語系化成大量的語言或有許多的媒體檔案），可能也會大幅增加應用程式的大小。 您可以考慮下載必要的語言資產之後，使用者安裝應用程式，但這也可能導致不良的使用者經驗，在低速網路。

通常有多種方式可以解決當地語系化問題而言最重要的項目請考慮足夠的事前並確保您的應用程式設計來處理它們。


### <a name="dates-times-numbers-and-currency"></a>日期、 時間、 數字和貨幣

如果您使用.NET 的格式化功能，請記得在指定的文化特性，以便的十進位分隔符號正確剖析 （並避免擲回例外狀況的轉換）。 例如 1.99 和 1,99 是有效的十進位表示法，視您的地區設定而定。

當資料來自已知來源 (ie。 從自己的程式碼或您控制的 web 服務) 可以硬例如 InvariantCulture 適用於標準英文語言格式的格式設定符合文化特性識別項。

```csharp
double.Parse("1,999.99", CultureInfo.InvariantCulture);
```

如果資料由應用程式使用者正在輸入，剖析使用 CultureInfo 執行個體，以反映其地區設定：

```csharp
double.Parse("1 999,99", CultureInfo.CreateSpecificCulture("fr-FR"));
```

請參閱[剖析數值字串](http://msdn.microsoft.com/library/xbtzcc4w(v=vs.110).aspx)和[剖析日期和時間字串](http://msdn.microsoft.com/library/2h3syy57(v=vs.110).aspx)MSDN 文件，如需詳細資訊。

<a name="rtl" />

### <a name="right-to-left-rtl-languages"></a>由右至左 (RTL) 語言

某些語言，例如阿拉伯文、 希伯來文和烏都文 （舉例來說），會由右至左讀取。
支援這些語言的應用程式應該使用螢幕設計，例如由右至左讀取器，以調整：

 - 文字應該是靠右對齊。
 - 標籤會顯示輸入欄位的右邊。
 - 通常會反轉預設按鈕的位置。
 - 階層式導覽撥動和動畫 （及其他瀏覽象徵物和動畫），使用方向的內容也應該反轉。

IOS 和 Android 支援由右至左配置和字型呈現時，使用內建功能，有助於讓上述的調整。 Xamarin.Forms 自動目前不支援從右至左呈現。

### <a name="sorting"></a>排序

不同語言有不同，定義其字母的排序順序，即使它們使用相同的字元集。

請參閱[詳細資料的字串比較](http://msdn.microsoft.com/library/dd465121(v=vs.110).aspx#the_details_of_string_comparison)中[在.NET Framework 中使用字串的最佳作法](http://msdn.microsoft.com/library/dd465121(v=vs.110).aspx)範例，其中的語言 (CultureInfo) 會影響排序次序。

也不太可能在行動平台上的內建的資料庫功能將會支援排序，因此您可能需要在您的商務邏輯中實作額外的程式碼的語言特有排序。

### <a name="text-search"></a>文字搜尋

請確定您撰寫並測試您的搜尋演算法使用多種語言記住。 要考量的事項包括：

 - 自動完成 – 如果您已建立的自動完成函式，請確定它來源建議適用於使用者的語言。
 - 資料 – 比對的查詢會搜尋輸入特定的查詢語言可執行針對只以該語言撰寫的內容，或針對您的應用程式中的所有內容嗎？
 - 詞幹分析 – 如果建置您的搜尋搜尋相似的單字、 字根及其他搜尋最佳化，會針對所有支援的語言建立這些最佳化？
 - 排序 – 請確定結果排序錯誤 （請參閱上面）。


### <a name="data-from-external-sources"></a>從外部來源的資料

許多應用程式從外部來源，從 Twitter 下載資料及 RSS 摘要，天氣、 新聞或股票價格。 這顯示給使用者時要考慮的可能性，您會在顯示畫面不相關或無法讀取資訊給他們。

有幾個可用來嘗試並確保您的應用程式會顯示與使用者相關資料的策略：

 - 不同的來源 – 您的應用程式可能會從根據使用者的語言或地區設定不同的來源下載資料。 新聞、 天氣和股票價格的地區設定可能會比較合理，比從北美地區的摘要項目下載。
 - 當地語系化的顯示 – 如果您要顯示 Twitter 或相片摘要時，您應該會顯示中繼資料 （例如所花費的時間） 在他或她自己的語言，即使本身的內容會保留在原始的語言。
 - 轉譯 – 您無法在執行機器翻譯，內送資料的應用程式中建置轉譯選項。 這可以是 自動或斟酌使用者 – 只務必通知使用者，如果這正在進行中，因為機器翻譯絕對不是完美 ！

這也可能影響音訊音軌的外部連結或視訊 – 設計您的應用程式務必事先規劃當做來源轉譯內容，或確保，使用者會適當地通知使用者介面中不會提供內容時其語言。


### <a name="dont-over-translate"></a>不過度翻譯

在您的應用程式中的某些字串可能不需要轉譯，或至少在需要特別注意的轉譯器。 範例可能包括：

 - Url – 如果您列出 URL，可能或可能不需要的語言來調整。 例如，facebook.com 並不需要它自動偵測在主要站台語言的翻譯。 其他站台都有特定地區設定的內容，您可能想要提供不同的 URL，例如與 yahoo.fr 或 yahoo.it yahoo.com。
 - 電話號碼 – 特別是那些與不同的國家/地區碼或特定語言的呼叫端的數字。
 - 連絡人詳細資料 – 地址和其他資訊可能會因語言或地區設定而異。
 - 商標和產品名稱 – 某些字串不需要轉譯，因為它們永遠寫入相同的語言。

最後，請務必包含轉譯程式的詳細的指示，如果某些字串需要特殊處理。


### <a name="formatted-text"></a>格式化文字

行動裝置應用程式通常不問題因為字串通常不包含豐富的格式化。 不過如果您的應用程式中需要 rich text 格式 （例如粗體或斜體格式） 可確保轉譯程式知道如何為輸入的格式，字串檔案它能正確地儲存，而且正確格式才會顯示給使用者 (ie。 不要不小心讓格式化的代碼本身會向使用者顯示）。



## <a name="translation-tips"></a>轉譯秘訣

轉譯應用程式所使用的字串會被視為在當地語系化過程的一部分。 通常這項工作將外包給翻譯服務，並由多國語言可能不知道您的應用程式或您公司的人員。

下列提示可幫助您產生較容易正確轉譯，並因此改善您當地語系化的應用程式的品質的字串。



### <a name="localize-complete-strings-not-words"></a>完整的字串，不是文字當地語系化

有時開發人員將嘗試要指定單一字或句子 '程式碼片段'，以便它們可以在整個應用程式，重複使用它們的方法。 例如，文字 「 您有 5 則訊息。 」 它們可能會指定下列字串翻譯

**錯誤**:

```csharp
"You have"
"no"
"message"
"messages"
```

然後再嘗試使用字串串連的程式碼建立正確的片語上作業：

**錯誤**:

```csharp
"You have" + " " + numMsgs + " " + "messages"
"You have" + " no " + "messages"
```

**這不建議使用**因為它不一定可用於所有語言，將會很難了解每個短的區段的內容轉譯器。 它也會使重複使用的已翻譯字串，可能會造成問題更新版本會以不同的內容 （和更新然後）。


### <a name="allow-for-parameter-re-ordering"></a>允許參數重新排序

某些程式語言會需要額外的語法，來指定參數的順序，在字串中，但是.NET 已經支援這個概念的已編號的預留位置，因此

**良好**:

```csharp
"a {0} b {1} cde {3}"
```

可能是轉譯的下 （其中的位置和順序預留位置會變更）

```csharp
"{2} {3} f g h {0}"
```

和語彙基元會排序為預期的轉譯器。 請務必要包含的每個預留位置中出現的內容時將字串傳送至轉譯器說明。


### <a name="use-multiple-strings-for-cardinality"></a>使用多個字串的基數

避免等字串`"You have {0} message/s."`使用每個狀態的特定字串來提供較佳使用者體驗：

**良好**:

```csharp
"You have no messages."
"You have 1 messages."
"You have 2 messages."
"You have {0} messages."
```

您必須撰寫程式碼來評估所顯示的數字的應用程式中，選擇適當的字串。 某些平台 （包括 iOS 和 Android） 有內建的功能，可自動選擇最佳的複數字串，根據目前的語言/地區設定的喜好設定。


### <a name="allowing-for-gender"></a>允許的性別

拉丁文語言有時候會使用不同的字，根據主體的性別。 如果您的應用程式知道性別，您應該允許以反映這個翻譯的字串。

即使在英文中，其中字串是指特定人員或應用程式使用者的還有更明顯的情況。 例如，有些網站顯示郵件一樣`"Bob commented on his post"`因此您需要字串男性，女性，和非二進位或未知的性別：

**良好**:

```csharp
"{0} commented on his post"
"{0} commented on her post"
"{0} commented on their post"
```

### <a name="dont-reuse-strings"></a>不要重複使用的字串

或更精確地說，不重複使用字串只是因為字串本身具有不同的用途或意義時，它們很相似。

例如： 假設您有應用程式中的 on/off 開關，而且交換器控制項需要的文字 'on' 和 'off' 當地語系化。 您也會顯示該設定的值其他位置中的文字標籤中的應用程式。 您應該與參數的狀態 （即使它們是相同的字串，在您的預設語言） – 切換顯示使用不同的字串，例如所示：

-   「 On 」 – 顯示在本身的交換器
-   「 關閉 」 – 顯示在本身的交換器
-   「 On 」 – 在標籤中顯示
-   「 關閉 」 – 在標籤中顯示

這會提供最大的彈性的轉譯器：

-   基於設計考量，可能是本身的交換器會使用小寫 「 開啟 」 和 「 關閉 」，但顯示標籤 「 開啟 」 和 「 關閉 」 時，請使用大寫。
-   某些語言可能需要縮寫成符合使用者介面控制項，同時完整單字 （轉譯） 可以出現在標籤中的參數值。
-   或者，對於某些語言呈現您可能是交換器的使用"I"及"O"的文化特性的熟悉度，但是您仍然可以讀取 「 開啟 」 或 「 關閉 」 標籤。

### <a name="translation-services"></a>翻譯服務

#### <a name="machine-translation"></a>機器轉譯

若要建置到應用程式的轉譯功能，請考慮[Azure 轉譯程式文字 API](https://azure.microsoft.com/en-au/services/cognitive-services/translator-text-api/)。

基於測試目的您可以使用許多線上轉譯工具在開發期間，包含應用程式中的某些當地語系化的文字：

- [Bing 翻譯](https://www.bing.com/translator/)
- [Google 翻譯](http://translate.google.com/)

還有許多其他可用。 機器翻譯品質通常不被視為夠好要發行應用程式沒有先檢閱並測試的專業的轉譯器或原生喇叭。

#### <a name="professional-translation"></a>專業轉譯

另外還有專業轉譯服務會接受字串並將它們散發給自己的轉譯器，您提供完成翻譯的費用。

其中一個最服務是[LionBridge](http://www.lionbridge.com/)。 大部分專業人員的服務支援所有常見檔案類型包括字串、 XML、 RESX 和 POT/PO。


## <a name="summary"></a>總結

這篇文章導入了一些概念，您應該要熟悉之前國際化應用程式，然後將當地語系化您的資源，並也討論了如何變更每個平台的語言喜好設定。

各種可能使用 Xamarin 的特定平台和跨平台的國際化技術可以套用這些概念。

繼續閱讀您感興趣的平台的技術詳細資料：

- [Xamarin.Forms](~/xamarin-forms/app-fundamentals/localization/index.md)使用 RESX 檔案的跨平台當地語系化。
- [Xamarin.iOS](~/ios/app-fundamentals/localization/index.md)原生平台當地語系化。
- [Xamarin.Android](~/android/app-fundamentals/localization.md)原生平台當地語系化。



## <a name="related-links"></a>相關連結

- [Apple 的當地語系化概觀](https://developer.apple.com/internationalization/)
- [Android 的當地語系化檢查清單](http://developer.android.com/distribute/tools/localization-checklist.html)
- [開發世界性的應用程式 (MSDN) 的最佳作法](http://msdn.microsoft.com/library/w7x1y988%28v=vs.90%29.aspx)
