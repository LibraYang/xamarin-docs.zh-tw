---
title: 在 iOS 11 中的架構變更
description: 本文件說明 32 位元應用程式在 iOS 11 中已被的取代。 它討論如何更新目標的 64 位元架構的應用程式。
ms.prod: xamarin
ms.assetid: 55F62F3F-8570-402B-B7D9-2875F76CB946
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 09/13/2016
ms.openlocfilehash: 09d528ceb0654debd7c0ac8818f19c622775eac2
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34787431"
---
# <a name="architecture-changes-in-ios-11"></a>在 iOS 11 中的架構變更

其中一個最大的變更，您應該留意 iOS 11 是已被取代的應用程式中所述的 32 位元支援[Apple](https://developer.apple.com/news/?id=06282017b)按 釋出。 所有新的應用程式與現有的應用程式的更新必須支援 64 位元。 32 位元應用程式**將不會啟動**iOS 11 中。

若要更新適用於 Mac 的 Visual Studio 中的應用程式，請使用下列步驟：

1. 以滑鼠右鍵按一下要開啟的專案名稱**專案選項**。
2. 瀏覽至**iOS 建置** 索引標籤。
3. 設定**支援的架構**下拉式清單可**x86_64**如**偵錯 | iPhoneSimulator**和**版本 | iPhoneSimulator**:

    ![變更模擬器架構下拉式清單](architecture-changes-images/image1.png)

4. 針對 iOS 裝置，將設定變更為**偵錯 | iPhone**並設定**支援的架構**下拉式清單可**ARM64**:

    ![變更裝置架構下拉式清單](architecture-changes-images/image2.png)

5. 將設定變更為**版本 | iPhone**並設定**支援的架構**下拉式清單可**ARM64**。

如需有關 32 位元和 64 位元架構的詳細資訊，請參閱[32/64 位元平台考量](~/cross-platform/macios/32-and-64/index.md#ios)指南。

## <a name="related-links"></a>相關連結

- [什麼是 iOS (Apple) 11 中的新功能](https://developer.apple.com/ios/)
- [更新應用程式市集產品網頁 (Apple)](https://developer.apple.com/app-store/product-page/)
- [正在更新您的應用程式適用於 iOS 11 (WWDC) （影片）](https://developer.apple.com/videos/play/wwdc2017/204/)
