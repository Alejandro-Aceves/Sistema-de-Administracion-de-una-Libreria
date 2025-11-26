## Diseno en DB Designer

<img width="1157" height="745" alt="image" src="https://github.com/user-attachments/assets/9d22a133-afe4-41c9-a476-2e843db22f53" />

## models.py

```python
from django.db import models


class Autor(models.Model):
    id_autor = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    nacionalidad = models.CharField(max_length=50)
    fecha_nacimiento = models.DateField()
    biografia = models.TextField()
    email = models.CharField(max_length=100)

    def __str__(self):
        return f"{self.nombre} {self.apellido}"


class Editorial(models.Model):
    id_editorial = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=100)
    direccion = models.CharField(max_length=255)
    telefono = models.CharField(max_length=20)
    email = models.CharField(max_length=100)
    pais = models.CharField(max_length=50)
    sitio_web = models.CharField(max_length=255)

    def __str__(self):
        return self.nombre


class Cliente(models.Model):
    id_cliente = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    direccion = models.CharField(max_length=255)
    telefono = models.CharField(max_length=20)
    email = models.CharField(max_length=100)
    fecha_registro = models.DateField()
    dni = models.CharField(max_length=20)

    def __str__(self):
        return f"{self.nombre} {self.apellido}"


class Empleado(models.Model):
    id_empleado = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    dni = models.CharField(max_length=20)
    fecha_contratacion = models.DateField()
    cargo = models.CharField(max_length=50)
    salario = models.DecimalField(max_digits=10, decimal_places=2)
    telefono = models.CharField(max_length=20)

    def __str__(self):
        return f"{self.nombre} {self.apellido}"


class Libro(models.Model):
    id_libro = models.AutoField(primary_key=True)
    titulo = models.CharField(max_length=255)
    isbn = models.CharField(max_length=13)
    fecha_publicacion = models.DateField()
    num_paginas = models.IntegerField()
    id_autor = models.ForeignKey(Autor, on_delete=models.CASCADE)
    id_editorial = models.ForeignKey(Editorial, on_delete=models.CASCADE)
    precio = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.IntegerField()

    def __str__(self):
        return self.titulo


class Venta(models.Model):
    id_venta = models.AutoField(primary_key=True)
    fecha_venta = models.DateTimeField()
    id_cliente = models.ForeignKey(Cliente, on_delete=models.CASCADE)
    id_empleado = models.ForeignKey(Empleado, on_delete=models.CASCADE)
    total_venta = models.DecimalField(max_digits=10, decimal_places=2)
    metodo_pago = models.CharField(max_length=50)
    descuento_aplicado = models.DecimalField(max_digits=5, decimal_places=2)

    def __str__(self):
        return f"Venta {self.id_venta}"


class Detalle_Venta(models.Model):
    id_detalle = models.AutoField(primary_key=True)
    id_venta = models.ForeignKey(Venta, on_delete=models.CASCADE)
    id_libro = models.ForeignKey(Libro, on_delete=models.CASCADE)
    cantidad = models.IntegerField()
    precio_unitario = models.DecimalField(max_digits=10, decimal_places=2)
    subtotal = models.DecimalField(max_digits=10, decimal_places=2)
    iva_aplicado = models.DecimalField(max_digits=5, decimal_places=2)

    def __str__(self):
        return f"Detalle {self.id_detalle} de Venta {self.id_venta.id_venta}"

```
