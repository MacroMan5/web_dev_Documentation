# Web Vitals  |  Articles  |  web.dev

**Source URL:** [https://web.dev/articles/vitals?hl=zh-tw](https://web.dev/articles/vitals?hl=zh-tw)  
**Last Updated:** 2025-05-23T01:10:40.026Z  
**Extracted:** 2025-05-31 16:58:10

---

# Web Vitals | Articles | web.dev

發布日期：2020 年 5 月 4 日

提供最佳化的使用者體驗品質，是任何網站長久獲得出色成效的關鍵。無論您是業主、行銷人員或開發人員，網站使用體驗指標都能協助您量化網站體驗，並找出改善之道。

## 總覽

Web Vitals 是 Google 推動的一項計畫，旨在針對不可或缺的品質信號提供統合一致的指南，協助發布商打造出色的網頁使用者體驗。

多年以來，Google 提供多種工具來評估及回報成效。有些開發人員擅長使用這些工具，但其他人則發現，面對眾多工具和指標，他們難以跟上腳步。

網站擁有者不必是成效專家，也能瞭解他們為使用者提供的體驗品質。網站體驗核心指標計畫旨在簡化整體環境，協助網站專注於最重要的指標，也就是**網站體驗核心指標**。

## Core Web Vitals

網站使用體驗核心指標是 Web Vitals 的其中一部分，適用於所有的網頁，所有網站擁有者都應評估這項指標，且會顯示在所有 Google 工具中。每個 Core Web Vitals 都代表使用者體驗的獨特面向，可[在實地測試中](https://web.dev/articles/user-centric-performance-metrics?hl=zh-tw#how_metrics_are_measured)進行評估，並反映出關鍵[以使用者為中心](https://web.dev/articles/user-centric-performance-metrics?hl=zh-tw#how_metrics_are_measured)結果的實際體驗。

構成網站體驗核心指標的指標會隨著時間[演進](#evolving-web-vitals)。目前的設定著重於使用者體驗的三個面向：_載入_、_互動性_和_視覺穩定性_，並包含下列指標 (以及各自的門檻)：

![建議的最大內容繪製門檻](https://web.dev/static/articles/vitals/image/largest-contentful-paint-ea2e6ec5569b6.svg?hl=zh-tw) ![Interaction to Next Paint 門檻建議](https://web.dev/static/articles/vitals/image/inp-thresholds.svg?hl=zh-tw) ![累計版面配置位移門檻建議](https://web.dev/static/articles/vitals/image/cumulative-layout-shift-t-5d49b9b883de4.svg?hl=zh-tw)

*   **[最大內容繪製 (LCP)](https://web.dev/articles/lcp?hl=zh-tw)**：評估_載入_效能。為了提供良好的使用者體驗，LCP 應在網頁開始載入後的 **2.5 秒**內完成。
*   **[Interaction to Next Paint (INP)](https://web.dev/articles/inp?hl=zh-tw)**：評估_互動性_。為了提供良好的使用者體驗，網頁的 INP 應低於 **200 毫秒**。
*   **[累計版面配置位移 (CLS)](https://web.dev/articles/cls?hl=zh-tw)**：評估_視覺穩定性_。為了提供良好的使用者體驗，網頁應維持 CLS 在 **0.1** 以下。

為確保多數使用者都能達到這些指標的建議目標，建議您以網頁載入的**第 75 個百分位數**做為評估門檻，並區分行動裝置和電腦裝置。

評估 Core Web Vitals 符合性時，如果網頁在三項 Core Web Vitals 指標的 75 百分位數達到建議目標，則視為通過。

### 生命週期

Core Web Vitals 追蹤功能的指標會經歷三個階段：實驗、待定和穩定。

![Core Web Vitals 指標的三個生命週期階段，以一系列三角形圖示呈現。從左到右依序為「實驗」、「待定」和「穩定版」。](https://web.dev/static/articles/vitals/image/the-three-lifecycle-phase-0d329be3158f9.svg?hl=zh-tw)

Core Web Vitals 生命週期階段。

每個階段的設計目的，都是要向開發人員傳達如何看待每項指標：

*   **實驗指標**是未來的 Core Web Vitals，可能會根據測試和社群意見進行重大變更。
*   **待定指標**是指未來的 Core Web Vitals，已通過測試和意見回饋階段，且已明確定義穩定版推出時間。
*   **穩定指標**是 Chrome 認為提供優質使用者體驗不可或缺的 Core Web Vitals 指標。

Core Web Vitals 的生命週期如下：

*   [LCP](https://web.dev/articles/lcp?hl=zh-tw)：穩定
*   [CLS](https://web.dev/articles/cls?hl=zh-tw)：穩定
*   [INP](https://web.dev/articles/inp?hl=zh-tw)：穩定版

#### 實驗功能

指標剛開發完成並進入生態系統時，會被視為_實驗指標_。

實驗階段的目的是評估指標的適合度，首先要探索要解決的問題，並可能重複處理先前指標未能解決的問題。舉例來說，[Interaction to Next Paint (INP)](https://web.dev/articles/inp?hl=zh-tw) 最初是做為實驗指標而開發，比[First Input Delay (FID)](https://web.dev/articles/fid?hl=zh-tw) 更能全面解決網站的執行階段效能問題。

Core Web Vitals 生命週期的實驗階段，也旨在找出錯誤，甚至探索對初始定義的變更，讓指標開發過程更具彈性。這也是社群回饋最關鍵的階段。

#### 待處理

當 Chrome 團隊判定實驗指標已收到足夠的意見回饋，且已證明其效用時，就會將其設為_待定指標_。舉例來說，在 2023 年，我們將 INP 從實驗功能升級為待定功能，最終目的是淘汰 FID。

待處理的指標會保留在這個階段至少六個月，讓生態系統有時間進行調整。隨著越來越多開發人員開始使用這項指標，社群意見回饋仍是這個階段的重要環節。

#### 穩定

網站體驗核心指標候選指標定案後，就會成為_穩定指標_。這時指標就能成為 Core Web Vitals。

我們會積極支援穩定的指標，並視情況修正錯誤和變更定義。穩定的 Core Web Vitals 指標一年內不會變動超過一次。我們會在指標的官方文件和變更記錄中，清楚說明 Core Web Vitals 的任何異動。所有評估項目都會納入網站體驗核心指標。

### 評估及回報 Core Web Vitals 的工具

Google 認為 Core Web Vitals 對所有網頁體驗至關重要。因此，我們致力於[在所有熱門工具中](https://web.dev/articles/vitals-tools?hl=zh-tw)顯示這些指標。以下各節將詳細說明哪些工具支援 Core Web Vitals。

#### 用於評估網站體驗核心指標的實地工具

[Chrome 使用者體驗報告](https://developer.chrome.com/docs/crux?hl=zh-tw)會針對每項 Core Web Vital 收集去識別化實際使用者評估資料。有了這項資料，網站擁有者就能快速評估自家網站的效能，不必手動在網頁上加入分析工具，而且還能支援 [Chrome DevTools](https://developer.chrome.com/docs/devtools/performance/overview?hl=zh-tw#compare)、[PageSpeed Insights](https://pagespeed.web.dev/?hl=zh-tw) 和 Search Console 的 [Core Web Vitals 報告](https://support.google.com/webmasters/answer/9205520?hl=zh-tw) 等工具。

Chrome 使用者體驗報告提供的資料可快速評估網站效能，但不會提供詳細的個別網頁檢視遙測資料，而這類資料通常是準確診斷、監控及快速回應回歸現象的必要條件。因此，我們強烈建議網站自行設定實際使用者監控功能。

#### 使用 JavaScript 評估 Core Web Vitals

每項 Core Web Vitals 都可以使用標準網路 API 在 JavaScript 中評估。

評估所有網站使用體驗核心指標最簡單的方法，就是使用 [web-vitals](https://github.com/GoogleChrome/web-vitals) JavaScript 程式庫，這是一個可直接用於實際環境的簡易包裝函式，可在底層網路 API 中評估各項指標，並與先前列出的所有 Google 工具回報的結果相符。

使用 [web-vitals](https://github.com/GoogleChrome/web-vitals) 程式庫，您可以透過呼叫單一函式來評估每個指標。如需完整的[用法](https://github.com/GoogleChrome/web-vitals#usage)和 [API](https://github.com/GoogleChrome/web-vitals#api) 詳細資料，請參閱說明文件。

```
import {onCLS, onINP, onLCP} from 'web-vitals';

function sendToAnalytics(metric) {
  const body = JSON.stringify(metric);
  // Use `navigator.sendBeacon()` if available, falling back to `fetch()`.
  (navigator.sendBeacon && navigator.sendBeacon('/analytics', body)) ||
    fetch('/analytics', {body, method: 'POST', keepalive: true});
}

onCLS(sendToAnalytics);
onINP(sendToAnalytics);
onLCP(sendToAnalytics);
```

設定網站使用 [web-vitals](https://github.com/GoogleChrome/web-vitals) 程式庫，以便評估並將網站使用體驗核心指標資料傳送至 Analytics 終端後，下一步就是匯總資料並製作報表，瞭解網頁是否達到至少 75% 網頁瀏覽量的建議門檻。

雖然部分數據分析供應商已內建網站使用體驗核心指標的支援功能，但即使是未內建基本自訂指標功能的供應商，也應該會在工具中提供網站使用體驗核心指標的評估功能。

如果開發人員偏好直接使用基礎網頁 API 來評估這些指標，可以參考下列指標指南，瞭解實作詳細資訊：

*   [在 JavaScript 中評估 LCP](https://web.dev/articles/lcp?hl=zh-tw#measure_lcp_in_javascript)
*   [在 JavaScript 中評估 INP](https://web.dev/articles/inp?hl=zh-tw#how-to-measure-inp)
*   [在 JavaScript 中評估 CLS](https://web.dev/articles/cls?hl=zh-tw#measure_cls_in_javascript)

如需有關使用熱門分析服務或自家數據分析工具評估這些指標的其他指引，請參閱「[在實務中評估網站使用體驗指標的最佳做法](https://web.dev/articles/vitals-field-measurement-best-practices?hl=zh-tw)」。

#### 用於評估 Core Web Vitals 的實驗室工具

雖然所有 Core Web Vitals 指標都是以實地指標為優先，但許多指標也可以在實驗室中評估。

實驗室測量是測試功能效能的最佳方式，可在功能發布給使用者前進行測試。這也是在效能迴歸發生前，捕捉迴歸的最佳方法。

您可以使用下列工具，在實驗室環境中評估 Core Web Vitals：

雖然實驗室測試對於提供優質體驗至關重要，但無法取代實地測試。

網站的成效可能會因使用者的裝置功能、網路狀況、裝置上執行的其他程序，以及使用者與網頁互動的方式而有大幅差異。事實上，每個 Core Web Vitals 指標的分數都可能受到使用者互動影響。只有實地測試才能準確掌握全貌。

### 改善分數的建議

以下指南提供針對各 Core Web Vitals 的最佳化建議，協助您改善網頁：

*   [最佳化 LCP](https://web.dev/articles/optimize-lcp?hl=zh-tw)
*   [最佳化 INP](https://web.dev/articles/optimize-inp?hl=zh-tw)
*   [最佳化 CLS](https://web.dev/articles/optimize-cls?hl=zh-tw)

改善 Core Web Vitals 的方法有很多種，每種方法在每種情況下對影響、關聯性和易用性的影響程度也不同。請參閱「[改善 Core Web Vitals 最有效的方式](https://web.dev/articles/top-cwv?hl=zh-tw)」，查看 Chrome 團隊提供的最佳建議。

## 其他網站體驗指標

雖然 Core Web Vitals 是瞭解及提供優質使用者體驗的關鍵指標，但還有其他輔助指標。

這些其他指標可做為代理指標，或做為三項 Core Web Vitals 的輔助指標，協助擷取更完整的使用體驗，或協助診斷特定問題。

舉例來說，指標「首次位元組時間 (TTFB)」[](https://web.dev/articles/ttfb?hl=zh-tw)和「首次顯示內容所需時間 (FCP)」[](https://web.dev/articles/fcp?hl=zh-tw) 都是_載入_體驗的重要面向，且兩者都很適合用於診斷 LCP 問題 (分別是 [伺服器回應時間](https://web.dev/articles/overloaded-server?hl=zh-tw)或[轉譯阻斷資源](https://developer.chrome.com/docs/lighthouse/performance/render-blocking-resources?hl=zh-tw))。

同樣地，[總阻斷時間 (TBT)](https://web.dev/articles/tbt?hl=zh-tw) 這類實驗室指標，對於找出並診斷可能影響 INP 的潛在_互動性_問題，也非常重要。不過，這項指標不屬於 Core Web Vitals 套件，因為無法在實地測量，也不反映[以使用者為中心](https://web.dev/articles/user-centric-performance-metrics?hl=zh-tw#how_metrics_are_measured)的結果。

## 網站體驗指標異動

網站使用體驗核心指標和網站使用體驗指標，是目前開發人員用來評估網站使用者體驗品質的最佳信號，但這些信號並非完美無缺，未來可能會進行改善或新增。

**網站使用體驗核心指標**與所有網頁相關，並在相關的 Google 工具中顯示。這些指標的變更會帶來廣泛影響，因此開發人員應預期網站使用體驗核心指標的定義和門檻會保持穩定，且更新會提前通知，並以每年的週期進行。

其他 Web Vitals 通常是特定情境或工具專屬，且可能比 Core Web Vitals 更偏向實驗性質。因此，相關定義和門檻可能會更頻繁地變更。

對於所有 Web Vitals，我們會在這個公開的[變更記錄](http://bit.ly/chrome-speed-metrics-changelog)中清楚記錄變更。

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
