---
title: 適用於 iOS 和 macOS 原生類型
description: 本文件說明如何 Xamarin 的統一的 API 將.NET 型別對應到 32 位元和 64 位元原生類型，視編譯目標架構為基礎。
ms.prod: xamarin
ms.assetid: B5237770-0FC3-4B01-9E22-766B35C9A952
author: asb3993
ms.author: amburns
ms.date: 01/25/2016
ms.openlocfilehash: fc2b91a9265fcf09e4f58d5de27a1fdef9350b2d
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34781100"
---
# <a name="native-types-for-ios-and-macos"></a>適用於 iOS 和 macOS 原生類型

Mac 和 iOS 應用程式開發介面使用永遠會在 32 位元平台上，在 64 位元平台上的 64 位元的 32 位元的架構特定的資料類型。

Objective C 的對應，例如`NSInteger`資料型別`int32_t`32 位元系統上和`int64_t`64 位元系統上。

要比對這種行為，我們有統一的 API，我們要取代的先前使用`int`(在.NET 中會定義為一律`System.Int32`) 成新的資料類型： `System.nint`。 您可以將"n"視為意義 「 原生 」，因此原生整數類型的平台。

這些新的資料類型，與相同來源的程式碼會編譯 32 位元和 64 位元架構，根據您編譯旗標。

## <a name="new-data-types"></a>新的資料類型

下表顯示我們的資料型別，以符合這個新 32/64 位元環境中的變更：

|原生類型|32 位元支援類型|64 位元支援類型|
|--- |--- |--- |
|`System.nint`|`System.Int32` (`int`)|`System.Int64` (`long`)|
|`System.nuint`|`System.UInt32` (`uint`)|`System.UInt64` (`ulong`)|
|`System.nfloat`|`System.Single` (`float`)|`System.Double` (`double`)|

我們之所以選擇這些名稱可讓您 C# 程式碼增加或減少看起來會像這樣今天的相同方式。

### <a name="implicit-and-explicit-conversions"></a>隱含和明確轉換

新的資料類型的設計目的被為了讓單一 C# 原始程式檔自然可 32 或 64 位元儲存體，根據主機平台和編譯設定。

這需要我們設計一組隱含和明確轉換平台專屬的資料類型的.NET 點整數和浮點資料類型。

不可能發生資料遺失 （32 位元值儲存在 64 位元空間） 的時，會提供隱含轉換運算子。

當沒有資料遺失的可能性時，提供明確轉換運算子 （64 位元值儲存在 32 個潛在 32 的儲存位置）。

 `int``uint`和`float`全部都是隱含地轉換成`nint`，`nuint`和`nfloat`為 32 位元永遠符合 32 或 64 個位元。

 `nint``nuint`和`nfloat`全部都是隱含地轉換成`long`，`ulong`和`double`32 或 64 位元值一律填滿 64 位元儲存體中。

您必須使用明確的轉換，從`nint`，`nuint`和`nfloat`到`int`，`uint`和`float`因為原生型別可能會持有的儲存體的 64 位元。

您必須使用明確的轉換，從`long`，`ulong`和`double`到`nint`，`nuint`和`nfloat`因為可能只能夠保留的存放裝置的 32 位元的原生類型。

## <a name="coregraphics-types"></a>CoreGraphics 類型

搭配 CoreGraphics 點、 大小以及矩形的資料類型使用 32 或 64 位元，根據裝置執行。  當我們原本繫結 iOS 和 Mac 應用程式開發介面時我們會使用現有的資料結構以符合主機平台的大小發生 (中的資料類型`System.Drawing`)。

移至時**統一**，您必須取代的執行個體`System.Drawing`與其`CoreGraphics`對應項目下, 表所示：

|System.Drawing 中的舊型別|新的資料型別 CoreGraphics|描述|
|--- |--- |--- |
|`RectangleF`|`CGRect`|浮點數的保存點矩形資訊。|
|`SizeF`|`CGSize`|浮點數的保存點 （寬度、 高度） 的大小資訊|
|`PointF`|`CGPoint`|保存浮點數、 點資訊 (X，Y)|

新的其中一個使用舊的資料類型使用浮點數儲存的資料結構中，項目，而`System.nfloat`。

## <a name="related-links"></a>相關連結

- [在跨平台應用程式中使用原生型別](~/cross-platform/macios/native-types-cross-platform.md)
- [傳統的 vs 統一的 API 差異](https://developer.xamarin.com/releases/ios/api_changes/classic-vs-unified-8.6.0/)
