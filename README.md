<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover" />
  <title>沖縄しおり 11/21〜11/24</title>

  <!-- iOS ホーム画面追加 (PWA) 用メタタグ -->
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <meta name="apple-mobile-web-app-title" content="沖縄しおり" />
  <meta name="theme-color" content="#0284c7" />
  <link id="appleTouchIcon" rel="apple-touch-icon" href="" />

  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Noto+Sans+JP:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <script src="https://cdn.tailwindcss.com/3.4.17"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['Inter', 'Noto Sans JP', 'sans-serif'],
          },
        },
      },
    };
  </script>
  <style>
    :root {
      --safe-top: env(safe-area-inset-top, 0px);
      --safe-bottom: env(safe-area-inset-bottom, 0px);
    }
    html, body {
      font-family: 'Inter', 'Noto Sans JP', -apple-system, BlinkMacSystemFont, sans-serif;
      -webkit-tap-highlight-color: transparent;
      overscroll-behavior-y: contain;
    }
    .pt-safe {
      padding-top: calc(12px + var(--safe-top));
    }
    .pb-safe-nav {
      padding-bottom: calc(10px + var(--safe-bottom));
    }
    .pb-content {
      padding-bottom: calc(96px + var(--safe-bottom));
    }
    .no-scrollbar::-webkit-scrollbar {
      display: none;
    }
    .no-scrollbar {
      -ms-overflow-style: none;
      scrollbar-width: none;
    }
    @keyframes slideUp {
      from { transform: translateY(100%); opacity: 0.6; }
      to { transform: translateY(0); opacity: 1; }
    }
    .animate-slide-up {
      animation: slideUp 0.22s cubic-bezier(0.16, 1, 0.3, 1);
    }
  </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-[100dvh] w-full antialiased selection:bg-sky-200">

  <!-- Top App Header -->
  <header class="sticky top-0 z-30 bg-gradient-to-r from-sky-600 via-cyan-600 to-teal-500 text-white shadow-md pt-safe">
    <div class="w-full max-w-3xl mx-auto px-4 pb-3 flex items-center justify-between gap-2">
      <div class="min-w-0">
        <div class="flex items-center gap-1.5 text-xs font-medium text-sky-100">
          <span>🌺 2026.11.21(土) – 11.24(火)</span>
          <span class="px-1.5 py-0.5 rounded bg-white/20 text-[10px] font-semibold">3泊4日</span>
        </div>
        <h1 class="text-lg font-bold tracking-tight truncate">沖縄旅のしおり</h1>
      </div>
      <div class="flex items-center gap-1.5 shrink-0">
        <button id="btnPwaGuide" type="button" title="iPhoneホーム画面に追加する方法"
          class="p-2 rounded-xl bg-white/15 hover:bg-white/25 active:scale-95 transition flex items-center gap-1 text-xs font-medium">
          <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z" />
          </svg>
          <span class="hidden sm:inline">アプリ化</span>
        </button>
        <button id="btnDataMenu" type="button" title="バックアップ・設定"
          class="p-2 rounded-xl bg-white/15 hover:bg-white/25 active:scale-95 transition">
          <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4" />
          </svg>
        </button>
      </div>
    </div>
  </header>

  <!-- Main Content -->
  <main class="w-full max-w-3xl mx-auto px-4 pt-4 pb-content">

    <!-- ==================== SCHEDULE VIEW ==================== -->
    <section id="viewSchedule" class="space-y-4">
      <!-- Live Okinawa Weather Strip -->
      <div class="bg-white rounded-2xl p-3.5 shadow-xs border border-slate-200/80">
        <div class="flex items-center justify-between mb-2">
          <div class="flex items-center gap-1.5">
            <span class="text-xs font-bold text-slate-700">🌤️ 那覇の天気・気温（リアルタイム予報）</span>
          </div>
          <button id="btnRefreshWeather" type="button" class="text-[11px] font-semibold text-sky-600 hover:text-sky-700 flex items-center gap-1 transition">
            <span>更新</span>
          </button>
        </div>
        <div id="weatherStrip" class="grid grid-cols-4 gap-2 text-center">
          <div class="col-span-4 py-2 text-xs text-slate-400">天気を取得中...</div>
        </div>
      </div>

      <!-- Day Filter Pills -->
      <div class="flex items-center gap-2 overflow-x-auto no-scrollbar pb-1" id="dayFilterBar">
        <!-- Rendered by JS -->
      </div>

      <!-- Day Summary / Add Button -->
      <div class="flex items-center justify-between gap-2">
        <p id="scheduleCountText" class="text-xs font-medium text-slate-500">読み込み中...</p>
        <button id="btnAddSchedule" type="button"
          class="inline-flex items-center gap-1.5 px-3.5 py-2 rounded-xl bg-sky-600 hover:bg-sky-700 active:scale-95 text-white text-xs font-semibold shadow-sm transition">
          <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4" />
          </svg>
          予定を追加
        </button>
      </div>

      <!-- Timeline List -->
      <div id="scheduleList" class="space-y-4">
        <!-- Rendered by JS -->
      </div>
    </section>

    <!-- ==================== PACKING LIST VIEW ==================== -->
    <section id="viewPacking" class="hidden space-y-4">
      <!-- Progress Card -->
      <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200/80">
        <div class="flex items-center justify-between mb-2">
          <div>
            <h2 class="text-sm font-bold text-slate-800">持ち物チェック進捗</h2>
            <p id="packingProgressText" class="text-xs text-slate-500 mt-0.5">0 / 0 個完了</p>
          </div>
          <span id="packingPercentBadge" class="px-2.5 py-1 rounded-full text-xs font-bold bg-sky-50 text-sky-700 border border-sky-200">
            0%
          </span>
        </div>
        <div class="w-full h-2.5 bg-slate-100 rounded-full overflow-hidden">
          <div id="packingProgressBar" class="h-full bg-gradient-to-r from-sky-500 to-teal-400 rounded-full transition-all duration-300" style="width: 0%"></div>
        </div>
      </div>

      <!-- Quick Add Form -->
      <form id="quickAddPackingForm" class="flex gap-2">
        <input id="quickPackingTitle" type="text" placeholder="持ち物を追加（例：日焼け止め）" required
          class="flex-1 min-w-0 px-3.5 py-2.5 rounded-xl bg-white border border-slate-200 text-sm focus:outline-none focus:ring-2 focus:ring-sky-500 focus:border-transparent shadow-sm" />
        <select id="quickPackingCat"
          class="px-2.5 py-2.5 rounded-xl bg-white border border-slate-200 text-xs font-medium text-slate-700 focus:outline-none focus:ring-2 focus:ring-sky-500 shadow-sm">
          <option value="必需品">必需品</option>
          <option value="ヲタク">ヲタク</option>
          <option value="衣類">衣類</option>
          <option value="ガジェット">ガジェット</option>
          <option value="その他">その他</option>
        </select>
        <button type="submit"
          class="px-3.5 py-2.5 rounded-xl bg-sky-600 hover:bg-sky-700 active:scale-95 text-white text-xs font-semibold shadow-sm transition shrink-0">
          追加
        </button>
      </form>

      <!-- Category Filter & Unchecked Toggle -->
      <div class="flex items-center justify-between gap-2">
        <div id="packingCategoryBar" class="flex items-center gap-1.5 overflow-x-auto no-scrollbar pb-1 flex-1">
          <!-- Rendered by JS -->
        </div>
      </div>

      <div class="flex items-center justify-between text-xs">
        <label class="inline-flex items-center gap-2 cursor-pointer select-none text-slate-600 font-medium">
          <input id="toggleUncheckedOnly" type="checkbox" class="w-4 h-4 rounded text-sky-600 focus:ring-sky-500 border-slate-300" />
          未チェックのみ表示
        </label>
        <button id="btnResetChecks" type="button" class="text-slate-400 hover:text-rose-600 font-medium transition">
          チェックをリセット
        </button>
      </div>

      <!-- Packing Items List -->
      <div id="packingList" class="space-y-2.5">
        <!-- Rendered by JS -->
      </div>
    </section>

  </main>

  <!-- Bottom Tab Navigation -->
  <nav class="fixed bottom-0 inset-x-0 z-30 bg-white/95 backdrop-blur-md border-t border-slate-200 pb-safe-nav">
    <div class="w-full max-w-3xl mx-auto grid grid-cols-2">
      <button id="tabSchedule" type="button"
        class="flex flex-col items-center justify-center py-2.5 text-sky-600 font-semibold transition">
        <svg class="w-6 h-6 mb-0.5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
        </svg>
        <span class="text-[11px]">タイムスケジュール</span>
      </button>
      <button id="tabPacking" type="button"
        class="flex flex-col items-center justify-center py-2.5 text-slate-400 hover:text-slate-600 font-medium transition">
        <svg class="w-6 h-6 mb-0.5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-6 9l2 2 4-4" />
        </svg>
        <span class="text-[11px]">持ち物リスト</span>
      </button>
    </div>
  </nav>

  <!-- ==================== MODALS ==================== -->

  <!-- Schedule Add/Edit Modal -->
  <div id="scheduleModal" class="fixed inset-0 z-50 hidden bg-slate-900/50 backdrop-blur-xs flex items-end sm:items-center justify-center p-0 sm:p-4">
    <div class="bg-white w-full sm:max-w-md rounded-t-3xl sm:rounded-2xl shadow-xl p-5 space-y-4 animate-slide-up max-h-[90vh] overflow-y-auto">
      <div class="flex items-center justify-between">
        <h3 id="scheduleModalTitle" class="text-base font-bold text-slate-800">予定を追加</h3>
        <button type="button" data-close-modal="scheduleModal" class="p-1.5 rounded-lg text-slate-400 hover:bg-slate-100">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>
      <form id="scheduleForm" class="space-y-3">
        <input type="hidden" id="schedId" />
        <div class="grid grid-cols-2 gap-3">
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">日付</label>
            <select id="schedDay" required class="w-full px-3 py-2 rounded-xl border border-slate-200 text-sm bg-slate-50 focus:bg-white focus:ring-2 focus:ring-sky-500 focus:outline-none">
              <option value="2026-11-21">11/21 (土)</option>
              <option value="2026-11-22">11/22 (日)</option>
              <option value="2026-11-23">11/23 (月・祝)</option>
              <option value="2026-11-24">11/24 (火)</option>
            </select>
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">カテゴリ</label>
            <select id="schedCategory" required class="w-full px-3 py-2 rounded-xl border border-slate-200 text-sm bg-slate-50 focus:bg-white focus:ring-2 focus:ring-sky-500 focus:outline-none">
              <option value="移動">✈️ 移動</option>
              <option value="宿泊">🏨 宿泊</option>
              <option value="イベント">🎤 イベント</option>
              <option value="食事">🍽️ 食事</option>
              <option value="観光">🏝️ 観光</option>
              <option value="その他">📝 その他</option>
            </select>
          </div>
        </div>
        <div class="grid grid-cols-2 gap-3">
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">開始時刻</label>
            <input id="schedTime" type="time" required class="w-full px-3 py-2 rounded-xl border border-slate-200 text-sm bg-slate-50 focus:bg-white focus:ring-2 focus:ring-sky-500 focus:outline-none" />
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">終了時刻（任意）</label>
            <input id="schedEndTime" type="time" class="w-full px-3 py-2 rounded-xl border border-slate-200 text-sm bg-slate-50 focus:bg-white focus:ring-2 focus:ring-sky-500 focus:outline-none" />
          </div>
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">予定タイトル</label>
          <input id="schedTitle" type="text" placeholder="例：首里城観光、国際通りで夕食" required
            class="w-full px-3 py-2 rounded-xl border border-slate-200 text-sm bg-slate-50 focus:bg-white focus:ring-2 focus:ring-sky-500 focus:outline-none" />
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">場所・メモ（任意）</label>
          <textarea id="schedMemo" rows="2" placeholder="住所、予約番号、持ち物メモなど"
            class="w-full px-3 py-2 rounded-xl border border-slate-200 text-sm bg-slate-50 focus:bg-white focus:ring-2 focus:ring-sky-500 focus:outline-none"></textarea>
        </div>
        <div class="flex items-center justify-between gap-2 pt-2">
          <button id="btnDeleteSchedule" type="button" class="hidden px-4 py-2.5 rounded-xl bg-rose-50 hover:bg-rose-100 text-rose-600 text-xs font-semibold transition">
            削除する
          </button>
          <div class="flex gap-2 ml-auto">
            <button type="button" data-close-modal="scheduleModal" class="px-4 py-2.5 rounded-xl bg-slate-100 hover:bg-slate-200 text-slate-600 text-xs font-semibold transition">
              キャンセル
            </button>
            <button type="submit" class="px-5 py-2.5 rounded-xl bg-sky-600 hover:bg-sky-700 text-white text-xs font-semibold shadow-sm transition">
              保存する
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>

  <!-- Packing Edit Modal -->
  <div id="packingModal" class="fixed inset-0 z-50 hidden bg-slate-900/50 backdrop-blur-xs flex items-end sm:items-center justify-center p-0 sm:p-4">
    <div class="bg-white w-full sm:max-w-md rounded-t-3xl sm:rounded-2xl shadow-xl p-5 space-y-4 animate-slide-up">
      <div class="flex items-center justify-between">
        <h3 class="text-base font-bold text-slate-800">持ち物を編集</h3>
        <button type="button" data-close-modal="packingModal" class="p-1.5 rounded-lg text-slate-400 hover:bg-slate-100">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>
      <form id="packingEditForm" class="space-y-3">
        <input type="hidden" id="packId" />
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">アイテム名</label>
          <input id="packTitle" type="text" required class="w-full px-3 py-2 rounded-xl border border-slate-200 text-sm bg-slate-50 focus:bg-white focus:ring-2 focus:ring-sky-500 focus:outline-none" />
        </div>
        <div class="grid grid-cols-2 gap-3">
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">カテゴリ</label>
            <select id="packCategory" class="w-full px-3 py-2 rounded-xl border border-slate-200 text-sm bg-slate-50 focus:bg-white focus:ring-2 focus:ring-sky-500 focus:outline-none">
              <option value="必需品">必需品</option>
              <option value="ヲタク">ヲタク</option>
              <option value="衣類">衣類</option>
              <option value="ガジェット">ガジェット</option>
              <option value="その他">その他</option>
            </select>
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">数量（任意）</label>
            <input id="packQty" type="text" placeholder="例：3日分、2本" class="w-full px-3 py-2 rounded-xl border border-slate-200 text-sm bg-slate-50 focus:bg-white focus:ring-2 focus:ring-sky-500 focus:outline-none" />
          </div>
        </div>
        <div class="flex items-center justify-between gap-2 pt-2">
          <button id="btnDeletePacking" type="button" class="px-4 py-2.5 rounded-xl bg-rose-50 hover:bg-rose-100 text-rose-600 text-xs font-semibold transition">
            削除する
          </button>
          <div class="flex gap-2">
            <button type="button" data-close-modal="packingModal" class="px-4 py-2.5 rounded-xl bg-slate-100 hover:bg-slate-200 text-slate-600 text-xs font-semibold transition">
              キャンセル
            </button>
            <button type="submit" class="px-5 py-2.5 rounded-xl bg-sky-600 hover:bg-sky-700 text-white text-xs font-semibold shadow-sm transition">
              保存する
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>

  <!-- iOS PWA Add to Home Screen Guide Modal -->
  <div id="pwaGuideModal" class="fixed inset-0 z-50 hidden bg-slate-900/50 backdrop-blur-xs flex items-end sm:items-center justify-center p-0 sm:p-4">
    <div class="bg-white w-full sm:max-w-md rounded-t-3xl sm:rounded-2xl shadow-xl p-5 space-y-4 animate-slide-up max-h-[90vh] overflow-y-auto">
      <div class="flex items-center justify-between">
        <h3 class="text-base font-bold text-slate-800">📱 iPhoneでアプリとして使う手順</h3>
        <button type="button" data-close-modal="pwaGuideModal" class="p-1.5 rounded-lg text-slate-400 hover:bg-slate-100">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>
      <div class="space-y-3 text-xs text-slate-600 leading-relaxed">
        <div class="p-3 rounded-xl bg-sky-50 border border-sky-100 text-sky-900">
          このHTMLファイルを公開URL（Firebase Hosting や GitHub Pages など）に配置し、iPhoneの <strong>Safari</strong> で開くとホーム画面に追加できます。
        </div>
        <ol class="space-y-2.5 list-decimal list-inside">
          <li>iPhoneの <strong>Safari</strong> でこのページのURLを開きます。</li>
          <li>画面下部の <strong>共有ボタン（□に↑のアイコン）</strong> をタップします。</li>
          <li>下にスクロールして <strong>「ホーム画面に追加」</strong> をタップします。</li>
          <li>右上の <strong>「追加」</strong> をタップすると、アプリアイコンがホーム画面に作成されます。</li>
        </ol>
        <p class="text-[11px] text-slate-500">
          ※入力した予定と持ち物は端末内のブラウザ（localStorage）に自動保存されます。
        </p>
      </div>
      <div class="grid grid-cols-2 gap-2">
        <button id="btnDownloadHtml" type="button" class="py-2.5 px-3 rounded-xl bg-teal-600 hover:bg-teal-700 text-white text-xs font-semibold transition">
          HTMLを保存
        </button>
        <button id="btnCopyHtml" type="button" class="py-2.5 px-3 rounded-xl bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-semibold transition">
          HTMLをコピー
        </button>
      </div>
      <button type="button" data-close-modal="pwaGuideModal" class="w-full py-2.5 rounded-xl bg-sky-600 hover:bg-sky-700 text-white text-xs font-semibold transition">
        閉じる
      </button>
    </div>
  </div>

  <!-- Data / Backup Modal -->
  <div id="dataMenuModal" class="fixed inset-0 z-50 hidden bg-slate-900/50 backdrop-blur-xs flex items-end sm:items-center justify-center p-0 sm:p-4">
    <div class="bg-white w-full sm:max-w-md rounded-t-3xl sm:rounded-2xl shadow-xl p-5 space-y-4 animate-slide-up max-h-[90vh] overflow-y-auto">
      <div class="flex items-center justify-between">
        <h3 class="text-base font-bold text-slate-800">データ管理・バックアップ</h3>
        <button type="button" data-close-modal="dataMenuModal" class="p-1.5 rounded-lg text-slate-400 hover:bg-slate-100">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>
      <div class="space-y-3">
        <button id="btnExportJson" type="button" class="w-full py-2.5 px-4 rounded-xl bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-semibold flex items-center justify-center gap-2 transition">
          JSONデータをコピー（バックアップ）
        </button>
        <div class="space-y-1.5">
          <label class="block text-xs font-semibold text-slate-600">JSONデータから復元</label>
          <textarea id="importJsonInput" rows="3" placeholder="バックアップしたJSONを貼り付け"
            class="w-full px-3 py-2 rounded-xl border border-slate-200 text-xs bg-slate-50 focus:bg-white focus:ring-2 focus:ring-sky-500 focus:outline-none"></textarea>
          <button id="btnImportJson" type="button" class="w-full py-2.5 px-4 rounded-xl bg-sky-600 hover:bg-sky-700 text-white text-xs font-semibold transition">
            貼り付けたデータで復元する
          </button>
        </div>
        <hr class="border-slate-200" />
        <button id="btnResetAllData" type="button" class="w-full py-2.5 px-4 rounded-xl bg-rose-50 hover:bg-rose-100 text-rose-600 text-xs font-semibold transition">
          初期データ（予約・テンプレート）に戻す
        </button>
      </div>
    </div>
  </div>

  <!-- Confirm Modal (replaces window.confirm) -->
  <div id="confirmModal" class="fixed inset-0 z-50 hidden bg-slate-900/50 backdrop-blur-xs flex items-center justify-center p-4">
    <div class="bg-white w-full max-w-xs rounded-2xl shadow-xl p-5 space-y-4">
      <p id="confirmMessage" class="text-sm font-medium text-slate-700 text-center"></p>
      <div class="grid grid-cols-2 gap-2">
        <button id="btnConfirmCancel" type="button" class="py-2 rounded-xl bg-slate-100 hover:bg-slate-200 text-slate-600 text-xs font-semibold transition">
          キャンセル
        </button>
        <button id="btnConfirmOk" type="button" class="py-2 rounded-xl bg-rose-600 hover:bg-rose-700 text-white text-xs font-semibold transition">
          実行する
        </button>
      </div>
    </div>
  </div>

  <!-- Toast -->
  <div id="toast" class="fixed top-16 left-1/2 -translate-x-1/2 z-50 hidden px-4 py-2 rounded-full bg-slate-900/90 text-white text-xs font-medium shadow-lg transition">
  </div>

  <script>
    (function () {
      const STORAGE_KEY = 'okinawa_trip_2026_11_v12';

      const DAYS = [
        { id: 'all', label: 'すべて' },
        { id: '2026-11-21', label: '11/21(土)', short: 'Day 1 · 11/21(土)' },
        { id: '2026-11-22', label: '11/22(日)', short: 'Day 2 · 11/22(日)' },
        { id: '2026-11-23', label: '11/23(月)', short: 'Day 3 · 11/23(月・祝)' },
        { id: '2026-11-24', label: '11/24(火)', short: 'Day 4 · 11/24(火)' },
      ];

      const CAT_META = {
        '移動': { icon: '✈️', badge: 'bg-sky-50 text-sky-700 border-sky-200' },
        '宿泊': { icon: '🏨', badge: 'bg-indigo-50 text-indigo-700 border-indigo-200' },
        'イベント': { icon: '🎤', badge: 'bg-pink-50 text-pink-700 border-pink-200' },
        '食事': { icon: '🍽️', badge: 'bg-amber-50 text-amber-700 border-amber-200' },
        '観光': { icon: '🏝️', badge: 'bg-teal-50 text-teal-700 border-teal-200' },
        'その他': { icon: '📝', badge: 'bg-slate-100 text-slate-700 border-slate-200' },
      };

      const PACK_CATS = ['すべて', '必需品', 'ヲタク', '衣類', 'ガジェット', 'その他'];

      const DEFAULT_DATA = {
        schedules: [
          {
            id: 's1',
            day: '2026-11-21',
            time: '06:40',
            endTime: '09:25',
            title: 'ANA NH993（羽田T2 → 那覇）',
            category: '移動',
            memo: '予約番号: FT25O2 / 羽田空港 第2ターミナル発（所要2時間45分・手荷物預けは30分前まで）',
            done: false,
          },
          {
            id: 's1a',
            day: '2026-11-21',
            time: '09:50',
            endTime: '10:18',
            title: '🚃 移動：那覇空港 → ラーメン二郎 沖縄店',
            category: '移動',
            memo: '手段：ゆいレール（那覇空港→牧志）＋徒歩12分 / 所要：約28分 / 交通費：320円',
            done: false,
          },
          {
            id: 's1b',
            day: '2026-11-21',
            time: '11:00',
            endTime: '12:00',
            title: '🍜 ラーメン二郎 沖縄店',
            category: '食事',
            memo: '沖縄県那覇市壺屋1-6-16（牧志駅徒歩約12分）/ 土曜昼営業 10:30〜14:30頃（材料切れ注意）',
            done: false,
          },
          {
            id: 's1c',
            day: '2026-11-21',
            time: '14:30',
            endTime: '14:51',
            title: '🚶 移動：二郎 沖縄店 → レイサー沖縄那覇美栄橋',
            category: '移動',
            memo: '手段：徒歩（1.4km・沖映通り経由） / 所要：約21分 / 交通費：0円',
            done: false,
          },
          {
            id: 's2',
            day: '2026-11-21',
            time: '15:00',
            endTime: '',
            title: 'レイサー沖縄那覇美栄橋 チェックイン',
            category: '宿泊',
            memo: '那覇市前島3-7-7（美栄橋駅徒歩6分）/ 無人ホテル（事前チェックイン・荷物預かり不可）',
            done: false,
          },
          {
            id: 's2a',
            day: '2026-11-21',
            time: '15:35',
            endTime: '15:52',
            title: '🚶 移動：ホテル → Livehouse Output',
            category: '移動',
            memo: '手段：徒歩（1.1km） / 所要：約17分 / 交通費：0円',
            done: false,
          },
          {
            id: 's2b',
            day: '2026-11-21',
            time: '16:00',
            endTime: '',
            title: '【入場】アイドル甲子園 in Output -DAY2-',
            category: 'イベント',
            memo: 'Livehouse Output（那覇市牧志2-3-22 2F）/ OPEN 16:00・START 16:30',
            done: false,
          },
          {
            id: 's2c',
            day: '2026-11-21',
            time: '16:30',
            endTime: '17:00',
            title: '🎤 myojou（アイドル甲子園 DAY2）',
            category: 'イベント',
            memo: 'Livehouse Output / 1番手（終演後物販）',
            done: false,
          },
          {
            id: 's2d',
            day: '2026-11-21',
            time: '17:30',
            endTime: '18:00',
            title: '🎤 透色ドロップ（アイドル甲子園 DAY2）',
            category: 'イベント',
            memo: 'Livehouse Output / 3番手（終演後物販）',
            done: false,
          },
          {
            id: 's2e',
            day: '2026-11-21',
            time: '18:45',
            endTime: '20:05',
            title: '📸 終演後物販・特典会（Output）',
            category: 'イベント',
            memo: 'チェキ5枚（予算 10,000円）',
            done: false,
          },
          {
            id: 's2f',
            day: '2026-11-21',
            time: '20:00',
            endTime: '20:15',
            title: '🚶 移動：Output → ひいき屋',
            category: '移動',
            memo: '手段：徒歩（1.0km・約15分・0円）※物販20:05終了のため、少し早めに抜けるかタクシー移動が安心',
            done: false,
          },
          {
            id: 's2g',
            day: '2026-11-21',
            time: '20:15',
            endTime: '',
            title: '🍽️ ひいき屋（20:15予約）',
            category: '食事',
            memo: '沖縄県那覇市安里379 / TEL: 050-5593-5620 / 帰りは徒歩約27分（0円）または安里→美栄橋(ゆいレール250円)',
            done: false,
          },
          {
            id: 's4',
            day: '2026-11-22',
            time: '11:00',
            endTime: '',
            title: 'レイサー沖縄那覇美栄橋 チェックアウト',
            category: '宿泊',
            memo: '11:00までに出発',
            done: false,
          },
          {
            id: 's4a',
            day: '2026-11-22',
            time: '11:05',
            endTime: '11:25',
            title: '🚶 移動：ホテル → 桜坂セントラル',
            category: '移動',
            memo: '手段：徒歩（1.3km・沖映通り経由） / 所要：約20分 / 交通費：0円',
            done: false,
          },
          {
            id: 's5',
            day: '2026-11-22',
            time: '11:30',
            endTime: '',
            title: '【入場】アイドル甲子園 in 桜坂セントラル -DAY3-',
            category: 'イベント',
            memo: '桜坂セントラル（那覇市牧志3-9-26）/ OPEN 11:30・START 12:00',
            done: false,
          },
          {
            id: 's5b',
            day: '2026-11-22',
            time: '12:00',
            endTime: '12:25',
            title: '🎤 透色ドロップ（アイドル甲子園 DAY3）',
            category: 'イベント',
            memo: '桜坂セントラル / 1番手（中物販）',
            done: false,
          },
          {
            id: 's5c',
            day: '2026-11-22',
            time: '12:25',
            endTime: '12:50',
            title: '🎤 myojou（アイドル甲子園 DAY3）',
            category: 'イベント',
            memo: '桜坂セントラル / 2番手（中物販）',
            done: false,
          },
          {
            id: 's5d',
            day: '2026-11-22',
            time: '13:20',
            endTime: '14:40',
            title: '📸 中物販・特典会（桜坂セントラル）',
            category: 'イベント',
            memo: 'チェキ5枚（予算 10,000円）',
            done: false,
          },
          {
            id: 's5e',
            day: '2026-11-22',
            time: '15:15',
            endTime: '15:38',
            title: '🚶 移動：桜坂セントラル → みんなの貸会議室 那覇泉崎店',
            category: '移動',
            memo: '手段：徒歩（1.7km・約23分 / 0円）※ゆいレール牧志→県庁前(約4分・250円)＋徒歩も可',
            done: false,
          },
          {
            id: 's6',
            day: '2026-11-22',
            time: '16:00',
            endTime: '17:30',
            title: '透色ドロップ 沖縄特典会',
            category: 'イベント',
            memo: 'みんなの貸会議室 那覇泉崎店 202会議室（那覇市泉崎1-13-3 / LivePocket）',
            done: false,
          },
          {
            id: 's7',
            day: '2026-11-22',
            time: '18:30',
            endTime: '',
            title: '🍻 11/22 オフ会（想定11名〜）',
            category: '食事',
            memo: '日程表ベース11名（フォーム回答で調整）\n① とりいちず 那覇泉崎店（泉崎1-14-7・個室/食べ飲み放題）\n② 肉と出汁 くぐ琉 久茂地本店（久茂地3-11-7・沖縄料理食べ飲み放題4,400円〜）\n③ 大衆酒場 マル八 那覇久茂地店（久茂地3-12-4・10名以上個室）\n④ ぱいかじ 国際通り店（久茂地3-29-68・沖縄料理）',
            done: false,
          },
          {
            id: 's8',
            day: '2026-11-23',
            time: '13:00',
            endTime: '',
            title: '【入場】エイトワンなりの感謝祭 2026 in 沖縄',
            category: 'イベント',
            memo: 'Livehouse Output（那覇市牧志2-3-22 2F）/ OPEN 13:00・START 13:30',
            done: false,
          },
          {
            id: 's8b',
            day: '2026-11-23',
            time: '15:15',
            endTime: '15:45',
            title: '🎤 透色ドロップ（エイトワン感謝祭）',
            category: 'イベント',
            memo: 'Livehouse Output / 5番手（終演後物販）',
            done: false,
          },
          {
            id: 's8c',
            day: '2026-11-23',
            time: '16:00',
            endTime: '17:30',
            title: '📸 終演後物販・特典会（Output）',
            category: 'イベント',
            memo: 'チェキ5枚（予算 10,000円）',
            done: false,
          },
          {
            id: 's9',
            day: '2026-11-23',
            time: '18:00',
            endTime: '',
            title: 'Mr.KINJO in Miegusuku チェックイン',
            category: '宿泊',
            memo: '11/23〜11/25予約（Outputから旭橋方面へ移動・ゆいレール牧志→旭橋 約6分/250円 または徒歩）',
            done: false,
          },
          {
            id: 's9a',
            day: '2026-11-24',
            time: '08:40',
            endTime: '09:10',
            title: '🚃 移動：ホテル → 那覇空港',
            category: '移動',
            memo: '手段：旭橋駅まで徒歩＋ゆいレール（旭橋→那覇空港 13分） / 交通費：290円',
            done: false,
          },
          {
            id: 's10',
            day: '2026-11-24',
            time: '10:20',
            endTime: '12:35',
            title: 'JAL902（那覇 → 羽田）',
            category: '移動',
            memo: '予約番号: 5F6DHP / 所要2時間15分・搭乗用2次元バーコード準備',
            done: false,
          },
        ],
        packing: [
          { id: 'p1', title: 'スマホ・航空券QR（ANA / JAL）', category: '必需品', qty: '', checked: false },
          { id: 'p2', title: '財布・現金・クレジットカード', category: '必需品', qty: '', checked: false },
          { id: 'p3', title: '身分証明書（免許証など）', category: '必需品', qty: '', checked: false },
          { id: 'p4', title: 'ホテル案内メール・暗証番号控え', category: '必需品', qty: '', checked: false },
          { id: 'p5', title: 'LivePocket チケット表示確認', category: 'ヲタク', qty: '', checked: false },
          { id: 'p6', title: 'ペンライト・電池・ヲタクグッズ', category: 'ヲタク', qty: '', checked: false },
          { id: 'p7', title: 'チェキケース・特典会用現金（1万円×3公演分＋α）', category: 'ヲタク', qty: '3万円〜', checked: false },
          { id: 'p8', title: 'Tシャツ・トップス（ライブ用・普段用）', category: '衣類', qty: '3〜4枚', checked: false },
          { id: 'p8b', title: 'ズボン・ボトムス', category: '衣類', qty: '2本', checked: false },
          { id: 'p8c', title: '下着・インナー', category: '衣類', qty: '3〜4枚', checked: false },
          { id: 'p8d', title: '靴下', category: '衣類', qty: '3〜4足', checked: false },
          { id: 'p8e', title: '部屋着・パジャマ', category: '衣類', qty: '1セット', checked: false },
          { id: 'p9', title: '羽織りもの・パーカー（機内・朝晩用）', category: '衣類', qty: '1枚', checked: false },
          { id: 'p9b', title: '衣類圧縮袋・洗濯ネット', category: '衣類', qty: '1〜2枚', checked: false },
          { id: 'p10', title: 'モバイルバッテリー・充電ケーブル', category: 'ガジェット', qty: '', checked: false },
          { id: 'p11', title: 'iPad / Apple Pencil（必要なら）', category: 'ガジェット', qty: '', checked: false },
          { id: 'p12', title: 'Ploom AURA・EVOスティック', category: 'その他', qty: '', checked: false },
          { id: 'p13', title: '常備薬・折りたたみ傘', category: 'その他', qty: '', checked: false },
        ],
      };

      let state = loadState();
      let activeTab = 'schedule';
      let selectedDay = 'all';
      let selectedPackCat = 'すべて';
      let uncheckedOnly = false;
      let confirmCallback = null;
      let weatherByDate = {};
      let weatherStatus = 'loading'; // 'loading' | 'ok' | 'error'

      function loadState() {
        try {
          const raw = localStorage.getItem(STORAGE_KEY);
          if (raw) {
            const parsed = JSON.parse(raw);
            if (parsed && Array.isArray(parsed.schedules) && Array.isArray(parsed.packing)) {
              return parsed;
            }
          }
        } catch (e) {}
        return JSON.parse(JSON.stringify(DEFAULT_DATA));
      }

      function saveState() {
        try {
          localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
        } catch (e) {}
      }

      function uid(prefix) {
        return prefix + '_' + Date.now().toString(36) + Math.random().toString(36).slice(2, 6);
      }

      function showToast(msg) {
        const el = document.getElementById('toast');
        el.textContent = msg;
        el.classList.remove('hidden');
        clearTimeout(el._timer);
        el._timer = setTimeout(() => el.classList.add('hidden'), 2400);
      }

      function openModal(id) {
        document.getElementById(id).classList.remove('hidden');
      }

      function closeModal(id) {
        document.getElementById(id).classList.add('hidden');
      }

      function askConfirm(message, onOk) {
        document.getElementById('confirmMessage').textContent = message;
        confirmCallback = onOk;
        openModal('confirmModal');
      }

      function escapeHtml(str) {
        return String(str || '')
          .replace(/&/g, '&amp;')
          .replace(/</g, '&lt;')
          .replace(/>/g, '&gt;')
          .replace(/"/g, '&quot;');
      }

      // Generate PNG apple-touch-icon dynamically for iOS Home Screen
      function generateAppleTouchIcon() {
        try {
          const canvas = document.createElement('canvas');
          canvas.width = 180;
          canvas.height = 180;
          const ctx = canvas.getContext('2d');
          const grad = ctx.createLinearGradient(0, 0, 180, 180);
          grad.addColorStop(0, '#0284c7');
          grad.addColorStop(1, '#14b8a6');
          ctx.fillStyle = grad;
          ctx.fillRect(0, 0, 180, 180);

          ctx.fillStyle = 'rgba(255,255,255,0.18)';
          ctx.beginPath();
          ctx.arc(145, 38, 42, 0, Math.PI * 2);
          ctx.fill();

          ctx.fillStyle = '#ffffff';
          ctx.font = 'bold 64px sans-serif';
          ctx.textAlign = 'center';
          ctx.textBaseline = 'middle';
          ctx.fillText('🌺', 90, 74);

          ctx.font = 'bold 24px sans-serif';
          ctx.fillText('沖縄旅', 90, 134);

          document.getElementById('appleTouchIcon').href = canvas.toDataURL('image/png');
        } catch (e) {}
      }

      // ==================== RENDER SCHEDULE ====================
      function renderDayFilters() {
        const bar = document.getElementById('dayFilterBar');
        bar.innerHTML = DAYS.map(d => {
          const active = selectedDay === d.id;
          return `<button type="button" data-day="${d.id}"
            class="px-3.5 py-1.5 rounded-full text-xs font-semibold whitespace-nowrap transition border ${
              active
                ? 'bg-sky-600 text-white border-sky-600 shadow-sm'
                : 'bg-white text-slate-600 border-slate-200 hover:bg-slate-100'
            }">${d.label}</button>`;
        }).join('');
      }

      function toMinutes(hhmm) {
        if (!hhmm || !hhmm.includes(':')) return null;
        const [h, m] = hhmm.split(':').map(Number);
        if (Number.isNaN(h) || Number.isNaN(m)) return null;
        return h * 60 + m;
      }

      function formatDuration(mins) {
        if (mins == null || mins <= 0) return '';
        const h = Math.floor(mins / 60);
        const m = mins % 60;
        if (h > 0 && m > 0) return `${h}時間${m}分`;
        if (h > 0) return `${h}時間`;
        return `${m}分`;
      }

      function renderSchedules() {
        renderDayFilters();
        const container = document.getElementById('scheduleList');
        const daysToShow = selectedDay === 'all' ? DAYS.slice(1) : DAYS.filter(d => d.id === selectedDay);

        let totalShown = 0;
        const htmlParts = [];

        daysToShow.forEach(dayObj => {
          const items = state.schedules
            .filter(s => s.day === dayObj.id)
            .sort((a, b) => (a.time || '').localeCompare(b.time || ''));

          totalShown += items.length;

          let itemsHtml = '';
          if (items.length === 0) {
            itemsHtml = `<div class="p-4 rounded-2xl border border-dashed border-slate-200 text-center text-xs text-slate-400 bg-white/60">
                 この日の予定はまだありません
               </div>`;
          } else {
            const chunks = [];
            if (dayObj.id === '2026-11-23' && items.length > 0 && (toMinutes(items[0].time) || 0) >= 720) {
              chunks.push(`
                <div class="ml-4 pl-4 border-l-2 border-dotted border-amber-300 py-1">
                  <div class="rounded-xl bg-amber-50/90 border border-amber-200/80 px-3 py-2 space-y-1">
                    <div class="flex items-center gap-1.5 text-[11px] font-bold text-amber-800">
                      <span>☕ 午前〜${escapeHtml(items[0].time)} 空き時間（ランチ余裕あり）</span>
                    </div>
                    <div class="text-[11px] text-amber-900/90 leading-relaxed">
                      🍽️ <strong>Output周辺の昼食候補：</strong><br/>
                      ・ステーキハウス88 国際通り店（牧志3-1-6 2F / 11:00〜）<br/>
                      ・やっぱりステーキ 4th 国際通り店（牧志3-12-4 2F / 11:00〜）<br/>
                      ・ジャッキーステーキハウス（11:00〜受付22:00）
                    </div>
                  </div>
                </div>
              `);
            }
            items.forEach((item, idx) => {
              // Check free time gap from previous item
              if (idx > 0) {
                const prev = items[idx - 1];
                const prevEnd = toMinutes(prev.endTime || prev.time);
                const curStart = toMinutes(item.time);
                if (prevEnd !== null && curStart !== null) {
                  const gap = curStart - prevEnd;
                  if (gap >= 15) {
                    let foodHtml = '';
                    if (dayObj.id === '2026-11-21' && gap >= 120) {
                      foodHtml = `
                        <div class="text-[11px] text-amber-900/90 leading-relaxed mt-1 pt-1 border-t border-amber-200/60">
                          🍽️ <strong>二郎後の休憩・軽食候補：</strong><br/>
                          ・ポーたま 牧志市場店（松尾2-8-35 / 7:00〜20:00）<br/>
                          ・C&amp;C Breakfast（松尾2-9-6 / 〜14:00）<br/>
                          ・第一牧志公設市場周辺でカフェ休憩
                        </div>
                      `;
                    } else if (dayObj.id === '2026-11-22' && gap >= 30 && prevEnd >= 840 && curStart <= 960) {
                      foodHtml = `
                        <div class="text-[11px] text-amber-900/90 leading-relaxed mt-1 pt-1 border-t border-amber-200/60">
                          🍽️ <strong>移動前のサクッと軽食候補：</strong><br/>
                          ・ポーたま 牧志市場店（松尾2-8-35 / 片手で食べられる）<br/>
                          ・松原製菓（松尾2-9-9 / サーターアンダギー・〜18:00）
                        </div>
                      `;
                    }
                    chunks.push(`
                      <div class="ml-4 pl-4 border-l-2 border-dotted border-amber-300 py-1">
                        <div class="${foodHtml ? 'rounded-xl px-3 py-2' : 'inline-flex items-center gap-1.5 px-2.5 py-1 rounded-full'} bg-amber-50 border border-amber-200/80 text-[11px] font-semibold text-amber-700">
                          <div class="flex items-center gap-1.5">
                            <span>☕ 空き時間：${formatDuration(gap)}</span>
                            <span class="text-[10px] font-normal text-amber-600/80">(${escapeHtml(prev.endTime || prev.time)}〜${escapeHtml(item.time)})</span>
                          </div>
                          ${foodHtml}
                        </div>
                      </div>
                    `);
                  }
                }
              }

              const timeStr = item.endTime ? `${item.time} – ${item.endTime}` : item.time;

              if (item.category === '移動') {
                const sMin = toMinutes(item.time);
                const eMin = toMinutes(item.endTime);
                const dur = (sMin !== null && eMin !== null && eMin > sMin) ? formatDuration(eMin - sMin) : '';
                chunks.push(`
                  <div class="ml-4 pl-4 border-l-2 border-dashed border-sky-300 py-1 ${item.done ? 'opacity-55' : ''}">
                    <div data-edit-sched="${item.id}" class="cursor-pointer bg-sky-50/75 hover:bg-sky-100/70 border border-sky-200/80 rounded-xl px-3 py-2 flex items-center justify-between gap-2 transition">
                      <div class="min-w-0 flex-1">
                        <div class="flex items-center flex-wrap gap-1.5">
                          <span class="text-[11px] font-bold text-sky-700 tabular-nums">${escapeHtml(timeStr)}</span>
                          ${dur ? `<span class="px-1.5 py-0.5 rounded bg-sky-600 text-white text-[10px] font-bold">所要 ${dur}</span>` : ''}
                        </div>
                        <div class="text-xs font-semibold text-slate-700 mt-0.5 truncate ${item.done ? 'line-through' : ''}">${escapeHtml(item.title)}</div>
                        ${item.memo ? `<div class="text-[11px] text-slate-500 mt-0.5 break-words">${escapeHtml(item.memo)}</div>` : ''}
                      </div>
                      <button type="button" data-toggle-sched="${item.id}" title="完了切り替え"
                        class="w-4 h-4 rounded-full border-2 flex items-center justify-center shrink-0 transition ${
                          item.done ? 'bg-teal-500 border-teal-500 text-white' : 'border-sky-300 hover:border-sky-500 bg-white'
                        }">
                        ${item.done ? '<svg class="w-2.5 h-2.5" fill="none" stroke="currentColor" stroke-width="3" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/></svg>' : ''}
                      </button>
                    </div>
                  </div>
                `);
              } else {
                const meta = CAT_META[item.category] || CAT_META['その他'];
                chunks.push(`
                  <div class="group bg-white rounded-2xl p-3.5 shadow-xs border border-slate-200/80 flex items-start gap-3 transition ${item.done ? 'opacity-60' : ''}">
                    <button type="button" data-toggle-sched="${item.id}" title="完了切り替え"
                      class="mt-0.5 w-5 h-5 rounded-full border-2 flex items-center justify-center shrink-0 transition ${
                        item.done ? 'bg-teal-500 border-teal-500 text-white' : 'border-slate-300 hover:border-sky-500'
                      }">
                      ${item.done ? '<svg class="w-3 h-3" fill="none" stroke="currentColor" stroke-width="3" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/></svg>' : ''}
                    </button>
                    <div class="flex-1 min-w-0 cursor-pointer" data-edit-sched="${item.id}">
                      <div class="flex items-center flex-wrap gap-1.5 mb-1">
                        <span class="text-xs font-bold text-sky-700 tabular-nums">${escapeHtml(timeStr)}</span>
                        <span class="px-2 py-0.5 rounded-full text-[10px] font-semibold border ${meta.badge}">
                          ${meta.icon} ${escapeHtml(item.category)}
                        </span>
                      </div>
                      <h3 class="text-sm font-bold text-slate-800 ${item.done ? 'line-through' : ''}">${escapeHtml(item.title)}</h3>
                      ${item.memo ? `<p class="text-xs text-slate-500 mt-1 whitespace-pre-line break-words">${escapeHtml(item.memo)}</p>` : ''}
                    </div>
                    <button type="button" data-edit-sched="${item.id}" class="p-1.5 rounded-lg text-slate-400 hover:text-sky-600 hover:bg-sky-50 shrink-0 transition" title="編集">
                      <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                      </svg>
                    </button>
                  </div>
                `);
              }
            });
            itemsHtml = chunks.join('');
          }

          htmlParts.push(`
            <div class="space-y-2">
              <div class="flex items-center justify-between px-1 gap-2">
                <div class="flex items-center gap-2 min-w-0">
                  <h2 class="text-xs font-bold uppercase tracking-wider text-slate-500">${dayObj.short}</h2>
                  ${(() => {
                    const w = weatherByDate[dayObj.id];
                    if (!w) return '';
                    return `<span class="inline-flex items-center gap-1 px-2 py-0.5 rounded-full bg-sky-50 border border-sky-200/80 text-[10px] font-semibold text-sky-800 whitespace-nowrap">${w.icon} ${w.max}°/${w.min}° · ☔${w.pop}%</span>`;
                  })()}
                </div>
                <span class="text-[11px] font-medium text-slate-400 shrink-0">${items.length}件</span>
              </div>
              <div class="space-y-2">${itemsHtml}</div>
            </div>
          `);
        });

        container.innerHTML = htmlParts.join('');
        document.getElementById('scheduleCountText').textContent = `表示中の予定: ${totalShown}件（タップで編集）`;
      }

      // ==================== RENDER PACKING ====================
      function renderPackingCategories() {
        const bar = document.getElementById('packingCategoryBar');
        bar.innerHTML = PACK_CATS.map(cat => {
          const active = selectedPackCat === cat;
          return `<button type="button" data-pack-cat="${cat}"
            class="px-3 py-1 rounded-full text-xs font-semibold whitespace-nowrap transition border ${
              active
                ? 'bg-slate-800 text-white border-slate-800'
                : 'bg-white text-slate-600 border-slate-200 hover:bg-slate-100'
            }">${cat}</button>`;
        }).join('');
      }

      function renderPacking() {
        renderPackingCategories();

        const total = state.packing.length;
        const checkedCount = state.packing.filter(p => p.checked).length;
        const pct = total === 0 ? 0 : Math.round((checkedCount / total) * 100);

        document.getElementById('packingProgressText').textContent = `${checkedCount} / ${total} 個準備完了`;
        document.getElementById('packingPercentBadge').textContent = `${pct}%`;
        document.getElementById('packingProgressBar').style.width = `${pct}%`;

        let filtered = state.packing;
        if (selectedPackCat !== 'すべて') {
          filtered = filtered.filter(p => p.category === selectedPackCat);
        }
        if (uncheckedOnly) {
          filtered = filtered.filter(p => !p.checked);
        }

        const list = document.getElementById('packingList');
        if (filtered.length === 0) {
          list.innerHTML = `
            <div class="p-6 rounded-2xl border border-dashed border-slate-200 text-center text-xs text-slate-400 bg-white">
              該当する持ち物はありません
            </div>
          `;
          return;
        }

        list.innerHTML = filtered.map(item => `
          <div class="bg-white rounded-2xl px-3.5 py-3 shadow-xs border border-slate-200/80 flex items-center gap-3 transition ${item.checked ? 'bg-slate-50/80 opacity-70' : ''}">
            <button type="button" data-toggle-pack="${item.id}"
              class="w-5 h-5 rounded-md border-2 flex items-center justify-center shrink-0 transition ${
                item.checked ? 'bg-sky-600 border-sky-600 text-white' : 'border-slate-300 hover:border-sky-500'
              }">
              ${item.checked ? '<svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" stroke-width="3" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/></svg>' : ''}
            </button>
            <div class="flex-1 min-w-0 cursor-pointer" data-toggle-pack="${item.id}">
              <div class="flex items-center gap-2 flex-wrap">
                <span class="text-sm font-medium text-slate-800 ${item.checked ? 'line-through text-slate-400' : ''}">${escapeHtml(item.title)}</span>
                ${item.qty ? `<span class="px-1.5 py-0.5 rounded bg-slate-100 text-[10px] font-semibold text-slate-600">${escapeHtml(item.qty)}</span>` : ''}
              </div>
              <span class="text-[10px] font-medium text-slate-400">${escapeHtml(item.category)}</span>
            </div>
            <button type="button" data-edit-pack="${item.id}" class="p-1.5 rounded-lg text-slate-400 hover:text-sky-600 hover:bg-sky-50 shrink-0 transition" title="編集">
              <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z" />
              </svg>
            </button>
          </div>
        `).join('');
      }

      // ==================== TAB SWITCHING ====================
      function switchTab(tab) {
        activeTab = tab;
        const isSched = tab === 'schedule';
        document.getElementById('viewSchedule').classList.toggle('hidden', !isSched);
        document.getElementById('viewPacking').classList.toggle('hidden', isSched);

        const tabS = document.getElementById('tabSchedule');
        const tabP = document.getElementById('tabPacking');
        tabS.className = `flex flex-col items-center justify-center py-2.5 transition ${isSched ? 'text-sky-600 font-semibold' : 'text-slate-400 hover:text-slate-600 font-medium'}`;
        tabP.className = `flex flex-col items-center justify-center py-2.5 transition ${!isSched ? 'text-sky-600 font-semibold' : 'text-slate-400 hover:text-slate-600 font-medium'}`;
      }

      // ==================== EVENT LISTENERS ====================
      document.getElementById('tabSchedule').addEventListener('click', () => switchTab('schedule'));
      document.getElementById('tabPacking').addEventListener('click', () => switchTab('packing'));

      document.getElementById('btnPwaGuide').addEventListener('click', () => openModal('pwaGuideModal'));
      document.getElementById('btnDataMenu').addEventListener('click', () => openModal('dataMenuModal'));

      document.querySelectorAll('[data-close-modal]').forEach(btn => {
        btn.addEventListener('click', () => closeModal(btn.getAttribute('data-close-modal')));
      });

      // Day filter delegation
      document.getElementById('dayFilterBar').addEventListener('click', e => {
        const btn = e.target.closest('[data-day]');
        if (!btn) return;
        selectedDay = btn.getAttribute('data-day');
        renderSchedules();
      });

      // Schedule list delegation (toggle done / edit)
      document.getElementById('scheduleList').addEventListener('click', e => {
        const toggleBtn = e.target.closest('[data-toggle-sched]');
        if (toggleBtn) {
          const id = toggleBtn.getAttribute('data-toggle-sched');
          const item = state.schedules.find(s => s.id === id);
          if (item) {
            item.done = !item.done;
            saveState();
            renderSchedules();
          }
          return;
        }
        const editEl = e.target.closest('[data-edit-sched]');
        if (editEl) {
          const id = editEl.getAttribute('data-edit-sched');
          const item = state.schedules.find(s => s.id === id);
          if (!item) return;
          document.getElementById('scheduleModalTitle').textContent = '予定を編集';
          document.getElementById('schedId').value = item.id;
          document.getElementById('schedDay').value = item.day;
          document.getElementById('schedCategory').value = item.category;
          document.getElementById('schedTime').value = item.time;
          document.getElementById('schedEndTime').value = item.endTime || '';
          document.getElementById('schedTitle').value = item.title;
          document.getElementById('schedMemo').value = item.memo || '';
          document.getElementById('btnDeleteSchedule').classList.remove('hidden');
          openModal('scheduleModal');
        }
      });

      // Add schedule button
      document.getElementById('btnAddSchedule').addEventListener('click', () => {
        document.getElementById('scheduleModalTitle').textContent = '予定を追加';
        document.getElementById('schedId').value = '';
        document.getElementById('schedDay').value = selectedDay === 'all' ? '2026-11-21' : selectedDay;
        document.getElementById('schedCategory').value = '観光';
        document.getElementById('schedTime').value = '12:00';
        document.getElementById('schedEndTime').value = '';
        document.getElementById('schedTitle').value = '';
        document.getElementById('schedMemo').value = '';
        document.getElementById('btnDeleteSchedule').classList.add('hidden');
        openModal('scheduleModal');
      });

      // Save schedule form
      document.getElementById('scheduleForm').addEventListener('submit', e => {
        e.preventDefault();
        const id = document.getElementById('schedId').value;
        const payload = {
          day: document.getElementById('schedDay').value,
          category: document.getElementById('schedCategory').value,
          time: document.getElementById('schedTime').value,
          endTime: document.getElementById('schedEndTime').value,
          title: document.getElementById('schedTitle').value.trim(),
          memo: document.getElementById('schedMemo').value.trim(),
        };
        if (!payload.title) return;

        if (id) {
          const idx = state.schedules.findIndex(s => s.id === id);
          if (idx !== -1) {
            state.schedules[idx] = { ...state.schedules[idx], ...payload };
          }
          showToast('予定を更新しました');
        } else {
          state.schedules.push({ id: uid('s'), ...payload, done: false });
          showToast('予定を追加しました');
        }
        saveState();
        renderSchedules();
        closeModal('scheduleModal');
      });

      // Delete schedule
      document.getElementById('btnDeleteSchedule').addEventListener('click', () => {
        const id = document.getElementById('schedId').value;
        if (!id) return;
        state.schedules = state.schedules.filter(s => s.id !== id);
        saveState();
        renderSchedules();
        closeModal('scheduleModal');
        showToast('予定を削除しました');
      });

      // Quick add packing
      document.getElementById('quickAddPackingForm').addEventListener('submit', e => {
        e.preventDefault();
        const input = document.getElementById('quickPackingTitle');
        const title = input.value.trim();
        if (!title) return;
        const cat = document.getElementById('quickPackingCat').value;
        state.packing.unshift({ id: uid('p'), title, category: cat, qty: '', checked: false });
        input.value = '';
        saveState();
        renderPacking();
        showToast('持ち物を追加しました');
      });

      // Packing category filter
      document.getElementById('packingCategoryBar').addEventListener('click', e => {
        const btn = e.target.closest('[data-pack-cat]');
        if (!btn) return;
        selectedPackCat = btn.getAttribute('data-pack-cat');
        renderPacking();
      });

      // Unchecked only toggle
      document.getElementById('toggleUncheckedOnly').addEventListener('change', e => {
        uncheckedOnly = e.target.checked;
        renderPacking();
      });

      // Packing list delegation
      document.getElementById('packingList').addEventListener('click', e => {
        const toggleEl = e.target.closest('[data-toggle-pack]');
        if (toggleEl) {
          const id = toggleEl.getAttribute('data-toggle-pack');
          const item = state.packing.find(p => p.id === id);
          if (item) {
            item.checked = !item.checked;
            saveState();
            renderPacking();
          }
          return;
        }
        const editBtn = e.target.closest('[data-edit-pack]');
        if (editBtn) {
          const id = editBtn.getAttribute('data-edit-pack');
          const item = state.packing.find(p => p.id === id);
          if (!item) return;
          document.getElementById('packId').value = item.id;
          document.getElementById('packTitle').value = item.title;
          document.getElementById('packCategory').value = item.category;
          document.getElementById('packQty').value = item.qty || '';
          openModal('packingModal');
        }
      });

      // Save packing edit
      document.getElementById('packingEditForm').addEventListener('submit', e => {
        e.preventDefault();
        const id = document.getElementById('packId').value;
        const item = state.packing.find(p => p.id === id);
        if (!item) return;
        item.title = document.getElementById('packTitle').value.trim();
        item.category = document.getElementById('packCategory').value;
        item.qty = document.getElementById('packQty').value.trim();
        saveState();
        renderPacking();
        closeModal('packingModal');
        showToast('持ち物を更新しました');
      });

      // Delete packing
      document.getElementById('btnDeletePacking').addEventListener('click', () => {
        const id = document.getElementById('packId').value;
        state.packing = state.packing.filter(p => p.id !== id);
        saveState();
        renderPacking();
        closeModal('packingModal');
        showToast('持ち物を削除しました');
      });

      // Reset checks
      document.getElementById('btnResetChecks').addEventListener('click', () => {
        askConfirm('すべての持ち物チェックを外しますか？', () => {
          state.packing.forEach(p => { p.checked = false; });
          saveState();
          renderPacking();
          showToast('チェックをリセットしました');
        });
      });

      // Export JSON
      document.getElementById('btnExportJson').addEventListener('click', () => {
        const text = JSON.stringify(state);
        if (navigator.clipboard && navigator.clipboard.writeText) {
          navigator.clipboard.writeText(text).then(() => showToast('JSONをコピーしました')).catch(() => fallbackCopy(text));
        } else {
          fallbackCopy(text);
        }
      });

      function fallbackCopy(text) {
        const ta = document.createElement('textarea');
        ta.value = text;
        document.body.appendChild(ta);
        ta.select();
        try { document.execCommand('copy'); showToast('JSONをコピーしました'); } catch (e) {}
        document.body.removeChild(ta);
      }

      // Import JSON
      document.getElementById('btnImportJson').addEventListener('click', () => {
        const raw = document.getElementById('importJsonInput').value.trim();
        if (!raw) return;
        try {
          const parsed = JSON.parse(raw);
          if (parsed && Array.isArray(parsed.schedules) && Array.isArray(parsed.packing)) {
            state = parsed;
            saveState();
            renderSchedules();
            renderPacking();
            document.getElementById('importJsonInput').value = '';
            closeModal('dataMenuModal');
            showToast('データを復元しました');
          } else {
            showToast('形式が正しくありません');
          }
        } catch (e) {
          showToast('JSONの読み込みに失敗しました');
        }
      });

      // Reset all data
      document.getElementById('btnResetAllData').addEventListener('click', () => {
        closeModal('dataMenuModal');
        askConfirm('初期データ（予約情報とテンプレート）に戻しますか？', () => {
          state = JSON.parse(JSON.stringify(DEFAULT_DATA));
          saveState();
          renderSchedules();
          renderPacking();
          showToast('初期データに戻しました');
        });
      });

      // Confirm modal buttons
      document.getElementById('btnConfirmCancel').addEventListener('click', () => {
        confirmCallback = null;
        closeModal('confirmModal');
      });
      document.getElementById('btnConfirmOk').addEventListener('click', () => {
        closeModal('confirmModal');
        if (typeof confirmCallback === 'function') {
          confirmCallback();
          confirmCallback = null;
        }
      });

      // ==================== WEATHER (Open-Meteo) ====================
      function wmoToInfo(code) {
        if (code === 0) return { icon: '☀️', label: '快晴' };
        if (code === 1 || code === 2) return { icon: '⛅', label: '晴れ' };
        if (code === 3) return { icon: '☁️', label: 'くもり' };
        if (code === 45 || code === 48) return { icon: '🌫️', label: '霧' };
        if ((code >= 51 && code <= 67) || (code >= 80 && code <= 82)) return { icon: '🌧️', label: '雨' };
        if (code >= 71 && code <= 77) return { icon: '❄️', label: '雪' };
        if (code >= 95) return { icon: '⛈️', label: '雷雨' };
        return { icon: '🌤️', label: '予報' };
      }

      function renderWeatherStrip() {
        const el = document.getElementById('weatherStrip');
        if (!el) return;
        if (weatherStatus === 'loading') {
          el.innerHTML = '<div class="col-span-4 py-2 text-xs text-slate-400">那覇の天気を取得中...</div>';
          return;
        }
        if (weatherStatus === 'error') {
          el.innerHTML = '<div class="col-span-4 py-2 text-xs text-rose-500">天気予報の取得に失敗しました（「更新」で再試行）</div>';
          return;
        }
        const targetDays = DAYS.slice(1);
        el.innerHTML = targetDays.map(d => {
          const w = weatherByDate[d.id];
          if (!w) {
            return `<div class="p-2 rounded-xl bg-slate-50 border border-slate-100"><div class="text-[10px] font-bold text-slate-500">${d.label}</div><div class="text-xs text-slate-400 mt-1">--</div></div>`;
          }
          return `
            <button type="button" data-weather-day="${d.id}" class="p-2 rounded-xl bg-slate-50 hover:bg-sky-50 border border-slate-200/70 transition text-center">
              <div class="text-[10px] font-bold text-slate-600">${d.label}</div>
              <div class="text-lg leading-tight my-0.5">${w.icon}</div>
              <div class="text-[11px] font-bold text-slate-800 tabular-nums"><span class="text-rose-500">${w.max}°</span> / <span class="text-sky-600">${w.min}°</span></div>
              <div class="text-[10px] text-slate-500">☔ ${w.pop}%</div>
            </button>
          `;
        }).join('');
      }

      async function fetchWeather(manual = false) {
        weatherStatus = 'loading';
        renderWeatherStrip();
        try {
          const url = 'https://api.open-meteo.com/v1/forecast?latitude=26.2124&longitude=127.6809&daily=weather_code,temperature_2m_max,temperature_2m_min,precipitation_probability_max&timezone=Asia%2FTokyo&start_date=2026-11-21&end_date=2026-11-24';
          const res = await fetch(url);
          if (!res.ok) throw new Error('HTTP ' + res.status);
          const data = await res.json();
          const d = data && data.daily;
          if (!d || !Array.isArray(d.time)) throw new Error('Invalid format');
          const nextMap = {};
          d.time.forEach((dateStr, i) => {
            const info = wmoToInfo(d.weather_code ? d.weather_code[i] : 0);
            nextMap[dateStr] = {
              icon: info.icon,
              label: info.label,
              max: Math.round(d.temperature_2m_max[i]),
              min: Math.round(d.temperature_2m_min[i]),
              pop: d.precipitation_probability_max ? (d.precipitation_probability_max[i] ?? 0) : 0,
            };
          });
          weatherByDate = nextMap;
          weatherStatus = 'ok';
          renderWeatherStrip();
          renderSchedules();
          if (manual) showToast('最新の天気予報を更新しました');
        } catch (err) {
          weatherStatus = 'error';
          renderWeatherStrip();
          if (manual) showToast('天気の取得に失敗しました');
        }
      }

      document.getElementById('btnRefreshWeather').addEventListener('click', () => fetchWeather(true));
      document.getElementById('weatherStrip').addEventListener('click', e => {
        const btn = e.target.closest('[data-weather-day]');
        if (!btn) return;
        selectedDay = btn.getAttribute('data-weather-day');
        renderSchedules();
      });

      document.getElementById('btnDownloadHtml').addEventListener('click', () => {
        const html = '<!DOCTYPE html>\n' + document.documentElement.outerHTML;
        const blob = new Blob([html], { type: 'text/html;charset=utf-8' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = 'okinawa_shiori_2026.html';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
        URL.revokeObjectURL(url);
        showToast('HTMLファイルを保存しました');
      });

      document.getElementById('btnCopyHtml').addEventListener('click', () => {
        const html = '<!DOCTYPE html>\n' + document.documentElement.outerHTML;
        if (navigator.clipboard && navigator.clipboard.writeText) {
          navigator.clipboard.writeText(html).then(() => showToast('HTMLをコピーしました')).catch(() => fallbackCopy(html));
        } else {
          fallbackCopy(html);
        }
      });

      // Init
      generateAppleTouchIcon();
      renderSchedules();
      renderPacking();
      fetchWeather(false);
    })();
  </script>
</body>
</html>
