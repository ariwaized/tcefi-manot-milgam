<!DOCTYPE html>
<html lang="he">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>כלי לסינון הזמנות</title>
    <!-- Tailwind CSS CDN for modern and clean styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Heebo:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Heebo', sans-serif;
            background-color: #f3f4f6;
        }
        .container {
            max-width: 1200px;
            margin: auto;
            padding: 2rem;
        }
        .card {
            background-color: white;
            padding: 2rem;
            border-radius: 1rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .styled-button {
            background-color: #4299e1; /* Tailwind blue-500 */
            color: white;
            font-weight: 700;
            padding: 0.75rem 1.5rem;
            border-radius: 0.75rem;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            transition: background-color 0.2s, transform 0.2s;
        }
        .styled-button:hover {
            background-color: #3182ce; /* Tailwind blue-600 */
            transform: translateY(-2px);
        }
        .load-buttons-container {
            display: flex;
            gap: 1rem;
            justify-content: center;
            margin-bottom: 1.5rem;
        }
        .hidden-input {
            display: none;
        }
        .date-buttons-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 1rem;
            margin-bottom: 2rem;
        }
        .summary-block {
            background-color: #f9fafb;
            padding: 1.5rem;
            border-radius: 0.75rem;
            margin-top: 1rem;
            box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.05);
        }
        .summary-item {
            display: flex;
            justify-content: space-between;
            font-size: 1.125rem;
            font-weight: 500;
            margin-bottom: 0.5rem;
        }
    </style>
</head>
<body dir="rtl" class="p-8">

    <div class="container text-right">
        <h1 class="text-4xl font-bold text-center text-gray-800 mb-8">כלי לסינון והפצת הזמנות</h1>
        
        <div class="card mb-8">
            <h2 class="text-2xl font-semibold text-gray-700 mb-4">טעינת נתונים:</h2>
            <p class="text-gray-600 mb-4">
                אנא טען את קובץ המוסדות וקובץ ההזמנות שלך. המערכת תזהה את העמודות באופן אוטומטי.
            </p>
            
            <div class="load-buttons-container">
                <button onclick="document.getElementById('institutions-file-input').click()" class="styled-button">טען קובץ מוסדות</button>
                <input type="file" id="institutions-file-input" class="hidden-input" accept=".xlsx,.xls,.csv">
                
                <button onclick="document.getElementById('orders-file-input').click()" class="styled-button">טען קובץ הזמנות</button>
                <input type="file" id="orders-file-input" class="hidden-input" accept=".xlsx,.xls,.csv">

                <button onclick="resetTool()" class="styled-button bg-red-500 hover:bg-red-600">איפוס</button>
            </div>
            <div id="message-area" class="text-center mt-4 font-semibold text-gray-700"></div>
        </div>

        <div class="card" id="main-content" style="display:none;">
            <h2 class="text-2xl font-semibold text-gray-700 mb-4">סיכומים לפי תאריך:</h2>
            <p class="text-gray-600 mb-4">לחץ על תאריך כדי לראות את הסיכום היומי.</p>
            <div class="date-buttons-container" id="date-buttons-container">
                <!-- Date buttons will be dynamically added here -->
            </div>
            <div id="summary-display">
                <!-- Summary blocks will be displayed here -->
            </div>
        </div>
    </div>

    <!-- Script to parse Excel files -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>

    <script>
        // Global variables to hold the loaded data
        let institutionsData = [];
        let ordersData = [];
        let combinedData = [];

        // Helper function to find a column name by a list of keywords
        function findColumnName(headers, keywords) {
            for (const keyword of keywords) {
                const foundHeader = headers.find(h => String(h).trim().includes(keyword.trim()));
                if (foundHeader) return foundHeader;
            }
            return null;
        }

        // Helper function to check if a string is a valid date (in a simple format)
        function isDateString(str) {
            if (typeof str !== 'string') return false;
            // Updated regex to support DD/MM/YYYY format as well as YYYY-MM-DD
            const dateRegex = /^(\d{4}-\d{2}-\d{2})|(\d{1,2}\/\d{1,2}\/\d{4})$/;
            return dateRegex.test(str);
        }

        // Function to parse an Excel file
        function parseExcel(file) {
            return new Promise((resolve, reject) => {
                const reader = new FileReader();
                reader.onload = (e) => {
                    try {
                        const data = new Uint8Array(e.target.result);
                        const workbook = XLSX.read(data, { type: 'array' });
                        const sheetName = workbook.SheetNames[0];
                        const worksheet = workbook.Sheets[sheetName];
                        const json = XLSX.utils.sheet_to_json(worksheet, { header: 1 });
                        
                        if (json.length === 0) {
                            resolve([]);
                            return;
                        }
                        
                        const headers = json[0];
                        const rows = json.slice(1).map(row => {
                            const obj = {};
                            headers.forEach((header, i) => {
                                obj[header] = row[i];
                            });
                            return obj;
                        });
                        resolve(rows);
                    } catch (error) {
                        reject(error);
                    }
                };
                reader.onerror = (e) => reject(e);
                reader.readAsArrayBuffer(file);
            });
        }
        
        // Function to handle the file loading and processing
        async function handleFileLoad(file, dataType) {
            try {
                const data = await parseExcel(file);
                if (!data || data.length === 0) {
                     document.getElementById('message-area').textContent = 'שגיאה: הקובץ ריק או לא תקין.';
                     return;
                }
                
                const headers = Object.keys(data[0]);

                if (dataType === 'institutions') {
                    const idCol = findColumnName(headers, ['סמל מוסד', 'institutionId']);
                    const kashrutCol = findColumnName(headers, ['כשרות', 'kashrut', 'סוג כשרות']);

                    if (!idCol || !kashrutCol) {
                        document.getElementById('message-area').textContent = 'שגיאה: לא נמצאו עמודות "סמל מוסד" או "כשרות" בקובץ המוסדות.';
                        return;
                    }

                    institutionsData = data.map(item => ({
                        id: parseInt(item[idCol]),
                        kashrut: item[kashrutCol]
                    })).filter(item => !isNaN(item.id) && item.kashrut);
                    
                    document.getElementById('message-area').textContent = 'קובץ מוסדות נטען בהצלחה.';

                } else if (dataType === 'orders') {
                    const idCol = findColumnName(headers, ['סמל מוסד', 'institutionId']);
                    const mealTypeCol = findColumnName(headers, ['סוג מנה', 'mealType']);
                    const commentsCol = findColumnName(headers, ['הערות', 'comments']);
                    
                    if (!idCol || !mealTypeCol) {
                         document.getElementById('message-area').textContent = 'שגיאה: לא נמצאו אחת מהעמודות הנדרשות בקובץ ההזמנות (סמל מוסד, סוג מנה).';
                         return;
                    }

                    // Identify date columns dynamically
                    const dateColumns = headers.filter(h => isDateString(h));

                    if (dateColumns.length === 0) {
                        document.getElementById('message-area').textContent = 'שגיאה: לא נמצאו עמודות תאריך בקובץ ההזמנות.';
                        return;
                    }

                    ordersData = [];
                    data.forEach(row => {
                        const institutionId = parseInt(row[idCol]);
                        const mealType = String(row[mealTypeCol]);

                        if (isNaN(institutionId) || !mealType) {
                            return; // Skip invalid rows
                        }

                        dateColumns.forEach(dateCol => {
                            const quantity = parseInt(row[dateCol]);
                            if (!isNaN(quantity) && quantity > 0) {
                                ordersData.push({
                                    date: dateCol,
                                    institutionId: institutionId,
                                    mealType: mealType,
                                    comments: commentsCol ? String(row[commentsCol]) : '',
                                    quantity: quantity
                                });
                            }
                        });
                    });

                    document.getElementById('message-area').textContent = 'קובץ הזמנות נטען בהצלחה.';
                }

                if (institutionsData.length > 0 && ordersData.length > 0) {
                    processAndRenderData();
                    document.getElementById('main-content').style.display = 'block';
                    document.getElementById('message-area').textContent = 'כל הקבצים נטענו בהצלחה. המערכת מוכנה.';
                }
            } catch (error) {
                document.getElementById('message-area').textContent = 'שגיאה בטעינת הקובץ. אנא ודא שהקובץ תקין.';
                console.error("Error loading file:", error);
            }
        }
        
        // Function to process the data based on keywords
        function processAndRenderData() {
            const institutionsMap = new Map();
            institutionsData.forEach(inst => {
                institutionsMap.set(inst.id, String(inst.kashrut));
            });

            combinedData = ordersData.map(order => {
                const rawKashrut = institutionsMap.get(order.institutionId);
                let kashrut = 'בדץ';
                if (rawKashrut && rawKashrut.includes('חבד')) {
                    kashrut = 'חבד';
                }

                const mealType = String(order.mealType);
                let packaging = 'אריזה לא ידועה';
                let mealCategory = 'רגיל';

                // Check for allergens ONLY in the meal type column, using a more robust check for the word 'אלרגנ'
                if (mealType.includes('אלרגנ')) {
                    mealCategory = 'אלרגנית';
                } else if (mealType.includes('צמחוני')) {
                    mealCategory = 'צמחונית';
                }
                
                // Determine packaging type based on meal type
                if (mealType.includes('תפזורת')) {
                    packaging = 'תפזורת';
                } else if (mealType.includes('חמגשית')) {
                    packaging = 'חמגשית';
                }

                return {
                    date: order.date,
                    institutionId: order.institutionId,
                    kashrut: kashrut,
                    mealType: mealType,
                    mealCategory: mealCategory,
                    packaging: packaging,
                    quantity: order.quantity
                };
            });
            populateDateButtons();
        }

        // Function to populate the date buttons
        function populateDateButtons() {
            const dateButtonsContainer = document.getElementById('date-buttons-container');
            dateButtonsContainer.innerHTML = '';
            
            const dates = [...new Set(ordersData.map(order => order.date))];
            dates.sort();

            dates.forEach(date => {
                const button = document.createElement('button');
                button.textContent = date;
                button.className = 'styled-button';
                button.onclick = () => showDateSummary(date);
                dateButtonsContainer.appendChild(button);
            });
        }

        // Function to show the summary for a selected date
        function showDateSummary(date) {
            const summaryDisplay = document.getElementById('summary-display');
            summaryDisplay.innerHTML = ''; // Clear existing summary

            const dateData = combinedData.filter(item => item.date === date);

            const totals = {};
            let allergenicTotal = 0;
            const vegetarianTotals = {}; // Object to hold detailed vegetarian totals
            let grandTotal = 0; // New variable for the grand total

            dateData.forEach(item => {
                grandTotal += item.quantity; // Sum all quantities

                if (item.mealCategory === 'אלרגנית') {
                    allergenicTotal += item.quantity;
                } else if (item.mealCategory === 'צמחונית') {
                    // Store vegetarian totals by packaging type
                    if (!vegetarianTotals[item.packaging]) {
                        vegetarianTotals[item.packaging] = 0;
                    }
                    vegetarianTotals[item.packaging] += item.quantity;
                } else {
                    const kashrut = item.kashrut || 'לא ידוע';
                    const packaging = item.packaging;
                    
                    if (!totals[kashrut]) {
                        totals[kashrut] = {};
                    }
                    if (!totals[kashrut][packaging]) {
                        totals[kashrut][packaging] = 0;
                    }
                    totals[kashrut][packaging] += item.quantity;
                }
            });

            // Display a summary for the grand total
            const grandTotalSummaryBlock = document.createElement('div');
            grandTotalSummaryBlock.className = 'summary-block bg-blue-100';
            grandTotalSummaryBlock.innerHTML = `
                <h3 class="text-xl font-bold mb-2">סה"כ מנות ליום זה</h3>
                <div class="summary-item">
                    <span>סה"כ מכל הסוגים:</span>
                    <span class="font-extrabold">${grandTotal}</span>
                </div>
            `;
            summaryDisplay.appendChild(grandTotalSummaryBlock);

            // Display a summary for allergenic meals
            const allergenicSummaryBlock = document.createElement('div');
            allergenicSummaryBlock.className = 'summary-block';
            allergenicSummaryBlock.innerHTML = `
                <h3 class="text-xl font-semibold mb-2">סיכום מנות אלרגניות</h3>
                <div class="summary-item">
                    <span>סה"כ:</span>
                    <span>${allergenicTotal}</span>
                </div>
            `;
            summaryDisplay.appendChild(allergenicSummaryBlock);

            // Display a detailed summary for vegetarian meals
            const vegetarianSummaryBlock = document.createElement('div');
            vegetarianSummaryBlock.className = 'summary-block';
            vegetarianSummaryBlock.innerHTML = `
                <h3 class="text-xl font-semibold mb-2">סיכום מנות צמחוניות</h3>
            `;
            for (const packaging in vegetarianTotals) {
                const itemDiv = document.createElement('div');
                itemDiv.className = 'summary-item';
                itemDiv.innerHTML = `
                    <span>סה"כ ${packaging}:</span>
                    <span>${vegetarianTotals[packaging]}</span>
                `;
                vegetarianSummaryBlock.appendChild(itemDiv);
            }
            summaryDisplay.appendChild(vegetarianSummaryBlock);

            // Display summaries grouped by Kashrut
            for (const kashrut in totals) {
                const kashrutSummaryBlock = document.createElement('div');
                kashrutSummaryBlock.className = 'summary-block';
                kashrutSummaryBlock.innerHTML = `
                    <h3 class="text-xl font-semibold mb-2">סיכום עבור כשרות: ${kashrut}</h3>
                `;
                
                for (const packaging in totals[kashrut]) {
                    const itemDiv = document.createElement('div');
                    itemDiv.className = 'summary-item';
                    itemDiv.innerHTML = `
                        <span>סה"כ ${packaging}:</span>
                        <span>${totals[kashrut][packaging]}</span>
                    `;
                    kashrutSummaryBlock.appendChild(itemDiv);
                }
                summaryDisplay.appendChild(kashrutSummaryBlock);
            }
        }

        // Function to reset the entire tool
        function resetTool() {
            institutionsData = [];
            ordersData = [];
            combinedData = [];
            document.getElementById('message-area').textContent = 'הכלי אופס בהצלחה. אנא טען קבצים חדשים.';
            document.getElementById('date-buttons-container').innerHTML = '';
            document.getElementById('summary-display').innerHTML = '';
            document.getElementById('main-content').style.display = 'none';
        }

        // Event listeners for file inputs
        document.getElementById('institutions-file-input').addEventListener('change', (event) => {
            const file = event.target.files[0];
            if (file) handleFileLoad(file, 'institutions');
        });

        document.getElementById('orders-file-input').addEventListener('change', (event) => {
            const file = event.target.files[0];
            if (file) handleFileLoad(file, 'orders');
        });
    </script>
</body>
</html>
