<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LifeDrop - Blood Donation Network</title>
    <style>
        :root {
            --primary-color: #e63946;
            --primary-hover: #c1121f;
            --bg-color: #f8f9fa;
            --card-bg: #ffffff;
            --text-color: #212529;
            --border-color: #dee2e6;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 0;
            line-height: 1.6;
        }

        header {
            background-color: var(--primary-color);
            color: white;
            padding: 40px 20px;
            text-align: center;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        header h1 {
            margin: 0;
            font-size: 2.5rem;
        }

        header p {
            margin: 10px 0 0 0;
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .container {
            max-width: 1000px;
            margin: 40px auto;
            padding: 0 20px;
            display: grid;
            grid-template-columns: 1fr;
            gap: 30px;
        }

        @media (min-width: 768px) {
            .container {
                grid-template-columns: 1.2fr 0.8fr;
            }
        }

        .card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 30px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            border: 1px solid var(--border-color);
        }

        .card h2 {
            margin-top: 0;
            color: var(--primary-color);
            border-bottom: 2px solid #f1faee;
            padding-bottom: 10px;
        }

        /* Form Styling */
        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
        }

        input, select, textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            box-sizing: border-box;
            font-size: 16px;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: var(--primary-color);
        }

        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 14px 20px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 6px;
            cursor: pointer;
            width: 100%;
            transition: background 0.2s;
        }

        button:hover {
            background-color: var(--primary-hover);
        }

        /* Stock Indicator Styling */
        .stock-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
            margin-top: 20px;
        }

        .stock-item {
            background: #fff5f5;
            border: 1px solid #ffa3a3;
            border-radius: 8px;
            text-align: center;
            padding: 15px 5px;
        }

        .blood-type {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--primary-color);
            display: block;
        }

        .stock-level {
            font-size: 0.85rem;
            color: #6c757d;
        }

        /* Quick Actions */
        .quick-actions a {
            display: block;
            text-align: center;
            background: #212529;
            color: white;
            text-decoration: none;
            padding: 12px;
            border-radius: 6px;
            font-weight: bold;
            margin-top: 15px;
            transition: background 0.2s;
        }

        .quick-actions a:hover {
            background: #000000;
        }

        .success-msg {
            display: none;
            background-color: #d4edda;
            color: #155724;
            padding: 15px;
            border-radius: 6px;
            margin-bottom: 20px;
            text-align: center;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <header>
        <h1>LifeDrop</h1>
        <p>A drop of blood can save a life. Request blood or find a donor today.</p>
    </header>

    <div class="container">
        
        <div class="card">
            <h2>Urgent Blood Request Form</h2>
            
            <div class="success-msg" id="success-message">
                🎉 Request Submitted! Local donors are being notified.
            </div>

            <form id="requestForm" onsubmit="handleRequest(event)">
                <div class="form-group">
                    <label for="patientName">Patient Name</label>
                    <input type="text" id="patientName" required placeholder="Enter patient full name">
                </div>

                <div class="form-group">
                    <label for="bloodGroup">Required Blood Type</label>
                    <select id="bloodGroup" required>
                        <option value="">-- Select Blood Type --</option>
                        <option value="A+">A+</option>
                        <option value="A-">A-</option>
                        <option value="B+">B+</option>
                        <option value="B-">B-</option>
                        <option value="AB+">AB+</option>
                        <option value="AB-">AB-</option>
                        <option value="O+">O+</option>
                        <option value="O-">O-</option>
                    </select>
                </div>

                <div class="form-group">
                    <label for="hospital">Hospital Name & Location</label>
                    <input type="text" id="hospital" required placeholder="City Hospital, Room 402">
                </div>

                <div class="form-group">
                    <label for="contact">Contact Number</label>
                    <input type="tel" id="contact" required placeholder="Enter phone number">
                </div>

                <button type="submit">Post Urgent Request</button>
            </form>
        </div>

        <div>
            <div class="card" style="margin-bottom: 30px;">
                <h2>Live Inventory Status</h2>
                <p style="font-size: 0.9rem; color: #6c757d; margin-top: -10px;">Simulated real-time blood bank availability:</p>
                
                <div class="stock-grid">
                    <div class="stock-item"><span class="blood-type">O+</span><span class="stock-level">Normal</span></div>
                    <div class="stock-item" style="background: #fff0f1; border-color: #ff4d4d;"><span class="blood-type" style="color: #ff4d4d;">O-</span><span class="stock-level" style="color: #ff4d4d; font-weight: bold;">CRITICAL</span></div>
                    <div class="stock-item"><span class="blood-type">A+</span><span class="stock-level">Normal</span></div>
                    <div class="stock-item"><span class="blood-type">B+</span><span class="stock-level">Low</span></div>
                    <div class="stock-item"><span class="blood-type">AB+</span><span class="stock-level">Normal</span></div>
                    <div class="stock-item"><span class="blood-type">A-</span><span class="stock-level">Low</span></div>
                    <div class="stock-item"><span class="blood-type">B-</span><span class="stock-level">Normal</span></div>
                    <div class="stock-item"><span class="blood-type">AB-</span><span class="stock-level">Low</span></div>
                </div>
            </div>

            <div class="card quick-actions">
                <h2>Quick Resources</h2>
                <p style="font-size: 0.9rem; color: #6c757d; margin-top: -10px;">Find physical help near you immediately.</p>
                
                <a href="https://www.google.com/maps/search/blood+bank+near+me/" target="_blank">📍 Find Nearest Blood Bank</a>
                <a href="https://www.google.com/maps/search/hospitals+near+me/" target="_blank">🏥 Find Nearby Hospitals</a>
            </div>
        </div>

    </div>

    <script>
        function handleRequest(event) {
            event.preventDefault(); // Prevents the page from refreshing
            
            // Show the success alert banner
            const successMsg = document.getElementById('success-message');
            successMsg.style.display = 'block';
            
            // Clear the form fields
            document.getElementById('requestForm').reset();
            
            // Smooth scroll to top of card to see message
            successMsg.scrollIntoView({ behavior: 'smooth', block: 'center' });
        }
    </script>
</body>
</html>
