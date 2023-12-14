# Olimpiadas
**Especificaciones:** Surge la problemática de optimizar el uso de espacios en los complejos polideportivos. Dada la subdivisión de complejos deportivos en aquellos destinados a un único deporte y los polideportivos, es esencial garantizar una distribución eficiente de las áreas designadas para cada deporte en los complejos polideportivos.

La pregunta clave es, cómo maximizar la utilización de los espacios disponibles en los complejos polideportivos, considerando las diferentes áreas destinadas a distintos deportes con indicadores de localización específicos. La optimización deberá tener en cuenta la variedad de deportes que se celebran en un mismo complejo polideportivo, garantizando la eficacia en la organización de eventos y minimizando posibles conflictos de programación.

Además, la gestión de eventos en cada complejo añade complejidad al escenario. ¿Cómo asegurar que los eventos programados en una sede no entren en conflicto con la disponibilidad de áreas específicas en los complejos polideportivos? Esto implica coordinar fechas, duraciones, participantes y comisarios de manera eficiente, evitando superposiciones y garantizando un flujo adecuado de las actividades deportivas.

La necesidad de mantener una lista actualizada de comisarios y su participación en eventos plantea otra dimensión de la problemática. ¿Cómo gestionar eficazmente la asignación de comisarios a eventos específicos, considerando sus roles como jueces u observadores, para asegurar una cobertura adecuada en cada competición?

Finalmente, la gestión del equipamiento necesario para eventos y mantenimiento también representa un desafío. ¿Cómo garantizar que cada evento cuente con el equipamiento requerido y que se realice un mantenimiento efectivo de las instalaciones sin afectar la realización de competiciones?

La problemática central radica en la optimización integral de los recursos y espacios en las sedes olímpicas, particularmente en los complejos polideportivos, para lograr una gestión eficiente y exitosa de los eventos deportivos.

1. **Complejos Deportivos:**
    - Los complejos deportivos están especializados en un único deporte.
    - Cada complejo deportivo tiene una localización específica, un jefe de organización individual y un área total ocupada.
2. **Complejos Polideportivos:**
    - Los complejos polideportivos albergan múltiples deportes, con áreas designadas para cada uno y un indicador de localización.
    - Al igual que los complejos deportivos, los polideportivos tienen una localización, un jefe de organización individual y un área total ocupada.
3. **Información Específica para Cada Tipo de Sede:**
    - Se mantiene información específica para cada tipo de sede, como el número de complejos y su presupuesto aproximado.
4. **Eventos en los Complejos:**
    - Cada complejo, ya sea deportivo o polideportivo, celebra eventos.
    - Para cada evento se registra información detallada, incluyendo fecha, duración, número de participantes y número de comisarios.
5. **Comisarios y su Involucramiento en Eventos:**
    - Se mantiene una lista de todos los comisarios, identificando si desempeñan el papel de juez u observador en cada evento.
    - La relación entre comisarios y eventos se registra para rastrear su participación específica.
6. **Equipamiento Necesario:**
    - Tanto para eventos como para el mantenimiento de los complejos, se requiere cierto equipamiento específico, como arcos, pértigas, barras paralelas, etc.

![image](https://github.com/Sgonzalez04/Olimpiadas/assets/141069199/957e2109-c163-4785-acd8-06c3f9477108)

# Identificacion de entidades y atributos

-- Active: 1700613091773@@127.0.0.1@3306@olimpiadas
-- Tabla ComplejosDeportivos
CREATE TABLE ComplejosDeportivos (
    ComplejoID INT PRIMARY KEY,
    Nombre VARCHAR(100),
    Localizacion VARCHAR(100),
    JefeOrganizacion VARCHAR(100),
    AreaOcupada DECIMAL(10, 2)
);
 
-- Tabla ComplejosPolideportivos
CREATE TABLE ComplejosPolideportivos (
    PolideportivoID INT PRIMARY KEY,
    Nombre VARCHAR(100),
    Localizacion VARCHAR(100),
    JefeOrganizacion VARCHAR(100),
    AreaOcupada DECIMAL(10, 2)
);

-- Tabla Deportes
CREATE TABLE Deportes (
    DeporteID INT PRIMARY KEY,
    NombreDeporte VARCHAR(100)
);

-- Tabla AreasPolideportivo
CREATE TABLE AreasPolideportivo (
    AreaID INT PRIMARY KEY,
    PolideportivoID INT,
    DeporteID INT,
    IndicadorLocalizacion VARCHAR(100),
    FOREIGN KEY (PolideportivoID) REFERENCES ComplejosPolideportivos(PolideportivoID),
    FOREIGN KEY (DeporteID) REFERENCES Deportes(DeporteID)
);

-- Tabla Eventos
CREATE TABLE Eventos (
    EventoID INT PRIMARY KEY,
    ComplejoID INT,
    PolideportivoID INT,
    Fecha DATE,
    Duracion TIME,
    NumParticipantes INT,
    FOREIGN KEY (ComplejoID) REFERENCES ComplejosDeportivos(ComplejoID),
    FOREIGN KEY (PolideportivoID) REFERENCES ComplejosPolideportivos(PolideportivoID)
);

-- Tabla Comisarios
CREATE TABLE Comisarios (
    ComisarioID INT PRIMARY KEY,
    Nombre VARCHAR(100),
    Rol VARCHAR(50)
);

-- Tabla ComisariosEventos
CREATE TABLE ComisariosEventos (
    ComisarioID INT,
    EventoID INT,
    FOREIGN KEY (ComisarioID) REFERENCES Comisarios(ComisarioID),
    FOREIGN KEY (EventoID) REFERENCES Eventos(EventoID),
    PRIMARY KEY (ComisarioID, EventoID)
);

-- Tabla Equipamiento
CREATE TABLE Equipamiento (
    EquipamientoID INT PRIMARY KEY,
    NombreEquipamiento VARCHAR(100),
    CantidadDisponible INT,
    EventoID INT,
    FOREIGN KEY (EventoID) REFERENCES Eventos(EventoID)
);

**Insertx**
-- Active: 1700613091773@@127.0.0.1@3306@olimpiadas
-- Datos para ComplejosDeportivos
INSERT INTO ComplejosDeportivos (ComplejoID, Nombre, Localizacion, JefeOrganizacion, AreaOcupada)
VALUES (1, 'Complejo Deportivo A', 'Ciudad A', 'Jefe A', 1500.00),
       (2, 'Complejo Deportivo B', 'Ciudad B', 'Jefe B', 2000.00);

-- Datos para ComplejosPolideportivos
INSERT INTO ComplejosPolideportivos (PolideportivoID, Nombre, Localizacion, JefeOrganizacion, AreaOcupada)
VALUES (1, 'Polideportivo A', 'Ciudad C', 'Jefe C', 3000.00),
       (2, 'Polideportivo B', 'Ciudad D', 'Jefe D', 2500.00),
       (3, 'Polideportivo C', 'Ciudad E', 'Jefe E', 1800.00);


-- Datos para Deportes
INSERT INTO Deportes (DeporteID, NombreDeporte)
VALUES (1, 'Fútbol'),
       (2, 'Baloncesto'),
       (3, 'Natación');

-- Datos para AreasPolideportivo
INSERT INTO AreasPolideportivo (AreaID, PolideportivoID, DeporteID, IndicadorLocalizacion)
VALUES (1, 1, 1, 'Área de Fútbol en Polideportivo A'),
       (2, 1, 2, 'Área de Baloncesto en Polideportivo A'),
       (3, 2, 3, 'Piscina en Polideportivo B');

-- Datos para Eventos
INSERT INTO Eventos (EventoID, ComplejoID, PolideportivoID, Fecha, Duracion, NumParticipantes)
VALUES (1, 1, 1, '2023-12-15', '12:00:00', 100),
       (2, 2, 2, '2023-12-16', '09:30:00', 50);

-- Datos para Comisarios
INSERT INTO Comisarios (ComisarioID, Nombre, Rol)
VALUES (1, 'Juan Pérez', 'Juez'),
       (2, 'María García', 'Observador'),
       (3, 'Pedro Rodríguez', 'Juez');

-- Datos para Equipamiento
INSERT INTO Equipamiento (EquipamientoID, NombreEquipamiento, CantidadDisponible, EventoID)
VALUES (1, 'Balones de Fútbol', 20, 1),
       (2, 'Balones de Baloncesto', 15, 2);

-- Datos para ComisariosEventos
INSERT INTO ComisariosEventos (ComisarioID, EventoID)
VALUES (1, 1),
       (2, 2),
       (3, 1),
       (3, 2);


# Imagen "Modelo Fisico"

![image](https://github.com/Sgonzalez04/Olimpiadas/assets/141069199/957e2109-c163-4785-acd8-06c3f9477108)




# Consultas


1. Consulta de Todos los Eventos en un Complejo Deportivo Específico:

    ```sql
    SELECT *
    FROM Eventos
    WHERE ComplejoID = 1; -- Cambia el ID del complejo deportivo según sea necesario
    ```

2. Consulta de Comisarios Asignados a un Evento en Particular

    ```sql
    SELECT Comisarios.*
    FROM Comisarios
    INNER JOIN ComisariosEventos ON Comisarios.ComisarioID = ComisariosEventos.ComisarioID
    WHERE ComisariosEventos.EventoID = 1; -- Cambia
    ```

3. Consulta de Todos los Eventos en un Rango de Fechas

    ```sql
    SELECT *
    FROM Eventos
    WHERE Fecha BETWEEN '2023-12-15' AND '2023-12-18'; -- Cambia
    ```

4. Consulta del Número Total de Comisarios Asignados a Eventos

    ```sql
    SELECT COUNT(*) AS TotalComisarios
    FROM ComisariosEventos;
    ```

5. Consulta de Complejos Polideportivos con Área Total Ocupada Superior a un Valor Específico

    ```sql
    SELECT *
    FROM ComplejosPolideportivos
    WHERE AreaOcupada > 2500; -- Cambia
    ```

6. Consulta de Eventos con Número de Participantes Mayor que la Media

    ```sql
    SELECT *
    FROM Eventos
    WHERE NumParticipantes > (SELECT AVG(NumParticipantes) FROM Eventos);
    ```

7. Consulta de Equipamiento Necesario para un Evento Específico

    ```sql
    SELECT Equipamiento.*
    FROM Equipamiento
    WHERE EventoID = 1; -- Cambia
    ```

8. Consulta de Eventos Celebrados en Complejos Deportivos con Jefe de Organización Específico

    ```sql
    SELECT Eventos.*
    FROM Eventos
    INNER JOIN ComplejosDeportivos ON Eventos.ComplejoID = ComplejosDeportivos.ComplejoID
    WHERE ComplejosDeportivos.JefeOrganizacion = 'Jefe A'; -- Cambia
    ```

9. Consulta de Complejos Polideportivos sin Eventos Celebrados

    ```sql
    SELECT ComplejosPolideportivos.*
    FROM ComplejosPolideportivos
    LEFT JOIN Eventos ON ComplejosPolideportivos.PolideportivoID = Eventos.PolideportivoID
    WHERE Eventos.PolideportivoID IS NULL;
    ```

10. Consulta de Comisarios que Actúan como Jueces en Todos los Eventos

     ```sql
    SELECT c.ComisarioID, c.Nombre
    FROM Comisarios c
    JOIN ComisariosEventos ce ON c.ComisarioID = ce.ComisarioID
    GROUP BY c.ComisarioID
    HAVING COUNT(DISTINCT ce.EventoID) = (
        SELECT COUNT(*)
        FROM Eventos
    );
     ```
