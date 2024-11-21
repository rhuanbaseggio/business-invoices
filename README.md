# business-invoices
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Business Estimates & Invoices</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f9;
        }
        .container {
            width: 80%;
            margin: auto;
            padding: 20px;
            background: white;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .form-group {
            margin: 15px 0;
        }
        input, select, button {
            padding: 10px;
            width: 100%;
            margin-top: 5px;
            box-sizing: border-box;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        th, td {
            padding: 10px;
            border: 1px solid #ddd;
            text-align: left;
        }
        .total {
            text-align: right;
            font-size: 1.2em;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Business Estimates & Invoices</h1>
        <form id="invoice-form">
            <div class="form-group">
                <label for="client-name">Client Name:</label>
                <input type="text" id="client-name" placeholder="Enter client name" required>
            </div>
            <div class="form-group">
                <label for="client-email">Client Email:</label>
                <input type="email" id="client-email" placeholder="Enter client email" required>
            </div>
            <div class="form-group">
                <label for="item-description">Item Description:</label>
                <input type="text" id="item-description" placeholder="Enter item description" required>
            </div>
            <div class="form-group">
                <label for="item-quantity">Quantity:</label>
                <input type="number" id="item-quantity" min="1" placeholder="Enter quantity" required>
            </div>
            <div class="form-group">
                <label for="item-price">Unit Price:</label>
                <input type="number" id="item-price" min="0.01" step="0.01" placeholder="Enter unit price" required>
            </div>
            <button type="button" onclick="generateInvoice()">Generate Invoice</button>
        </form>
        <table id="invoice-table">
            <thead>
                <tr>
                    <th>Item</th>
                    <th>Description</th>
                    <th>Quantity</th>
                    <th>Price</th>
                    <th>Total</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>
        <div class="total" id="invoice-total">Total: $0.00</div>
    </div>
    <script>
        const invoiceTable = document.getElementById('invoice-table').querySelector('tbody');
        const invoiceTotal = document.getElementById('invoice-total');

        function generateInvoice() {
            const clientName = document.getElementById('client-name').value;
            const clientEmail = document.getElementById('client-email').value;
            const itemDescription = document.getElementById('item-description').value;
            const itemQuantity = parseInt(document.getElementById('item-quantity').value);
            const itemPrice = parseFloat(document.getElementById('item-price').value);

            if (!clientName || !clientEmail || !itemDescription || !itemQuantity || !itemPrice) {
                alert('Please fill out all fields.');
                return;
            }

            const itemTotal = itemQuantity * itemPrice;
            const row = `<tr>
                            <td>${itemDescription}</td>
                            <td>${clientName}</td>
                            <td>${itemQuantity}</td>
                            <td>$${itemPrice.toFixed(2)}</td>
                            <td>$${itemTotal.toFixed(2)}</td>
                        </tr>`;
            invoiceTable.innerHTML += row;

            const currentTotal = parseFloat(invoiceTotal.textContent.replace('Total: $', '')) || 0;
            invoiceTotal.textContent = `Total: $${(currentTotal + itemTotal).toFixed(2)}`;
        }
    </script>
</body>
</html>
