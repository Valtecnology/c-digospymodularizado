```
# c-digospymodularizado
from models import Participante, Disciplina, Evento, Encuentro
from database import connect_db, create_tables
from relations import define_relations
from utils import insert_sample_data, validate_data



codigospyproyectomultideportivo

class Participante:
    def __init__(self, id, nombre, apellido, edad, genero, disciplina):
        self.id = id
        self.nombre = nombre
        self.apellido = apellido
        self.edad = edad
        self.genero = genero
        self.disciplina = disciplina

class Disciplina:
    def __init__(self, id, nombre, descripcion):
        self.id = id
        self.nombre = nombre
        self.descripcion = descripcion

class Evento:
    def __init__(self, id, nombre, fecha_inicio, fecha_fin):
        self.id = id
        self.nombre = nombre
        self.fecha_inicio = fecha_inicio
        self.fecha_fin = fecha_fin

class Encuentro:
    def __init__(self, id, fecha, hora):
        self.id = id
        self.fecha = fecha
        self.hora = hora


def main():
    db = connect_db()
    create_tables(db)
    define_relations(db)
    insert_sample_data(db)
    # Lógica principal de la aplicación
    print("Aplicación iniciada correctamente")

if __name__ == "__main__":
    main()

import sqlite3

def connect_db():
    return sqlite3.connect('database.db')

def create_tables(db):
    cursor = db.cursor()
    
    cursor.execute('''CREATE TABLE IF NOT EXISTS Participante (
                        id INTEGER PRIMARY KEY,
                        nombre TEXT,
                        apellido TEXT,
                        edad INTEGER,
                        genero TEXT,
                        disciplina TEXT)''')
    
    cursor.execute('''CREATE TABLE IF NOT EXISTS Disciplina (
                        id INTEGER PRIMARY KEY,
                        nombre TEXT,
                        descripcion TEXT)''')
    
    cursor.execute('''CREATE TABLE IF NOT EXISTS Evento (
                        id INTEGER PRIMARY KEY,
                        nombre TEXT,
                        fecha_inicio TEXT,
                        fecha_fin TEXT)''')
    
    cursor.execute('''CREATE TABLE IF NOT EXISTS Encuentro (
                        id INTEGER PRIMARY KEY,
                        fecha TEXT,
                        hora TEXT)''')
    
    db.commit()



   def define_relations(db):
    cursor = db.cursor()
    
    cursor.execute('''CREATE TABLE IF NOT EXISTS Participa (
                        participante_id INTEGER,
                        evento_id INTEGER,
                        FOREIGN KEY(participante_id) REFERENCES Participante(id),
                        FOREIGN KEY(evento_id) REFERENCES Evento(id))''')
    
    cursor.execute('''CREATE TABLE IF NOT EXISTS CompiteEn (
                        participante_id INTEGER,
                        disciplina_id INTEGER,
                        FOREIGN KEY(participante_id) REFERENCES Participante(id),
                        FOREIGN KEY(disciplina_id) REFERENCES Disciplina(id))''')
    
    cursor.execute('''CREATE TABLE IF NOT EXISTS Incluye (
                        evento_id INTEGER,
                        disciplina_id INTEGER,
                        FOREIGN KEY(evento_id) REFERENCES Evento(id),
                        FOREIGN KEY(disciplina_id) REFERENCES Disciplina(id))''')
    
    cursor.execute('''CREATE TABLE IF NOT EXISTS Organiza (
                        evento_id INTEGER,
                        encuentro_id INTEGER,
                        FOREIGN KEY(evento_id) REFERENCES Evento(id),
                        FOREIGN KEY(encuentro_id) REFERENCES Encuentro(id))''')
    
    db.commit()

def validate_data(data):
    # Funciones de validación de datos
    pass
 
        ```

