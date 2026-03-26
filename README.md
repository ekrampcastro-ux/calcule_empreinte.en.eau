
<html>
<head>
    <title>Calculateur d'empreinte eau</title>
    <meta charset="utf-8">
    <style>
        body {
            font-family: Arial;
            background: #e3f2fd;
            text-align: center;
        }

        h1 { color: #0d47a1; }

        .box {
            background: white;
            padding: 20px;
            margin: 20px auto;
            width: 320px;
            border-radius: 15px;
        }

        input { margin: 5px; }

        button {
            padding: 10px;
            background: #1565c0;
            color: white;
            border: none;
            border-radius: 10px;
            cursor: pointer;
        }

        #result { margin-top: 20px; font-size: 18px; }
    </style>
</head>

<body>

<h1>💧 Calcule ta consommation d’eau réelle</h1>

<div class="box">

🚿 Douche (min/jour) :<br>
<input type="number" id="douche" min="0" value="10"><br>

🛁 Bain (par semaine) :<br>
<input type="number" id="bain" min="0" value="0"><br>

🚽 Toilettes (fois/jour) :<br>
<input type="number" id="toilette" min="0" value="5"><br>

🍽️ Lave-vaisselle (fois/semaine) :<br>
<input type="number" id="vaisselle" min="0" value="4"><br>

👕 Machine à laver (semaine) :<br>
<input type="number" id="linge" min="0" value="3"><br>

🌱 Arrosage (min/jour) :<br>
<input type="number" id="jardin" min="0" value="5"><br>

🍔 Fast-food / repas industriel (par semaine) :<br>
<input type="number" id="fastfood" min="0" value="2"><br>

🍳 Repas maison (par jour) :<br>
<input type="number" id="cuisine" min="0" value="2"><br>

🥤 Verres d’eau / jour :<br>
<input type="number" id="boisson" min="0" value="5"><br>

📺 Écran (h/jour) :<br>
<input type="number" id="ecran" min="0" value="3"><br>

🤖 IA / recherches (requêtes/jour) :<br>
<input type="number" id="ia" min="0" value="10"><br><br>

<button onclick="calculer()">Calculer</button>

<div id="result"></div>

</div>

<script>
function calculer() {

    function val(id){
        return Math.max(0, Number(document.getElementById(id).value) || 0);
    }

    var douche = val("douche");
    var bain = val("bain");
    var toilette = val("toilette");
    var vaisselle = val("vaisselle");
    var linge = val("linge");
    var jardin = val("jardin");
    var cuisine = val("cuisine");
    var boisson = val("boisson");
	var fastfood = val("fastfood");
    var ecran = val("ecran");
    var ia = val("ia");

    // ordres de grandeur réalistes
    var eauDouche = douche * 10;
    var eauBain = bain * 150 / 7;
    var eauToilette = toilette * 6;
    var eauVaisselle = vaisselle * 12 / 7;
    var eauLinge = linge * 50 / 7;
    var eauJardin = jardin * 15;
    var eauCuisine = cuisine * 8;
    var eauBoisson = boisson * 0.25;
	var eauFastFood = fastfood * 9;
    var eauEcran = ecran * 3;
    var eauIA = ia * 2; // estimation eau IA

    var total = Math.round(
        eauDouche + eauBain + eauToilette + eauVaisselle +
        eauLinge + eauJardin + eauCuisine +
        eauBoisson + eauEcran + eauIA+ eauFastFood
    );

    var message = "";
    if (total > 3000) message = "⚠️ Ta consommation est très élevée, principalement à cause des usages indirects comme la viande, le fast-food et le mode de vie quotidien, qui demandent énormément d’eau sans que tu t’en rendes compte.";
    else if (total > 1500) message = "😬 Ta consommation est élevée, principalement à cause des usages indirects comme la viande, le fast-food et les activités quotidiennes gourmandes en eau.";
	 else if (total > 600) message = " Ta consommation est modérée mais peut être réduite, notamment en limitant certains usages comme l’alimentation industrielle ou le temps d’eau utilisé.";
    else message = "👍 Ta consommation est maîtrisée, mais une grande partie reste invisible, notamment liée à l’alimentation et au mode de vie.";

    document.getElementById("result").innerHTML =
        "💧 <b>" + total + " L/jour</b><br>" + message +
        "<br><br>🤖 Même l’IA et les écrans consomme de l’eau (refroidissement des serveurs)";
}
</script>

</body>
</html>
