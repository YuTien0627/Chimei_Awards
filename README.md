<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>奇美醫院 2020-2024 院外競賽得獎紀錄 (探索版)</title>
    <!-- 更新 Plotly.js 的 CDN 連結至最新穩定版本，以解決過時警告 -->
    <script src="https://cdn.plot.ly/plotly-2.32.0.min.js"></script>
    <!-- Font Awesome 6.x CDN for icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.2/css/all.min.css" xintegrity="sha512-SnH5WK+bZxgPHs44uWIX+LLJAJ9/2PkPKZ5QiAj6Ta86w+fsb2TkcmfRyVX3pBnMFcV7oQPJkl9QevSCWr3W6A==" crossorigin="anonymous" referrerpolicy="no-referrer" />
    <style>
        body {
            font-family: 'Segoe UI', 'Microsoft JhengHei', 'Helvetica Neue', sans-serif;
            background-color: #f4f7f6;
            color: #333;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 1200px;
            margin: auto;
        }
        header {
            text-align: center;
            border-bottom: 2px solid #005a9c;
            padding-bottom: 10px;
            margin-bottom: 20px;
        }
        h1, h2, h3 { color: #005a9c; }
        .tab-nav {
            display: flex;
            flex-wrap: wrap;
            border-bottom: 2px solid #ccc;
            margin-bottom: 20px;
        }
        .tab-link {
            padding: 10px 20px;
            cursor: pointer;
            border: none;
            background-color: transparent;
            font-size: 1.1em;
            margin-bottom: -2px;
            border-bottom: 3px solid transparent;
            transition: all 0.3s ease;
            display: flex; /* Enable flexbox for icon alignment */
            align-items: center; /* Vertically align icon and text */
            gap: 8px; /* Space between icon and text */
        }
        .tab-link:hover {
            background-color: #e0eaf4;
        }
        .tab-link.active {
            border-bottom-color: #005a9c;
            font-weight: bold;
            color: #005a9c;
        }
        .tab-content { display: none; animation: fadeIn 0.5s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        
        /* 修正圖表佈局的容器 */
        .charts-grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(450px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        .charts-grid-container .full-width {
            grid-column: 1 / -1; /* 讓此元素橫跨所有欄位 */
        }

        .chart-container {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            min-height: 400px; /* 確保圖表有足夠空間 */
            display: flex; /* 讓內容居中 */
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }
        .metrics {
            display: flex;
            justify-content: space-around;
            text-align: center;
            margin-bottom: 30px;
            gap: 20px;
        }
        .metric-card {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            flex-grow: 1;
            display: flex; /* Enable flexbox for icon alignment */
            align-items: center; /* Vertically align icon and text */
            justify-content: center;
            flex-direction: column;
        }
        .metric-card h3 { margin: 0 0 10px 0; font-size: 1em; }
        .metric-card .value { font-size: 2.5em; font-weight: bold; color: #005a9c; }
        .metric-card i {
            font-size: 2em;
            margin-bottom: 10px;
            color: #007acc;
        }

        /* Accordion for yearly tabs */
        .accordion details {
            background: #fff;
            border-radius: 8px;
            margin-bottom: 10px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            transition: all 0.3s ease;
        }
        .accordion details:hover {
            box-shadow: 0 4px 8px rgba(0,0,0,0.15);
        }
        .accordion summary {
            font-weight: bold;
            font-size: 1.2em;
            padding: 15px;
            cursor: pointer;
            list-style: none; /* 移除預設標記 */
            position: relative;
            outline: none; /* 移除點擊時的藍色邊框 */
            display: flex; /* Enable flexbox for icon alignment */
            align-items: center; /* Vertically align icon and text */
            gap: 10px; /* Space between icon and text */
        }
        .accordion summary i {
            color: #005a9c;
            font-size: 1.2em;
        }
        .accordion summary::after { /* 自訂標記 */
            content: '+';
            position: absolute;
            right: 20px;
            font-size: 1.5em;
            color: #007acc;
            transition: transform 0.3s ease;
        }
        .accordion details[open] summary::after { 
            content: '−'; 
            transform: rotate(180deg);
        }
        .award-list {
            padding: 0 15px 15px 40px;
            border-top: 1px solid #eee;
        }
        .award-item {
            border-bottom: 1px solid #f0f0f0;
            padding: 10px 0;
            display: flex;
            align-items: flex-start; /* Align icon and text at the top */
            gap: 8px; /* Space between icon and text */
        }
        .award-item i {
            color: #d9534f;
            font-size: 1em;
            margin-top: 3px; /* Adjust vertical alignment for icon */
        }
        .award-item:last-child { border-bottom: none; }
        .award-item .team { font-weight: bold; color: #005a9c; }
        .award-item .award { color: #d9534f; margin-left: 10px; font-weight: bold; }
        .award-item .project { font-size: 0.9em; color: #555; margin-top: 5px; line-height: 1.5; }
        /* Search Tab */
        #search-container {
            position: relative;
        }
        #search-container input {
            width: 100%;
            padding: 12px 12px 12px 40px; /* Add left padding for icon */
            font-size: 1.2em;
            margin-bottom: 20px;
            box-sizing: border-box;
            border: 2px solid #ccc;
            border-radius: 8px;
            transition: border-color 0.3s ease, box-shadow 0.3s ease;
        }
        #search-container input:focus {
            border-color: #007acc;
            box-shadow: 0 0 0 3px rgba(0, 122, 204, 0.2);
            outline: none;
        }
        #search-container i.fa-search {
            position: absolute;
            left: 15px;
            top: 15px;
            color: #888;
            font-size: 1em;
        }
        #search-results .team-result-group { 
            margin-bottom: 25px; 
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        #search-results .team-result-group h3 {
             border-bottom: 2px solid #007acc;
             padding-bottom: 5px;
             margin-top: 0;
        }
        #overall-data-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.9em;
        }
        #overall-data-table th, #overall-data-table td {
            padding: 10px;
            border: 1px solid #eee;
            text-align: left;
            vertical-align: top;
        }
        #overall-data-table th {
            background-color: #e0eaf4;
            color: #005a9c;
            font-weight: bold;
        }
        #overall-data-table tbody tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        #overall-data-table tbody tr:hover {
            background-color: #eaf6ff;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>奇美醫院 2020–2024 院外競賽得獎紀錄</h1>
        </header>

        <div class="tab-nav">
            <button class="tab-link active" onclick="openTab(event, 'overall')"><i class="fas fa-globe"></i> 總覽</button>
            <button class="tab-link" onclick="openTab(event, '2024')"><i class="fas fa-calendar-alt"></i> 2024年</button>
            <button class="tab-link" onclick="openTab(event, '2023')"><i class="fas fa-calendar-alt"></i> 2023年</button>
            <button class="tab-link" onclick="openTab(event, '2022')"><i class="fas fa-calendar-alt"></i> 2022年</button>
            <button class="tab-link" onclick="openTab(event, '2021')"><i class="fas fa-calendar-alt"></i> 2021年</button>
            <button class="tab-link" onclick="openTab(event, '2020')"><i class="fas fa-calendar-alt"></i> 2020年</button>
            <button class="tab-link" onclick="openTab(event, 'search')"><i class="fas fa-search"></i> 團隊搜尋</button>
        </div>

        <div id="overall" class="tab-content" style="display: block;"></div>
        <div id="2024" class="tab-content"></div>
        <div id="2023" class="tab-content"></div>
        <div id="2022" class="tab-content"></div>
        <div id="2021" class="tab-content"></div>
        <div id="2020" class="tab-content"></div>
        <div id="search" class="tab-content"></div>
    </div>

    <script>
        // 獎項資料 - 已根據圖片和之前檔案片段重新整理並使用完整競賽名稱
        const awardData = [
            // 2020年
            { year: 2020, team: "藥帶圈（藥劑部、資訊室、全人醫療科、整合醫療中心、醫療事務室）", competition: "醫策會-國家醫療品質獎(NHQA) - 主題類", organizer: "醫策會", award: "主題改善菁英組-銀獎、創意獎", project: "透過連續性藥物整合照護減少住院病人的用藥疏失" },
            { year: 2020, team: "藥帶圈（藥劑部、資訊室、全人醫療科、整合醫療中心、醫療事務室）", competition: "中衛發展中心-台灣持續改善競賽(TCIA)", organizer: "中衛發展中心", award: "團結組-銅塔3星獎", project: "透過連續性藥物整合照護減少住院病人的用藥疏失" },
            { year: 2020, team: "藥帶圈（藥劑部、資訊室、全人醫療科、整合醫療中心、醫療事務室）", competition: "臺灣醫療品質協會-品質改善成果發表競賽", organizer: "臺灣醫療品質協會", award: "初階組-金品獎", project: "透過連續性藥物整合照護減少住院病人的用藥疏失" },
            { year: 2020, team: "強心圈（心臟血管內科、全人醫療科、復健部、藥劑部、營養科、護理部3CI）", competition: "醫策會-國家醫療品質獎(NHQA) - 主題類", organizer: "醫策會", award: "主題改善組-銀獎", project: "提升嚴重心臟衰竭病人的生活品質" },
            { year: 2020, team: "CEOs二圈（加護醫學部、護理部6BI、復健部、呼吸治療科、感染管制中心、社會服務部、營養科、藥劑部、心臟血管內科、整形外科、品質管理中心、資訊室）", competition: "醫策會-國家醫療品質獎(NHQA) - 主題類", organizer: "醫策會", award: "主題改善組-銅獎、創意獎", project: "提升內科加護病房病人失禁性皮膚炎之照護品質" },
            { year: 2020, team: "肝癌照護團隊（胃腸肝膽科、影像醫學部、癌症中心）", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "標章認證", project: "全方位多專科肝癌診療" },
            { year: 2020, team: "防疫指揮中心醫療執行組、品質管理中心", competition: "臺灣醫療品質協會-品質改善成果發表競賽", organizer: "臺灣醫療品質協會", award: "防疫專題個人獎", project: "洗手消毒，衛生抗疫" },
            { year: 2020, team: "防疫指揮中心醫療執行組、品質管理中心", competition: "臺灣醫療品質協會-品質改善成果發表競賽", organizer: "臺灣醫療品質協會", award: "防疫專題個人獎", project: "醫病溝通，團結抗疫－防疫溝通 CICARE，關心事當回電" },

            // 2021年
            { year: 2021, team: "救生圈（加護醫學部、護理部6BI、復健部、呼吸治療科、感染管制中心、社會服務部、營養科、藥劑部、心臟血管內科、整形外科、品質管理中心、資訊室）", competition: "醫策會-國家醫療品質獎(NHQA) - 主題類", organizer: "醫策會", award: "主題改善菁英組-銅獎、創意獎", project: "運用流程改造開創加護病房之醫療價值" },
            { year: 2021, team: "救生圈（加護醫學部、護理部6BI、復健部、呼吸治療科、感染管制中心、社會服務部、營養科、藥劑部、心臟血管內科、整形外科、品質管理中心、資訊室）", competition: "中衛發展中心-台灣持續改善競賽(TCIA)", organizer: "中衛發展中心", award: "金塔三星獎", project: "運用流程改造開創加護病房之醫療價值" },
            { year: 2021, team: "藥帶圈（藥劑部、資訊室、全人醫療科、醫療事務室）", competition: "醫策會-國家醫療品質獎(NHQA) - 主題類", organizer: "醫策會", award: "主題改善組-銅獎", project: "透過連續性藥物整合照護減少常規手術病人抗血栓藥物的用藥疏失" },
            { year: 2021, team: "藥帶圈（藥劑部、資訊室、全人醫療科、醫療事務室）", competition: "中衛發展中心-台灣持續改善競賽(TCIA)", organizer: "中衛發展中心", award: "銀塔三星獎", project: "透過連續性藥物整合照護減少常規手術病人抗血栓藥物的用藥疏失" },
            { year: 2021, team: "急品圈安老組", competition: "臺灣醫療品質協會-品質改善成果發表競賽", organizer: "臺灣醫療品質協會", award: "金品獎、創新獎", project: "提高急診高齡病人譫妄症之診斷率及預後" },
            { year: 2021, team: "強心圈（心臟內科、全人醫療科、復健部、藥劑部、營養科、護理部3CI）", competition: "台灣醫務管理學會-台灣健康照護品質管理競賽", organizer: "台灣醫務管理學會", award: "銅獎", project: "整合跨領域醫療資源改善心臟衰竭個案照護品質" },
            { year: 2021, team: "急診醫學部", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "標章認證", project: "以電腦輔助之高齡急診病人藥物整合，從急診、住院到居家醫療的全程照護" },
            { year: 2021, team: "實證醫學類 文獻查證臨床組", competition: "醫策會-國家醫療品質獎(NHQA) - 實證醫學類", organizer: "醫策會", award: "潛力獎", project: "推動實證醫學歷程" },
            { year: 2021, team: "擬真情境類 急重症照護組", competition: "醫策會-國家醫療品質獎(NHQA) - 擬真情境類", organizer: "醫策會", award: "銅獎", project: "擬真教學推動歷程" },

            // 2022年
            { year: 2022, team: "強心圈（心臟內科、全人醫療科、復健部、藥劑部、營養科、護理部3CI）", competition: "醫策會-國家醫療品質獎(NHQA) - 主題類", organizer: "醫策會", award: "銅獎", project: "運用精準醫療提升COVID-19疫情下心臟衰竭照護成效" },
            { year: 2022, team: "CEOs圈（加護醫學部、護理部6BI、復健部、呼吸治療科、感染管制中心、社會服務部、營養科、藥劑部、心臟血管內科、整形外科、品質管理中心、資訊室）", competition: "醫策會-國家醫療品質獎(NHQA) - 主題類", organizer: "醫策會", award: "銀獎", project: "提升內科加護病房緩和照護品質" },
            { year: 2022, team: "好孕圈（婦產部、護理部、營養科、社會服務部、資訊室）", competition: "臺灣醫療品質協會-品質改善成果發表競賽", organizer: "臺灣醫療品質協會", award: "銀品獎", project: "縮短初產婦初次產前衛教平均時間" },
            { year: 2022, team: "救生圈（加護醫學部、護理部6BI、復健部、呼吸治療科、感染管制中心、社會服務部、營養科、藥劑部、心臟血管內科、整形外科、品質管理中心、資訊室）", competition: "台灣醫務管理學會-台灣健康照護品質管理競賽", organizer: "台灣醫務管理學會", award: "金獎", project: "運用流程改造開創加護病房之醫療價值" },
            { year: 2022, team: "麻醉部", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "標章認證", project: "醉關懷的是您：以病人為導向的麻醉照護品質提升" },
            { year: 2022, team: "急診醫學部（急診室、整合醫療中心、精神醫學部）", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "醫療院所類 醫院特色醫療組 國家品質標章認證", project: "電腦輔助進行高齡急診病人譫妄症篩檢與治療" },
            { year: 2022, team: "急診醫學部（AI中心、資訊室、急診室）", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "醫療院所類 醫院智慧醫療組 國家品質標章認證", project: "跨院區即時AIoT肺炎病情預測系統" },
            { year: 2022, team: "電子發票即時雲團隊（總務室、會計室、資訊室、資材室、藥劑部、視聽中心）", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "醫療院所類 醫院醫務管理組 國家品質標章認證", project: "數位財務與會計-建置電子發票即時雲" },

            // 2023年
            { year: 2023, team: "救生圈（加護醫學部、復健部、呼吸治療科、護理部、社會服務部、營養科、耳鼻喉科部）", competition: "醫策會-國家醫療品質獎(NHQA) - 主題類", organizer: "醫策會", award: "銀獎、創意獎", project: "提升急性呼吸衰竭病人拔管後吞嚥功能暨預防吸入性肺炎發生" },
            { year: 2023, team: "急診醫學部、高齡急診科、護理部(急診室)、社會服務部、整合醫療中心", competition: "醫策會-國家醫療品質獎(NHQA) - 主題類", organizer: "醫策會", award: "銅獎", project: "提升高齡急診病人譫妄症診斷率及預後" },
            { year: 2023, team: "ICG圈（外科部、護理部等）", competition: "臺灣醫療品質協會-品質改善成果發表競賽", organizer: "臺灣醫療品質協會", award: "銅品獎", project: "降低某外科病房給藥異常事件發生率" },
            { year: 2023, team: "強心圈（心臟內科、全人醫療科、復健部、藥劑部、營養科、護理部3CI）", competition: "台灣醫務管理學會-台灣健康照護品質管理競賽", organizer: "台灣醫務管理學會", award: "佳作", project: "運用精準醫療提升COVID-19疫情下心臟衰竭照護成效" },
            { year: 2023, team: "護理部4A加護病房", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "護理特色專科組 國家品質標章認證 銅獎", project: "warm up～〝暖心護兒〞優質重症早產兒體溫照護" },
            { year: 2023, team: "放射腫瘤部", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "標章認證", project: "毫米之間求完美：奇美超弧刀精準腦部放射手術治療" },
            { year: 2023, team: "移植醫學科、器捐團隊、3D列印團隊", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "公益服務類 國家品質標章認證", project: "展現生命之愛- 3D器官撫慰悲傷的心靈" },
            { year: 2023, team: "急診醫學部", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "標章認證 (續審)", project: "以電腦輔助進行高齡急診病人譫妄症篩檢與治療" },

            // 2024年 (根據圖片和之前資料重新整理)
            { year: 2024, team: "強心圈（心臟血管內科、心臟血管外科、全人醫療科、復健部、藥劑部、營養科、內科部、護理部(3CI)、加護醫學部）", competition: "醫策會-國家醫療品質獎(NHQA) - 主題類", organizer: "醫策會", award: "主題改善菁英組-銅獎、創意獎", project: "提升心臟衰竭末期的醫療照護品質" },
            { year: 2024, team: "急品圈安老組（急診醫學部、綜合醫療中心、護理部(急診室、9A病房)、復健醫學部）", competition: "醫策會-國家醫療品質獎(NHQA) - 主題類", organizer: "醫策會", award: "主題改善菁英組-佳作", project: "提升急診高齡病人出院準備服務成效" },
            { year: 2024, team: "急品圈安老組（急診醫學部、綜合醫療中心、護理部(急診室、9A病房)、復健醫學部）", competition: "中衛發展中心-台灣持續改善競賽(TCIA)", organizer: "中衛發展中心", award: "團結組-金塔3星獎", project: "提升急診高齡病人出院準備服務成效" },
            { year: 2024, team: "急品圈安老組（急診醫學部、綜合醫療中心、護理部(急診室、9A病房)、復健醫學部）", competition: "臺灣醫療品質協會-品質改善成果發表競賽", organizer: "臺灣醫療品質協會", award: "初階組-優良海報獎", project: "提升急診高齡病人出院準備服務成效" },
            { year: 2024, team: "救腦圈（腦中風中心、復健部(6A)、神經外科、神經內科、胸腔內科、護理部、神經部）", competition: "中衛發展中心-台灣持續改善競賽(TCIA)", organizer: "中衛發展中心", award: "團結組-銀塔3星獎", project: "提升腦中風中心病人的全方位復歸效率" },
            { year: 2024, team: "救腦圈（腦中風中心、復健部(6A)、神經外科、神經內科、胸腔內科、護理部、神經部）", competition: "臺灣醫療品質協會-品質改善成果發表競賽", organizer: "臺灣醫療品質協會", award: "初階組-銅品獎", project: "提升腦中風中心病人的全方位復歸效率" },
            { year: 2024, team: "綠巨人圈（護理部(手術室)、外科部(一般及消化外科)、開刀房）", competition: "醫策會-國家醫療品質獎(NHQA) - 主題類", organizer: "醫策會", award: "主題改善組-銅獎、人因特別獎", project: "降低手術病人術中壓力性損傷發生率" },
            { year: 2024, team: "綠巨人圈（護理部(手術室)、外科部(一般及消化外科)、開刀房）", competition: "臺灣醫療品質協會-品質改善成果發表競賽", organizer: "臺灣醫療品質協會", award: "初階組-優良獎", project: "降低手術病人術中壓力性損傷發生率" },
            { year: 2024, team: "醫e圈（藥劑部（門診）、加護醫學部（神經科））", competition: "臺灣醫療品質協會-品質改善成果發表競賽", organizer: "臺灣醫療品質協會", award: "初階組-優良獎", project: "提升加護病房住院病人藥品辨識率" },
            { year: 2024, team: "足穩圈（護理部(9A病房)、老年醫學科、復健部、藥劑部）", competition: "臺灣醫療品質協會-品質改善成果發表競賽", organizer: "臺灣醫療品質協會", award: "初階組-銀品獎", project: "提升綜合病房高齡跌倒預防成效" },
            { year: 2024, team: "是8Life圈（護理部(8A病房)、自殺防治中心、精神醫學部、營養科）", competition: "臺灣醫療品質協會-品質改善成果發表競賽", organizer: "臺灣醫療品質協會", award: "初階組-優良品獎", project: "降低大腸癌病人化療期間2星期腹瀉發生率" },
            // 以下是之前數據中包含的SNQ和醫務管理學會獎項，圖片中沒有，但應保留
            { year: 2024, team: "放射腫瘤部", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "標章認證", project: "護心、細心、放心：奇美精準呼吸調控乳癌放射線治療" },
            { year: 2024, team: "ICG圈（外科部、兒科部等）", competition: "台灣醫務管理學會-台灣健康照護品質管理競賽", organizer: "台灣醫務管理學會", award: "佳作、最佳創新主題獎", project: "降低某外科病房給藥異常事件發生率" },
            { year: 2024, team: "大腸直腸癌團隊", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "醫療院所類 醫院特色醫療組 國家品質標章認證", project: "以病人為中心，奇美大腸直腸癌全方面照護" },
            { year: 2024, team: "急診醫學部", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "醫療院所類 醫院特色醫療組 國家品質標章認證", project: "以跨領域團隊合作進行急診出院病人之居家醫療轉介" },
            { year: 2024, team: "復健部", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "醫療院所類 醫院醫事服務組 國家品質標章認證", project: "安心出院、放心回家--以家庭為中心的跨院區居家復健服務" },
            { year: 2024, team: "癌症中心", competition: "生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)", organizer: "生策中心", award: "醫療院所類 醫院醫事服務組 國家品質標章認證", project: "給你安心與安全-全方位癌症化療照護" },
        ];

        // 根據競賽名稱判斷類別，由於 awardData.competition 已是完整名稱，直接返回即可
        function getCategory(competition) {
            return competition;
        }

        // 頁面載入完成後執行初始化
        document.addEventListener('DOMContentLoaded', function() {
            renderOverallDashboard(); // 渲染總覽頁籤
            // 渲染各年份頁籤
            ['2024', '2023', '2022', '2021', '2020'].forEach(year => renderYearlyDashboard(year));
            renderSearchTab(); // 渲染團隊搜尋頁籤
        });

        // 開啟指定頁籤
        function openTab(evt, tabName) {
            let i, tabcontent, tablinks;
            tabcontent = document.getElementsByClassName("tab-content");
            for (i = 0; i < tabcontent.length; i++) {
                tabcontent[i].style.display = "none";
            }
            tablinks = document.getElementsByClassName("tab-link");
            for (i = 0; i < tablinks.length; i++) {
                tablinks[i].className = tablinks[i].className.replace(" active", "");
            }
            document.getElementById(tabName).style.display = "block";
            evt.currentTarget.className += " active";
        }

        // 渲染總覽頁籤的儀表板
        function renderOverallDashboard() {
            const container = document.getElementById('overall');
            const data = awardData;

            // 總覽頁籤的 HTML 結構，包含三個圖表容器和一個資料表格容器
            container.innerHTML = `
                <div class="charts-grid-container">
                    <div class="chart-container" id="chart_overall_by_year"></div>
                    <div class="chart-container" id="chart_overall_by_category"></div>
                    <div class="chart-container full-width" id="chart_overall_top_teams"></div>
                </div>
                <h2 style="margin-top: 30px;">完整得獎紀錄</h2>
                <div style="max-height: 500px; overflow-y: auto; background-color: #fff; padding: 15px; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1);">
                    <table id="overall-data-table">
                        <thead>
                            <tr>
                                <th>年份</th>
                                <th>團隊/科部</th>
                                <th>競賽名稱</th>
                                <th>獎項</th>
                                <th>參賽主題</th>
                            </tr>
                        </thead>
                        <tbody></tbody>
                    </table>
                </div>
            `;

            // 圖表：歷年獲獎趨勢 (柱狀圖)
            const countByYear = data.reduce((acc, {year}) => { acc[year] = (acc[year] || 0) + 1; return acc; }, {});
            Plotly.newPlot('chart_overall_by_year', [{
                x: Object.keys(countByYear).sort(),
                y: Object.keys(countByYear).sort().map(year => countByYear[year]),
                type: 'bar', marker: {color: '#007acc'}
            }], { title: '<b>歷年獲獎趨勢</b>', margin: {t:40} }, {responsive: true});

            // 圖表：競賽類別總覽 (圓餅圖) - 使用精確的競賽名稱
            const countByCompetition = data.reduce((acc, item) => {
                const competitionName = getCategory(item.competition);
                acc[competitionName] = (acc[competitionName] || 0) + 1;
                return acc;
            }, {});
            Plotly.newPlot('chart_overall_by_category', [{
                labels: Object.keys(countByCompetition),
                values: Object.values(countByCompetition),
                type: 'pie', textinfo: 'label+percent',
                automargin: true // 自動調整邊距以避免標籤重疊
            }], { title: '<b>競賽類別總覽 (五年)</b>', showlegend: true, margin: {t:40} }, {responsive: true});

            // 圖表：五年獲獎團隊Top 10 (水平柱狀圖)
            const teamCounts = data.reduce((acc, item) => {
                acc[item.team] = (acc[item.team] || 0) + 1;
                return acc;
            }, {});
            // 排序並取前10名
            const sortedTeams = Object.entries(teamCounts).sort(([,a], [,b]) => b - a).slice(0, 10);
            const topTeams = sortedTeams.map(([team]) => team).reverse(); // 反轉以便 Plotly 正確顯示由上而下
            const topTeamCounts = sortedTeams.map(([,count]) => count).reverse(); // 反轉以便 Plotly 正確顯示由上而下

            Plotly.newPlot('chart_overall_top_teams', [{
                x: topTeamCounts,
                y: topTeams,
                type: 'bar',
                orientation: 'h', // 水平柱狀圖
                marker: {color: '#d9534f'}
            }], { 
                title: '<b>五年獲獎團隊Top 10</b>', 
                margin: {l:150, t:40, r:20, b:20}, // 調整左邊距以容納長標籤
                yaxis: {automargin: true} // 自動調整Y軸標籤邊距
            }, {responsive: true});

            // 填充完整得獎紀錄資料表
            const tableBody = document.querySelector('#overall-data-table tbody');
            data.forEach(item => {
                const row = tableBody.insertRow();
                row.innerHTML = `
                    <td>${item.year}</td>
                    <td>${item.team}</td>
                    <td>${getCategory(item.competition)}</td>
                    <td>${item.award}</td>
                    <td>${item.project}</td>
                `;
            });
        }

        // 渲染各年份頁籤的儀表板
        function renderYearlyDashboard(year) {
            const container = document.getElementById(year);
            const dataForYear = awardData.filter(item => item.year == year);

            // 如果該年份沒有資料，顯示提示訊息
            if (!dataForYear.length) {
                container.innerHTML = `<p style="text-align:center; padding: 40px; color: #666;">${year}年無相關得獎資料。</p>`;
                return;
            }
            
            // 計算該年份的獨立團隊數量
            const uniqueTeams = new Set(dataForYear.map(item => item.team));
            
            // 根據精確的競賽名稱分組資料
            const groupedData = dataForYear.reduce((acc, item) => {
                const competitionName = getCategory(item.competition);
                if (!acc[competitionName]) acc[competitionName] = [];
                acc[competitionName].push(item);
                return acc;
            }, {});

            let contentHTML = `
                <div class="metrics">
                    <div class="metric-card">
                        <i class="fas fa-trophy"></i>
                        <h3>${year}年 總得獎數</h3>
                        <div class="value">${dataForYear.length}</div>
                    </div>
                    <div class="metric-card">
                        <i class="fas fa-users"></i>
                        <h3>${year}年 參與團隊數</h3>
                        <div class="value">${uniqueTeams.size}</div>
                    </div>
                </div>
                <h2>${year}年 獲獎競賽探索</h2>
                <div class="accordion">
            `;

            // 遍歷分組後的資料，生成摺疊選單
            // 確保類別的順序一致，按照您提供的五個競賽順序，並細分NHQA
            const orderedCompetitions = [
                '醫策會-國家醫療品質獎(NHQA) - 主題類',
                '醫策會-國家醫療品質獎(NHQA) - 系統類',
                '醫策會-國家醫療品質獎(NHQA) - 智慧醫療類',
                '醫策會-國家醫療品質獎(NHQA) - 傑出醫療類',
                '醫策會-國家醫療品質獎(NHQA) - 實證醫學類',
                '醫策會-國家醫療品質獎(NHQA) - 擬真情境類',
                '中衛發展中心-台灣持續改善競賽(TCIA)',
                '臺灣醫療品質協會-品質改善成果發表競賽',
                '台灣醫務管理學會-台灣健康照護品質管理競賽',
                '生策中心-國家品質標章暨國家生技醫療品質獎(SNQ)'
            ];

            orderedCompetitions.forEach(compName => {
                if (groupedData[compName] && groupedData[compName].length > 0) {
                    let iconClass = 'fas fa-award'; // Default icon
                    if (compName.includes('醫策會')) iconClass = 'fas fa-hospital';
                    else if (compName.includes('中衛發展中心')) iconClass = 'fas fa-cogs';
                    else if (compName.includes('臺灣醫療品質協會')) iconClass = 'fas fa-ribbon';
                    else if (compName.includes('台灣醫務管理學會')) iconClass = 'fas fa-chart-line';
                    else if (compName.includes('生策中心')) iconClass = 'fas fa-certificate';

                    contentHTML += `<details><summary><i class="${iconClass}"></i><h3>${compName} (${groupedData[compName].length}項)</h3></summary><div class="award-list">`;
                    // 按照團隊名稱排序獎項
                    groupedData[compName].sort((a, b) => a.team.localeCompare(b.team, 'zh-TW'));
                    groupedData[compName].forEach(item => {
                        contentHTML += `
                            <div class="award-item">
                                <i class="fas fa-medal"></i>
                                <span class="team">${item.team}</span>
                                <span class="award">【${item.award}】</span>
                                <div class="project">${item.project}</div>
                            </div>
                        `;
                    });
                    contentHTML += `</div></details>`;
                }
            });
            
            contentHTML += `</div>`;
            container.innerHTML = contentHTML;
        }

        // 渲染團隊搜尋頁籤
        function renderSearchTab() {
            const container = document.getElementById('search');
            container.innerHTML = `
                <div id="search-container">
                    <i class="fas fa-search"></i>
                    <input type="text" id="team-search-input" placeholder="請輸入單位或團隊名稱關鍵字，例如「強心圈」或「急診」...">
                </div>
                <div id="search-results">
                    <p style="text-align:center; padding: 20px; color: #666;">請在上方輸入框進行搜尋。</p>
                </div>
            `;

            const searchInput = document.getElementById('team-search-input');
            const resultsContainer = document.getElementById('search-results');

            // 監聽搜尋框的輸入事件
            searchInput.addEventListener('input', function() {
                const query = this.value.trim().toLowerCase();
                // 如果搜尋關鍵字少於1個字，顯示提示訊息
                if (query.length < 1) {
                    resultsContainer.innerHTML = '<p style="text-align:center; padding: 20px; color: #666;">請在上方輸入框進行搜尋。</p>';
                    return;
                }

                // 過濾資料，找出團隊名稱包含關鍵字的項目
                const filteredData = awardData.filter(item => item.team.toLowerCase().includes(query));
                
                // 如果沒有找到符合條件的資料，顯示提示訊息
                if (filteredData.length === 0) {
                    resultsContainer.innerHTML = '<p style="text-align:center; padding: 20px; color: #666;">找不到符合條件的團隊或單位。</p>';
                    return;
                }

                // 先按團隊分組，再按年份分組
                const groupedByTeam = filteredData.reduce((acc, item) => {
                    if (!acc[item.team]) acc[item.team] = {};
                    if (!acc[item.team][item.year]) acc[item.team][item.year] = [];
                    acc[item.team][item.year].push(item);
                    return acc;
                }, {});

                let resultsHTML = '';
                // 遍歷每個團隊的搜尋結果
                for (const team in groupedByTeam) {
                    resultsHTML += `<div class="team-result-group"><h3>${team}</h3><div class="accordion">`;
                    // 獲取並降序排序該團隊有獲獎的年份
                    const years = Object.keys(groupedByTeam[team]).sort((a,b) => b-a); 
                    
                    // 遍歷每個年份，生成摺疊選單
                    years.forEach(year => {
                         resultsHTML += `<details><summary><h4>${year}年 (${groupedByTeam[team][year].length}項)</h4></summary><div class="award-list">`;
                         // 遍歷該年份下的所有獎項
                         groupedByTeam[team][year].forEach(award => {
                             // 在搜尋結果中顯示精確的競賽名稱
                             resultsHTML += `
                                <div class="award-item">
                                    <i class="fas fa-medal"></i>
                                    <span class="team">${getCategory(award.competition)}</span>
                                    <span class="award">【${award.award}】</span>
                                    <div class="project">${award.project}</div>
                                </div>
                             `;
                         });
                         resultsHTML += `</div></details>`;
                    });
                    resultsHTML += `</div></div>`;
                }
                resultsContainer.innerHTML = resultsHTML;
            });
        }
    </script>
</body>
</html>
