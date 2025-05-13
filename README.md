# powerPulses11


<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Simple Form</title>
</head>
<body>
    <h2>Enter your name</h2>
    <input type="text" id="nameInput" />
    <button onclick="greet()">Submit</button>
    <p id="output"></p>

    <script>
        function greet() {
            const name = document.getElementById("nameInput").value;
            document.getElementById("output").innerText = "Hello, " + name + "!";
        }
    </script>
</body>
</html>



// test.js
require('chromedriver');

const { Builder, By, until } = require('selenium-webdriver');
const path = require('path');

(async function runTest() {
    let driver = await new Builder().forBrowser('chrome').build();

    try {
        const filePath = `file://${path.resolve(__dirname, 'index.html')}`;
        await driver.get(filePath);

        // Find input, enter name
        const input = await driver.findElement(By.id('nameInput'));
        await input.sendKeys('Alice');

        // Click the button
        const button = await driver.findElement(By.tagName('button'));
        await button.click();

        // Wait for output and assert
        const output = await driver.wait(until.elementLocated(By.id('output')), 5000);
        const text = await output.getText();

        if (text === 'Hello, Alice!') {
            console.log('✅ Test passed!');
        } else {
            console.log('❌ Test failed! Output:', text);
        }
    } finally {
        await driver.quit();
    }
})();
