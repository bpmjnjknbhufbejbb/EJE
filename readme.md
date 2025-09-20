from PyQt5.QtWidgets import QApplication, QWidget, QLabel, QLineEdit, QPushButton, QVBoxLayout, QHBoxLayout, QComboBox, QTableWidget, QTableWidgetItem

class MiBilletera(QWidget):
    def __init__(self):
      super().__init__()
      self.setWindowTitle("Mi Billetera")
      self.movimientos = []
      self.initUI()

    def initUI(self):
        # Creamos los widgets
        self.monto_input = QLineEdit()
        self.tipo_combo = QComboBox()
        self.tipo_combo.addItems(["Ingreso", "Gasto"])
        self.descripcion_input = QLineEdit()
        self.agregar_btn = QPushButton("Agregar")
        self.tabla = QTableWidget()
        self.tabla.setColumnCount(3)
        self.tabla.setHorizontalHeaderLabels(["Monto", "Tipo", "Descripción"])

        # Conectamos el botón
        self.agregar_btn.clicked.connect(self.agregar_movimiento)

        # Layout
        layout = QVBoxLayout()
        layout.addWidget(QLabel("Monto:"))
        layout.addWidget(self.monto_input)
        layout.addWidget(QLabel("Tipo:"))
        layout.addWidget(self.tipo_combo)
        layout.addWidget(QLabel("Descripción:"))
        layout.addWidget(self.descripcion_input)
        layout.addWidget(self.agregar_btn)
        layout.addWidget(self.tabla)

        self.setLayout(layout)

    def agregar_movimiento(self):
        monto = self.monto_input.text()
        tipo = self.tipo_combo.currentText()
        descripcion = self.descripcion_input.text()
        self.movimientos.append((monto, tipo, descripcion))
        self.actualizar_tabla()

    def actualizar_tabla(self):
        self.tabla.setRowCount(len(self.movimientos))
        for i, (monto, tipo, descripcion) in enumerate(self.movimientos):
            self.tabla.setItem(i, 0, QTableWidgetItem(monto))
            self.tabla.setItem(i, 1, QTableWidgetItem(tipo))
            self.tabla.setItem(i, 2, QTableWidgetItem(descripcion))

app = QApplication([])
ventana = MiBilletera()
ventana.show()
app.exec_()

#hemos realizado una problematica basada para organizar nuestros gastos e ingresos,
#con una interfaz grafica sencilla y facil de usar, donde podemos agregar los movimientos los gastos y 
#ingresos y verlos en una tabla organizada. donde se le coloca su monto, tipo y descripcion. Para llevar 
#un mejor control de nuestros gastos e ingresos.

#Alondra Aminta Andrade Escobar SMSS069624
#Jairo Antonio Vasquez Marinez SMSS026624
