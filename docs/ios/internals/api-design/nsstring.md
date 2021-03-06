---
title: 在 Xamarin.iOS 和 Xamarin.Mac NSString
description: 本文件說明如何 Xamarin.iOS 無障礙地 NSString 將物件轉換成 C# 字串物件，這不會發生時。
ms.prod: xamarin
ms.assetid: 785744B3-42E2-4590-8F41-435325E609B9
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/21/2017
ms.openlocfilehash: baf36700ab4d608296a9a67e234ce613da9ca077
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34786086"
---
# <a name="nsstring-in-xamarinios-and-xamarinmac"></a>在 Xamarin.iOS 和 Xamarin.Mac NSString

使用 api 公開的原生.NET 字串型別，會呼叫 Xamarin.iOS 和 Xamarin.Mac 設計的`string`、 C# 中的字串處理與其他.NET 程式設計語言，並公開 （expose） 做為資料類型，而不是API所公開的字串`NSString`資料型別。

這表示一種特殊類型中的 開發人員應該不需要保留要用於呼叫 Xamarin.iOS 和 Xamarin.Mac API （整合） 的字串 (`Foundation.NSString`)，他們可以繼續使用單聲道的`System.String`所有作業，以及每當API Xamarin.iOS 或 Xamarin.Mac 中的需要字串時，我們的 API 繫結會負責封送處理資訊。

例如，OBJECTIVE-C 「 文字 」 上的屬性`UILabel`型別的`NSString`，宣告如下：

```objc
@property(nonatomic, copy) NSString *text
```

這會顯示在 Xamarin.iOS 為︰

```csharp
class UILabel {
    public string Text { get; set; }
}
```

在幕後，這個屬性的實作封送處理為 C# 字串`NSString`呼叫`objc_msgSend`相同的方式，像是 Objective C 的方法。

第三方 OBJECTIVE-C api，不會耗用少數`NSString`，但改為使用在 C 字串 ("*char*")。 在這些情況下，您仍然可以使用 C# 字串資料類型，但您必須使用[[PlainString]](~/cross-platform/macios/binding/objective-c-libraries.md)屬性告知繫結產生器，此字串應該不會封送處理為`NSString`，但改為在 C 字串。

 <a name="Exceptions_to_the_Rule" />

## <a name="exceptions-to-the-rule"></a>規則的例外狀況

在 Xamarin.iOS 和 Xamarin.Mac 中，我們進行了這個規則的例外狀況。 決定當我們公開`string`s，和當我們做出 except 和公開`NSString`s，會`NSString`方法可能會進行指標比較，而不是內容的比較。

這種情形時 OBJECTIVE-C Api 會使用公用`NSString`常數做為權杖，代表某些動作，而不是比較字串的實際內容。

在這些情況下，`NSString`應用程式開發介面已公開，且有少數的 Api，此行為。 您也會發現 NSString 屬性會公開某些類別中。 這些`NSString`屬性會公開為通知等項目。 這些是屬性通常看起來像這樣：

```csharp
class Foo {
     public NSString FooNotification { get; }
}
```
通知是金鑰，用於`NSNotification`當您想要註冊特定事件正在廣播由執行階段類別。

索引鍵通常看起來像這樣：

```csharp
class Foo {
     public NSString FooBarKey { get; }
}
```

另一個位置其中`NSString`s 會公開在 API 為語彙基元，可用做為參數，在 iOS 中的特定應用程式開發介面或 OS X 採用`NSDictionary`物件做為參數。 字典通常包含`NSString`索引鍵。 Xamarin.iOS，依照慣例，名稱與靜態`NSString`將 「 金鑰 」 名稱的屬性。
