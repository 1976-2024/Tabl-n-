# Tabl-n-from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///database.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
db = SQLAlchemy(app)

from routes import productos, ventas, reportes

app.register_blueprint(productos.bp, url_prefix='/productos')
app.register_blueprint(ventas.bp, url_prefix='/ventas')
app.register_blueprint(reportes.bp, url_prefix='/reportes')

if __name__ == '__main__':
    app.run(debug=True)
from app import db

class Producto(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    nombre = db.Column(db.String(100), nullable=False)
    precio = db.Column(db.Float, nullable=False)
    stock = db.Column(db.Integer, nullable=False)

class Venta(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    producto_id = db.Column(db.Integer, db.ForeignKey('producto.id'), nullable=False)
    cantidad = db.Column(db.Integer, nullable=False)
    total = db.Column(db.Float, nullable=False)
