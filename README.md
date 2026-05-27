# =====================================================
#  COLEGIO MUNDO DE RAYATI 
# Sistema Web Escolar con Flask
# Diseño Rosita + Registro Completo
# =====================================================

from flask import Flask, render_template_string, request

app = Flask(__name__)

# ==========================================
# LISTAS PARA GUARDAR DATOS
# ==========================================
alumnos = []
docentes = []
padres = []

# ==========================================
# HTML + CSS
# ==========================================
pagina = """

<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <title>Colegio Mundo de Rayati</title>

    <style>

        body{
            margin:0;
            padding:0;
            background: linear-gradient(to right,#ffd6e7,#ffeaf4);
            font-family: 'Comic Sans MS';
        }

        .contenedor{
            width:85%;
            margin:auto;
            margin-top:30px;
            background:white;
            padding:30px;
            border-radius:25px;
            box-shadow:0px 0px 20px pink;
        }

        h1{
            text-align:center;
            color:#ff1493;
            font-size:50px;
        }

        .subtitulo{
            text-align:center;
            color:#c71585;
            font-size:20px;
            margin-bottom:30px;
        }

        .tarjeta{
            background:#fff0f5;
            padding:20px;
            border-radius:20px;
            margin-top:25px;
            box-shadow:0px 0px 10px #ffb6c1;
        }

        h2{
            color:#db2d7a;
        }

        input{
            width:95%;
            padding:12px;
            margin-top:10px;
            border-radius:10px;
            border:2px solid pink;
            font-size:15px;
        }

        button{
            width:100%;
            margin-top:15px;
            padding:12px;
            border:none;
            border-radius:12px;
            background:#ff69b4;
            color:white;
            font-size:18px;
            cursor:pointer;
            transition:0.3s;
        }

        button:hover{
            background:#ff1493;
        }

        ul{
            color:#c2185b;
            font-size:17px;
        }

        .footer{
            text-align:center;
            margin-top:30px;
            color:#b03060;
            font-size:18px;
        }

    </style>

</head>

<body>

<div class="contenedor">

    <h1> Colegio Mundo de Rayati </h1>

   
    </div>

    <!-- ================================= -->
    <!-- REGISTRO DE ALUMNOS -->
    <!-- ================================= -->

    <div class="tarjeta">

        <h2> Registro de Alumnos</h2>

        <form method="POST">

            <input type="text"
                   name="nombre_alumno"
                   placeholder="Nombre del Alumno"
                   required>

            <input type="text"
                   name="edad"
                   placeholder="Edad"
                   required>

            <input type="text"
                   name="grado"
                   placeholder="Grado"
                   required>

            <button type="submit"
                    name="tipo"
                    value="alumno">

                Guardar Alumno

            </button>

        </form>

        <ul>

            {% for a in alumnos %}
                <li>{{a}}</li>
            {% endfor %}

        </ul>

    </div>

    <!-- ================================= -->
    <!-- REGISTRO DOCENTES -->
    <!-- ================================= -->

    <div class="tarjeta">

        <h2>Registro de Docentes</h2>

        <form method="POST">

            <input type="text"
                   name="nombre_docente"
                   placeholder="Nombre del Docente"
                   required>

            <input type="text"
                   name="curso"
                   placeholder="Curso"
                   required>

            <button type="submit"
                    name="tipo"
                    value="docente">

                Guardar Docente

            </button>

        </form>

        <ul>

            {% for d in docentes %}
                <li>{{d}}</li>
            {% endfor %}

        </ul>

    </div>

    <!-- ================================= -->
    <!-- REGISTRO PADRES -->
    <!-- ================================= -->

    <div class="tarjeta">

        <h2>Registro de Padres de Familia</h2>

        <form method="POST">

            <input type="text"
                   name="nombre_padre"
                   placeholder="Nombre del Padre o Madre"
                   required>

            <input type="text"
                   name="hijo"
                   placeholder="Nombre del Hijo(a)"
                   required>

            <button type="submit"
                    name="tipo"
                    value="padre">

                Guardar Padre

            </button>

        </form>

        <ul>

            {% for p in padres %}
                <li>{{p}}</li>
            {% endfor %}

        </ul>

    </div>

    <div class="footer">
        Plataforma Escolar - Mundo de Rayati 
    </div>

</div>

</body>
</html>

"""

# ==========================================
# FUNCION PRINCIPAL
# ==========================================
@app.route("/", methods=["GET", "POST"])

def inicio():

    if request.method == "POST":

        tipo = request.form["tipo"]

        # ==================================
        # ALUMNOS
        # ==================================

        if tipo == "alumno":

            nombre = request.form["nombre_alumno"]
            edad = request.form["edad"]
            grado = request.form["grado"]

            alumnos.append(
                f"Alumno: {nombre} | Edad: {edad} | Grado: {grado}"
            )

        # ==================================
        # DOCENTES
        # ==================================

        elif tipo == "docente":

            nombre = request.form["nombre_docente"]
            curso = request.form["curso"]

            docentes.append(
                f"Docente: {nombre} | Curso: {curso}"
            )

        # ==================================
        # PADRES
        # ==================================

        elif tipo == "padre":

            nombre = request.form["nombre_padre"]
            hijo = request.form["hijo"]

            padres.append(
                f"Padre/Madre: {nombre} | Hijo(a): {hijo}"
            )

    return render_template_string(
        pagina,
        alumnos=alumnos,
        docentes=docentes,
        padres=padres
    )

# ==========================================
# EJECUTAR SERVIDOR
# ==========================================
if __name__ == "__main__":
       app.run(host="0.0.0.0", port=8080)
