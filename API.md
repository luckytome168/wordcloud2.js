<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Word Cloud Example</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        #wordCloud {
            width: 600px;
            height: 400px;
            border: 1px solid #ccc;
        }
    </style>
</head>
<body>
    <div id="wordCloud"></div>
    <script src="https://cdn.jsdelivr.net/npm/d3@6"></script>
    <script src="https://cdn.jsdelivr.net/npm/d3-cloud"></script>
    <script>
        const words = [
            {text: "我們", size: 75},
            {text: "家長", size: 54},
            {text: "市長", size: 17},
            {text: "檢察官", size: 16},
            {text: "媒體", size: 14},
            {text: "調查", size: 10},
            {text: "特別", size: 9},
            {text: "說明", size: 9},
            {text: "孩子", size: 9},
            {text: "問題", size: 7},
            {text: "過程", size: 7},
            {text: "醫院", size: 7},
            {text: "報告", size: 7},
            {text: "專業", size: 6},
            {text: "詢問", size: 6},
            {text: "毛髮", size: 6},
            {text: "期待", size: 6},
            {text: "專案", size: 5},
            {text: "記者會", size: 5},
            {text: "面對面", size: 5}
        ];

        const width = 600;
        const height = 400;

        const layout = d3.layout.cloud()
            .size([width, height])
            .words(words.map(d => Object.assign({}, d)))
            .padding(5)
            .rotate(() => ~~(Math.random() * 2) * 90)
            .font("Impact")
            .fontSize(d => d.size)
            .on("end", draw);

        layout.start();

        function draw(words) {
            d3.select("#wordCloud").append("svg")
                .attr("width", layout.size()[0])
                .attr("height", layout.size()[1])
                .append("g")
                .attr("transform", `translate(${layout.size()[0] / 2},${layout.size()[1] / 2})`)
                .selectAll("text")
                .data(words)
                .enter().append("text")
                .style("font-size", d => d.size + "px")
                .style("font-family", "Impact")
                .style("fill", () => d3.schemeCategory10[Math.floor(Math.random() * 10)])
                .attr("text-anchor", "middle")
                .attr("transform", d => `translate(${[d.x, d.y]})rotate(${d.rotate})`)
                .text(d => d.text);
        }
    </script>
</body>
</html>
