# 📋 HealthGo - 智慧健康管理解決方案

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Kotlin](https://img.shields.io/badge/Language-Kotlin-purple.svg)
![Architecture](https://img.shields.io/badge/Architecture-MVVM-orange.svg)
![Jetpack Compose](https://img.shields.io/badge/UI-Jetpack_Compose-green.svg)

**HealthGo** 是一款專為忙碌現代人設計的健康追蹤 App，結合數據視覺化與自動化提醒功能。本專案核心目標在於解決使用者「紀錄不便」與「數據難以解讀」的痛點，並展現現代化 Android 開發的最佳實踐。

---

## 🚀 技術亮點 (Technical Highlights)

* **語言與基礎**: 100% **Kotlin** 開發，深度使用 **Coroutines & Flow** 處理非同步任務。
* **架構設計**: 採用 **MVVM**，確保程式碼具備高度的可測試性與維護性。
* **介面開發**: 使用 **Jetpack Compose** 建構聲明式 UI，並導入 **Material 3** 動態色彩設計。
* **數據持久化**: 透過 **Room Database** 實現離線優先策略，並使用 **DataStore** 儲存使用者偏好。
* **依賴注入**: 使用 **Hilt (Dagger)** 管理組件生命週期，實現解耦。

---

## 🛠 解決的關鍵問題 (Problem & Solution)

### 1. 複雜數據的即時渲染優化
* **痛點**: 歷史紀錄數據量龐大時，UI 列表滾動會產生明顯卡頓。
* **解決方案**: 導入 **Paging 3** 分頁載入技術，搭配 **DiffUtil** 僅更新變動項目，顯著降低記憶體佔用並提升滾動流暢度。

### 2. 異步數據同步的資料一致性
* **痛點**: 多個後台任務同時寫入資料庫時，容易產生數據競爭 (Race Condition)。
* **解決方案**: 建立 **Single Source of Truth (SSOT)**，利用 **Kotlin Flow** 的 `stateIn` 操作符，確保 UI 永遠只反映本地資料庫的最準確狀態。

### 3. 省電機制下的精準提醒
* **痛點**: Android Doze Mode 常導致健康提醒功能失效。
* **解決方案**: 結合 **AlarmManager** 處理精準提醒，並使用 **WorkManager** 負責彈性的數據備份任務，平衡效能與電力消耗。

---

## 🏗 專案架構 (Project Architecture)

專案嚴格遵循職責分離原則，分為以下層級：

```text
app
 ├── data
 │    ├── repository  # 數據調度與決策中心
 │    ├── local       # Room Database, DAO
 │    └── remote      # Retrofit API 介面定義
 ├── domain
 │    ├── model       # 業務實體對象
 │    └── usecase     # 核心業務邏輯處理
 └── ui
      ├── viewmodel   # 狀態管理與邏輯
      └── screens     # Compose UI 元件
