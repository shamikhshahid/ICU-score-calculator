<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ICU Score Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            backdrop-filter: blur(10px);
        }

        .header {
            background: linear-gradient(135deg, #2c3e50, #3498db);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            font-weight: 700;
        }

        .header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .content {
            padding: 40px;
        }

        .score-selector {
            margin-bottom: 30px;
        }

        .score-selector label {
            display: block;
            font-weight: 600;
            margin-bottom: 10px;
            font-size: 1.1rem;
            color: #2c3e50;
        }

        .score-selector select {
            width: 100%;
            padding: 15px;
            font-size: 1rem;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            background: white;
            transition: all 0.3s ease;
        }

        .score-selector select:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
        }

        .score-info {
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 30px;
            border-left: 5px solid #3498db;
        }

        .score-info h3 {
            color: #2c3e50;
            margin-bottom: 10px;
            font-size: 1.3rem;
        }

        .score-info p {
            color: #555;
            font-size: 1rem;
        }

        .form-section {
            background: #fff;
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            font-weight: 600;
            margin-bottom: 8px;
            color: #2c3e50;
        }

        .form-group input,
        .form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1rem;
            transition: all 0.3s ease;
        }

        .form-group input:focus,
        .form-group select:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
        }

        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }

        .btn {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            border: none;
            padding: 15px 30px;
            font-size: 1.1rem;
            font-weight: 600;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 100%;
            margin-top: 20px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(52, 152, 219, 0.3);
        }

        .btn:active {
            transform: translateY(0);
        }

        .results {
            background: linear-gradient(135deg, #27ae60, #2ecc71);
            color: white;
            padding: 30px;
            border-radius: 15px;
            margin-top: 30px;
            text-align: center;
        }

        .results h3 {
            font-size: 1.5rem;
            margin-bottom: 15px;
        }

        .score-value {
            font-size: 3rem;
            font-weight: 700;
            margin: 20px 0;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
        }

        .interpretation {
            background: rgba(255, 255, 255, 0.2);
            padding: 20px;
            border-radius: 10px;
            margin-top: 20px;
        }

        .hidden {
            display: none;
        }

        .warning {
            background: #fff3cd;
            border: 1px solid #ffeaa7;
            color: #856404;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
        }

        .warning strong {
            display: block;
            margin-bottom: 5px;
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 2rem;
            }
            
            .content {
                padding: 20px;
            }
            
            .form-row {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>ICU Score Calculator</h1>
            <p>Professional ICU and Emergency Medicine Assessment Tools</p>
        </div>

        <div class="content">
            <div class="warning">
                <strong>Medical Disclaimer:</strong>
                This calculator is for educational and reference purposes only. Always consult with qualified healthcare professionals for patient care decisions. Not intended for direct clinical use without proper medical supervision.
            </div>

            <div class="score-selector">
                <label for="scoreSelect">Select Score:</label>
                <select id="scoreSelect">
                    <option value="">Choose a scoring system...</option>
                    <option value="apache2">APACHE II</option>
                    <option value="sofa">SOFA</option>
                    <option value="qsofa">qSOFA</option>
                    <option value="gcs">Glasgow Coma Scale (GCS)</option>
                    <option value="rass">RASS</option>
                    <option value="camicu">CAM-ICU</option>
                    <option value="saps2">SAPS II</option>
                    <option value="nutric">NUTRIC Score</option>
                    <option value="rifle">RIFLE</option>
                    <option value="pao2fio2">PaO2/FiO2 Ratio</option>
                </select>
            </div>

            <div id="scoreInfo" class="score-info hidden"></div>
            <div id="calculatorForm" class="form-section hidden"></div>
            <div id="results" class="results hidden"></div>
        </div>
    </div>

    <script>
        const scores = {
            apache2: {
                name: "APACHE II",
                description: "Predicts ICU mortality using a range of physiological and chronic health variables.",
                fields: [
                    { name: "temperature", label: "Temperature (°C)", type: "number", step: "0.1", min: "32", max: "45" },
                    { name: "map", label: "Mean Arterial Pressure (mmHg)", type: "number", min: "0", max: "300" },
                    { name: "heartRate", label: "Heart Rate (bpm)", type: "number", min: "0", max: "300" },
                    { name: "respRate", label: "Respiratory Rate (/min)", type: "number", min: "0", max: "100" },
                    { name: "pao2", label: "PaO2 (mmHg) or A-a gradient", type: "number", step: "0.1", min: "0" },
                    { name: "ph", label: "Arterial pH", type: "number", step: "0.01", min: "6.0", max: "8.0" },
                    { name: "sodium", label: "Serum Sodium (mEq/L)", type: "number", min: "100", max: "200" },
                    { name: "potassium", label: "Serum Potassium (mEq/L)", type: "number", step: "0.1", min: "0", max: "10" },
                    { name: "creatinine", label: "Serum Creatinine (mg/dL)", type: "number", step: "0.1", min: "0" },
                    { name: "hematocrit", label: "Hematocrit (%)", type: "number", step: "0.1", min: "0", max: "100" },
                    { name: "wbc", label: "White Blood Cell Count (×10³/μL)", type: "number", step: "0.1", min: "0" },
                    { name: "gcs", label: "Glasgow Coma Scale", type: "number", min: "3", max: "15" },
                    { name: "age", label: "Age (years)", type: "number", min: "0", max: "120" },
                    { name: "chronicHealth", label: "Chronic Health Points", type: "select", options: [
                        { value: "0", text: "No chronic health problems" },
                        { value: "2", text: "Non-operative or emergency postoperative" },
                        { value: "5", text: "Elective postoperative" }
                    ]}
                ]
            },
            sofa: {
                name: "SOFA",
                description: "Assesses organ dysfunction and predicts ICU mortality in sepsis.",
                fields: [
                    { name: "pao2fio2", label: "PaO2/FiO2 Ratio", type: "number", min: "0" },
                    { name: "platelets", label: "Platelet Count (×10³/μL)", type: "number", min: "0" },
                    { name: "bilirubin", label: "Bilirubin (mg/dL)", type: "number", step: "0.1", min: "0" },
                    { name: "map", label: "Mean Arterial Pressure (mmHg)", type: "number", min: "0", max: "300" },
                    { name: "vasopressors", label: "Vasopressor Use", type: "select", options: [
                        { value: "none", text: "No vasopressors" },
                        { value: "dopa5", text: "Dopamine ≤5 μg/kg/min" },
                        { value: "dopa15", text: "Dopamine 5.1-15 μg/kg/min" },
                        { value: "dopa15plus", text: "Dopamine >15 μg/kg/min or any norepinephrine" }
                    ]},
                    { name: "gcs", label: "Glasgow Coma Scale", type: "number", min: "3", max: "15" },
                    { name: "creatinine", label: "Creatinine (mg/dL)", type: "number", step: "0.1", min: "0" },
                    { name: "urineOutput", label: "Urine Output (mL/day)", type: "number", min: "0" }
                ]
            },
            qsofa: {
                name: "qSOFA",
                description: "Quick bedside assessment for identifying patients at risk of sepsis-related mortality.",
                fields: [
                    { name: "respRate", label: "Respiratory Rate ≥22/min", type: "select", options: [
                        { value: "0", text: "No (<22/min)" },
                        { value: "1", text: "Yes (≥22/min)" }
                    ]},
                    { name: "alteredMental", label: "Altered Mental Status", type: "select", options: [
                        { value: "0", text: "No" },
                        { value: "1", text: "Yes" }
                    ]},
                    { name: "systolicBP", label: "Systolic BP ≤100 mmHg", type: "select", options: [
                        { value: "0", text: "No (>100 mmHg)" },
                        { value: "1", text: "Yes (≤100 mmHg)" }
                    ]}
                ]
            },
            gcs: {
                name: "Glasgow Coma Scale (GCS)",
                description: "Evaluates level of consciousness in trauma and neurological patients.",
                fields: [
                    { name: "eyeOpening", label: "Eye Opening", type: "select", options: [
                        { value: "1", text: "1 - No eye opening" },
                        { value: "2", text: "2 - Eye opening to pain" },
                        { value: "3", text: "3 - Eye opening to verbal command" },
                        { value: "4", text: "4 - Eyes open spontaneously" }
                    ]},
                    { name: "verbalResponse", label: "Verbal Response", type: "select", options: [
                        { value: "1", text: "1 - No verbal response" },
                        { value: "2", text: "2 - Incomprehensible sounds" },
                        { value: "3", text: "3 - Inappropriate words" },
                        { value: "4", text: "4 - Confused" },
                        { value: "5", text: "5 - Oriented" }
                    ]},
                    { name: "motorResponse", label: "Motor Response", type: "select", options: [
                        { value: "1", text: "1 - No motor response" },
                        { value: "2", text: "2 - Extension to pain" },
                        { value: "3", text: "3 - Flexion to pain" },
                        { value: "4", text: "4 - Withdrawal from pain" },
                        { value: "5", text: "5 - Localizing pain" },
                        { value: "6", text: "6 - Obeys commands" }
                    ]}
                ]
            },
            rass: {
                name: "RASS",
                description: "Measures sedation and agitation levels in ICU patients.",
                fields: [
                    { name: "level", label: "RASS Level", type: "select", options: [
                        { value: "4", text: "+4 Combative" },
                        { value: "3", text: "+3 Very agitated" },
                        { value: "2", text: "+2 Agitated" },
                        { value: "1", text: "+1 Restless" },
                        { value: "0", text: "0 Alert and calm" },
                        { value: "-1", text: "-1 Drowsy" },
                        { value: "-2", text: "-2 Light sedation" },
                        { value: "-3", text: "-3 Moderate sedation" },
                        { value: "-4", text: "-4 Deep sedation" },
                        { value: "-5", text: "-5 Unarousable" }
                    ]}
                ]
            },
            camicu: {
                name: "CAM-ICU",
                description: "Detects delirium in ICU patients.",
                fields: [
                    { name: "acuteOnset", label: "Acute onset or fluctuating course", type: "select", options: [
                        { value: "0", text: "No" },
                        { value: "1", text: "Yes" }
                    ]},
                    { name: "inattention", label: "Inattention", type: "select", options: [
                        { value: "0", text: "No" },
                        { value: "1", text: "Yes" }
                    ]},
                    { name: "disorganizedThinking", label: "Disorganized thinking", type: "select", options: [
                        { value: "0", text: "No" },
                        { value: "1", text: "Yes" }
                    ]},
                    { name: "alteredConsciousness", label: "Altered level of consciousness", type: "select", options: [
                        { value: "0", text: "No" },
                        { value: "1", text: "Yes" }
                    ]}
                ]
            },
            pao2fio2: {
                name: "PaO2/FiO2 Ratio",
                description: "Measures the degree of hypoxemia and ARDS severity.",
                fields: [
                    { name: "pao2", label: "PaO2 (mmHg)", type: "number", step: "0.1", min: "0" },
                    { name: "fio2", label: "FiO2 (decimal, e.g., 0.21 for 21%)", type: "number", step: "0.01", min: "0.21", max: "1.0" }
                ]
            }
        };

        const scoreSelect = document.getElementById('scoreSelect');
        const scoreInfo = document.getElementById('scoreInfo');
        const calculatorForm = document.getElementById('calculatorForm');
        const results = document.getElementById('results');

        scoreSelect.addEventListener('change', function() {
            const selectedScore = this.value;
            if (selectedScore && scores[selectedScore]) {
                showScoreCalculator(selectedScore);
            } else {
                hideAll();
            }
        });

        function hideAll() {
            scoreInfo.classList.add('hidden');
            calculatorForm.classList.add('hidden');
            results.classList.add('hidden');
        }

        function showScoreCalculator(scoreKey) {
            const score = scores[scoreKey];
            
            // Show score info
            scoreInfo.innerHTML = `
                <h3>${score.name}</h3>
                <p>${score.description}</p>
            `;
            scoreInfo.classList.remove('hidden');

            // Create form
            let formHTML = `<h3>Enter ${score.name} Parameters</h3>`;
            
            if (score.fields.length <= 6) {
                // Single column for shorter forms
                score.fields.forEach(field => {
                    formHTML += createFieldHTML(field);
                });
            } else {
                // Two columns for longer forms
                formHTML += '<div class="form-row">';
                score.fields.forEach(field => {
                    formHTML += `<div>${createFieldHTML(field)}</div>`;
                });
                formHTML += '</div>';
            }
            
            formHTML += `<button type="button" class="btn" onclick="calculateScore('${scoreKey}')">Calculate ${score.name} Score</button>`;
            
            calculatorForm.innerHTML = formHTML;
            calculatorForm.classList.remove('hidden');
            results.classList.add('hidden');
        }

        function createFieldHTML(field) {
            let html = `<div class="form-group">
                <label for="${field.name}">${field.label}</label>`;
            
            if (field.type === 'select') {
                html += `<select id="${field.name}" required>
                    <option value="">Select...</option>`;
                field.options.forEach(option => {
                    html += `<option value="${option.value}">${option.text}</option>`;
                });
                html += '</select>';
            } else {
                html += `<input type="${field.type}" id="${field.name}" 
                    ${field.min ? `min="${field.min}"` : ''}
                    ${field.max ? `max="${field.max}"` : ''}
                    ${field.step ? `step="${field.step}"` : ''}
                    required>`;
            }
            
            html += '</div>';
            return html;
        }

        function calculateScore(scoreKey) {
            const score = scores[scoreKey];
            let calculatedScore = 0;
            let interpretation = '';

            // Get form values
            const values = {};
            score.fields.forEach(field => {
                const element = document.getElementById(field.name);
                values[field.name] = element.value;
            });

            // Calculate based on score type
            switch(scoreKey) {
                case 'apache2':
                    calculatedScore = calculateApache2(values);
                    interpretation = getApache2Interpretation(calculatedScore);
                    break;
                case 'sofa':
                    calculatedScore = calculateSOFA(values);
                    interpretation = getSOFAInterpretation(calculatedScore);
                    break;
                case 'qsofa':
                    calculatedScore = calculateQSOFA(values);
                    interpretation = getQSOFAInterpretation(calculatedScore);
                    break;
                case 'gcs':
                    calculatedScore = calculateGCS(values);
                    interpretation = getGCSInterpretation(calculatedScore);
                    break;
                case 'rass':
                    calculatedScore = values.level;
                    interpretation = getRASSInterpretation(calculatedScore);
                    break;
                case 'camicu':
                    calculatedScore = calculateCAMICU(values);
                    interpretation = getCAMICUInterpretation(calculatedScore);
                    break;
                case 'pao2fio2':
                    calculatedScore = calculatePaO2FiO2(values);
                    interpretation = getPaO2FiO2Interpretation(calculatedScore);
                    break;
            }

            showResults(score.name, calculatedScore, interpretation);
        }

        function calculateApache2(values) {
            let score = 0;
            
            // Temperature points (°C)
            const temp = parseFloat(values.temperature);
            if (temp >= 41 || temp <= 29.9) score += 4;
            else if ((temp >= 39 && temp <= 40.9) || (temp >= 30 && temp <= 31.9)) score += 3;
            else if ((temp >= 38.5 && temp <= 38.9) || (temp >= 32 && temp <= 33.9)) score += 1;
            else if (temp >= 36 && temp <= 38.4) score += 0;
            else if (temp >= 34 && temp <= 35.9) score += 1;
            
            // Mean Arterial Pressure (mmHg)
            const map = parseFloat(values.map);
            if (map >= 160) score += 4;
            else if (map >= 130) score += 3;
            else if (map >= 110) score += 2;
            else if (map >= 70) score += 0;
            else if (map >= 50) score += 2;
            else if (map <= 49) score += 4;
            
            // Heart Rate (bpm)
            const hr = parseFloat(values.heartRate);
            if (hr >= 180) score += 4;
            else if (hr >= 140) score += 3;
            else if (hr >= 110) score += 2;
            else if (hr >= 70) score += 0;
            else if (hr >= 55) score += 2;
            else if (hr >= 40) score += 3;
            else if (hr <= 39) score += 4;
            
            // Respiratory Rate (/min)
            const rr = parseFloat(values.respRate);
            if (rr >= 50) score += 4;
            else if (rr >= 35) score += 3;
            else if (rr >= 25) score += 1;
            else if (rr >= 12) score += 0;
            else if (rr >= 10) score += 1;
            else if (rr >= 6) score += 2;
            else if (rr <= 5) score += 4;
            
            // Oxygenation (PaO2 if FiO2 >= 0.5, use A-a gradient; if FiO2 < 0.5, use PaO2)
            const pao2 = parseFloat(values.pao2);
            if (pao2 >= 500) score += 4; // A-a gradient
            else if (pao2 >= 350) score += 3;
            else if (pao2 >= 200) score += 2;
            else if (pao2 < 200 && pao2 >= 70) score += 0; // PaO2
            else if (pao2 < 70 && pao2 >= 61) score += 1;
            else if (pao2 < 61 && pao2 >= 55) score += 3;
            else if (pao2 < 55) score += 4;
            
            // Arterial pH
            const ph = parseFloat(values.ph);
            if (ph >= 7.7) score += 4;
            else if (ph >= 7.6) score += 3;
            else if (ph >= 7.5) score += 1;
            else if (ph >= 7.33) score += 0;
            else if (ph >= 7.25) score += 2;
            else if (ph >= 7.15) score += 3;
            else if (ph < 7.15) score += 4;
            
            // Serum Sodium (mEq/L)
            const sodium = parseFloat(values.sodium);
            if (sodium >= 180) score += 4;
            else if (sodium >= 160) score += 3;
            else if (sodium >= 155) score += 2;
            else if (sodium >= 150) score += 1;
            else if (sodium >= 130) score += 0;
            else if (sodium >= 120) score += 2;
            else if (sodium >= 111) score += 3;
            else if (sodium <= 110) score += 4;
            
            // Serum Potassium (mEq/L)
            const potassium = parseFloat(values.potassium);
            if (potassium >= 7) score += 4;
            else if (potassium >= 6) score += 3;
            else if (potassium >= 5.5) score += 1;
            else if (potassium >= 3.5) score += 0;
            else if (potassium >= 3) score += 1;
            else if (potassium >= 2.5) score += 2;
            else if (potassium < 2.5) score += 4;
            
            // Serum Creatinine (mg/dL) - doubled if acute renal failure
            const creatinine = parseFloat(values.creatinine);
            if (creatinine >= 3.5) score += 4;
            else if (creatinine >= 2) score += 3;
            else if (creatinine >= 1.5) score += 2;
            else if (creatinine >= 0.6) score += 0;
            else if (creatinine < 0.6) score += 2;
            
            // Hematocrit (%)
            const hct = parseFloat(values.hematocrit);
            if (hct >= 60) score += 4;
            else if (hct >= 50) score += 2;
            else if (hct >= 46) score += 1;
            else if (hct >= 30) score += 0;
            else if (hct >= 20) score += 2;
            else if (hct < 20) score += 4;
            
            // White Blood Cell Count (×10³/μL)
            const wbc = parseFloat(values.wbc);
            if (wbc >= 40) score += 4;
            else if (wbc >= 20) score += 2;
            else if (wbc >= 15) score += 1;
            else if (wbc >= 3) score += 0;
            else if (wbc >= 1) score += 2;
            else if (wbc < 1) score += 4;
            
            // Glasgow Coma Scale
            const gcs = parseFloat(values.gcs);
            score += (15 - gcs);
            
            // Age points
            const age = parseFloat(values.age);
            if (age >= 75) score += 6;
            else if (age >= 65) score += 5;
            else if (age >= 55) score += 3;
            else if (age >= 45) score += 2;
            else score += 0;
            
            // Chronic health points
            score += parseFloat(values.chronicHealth);
            
            return Math.round(score);
        }

        function calculateSOFA(values) {
            let score = 0;
            
            // Respiratory System (PaO2/FiO2)
            const pao2fio2 = parseFloat(values.pao2fio2);
            if (pao2fio2 < 100) score += 4;
            else if (pao2fio2 < 200) score += 3;
            else if (pao2fio2 < 300) score += 2;
            else if (pao2fio2 < 400) score += 1;
            else score += 0;
            
            // Coagulation (Platelets ×10³/μL)
            const platelets = parseFloat(values.platelets);
            if (platelets < 20) score += 4;
            else if (platelets < 50) score += 3;
            else if (platelets < 100) score += 2;
            else if (platelets < 150) score += 1;
            else score += 0;
            
            // Liver (Bilirubin mg/dL)
            const bilirubin = parseFloat(values.bilirubin);
            if (bilirubin >= 12) score += 4;
            else if (bilirubin >= 6) score += 3;
            else if (bilirubin >= 2) score += 2;
            else if (bilirubin >= 1.2) score += 1;
            else score += 0;
            
            // Cardiovascular System
            const map = parseFloat(values.map);
            const vasopressors = values.vasopressors;
            
            if (vasopressors === 'dopa15plus') score += 4; // Dopamine >15 or any norepinephrine
            else if (vasopressors === 'dopa15') score += 3; // Dopamine 5.1-15
            else if (vasopressors === 'dopa5') score += 2; // Dopamine ≤5
            else if (map < 70) score += 1;
            else score += 0;
            
            // Central Nervous System (Glasgow Coma Scale)
            const gcs = parseFloat(values.gcs);
            if (gcs < 6) score += 4;
            else if (gcs <= 9) score += 3;
            else if (gcs <= 12) score += 2;
            else if (gcs <= 14) score += 1;
            else score += 0;
            
            // Renal System
            const creatinine = parseFloat(values.creatinine);
            const urineOutput = parseFloat(values.urineOutput);
            
            if (creatinine >= 5 || urineOutput < 200) score += 4;
            else if (creatinine >= 3.5 || urineOutput < 500) score += 3;
            else if (creatinine >= 2 || urineOutput < 1000) score += 2;
            else if (creatinine >= 1.2) score += 1;
            else score += 0;
            
            return score;
        }

        function calculateQSOFA(values) {
            return parseInt(values.respRate) + parseInt(values.alteredMental) + parseInt(values.systolicBP);
        }

        function calculateGCS(values) {
            return parseInt(values.eyeOpening) + parseInt(values.verbalResponse) + parseInt(values.motorResponse);
        }

        function calculateCAMICU(values) {
            const features = parseInt(values.acuteOnset) + parseInt(values.inattention) + 
                           parseInt(values.disorganizedThinking) + parseInt(values.alteredConsciousness);
            return (values.acuteOnset === '1' && values.inattention === '1' && 
                   (values.disorganizedThinking === '1' || values.alteredConsciousness === '1')) ? 1 : 0;
        }

        function calculatePaO2FiO2(values) {
            return Math.round((parseFloat(values.pao2) / parseFloat(values.fio2)) * 10) / 10;
        }

        function getApache2Interpretation(score) {
            // APACHE II mortality prediction based on original validation
            let mortality;
            if (score <= 4) mortality = 4;
            else if (score <= 9) mortality = 8;
            else if (score <= 14) mortality = 15;
            else if (score <= 19) mortality = 24;
            else if (score <= 24) mortality = 40;
            else if (score <= 29) mortality = 55;
            else if (score <= 34) mortality = 73;
            else mortality = 85;
            
            return `APACHE II Score: ${score}/71. Predicted hospital mortality: approximately ${mortality}%`;
        }

        function getSOFAInterpretation(score) {
            let mortality, organFailure;
            
            if (score <= 6) {
                mortality = "<10%";
                organFailure = "No to mild organ dysfunction";
            } else if (score <= 9) {
                mortality = "15-20%";
                organFailure = "Moderate organ dysfunction";
            } else if (score <= 12) {
                mortality = "40-50%";
                organFailure = "Severe organ dysfunction";
            } else {
                mortality = ">50%";
                organFailure = "Multiple organ failure";
            }
            
            return `SOFA Score: ${score}/24. ${organFailure}. ICU mortality risk: ${mortality}`;
        }

        function getQSOFAInterpretation(score) {
            if (score >= 2) {
                return `qSOFA Score: ${score}/3. POSITIVE - High risk for sepsis-related poor outcomes. Consider sepsis workup and possible ICU care.`;
            } else {
                return `qSOFA Score: ${score}/3. NEGATIVE - Lower risk for sepsis-related poor outcomes. Continue monitoring.`;
            }
        }

        function getGCSInterpretation(score) {
            let severity, description;
            
            if (score <= 8) {
                severity = "Severe brain injury";
                description = "Coma state - requires immediate intervention";
            } else if (score <= 12) {
                severity = "Moderate brain injury";
                description = "Significant impairment - close monitoring required";
            } else if (score <= 14) {
                severity = "Mild brain injury";
                description = "Mild impairment - regular assessment needed";
            } else {
                severity = "Normal";
                description = "Normal neurological function";
            }
            
            return `GCS Score: ${score}/15. ${severity}. ${description}`;
        }

        function getSAPS2Interpretation(score) {
            // SAPS II mortality prediction using logistic regression equation
            // Mortality = e^(-7.7631 + 0.0737 × SAPS II + 0.9971 × ln(SAPS II + 1)) / (1 + e^(-7.7631 + 0.0737 × SAPS II + 0.9971 × ln(SAPS II + 1)))
            
            let mortality;
            if (score <= 29) mortality = "<10%";
            else if (score <= 40) mortality = "10-25%";
            else if (score <= 52) mortality = "25-50%";
            else if (score <= 64) mortality = "50-75%";
            else if (score <= 77) mortality = "75-90%";
            else mortality = ">90%";
            
            return `SAPS II Score: ${score}/163. Predicted hospital mortality: ${mortality}`;
        }

        function getNUTRICInterpretation(score) {
            if (score < 5) {
                return `NUTRIC Score: ${score}/9. LOW nutritional risk. These patients are unlikely to benefit significantly from aggressive nutrition therapy.`;
            } else if (score <= 9) {
                return `NUTRIC Score: ${score}/9. HIGH nutritional risk. These patients are likely to benefit from nutrition therapy and should receive early, aggressive nutritional support.`;
            }
            
            return `NUTRIC Score: ${score}/9. VERY HIGH nutritional risk. Immediate aggressive nutrition therapy is strongly recommended.`;
        }

        function getRASSInterpretation(score) {
            const interpretations = {
                '4': "Combative - Overtly combative, violent, immediate danger to staff",
                '3': "Very agitated - Pulls or removes tubes/catheters, aggressive",
                '2': "Agitated - Frequent non-purposeful movement, fights ventilator",
                '1': "Restless - Anxious, apprehensive, movements not aggressive",
                '0': "Alert and calm - Spontaneous, appropriate interaction",
                '-1': "Drowsy - Not fully alert, sustained awakening to voice (>10 sec)",
                '-2': "Light sedation - Briefly awakens to voice (<10 sec)",
                '-3': "Moderate sedation - Movement/eye opening to voice (no eye contact)",
                '-4': "Deep sedation - No response to voice, movement/eye opening to physical stimulation",
                '-5': "Unarousable - No response to voice or physical stimulation"
            };
            return interpretations[score] || "Invalid score";
        }

        function getCAMICUInterpretation(score) {
            if (score === 1) return "Positive CAM-ICU - Delirium present";
            else return "Negative CAM-ICU - No delirium detected";
        }

        function getPaO2FiO2Interpretation(score) {
            if (score >= 300) return "Normal oxygenation";
            else if (score >= 200) return "Mild ARDS";
            else if (score >= 100) return "Moderate ARDS";
            else return "Severe ARDS";
        }

        function showResults(scoreName, score, interpretation) {
            results.innerHTML = `
                <h3>${scoreName} Results</h3>
                <div class="score-value">${score}</div>
                <div class="interpretation">
                    <h4>Interpretation:</h4>
                    <p>${interpretation}</p>
                </div>
            `;
            results.classList.remove('hidden');
            results.scrollIntoView({ behavior: 'smooth' });
        }

        // Add SAPS II and NUTRIC calculations
        function addAdvancedScores() {
            scores.saps2 = {
                name: "SAPS II",
                description: "Predicts ICU mortality based on physiological measurements and underlying disease.",
                fields: [
                    { name: "age", label: "Age (years)", type: "number", min: "0", max: "120" },
                    { name: "heartRate", label: "Heart Rate (bpm)", type: "number", min: "0", max: "300" },
                    { name: "systolicBP", label: "Systolic BP (mmHg)", type: "number", min: "0", max: "300" },
                    { name: "bodyTemp", label: "Body Temperature (°C)", type: "number", step: "0.1", min: "32", max: "45" },
                    { name: "gcs", label: "Glasgow Coma Scale", type: "number", min: "3", max: "15" },
                    { name: "pao2fio2", label: "PaO2/FiO2 Ratio", type: "number", min: "0" },
                    { name: "urineOutput", label: "Urine Output (L/24h)", type: "number", step: "0.1", min: "0" },
                    { name: "bun", label: "BUN (mg/dL)", type: "number", step: "0.1", min: "0" },
                    { name: "wbc", label: "WBC (×10³/μL)", type: "number", step: "0.1", min: "0" },
                    { name: "sodium", label: "Sodium (mEq/L)", type: "number", min: "100", max: "200" },
                    { name: "potassium", label: "Potassium (mEq/L)", type: "number", step: "0.1", min: "0", max: "10" },
                    { name: "bicarbonate", label: "Bicarbonate (mEq/L)", type: "number", step: "0.1", min: "0", max: "50" },
                    { name: "bilirubin", label: "Bilirubin (mg/dL)", type: "number", step: "0.1", min: "0" },
                    { name: "admissionType", label: "Type of Admission", type: "select", options: [
                        { value: "0", text: "Scheduled surgical" },
                        { value: "6", text: "Medical" },
                        { value: "8", text: "Unscheduled surgical" }
                    ]},
                    { name: "chronicDiseases", label: "Chronic Diseases", type: "select", options: [
                        { value: "0", text: "None" },
                        { value: "9", text: "Metastatic cancer" },
                        { value: "10", text: "Hematologic malignancy" },
                        { value: "17", text: "AIDS" }
                    ]}
                ]
            };

            scores.nutric = {
                name: "NUTRIC Score",
                description: "Assesses nutritional risk in critically ill patients.",
                fields: [
                    { name: "age", label: "Age", type: "select", options: [
                        { value: "0", text: "<50 years" },
                        { value: "1", text: "50-74 years" },
                        { value: "2", text: "≥75 years" }
                    ]},
                    { name: "apache2", label: "APACHE II Score", type: "select", options: [
                        { value: "0", text: "<15" },
                        { value: "1", text: "15-19" },
                        { value: "2", text: "20-28" },
                        { value: "3", text: ">28" }
                    ]},
                    { name: "sofa", label: "SOFA Score", type: "select", options: [
                        { value: "0", text: "<6" },
                        { value: "1", text: "6-9" },
                        { value: "2", text: "≥10" }
                    ]},
                    { name: "comorbidities", label: "Number of Comorbidities", type: "select", options: [
                        { value: "0", text: "0-1" },
                        { value: "1", text: "≥2" }
                    ]},
                    { name: "daysToICU", label: "Days from Hospital to ICU", type: "select", options: [
                        { value: "0", text: "0-1 days" },
                        { value: "1", text: "≥2 days" }
                    ]},
                    { name: "il6", label: "IL-6 (optional)", type: "select", options: [
                        { value: "0", text: "Not available/Normal" },
                        { value: "1", text: "Elevated" }
                    ]}
                ]
            };

            scores.rifle = {
                name: "RIFLE",
                description: "Classifies severity of acute kidney injury.",
                fields: [
                    { name: "creatinine", label: "Serum Creatinine (mg/dL)", type: "number", step: "0.1", min: "0" },
                    { name: "baselineCreatinine", label: "Baseline Creatinine (mg/dL)", type: "number", step: "0.1", min: "0" },
                    { name: "urineOutput", label: "Urine Output (mL/kg/h)", type: "number", step: "0.1", min: "0" }
                ]
            };
        }

        // Add calculation functions for advanced scores
        function calculateSAPS2(values) {
            let score = 0;
            
            // Age points
            const age = parseFloat(values.age);
            if (age < 40) score += 0;
            else if (age < 60) score += 7;
            else if (age < 70) score += 12;
            else if (age < 75) score += 15;
            else if (age < 80) score += 16;
            else score += 18;
            
            // Heart Rate (bpm)
            const hr = parseFloat(values.heartRate);
            if (hr < 40) score += 11;
            else if (hr < 70) score += 2;
            else if (hr < 120) score += 0;
            else if (hr < 160) score += 4;
            else score += 7;
            
            // Systolic Blood Pressure (mmHg)
            const sbp = parseFloat(values.systolicBP);
            if (sbp < 70) score += 13;
            else if (sbp < 100) score += 5;
            else if (sbp < 200) score += 0;
            else score += 2;
            
            // Body Temperature (°C)
            const temp = parseFloat(values.bodyTemp);
            if (temp < 39) score += 0;
            else score += 3;
            
            // Glasgow Coma Scale
            const gcs = parseFloat(values.gcs);
            if (gcs < 6) score += 26;
            else if (gcs < 9) score += 13;
            else if (gcs < 11) score += 7;
            else if (gcs < 14) score += 5;
            else score += 0;
            
            // PaO2/FiO2 Ratio
            const pao2fio2 = parseFloat(values.pao2fio2);
            if (pao2fio2 < 100) score += 11;
            else if (pao2fio2 < 200) score += 9;
            else if (pao2fio2 < 300) score += 6;
            else score += 0;
            
            // Urine Output (L/24h)
            const urine = parseFloat(values.urineOutput);
            if (urine < 0.5) score += 11;
            else if (urine < 1) score += 4;
            else score += 0;
            
            // BUN (mg/dL)
            const bun = parseFloat(values.bun);
            if (bun < 28) score += 0;
            else if (bun < 84) score += 6;
            else score += 10;
            
            // WBC (×10³/μL)
            const wbc = parseFloat(values.wbc);
            if (wbc < 1) score += 12;
            else if (wbc < 20) score += 0;
            else score += 3;
            
            // Sodium (mEq/L)
            const sodium = parseFloat(values.sodium);
            if (sodium < 125) score += 5;
            else if (sodium < 145) score += 0;
            else score += 1;
            
            // Potassium (mEq/L)
            const potassium = parseFloat(values.potassium);
            if (potassium < 3) score += 3;
            else if (potassium < 5) score += 0;
            else score += 3;
            
            // Bicarbonate (mEq/L)
            const bicarbonate = parseFloat(values.bicarbonate);
            if (bicarbonate < 15) score += 6;
            else if (bicarbonate < 20) score += 3;
            else score += 0;
            
            // Bilirubin (mg/dL)
            const bilirubin = parseFloat(values.bilirubin);
            if (bilirubin < 4) score += 0;
            else if (bilirubin < 6) score += 4;
            else score += 9;
            
            // Admission type
            score += parseFloat(values.admissionType);
            
            // Chronic diseases
            score += parseFloat(values.chronicDiseases);
            
            return Math.round(score);
        }

        function calculateNUTRIC(values) {
            return parseInt(values.age) + parseInt(values.apache2) + parseInt(values.sofa) + 
                   parseInt(values.comorbidities) + parseInt(values.daysToICU) + parseInt(values.il6);
        }

        function calculateRIFLE(values) {
            const creatinine = parseFloat(values.creatinine);
            const baseline = parseFloat(values.baselineCreatinine);
            const urineOutput = parseFloat(values.urineOutput);
            
            const creatinineRatio = creatinine / baseline;
            
            if (creatinineRatio >= 3 || creatinine >= 4 || urineOutput < 0.3) {
                return "Failure";
            } else if (creatinineRatio >= 2 || urineOutput < 0.5) {
                return "Injury";
            } else if (creatinineRatio >= 1.5 || urineOutput < 0.5) {
                return "Risk";
            } else {
                return "Normal";
            }
        }

        function getSAPS2Interpretation(score) {
            if (score < 29) return "Low mortality risk (<10%)";
            else if (score < 40) return "Low-moderate mortality risk (10-25%)";
            else if (score < 50) return "Moderate mortality risk (25-50%)";
            else if (score < 60) return "High mortality risk (50-75%)";
            else return "Very high mortality risk (>75%)";
        }

        function getNUTRICInterpretation(score) {
            if (score < 5) return "Low nutritional risk - Nutrition therapy may not be beneficial";
            else if (score <= 9) return "High nutritional risk - Likely to benefit from nutrition therapy";
            else return "Very high nutritional risk - Aggressive nutrition therapy recommended";
        }

        function getRIFLEInterpretation(classification) {
            const interpretations = {
                "Normal": "No acute kidney injury",
                "Risk": "Risk of AKI - Monitor closely",
                "Injury": "Kidney injury present - Intervention may be needed",
                "Failure": "Kidney failure - Immediate intervention required"
            };
            return interpretations[classification] || "Unable to classify";
        }

        // Initialize advanced scores
        addAdvancedScores();

        // Update the main calculation function to handle new scores
        const originalCalculateScore = calculateScore;
        calculateScore = function(scoreKey) {
            const score = scores[scoreKey];
            let calculatedScore = 0;
            let interpretation = '';

            // Get form values
            const values = {};
            score.fields.forEach(field => {
                const element = document.getElementById(field.name);
                values[field.name] = element.value;
            });

            // Calculate based on score type
            switch(scoreKey) {
                case 'apache2':
                    calculatedScore = calculateApache2(values);
                    interpretation = getApache2Interpretation(calculatedScore);
                    break;
                case 'sofa':
                    calculatedScore = calculateSOFA(values);
                    interpretation = getSOFAInterpretation(calculatedScore);
                    break;
                case 'qsofa':
                    calculatedScore = calculateQSOFA(values);
                    interpretation = getQSOFAInterpretation(calculatedScore);
                    break;
                case 'gcs':
                    calculatedScore = calculateGCS(values);
                    interpretation = getGCSInterpretation(calculatedScore);
                    break;
                case 'rass':
                    calculatedScore = values.level;
                    interpretation = getRASSInterpretation(calculatedScore);
                    break;
                case 'camicu':
                    calculatedScore = calculateCAMICU(values);
                    interpretation = getCAMICUInterpretation(calculatedScore);
                    break;
                case 'saps2':
                    calculatedScore = calculateSAPS2(values);
                    interpretation = getSAPS2Interpretation(calculatedScore);
                    break;
                case 'nutric':
                    calculatedScore = calculateNUTRIC(values);
                    interpretation = getNUTRICInterpretation(calculatedScore);
                    break;
                case 'rifle':
                    calculatedScore = calculateRIFLE(values);
                    interpretation = getRIFLEInterpretation(calculatedScore);
                    break;
                case 'pao2fio2':
                    calculatedScore = calculatePaO2FiO2(values);
                    interpretation = getPaO2FiO2Interpretation(calculatedScore);
                    break;
            }

            showResults(score.name, calculatedScore, interpretation);
        };
    </script>
</body>
</html>
