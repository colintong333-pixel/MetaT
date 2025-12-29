JavaScript

    const unitMap = {
        length: { l1: "Miles to Km", l2: "Km to Miles", factor: 1.60934, u1: "mi", u2: "km" },
        weight: { l1: "Lbs to Kg", l2: "Kg to Lbs", factor: 0.453592, u1: "lbs", u2: "kg" },
        temp: { l1: "Fah to Cel", l2: "Cel to Fah" },
        kitchen: { l1: "Cups to Grams (Flour)", l2: "Grams to Cups (Flour)", factor: 120, u1: "cups", u2: "g" }
    };

    function convert() {
        const val = parseFloat(document.getElementById('inputVal').value);
        if (isNaN(val)) return;
        
        const cat = document.getElementById('category').value;
        const type = document.getElementById('unitType').value;
        let res, unit;

        if (cat === 'temp') {
            res = (type === 'toMetric') ? (val - 32) * 5/9 : (val * 9/5) + 32;
            unit = (type === 'toMetric') ? "°C" : "°F";
        } else {
            // Standard multiplier logic for Length, Weight, and Kitchen
            res = (type === 'toMetric') ? val * unitMap[cat].factor : val / unitMap[cat].factor;
            unit = (type === 'toMetric') ? unitMap[cat].u2 : unitMap[cat].u1;
        }

        const final = res.toFixed(2);
        document.getElementById('output').innerText = `${final} ${unit}`;
        
        // Save to history logic
        clearTimeout(window.historyTimer);
        window.historyTimer = setTimeout(() => {
            addToHistory(`${val}${unitMap[cat]?.u1 || ''} → ${final} ${unit}`);
        }, 1200);
    }
