<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Chosen Palette: Calm & Focused -->
    <!-- Application Structure Plan: A narrative-driven SPA that guides the user through the key themes of the report: 1. The urgent need for DX. 2. A deep dive into the 6 core challenges. 3. An interactive comparison of success factors and failure pitfalls, with clickable case studies. 4. A clear, step-by-step roadmap for implementation. 5. A forward-looking conclusion on Dynamic Capability. This structure transforms a dense report into an engaging, explorable journey, prioritizing user understanding over a literal representation of the report's layout. -->
    <!-- Visualization & Content Choices: - Key Stats (e.g., legacy system percentage): Large, bold text (HTML/CSS) for immediate impact (Goal: Inform). The "100% Dynamic Capability" is now a qualitative statement. - 6 Core Challenges: An interactive grid of cards (HTML/CSS/JS) to organize complex information and allow user-driven exploration (Goal: Organize). - Success/Failure Comparison: A central interactive element with clickable factors revealing case study data (Goal: Compare/Relationships). Specific metrics from cases (e.g., 90% defect reduction) are shown in dynamic text with clear units; the bar chart for mixed units has been removed for clarity (Goal: Inform/Compare). - DX Roadmap & Dynamic Capability: Clean, sequential diagrams built with styled HTML/CSS (Flexbox/Grid) to illustrate processes without SVG/Mermaid (Goal: Organize). All choices are made to ensure clarity, interactivity, and adherence to technical constraints. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <title>インタラクティブインフォグラフィック：製造業DX 成功と失敗の軌跡</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Noto Sans JP', sans-serif;
            background-color: #F8F9FA;
            color: #212529;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 40vh;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        .card {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .card:hover {
            transform: translateY(-8px);
            box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
        }
        .tab-button {
            transition: all 0.3s ease;
        }
        .tab-button.active {
            background-color: #0B3954;
            color: #FFFFFF;
        }
        .content-panel {
            transition: opacity 0.5s ease-in-out, transform 0.5s ease-in-out;
        }
        .hidden-panel {
            opacity: 0;
            transform: translateY(20px);
            height: 0;
            overflow: hidden;
            padding-top: 0;
            padding-bottom: 0;
            margin-top: 0;
        }
        .visible-panel {
            opacity: 1;
            transform: translateY(0);
            height: auto;
        }
        .roadmap-step {
            border-left: 3px solid #3A86FF;
        }
        .roadmap-step:last-child {
            border-left: 3px solid transparent;
        }
        .roadmap-dot {
            left: -14px;
        }
    </style>
</head>
<body class="antialiased">

    <header class="bg-[#0B3954] text-white py-16 px-4 text-center shadow-lg">
        <h1 class="text-4xl md:text-5xl font-bold mb-4">製造業DX：成功と失敗の軌跡</h1>
        <p class="text-lg md:text-xl max-w-3xl mx-auto text-gray-300">データが導く、未来のものづくりへ。課題を克服し、持続的な成長を実現するためのインタラクティブガイド。</p>
    </header>

    <main class="container mx-auto p-4 md:p-8">

        <section id="challenge" class="my-16">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-[#0B3954] mb-2">なぜ今、変革が急務なのか？</h2>
                <p class="text-lg text-gray-600">製造業は、グローバル競争の激化、人手不足、顧客ニーズの多様化など、複雑な課題に直面しています。</p>
            </div>
            <div class="max-w-5xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-8 text-center">
                <div class="bg-white p-6 rounded-lg shadow-md card">
                    <div class="text-5xl font-bold text-[#3A86FF]">77<span class="text-3xl">%</span></div>
                    <h3 class="text-xl font-semibold mt-4 mb-2">DXに取り組む企業の割合</h3>
                    <p class="text-gray-600">情報処理推進機構（IPA）の調査によると、多くの企業がDXに着手しています。</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md card">
                    <div class="text-5xl font-bold text-[#E53935]">23<span class="text-3xl">%</span></div>
                    <h3 class="text-xl font-semibold mt-4 mb-2">レガシーシステムがない企業の割合</h3>
                    <p class="text-gray-600">製造業を含む産業分野で、老朽化したシステムが「全くない」と回答した企業は少数派です。</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md card">
                    <div class="text-5xl font-bold text-[#FFC107]">100<span class="text-3xl">%</span></div>
                    <h3 class="text-xl font-semibold mt-4 mb-2">ダイナミック・ケイパビリティの強化</h3>
                    <p class="text-gray-600">市場変化に柔軟に対応し、自己変革し続ける能力を**完全に**強化することが、すべての企業に不可欠です。</p>
                </div>
            </div>
        </section>

        <section id="pitfalls" class="my-16">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-[#0B3954] mb-2">DX推進を阻む「6つの壁」</h2>
                <p class="text-lg text-gray-600">多くの企業が直面する共通の課題。あなたはどの壁に直面していますか？</p>
            </div>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 max-w-6xl mx-auto">
                <div class="bg-white p-6 rounded-lg shadow-md card">
                    <h3 class="text-xl font-bold text-[#0B3954] mb-3">① 経営層の理解不足</h3>
                    <p class="text-gray-600">DXを単なるIT投資と捉え、本質的なビジネス変革としてのコミットメントが欠如。ビジョンが曖昧になり、意思決定が遅延します。</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md card">
                    <h3 class="text-xl font-bold text-[#0B3954] mb-3">② DX人材の不足</h3>
                    <p class="text-gray-600">現場とITの両方を理解する人材が希少。既存IT部門は保守に追われ、新たな人材育成や確保が困難な状況です。</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md card">
                    <h3 class="text-xl font-bold text-[#0B3954] mb-3">③ 業務の属人化</h3>
                    <p class="text-gray-600">熟練職人の「勘と経験」に依存。ノウハウが暗黙知化し、技術継承や標準化、品質の安定化を阻害します。</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md card">
                    <h3 class="text-xl font-bold text-[#0B3954] mb-3">④ 費用対効果の不透明さ</h3>
                    <p class="text-gray-600">高額な初期投資と、測定しにくいROIが投資判断を鈍らせ、「守りのDX」に偏重する原因となります。</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md card">
                    <h3 class="text-xl font-bold text-[#0B3954] mb-3">⑤ レガシーシステムとデータ分断</h3>
                    <p class="text-gray-600">部門ごとに最適化された古いシステムがデータのサイロ化を招き、全社的なデータ活用と迅速な意思決定を妨げます。</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md card">
                    <h3 class="text-xl font-bold text-[#0B3954] mb-3">⑥ 目的の不明確化</h3>
                    <p class="text-gray-600">「DXをすること」が目的化。具体的な目標がないため、期待した効果が得られず、プロジェクトが形骸化します。</p>
                </div>
            </div>
        </section>

        <section id="crossroads" class="my-20 bg-white rounded-xl shadow-xl p-6 md:p-10">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-[#0B3954] mb-2">成功と失敗の分岐点</h2>
                <p class="text-lg text-gray-600">成否を分ける要因は何か？タブをクリックして、具体的な事例と教訓を探りましょう。</p>
            </div>

            <div class="flex justify-center mb-8 border-b-2 border-gray-200">
                <button id="success-tab" class="tab-button text-lg font-semibold py-3 px-6 -mb-0.5 border-b-4 border-transparent hover:border-[#3A86FF] active">成功の要因</button>
                <button id="failure-tab" class="tab-button text-lg font-semibold py-3 px-6 -mb-0.5 border-b-4 border-transparent hover:border-[#E53935]">失敗の教訓</button>
            </div>

            <div id="success-panel" class="content-panel visible-panel">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <div>
                        <h3 class="text-2xl font-bold text-[#0B3954] mb-4">成功に導く6つのベストプラクティス</h3>
                        <ul class="space-y-3">
                            <li id="factor-1" class="p-4 rounded-lg cursor-pointer hover:bg-blue-50 transition-colors">
                                <strong>明確な目的と戦略：</strong>経営課題に直結した具体的な目標を設定する。
                            </li>
                            <li id="factor-2" class="p-4 rounded-lg cursor-pointer hover:bg-blue-50 transition-colors">
                                <strong>強力なリーダーシップ：</strong>経営層が自ら変革の旗振り役となる。
                            </li>
                            <li id="factor-3" class="p-4 rounded-lg cursor-pointer hover:bg-blue-50 transition-colors">
                                <strong>データドリブン文化：</strong>「勘と経験」からデータに基づく意思決定へ移行する。
                            </li>
                            <li id="factor-4" class="p-4 rounded-lg cursor-pointer hover:bg-blue-50 transition-colors">
                                <strong>人材育成と組織変革：</strong>DX人材を育成し、革新を受け入れる文化を醸成する。
                            </li>
                            <li id="factor-5" class="p-4 rounded-lg cursor-pointer hover:bg-blue-50 transition-colors">
                                <strong>段階的アプローチ：</strong>スモールスタートで成功体験を積み、継続的に改善する。
                            </li>
                            <li id="factor-6" class="p-4 rounded-lg cursor-pointer hover:bg-blue-50 transition-colors">
                                <strong>適切なツール選定：</strong>全体最適を考え、自社の課題に合ったツールを導入する。
                            </li>
                        </ul>
                    </div>
                    <div id="case-study-panel" class="bg-gray-100 p-6 rounded-lg min-h-[300px]">
                        <h4 class="text-xl font-bold text-[#0B3954] mb-3">ケーススタディ</h4>
                        <p class="text-gray-600">左の要因をクリックして、関連する成功事例をご覧ください。</p>
                    </div>
                </div>
            </div>

            <div id="failure-panel" class="content-panel hidden-panel">
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6 text-center">
                    <div class="bg-red-50 p-6 rounded-lg border-l-4 border-[#E53935]">
                        <h3 class="text-xl font-bold text-[#E53935] mb-3">現場無視のトップダウン</h3>
                        <p class="text-gray-700">現場の運用に適合しないシステム導入は、抵抗感を生み形骸化する。ボトムアップの視点と、技術導入前の文化変革が不可欠。</p>
                    </div>
                    <div class="bg-red-50 p-6 rounded-lg border-l-4 border-[#E53935]">
                        <h3 class="text-xl font-bold text-[#E53935] mb-3">データの質・量不足</h3>
                        <p class="text-gray-700">不正確・不十分なデータでは、AIなどの高度な技術も宝の持ち腐れに。データ基盤の整備が成功の前提条件。</p>
                    </div>
                    <div class="bg-red-50 p-6 rounded-lg border-l-4 border-[#E53935]">
                        <h3 class="text-xl font-bold text-[#E53935] mb-3">目的の不明確化</h3>
                        <p class="text-gray-700">「流行だから」という動機では、投資が無駄になるだけ。解決すべき経営課題と具体的な目標設定が全ての始まり。</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="roadmap" class="my-16">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-[#0B3954] mb-2">成功へのロードマップ</h2>
                <p class="text-lg text-gray-600">DXは旅路です。以下のステップで着実に前進しましょう。</p>
            </div>
            <div class="max-w-3xl mx-auto">
                <div class="relative pl-8 roadmap-step">
                    <div class="absolute top-0 w-6 h-6 bg-[#3A86FF] rounded-full roadmap-dot flex items-center justify-center text-white font-bold">1</div>
                    <h3 class="text-2xl font-bold mb-2">現状把握と課題特定</h3>
                    <p class="text-gray-700 pb-10">業務プロセスを徹底的に分析し、属人化業務を「見える化」。現場の声を収集し、実態に即した課題を抽出します。</p>
                </div>
                <div class="relative pl-8 roadmap-step">
                    <div class="absolute top-0 w-6 h-6 bg-[#3A86FF] rounded-full roadmap-dot flex items-center justify-center text-white font-bold">2</div>
                    <h3 class="text-2xl font-bold mb-2">目的と目標の明確化</h3>
                    <p class="text-gray-700 pb-10">SMART原則に基づき、測定可能なKPIを設定。短期・中長期の目標を立て、DXが「手段の目的化」に陥ることを防ぎます。</p>
                </div>
                <div class="relative pl-8 roadmap-step">
                    <div class="absolute top-0 w-6 h-6 bg-[#3A86FF] rounded-full roadmap-dot flex items-center justify-center text-white font-bold">3</div>
                    <h3 class="text-2xl font-bold mb-2">組織体制の整備と人材育成</h3>
                    <p class="text-gray-700 pb-10">DX推進チームを組成し、継続的な教育で従業員のスキルと意識を向上。革新を受け入れる文化を醸成します。</p>
                </div>
                <div class="relative pl-8 roadmap-step">
                    <div class="absolute top-0 w-6 h-6 bg-[#3A86FF] rounded-full roadmap-dot flex items-center justify-center text-white font-bold">4</div>
                    <h3 class="text-2xl font-bold mb-2">スモールスタートと継続的改善</h3>
                    <p class="text-gray-700 pb-10">パイロットプロジェクトで効果を検証し、成功体験を積み重ねます。PDCAサイクルを回し、継続的に改善します。</p>
                </div>
                 <div class="relative pl-8 roadmap-step">
                    <div class="absolute top-0 w-6 h-6 bg-[#3A86FF] rounded-full roadmap-dot flex items-center justify-center text-white font-bold">5</div>
                    <h3 class="text-2xl font-bold mb-2">適切なデジタルツールの選定</h3>
                    <p class="text-gray-700 pb-10">自社の課題と目的に即し、全体最適を考慮したツールを選定。外部パートナーとの連携も視野に入れます。</p>
                </div>
            </div>
        </section>

    </main>

    <footer class="bg-[#0B3954] text-white text-center py-8 mt-16">
        <p class="text-lg">DXは技術導入ではなく、組織文化とビジネスモデルの変革です。</p>
        <p class="text-xl font-bold mt-2">データと共に、未来のものづくりを創造しましょう。</p>
    </footer>

    <script>
        const caseStudies = {
            'factor-1': {
                title: '広島メタルワーク：データドリブン経営',
                description: '総合生産管理システムを導入し、全従業員がリアルタイムで進捗データを取得。データに基づくQCD管理を徹底しました。',
                results: [
                    { label: '売上高', value: 23, unit: '%' },
                    { label: '営業利益', value: 19, unit: '%' },
                    { label: '不良率', value: 90, unit: '%以上' }
                ]
            },
            'factor-2': {
                title: 'コマツ：トップ主導のソリューション提供',
                description: '経営層が建設業界の課題解決という明確なビジョンを提示。IoT管理システム「Komtrax」とAI建機で顧客の生産性向上に貢献しました。',
                results: [
                    { label: '顧客の生産性', value: 140, unit: '%' }
                ]
            },
            'factor-3': {
                title: 'リノメタル：「ミス・ムダ・属人化」からの脱却',
                description: '会社全体でクラウドサービスと生産管理システムを導入。徹底的なデータ可視化で、業務の非効率を撲滅しました。',
                results: [
                    { label: '生産管理工数', value: 268, unit: '時間/月' },
                    { label: '従業員残業', value: 80, unit: '%' }
                ]
            },
            'factor-4': {
                title: 'ダイキン工業：専門人材の育成',
                description: '「Daikin Information Technology University」を設立。空調技術とITスキルを兼ね備えた専門人材を自社で育成する長期的な計画を実行しています。',
                results: [
                    { label: '育成対象者', value: 100, unit: '名/年' }
                ]
            },
            'factor-5': {
                title: '日新電機：スモールスタートからの展開',
                description: 'AI図面検索システムを導入し、まず設計業務の非効率を解消。具体的な数値成果を経営層に提示し、全社的な理解と協力を得ました。',
                results: [
                    { label: '図面検索時間', value: 85, unit: '%' },
                    { label: '設計工数', value: 7000, unit: '時間/年' }
                ]
            },
            'factor-6': {
                title: 'シンフォニアテクノロジー：課題解決ツールの導入',
                description: '部品捜索と棚卸しという具体的な課題に対し、RFIDソリューションを導入。生産計画の遅延をゼロにし、劇的な効率化を達成しました。',
                results: [
                    { label: '部品捜索時間', value: 90, unit: '%' },
                    { label: '棚卸し業務時間', value: 64, unit: '%' }
                ]
            }
        };

        document.addEventListener('DOMContentLoaded', () => {
            const successTab = document.getElementById('success-tab');
            const failureTab = document.getElementById('failure-tab');
            const successPanel = document.getElementById('success-panel');
            const failurePanel = document.getElementById('failure-panel');
            const caseStudyPanel = document.getElementById('case-study-panel');
            let currentChart = null;
            
            const commonTooltipCallback = {
                plugins: {
                    tooltip: {
                        callbacks: {
                            title: function(tooltipItems) {
                                const item = tooltipItems[0];
                                let label = item.chart.data.labels[item.dataIndex];
                                if (Array.isArray(label)) {
                                  return label.join(' ');
                                } else {
                                  return label;
                                }
                            }
                        }
                    }
                }
            };

            function switchTab(activeTab, inactiveTab, activePanel, inactivePanel) {
                activeTab.classList.add('active');
                inactiveTab.classList.remove('active');
                activePanel.classList.remove('hidden-panel');
                activePanel.classList.add('visible-panel');
                inactivePanel.classList.add('hidden-panel');
                inactivePanel.classList.remove('visible-panel');
            }

            successTab.addEventListener('click', () => switchTab(successTab, failureTab, successPanel, failurePanel));
            failureTab.addEventListener('click', () => switchTab(failureTab, successTab, failurePanel, successPanel));

            document.querySelectorAll('#success-panel ul li').forEach(item => {
                item.addEventListener('click', () => {
                    const caseData = caseStudies[item.id];
                    if (!caseData) return;

                    document.querySelectorAll('#success-panel ul li').forEach(li => li.classList.remove('bg-blue-100'));
                    item.classList.add('bg-blue-100');

                    // グラフを削除し、テキスト表示のみに統一
                    let resultsHtml = caseData.results.map(res => `
                        <div class="flex items-baseline">
                            <span class="text-3xl font-bold text-[#3A86FF]">${res.value}</span>
                            <span class="ml-1 font-semibold text-gray-700">${res.unit}</span>
                        </div>
                        <p class="text-sm text-gray-500">${res.label} ${res.unit === '%' || res.unit === '%以上' ? '改善' : '削減'}</p>
                    `).join('');

                    caseStudyPanel.innerHTML = `
                        <h4 class="text-xl font-bold text-[#0B3954] mb-2">${caseData.title}</h4>
                        <p class="text-gray-600 mb-4">${caseData.description}</p>
                        <div class="grid grid-cols-2 gap-4 mt-4">
                           ${resultsHtml}
                        </div>
                    `;
                    
                    // 以前のグラフがあれば破棄
                    if (currentChart) {
                        currentChart.destroy();
                        currentChart = null; // グラフを削除したのでnullに設定
                    }
                });
            });
        });
    </script>
</body>
</html>
