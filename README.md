<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>恋爱体质测试 - 你的恋爱DNA大揭秘！</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@400;500;700;900&display=swap" rel="stylesheet">
    <style>
        /* ==================== 全局样式 ==================== */
        :root {
            --primary-color: #FF6B9D;
            --secondary-color: #FF8E53;
            --accent-color: #FEC163;
            --purple: #A855F7;
            --bg-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            --card-bg: rgba(255, 255, 255, 0.95);
            --text-primary: #1F2937;
            --text-secondary: #6B7280;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Noto Sans SC', -apple-system, BlinkMacSystemFont, sans-serif;
            min-height: 100vh;
            background: var(--bg-gradient);
            color: var(--text-primary);
            overflow-x: hidden;
            position: relative;
        }

        /* 背景装饰 */
        .bg-decorations {
            position: fixed;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
            overflow: hidden;
        }

        .floating-emoji {
            position: absolute;
            font-size: 2rem;
            opacity: 0.15;
            animation: float 20s infinite ease-in-out;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-100px) rotate(180deg); }
        }

        /* 主容器 */
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* 页面切换 */
        .page {
            display: none;
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.4s ease;
        }

        .page.active {
            display: flex;
            flex-direction: column;
            opacity: 1;
            transform: translateY(0);
        }

        /* ==================== 首页样式 ==================== */
        .home-page {
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 40px 20px;
            flex-grow: 1;
        }

        .logo {
            font-size: 4rem;
            margin-bottom: 20px;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        .title {
            font-size: 2.5rem;
            font-weight: 900;
            color: white;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .subtitle {
            font-size: 1.2rem;
            color: rgba(255,255,255,0.9);
            margin-bottom: 30px;
        }

        .intro-card {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 30px;
            margin: 30px 0;
            box-shadow: 0 20px 60px rgba(0,0,0,0.15);
            backdrop-filter: blur(10px);
        }

        .intro-title {
            font-size: 1.4rem;
            color: var(--primary-color);
            margin-bottom: 15px;
            font-weight: 700;
        }

        .intro-content {
            font-size: 1rem;
            line-height: 1.8;
            color: var(--text-secondary);
            margin-bottom: 20px;
            text-align: left;
        }

        .intro-content p {
            margin-bottom: 12px;
        }

        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .feature-item {
            background: linear-gradient(135deg, #FF6B9D 0%, #FF8E53 100%);
            padding: 25px;
            border-radius: 15px;
            color: white;
            text-align: center;
            transition: transform 0.3s ease;
        }

        .feature-item:hover {
            transform: translateY(-5px);
        }

        .feature-icon {
            font-size: 3rem;
            margin-bottom: 10px;
        }

        .feature-text {
            font-weight: 600;
            font-size: 1.1rem;
        }

        .slogan {
            font-size: 1.5rem;
            color: #FEC163;
            font-weight: 700;
            margin: 30px 0;
            font-style: italic;
        }

        .btn-start {
            background: linear-gradient(135deg, #FF6B9D 0%, #FF8E53 100%);
            color: white;
            border: none;
            padding: 18px 50px;
            font-size: 1.3rem;
            font-weight: 700;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 10px 30px rgba(255, 107, 157, 0.4);
        }

        .btn-start:hover {
            transform: translateY(-3px) scale(1.05);
            box-shadow: 0 15px 40px rgba(255, 107, 157, 0.6);
        }

        /* ==================== 测试页面样式 ==================== */
        .test-page {
            align-items: center;
            justify-content: center;
            flex-grow: 1;
            padding: 20px;
        }

        .progress-container {
            width: 100%;
            max-width: 500px;
            margin-bottom: 30px;
        }

        .progress-bar {
            width: 100%;
            height: 10px;
            background: rgba(255,255,255,0.3);
            border-radius: 5px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #FF6B9D, #FF8E53);
            border-radius: 5px;
            transition: width 0.5s ease;
        }

        .progress-text {
            text-align: center;
            color: white;
            font-weight: 600;
            margin-top: 10px;
            font-size: 1.1rem;
        }

        .question-card {
            background: var(--card-bg);
            border-radius: 25px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.15);
            width: 100%;
            max-width: 600px;
            margin-bottom: 30px;
            backdrop-filter: blur(10px);
        }

        .question-emoji {
            font-size: 4rem;
            text-align: center;
            margin-bottom: 20px;
        }

        .question-text {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--text-primary);
            text-align: center;
            line-height: 1.5;
            margin-bottom: 30px;
        }

        .options-container {
            display: flex;
            flex-direction: column;
            gap: 15px;
            width: 100%;
            max-width: 600px;
        }

        .option-btn {
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            border: 2px solid transparent;
            padding: 20px 25px;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1.1rem;
            color: var(--text-primary);
            text-align: left;
            position: relative;
            overflow: hidden;
        }

        .option-btn:hover {
            background: linear-gradient(135deg, #FFE4EC 0%, #FFF4E6 100%);
            border-color: var(--primary-color);
            transform: translateX(5px);
        }

        .option-btn.selected {
            background: linear-gradient(135deg, #FF6B9D 0%, #FF8E53 100%);
            color: white;
            border-color: transparent;
        }

        .option-emoji {
            font-size: 1.5rem;
            margin-right: 12px;
        }

        .option-text {
            flex-grow: 1;
        }

        /* 点击动画 */
        .option-btn.clicked {
            animation: clickEffect 0.4s ease;
        }

        @keyframes clickEffect {
            0% { transform: scale(1); }
            50% { transform: scale(0.95); }
            100% { transform: scale(1); }
        }

        /* 页面切换动画 */
        .slide-out {
            animation: slideOut 0.4s ease forwards;
        }

        .slide-in {
            animation: slideIn 0.4s ease forwards;
        }

        @keyframes slideOut {
            to { opacity: 0; transform: translateX(-50px); }
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateX(50px); }
            to { opacity: 1; transform: translateX(0); }
        }

        /* ==================== 结果页面样式 ==================== */
        .result-page {
            align-items: center;
            padding: 20px;
        }

        .result-header {
            text-align: center;
            margin-bottom: 40px;
        }

        .result-title {
            font-size: 2rem;
            font-weight: 900;
            color: white;
            margin-bottom: 10px;
        }

        .score-container {
            background: linear-gradient(135deg, #FF6B9D 0%, #FF8E53 100%);
            padding: 40px 60px;
            border-radius: 25px;
            text-align: center;
            margin: 30px 0;
            box-shadow: 0 20px 60px rgba(255, 107, 157, 0.4);
        }

        .score-number {
            font-size: 4.5rem;
            font-weight: 900;
            color: white;
            display: block;
            animation: scoreReveal 1.5s ease;
        }

        @keyframes scoreReveal {
            0% { transform: scale(0); opacity: 0; }
            50% { transform: scale(1.2); }
            100% { transform: scale(1); opacity: 1; }
        }

        .score-label {
            color: rgba(255,255,255,0.9);
            font-size: 1.2rem;
            font-weight: 600;
        }

        .result-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            width: 100%;
            max-width: 800px;
            margin-bottom: 30px;
        }

        .result-card {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
            backdrop-filter: blur(10px);
            transition: transform 0.3s ease;
        }

        .result-card:hover {
            transform: translateY(-5px);
        }

        .card-icon {
            font-size: 3rem;
            margin-bottom: 15px;
            display: block;
        }

        .card-title {
            font-size: 1.3rem;
            font-weight: 700;
            color: var(--primary-color);
            margin-bottom: 15px;
        }

        .card-content {
            color: var(--text-secondary);
            line-height: 1.8;
        }

        .highlight {
            color: var(--primary-color);
            font-weight: 700;
        }

        /* 数据可视化 */
        .charts-section {
            width: 100%;
            max-width: 800px;
            margin-bottom: 30px;
        }

        .chart-container {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }

        .chart-title {
            text-align: center;
            font-size: 1.3rem;
            font-weight: 700;
            color: var(--primary-color);
            margin-bottom: 25px;
        }

        .bar-chart {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .bar-item {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .bar-label {
            width: 120px;
            font-weight: 600;
            color: var(--text-secondary);
            font-size: 0.95rem;
        }

        .bar-track {
            flex: 1;
            height: 16px;
            background: #f0f0f0;
            border-radius: 8px;
            overflow: hidden;
        }

        .bar-fill {
            height: 100%;
            border-radius: 8px;
            transition: width 1s ease;
            position: relative;
        }

        .bar-value {
            width: 50px;
            font-weight: 700;
            color: var(--text-primary);
            font-size: 0.95rem;
        }

        /* 按钮组 */
        .button-group {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            justify-content: center;
            margin: 30px 0;
        }

        .btn-action {
            padding: 15px 35px;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            border: none;
            box-shadow: 0 5px 20px rgba(0,0,0,0.15);
        }

        .btn-share {
            background: linear-gradient(135deg, #10B981 0%, #059669 100%);
            color: white;
        }

        .btn-share:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 30px rgba(16, 185, 129, 0.4);
        }

        .btn-retake {
            background: linear-gradient(135deg, #8B5CF6 0%, #6D28D9 100%);
            color: white;
        }

        .btn-retake:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 30px rgba(139, 92, 246, 0.4);
        }

        /* Toast提示 */
        .toast {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%) translateY(100px);
            background: #1F2937;
            color: white;
            padding: 15px 30px;
            border-radius: 10px;
            font-weight: 600;
            z-index: 1000;
            transition: all 0.3s ease;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        .toast.show {
            transform: translateX(-50%) translateY(0);
        }

        /* ==================== 页脚样式 ==================== */
        .footer {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            padding: 30px 20px;
            text-align: center;
            color: white;
            margin-top: auto;
            border-radius: 20px 20px 0 0;
        }

        .footer-content {
            max-width: 800px;
            margin: 0 auto;
        }

        .footer-text {
            font-size: 0.9rem;
            opacity: 0.9;
            line-height: 1.8;
            margin-bottom: 15px;
        }

        .footer-links {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
            font-size: 0.85rem;
        }

        .footer-link {
            color: rgba(255,255,255,0.8);
            text-decoration: none;
            transition: color 0.3s ease;
        }

        .footer-link:hover {
            color: #FEC163;
        }

        /* ==================== 响应式设计 ==================== */
        @media (max-width: 768px) {
            .title {
                font-size: 2rem;
            }
            
            .logo {
                font-size: 3rem;
            }
            
            .question-card {
                padding: 30px 20px;
            }
            
            .question-text {
                font-size: 1.3rem;
            }
            
            .option-btn {
                padding: 15px 20px;
                font-size: 1rem;
            }
            
            .result-cards {
                grid-template-columns: 1fr;
            }
            
            .score-number {
                font-size: 3.5rem;
            }
            
            .button-group {
                flex-direction: column;
                align-items: stretch;
            }
            
            .bar-label {
                width: 90px;
                font-size: 0.85rem;
            }
        }

        @media (max-width: 480px) {
            .container {
                padding: 15px;
            }
            
            .intro-card {
                padding: 20px;
            }
            
            .features {
                grid-template-columns: 1fr;
            }
            
            .btn-start {
                padding: 15px 40px;
                font-size: 1.1rem;
            }
            
            .score-container {
                padding: 30px 40px;
            }
        }

        /* 加载动画 */
        .loading {
            display: none;
            text-align: center;
            padding: 40px;
        }

        .loading.active {
            display: block;
        }

        .spinner {
            width: 50px;
            height: 50px;
            border: 4px solid #f3f3f3;
            border-top: 4px solid #FF6B9D;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 0 auto;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <!-- 背景装饰 -->
    <div class="bg-decorations" id="bgDecorations"></div>

    <!-- 主容器 -->
    <div class="container">
        <!-- 首页 -->
        <div class="page home-page active" id="homePage">
            <div class="logo">💕</div>
            <h1 class="title">恋爱体质测试</h1>
            <p class="subtitle">你的恋爱DNA大揭秘！</p>
            
            <div class="intro-card">
                <h2 class="intro-title">🎯 什么是恋爱体质测试？</h2>
                <div class="intro-content">
                    <p>🧬 恋爱体质测试是一套专业的心理评估工具，通过25道精心设计的幽默风趣题目，深度解析你的恋爱人格特质、依恋模式、情感需求等核心维度。</p>
                    <p>🎪 我们将心理学专业理论与网络热梗、神评论巧妙融合，让你在欢声笑语中完成科学评估，了解自己在爱情中的真实面貌。</p>
                </div>

                <h2 class="intro-title">❓ 为什么要做这个测试？</h2>
                <div class="intro-content">
                    <p>✅ <strong>了解自己：</strong>发现你的恋爱优势和盲点，认识真实的恋爱人格</p>
                    <p>✅ <strong>寻找真爱：</strong>了解自己适合什么样的伴侣，提高恋爱成功率</p>
                    <p>✅ <strong>改善关系：</strong>识别关系中的问题，获得针对性的成长建议</p>
                    <p>✅ <strong>娱乐放松：</strong>在测试过程中享受幽默风趣的题目设计，收获快乐</p>
                </div>

                <div class="features">
                    <div class="feature-item">
                        <div class="feature-icon">🧠</div>
                        <div class="feature-text">专业科学</div>
                    </div>
                    <div class="feature-item">
                        <div class="feature-icon">😂</div>
                        <div class="feature-text">幽默风趣</div>
                    </div>
                    <div class="feature-item">
                        <div class="feature-icon">📊</div>
                        <div class="feature-text">多维分析</div>
                    </div>
                    <div class="feature-item">
                        <div class="feature-icon">💡</div>
                        <div class="feature-text">精准解读</div>
                    </div>
                </div>
            </div>

            <p class="slogan">"你的恋爱体质，决定了你能遇见什么样的爱情 💫"</p>
            <button class="btn-start" onclick="startTest()">🚀 开始测试</button>
        </div>

        <!-- 测试页面 -->
        <div class="page test-page" id="testPage">
            <div class="progress-container">
                <div class="progress-bar">
                    <div class="progress-fill" id="progressFill"></div>
                </div>
                <div class="progress-text" id="progressText">1/25题</div>
            </div>

            <div class="question-card" id="questionCard">
                <div class="question-emoji" id="questionEmoji">🤔</div>
                <h3 class="question-text" id="questionText">题目加载中...</h3>
                <div class="options-container" id="optionsContainer"></div>
            </div>

            <div class="loading" id="loading">
                <div class="spinner"></div>
                <p style="margin-top: 20px; color: white; font-weight: 600;">正在分析你的恋爱DNA...</p>
            </div>
        </div>

        <!-- 结果页面 -->
        <div class="page result-page" id="resultPage">
            <div class="result-header">
                <h2 class="result-title">🎉 测试结果</h2>
                <p style="color: rgba(255,255,255,0.9);">基于25道题的专业分析</p>
            </div>

            <div class="score-container">
                <span class="score-number" id="scoreNumber">0</span>
                <span class="score-label">恋爱体质得分</span>
            </div>

            <div class="result-cards">
                <div class="result-card">
                    <span class="card-icon">🎭</span>
                    <h3 class="card-title">恋爱人格类型</h3>
                    <div class="card-content" id="personalityType"></div>
                </div>

                <div class="result-card">
                    <span class="card-icon">💝</span>
                    <h3 class="card-title">恋爱核心特质</h3>
                    <div class="card-content" id="coreTraits"></div>
                </div>

                <div class="result-card">
                    <span class="card-icon">🔥</span>
                    <h3 class="card-title">恋爱占有欲类型</h3>
                    <div class="card-content" id="possessivenessType"></div>
                </div>

                <div class="result-card">
                    <span class="card-icon">💞</span>
                    <h3 class="card-title">恋爱依恋人格</h3>
                    <div class="card-content" id="attachmentType"></div>
                </div>
            </div>

            <div class="charts-section">
                <div class="chart-container">
                    <h3 class="chart-title">📊 六维恋爱能力分析</h3>
                    <div class="bar-chart" id="barChart"></div>
                </div>
            </div>

            <div class="button-group">
                <button class="btn-action btn-share" onclick="shareResult()">📤 分享结果</button>
                <button class="btn-action btn-retake" onclick="retakeTest()">🔄 重新测试</button>
            </div>
        </div>

        <!-- 页脚 -->
        <footer class="footer">
            <div class="footer-content">
                <p class="footer-text">
                    💝 恋爱体质测试 - 你的专业恋爱顾问<br>
                    本测试仅供娱乐和参考，结果不构成任何医疗或心理诊断建议。<br>
                    如遇感情问题，建议寻求专业心理咨询师的帮助。
                </p>
                <div class="footer-links">
                    <a href="#" class="footer-link">关于我们</a>
                    <a href="#" class="footer-link">隐私政策</a>
                    <a href="#" class="footer-link">使用条款</a>
                    <a href="#" class="footer-link">联系方式</a>
                </div>
                <p style="margin-top: 20px; font-size: 0.8rem; opacity: 0.7;">
                    © 恋爱体质测试 | 用科学解读爱情，用幽默温暖人生 ❤️
                </p>
            </div>
        </footer>
    </div>

    <!-- Toast提示 -->
    <div class="toast" id="toast"></div>

    <script>
        // ==================== 题目数据 ====================
        const questions = [
            {
                emoji: "💭",
                question: "当你第一次见到心动的人，第一反应是？",
                options: [
                    { emoji: "😵", text: "大脑短路，智商瞬间清零", score: 8 },
                    { emoji: "🕵️", text: "暗中观察，开始搜集TA的情报", score: 6 },
                    { emoji: "😎", text: "保持高冷，内心慌得一批", score: 5 },
                    { emoji: "🤳", text: "假装看手机，实则疯狂偷拍", score: 7 }
                ]
            },
            {
                emoji: "🎁",
                question: "情人节礼物，你会选择？",
                options: [
                    { emoji: "💎", text: "奢侈品，贵就完事了！", score: 9 },
                    { emoji: "🎨", text: "DIY手工，心意无价", score: 8 },
                    { emoji: "🧧", text: "直接发红包，简单粗暴", score: 5 },
                    { emoji: "📱", text: "问TA想要啥，精准投喂", score: 6 }
                ]
            },
            {
                emoji: "🤳",
                question: "对方突然不回消息，你会？",
                options: [
                    { emoji: "📞", text: "夺命连环call，直到TA接为止", score: 9 },
                    { emoji: "🧘", text: "淡定淡定，可能是没电了吧", score: 4 },
                    { emoji: "🎭", text: "表面云淡风轻，内心已经脑补出一部狗血剧", score: 7 },
                    { emoji: "🌙", text: "睡觉睡觉，手机关机", score: 3 }
                ]
            },
            {
                emoji: "📸",
                question: "情侣头像，你的态度是？",
                options: [
                    { emoji: "💑", text: "必须安排！这可是官宣神器", score: 8 },
                    { emoji: "🤔", text: "看情况，不要那么张扬", score: 5 },
                    { emoji: "🙅", text: "拒绝！我的头像代表我的灵魂", score: 3 },
                    { emoji: "😏", text: "偷偷用，别让人发现", score: 6 }
                ]
            },
            {
                emoji: "💪",
                question: "伴侣和异性朋友吃饭，你的反应？",
                options: [
                    { emoji: "🚫", text: "绝对不行！这是原则问题", score: 10 },
                    { emoji: "🤷", text: "正常社交，我相信TA", score: 3 },
                    { emoji: "👀", text: "只要提前报备，我OK", score: 5 },
                    { emoji: "😏", text: "暗中跟随，来个突击检查", score: 8 }
                ]
            },
            {
                emoji: "🍿",
                question: "约会看电影，你更喜欢？",
                options: [
                    { emoji: "🤗", text: "全程抱抱，电影是啥不重要", score: 8 },
                    { emoji: "🎬", text: "认真看电影，看完讨论剧情", score: 5 },
                    { emoji: "💬", text: "边看边吐槽，自带弹幕", score: 6 },
                    { emoji: "😴", text: "电影院的沙发最适合睡觉", score: 4 }
                ]
            },
            {
                emoji: "🌙",
                question: "睡前的最后一条消息，你会发？",
                options: [
                    { emoji: "💕", text: "甜言蜜语，土味情话走起", score: 8 },
                    { emoji: "😴", text: "一个表情包完事", score: 4 },
                    { emoji: "📱", text: "晚安，明天见", score: 5 },
                    { emoji: "🤔", text: "假装睡着了，其实还在等消息", score: 7 }
                ]
            },
            {
                emoji: "🥘",
                question: "第一次去TA家见父母，你会？",
                options: [
                    { emoji: "😰", text: "紧张到脚趾抠地", score: 6 },
                    { emoji: "📝", text: "做足功课，准备见面礼", score: 7 },
                    { emoji: "😎", text: "大大方方，自信满满", score: 8 },
                    { emoji: "🏃", text: "找借口推迟，能拖就拖", score: 4 }
                ]
            },
            {
                emoji: "🔥",
                question: "吵架后，你通常会？",
                options: [
                    { emoji: "😤", text: "冷战到底，看谁先低头", score: 8 },
                    { emoji: "🤝", text: "主动求和，感情要紧", score: 5 },
                    { emoji: "🎤", text: "冷静沟通，解决问题", score: 7 },
                    { emoji: "📱", text: "发朋友圈内涵一下", score: 9 }
                ]
            },
            {
                emoji: "💼",
                question: "伴侣工作很忙经常加班，你会？",
                options: [
                    { emoji: "😤", text: "抱怨TA没时间陪我", score: 8 },
                    { emoji: "👍", text: "表示理解，默默支持", score: 5 },
                    { emoji: "☕", text: "去公司送奶茶，刷存在感", score: 6 },
                    { emoji: "📱", text: "既然忙那我也玩我的", score: 4 }
                ]
            },
            {
                emoji: "🏖️",
                question: "旅行时你的风格是？",
                options: [
                    { emoji: "📋", text: "详细攻略，按计划执行", score: 6 },
                    { emoji: "🌊", text: "随心所欲，走到哪算哪", score: 7 },
                    { emoji: "🛏️", text: "酒店躺尸，哪都不去", score: 4 },
                    { emoji: "📸", text: "疯狂拍照，发朋友圈重要", score: 8 }
                ]
            },
            {
                emoji: "🎂",
                question: "伴侣生日，你的庆祝方式？",
                options: [
                    { emoji: "🎉", text: "安排惊喜派对，邀请所有朋友", score: 8 },
                    { emoji: "🕯️", text: "烛光晚餐，只有我们俩", score: 6 },
                    { emoji: "🎁", text: "送个礼物，简单说句生日快乐", score: 4 },
                    { emoji: "💰", text: "转账520，简单粗暴", score: 5 }
                ]
            },
            {
                emoji: "📱",
                question: "查看伴侣手机，你觉得？",
                options: [
                    { emoji: "🔓", text: "没啥不能看的，随便翻", score: 4 },
                    { emoji: "🚫", text: "坚决不查，信任最重要", score: 6 },
                    { emoji: "👀", text: "偶尔偷看，别被发现就行", score: 7 },
                    { emoji: "🤔", text: "想查但不敢，怕看到不该看的", score: 8 }
                ]
            },
            {
                emoji: "💄",
                question: "伴侣夸别的异性好看，你会？",
                options: [
                    { emoji: "🔥", text: "当场炸毛，'那你去追TA啊'", score: 9 },
                    { emoji: "😌", text: "淡定淡定，谁还没眼光", score: 5 },
                    { emoji: "😏", text: "暗戳戳吃醋，但不说出来", score: 7 },
                    { emoji: "🤳", text: "立即自拍，'看看我更好看'", score: 6 }
                ]
            },
            {
                emoji: "🎮",
                question: "周末宅家，你们会？",
                options: [
                    { emoji: "🎮", text: "一起打游戏，开黑上分", score: 6 },
                    { emoji: "📱", text: "各玩各的手机，偶尔说几句话", score: 4 },
                    { emoji: "🍿", text: "一起追剧，吃零食聊天", score: 7 },
                    { emoji: "🛏️", text: "从早睡到晚，这就是幸福", score: 5 }
                ]
            },
            {
                emoji: "🎤",
                question: "去KTV，你的表现是？",
                options: [
                    { emoji: "🎤", text: "麦霸上身，不让别人唱", score: 7 },
                    { emoji: "👏", text: "只听不唱，做忠实观众", score: 4 },
                    { emoji: "🎵", text: "只唱情歌，每首都是给TA的", score: 8 },
                    { emoji: "😴", text: "找个角落睡觉", score: 3 }
                ]
            },
            {
                emoji: "🐶",
                question: "关于养宠物，你会？",
                options: [
                    { emoji: "🐕", text: "必须养狗，忠诚又可爱", score: 6 },
                    { emoji: "🐱", text: "必须养猫，高冷有性格", score: 6 },
                    { emoji: "🙅", text: "不养不养，太麻烦了", score: 4 },
                    { emoji: "💕", text: "养什么都行，主要是和TA一起照顾", score: 8 }
                ]
            },
            {
                emoji: "💰",
                question: "关于经济问题，你的看法？",
                options: [
                    { emoji: "💳", text: "AA制，各花各的", score: 5 },
                    { emoji: "💰", text: "男方多出一些，表示照顾", score: 6 },
                    { emoji: "🏦", text: "建立共同账户，一起管理", score: 7 },
                    { emoji: "🤝", text: "有钱的多出，没钱的出力", score: 8 }
                ]
            },
            {
                emoji: "😴",
                question: "关于睡姿，你更喜欢？",
                options: [
                    { emoji: "🤗", text: "抱在一起睡，超有安全感", score: 8 },
                    { emoji: "😴", text: "各睡各的，互不打扰", score: 4 },
                    { emoji: "🤝", text: "偶尔抱抱，平时分开", score: 6 },
                    { emoji: "🤚", text: "一定要牵着手才能睡着", score: 9 }
                ]
            },
            {
                emoji: "🎭",
                question: "伴侣提出冷静一下，你会？",
                options: [
                    { emoji: "😭", text: "崩溃大哭，'你是不爱我了'", score: 9 },
                    { emoji: "🧘", text: "给TA空间，自己也冷静一下", score: 6 },
                    { emoji: "🤝", text: "立即沟通，解决问题最重要", score: 7 },
                    { emoji: "❄️", text: "好，那我也冷静一下", score: 5 }
                ]
            },
            {
                emoji: "💑",
                question: "公开恋情的方式，你会？",
                options: [
                    { emoji: "📱", text: "朋友圈官宣，让全世界都知道", score: 8 },
                    { emoji: "🤫", text: "低调低调，只告诉亲密朋友", score: 5 },
                    { emoji: "🤷", text: "对方想怎么公开就怎么公开", score: 4 },
                    { emoji: "🔒", text: "暂时保密，稳定了再说", score: 6 }
                ]
            },
            {
                emoji: "📖",
                question: "伴侣推荐你一本书/一部剧，你会？",
                options: [
                    { emoji: "📚", text: "立刻去看，因为TA推荐的", score: 8 },
                    { emoji: "👀", text: "看简介，感兴趣再看", score: 5 },
                    { emoji: "🤥", text: "假装看了，其实根本没看", score: 7 },
                    { emoji: "👫", text: "和TA一起看，边看边讨论", score: 9 }
                ]
            },
            {
                emoji: "✈️",
                question: "关于异地恋，你的态度是？",
                options: [
                    { emoji: "💔", text: "坚决不行，接受不了", score: 8 },
                    { emoji: "💕", text: "只要相爱，距离不是问题", score: 6 },
                    { emoji: "🌍", text: "挺好的，各自有自己的空间", score: 4 },
                    { emoji: "🚀", text: "想办法结束异地，这是目标", score: 7 }
                ]
            },
            {
                emoji: "📝",
                question: "你和伴侣的未来规划，你会？",
                options: [
                    { emoji: "💕", text: "从小细节到大方向，都想一起", score: 9 },
                    { emoji: "🤷", text: "顺其自然，船到桥头自然直", score: 4 },
                    { emoji: "🎯", text: "有大概方向，具体以后再说", score: 6 },
                    { emoji: "🤔", text: "不太敢想，怕失望", score: 7 }
                ]
            },
            {
                emoji: "🌹",
                question: "最后，你理想的恋爱状态是？",
                options: [
                    { emoji: "🔥", text: "热恋期永远不结束", score: 8 },
                    { emoji: "🌊", text: "细水长流，平淡是真", score: 5 },
                    { emoji: "🤝", text: "各自独立，又相互依赖", score: 7 },
                    { emoji: "💝", text: "我完全被爱包围", score: 9 }
                ]
            }
        ];

        // ==================== 全局变量 ====================
        let currentQuestion = 0;
        let totalScore = 0;
        let answers = [];
        
        // 维度分数
        let dimensions = {
            passion: 0,       // 热情度
            rationality: 0,   // 理性度
            emotional: 0,     // 情绪度
            possessiveness: 0,// 占有欲
            independence: 0,  // 独立性
            trust: 0          // 信任度
        };

        // ==================== 初始化 ====================
        document.addEventListener('DOMContentLoaded', function() {
            initBackgroundDecorations();
        });

        /**
         * 初始化背景装饰
         * 创建漂浮的emoji装饰元素
         */
        function initBackgroundDecorations() {
            const container = document.getElementById('bgDecorations');
            const emojis = ['💕', '💖', '💗', '💓', '❤️', '🌹', '✨', '💫'];
            
            for (let i = 0; i < 20; i++) {
                const emoji = document.createElement('span');
                emoji.className = 'floating-emoji';
                emoji.textContent = emojis[Math.floor(Math.random() * emojis.length)];
                emoji.style.left = Math.random() * 100 + '%';
                emoji.style.top = Math.random() * 100 + '%';
                emoji.style.animationDelay = Math.random() * 10 + 's';
                emoji.style.fontSize = (Math.random() * 2 + 1.5) + 'rem';
                container.appendChild(emoji);
            }
        }

        /**
         * 页面切换动画
         * @param {string} fromId - 当前页面ID
         * @param {string} toId - 目标页面ID
         */
        function switchPage(fromId, toId) {
            const fromPage = document.getElementById(fromId);
            const toPage = document.getElementById(toId);
            
            fromPage.classList.remove('active');
            setTimeout(() => {
                toPage.classList.add('active');
            }, 300);
        }

        /**
         * 开始测试
         * 从首页切换到测试页面，显示第一道题目
         */
        function startTest() {
            switchPage('homePage', 'testPage');
            setTimeout(() => {
                showQuestion(0);
            }, 400);
        }

        /**
         * 显示指定索引的题目
         * @param {number} index - 题目索引
         */
        function showQuestion(index) {
            const question = questions[index];
            const questionCard = document.getElementById('questionCard');
            const questionEmoji = document.getElementById('questionEmoji');
            const questionText = document.getElementById('questionText');
            const optionsContainer = document.getElementById('optionsContainer');
            
            // 添加进入动画
            questionCard.classList.remove('slide-in');
            void questionCard.offsetWidth; // 触发重绘
            questionCard.classList.add('slide-in');
            
            // 更新题目内容
            questionEmoji.textContent = question.emoji;
            questionText.textContent = question.question;
            
            // 清空并重新生成选项
            optionsContainer.innerHTML = '';
            
            question.options.forEach((option, optIndex) => {
                const button = document.createElement('button');
                button.className = 'option-btn';
                button.innerHTML = `
                    <span class="option-emoji">${option.emoji}</span>
                    <span class="option-text">${option.text}</span>
                `;
                
                // 单击进入下一题
                button.addEventListener('click', function() {
                    handleAnswer(index, optIndex, button);
                });
                
                optionsContainer.appendChild(button);
            });
            
            // 更新进度条
            updateProgress(index + 1);
        }

        /**
         * 处理用户选择
         * @param {number} questionIndex - 题目索引
         * @param {number} optionIndex - 选项索引
         * @param {HTMLElement} button - 按钮元素
         */
        function handleAnswer(questionIndex, optionIndex, button) {
            const question = questions[questionIndex];
            const option = question.options[optionIndex];
            
            // 记录答案
            answers.push({
                question: questionIndex,
                answer: optionIndex,
                score: option.score
            });
            
            // 累加总分
            totalScore += option.score;
            
            // 更新维度分数
            updateDimensions(questionIndex, option.score);
            
            // 添加点击动画效果
            button.classList.add('clicked');
            
            // 延迟后进入下一题
            setTimeout(() => {
                if (currentQuestion < questions.length - 1) {
                    currentQuestion++;
                    showQuestion(currentQuestion);
                } else {
                    showLoading();
                }
            }, 400);
        }

        /**
         * 更新各维度分数
         * 根据题目类型和得分更新相应维度
         * @param {number} questionIndex - 题目索引
         * @param {number} score - 得分
         */
        function updateDimensions(questionIndex, score) {
            // 根据题目类型分配到不同维度
            const category = getCategory(questionIndex);
            dimensions[category] += score;
        }

        /**
         * 获取题目所属分类
         * @param {number} index - 题目索引
         * @returns {string} 分类名称
         */
        function getCategory(index) {
            const categories = [
                'emotional',      // 0: 初次见面 - 情绪反应
                'passion',        // 1: 礼物 - 热情度
                'emotional',      // 2: 不回消息 - 情绪度
                'passion',        // 3: 情侣头像 - 热情度
                'possessiveness', // 4: 异性朋友 - 占有欲
                'passion',        // 5: 看电影 - 热情度
                'emotional',      // 6: 睡前消息 - 情绪度
                'rationality',    // 7: 见父母 - 理性度
                'rationality',    // 8: 吵架处理 - 理性度
                'trust',          // 9: 工作忙 - 信任度
                'independence',   // 10: 旅行 - 独立性
                'passion',        // 11: 生日 - 热情度
                'trust',          // 12: 查手机 - 信任度
                'possessiveness', // 13: 夸异性 - 占有欲
                'independence',   // 14: 周末宅家 - 独立性
                'passion',        // 15: KTV - 热情度
                'emotional',      // 16: 养宠物 - 情绪度
                'rationality',    // 17: 经济问题 - 理性度
                'emotional',      // 18: 睡姿 - 情绪度
                'emotional',      // 19: 冷静一下 - 情绪度
                'passion',        // 20: 公开恋情 - 热情度
                'trust',          // 21: 推荐内容 - 信任度
                'rationality',    // 22: 异地恋 - 理性度
                'rationality',    // 23: 未来规划 - 理性度
                'emotional'       // 24: 理想恋爱 - 情绪度
            ];
            
            return categories[index] || 'emotional';
        }

        /**
         * 更新进度条
         * @param {number} current - 当前题号
         */
        function updateProgress(current) {
            const progressFill = document.getElementById('progressFill');
            const progressText = document.getElementById('progressText');
            
            const percentage = (current / questions.length) * 100;
            progressFill.style.width = percentage + '%';
            progressText.textContent = `${current}/${questions.length}题`;
        }

        /**
         * 显示加载动画
         */
        function showLoading() {
            const questionCard = document.getElementById('questionCard');
            const loading = document.getElementById('loading');
            const progressContainer = document.querySelector('.progress-container');
            
            questionCard.style.display = 'none';
            progressContainer.style.display = 'none';
            loading.classList.add('active');
            
            // 模拟加载过程
            setTimeout(() => {
                loading.classList.remove('active');
                calculateResults();
                switchPage('testPage', 'resultPage');
                setTimeout(() => {
                    displayResults();
                }, 400);
            }, 2000);
        }

        /**
         * 计算测试结果
         * 分析各维度数据，生成结果
         */
        function calculateResults() {
            // 标准化分数到0-100
            const maxPossibleScore = questions.length * 10;
            const normalizedScore = Math.round((totalScore / maxPossibleScore) * 100);
            
            // 确定人格类型
            const personality = determinePersonality();
            
            // 确定核心特质
            const traits = determineTraits();
            
            // 确定占有欲类型
            const possessiveness = determinePossessiveness();
            
            // 确定依恋类型
            const attachment = determineAttachment();
            
            return {
                score: normalizedScore,
                personality,
                traits,
                possessiveness,
                attachment,
                dimensions
            };
        }

        /**
         * 确定恋爱人格类型
         * 基于各维度分数综合判断
         */
        function determinePersonality() {
            const { passion, rationality, emotional, possessiveness, independence, trust } = dimensions;
            
            // 计算各维度的相对强弱
            const maxDim = Math.max(passion, rationality, emotional, possessiveness, independence, trust);
            
            if (emotional === maxDim && passion > 40) {
                return {
                    type: "💖 热情浪漫型",
                    desc: "你是个天生的浪漫主义者！对爱情充满热情，情感表达直白热烈。在你眼中，爱情是生活的全部，你愿意为爱付出一切。但这种热烈的爱的同时也容易情绪化，学会适当控制情绪会让关系更和谐哦~"
                };
            } else if (rationality === maxDim && independence > 30) {
                return {
                    type: "🧠 理性独立型",
                    desc: "你是成熟的理性派！在爱情中保持头脑清醒，不会轻易被情绪左右。你有自己的生活和追求，不会因恋爱失去自我。这种特质让你在关系中更稳定，但偶尔也要展露柔软的一面，让对方感受到被需要。"
                };
            } else if (possessiveness > 40 && emotional > 35) {
                return {
                    type: "🔒 依恋粘人型",
                    desc: "你对伴侣有强烈的依赖和占有欲！一旦爱上就会全心全意，希望时刻与对方在一起。这种深情很动人，但过度的占有欲可能会让伴侣感到压力。学会给彼此空间，信任会让关系更轻松。"
                };
            } else if (independence === maxDim && rationality > 30) {
                return {
                    type: "🦅 自由洒脱型",
                    desc: "你追求自由平等的爱情！重视个人空间，不喜欢被束缚。最好的关系是两个独立的人相互扶持。这种特质很吸引人，但要警惕过度独立，该依赖时也要学会依赖。"
                };
            } else if (trust > 40) {
                return {
                    type: "💝 信任温暖型",
                    desc: "你拥有最健康的恋爱观！在关系中既给予爱也接受爱，懂得平衡亲密与独立。这种安全感让你和伴侣都能在关系中感到舒适和被珍惜。继续保持，你会收获幸福的爱情！"
                };
            } else {
                return {
                    type: "💫 平衡温和型",
                    desc: "你在各方面都很平衡！在热情与理性、依赖与独立之间找到了很好的平衡点。你的爱情稳定而温馨，是很多人羡慕的'细水长流'。继续保持，你的爱情会很长久~"
                };
            }
        }

        /**
         * 确定核心恋爱特质
         * 列出用户的主要恋爱特点
         */
        function determineTraits() {
            const traits = [];
            const { passion, rationality, emotional, possessiveness, independence, trust } = dimensions;
            
            if (passion > 35) {
                traits.push("🔥 对爱情充满热情，善于制造浪漫氛围");
            }
            if (rationality > 35) {
                traits.push("🧠 遇事冷静，能够理性分析和解决问题");
            }
            if (emotional > 35) {
                traits.push("💝 情感细腻，能够敏锐感知伴侣情绪");
            }
            if (possessiveness > 35) {
                traits.push("🎯 重视归属感，希望与伴侣建立深度连接");
            }
            if (independence > 35) {
                traits.push("🦅 有自己的生活追求，不会完全依附于伴侣");
            }
            if (trust > 35) {
                traits.push("💞 懂得信任，能够给予伴侣足够的空间");
            }
            
            if (traits.length === 0) {
                traits.push("🌱 正在成长中，有很大的恋爱潜力");
            }
            
            return traits.join("<br><br>");
        }

        /**
         * 确定占有欲类型
         * 基于possessiveness维度判断
         */
        function determinePossessiveness() {
            const { possessiveness } = dimensions;
            
            if (possessiveness > 45) {
                return {
                    type: "🔐 高占有欲型",
                    desc: "你的占有欲比较强，希望时刻了解伴侣的动向。这源于你对感情的重视和不安全感。试着学会信任对方，给彼此一些空间，关系会更轻松愉快。培养自己的兴趣爱好，减少对伴侣的过度依赖。"
                };
            } else if (possessiveness > 25) {
                return {
                    type: "🔒 中等占有欲型",
                    desc: "你的占有欲适中，既重视与伴侣的亲密关系，又能给对方适当的空间。这是比较健康的恋爱状态，懂得平衡亲密与自由。继续保持这种平衡，让关系稳定发展。"
                };
            } else {
                return {
                    type: "🔓 低占有欲型",
                    desc: "你的占有欲较低，非常尊重伴侣的个人空间和自由。这种特质让伴侣感到轻松，但有时可能会让对方觉得你不够在意。适当表达在意和关心，让对方感受到被重视。"
                };
            }
        }

        /**
         * 确定依恋人格类型
         * 基于emotional和trust维度判断
         */
        function determineAttachment() {
            const { emotional, trust, possessiveness, independence } = dimensions;
            
            if (emotional > 40 && possessiveness > 35 && independence < 25) {
                return {
                    type: "💕 焦虑依恋型",
                    desc: "你在感情中容易焦虑，害怕被抛弃，需要大量确认和安抚。你对伴侣有强烈的情感需求，渴望深度连接。学会自我安抚，建立自信心，减少对伴侣的过度依赖会让你更幸福。"
                };
            } else if (emotional < 25 && independence > 35 && trust > 30) {
                return {
                    type: "❄️ 回避依恋型",
                    desc: "你在感情中保持距离，害怕过于亲密会失去自我。你重视独立和自由，有时会让人觉得难以接近。尝试表达真实情感，学会接受亲密关系中的脆弱，会让关系更进一步。"
                };
            } else if (trust > 40 && emotional > 25 && possessiveness < 35) {
                return {
                    type: "✅ 安全依恋型",
                    desc: "恭喜你！你拥有最健康的依恋类型。在关系中既能够给予爱，也能够接受爱，懂得平衡亲密与独立。继续保持这种健康的恋爱模式，你会收获最幸福的爱情！"
                };
            } else {
                return {
                    type: "🎭 混合依恋型",
                    desc: "你的依恋类型比较复杂，不同情况下会有不同的表现。这说明你还在探索和成长中，这是正常的。多了解自己，在关系中慢慢找到最舒服的状态，爱情会越来越美好。"
                };
            }
        }

        /**
         * 显示测试结果
         * 在结果页面展示所有分析数据
         */
        function displayResults() {
            const results = calculateResults();
            
            // 显示总分动画
            animateScore(results.score);
            
            // 显示人格类型
            document.getElementById('personalityType').innerHTML = `
                <strong style="font-size: 1.2rem; color: var(--primary-color);">${results.personality.type}</strong><br><br>
                ${results.personality.desc}
            `;
            
            // 显示核心特质
            document.getElementById('coreTraits').innerHTML = results.traits;
            
            // 显示占有欲类型
            document.getElementById('possessivenessType').innerHTML = `
                <strong style="font-size: 1.2rem; color: var(--primary-color);">${results.possessiveness.type}</strong><br><br>
                ${results.possessiveness.desc}
            `;
            
            // 显示依恋类型
            document.getElementById('attachmentType').innerHTML = `
                <strong style="font-size: 1.2rem; color: var(--primary-color);">${results.attachment.type}</strong><br><br>
                ${results.attachment.desc}
            `;
            
            // 绘制柱状图
            drawBarChart();
        }

        /**
         * 分数动画效果
         * @param {number} targetScore - 目标分数
         */
        function animateScore(targetScore) {
            const scoreElement = document.getElementById('scoreNumber');
            let currentScore = 0;
            const duration = 1500;
            const increment = Math.ceil(targetScore / (duration / 20));
            
            const animation = setInterval(() => {
                currentScore += increment;
                if (currentScore >= targetScore) {
                    currentScore = targetScore;
                    clearInterval(animation);
                }
                scoreElement.textContent = currentScore;
            }, 20);
        }

        /**
         * 绘制柱状图
         * 显示六个维度的得分
         */
        function drawBarChart() {
            const container = document.getElementById('barChart');
            const colors = [
                '#FF6B9D', // 热情度 - 粉色
                '#A855F7', // 理性度 - 紫色
                '#3B82F6', // 情绪度 - 蓝色
                '#F59E0B', // 占有欲 - 橙色
                '#10B981', // 独立性 - 绿色
                '#EF4444'  // 信任度 - 红色
            ];
            
            const labels = ['热情度', '理性度', '情绪度', '占有欲', '独立性', '信任度'];
            const values = [
                Math.min(100, Math.round((dimensions.passion / 50) * 100)),
                Math.min(100, Math.round((dimensions.rationality / 50) * 100)),
                Math.min(100, Math.round((dimensions.emotional / 60) * 100)),
                Math.min(100, Math.round((dimensions.possessiveness / 50) * 100)),
                Math.min(100, Math.round((dimensions.independence / 40) * 100)),
                Math.min(100, Math.round((dimensions.trust / 40) * 100))
            ];
            
            container.innerHTML = '';
            
            labels.forEach((label, index) => {
                const barItem = document.createElement('div');
                barItem.className = 'bar-item';
                barItem.innerHTML = `
                    <div class="bar-label">${label}</div>
                    <div class="bar-track">
                        <div class="bar-fill" style="width: 0%; background: ${colors[index]}"></div>
                    </div>
                    <div class="bar-value">${values[index]}%</div>
                `;
                container.appendChild(barItem);
            });
            
            // 延迟执行动画
            setTimeout(() => {
                const fills = container.querySelectorAll('.bar-fill');
                fills.forEach((fill, index) => {
                    fill.style.width = values[index] + '%';
                });
            }, 300);
        }

        /**
         * 分享结果
         * 复制结果文本到剪贴板
         */
        function shareResult() {
            const results = calculateResults();
            const shareText = `我在【恋爱体质测试】中得了${results.score}分！\n\n我的恋爱人格类型是：${results.personality.type}\n\n快来看看你的恋爱体质是什么吧！💕`;
            
            if (navigator.clipboard) {
                navigator.clipboard.writeText(shareText).then(() => {
                    showToast('✅ 结果已复制，快去分享给朋友吧！');
                }).catch(() => {
                    showToast('❌ 复制失败，请手动分享');
                });
            } else {
                // 降级处理
                const textarea = document.createElement('textarea');
                textarea.value = shareText;
                document.body.appendChild(textarea);
                textarea.select();
                document.execCommand('copy');
                document.body.removeChild(textarea);
                showToast('✅ 结果已复制，快去分享给朋友吧！');
            }
        }

        /**
         * 重新测试
         * 重置所有数据，返回首页
         */
        function retakeTest() {
            // 重置变量
            currentQuestion = 0;
            totalScore = 0;
            answers = [];
            dimensions = {
                passion: 0,
                rationality: 0,
                emotional: 0,
                possessiveness: 0,
                independence: 0,
                trust: 0
            };
            
            // 重置UI
            document.getElementById('questionCard').style.display = 'block';
            document.querySelector('.progress-container').style.display = 'block';
            document.getElementById('scoreNumber').textContent = '0';
            
            // 切换到首页
            switchPage('resultPage', 'homePage');
        }

        /**
         * 显示Toast提示
         * @param {string} message - 提示消息
         */
        function showToast(message) {
            const toast = document.getElementById('toast');
            toast.textContent = message;
            toast.classList.add('show');
            
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }
    </script>
</body>
</html>
