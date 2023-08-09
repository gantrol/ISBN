<script>
    let inputISBN = "";
    let checkDigit = "";

    function calculateCheckDigit() {
        const cleanISBN = inputISBN.replace(/-/g, "");
        if (cleanISBN.length === 9) {
            // ISBN-10
            const weights = [...Array(9).keys()].map(x => x + 1);
            const remainder = [...cleanISBN].reduce((acc, digit, index) => acc + digit * weights[index], 0) % 11;
            checkDigit = remainder === 10 ? "X" : remainder.toString();
        } else if (cleanISBN.length === 12) {
            // ISBN-13
            const weights = [...Array(12).keys()].map(x => (x % 2 === 0 ? 1 : 3));
            const remainder = [...cleanISBN].reduce((acc, digit, index) => acc + digit * weights[index], 0) % 10;
            checkDigit = (10 - remainder) === 10 ? "0" : (10 - remainder).toString();
        } else {
            checkDigit = "输入的ISBN长度无效";
        }
    }
</script>

<style>
    h1 {
        color: #333;
        text-align: center;
    }
    .container {
        width: 80%;
        margin: 0 auto;
        padding: 20px;
        border: 1px solid #ccc;
        border-radius: 10px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    label,
    input,
    button,
    p {
        display: block;
        margin-bottom: 15px;
    }
    input {
        width: 100%;
        padding: 10px;
        border: 1px solid #ccc;
        border-radius: 5px;
    }
    button {
        padding: 10px 20px;
        background-color: #007bff;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
    button:hover {
        background-color: #0056b3;
    }
    p {
        font-size: 18px;
        color: #333;
    }
</style>

<div class="container">
    <h1>ISBN校验位计算器</h1>
    <label for="isbn">请输入ISBN（9位用于ISBN-10，12位用于ISBN-13）：</label>
    <input id="isbn" type="text" bind:value={inputISBN} />
    <button on:click={calculateCheckDigit}>计算校验位</button>
    <p>校验位：{checkDigit}</p>
</div>
