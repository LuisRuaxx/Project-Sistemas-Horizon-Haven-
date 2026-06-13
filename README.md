# Project-Sistemas-Horizon-Haven-
Proyecto de Sistemas


# Comenzamos la sintaxis para crear la base de datos:

[Tren.txt](https://github.com/user-attachments/files/28917084/Tren.txt)
-- Crear base de datos
CREATE DATABASE IF NOT EXISTS horizon_haven;
USE horizon_haven;

-- =========================
-- TABLA USUARIOS
-- =========================
CREATE TABLE usuarios (
    id_user INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    correo VARCHAR(150) NOT NULL UNIQUE,
    contrasena VARCHAR(255) NOT NULL
);

-- =========================
-- TABLA VIVIENDAS
-- =========================
CREATE TABLE viviendas (
    id_vivienda INT AUTO_INCREMENT PRIMARY KEY,
    tipo_vivienda ENUM(
        'Apartamento',
        'Casa',
        'Loft',
        'Penthouse',
        'Duplex',
        'Finca',
        'Estudio'
    ) NOT NULL,
    precio DECIMAL(12,2) NOT NULL,
    tamano DECIMAL(10,2) NOT NULL,
    estado ENUM(
        'Excelente',
        'Buena',
        'Media',
        'Mala',
        'Deteriorada'
    ) NOT NULL
);

-- =========================
-- TABLA CITAS
-- =========================
CREATE TABLE citas (
    id_cita INT AUTO_INCREMENT PRIMARY KEY,
    id_vivienda INT NOT NULL,
    id_user INT NOT NULL,
    fecha DATE NOT NULL,
    hora TIME NOT NULL,

    CONSTRAINT fk_citas_vivienda
        FOREIGN KEY (id_vivienda)
        REFERENCES viviendas(id_vivienda)
        ON DELETE CASCADE
        ON UPDATE CASCADE,

    CONSTRAINT fk_citas_usuario
        FOREIGN KEY (id_user)
        REFERENCES usuarios(id_user)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
