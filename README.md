<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>卜卦系統</title>
    <style>
        body {
            font-family: 'Microsoft JhengHei', Arial, sans-serif;
            line-height: 1.6;
            color: #333;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        h1, h2 {
            color: #2c3e50;
            text-align: center;
        }
        .instruction, .input-container, #result {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }
        .instruction {
            font-style: italic;
            text-align: center;
            color: #34495e;
        }
        label, input, button {
            display: block;
            width: 100%;
            margin-bottom: 10px;
        }
        input {
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 10px;
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #2980b9;
        }
    </style>
</head>
<body>
    <h1>卜卦系統</h1>
    <div class="instruction">
        <p>請在心中誠心默念你想要卜卦的問題，再開始抽取數字</p>
    </div>
    <div class="input-container">
        <label for="upperNumber">上卦數字 (0-999)：</label>
        <input type="number" id="upperNumber" min="0" max="999" required>
        <label for="lowerNumber">下卦數字 (0-999)：</label>
        <input type="number" id="lowerNumber" min="0" max="999" required>
        <button onclick="castDivination()">卜卦</button>
    </div>
    <div id="result"></div>

    <script>
        const basicHexagrams = ["乾", "兌", "離", "震", "巽", "坎", "艮", "坤"];
        
        const hexagramCombinations = [
            "乾為天", "天澤履", "天火同人", "天雷無妄", "天風姤", "天水訟", "天山遯", "天地否",
            "澤天夬", "兌為澤", "澤火革", "澤雷隨", "澤風大過", "澤水困", "澤山咸", "澤地萃",
            "火天大有", "火澤睽", "離為火", "火雷噬嗑", "火風鼎", "火水未濟", "火山旅", "火地晉",
            "雷天大壯", "雷澤歸妹", "雷火豐", "震為雷", "雷風恆", "雷水解", "雷山小過", "雷地豫",
            "風天小畜", "風澤中孚", "風火家人", "風雷益", "巽為風", "風水渙", "風山漸", "風地觀",
            "水天需", "水澤節", "水火既濟", "水雷屯", "水風井", "坎為水", "水山蹇", "水地比",
            "山天大畜", "山澤損", "山火賁", "山雷頤", "山風蠱", "山水蒙", "艮為山", "山地剝",
            "地天泰", "地澤臨", "地火明夷", "地雷復", "地風升", "地水師", "地山謙", "坤為地"
        ];

        function getHexagram(number) {
            return basicHexagrams[number % 8];
        }

        function castDivination() {
            const upperNumber = parseInt(document.getElementById('upperNumber').value);
            const lowerNumber = parseInt(document.getElementById('lowerNumber').value);

            if (isNaN(upperNumber) || isNaN(lowerNumber) || upperNumber < 0 || upperNumber > 999 || lowerNumber < 0 || lowerNumber > 999) {
                alert("請輸入0到999之間的數字");
                return;
            }

            const upperHexagram = getHexagram(upperNumber);
            const lowerHexagram = getHexagram(lowerNumber);
            const combinationIndex = basicHexagrams.indexOf(upperHexagram) * 8 + basicHexagrams.indexOf(lowerHexagram);
            const combination = hexagramCombinations[combinationIndex];

            const resultDiv = document.getElementById('result');
            resultDiv.innerHTML = `
                <h2>卜卦結果</h2>
                <p><strong>上卦：</strong>${upperHexagram}（數字：${upperNumber}）</p>
                <p><strong>下卦：</strong>${lowerHexagram}（數字：${lowerNumber}）</p>
                <h3>卦象組合</h3>
                <p><strong>${combination}</strong></p>
                <p>這個卦象代表...（這裡可以添加具體的卦象解釋）</p>
            `;
        }
    </script>
</body>
</html>
