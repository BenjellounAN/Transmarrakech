<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Reservation Form</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }

        .header {
            background-color: #333;
            padding: 20px;
            text-align: center;
            color: #fff;
        }

        .header h1 {
            margin: 0;
            font-size: 36px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .container {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            padding: 20px;
        }

        .reservation-form {
            background-color: #fff;
            border-radius: 8px;
            padding: 30px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 500px;
        }

        h1 {
            text-align: center;
            font-size: 24px;
            margin-bottom: 20px;
            color: #333;
        }

        .form-group {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            padding: 10px;
            background-color: #f7f7f7;
        }

        .form-group label i {
            font-size: 18px;
            color: #555;
            margin-right: 10px;
        }

        .form-group input,
        .form-group select {
            border: none;
            background: none;
            outline: none;
            flex: 1;
            font-size: 14px;
        }

        .form-group label {
            font-weight: bold;
            margin-bottom: 5px;
        }

        .submit-btn {
            width: 100%;
            background-color: #c4a251;
            color: #fff;
            font-size: 16px;
            padding: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            text-transform: uppercase;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .submit-btn:hover {
            background-color: #b49446;
        }

        .submit-btn i {
            margin-right: 8px;
            font-size: 16px;
        }

        .success-message {
            display: none;
            text-align: center;
            background-color: #d4edda;
            color: #155724;
            padding: 10px;
            border: 1px solid #c3e6cb;
            border-radius: 5px;
            margin-top: 20px;
            font-size: 14px;
        }

    </style>
</head>
<body>
    <div class="header">
        <h1>Online Reservation</h1>
    </div>

    <div class="container">
        <div class="reservation-form">
            <h1>BOOK NOW</h1>
            <form id="reservation-form">
                <div class="form-group">
                    <label for="name"><i class="fa-solid fa-user"></i></label>
                    <input type="text" id="name" placeholder="Your Name" required>
                </div>
                <div class="form-group">
                    <label for="trip-type"><i class="fa-solid fa-arrows-rotate"></i></label>
                    <select id="trip-type" required>
                        <option value="one-way">One-Way</option>
                        <option value="round-trip">Round-Trip</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="from"><i class="fa-solid fa-location-dot"></i></label>
                    <input type="text" id="from" placeholder="Marrakech Airport RAK" required>
                </div>
                <div class="form-group">
                    <label for="to"><i class="fa-solid fa-location-dot"></i></label>
                    <input type="text" id="to" placeholder="Essaouira" required>
                </div>
                <div class="form-group">
                    <label for="date"><i class="fa-solid fa-calendar-days"></i></label>
                    <input type="date" id="date" required>
                </div>
                <div class="form-group">
                    <label for="time"><i class="fa-solid fa-clock"></i></label>
                    <input type="time" id="time" required>
                </div>
                <div id="return-fields"></div>

                <div class="form-group">
                    <label for="phone"><i class="fa-solid fa-phone"></i></label>
                    <input type="tel" id="phone" placeholder="Your Phone Number" required>
                </div>

                <div class="form-group">
                    <label for="people"><i class="fa-solid fa-user-group"></i></label>
                    <select id="people" required>
                        <option value="1">1 Person</option>
                        <option value="2">2 People</option>
                        <option value="3">3 People</option>
                        <option value="4">4 People</option>
                        <option value="5">+5 People</option>
                    </select>
                </div>

                <div class="form-group">
                    <label for="bags"><i class="fa-solid fa-suitcase"></i></label>
                    <select id="bags" required>
                        <option value="1">1 Bag</option>
                        <option value="2">2 Bags</option>
                        <option value="3">3 Bags</option>
                        <option value="4">4 Bags</option>
                        <option value="5">+5 Bags</option>
                    </select>
                </div>

                <button type="submit" class="submit-btn">
                    <i class="fa-solid fa-check"></i>FINISH YOUR BOOKING 
                </button>
            </form>
            <div class="success-message" id="success-message">
                Booking confirmed ✅. Our team will message you on WhatsApp soon.
            </div>
        </div>
    </div>

    <script>
        const tripType = document.getElementById('trip-type');
        const returnFields = document.getElementById('return-fields');
        const form = document.getElementById('reservation-form');
        const successMessage = document.getElementById('success-message');

        tripType.addEventListener('change', function () {
            if (tripType.value === 'round-trip') {
                returnFields.innerHTML = `
                    <div class="form-group">
                        <label for="return-date"><strong>Return Date</strong></label>
                        <input type="date" id="return-date" placeholder="Return Date" required>
                    </div>
                    <div class="form-group">
                        <label for="return-time"><i class="fa-solid fa-clock"></i></label>
                        <input type="time" id="return-time" placeholder="Return Time" required>
                    </div>
                `;
            } else {
                returnFields.innerHTML = '';
            }
        });

        form.addEventListener('submit', function (e) {
            e.preventDefault();
            const name = document.getElementById('name').value;
            const tripType = document.getElementById('trip-type').value;
            const from = document.getElementById('from').value;
            const to = document.getElementById('to').value;
            const date = document.getElementById('date').value;
            const time = document.getElementById('time').value;
            const phone = document.getElementById('phone').value;
            const people = document.getElementById('people').value;
            const bags = document.getElementById('bags').value;

            let message = `Reservation Details:\n`;
            message += `Name: ${name}\n`;
            message += `Trip Type: ${tripType === 'one-way' ? 'One-Way' : 'Round-Trip'}\n`;
            message += `From: ${from}\n`;
            message += `To: ${to}\n`;
            message += `Departure Date: ${date}\n`;
            message += `Departure Time: ${time}\n`;
            if (tripType === 'round-trip') {
                const returnDate = document.getElementById('return-date').value;
                const returnTime = document.getElementById('return-time').value;
                message += `Return Date: ${returnDate}\n`;
                message += `Return Time: ${returnTime}\n`;
            }
            message += `Phone: ${phone}\n`;
            message += `People: ${people}\n`;
            message += `Bags: ${bags}\n`;

            const whatsappNumber = "212709191563";
            const whatsappLink = `https://wa.me/${whatsappNumber}?text=${encodeURIComponent(message)}`;

            window.open(whatsappLink, '_blank');

            successMessage.style.display = 'block';
        });
    </script>
</body>
</html>
