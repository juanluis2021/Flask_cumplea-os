# Flask_cumplea-os
#El método "POST" se utiliza para agregar nuevas entradas a la base de datos cuando
##se envía un formulario, mientras que el método "GET" 
##se utiliza para mostrar las entradas existentes en la base de datos cuando se accede a la ruta inicial.


import sqlite3
import os
from flask import Flask, flash, jsonify, redirect, render_template, request, session

app = Flask(__name__)
app.config["TEMPLATES_AUTO_RELOAD"] = True

from cs50 import SQL
import sqlite3
from flask import Flask, redirect, render_template, request

app = Flask(__name__)

try:
    conn = sqlite3.connect("env/birthdays/birthdays")
    db = conn.cursor()
    print("Conexión exitosa a la base de datos")
except sqlite3.Error as e:
    print("Error al conectar a la base de datos:", str(e))

@app.route("/", methods=["GET", "POST"])
def index():
    if request.method == "POST":
        id = request.form.get("id")
        name = request.form.get("name")
        month = request.form.get("month")
        day = request.form.get("day")

        db.execute("INSERT INTO birthdays (id, name, month, day) VALUES (?, ?, ?, ?)",  (id, name, month, day))
                 
        conn.commit()

        return redirect("/")

    elif request.method == "GET":
        id = request.args.get("id")
        if id:
            db.execute("DELETE FROM birthdays WHERE id = ?", (id,))
            conn.commit()

        entries = db.execute("SELECT * FROM birthdays").fetchall()
        return render_template("index.html", entries=entries)

if __name__ == '__main__':
    app.run(debug=True)

#SQLITE3

import sqlite3
try:
    mi_conexion = sqlite3.connect("env/birthdays/birthdays")  ##conexion a la base de datos 
    cursor = mi_conexion.cursor()
    cursor.execute("""CREATE TABLE birthdays (id number, name varchar(50), month number, day number)""")
    mi_conexion  = sqlite3.connect("birthdays")
    add_datos = [("1","alfonso","12","23")]
    cursor.executemany("insert into birthdays values ( ?,?,?,?)",add_datos)
    mi_conexion.commit()
    mi_conexion.close()


    cursor =mi_conexion.cursor()
    cursor.execute("select * from birthdays")
    rows= cursor.fetchall()
    for row in rows:
       print("bien")
       print(row)

    ##mi_conexion.commit()
    ##mi_conexion.close()
##except Exception as ex:
    ##print(ex)
except sqlite3.Error as ex:
   print("Error occurred while accessing the database:", ex)
   
##finally:
   ## if db:
      ##  db.close()


#HTML

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>cumpleaños</title>
</head>
<body>
    
    <form action="/" method="POST">
        <input name="id" placeholder="id" type="number" min="1" max="2000">
        <input name="name" placeholder="Name" type="text">
        <input name="month" placeholder="Month" type="number" min="1" max="12">
        <input name="day" placeholder="Day" type="number" min="1" max="31">
        <input type="submit" value="Add Birthday">
    </form>


    <form action="/" method="GET">
        <input type="hidden" name="_method" value="DELETE">
        <input name="id" placeholder="id" type="number" min="1" max="2000">
        <input type="submit" value="Borrar registro ">
    </form>


</body>




3
