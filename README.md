<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Caisse Enregistreuse El vino</title>
    
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #0bb1a8;
        }

        img {
            width: 100px;
            height: 100px;
        }

        header {
            background-color: #0bb1a8;
            color: #fff;
            text-align: center;
            padding: 1em;
        }

        section {
            display: flex;
            flex-wrap: wrap; 
            justify-content: space-around;
            padding: 2em;
        }

        #products, #cart {
            width: 100%; 
            margin-bottom: 1em; 
        }

        #products, #cart, #receipt {
            background-color: #fff;
            padding: 1em;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        button:hover {
            background-color: red;
            font-size: 30px;
            transition: 2s;
        }

        button {
            width: 100%; /* Sur les petits écrans, occuper la largeur complète */
            padding: 10px;
            margin-top: 5px;
            background-color: #000000;
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        @media screen and (min-width: 768px) {
            
            #products {
                width: 60%;
            }

            #cart {
                width: 35%;
            }
        }
    </style>
</head>
<body>

    <header>
        <h1>Caisse Enregistreuse</h1> 
        <img src="EL VI.png" >
    </header>

    <section>
        <div id="products">
                <li>Chenet Ice - 5000 XOF <button onclick="addToCart('Chenet Ice', 5000)">Ajouter</button></li>
                <li>Bagatelle BLC - 5000 XOF <button onclick="addToCart('Bagatelle BLC', 5000)">Ajouter</button></li>
                <li>Bagatelle rose - 6000 XOF <button onclick="addToCart('Bagatelle rose', 6000)">Ajouter</button></li>
                <li>Pavillon reine - 4000 XOF <button onclick="addToCart('Pavillon reine', 4000)">Ajouter</button></li>
                <li>Baudeville BLC - 5500 XOF <button onclick="addToCart('Baudeville BLC', 5500)">Ajouter</button></li>
                <li>Baudeville rouge - 5500 XOF <button onclick="addToCart('Baudeville rouge', 5500)">Ajouter</button></li>
                <li>Poulma BLC - 5500 XOF <button onclick="addToCart('Poulma BLC', 5500)">Ajouter</button></li>
                <li>Probus - 3500 XOF <button onclick="addToCart('Probus', 3500)">Ajouter</button></li>
                <li>Le Lys rouge - 4000 XOF <button onclick="addToCart('Le Lys rouge', 4000)">Ajouter</button></li>
                <li>Carillonade Bordeaux - 5000 XOF <button onclick="addToCart('Carillonade Bordeaux', 5000)">Ajouter</button></li>
                <li>Carillonade Cabernet - 5000 XOF <button onclick="addToCart('Carillonade Cabernet', 5000)">Ajouter</button></li>
                <li>Carillonade Merlot - 5000 XOF <button onclick="addToCart('Carillonade Merlot', 5000)">Ajouter</button></li>
                <li>Roche Mazet Merlot - 6000 XOF <button onclick="addToCart('Roche Mazet Merlot', 6000)">Ajouter</button></li>
                <li>Roche mazet cab - 6000 XOF <button onclick="addToCart('Roche mazet cab', 6000)">Ajouter</button></li>
                <li>RLG’ - 3000 XOF - <button onclick="addToCart('RLG’', 3000)">Ajouter</button></li>
                <li>Chemin des Papes - 6500 XOF <button onclick="addToCart('Chemin des Papes', 6500)">Ajouter</button></li>
                <li>Pte vendange - 2500 XOF <button onclick="addToCart('Pte vendange', 2500)">Ajouter</button></li>
                <li>Green Lee R 1L - 5000 XOF <button onclick="addToCart('Green Lee R 1L', 5000)">Ajouter</button></li>
                <li>RLG Mouelleux - 3000 XOF <button onclick="addToCart('RLG Mouelleux ' , 3000)">Ajouter</button></li>
        </div>

        <h2>Panier</h2>
        <ul id="cart-items"></ul>
        <p>Total: <span id="total">0</span> XOF</p>
        <button onclick="checkout()">Payer</button>
    </div>
</section>

<div id="receipt"></div>

<script>
    let cartItems = [];
    let total = 0;

    function addToCart(item, price) {
        cartItems.push({ item, price });
        total += price;
        updateCart();
    }

    function updateCart() {
        const cartList = document.getElementById('cart-items');
        const totalElement = document.getElementById('total');
        
        cartList.innerHTML = "";
        cartItems.forEach(cartItem => {
            const li = document.createElement('li');
            li.textContent = `${cartItem.item} - ${cartItem.price} XOF`;
            cartList.appendChild(li);
        });

        totalElement.textContent = total;
    }

    function checkout() {
        const receipt = document.getElementById('receipt');
        
        if (cartItems.length === 0) {
            alert('Le panier est vide. Veuillez ajoutez des articles avant de payer merci.');
            return;
        }

        const timestamp = new Date().toLocaleString();
        const receiptContent = `
            <h2>Reçu - ${timestamp}</h2>
            <ul>${getReceiptItems()}</ul>
            <p>Total: ${total} XOF</p>
        `;
        receipt.innerHTML = receiptContent;

        // Enregistrez la transaction dans l'historique ici
        // Vous pouvez stocker ces informations côté serveur dans une base de données

        alert(`Paiement de ${total} XOF effectué avec succès! Merci à bientôt El vino`);

        // Réinitialisez le panier et le total
        cartItems = [];
        total = 0;
        updateCart();
    }

    function getReceiptItems() {
        return cartItems.map(cartItem => `<li>${cartItem.item} - ${cartItem.price} XOF</li>`).join('');
    }
</script>

</body>
</html>
