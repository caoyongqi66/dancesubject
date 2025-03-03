<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>民族民间舞蹈教学目标设计</title>
  <!-- 引入Google Fonts（装饰性字体） -->
  <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@700&display=swap" rel="stylesheet">
  <!-- 引入Font Awesome图标库 -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" integrity="sha512-uO3SXz3F+X+EiR+3CEj+ZlPR0e1JvQFnB/7aDNDM+hWRSBs19zC5HkPH76aJfR3z+DZSwIkyZ3Uq4zD4+4eHUg==" crossorigin="anonymous" referrerpolicy="no-referrer" />
  <!-- 更新第三方库CDN链接 -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/docx@7.1.0/build/index.min.js"></script>
  
  <style>
    /* 整体背景及字体 */
    body {
      font-family: "Noto Sans SC", Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: linear-gradient(135deg, #f0f4f8, #d9e2ec);
      color: #333;
    }
    /* APP容器 */
    #app {
      position: relative;
      padding: 20px;
      background: rgba(255,255,255,0.95);
      max-width: 1200px;
      margin: 20px auto;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.2);
      overflow: hidden;
    }
    /* 主题切换按钮 */
    .themeToggle {
      position: absolute;
      top: 10px;
      right: 10px;
      background: transparent;
      border: none;
      font-size: 24px;
      color: #2a5d84;
      cursor: pointer;
      transition: color 0.3s;
      z-index: 1000;
    }
    .themeToggle:hover {
      color: #ff6f61;
    }
    /* 主标题样式：28px，加粗，纯黑 */
    #mainTitle {
      margin: 0;
      padding: 20px;
      font-size: 28px;
      font-weight: bold;
      color: #000;
      text-align: center;
      font-family: 'Cinzel', serif;
      display: none;
    }
    /* 单元选择界面背景 */
    #unitSelection {
      position: relative;
      background: url('https://example.com/dance_background.jpg') no-repeat center center;
      background-size: 110%;
      text-align: center;
      animation: zoomIn 20s infinite alternate;
    }
    #unitSelection::before {
      content: "";
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(255,255,255,0.7);
      z-index: 0;
    }
    #unitSelection > * {
      position: relative;
      z-index: 1;
    }
    /* 领域选择容器 */
    #fieldContainer {
      text-align: center;
    }
    /* 顶栏采用Flex布局 */
    .topBar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      width: 100%;
      padding: 8px 15px;
      box-sizing: border-box;
      background: #f0f8ff;
      border-bottom: 1px solid #ddd;
      border-radius: 4px;
      margin-bottom: 10px;
    }
    /* 按钮样式 */
    .backBtn, .exportBtn {
      background-color: #d1e0e0;
      color: #333;
      border: none;
      cursor: pointer;
      border-radius: 4px;
      padding: 8px 16px;
      transition: background 0.3s, transform 0.2s;
    }
    .backBtn:hover, .exportBtn:hover {
      background-color: #b0c4de;
      transform: scale(1.05);
    }
    /* 居中标题 */
    .centerTitle {
      text-align: center;
      margin: 15px 0;
      color: #2a5d84;
      font-family: 'Cinzel', serif;
    }
    /* 卡片样式 */
    .unitCard, .fieldCard {
      display: inline-block;
      margin: 10px;
      padding: 20px;
      border: 1px solid #ccc;
      cursor: pointer;
      background-color: #fff;
      transition: background 0.3s, transform 0.2s, box-shadow 0.2s;
      border-radius: 8px;
      box-shadow: 0 1px 4px rgba(0,0,0,0.15);
      text-align: center;
    }
    .unitCard:hover, .fieldCard:hover {
      background-color: #e6f2ff;
      transform: scale(1.03);
      box-shadow: 0 2px 6px rgba(0,0,0,0.2);
    }
    /* 领域卡片特殊配色 */
    .fieldCard.cognitive {
      background-color: #FF6F61;
      color: #fff;
      font-weight: bold;
    }
    .fieldCard.emotional {
      background-color: #66CC66;
      color: #fff;
      font-weight: bold;
    }
    .fieldCard.motor {
      background-color: #87CEEB;
      color: #fff;
      font-weight: bold;
    }
    /* 表格容器 */
    .tableContainer {
      width: 100%;
      overflow-x: auto;
      margin-top: 20px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      background: #fff;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 10px;
      text-align: center;
      vertical-align: middle;
      transition: box-shadow 0.3s;
    }
    th:hover, td:hover {
      box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
    }
    thead th, tbody td:first-child {
      font-weight: bold;
    }
    thead th {
      background-color: #f7f7f7;
    }
    select, textarea, input {
      width: 100%;
      box-sizing: border-box;
      padding: 5px;
      border: 1px solid #bbb;
      border-radius: 4px;
      outline: none;
      transition: border-color 0.3s;
    }
    select:focus, textarea:focus, input:focus {
      border-color: #2a5d84;
    }
    th.diagCell {
      position: relative;
      min-width: 80px;
      min-height: 60px;
      background-color: #f7f7f7;
    }
    .diagLine {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
    }
    .diagBottomLeft {
      position: absolute;
      bottom: 4px;
      left: 4px;
      font-size: 12px;
      color: #555;
    }
    .diagTopRight {
      position: absolute;
      top: 4px;
      right: 4px;
      font-size: 12px;
      color: #555;
    }
    /* 汇总块样式 */
    .summaryBlock {
      margin-bottom: 1em;
      line-height: 1.6;
      text-align: left;
      background: #fff;
      padding: 10px 15px;
      border: 1px solid #ddd;
      border-radius: 4px;
      box-shadow: 0 1px 3px rgba(0,0,0,0.1);
    }
    .summaryBlock h3 {
      margin-top: 0;
      color: #2a5d84;
    }
    .summaryBlock ol {
      margin-left: 20px;
    }
    #hiddenParser {
      display: none;
      visibility: hidden;
    }
    /* 页面转场动画 */
    .fade-in {
      animation: fadeIn 0.5s ease-out;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    /* 移动端样式优化 */
    @media screen and (max-width: 600px) {
      #app {
        padding: 10px;
        margin: 10px;
      }
      #mainTitle {
        font-size: 24px;
        padding: 15px;
      }
      .backBtn, .exportBtn {
        padding: 12px 20px;
        font-size: 16px;
      }
      .unitCard, .fieldCard {
        padding: 15px;
        margin: 8px;
        font-size: 16px;
      }
      .topBar {
        padding: 10px 15px;
      }
      th, td {
        padding: 8px;
        font-size: 14px;
      }
    }
    /* 自定义主题（用户可切换） */
    .custom-theme {
      background: linear-gradient(135deg, #d4fc79, #96e6a1);
    }
    .custom-theme .backBtn, 
    .custom-theme .exportBtn {
      background-color: #ffcc00;
      color: #333;
    }
    /* 缩放动画 */
    @keyframes zoomIn {
      from { transform: scale(1); }
      to { transform: scale(1.05); }
    }
  </style>
</head>

<body onload="initPage()">
  <div id="app">
    <!-- 主题切换按钮 -->
    <button class="themeToggle" onclick="toggleTheme()"><i class="fa fa-gear"></i></button>
    <!-- 第一个界面：标题和单元选择 -->
    <h1 id="mainTitle">民族民间舞蹈教学目标设计</h1>
    <div id="unitSelection" style="display: none;">
      <!-- 删除了“请选择您要编辑的单元”的提示 -->
      <div class="unitCard" onclick="selectUnit('民族文化单元')">民族文化单元</div>
      <div class="unitCard" onclick="selectUnit('基础性组合单元')">基础性组合单元</div>
      <div class="unitCard" onclick="selectUnit('风格性组合单元')">风格性组合单元</div>
      <div class="unitCard" onclick="selectUnit('综合表演性组合单元')">综合表演性组合单元</div>
    </div>

    <!-- 第二个界面：选择领域 -->
    <div id="fieldSelection" style="display: none;">
      <div class="topBar">
        <button class="backBtn" onclick="goBackToUnitSelection()">返回</button>
      </div>
      <h2 class="centerTitle">请选择要编辑的领域</h2>
      <div id="fieldContainer"></div>
    </div>

    <!-- 第三个界面：内容编辑 -->
    <div id="contentEditor" style="display: none;">
      <div class="topBar">
        <button class="backBtn" onclick="goBackToFieldSelection()">返回</button>
      </div>
      <h2 class="centerTitle" id="editorTitle"></h2>
      <div class="tableContainer">
        <table id="knowledgeTable">
          <thead id="tableHead"></thead>
          <tbody id="tableBody"></tbody>
        </table>
      </div>
      <button class="exportBtn" onclick="goToSummaryPage()">设计目标的汇总</button>
    </div>

    <!-- 第四个界面：汇总及导出 -->
    <div id="summaryPage" style="display: none;">
      <div class="topBar">
        <div class="exportGroup">
          <select id="exportFormat">
            <option value="pdf">PDF</option>
            <option value="word">Word</option>
          </select>
          <button class="exportBtn" onclick="exportSelected()">导出</button>
        </div>
        <button class="backBtn" onclick="toggleView('contentEditor')">返回</button>
      </div>
      <h2 class="centerTitle">设计目标的汇总</h2>
      <div id="summaryContent"></div>
    </div>

    <!-- 用于后台重建表格进行解析 -->
    <div id="hiddenParser"></div>
  </div>

  <script>
    /* ========== 全局配置 ========== */
    const fieldOptions = {
      "民族文化单元": ["认知领域", "情感领域"],
      "基础性组合单元": ["认知领域", "情感领域", "动作领域"],
      "风格性组合单元": ["认知领域", "情感领域", "动作领域"],
      "综合表演性组合单元": ["认知领域", "情感领域", "动作领域"]
    };

    const specialCases = {
      "风格性组合单元-动作领域": true,
      "综合表演性组合单元-动作领域": true
    };

    let currentUnit = "";
    let currentField = "";

    const tableData = {
      "民族文化单元-认知领域": {
        headers: ["", "记忆", "理解", "应用", "评价", "综合"],
        headerOptions: {
          "记忆": ["识别", "描述", "回忆"],
          "理解": ["转换", "解释", "举例", "推断"],
          "应用": ["运用", "表现", "实施"],
          "评价": ["分析", "比较", "区别", "检查", "评论"],
          "综合": ["重组", "构建", "创新"]
        },
        rows: [
          { name: "陈述性知识", options: ["民族历史", "民族观念", "民族饰物", "民族环境", "民族饮食", "民族风俗", "民族舞蹈"] },
          { name: "程序性知识", options: ["无"] },
          { name: "元认知知识", options: ["组织策略", "学习总结与反思"] }
        ]
      },
      "民族文化单元-情感领域": {
        headers: ["", "接受", "反应", "重视", "整合", "性格化"],
        headerOptions: {
          "接受": ["注意", "关注", "认同", "接纳"],
          "反应": ["遵守（服从）", "讨论（交流）", "执行"],
          "重视": ["区分", "解释", "提出", "分析", "尊重", "调整"],
          "整合": ["计划", "组织", "归纳", "构建"],
          "性格化": ["稳定的态度与行为"]
        },
        rows: [
          { name: "社会性情感", options: ["文化尊重", "文化传承", "民族融合", "课堂规则", "师生礼仪"] },
          { name: "发展性情感", options: ["思考意识", "问题意识"] },
          { name: "美感", options: ["民族地区自然环境美感", "民族社会观念"] }
        ]
      },
      "基础性组合单元-认知领域": {
        headers: ["", "记忆", "理解", "应用", "评价", "综合"],
        headerOptions: {
          "记忆": ["识别", "描述", "回忆"],
          "理解": ["转换", "解释", "举例", "推断"],
          "应用": ["运用", "表现", "实施"],
          "评价": ["分析", "比较", "区别", "检查", "评论"],
          "综合": ["重组", "构建", "创新"]
        },
        rows: [
          { name: "陈述性知识", options: ["舞蹈术语", "舞蹈要素", "舞蹈理论"] },
          { name: "程序性知识", options: ["动作的方位", "动作的发力", "动作的路线"] },
          { name: "元认知知识", options: ["复述策略", "精加工策略", "学习动机", "学习目标", "学习进展", "学习总结与反思"] }
        ]
      },
      "基础性组合单元-动作领域": {
        headers: ["", "知觉", "模仿", "生成", "自动化", "创造"],
        headerOptions: {
          "知觉": ["感知", "选择", "转换"],
          "模仿": ["模仿", "协调"],
          "生成": ["指引", "修正", "练习"],
          "自动化": ["熟练", "固定", "稳定"],
          "创造": ["融合", "编排", "创新"]
        },
        // 修改为5行编辑，行名称为基础性技能1至5
        rows: [
          { name: "基础性技能", options: ["头部与眼部训练", "颈部与肩部训练", "手位与手臂训练", "腿部与脚部训练", "基本体态与动律训练"] },
          { name: "基础性技能", options: ["头部与眼部训练", "颈部与肩部训练", "手位与手臂训练", "腿部与脚部训练", "基本体态与动律训练"] },
          { name: "基础性技能", options: ["头部与眼部训练", "颈部与肩部训练", "手位与手臂训练", "腿部与脚部训练", "基本体态与动律训练"] },
          { name: "基础性技能", options: ["头部与眼部训练", "颈部与肩部训练", "手位与手臂训练", "腿部与脚部训练", "基本体态与动律训练"] },
          { name: "基础性技能", options: ["头部与眼部训练", "颈部与肩部训练", "手位与手臂训练", "腿部与脚部训练", "基本体态与动律训练"] }
        ]
      },
      "基础性组合单元-情感领域": {
        headers: ["", "接受", "反应", "重视", "整合", "性格化"],
        headerOptions: {
          "接受": ["注意", "关注", "认同", "接纳"],
          "反应": ["遵守（服从）", "讨论（交流）", "执行"],
          "重视": ["区分", "解释", "提出", "分析", "尊重", "调整"],
          "整合": ["计划", "组织", "归纳", "构建"],
          "性格化": ["稳定的态度与行为"]
        },
        rows: [
          { name: "社会性情感", options: ["集体主义", "沟通互动", "团结合作", "课堂规则", "师生礼仪"] },
          { name: "发展性情感", options: ["问题意识", "自主学习", "正面情感"] },
          { name: "美感", options: ["民族艺术美感"] }
        ]
      },
      "风格性组合单元-认知领域": {
        headers: ["", "记忆", "理解", "应用", "评价", "综合"],
        headerOptions: {
          "记忆": ["识别", "描述", "回忆"],
          "理解": ["转换", "解释", "举例", "推断"],
          "应用": ["运用", "表现", "实施"],
          "评价": ["分析", "比较", "区别", "检查", "评论"],
          "综合": ["重组", "构建", "创新"]
        },
        rows: [
          { name: "陈述性知识", options: ["舞蹈术语", "舞蹈要素", "舞蹈理论"] },
          { name: "程序性知识", options: ["动作的方位", "动作的发力", "动作的路线", "动作的节奏", "气息对动作表现力", "气息对动作稳定性", "气息对动作力度", "不同的情绪情感"] },
          { name: "元认知知识", options: ["组织策略性", "计划、监控、调节策略", "学习动机", "学习目标", "学习进展", "学习总结与反思"] }
        ]
      },
      "风格性组合单元-情感领域": {
        headers: ["", "接受", "反应", "重视", "整合", "性格化"],
        headerOptions: {
          "接受": ["注意", "关注", "认同", "接纳"],
          "反应": ["遵守（服从）", "讨论（交流）", "执行"],
          "重视": ["区分", "解释", "提出", "分析", "尊重", "调整"],
          "整合": ["计划", "组织", "归纳", "构建"],
          "性格化": ["稳定的态度与行为"]
        },
        rows: [
          { name: "社会性情感", options: ["集体主义", "组织协调", "友好包容", "团队合作", "沟通互动"] },
          { name: "发展性情感", options: ["问题意识", "自主学习意识", "正面情感", "负面情感"] },
          { name: "美感", options: ["民族艺术美感", "民族社会观念美感"] }
        ]
      },
      "风格性组合单元-动作领域": {
        headers: ["", "知觉", "模仿", "生成", "自动化", "创作"],
        headerOptions: {
          "知觉": ["感知", "选择", "转换"],
          "模仿": ["模仿", "协调"],
          "生成": ["指引", "修正", "练习"],
          "自动化": ["熟练", "固定", "稳定"],
          "创作": ["融合", "编排", "创新"]
        },
        rows: [
          { name: "简单组合技能", options: ["课时名称A", "课时名称B"] }
        ]
      },
      "综合表演性组合单元-认知领域": {
        headers: ["", "记忆", "理解", "应用", "评价", "综合"],
        headerOptions: {
          "记忆": ["识别", "描述", "回忆"],
          "理解": ["转换", "解释", "举例", "推断"],
          "应用": ["运用", "表现", "实施"],
          "评价": ["分析", "比较", "区别", "检查", "评论"],
          "综合": ["重组", "构建", "创新"]
        },
        rows: [
          { name: "陈述性知识", options: ["舞蹈术语", "舞蹈要素", "舞蹈理论"] },
          { name: "程序性知识", options: ["气息对动作表现力", "气息对动作稳定性", "气息对动作力度", "不同的情绪情感"] },
          { name: "元认知知识", options: ["认知任务的知识", "学习动机", "学习目标", "学习进展", "学习总结与反思"] }
        ]
      },
      "综合表演性组合单元-情感领域": {
        headers: ["", "接受", "反应", "重视", "整合", "性格化"],
        headerOptions: {
          "接受": ["注意", "关注", "认同", "接纳"],
          "反应": ["遵守（服从）", "讨论（交流）", "执行"],
          "重视": ["区分", "解释", "提出", "分析", "尊重", "调整"],
          "整合": ["计划", "组织", "归纳", "构建"],
          "性格化": ["稳定的态度与行为"]
        },
        rows: [
          { name: "社会性情感", options: ["集体主义", "组织协调", "友好包容", "团队合作", "沟通互动"] },
          { name: "发展性情感", options: ["正面情感", "负面情感"] },
          { name: "美感", options: ["民族艺术美感", "民族社会观念美感"] }
        ]
      },
      "综合表演性组合单元-动作领域": {
        headers: ["", "知觉", "模仿", "生成", "自动化", "创作"],
        headerOptions: {
          "知觉": ["感知", "选择", "转换"],
          "模仿": ["模仿", "协调"],
          "生成": ["指引", "修正", "练习"],
          "自动化": ["熟练", "固定", "稳定"],
          "创作": ["融合", "编排", "创新"]
        },
        rows: [
          { name: "复杂组合技能", options: ["组合课时1", "组合课时2"] }
        ]
      }
    };

    function toggleView(viewId) {
      // 根据当前界面决定是否显示主标题
      if (viewId === "unitSelection") {
        document.getElementById("mainTitle").style.display = "block";
      } else {
        document.getElementById("mainTitle").style.display = "none";
      }
      // 隐藏所有界面
      document.getElementById("unitSelection").style.display = "none";
      document.getElementById("fieldSelection").style.display = "none";
      document.getElementById("contentEditor").style.display = "none";
      document.getElementById("summaryPage").style.display = "none";
      const t = document.getElementById(viewId);
      if (t) {
        t.style.display = "block";
        t.classList.add("fade-in");
        setTimeout(() => t.classList.remove("fade-in"), 500);
      }
    }

    function initPage() {
      document.getElementById("mainTitle").style.display = "block";
      toggleView("unitSelection");
    }

    function selectUnit(unit) {
      currentUnit = unit;
      toggleView("fieldSelection");
      const fc = document.getElementById("fieldContainer");
      fc.innerHTML = "";
      (fieldOptions[unit] || []).forEach(f => {
        const fd = document.createElement("div");
        fd.classList.add("fieldCard");
        fd.textContent = f;
        if(f === "认知领域") {
          fd.classList.add("cognitive");
        } else if(f === "情感领域") {
          fd.classList.add("emotional");
        } else if(f === "动作领域") {
          fd.classList.add("motor");
        }
        fd.onclick = () => selectField(f);
        fc.appendChild(fd);
      });
    }

    function selectField(f) {
      currentField = f;
      document.getElementById("editorTitle").textContent = `${currentUnit} - ${currentField}`;
      toggleView("contentEditor");
      updateTable();
      loadCurrentContent();
    }

    function goBackToUnitSelection() { toggleView("unitSelection"); }
    function goBackToFieldSelection() {
      saveCurrentContent();
      toggleView("fieldSelection");
    }

    function generateOptions(opts) {
      let html = `<option value="" selected>-</option>`;
      opts.forEach(o => {
        html += `<option value="${o}">${o}</option>`;
      });
      return html;
    }

    function updateTable() {
      const key = `${currentUnit}-${currentField}`;
      const data = tableData[key];
      const tableHead = document.getElementById("tableHead");
      const tableBody = document.getElementById("tableBody");

      if (!data) {
        tableHead.innerHTML = "<tr><th>无数据</th></tr>";
        tableBody.innerHTML = "<tr><td>当前单元和领域没有可用内容</td></tr>";
        return;
      }

      if (specialCases[key]) {
        let headRow = `
          <tr>
            <th colspan="2" class="diagCell">
              <svg class="diagLine" viewBox="0 0 100 100" preserveAspectRatio="none">
                <line x1="0" y1="0" x2="100" y2="100" stroke="#666" stroke-width="1"></line>
              </svg>
              <span class="diagBottomLeft"><span class="rowLabel">知识类型</span></span>
              <span class="diagTopRight"><span class="rowLabel">水平层级</span></span>
            </th>
        `;
        for (let i = 1; i < data.headers.length; i++) {
          let colName = data.headers[i];
          let colOpts = data.headerOptions[colName] || [];
          headRow += `<th><span class="rowLabel">${colName}</span><br><select>${generateOptions(colOpts)}</select></th>`;
        }
        headRow += "</tr>";
        tableHead.innerHTML = headRow;

        let skillName = key.includes("风格性") ? "简单组合技能" : "复杂组合技能";
        let rowsHtml = "";
        for (let r = 0; r < 6; r++) {
          let tr = `<tr>
            <td><span class="rowLabel">${skillName}</span></td>
            <td><input type="text" placeholder="具体组合名称"></td>
          `;
          for (let c = 1; c < data.headers.length; c++) {
            tr += `<td><textarea></textarea></td>`;
          }
          tr += "</tr>";
          rowsHtml += tr;
        }
        tableBody.innerHTML = rowsHtml;
      } else {
        let row = `
          <tr>
            <th class="diagCell">
              <svg class="diagLine" viewBox="0 0 100 100" preserveAspectRatio="none">
                <line x1="0" y1="0" x2="100" y2="100" stroke="#666" stroke-width="1"></line>
              </svg>
              <span class="diagBottomLeft"><span class="rowLabel">知识类型</span></span>
              <span class="diagTopRight"><span class="rowLabel">水平层级</span></span>
            </th>
        `;
        for (let i = 1; i < data.headers.length; i++) {
          let colName = data.headers[i];
          let colOpts = data.headerOptions[colName] || [];
          row += `<th><span class="rowLabel">${colName}</span><br><select>${generateOptions(colOpts)}</select></th>`;
        }
        row += "</tr>";
        tableHead.innerHTML = row;

        let bodyHtml = "";
        (data.rows || []).forEach(r => {
          let rowOpts = generateOptions(r.options || []);
          bodyHtml += `
            <tr>
              <td><span class="rowLabel">${r.name}</span><br><select>${rowOpts}</select></td>
              ${"<td><textarea></textarea></td>".repeat(data.headers.length - 1)}
            </tr>
          `;
        });
        tableBody.innerHTML = bodyHtml;
      }
    }

    function saveCurrentContent() {
      const key = `${currentUnit}-${currentField}`;
      const table = document.getElementById("knowledgeTable");
      if (!table) return;
      let dataObj = {};
      let idx = 0;
      table.querySelectorAll("input, textarea, select").forEach(el => {
        dataObj[`field_${idx++}`] = el.value;
      });
      localStorage.setItem(`teachingData_${key}`, JSON.stringify(dataObj));
    }

    function loadCurrentContent() {
      const key = `${currentUnit}-${currentField}`;
      const table = document.getElementById("knowledgeTable");
      if (!table) return;
      let str = localStorage.getItem(`teachingData_${key}`);
      if (!str) return;
      try {
        let dataObj = JSON.parse(str);
        let idx = 0;
        table.querySelectorAll("input, textarea, select").forEach(el => {
          let val = dataObj[`field_${idx++}`];
          if (val !== undefined) {
            if (el.tagName.toLowerCase() === "select") {
              let exist = Array.from(el.options).some(opt => opt.value === val);
              if (!exist) return;
            }
            el.value = val;
          }
        });
      } catch (e) { console.warn("加载本地数据失败:", e); }
    }

    function goToSummaryPage() {
      saveCurrentContent();
      toggleView("summaryPage");
      const summaryDiv = document.getElementById("summaryContent");
      summaryDiv.innerHTML = "";

      let keys = Object.keys(localStorage).filter(k => k.startsWith("teachingData_"));
      if (keys.length === 0) {
        summaryDiv.innerHTML = "<p>尚未填写任何内容。</p>";
        return;
      }

      keys.forEach(storeKey => {
        let name = storeKey.replace("teachingData_", "");
        if (!tableData[name]) return;
        let dataStr = localStorage.getItem(storeKey) || "";
        if (!dataStr) return;

        let parserDiv = document.getElementById("hiddenParser");
        parserDiv.innerHTML = "";
        let tmpTable = document.createElement("table");
        parserDiv.appendChild(tmpTable);

        let thead = document.createElement("thead");
        let tbody = document.createElement("tbody");
        tmpTable.appendChild(thead);
        tmpTable.appendChild(tbody);

        let data = tableData[name];
        if (specialCases[name]) {
          let row = `
            <tr>
              <th colspan="2" class="diagCell">
                <svg class="diagLine" viewBox="0 0 100 100" preserveAspectRatio="none">
                  <line x1="0" y1="0" x2="100" y2="100" stroke="#666" stroke-width="1"></line>
                </svg>
                <span class="diagBottomLeft"><span class="rowLabel">知识类型</span></span>
                <span class="diagTopRight"><span class="rowLabel">水平层级</span></span>
              </th>
          `;
          for (let i = 1; i < data.headers.length; i++) {
            let colName = data.headers[i];
            row += `<th><span class="rowLabel">${colName}</span><br><select>${generateOptions(data.headerOptions[colName] || [])}</select></th>`;
          }
          row += "</tr>";
          thead.innerHTML = row;

          for (let r = 0; r < 6; r++) {
            let tr = document.createElement("tr");
            let td0 = document.createElement("td");
            td0.innerHTML = `<span class="rowLabel">${name.includes("风格性") ? "简单组合技能" : "复杂组合技能"}</span>`;
            tr.appendChild(td0);

            let td1 = document.createElement("td");
            let inp = document.createElement("input");
            inp.type = "text";
            inp.placeholder = "具体组合名称";
            td1.appendChild(inp);
            tr.appendChild(td1);

            for (let c = 1; c < data.headers.length; c++) {
              let td2 = document.createElement("td");
              let ta = document.createElement("textarea");
              td2.appendChild(ta);
              tr.appendChild(td2);
            }
            tbody.appendChild(tr);
          }
        } else {
          let row = `
            <tr>
              <th class="diagCell">
                <svg class="diagLine" viewBox="0 0 100 100" preserveAspectRatio="none">
                  <line x1="0" y1="0" x2="100" y2="100" stroke="#666" stroke-width="1"></line>
                </svg>
                <span class="diagBottomLeft"><span class="rowLabel">知识类型</span></span>
                <span class="diagTopRight"><span class="rowLabel">水平层级</span></span>
              </th>
          `;
          for (let i = 1; i < data.headers.length; i++) {
            let colName = data.headers[i];
            row += `<th><span class="rowLabel">${colName}</span><br><select>${generateOptions(data.headerOptions[colName] || [])}</select></th>`;
          }
          row += "</tr>";
          thead.innerHTML = row;

          (data.rows || []).forEach(r => {
            let tr = document.createElement("tr");
            let td1 = document.createElement("td");
            td1.innerHTML = `<span class="rowLabel">${r.name}</span><br><select>${generateOptions(r.options || [])}</select>`;
            tr.appendChild(td1);

            for (let c = 1; c < data.headers.length; c++) {
              let td2 = document.createElement("td");
              let ta = document.createElement("textarea");
              td2.appendChild(ta);
              tr.appendChild(td2);
            }
            tbody.appendChild(tr);
          });
        }

        let savedObj = JSON.parse(dataStr);
        let idx = 0;
        tmpTable.querySelectorAll("input, textarea, select").forEach(el => {
          let val = savedObj[`field_${idx++}`];
          if (val !== undefined) {
            if (el.tagName.toLowerCase() === "select") {
              let exist = Array.from(el.options).some(opt => opt.value === val);
              if (!exist) return;
            }
            el.value = val;
          }
        });

        let lines = [];
        parseTableData(tmpTable, data.headers.length, name, lines);

        if (lines.length > 0) {
          let block = `<div class="summaryBlock"><h3>【${name}】</h3><ol>`;
          lines.forEach(x => block += `<li>${x}</li>`);
          block += "</ol></div>";
          summaryDiv.innerHTML += block;
        }
      });

      if (!document.getElementById("summaryContent").innerHTML.trim()) {
        document.getElementById("summaryContent").innerHTML = "<p>尚未填写任何内容。</p>";
      }
    }

    function parseTableData(tmpTable, columnsCount, fullKey, linesArr) {
      let thead = tmpTable.querySelector("thead");
      if (!thead) return;
      let headerRow = thead.querySelector("tr");
      if (!headerRow) return;

      let colSelects = [];
      if (specialCases[fullKey]) {
        let allSel = headerRow.querySelectorAll("select");
        colSelects = Array.from(allSel).map(s => s.value || "-");
      } else {
        if (headerRow.cells.length === columnsCount) {
          for (let i = 1; i < columnsCount; i++) {
            let sel = headerRow.cells[i].querySelector("select");
            colSelects.push(sel?.value || "-");
          }
        }
      }

      let tbody = tmpTable.querySelector("tbody");
      let rows = tbody.querySelectorAll("tr");
      rows.forEach((rowObj, rowIdx) => {
        if (!specialCases[fullKey]) {
          let rowVal = getRowVal(rowObj.cells[0]);
          for (let c = 1; c < columnsCount; c++) {
            let colVal = (colSelects[c - 1] || "-").trim();
            let cell = rowObj.cells[c];
            if (!cell) return;
            let ta = cell.querySelector("textarea");
            let textVal = ta ? ta.value.trim() : "";

            if (colVal === "-" && rowVal === "-" && !textVal) continue;
            if (colVal === "-" && !textVal) continue;
            if (rowVal === "-" && !textVal) continue;

            let combined = "";
            if (colVal === "-") combined = rowVal;
            else if (rowVal === "-") combined = colVal;
            else combined = `${colVal} - ${rowVal}`;
            if (textVal) combined += `: ${textVal}`;
            linesArr.push(combined);
          }
        } else {
          let knowledgeCell = rowObj.cells[1];
          let inp = knowledgeCell ? knowledgeCell.querySelector("input") : null;
          let rowVal = inp ? (inp.value.trim() || "-") : "-";
          for (let c = 2; c < columnsCount; c++) {
            let colVal = (colSelects[c - 2] || "-").trim();
            let cell = rowObj.cells[c];
            if (!cell) return;
            let ta = cell.querySelector("textarea");
            let textVal = ta ? ta.value.trim() : "";

            if (colVal === "-" && rowVal === "-" && !textVal) continue;
            if (colVal === "-" && !textVal) continue;
            if (rowVal === "-" && !textVal) continue;

            let combined = "";
            if (colVal === "-") combined = rowVal;
            else if (rowVal === "-") combined = colVal;
            else combined = `${colVal} - ${rowVal}`;
            if (textVal) combined += `: ${textVal}`;
            linesArr.push(combined);
          }
        }
      });
    }

    function getRowVal(td) {
      if (!td) return "-";
      let sel = td.querySelector("select");
      if (sel) return sel.value || "-";
      let txt = td.innerText.trim() || "-";
      return txt;
    }

    async function exportToPDF() {
      try {
        if(document.getElementById("summaryPage").style.display === "none"){
          goToSummaryPage();
        }
        saveCurrentContent();
        const { jsPDF } = window.jspdf;
        const doc = new jsPDF({
          orientation: 'p',
          unit: 'mm',
          format: 'a4'
        });
        const simsunBase64 = "BASE64_SIMSUN";
        if(simsunBase64 === "BASE64_SIMSUN"){
          console.warn("未替换BASE64_SIMSUN，回退使用helvetica字体（中文可能乱码）");
          doc.setFont("helvetica");
        } else {
          doc.addFileToVFS("simsun.ttf", simsunBase64);
          doc.addFont("simsun.ttf", "simsun", "normal");
          doc.setFont("simsun");
        }
        doc.setFontSize(12);
        const text = getSummaryPlainText();
        if (!text.trim()){
          doc.text("没有内容可导出", 20, 20);
        } else {
          const lines = doc.splitTextToSize(text, 180);
          doc.text(20, 20, lines);
        }
        doc.save("教学目标.pdf");
      } catch (e) {
        console.error("PDF导出失败：", e);
        alert("PDF导出失败，请检查控制台日志。");
      }
    }

    async function exportToWord() {
      try {
        saveCurrentContent();
        const { Document, Packer, Paragraph, TextRun } = window.docx;
        const doc = new Document({
          sections: [{
            properties: {},
            children: [
              new Paragraph({
                children: [
                  new TextRun({
                    text: getSummaryPlainText(),
                    font: "SimSun"
                  })
                ]
              })
            ]
          }]
        });
        const blob = await Packer.toBlob(doc);
        const url = URL.createObjectURL(blob);
        const link = document.createElement("a");
        link.href = url;
        link.download = "教学目标.docx";
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
        setTimeout(() => URL.revokeObjectURL(url), 100);
      } catch (e) {
        console.error("Word导出失败:", e);
      }
    }

    function exportSelected() {
      let fmt = document.getElementById("exportFormat").value;
      if (fmt === "pdf") {
        exportToPDF();
      } else {
        exportToWord();
      }
    }

    function getSummaryPlainText() {
      const summaryDiv = document.getElementById("summaryContent");
      if (!summaryDiv) return "";
      return summaryDiv.textContent;
    }

    // 主题切换：切换自定义主题样式
    function toggleTheme() {
      document.getElementById("app").classList.toggle("custom-theme");
    }
  </script>
</body>
</html>
