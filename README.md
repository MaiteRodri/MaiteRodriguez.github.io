
<!DOCTYPE html>

<html lang="es">
<head>
<meta charset="utf-8"/>
<meta content="width=device-width, initial-scale=1" name="viewport"/>
<title>Cuestionario de Apego Adulto</title>
<style>
        * { box-sizing: border-box; }
        body { font-family: Arial, sans-serif; padding: 20px; max-width: 800px; margin: auto; }
        h1 { text-align: center; }
        .question { margin-bottom: 10px; }
        label { font-size: 16px; }
        select { width: 100%; padding: 8px; font-size: 16px; margin-top: 4px; }
        button { width: 100%; padding: 12px; font-size: 18px; margin-top: 20px; }
        .result { margin-top: 20px; font-weight: bold; }
    
    .logo {
        display: block;
        max-width: 100%;
        height: auto;
        margin: 0 auto 20px auto;
    }
    </style>
</head>
<body>
<img alt="PsicoSalud Pamplona" class="logo" src="https://static.wixstatic.com/media/291ded_6598c5b25c82447c903f59b5d243f724~mv2.jpg/v1/fill/w_816,h_306,al_c/291ded_6598c5b25c82447c903f59b5d243f724~mv2.jpg"/><h1>Cuestionario de Apego Adulto (Melero y Cantero)</h1>
<form id="attachmentForm">
<div id="questions"></div>
<button onclick="calculateResult()" type="button">Calcular resultado</button>
</form>
<div class="result" id="result"></div>
<script>
        const questions = [
    { text: "1. Me preocupa que los demás no me quieran tanto como yo a ellos.", type: "ansiedad", reverse: false },
    { text: "2. Me preocupa que mis relaciones cercanas no duren para siempre.", type: "ansiedad", reverse: false },
    { text: "3. Me angustio cuando siento que alguien a quien quiero se va a alejar.", type: "ansiedad", reverse: false },
    { text: "4. Me preocupa que las personas que quiero encuentren a alguien mejor que yo.", type: "ansiedad", reverse: false },
    { text: "5. Me molesta mucho que me critiquen personas a las que quiero.", type: "ansiedad", reverse: false },
    { text: "6. Me preocupo frecuentemente por mis relaciones.", type: "ansiedad", reverse: false },
    { text: "7. Siento celos cuando mi pareja presta atención a otra persona.", type: "ansiedad", reverse: false },
    { text: "8. Me cuesta creer que alguien me quiera de verdad.", type: "ansiedad", reverse: false },
    { text: "9. Necesito muchas pruebas de que las personas a las que quiero me valoran.", type: "ansiedad", reverse: false },
    { text: "10. Siento que, a menudo, me quieren menos de lo que yo quiero a los demás.", type: "ansiedad", reverse: false },
    { text: "11. Tiendo a idealizar a las personas de las que me enamoro.", type: "ansiedad", reverse: false },
    { text: "12. Me inquieta que las personas con las que tengo una relación se alejen de mí.", type: "ansiedad", reverse: false },
    { text: "13. Me siento muy mal si alguien a quien quiero se enfada conmigo.", type: "ansiedad", reverse: false },
    { text: "14. Me angustio cuando no estoy cerca de las personas que me importan.", type: "ansiedad", reverse: false },
    { text: "15. Me siento incómodo si no sé qué piensan de mí las personas a las que quiero.", type: "ansiedad", reverse: false },
    { text: "16. Temo que las personas que me importan me abandonen.", type: "ansiedad", reverse: false },
    { text: "17. Necesito estar muy cerca de las personas que me importan.", type: "ansiedad", reverse: false },
    { text: "18. Temo que si me acerco demasiado a alguien, esa persona no me quiera tanto como yo a ella.", type: "ansiedad", reverse: false },
    { text: "19. Me siento incómodo si alguien se me acerca demasiado emocionalmente.", type: "evitacion", reverse: false },
    { text: "20. Me resulta fácil acercarme emocionalmente a los demás.", type: "evitacion", reverse: true },
    { text: "21. Me cuesta mucho expresar mis sentimientos a los demás.", type: "evitacion", reverse: false },
    { text: "22. Me resulta difícil confiar plenamente en los demás.", type: "evitacion", reverse: false },
    { text: "23. Prefiero no depender de nadie.", type: "evitacion", reverse: false },
    { text: "24. Evito mostrarme vulnerable con los demás.", type: "evitacion", reverse: false },
    { text: "25. Prefiero mantener cierta distancia en mis relaciones íntimas.", type: "evitacion", reverse: false },
    { text: "26. Me siento incómodo si alguien espera que le cuente cosas íntimas sobre mí.", type: "evitacion", reverse: false },
    { text: "27. Me cuesta compartir mis pensamientos y sentimientos con otros.", type: "evitacion", reverse: false },
    { text: "28. Me molesta que los demás se me acerquen demasiado.", type: "evitacion", reverse: false },
    { text: "29. Prefiero resolver mis problemas solo.", type: "evitacion", reverse: false },
    { text: "30. No me gusta que los demás vean mis debilidades.", type: "evitacion", reverse: false },
    { text: "31. Me siento incómodo si tengo que depender de alguien.", type: "evitacion", reverse: false },
    { text: "32. Evito implicarme demasiado emocionalmente con los demás.", type: "evitacion", reverse: false },
    { text: "33. Me siento cómodo compartiendo mis pensamientos y sentimientos con otros.", type: "evitacion", reverse: true },
    { text: "34. Me resulta difícil pedir ayuda incluso cuando la necesito.", type: "evitacion", reverse: false },
    { text: "35. Prefiero mantener mi independencia en todas las circunstancias.", type: "evitacion", reverse: false },
    { text: "36. Me cuesta aceptar el apoyo de los demás.", type: "evitacion", reverse: false },
    { text: "37. Evito pensar en lo que siento en mis relaciones.", type: "evitacion", reverse: false },
    { text: "38. No necesito a nadie para sentirme completo.", type: "evitacion", reverse: false },
    { text: "39. Me resulta fácil confiar en los demás.", type: "evitacion", reverse: true },
    { text: "40. Me resulta difícil expresar mis necesidades emocionales.", type: "evitacion", reverse: false }
];

        const container = document.getElementById("questions");
        questions.forEach((q, i) => {
            const div = document.createElement("div");
            div.className = "question";
            div.innerHTML = `<label>${q.text}</label><br>
                <select name="q${i}" required>
                    <option value="">Seleccione</option>
                    <option value="1">1 - Totalmente en desacuerdo</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                    <option value="5">5 - Totalmente de acuerdo</option>
                </select>`;
            container.appendChild(div);
        });

        function calculateResult() {
            const form = document.forms["attachmentForm"];
            let ansiedadTotal = 0, evitacionTotal = 0;
            let ansiedadCount = 0, evitacionCount = 0;

            questions.forEach((q, i) => {
                const value = parseInt(form[`q${i}`].value);
                if (isNaN(value)) return;

                const score = q.reverse ? 6 - value : value;

                if (q.type === "ansiedad") {
                    ansiedadTotal += score;
                    ansiedadCount++;
                } else {
                    evitacionTotal += score;
                    evitacionCount++;
                }
            });

            const ansiedadAvg = ansiedadTotal / ansiedadCount;
            const evitacionAvg = evitacionTotal / evitacionCount;

            let apego = "";
            if (ansiedadAvg < 3 && evitacionAvg < 3)
                apego = "Seguro (baja ansiedad, baja evitación)";
            else if (ansiedadAvg >= 3 && evitacionAvg < 3)
                apego = "Ansioso-preocupado (alta ansiedad, baja evitación)";
            else if (ansiedadAvg < 3 && evitacionAvg >= 3)
                apego = "Evitativo (baja ansiedad, alta evitación)";
            else
                apego = "Temeroso-desorganizado (alta ansiedad, alta evitación)";

            document.getElementById("result").innerHTML =
                `Puntaje Ansiedad: ${ansiedadAvg.toFixed(2)}<br>
                 Puntaje Evitación: ${evitacionAvg.toFixed(2)}<br>
                 Tipo de Apego: <strong>${apego}</strong>`;
        }
    </script>
</body>
</html>
