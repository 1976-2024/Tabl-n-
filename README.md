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
